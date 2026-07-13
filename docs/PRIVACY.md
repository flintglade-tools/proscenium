# Privacy notice

Effective date: July 13, 2026.

Proscenium is published under the Flintglade identity. Questions may be sent to [support@flintglade.com](mailto:support@flintglade.com).

## Local product data

Captured events, endpoint definitions, scenarios, and evidence remain on the user's machine unless the user deliberately sends or exports them. Proscenium has no analytics SDK, advertising SDK, hosted payload inbox, or background telemetry in version 0.1.

Sensitive request headers are redacted automatically. Users can configure JSON-pointer body redaction. If configured JSON redaction cannot safely parse a body, Proscenium stores a fixed omission marker instead of the original body. Because Proscenium cannot infer every sensitive field, synthetic data is recommended.

## Licensing and payment data

License activation sends the product identifier and entered license key to `licenses.flintglade.com`. Normal service metadata such as IP address, time, and user agent may be processed for security, delivery, and rate limiting. The client caches the license key and a short-lived signed entitlement lease in `%LOCALAPPDATA%\Flintglade\Proscenium\data\license.json` on Windows, unless `--data-dir` selects another location. The lease contains a purchase identifier and a one-way hash binding it to the key; it contains no email or customer name.

Stripe processes checkout and payment information under its own privacy terms. Flintglade's licensing service receives purchase identifiers, product metadata, payment status, refund/dispute status, and the purchaser email needed to deliver or recover a license. Proscenium does not receive full card data.

## Retention and requests

Local data remains until the user deletes the application data or removes endpoints/events. Exact controls and paths are documented in [DATA-REMOVAL.md](DATA-REMOVAL.md). Payment and licensing records are retained as necessary for delivery, fraud prevention, accounting, disputes, and legal obligations. Requests concerning accessible Flintglade records may be sent to the support address. Identity verification may be required before fulfilling a request.
