# Architecture Decisions: Search, Sort, Filter, and Analytics

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

### Example Index Structure
```json
[
  {
    "code": "FBF-004",
    "title": "Footprints Bookmark",
    "author": "Mary Stevenson",
    "price": 3.99,
    "tags": ["bookmark", "inspirational", "beach"],
    "created": "2024-01-15",
    "url": "/prod/FBF-004.html"
  }
]

