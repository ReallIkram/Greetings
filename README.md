# Noor Academy

Responsive Quran academy web prototype. This is a browser-based JavaScript application, not a Flutter project or a production school system.

## Run

From this directory run `python3 -m http.server 8000 --bind 127.0.0.1` and open the served page. No dependency installation or build is required. Publish the `public` directory with GitHub Pages. Source files are at the repository root; after edits run `cp index.html style.css app.js public/`.

## Try the demo

Switch the role dropdown to Teacher or Admin to schedule classes, save feedback, or add resource links. Use Student to join a practice session; leave it to save attendance and elapsed time. Parent shows the same demo student's reports. Admin can add directory entries. Changes persist in localStorage on the same browser. Reset demo clears them.

The Quran reader fetches Arabic text and per-verse audio from `api.alquran.cloud`. Audio streams from the API's returned CDN URLs. If unavailable, a Quran.com fallback link is shown. Live meeting opens an external public Jitsi room; moderator authentication or service restrictions may apply. Attendance measures the local timer, not provider-confirmed call participation. Do not use real student information.

## Deployment

The GitHub Actions workflow uploads only `public/` to GitHub Pages. In repository Settings → Pages select GitHub Actions as the source, then run Deploy Noor Academy if needed. The expected project URL is `https://reallikram.github.io/Greetings/` (case-sensitive repository path). The lowercase `/greetings/` path is not guaranteed by this repository name.

## Production work remaining

This demo does not provide secure authentication, server-enforced roles, child-parent access isolation, shared database records, uploads, push/email delivery, verified call tracking, or Android/iOS builds. These require a separate implementation and configured services. Role preview is not authorization. Directory entries are not user accounts.

For the requested Flutter/Firebase implementation, create a Firebase project with web/Android/iOS app registrations, Auth, Firestore and Storage. Enforce tenant and parent-child permissions in server-side security rules; create user roles through privileged server code. Add provider-verified call events, Cloud Functions for feedback notifications, FCM consent/token registration, and SendGrid credentials stored only in backend secrets. Never place privileged credentials in GitHub Pages assets. Jitsi may serve the call proof of concept; test moderation and privacy before real classes. Deploy and test rules and multi-user access controls before entering personal data.
