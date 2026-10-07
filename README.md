# Malaq Impact Initiative: Website

A static, multi-page website for Malaq Impact Initiative, an NGO working to end
technology-facilitated gender-based violence (TFGBV) in Uganda.

Built with plain HTML/CSS/JavaScript (ES6 classes, no framework/build step, no
database) so it can be hosted directly on GitHub Pages.

## Project structure

```
index.html              Home: hero, issue, 10 forms, why Uganda, approach,
                        programmes, survivors, impact, resources, partners
about.html              Who we are, mission, vision, who we work with
team.html               Leadership, board and advisors, values
safeguarding.html       Safeguarding commitments, policies, raising a concern
the-issue.html          Definition, the 10 forms, why Uganda, harm
our-work.html           Three pillars, five programme areas, impact
resources.html          Filterable resource library
get-help.html           Emergency card, Malaq support channels, other services,
                        next steps, safe browsing
digital-safety.html     Tabbed safety guides and an interactive safety check
get-involved.html       Five audience paths, partnerships, awareness
news.html               News and stories (placeholders)
contact.html            Contact channels and general enquiry form (Formspree)
privacy.html            Privacy policy with a live table of contents
404.html                Not found page

partials/
  header.html           Shared header, desktop nav and mobile menu
  footer.html           Shared footer

assets/
  css/main.css          Design system and all styles (tokens at the top)
  icons/sprite.svg      Every icon on the site, referenced with <use>
  js/boot.js            Tiny script that enables JS-only styles before paint
  js/main.js            App entry point
  js/classes/           One class per behaviour: PartialLoader, Navigation,
                        Dropdown, QuickExit, RevealOnScroll, CounterGroup,
                        Accordion, Tabs, SafetyChecklist, ScrollSpy, BackToTop,
                        ContactForm, ResourceFilter
  favicon.svg
```

Each page loads `partials/header.html` and `partials/footer.html` at runtime via
`fetch()`, so the header and footer only need to be edited in one place.

## Design system

- **Colours** are CSS variables at the top of `assets/css/main.css`: deep plum
  and purple for identity, teal for safety and action, a warm cream background
  and an apricot highlight used sparingly.
- **Type** pairs Fraunces (display headings) with Manrope (body and interface).
- **Icons** live in `assets/icons/sprite.svg`. To use one:
  `<svg class="icon" aria-hidden="true"><use href="assets/icons/sprite.svg#lock"></use></svg>`.
- **Layout** is mobile first and tested at phone (360px), tablet (768px) and
  desktop (1280px+) widths. The full navigation appears from 1180px; below
  that the menu button opens a full-screen menu.

## Running locally

Because the header/footer are loaded via `fetch()`, opening `index.html`
directly by double-clicking it won't work (browsers block `fetch` on the
`file://` protocol). Serve the folder with any local static server, e.g.:

```bash
# Python
python -m http.server 8000

# Node (no install needed)
npx serve .
```

Then open `http://localhost:8000`.

## Things you still need to fill in

Search the codebase for `TODO` and `Image placeholder` to find every spot
marked for your input. In summary:

1. **Images**: every `.ph` block is a labelled empty slot. Replace the whole
   block with an `<img>` tag (with meaningful `alt` text) once you have real
   photos, for example
   `<img src="assets/images/hero.jpg" alt="Young women at a digital safety workshop" />`.
