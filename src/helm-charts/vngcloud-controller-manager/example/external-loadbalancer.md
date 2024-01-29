<div style="float: right;"><img src="../../../images/01.png" width="160px" /></div><br>


# External LoadBalancer
## Example 1: Nginx service
In this hands-on lab, you'll deploy an Nginx deployment and leverage the `vngcloud-controller-manager` to seamlessly expose this service to the internet using an L4 load balancer. Apply the [nginx-internet-facing.yaml]().

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: external-http-nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
---
kind: Service
apiVersion: v1
metadata:
  name: external-http-nginx-service
  annotations:
    vks.vngcloud.vn/load-balancer-name: "my-nginx-service"                  # Name of the load balancer
    vks.vngcloud.vn/package-id: "lbp-ddbf9313-3f4c-471b-afd5-f6a3305159fc"  # ID of the load balancer package
spec:
  selector:
    app: nginx
  type: LoadBalancer
  ports:
  - name: http
    port: 80
    targetPort: 80
```

```bash
kubectl apply -f nginx-internet-facing.yaml
```

<center>

  ![](../../../images/ccm/27.png)
  ![](../../../images/ccm/28.png)
  \\( \small{Loadbalancer \space \space information} \\)

</center>

Check that the Nginx service has been exposed to the internet by accessing the external IP address of the load balancer.
```bash
kubectl get svc -owide
kubectl get pods -owide
```

<center>

  ![](./../../../images/ccm/29.png)

</center>

Access the service via the external IP address of the load balancer.

<center>

  ![](./../../../images/ccm/30.1.png)

</center>