# 4 — Practical Scenarios & Cheatsheet

Applied workflows combining the operators and services from the previous modules.

---

## Scenario 1 — Company exposure assessment

Map what an adversary could find about your organization before they do.

```
# 1. Baseline: what does Google have indexed?
site:company.com

# 2. Exposed documents
site:company.com filetype:pdf | filetype:docx | filetype:xlsx | filetype:pptx

# 3. Sensitive documents
site:company.com filetype:pdf "confidential" | "internal" | "restricted"
site:company.com filetype:xlsx "password" | "credentials" | "api"

# 4. Exposed config and backup files
site:company.com ext:env | ext:cfg | ext:sql | ext:bak | ext:log | ext:conf

# 5. Open directory listings
site:company.com intitle:"index of /"

# 6. Login and admin panels
site:company.com inurl:admin | inurl:login | inurl:wp-admin | inurl:phpmyadmin

# 7. Subdomains
site:*.company.com -www

# 8. Cloud storage
site:s3.amazonaws.com "company"
site:storage.googleapis.com "company"

# 9. Code repository leaks
site:github.com "company.com" password | secret | api_key | token

# 10. Paste sites
site:pastebin.com "company.com"
```

Document every finding with URL, date, and a screenshot. Each result is a remediation item.

---

## Scenario 2 — Image verification

Determine if a circulating image is authentic and trace its origin.

```
1. Reverse search: images.google.com → camera icon → upload or URL

2. Analyze results:
   - Does it appear on credible news sources?
   - Is there an earlier version? (Sort by date)
   - Does the context across sites match the claim?

3. Download the earliest version found
   exiftool image.jpg
   # Look for: DateTimeOriginal, GPS coordinates, CameraModel

4. Identify visual landmarks:
   - Buildings, signs, street markings, vegetation type
   - Vehicle models and license plate format (country indicator)
   - Weather, shadows, time of day

5. Cross-reference with Maps:
   google.com/maps → paste coordinates or search landmark name
   Switch to Street View to confirm building layout

6. Check historical imagery in Google Earth Pro for the identified location
```

---

## Scenario 3 — Person of interest (public figures only)

Research a public figure — executive, researcher, public official.

```
# Name + organization
"First Last" "Company Name"

# Professional profiles
site:linkedin.com/in "First Last" "Company Name"

# Published work
author:"First Last" site:scholar.google.com

# Patents
inventor:"First Last" site:patents.google.com

# News and press mentions
"First Last" site:reuters.com | site:ft.com | site:bloomberg.com

# Presentations and slides
"First Last" filetype:pdf | filetype:pptx site:conference-site.com

# Email format discovery (from published docs)
site:company.com "First Last" "@company.com" filetype:pdf
```

Respect privacy — this workflow applies to public figures in their public capacity.

---

## Scenario 4 — Government and institutional documents

```
# Spanish government
site:gob.es filetype:pdf "ciberseguridad" 2024
site:gob.es | site:boe.es "inteligencia artificial" filetype:pdf

# EU institutions
site:europa.eu filetype:pdf "cybersecurity" "threat landscape"
site:enisa.europa.eu filetype:pdf 2024

# US government
site:cisa.gov filetype:pdf "advisory" 2024
site:nist.gov filetype:pdf "framework"
site:defense.gov filetype:pdf "strategy" 2024

# UK government
site:gov.uk filetype:pdf "cyber" "national security"

# Academic on a topic
site:*.edu filetype:pdf "adversarial machine learning"
```

---

## Scenario 5 — Monitoring setup

Configure passive monitoring so information comes to you.

```
# google.com/alerts — example queries:

"Company Name" -site:company.com
# Catch external mentions

"Company Name" password | credential | leak | breach | "data dump"
# Early warning on exposure

"CEO Name" OR "CISO Name" announcement | leaves | joins | appointed
# Personnel changes

"CVE-2024" "Company Product"
# Vulnerability mentions affecting your stack

"topic keyword" filetype:pdf after:2024-01-01
# New publications on a topic
```

---

## Operator Cheatsheet

| Operator | Description | Example |
|----------|-------------|---------|
| `site:domain.com` | Limit to domain | `site:gov.uk filetype:pdf` |
| `filetype:ext` | Specific file type | `filetype:xlsx "budget"` |
| `"phrase"` | Exact string match | `"not for distribution"` |
| `-term` | Exclude term | `site:example.com -www` |
| `*` | Wildcard in phrase | `"the * most wanted"` |
| `OR` / `\|` | Either term | `CEO OR "chief executive"` |
| `intitle:` | In page title | `intitle:"index of /"` |
| `inurl:` | In URL | `inurl:wp-admin` |
| `intext:` | In page body | `intext:"db_password"` |
| `related:` | Similar sites | `related:reuters.com` |
| `cache:` | Cached version | `cache:example.com/page` |
| `allintitle:` | All words in title | `allintitle:admin panel login` |
| `allinurl:` | All words in URL | `allinurl:wp-admin upload` |
| `author:` | Author (Scholar) | `author:"Bruce Schneier"` |
| `assignee:` | Patent assignee | `assignee:"Palo Alto Networks"` |
| `inventor:` | Patent inventor | `inventor:"Name" site:patents.google.com` |

---

## Tips

Start with broad queries and narrow down. A query returning thousands of results needs more operators; a query returning zero needs fewer or different terms.

Test operators individually before combining — this tells you which one is restricting your results when a combination returns nothing.

Google changes its algorithm and operator support. What works today may behave differently in six months. If a query stops working, test each operator in isolation to find what changed.

Never run automated mass queries against Google's public search. Rate limit manual sessions. For production OSINT pipelines, use the Custom Search JSON API (has a free tier).
