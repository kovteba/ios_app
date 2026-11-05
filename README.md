# ios_app

Public pages for all iOS apps: privacy policies, support pages, App Store texts, screenshots and feature descriptions. Served with GitHub Pages at https://kovteba.github.io/ios_app/.

## Apps

| App | Folder | Presentation | Privacy Policy |
|---|---|---|---|
| Debit Credit | [`debit-credit/`](debit-credit) | [page](https://kovteba.github.io/ios_app/debit-credit/) | [EN](https://kovteba.github.io/ios_app/debit-credit/privacy-en.html) · [UK](https://kovteba.github.io/ios_app/debit-credit/privacy.html) |

## Structure

Every app gets its own folder in the repository root, named after the app in lowercase kebab-case (it becomes part of the URL):

```
<app-name>/
├── README.md            presentation on GitHub: description, features, screenshots, links
├── index.html           presentation + support page (App Store "Support URL")
├── privacy.html         Privacy Policy, Ukrainian
├── privacy-en.html      Privacy Policy, English (App Store "Privacy Policy URL")
├── style.css
├── app-store/           App Store Connect texts (name, subtitle, description, keywords, privacy answers)
├── icon/                app icon
└── screenshots/
    ├── iphone/<lang>/   full-size App Store screenshots
    ├── ipad/<lang>/
    ├── mac/<lang>/
    └── web/<lang>/      small JPEG previews for index.html and README.md
```

## Adding a new app

```bash
cp -R _template my-new-app
```

Then replace every `APP_NAME` / `CONTACT_EMAIL` placeholder, fill in the texts, drop the screenshots in, add a row to the table above and a card to the root `index.html`.

Web previews from full-size iPhone screenshots:

```bash
for f in my-new-app/screenshots/iphone/en/*.png; do mkdir -p my-new-app/screenshots/web/en; sips -s format jpeg -s formatOptions 80 --resampleWidth 660 "$f" --out "my-new-app/screenshots/web/en/$(basename "${f%.png}").jpg"; done
```

## GitHub Pages

Settings → Pages → Deploy from a branch → `main` / `(root)` → Save. Pages for a repository named `ios_app` are served at `https://kovteba.github.io/ios_app/<app-name>/...`. The repository must be public for Pages on a free plan.
