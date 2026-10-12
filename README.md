# TheRuinForge — AI-powered Roblox Luau Forge

TheRuinForge is a Node.js web app for generating Roblox Luau scripts and getting coding help from Ruin AI. It includes a crimson/black responsive interface, script category library, AI generation and request explanation, an AI chat helper, Discord OAuth sign-in, and server-side Discord membership verification.

## Requirements
- Node.js 18 or newer
- A Discord application and bot in your community server
- An OpenAI API key for live AI generation (API billing/limits are separate from a ChatGPT subscription)

## Run locally
1. Copy `.env.example` to `.env` and fill in your Discord settings and a private `OPENAI_API_KEY`.
2. In Discord Developer Portal → OAuth2, add `http://localhost:3000/auth/discord/callback` as a redirect URL. Set `DISCORD_REDIRECT_URI` to that exact URL.
3. Run `npm ci` then `npm start`, and open `http://localhost:3000`.

## Deploy from GitHub to Render
1. Extract this ZIP and upload the project files to a new GitHub repository. Do not upload `.env`, API keys, Discord tokens, or `node_modules`.
2. In Render, create a Blueprint using the repository's `render.yaml` (or create a Node web service with build command `npm ci` and start command `npm start`).
3. In Render → Environment, set `DISCORD_CLIENT_ID`, `DISCORD_CLIENT_SECRET`, `DISCORD_GUILD_ID`, `DISCORD_BOT_TOKEN`, and `OPENAI_API_KEY`. The Blueprint generates `SESSION_SECRET`. Set `DISCORD_REDIRECT_URI` to `https://YOUR-SERVICE.onrender.com/auth/discord/callback`.
4. In Discord Developer Portal → OAuth2, register that exact callback URL. Save the environment variables and redeploy.
5. Add a custom domain in Render → Settings → Custom Domains and follow its DNS instructions. If using a custom domain, update `DISCORD_REDIRECT_URI` in Render and register the matching callback URL in Discord Developer Portal.

## How Ruin AI works
- `/api/ai` runs only on the server and requires a valid Discord session plus membership in the configured Discord server.
- The OpenAI API key stays in the server environment; it is never sent to the browser.
- `OPENAI_MODEL` defaults to `gpt-4.1-mini` and can be changed in Render if your account has access to another supported model.
- The API endpoint has a small per-minute rate limit. Provider usage limits and costs apply.
- Generated code is not guaranteed to be perfect. Review it and test in a private Roblox Studio place before publishing.

## Discord setup troubleshooting
- The callback URL must match exactly in Render and Discord Developer Portal, including HTTPS and path.
- `DISCORD_BOT_TOKEN` is different from `DISCORD_CLIENT_SECRET`. The bot must be in the target server; `DISCORD_GUILD_ID` must be the server ID.
- If membership checks fail, inspect Render Logs for `Discord membership verification failed`. If OAuth fails, inspect logs for `Discord OAuth callback failed`. Never paste tokens into logs or public issues.
- The app logs errors server-side but does not send secrets to the browser.

## Security notes
- Never commit `.env`, `DISCORD_CLIENT_SECRET`, `DISCORD_BOT_TOKEN`, `OPENAI_API_KEY`, or `SESSION_SECRET`. `.gitignore` excludes environment files.
- If any secret was previously committed to a public repository, rotate it before deploying.
- The app uses Express's default in-memory session store. This is fine for a small initial deployment, but for a production service with multiple instances or frequent restarts, use a persistent session store.
- This project is not affiliated with Roblox Corporation.
