# Changelog

All notable changes to this project will be documented in this file.

## [1.0.0] - 2025-09-25

### Breaking changes
- Bump Gradle wrapper to 8.7 and Android Gradle Plugin to 8.6.0, requiring builds with JDK 17.
- Increase Android `minSdk` requirement to 28 and align compile/target SDKs with API level 35.

### New features
- Modernize the library module with AndroidX configuration, Jacoco reporting, and publishing helpers for Maven Central bundles.
- Refresh the sample app harness to showcase the updated utilities on the latest Android toolchain.

### Bug fixes
- None.

### Dependencies updates
- Update enforced dependency graph to prefer latest OpenSRP artifacts and CommonsWare `saferoom.x:1.3.0`.
- Add Robolectric 4.10.3 and Mockito 4.11.0 for unit testing on JDK 17.

### Documentation
- Rewrite the README with installation guidance, usage snippets, and contribution notes.
- Add JitPack badges for latest release, latest tag, and `master-SNAPSHOT` builds.

## [0.0.7]
- Previous release (details unavailable).
