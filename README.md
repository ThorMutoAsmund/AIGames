# AI Games

Static multi-game site where each game lives in its own folder and is served from that folder's `index.html`.

## Current game routes

- `/colorgame/`
- `/geometrydash/`
- `/tictactoe/`

## Add a new game

1. Create a new folder (for example `snake`).
2. Put an `index.html` file inside it.
3. Add a link to that folder in root `index.html`.
4. Commit and push.

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
