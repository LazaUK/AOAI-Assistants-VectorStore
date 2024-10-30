# Azure OpenAI Assistants API: Creating your first 10K Vector Store

**Vector Store** is a new object in Azure OpenAI (AOAI) Assistants API, that makes uploaded files searcheable, by automatically parsing, chunking and embedding their content.

At the time of writing (October 2024), Vector Store was supporting the ingestion of up to **10,000** files.

> [!WARNING]
> Uploading thousands of files may fail because of timeout or other disruptions to API operation. That's why the upload process is enforcing two **maximum file** limits:
> - up to _100_ files max, when creating new Vector Store;
> - up to _500_ files max, when adding files to the existing Vector Store.

## Table of contents:
- [Pre-requisites](https://github.com/LazaUK/AOAI-Assistants-VectorStore#pre-requisites)
- [Scenario 1: Authenticating with API Key](https://github.com/LazaUK/AOAI-Assistants-VectorStore#scenario-1-authenticating-with-api-key)
- [Scenario 2: Authenticating with Entra ID](https://github.com/LazaUK/AOAI-Assistants-VectorStore#scenario-2-authenticating-with-entra-id)

## Pre-requisites
1. Upgrade openai Python package to its latest supported version:
``` PowerShell
pip install --upgrade openai
```
2. Set the following 3 environment variables before running the notebook:

| Environment Variable | Description |
| --- | --- |
| _AZURE_OPENAI_API_BASE_ | URL of AOAI endpoint |
| _AZURE_OPENAI_API_VERSION_ | API version of AOAI endpoint |
| _AZURE_OPENAI_API_KEY_ | API key of AOAI endpoint (_required for Scenario 1 only_) |

## Scenario 1: Authenticating with API Key
1. Retrieve values of environment variables:
``` Python
AOAI_API_BASE = os.getenv("AZURE_OPENAI_API_BASE")
AOAI_API_VERSION = os.getenv("AZURE_OPENAI_API_VERSION")
AOAI_API_KEY = os.getenv("AZURE_OPENAI_API_KEY")
```
2. Instantiate Azure OpenAI client:
``` Python
client = AzureOpenAI(
    azure_endpoint = AOAI_API_BASE,
    api_version = AOAI_API_VERSION,
    api_key = AOAI_API_KEY
)
```
3. Instantiate new Vector Store:
``` Python
vector_store = client.beta.vector_stores.create(
    name = "<VECTOR_STORE_NAME>"
)
```
4. Populate the Vector Store with your files in bacthes:
``` Python
file_batch = client.beta.vector_stores.file_batches.upload_and_poll(
    vector_store_id = vector_store.id,
    files = file_streams
)
```
5. If successful, you should see something like this:
``` JSON
Uploading files to the vector store from folder1...
Files upload status: completed
- cancelled: 0
- completed: 100
- failed: 0
- in progress: 0
----------------------------------------
Total: 100

Uploading files to the vector store from folder2...
Files upload status: completed
- cancelled: 0
- completed: 500
- failed: 0
- in progress: 0
----------------------------------------
Total: 500
```

## Scenario 2: Authenticating with Entra ID
1. Retrieve values of environment variables:
``` Python
AOAI_API_BASE = os.getenv("AZURE_OPENAI_API_BASE")
AOAI_API_VERSION = os.getenv("AZURE_OPENAI_API_VERSION")
```
2. Define Entra ID as a token provider:
``` Python
token_provider = get_bearer_token_provider(
    DefaultAzureCredential(),
    "https://cognitiveservices.azure.com/.default"
)
```
3. Instantiate Azure OpenAI client:
``` Python
client = AzureOpenAI(
    azure_endpoint = AOAI_API_BASE,
    api_version = AOAI_API_VERSION,
    api_key = AOAI_API_KEY
)
```
4. Instantiate new Vector Store:
``` Python
vector_store = client.beta.vector_stores.create(
    name = "<VECTOR_STORE_NAME>"
)
```
5. Populate the Vector Store with your files in bacthes:
``` Python
file_batch = client.beta.vector_stores.file_batches.upload_and_poll(
    vector_store_id = vector_store.id,
    files = file_streams
)
```
6. If successful, you should see something like this:
``` JSON
Uploading files to the vector store from folder1...
Files upload status: completed
- cancelled: 0
- completed: 100
- failed: 0
- in progress: 0
----------------------------------------
Total: 100

Uploading files to the vector store from folder2...
Files upload status: completed
- cancelled: 0
- completed: 500
- failed: 0
- in progress: 0
----------------------------------------
Total: 500
```
