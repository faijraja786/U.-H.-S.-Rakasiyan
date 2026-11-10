# EduFuture Cloud (Firebase backend)

## Features
Google/email login, persistent login across refresh, email password reset, student planner/aim/daily targets, tasks, flashcards, timed quizzes, PYQ/notes file upload, dynamic quiz builder, server-side scoring, answer key hidden from students, result/rank locked for 48 hours, superadmin-controlled admin addition.

## Setup
1. Create project at https://console.firebase.google.com/
2. Enable Authentication: Email/Password and Google.
3. Create Firestore and Storage.
4. Put Firebase Web App config into `public/firebase-config.js`.
5. Install Node.js and Firebase CLI: `npm i -g firebase-tools`, then `firebase login`.
6. Copy `.firebaserc.example` to `.firebaserc` and set your project ID.
7. On first deploy, Firebase CLI will prompt for the `BOOTSTRAP_ADMIN_EMAIL` parameter. Enter the exact email that will become the first superadmin. Never put service-account keys in public files.
8. Deploy with `firebase deploy`.
9. First admin signs up using that exact email, opens the Home page and clicks **Initialize first admin** once. Afterwards that superadmin can add admins. Each new admin must sign in once first.
10. Add Hosting domain in Firebase Auth authorized domains.

## Important
- Students never receive answer keys; scoring happens in Cloud Functions.
- Result/rank releases at least 48 hours after an attempt is submitted.
- Admin password change uses Firebase password-reset email to the admin's registered email.
- Notes/PYQ files go to Firebase Storage; max 30 MB according to rules.
- Firestore/Storage/Functions may require a billing-enabled Firebase plan. Add App Check, rate limiting and test rules in Emulator before production.
- This is a deployable starter, not a security audit. Firebase config is public by design; service-account keys must remain secret.
