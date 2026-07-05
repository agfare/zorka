# Zorka VPN — Landing Site

A static marketing site for Zorka VPN with three pages (Home, Pricing, Contact), built with plain HTML/CSS/JS — no build step, no framework, ready to publish on GitHub Pages.

## Project structure

```
Zorka/
├── index.html            Home page
├── pricing.html           Pricing page (3 tiers, Stripe Payment Link buttons)
├── contact.html           Contact page (mailto + FAQ)
├── 404.html               Custom not-found page
├── .nojekyll              Disables GitHub Pages' Jekyll processing
├── assets/
│   ├── css/style.css      Shared stylesheet (colors, layout, components)
│   ├── js/main.js         Mobile nav toggle, active link, footer year
│   └── img/               Logo + favicon (SVG)
└── README.md
```

## 1. Publish on GitHub Pages

1. Push this folder to a GitHub repository (e.g. `zorka-vpn`).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`.
4. Choose branch `main` and folder `/ (root)`, then **Save**.
5. Your site will be live at `https://<your-username>.github.io/<repo-name>/` within a minute or two.

The `.nojekyll` file is already included so GitHub Pages serves the files as-is without running them through Jekyll.

If you later add a custom domain, create a `CNAME` file at the repo root containing just the domain name, and configure the DNS records per [GitHub's custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site).

## 2. Connect Stripe payments (Payment Links)

This site uses **Stripe Payment Links**, which requires no backend code — perfect for a static GitHub Pages site.

1. Log in to the [Stripe Dashboard](https://dashboard.stripe.com/).
2. Create three products/prices (or one product with three recurring prices), matching the plans on the Pricing page:
   - **Monthly** — $9.99, recurring every 1 month
   - **Yearly** — $59.99, recurring every 1 year
   - **2-Year** — $79.99, recurring every 2 years (or as a one-time price if your Stripe plan doesn't support a 2-year interval — you'd then manually re-invoice or use Stripe's custom billing intervals)
3. For each price, go to **Payment Links → + New**, select the price, and create the link.
4. Copy each generated URL (it looks like `https://buy.stripe.com/xxxxxxxx`).
5. Open [`pricing.html`](pricing.html) and replace the three placeholder URLs (search for `REPLACE_`):

   | Placeholder | Replace with |
   |---|---|
   | `https://buy.stripe.com/REPLACE_MONTHLY` | Your Monthly Payment Link |
   | `https://buy.stripe.com/REPLACE_YEARLY` | Your Yearly Payment Link |
   | `https://buy.stripe.com/REPLACE_2YEAR` | Your 2-Year Payment Link |

6. Commit and push — the buttons will now open real Stripe-hosted checkout pages in a new tab.

Stripe Payment Links handle the entire checkout, card collection, and receipt flow — nothing else needs to change on the site.

## 3. Customize branding

- **Colors**: edit the CSS custom properties at the top of [`assets/css/style.css`](assets/css/style.css) (`:root { --color-primary: ...; }` etc).
- **Logo**: replace [`assets/img/logo.svg`](assets/img/logo.svg) and [`assets/img/favicon.svg`](assets/img/favicon.svg).
- **Copy**: edit the text directly in `index.html`, `pricing.html`, and `contact.html`.
- **Support email**: replace `support@zorkavpn.com` in [`contact.html`](contact.html) with your real support address.
- **Social links**: replace the `href="#"` placeholders in the contact page's social links with your real profile URLs.

## 4. Preview locally

Just open `index.html` directly in a browser, or serve the folder with any static file server, e.g.:

```
npx serve .
```

Then visit the printed local URL.
