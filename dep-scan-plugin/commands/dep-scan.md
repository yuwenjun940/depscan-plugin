---
allowed-tools: Bash(*)
description: Scan project dependencies for known vulnerabilities
---

## Context

- Current directory: !`pwd`

## Your task

You MUST perform dependency vulnerability scanning for the project. Follow these steps:

1. **Detect which package managers are present** by checking for lock files or manifest files.
   - Node.js: package-lock.json, yarn.lock, or pnpm-lock.yaml
   - Python: requirements.txt, Pipfile, poetry.lock, or pyproject.toml
   - Rust: Cargo.toml
   - Go: go.sum

2. **For each detected ecosystem, check if the corresponding scanner is available**:
   - Node.js: `npm audit` (requires npm)
   - Python: `pip-audit` (requires `pip install pip-audit`)
   - Rust: `cargo audit` (requires `cargo install cargo-audit`)
   - Go: `govulncheck` (requires `go install golang.org/x/vuln/cmd/govulncheck@latest`) or fallback to `go list -m all`

3. **Run the scanner(s)**:
   - If the scanner is available, run it and capture the output.
   - If the scanner is not available, output a clear message indicating the missing tool and how to install it.

4. **Format the output**:
   - If no vulnerabilities are found, output a success message.
   - If vulnerabilities are found, output the details in a readable format.
   - If multiple ecosystems are scanned, separate the results clearly.

5. **Exit with appropriate code**:
   - Exit with 0 if no vulnerabilities are found and all scanners ran successfully.
   - Exit with 1 if vulnerabilities are found.
   - Exit with 2 if a required scanner is missing.

You MUST use the Bash tool to perform all detection and scanning steps. Do not use any other tools. Provide the exact command(s) to run in your response, and the system will execute them.
