# Ilyaz AI — Passing Package Game

A static, mobile-friendly Kannada quiz application. Public visitors do not need accounts. Quiz content can be stored locally in the admin browser or distributed as static JSON files.

## Run locally

Because the app uses IndexedDB, fetch, and a service worker, run it through a local web server rather than opening `index.html` directly.

```bash
python -m http.server 8000
```

Open `http://localhost:8000`.

## Demo admin access

- Username: `admin`
- Password: `ilyaz2026`

Change `ADMIN_USER` and `ADMIN_PASS` in `js/admin.js` before deploying if desired. **This is not secure authentication.** Anyone can inspect the client-side source and discover or bypass it. Do not use this approach for confidential content or real access control.

## Included sample quiz

A four-question Kannada basics quiz is included as a published static JSON sample and is also created in the admin browser the first time the app is opened.

## Word document import

Use the included `sample-quiz-template.docx`. Keep a single table with these columns:

1. Sl No
2. Question
3. Correct Answer
4. Wrong Answer 1
5. Wrong Answer 2
6. Wrong Answer 3
7. Image

The image column is optional. This browser importer reads table text and attempts to read inline images converted by Mammoth. Complex Word layouts, floating images, merged cells, and image anchoring may need manual correction. Review the import preview before saving.

Mammoth.js is loaded from jsDelivr, so DOCX import needs an internet connection. The app itself can run without that CDN for manual quizzes.

## Local storage vs shared publishing

- Admin-created quizzes are stored in IndexedDB in that browser only.
- Export a quiz or backup from **Admin → Publish & backup**.
- To share a quiz publicly, add its JSON file to `data/quizzes/` and list its filename in `data/quiz-index.json`, then redeploy.
- Example index: `["kannada-basics.json"]`.
- Each public JSON file should contain one quiz object with `published: true`, `id`, `title`, `questions`, and optional `settings`.
- Anyone can inspect public quiz JSON. Do not publish private content.

A static browser app cannot upload files into your hosting account or synchronize IndexedDB across devices. Automated publishing and genuinely secure admin authentication require a serverless/backend service.

## Kannada voice

The app uses the browser Web Speech API and looks for an installed voice with language `kn-IN`. Voice availability varies by device, browser, and installed speech packs. If no Kannada voice is installed, the app displays a notice rather than speaking Kannada text with an English voice.

## Sound

Short tones are generated with Web Audio API. Browsers may require a first user interaction before audio can play. Sound can be disabled in the admin settings.

## Deployment

Upload the project folder to Netlify, Vercel, or GitHub Pages. Keep the folder structure intact. Use HTTPS hosting for best browser API support.

## Privacy

No student accounts or attempt history are collected. Local quizzes remain in the browser's IndexedDB until the browser data is cleared. Public quiz content is downloaded by visitors. This demo does not provide secure admin authentication.
