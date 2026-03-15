# 1 — Introduction & Ethics

## What is OSINT

Open Source Intelligence (OSINT) is the collection and analysis of information from publicly available sources. No hacking, no exploits, no unauthorized access — just systematic use of what's already out there.

Google is central to OSINT because it indexes an enormous fraction of the public web and provides a query language (operators) that lets you filter results with surgical precision. Combined with its ancillary services — Maps, Images, Scholar, Patents, Trends, Alerts — it covers reconnaissance scenarios that would otherwise require specialized tools.

## Why Google specifically

- Largest index of publicly accessible content on the web
- Operator syntax powerful enough to surface files, directories, and pages that were never intended to be findable
- Services covering geospatial, academic, temporal, and media intelligence
- Free, no account required for basic use, API available for automation

## Legitimate use cases

- **Defensive reconnaissance:** Map your own organization's public exposure before attackers do
- **Threat intelligence:** Track threat actors, campaigns, and TTPs surfacing in public reporting
- **Investigations:** Verify claims, locate sources, build profiles from public records
- **Journalism and research:** Find primary sources, government documents, academic publications
- **Due diligence:** Background research on companies, individuals, and events

## Legal and ethical boundaries

**What is always acceptable:**
- Searching for information about your own organization
- Authorized penetration testing engagements (with written scope)
- Academic and journalistic research on public figures and organizations
- Verifying publicly shared content

**What requires careful consideration:**
- Research on private individuals — even publicly available personal data may be subject to GDPR, CCPA, or equivalent legislation depending on jurisdiction and purpose
- Automated querying — mass-automated dork queries violate Google's Terms of Service
- Aggregation — combining individually innocuous public data points into a detailed profile of a private person can cross legal and ethical lines even if each piece was public

**What is never acceptable:**
- Using OSINT findings to access systems without authorization
- Targeting private individuals for harassment, stalking, or harm
- Publishing sensitive information found through OSINT without legal justification

## Practical rule

Before running a query, ask: would I be comfortable explaining to a lawyer or employer what I was looking for and why? If yes, proceed. If not, reconsider.

---

Continue to [2 — Google Operators & Dorking](2_Google_Operators_Dorking.md)
