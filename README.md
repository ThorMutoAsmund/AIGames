# AI Games

Static multi-game site where each game lives in its own folder and is served from that folder's `index.html`.

## Current game routes

- `/colorgame/`
- `/geometrydash/`
- `/tictactoe/`
- `/ormespil/`

## Add a new game

1. Create a new folder (for example `snake`).
2. Put an `index.html` file inside it.
3. Add a link to that folder in root `index.html`.
4. Commit and push.

## Firebase leaderboard for Ormespil

To enable a shared leaderboard for everyone in `ormespil`:

1. Copy `ormespil/firebase-config.example.js` to `ormespil/firebase-config.js`.
2. Fill in your Firebase project values in that file.
3. In Firebase Realtime Database rules, allow read + validated write for the leaderboard path.

Suggested starter rules:

```json
{
  "rules": {
    "scores": {
      "ormespil": {
        "leaderboard": {
          "$entryId": {
            ".read": true,
            ".write": true,
            ".validate": "newData.val() == null || (newData.hasChildren(['name','score']) && newData.child('name').isString() && newData.child('name').val().matches(/^[A-Z]{1,6}$/) && newData.child('score').isNumber() && newData.child('score').val() >= 0 && (!newData.child('createdAt').exists() || newData.child('createdAt').isNumber()))"
          }
        }
      }
    }
  }
}
```

Without `ormespil/firebase-config.js`, the game automatically falls back to per-browser local storage.

## Firebase global high score for Geometry Dash

To enable one shared high score for everyone in `geometrydash`:

1. Copy `geometrydash/firebase-config.example.js` to `geometrydash/firebase-config.js`.
2. Fill in your Firebase project values in that file.
3. Add rules for the geometrydash score path in Realtime Database.

Example rule block (combine with your existing rules):

```json
{
  "rules": {
    "scores": {
      "geometrydash": {
        "highscore": {
          ".read": true,
          ".write": true,
          ".validate": "newData.isNumber() && newData.val() >= 0 && (!data.exists() || newData.val() >= data.val())"
        }
      }
    }
  }
}
```

Without `geometrydash/firebase-config.js`, the game falls back to per-browser local storage.

## Publish with GitHub Pages

1. Create a new GitHub repository.
2. Push this folder to the repository.
3. In GitHub, open **Settings > Pages**.
4. Set **Source** to **Deploy from a branch**.
5. Select branch **main** and folder **/(root)**.
6. Save and wait for deployment.

Your public links will be:

- Home: `https://<your-username>.github.io/<repo-name>/`
- Game: `https://<your-username>.github.io/<repo-name>/<folder-name>/`
