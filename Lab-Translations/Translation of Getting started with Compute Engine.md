# GCP Fundamentals: Getting Started with Compute Engine

  Objectives
  In this lab, you will learn how to perform the following tasks:
- Create a Compute Engine virtual machine using the gcloud command-line   interface.

- Connect between the two instances.

## Task 1: Sign in into Google Cloud Platform Console

1. After signing in, launch cloud shell or cloud SDK. Then configure it with your project ID using the command below:

    gcloud config set project [PROJECT_ID]

2. Next would be to set default region and zone like this:

    gcloud config set compute/zone us-central1-c

### Task 2

1. Creating a virtual machine instance called chukwunonso-vm-1 in that zone, execute this command in cloud shell:

    gcloud compute instances create "chukwunonso-vm-1" \
--machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image "debian-9-stretch-v20200902" \
--subnet "default" --tags=http-server


2. Create Firewall rule. Enter the command below in cloud shell. Change [PROJECT_ID] to your project ID

gcloud compute --project=[PROJECT_ID] firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server

3.This will create virtual machine instance


#### Task 3
    Create another virtual machine instance 
1. Set your default zone using this command:

    gcloud config set compute/zone us-central1-f

2. To create a virtual machine instance called 'chukwunonso-vm-2' in the set zone, run this command in cloud shell:

gcloud compute instances create "chukwunonso-vm-2" \
--machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image "debian-9-stretch-v20200902" \
--subnet "default"

3. Allow few minutes for the VM to launch


##### Task 4
Connect between two VM instances

1. This will be done in cloud shell. Note the instance 'chukwunonso-vm-1' which will be refered to as [INSTANCE_NAME_1].

Use ping command to confirm that chukwunonso-vm-2 can reach chukwunonso-vm-1 over the network. Run this command in cloud shell:

    gcloud compute ssh chukwunonso-vm-2 --zone=us-central1-f

This will allow you to ssh into 'chukwunonso-vm-2'

Ping chukwunonso-vm-1 from chukwunonso-vm-2 command prompt using the instance name. Run this command:

    ping [INSTANCE_NAME_1].[ZONE].c.[PROJECT_ID].internal -c 3

Replace [INSTANCE_NAME_1] with 'chukwunonso-vm-1', replace [ZONE] with 'us-central1-c' and [PROJECT_ID] with your project ID

The ping will run three times and stop with zero loss.



2. Use ssh command to open a command prompt on chukwunonso-vm-1 from chukwunonso-vm-2:
    
    gcloud compute ssh chukwunonso-vm-1 --zone=us-central1-c

3. At the command prompt on chukwunonso-vm-1, install Nginx web server. Run the command:

      sudo apt-get install nginx-light -y

4. Use the nano text editor to add a custom message to the home page of the web server. Run this command:

      sudo nano /var/www/html/index.nginx-debian.html

5. Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:

      Hi from Chukwunonso

6. Press Ctrl+O and then press Enter and then press Ctrl+X to exit the nano text editor.

7. Exit the editor and confirm that the web server is serving your new page. At the command prompt on chukwunonso-vm-1, execute this command:

      curl http://localhost/

8. Result: The response will be the HTML source of the web server's home page, including the line of custom text 'Hi from Chukwunonso'.

9. To exit the command prompt on chukwunonso-vm-1, execute this command:

       exit

9. To confirm that chukwunonso-vm-2 can reach the web server on chukwunonso-vm-1, at the command prompt on chukwunonso-vm-2, execute this command:

       curl http://chukwunonso-vm-1/

Result: The response will again be the HTML source of the web server's home page, including the line of custom text ('Hi from Chukwunonso').

10. Now get the external IP of the chukwunonso-vm-1 instance from this command:

       gcloud compute instances list --zone us-central1-a

11. Paste the copied IP address of chukwunonso-vm-1 into a new browser tab and hit enter:

Result: You will see your web server's home page, including the custom text.