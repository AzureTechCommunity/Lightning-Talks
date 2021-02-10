---
title: The New Azure SDK for JavaScript
author: Presenter Name
---

## What is Going On❓

### Current State of Play

:::::::::::::: {.columns}
::: {.column width="50%"}

Originally, each Azure team built their own JavaScript SDKs resulting in:

- Many GitHub Repos Across Different Organizations
- Incosistent Operating System Support
- Unique Continuous Integration Processes and Platforms
- Varying Levels of Language/Framework Support
- Inconsistent Package Manager\[s\] Used
- Undiscoverable API Paradigms

:::
::: {.column width="50%"}

![ ][images-sdk_current_state]

:::
::::::::::::::

::: notes

Each Azure team built their SDKs at different points in their product's maturity.

Language, operating system, and package manager support can vary wildly between SDKs.

It's also very difficult to discover new APIs as each API uses a different paradigm, naming scheme, GitHub repo structure, and even location on GitHub.

:::

### The New Azure SDK

:::::::::::::: {.columns}
::: {.column width="50%"}

![ ][images-sdk_new_state]

:::
::: {.column width="50%"}

The new Azure SDK introduces common guidelines that is designed to provide:

- Equitable Operating System Support
- Predictable Language Support
- Consistent Authentication Support
- Universal Continuous Integration Process
- Packages Available in Popular Package Managers

:::
::::::::::::::

::: notes

This is the first step towards applying a common set of standards to all Azure SDKs

Having a common model, makes it easier for new Azure teams to create a discoverable and predictable SDK

Having a core framework in place makes it easier to add support for new languages, operating systems, and package managers in the future

:::

### The Azure SDKs on GitHub

:::::::::::::: {.columns}
::: {.column width="50%"}

| Repository | Description |
| --- | --- |
| [azure/azure-sdk][github.com/azure/azure-sdk] | Documentation on guidelines and policies |
| **[azure/azure-sdk-for-js][github.com/azure/azure-sdk-for-js]** | **SDK for JavaScript** |
| [azure/azure-sdk-for-net][github.com/azure/azure-sdk-for-net] | SDK for .NET |
| [azure/azure-sdk-for-python][github.com/azure/azure-sdk-for-python] | SDK for Python |
| [azure/azure-sdk-for-java][github.com/azure/azure-sdk-for-java] | SDK for Java |

:::
::: {.column width="50%"}

![ ][images-github]

:::
::::::::::::::

::: notes

The [github.com/azure/azure-sdk][] repository contains releases, documentation, and guidelines for all of the other repositories

The .NET, **JavaScript**, Python, and Java repositories contain source code, samples, and documentation relevant to that language

Each language repository contains SDK source code to access multiple Azure services in a predictable and consistent manner

:::

### Even More Azure SDKs on GitHub

:::::::::::::: {.columns}
::: {.column width="50%"}

| Repository | Description |
| --- | --- |
| [github.com/azure/azure-sdk-for-ios][github.com/azure/azure-sdk-for-ios] | Client SDK for iOS Apps |
| [github.com/azure/azure-sdk-for-android][github.com/azure/azure-sdk-for-android] | Client SDK for Android Apps |
| [github.com/azure/azure-sdk-for-go][github.com/azure/azure-sdk-for-go] | SDK for Go |
| [github.com/azure/azure-sdk-for-cpp][github.com/azure/azure-sdk-for-cpp] | SDK for C++ |
| [github.com/azure/azure-sdk-for-c][github.com/azure/azure-sdk-for-c] | SDK for Embedded C |

:::
::: {.column width="50%"}

![ ][images-github]

:::
::::::::::::::

::: notes

The underlying guidelines and processes made it easier to add new languages

Each language supports a growing amount of Azure services

:::

## Demo: Exploring the Azure SDK for JavaScript Repository

::: notes

