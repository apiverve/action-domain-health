# APIVerve Domain Health Action

> Monitor domain expiration, WHOIS changes, and domain availability

> **Beta Release** - This action is in beta. We'd love your feedback! [Open an issue](https://github.com/apiverve/action-domain-health/issues) if you encounter any problems.

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Domain_Health-blue?logo=github)](https://github.com/apiverve/action-domain-health)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**[Browse All APIs](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=domain-health)** | **[Get Free API Key](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=domain-health)** | **[Documentation](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=domain-health)**

---

## What does this action do?

This action provides access to APIVerve's Domain Health APIs directly in your GitHub workflows:

- Alert before domains expire
- Monitor WHOIS record changes
- Check domain availability for new projects
- Verify domain is responding

### Available APIs

| API | Description |
|-----|-------------|
| `domainexpiration` | Domain Expiration Checker is a simple tool for checking the expiration date and age of a domain. It returns the expiration date and age of the domain provided. |
| `whoislookup` | Whois Lookup is a simple tool for checking the registration of a domain name. It returns the name and contact information of the domain owner, the domain registrar, and more. |
| `domainavailability` | Domain Availability Checker is a simple tool for checking the availability of a domain. It returns if the domain is available or not. |
| `domainpinger` | domainpinger API |

---

## Quick Start

```yaml
- name: Domain Health
  uses: apiverve/action-domain-health@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: domainexpiration
    params: '{&quot;domain&quot;: &quot;example.com&quot;}'
```

---

## Setup

### 1. Get Your API Key

Sign up for a free account at [dashboard.apiverve.com/signup](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=domain-health) and create an API key.

### 2. Add Secret to Repository

Go to your repository **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

- Name: `APIVERVE_KEY`
- Value: Your API key from the dashboard

### 3. Use in Workflow

```yaml
- name: Domain Health
  uses: apiverve/action-domain-health@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: domainexpiration
    params: '{"your": "parameters"}'
```

---

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `api_key` | Your APIVerve API key (or set `APIVERVE_API_KEY` env var) | Yes* | - |
| `api` | API to use: `domainexpiration`, `whoislookup`, `domainavailability`, `domainpinger` | No | `domainexpiration` |
| `params` | JSON parameters for the API | No | `{}` |
| `output_file` | Path to save binary output (images, PDFs) | No | - |
| `format` | Response format: `json`, `yaml`, or `xml` | No | `json` |
| `fail_on_error` | Fail workflow if API returns error | No | `true` |

*\*API key is required but can be provided via input OR `APIVERVE_API_KEY` / `APIVERVE_KEY` environment variable.*

## Outputs

| Output | Description |
|--------|-------------|
| `result` | Full API response as JSON |
| `data` | The `data` field from response as JSON |
| `status` | API status (`ok` or `error`) |
| `file` | Path to downloaded file (if `output_file` was used) |

---

## Examples

### Expiration Check

Check when a domain expires

```yaml
- name: Expiration Check
  id: domain-health-0
  uses: apiverve/action-domain-health@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: domainexpiration
    params: '{&quot;domain&quot;: &quot;example.com&quot;}'

- name: Use result
  run: echo "Result: ${{ steps.domain-health-0.outputs.data }}"
```

### WHOIS Lookup

Get WHOIS information for a domain

```yaml
- name: WHOIS Lookup
  id: domain-health-1
  uses: apiverve/action-domain-health@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: whoislookup
    params: '{&quot;domain&quot;: &quot;example.com&quot;}'

- name: Use result
  run: echo "Result: ${{ steps.domain-health-1.outputs.data }}"
```


---

## Full Workflow Example

```yaml
name: Domain Health Workflow

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  domain-health:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Domain Health
        id: result
        uses: apiverve/action-domain-health@v1
        with:
          api_key: ${{ secrets.APIVERVE_KEY }}
          api: domainexpiration
          params: '{&quot;domain&quot;: &quot;example.com&quot;}'

      - name: Show result
        run: |
          echo "Status: ${{ steps.result.outputs.status }}"
          echo "Data: ${{ steps.result.outputs.data }}"
```

---

## Related Actions

Looking for more APIVerve actions?

- [apiverve/action](https://github.com/apiverve/action) - Generic action for all 350+ APIs
- [apiverve/action-release-assets](https://github.com/apiverve/action-release-assets) - Generate QR codes, barcodes, and badges for your GitHub releases
- [apiverve/action-visual-testing](https://github.com/apiverve/action-visual-testing) - Capture screenshots and generate PDFs for visual regression testing and documentation
- [apiverve/action-dns-monitor](https://github.com/apiverve/action-dns-monitor) - Verify DNS configuration, check propagation, and validate DNSSEC after deployments

**[Browse all APIVerve Actions →](https://github.com/marketplace?query=apiverve)**

---

## Pricing

- **Free tier** - Get started with generous free limits
- **Pro plans** - Higher rate limits and priority support for production use

Check out [pricing details](https://apiverve.com/pricing?utm_source=github&utm_medium=action&utm_campaign=domain-health).

---

## Resources

- **API Documentation**: [docs.apiverve.com](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=domain-health)
- **API Marketplace**: [apiverve.com/marketplace](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=domain-health)
- **Issues & Support**: [GitHub Issues](https://github.com/apiverve/action-domain-health/issues)
- **Email**: support@apiverve.com

---

## License

MIT - see [LICENSE](LICENSE)

---

Built by [APIVerve](https://apiverve.com?utm_source=github&utm_medium=action&utm_campaign=domain-health) - 350+ APIs for developers
