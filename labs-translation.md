# Lab: Google Cloud Fundamentals: Getting Started with Compute Engine

## Objectives

In this lab, you will learn how to perform the following tasks:

- Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

- Create a Compute Engine virtual machine using the gcloud command-line interface.

- Connect between the two instances.

## Steps

1.  Create a virtual machine using the GCP Console.
    gcloud compute instances create my-vm-1 --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v2090213" --subnet "default" --tags http

    gcloud compute firewall-rules create allow-http --action=ALLOW --direction=INGRESS --rules=tcp:80 --target-tags=http

2.  Create a virtual machine using the gcloud command line
    gcloud config set compute/zone us-central1-b

    gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

3.  Connect between VM instances

a) Use the ping command to confirm that my-vm-2 can reach my-vm-1 - Connect to my-vm-2:
gcloud compute ssh my-vm-2

    - ping my-vm-1 froom my-vm-2:

        ping -c 4 my-vm-1

    - Use the ssh command to open a command prompt on my-vm-1 from my-vm-2:

        ssh my-vm-1

    - At the command prrompt on my-vm-1, install the nginx web server:
        sudo apt-get install nginx-light -y

    - Use the nano text editor to add a custom message to the home page of the web server:

        sudo nano /var/www/html/index.nginx-debian.html

    - Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:

        Hi from Douglas

    - Exit the editor then confim that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:

        curl http://localhost/

        Result: response will again be the HTML source of the web server's home page, including your line of custom text.

    - To exit the command prompt on my-vm-1, execute this command:

        exit

    - To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:

        curl http://my-vm-1/

        Result: response will again be the HTML source of the web server's home page, including your line of custom text.

b) Get the external IP of my-vm-1 instance

    gcloud compute instances list --zone us-central1-a

    Paste it into the address bar of a new browser tab. You will see your web server's home page, including your custom text.

# Lab: GCP Fundamentals: Getting Started with Cloud Storage and Cloud SQL

## Objectives

In this lab, you learn how to perform the following tasks:

- Create a Cloud Storage bucket and place an image into it.

- Create a Cloud SQL instance and configure it.

- Connect to the Cloud SQL instance from a web server.

- Use the image in the Cloud Storage bucket on a web page.

## Steps

1. Deploy a web server VM instance
2. Create a Cloud Storage bucket using the gsutil command line
3. Create the Cloud SQL instance
4. Configure an application in a Compute Engine instance to use Cloud SQL
5. Configure an application in a Compute Engine instance to use a Cloud Storage object

# Lab : Google Cloud Fundamentals: Getting Started with App Engine

## Objectives

n this lab, you learn how to perform the following tasks:

- Initialize App Engine.

- Preview an App Engine application running locally in Cloud Shell.

- Deploy an App Engine application, so that others can reach it.

- Disable an App Engine application, when you no longer want it to be visible.

## Steps

1.  Initialize App Engine

    - Initialize your App Engine app with your project and choose its region:
      gcloud app create --project=\$DEVSHELL_PROJECT_ID

    - Clone the source code repository for a sample application in the hello_world directory:
      git clone https://github.com/GoogleCloudPlatform/python-docs-samples

    - Navigate to the source directory:
      cd python-docs-samples/appengine/standard_python3/hello_world

2.  Run Hello World application locally

    - Execute the following command to download and update the packages list.

      sudo apt-get update

    - Set up a virtual environment in which you will run your application. Python virtual environments are used to isolate package installations from the system.

      sudo apt-get install virtualenv

    - If prompted [Y/n], press Y and then Enter.

      virtualenv -p python3 venv

    - Activate the virtual environment.

      source venv/bin/activate

    - Navigate to your project directory and install dependencies.

      pip install -r requirements.txt

    - Run the application:

      python main.py

    - In Cloud Shell, click Web preview (Web Preview) > Preview on port 8080 to preview the application. To access the Web preview icon, you may need to collapse the Navigation menu.

      Result: See 'Hello World' in preview screen

    - verify app is not deployed

      gcloud app versions list

3.  Deploy and run Hello World on App Engine

    - Navigate to the source directory:

      cd ~/python-docs-samples/appengine/standard_python3/hello_world

    - Deploy your Hello World application

      gcloud app deploy

      If prompted "Do you want to continue (Y/n)?", press Y and then Enter. This app deploy command uses the app.yaml file to identify project configuration.

    - Launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com
      https://qwiklabs-gcp-02-7502520b3295.uc.r.appspot.com/

      gcloud app browse

    - Copy and paste the URL into a new browser window.

      Result: web page with 'Hello World'

4.  Disable the application

    -
    -
    -
    -
    -
