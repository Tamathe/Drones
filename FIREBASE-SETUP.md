# Live shared hub — Firebase setup

`index.html` stores its tasks, decisions, team-doc links, and activity log in a
**shared Firebase Realtime Database**, so the whole team sees the same **live**
data — no more per-browser copies. Viewing is open to anyone with the link;
**editing requires the team password**.

## What you do once (~10 min, all free)

1. Go to <https://console.firebase.google.com> → **Add project** (any name, e.g.
   "drones-hub"). You can disable Google Analytics — not needed.
2. On the project home, click the **web icon `</>`** to add a Web App. Give it a
   nickname, **do not** enable Hosting. Copy the **`firebaseConfig`** object it shows.
3. Left menu → **Build → Realtime Database → Create database**. Pick a location;
   start in **Locked mode** (we set the rules in step 6).
4. Left menu → **Build → Authentication → Get started → Email/Password → Enable → Save**.
5. **Authentication → Users → Add user.** Email: `editor@drones.app` (use exactly
   this), Password: **the team edit password** you want. Create it, then copy that
   user's **User UID** (the long string in the Users table).
6. **Realtime Database → Rules** tab → paste the contents of `database.rules.json`
   (in this folder), replacing `PASTE_EDITOR_UID` with the UID from step 5 →
   **Publish**.

## What to send me

- The **`firebaseConfig`** object (from step 2).
- The **editor User UID** (from step 5), if you didn't paste the rules yourself in step 6.

Then I drop the config into `index.html`, confirm the rules, merge this branch to
`main`, and push. The first time you click **Unlock to edit** and enter the password,
the board seeds itself from the current content. After that everyone sees edits live.

## Notes

- The Firebase config in `index.html` is **not a secret** — security is enforced by
  the database rules, not by hiding the config. It is fine that it lives in the public repo.
- The whole team shares one edit password. Change it anytime under
  **Authentication → Users**.
- The free "Spark" plan is far more than enough for a team this size.
- Data model (for reference): `hub/sections`, `hub/tasks` (each task carries its
  `sid` section id), `hub/decisions`, `hub/docs`, `hub/log`, `hub/meta/seeded`.
