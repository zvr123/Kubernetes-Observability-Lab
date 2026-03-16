# Kubernetes-Observability-Lab
Step 1 — Prepare the Environment
----------------------------------
$ kubectl create namespace monitoring-dev
namespace/monitoring-dev created
$ kubectl create namespace monitoring-prod
namespace/monitoring-prod created


Step 2 — Add Helm Repositories
---------------------------------
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
"prometheus-community" has been added to your repositories
$ helm repo add grafana https://grafana.github.io/helm-charts
"grafana" has been added to your repositories
$ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "grafana" chart repository
...Successfully got an update from the "prometheus-community" chart repository
...Successfully got an update from the "stable" chart repository
...Successfully got an update from the "bitnami" chart repository
Update Complete. ⎈Happy Helming!⎈


Step 3 — Prepare Values Files
------------------------------
Create values-dev.yaml and values-prod.yaml


Step 4 — Deploy Prometheus & Grafana
-------------------------------------
# Dev environment
helm upgrade --install monitoring-dev prometheus-community/kube-prometheus-stack -n monitoring-dev --create-namespace -f values-dev.yaml

Get your grafana admin user password by running:

  kubectl get secret --namespace monitoring-dev -l app.kubernetes.io/component=admin-secret -o jsonpath="{.items[0].data.admin-password}" | base64 --decode ; echo
devadmin


# Prod environment
helm upgrade --install monitoring-prod prometheus-community/kube-prometheus-stack -n monitoring-prod --create-namespace -f values-prod.yaml

Get your grafana admin user password by running:

  kubectl get secret --namespace monitoring-prod -l app.kubernetes.io/component=admin-secret -o jsonpath="{.items[0].data.admin-password}" | base64 --decode ; echo
prodadmin



 Step 5 — Deploy Loki + Fluent Bit (Logging)
 ---------------------------------------------
 $ helm upgrade --install loki-dev grafana/loki-stack -n monitoring-dev
NAME: loki-dev
LAST DEPLOYED: Mon Feb 23 20:45:43 2026
NAMESPACE: monitoring-dev
STATUS: deployed
REVISION: 1
NOTES:
The Loki stack has been deployed to your cluster. Loki can now be added as a datasource in Grafana.

 $ helm upgrade --install loki-prod grafana/loki-stack -n monitoring-prod
 NAME: loki-prod
LAST DEPLOYED: Mon Feb 23 20:46:21 2026
NAMESPACE: monitoring-prod
STATUS: deployed
REVISION: 1
NOTES:
The Loki stack has been deployed to your cluster. Loki can now be added as a datasource in Grafana.


 Step 6 — Port Forward Dashboards
 ---------------------------------
 kubectl port-forward svc/monitoring-grafana -n monitoring-dev 3000:80