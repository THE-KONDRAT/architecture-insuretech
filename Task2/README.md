Запуск
Предполагается, что minikube уже запущен
1. Активировать metrics-server
```shell
minikube addons enable metrics-server
```
Потом надо подождать 1-2 минуты, пока metrics-server начнёт отдавать метрики
2. Применить файл
```shell
kubectl apply -f deployment.yaml
```
3. Проверить приложение
Из Task2
```shell
kubectl port-forward deployment/scaletestapp-deployment 8080:8080
```
4. Проверить оба ресурса из задания
Идентификатор пода:
```shell
curl localhost:8080/
```
Должно вернуться что-то вроде
```shell
Идентификатор пода: scaletestapp-deployment-685c9bb848-6cnbb
```
Метрики в формате Prometheus:
```shell
curl localhost:8080/metrics
```
Вернётся примерно это:
```shell
# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 0
...
# HELP http_requests_total No of request handled
# TYPE http_requests_total counter
http_requests_total 2
# HELP process_cpu_seconds_total Total user and system CPU time spent in seconds.
# TYPE process_cpu_seconds_total counter
process_cpu_seconds_total 0.04
...
# HELP process_virtual_memory_bytes Virtual memory size in bytes.
# TYPE process_virtual_memory_bytes gauge
process_virtual_memory_bytes 1.261006848e+09
# HELP process_virtual_memory_max_bytes Maximum amount of virtual memory available in bytes.
# TYPE process_virtual_memory_max_bytes gauge
process_virtual_memory_max_bytes 1.8446744073709552e+19
# HELP promhttp_metric_handler_requests_in_flight Current number of scrapes being served.
# TYPE promhttp_metric_handler_requests_in_flight gauge
promhttp_metric_handler_requests_in_flight 1
# HELP promhttp_metric_handler_requests_total Total number of scrapes by HTTP status code.
# TYPE promhttp_metric_handler_requests_total counter
promhttp_metric_handler_requests_total{code="200"} 0
promhttp_metric_handler_requests_total{code="500"} 0
promhttp_metric_handler_requests_total{code="503"} 0
```