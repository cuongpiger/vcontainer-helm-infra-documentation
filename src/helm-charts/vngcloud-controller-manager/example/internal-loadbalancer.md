<div style="float: right;"><img src="../../../images/01.png" width="160px" /></div><br>


# Internal LoadBalancer
Experience seamless internal load balancing for your Apache HTTP Server deployment on Kubernetes! In this deployment, we'll create a robust and scalable setup using a Deployment and an internal LoadBalancer-type Service.

Key Steps:

- **Step 1**: Apache HTTP Server Deployment:
  - Deploy the Apache HTTP Server using a Kubernetes Deployment, ensuring scalable and reliable operation.

- **Step 2**: Internal LoadBalancer Service:
  - Leverage the Service type LoadBalancer to create an internal load balancer, making your Apache HTTP Server accessible within the Kubernetes cluster.

- **Step 3**: Verification with Ubuntu Pod:
  - Validate the functionality of your internal load balancer by - creating an Ubuntu Pod within the same cluster.
  - Test connectivity to the Apache HTTP Server service, ensuring that the internal load balancer is working correctly.

**Why Internal Load Balancing?**
- Securely expose your services within your Kubernetes cluster without external access.
- Enhance isolation and privacy by utilizing internal IP addresses.
- Perfect for scenarios where your Apache HTTP Server service is intended for internal communication within your infrastructure.

## Get Started
Deploy your Apache HTTP Server with the provided manifest. This service will be accessible via the internal load balancer on port 8080.

***File [internal-loadbalancer.yaml](adasas)***
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: internal-http-apache2-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: apache2
  template:
    metadata:
      labels:
        app: apache2
    spec:
      containers:
        - name: apache2
          image: httpd
          ports:
            - containerPort: 80
---

apiVersion: v1
kind: Service
metadata:
  name: internal-http-apache2-service
  annotations:
    vks.vngcloud.vn/internal-load-balancer: "true"  # MUST set like this to create an internal loadbalancer
spec:
  selector:
    app: apache2
  type: LoadBalancer                                # MUST set like this to create an internal loadbalancer
  ports:
    - name: http
      protocol: TCP
      port: 8080                                    # CAN be accessed via this port with other service in the same VPC
      targetPort: 80
```