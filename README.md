# .github

Shared reusable GitHub Actions workflows.

## Workflows

### `security.yml` — Semgrep + Gitleaks + Zizmor

Runs three security jobs: SAST (Semgrep), secret scanning (Gitleaks), and GitHub Actions security audit (Zizmor).

**Inputs**

| Input | Description | Default |
|-------|-------------|---------|
| `default-branch` | Default branch name | `main` |

**Caller example**

```yaml
jobs:
  security:
    uses: damoun/.github/.github/workflows/security.yml@main
```

---

### `helm.yml` — Lint + Validate + Trivy

Lints and validates Helm charts, then scans packaged charts with Trivy (vulnerabilities, secrets and misconfigurations).

**Inputs**

| Input | Description | Default |
|-------|-------------|---------|
| `charts_dir` | Path to charts directory | `charts` |
| `helm_version` | Helm version | `v3.17.0` |

**Caller example**

```yaml
jobs:
  helm:
    uses: damoun/.github/.github/workflows/helm.yml@main
    with:
      charts_dir: charts
```

---

### `image.yml` — Trivy

Scans a published container image with Trivy and uploads the results to code scanning. Run it on a schedule: new CVEs show up against images that have not changed. One image per repo, since every upload uses the `trivy-image` category.

**Inputs**

| Input | Description | Default |
|-------|-------------|---------|
| `image` | Image reference to scan | required |

**Caller example**

```yaml
on:
  schedule:
    - cron: "0 6 * * 1"
  workflow_dispatch:

jobs:
  image:
    uses: damoun/.github/.github/workflows/image.yml@main
    permissions:
      contents: read
      security-events: write
    with:
      image: ghcr.io/damoun/my-image:latest
```

---

### `terraform.yml` — Docs + Fmt + tfsec

Three jobs: auto-generates terraform-docs, checks formatting, and runs tfsec SARIF scan.

**Inputs**

| Input | Description | Default |
|-------|-------------|---------|
| `terraform-version` | Terraform version | `latest` |
| `working-directory` | Directory with `.tf` files | `.` |

**Caller example**

```yaml
jobs:
  terraform:
    uses: damoun/.github/.github/workflows/terraform.yml@main
    with:
      working-directory: terraform
```
