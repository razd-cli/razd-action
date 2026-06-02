# Release v2.0.0 - razd-action

**Major version bump — breaking changes**

## What's New

- **Direct binary installation** — razd is now installed directly from GitHub Releases instead of the vfox plugin. This is faster, more reliable, and removes the vfox dependency.
- **New `razd-version` input** — specify a particular razd version (e.g. `1.2.3`) or use `latest` (default).
- **Updated mise default** — mise-version default updated to `2025.6.6`.

## Breaking Changes

- razd is no longer installed via `mise plugin install razd`. It is downloaded as a standalone binary from GitHub Releases.
- If you relied on the vfox plugin mechanism, switch to the new `razd-version` input.

## Migration from v1

```yaml
# v1 (old)
- uses: razd-cli/razd-action@v1
  with:
    mise-version: '2025.11.2'

# v2 (new)
- uses: razd-cli/razd-action@v2
  with:
    mise-version: '2025.6.6'
    razd-version: 'latest'
```

## Usage

```yaml
- uses: razd-cli/razd-action@v2
```

### With options

```yaml
- uses: razd-cli/razd-action@v2
  with:
    mise-version: '2025.6.6'
    razd-version: '1.2.3'
    checkout-repository: 'true'
```

## Inputs

| Parameter | Description | Default |
|-----------|-------------|---------|
| `mise-version` | Version of mise to install | `2025.6.6` |
| `razd-version` | Version of razd (`latest` or specific) | `latest` |
| `checkout-repository` | Whether to checkout repository | `true` |

---

**Full Changelog**: https://github.com/razd-cli/razd-action/compare/v1.0.1...v2.0.0