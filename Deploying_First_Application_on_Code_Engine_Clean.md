# Lab: Deploying Your First Application on Code Engine

![Cognitive Class Logo](https://images.gitbook.com/__img/dpr=2,width=760,onerror=redirect,format=auto,signature=538401116/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FIBM-CD0250EN-SkillsNetwork%2Fimages%2FIDSN-logo.png)

**Estimated Time:** 15 minutes

## Overview

In this lab, you will learn how to deploy a **Hello World** web application from GitHub on Code Engine. IBM Cloud Code Engine has been made available to you through this lab environment.

## Learning Objectives

After completing this lab, you will be able to:

- Start the Code Engine service to create applications.
- Use the Code Engine service to deploy an application and create a remote access URL for the application.
- List the applications you have deployed.

## Setting Up Code Engine

1. In your lab environment, click the **Cloud** dropdown and choose **Code Engine**.
2. The Code Engine setup panel will appear.
3. Click **Create Project**.

![Create Code Engine Project](https://images.gitbook.com/__img/dpr=2,width=760,onerror=redirect,format=auto,signature=-552486815/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FIBM-CD0250EN-SkillsNetwork%2Flabs%2Fmodule%25204%2Fimages%2Fcode_engine.png)

The Code Engine environment may take some time to prepare. The setup panel will display the progress status.

![Code Engine Preparation](https://images.gitbook.com/__img/dpr=2,width=760,onerror=redirect,format=auto,signature=545537781/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FIBM-CD0250EN-SkillsNetwork%2Flabs%2Fmodule%25204%2Fimages%2Fcode_engine_prep.png)

Once the Code Engine setup is complete and the environment is active, click **Code Engine CLI** to start the preconfigured CLI in the terminal.

![Start Code Engine CLI](https://images.gitbook.com/__img/dpr=2,width=760,onerror=redirect,format=auto,signature=519015917/https%3A%2F%2Fcf-courses-data.s3.us.cloud-object-storage.appdomain.cloud%2FIBM-CD0250EN-SkillsNetwork%2Flabs%2Fmodule%25204%2Fimages%2Fstart_CE_CLI.png)

The preconfigured CLI starts with the home directory set to the current directory. As part of the preconfiguration, the project and Kubeconfig have already been set up.

## Deploying Your First Application

You will now use the CLI to deploy the **Hello World** application.

### 1. List Existing Applications

Run the following command to see the list of existing applications:

```bash
ibmcloud code-engine application list
```

There will be no applications listed if this is your first time running the lab.

You can also use the shorter form:

```bash
ibmcloud ce app list
```

### 2. Deploy the Hello World Application

You will deploy a simple Express web application that serves one REST API endpoint at the root level and returns the string **Hello World**.

The application source code is available at:

`https://github.com/ibm-developer-skills-network/labjq-jsexpressserver`

Run the following command to deploy the application:

```bash
ibmcloud ce application create \
  --name helloworld \
  --build-source https://github.com/ibm-developer-skills-network/labjq-jsexpressserver \
  --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld \
  --registry-secret icr-secret \
  --port 5000
```

This command creates the application and internally sets up the required infrastructure. After a few seconds, you will receive a confirmation along with the application's URL.

Open the generated URL by using **Ctrl + Click** on Windows or **Cmd + Click** on Mac. Alternatively, copy the URL and paste it into a browser. The Hello World application page should render.

### 3. Get Application Details

To get detailed information about the deployed application, run:

```bash
ibmcloud ce app get --name helloworld
```

This command displays detailed information about the application, including:

- Creation time
- Resources used
- Number of instances
- Other application details

## Congratulations!

You have successfully completed this lab and deployed your first application on **Code Engine**.

## Author

**Lavanya T S**

© IBM Corporation. All rights reserved.
