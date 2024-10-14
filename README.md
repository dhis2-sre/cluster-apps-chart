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

Bump the version in [Chart.yaml](./charts/cluster-apps/Chart.yaml), commit and push.

**NOTE: do not create a tag yourself!**

Our release workflow will then using [Helm chart releaser action](https://github.com/helm/chart-releaser-action)

* create a tag `cluster-apps-<version>`
* create a [release](https://github.com/dhis2-sre/cluster-apps-chart/releases) associated with the new tag
* commit an updated index.yaml with the new release
* redeploy the GitHub pages to serve the new index.yaml

Note: there might be a slight delay between the release and the `index.yaml` file being updated as GitHub pages have to
be re-deployed.
