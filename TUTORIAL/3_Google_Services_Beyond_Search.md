# 3 — Google Services Beyond Search

The main search engine is one piece. Google's ecosystem covers geospatial intelligence, academic research, patent analysis, temporal trend data, and passive monitoring — each with distinct OSINT applications.

## Google Images — Reverse Image Search

Go to [images.google.com](https://images.google.com) and click the camera icon. Upload a file or paste a URL.

**What it tells you:**
- Where else the image appears on the web
- Earlier versions of the same image (useful for detecting manipulated or reused photos)
- Visually similar images that may provide context
- Sites that have republished the image

**OSINT workflow for image verification:**
1. Reverse search the image
2. Check if results include credible news sources
3. Look for the oldest indexed version — if a "breaking news" image predates the event, it's recycled
4. Download the earliest version and extract EXIF data: `exiftool image.jpg`
5. Use visual landmarks (buildings, signs, vegetation, vehicles) to cross-reference with Maps

EXIF data often gets stripped when images are uploaded to social media, but the original source may retain it.

## Google Maps and Street View

**Geocoding:** Search any address, place name, or coordinate pair (`40.4168, -3.7038`).

**Reverse geocoding:** Right-click any map point to get coordinates or the nearest address.

**Street View:** Ground-level imagery for physical reconnaissance. Check the capture date (bottom-left) — Google updates coverage irregularly, so some areas are years old.

**Historical imagery:** In Google Earth Pro (free desktop download), use the clock icon to view satellite imagery from different dates at the same location. Useful for tracking construction, infrastructure changes, or vehicle presence over time.

**OSINT applications:**
- Verify a business address before a field investigation
- Assess physical security of a facility from public imagery
- Confirm a location claimed in an image by matching visual features
- Track changes to a site over time using historical satellite imagery
- Identify building entrances, camera positions, and vehicle access points

## Google Scholar — [scholar.google.com](https://scholar.google.com)

Academic paper search. Uses similar operator syntax to the main search engine.

```
# Papers by a specific author
author:"Bruce Schneier"

# Papers from a specific institution
"MIT" "machine learning" site:scholar.google.com

# Papers citing a specific work
cites:[article ID from Scholar URL]
```

**OSINT applications:**
- Build profiles of technical experts and researchers
- Map institutional affiliations
- Identify co-authors and research networks
- Find pre-publication versions of papers

## Google Patents — [patents.google.com](https://patents.google.com)

Full-text patent search with inventor, assignee, and date filters.

```
# Patents by a company
assignee:"Palo Alto Networks"

# Patents by an inventor
inventor:"John Smith" assignee:"Company Name"

# Patents on a technology
"neural network" "intrusion detection" before:2020
```

**OSINT applications:**
- Map a company's R&D direction and technology priorities
- Identify key engineers and researchers by name
- Trace relationships between companies through shared inventors or cross-licensing
- Find technical details on proprietary systems described in patents

## Google Trends — [trends.google.com](https://trends.google.com)

Relative search interest for terms over time and by geography.

**OSINT applications:**
- Verify when public interest in a topic or person spiked (correlate with events)
- Compare brand recognition across regions
- Detect emerging topics before they appear in mainstream news
- Track search interest around a specific incident or disclosure

Trends shows relative popularity, not absolute volume. Use it for comparison and timing, not absolute measurement.

## Google Alerts — [google.com/alerts](https://google.com/alerts)

Passive monitoring — receive email or RSS notifications when new content matching a query gets indexed.

Supports the same operator syntax as search:

```
# Monitor mentions of an organization
"Company Name" -site:company.com

# Monitor for credential leaks
"Company Name" password | credential | "api key"

# Monitor a person in news
"First Last" CEO | "chief executive" site:reuters.com | site:ft.com

# Monitor new files about a topic
"topic keyword" filetype:pdf
```

**Setup:** Go to google.com/alerts, enter your query, choose frequency (as-it-happens, daily, weekly), and delivery method (email or RSS).

Alerts are passive — content must be newly indexed to trigger. They won't catch existing content and may miss content on sites Google indexes infrequently.

## YouTube

Owned by Google. Searchable with standard operators from the main search engine.

```
# Find videos mentioning a term in title
intitle:"Company Name" site:youtube.com

# Combine with date filters in Google Search Tools
site:youtube.com "topic" after:2024-01-01
```

**Within YouTube itself:**
- Use the Filters panel to sort by upload date, duration, and type
- Auto-generated transcripts are searchable — click the `...` menu on a video and select "Show transcript"
- Check video descriptions and comments for additional context, links, and usernames
- Pinned comments and community posts on channels often contain additional information

**Geolocation from video content:**
1. Pause on frames with visible buildings, signs, or infrastructure
2. Cross-reference with Google Maps satellite and Street View
3. Check the video description for location tags
4. Use the video's upload metadata as a temporal anchor

---

Continue to [4 — Practical Scenarios & Cheatsheet](4_Practical_Scenarios_Cheatsheet.md)
