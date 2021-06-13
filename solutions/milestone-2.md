## Solution

```sh
$ curl http://$INGRESS/wrongpath
404 page not found
```

The corresponding access log from ingress gateway pod:

```sh
$ kubectl -n istio-system logs -l app=istio-ingressgateway --tail=1 | jq .
{
  "x_forwarded_for": "100.96.1.0",
  "requested_server_name": "-",
  "bytes_received": "0",
  "istio_policy_status": "-",
  "bytes_sent": "19",
  "upstream_cluster": "outbound|80||frontend.online-boutique.svc.cluster.local",
  "downstream_remote_address": "100.96.1.0:33759",
  "authority": "10.110.168.216",
  "path": "/wrongpath",
  "protocol": "HTTP/1.1",
  "upstream_service_time": "1",
  "upstream_local_address": "100.96.4.101:58758",
  "duration": "1",
  "upstream_transport_failure_reason": "-",
  "route_name": "-",
  "downstream_local_address": "100.96.4.101:8080",
  "user_agent": "curl/7.64.1",
  "response_code": "404",
  "response_flags": "-",
  "start_time": "2020-12-30T07:25:16.375Z",
  "method": "GET",
  "request_id": "16a7a86d-dfb8-9aec-9286-3cd7a3b1ad55",
  "upstream_host": "100.96.4.106:8080"
}
```

As you can see from the access log above the request to “http://$INGRESS/wrongpath” is sent from the ingress gateway pod to the upstream service frontend service and the frontend service returns a 404 response code which is proxied back to the client. This occurs due to the VirtualService resource frontend-virtual-service configured with no match clause which sends all traffic received at port 80 on Istio ingress gateway to the frontend service irrespective of the specified path in the request.
