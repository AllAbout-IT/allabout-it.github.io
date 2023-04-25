---
layout: default
title: Create Ingress Controller
parent: 01.Architecture Application by AWS EKS
grand_parent: AWS Workshop Studio
# great_grand_parent: PROJECT
# has_children: true
nav_order: 1006
# permalink: /docs/01.PROJECT
---
# Create Ingress Controller
{:. no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

### Ingrees Controller

In this lab, we will use [**AWS Load Balancer Controller**](/https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/) for Ingress Controller.

{: .note}  
The AWS ALB Ingress Controller has been rebranded to AWS Load Balancer Controller.

**Ingress** is a rule and resource object that defines how to handle requests, primarily when accessing from outside the cluster to inside the Kubernetes cluster. In short, it serve as a gateway for external requests to access inside of the cluster. You can set up it for load balancing for external requests, processing TLS/SSL certificates, routing to HTTP routes, and so on. Ingress processes requests from the L7.

In Kubernetes, you can also externally expose to NodePort or LoadBalancer type in Service object, but if you use a Serivce object without any Ingress, you must consider detailed options such as routing rules and TLS/SSL to all services. That's why Ingress is needed in Kubernetes environment.

![1](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/1.png)

Ingress means the object that you have set up rules for handling external requests, and **Ingress Controller** is needed for these settings to work. Unlike other controllers that run as part of the kube-controller-manager, the ingress controller is not created with the cluster by nature. Therefore, you need to install it yourself.

## Create AWS Load Balancer Controller

### Create AWS Load Balancer Controller

The [**AWS Load Balancer Controller**](/https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html) manages AWS Elastic Load Balancers for a Kubernetes cluster. The controller provisions the following resources.

* It satisfies Kubernetes Ingress resources by provisioning Application Load Balancers.
* It satisfies Kubernetes Service resources by provisioning Network Load Balancers.

The controller was formerly named the AWS ALB Ingress Controller. There are two **traffic modes** supported by each type of AWS Load Balancer controller:

* Instance(default): Register nodes in the cluster as targets for ALB. Traffic reaching the ALB is routed to NodePort and then proxied to the Pod.
* IP: Register the Pod as an ALB target. Traffic reaching the ALB is routed directly to the Pod. In order to use that traffic mode, you must explicitly specify it in the ingress.yaml file with comments.

![2](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/2.png)

{: .note}  
Create a folder named manifests in the root folder (for example, /home/ec2-user/environment/) to manage manifests. Then, inside the manifests folder, create a folder alb-controller to manage the manifest associated with the ALB Ingress Controller.

  ```sh
  cd ~/environment

  mkdir -p manifests/alb-ingress-controller && cd manifests/alb-ingress-controller

  # Final location
  /home/ec2-user/environment/manifests/alb-ingress-controller
  ```  

Before deploying the AWS Load Balancer controller, we need to do some things. Because the controller operates over the worker node, you must make it accessible to AWS ALB/NLB resources through IAM permissions. IAM permissions can install IAM Roles for ServiceAccount or attach directly to IAM Roles on the worker node.

1. First, create **IAM OpenID Connect (OIDC) identity provider** for the cluster. **IAM OIDC provider** must exist in the cluster(in this lab, eks-demo) in order for objects created by Kubernetes to use [**service account**](/https://kubernetes.io/ko/docs/reference/access-authn-authz/service-accounts-admin/)  which purpose is to authenticate to API Server or external services.

    ```sh
    eksctl utils associate-iam-oidc-provider \
    --region ${AWS_REGION} \
    --cluster eks-demo \
    --approve
    ```  

{: .warning}  
Let's find out a little more here.

* The IAM OIDC identity provider you create can be found in Identity providers menu on IAM console or in the commands below.
* Check the OIDC provider URL of the cluster through the commands below.

  ![3](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/3.png)

  Result from the command have the following format:

  ```sh
  https://oidc.eks.ap-northeast-2.amazonaws.com/id/8A6E78112D7F1C4DC352B1B511DD13CF
  ```

* Copy the value after **/id/** from the output above, then execute the command as shown below.

  ```sh
  aws iam list-open-id-connect-providers | grep 8A6E78112D7F1C4DC352B1B511DD13CF
  ```

* If the result appears, **IAM OIDC identity provider** is created in the cluster, and if no value appears, you must execute the creation operation again.

2. Create an IAM Policy to grant to the AWS Load Balancer Controller.

    ```sh
    curl -o iam-policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.4/docs/install/iam_policy.json
    ```

    ```sh
    aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam-policy.json
    ```

    ![4](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/4.png)

3. Create ServiceAccount for AWS Load Balancer Controller.

    ```sh
    eksctl create iamserviceaccount \
    --cluster eks-demo \
    --namespace kube-system \
    --name aws-load-balancer-controller \
    --attach-policy-arn arn:aws:iam::$ACCOUNT_ID:policy/AWSLoadBalancerControllerIAMPolicy \
    --override-existing-serviceaccounts \
    --approve
    ```  

    ![5](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/5.png)

When deploying an EKS cluster, you can also add the IAM policy associated with the AWS Load Balancer Controller to the Worker node in the form of Addon. However, in this lab, we will conduct with the reference, [**here**](/https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/deploy/installation/).

Also, please refer simple hands on lab about IAM roles for service accounts([**IRSA**](/<https://aws.amazon.com/blogs/opensource/introducing-fine-grained-iam-roles-service-accounts/) ) in [**here**](/https://aws.amazon.com/premiumsupport/knowledge-center/eks-restrict-s3-bucket/?nc1=h_ls).

### Add Controller to Cluster

1. Add AWS Load Balancer controller to the cluster. First, install [**cert-manager**](/https://github.com/jetstack/cert-manager)  to insert the certificate configuration into the Webhook. **Cert-manager** is an open source that automatically provisions and manages TLS certificates within a Kubernetes cluster.

    ```sh
    kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.5.4/cert-manager.yaml
    ```

    ![6](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/6.png)

2. Download Load balancer controller yaml file.

    ```sh
    wget https://github.com/kubernetes-sigs/aws-load-balancer-controller/releases/download/v2.4.4/v2_4_4_full.yaml
    ```  

    ![7](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/7.png)

3. In yaml file, edit cluster-name to **eks-demo**.

    ```sh
    vi v2_4_4_full.yaml
    ```

    ```yml
    spec:
        containers:
        - args:
            - --cluster-name=eks-demo # Insert EKS cluster that you created
            - --ingress-class=alb
            image: amazon/aws-alb-ingress-controller:v2.4.4
    ```

      ![8](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/8.png)  

    And remove the ServiceAccount yaml spec written in the yaml file. This is because we have already created a ServiceAccount for AWS Load Balancer Controller. Delete the contents below and save the yaml file.

    ![9](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/9.png)

    After done.
    ![10](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/10.png)  

4. Deploy **AWS Load Balancer controller** file.

    ```sh
    kubectl apply -f v2_4_4_full.yaml
    ```

    ![11](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/11.png)

5. Check that the deployment is successed and the controller is running through the command below. When the result is derived, it means success.

    ```sh
    kubectl get deployment -n kube-system aws-load-balancer-controller
    ```  

    ![12](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/12.png)

    In addition, the command below shows that service account has been created.

    ```sh
    kubectl get sa aws-load-balancer-controller -n kube-system -o yaml
    ```  

    ![13](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/13.png)

Pods running inside the cluster for the necessary functions are called Addon. Pods used for add-on are managed by the Deployment, Replication Controller, and so on. And the namespace that this add-on uses is kube-system. Because the namespace is specified as kube-system in the yaml file, it is successfully deployed when the pod name is derived from the command above. You can also check the relevant logs with the commands below.

```sh
kubectl logs -n kube-system $(kubectl get po -n kube-system | egrep -o "aws-load-balancer[a-zA-Z0-9-]+")
```

![14](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/14.png)
![15](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/15.png)

Detailed property values are available with the commands below.

```sh
ALBPOD=$(kubectl get pod -n kube-system | egrep -o "aws-load-balancer[a-zA-Z0-9-]+")

kubectl describe pod -n kube-system ${ALBPOD}
```

![16](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/16.png)
![17](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/06.CreateIngressController/pics/17.png)
