# LAB: Google Cloud Fundamentals: Getting Started with App Engine

 Objectives:

In this lab, you learn how to perform the following tasks:
- Initialize App Engine.
- Preview an App Engine application running locally in Cloud Shell.
- Deploy an App Engine application so that others can reach it.
- Disable an App Engine application when you no longer want it to be visible.

## Task 1: Initialize App Engine

- To initialize your App Engine app with a project and choose its region, run the command:

	gcloud app create --project=PROJECT_ID --region=us-central


- To clone the source code repository for a sample application in the hello_world directory, run the command:

	git clone https://github.com/GoogleCloudPlatform/python-docs-samples

- Navigate to the source directory:

	cd python-docs-samples/appengine/standard_python3/hello_world

### Task 2: Run Hello World application locally

- Execute the following command to download and update the packages list: 

	sudo apt-get update

- To set up a python virtual environment in which you will run your application, use the commands below:

	sudo apt-get install virtualenv -y

	virtualenv -p python3 venv

- To activate the virtual environment, run the command:

	source venv/bin/activate

- To navigate to your project directory and install dependencies, execute:

	pip install -r requirements.txt

- To run the application, execute the command:

	python main.py

    Please ignore the warning if any.

- In Cloud Shell, click Web preview and then click Preview on port 8080 to preview the application.
- To end the test, return to Cloud Shell and press Ctrl+C to abort the deployed service.
- Using the Cloud Console, verify that the app is not deployed. In the Cloud Console, on the Navigation menu, click App Engine and then Dashboard.
Result: No resources are deployed.

#### Task 3: Deploy and run Hello World on App Engine

To deploy your application to the App Engine Standard environment:

- Navigate to the source directory by running the command:

	cd ~/python-docs-samples/appengine/standard_python3/hello_world

- Deploy your Hello World application with the command:

	gcloud app deploy

    If prompted “Do you want to continue (Y/n)?”, press Y and then Enter.

This app deploy command uses the app.yaml file to identify project configuration.

- To launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com, run the command:

	gcloud app browse

Copy and paste the URL into a new browser window.
Result: Hello World!

##### Task 4: Disable the application

- To disable the application, run the command:

        gcloud app versions stop [APP_ID]

Result: if browser is refreshed, you will get a 404 error.