# InvoiceFlow — Stage 1

Professional invoices for UK sole traders, freelancers and small businesses.

**Stage 1 (this download)** gives you a working website:

| Page | What it does |
|---|---|
| `/` | Landing page: hero, features, how it works, pricing comparison, FAQ, footer |
| `/create` | The invoice generator: live preview, exact totals, VAT, discounts, 3 templates, logo upload, PDF download, print |
| `/create?sample=1` | A clearly labelled sample invoice for new users |
| `/invoices` | Saved invoices: totals summary, search, status filters, change status, edit, duplicate, download, delete |

> **Where's the data stored?** In Stage 1, invoices are saved in the user's own browser (`localStorage`). There are no accounts yet, so no paid-plan limits apply. Stage 3 moves everything to Supabase with secure logins, and Stage 4 adds Stripe. The website says this honestly to visitors.

---

## 1. Run it on your computer

You only need to do steps 1–2 once.

1. **Install Node.js** (version 22 or newer) from <https://nodejs.org> — choose the "LTS" download and click through the installer.
2. **Install a code editor**: [Visual Studio Code](https://code.visualstudio.com) is free and beginner-friendly.
3. **Unzip** `invoiceflow-stage1.zip` somewhere easy, like your Documents folder.
4. In VS Code, choose **File → Open Folder…** and pick the `invoiceflow` folder.
5. Open a terminal inside VS Code: **Terminal → New Terminal**.
6. Install the project's building blocks (takes 1–2 minutes, only needed once):
   ```bash
   npm install
   ```
7. Start the website:
   ```bash
   npm run dev
   ```
8. Open <http://localhost:3000> in your browser. 🎉

To stop it, click in the terminal and press `Ctrl + C`. Any change you save in a file appears in the browser automatically.

### Useful commands

| Command | What it does |
|---|---|
| `npm run dev` | Runs the site locally for development |
| `npm test` | Runs the 12 automatic tests that check the money maths |
| `npm run typecheck` | Checks the code for mistakes |
| `npm run build` | Builds the production version (Vercel does this for you) |

If `npm run build` or `npm run typecheck` shows an error, copy the whole message and send it to me — I'll fix it.

---

## 2. How the code is organised

```
app/                    Pages (Next.js "App Router")
  page.tsx              Landing page
  create/               Invoice generator page
  invoices/page.tsx     Saved invoices list
  globals.css           Brand colours, fonts, animations, print styles
components/
  brand/logo.tsx        InvoiceFlow logo
  landing/              Header, pricing, footer
  invoice/              Editor, line items, logo upload, live preview, PDF
  ui/                   Buttons, inputs, cards (shadcn/ui style)
lib/
  invoice/calculations.ts   ⭐ All money maths (in whole pennies — no rounding errors)
  invoice/calculations.test.ts  Tests for the maths
  invoice/validation.ts     Friendly error messages + UK VAT invoice checks
  invoice/storage.ts        Saving (browser now, Supabase in Stage 3)
  invoice/format.ts         £ and UK date formatting
  plans.ts                  Free / Pro / Business plan definitions and limits
```

### Why the maths is trustworthy

Computers store numbers like `0.1` imprecisely, which is why some invoice tools show £0.30000000004. InvoiceFlow converts every amount to whole pennies first and only uses whole-number maths, rounding half-up to the nearest penny. VAT is calculated per rate band (20%, 5%, 0%) after any discount, and a discount is shared exactly across bands so the numbers always add up. `npm test` proves it.

---

## 3. Put it online with Vercel (free)

1. Create a free account at <https://github.com> and install **GitHub Desktop** (<https://desktop.github.com>).
2. In GitHub Desktop: **File → Add Local Repository** → choose the `invoiceflow` folder → it will offer to "create a repository" — accept. Then click **Publish repository** (keep it **private**).
3. Create a free account at <https://vercel.com> and choose **Continue with GitHub**.
4. Click **Add New… → Project**, pick `invoiceflow`, and click **Deploy**. No settings to change for Stage 1.
5. After about a minute you'll get a live address like `invoiceflow-yourname.vercel.app`.

From now on, every time you commit and push in GitHub Desktop, Vercel updates the live site automatically.

## 4. Connect your own domain

1. Buy a domain (e.g. `invoiceflow.co.uk`) from a registrar such as Namecheap, Cloudflare or 123-reg. Check the name isn't already trademarked or in use by another invoicing company.
2. In Vercel: open your project → **Settings → Domains** → type your domain → **Add**.
3. Vercel shows you one or two DNS records (usually an `A` record and a `CNAME` for `www`). Log in to your registrar, find **DNS settings**, and add exactly those records.
4. Wait 5 minutes to a few hours. Vercel shows a green tick when it's working and adds the HTTPS padlock automatically.
5. In Vercel → **Settings → Environment Variables**, add `NEXT_PUBLIC_SITE_URL` = `https://yourdomain.co.uk`, then redeploy.

---

## 5. Test checklist for Stage 1

Tick these off on both a phone and a computer:

- [ ] `npm test` shows **12 passing**.
- [ ] Landing page: every button goes somewhere; FAQ items open and close; mobile menu works.
- [ ] Create an invoice with only a business name, customer name and one item → **Download PDF** works and opens.
- [ ] Add 3+ items with quantities like `1.5` and prices like `19.99` → check totals with a calculator.
- [ ] Turn VAT on → enter a VAT number → mix 20% and 5% items → check the VAT summary.
- [ ] Add a 10% discount, then a £25 fixed discount → totals update instantly.
- [ ] Upload a PNG and a JPG logo → shows in preview and PDF.
- [ ] Switch between Classic, Modern and Minimal → preview and PDF both change.
- [ ] Leave the customer name empty → Download shows a friendly error and scrolls to it.
- [ ] Save → go to **My invoices** → it's listed. Duplicate it → new number, today's date.
- [ ] Mark an invoice as sent with a due date in the past → it shows as **Overdue**.
- [ ] Mark it **Paid** → totals at the top update.
- [ ] Search by customer name and by invoice number; try each status filter.
- [ ] **Print** → only the invoice prints, on A4.
- [ ] Delete an invoice → asks to confirm → gone.

---

## 6. What's next

| Stage | Contents |
|---|---|
| ✅ 1 | Landing page, invoice generator, live preview, PDF, templates, local saving |
| 2 | Customer management (saved customers, quick-select, history) + full dashboard with Recharts monthly income chart, recent invoices, CSV export |
| 3 | Supabase: sign up, login, password reset, profiles, invoices & customers in the database, Row Level Security SQL migrations, logo storage |
| 4 | Stripe: Checkout, Customer Portal, webhooks, subscription status in the database, **server-side** plan limits (3 invoices/month on Free, template & feature gating), clearly labelled test mode |
| 5 | Business plan features: recurring invoices, payment reminder emails, multiple business profiles, advanced reports |

Before taking real customers, read **COMPLIANCE.md**.
