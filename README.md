# OX Security Scan GitHub Action

A [GitHub Action](https://github.com/features/actions) for using [OX Security](https://www.ox.security) to scan for vulnerabilities in your software projects. Scans include searching for secrets, SAST issues, SCA and Open Source dependecy issues, IaC issues, etc. Scans can be configured to highlight critical issues or automatically block risks introduced into the codebase as part of your pipeline based on security policies. Security policies can be configured per repository in the [OX Security application](https://app.ox.security).

If you want to learn more, contact us at <support@ox.security>.

You can use the Action as follows:

```yaml
name: Example workflow with OX Security Scan
on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, reopened, synchronize]
    branches:
      - main
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Run OX Security Scan to check for vulnerabilities
        with:
          ox_api_key: ${{ secrets.OX_API_KEY }}
        uses: oxsecurity/ox-security-scan@main
```

### Generating an OX Security API key

The Actions example above refers to an OX Security API key:

```yaml
with:
  ox_api_key: ${{ secrets.OX_API_KEY }}
```

Once you login to your [OX Security](https://app.ox.security) account, an API key can be generated on the [API key settings tab of the Settings page](https://app.ox.security/settings?tab=apiKey). This is the only required input the action expects.

### Inputs

You can modify the action's behavior with the inputs listed below. Workflow files must use the `with` keyword to set an input value. For more information about the `with` syntax, see ["Workflow syntax for GitHub Actions"](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idstepswith).

#### `ox_override_blocking`

Default: `false`

To override a step failure on a blocking issue, set `ox_override_blocking` to `true`.

```yaml
with:
  ox_override_blocking: true
```

---

#### `ox_timeout`

Default: `20`

Timeout in minutes after which the OX Security scan will be canceled. If a timeout occurs, step failure will depend on the value of `ox_fail_on_timeout` option.

```yaml
with:
  ox_timeout: 20
```

---

#### `ox_fail_on_timeout`

Default: `false`

To have a scan timeout cause a step failure, set `ox_fail_on_timeout` to `true`.

```yaml
with:
  ox_fail_on_timeout: true
```

---

#### `ox_fail_on_error`

Default: `false`

To have an error (i.e. network, infrastructure) cause a step failure, set `ox_fail_on_error` to `true`.

```yaml
with:
  ox_fail_on_error: true
```
