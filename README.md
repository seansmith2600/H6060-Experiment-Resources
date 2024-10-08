# H6060-Experiment-Workflows

This GitHub repository contains GitHub workflows for H6060 experiments.

## GitHub Actions

All GitHub Actions are stored in the `.github/actions` directory.

## GitHub Workflows

All GitHub Actions are stored in the `.github/workflows` directory.

## SCA and SAST Scans

The following SCA and SAST tools are supported within the experiment GitHub workflows:

| Tool Type | Tool Name              | Java | Python | JavaScript |
|-----------|------------------------|------|--------|------------|
| SCA       | Dependabot             | yes  | yes    | yes        |
| SCA       | Eclipse Steady         | yes  | yes    | no         |
| SCA       | Grype                  | yes  | yes    | yes        |
| SCA       | OWASP Dependency Check | yes  | yes    | yes        |
| SCA       | Snyk                   | yes  | yes    | yes        |
| SAST      | CodeQL                 | yes  | yes    | yes        |
| SAST      | DeepSource             | yes  | yes    | yes        |
| SAST      | Horusec                | yes  | yes    | yes        |
| SAST      | Semgrep                | yes  | yes    | yes        |
| SAST      | Snyk Code              | yes  | yes    | yes        |
| SAST      | SonarQube              | yes  | yes    | yes        |

## Pre-requisites

Before running the GitHub workflows, the following pre-requisites must be met:

**General pre-requisites:**
- The project must be built successfully in a separate GitHub Workflow job.

**Hosting pre-requisites:**
- A SonarQube instance must be hosted and accessible.
- An Eclipse Steady instance must be hosted and accessible.

**Account pre-requisites:**
- A Honeycomb account must be created to export GitHub Workflow metrics.
- An NVD API key must be obtained to access the NVD API.
- An OpenCVE account must be created to authenticate with OpenCVE.
- A Semgrep account must be created to authenticate with Semgrep.
- A Snyk account must be created to authenticate with Snyk.

**GitHub repository pre-requisites:**
- Dependabot alerts must be enabled in the GitHub repository settings.

## Triggering the GitHub Workflows

The workflow can be triggered using the following example snippet:

