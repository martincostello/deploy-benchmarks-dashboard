# Deploy Benchmarks Dashboard 🚀📈

[![Deploy status][deploy-badge]][deploy-status]

## Introduction

A shared GitHub Actions workflow for deploying [martincostello/benchmarks-dashboard][benchmarks-dashboard] to GitHub Pages.

See [this blog post][blog-post] for more information about the motivation behind this project and the associated dashboard.

## Usage

The shared workflow can be used in any repository to deploy the benchmarks dashboard to GitHub Pages.

An example workflow to do this is shown below.

```yaml
name: deploy

on:
  schedule:
    - cron: '0 9 * * WED' # Re-deploy every Wednesday at 0900 UTC

permissions: {}

jobs:
  deploy:
    uses: martincostello/deploy-benchmarks-dashboard/.github/workflows/deploy.yml@v1
    # Grant sufficient permissions to build the dashboard and deploy to GitHub Pages
    permissions:
      contents: read
      id-token: write
      pages: write
    with:
      # Use a custom configuration file from the default branch of the current repository
      configuration-url: ${{ format('https://raw.githubusercontent.com/{0}/refs/heads/{1}/appsettings.json', github.repository, github.event.repository.default_branch) }}
```

An example workflow for deploying the dashboard can be found in [.github/workflows/deploy-dashboard.yml][example].

### Options

The shared workflow supports the following options:

| **Name**            | **Description**                                                                  | **Required** | **Type**  | **Default**                                           |
|:--------------------|:---------------------------------------------------------------------------------|:-------------|:----------|:------------------------------------------------------|
| `configuration-url` | The URL of the configuration file to use for the dashboard.                      | **Yes**      | `string`  | -                                                     |
| `artifact-name`     | The optional name of the artifact to build and deploy the dashboard from.        | No           | `string`  |`dashboard`                                            |
| `deploy`            | Whether to deploy the dashboard after building it.                               | No           | `boolean` | Only deploy from the default branch of the repository |
| `environment`       | The GitHub environment to deploy the dashboard to.                               | No           | `string`  | `github-pages`                                        |
| `ref`               | The optional reference of the repository to build and deploy the dashboard from. | No           | `string`  | `main`                                                |
| `repository`        | The optional full name of the repository to build and deploy the dashboard from. | No           | `string`  | `martincostello/benchmarks-dashboard`                 |
| `runs-on`           | The optional type of runner to use.                                              | No           | `string`  | `ubuntu-latest`                                       |

## Feedback

Any feedback or issues can be added to the issues for this project in [GitHub][issues].

## Repository

The repository is hosted in [GitHub][repo]: <https://github.com/martincostello/deploy-benchmarks-dashboard.git>

## License

This project is licensed under the [Apache 2.0][license] license.

[benchmarks-dashboard]: https://github.com/martincostello/benchmarks-dashboard "The Benchmarks Dashboard repository in GitHub.com"
[blog-post]: https://blog.martincostello.com/continuous-benchmarks-on-a-budget/ "Continuous Benchmarks on a Budget"
[deploy-badge]: https://github.com/martincostello/deploy-benchmarks-dashboard/actions/workflows/deploy-dashboard.yml/badge.svg?branch=main
[deploy-status]: https://github.com/martincostello/deploy-benchmarks-dashboard/actions?query=workflow%3Adeploy-dashboard+branch%3Amain "Continuous Deployment for this repository"
[example]: https://github.com/martincostello/deploy-benchmarks-dashboard/blob/main/.github/workflows/deploy-dashboard.yml "Example GitHub Actions workflow for deploying the dashboard"
[issues]: https://github.com/martincostello/deploy-benchmarks-dashboard/issues "Issues for this repository on GitHub.com"
[license]: https://www.apache.org/licenses/LICENSE-2.0.txt "The Apache 2.0 license"
[repo]: https://github.com/martincostello/deploy-benchmarks-dashboard "This repository on GitHub.com"
