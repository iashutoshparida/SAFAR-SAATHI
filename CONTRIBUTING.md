# Contributing to SAFAR SAATHI

Thanks for helping keep the data accurate. Bank lounge policies change frequently — contributions are what make this tool useful.

\---

## What you can contribute

* **Update an existing card** — spend conditions changed, visit caps updated, access program switched
* **Add a new card variant** — a card that isn't listed yet
* **Add a new bank / issuer** — an issuer not currently covered
* **Fix a lounge** — wrong terminal, wrong network acceptance, new lounge opened
* **Add an airport** — a domestic airport not currently listed

\---

## File structure

All data lives in the `data/` folder:

```
data/
  cards.json      ← card variants and eligibility per card
  airports.json   ← airports, lounges, and network acceptance per lounge
  \_snapshots/     ← timestamped history of every validated version (auto-managed)
```

Do not edit `index.html` for data changes — all data lives in the JSON files.

\---

## cards.json structure

The file has two top-level keys: `cards` and `eligibility`.

### `cards`

A map of issuer name → array of card variant names.

```json
"HDFC Bank": \[
  "Infinia (Metal)",
  "Regalia Gold",
  "Regalia"
]
```

### `eligibility`

A map of `"Issuer::Card Name"` → eligibility object.

```json
"HDFC Bank::Regalia Gold": {
  "status": "yes",
  "domestic\_visits": "12/year",
  "intl\_visits": "6/year (Priority Pass)",
  "spend\_req": null,
  "access\_via": "Priority Pass + DreamFolks",
  "last\_verified": "2026-03",
  "notes": \[
    "Priority Pass for international",
    "DreamFolks for domestic"
  ]
}
```

**Field reference:**

|Field|Type|Values|
|-|-|-|
|`status`|string|`"yes"` / `"partial"` / `"no"`|
|`domestic\_visits`|string|e.g. `"8/year"`, `"2/quarter"`, `"Unlimited"`, `"None"`|
|`intl\_visits`|string|same format as above|
|`spend\_req`|string or null|e.g. `"₹50,000/quarter"` or `null`|
|`access\_via`|string|e.g. `"DreamFolks"`, `"Priority Pass + DreamFolks"`|
|`last\_verified`|string|`"YYYY-MM"` format — set this to the current month|
|`notes`|array of strings|Any caveats, conditions, or useful info|

**Status values and what they mean in the app:**

|JSON value|App label|Meaning|
|-|-|-|
|`"yes"`|🟢 Eligible|Walk in — no spend conditions|
|`"partial"`|🟡 Conditional|Spend threshold, voucher required, or domestic-only|
|`"no"`|🔴 No Access|Card has no lounge benefit|

\---

## airports.json structure

A map of IATA code → airport object.

```json
"BLR": {
  "name": "Bengaluru (Kempegowda)",
  "lounges": \[
    {
      "name": "Plaza Premium Lounge",
      "terminal": "T2",
      "networks": \["visa", "mastercard", "rupay", "amex", "priority\_pass", "dreamfolks"]
    }
  ]
}
```

**Valid network values:** `visa`, `mastercard`, `rupay`, `amex`, `diners`, `priority\_pass`, `dreamfolks`

\---

## How to submit an update

1. Fork this repo
2. Edit `data/cards.json` or `data/airports.json`
3. Set `last\_verified` to the current month (`"YYYY-MM"`)
4. Include a source link in your pull request description (bank website, DreamFolks page, etc.)
5. Submit the pull request

\---

## Validation

The maintainer runs a local validator before merging any PR. It checks:

* JSON is valid and correctly structured
* All required fields are present with correct types
* `status` is one of `yes`, `partial`, `no`
* `last\_verified` is in `YYYY-MM` format
* Every card in `eligibility` has a matching entry in `cards` and vice versa
* Airport lounge networks use only valid values

If your PR fails validation it will not be merged until fixed. If you want to self-check before submitting, clone the repo and open an issue asking for the validator script.

\---

## Keeping data fresh

Each eligibility entry has a `last\_verified` field. If you notice an entry is outdated (more than 6 months old), please verify and update it even if the underlying data hasn't changed — just update the date to confirm it's still accurate.

\---

## Questions?

Open an issue if you're unsure about anything before submitting.

