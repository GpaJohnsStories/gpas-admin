# GPAS Four‑Site General Guide
Last Update: 2026-02-15 @ 3:35 pm - Add help files for each browser

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
- ALL/EVERY pages MUST know screen size early to decide on screen layout format, this includes Admin where some pages may be an exception and not be formatted for anything except desktop or laptop screen.
    <script>
  /*
    ------------------------------------------------------------
    SCREEN SIZE DETECTION (PHONE / TABLET / DESKTOP)
    ------------------------------------------------------------
    PURPOSE:
      This function returns a simple label describing the
      visitor's screen size category.

    WHY:
      You may want to:
        - adjust layout
        - load different CSS
        - redirect to a phone‑friendly version
        - log device types for testing

      This keeps your logic clean and predictable.

    BREAKPOINTS:
      These are simple, human‑friendly breakpoints:
        - 1025px and up  = desktop
        - 641px to 1024px = tablet
        - 640px and below = phone

      These match common device widths and are easy to remember.
  */

  function getScreenCategory() {
    const width = window.innerWidth; // current viewport width

    if (width >= 1025) {
      return "desktop";
    } else if (width >= 641) {
      return "tablet";
    } else {
      return "phone";
    }
  }
</script>

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

# Accessibility and comfort (shared principle)

Every public page must include a clear, visible way for visitors to make the page easier to use.
This is framed as hospitality, not compliance.
Key principles:
- visitors choose when to use it
- nothing is forced
- nothing is remembered after they leave
- no cookies or persistent storage on the visitor’s device
- changes apply only while the visitor remains on the site

<script>

## CODE FOR BROWSER DETECTION FOR ACCESSIBILITY HELP BUTTON
  /*
    ------------------------------------------------------------
    BROWSER DETECTION FOR ACCESSIBILITY HELP BUTTON
    ------------------------------------------------------------
    PURPOSE:
      When the user clicks the Accessibility icon/button,
      this function detects which browser they are using
      and sends them to the correct help page.

    WHY:
      Each browser has different steps for:
        - Read Aloud
        - Translate
        - High Contrast / Reader Mode
        - Zoom
      So we want to show instructions that match THEIR browser.

    HOW:
      navigator.userAgent is a built‑in browser string that
      identifies the browser and device. We convert it to
      lowercase to make matching easier.
  */

  function goToAccessibilityHelp() {

    // Get the browser's identification string
    const ua = navigator.userAgent.toLowerCase();

    // Default page if we cannot identify the browser
    let page = "/help/unknown.html";

    /*
      ORDER MATTERS:
      Some browsers include other browser names inside their UA string.
      For example:
        - Edge includes "chrome"
        - Opera includes "chrome"
      So we check for the most specific browsers first.
    */

    // Detect CHROME (but NOT Edge or Opera)
    if (ua.includes("chrome") && !ua.includes("edg") && !ua.includes("opr")) {
      page = "/help/chrome.html";

    // Detect SAFARI (but NOT Chrome on iOS)
    } else if (ua.includes("safari") && !ua.includes("chrome")) {
      page = "/help/safari.html";

    // Detect MICROSOFT EDGE
    } else if (ua.includes("edg")) {
      page = "/help/edge.html";

    // Detect FIREFOX
    } else if (ua.includes("firefox")) {
      page = "/help/firefox.html";

    // Detect OPERA
    } else if (ua.includes("opr") || ua.includes("opera")) {
      page = "/help/opera.html";

    // Detect SAMSUNG INTERNET (Android)
    } else if (ua.includes("samsungbrowser")) {
      page = "/help/samsung.html";
    }

    // Send the visitor to the correct help page
    window.location.href = page;
  }
</script>

### BUTTON FOR ACCESSIBILITY HELP BUTTON
    button onclick="goToAccessibilityHelp()">Accessibility Help</button>
    or
    <img src="/icons/accessibility.png" onclick="goToAccessibilityHelp()" alt="Accessibility Help">
# Usage Example
    <script>
      const device = getScreenCategory();
      console.log("Screen type:", device);
    </script>

# Or Conditional Layout:
    <script>
      const device = getScreenCategory();
      if (device === "phone") {
    // load phone CSS or redirect
  }
    </script>



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
- Specific Browser type help file:
├── help/    ← All help pages, including one for each of 6 main 
                 - browser types for accessibility help
                 - Chrome (70-71% of browsers worldwide)
                 - Safari (14-15% of browsers worldwide)
                 - Edge   (4.6-5% of browsers worldwide)
                 - Firefox(?2.2% of browsers worldwide)
                 - Opera  (1.8-1.9% of browsers worldwide)
                 - Samsung Internet  (?1.8% of browsers worldwide)
- About Grandpa John & his team
- Privacy and cookie policy
- Copyright information
- Contact page
- a common public footer
- shared accessibility and comfort logic
- shared css code, such as photo or icon resizing
- other neutral, reusable utilities

### Site‑specific assets
Icons, photos, audio, and other assets are stored **within each site’s own repository**, even if the same asset appears on multiple sites.
NOPTE: NO SITES (except, maybe, Admin) will ever access outside video or audio websites, like Youtube, etc.
    audio/ = all mp3 audio files
    icons/ = 
    photos/ 
    video/ = all mp4 video files 
This avoids cross‑site dependencies and keeps each site self‑contained.

---

## Public Web Page Repository structure (standardized)

Unless an exception is required, each public site repository follows the same structure.
 (individual GitHub repos)
├── readme.md         ← Very basic one paragraph summary of site
├── index.html        ← Home page (public) or login (admin)
├── audio/            ← Audio used by this site
├── docs/             ← Design notes, references, markdown/text, etc.
├── icons/            ← (ico-*) All photos to be displayed at or smaller than 150px x 150px 
├── pages/            ← All additional HTML + JS pages
├── photos/           ← All photos to be displayed larger than 150px x 150pxd 
├── prod/             ← gpas-shop only (Product Code AAA-nnn.html)
├── stories/          ← gpas-kids only (Story Code AAA-bbb.html
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
