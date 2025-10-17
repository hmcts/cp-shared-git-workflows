# CP Shared Git Workflows

This repository maintains shared GitHub Actions workflows that can be used by applications across the organization.

## Workflows

### Secrets Scanning Shared Workflow

A reusable workflow that performs comprehensive secret scanning using 
* Gitleaks with HMCTS-specific rules along with built-in rules
* trufflehog

#### Features

- **Comprehensive Secret Detection**: Uses Gitleaks to scan for exposed secrets, API keys, passwords, and other sensitive information
- **HMCTS-Specific Rules**: Includes custom rules tailored for identifying HMCTS sensitive information
- **Reusable Design**: Can be easily integrated into any repository's CI/CD pipeline

#### Usage

To use this workflow in your repository, create a workflow file (e.g., `.github/workflows/secret-scanning.yml`) with the following content:

```yaml
name: Secret Scanning
on:
  push:
    branches: [ main, develop ]
  pull_request: #Run on all branches

jobs:
  scan:
    uses: hmcts/cp-shared-git-workflows/.github/workflows/shared-secret-scanning.yml@main
    secrets:
      GITLEAKS_LICENSE: ${{ secrets.GITLEAKS_LICENSE }}
      secrets: inherit
```

#### Required Secrets

The following secrets must be configured:

| Secret Name | Description | Required |
|-------------|-------------|----------|
| `GITLEAKS_LICENSE` | Gitleaks license key for advanced scanning capabilities | Yes |
| `HMCTS_CP_GITLEAKS_REGEX_INTERNAL_URL` | Regex patterns for detecting internal HMCTS URLs | Yes |
| `HMCTS_CP_GITLEAKS_REGEX_SYSTEM_IDS` | Regex patterns for detecting HMCTS system identifiers | Yes |


#### Integration Steps

1. **Add Secrets to Repository**:
   - Go to your repository's/Organisation Settings → Secrets and variables → Actions
   - Add the required secrets listed above

2. **Create Workflow File**:
   - Create `.github/workflows/secret-scanning.yml` in your repository
   - Use the example configuration provided above

3. **Customize Triggers**:
   - Modify the `on` section to match your repository's branching strategy
   - Add additional triggers as needed (e.g., schedule, manual dispatch)

#### Troubleshooting

- **Missing Secrets**: Ensure all required secrets are properly configured
- **False Positives**: Review and adjust regex patterns if legitimate content is flagged

#### Support

For issues or questions regarding this workflow, please:
1. Check the [Issues](https://github.com/hmcts/cp-shared-git-workflows/issues) page
2. Create a new issue with detailed information about your problem
3. Contact the development team for urgent security concerns

