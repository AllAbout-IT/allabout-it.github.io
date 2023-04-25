---
layout: default
title: Container Image
parent: 01.Architecture Application by AWS EKS
grand_parent: AWS Workshop Studio
# great_grand_parent: PROJECT
# has_children: true
nav_order: 1004
# permalink: /docs/01.PROJECT
---
# Container Image
{: .no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

* **Docker**  
[**Docker**](/https://aws.amazon.com/docker/?nc1=h_ls) is a software platform that allows you to build, test and deploy containerized applications. Docker packages software into standardized units called containers, which contain everything you need to run the software, including libraries, system tools, code, runtime, and so on.

  To learn more about Docker, click [**here**](/https://www.docker.com/resources/what-container/).

* **Container Image**  
Container image is a combination of the files and settings required to run the container. These images can be uploaded and downloaded in the repository. And the state in which the image was executed is container. Container images can be downloaded and used by official image repositories such as [**Docker Hub**](/https://aws.amazon.com/blogs/containers/deploy-applications-on-amazon-ecs-using-docker-compose/) or created directly.

## Build Container Image

{. note: }  
This part is an independent lab for those who want to learn more about containers and container images. If you don't proceed with this lab, you won't have any problem with **configuring web application with Amazon EKS**. If you don't want this lab, move onto the Upload Image to **Amazon ECR chapter**.

### Create Container Image Yourself

![1](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/1.png)

**Docker** File is a **setup file for building container images**. That is, think of it as a blueprint for the image to be built. When these images become containers, the application is actually running.

* Paste the values below in the root folder(/home/ec2-user/environment).

  ```sh
  cd ~/environment/
  ```

  ```sh
  cat << EOF > Dockerfile
  FROM nginx:latest
  RUN  echo '<h1> test nginx web page </h1>'  >> index.html
  RUN cp /index.html /usr/share/nginx/html
  EOF

  ```

  Instruction component in the Docker File is as follows.

  1. **FROM**: Set the Base Image(Specify OS or version)

  2. **RUN** : Execute any commands in a new layer on top of the current image and commit the results

  3. **WORKDIR**: Where to perform instructions such as RUN, CMD, ENTRYPOINT, COPY, ADD in the Docker File

  4. **EXPOSE**: Specify the port number to connect to the host

  5. **CMD**: Commands for running application

* Create an image with the docker build command. In name, enter the name of the container image and in case of tag, if not named, you will have a value called latest. In this lab, you will write test-image by container image name.

  ```sh
  docker build -t test-image .
  ```  

  ![2](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/2.png)

* Check the images created with the **docker images command**.

  ```sh
  docker images
  ```

  ![3](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/3.png)

* Run the image as a container with the **docker run command**. The command below uses a container image named test-image to run a container named test-nginx, which means that 8080 ports of the host and 80 ports of the container are mapped.

  ```sh
  docker run -p 8080:80 --name test-nginx test-image
  ```

* You can use the docker ps command to check which containers are running on the current host. **Open a new terminal on AWS Cloud9** and type the command below.

  ```sh
  curl http://localhost:8080
  ```  

  ![5](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/5.png)

  ```sh
  docker ps
  ```  

  ![6](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/6.png)

* You can check the status by outputting logs from the container with the **docker logs command**.

  ```sh
  docker logs -f test-nginx
  ```

  ![7](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/7.png)

* You can access into the inside shell environment of the container with **docker exec command**. After access, you can apprehend the internal structure and exit through the **exit** command.

  ```sh
  docker exec -it test-nginx /bin/bash
  ```

  ![9](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/9.png)

* In AWS cloud9, you can see which applications are currently running by clicking the top Tools > Preview > Preview Running Application.

  ![8](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/8.png)

  ![10](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/10.png)
  If you see notification message from new pop-up window, you have to change to allow third-party cookies at IDE configuration. and reload again. Also, you can find more detailed information at [here](/https://docs.aws.amazon.com/cloud9/latest/user-guide/troubleshooting.html#troubleshooting-preview).

  For example(in chrome)

  1. Chrome > settings > Privacy and security > Cookies and other site data  
  ![12](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/12.png)
  ![13](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/13.png)
  ![14](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/14.png)
  ![15](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/15.png)
  
  2. Select **Block third-party cookies in incognito** on General settings list.
  ![16](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/16.png)
  
* try to open preview on cloud9 after fixing you fixed

  ![11](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/11.png)  

* Stop running containers with **docker stop command**.

  ```sh
  docker stop test-nginx
  ```

  ![17](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/17.png)

* Delete the container with the **docke rm command**. The container deletion is possible only when the container is stopped.  

  ```sh
  docker rm test-nginx
  ```  

  ![18](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/18.png)

* Delete the container image with **docke rmi command**.

  ```sh
  docker rmi test-image
  ```  

  ![19](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/19.png)

## Upload container image to Amazon ECR

### Create Amazon ECR Repository and Upload Image

Create repositories and upload container images in the docker container registry **Amazon Elastic Container Registry(ECR)**.

Amazon Elastic Container Registry([Amazon ECR](/https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html) is an AWS managed container image registry service that is secure, scalable, and reliable. Amazon ECR supports private container image repositories with resource-based permissions using AWS IAM. This is so that specified users or Amazon EC2 instances can access your container repositories and images. You can use your preferred CLI to push, pull, and manage Docker images, Open Container Initiative (OCI) images, and OCI compatible artifacts.

* Download the source code to be containerized through the command below.

  ```sh
  git clone https://github.com/joozero/amazon-eks-flask.git
  ```

  ![22](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/22.png)

* Through the AWS CLI, create an image repository. In this lab, we will set the repository name to **demo-flask-backend**. Also, specify AWS Region code(for example, ap-northeast-2) to deploy the EKS cluster in **--region**'s value.

  ```sh
  aws ecr create-repository \
  --repository-name demo-flask-backend \
  --image-scanning-configuration scanOnPush=true \
  --region ${AWS_REGION}
  ```

  **--repository-name**: Sets the name of the new repository.
  **--image-scanning-configuration scanOnPush=true**: Enables image scanning when pushing images to the repository.
  **--region ${AWS_REGION}**: Sets the AWS region where the repository will be created.

  ![23](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/23.png)

* When you enter this CLI, information about the repository is derived from the resulting value. You can also find the repositories created in the [**Amazon ECR Console**](/https://us-east-1.console.aws.amazon.com/ecr/repositories?region=us-east-1).

  ![24](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/24.png)

{: .warning }
For the tasks below, your personal account information will be included. Click on the repository you just created on the [**Amazon ECR Console**](/https://us-east-1.console.aws.amazon.com/ecr/get-started?region=us-east-1) , then click View push commands in the upper right corner to find the guide below.

* Elastic Container Registry > Repositories > [Repository name] > View push commands
  ![25](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/25.png)
  ![31](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/31.png)
* To push the container image to the repository, bring the authentication token and pass the authentication to the **docker login** command. At this point, specify the user name as AWS and specify the Amazon ECR registry URI that you want to authenticate with.

  ```sh
  aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
  ```

{: .warning: }
If the above command does not work properly, check whether environment variable named ACCOUNT_ID is called in the terminal.

* Input the **downloaded source code location(for example, /home/ec2-user/environment/amazon-eks-flask)** and enter the command below to build the docker image.

  ```sh
  cd ~/environment/amazon-eks-flask

  docker build -t demo-flask-backend .
  ```

* When the image is built, use the **docker tag command** to enable it to be pushed to a specific repository.

  ```sh
  docker tag demo-flask-backend:latest $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/demo-flask-backend:latest
  ```  

* Push the image into the repository via the docker push command.

  ```sh
  docker push $ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/demo-flask-backend:latest
  ```  

  ![27](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/27.png)
  ![28](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/28.png)
  ![29](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/04.ContainerImage/pics/29.png)
