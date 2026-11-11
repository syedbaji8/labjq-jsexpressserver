# Lab: Deploying Your First Docker Image on Code Engine

![cognitiveclass.ai logo](https://images.gitbook.com/__img/dpr=2,width=760,onerror=redirect,format=auto,signature=538401116/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FIBM-CD0250EN-SkillsNetwork%2Fimages%2FIDSN-logo.png)

In this lab, you will learn how to deploy your first Docker image on Code Engine. IBM Cloud Code Engine has been made available to you through this lab environment.

**Estimated Time:** 20 minutes

## Learning Objectives

After completing this lab, you will be able to:

- Start the Code Engine service to create applications.
- Use the Code Engine service to deploy an application from a Docker image and create a remote access URL for the application.
- List the applications you have deployed.

## Deploying the Docker Image

### Step 1: Open the Code Engine CLI

Go to the **Code Engine CLI** terminal. If you do not have one, set it up first.

### Step 2: Create a Code Engine Project

In your lab environment:

1. Click the **Cloud** dropdown.
2. Choose **Code Engine**.
3. When the Code Engine setup panel appears, click **Create Project**.

![Create Code Engine Project](https://images.gitbook.com/__img/dpr=2,width=970,onerror=redirect,format=auto,signature=-552486815/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FIBM-CD0250EN-SkillsNetwork%2Flabs%2Fmodule%25204%2Fimages%2Fcode_engine.png)

### Step 3: Wait for the Environment to Prepare

The Code Engine environment may take some time to prepare. The setup panel displays the progress status.

![Code Engine Preparation](https://images.gitbook.com/__img/dpr=2,width=970,onerror=redirect,format=auto,signature=545537781/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FIBM-CD0250EN-SkillsNetwork%2Flabs%2Fmodule%25204%2Fimages%2Fcode_engine_prep.png)

### Step 4: Start the Code Engine CLI

Once the Code Engine setup is complete and active, click **Code Engine CLI** to open the pre-configured CLI in the terminal.

![Start Code Engine CLI](https://images.gitbook.com/__img/dpr=2,width=970,onerror=redirect,format=auto,signature=519015917/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FIBM-CD0250EN-SkillsNetwork%2Flabs%2Fmodule%25204%2Fimages%2Fstart_CE_CLI.png)

The CLI is pre-configured. The home directory is set to the current directory, and the project and Kubeconfig are already configured.

![Pre-configured CLI](https://images.gitbook.com/__img/dpr=2,width=970,onerror=redirect,format=auto,signature=-1740309172/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FlFJI72TNlKUD1pvePKhIQQ%2Fstep4.png)

## Deploy the Hello World Application

You will now use the CLI to deploy the **Hello World** application.

### Step 5: List Existing Applications

Run the following command to see the list of applications that currently exist:

```bash
ibmcloud ce app list
```

### Step 6: Clone the Application Source Code

You will clone the code from GitHub, Dockerize it, and deploy the web application.

The application serves one REST API endpoint at the root level and returns:

`Hello World`

Run:

```bash
git clone https://github.com/ibm-developer-skills-network/labjq-jsexpressserver
```

### Step 7: Change to the Cloned Directory

```bash
cd labjq-jsexpressserver
```

### Step 8: Build the Docker Image

Run `docker build` in the current directory and tag the image.

> **Note:** The application is named `helloworld2` because an earlier instance of `helloworld` may already exist in the project space.

```bash
docker build . -t us.icr.io/${SN_ICR_NAMESPACE}/helloworld2
```

### Step 9: Push the Docker Image

Push the image to your IBM Cloud Container Registry namespace:

```bash
docker push us.icr.io/${SN_ICR_NAMESPACE}/helloworld2
```

### Step 10: Create the Code Engine Application

Now that the image is ready for deployment, create the application.

Because the image has already been built and pushed, you do not need to specify a build source. This command creates the application and internally sets up the required infrastructure.

After a few seconds, you should receive confirmation along with the application's URL.

```bash
ibmcloud ce application create \
  --name helloworld2 \
  --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld2 \
  --registry-secret icr-secret \
  --port 5000
```

![Application Deployment](https://images.gitbook.com/__img/dpr=2,width=760,onerror=redirect,format=auto,signature=-1061213958/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FjYz1YfMS5dlRJB04CBSmew%2Fstep7.png)

### Step 11: Open the Application

Press **Ctrl** (Windows) or **Cmd** (Mac) and click the generated URL.

Alternatively:

1. Copy the URL.
2. Paste it into a browser.
3. Press **Enter**.

The **Hello World** application page should render successfully.

## Practice Exercise

1. Open the file:

   `labjq-jsexpressserver/app.js`

2. Change the message from:

   ```text
   Hello World
   ```

   to:

   ```text
   Hello yourname!
   ```

3. Save the file.
4. Build and push the Docker image again.
5. Update the application using:

```bash
ibmcloud ce application update \
  --name helloworld2 \
  --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld2 \
  --registry-secret icr-secret \
  --port 5000
```

Open the generated URL and verify that the application has been updated.

## Congratulations!

You have successfully completed this lab and deployed your first application on **IBM Cloud Code Engine**.

---

## Author

**Lavanya T S**

© IBM Corporation. All rights reserved.
