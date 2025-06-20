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

