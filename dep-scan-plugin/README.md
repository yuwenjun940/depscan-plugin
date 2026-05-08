# DepScan Plugin for Claude Code

A Claude Code plugin that scans project dependencies for known vulnerabilities across multiple ecosystems (Node.js, Python, Rust, Go).

## Features

- ✅ Multi-ecosystem support (Node.js/npm, Python/pip, Rust/cargo, Go)
- ✅ Automatic ecosystem detection based on lock files
- ✅ Clear vulnerability reporting with severity levels
- ✅ Fix suggestions where available
- ✅ JSON and text output formats
- ✅ Easy installation via Claude Code plugin system

## Installation

1. Install Claude Code (if not already installed):
   ```bash
   # Recommended method
   curl -fsSL https://claude.ai/install.sh | bash
   ```

2. Install the DepScan plugin:
   ```bash
   # From local directory
   claude plugin install /path/to/dep-scan-plugin
   ```

## Usage

Navigate to your project directory and run:

```bash
# Basic scan
/dep-scan

# Scan with auto-fix (where supported)
/dep-scan --fix

# Get JSON output for integration
/dep-scan --format json
```

## Supported Ecosystems

| Ecosystem | Lock Files | Scanner Command |
|-----------|------------|-----------------|
| Node.js | package-lock.json, yarn.lock, pnpm-lock.yaml | `npm audit` |
| Python | requirements.txt, Pipfile, poetry.lock, pyproject.toml | `pip-audit` |
| Rust | Cargo.toml | `cargo audit` |
| Go | go.sum | `govulncheck` (fallback to `go list -m all`) |

## Output Examples

### Text Format
```
=== NODEJS ===
{
  "auditReportVersion": 2,
  "vulnerabilities": {
    "lodash": { ... }
  }
}
```

### JSON Format
```json
{
  "nodejs": {
    "exit_code": 1,
    "stdout": "{ ... }",
    "stderr": ""
  }
}
```

## Development

This plugin was created using the Claude Code Plugin Development Kit. To modify or extend:

1. Edit the command in `commands/dep-scan.md`
2. Update metadata in `.claude-plugin/plugin.json`
3. Test with `/dep-scan` in any project directory

## License

MIT

## Author

来福 (laifu@example.com)