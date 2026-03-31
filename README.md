# Null-Friction `.github` Repository

Organization-wide GitHub configuration and shared actions for the Null-Friction organization.

## Shared Actions

### Aikido Safe Chain

Protects package installs from supply chain attacks using [Aikido Safe Chain](https://github.com/AikidoSec/safe-chain). This composite action installs Safe Chain and configures it to intercept package manager commands (`npm`, `yarn`, `pnpm`, `pip`, etc.), blocking packages that are too new or flagged as malicious.

**Inputs:**

| Input | Description | Required | Default |
|---|---|---|---|
| `minimum-package-age-hours` | Minimum package age in hours before allowing install | No | `48` |
| `logging` | Logging level: `silent`, `normal`, or `verbose` | No | `normal` |

**Usage:**

Add the action to your workflow before any package install step:

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: Null-Friction/.github/.github/actions/safe-chain@main
  - run: npm ci
```

To customize the minimum package age or logging level:

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: Null-Friction/.github/.github/actions/safe-chain@main
    with:
      minimum-package-age-hours: "72"
      logging: "verbose"
  - run: npm ci
```
