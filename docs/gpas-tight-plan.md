# GPAS content security and validity plan
Last Updated: 02/11/2026 @ 11:48 am

This plan defines a single **content contract** and enforces it in three places:

1. **shop-prod-format.html** (authoring gatekeeper)
2. **JSON index builder** (integrity auditor)
3. **shop index.html** (runtime civility + safe rendering)

The goal is simple: **normalize once, validate everywhere, fail loudly in admin/build, respond gently at runtime**.

---

## Definitions

- **Product HTML file:** A single product’s source-of-truth HTML in the shop repo.
- **Index JSON file:** The generated index used by `shop index.html` for listing/search.
- **Contract:** The required fields, formats, and permitted content rules below.
- **Bad word list:** A maintained list of disallowed words/phrases (publicly readable if stored in a public repo; write-protected by GitHub permissions).

---

## Shared contract rules

### Required fields and where they must exist

Every product must provide these fields:

- **Product code:** `data-code` (attribute)
- **Search title:** `data-title` (attribute)
- **Author or version:** `data-author` (attribute)
- **Price:** `data-price` (attribute)
- **Tags:** `data-tags` (attribute)
- **Date:** `data-date` (attribute)
- **Display title:** `<h3>` text content (element content)
- **Product link URL:** href or equivalent field used for product link (must not be blank)
- **Product image URL:** src or equivalent field used for product image (must not be blank)

#### Blank-allowed fields
These fields may be blank but must still exist:

- **data-author:** may be `""` (empty string)
- **data-price:** may be `""` (empty string)

> Contract note: for blank-allowed fields, store empty as `""` (preferred) rather than `" "` (space). Spaces should be treated as invalid and normalized to empty by the formatter, and flagged by the index builder.

---

## Product code standard

### `data-code` must match

Pattern:

- **Position 1:** `F` or `H`
- **Position 2:** `T`, `B`, or `O` (letter O)
- **Position 3:** `K`, `F`, or `S`
- **Position 4:** `-`
- **Positions 5–7:** exactly three digits `000`–`999`

Example: `FBF-004`

### Uniqueness rule

For all product files sharing the same first four characters (example: `FBF-`), positions 5–7 must be **unique**.

- Duplicate code within the same prefix group is an **ERROR**.

---

## Title rules

### Display title (`<h3>`)
- Must remain exactly as entered by the authoring tool.
- Must not contain bad words.
- May include punctuation, unusual capitalization, and emphasis (example: `Prayer, NOT Worry!`).

### Search title (`data-title`)
- Must be **all lowercase**.
- Must equal the display title lowercased (same characters, just lowered).
- Must not contain bad words.

---

## Tags rules

### `data-tags`
- Must exist and must not be blank.
- Must be **lowercase**.
- Must be **comma-separated**.
- Must contain **no spaces** (neither around commas nor inside tag tokens).
- Must not contain bad words.

---

## Price rules

### `data-price`
- Must exist.
- May be blank.
- If non-blank: must parse as a valid numeric currency-like value.

### High price confirmation (formatter only)
- In **shop-prod-format.html** only: if price is ≥ `100.00`, require explicit confirmation before save.

---

## URLs rules

### Product link URL
- Must exist.
- Must not be blank.
- Must appear valid: begins with `http://` or `https://`
- Must be scanned for banned substrings (see bad-word scanning rules).

### Product image URL
- Must exist.
- Must not be blank.
- Must appear valid: begins with `http://` or `https://`
- Must be scanned for banned substrings (see bad-word scanning rules).

---

## Description rules

The description must satisfy one of these two options:

### Option A: Placeholder
Must be **exactly**:

`No Description Is Currently Available.`

- Exact spelling
- Exact capitalization
- Exact punctuation

### Option B: Written description
- Must contain **at least 10 words**.
- Must not contain bad words.
- Must not contain unapproved HTML.
- Must not contain script-like or CSS-like content.

---

## Approved HTML tags in descriptions

Only these HTML tags are permitted in the description HTML:

- `<br>`
- `<b>`
- `<em>`
- `<i>`
- `<u>`
- `<p>`
- `<h1>`
- `<h2>`
- `<h3>`

Explicitly disallowed (non-exhaustive):
- `<div>`
- `<table>`
- `<script>`
- `<style>`
- `<iframe>`
- any inline CSS
- any JavaScript or event handlers (e.g., `onclick=...`)

> Contract note: treat **any** tag not on the approved list as an error, including custom elements.

