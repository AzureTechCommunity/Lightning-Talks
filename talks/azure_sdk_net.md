---
title: The New Azure SDK for .NET
author: Presenter Name
---

## What is Going On❓

### Current State of Play

:::::::::::::: {.columns}
::: {.column width="50%"}

Originally, each Azure team built their own .NET SDKs resulting in:

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

Each Azure team built their SDKs at different points in their product's maturity

Language, operating system, and package manager support can vary wildly between SDKs

It's also very difficult to discover new APIs as each API uses a different paradigm, naming scheme, GitHub repo structure, and even location on GitHub

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

- [azure/azure-sdk][github.com/azure/azure-sdk]
  - Documentation on guidelines and policies
- **[azure/azure-sdk-for-net][github.com/azure/azure-sdk-for-net]**
  - **SDK for .NET**
- [azure/azure-sdk-for-js][github.com/azure/azure-sdk-for-js]
  - SDK for JavaScript
- [azure/azure-sdk-for-python][github.com/azure/azure-sdk-for-python]
  - SDK for Python
- [azure/azure-sdk-for-java][github.com/azure/azure-sdk-for-java]
  - SDK for Java

:::
::: {.column width="50%"}

![ ][images-github]

:::
::::::::::::::

::: notes

The [github.com/azure/azure-sdk][] repository contains releases, documentation, and guidelines for all of the other repositories

The **.NET**, JavaScript, Python, and Java repositories contain source code, samples, and documentation relevant to that language

Each language repository contains SDK source code to access multiple Azure services in a predictable and consistent manner

:::

### Even More Azure SDKs on GitHub

:::::::::::::: {.columns}
::: {.column width="50%"}

- [github.com/azure/azure-sdk-for-ios][github.com/azure/azure-sdk-for-ios]
  - Client SDK for iOS Apps
- [github.com/azure/azure-sdk-for-android][github.com/azure/azure-sdk-for-android]
  - Client SDK for Android Apps
- [github.com/azure/azure-sdk-for-go][github.com/azure/azure-sdk-for-go]
  - SDK for Go
- [github.com/azure/azure-sdk-for-cpp][github.com/azure/azure-sdk-for-cpp]
  - SDK for C++
- [github.com/azure/azure-sdk-for-c][github.com/azure/azure-sdk-for-c]
  - SDK for Embedded C

:::
::: {.column width="50%"}

![ ][images-github]

:::
::::::::::::::

::: notes

The underlying guidelines and processes made it easier to add new languages

Each language supports a growing amount of Azure services

:::

## Demo: Exploring the Azure SDK for .NET Repository

::: notes

