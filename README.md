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
