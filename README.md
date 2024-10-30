# Azure OpenAI Assistants API: Creating your first 10K Vector Store

**Vector Store** is a new object in Assistants API, that makes uploaded files searcheable, by automatically parsing, chunking and embedding their content.

At the time of writing (October 2024), Vector Store was supporting the ingestion of up to **10,000** files.

> [!WARNING]
> Uploading thousands of files may fail because of timeout or other disruptions to API operation. That's why the upload process is enforcing two **maximum file** limits:
> - up to _100_ files max, when creating new Vector Store;
> - up to _500_ files max, when adding files to the existing Vector Store.

## Table of contents:
- [Pre-requisites]()
- [Scenario 1: Authenticating with API Key]()
- [Scenario 2: Authenticating with Entra ID]()

## Pre-requisites
1.

## Scenario 1: Authenticating with API Key

## Scenario 2: Authenticating with Entra ID
