# BuildReflect AI: deployment

A static React + TypeScript + Tailwind page (`index.html`) plus one serverless function (`api/feedback.js`).
The AI key lives only on the server. The browser never sees it.

## Deploy on Vercel (free)
1. Put these files in a GitHub repo (or run `npx vercel` in this folder).
2. In Vercel, import the repo. No build settings are needed.
3. Add environment variable `ANTHROPIC_API_KEY` (Project Settings, Environment Variables).
   Optional: `ANTHROPIC_MODEL` (default `claude-sonnet-5-5`).
4. Redeploy. The yellow "Demo mode" banner turns into a green "AI mode" banner.

Without the key the app still works in clearly labelled demo mode (rule-based, not AI).

## Notes
- `index.html` sets `window.BUILDREFLECT_API = "/api/feedback"`. Netlify users: move the function to `netlify/functions` and change that path.
- The function trims input lengths and only forwards the form fields. Add rate limiting (for example Vercel Firewall) before sharing it widely.
- Source: `app.source.tsx` is the readable TypeScript. `index.html` contains it precompiled.
- Tailwind loads from its CDN (fine for a prototype). For production, build Tailwind into a stylesheet.
- Student text is sent to an AI provider. Check your school or organisation's data policy first.
