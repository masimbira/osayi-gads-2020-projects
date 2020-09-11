**##LAB: Google Cloud Fundamentals: Getting Started with GKE**

**#OBJECTIVES:**

1. Provision a  cluster using Kubernetes Engine.
2. Deploy and manage Docker containers using `kubectl`

## STEPS:

1. ## Enable the  needed APIs  using the Google Cloud Console:

   ```
   To see a list of available services for a project use command below:
   			
   		  gcloud services list --available
   
   To enable the two needed APIs use the following command:
   
   		  gcloud services enable  Kubernetes Engine API  Container Registry API
   
   ```

2. ## Start a Kubernetes Engine cluster in  Cloud Shell

   ```
   Place the zone  assigned you to into an environment variable called MY_ZONE:
   
   ​      	export MY_ZONE=us-central1-a
   
   - Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster **webfrontend** and configure it to run 2 nodes. Command below also automatically authenticates kubectl:
   
     ​		gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
   
   - After the cluster is created, check your installed version of Kubernetes using the `kubectl version` command:
   
     ​			kubectl version
   
     -View your running nodes in the GCP Console using command:
   
     ​			gcloud compute instances list
   ```

   

3. ##  Run and deploy a container

   ```
   From your Cloud Shell prompt, launch a single instance of the nginx container.
   			kubectl create deploy nginx --image=nginx:1.17.10
   			
   View the pod running the nginx container:
   			kubectl get pods
   	RESULT:
   
   Expose the nginx container to the Internet:
   			kubectl expose deployment nginx --port 80 --type LoadBalancer
   			
   View the new service:
   			kubectl get services
   	RESULT:
   			
   Copy the displayed External-IP for your service	and paste it into a new browser tab:
   			RESULT: The default home page of the Nginx browser is displayed.
   			
   Scale up the number of pods running on your service:
   				kubectl scale deployment nginx --replicas 3
   
   Confirm that Kubernetes has updated the number of pods:
   				kubectl get pods
   		RESULT: 
   		
   Confirm that your external IP address has not changed:
     				kubectl get services
     		RESULT: 
     		
     		
   Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding				
   			
   ```

   

   

