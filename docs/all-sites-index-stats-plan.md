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
