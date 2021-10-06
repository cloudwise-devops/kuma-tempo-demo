kubectl create ns bookinfo
kubectl label namespace bookinfo kuma.io/sidecar-injection=enabled --overwrite
kubectl apply -n bookinfo -f https://raw.githubusercontent.com/istio/istio/release-1.10/samples/bookinfo/platform/kube/bookinfo.yaml



kubectl create ns tracing
 
helm repo add grafana https://grafana.github.io/helm-charts

helm install tempo grafana/tempo --version 0.7.4 -n tracing -f  ../../kuma-tempo-demo/yamls/1-tempo.yaml

helm install loki grafana/loki-stack --version 2.4.1 -n tracing -f yamls/2-loki.yaml


kubectl apply -n tracing -f https://raw.githubusercontent.com/antonioberben/examples/master/opentelemetry-collector/otel.yaml
