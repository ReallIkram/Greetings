# Noor Academy

Responsive Quran academy web prototype. This is a browser-based JavaScript application, not a Flutter project or a production school system.

## Run

From this directory run `python3 -m http.server 8000 --bind 127.0.0.1 --directory public` and open `http://127.0.0.1:8000/`. No dependency installation is required to serve the included files. Source files are at the repository root; after edits run `npm run build` to refresh `public/`. This build uses only Node.js built-in modules.

## Try the demo

Switch the role dropdown to Teacher or Admin to schedule classes, save feedback, or add resource links. Use Student to join a practice session; leave it to save attendance and elapsed time. Parent shows the same demo student's reports. Admin can add directory entries. Changes persist in localStorage on the same browser. Reset demo clears them.

The Quran reader fetches Arabic text and per-verse audio from `api.alquran.cloud`. Audio streams from the API's returned CDN URLs. If unavailable, a Quran.com fallback link is shown. Live meeting opens an external public Jitsi room; moderator authentication or service restrictions may apply. Attendance measures the local timer, not provider-confirmed call participation. Do not use real student information.

## Deployment

The failed runs reported `Get Pages site failed` and `HttpError: Not Found` in `actions/configure-pages`. The repository did not have an accessible Pages site configured. Re-running the old workflow alone will not resolve that prerequisite.

1. Push these changes to `main`.
2. As a repository administrator, open [Settings → Pages](https://github.com/ReallIkram/Greetings/settings/pages). Under **Build and deployment → Source**, select **GitHub Actions**. This enables the Pages site; no personal access token needs to be added to the code or workflow.
3. Open [Deploy Noor Academy](https://github.com/ReallIkram/Greetings/actions/workflows/pages.yml), choose **Run workflow**, select `main`, and run it. Approve the `github-pages` environment if repository protection rules request it.
4. Wait for both `build` and `deploy` to succeed. Use the URL shown by the successful `github-pages` deployment.

Expected URL after successful deployment: **https://reallikram.github.io/Greetings/**. This is an expected address, not confirmation that the site is live. Keep the uppercase `Greetings` path.

The workflow installs locked test dependencies, builds `public/`, and tests it under `/Greetings/` before uploading only that directory. Only pushes to `main` deploy automatically; other branches can be checked locally. The build uses current Node.js 24 actions and a pinned Ubuntu runner version.

For another static hosting provider, upload the contents of `public/`, with `index.html` at the publish root. No server, environment variables, or SPA rewrite rules are needed. Third-party Quran and video services still require internet access.

## Production work remaining

This demo does not provide secure authentication, server-enforced roles, child-parent access isolation, shared database records, uploads, push/email delivery, verified call tracking, or Android/iOS builds. These require a separate implementation and configured services. Role preview is not authorization. Directory entries are not user accounts.

For the requested Flutter/Firebase implementation, create a Firebase project with web/Android/iOS app registrations, Auth, Firestore and Storage. Enforce tenant and parent-child permissions in server-side security rules; create user roles through privileged server code. Add provider-verified call events, Cloud Functions for feedback notifications, FCM consent/token registration, and SendGrid credentials stored only in backend secrets. Never place privileged credentials in GitHub Pages assets. Jitsi may serve the call proof of concept; test moderation and privacy before real classes. Deploy and test rules and multi-user access controls before entering personal data.

## Validation

Run `npm ci`, `npm run build`, and `npm test` while the local HTTP server above is running. The test uses `/usr/bin/chromium`; override with `CHROMIUM_PATH` when needed. Alternatively, run `npx playwright install chromium` and set `PLAYWRIGHT_BUNDLED_CHROMIUM=1` for the test. Set `TEST_BASE_URL` to test a served project path. It exercises scheduling, teacher-to-parent feedback, timed attendance, persisted records, mobile overflow, and Quran response rendering using a mocked API response. Live Quran API connectivity and live video calls are separate manual checks.
