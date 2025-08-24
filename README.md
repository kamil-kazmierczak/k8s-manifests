# k8s-manifests

## Deploy pgAdmin4

1. Skopiuj plik `secret.yaml.example` do `secret.yaml` i ustaw swoje dane:
   ```bash
   cp db-tools/pgadmin/secret.yaml.example db-tools/pgadmin/secret.yaml

2. Zastosuj wszystkie manifesty:
   kubectl apply -f db-tools/pgadmin/

3. Sprawdź:
   kubectl -n db-tools get pods
   kubectl -n db-tools get svc
