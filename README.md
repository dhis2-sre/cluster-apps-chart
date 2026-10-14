# Cluster apps

This chart installs our cluster apps

# Install

There are multiple ways to install helm charts. Currently supported from this repository is basic Helm and Skaffold.

## Helm

The chart is published to https://dhis2-sre.github.io/cluster-apps-chart

To install the chart you first need to add this chart repository

```sh
helm repo add cluster-apps https://dhis2-sre.github.io/cluster-apps-chart
helm repo update
helm search repo cluster-apps/cluster-apps --versions

helm install cluster-apps cluster-apps/cluster-apps
```

The versions returned are gathered from [index.yaml](./index.yaml) which is
published to [this GitHub page](https://dhis2-sre.github.io/cluster-apps-chart/index.yaml).

## Skaffold

```sh
skaffold run
```

## Release chart

Bump the version in [Chart.yaml](./charts/cluster-apps/Chart.yaml) and merge the change to `master`.

**NOTE: do not create a tag yourself!**

The release workflow:

* packages the chart and creates its GitHub release and tag `cluster-apps-<version>`, skipping existing releases
* builds the documentation and indexes the published chart packages, including older versions
* uploads and deploys the site using GitHub's standard Pages actions

In Settings -> Pages, the source must be **GitHub Actions**. The index is generated from the
[releases](https://github.com/dhis2-sre/cluster-apps-chart/releases) and is not committed to the repository.

To retry publication after a failure, run **Release Charts** manually on `master`.
