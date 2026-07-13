# Data removal

Proscenium stores local state in `%LOCALAPPDATA%\Flintglade\Proscenium\data` on Windows unless you launch it with `--data-dir`.

The directory can contain `state.json` and `license.json` plus temporary, backup, or lock companions. The browser launch token exists only in session storage for the open browser session.

Within the app:

- **Clear events & rewind** removes one endpoint's events, resets its hit count, and restarts its response sequence.
- **Delete endpoint & events** removes the endpoint and all events captured for it.
- **Remove local activation** deletes the cached license key and signed entitlement lease from this device.

For complete removal, close Proscenium, optionally export any evidence you want to retain, delete `%LOCALAPPDATA%\Flintglade\Proscenium\data`, and then delete the extracted program folder. If you supplied `--data-dir`, delete that directory instead.
