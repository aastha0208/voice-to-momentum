# Setup

## 1. Start locally

Install Node.js 20+ from https://nodejs.org/ if necessary. Extract this package and open a terminal in the `voice-to-momentum` folder.

```bash
node --version
node scripts/local-server.mjs
```

Open http://localhost:3000. Stop with Ctrl+C. A different port is supported:

```bash
node scripts/local-server.mjs --port 3001
```

No `npm install` is required. `npm run dev` is equivalent to the default start command.

## 2. Try the free demo

Select a synthetic example and click Analyze conversation. All demo results initially require review. Correct a category, restore it, approve a route, reopen review, export CSV, and clear the conversation.

## 3. Enable live Jev

1. Open https://console.typesafe.ai and obtain a TypeSafe API key.
2. Check the account's current credit balance and billing terms. Live usage may cost money.
3. In the app select **Live · Jev API**.
4. Enter the key in the session-only password field. Do not place it in source, screenshots, issues, or commits.
5. Choose a model. Default is `jev-latest`; use an available versioned ID for repeatable validation.
6. Paste synthetic excerpts separated by blank lines and click Analyze conversation.
7. Confirm the result header says **Live Jev** and shows a model version. Export original outputs before editing.

The UI does not read `.env` files; the key is entered in the app. No environment setup is needed. A failed live request is not a completed analysis; previous results can remain visible with an error message.

## 4. Customize

- Categories and destinations: rename, add, or remove pairs. The live request includes an Unclear fallback.
- Areas: one per line, at least two. Keep an `Other / unclear` option.
- Save preferences stores settings in this browser only.
- Reanalyze after changing categories or areas. Changing route labels or thresholds does not reclassify text.
- The impact rubric is fixed in this version.

## Troubleshooting

| Symptom | Action |
| --- | --- |
| Threshold disabled | Expected in Demo mode; there is no model confidence |
| Threshold changes but route does not | Check follow-up, unclear category, and human approval |
| Other / unclear in Demo | Keyword rules do not understand synonyms or context |
| API key rejected | Check the key, organization, and account access |
| Provider request fails | Check credits, selected model, provider status and request limits |
| Missing credit / HTTP 402 | The current UI may show a generic provider error; inspect your TypeSafe balance |
| Port in use | Stop the other process or use `--port 3001` |
| Refresh loses results | Expected; conversations and results are not persisted |

## Prepare a GitHub repository

This export intentionally excludes the hosted site's identity, deployment artifacts, source-access credentials and Git history. It is a standalone starter, not a GitHub repository already created for you.

1. Create an empty GitHub repository named `voice-to-momentum` (or your preferred name).
2. From this extracted folder:

```bash
git init
git add .
git commit -m "Initial Voice To Momentum prototype"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/voice-to-momentum.git
git push -u origin main
```

Replace `YOUR-USERNAME`. Review staged files before committing. Use your normal GitHub authentication; never put a token in the remote URL. Choose repository visibility deliberately and select a license if you want to permit reuse.
