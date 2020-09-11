# Lab: Google Cloud Fundamentals: Getting Started with GKE

 Objectives:

In this lab, you will learn how to perform the following tasks:

 - Provision a Kubernetes cluster using Kubernetes Engine.

 - Deploy and manage Docker containers using kubectl.


## Task 1: Sign in to the Google Cloud Platform

- Sign in into GCP through cloud shell by executing this command:

      gcloud auth login

- Set the default project by running the command:

      gcloud config set project [PROJECT_ID]

### Task 2: Confirm that needed APIs are enabled


1. Use the gcloud services command to confirm that both the Kubernetes Engine API and the Containers Registry API are enabled. To confirm, run the command:

        gcloud services list --enabled
    
  Result: Both API's are enabled.


#### Task 3: Start a Kubernetes Engine cluster

1. Assign your zone to an environment variable called MY_ZONE. To assign run the command:

        export MY_ZONE=us-central1-c
    
2. Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster 'webfrontend' and configure it to run 2 nodes. Execute the command below:

        gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

3. After the cluster is created, check your installed version of Kubernetes using the 'kubectl version' command:

        kubectl version

4. View your running nodes in cloud shell by running the command:

       kubectl get nodes


##### Task 4: Run and deploy a container

1. Launch a single instance of the nginx container in cloud shell by executing the command:

        kubectl create deploy nginx --image=nginx:1.17.10

2. View the pod running the nginx container:

        kubectl get pods

3. Expose the nginx container to the Internet with loadbalancer:

        kubectl expose deployment nginx --port 80 --type LoadBalancer

4. View the new service with the command:

        kubectl get services

- Result: The external IP address to view your webserver's home page is displayed.

5. Scale up the number of pods running on your service with the command:

        kubectl scale deployment nginx --replicas 3

6. Confirm that Kubernetes has updated the number of pods:

        kubectl get pods

7. Confirm that your external IP address has not changed:

        kubectl get services

- Result: The IP address did not change.