1. Use this link to visit the Azure SDK for JavaScript GitHub repository: [github.com/azure/azure-sdk-for-js][].
1. Review the contents of the **readme.md** file.
1. Navigate to the **samples** folder of the source code: [github.com/azure/azure-sdk-for-js/~/samples][]
1. Navigate to the **API documentation** page for the Azure SDK for JavaScript: [github.io/azure/azure-sdk-for-js][].
1. Navigate to the **latest releases** page for the Azure SDK: [github.io/azure/azure-sdk/~/#javascript][]
1. Walk through the various Azure services that currently have a **preview** or **generally available** client library.
1. Navigate to the **Gitter community** for the Azure SDK for JavaScript: [gitter.im/azure/azure-sdk-for-js][].

:::

## Why Build a New SDK❓

### Design Paradigms

**Developer productivity** is the core objective. The overall guidelines and each individual SDK is built around these paradigms:

| | |
| --- | --- |
| Idiomatic | Each SDK feels **natural and conventional** to the target language |
| Consistent | SDKs are **consistent** across various languages and Azure services |
| Approachable | SDKs are **well documented** with the goal of getting developers started quickly |
| Diagnosable | SDKs feature **logging** and **discoverability** as core-level features |
| Dependable | SDKs are **stable** with a focus on compatibility for seamless upgrades |

::: notes

Building SDKs that model these paradigms can help increase developer productivity across all of Azure.

The paradigms are a core part of the underlying guidelines that are used to design each individual SDK.

Many existing SDKs required some rework to implement all five paradigms.

:::

### Old JavaScript SDK Example

> **NPM Package**: [azure-storage][npmjs.com/azure-storage]

```js
var azure = require('azure-storage');

const connectionString = "UseDevelopmentStorage=true";

var client = azure.createBlobService(connectionString);

client.createContainerIfNotExists("files", {}, (error, result) => {
  
  // next steps

});
```

::: notes

To get a client, you need to use the **azure** constant and the **createBlobService** method

Documentation and quickstarts aren't very consistent, so it can be difficult to discover all the different ways you can create a client

API calls inconsistently support synchronous and asynchronous operations

:::

### New JavaScript SDK Example

> **NPM Package**: [@azure/storage-blob][npmjs.com/@azure/storage-blob]

```js
const { BlobServiceClient } = require("@azure/storage-blob");

async function run() {

  const connectionString = "UseDevelopmentStorage=true";
  
  const client = BlobServiceClient.fromConnectionString(connectionString);
  
  const container = client.getContainerClient("files");

  await container.createIfNotExists();

  // next steps

}

run();
```

::: notes

The new SDK supports both synchronous and asynchronous API calls consistently

The new SDK uses the **promises** API for JavaScript

The SDK also renames the classes to be consistent across languages while respecting each individual languages' idiomatic standards

:::

## Demo: Using the Azure SDK for JavaScript to Create a Container

::: notes

> **Prerequisites**: *Ensure you have Node.js version **8.0.0** or higher installed.*

1. Open a new instance of **Visual Studio Code** in an empty folder.
1. If you have not already, install the [Azure Storage][visualstudio.com/ms-azuretools.vscode-azurestorage] extension for Visual Studio Code.
1. If you have not already, install the [Azurite][visualstudio.com/azurite.azurite] extension for Visual Studio Code.
1. Open a new **terminal** and perform the following actions:
    1. Initialize a new **package.json** file:

        ```sh
        npm init --force
        ```

    1. Install the **[@azure/storage-blob][npmjs.com/@azure/storage-blob]** package from NPM:

        ```sh
        npm install @azure/storage-blob --save
        ```

1. Create a new file named **index.js** and open it in the editor.
1. Import the **BlobServiceClient** type:

    ```js
    const { BlobServiceClient } = require("@azure/storage-blob");
    ```

1. Create and invoke a new asynchronous function named **run**:

    ```js
    async function run() {

    }

    run();
    ```

1. Within the **run** function, create a constant named **connectionString** with a value of **"UseDevelopmentStorage=true"**:

    ```js
    const connectionString = "UseDevelopmentStorage=true";
    ```

1. Still within the **run** function, create a constant named **client** that stores the result of invoking the **fromConnectionString** method of the **BlobServiceClient** constant passing in the **connectionString** constant as a constructor parameter:

    ```js
    const client = BlobServiceClient.fromConnectionString(connectionString);
    ```

1. Still within the **run** function, create a constant named **container** that stores the result of invoking the **getContainerClient** method of the **client** constant passing in the value **"files"** constant as a parameter:

    ```js
    const container = client.getContainerClient("files");
    ```

1. Still within the **run** function, invoke the **createIfNotExists** method of the **container** constant:

    ```js
    await container.createIfNotExists();
    ```

1. **Save** your changes to the **index.js** file.

1. **Start** the Azurite emulator using either the option on the **status bar** or the ``Azurite: Start`` command in the **Command Palette**.

1. In the **Activity Bar**, navigate to the **Azure** option.

1. In the document tree within the **Azure** pane, expand the following nodes: **Storage** => **Attached Storage** => **Local Emulator** => **Blob Containers**.

1. Open a new **terminal** and run the Node.js application:

    ```sh
    node index.js
    ```

1. Back in the **Azure** pane, open the context menu for the **Blob Containers** node and then select **Refresh**.

1. Observe the newly created **files** container in the document tree.

:::

[images-github]: media/github.png
[images-sdk_current_state]: media/sdk_current_state.png
[images-sdk_new_state]: media/sdk_new_state.png
[github.com/azure/azure-sdk]: https://github.com/azure/azure-sdk
[github.com/azure/azure-sdk-for-android]: https://github.com/azure/azure-sdk-for-android
[github.com/azure/azure-sdk-for-c]: https://github.com/azure/azure-sdk-for-c
[github.com/azure/azure-sdk-for-cpp]: https://github.com/azure/azure-sdk-for-cpp
[github.com/azure/azure-sdk-for-go]: https://github.com/azure/azure-sdk-for-go
[github.com/azure/azure-sdk-for-ios]: https://github.com/azure/azure-sdk-for-ios
[github.com/azure/azure-sdk-for-java]: https://github.com/azure/azure-sdk-for-java
[github.com/azure/azure-sdk-for-js]: https://github.com/azure/azure-sdk-for-js
[github.com/azure/azure-sdk-for-js/~/samples]: https://github.com/Azure/azure-sdk-for-js/tree/master/samples
[github.com/azure/azure-sdk-for-net]: https://github.com/azure/azure-sdk-for-net
[github.com/azure/azure-sdk-for-python]: https://github.com/azure/azure-sdk-for-python
[github.io/azure/azure-sdk/~/#javascript]: https://azure.github.io/azure-sdk/#javascript
[github.io/azure/azure-sdk-for-js]: https://azure.github.io/azure-sdk-for-js/
[gitter.im/azure/azure-sdk-for-js]: https://gitter.im/Azure/azure-sdk-for-js
[npmjs.com/@azure/storage-blob]: https://www.npmjs.com/package/@azure/storage-blob
[npmjs.com/azure-storage]: https://www.npmjs.com/package/azure-storage
[visualstudio.com/azurite.azurite]: https://marketplace.visualstudio.com/items?itemName=Azurite.azurite
[visualstudio.com/ms-azuretools.vscode-azurestorage]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage
