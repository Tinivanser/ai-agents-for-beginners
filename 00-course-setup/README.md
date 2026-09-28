# Course Setup

## Introduction

This lesson will cover how to run the code samples of this course.

## Clone or Fork this Repo

To begin, clone the repository to run and edit the notebooks locally. Forking is optional if you want to keep your changes on GitHub.

This can be done by clicking the link to <a href="https://github.com/microsoft/ai-agents-for-beginners/fork" target="_blank">fork the repo</a>

If you fork the repository, you will see your copy on GitHub:

![Forked Repo](./images/forked-repo.png)

## Running the Code

This course offers a series of Jupyter Notebooks that you can run with to get hands-on experience building AI Agents.

The code samples use either:

**Requires GitHub Account - Free**:

1) Semantic Kernel Agent Framework + GitHub Models Marketplace: [Lesson 1 notebook](../01-intro-to-ai-agents/code_samples/01-semantic-kernel.ipynb)
2) AutoGen Framework + GitHub Models Marketplace: [Lesson 2 notebook](../02-explore-agentic-frameworks/code_samples/02-autogen.ipynb)

**Requires Azure Subscription**:
3) Azure AI Foundry + Azure AI Agent Service: [Lesson 2 notebook](../02-explore-agentic-frameworks/code_samples/02-azureaiagent.ipynb)

We encourage you to try out all three types of examples to see which one works best for you.

Whichever option you choose, it will determine which setup steps you need to follow below:

## Requirements

- Python 3.12+
  - **NOTE**: If you don't have Python3.12 installed, ensure you install it.  Then create your venv using python3.12 to ensure the correct versions are installed from the requirements.txt file.
- A GitHub account for GitHub Models samples **or** an Azure subscription and AI Foundry project for Azure AI Agent Service samples

We have included a `requirements.txt` file in the root of this repository that contains all the required Python packages to run the code samples.

