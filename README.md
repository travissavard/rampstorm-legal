# Rampstorm legal site

Static pages for **Rampstorm** (Android, Google Play package `com.rampstorm.productseal`, developer
ProductSeal), hosted on GitHub Pages. They provide the URLs Google Play and AdMob ask for:

| Page | Path | Use it for |
| --- | --- | --- |
| Home | `index.html` | Play Console store listing "Website" field |
| Privacy policy | `privacy/index.html` | Play Console > App content > Privacy policy; AdMob Privacy & messaging |
| Terms of use | `terms/index.html` | Linked from the game and the store listing |
| Licences | `licenses/index.html` | Open-source and third-party notices |
| Support | `support/index.html` | Help, restoring purchases, deleting data, ad choices |
| Not found | `404.html` | Served by GitHub Pages for missing paths |

Everything is plain HTML plus one shared `style.css`. There are no scripts, external fonts, trackers,
cookies or analytics, and no build step. `.nojekyll` tells GitHub Pages to serve the files as they are.

## Publish on GitHub Pages

1. Create a public repository, for example `rampstorm-legal`, and put the **contents** of this folder
   at the repository root (including the hidden `.nojekyll` file).
2. In the repository, go to **Settings > Pages**, choose **Deploy from a branch**, branch `main`,
   folder `/ (root)`, and save.
3. After a minute the site is at `https://<your-github-user>.github.io/rampstorm-legal/`. The pages are:
   - `https://<your-github-user>.github.io/rampstorm-legal/`
   - `https://<your-github-user>.github.io/rampstorm-legal/privacy/`
   - `https://<your-github-user>.github.io/rampstorm-legal/terms/`
   - `https://<your-github-user>.github.io/rampstorm-legal/licenses/`
   - `https://<your-github-user>.github.io/rampstorm-legal/support/`

All links between pages are relative, so the site works under any repository name or a custom domain.
Open `index.html` directly from disk to preview it locally.

## Update the pages

- **Edit the HTML directly.** Each page is self-contained apart from `style.css`. Keep links relative
  (`../privacy/index.html`, never `/privacy/`), because a project site lives under a sub-path.
- **Change the effective date** at the top and in the footer of `privacy/index.html` or
  `terms/index.html` whenever the substance changes, and mention important changes in the game's
  release notes.
- **Keep the privacy policy and the Play Data safety form in step.** The data types in section 3 of the
  privacy policy (device or other IDs, approximate location, app interactions, crash logs,
  diagnostics) must match `docs/privacy/DATA_SAFETY_INVENTORY.md` and what is submitted in Play Console.
  If the game adds a backend, accounts, cloud save, analytics, leaderboards or another SDK, or changes
  the ads SDK version, update both before that version is released.
- **Update the licences page when dependencies change.** Rebuild the Android app, list its contents
  (`unzip -l app.apk`, the `META-INF/*.version` files and the `*.properties` files at the APK root give
  library versions; `aapt2 dump badging app.apk` gives permissions) and add or remove entries.
  Licence texts are copied verbatim from the upstream `LICENSE` files at the shipped tag; copy them
  again rather than editing them. The permissions table in section 6 of the privacy policy should
  match the badging output.
- **404 page.** `404.html` uses inline CSS because GitHub Pages serves it at whatever path was missing.

## Not in this folder

- `app-ads.txt`. AdMob looks for it at the **root of the developer website's domain**
  (`https://example.com/app-ads.txt`). A GitHub Pages project site lives under a sub-path, so AdMob
  cannot find a file placed here. Use a custom domain on this site, or a `<user>.github.io` user site,
  and put `app-ads.txt` (with the AdMob publisher line from your AdMob account) at that root.
