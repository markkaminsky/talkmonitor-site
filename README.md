# TalkMonitor — support & privacy pages

Static pages for **App Store Connect** (Support URL + Privacy Policy URL). Not part of the iOS app bundle.

## LIVE — deployed 2026-07-13 on GitHub Pages

Repo: <https://github.com/markkaminsky/talkmonitor-site> (Pages from `main`, HTTPS enforced).

## App Store Connect — paste these

| Field | URL |
|-------|-----|
| **Support URL** | `https://markkaminsky.github.io/talkmonitor-site/support/` |
| **Privacy Policy URL** | `https://markkaminsky.github.io/talkmonitor-site/privacy/` |

**Contact:** msksoftware@yahoo.ca

## Redeploy after editing these pages

```
SITE=$(mktemp -d) && cp -R website/. "$SITE/" && touch "$SITE/.nojekyll" \
  && cd "$SITE" && git init -q -b main && git add -A \
  && git commit -q -m "Update site" \
  && git push -q --force https://github.com/markkaminsky/talkmonitor-site.git main
```

All URLs in the pages are **relative**, so the site works at a domain root
(Netlify, custom domain) or under a subpath (GitHub Pages) unchanged. To move
to Netlify later: drag this folder onto a Netlify deploy (the `_headers` file
only takes effect there), update the two URLs in App Store Connect, and update
the absolute `og:url` / `og:image` tags in `index.html`.

## Contents

```
website/
  index.html           → landing (optional)
  support/index.html   → App Store Support URL
  privacy/index.html   → App Store Privacy Policy URL
  styles.css           → one shared stylesheet (all pages)
  assets/              → logo.png, favicon.png, apple-touch-icon.png (from LaunchOrb)
  _headers             → Netlify cache/security headers (other hosts ignore it)
```

**Content rule:** every claim on these pages must match the shipped app — the privacy
policy discloses the on-device tone trend and the opt-in soft-response generation
(recent words → Apple Intelligence, on-device only). If app data flows change, update
`privacy/index.html` and its effective date in the same commit.

## Preview locally

```
python3 -m http.server 8788 --directory website
```
(absolute paths like `/styles.css` need a server root — opening the files directly won't style them.)
