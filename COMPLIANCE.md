# Before you launch: UK legal & HMRC checklist

I'm not a lawyer or accountant. This is a list of things to **check with a qualified accountant or solicitor** before you take paying customers. Rules change, so confirm each point on GOV.UK.

## 1. What InvoiceFlow already puts on invoices

| Requirement | Where it's handled |
|---|---|
| Unique invoice number | Auto-numbered `INV-0001…`; duplicates are blocked when saving |
| Seller's name & address, customer's name & address | Business and customer sections |
| Invoice date and due date, UK date format | Invoice details |
| Description, quantity, unit price, line amount | Line items |
| Total amount owed in £ | Totals |
| Limited company number + where registered | Footer, if a company number is entered |
| **VAT invoices:** VAT number, "VAT Invoice" title, VAT rate per line, net per rate, VAT per rate, total VAT, tax point if different | Shown only when "Charge VAT" is switched on; validation requires the VAT number and both addresses |

VAT is **off by default** and only switched on automatically if the user has saved a VAT number.

## 2. Things to check before launch

**Invoice content**
- [ ] **Limited companies** must also show their **registered office address** if it differs from the trading address, and their full registered name. Stage 3 will add a "Registered office" field. Until then, tell limited-company users to use their registered office as the business address.
- [ ] **Sole traders trading under a business name** should show their own name and an address where documents can be served (Companies Act 2006 / Business Names rules). Consider adding an "Owner name" field.
- [ ] **Sequential numbering:** HMRC expects VAT invoice numbers to be unique and sequential. Users can edit numbers in InvoiceFlow, so consider warning them about gaps.
- [ ] **Simplified (≤ £250 incl. VAT) and modified (retail, > £250) VAT invoices** are separate formats. InvoiceFlow always produces a full VAT invoice, which is the safe default, but confirm that's acceptable for your target users.
- [ ] **Special VAT cases are not handled:** the construction **domestic reverse charge** (very relevant for builders, electricians and plumbers working for VAT-registered contractors), the Flat Rate Scheme, margin schemes, exempt supplies, and supplies to customers outside the UK. Get an accountant to review these. Reverse charge support is a strong candidate for a future feature.
- [ ] **VAT registration threshold:** it was raised to £90,000 in April 2024. Check the current figure before quoting it anywhere on the site.
- [ ] **Late payment:** B2B invoices can claim statutory interest and fixed compensation under the Late Payment of Commercial Debts (Interest) Act 1998. You could offer optional wording for this in the payment terms.

**Making Tax Digital (MTD)**
- [ ] **MTD for VAT** applies to all VAT-registered businesses, and **MTD for Income Tax** started on 6 April 2026 for sole traders and landlords with qualifying income over £50,000. It extends to over £30,000 from April 2027 and over £20,000 from April 2028.
- [ ] InvoiceFlow is **not** MTD-recognised software and does not submit anything to HMRC. The FAQ says so. **Never market it as "MTD compliant"** unless you build and get HMRC recognition for that.
- [ ] A useful, honest feature would be a CSV export that users' MTD software or accountant can import (Stage 2).

**Your own business (running the SaaS)**
- [ ] **Privacy policy & cookie notice** (UK GDPR / Data Protection Act 2018 / PECR). Needed before Stage 3, when you store personal data. Add footer links only once the pages exist.
- [ ] **Register with the ICO** and pay the data protection fee. Most businesses processing personal data must do this.
- [ ] **Terms of service:** subscriptions, cancellation, refunds, liability limits, and "not tax advice".
- [ ] **Consumer Contracts Regulations:** a 14-day cancellation right for sole-trader customers who count as consumers, and clear pre-contract pricing. Also check the **Digital Markets, Competition and Consumers Act 2024** subscription rules (reminders and easy cancellation) as they come into force.
- [ ] **Data processing agreements** with Supabase and Stripe. Check where data is hosted (choose an EU/UK Supabase region).
- [ ] **Charging VAT on your own subscriptions** once your turnover passes the threshold. Stripe Tax can help.
- [ ] **Trademark check** on the name "InvoiceFlow" (UK IPO search) — similar names may already exist.

## 3. Stage 1 data notice

Stage 1 stores data in the visitor's browser only. Nothing is sent to a server, so there is no personal data processing on your side yet. This changes in Stage 3. Have the privacy policy ready before then.
