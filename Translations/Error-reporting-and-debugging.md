# ##LAB: Error Reporting and Debugging

## #OBJECTIVES

In this lab, you learn how to perform the following tasks:

- Launch a simple Google App Engine application
- Introduce an error into the application
- Explore Cloud Error Reporting
- Use Cloud Debugger to identify the error in the code
- Fix the bug and monitor in Cloud Operations

## ##STEPS

## Task 1: Create an application

- [ ] ### Get and test the application

  1. In the Cloud Console, launch Cloud Shell by clicking **Activate Cloud Shell** 

  2. To create a local folder and get the App Engine **Hello world** application, run the following commands:

     ```
     mkdir appengine-hello cd appengine-hello gsutil cp gs://cloud-training/archinfra/gae-hello/*
     ```

  3. To run the application using the local development server in Cloud Shell, run the following command:

     ```
     dev_appserver.py $(pwd)
     ```

  4. In Cloud Shell, click **Web Preview** > **Preview on port 8080**

     ```
     RESULT: A new browser window opens to the localhost and displays the message **Hello, World!**
     ```

  5. In Cloud Shell, press  to exit the development server

     ```
     Ctrl+C
     ```

- [ ] ### Deploy the application to App Engine

  1. To deploy the application to App Engine, run the following command:

     ```
     gcloud app deploy app.yaml
     ```

  2. If prompted for a region, enter the number corresponding to a region.

  3. When prompted, type **Y** to continue.

  4. When the process is done, verify that the application is working by running the following command:

     gcloud app browse

     RESULT: Your application is displayed in a new browser window

  5. To exit the development mode press:

     ```
     Ctrl + C
     ```

- [ ] ### Introduce an error to break the application

  1. To examine the `main.py` file, run the following command:

     ```
     cat main.py
     ```

     ​		NOTE: The application imports `webapp2`

  2. To use the sed stream editor to change the import library to the nonexistent `webapp22`, run the following command:

     ```
     sed -i -e 's/webapp2/webapp22/' main.py
     ```

  3. To verify the change you made in the `main.py` file, run the following command:				

     ```
     cat main.py
     ```

     RESULT: The application now tries to import the nonexistent `webapp22`.

- [ ] ### Re-deploy the application to App Engine

  1. To  re-deploy the application to App Engine, run the following command:

     ```
     gcloud app deploy app.yaml --quiet
     ```

  2. Verify that the application is broken by running the following command:	

     ```
     gcloud app browse
     ```

     ​	RESULT: Your application is displayed in a new browser window with error messages

  3. To exit development mode press:

     ```
     	Ctrl + C
     ```

## Task 2: Explore Cloud Error Reporting

- [ ] ### 	View Error Reporting and trigger additional errors

  1. ​	In Cloud Shell, run the following command:

     ```
     gcloud app browse
     ```

     RESULT: Your application is displayed in a new browser window

  2. Click the resulting link several times to generate more errors.

     

- [ ] ### View details and identify the cause

  1. Click the Error name: **ImportError: No module named webapp22**.

     ​		RESULT: You can see a detailed graph of the errors

  2. For **Stack trace sample**, click **Parsed**. This opens the Cloud Debugger, showing the error in the code!



- [ ] ### View the logs and fix the error

  1.  In Cloud Shell, fix the error by running the following command:

     ```
     sed -i -e 's/webapp22/webapp2/' main.py
     ```

  2. To re-deploy the application to App Engine, run the following command:

     ```
     gcloud app deploy app.yaml --quiet
     ```

  3. When the process is done, to verify that the application is working again, run the following command:

     ```
     gcloud app browse
     ```

  4. On the **Cloud Error Reporting** page, ensure that **Auto Reload** is enabled to and see that no new errors are added

  

  