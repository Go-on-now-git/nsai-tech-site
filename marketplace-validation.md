# NSAI Marketplace and QueryForge Lite Validation

## Published first-party catalog

On August 26, 2026, `https://nsai.tech/marketplace/` was verified as a first-party catalog rather than a redirect. It exposes NSAI’s two free Gumroad resources, QueryForge Lite, the Prompt Vault, NUB Installer, AEGIS source repository, and service inquiry paths.

## QueryForge Lite scope validation

On the deployed `https://nsai.tech/queryforge/` page, selecting **18+** changed all four visible research-lane queries by appending the age-restricted public-research constraint `("18+" OR "age-restricted")`. This confirms the visual scope control materially changes the generated query deck and the subsequent export/handoff source data.

The same age-scoped deck successfully emitted both a CSV export and a Notion-compatible Markdown export in the live browser, each confirmed by its visible success notice.

Selecting **21+** produced the distinct constraint `("21+" OR "legal-age")` exactly once in every lane. With 21+ selected, enabling the explicit-category checkbox removed the default `-explicit -adult` exclusions while retaining the 21+ constraint. The toggle remains unavailable under the General scope.

### Final release check

Commit `8524a35` is deployed through GitHub Pages. Its public source contains the `ageClause` in the primary deterministic query builder and no longer contains the former `scopedSuffix` or `applyScope` post-render logic. A final live 18+ test showed `("18+" OR "age-restricted")` once per research lane, positioned within the primary generated query rather than appended after rendering.

Changing the live research mode from Open research to Source files retained one 18+ clause per lane and introduced no duplicate suffixes. Returning to General scope removed the age clause, disabled and cleared the explicit-category control, and restored the default `-explicit -adult` exclusions.
