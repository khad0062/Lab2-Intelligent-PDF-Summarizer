# Lab 2: Build an Intelligent PDF Summarizer using Azure Durable Functions
## Azure Durable Functions
Azure Durable Functions is an extension of Azure Functions that lets you write stateful workflows in a serverless environment. In short, they make it easy to orchestrate long-running, stateful, 
and reliable workflows using code—without worrying about the underlying infrastructure.

Core Concepts
Durable Functions = Serverless + Orchestration + State

Serverless: You only pay for what you use, and Microsoft manages the servers.

Orchestration: You can coordinate the execution of other functions, including sequential, parallel, or even human-interaction steps.

Stateful: Durable Functions keep track of the workflow's progress and state, so you don’t have to manage this yourself.

The application's workflow is as follows:
1. Trigger:
Listens for new blobs (PDFs) in the input container.

2. Durable Orchestration:

- - Step 1: Analyze the PDF with Document Intelligence (OCR/structure extraction).

- - Step 2: Summarize the extracted text using Azure OpenAI.

## Prerequsites
- [Install the latest Azure Functions Core Tools to use the CLI](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local)
- Python 3.9 or greater
- Access permissions to [create Azure OpenAI resources and to deploy models](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/role-based-access-control).
- [Start and configure an Azurite storage emulator for local storage](https://learn.microsoft.com/azure/storage/common/storage-use-azurite).
- Search for the Document intelligence and create Document Intelligence under AI Foundry.

## local.settings.json
You will need to configure a `local.settings.json` file at the root of the repo that looks similar to the below. Make sure to replace the placeholders with your specific values.

```json
{
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "AzureWebJobsFeatureFlags": "EnableWorkerIndexing",
    "FUNCTIONS_WORKER_RUNTIME": "python",
    "BLOB_STORAGE_ENDPOINT": "<BLOB-STORAGE-ENDPOINT>",
    "COGNITIVE_SERVICES_ENDPOINT": "<COGNITIVE-SERVICE-ENDPOINT>",
    "AZURE_OPENAI_ENDPOINT": "AZURE-OPEN-AI-ENDPOINT>",
    "AZURE_OPENAI_KEY": "<AZURE-OPEN-AI-KEY>",
    "CHAT_MODEL_DEPLOYMENT_NAME": "<AZURE-OPEN-AI-MODEL>"
  }
}
```

## Running the app locally
1. Start Azurite: Begin by starting Azurite, the local Azure Storage emulator.

2. Install the Requirements: Open your terminal and run the following command to install the necessary packages:

```bash
python3 -m pip install -r requirements.txt
```
3. Create two containers in your storage account. One called `input` and the other called `output`. 

4. Start the Function App: Start the function app to run the application locally.

```bash
func start --verbose
```

5. Upload PDFs to the `input` container. That will execute the blob storage trigger in your Durable Function.

6. After several seconds, your appliation should have finished the orchestrations. Switch to the `output` container and notice that the PDFs have been summarized as new files. 

  


