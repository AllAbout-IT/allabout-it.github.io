---
layout: default
title: 07.Deploy Microservices
parent: 01.Architecture Application by AWS EKS
grand_parent: AWS Workshop Studio
# great_grand_parent: PROJECT
# has_children: true
nav_order: 1007
# permalink: /docs/01.PROJECT
---
# Deploy Microservices
{:. no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

In this lab, you will learn how to deploy the backend, frontend to Amazon EKS, which makes up the web service. The order in which each service is deployed is as follows.

![1](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/1.png)

* Download source code from git repository
* Create a repository for each container image in Amazon ECR
* Build container image from source code location, including Dockerfile, and push to repository
* Create and deploy Deployment, Service, Ingress manifest files for each service.

The figure below shows the order in which end users access the web service.

![2](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/2.png)

## Deploy First Backend Service

The architecture from now on would be shown below.

![3](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/3.png)

### Deploy flask backend

{: .note}  
To proceed with this lab, **Upload container image to Amazon ECR** part must be preceded.

1. Move on to **manifests folder**(/home/ec2-user/environment/manifests).

    ```sh
    cd ~/environment/manifests/
    ```  

2. Create deploy manifest.

    ```yml
    cat <<EOF> flask-deployment.yaml
    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: demo-flask-backend
      namespace: default
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: demo-flask-backend
      template:
        metadata:
          labels:
            app: demo-flask-backend
        spec:
          containers:
            - name: demo-flask-backend
              image: $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/demo-flask-backend:latest
              imagePullPolicy: Always
              ports:
                - containerPort: 8080
    EOF
    ```  

    ![5](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/5.png)

3. Next, create **service manifest**.

    ```yml
    cat <<EOF> flask-service.yaml
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: demo-flask-backend
      annotations:
        alb.ingress.kubernetes.io/healthcheck-path: "/contents/aws"
    spec:
      selector:
        app: demo-flask-backend
      type: NodePort
      ports:
        - port: 8080
          targetPort: 8080
          protocol: TCP
    EOF
    ```  

    ![6](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/6.png)

4. Finally, create **ingress manifest**.

    ```sh
    cat <<EOF> flask-ingress.yaml
    ---
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
        name: "flask-backend-ingress"
        namespace: default
        annotations:
          kubernetes.io/ingress.class: alb
          alb.ingress.kubernetes.io/scheme: internet-facing
          alb.ingress.kubernetes.io/target-type: ip
          alb.ingress.kubernetes.io/group.name: eks-demo-group
          alb.ingress.kubernetes.io/group.order: '1'
    spec:
        rules:
        - http:
            paths:
              - path: /contents
                pathType: Prefix
                backend:
                  service:
                    name: "demo-flask-backend"
                    port:
                      number: 8080
    EOF
    ```  

    ![7](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/7.png)  

5. Deploy the manifest created above in the order shown below. Ingress provisions Application Load Balancer(ALB).

    ```sh
    kubectl apply -f flask-deployment.yaml
    kubectl apply -f flask-service.yaml 
    kubectl apply -f flask-ingress.yaml
    ```  

    ![8](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/8.png)  

6. Paste the results of the following command into the Web browser or API platform(like Postman) to check:

    ```sh
    echo http://$(kubectl get ingress/flask-backend-ingress -o jsonpath='{.status.loadBalancer.ingress[*].hostname}')/contents/aws
    ```  

    ![9](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/9.png)

## Deploy Express backend

The architecture from now on would be shown below.

![4](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/4.png)

1. Move on to **manifests folder**(/home/ec2-user/environment/manifests).

    ```sh
    cd ~/environment/manifests/
    ```

2. Create **deploy manifest** which contains built pre-built container image.

    ```yml
    cat <<EOF> nodejs-deployment.yaml
    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: demo-nodejs-backend
      namespace: default
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: demo-nodejs-backend
      template:
        metadata:
          labels:
            app: demo-nodejs-backend
        spec:
          containers:
            - name: demo-nodejs-backend
              image: public.ecr.aws/y7c9e1d2/joozero-repo:latest
              imagePullPolicy: Always
              ports:
                - containerPort: 3000
    EOF
    ```  

    ![10](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/10.png)  

3. And then, create **service manifest file**.

    ```yml
    cat <<EOF> nodejs-service.yaml
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: demo-nodejs-backend
      annotations:
        alb.ingress.kubernetes.io/healthcheck-path: "/services/all"
    spec:
      selector:
        app: demo-nodejs-backend
      type: NodePort
      ports:
        - port: 8080
          targetPort: 3000
          protocol: TCP
    EOF
    ```  

    ![11](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/11.png)  

4. create **ingress manifest**.  

    ```yml
    cat <<EOF> nodejs-ingress.yaml
    ---
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: "nodejs-backend-ingress"
      namespace: default
      annotations:
        kubernetes.io/ingress.class: alb
        alb.ingress.kubernetes.io/scheme: internet-facing
        alb.ingress.kubernetes.io/target-type: ip
        alb.ingress.kubernetes.io/group.name: eks-demo-group
        alb.ingress.kubernetes.io/group.order: '2'
    spec:
      rules:
      - http:
            paths:
              - path: /services
                pathType: Prefix
                backend:
                  service:
                    name: "demo-nodejs-backend"
                    port:
                      number: 8080
    EOF
    ```  

    ![12](/\docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/12.png)  

5. Deploy the manifest files.

    ```sh  
    kubectl apply -f nodejs-deployment.yaml
    kubectl apply -f nodejs-service.yaml
    kubectl apply -f nodejs-ingress.yaml
    ```

    ![13](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/13.png)  

6. Paste the results of the following command into the Web browser or API platform(like Postman) to check.  

    ```sh
    echo http://$(kubectl get ingress/nodejs-backend-ingress -o jsonpath='{.status.loadBalancer.ingress[*].hostname}')/services/all
    ```  

    ![14](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/14.png)  

## Deploy Frontend Service

### Deploy React Frontend  

Once you have deployed two backend services, you will now deploy the frontend to configure the web page's screen.

1. Download the source code to be containerized through the command below.

    ```sh
    cd /home/ec2-user/environment
    git clone <https://github.com/joozero/amazon-eks-frontend.git>
    ```  

    ![15](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/15.png)

2. Through AWS CLI, create an image repository. In this lab, we will set the repository name to **demo-frontend**.

    ```sh
    aws ecr create-repository \
    --repository-name demo-frontend \
    --image-scanning-configuration scanOnPush=true \
    --region ${AWS_REGION}
    ```

    ![16](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/16.png)

3. To spray two backend API data on the web screen, we have to change source code. Change the url values in **App.js** file and **page/upperPage.js** file from the frontend source code(location: /home/ec2-user/environment/amazon-eks-frontend/src).  

    ![18](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/18.png)

    Environment > amazon-eks-frontend > src > App.js  

    ![17](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/17.png)
    ![19](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/19.png)  

    In the above source code, paste the values derived from the result (ingress addresses) below.

    Environment > amazon-eks-frontend > src > page > UpperPage.js  

    ![20](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/20.png)

    ![22](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/22.png)

    ```sh
    echo http://$(kubectl get ingress/flask-backend-ingress -o jsonpath='{.status.loadBalancer.ingress[*].hostname}')/contents/'${search}'
    ```  

    ![21](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/21.png)  

4. Execute the following command in the location of the amazon-eks-frontend folder.

    ```sh
    cd /home/ec2-user/environment/amazon-eks-frontend
    npm install
    npm run build
    ```

    ![23](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/23.png)
    ![24](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/24.png)

5. Refer [**Upload container image to Amazon ECR**](/https://catalog.us-east-1.prod.workshops.aws/workshops/9c0aa9ab-90a9-44a6-abe1-8dff360ae428/en-US/40-container/200-eks) guide and proceed to create container image repository and push image. In this lab, set the image repository name to demo-frontend.

    ```sh
    docker build -t demo-frontend .

    docker tag demo-frontend:latest $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/demo-frontend:latest
    ```

    ![25](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/25.png)

    ```sh
    docker push $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/demo-frontend:latest
    ```  

    ![26](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/07.DeployMicroservices/pics/26.png)  

    {: .warning}  
    During applying above CLI, if you receive message which said denied: Your authorization token has expired. Reauthenticate and try again., then applying bottom command line and do this again

    ```sh
    aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
    ```  

6. Move to manifests folder. At this point, type image value to demo-frontend repository URI.  

    ```yml
    cd /home/ec2-user/environment/manifests

    cat <<EOF> frontend-deployment.yaml
    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: demo-frontend
      namespace: default
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: demo-frontend
      template:
        metadata:
          labels:
            app: demo-frontend
        spec:
          containers:
            - name: demo-frontend
              image: $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/demo-frontend:latest
              imagePullPolicy: Always
              ports:
                - containerPort: 80
    EOF
    ```  

    ```yml
    cat <<EOF> frontend-service.yaml
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: demo-frontend
      annotations:
        alb.ingress.kubernetes.io/healthcheck-path: "/"
    spec:
      selector:
        app: demo-frontend
      type: NodePort
      ports:
        - protocol: TCP
          port: 80
          targetPort: 80
    EOF
    ```

    ```yml
    cat <<EOF> frontend-ingress.yaml
    ---
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: "frontend-ingress"
      namespace: default
      annotations:
        kubernetes.io/ingress.class: alb
        alb.ingress.kubernetes.io/scheme: internet-facing
        alb.ingress.kubernetes.io/target-type: ip
        alb.ingress.kubernetes.io/group.name: eks-demo-group
        alb.ingress.kubernetes.io/group.order: '3'
    spec:
      rules:
        - http:
            paths:
              - path: /
                pathType: Prefix
                backend:
                  service:
                    name: "demo-frontend"
                    port:
                      number: 80
    EOF
    ```  

    ```sh
    kubectl apply -f frontend-deployment.yaml
    kubectl apply -f frontend-service.yaml
    kubectl apply -f frontend-ingress.yaml
    ```