2. **Contact form endpoint** (`contact.html`): currently points to
   `https://formspree.io/f/YOUR_FORM_ID`. Once the `info@malaq.org` mailbox
   exists in Zoho:
   1. Create a free account at [formspree.io](https://formspree.io).
   2. Create a new form using that email as the recipient.
   3. Copy the endpoint URL Formspree gives you and paste it into the
      `action="..."` attribute of the `<form data-contact-form>` in
      `contact.html`.
   4. Spam protection is already wired up via Formspree's built-in honeypot
      (the hidden `_gotcha` field), so no extra setup is needed.
3. **Malaq support channels** (`get-help.html`, "How Malaq can help"): phone,
   WhatsApp, email and support hours. Only publish channels that are monitored.
4. **Other support services** (`get-help.html`): national GBV helpline, police,
   legal aid and counselling contacts, plus the emergency number in the red
   card. Verify each with a live source before publishing.
5. **Phone numbers** (`contact.html`, `get-help.html`): shown as
   `+256 XXX XXX XXX`. The email addresses are already set to
   `info@`, `help@`, `partnerships@`, `media@` and `safeguarding@malaq.org`
   (create these five mailboxes in Zoho).
6. **Impact figures shown as XX** (`index.html`, `our-work.html`): Malaq's own
   programme results (people reached, survivors supported, sessions, outputs).
   Replace them only with verified figures. To animate a number, add
   `data-count="68" data-suffix="%"` to its `.stat__num` and remove the
   `stat__num--pending` class.

   The Uganda statistics are already filled in with sourced figures (Pollicy
   2020, DataReportal Digital 2026, GSMA Mobile Gender Gap Report 2026). Review
   them each year and update the number, label and source link together.
7. **Team and governance** (`team.html`): the Founder and Chair's profile is
   live (photo in `assets/images/founder.*`). Her biography was written from
   two facts (degree, profession), so expand it with her approved wording.
   Other team members show a photo, name and role only (no biography). The
   Secretary is added; to add more, copy a `.member` card and put a 4:5
   portrait in `assets/images/team/`. Remaining leadership cards and the
   board and advisors are placeholders (remove any that are not needed).
8. **Safeguarding** (`safeguarding.html`): link each policy PDF once approved,
   and add the safeguarding contact phone.
9. **Partner logos** (`index.html`, `get-involved.html`): replace the
   placeholders with confirmed partners only.
10. **Resources** (`resources.html`): replace the "Coming soon" cards with real
    documents. Instructions are in a comment at the top of the library.
11. **Social media links**: placeholder `#` links in `partials/footer.html`.
12. **Donations** (`get-involved.html`, funders card): link to a giving page
    once one exists.
13. **Mission and vision** (`about.html`): confirm the final wording with
    leadership.

## Hosting and domain

- **Repository:** [github.com/malaqimpact/malaqimpact.github.io](https://github.com/malaqimpact/malaqimpact.github.io),
  owned by the `malaqimpact` GitHub organisation.
- **GitHub address:** https://malaqimpact.github.io/
- **Domain:** `malaq.org`, registered with Namecheap, DNS managed in
  **Cloudflare**. All DNS records (website and email) are edited in Cloudflare.

DNS records for the website (Cloudflare, proxy status **DNS only**, grey cloud):

| Type  | Name  | Content                  |
|-------|-------|--------------------------|
| A     | `@`   | `185.199.108.153`        |
| A     | `@`   | `185.199.109.153`        |
| A     | `@`   | `185.199.110.153`        |
| A     | `@`   | `185.199.111.153`        |
| AAAA  | `@`   | `2606:50c0:8000::153`    |
| AAAA  | `@`   | `2606:50c0:8001::153`    |
| AAAA  | `@`   | `2606:50c0:8002::153`    |
| AAAA  | `@`   | `2606:50c0:8003::153`    |
| CNAME | `www` | `malaqimpact.github.io`  |

The `CNAME` file in the repo root holds `malaq.org`. Keep "Enforce HTTPS"
switched on under **Settings > Pages**.

## Security notes

- **Content-Security-Policy** is set via a `<meta>` tag in every page
  (restricts scripts/styles/connections to this site, Google Fonts, and
  Formspree). GitHub Pages doesn't let you set real HTTP response headers, so
  this meta-tag CSP is the strongest option available without moving to a
  platform like Cloudflare Pages or Netlify (which support a `_headers` file
  for additional headers like `X-Frame-Options`).
- No inline `<script>`/`onclick=` handlers anywhere, and no inline `style=`
  attributes either (the CSP has no `unsafe-inline`). All JS is in external
  files using `addEventListener`, and all styling is in CSS classes, which
  reduces XSS risk.
- The contact form is spam-protected with Formspree's honeypot field and
  validated client-side, and Formspree itself enforces its own server-side
  protections and submission limits.
- No analytics/tracking scripts and no database, so there's nothing to be
  breached beyond the static files themselves.
- All external links use `rel="noopener noreferrer"`.

## The "Quick Exit" safety feature

A red **Quick exit** button appears in the header on every page. Clicking it
(or pressing `Escape` three times quickly) hides the page instantly and redirects to
`https://www.google.com` and *replaces* the current history entry, so the
back button won't return to this site. This is standard practice on
GBV-support websites. You can change the destination URL by editing
`QuickExit.DESTINATION` in `assets/js/classes/QuickExit.js`.

## Deploying

GitHub Pages deploys automatically from the `main` branch root. Push a change
and the live site updates within a minute or two.
