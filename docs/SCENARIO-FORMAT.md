# Scenario pack format

Scenario packs are strict JSON. Unknown fields fail parsing. The current `schema_version` is `1`.

```json
{
  "schema_version": 1,
  "name": "Payment receiver contract",
  "description": "Synthetic failure and idempotency cases.",
  "endpoints": [],
  "cases": [
    {
      "name": "accepts a signed event",
      "method": "POST",
      "path": "/webhooks",
      "headers": {"x-event-kind": "payment.succeeded"},
      "body": {"id": "evt_demo_1", "amount": 2500},
      "expected_status": 202,
      "expected_body_contains": "queued",
      "max_duration_ms": 2000,
      "delay_before_ms": 0,
      "signature": {
        "profile": "stripe_style",
        "secret_env": "PROSCENIUM_WEBHOOK_SECRET",
        "message_id": "evt_demo_1",
        "timestamp_offset_seconds": 0,
        "corrupt": false
      }
    }
  ]
}
```

Supported signature profiles are `generic_hmac_sha256`, `github_sha256`, `stripe_style`, and `standard_webhooks`. Standard Webhooks secrets must use the `whsec_` base64 form.

To test duplicates, repeat two cases with the same body and `message_id`. Case order is execution order. To test expiry, use a negative `timestamp_offset_seconds`. To test invalid signatures without storing a wrong secret, set `corrupt` to `true`. Delays are bounded to 30 seconds; signature offsets are bounded to seven days.

Static authorization, cookie, token, key, and secret headers are rejected. Use `secret_env` for signing material. The runner never writes secret values to JSON or JUnit output.

Response assertions cover status, a bounded body-preview substring, and elapsed time. The runner exits `0` when all cases pass, `1` when assertions fail, and `2` for invalid input or operational errors.
