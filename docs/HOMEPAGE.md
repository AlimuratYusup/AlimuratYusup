# Personal homepage

The homepage retains al-folio's light typography and layout with Texas A&M maroon (`#500000`) accents. Its templates are intentional site overrides; runtime gems remain unchanged.

## Content

Edit `_pages/about.md` for the biography, portrait, education and experience entries, and visitor-map URL. Only facts already supplied in the biography are displayed; unknown dates and degree details are omitted.

News and selected publications are disabled until real content replaces the starter examples. Replace `_news` entries, then set `announcements.enabled: true`. Replace the bibliography, mark the desired papers `selected={true}`, and set `selected_papers: true`. Both modules have section anchors and reuse the plugin's content rendering. Latest Posts is hidden on the homepage; the other site pages are retained.

The email, LinkedIn, Google Scholar, and CV icons use `_data/socials.yml` and the existing social-link plugin. The supplied CV is moved to `assets/pdf/Alimurat_CV.pdf`, linked directly from the CV icon. Starter social profiles have been replaced with the supplied personal links.

The portrait is `assets/img/id_photo_lite_grain.png`, moved from the supplied source location. Jekyll generates responsive WebP variants.

## Appearance

`_sass/_themes.scss` provides the light palette. `_includes/head.liquid` loads `assets/css/homepage.scss` and keeps code highlighting light. `_layouts/about.liquid` arranges the homepage modules. `_includes/footer.liquid` renders only the copyright year and name in document flow. `enable_darkmode: false` also removes the navbar icon and search theme actions.

The visitor map uses MapMyVisitors' HTTPS PNG endpoint with the existing tracking ID. It updates on page visits without injecting third-party JavaScript or moving DOM elements. Its reserved aspect ratio prevents layout shifts; an unavailable image produces a compact fallback. The provider ignores marker-color parameters on static images, so an SVG color filter maps its pink markers to maroon while preserving neutral grays. Visitor locations and totals are supplied by MapMyVisitors.

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
