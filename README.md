# Task3 - NeuralPath landing page

A single-page landing site for "NeuralPath", a made-up AI learning platform. Everything is in one file, `learn.html`, with no build step.

## What it does

- Sections: hero, about, services (AI tutor, structured courses, analytics dashboard, live mentor sessions), how it works, testimonials, contact and footer.
- "Start Free Trial" opens a modal where you pick a plan (Starter, Pro, Enterprise) and enter a name and email.
- Contact form and newsletter signup.
- A chat box in the "How It Works" section that acts as an AI tutor demo.
- Scroll-reveal animations and a nav bar that changes background on scroll.

## Tech stack

- Plain HTML, CSS and JavaScript (no framework, no npm packages)
- Google Fonts (Playfair Display, Outfit)
- Supabase REST API for storing form data (called with `fetch`)
- Anthropic Messages API for the chat demo (called from the browser)

## Files

- `learn.html` - the whole page: markup, styles and scripts
- `.gitignore` - ignores `.env` and `node_modules`

## How to run

Open `learn.html` in a browser. No server is needed.

To make the forms and chat work, edit the `CONFIG` object near the top of the file:

```js
const CONFIG = {
  SUPABASE_URL:      "YOUR_SUPABASE_URL",
  SUPABASE_ANON_KEY: "YOUR_SUPABASE_ANON_KEY",
  ANTHROPIC_API_KEY: "YOUR_ANTHROPIC_API_KEY",
};
```

The SQL for the three Supabase tables (`contact_messages`, `newsletter_subscribers`, `enrollments`) and their insert policies is in the comment above `CONFIG`. Do not commit real keys. The comment in the file also says the Anthropic call should go through a backend in production, since the key is visible in the browser.

## Known issues

- The placeholder strings in `CONFIG` are non-empty, so the "not configured" fallbacks (forms pretending to save, canned chat answers) never trigger until you set the values to empty strings or real keys.
- In `sendChat()` the request URL is a Gemini endpoint (`generativelanguage.googleapis.com`) while the headers and body are for the Anthropic API, so the live chat call will not work as written. The URL needs to be `https://api.anthropic.com/v1/messages`.
