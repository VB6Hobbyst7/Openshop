# Roadmap: OpenShop

`ROADMAP.md` is the single actionable source. Historical and completed work is archived in `CHANGELOG.md`. Blocked work stays in `Roadmap_Blocked.md`.

## Issue Intake (2026-09-26)

- [ ] P1: Unusable on iOS: the canvas ceiling probe measures 1 px, so every image is rejected (issue #10)
  Reported: liangforstudy, 2026-09-20, latest release, iOS Safari, bug, two screenshots.
  Why: every image load fails with "New image dimensions exceed the measured browser canvas ceiling (1 px per side / 1 pixels total)". The ceiling probe that measures the largest canvas the browser allows returns 1 px on iOS, most likely because Safari refuses the probe canvas (memory-limited canvas allocation returns a blank context, and the probe reads that as the limit) or because the probe runs before the page is visible.
  Next: reproduce in a WebKit engine (Playwright webkit) and on a real iPhone; when the probe returns something implausibly small, fall back to a known-safe iOS ceiling (4096 per side, 16.7 million pixels) instead of the measured value, and say in the error what was measured.
  Acceptance: a 12 megapixel photo opens on iOS Safari; the probe's measured and effective ceilings are visible in the diagnostics panel.
  Evidence: https://github.com/SysAdminDoc/Openshop/issues/10
  Complexity: M
