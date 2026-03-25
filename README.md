# Happy Cloud Platform Observability

<!-- prettier-ignore-start -->
![k8s](https://shields.io/badge/k8s-black?logo=kubernetes&style=for-the-badge%22)
![grafana](https://shields.io/badge/grafana-black?logo=grafana&style=for-the-badge%22)
![prometheus](https://shields.io/badge/prometheus-black?logo=prometheus&style=for-the-badge%22)
![elasticsearch](https://shields.io/badge/elasticsearch-black?logo=elasticsearch&style=for-the-badge%22)
![fluentd](https://shields.io/badge/fluentd-black?logo=fluentd&style=for-the-badge%22)
![kibana](https://shields.io/badge/kibana-black?logo=kibana&style=for-the-badge%22)
![jaeger](https://shields.io/badge/jaeger-black?logo=jaeger&style=for-the-badge%22)

## 해피 클라우드 플랫폼 아키텍처

![img.png](img.png)


### Metrics (Prometheus + Grafana)

![img_1.png](img_1.png)

![img_2.png](img_2.png)

* kube-prometheus-stack install

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install monitoring prometheus-community/kube-prometheus-stack \
  -n monitoring --create-namespace \
  -f metrics/k8s/values-monitoring-lite.yaml
```

* grafana 비밀번호 확인 (ID: admin)

```
kubectl get secret monitoring-grafana -n monitoring \
  -o jsonpath="{.data.admin-password}" | base64 -d && echo
```

* service monitor 적용

```
$ kubectl apply -f metrics/k8s/user-service-monitor.yaml
$ kubectl apply -f metrics/k8s/compute-service-monitor.yaml
$ kubectl apply -f metrics/k8s/orchestrator-worker-monitor.yaml
$ kubectl apply -f metrics/k8s/api-gateway-monitor.yaml
```



### Logs




### Traces

