# GPAS Four‑Site General Guide
Last Update: 2026-02-08 @ 1:54 pm

## Purpose of this guide

This document defines the shared vision, structure, and boundaries for four related websites:

- **gpaskids.com**
- **gpasfaith.com**
- **gpasshop.com**
- **gpasadmin** (private, GitHub‑hosted, no public domain)

It establishes how the sites relate to one another, who they are for, and the principles that guide all technical and design decisions.

This guide is intentionally high‑level so it can remain valid even as individual pages, features, and layouts evolve.

---

## The shared concept

All four sites belong to one family.

The three public sites should feel like different rooms in the same house — familiar, safe, and welcoming — while the admin site is the quiet back room where the work gets done.

The emotional model for the public sites is:

> *Sitting in Grandpa John’s living room, listening to stories, or talking neighbor‑to‑neighbor over the back fence.*

This implies:
- no pressure
- no judgment
- no urgency
- no manipulation
- no obligation to stay

Visitors should feel free to browse, linger, or leave without explanation.

---

## The four sites at a glance

### gpaskids.com
- **Purpose:** stories and gentle learning for children and families
- **Tone:** warm, playful, reassuring
- **Primary audience:** children, parents, grandparents and teachers
- **Key value:** safety and trust and fun

### gpasfaith.com
- **Purpose:** faith‑related reflections, verses, and lived wisdom
- **Tone:** calm, invitational, non‑judgmental
- **Primary audience:** adults, late teens and seniors seeking encouragement or understanding
- **Key value:** respect for where the reader is

### gpasshop.com
- **Purpose:** offer products connected to the GPAS world
- **Tone:** honest, neighborly, unhurried
- **Primary audience:** thoughtful buyers and gift‑givers
- **Key value:** clarity and trust

### gpasadmin
- **Purpose:** manage content, structure, and publishing for the other three sites
- **Tone:** practical and clear
- **Audience:** a single admin user
- **Hosting:** GitHub repository only, never tied to a public domain
- **Key value:** simplicity and control

---

## Expected devices and usage patterns

### Public sites
- **Primary device:** tablet
- **Secondary device:** phone
- **Last priority:** desktop/laptop

Design assumptions:
- pages must work comfortably on tablets first
- phone layouts must remain readable and touch‑friendly
- desktop layouts should feel intentional but never required
- ALL PAGES, without any exceptions, MUST allow viewer to pinch-zoom
    using this code or something similar:
    <meta name="viewport" content="width=device-width, initial-scale=1">


### Admin site
- **Required device:** desktop or laptop
- Tablets and phones are not supported for admin work

---

## Accessibility and comfort (shared principle)

Every public page must include a clear, visible way for visitors to make the page easier to use.

This is framed as hospitality, not compliance.

Key principles:
- visitors choose when to use it
- nothing is forced
- nothing is remembered after they leave
- no cookies or persistent storage on the visitor’s device
- changes apply only while the visitor remains on the site

The exact controls may evolve, but the intent does not:
- easier reading
- reduced strain
- gentle pacing
- easy listening
---

## Design consistency across public sites

The three public sites should feel related without being identical.

Shared elements:
- similar page structure
- similar typography scale
- similar navigation patterns
- similar accessibility controls
- similar tone of voice

Allowed differences:
- color palettes
- imagery
- content density
- emphasis (stories vs. verses vs. products)

A visitor should never feel lost moving from one site to another.

---

## Content philosophy

Content is:
- human‑written
- calm
- respectful
- not optimized for shock or outrage
- not written to trap attention

Each page should quietly answer:
- “What is this?”
- “Who is this for?”
- “What can I do here?”

And then get out of the way.

---

## Technical boundaries (shared across all sites)

These are guardrails, not restrictions for their own sake.

- Sites are static and GitHub‑hosted.
- Content lives in files, not databases.
- HTML and JavaScript are the primary tools.
- CSS is used only when it is the clearest, most honest solution.
- Code is heavily commented and clearly flagged.
- Structure is predictable and readable.
- No third‑party frameworks that obscure understanding.

The goal is:
> *Future‑you can open any file and understand what’s going on.*

---

## Privacy posture

Across all public sites:
- no cookies
- no persistent identifiers stored on the visitor’s device
- no behavioral profiling
- no dark patterns

Any analytics or counting is:
- coarse
- respectful
- used for understanding reach, not individuals

---

## Shared code and assets

### Common code
This repo contains pages used by all three public sites, such as:
- About Grandpa John & his team
- Privacy and cookie policy
- Copyright information
- Contact page
- a common public footer
- shared accessibility and comfort logic
- shared css code, such as photo or icon resizing
- other neutral, reusable utilities

Public sites may link to these pages as needed.

*** Photo Size Names for common sizes of photos to be created by the common photo css code
Photo Sizes
├── sizeP   ← Primary / Promo
│            Featured cards, hero items, main product or story tiles
│            Square display; image scales to fit container
│
├── sizeA   ← Auxiliary / All‑Other
│            Thumbnails, search results, filtered lists
│            Smaller square display for visual rhythm
│
├── sizeS   ← Spotlight / Story
│            Large emphasis images, story highlights, detail views
│            Large square display used sparingly
│
└── sizeT   ← Tall
             Full product cards, reading‑flow images
             Fixed max width; height adjusts naturally

*** Icon Size Names for common sizes of icons to be created by the common icon css code
Icon Sizes
├── iconS   ← Small UI Icon
│            Inline controls, subtle indicators
│            Fixed visual size; unobtrusive
│
├── iconM   ← Medium / Touch Icon
│            Primary buttons, accessibility controls
│            Touch‑friendly and clear
│
├── iconL   ← Large / Feature Icon
│            Emphasis icons, section markers
│            Visually prominent without overpowering
│
└── iconX   ← Reserved / Future
             Placeholder for special cases
             Allows expansion without renaming


### Site‑specific assets
Icons, photos, audio, and other assets are stored **within each site’s own repository**, even if the same asset appears on multiple sites.

This avoids cross‑site dependencies and keeps each site self‑contained.

---

## Repository structure (standardized)

Unless an exception is required, each site repository follows the same structure.
 (individual GitHub repos)
├── readme.md         ← Guidance for building this particular site 
├── index.html        ← Home page (public) or login (admin)
├── audio/            ← Audio used by this site
├── docs/             ← Design notes, references, markdown/text
├── icons/            ← Small icons (ico-*)
├── pages/            ← All additional HTML + JS pages
├── photos/           ← Large images
├── prod/             ← gpas-shop only (cards/, audio/)
├── stories/          ← gpas-kids only
└── readings/         ← gpas-faith only (articles, verses, prayers)

---

## Relationship between the sites

- The three public sites may link to one another naturally.
- None of them should depend on another to function.
- The admin site supports all three but is never visible to the public.

Each site stands on its own, but together they tell a larger story.

---

## What this guide is — and is not

This guide **is**:
- a shared vision
- a set of values
- a stable reference point

This guide is **not**:
- a coding manual
- a feature checklist
- a final design specification

Those documents may exist separately and evolve over time without changing the intent defined here.
