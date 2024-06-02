---
title: 'How to Create, Configure, and Manage a Self-Hosted Agent in Azure DevOps'
description: 'Learn to create, configure, and manage a self-hosted agent in Azure DevOps for custom builds and deployments. Optimize and efficiently manage your CI/CD pipelines for greater control and flexibility.'
publishDate: '31 May 2024'
tags: ['AzureDevOps', 'SelfHostedAgent', 'CICD', 'DevOps', 'BuildPipeline', 'Deployment', 'Azure']
draft: false
coverImage:
  src: './azure-devops.jpg'
  alt: 'Azure DevOps'
---

In the intricate realm of DevOps, flexibility and granular control over your build and deployment processes are essential. While Azure DevOps offers robust cloud-hosted agents, there are scenarios where self-hosted agents become indispensable. Whether it’s for specific tool integrations, customized configurations, or compliance with stringent security policies, self-hosted agents provide the ultimate control. This guide will walk you through setting up a self-hosted agent in Azure DevOps, enriched with best practices, detailed steps, and management tips.

## Prerequisites

Before diving in, ensure you have the following prerequisites:

1. **Azure DevOps Account**: Create one at [Azure DevOps](https://azure.microsoft.com/en-us/services/devops/) if you haven’t already.
2. **Agent Machine**: A physical or virtual machine running Windows, macOS, or Linux.
3. **Network and Permissions**: Ensure the machine has internet access and administrative permissions to install software.

## Step 1: Create a Personal Access Token (PAT)

To authenticate your self-hosted agent with Azure DevOps, you need a Personal Access Token (PAT).

1. **Navigate to your Azure DevOps organization settings.**
2. **Select "Personal Access Tokens" under the "Security" tab.**
3. **Click on "New Token".**
4. **Set the appropriate scopes** (e.g., Agent Pools (read, manage)) and create the token.
5. **Copy the token** and store it securely.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ku1e52674m879n34okx7.png)

## Step 2: Download the Agent Package

On your agent machine:

1. Navigate to your Azure DevOps project.
2. Go to **Project Settings** > **Agent pools**.
3. Select the desired agent pool or create a new one.
4. Click on **New Agent**.
5. Download the appropriate agent package for your operating system.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lxc0vs8xod8m6tvrtjfp.png)

## Step 3: Configure the Agent

### On Windows:

1. **Extract the downloaded zip file.**
2. **Open Command Prompt** and navigate to the extracted directory.
3. **Run `config.cmd`.**
4. **Provide the server URL** (e.g., `https://dev.azure.com/yourorganization`).
5. **Paste the PAT** when prompted.
6. **Configure the agent** with the default options or customize as needed.
7. **Run the agent** by executing `run.cmd`.

### On Linux:

1. Download the file

   ```bash
   wget https://vstsagentpackage.azureedge.net/agent/3.239.1/vsts-agent-osx-x64-3.239.1.tar.gz
   ```

2. **Extract the downloaded tar.gz file:**

   ```bash
   tar zxvf vsts-agent-linux-x64-*.tar.gz
   ```

3. **Navigate to the extracted directory:**

   ```bash
   cd vsts-agent-linux-x64
   ```

4. **Run the configuration script:**

   ```bash
   ./config.sh
   ```

5. **Provide the server URL and PAT** when prompted.
6. **Configure the agent**, then start it:

   ```bash
   ./svc.sh install
   ./svc.sh start
   ```

### On macOS:

1. **Extract the downloaded tar.gz file:**

   ```bash
   tar zxvf vsts-agent-osx-x64-*.tar.gz

   ```

2. **Navigate to the extracted directory:**

   ```bash
   cd vsts-agent-osx-x64

   ```

3. **Run the configuration script:**

   ```bash
   ./config.sh

   ```

4. **Provide the server URL and PAT** when prompted.
5. **Configure the agent**, then start it:

   ```bash
   ./svc.sh install
   ./svc.sh start

   ```

## Step 4: Verify Agent Configuration

Back in Azure DevOps:

1. **Navigate to "Project Settings" > "Agent Pools".**
2. **Select your pool** and check if the new agent is listed and online.

## Managing the Agent

### Removing the Agent

If you need to remove the agent from your pool:

1. **Stop the Agent**:
   - On Windows: Run `svc.sh stop` or manually stop the service from the Services app.
   - On Linux/macOS: Run `./svc.sh stop`.
2. **Unconfigure the Agent**:
   - Navigate to the agent's directory and run the unconfiguration command:
     - On Windows: `config.cmd remove`
     - On Linux/macOS: `./config.sh remove`
3. **Delete the Agent Directory**:
   - Once unconfigured, you can safely delete the agent's directory to free up space.

### Reconfiguring the Agent

To reconfigure an existing agent:

1. **Navigate to the Agent Directory**:
   - If you haven’t deleted the agent directory, navigate back to it.
2. **Run the Configuration Command**:
   - On Windows: `config.cmd`
   - On Linux/macOS: `./config.sh`
3. **Follow the Configuration Steps**:
   - Provide the server URL and PAT when prompted.
   - Customize the agent settings as needed.
4. **Start the Agent**:
   - On Windows: Run `run.cmd` or start the service from the Services app.
   - On Linux/macOS: Run `./svc.sh start`.

## Best Practices

1. **Security**: Regularly rotate your PATs and ensure they have the least privilege necessary.
2. **Maintenance**: Keep the agent machine updated with the latest security patches and software updates.
3. **Scalability**: For large teams or complex pipelines, consider setting up multiple agents to distribute the workload.
4. **Monitoring**: Utilize Azure Monitor or other monitoring tools to keep an eye on the health and performance of your self-hosted agents.

## Conclusion

Setting up, configuring, and managing a self-hosted agent in Azure DevOps empowers you with greater control and customization of your CI/CD pipelines. It’s a straightforward process that opens up a world of possibilities for optimizing your development workflow. Whether you're integrating specific tools, enhancing security, or boosting performance, a self-hosted agent is a powerful addition to your DevOps toolkit.

Happy DevOps-ing!

---
