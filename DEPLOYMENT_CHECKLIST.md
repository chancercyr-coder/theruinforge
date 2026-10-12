# Launch checklist

- [ ] Keep `.env` out of GitHub.
- [ ] Set the six Discord/session variables in Render.
- [ ] Set `OPENAI_API_KEY` in Render Environment Variables.
- [ ] Register the exact HTTPS `/auth/discord/callback` URL in Discord OAuth2 Redirects.
- [ ] Confirm the bot is in the correct server and has the correct token.
- [ ] Redeploy and watch Render Logs while testing Discord login.
- [ ] Sign in with a Discord account that is already a member of the server.
- [ ] Test AI generation and chat. Check Render logs if AI is unavailable.
- [ ] Test generated scripts in a private Roblox Studio place before publishing.
- [ ] Configure custom domain DNS in Render and update the OAuth redirect URI if using it.
