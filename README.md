# github/ossar-action

![OSSAR windows-latest](https://github.com/microsoft/security-code-analysis-action/workflows/OSSAR%20windows-latest/badge.svg)  
![OSSAR ubuntu-latest](https://github.com/microsoft/security-code-analysis-action/workflows/OSSAR%20ubuntu-latest/badge.svg)

Run multiple open source security static analysis tools without the added complexity with OSSAR (Open Source Static Analysis Runner).

This action runs the [Microsoft Security Code Analysis CLI](https://aka.ms/mscadocs) for security analysis by:

* Installing the Microsoft Security Code Analysis CLI
* Installing the latest Microsoft security policy
* Installing the latest Microsoft and 3rd party security tools
* Automatic or user-provided configuration of security tools
* Execution of a full suite of security tools
* Normalized processing of results into the SARIF format
* Build breaks and more

# Usage

See [action.yml](action.yml)

## Basic

Run OSSAR with the default policy and recommended tools.

```yaml
steps:
- uses: actions/checkout@v2
- uses: actions/setup-dotnet@v1
  with:
    dotnet-version: '3.1.201'
- name: Run OSSAR
  uses: github/ossar-action@master
  id: ossar
- name: Upload results to Security tab
  uses: github/codeql-action/upload-sarif@v1
  with:
    sarif_file: ${{ steps.ossar.outputs.sarifFile }}
```

## Upload Results to the Security tab

To upload results to the Security tab of your repo, run the `github/codeql-action/upload-sarif` action immediately after running MSCA. MSCA sets the action output variable `sarifFile` to the path of a single SARIF file that can be uploaded to this API.

```yaml
- name: Upload results to Security tab
  uses: github/codeql-action/upload-sarif@v1
  with:
    sarif_file: ${{ steps.ossar.outputs.sarifFile }}
```

# License

The scripts and documentation in this project are released under the [MIT License](LICENSE)

# Contributing

Contributions are welcome! See the [Contributor's Guide](docs/contributors.md).