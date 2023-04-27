

[![metis](https://static-asserts-public.s3.eu-central-1.amazonaws.com/metis-min-logo.png)](https://www.metisdata.io/)

# Metis Metadata Collector

Using the [Documentation](https://docs.metisdata.io/metis/metadata-collector/troubleshooting-the-production-db) of [Metis](https://app.metisdata.io/).

## Setup

1. Add metis helm chart
```sh
helm repo add metis-data https://metis-data.github.io/helm-charts/
helm repo update
```

2. Create helm chart with specific api-key and pg connection 
```sh
helm install my-release metis-data/metis-md-collector \
  --set METIS_API_KEY=your_api_key \
  --set DB_CONNECTION_STRINGS=connection_string_1;
```


### Environment:
- DB_CONNECTION_STRINGS: your database connection details e.g 'postgres://user:password@host:port/database'
- METIS_API_KEY: Metis Api Key generated at [Metis](https://app.metisdata.io/)