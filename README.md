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

Lints and validates Helm charts, then scans packaged charts with Trivy.

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
