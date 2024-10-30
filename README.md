# Azure OpenAI Assistants API: Creating your first 10K Vector Store

**Vector Store** is a new object in Azure OpenAI (AOAI) Assistants API, that makes uploaded files searcheable, by automatically parsing, chunking and embedding their content.

At the time of writing (October 2024), Vector Store was supporting the ingestion of up to **10,000** files.

> [!WARNING]
> Uploading thousands of files may fail because of timeout or other disruptions to API operation. That's why the upload process is enforcing two **maximum file** limits:
> - up to _100_ files max, when creating new Vector Store;
> - up to _500_ files max, when adding files to the existing Vector Store.

## Table of contents:
- [Pre-requisites](https://github.com/LazaUK/AOAI-Assistants-VectorStore#pre-requisites)
- [Scenario 1: Authenticating with API Key]()
- [Scenario 2: Authenticating with Entra ID]()

## Pre-requisites
1. Upgrade openai Python package to its latest supported version:
``` PowerShell
pip install --upgrade openai
```
3. Set the following 4 environment variables before running the notebook:

| Environment Variable | Description |
| --- | --- |
| _AZURE_OPENAI_API_BASE_ | URL of AOAI endpoint |
| _AZURE_OPENAI_API_DEPLOY_ | Name of AOAI deployment |
| _AZURE_OPENAI_API_VERSION_ | API version of AOAI endpoint |
| _AZURE_OPENAI_API_KEY_ | API key of AOAI endpoint |


## Scenario 1: Authenticating with API Key

## Scenario 2: Authenticating with Entra ID
