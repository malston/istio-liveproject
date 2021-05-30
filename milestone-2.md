## Milestone 2

We curl the ingress gateway hosted at 127.0.0.1 and get back a 404 because there isn't a virtual service to handle that route

```shell
⎈ |minikube:online-boutique py-3.8.6 malston-a01 in ~/workspace
○ → curl http://$INGRESS/wrongpath
404 page not found
```

```shell
⎈ |minikube:online-boutique py-3.8.6 malston-a01 in ~/workspace
○ → echo '{"downstream_local_address":"172.17.0.4:8080","response_code_details":"via_upstream","authority":"127.0.0.1","path":"/wrongpath","method":"GET","upstream_cluster":"outbound|80||frontend.online-boutique.svc.cluster.local","protocol":"HTTP/1.1","upstream_local_address":"172.17.0.4:46062","downstream_remote_address":"172.17.0.1:4767","route_name":null,"upstream_host":"172.17.0.9:8080","response_flags":"-","request_id":"a279ad6e-0e1c-98ea-9d74-d6028e2017f8","user_agent":"curl/7.64.1","duration":3,"bytes_received":0,"start_time":"2021-05-30T18:50:42.181Z","bytes_sent":19,"upstream_transport_failure_reason":null,"upstream_service_time":"2","requested_server_name":null,"response_code":404,"connection_termination_details":null,"x_forwarded_for":"172.17.0.1"}' | jq .
```

From the ingress-gateway logs we can see that the request comes in and is routed to  `frontend.online-boutique.svc.cluster.local`

```json
{
  "downstream_local_address": "172.17.0.4:8080",
  "response_code_details": "via_upstream",
  "authority": "127.0.0.1",
  "path": "/wrongpath",
  "method": "GET",
  "upstream_cluster": "outbound|80||frontend.online-boutique.svc.cluster.local",
  "protocol": "HTTP/1.1",
  "upstream_local_address": "172.17.0.4:46062",
  "downstream_remote_address": "172.17.0.1:4767",
  "route_name": null,
  "upstream_host": "172.17.0.9:8080",
  "response_flags": "-",
  "request_id": "a279ad6e-0e1c-98ea-9d74-d6028e2017f8",
  "user_agent": "curl/7.64.1",
  "duration": 3,
  "bytes_received": 0,
  "start_time": "2021-05-30T18:50:42.181Z",
  "bytes_sent": 19,
  "upstream_transport_failure_reason": null,
  "upstream_service_time": "2",
  "requested_server_name": null,
  "response_code": 404,
  "connection_termination_details": null,
  "x_forwarded_for": "172.17.0.1"
}
```

The request is proxied by the ingress gateway to the frontend service as seen by the `upstream_cluster` value in the log message.
