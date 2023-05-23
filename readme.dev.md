
helm package metis-md-collector 
helm repo index . --url https://metis-data.github.io/helm-charts/ --merge index.yaml


Dry run:
helm repo update
helm install --dry-run --debug metis-mmc metis-data/metis-md-collector -f values.yaml 

|

helm install  --dry-run --debug metis-mmc metis-data/metis-md-collector --namespace metis --create-namespace \         ✱
  --set METIS_API_KEY=DHuUr5UXrg1jP0ZuB8Sl35t970UpQ5eFr75SD0xb \  --set DB_CONNECTION_STRINGS=postgresql://postgres:postgres@localhost:5432/platform;

  helm delete metis-mmc --namespace metis