# Lista+ — website

Single-page marketing site for the **Lista+** Android app (`com.jorres.listaplus`).
Static HTML, no build step, no dependencies.

```
index.html            the site, including all four policy modals
privacy.html          plain policy page — this is what Google Play points at
delete-account.html   plain deletion page — this is what Google Play points at
assets/               logos and screenshots
.nojekyll             harmless on Netlify; keeps GitHub Pages from processing the files
```

## Deploying (Netlify)

No build command and no framework. Connect the repo and set:

| Setting | Value |
|---|---|
| Build command | *(leave empty)* |
| Publish directory | `.` |

Netlify serves `index.html` at the root automatically.

## The policy modals

Four panels live at the bottom of the page: **Privacy Policy**, **Data Collection
Statement**, **Deleting Your Account**, and **Legal & Terms**. Each can also be opened
directly by URL, which is what an external link needs:

```
/#privacy
/#data
/#delete
/#legal
```

> ⚠️ **Do not give these fragment URLs to Google Play.** A modal needs JavaScript and a
> click before the text appears, and a reviewer following a link expects the policy
> rendered immediately.
>
> Point Play at the plain pages in this repo instead — they contain no JavaScript at all
> and render on load:
>
> ```
> /privacy.html          → App content > Privacy policy, and the Store listing
> /delete-account.html   → App content > Data safety > Data deletion
> ```
>
> When filling in Data safety, also tick that an in-app deletion path exists
> (More → Account → Delete cloud account). Having both is the strongest answer.

## Keeping the copy honest

The policy text makes specific factual claims — no analytics, exactly two permissions,
PBKDF2 password hashing, data hosted in Singapore, and precisely which entities are backed
up. **There are now three copies of this content:**

1. `docs/` in the app repo (source)
2. `privacy.html` + `delete-account.html` here (canonical — what Play sees)
3. the modals in `index.html` (same content, presented for people browsing the site)

If the app's behaviour changes, update **all three** and bump the "last updated" date. An
inaccurate privacy policy is a policy violation in itself, not merely stale documentation.
Copies 2 and 3 live in this repo, so at least they move in one commit.

## Messaging

Lista+ is described throughout as a **record-keeping tool for credit already extended** —
never as lending, loans, or a financial service. That framing is deliberate: it matches
the "no financial features" declaration in Play's App content questionnaire, and Play's
financial-products policies bite apps that read like loan offerings. Keep it in any edit.

## Assets

Logos come from `Desktop/ListaPlus-Logos/`, screenshots from
`Desktop/ListaPlus-Showcase/screenshots/light/` (downscaled to 540px wide).

The logo files carry a **white background baked in** — they were cut from a flattened JPEG
sheet, and their interiors contain white and cream (the notebook page, the eyes), so the
background cannot be keyed out without punching holes through the artwork. The hero
therefore presents the lockup on a deliberate white plate, which reads as designed rather
than as a stray white box in dark mode. The header uses `icon.png` instead, which is
full-bleed emerald and needs no plate.
