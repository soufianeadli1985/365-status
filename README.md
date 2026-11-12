# Microsoft 365 & Azure public status dashboard

**No Microsoft login, no secrets, no paid hosting.** Public status only. It is **not** a tenant-level Microsoft 365 health monitor, and it does not test whether Outlook is reachable from your network.

## Install in your GitHub repository

1. Extract the ZIP, including the hidden `.github` folder.
2. Upload the **contents** of this folder to the root of `soufianeadli1985/365-status` (not the enclosing folder). Replace any old `index.html`.
3. On GitHub, open **Settings → Actions → General → Workflow permissions** and choose **Read and write permissions** if your repository allows it. Save.
4. Go to **Actions → Update public Microsoft status → Run workflow**. Confirm it completes successfully and commits `status.json` and `history.json`.
5. Go to **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, `main`, `/(root)` and Save.
6. Your expected public URL: `https://soufianeadli1985.github.io/365-status/`.

GitHub Actions checks every 15 minutes (best effort; schedules can be delayed). The browser reloads JSON every 60 seconds. A reading older than 60 minutes is marked **UNKNOWN**. If GitHub blocks workflow commits, inspect the Actions log and repository workflow permissions. Do not enable GitHub Pages publishing from Actions unless you also replace this branch-based deployment configuration.

## Sources and limitations

- Microsoft public status: https://status.cloud.microsoft/
- Azure broad-impact status: https://azure.status.microsoft/en-us/status
- Azure public RSS: https://rssfeed.azure.status.microsoft/en-us/status/feed/
- Microsoft public feed (if available): https://status.cloud.microsoft/api/feed/mac

Public Microsoft status **does not give per-tenant Exchange/Teams/SharePoint/OneDrive health**, so those individual rows and all regional Microsoft 365 rows remain UNKNOWN. An Azure green signal cannot be used to label Outlook green. Microsoft sometimes changes public page HTML or feed endpoints; the collector fails closed to UNKNOWN rather than inventing uptime. Feed entries are historical and never automatically counted as active. The 48-hour line graph is a history of public checks, not real network measurements.

## Local test

`python scripts/update_status.py` (requires outbound Internet), then serve the folder with `python -m http.server 8000` and open `http://localhost:8000`.

## Security

No API keys or private tenant data are needed. This is a public informational page. Keep private tenant incident details out of the public repository. The GitHub Action uses only `contents: write` to commit public snapshots.
