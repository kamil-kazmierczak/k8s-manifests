# 1) Argo CD
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
kubectl create ns argocd
helm upgrade --install argocd argo/argo-cd \
  -n argocd \
  --set applicationset.enabled=true \
  --set crds.install=true \
  --set server.service.type=NodePort \
  --set server.service.nodePortHttps=30080

# 2) Hasło do UI/CLI
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

# 3) Dodaj Twój ApplicationSet
kubectl -n argocd apply -f clusters/k3s/apps-appset.yaml

# 4) Sprawdź
kubectl -n argocd get applications
# UI: https://<IP_noda>:30080  (admin / <hasło z kroku 2>)
