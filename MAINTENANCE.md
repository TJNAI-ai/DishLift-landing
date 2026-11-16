# Maintenance mode

dishlift.app is serving a maintenance page from the files at the repository root (`index.html` and `404.html`). The original site is in `_source/`, which GitHub Pages (Jekyll) does not publish. The `CNAME` file and `.well-known/security.txt` were left in place so the custom domain, HTTPS, and security contact stay intact. Favicons stay at the root so the browser tab still shows the DishLift icon.

## Restore the original site

Do not rewrite history or force-push. Work on a branch and merge to `main`.

1. From the repository root, move the original files back:

   ```bash
   git mv _source/.nojekyll .
   git mv _source/404.html _source/README.md _source/assets \
     _source/index.html _source/privacy.html _source/robots.txt \
     _source/sitemap.xml _source/support.html _source/terms.html .
   rmdir _source
   ```

2. Remove the maintenance-only files that should not stay on the live site:

   ```bash
   git rm -f _config.yml MAINTENANCE.md
   ```

   Keep `CNAME`, `favicon.ico`, `apple-touch-icon.png`, and `.well-known/`. The move in step 1 replaces the maintenance `index.html`, `404.html`, `robots.txt`, and `README.md`.

3. Commit, open a pull request if `main` cannot be pushed directly, and merge. GitHub Pages will republish from `main` at `/`. DNS does not need to change.
