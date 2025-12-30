# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## Added

- Download gh-oss-stats binary from latest release based on OS and ARCH
    - Update workflow test: test with different supported and unsupported combos
- added write permission to github workflow example

## Fixes
- run test action on debug data


## [0.1.0] - 2025-12-XX

### Added
- Initial release of gh-oss-stats-action
- Support for 4 badge styles: summary, compact, detailed, minimal
- Support for 2 badge variants: default, text-based
- Support for 6 color themes: dark, light, nord, dracula, gruvbox-dark, gruvbox-light
- Auto-commit functionality for badge updates
- Support for filtering by stars and excluding organizations
- Configurable sorting (by PRs, stars, or commits)

### Features
- 48 badge combinations (6 themes × 2 variants × 4 styles)
- Zero-configuration setup (works with default GitHub token)
- Smart change detection (only commits when badge changes)
- Verbose logging option for debugging

[Unreleased]: https://github.com/mabd-dev/gh-oss-stats-action/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/mabd-dev/gh-oss-stats-action/releases/tag/v0.1.0
