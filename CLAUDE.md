# GuideNord website (`kallistesoft/guidenord-site`, local folder guidehunter-site)

Promo site of the GuideNord app (Android + iPhone), FR at `/`, EN at `/en/`: species, provinces, tips, FAQ, and the
app's privacy policy and account-deletion pages (the URLs given to Google Play). Live at https://guidenordapp.com
(guidenordapp.ca 301s to it through a hand-written `.htaccess` on the hosting, not in git).

## Stack, build, check, deploy
- Plain Node 22, no dependencies. `node tools/build.mjs` writes `site/` (not committed, also writes `app-ads.txt`).
- Check: `tools/check.sh` (= build + `node tools/check.mjs`: dead links, titles, descriptions, hreflang, JSON-LD).
  The global pre-push hook runs it, and CI runs the same on every PR.
- Preview: `cd site && python3 -m http.server 8765` (127.0.0.1).
- Deploy: every push to `main` uploads `site/` to GoDaddy through the shared FTPS workflow. PRs only build and check.
- Share images: `npm i --no-save puppeteer-core && node tools/images.mjs`, commit the PNGs.

## Rules (owner)
- The app's name lives only in `tools/config.mjs`; write `{app}` in content. `playUrl` null = "coming soon".
- Content follows `data/BRIEF.md`: no invented facts, Québec French. The app covers ALL of Canada: never scope copy
  to Québec. The legal notice is a draft not reviewed by a lawyer; `checked` dates only when actually verified.
- Screenshots use test data only: never a real person's name, email or location.
- The owner wants to see new pages (local preview) before they deploy.
- Keep the Search Console TXT and Bing CNAME records at GoDaddy.

## Branches and PRs
- Feature branch → push → PR against `main` (never stacked). The owner merges; never `gh pr merge`, never `--admin`.

## Autonomy, to-dos, decisions
- Fixes on a branch freely; new pages and copy wait for the owner's look.
- To-dos: the app repo's `FOLLOW-UP.md` (guidenord-android). Non-blocking choices: `DECISIONS.md`, with the default taken.