From the repository root, create a virtual environment and install the packages:

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```
On Windows Command Prompt, activate with `.venv\Scripts\activate.bat` instead. Keep the repository root as the working directory so the notebooks can load the root `.env` file.

## Set Up VS Code

Select the `.venv` interpreter as your notebook kernel in VS Code before running cells in the notebook linked above.

## Set Up for Samples using GitHub Models 

### Step 1: Retrieve Your GitHub Personal Access Token (PAT)

Currently, this course uses the GitHub Models Marketplace to offer free access to Large Language Models (LLMs) that will be used to create AI Agents.

To access this service, you will need to create a GitHub Personal Access Token.

This can be done by going to your <a href="https://github.com/settings/personal-access-tokens" target="_blank">Personal Access Tokens settings</a> in your GitHub Account.

Select the `Fine-grained tokens` option on the left side of your screen.

Then select `Generate new token`.

![Generate Token](./images/generate-token.png)

You will be prompted to enter a name for your token, select the expiration date (Recommended: 30 Days), and select the scopes for your token (Public Repositories).

It's also necessary to edit the permissions of this token: Permissions -> Models -> Allows access to GitHub Models

Copy your new token; you will add it to the `.env` file created in the next step.


### Step 2: Create Your `.env` File

To create your `.env` file run the following command in your terminal.

```bash
cp .env.example .env
```

This will copy the example file and create a `.env` in your directory and where you fill in the values for the environment variables.

With your token copied, open the `.env` file in your favorite text editor and paste your token into the `GITHUB_TOKEN` field.

You can now run the GitHub Models notebooks linked above. Other notebooks may require additional services and variables described in their opening cells.

## Set Up for Samples using Azure AI Foundry and Azure AI Agent Service

### Step 1: Retrieve Your Azure Project Endpoint


Follow the steps to creating a hub and project in Azure AI Foundry found here: [Hub resources overview](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/ai-resources)


Once you have created your project, you will need to retrieve its project endpoint.

This can be done by going to the **Overview** page of your project in the Azure AI Foundry portal.

![Project Connection String](./images/project-endpoint.png)

### Step 2: Create Your `.env` File

To create your `.env` file run the following command in your terminal.

```bash
cp .env.example .env
```

This will copy the example file and create a `.env` in your directory and where you fill in the values for the environment variables.

Copy the project endpoint, then open the `.env` file in your favorite text editor and paste it into the `PROJECT_ENDPOINT` field.

### Step 3: Sign in to Azure

As a security best practice, we'll use [keyless authentication](https://learn.microsoft.com/azure/developer/ai/keyless-connections?tabs=csharp%2Cazure-cli?WT.mc_id=academic-105485-koreyst) to authenticate to Azure OpenAI with Microsoft Entra ID. Before you can do so, you'll first need to install the **Azure CLI** per the [installation instructions](https://learn.microsoft.com/cli/azure/install-azure-cli?WT.mc_id=academic-105485-koreyst) for your operating system.

Next, open a terminal and run `az login --use-device-code` to sign in to your Azure account.

Once you've logged in, select your subscription in the terminal.


## Additional Environment Variables - Azure Search and Azure OpenAI 

For the Agentic RAG Lesson - Lesson 5 - there are samples that use Azure Search and Azure OpenAI.

If you want to run these samples, you will need to add the following environment variables to your `.env` file:

### Overview Page (Project)

- `AZURE_SUBSCRIPTION_ID` - Check **Project details** on the **Overview** page of your project.

- `AZURE_AI_PROJECT_NAME` - Look at the top of the **Overview** page for your project.

- `AZURE_OPENAI_SERVICE` - Find this in the **Included capabilities** tab for **Azure OpenAI Service** on the **Overview** page.

### Management Center

- `AZURE_OPENAI_RESOURCE_GROUP` - Go to **Project properties** on the **Overview** page of the **Management Center**.

- `GLOBAL_LLM_SERVICE` - Under **Connected resources**, find the **Azure AI Services** connection name. If not listed, check the **Azure portal** under your resource group for the AI Services resource name.

### Models + Endpoints Page

- `AZURE_OPENAI_EMBEDDING_DEPLOYMENT_NAME` - Select your embedding model (e.g., `text-embedding-ada-002`) and note the **Deployment name** from the model details.

- `AZURE_OPENAI_CHAT_DEPLOYMENT_NAME` and `AZURE_OPENAI_DEPLOYMENT_NAME` - Select your chat model (e.g., `gpt-4o-mini`) and use its **Deployment name** for both variables.

### Azure Portal

- `AZURE_OPENAI_ENDPOINT` - Look for **Azure AI services**, click on it, then go to **Resource Management**, **Keys and Endpoint**, scroll down to the "Azure OpenAI endpoints", and copy the one that says "Language APIs".

- `AZURE_OPENAI_API_KEY` - From the same screen, copy KEY 1 or KEY 2.

- `AZURE_SEARCH_SERVICE_ENDPOINT` - Find your **Azure AI Search** resource, click it, and see **Overview**.

- `AZURE_SEARCH_API_KEY` - Then go to **Settings** and then **Keys** to copy the primary or secondary admin key.

### External Webpage

- `AZURE_OPENAI_API_VERSION` - Visit the [API version lifecycle](https://learn.microsoft.com/en-us/azure/ai-services/openai/api-version-deprecation#latest-ga-api-release) page under **Latest GA API release**.

### Setup keyless authentication

Rather than hardcode your credentials, we'll use a keyless connection with Azure OpenAI. To do so, we'll import `DefaultAzureCredential` and later call the `DefaultAzureCredential` function to get the credential.

```python
from azure.identity import DefaultAzureCredential, InteractiveBrowserCredential
```

## Stuck Somewhere?

If you have any issues running this setup, hop into our <a href="https://discord.gg/kzRShWzttr" target="_blank">Azure AI Community Discord</a> or <a href="https://github.com/microsoft/ai-agents-for-beginners/issues?WT.mc_id=academic-105485-koreyst" target="_blank">create an issue</a>.

## Next Lesson

You are now ready to run the code for this course. Happy learning more about the world of AI Agents! 

[Introduction to AI Agents and Agent Use Cases](../01-intro-to-ai-agents/README.md)
