# Platform Baseline Research

Research for GitHub issue [#2 — "Verify the platform baseline for the checklist product"](https://github.com/zpc888/ultra-checklist/issues/2), part of the build-ready checklist-management specification (#1).

Question: which stable Spring Boot 4 and Java 25 versions are compatible, what Angular release should the spec target at handoff, and what PostgreSQL version and supported deployment baseline should it name?

All findings below are sourced directly from the owning project's official docs/release channels, verified 2026-09-27.

## Spring Boot 4 / Java 25

- **Target for the spec:** Spring Boot **4.1.1** (built on Spring Framework **7.0.9+**), running on Java **25 (LTS)**.
- Spring Boot 4.0.0 GA was announced 20 November 2025, built on Spring Framework 7 (spring.io blog). The line has since progressed to the current stable **4.1.1**, published 2026-08-20 per the project's GitHub Releases feed; a 4.2.0-M2 pre-release exists but is not stable.
- The official System Requirements page states: *"Spring Boot 4.1.1 requires at least Java 17 and is compatible with versions up to and including Java 26. Spring Framework 7.0.9 or above is also required."* Java 17 is the floor; Java 25 sits within the fully supported range.
- Java 25 reached General Availability on **16 September 2025** and is confirmed by the OpenJDK project page to be a **long-term support (LTS)** release from most vendors — making it the correct current LTS baseline to pair with Spring Boot 4.x.
- Build-tool baselines (same requirements page): Maven 3.6.3+, or Gradle 8.14+ (8.x)/9.x.

**Sources:**
- Spring Boot 4.0.0 GA announcement — https://spring.io/blog/2025/11/20/spring-boot-4-0-0-available-now
- Spring Boot System Requirements (current stable) — https://docs.spring.io/spring-boot/system-requirements.html
- Spring Boot GitHub Releases (confirms 4.1.1, published 2026-08-20) — https://github.com/spring-projects/spring-boot/releases
- OpenJDK JDK 25 project page (LTS status, GA date) — https://openjdk.org/projects/jdk/25/

## Angular

- **Target for the spec:** Angular **22** (current published release **22.2.0**), on Node.js **^22.22.3 || ^24.15.0 || ^26.0.0** and TypeScript **>=6.0.0 <6.1.0**.
- The npm registry's `dist-tags.latest` for `@angular/core` is `22.2.0`, published 2026-09-23 (verified directly against `registry.npmjs.org/@angular/core`).
- angular.dev's official releases page confirms the current support-window policy: **all major releases are supported for 24 months** — 12 months Active + 12 months LTS (security/regression fixes only). As of Angular v22 the major-release cadence changed from 6 months to **12 months, with 4-6 minor releases per major**; earlier majors (v2–v19) are no longer supported at all.
- The official version-compatibility table (angular.dev/reference/versions) lists, for Angular 22.0.x: Node.js `^22.22.3 || ^24.15.0 || ^26.0.0`, TypeScript `>=6.0.0 <6.1.0`, RxJS `^6.5.3 || ^7.4.0`.
- Angular 22 is the newest major and therefore has the longest remaining support runway of any currently-published release — the right choice for a greenfield spec over v20/v21, which are already in (or approaching) LTS-only mode.

**Sources:**
- Angular versioning, release-cadence, and support-window policy — https://angular.dev/reference/releases
- Angular Node.js/TypeScript/RxJS version-compatibility table — https://angular.dev/reference/versions
- npm registry metadata for `@angular/core` (verifies latest = 22.2.0) — https://registry.npmjs.org/@angular/core

## PostgreSQL

- **Target for the spec:** PostgreSQL **18**, always tracking the latest minor (currently **18.6**).
- The official Versioning Policy page's releases table confirms PostgreSQL 18 first released **25 September 2025**, current minor **18.6**, and scheduled final release/EOL **14 November 2030** — the longest remaining support runway of any currently supported major (17, 16, 15, 14 are also still supported but EOL sooner: Nov 2029, Nov 2028, Nov 2027, Nov 2026 respectively).
- Official policy: a new major version ships roughly annually; each major version receives minor (bug/security) releases at least once every 3 months; **each major version is supported for 5 years after its initial release**, after which a final minor ships and the version goes end-of-life.
- The same page explicitly recommends: **"We recommend that users always run the current minor release associated with their major version."** Minor upgrades require no dump/restore (stop server → install new binaries → restart); major upgrades require `pg_upgrade` or dump/reload.
- Recommendation for the spec: name **PostgreSQL 18.x**, deployed/upgraded to the latest 18.y minor at build time, with a documented policy to apply minor updates promptly per the community's own guidance.

**Sources:**
- PostgreSQL Versioning Policy (cadence, 5-year support window, releases table) — https://www.postgresql.org/support/versioning/

## Summary for the spec

| Component | Version to name | Support runway |
|---|---|---|
| Backend runtime | Java 25 (LTS) | LTS release, GA 2025-09-16 |
| Backend framework | Spring Boot 4.1.1 / Spring Framework 7.0.9+ | Current stable line |
| Frontend framework | Angular 22 (22.2.0) | Active until ~2027-06, LTS until ~2028-06 |
| Database | PostgreSQL 18 (current minor 18.6) | Supported until 2030-11-14 |
