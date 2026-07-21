# 💸 Split-it

A simple, mobile-friendly web app for tracking shared expenses and splitting them with friends. Add what everyone spent, tag it with your own categories (Food, Badminton, whatever you like), and Split-it shows who owes whom and the fewest payments needed to settle up.

**Live demo:** _(GitHub Pages link will go here once Pages is enabled)_

## Features

- Add expenses with a description, amount, who paid, and who it's split between
- **Admin role with PIN** — the group creator sets a 4-digit PIN; only the admin can add/remove people and categories
- **Monthly WhatsApp reminders** — in the first week of each month a reminder banner appears, and the admin gets one-tap "Remind" buttons that open WhatsApp with each person's pending balance pre-written
- **Custom categories** — start with Food, Badminton, Transport, Groceries, Rent, Other, and add your own (with emoji)
- Automatic **balances** — see who's up and who's down at a glance
- **Suggested settle-up** — the minimum set of payments to square everyone up
- **Group codes** — share one code so friends join the same group
- **Real-time sync** across devices when Firebase is set up
- Works offline / on one device even without Firebase (local mode)
- No build step — it's a single `index.html` file

## How to use

1. Open the app.
2. Enter your name and either **create a new group** or **join** with a code a friend shared.
3. In **People & Categories**, add everyone in the group and any custom categories.
4. Tap **＋ Add expense**, fill in the details, choose a category, and pick who to split between.
5. Check the **Balances** tab to see who owes whom and how to settle up.

Share your group **code** (shown top-right and on the People & Categories tab) with friends so they see the same data.

## Enabling real-time sync (Firebase) — ~5 minutes

Out of the box the app runs in **local mode** (data is saved only in your browser). To let everyone share the same live data across phones and laptops, connect a free Firebase project:

1. Go to <https://console.firebase.google.com> and click **Add project** (any name). You can skip Google Analytics.
2. In the project, click the **Web** icon (`</>`) to "Add app". Give it a nickname and register — you don't need Hosting.
3. Firebase shows a `firebaseConfig` object. Copy it.
4. In **Build → Firestore Database**, click **Create database**, choose **Start in test mode** (fine for a friends group), and pick a location.
5. Open `index.html`, find the `window.FIREBASE_CONFIG` block near the bottom, and paste your values, e.g.:

   ```js
   window.FIREBASE_CONFIG = {
     apiKey: "AIza...",
     authDomain: "your-project.firebaseapp.com",
     projectId: "your-project",
     storageBucket: "your-project.appspot.com",
     messagingSenderId: "000000000000",
     appId: "1:0000:web:abcdef"
   };
   ```

6. Save, commit, and push. The badge in the top bar will switch from **"On this device"** to **"Live sync"**.

> These Firebase web keys are safe to commit publicly — they identify the project, not grant secret access. Test-mode Firestore rules are open, which is fine for a small trusted group. For anything larger, tighten the security rules later.

## Hosting (free) with GitHub Pages

1. Push this repo to GitHub.
2. Repo **Settings → Pages**.
3. Under "Build and deployment", set **Source: Deploy from a branch**, **Branch: `main` / `root`**, then **Save**.
4. After a minute your site is live at `https://<your-username>.github.io/<repo-name>/`.

## Tech

Plain HTML, CSS, and JavaScript. Firebase Firestore (via CDN) for optional real-time sync. No frameworks, no build tools.
