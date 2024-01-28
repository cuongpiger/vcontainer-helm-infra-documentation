<div style="float: right;"><img src="../../images/01.png" width="160px" /></div><br>


# Overview

<center>

  ![](./../../images/ccm/01.png)<br>
  _**Figure 1**_

</center>

The `vngcloud-controller-manager` is a powerful Kubernetes plugin designed to streamline and enhance network load balancing within your clusters. This controller manager extends the capabilities of your Kubernetes environment.

**Key highlights**:
  - **Seamless Integration**: Integrate `vngcloud-controller-manager` effortlessly into your Kubernetes environment, ensuring a smooth and straightforward setup.
  - **Optimized Load Distribution**: Harness the power of advanced load balancing techniques to intelligently distribute traffic across your application instances, promoting optimal resource utilization.
  - **Flexible Configuration**: Tailor load balancing settings to match the specific requirements of your workloads, providing the flexibility needed for diverse application architectures.
  - **Scalability and Reliability**: Achieve new heights in application scalability with robust load balancing mechanisms that adapt dynamically to changing workloads.

# The plugin's annotations
The `vngcloud-controller-manager` utilizes Kubernetes annotations to define load balancer configurations. Below is a list of annotations that you can use to customize your load balancer settings in the Kubernetes `Service` manifest.
|#|Annotation|Description|Default/Example|
|-|-|-|-|
|1|`vks.vngcloud.vn/load-balancer-id`|The ID of the load balancer to be used for the service. If this annotation is not specified, a new load balancer will be created for the service.|- Default is empty.<br>- E.g: `lb-67cd0bbc-4c27-xxxx-xxxx-9f416a509577`.|
|2|`vks.vngcloud.vn/load-balancer-name`|Specify the load balancer's name for the service. If this annotation is omitted, the load balancer's name will be auto-generated in the format: `vks-<piece-of-cluster-uuid>-<service-namespace>-<service-name>`. If a specific load balancer name is provided, it will be formatted as: `vks-<piece-of-cluster-uuid>-<your-loadbalancer-name>`. This field is **disregarded** when the `vks.vngcloud.vn/load-balancer-id` field is provided.|- Default is empty.<br>- E.g: `my-new-loadbalancer`.|
|3|`vks.vngcloud.vn/package-id`|The ID of the network load-balancer package to be used for the service. If this annotation is not specified, the default package will be used. This field is **ignored** when the `vks.vngcloud.vn/load-balancer-id` field is provided. |- Default: `lbp-847d4d84-bc1b-4c42-b0ee-c6bc5dd83d2a` _(`VNG NLB_Small`)_.|
|4|`vks.vngcloud.vn/enable-secgroup-default`|Specify whether to attach the `Default` security group to the members of this load balancer.|- Default: `true`.|
|5|`vks.vngcloud.vn/idle-timeout-client`|Connection idle timeout is the maximum time a connection can remain open without any data transfer, after which the load balancer will close the connection. Range:  \\( 1 \Rightarrow 3600 \\).|- Default: `50`.|

