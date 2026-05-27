# SAFAR SAATHI

**Know before you go.** Check if your Indian credit or debit card gets you into the airport lounge — before you're standing at the door.


## The problem

Millions of Indians waste time at airport lounges trying to figure out if their card qualifies. The staff swipe, the machine beeps, nobody knows why. This tool solves that before you even leave home.

## What it does

- Add your credit and debit cards to a wallet — wallet persists across sessions
- Pick your departure airport
- Instantly see which cards grant lounge access, which are conditional, and which don't work
- View visit limits, spend conditions, and access programs (Priority Pass, DreamFolks, LoungeKey, RuPay, Visa, etc.)
- See which lounges are at your airport, which terminal they're in, and which networks each accepts

## Coverage

**Banks / Issuers:** American Express · AU Small Finance Bank · Axis Bank · Federal Bank · HDFC Bank · ICICI Bank · IDFC FIRST Bank · IndusInd Bank · Kotak Mahindra Bank · Priority Pass · RBL Bank · SBI Card · Standard Chartered · Yes Bank

**Airports:** AMD · BLR · CCU · COK · DEL · GAU · GOI · HYD · IXC · JAI · LKO · MAA · BOM · PNQ · TRV

**Access programs tracked:** Priority Pass · DreamFolks · LoungeKey · Visa lounge · Mastercard lounge · RuPay lounge · Amex Centurion · Diners Club

## How to use

1. Open the app
2. Select your bank / issuer and card variant, add it to your wallet
3. Repeat for all your cards
4. Pick your airport and hit **Check Eligibility**
5. See your results — eligible, conditional, or no access

## Status legend

| Status | Meaning |
|--------|---------|
| 🟢 Eligible | Walk in — no conditions |
| 🟡 Conditional | Spend threshold or voucher required |
| 🔴 No Access | This card has no lounge benefit |

## Data

Card and airport data lives in two open JSON files in the `data/` folder — anyone can read, fork, or submit a pull request to update them. See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide.

The app fetches live data from GitHub on every load, with a bundled fallback for offline use. Data was last compiled from public bank disclosures, DreamFolks, Priority Pass, and card network program pages — March 2026.

Lounge policies, spend thresholds, and visit caps change frequently. Always verify with your bank or card issuer before travel.

## Tech

Single-file static HTML app (`index.html`). No backend, no database, no login, no ads. Card and airport data is maintained in `data/cards.json` and `data/airports.json` and fetched at runtime. Works offline using bundled data. Wallet persists in browser localStorage.


