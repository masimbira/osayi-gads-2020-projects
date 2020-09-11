#**LAB1: Google Cloud Fundamentals: Getting Started with Compute Engine**

**##OBJECTIVES:**

1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
2. Create a Compute Engine virtual machine using the gcloud command-line interface.
3. Connect between the two instances.

**##STEPS:**

1. ## Create a virtual machine using the GCP Console:

   ```
   gcloud compute instances create "my-vm-1" \ 
   
   --machine-type "n1-standard-1" \ 
   
   --image-project "debian-cloud" \
   
    --image "debian-9-stretch-v20190213" \ 
   
   --subnet "default"\
   
   --tags http
   ```

   

2. ## Create a virtual machine using the gcloud command line

   ```
   gcloud config set compute/zone us-central1-b
   
   gcloud compute instances create "my-vm-2" \ 
   
   --machine-type "n1-standard-1" \
   
    --image-project "debian-cloud" \ 
   
   --image "debian-9-stretch-v20190213" \ 
   
   --subnet "default"
   ```

   

3. ##  Connect between VM instances

   - [ ] Use the `ping` command to confirm that **my-vm-2** can reach **my-vm-1** over the network:

     - Connect to my-vm-2:

          ```
       gcloud compute ssh my-vm-2
          ```

          

     - ping my-vm-1 from my-vm-2

          ```
       ping -c 4 my-vm-1
          ```

          

     - Use ssh command to open a command prompt on my-vm-1 from my-vm-2:

          ```
       ssh my-vm-1
          ```

          

     - At the command prompt on my-vm-1, install the Nginx web server:

       ```
        sudo apt-get install nginx-light -y
       ```

       

     - Use the **nano** text editor to add a custom message to the home page of the web server:

          ```
       sudo nano /var/www/html/index.nginx-debian.html
          ```
   
       
   
  -  Add text like this, and replace YOUR_NAME with your name:
   
     ***Hi from YOUR_NAME***
   
     - Exit the nano text editor and confirm that the web server is serving your new page. At the command prompt on **my-vm-1**, execute this command:
   
       ```
       curl http://localhost/
       ```
   
       ​		Result: HTML source of the web server's home page, including your line of custom text.
   
     - To exit the command prompt on **my-vm-1**, execute this command:
   
         ```
         exit
         ```
   
         
   
     - To confirm that **my-vm-2** can reach the web server on **my-vm-1**, at the command prompt on **my-vm-2**, execute this command:
   
        ​	
        
        ```
        curl http://localhost/
        ```
        
        ​	Result:  HTML source of the web server's home page, including your line of custom text
   
       
   
   - [ ] Get External IP address for my-vm-1 from command below:
   
   ```
   gcloud compute instances list --zone us-central1-a
   ```
   
   
   ​	Copy the External IP address for **my-vm-1** and paste it into the address bar of a new browser tab:
   

   ​			   *Result: You will see your web server's home page, including your custom text.