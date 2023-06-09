

[![metis](https://static-asserts-public.s3.eu-central-1.amazonaws.com/metis-min-logo.png)](https://www.metisdata.io/)

# Metis Metadata Collector Helm Chart

This repository contains [Helm](https://helm.sh) charts for the [Metadata collector](https://docs.metisdata.io/metis/metadata-collector/troubleshooting-the-production-db) project.

## Usage
[Helm](https://helm.sh) must be installed to use the charts.


## Prerequisites
* A Kubernetes cluster running version 1.11 or later.
* Helm installed and initialized in your cluster. Please refer to Helm's [documentation](https://helm.sh/docs) to get started.
* Access to the Kubernetes cluster with sufficient privileges to create and manage resources.


## Setup

1. Add the Metis Helm repository to your local Helm installation and update the Helm repository to ensure that you have the latest version:

```sh
helm repo add metis-data https://metis-data.github.io/helm-charts/
helm repo update
```

2. Create helm chart with specific api-key and pg connection on your relevant namespace

```sh
helm install metis-mmc metis-data/metis-md-collector \
  --set METIS_API_KEY=DHuUr5UXrg1jP0ZuB8Sl35t970UpQ5eFr75SD0xb \
  --set DB_CONNECTION_STRINGS=postgresql://postgres:postgres@localhost:5432/platform;
```
This command will install metis collector in your Kubernetes cluster.

3. (Optional) Customize the Metis collector installation by modifying the values in the Helm chart. You can modify the values in the Helm chart by creating a YAML file with your custom values and using the --values option. For example:

```sh
helm install metis-mmc metis-data/metis-md-collector -f my-values.yml --namespace metis --create-namespace
```

Example:
```
helm install --dry-run --debug metis-mmc metis-data/metis-md-collector \
  --set apiKey=DHuUr5UXrg1jl370UpQ5eFr75SD0xb \
  --set dbConnectionStrings=postgresql://postgres:postgres@localhost:5432/platform;
```

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.\
You can then run `helm search repo teletrace` to see the charts.

### Environment:
- `DB_CONNECTION_STRINGS`: your database connection details e.g 'postgres://user:password@host:port/database'
- `API_KEY`: Metis Api Key generated at [Metis](https://app.metisdata.io/)


### Clean up

```sh
helm delete metis-mmc --namespace metis
```

## Conclusion
In this tutorial, you learned how to install Metis collector using Helm chart. Helm chart simplifies the installation and management of Metis collector in a Kubernetes cluster. You can customize the installation by modifying the values in the Helm chart. With Metis collector installed, you can now use it to get better observability and reports of your databases.


## For developers 
 
### Release new version
1. Update chart version here: `charts/metis-md-collector/Chart.yaml`

2. Package helm and update index: 
```sh
cd ./helm-charts/charts
helm package metis-md-collector
helm repo index . --url https://metis-data.github.io/helm-charts/ --merge index.yaml 
```