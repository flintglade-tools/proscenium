# Install and launch

Proscenium 0.1.0 supports Windows x64.

1. Download the ZIP and matching `.sha256` file from the official GitHub release.
2. Verify the ZIP hash:

   ```powershell
   Get-FileHash .\proscenium-0.1.0-windows-x64.zip -Algorithm SHA256
   ```

3. Compare the lowercase result with the first value in the `.sha256` file.
4. Extract the ZIP to a folder you control. Do not run the executable from inside the ZIP.
5. Start `proscenium.exe`. It binds only to a random `127.0.0.1` port and opens the local interface in your browser.

This release is not Authenticode-signed, so Windows may show an unknown-publisher warning. Verify the release hash before choosing to run it. Flintglade never asks you to disable antivirus or browser protections.

For command-line help:

```powershell
.\proscenium.exe --help
```

See [DATA-REMOVAL.md](DATA-REMOVAL.md) for the exact local data location and removal steps.
