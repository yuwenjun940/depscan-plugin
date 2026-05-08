# DepScan Demonstration Output

This file shows what the output of the DepScan plugin looks like when run on a test project with a vulnerable dependency (lodash@4.17.15).

## 1. Basic Scan (`/dep-scan`)

```json
{
  "auditReportVersion": 2,
  "vulnerabilities": {
    "lodash": {
      "name": "lodash",
      "severity": "high",
      "isDirect": true,
      "via": [
        {
          "source": 1106913,
          "name": "lodash",
          "dependency": "lodash",
          "title": "Command Injection in lodash",
          "url": "https://github.com/advisories/GHSA-35jh-r3h4-6jhm",
          "severity": "high",
          "cwe": [
            "CWE-77",
            "CWE-94"
          ],
          "cvss": {
            "score": 7.2,
            "vectorString": "CVSS:3.1/AV:N/AC:L/PR:H/UI:N/S:U/C:H/I:H/A:H"
          },
          "range": "<4.17.21"
        },
        {
          "source": 1106920,
          "name": "lodash",
          "dependency": "lodash",
          "title": "Prototype Pollution in lodash",
          "url": "https://github.com/advisories/GHSA-p6mc-m468-83gw",
          "severity": "high",
          "cwe": [
            "CWE-770",
            "CWE-1321"
          ],
          "cvss": {
            "score": 7.4,
            "vectorString": "CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:U/C:N/I:H/A:H"
          },
          "range": ">=3.7.0 <4.17.19"
        },
        {
          "source": 1108258,
          "name": "lodash",
          "dependency": "lodash",
          "title": "Regular Expression Denial of Service (ReDoS) in lodash",
          "url": "https://github.com/advisories/GHSA-29mw-wpgm-hmr9",
          "severity": "moderate",
          "cwe": [
            "CWE-400",
            "CWE-1333"
          ],
          "cvss": {
            "score": 5.3,
            "vectorString": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:L"
          },
          "range": ">=4.0.0 <4.17.21"
        },
        {
          "source": 1112455,
          "name": "lodash",
          "dependency": "lodash",
          "title": "Lodash has Prototype Pollution Vulnerability in `_.unset` and `_.omit` functions",
          "url": "https://github.com/advisories/GHSA-xxjr-mmjv-4gpg",
          "severity": "moderate",
          "cwe": [
            "CWE-1321"
          ],
          "cvss": {
            "score": 6.5,
            "vectorString": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:L/A:L"
          },
          "range": ">=4.0.0 <=4.17.22"
        },
        {
          "source": 1115806,
          "name": "lodash",
          "dependency": "lodash",
          "title": "lodash vulnerable to Code Injection via `_.template` imports key names",
          "url": "https://github.com/advisories/GHSA-r5fr-rjxr-66jc",
          "severity": "high",
          "cwe": [
            "CWE-94"
          ],
          "cvss": {
            "score": 8.1,
            "vectorString": "CVSS:3.1/AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H"
          },
          "range": ">=4.0.0 <=4.17.23"
        },
        {
          "source": 1115810,
          "name": "lodash",
          "dependency": "lodash",
          "title": "lodash vulnerable to Prototype Pollution via array path bypass in `_.unset` and `_.omit`",
          "url": "https://github.com/advisories/GHSA-f23m-r3pf-42rh",
          "severity": "moderate",
          "cwe": [
            "CWE-1321"
          ],
          "cvss": {
            "score": 6.5,
            "vectorString": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:L/A:L"
          },
          "range": "<=4.17.23"
        }
      ],
      "effects": [],
      "range": "<=4.17.23",
      "nodes": [
        "node_modules/lodash"
      ],
      "fixAvailable": true
    }
  },
  "metadata": {
    "vulnerabilities": {
      "info": 0,
      "low": 0,
      "moderate": 0,
      "high": 1,
      "critical": 0,
      "total": 1
    },
    "dependencies": {
      "prod": 2,
      "dev": 0,
      "optional": 0,
      "peer": 0,
      "peerOptional": 0,
      "total": 1
    }
  }
}
```

## 2. Scan with Fix Attempt (`/dep-scan --fix`)

Note: The `npm audit fix` command will attempt to update lodash to a non-vulnerable version.

After running `/dep-scan --fix`, you would see output similar to:

```
up to date in 0.3s
found 0 vulnerabilities
```

And the `package-lock.json` would be updated to use lodash@4.17.21 or later.

## 3. Supported Ecosystems

The plugin automatically detects the following ecosystems by looking for lock files:

- **Node.js**: package-lock.json, yarn.lock, pnpm-lock.yaml → runs `npm audit`
- **Python**: requirements.txt, Pipfile, poetry.lock, pyproject.toml → runs `pip-audit`
- **Rust**: Cargo.toml → runs `cargo audit`
- **Go**: go.sum → runs `govulncheck` (if available) or falls back to `go list -m all`

## 4. Output Formats

- **Text (default)**: Human-readable output, suitable for terminal viewing.
- **JSON** (`/dep-scan --format json`): Machine-readable output for integration with other tools.

## 5. Example Usage in Claude Code

In any project directory, simply invoke the slash command:

```
/dep-scan
```

To attempt automatic fixes:

```
/dep-scan --fix
```

To get JSON output for further processing:

```
/dep-scan --format json
```