```yaml
  java-scanning:
    needs: build-application 
    name: Run Java Scanning Workflow
    uses: seansmith2600/H6060-Experiment-Workflows/.github/workflows/experiment-1-java.yml@main
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN }}
      github-api-token: ${{ secrets.GIT_API_TOKEN }}
      nvd-api-key: ${{ secrets.NVD_API_KEY }}
      opencve-username: ${{ secrets.OPENCVE_USERNAME }}
      opencve-password: ${{ secrets.OPENCVE_PASSWORD }}
      honeycomb-api-key: ${{ secrets.HONEYCOMB_API_KEY }}
      eclipse-steady-host-url: ${{ secrets.ECLIPSE_STEADY_HOST_URL }}
      deepsource-api-key: ${{ secrets.DEEPSOURCE_API_KEY }}
      semgrep-app-token: ${{ secrets.SEMGREP_APP_TOKEN }}
      snyk-token: ${{ secrets.SNYK_TOKEN }}
      sonarqube-username: ${{ secrets.SONARQUBE_USERNAME }}
      sonarqube-password: ${{ secrets.SONARQUBE_PASSWORD }}
      sonarqube-token-ubuntu: ${{ secrets.SONARQUBE_TOKEN_UBUNTU }}
      sonarqube-token-macos: ${{ secrets.SONARQUBE_TOKEN_MACOS }}
      sonarqube-token-windows: ${{ secrets.SONARQUBE_TOKEN_WINDOWS }}
      sonarqube-user-token-ubuntu: ${{ secrets.SONARQUBE_USER_TOKEN_UBUNTU }}
      sonarqube-user-token-macos: ${{ secrets.SONARQUBE_USER_TOKEN_MACOS }}
      sonarqube-user-token-windows: ${{ secrets.SONARQUBE_USER_TOKEN_WINDOWS }}
      sonarqube-url-ubuntu: ${{ secrets.SONARQUBE_URL_UBUNTU }}
      sonarqube-url-macos: ${{ secrets.SONARQUBE_URL_MACOS }}
      sonarqube-url-windows: ${{ secrets.SONARQUBE_URL_WINDOWS }}
    with:
      eclipse-steady-workspace-token: 1111-2222-3333-4444
      eclipse-steady-application-group-id: com.example
      eclipse-steady-application-artifact-id: my-project
      eclipse-steady-application-version: 1.0.0
      eclipse-steady-project-source-directories: src
      project-name: my-project
      build-artifact: java-build
      build-directory: target

  python-scanning:
    needs: build-application
    name: Run Python Scanning Workflow
    uses: seansmith2600/H6060-Experiment-Workflows/.github/workflows/experiment-2-python.yml@main
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN }}
      github-api-token: ${{ secrets.GIT_API_TOKEN }}
      nvd-api-key: ${{ secrets.NVD_API_KEY }}
      opencve-username: ${{ secrets.OPENCVE_USERNAME }}
      opencve-password: ${{ secrets.OPENCVE_PASSWORD }}
      honeycomb-api-key: ${{ secrets.HONEYCOMB_API_KEY }}
      eclipse-steady-host-url: ${{ secrets.ECLIPSE_STEADY_HOST_URL }}
      deepsource-api-key: ${{ secrets.DEEPSOURCE_API_KEY }}
      oss-index-username: ${{ secrets.OSS_INDEX_USERNAME }}
      oss-index-password: ${{ secrets.OSS_INDEX_PASSWORD }}
      semgrep-app-token: ${{ secrets.SEMGREP_APP_TOKEN }}
      snyk-token: ${{ secrets.SNYK_TOKEN }}
      sonarqube-username: ${{ secrets.SONARQUBE_USERNAME }}
      sonarqube-password: ${{ secrets.SONARQUBE_PASSWORD }}
      sonarqube-token-ubuntu: ${{ secrets.SONARQUBE_TOKEN_UBUNTU }}
      sonarqube-token-macos: ${{ secrets.SONARQUBE_TOKEN_MACOS }}
      sonarqube-token-windows: ${{ secrets.SONARQUBE_TOKEN_WINDOWS }}
      sonarqube-user-token-ubuntu: ${{ secrets.SONARQUBE_USER_TOKEN_UBUNTU }}
      sonarqube-user-token-macos: ${{ secrets.SONARQUBE_USER_TOKEN_MACOS }}
      sonarqube-user-token-windows: ${{ secrets.SONARQUBE_USER_TOKEN_WINDOWS }}
      sonarqube-url-ubuntu: ${{ secrets.SONARQUBE_URL_UBUNTU }}
      sonarqube-url-macos: ${{ secrets.SONARQUBE_URL_MACOS }}
      sonarqube-url-windows: ${{ secrets.SONARQUBE_URL_WINDOWS }}
    with:
      eclipse-steady-workspace-token: 1111-2222-3333-4444
      eclipse-steady-application-group-id: com.example
      eclipse-steady-application-artifact-id: my-project
      eclipse-steady-application-version: 1.0.0
      eclipse-steady-project-source-directories: src
      sonarqube-sources: src
      project-name: my-project
      build-artifact: python-build
      build-directory: dist

  javascript-scanning:
    needs: build-application
    name: Run JavaScript Scanning Workflow
    uses: seansmith2600/H6060-Experiment-Workflows/.github/workflows/experiment-3-javascript.yml@main
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN }}
      github-api-token: ${{ secrets.GIT_API_TOKEN }}
      nvd-api-key: ${{ secrets.NVD_API_KEY }}
      opencve-username: ${{ secrets.OPENCVE_USERNAME }}
      opencve-password: ${{ secrets.OPENCVE_PASSWORD }}
      honeycomb-api-key: ${{ secrets.HONEYCOMB_API_KEY }}
      eclipse-steady-host-url: ${{ secrets.ECLIPSE_STEADY_HOST_URL }}
      deepsource-api-key: ${{ secrets.DEEPSOURCE_API_KEY }}
      oss-index-username: ${{ secrets.OSS_INDEX_USERNAME }}
      oss-index-password: ${{ secrets.OSS_INDEX_PASSWORD }}
      semgrep-app-token: ${{ secrets.SEMGREP_APP_TOKEN }}
      snyk-token: ${{ secrets.SNYK_TOKEN }}
      sonarqube-username: ${{ secrets.SONARQUBE_USERNAME }}
      sonarqube-password: ${{ secrets.SONARQUBE_PASSWORD }}
      sonarqube-token-ubuntu: ${{ secrets.SONARQUBE_TOKEN_UBUNTU }}
      sonarqube-token-macos: ${{ secrets.SONARQUBE_TOKEN_MACOS }}
      sonarqube-token-windows: ${{ secrets.SONARQUBE_TOKEN_WINDOWS }}
      sonarqube-user-token-ubuntu: ${{ secrets.SONARQUBE_USER_TOKEN_UBUNTU }}
      sonarqube-user-token-macos: ${{ secrets.SONARQUBE_USER_TOKEN_MACOS }}
      sonarqube-user-token-windows: ${{ secrets.SONARQUBE_USER_TOKEN_WINDOWS }}
      sonarqube-url-ubuntu: ${{ secrets.SONARQUBE_URL_UBUNTU }}
      sonarqube-url-macos: ${{ secrets.SONARQUBE_URL_MACOS }}
      sonarqube-url-windows: ${{ secrets.SONARQUBE_URL_WINDOWS }}
    with:
      sonarqube-sources: src
      project-name: my-project
      build-artifact: javascript-build
      build-directory: ''
```