1. Use this link to visit the Azure SDK for .NET GitHub repository: [github.com/azure/azure-sdk-for-net][].
1. Review the contents of the **readme.md** file.
1. Navigate to the **samples** folder of the source code: [github.com/azure/azure-sdk-for-net/~/samples][]
1. Navigate to the **API documentation** page for the Azure SDK for .NET: [github.io/azure/azure-sdk-for-net][].
1. Navigate to the **latest releases** page for the Azure SDK: [github.io/azure/azure-sdk/~/#net][]
1. Walk through the various Azure services that currently have a **preview** or **generally available** client library.
1. Navigate to the **Gitter community** for the Azure SDK for .NET: [gitter.im/azure/azure-sdk-for-net][].

:::

## Why Build a New SDK❓

### Design Paradigms

**Developer productivity** is the core objective. The overall guidelines and each individual SDK is built around these paradigms:

- **Idiomatic**
  - Each SDK feels **natural and conventional** to the target language
- **Consistent**
  - SDKs are **consistent** across various languages and Azure services
- **Approachable**
  - SDKs are **well documented** with the goal of getting developers started quickly
- **Diagnosable**
  - SDKs feature **logging** and **discoverability** as core-level features
- **Dependable**
  - SDKs are **stable** with a focus on compatibility for seamless upgrades

::: notes

Building SDKs that model these paradigms can help increase developer productivity across all of Azure.

The paradigms are a core part of the underlying guidelines that are used to design each individual SDK.

Many existing SDKs required some rework to implement all five paradigms.

:::

### Old .NET SDK Example

```csharp
using Microsoft.Azure.Storage;
using Microsoft.Azure.Storage.Blob;

string connectionString = "UseDevelopmentStorage=true";

CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudBlobClient client = account.CreateCloudBlobClient();
```

::: notes

**NuGet Package**: [Microsoft.Azure.Storage.Blob][nuget.org/microsoft.azure.storage.blob]

:::

### Old .NET SDK Example (cont.)

```csharp
CloudBlobContainer container = client.GetContainerReference("files");

container.CreateIfNotExists();
```

::: notes

To get a client, you need to create **CloudStorageAccount** and **CloudBlobClient** instances

API calls inconsistently support synchronous and asynchronous operations

:::

### New .NET SDK Example

```csharp
using Azure.Storage.Blobs;

string connectionString = "UseDevelopmentStorage=true";

BlobServiceClient client = new BlobServiceClient(connectionString);
```

::: notes

**NuGet Package**: [Azure.Storage.Blobs][nuget.org/azure.storage.blobs]

:::

### New .NET SDK Example (cont.)

```csharp
BlobContainerClient container = client.GetBlobContainerClient("files");

await container.CreateIfNotExistsAsync();
```

::: notes

The new SDK supports both synchronous and asynchronous API calls consistently

The SDK also renames the classes to be consistent across languages while respecting each individual languages' idiomatic standards

:::

## Demo: Using the Azure SDK for .NET to Create a Container

::: notes

> **Prerequisites**: *Ensure you have **.NET 5** or higher installed.*

1. Open a new instance of **Visual Studio Code** in an empty folder.
1. If you have not already, install the [Azure Storage][visualstudio.com/ms-azuretools.vscode-azurestorage] extension for Visual Studio Code.
1. If you have not already, install the [Azurite][visualstudio.com/azurite.azurite] extension for Visual Studio Code.
1. Open a new **terminal** and perform the following actions:
    1. Install the [Preview.CSharp.Templates][nuget.org/preview.csharp.templates] project template package from NuGet:

        ```sh
        dotnet new --install Preview.CSharp.Templates
        ```

    1. Initialize an empty **[top-level program][docs.com/dotnet/csharp/tutorials/exploration/top-level-statements]** using the **dotnet** CLI:

        ```sh
        dotnet new script-empty
        ```

    1. Install the **[Azure.Storage.Blobs][nuget.org/azure.storage.blobs]** package from NPM:

        ```sh
        dotnet add package Azure.Storage.Blobs
        ```

1. Open the **Program.cs** file in the editor.
1. Create a using directive for the **Azure.Storage.Blobs** namespace:

    ```js
    using Azure.Storage.Blobs;
    ```

1. Create a variable named **connectionString** of type **string** with a value of **"UseDevelopmentStorage=true"**:

    ```js
    string connectionString = "UseDevelopmentStorage=true";
    ```

1. Create a variable named **client** of type **BlobServiceClient** that stores the result of invoking the constructor of the **BlobServiceClient** class passing in the **connectionString** variable as a parameter:

    ```js
    BlobServiceClient client = new BlobServiceClient(connectionString);
    ```

1. Create a variable named **container** of type **BlobContainerClient** that stores the result of invoking the **GetBlobContainerClient** method of the **client** variable passing in the value **"files"** as a parameter:

    ```js
    BlobContainerClient container = client.GetBlobContainerClient("files");
    ```

1. Asynchronously invoke the **CreateIfNotExistsAsync** method of the **container** variable:

    ```js
    await container.CreateIfNotExistsAsync();
    ```

1. **Save** your changes to the **Program.cs** file.

1. **Start** the Azurite emulator using either the option on the **status bar** or the ``Azurite: Start`` command in the **Command Palette**.

1. In the **Activity Bar**, navigate to the **Azure** option.

1. In the document tree within the **Azure** pane, expand the following nodes: **Storage** => **Attached Storage** => **Local Emulator** => **Blob Containers**.

1. Open a new **terminal** and run the .NET application:

    ```sh
    dotnet run
    ```

1. Back in the **Azure** pane, open the context menu for the **Blob Containers** node and then select **Refresh**.

1. Observe the newly created **files** container in the document tree.

:::

[images-github]: media/github.png
[images-sdk_current_state]: media/sdk_current_state.png
[images-sdk_new_state]: media/sdk_new_state.png
[docs.com/dotnet/csharp/tutorials/exploration/top-level-statements]: https://docs.microsoft.com/en-us/dotnet/csharp/tutorials/exploration/top-level-statements
[github.com/azure/azure-sdk]: https://github.com/azure/azure-sdk
[github.com/azure/azure-sdk-for-android]: https://github.com/azure/azure-sdk-for-android
[github.com/azure/azure-sdk-for-c]: https://github.com/azure/azure-sdk-for-c
[github.com/azure/azure-sdk-for-cpp]: https://github.com/azure/azure-sdk-for-cpp
[github.com/azure/azure-sdk-for-go]: https://github.com/azure/azure-sdk-for-go
[github.com/azure/azure-sdk-for-ios]: https://github.com/azure/azure-sdk-for-ios
[github.com/azure/azure-sdk-for-java]: https://github.com/azure/azure-sdk-for-java
[github.com/azure/azure-sdk-for-js]: https://github.com/azure/azure-sdk-for-js
[github.com/azure/azure-sdk-for-net]: https://github.com/azure/azure-sdk-for-net
[github.com/azure/azure-sdk-for-net/~/samples]: https://github.com/Azure/azure-sdk-for-net/tree/master/samples
[github.com/azure/azure-sdk-for-python]: https://github.com/azure/azure-sdk-for-python
[github.io/azure/azure-sdk/~/#net]: https://azure.github.io/azure-sdk/#net
[github.io/azure/azure-sdk-for-net]: https://azure.github.io/azure-sdk-for-net/
[gitter.im/azure/azure-sdk-for-net]: https://gitter.im/Azure/azure-sdk-for-net
[nuget.org/microsoft.azure.storage.blob]: https://www.nuget.org/packages/Microsoft.Azure.Storage.Blob/
[nuget.org/azure.storage.blobs]: https://www.nuget.org/packages/Azure.Storage.Blobs/
[nuget.org/preview.csharp.templates]: https://www.nuget.org/packages/Preview.CSharp.Templates/
