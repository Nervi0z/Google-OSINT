<div align="center">
  <img src="./assets/img/header.svg" alt="google-osint" width="100%"/>
</div>

---

Practical guide to OSINT using Google and its ecosystem. Covers search operators, Google Dorking, reverse image search, geospatial intelligence via Maps and Street View, academic and patent research, and passive monitoring with Alerts.

Built for SOC analysts, threat intelligence researchers, investigators, and anyone who needs to find information efficiently using publicly available sources.

> All techniques described here apply to publicly accessible information. Use them responsibly, ethically, and within applicable law. This repository is for defensive and educational use.

---

## Contents

- [Quick Reference — Operators](#quick-reference--operators)
- [Tutorial Modules](#tutorial-modules)
- [Dork Cheatsheet](#dork-cheatsheet)
- [Practical Scenarios](#practical-scenarios)
- [Google Services Beyond Search](#google-services-beyond-search)
- [Ethics and Legal Boundaries](#ethics-and-legal-boundaries)
- [Contributing](#contributing)

---

## Quick Reference — Operators

The building blocks. Combine these to build precise queries.

| Operator | What it does | Example |
|----------|-------------|---------|
| `site:domain.com` | Restrict results to a specific domain | `site:gov.uk filetype:pdf` |
| `filetype:ext` / `ext:` | Find specific file types | `filetype:xlsx "budget 2024"` |
| `"exact phrase"` | Match a literal string | `"internal use only"` |
| `-term` | Exclude results containing a term | `jaguar speed -car` |
| `*` | Wildcard for unknown words in a phrase | `"the * most wanted"` |
| `OR` / `\|` | Either term A or term B | `CEO OR "chief executive"` |
| `intitle:term` | Term must appear in the page title | `intitle:"index of /"` |
| `inurl:term` | Term must appear in the URL | `inurl:admin inurl:login` |
| `intext:term` | Term must appear in the page body | `intext:"db_password"` |
| `related:url` | Find sites similar to a given URL | `related:reuters.com` |
| `cache:url` | Show Google's cached version of a page | `cache:example.com/page` |
| `allintitle:` | All words must appear in title | `allintitle:admin panel login` |
| `allinurl:` | All words must appear in URL | `allinurl:wp-admin upload` |

---

## Tutorial Modules

Read in order for a structured progression. Each module builds on the previous one.

| Module | Content |
|--------|---------|
| [1 — Introduction & Ethics](TUTORIAL/1_Introduction_Ethics.md) | What OSINT is, why Google is central, legal and ethical foundations |
| [2 — Google Operators & Dorking](TUTORIAL/2_Google_Operators_Dorking.md) | Complete operator reference, combining operators, advanced dorking techniques |
| [3 — Google Services Beyond Search](TUTORIAL/3_Google_Services_Beyond_Search.md) | Images, Maps, Street View, Scholar, Patents, Trends, Alerts, YouTube |
| [4 — Practical Scenarios & Cheatsheet](TUTORIAL/4_Practical_Scenarios_Cheatsheet.md) | Applied workflows for real investigation tasks, quick reference sheet |

---

## Dork Cheatsheet

Ready-to-use dorks for common OSINT tasks. Replace bracketed values with your targets.

**Exposed files and directories**
```
intitle:"index of /" "parent directory"
intitle:"index of /" + "server at"
intitle:"index of" inurl:ftp
site:[target.com] intitle:"index of /"
```

**Sensitive documents**
```
site:[target.com] filetype:pdf "confidential" | "internal use only"
site:[target.com] filetype:xlsx | filetype:csv "password" | "credentials"
site:[target.com] ext:sql | ext:bak | ext:config
site:[target.com] filetype:pdf "not for distribution"
```

**Login and admin panels**
```
site:[target.com] intitle:"login" | intitle:"sign in" | inurl:admin
site:[target.com] inurl:wp-admin | inurl:wp-login
site:[target.com] inurl:"/admin/login" | inurl:"/administrator"
intitle:"phpMyAdmin" inurl:"/phpmyadmin/"
```

**Exposed credentials and configuration**
```
site:[target.com] filetype:env | filetype:cfg | filetype:conf
site:[target.com] intext:"password" filetype:log
filetype:sql intext:"INSERT INTO" intext:"password"
site:pastebin.com "[target.com]" password | credential | key
```

**Employee and organizational intelligence**
```
site:linkedin.com/in "[Company Name]"
site:linkedin.com/in "[Company Name]" "engineer" | "analyst" | "developer"
"[Company Name]" filetype:pdf "org chart" | "organization chart"
site:[target.com] "email" "@[target.com]" filetype:pdf | filetype:docx
```

**Subdomain and infrastructure discovery**
```
site:*.target.com -www
inurl:*.target.com filetype:pdf
site:target.com -site:www.target.com
```

**Cached and archived content**
```
cache:[target.com]/removed-page
site:web.archive.org "[target.com]"
```

**Government and academic sources**
```
site:gov.es | site:gob.es filetype:pdf "informe" | "estudio" 2024
site:*.edu filetype:pdf "research" "[topic]"
site:gov.uk filetype:pdf "[topic]" "restricted"
```

---

## Practical Scenarios

**Scenario 1 — Company profiling**

Build a public intelligence picture of a target organization.

```
# Step 1: map indexed content
site:company.com

# Step 2: find public documents
site:company.com filetype:pdf | filetype:pptx | filetype:docx

# Step 3: press and news mentions
"Company Name" site:reuters.com | site:bloomberg.com | site:ft.com

# Step 4: employee enumeration (public profiles only)
site:linkedin.com/in "Company Name"
site:linkedin.com/in "Company Name" "security" | "IT" | "engineer"

# Step 5: patents and R&D
site:patents.google.com "Company Name"
intitle:"Company Name" site:patents.google.com

# Step 6: job postings (reveal tech stack)
site:linkedin.com/jobs "Company Name"
"Company Name" site:indeed.com | site:glassdoor.com "software engineer"
```

**Scenario 2 — Image verification**

Determine if an image is authentic and find its original source.

```
1. Upload the image to images.google.com (camera icon)
2. Check if it appears on credible news sources
3. Look for earlier versions of the same image
4. Extract visual clues: buildings, signs, vehicles, vegetation
5. Cross-reference with Google Maps Street View to confirm location
6. Download the earliest version and check EXIF data with ExifTool
```

**Scenario 3 — Document hunting on government domains**

```
site:gob.es filetype:pdf "energías renovables" "informe" 2024
site:gob.es filetype:pdf "ciberseguridad" "estrategia nacional"
site:defense.gov filetype:pdf "strategy" | "assessment" 2024
site:europa.eu filetype:pdf "cybersecurity" "threat landscape"
```

**Scenario 4 — Exposed infrastructure**

```
# Open directory listings
intitle:"index of /" inurl:[target.com]

# Exposed configuration files
site:[target.com] ext:env | ext:cfg | ext:ini

# Public cloud storage
site:s3.amazonaws.com "[company]"
site:storage.googleapis.com "[company]"
site:blob.core.windows.net "[company]"

# Exposed camera interfaces
intitle:"webcam" | intitle:"IP camera" inurl:[target network range]
```

---

## Google Services Beyond Search

**Google Images — reverse image search**

Go to [images.google.com](https://images.google.com), click the camera icon. Upload an image or paste a URL. Use cases: verify photo authenticity, find original source, identify people or locations, discover profiles associated with an image.

For EXIF metadata extraction, download the original image from the earliest indexed source and run `exiftool image.jpg` locally.

**Google Maps and Street View**

Right-click any point on the map to get coordinates. Switch to Street View for ground-level reconnaissance. Check the capture date (shown bottom-left) — historical imagery can reveal changes over time. Google Earth Pro (free desktop app) provides historical satellite imagery for the same location at different dates.

**Google Scholar**

Use `author:"Name Surname"` to find publications by a specific person. Use `site:scholar.google.com` combined with institution names to find affiliated researchers. Useful for building profiles of academics, technical experts, or identifying patent holders.

**Google Patents — [patents.google.com](https://patents.google.com)**

Search by company name, inventor, or technology keyword. Reveals R&D direction, identifies key engineers, and maps relationships between organizations through co-inventors and assignees.

**Google Trends — [trends.google.com](https://trends.google.com)**

Compare search interest for multiple terms over time and by region. Useful for tracking public attention around events, individuals, or organizations. Spikes in interest often correlate with news events.

**Google Alerts — [google.com/alerts](https://google.com/alerts)**

Set up passive monitoring using the same operator syntax as search queries. Alerts fire when new content matching your query is indexed. Use cases: brand monitoring, tracking mentions of a person or organization, early warning on threat actor TTPs appearing in public reporting.

**YouTube**

Search with filters (date, type, duration). Transcripts are searchable — use `site:youtube.com "keyword"` to surface videos where the term appears in auto-generated captions. Geolocate content using visual clues, description text, or the location tag if set.

---

## Ethics and Legal Boundaries

Google dorking and OSINT techniques operate on publicly accessible information. The following boundaries apply:

- **Authorized use only:** Do not use these techniques to access information on systems you do not own or have explicit permission to test
- **No automation against Google ToS:** Tools that mass-automate dork queries violate Google's Terms of Service — use manual queries or rate-limited tooling
- **Privacy:** Finding personal information about private individuals, even if technically public, may violate privacy laws (GDPR, CCPA) depending on jurisdiction and purpose
- **Intent matters:** Reconnaissance for defensive purposes (your own organization's exposure) is legitimate. Using the same techniques to target others without authorization is not

For a full discussion of OSINT ethics and legal frameworks, see [TUTORIAL/1_Introduction_Ethics.md](TUTORIAL/1_Introduction_Ethics.md).

---

## Contributing

Open an issue to suggest new dorks, scenarios, or corrections. To contribute directly, fork the repo, make changes on a descriptive branch, and open a pull request.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full process.

---

License: [MIT](LICENSE)