## GitHub Workflow Inputs

The following GitHub Action organisation/repository secrets should be set in a GitHub repository settings for confidentiality. 

GitHub Actions does not currently support the inheritance of secrets to reusable workflows. Therefore, the GitHub Action organisation/repository secrets must be passed as secrets to the GitHub workflows.
- See [GitHub Actions: Support for inheriting secrets in reusable workflows](https://github.com/github/roadmap/issues/636) for more information.

| Secret Name                    | Description                                          |
|--------------------------------|------------------------------------------------------|
| `DEEPSOURCE_API_KEY`           | API key to authenticate with DeepSource              |
| `GITHUB_API_TOKEN`             | GitHub API token to access the GitHub API            |
| `HONEYCOMB_API_KEY`            | Honeycomb API key to export GitHub Workflow metrics  |
| `NVD_API_KEY`                  | API key to access the NVD API                        |
| `OPENCVE_USERNAME`             | Username to authenticate with OpenCVE                |
| `OPENCVE_PASSWORD`             | Password to authenticate with OpenCVE                |
| `OSS_INDEX_USERNAME`           | Username for OSS Index                               |
| `OSS_INDEX_PASSWORD`           | Password for OSS Index                               |
| `SEMGREP_APP_TOKEN`            | Token to authenticate with Semgrep                   |
| `SNYK_TOKEN`                   | Token to authenticate with Snyk                      |
| `SONARQUBE_PASSWORD`           | Password to authenticate with SonarQube              |
| `SONARQUBE_USERNAME`           | Username to authenticate with SonarQube              |
| `SONARQUBE_TOKEN_UBUNTU`       | Token to authenticate with SonarQube on Ubuntu 22.04 |
| `SONARQUBE_TOKEN_WINDOWS`      | Token to authenticate with SonarQube on Windows 2022 |
| `SONARQUBE_TOKEN_MACOS`        | Token to authenticate with SonarQube on MacOS 14     |
| `SONARQUBE_USER_TOKEN_UBUNTU`  | Token to query API with SonarQube on Ubuntu 22.04    |
| `SONARQUBE_USER_TOKEN_WINDOWS` | Token to query API with SonarQube on Windows 2022    |
| `SONARQUBE_USER_TOKEN_MACOS`   | Token to query API with SonarQube on MacOS 14        |
| `SONARQUBE_URL_UBUNTU`         | URL of Ubuntu 22.04 SonarQube                        |
| `SONARQUBE_URL_WINDOWS`        | URL of Windows 2022 SonarQube                        |
| `SONARQUBE_URL_MACOS`          | URL of MacOS 14 SonarQube                            |

The following secrets are supported for the GitHub workflows:

| name                             | required | description                                          |
|----------------------------------|----------|------------------------------------------------------|
| **github-token**                 | true     | GitHub token to download build artifacts             |
| **github-api-token**             | true     | GitHub API token to access the GitHub API            |
| **nvd-api-key**                  | true     | API key to access the NVD API                        |
| **opencve-username**             | true     | Username to authenticate with OpenCVE                |
| **opencve-password**             | true     | Password to authenticate with OpenCVE                |
| **honeycomb-api-key**            | true     | Honeycomb API key to export GitHub Workflow metrics  |
| **deepsource-api-key**           | false    | API key to authenticate with DeepSource              |
| **eclipse-steady-host-url**      | false    | URL of the Eclipse Steady instance                   |
| **semgrep-app-token**            | false    | Token to authenticate with Semgrep                   |
| **snyk-token**                   | false    | Token to authenticate with Snyk                      |
| **sonarqube-username**           | false    | Username to authenticate with SonarQube              |
| **sonarqube-password**           | false    | Password to authenticate with SonarQube              |
| **sonarqube-token-ubuntu**       | false    | Token to authenticate with SonarQube on Ubuntu 22.04 |
| **sonarqube-token-macos**        | false    | Token to authenticate with SonarQube on MacOS 14     |
| **sonarqube-token-windows**      | false    | Token to authenticate with SonarQube on Windows 2022 |
| **sonarqube-user-token-ubuntu**  | false    | Token to query API with SonarQube on Ubuntu 22.04    |
| **sonarqube-user-token-macos**   | false    | Token to query API with SonarQube on MacOS 14        |
| **sonarqube-user-token-windows** | false    | Token to query API with SonarQube on Windows 2022    |
| **sonarqube-url-ubuntu**         | false    | URL of Ubuntu 22.04 SonarQube                        |
| **sonarqube-url-macos**          | false    | URL of MacOS 14 SonarQube                            |
| **sonarqube-url-windows**        | false    | URL of Windows 2022 SonarQube                        |


The following inputs are supported for the GitHub workflows:

### experiment-1-java.yml

| name                                          | required | type    | default                                  | description                                             |
|-----------------------------------------------|----------|---------|------------------------------------------|---------------------------------------------------------|
| **sast-codeql-enabled**                       | false    | boolean | true                                     | Enable CodeQL scan (SAST)                               |
| **sast-horusec-enabled**                      | false    | boolean | true                                     | Enable Horusec scan (SAST)                              |
| **sast-semgrep-enabled**                      | false    | boolean | true                                     | Enable Semgrep scan (SAST)                              |
| **sast-sonarqube-enabled**                    | false    | boolean | true                                     | Enable SonarQube scan (SAST)                            |
| **sast-snyk-code-enabled**                    | false    | boolean | true                                     | Enable Snyk Code scan (SAST)                            |
| **sca-eclipse-steady-enabled**                | false    | boolean | true                                     | Enable Eclipse Steady scan (SCA)                        |
| **sca-grype-enabled**                         | false    | boolean | true                                     | Enable Grype scan (SCA)                                 |
| **sca-owasp-dependency-check-enabled**        | false    | boolean | true                                     | Enable OWASP Dependency Check scan (SCA)                |
| **sca-snyk-enabled**                          | false    | boolean | true                                     | Enable Snyk scan (SCA)                                  |
| **reporting-enabled**                         | false    | boolean | true                                     | Enable reporting of scan results                        |
| **eclipse-steady-workspace-token**            | false    | string  |                                          | Token used to identify project workspace                |
| **eclipse-steady-application-group-id**       | false    | string  |                                          | Group ID of the application                             |
| **eclipse-steady-application-artifact-id**    | false    | string  |                                          | Artifact ID of the application                          |
| **eclipse-steady-application-version**        | false    | string  |                                          | Version of the application                              |
| **eclipse-steady-project-source-directories** | false    | string  |                                          | Project source directories to scan (separated by comma) |
| **horusec-files-or-paths-to-ignore**          | false    | string  | \*\*/test/\*\*                           | Files or paths to ignore during the Horusec scan        |
| **semgrep-files-or-paths-to-ignore**          | false    | string  | test,tests                               | Files or paths to ignore during the Semgrep scan        |
| **java-version**                              | false    | string  | 17                                       | Java version to install                                 |
| **java-distribution**                         | false    | string  | temurin                                  | Java distribution to install                            |
| **project-name**                              | false    | string  |                                          | Name of project to be scanned                           |
| **build-command**                             | false    | string  | mvn -Dmaven.test.skip=true clean install | Build command for Java application Maven scan           |
| **build-artifact**                            | false    | string  |                                          | Name of project build artifact                          |
| **build-directory**                           | false    | string  |                                          | Name of project build directory                         |

### experiment-2-python.yml

| name                                          | required | type    | default        | description                                             |
|-----------------------------------------------|----------|---------|----------------|---------------------------------------------------------|
| **sast-codeql-enabled**                       | false    | boolean | true           | Enable CodeQL scan (SAST)                               |
| **sast-horusec-enabled**                      | false    | boolean | true           | Enable Horusec scan (SAST)                              |
| **sast-semgrep-enabled**                      | false    | boolean | true           | Enable Semgrep scan (SAST)                              |
| **sast-sonarqube-enabled**                    | false    | boolean | true           | Enable SonarQube scan (SAST)                            |
| **sast-snyk-code-enabled**                    | false    | boolean | true           | Enable Snyk Code scan (SAST)                            |
| **sca-eclipse-steady-enabled**                | false    | boolean | true           | Enable Eclipse Steady scan (SCA)                        |
| **sca-grype-enabled**                         | false    | boolean | true           | Enable Grype scan (SCA)                                 |
| **sca-owasp-dependency-check-enabled**        | false    | boolean | true           | Enable OWASP Dependency Check scan (SCA)                |
| **sca-snyk-enabled**                          | false    | boolean | true           | Enable Snyk scan (SCA)                                  |
| **reporting-enabled**                         | false    | boolean | true           | Enable reporting of scan results                        |
| **eclipse-steady-workspace-token**            | false    | string  |                | Token used to identify project workspace                |
| **eclipse-steady-application-group-id**       | false    | string  |                | Group ID of the application                             |
| **eclipse-steady-application-artifact-id**    | false    | string  |                | Artifact ID of the application                          |
| **eclipse-steady-application-version**        | false    | string  |                | Version of the application                              |
| **eclipse-steady-project-source-directories** | false    | string  |                | Project source directories to scan (separated by comma) |
| **horusec-files-or-paths-to-ignore**          | false    | string  | \*\*/test/\*\* | Files or paths to ignore during the Horusec scan        |
| **semgrep-files-or-paths-to-ignore**          | false    | string  | test,tests     | Files or paths to ignore during the Semgrep scan        |
| **sonarqube-sources**                         | false    | string  | src            | Source code directory to scan                           |
| **python-version**                            | false    | string  | 3.8            | Python version to install                               |
| **project-name**                              | false    | string  |                | Name of project to be scanned                           |
| **build-artifact**                            | false    | string  |                | Name of project build artifact                          |
| **build-directory**                           | false    | string  |                | Name of project build directory                         |

### experiment-3-javascript.yml

| name                                   | required | type    | default        | description                                        |
|----------------------------------------|----------|---------|----------------|----------------------------------------------------|
| **sast-codeql-enabled**                | false    | boolean | true           | Enable CodeQL scan (SAST)                          |
| **sast-horusec-enabled**               | false    | boolean | true           | Enable Horusec scan (SAST)                         |
| **sast-semgrep-enabled**               | false    | boolean | true           | Enable Semgrep scan (SAST)                         |
| **sast-sonarqube-enabled**             | false    | boolean | true           | Enable SonarQube scan (SAST)                       |
| **sast-snyk-code-enabled**             | false    | boolean | true           | Enable Snyk Code scan (SAST)                       |
| **sca-grype-enabled**                  | false    | boolean | true           | Enable Grype scan (SCA)                            |
| **sca-owasp-dependency-check-enabled** | false    | boolean | true           | Enable OWASP Dependency Check scan (SCA)           |
| **sca-snyk-enabled**                   | false    | boolean | true           | Enable Snyk scan (SCA)                             |
| **reporting-enabled**                  | false    | boolean | true           | Enable reporting of scan results                   |
| **horusec-files-or-paths-to-ignore**   | false    | string  | \*\*/test/\*\* | Files or paths to ignore during the Horusec scan   |
| **owasp-properties-file**              | false    | string  |                | Path to the OWASP Dependency Check properties file |
| **semgrep-files-or-paths-to-ignore**   | false    | string  | test,tests     | Files or paths to ignore during the Semgrep scan   |
| **sonarqube-sources**                  | false    | string  | src            | Source code directory to scan                      |
| **node-version**                       | false    | string  | 16.x           | Node version to install                            |
| **project-name**                       | false    | string  |                | Name of project to be scanned                      |
| **build-artifact**                     | false    | string  |                | Name of project build artifact                     |
| **build-directory**                    | false    | string  |                | Name of project build directory                    |
