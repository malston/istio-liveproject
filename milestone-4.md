# Milestone 4

```shell
kubectl apply -n istio-system -f - << EOF
apiVersion: "security.istio.io/v1beta1"
kind: "AuthorizationPolicy"
metadata:
  name: online-boutique
  namespace: istio-system
spec:
  selector:
    matchLabels:
      istio: ingressgateway
  action: DENY
  rules:
  - when:
    - key: "request.auth.audiences"
      notValues: ["boutiquestore.com"]
    to:
    - operation:
        paths: ["/cart"]
        ports: [ "8443" ]
---
EOF
```

Traffic to path "/cart" on port "80" is allowed to port 80 without a JWT token:

```shell
$ curl -v -sS --write-out "%{http_code}" -o /dev/null "http://$INGRESS:80/cart"
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 80 (#0)
> GET /cart HTTP/1.1
> Host: 127.0.0.1
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 200 OK
< set-cookie: shop_session-id=e37aff7c-e75a-4262-9e63-88b6b6353f34; Max-Age=172800
< date: Mon, 28 Jun 2021 19:01:34 GMT
< content-type: text/html; charset=utf-8
< x-envoy-upstream-service-time: 182
< server: istio-envoy
< transfer-encoding: chunked
<
{ [6758 bytes data]
* Connection #0 to host 127.0.0.1 left intact
* Closing connection 0
200
```

Traffic to path "/cart" on port "443" is denied without a JWT token:

```shell
curl -H "Host: marketplace.boutiquestore.com" --cacert root.crt --resolve "marketplace.boutiquestore.com:443:$INGRESS_IP" "https://marketplace.boutiquestore.com:443/cart"
RBAC: access denied
```
