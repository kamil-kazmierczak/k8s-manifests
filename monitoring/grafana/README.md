## Wymagania

 - Działający klaster Kubernetes (np. K3s/Kind/Minikube)

 - Skonfigurowany kubectl z dostępem do klastra

## Deploy pgAdmin4

 1. Utwórz sekret z danymi logowania
```
cp monitoring/grafana/secret.yaml.example monitoring/grafana/secret.yaml
# edytuj: admin-user, admin-password
```

 2. Zastosuj manifesty
```
kubectl apply -f monitoring/grafana/
```

 3. Sprawdź status zasobów
```
kubectl -n monitoring get pods
kubectl -n monitoring get svc
```

## Dostęp

 - Usługa pgadmin4 działa jako NodePort

 - Domyślny port NodePort: 30300

 - Adres URL:
```
http://<IP_węzła>:30300
```

## Dane logowania

Ustaw w `monitoring/grafana/secret.yaml`:

 - `admin-user`

 - `admin-password`

## Bezpieczeństwo

 - Nie commituj pliku secret.yaml do repozytorium

 - Commituj wyłącznie secret.yaml.example

Przykładowy wpis do .gitignore:
```
monitoring/grafana/secret.yaml
```

## Notatki

 - `storageClassName`: `local-path` (domyślny w K3s) — zmień, jeśli używasz innego storage class

 - Obraz kontenera: `grafana/grafana-oss:11.2.0` — wersję aktualizujesz w `deployment.yaml`

## Usunięcie (cleanup)

Aby usunąć wdrożenie pgAdmin4:
```
kubectl delete -f monitoring/grafana/
```
