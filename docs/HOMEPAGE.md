# Personal homepage

The homepage retains al-folio's light typography and layout with Texas A&M maroon (`#500000`) accents. Its templates are intentional site overrides; runtime gems remain unchanged.

## Content

Edit `_pages/about.md` for the biography, portrait, the `experience:` and `education:` timelines, and the visitor-map URL. Each timeline entry takes `institution`, `url`, `logo` (or `initials` when no logo exists), `role`, `detail`, and `period`; dates come from the CV.

Selected publications reuse the gem's `selected_papers.liquid`: entries in `_bibliography/papers.bib` marked `selected={true}` appear under "selected publications" in the original al-folio style, with the venue badge colored from `_data/venues.yml`. News stays disabled until real `_news` entries exist (`announcements.enabled: true`). Latest Posts is hidden. The navbar shows only about, publications, and CV; the other starter pages remain in the repo with `nav: false` and posts are excluded from search.

There is no CV page. The CV is offered only as `assets/pdf/Alimurat_CV.pdf`, linked from the homepage CV icon via `_data/socials.yml`.

The email, LinkedIn, Google Scholar, and CV icons use `_data/socials.yml` and the existing social-link plugin. The supplied CV is moved to `assets/pdf/Alimurat_CV.pdf`, linked directly from the CV icon. Starter social profiles have been replaced with the supplied personal links.

The portrait is `assets/img/id_photo_lite_grain.png`, rendered as a 170px circle floated right (150px centered on mobile). Jekyll generates responsive WebP variants. `assets/img/TACO_icon.png` is the full TACO Group wordmark (rectangular), so the timeline logo column is 76px wide and every logo is centered in it.

## Appearance

`_sass/_themes.scss` provides the light palette. `_includes/head.liquid` loads `assets/css/homepage.scss` and keeps code highlighting light. `_layouts/about.liquid` arranges the homepage modules. `_includes/footer.liquid` renders a single static line ("Last updated by <first name>, <month year>. Template modified from al-folio.") in document flow; the month comes from the build time. `enable_darkmode: false` also removes the navbar icon and search theme actions.

The visitor map uses MapMyVisitors' HTTPS PNG endpoint with the existing tracking ID, shown at 220px wide, grayscale and faded, without a heading, just above the footer. It updates on page visits without injecting third-party JavaScript. Its reserved aspect ratio prevents layout shifts; an unavailable image produces a compact fallback. Visitor locations and totals are supplied by MapMyVisitors.

After editing any of the four overrides, review the diff and run `bundle exec al-folio upgrade overrides accept PATH`, followed by `bundle exec al-folio upgrade overrides audit --fail-on-stale`. Include `.al-folio-overrides.yml` with the changes. The style contract only permits these exact overrides and checks their acknowledged local hashes.

## Local verification

Use the existing Docker service; no additional container is needed. Configuration changes trigger its existing Jekyll restart mechanism.

```sh
npm run lint:prettier
npm run lint:style-contract
NO_WEBSERVER=1 SITE_URL=http://localhost:8080/ npm run test:visual -- homepage.spec.js
```

The homepage tests cover light rendering with a saved dark preference, theme-action removal, responsive content, visitor-map loading and failure, and the footer's position. Legacy visual parity against an upstream starter is not an acceptance baseline for this customized site.

Use Node 20 or 24 LTS for the test tools. Set `PLAYWRIGHT_CHANNEL=chrome` to test with installed Chrome instead of downloaded browsers; this also runs the mobile viewport in Chromium. Without that setting, the mobile project uses WebKit.
