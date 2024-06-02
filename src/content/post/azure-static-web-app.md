---
title: 'Deploying a Vue or React App Using Azure Static Web Apps and Azure DevOps'
description: 'This post is purely for testing if the css is correct for the title on the page'
publishDate: '01 Jun 2024'
tags: ['AzureStaticWebApps', 'AzureDevOps', 'web-development', 'Azure', 'DevOps']
draft: false
coverImage:
  src: './azure-devops.jpg'
  alt: 'Azure DevOps'
---

Deploying a frontend application with Azure Static Web Apps integrated with Azure DevOps leverages the power of continuous integration and continuous deployment (CI/CD). This guide will walk you through the detailed steps to achieve a seamless deployment of your Vue or React application.

## Step 1: Log into Azure Portal

1. Access the [Azure Portal](https://portal.azure.com/).
2. Navigate to **App Services** and select **Static Web App**.

## Step 2: Select or Create a Resource Group

1. Choose an existing resource group if available.
2. To create a new resource group, click on **Create new**. Use a clear and consistent naming convention (e.g., `rg-myproject-prod`).

## Step 3: Configure Static Web App

1. Enter a unique name for your Static Web App.
2. Choose the appropriate hosting plan:
   - **Free**
   - **Standard**
   - **Dedicated**
     Click **Compare plans** to understand the differences and select the best option.

## Step 4: Set Up Deployment with Azure DevOps

1. Under **Deployment details**, select **Azure DevOps**.
2. Authenticate and choose your Azure DevOps organization.
3. Select the project, repository, and branch for the deployment.

## Step 5: Configure Build Details

1. Select from the available build presets or configure a custom build preset.
2. Define the **App location**:
   - `/` if the code is in the root directory
   - `/app` if the code is in a folder named `app`
3. Specify the **API location**:
   - `/api` if you have Azure Functions code in an `api` folder.
4. Set the **Output location**:
   - For example, if the build output is in `build` within the app directory, set it to `build`.

## Step 6: Advanced Deployment Settings

1. If uncertain about some deployment details, select **Other** to allow post-deployment adjustments.
2. Click **Next: Advanced** to choose the region for Azure Functions and configure staging environments.

## Step 7: Add Tags and Review

1. Add relevant tags for resource management and tracking.
2. Click **Next** to review all configurations.
3. If everything is correct, click **Create** to initiate the deployment.

## Step 8: Deployment Process

1. You will be redirected to a deployment page.
2. Wait for the deployment to complete. This can take a few minutes.
3. Once completed, a notification saying "Your Deployment is complete" will appear.
4. Click **Go to Resource** to navigate to your newly created Static Web App.

## Step 9: Verify Azure DevOps Pipeline

1. Navigate to your Azure DevOps project.
2. Inspect the pipeline for any failures or issues.
3. Click on **Deployment history** to view Azure DevOps pipeline runs.
4. Your repository will automatically be added with a YAML file. Review and modify this file to:
   - Add deployment approval checks.
   - Configure different deployment slots (e.g., staging and production).
   - To add a staging slot, include `deployment_environment: staging` under the `AzureStaticWebApp@0` task in the YAML file.

## Step 10: Verify and Access Your Deployed App

1. Once the pipeline run is successful, return to the Azure portal.
2. Navigate to **Static Web Apps** and select your deployed application.
3. In the **Overview** section, click on the provided URL to view your web application.

## Conclusion

Deploying a Vue or React application using Azure Static Web Apps combined with Azure DevOps provides a robust CI/CD pipeline, ensuring your app remains up-to-date with the latest code changes. This integration facilitates streamlined deployments, efficient resource management, and enhanced collaboration within your development team.

## References

- [Azure Static Web Apps Documentation](https://docs.microsoft.com/en-us/azure/static-web-apps/)
- [Azure DevOps Documentation](https://docs.microsoft.com/en-us/azure/devops/?view=azure-devops)

This comprehensive deployment approach not only simplifies the process but also ensures a scalable and maintainable solution for modern web applications.

**Sample `.yaml` for reference**

```yaml
name: Azure Static Web Apps CI/CD

pr:
  branches:
    include:
      - main
trigger:
  branches:
    include:
      - main

jobs:
  - job: build_and_deploy_job
    displayName: Build and Deploy Job
    condition: or(eq(variables['Build.Reason'], 'Manual'),or(eq(variables['Build.Reason'], 'PullRequest'),eq(variables['Build.Reason'], 'IndividualCI')))
    pool:
      vmImage: ubuntu-latest
    variables:
      - group: Azure-Static-Web-Apps
    steps:
      - checkout: self
        submodules: true
      - task: AzureStaticWebApp@0
        inputs:
          azure_static_web_apps_api_token: $(AZURE_STATIC_WEB_APPS_API_TOKEN_DELIGHTFUL_BAY_02378850F)
          ###### Repository/Build Configurations - These values can be configured to match your app requirements. ######
          # For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
          app_location: '/' # App source code path
          api_location: '' # Api source code path - optional
          output_location: 'dist' # Built app content directory - optional
```
