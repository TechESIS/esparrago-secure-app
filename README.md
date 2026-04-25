# esparrago-secure-app

# Secure DevSecOps Application

This project demonstrates an advanced DevSecOps CI pipeline implemented entirely in GitHub Actions.

## Pipeline Overview

Two-stage pipeline:

1. Scan Stage
   - Semgrep (SAST)
   - pip-audit (dependencies)
   - TruffleHog (secrets)

2. Build Stage (only if scan passes)
   - Docker build
   - Trivy container scan
   - SBOM generation
   - Trusted artifact marking

## Security Features

- No hardcoded secrets
- Secure dependency management
- Container hardening
- Multi-layer security scanning

## Artifacts Produced

- dep-scan.json → Dependency vulnerabilities
- trivy-report.json → Container vulnerabilities
- sbom.json → Software Bill of Materials
- build-metadata.txt → Trusted build + image ID

## Traceability

Each build is tagged using:

secure-app:<commit-sha>

## Trusted Build Logic

A build is considered trusted only if:
- All scans pass
- No high/critical vulnerabilities
- Pipeline completes successfully
