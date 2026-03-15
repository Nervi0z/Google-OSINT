# Contributing

Contributions are welcome: new dorks, corrected operators, additional scenarios, broken links, and outdated content.

---

## Ways to contribute

- **New dork:** Open an [issue](https://github.com/Nervi0z/Google-OSINT/issues/new?template=add-dork.md) with the query, its use case, and a note on what it surfaces
- **New scenario:** Open an issue to discuss scope before writing
- **Fix:** Broken link, outdated operator, incorrect example — submit a pull request directly
- **Typos and formatting:** Small fixes as pull requests without an issue

---

## Submitting a pull request

1. Fork the repository
2. Clone your fork:
   ```bash
   git clone https://github.com/YOUR_USERNAME/Google-OSINT.git
   ```
3. Create a descriptive branch:
   ```bash
   git checkout -b add-cloud-storage-dorks
   git checkout -b fix-filetype-operator-example
   ```
4. Edit `README.md` or the relevant file in `TUTORIAL/`
5. Commit with [Conventional Commits](https://www.conventionalcommits.org/) prefixes:
   ```bash
   git commit -m "feat: add cloud storage exposure dorks"
   git commit -m "fix: correct filetype operator syntax example"
   git commit -m "docs: expand company profiling scenario"
   ```
6. Push and open a pull request against `main`

---

## Quality criteria

- Dorks must be tested and functional — no theoretical queries
- Use cases must be specific to a defensive or legitimate investigative context
- No emojis, no generic filler language
- All examples must use placeholder values like `[target.com]`, not real domains
- Respect the ethics section — do not add content that facilitates unauthorized access
