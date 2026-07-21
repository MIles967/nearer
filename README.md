# Nearer — Daily Scripture

A warm, mobile-friendly Christian devotional web app. Single self-contained HTML file — no build step, no server, no dependencies to install.

## Features

- **Today** — a daily rotating verse with an illuminated design and a candle-lit reading streak (current + longest, last 7 days).
- **Read** — a contemplative, book-like Scripture reader. Verses flow as prose on a soft parchment surface, with a gentle opening invitation and a closing prayer for each chapter. Tap any verse to highlight it in a color or keep a personal note. Continuous Previous / Next chapter navigation across the whole Bible.
- **Feelings** — search Scripture by how you feel, across 10 color-coded moods (anxious, afraid, grieving, lonely, angry, doubting, joyful, grateful, hopeful, overwhelmed).
- **Together** — a shared reflection wall where readers can post thoughts (optionally tied to a verse), heart posts, and reply to one another.
- **Me** — your display name, streak stats, and every verse you've highlighted or annotated.

## Bible text

Scripture uses the **World English Bible (WEB)**, which is in the public domain. The full book of **Genesis** (all 50 chapters) plus a hand-picked set of well-loved chapters (Psalms, Proverbs, Isaiah, Matthew, John, Romans, 1 Corinthians, Philippians) are included. The book browser shows the full 66-book structure organized by Old and New Testament, marking which books are currently available.

> **Note on the ESV:** The English Standard Version is copyrighted by Crossway and cannot be embedded directly. The reader is structured so Crossway's official ESV API can be connected later with an API key.

## Running it

Just open `index.html` in any modern browser. To host it for free with a real URL:

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Set the source to your `main` branch (root).
4. Your app will be live at `https://<username>.github.io/<repo>/`.

## Storage & privacy

Highlights, notes, streaks, and your display name are saved to your own device/account. Posts and replies in **Together** are shared and visible to everyone using the app.

## Project structure

```
.
├── index.html      # The entire app: HTML, CSS, JavaScript, and Bible data all in one file
├── README.md       # This file
├── LICENSE.md      # Code license + WEB public-domain attribution
└── .gitignore      # Ignore rules (OS files, editor files, secrets)
```

That's the whole project. There is **no build step and no dependencies to install** — `index.html` is fully self-contained. Fonts load from Google Fonts over the network; everything else (styles, logic, Scripture text) is embedded directly in the file.

## How it's built (for recreating / extending it)

Everything lives inside the `<script>` block in `index.html`:

- **`BIBLE`** — an object mapping a chapter key (e.g. `"Genesis 1"`, `"Psalm 23"`) to `{ ref, verses }`, where `verses` is an array of `[verseNumber, "text"]` pairs. To add more Scripture, add more entries here.
- **`AVAILABLE_CONTENT`** — maps each canonical book name to the list of chapter keys present in `BIBLE`. Update this when you add chapters so the book browser shows them as available.
- **`OLD_TESTAMENT_BOOKS` / `NEW_TESTAMENT_BOOKS`** — the full 66-book canon used by the book browser.
- **`READING_SEQUENCE`** — auto-generated flat reading order that powers continuous Previous/Next navigation.
- **`DAILY_VERSES`** — the pool the "Today" verse rotates through.
- **`FEELINGS`** — the mood-based verse search data (label, color, and verses per feeling).
- **`READING_INVITATIONS` / `CLOSING_PRAYERS`** — the devotional text shown around each chapter in the reader.

### Adding the full Bible
The included WEB text was extracted from the public-domain USFX edition in the
`seven1m/open-bibles` project (footnotes stripped, verses split out). You can pull
any additional books the same way and paste them into the `BIBLE` object using the
same `[verseNumber, "text"]` format.

### Connecting the ESV (optional)
To use the ESV instead of the WEB, sign up for a Crossway ESV API key, then replace
the local `BIBLE` lookups in the reader with fetches to their API. Keep the key out
of source control (see `.gitignore`).
