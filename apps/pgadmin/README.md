## Wymagania

 - Działający klaster Kubernetes (np. K3s/Kind/Minikube)

 - Skonfigurowany kubectl z dostępem do klastra

## Deploy pgAdmin4

 1. Utwórz sekret z danymi logowania
```
cp db-tools/pgadmin/secret.yaml.example db-tools/pgadmin/secret.yaml
# edytuj: PGADMIN_DEFAULT_EMAIL, PGADMIN_DEFAULT_PASSWORD
```

 2. Zastosuj manifesty
```
kubectl apply -f db-tools/pgadmin/
```

 3. Sprawdź status zasobów
```
kubectl -n db-tools get pods
kubectl -n db-tools get svc
```

## Dostęp

 - Usługa pgadmin4 działa jako NodePort

 - Domyślny port NodePort: 30432

 - Adres URL:
```
http://<IP_węzła>:30432
```

## Dane logowania

Ustaw w `db-tools/pgadmin/secret.yaml`:

 - `PGADMIN_DEFAULT_EMAIL`

 - `PGADMIN_DEFAULT_PASSWORD`

## Bezpieczeństwo

 - Nie commituj pliku secret.yaml do repozytorium

 - Commituj wyłącznie secret.yaml.example

Przykładowy wpis do .gitignore:
```
db-tools/pgadmin/secret.yaml
```

## Notatki

 - `storageClassName`: `local-path` (domyślny w K3s) — zmień, jeśli używasz innego storage class

 - Obraz kontenera: `dpage/pgadmin4:8.11` — wersję aktualizujesz w `deployment.yaml`

## Usunięcie (cleanup)

Aby usunąć wdrożenie pgAdmin4:
```
kubectl delete -f db-tools/pgadmin/
```
