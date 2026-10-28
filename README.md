# Baylor Tennis Stringing

A shared stringing log and string inventory for the Baylor tennis team. It's one static page hosted on GitHub Pages, with the data kept in Firebase Firestore.

- **Log a session:** tap the players you strung, set how many racquets each, and hit Log. Each player's saved string and tension are used.
- **Inventory:** strings are tracked in reels and sets. The estimate counts down as jobs are logged. A count or restock resets it.
- **Sign-in:** just a name, remembered on each device. Anyone with the link can view and log.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole site (markup, styles, and app code) |
| `firebase-config.js` | Your Firebase project's web settings (not secret) |
| `firestore.rules` | Database rules: open read/write, limited to the site's three collections with basic checks |

## One-time setup

1. **Firebase project:** go to [console.firebase.google.com](https://console.firebase.google.com), choose **Create a project** (Google Analytics can stay off).
2. **Database:** open **Build → Firestore Database → Create database**. Pick a US location and start in **production mode**.
3. **Rules:** on the Firestore **Rules** tab, replace everything with the contents of `firestore.rules`, then click **Publish**.
4. **Web settings:** go to **Project settings** (gear icon) → **Your apps** → the web icon `</>`. Name it anything and skip Hosting. Copy the `firebaseConfig` values into `firebase-config.js`.
5. **GitHub Pages:** in the repo, open **Settings → Pages**. Set Source to **Deploy from a branch**, branch `main`, folder `/ (root)`. The site goes live at `https://<user>.github.io/<repo>/`.

## Data

Collections: `players`, `strings`, and `jobs` (one job per player per session, linked by `sessionId`). Estimated sets left for a string = `baselineSets` minus the sets used by jobs logged after `baselineAt`. A hybrid uses half a set of each string per racquet.

The Firestore free tier (50k reads and 20k writes a day) covers a team easily.
