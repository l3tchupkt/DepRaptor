# Changelog

All notable changes to DepRaptor will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-03-14

### Added
- Multi-target input modes: local path, GitHub URL, GitHub org, repo list file, path list file
- Interactive workflow mode — guided step-by-step when no flags are passed
- Modular payload system: system_info, webhook, discord, interactsh, ci_env_dump, custom
- Autopublish support with mandatory safety confirmation before any publish
- Simulate mode — full dry-run without publishing
- Risk scoring engine (0–10) with per-package reasons
- CI/CD detection: GitHub Actions, GitLab CI, Jenkins, CircleCI, Azure Pipelines
- GitHub org scanner via `org:name` target format
- User config file support: `~/.depraptor/config.yaml`
- `depraptor doctor` command — checks git, npm, python, twine, cargo, gem, trufflehog
- Structured logging to `results/logs/scan.log`
- Optional TruffleHog secret scanning via `--secrets`
- Publisher modules: PyPI (twine), npm, RubyGems
- Thread-safe registry cache with deduplication — no duplicate HTTP calls
- False-positive fix: pip `--hash`, `-r`, `-c` flags no longer parsed as package names

### Changed
- CLI restructured to multi-command Typer app: `depraptor scan` + `depraptor doctor`
- `--payload` now uses `None` sentinel so interactive mode only triggers when truly no flags passed
- Registry cache is now thread-safe with `threading.Lock`
- Confusion checker deduplicates by `(ecosystem, name)` before hitting registries

### Fixed
- Windows `cp1252` encoding crash — all file writes use `encoding='utf-8'`
- `rglob("requirements*.txt")` → `rglob("*requirements*.txt")` to match `sample_requirements.txt`
- `--payload system_info` explicit flag no longer triggers interactive menu

## [1.0.0] - 2024-01-15

### Added
- Initial release of DepRaptor
- Multi-ecosystem dependency scanning (Python, Node.js, Ruby, Go, Rust)
- Local directory and GitHub repository scanning
- Automated dependency confusion detection via public registry checks
- PoC package generation for Python and Node.js
- JSON and Markdown report generation
- Rich CLI with progress indicators and color output
- Multithreaded registry checking with configurable thread pool
- Registry result caching for performance
- Comprehensive logging