---

## Bad-word scanning rules

### Scope
Bad-word scanning applies to **all text strings**, including:
- display title text
- `data-title`
- `data-author`
- `data-tags`
- description text and description HTML
- product link URL
- product image URL
- any other user-entered string field

### Matching rule
- Checks must be **case-insensitive**.
- Checks must detect banned words/phrases even when **concatenated** inside longer strings (including URLs and run-together words).
- Therefore: do **substring scanning** on a normalized copy of the text.

### Normalization for scanning
For scanning only (do not alter stored values):
- lowercase the string
- optionally collapse whitespace sequences to a single space for phrase checks
- optionally remove obvious separators for “run-together” detection (example: `-`, `_`, `.`) if desired for stricter matching

### Allowed words exceptions
Some words are explicitly allowed and must **not** be flagged:
- `hell`
- `damn`

> Implementation note: enforce “allowed words” as an exceptions list that is checked before rejecting a match.

### Bad-word list storage
Maintain the bad-word list and allowed-word exceptions in a single shared file in the admin repo (publicly readable if the repo is public).

- Readable by anyone does not imply writable by anyone.
- Only authorized users can change it via GitHub write permissions.

---

## Enforcement points

### 1) shop-prod-format.html (authoring gatekeeper)

#### Purpose
Prevent invalid content from ever being saved/committed.

#### Responsibilities
- Normalize input into contract-compliant values (especially `data-title`, `data-tags`, empty fields).
- Run the full validation suite described above.
- Show clear, human-readable errors that identify:
  - field name
  - failing rule
  - offending value (or excerpt)
- Block “save to GitHub” (or export) if any error is present.
- For high prices (≥ `100.00`), require explicit confirmation before save.

#### Failure behavior
- **Hard stop** on any validation error.
- No silent corrections except normalization steps the tool explicitly owns (example: lowercasing `data-title`).

---

### 2) JSON index builder (integrity auditor)

#### Purpose
Detect drift, manual edits, or contract violations before publishing the index.

#### Responsibilities
- Re-run the **same validation suite** against product HTML inputs.
- Enforce uniqueness rules (especially code uniqueness within prefix groups).
- Reject any file that violates the contract and stop the build.

#### Failure behavior
- **Hard stop**: do not generate an index JSON if any product file fails.
- Never auto-fix.
- Report errors with:
  - product filename
  - product code (if parseable)
  - field name
  - failing rule

---

### 3) shop index.html (runtime search and display)

Runtime behavior has two goals:
1. Keep the shopping experience welcoming and safe.
2. Avoid breaking the page due to bad inputs.

#### A) Search input civility enforcement
Before running search:

- Normalize the search input for checking (lowercase).
- Scan for banned substrings (same matching rule used elsewhere).
- If banned content is detected:
  - do not run the search
  - show a friendly message:

`Sorry, we don’t use some of those words here. Please use nicer words. Thank you.`

#### Strike counter behavior
- Keep an in-memory strike counter for invalid search attempts.
- Increment only when the user’s search input triggers the bad-word filter.
- On the 3rd strike:
  - disable the search input and search button for that page session
  - show message:

`You have 3 strikes with your search words. Sorry, but 3 strikes, like in Baseball, and you are OUT! Good-bye.`

Notes:
- This lockout is **session-only** (in-memory).
- Reloading the page or reopening the site resets strikes to zero.
- Do not attempt to close the browser or tab.

#### B) Data safety checks for rendering
- The index page may assume the JSON index was built by the validated builder.
- However, basic defensive checks may still be used to prevent runtime crashes (e.g., missing fields).
- If something critical is missing, display a generic fallback (or omit the item) without exposing details to users.

> Contract note: the primary enforcement for data integrity is admin + build. Runtime should remain user-friendly and stable.

---

## Error levels and messaging

### Admin/build errors
- Always specific and actionable.
- Include file/field/rule.
- Stop the operation.

### Runtime messages
- Always gentle and non-technical.
- Do not reveal the exact banned word list.
- Do not shame the user; simply set boundaries.

---

## Operational notes

- Treat the bad-word list as **policy**: editable by you, versioned in GitHub, and referenced by all three enforcement points.
- Keep the contract rules in a single “contract comments block” and copy it verbatim into:
  - shop-prod-format.html
  - JSON index builder
  so both stay synchronized.
- Any future field additions must update:
  - the contract
  - formatter validation
  - builder validation
  - runtime assumptions (only if needed)

---
