# Maintain Learning Paths

Validate all resource URLs in the BridgeNewProficiency learning path files and replace any that are broken, expired, or no longer relevant.

## What this skill does

1. Scans all `cale-invatare-*.md` files for Markdown links in table rows
2. Checks each URL for availability (HTTP 200 + correct page title)
3. Replaces invalid or expired links with working alternatives from the same domain or equivalent free resources
4. Ensures all replacements are free, publicly accessible, and still relevant to QA/testing

## How to run

```
/maintain-learning-paths
```

Optionally target a single file:
```
/maintain-learning-paths cale-invatare-testare-manuala.md
```

## Validation rules

- **404 / connection error / domain-for-sale page** → replace
- **Redirect to login wall without free tier** → replace  
- **Course deleted from platform** (e.g. TAU course removed) → replace with active equivalent
- **Domain changed** but content exists at new URL → update URL, keep resource name
- **Platform deprecated / rebranded** → update label and URL (e.g. Mode Analytics → ThoughtSpot)
- **402 Payment Required** → replace with free alternative
- **200 OK but page title says "404" or "Page Not Found"** → treat as broken, replace
- **403 or connection refused** → likely bot protection on legitimate site; check via WebFetch to confirm content exists before replacing

## Important lessons from 2026-06 validation run

### Platform-level changes to watch for

- **Test Automation University (TAU)** removed ~15 courses. Check each course URL individually.
  Working courses (June 2026): `playwright-intro/`, `junit5-tutorial/`, `automating-your-api-tests-with-rest-assured/`, `selenium-webdriver-tutorial-java/`, `selenium-webdriver-python-tutorial/`, `github-actions-for-testing/`, `setting-a-foundation-for-successful-test-automation/`, `pact-contract-tests/`, `performance-and-load-testing/`, `appium-java-tutorial/`, `appium-java-tutorial-1/`, `modern-functional-testing/`, `automated-visual-testing-a-fast-path-to-test-automation-success/`, `unit-testing/`, `scaling-tests-with-docker/`

- **Ministry of Testing** restructured all article URLs. `/articles/X` paths mostly 404.
  New patterns: `/articles/what-is-software-testing`, `/software-testing-glossary/X`, `/topics/X`, `/testbash-sessions/X`

- **Mode Analytics** was acquired by ThoughtSpot. URLs still work but rebrand the label.

- **rework.withgoogle.com** guides were removed. The psychological safety guide at `/guides/understanding-team-effectiveness/` is gone. Use CCL: `https://www.ccl.org/articles/leading-effectively-articles/what-is-psychological-safety-at-work/`

- **thebalancemoney.com** articles moved behind a paywall (402). Use free alternatives (MIT career center, Glassdoor, etc.)

- **PostgreSQL Tutorial** (postgresqltutorial.com) URL structure changed. Use `/postgresql-tutorial/X` prefix.

### URL verification approach

**Do NOT rely only on HTTP status code.** Some sites return 200 with a "Not Found" page title. Always check both:
1. HTTP status code (200 = potentially ok, 404/402/308 = needs action)
2. Page title — confirm it matches expected content

For 403 responses: most are bot protection (ASQ, Agile Alliance, Glassdoor, LinkedIn Learning, Runestone Academy). Verify via WebFetch if unsure. Do NOT replace 403 URLs unless you confirm via WebFetch that the content no longer exists.

For 308 responses: permanent redirects that work fine for browser users. Update the URL to the final destination if you can determine it; otherwise leave as-is.

### Replacement sources (priority order)

1. Same article on the same site (URL slug changed)
2. Official docs for the tool/technology
3. Test Automation University (testautomationu.applitools.com) — for QA courses
4. DeepLearning.AI free short courses — for AI/prompt engineering content
5. freeCodeCamp, Hyperskill, W3Schools, MDN — for language/tech fundamentals
6. Ministry of Testing `/topics/X` pages — for testing methodology topics (when specific article is gone)
7. Martin Fowler blog / continuousdelivery.com — for methodology/architecture
8. YouTube official channels (freeCodeCamp, official project channels)
9. GitHub project pages — for open source tool documentation

## Steps Claude follows

```
1. For each cale-invatare-*.md file:
   a. Extract all URLs from markdown link syntax [label](url)
   b. Skip: code examples (example.com, reqres.in), anchor-only links (#), relative paths (./)
   c. For each URL:
      - Do HTTP GET with MaximumRedirection 5
      - Check status code AND extract <title> from response HTML
      - Flag as broken: 404, 402, 308 (if redirect target unknown), 200 with "not found" title
      - Flag as uncertain: 403, connection closed (verify with WebFetch)
   d. For broken URLs: search for replacement, verify replacement URL, update file
   
2. Commit with message: "fix: replace N broken URLs in learning paths"
```

## Notes

- Skip URLs that are code examples (`https://example.com`, `https://reqres.in`, etc.)
- Skip anchor-only links (#section) and relative links (./file.md)
- Discord invite links expire — replace with official community page if broken
- YouTube video links: verify the video still exists (not deleted/private) by checking for "Video unavailable" in title
- TAU courses move URLs frequently — check `testautomationu.applitools.com/` homepage for current catalog
- When replacing a TAU course with a different source, update both the URL AND the label to reflect the new source