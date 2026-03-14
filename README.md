<img width="1700" height="460" alt="github-header-banner (2)" src="https://github.com/user-attachments/assets/537fef11-f316-4cfd-9067-8113a4c211a7" />

# DepRaptor

**Dependency Confusion Vulnerability Scanner and PoC Generator**

Developer: LAKSHMIKANTHAN K (letchupkt)

## Overview

DepRaptor is a production-grade security tool designed for security researchers and bug bounty hunters to detect and demonstrate dependency confusion vulnerabilities in software projects. It scans projects across multiple ecosystems, identifies packages vulnerable to dependency confusion attacks, and automatically generates proof-of-concept packages.

## Features

- **Multi-Ecosystem Support**: Python (PyPI), Node.js (npm), Ruby (RubyGems), Go, Rust (crates.io)
- **Local & Remote Scanning**: Scan local directories or GitHub repositories
- **Automated Detection**: Check packages against public registries
- **PoC Generation**: Automatically create proof-of-concept packages
- **Professional Reports**: Generate JSON and Markdown reports
- **Modern CLI**: Rich terminal UI with progress indicators
- **Multithreaded**: Fast registry checks with configurable thread pools
- **Comprehensive Logging**: Detailed logs for audit trails

## Installation

### From PyPI 

```bash
pip install depraptor
```

## Usage

### Basic Scan

 current directory:
```bash
depraptor  .
```

Scan specific project:
```bash
depraptor  ./my-project
```

Scan GitHub repository:
```bash
depraptor  https://github.com/org/repo
```

### Advanced Options

```bash
depraptor  <target> [OPTIONS]
```

Options:
- `--threads, -t`: Number of threads for registry checks (default: 10)
- `--output, -o`: Custom output directory (default: ./results)
- `--repo-dir`: Custom repository clone directory (default: ./repos)
- `--verbose, -v`: Enable verbose logging

### Examples

```bash
# Scan with 20 threads
depraptor  . --threads 20

# Custom output directory
depraptor  ./project --output ./scan-results

# Verbose mode
depraptor  https://github.com/org/repo --verbose
```

## Output Structure

```
./
├── repos/              # Cloned repositories
│   └── org_repo/
├── results/            # Scan results
│   ├── report.json     # JSON report
│   ├── report.md       # Markdown report
│   ├── dependencies.json
│   ├── pocs/           # Generated PoC packages
│   │   └── package-name/
│   │       ├── setup.py
│   │       ├── payload.py
│   │       └── README.md
│   └── logs/
│       └── depraptor.log
```

## Supported Dependency Files

### Python
- `requirements.txt`
- `setup.py`
- `pyproject.toml`
- `Pipfile`

### Node.js
- `package.json`

### Ruby
- `Gemfile`

### Go
- `go.mod`

### Rust
- `Cargo.toml`

## How It Works

1. **Dependency Extraction**: Recursively scans project for dependency files
2. **Registry Checking**: Queries public registries to verify package existence
3. **Vulnerability Detection**: Identifies packages not found in public registries
4. **PoC Generation**: Creates proof-of-concept packages for vulnerable dependencies
5. **Report Generation**: Produces comprehensive reports in multiple formats

## PoC Package Behavior

Generated PoC packages are designed for authorized testing only. When installed, they:

1. Log system information (username, hostname, working directory)
2. Capture environment variables
3. Write all data to `payload_log.txt`

**The PoC packages DO NOT:**
- Exfiltrate data to external servers
- Modify system files
- Execute malicious code

## Security Notice

⚠️ **WARNING**: This tool is intended ONLY for:

- Authorized security testing
- Bug bounty programs with proper scope
- Security research with explicit permission

**DO NOT:**
- Upload PoC packages to public registries without authorization
- Use this tool on systems you don't own or have permission to test
- Violate any laws or terms of service

Unauthorized use may be illegal and unethical.

## Example Output

```
________                  __________                  __                  
\______ \    ____  ______ \______   \_____   ______ _/  |_  ____ _______  
 |    |  \ _/ __ \ \____ \ |       _/\__  \  \____ \\   __\/  _ \\_  __ \ 
 |    `   \\  ___/ |  |_> >|    |   \ / __ \_|  |_> >|  | (  <_> )|  | \/ 
/_______  / \___  >|   __/ |____|_  /(____  /|   __/ |__|  \____/ |__|    
        \/      \/ |__|           \/      \/ |__|                         

Dependency Confusion Scanner
Developer: LAKSHMIKANTHAN K (letchupkt)

✓ Found 45 dependencies
✓ Found 3 vulnerable dependencies
✓ Generated 3 PoC packages
✓ Reports saved to ./results
```

## Development

### Project Structure

```
depraptor/
├── cli/
│   └── main.py              # CLI interface
├── scanner/
│   ├── dependency_parser.py # Dependency extraction
│   └── confusion_checker.py # Vulnerability detection
├── poc/
│   └── poc_generator.py     # PoC package generation
├── report/
│   └── report_writer.py     # Report generation
└── utils/
    ├── banner.py            # CLI banner
    ├── config.py            # Configuration
    ├── filesystem.py        # File utilities
    ├── github.py            # GitHub integration
    └── registry.py          # Registry checking
```

### Running Tests

```bash
pytest tests/
```

### Building the Package

```bash
python -m build
```

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

MIT License - See LICENSE file for details

## Disclaimer

This tool is provided for educational and authorized security testing purposes only. The author and contributors are not responsible for any misuse or damage caused by this tool. Always obtain proper authorization before testing any systems.

## Acknowledgments

Built for the security research community to help identify and responsibly disclose dependency confusion vulnerabilities.

---

**Developer**: LAKSHMIKANTHAN K (letchupkt)
