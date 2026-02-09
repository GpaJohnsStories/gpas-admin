# GPAS Shop Design Guide
Last Update: 2026-02-09 @ 1:10 pm

## Purpose of this guide

This document defines the design intent, structure, and boundaries for **gpasshop.com**.

It builds directly on the shared principles defined in  
**all-sites-general-design.md** and describes how those principles are expressed when offering physical products.

This guide is intentionally high-level so it can remain valid even as layouts, features, and content evolve.

---

## The role of the shop

The GPAS shop exists to offer products that are meaningfully connected to the GPAS world.

At present, this includes products related to:
- **gpaskids.com**
- **gpasfaith.com**

The shop is designed to grow naturally as the GPAS world grows.

Products are introduced through suggestion and conversation, not pressure or persuasion.

---

## What is a “product” in the GPAS world?

In the GPAS world, a product is not an impulse item or a sales target.

A product is a **physical extension of the ideas, values, and tone** found across the GPAS websites.

Products are presented calmly and honestly, with enough context for a visitor to decide whether an item feels right for them — or not.

---

## Core product categories

### T-shirts

T-shirts are offered for:
- children
- teens
- adults
- seniors

They may be:
- fun
- affirmative
- faith-based

T-shirts are treated as expressive items, meant to communicate encouragement, joy, or belief in a gentle and approachable way.

---

### Books and Bibles

Books and Bibles are offered for:
- children
- teens
- adults
- seniors

They may be:
- fun
- affirmative
- faith-based

Books are treated as companions rather than commodities — items meant to be read, shared, revisited, and passed along.

---

### Other Stuff

“Other Stuff” includes items that support togetherness, creativity, and shared experience, such as:
- non-electronic games
- kits for building or making things together
- other physical items that feel like a natural fit for the GPAS world

Electronic games and purely digital experiences are intentionally excluded.

---

## What a product is not

A GPAS product is never:
- urgent
- manipulative
- trendy for its own sake
- designed to create pressure or fear of missing out

The shop does not attempt to convert visitors into buyers.

---

## The shop as a library

The GPAS shop is best understood as a **library** — or as a display room filled with good things that can be brought out from the back room when someone shows interest.

This concept applies across all GPAS public sites:
- the shop offers products
- kids offers stories
- faith offers verses, readings, and reflections

Each site is built around directories of items presented in a way that encourages browsing without pressure.

---

## The home page experience

The shop home page should feel like walking into a small, welcoming store.

There is:
- no large header bar
- no traditional navigation menu
- no visual pressure to “start shopping”

Orientation comes first. Conversion is never the goal.

---

## Home page layout (desktop reference)

The entire home page is treated as one unified display surface.

### Main Row 1
- Column 1: highlighted product
- Column 2: welcoming image of Grandpa John’s shop
- Column 3: blackboard with a short welcome note
- Column 4: primary display window

### Main Row 2
- Columns 1–3: sorting, filtering, and search instructions
- Column 4: continuation of the display window

### Main Rows 3 and 4
- Columns 1–3: product thumbnails
- Column 4: continuation of the display window

---

## Product cards as standalone files

Each product is represented by a standalone HTML file stored in the `prod/` directory.

These files are self-contained product cards designed to be loaded into the display window.

---

## Product code and file naming

Each product card file uses a seven-character product code:

