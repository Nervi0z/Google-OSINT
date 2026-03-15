# 2 — Google Operators & Dorking

Search operators are special commands that filter Google results with precision. Combining them — "dorking" — lets you surface specific files, directories, and pages that standard searches miss.

## Core Operators

### `site:`
Restricts results to a specific domain or subdomain.

```
site:example.com
site:blog.example.com
informe anual site:empresa.es
```

### `filetype:` / `ext:`
Finds specific file types. Both work identically.

```
filetype:pdf "annual report"
ext:xlsx budget 2024
filetype:sql site:example.com
```

Common extensions for OSINT: `pdf`, `docx`, `xlsx`, `pptx`, `txt`, `csv`, `log`, `sql`, `bak`, `config`, `xml`, `json`, `env`, `cfg`

### `"exact phrase"`
Matches a literal string — useful for finding specific document titles, error messages, or quoted text.

```
"internal use only"
"not for public distribution"
"db_password ="
```

### `-` (exclusion)
Removes results containing a term.

```
site:example.com -www
jaguar speed -car
"Python" programming -snake
```

### `*` (wildcard)
Placeholder for one or more unknown words within a quoted phrase.

```
"the * most wanted"
"CEO of * announced"
```

### `OR` / `|`
Either term A or term B — useful when targets use multiple naming conventions.

```
"Chief Information Security Officer" OR CISO
filetype:pdf | filetype:docx site:example.com
```

## Location Operators

### `intitle:`
Term must appear in the page title (browser tab text).

```
intitle:"index of /"
intitle:"login panel"
intitle:"admin" inurl:example.com
```

### `inurl:`
Term must appear in the URL.

```
inurl:admin
inurl:wp-login.php
inurl:".env" site:github.com
```

### `intext:`
Term must appear in the page body — ignores title, URL, and links.

```
intext:"db_password"
intext:"BEGIN RSA PRIVATE KEY"
intext:"mysql_connect"
```

### `allintitle:` / `allinurl:` / `allintext:`
All words following the operator must appear in their respective location.

```
allintitle:admin panel login
allinurl:wp-admin upload
```

## Discovery Operators

### `related:`
Finds websites similar to a given URL — useful for mapping an organization's web ecosystem.

```
related:target.com
related:reuters.com
```

### `cache:`
Shows Google's cached snapshot of a page — useful when a page has been taken down or modified.

```
cache:example.com/removed-page
```

## Combining Operators: Dorking

The power comes from combining operators. Build queries from general to specific, adding operators one at a time.

**Open directory listings:**
```
intitle:"index of /" "parent directory"
intitle:"index of /" + "server at"
site:target.com intitle:"index of /"
```

**Exposed login panels:**
```
site:target.com intitle:"login" | intitle:"sign in" | inurl:login | inurl:admin
site:target.com inurl:wp-admin | inurl:administrator
```

**Sensitive documents:**
```
site:target.com filetype:pdf "confidential" | "internal use only"
site:target.com filetype:xlsx | filetype:csv "password" | "credentials"
```

**Exposed config and backup files:**
```
site:target.com ext:sql | ext:bak | ext:config
filetype:sql intext:"INSERT INTO" intext:"password"
site:target.com filetype:env | filetype:cfg
```

**Exposed credentials:**
```
site:pastebin.com "target.com" password | credential | token
site:github.com "target.com" password | secret | api_key
intext:"BEGIN RSA PRIVATE KEY" site:github.com
```

**Cloud storage:**
```
site:s3.amazonaws.com "target"
site:storage.googleapis.com "target"
site:blob.core.windows.net "target"
```

## Practical Tips

Start simple — one or two operators first. Add more if results are too broad. Google may trigger CAPTCHAs on complex queries in rapid succession — slow down and use manual queries.

Not all operators work equally well on all queries. `filetype:` is reliable. `cache:` has been deprecated in some regions. Test what works in your context.

For OSINT on your own organization, run these queries regularly — your exposure changes as new content gets indexed.

---

Continue to [3 — Google Services Beyond Search](3_Google_Services_Beyond_Search.md)
