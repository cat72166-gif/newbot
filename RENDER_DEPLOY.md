# Deploy to Render

1. Push this project to your GitHub repository. Keep `.env` out of Git; `.gitignore` excludes local environment files and `node_modules`.
2. In Render, choose **New + → Blueprint** and connect the repository. Render reads `render.yaml`, which installs dependencies from `package-lock.json`, installs Chromium into Playwright's local `node_modules` browser directory, starts the bot with `PLAYWRIGHT_BROWSERS_PATH=0 npm start`, and checks `/health`.
3. Set `TELEGRAM_BOT_TOKEN` and `TELEGRAM_CHAT_ID` as secret environment variables in Render. Optional stats-bot variables are `TRANSFERMARKT_BOT_TOKEN` and `TRANSFERMARKT_CHAT_ID`. `PLAYWRIGHT_BROWSERS_PATH=0` is configured by the Blueprint for both browser installation and runtime.
4. Deploy. For an existing service after changing the build command, choose **Manual Deploy → Clear build cache & Deploy**. Check **Logs** for `Starting browser` and repeated scan messages.
5. Confirm `/health` responds successfully and `/api/state` returns JSON whose `lastSuccessfulCheckAt` updates after each scan. Open the service URL for the dashboard. Send `/start` to your Telegram bot first.

The project checks the AR BET page; external site changes, bot token errors, browser blocks/CAPTCHAs, or outages can still interrupt it. Never commit or upload `.env`.
