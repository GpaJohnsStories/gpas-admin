GPAS Shop Design Guide
Last Update: 2026‑02‑09

Purpose of this document
This document defines the design intent, structure, and behavior of gpasshop.com.

It builds directly on the shared principles defined in
all-sites-general-design.md and describes how those principles are expressed when offering physical products.

This guide focuses on meaning, flow, and boundaries, not implementation details.

What is a “product” in the GPAS world?
In the GPAS world, a product is not an impulse item or a sales target.
It is a physical extension of the ideas, values, and tone found across the GPAS websites.

The purpose of gpasshop.com is to offer products that are meaningfully connected to all other GPAS sites. At present, this includes gpaskids.com and gpasfaith.com, and the shop is designed to grow naturally as the GPAS world grows.

Products are introduced through suggestion and conversation, not pressure or persuasion. The shop exists to help visitors discover items that feel like a good fit for their family, their values, or their stage of life.

Core product categories
T‑shirts
Offered for children, teens, adults, and seniors.
They may be fun, affirmative, or faith‑based.

T‑shirts are treated as expressive items, meant to communicate encouragement, joy, or belief in a gentle and approachable way.

Books and Bibles
Offered for children, teens, adults, and seniors.
They may be fun, affirmative, or faith‑based.

Books are treated as companions, not commodities — items meant to be read, shared, revisited, and passed along.

Other Stuff
Includes items that support togetherness, creativity, and shared experience, such as:

non‑electronic games

kits for building or making things together

other physical items that feel like a natural fit for the GPAS world

Electronic games and purely digital experiences are intentionally excluded.

What a product is not
A GPAS product is never:

urgent

manipulative

trendy for its own sake

designed to create pressure or fear of missing out

The shop does not attempt to convert visitors into buyers.
It exists to offer clear, honest choices and then step back.

The shop as a library
The GPAS shop is best understood as a library — or a display room filled with good things that can be brought out from the back room when someone shows interest.

This concept applies across all GPAS public sites:

the shop offers products

kids offers stories

faith offers verses, readings, and reflections

Each site is built around directories of items presented in a way that encourages browsing without pressure.

The home page experience
The shop home page should feel like walking into a small, welcoming store.

There is:

no large header bar

no traditional navigation menu

no visual pressure to “start shopping”

Instead, the page offers:

clear instructions on how to use the site

a small number of highlighted items

visible thumbnails that invite exploration

Orientation comes first. Conversion is never the goal.

Home page layout (desktop reference)
The entire home page is treated as one unified display surface, implemented as a single flexible table.

Main Row 1
Column 1: highlighted product

Column 2: welcoming image of Grandpa John’s shop — early‑1900s style, bright, cared for, and comforting

Column 3: blackboard with a short welcome note from Grandpa John

Column 4: the primary display window, extending to the bottom of the screen

Main Row 2
Columns 1–3: blackboards explaining sorting, filtering, and searching

Column 4: continuation of the display window

Main Rows 3 and 4
Columns 1–3: thumbnail images of products

initially populated by most‑viewed items

clicking a thumbnail loads the product into the display window

columns are half‑width, allowing six items per row

Column 4: continuation of the display window

Tablet and phone layouts adapt from this structure.

Product cards as standalone files
Each product is represented by a standalone HTML file stored in the prod/ directory of the gpas-shop repository.

These files are self‑contained product cards, designed to be loaded into the display window.

They are modular, readable, and free from hidden dependencies.

Product code and file naming
Each product card file uses a seven‑character product code:

Code
AAA-nnn.html
Product code structure
Position 1 — Interest

F = Faith

H = Happy / Fun

Position 2 — Product type

T = T‑shirts

B = Books & Bibles

O = Other Stuff

Position 3 — Site family

K = gpaskids.com

F = gpasfaith.com

S = gpasshop.com

Position 4 — Separator

Always a dash (-)

Positions 5–7 — Sequence number

Automatically assigned

Based on existing files with the same first three characters

Starts at 001 if none exist

Metadata inside the product card
Each product card stores key information using data-* attributes on the <article> element, including:

product code

title

author or creator

price (if applicable)

tags or keywords

creation date

This metadata supports sorting, filtering, and searching without parsing visible content.

Product description
Descriptions are written by Grandpa John, with assistance from Copilot.

They are:

typically under 200 words

conversational and honest

focused on lived experience

Basic HTML formatting is allowed so descriptions can be dropped directly into the display window.

The display window (single, shared)
The shop contains one and only one display window.

All product exploration flows through this single, stable viewing area.

The display window:

has a fixed width aligned with the column system

has a fixed height defining the visible reading area

remains present even when empty

provides vertical scrolling when needed

never allows horizontal overflow

The page layout never shifts when a product is opened.

Separation of responsibilities
The table defines spatial relationships

The display window defines the viewing boundary

The product card provides content only

Product cards do not manage layout, scrolling, or positioning.

Call to action
Each product card ends with a single, clearly labeled button linking to the external retailer.

The button:

uses plain language

opens in a new tab

implies no urgency

The shop’s role ends here.
The decision to continue belongs entirely to the visitor.

What the shop deliberately avoids
The shop avoids:

urgency cues

countdowns

scarcity language

pop‑ups

forced navigation

behavioral tracking

Trust is earned by restraint.

Relationship to kids and faith
The shop establishes patterns that gpaskids.com and gpasfaith.com inherit:

library‑based browsing

single display window

calm discovery

content‑first presentation

Commerce does not lead the GPAS world.
It follows the same values.

Closing note
The GPAS shop is not a funnel.
It is a room.

Visitors are welcome to browse, linger, or leave — without explanation.
