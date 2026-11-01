# TutoRoo — Vue 3 landing page

This is a fresh Vue 3 + Vite project based on the recommended **F** TutoRoo pre-launch landing page direction.

## Requirements
- Node.js 18 or newer
- npm

## Run locally

```bash
npm install
npm run dev
```

Open the local URL printed by Vite (usually http://localhost:5173).

## Production build

```bash
npm run build
npm run preview
```

## Project structure

```text
tutaroo/
├── index.html
├── package.json
└── src/
    ├── App.vue
    ├── main.js
    └── style.css
```

## Before launch

The forms currently show a local preview confirmation only. They do not store or send sign-ups yet. Connect them to MailerLite (or your chosen mailing-list provider), and create separate parent/learner and founding-tutor groups.

The design uses temporary remote Unsplash photos and Google Fonts. Replace these with approved brand assets and licensed photography before production.

The PDF includes items still awaiting confirmation, such as final launch date, tutor fee wording, founding-tutor reward, parent early-bird offer, and company name for the footer. Those have deliberately been kept neutral or marked as provisional rather than invented.
