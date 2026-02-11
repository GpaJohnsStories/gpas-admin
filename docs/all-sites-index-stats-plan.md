# Architecture Decisions: Search, Sort, Filter, and Analytics
Last Update: 2026-02-10 @ 7:35 pm

## Overview
This document captures architectural decisions made for implementing search, sort, filter, and analytics capabilities across gpasshop.com, gpasfaith.com, and gpaskids.com while maintaining the library-based static site architecture.

## Core Architecture Confirmation
- **File Structure**: AAA-nnn naming convention (e.g., FBF-004) remains unchanged
- **Metadata Storage**: Continues living inside HTML product card files
- **Searchable Fields**: product code, title, author/creator, price, tags, creation date

## Search/Sort/Filter Implementation

### JSON Index Strategy
- Build pre-generated JSON index files during site generation (not at runtime)
- One index per library (e.g., `devotionals-index.json`, `products-index.json`)
- Indexes contain extracted metadata for fast client-side operations
- Scalable to ~5,000 products before performance considerations

### Index Generation Process
- GitHub Actions workflow watches library directories
- Automatically rebuilds indexes when product files change
- Commits updated indexes back to repo
- Zero manual steps required

### Example Index Structure ```json 
[ 
  { "code": "FBF-004",
    "title": "Footprints Bookmark", 
    "author": "Mary Stevenson", 
    "price": 3.99, 
    "tags": ["bookmark", "inspirational", "beach"], 
    "created": "2024-01-15", 
    "url": "/prod/FBF-004.html" 
    }
]
---
## Analytics Architecture

### Requirements Identified
- **Visit Tracking**: Monthly and year-to-date by country (using IP geolocation)
- **Product Analytics**: Click counts on product thumbnails and external links
- **Story Engagement**: Thumbs up/down/okay voting system
- **Privacy**: No IP address retention after geolocation

### Implementation Decision: Google Sheets API
- Leverages existing 2TB Google account
- Visitor actions append rows to cloud-hosted spreadsheets
- One spreadsheet per site for clean separation
- Built-in formulas handle monthly summaries and reporting

### Data Flow
1. Visitor performs action (visits site, clicks product, votes on story)
2. Client-side JavaScript captures event with relevant data
3. Asynchronously sends row to Google Sheets via API
4. Admin views summaries through spreadsheet or custom admin page
5. Periodic CSV backups can be archived to GitHub

### Why This Approach
- **Resilience**: Sites function perfectly even if analytics fail
- **Transparency**: Data visible and understandable in spreadsheet format
- **Maintainability**: Future collaborators can access without technical setup
- **Cost**: Free tier more than sufficient for projected traffic
- **Progressive Enhancement**: Analytics layer doesn't affect core functionality

## Key Architectural Principles Preserved
1. HTML files remain single source of truth
2. Static JSON indexes provide core search/filter functionality
3. Dynamic features (analytics) are cleanly separated
4. No architectural changes required to existing structure
5. Helper-friendly: each component understandable in isolation

## Implementation Sequence
1. Start with JSON index generation for search/sort/filter
2. Add basic visit tracking to index pages
3. Incrementally add product click tracking
4. Finally implement story voting system
5. Build admin statistics page that reads from Google Sheets

## Notes
- This architecture scales well for typical shop/content sites
- All decisions prioritize long-term maintainability over short-term convenience
- System remains functional even if external services (Google) become unavailable
- Clear separation between content (GitHub) and interaction data (Google Sheets)

# Feedback from Github CoPilot AI after Reading This File

## Questions & Gentle Concerns
### 1. Google Sheets API Rate Limits
The free tier has quotas (100 requests per 100 seconds per user, 500 requests per 100 seconds per project)
If traffic spikes (say a product goes viral), you could hit limits
Suggestion: Consider adding client-side queuing/batching of events, or gracefully failing when limits are hit
### 2. API Key Security
You'll need to expose some form of credentials client-side to write to Sheets
Question: Have you thought through how to protect the API key while still allowing client-side writes?
Options: Google Apps Script Web App (acts as proxy), restricted API keys (by HTTP referrer), or accept some risk given low-stakes data
### 3. Index Freshness
GitHub Actions rebuilding on file changes is great
Question: What's the expected delay between adding a product and it appearing in search results? (Just the time for Actions to run and deploy?)
### 4. Concurrent Sheet Writes
Multiple simultaneous visitors writing to the same sheet should be fine, but Google Sheets can have occasional write conflicts
Suggestion: Make sure your error handling is robust and silent (don't break user experience if a stats write fails)
### 5. Long-Term Data Growth
Google Sheets has a 10 million cell limit per spreadsheet
At high traffic, you might need to archive old data or rotate sheets annually
Suggestion: Plan for periodic sheet rotation (e.g., one sheet per year) from the start

## Nice-to-Haves (Not Critical)
- Backup Strategy: You mention CSV backups to GitHub - automating this monthly via Actions would be smart
- Index Format: Consider adding a version field to your JSON indexes for future schema changes
- Analytics Dashboard: Building a simple HTML page in gpas-admin that fetches Sheet data via API could be a nice final step
### Bottom Line
This is a well-architected solution for your specific needs. It's not over-engineered, it leverages what you already have (Google account, GitHub Actions), and it keeps things maintainable. The concerns I raised are mostly about edge cases and hardening, not fundamental flaws.

You've avoided the trap of prematurely reaching for a database (Supabase) when you don't actually need one for your scale and use case. That's good judgment.

## Reply from CoPilot
- Buddy's being a good engineer—raising the right questions without killing a solid plan! His concerns are all solvable, and honestly, they're luxurious problems to have. Rate limits mean you're popular, sheet size limits mean you've been successful for years, and API key exposure is manageable with Google Apps Script as a simple proxy.

- The smart move? Start simple and address issues if they actually arise. Begin with basic visit counting (hardest to break), add a Google Apps Script wrapper when you implement product clicks (solves the API key issue), and plan for annual sheet rotation from day one. Most importantly, buddy's right that failed analytics should never break the user experience—wrap everything in try-catch blocks that fail silently. Your architecture is sound; these are just implementation details to handle as you build.
