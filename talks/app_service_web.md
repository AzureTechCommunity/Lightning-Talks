---
title: Host your web apps with Azure App Service
author: Presenter Name
---

## What is App Service❓ What are Web Apps❓

### App Service

:::::::::::::: {.columns}
::: {.column width="50%"}

- HTTP-based service for _hosting web applications_
- Develop in your favorite server-side language including:
  - .NET
  - Java
  - Ruby
  - Node.js
  - Python
  - PHP
- _Scale_ and _run_ applications with little to no friction

:::
::: {.column width="50%"}

![ ][images-app_services]

:::
::::::::::::::

::: notes

App services supports many languages natively and can automatically build the code as part of the deployment process

Scale up and out can happen both manually and automatically making it easier to achieve global scale

Code is ran in a fully-managed production environment with automatic OS and framework patching

:::

### Code-based Web Apps!

:::::::::::::: {.columns}
::: {.column width="50%"}

![ ][images-oryx]

:::
::: {.column width="50%"}

Deploy code to Web Apps

- Deploy code directly from a _deployment source_
  - GitHub
  - Azure Repos
  - OneDrive
- Code is _built automatically_ using the Oryx ([github.com/microsoft/oryx][]) build system
- You can configure _continuous deployment_ and use _deployment slots_

:::
::::::::::::::

::: notes

This was the original way to deploy to App Service Web Apps (using Kudu)

When you deploy code, Oryx will detect the framework using built-in rules, and then perform a build

It's trivial to configure automated deployment processes and deploy to slots other than your production slot

:::

### Container-based Web Apps

:::::::::::::: {.columns}
::: {.column width="50%"}

![ ][images-docker]

:::
::: {.column width="50%"}

Use Docker containers with Web Apps

- Host applications using a _custom container_ from
  - Docker Hub
  - Azure Container Registry
  - GitHub Packages
- Run _multi-container_ applications with _Docker Compose_
- Configure _continuous deployment_ from container registries

:::
::::::::::::::

::: notes

If you already are invested in Docker, this is the far easier path

You can isolate your application and dependencies from the software stack running in the Web App

This is a great way to try out new programming frameworks prior to their typical availability

This is also a great way to lock your application to a specific older framework

:::

## Demo: Deploying an App Service Web App from a container

::: notes

1. Use this link to generate a new GitHub repository using the [github.com/msusdev/example-next-web-app][] template: [github.com/msusdev/example-next-web-app/generate][].
1. Use the [Azure Portal][azure-portal] to [open the "Create Web App" wizard][azure-create-web-app].
1. In the **Basics** tab, perform the following actions:
    1. Select any subscription, region, and resource group.
    1. Give you web app an easily memorized unique name.
    1. In the **Publish** section, select **Docker Container**.
    1. In the **Operating System** section, select **Linux**.
    1. Select a region that you will use for both demos in this presentation.
    1. Leave the **App Service Plan** set to it's default option.
    1. Select **Next: Docker**.
1. In the **Docker** tab, perform the following actions:
    1. In the **Options** list, select **Single Container**.
    1. In the **Image Source** list, select **Docker Hub**.
    1. In the **Access Type** list, select **Public**.
    1. In the **Image and tag** box, enter ``msusdev/webnext:20``
    1. Select **Review + create**.
1. In the **Review + create** tab, select **Create** to deploy the new Web App.
1. Wait for the deployment process to finish, then select **Go to resource**.
1. In the resource blade, select **Browse**.
1. Observe the deployed web application.

:::

## That's cool, how about the new Azure Static Web Apps❓

### Azure Static Web Apps

:::::::::::::: {.columns}
::: {.column width="50%"}

_Build_  and _host_ static web applications

- Uses Oryx (([github.com/microsoft/oryx][])) build engine
- Built-in support for _authentication_ and _authorization_
- _Azure Functions_ ➡️ APIs
- _GitHub Actions_ ➡️ CI/CD

:::
::: {.column width="50%"}

![ ][images-static_web_apps]

:::
::::::::::::::

::: notes

New service focused on the specific needs of JavaScript-based static web applications

Ideal for frameworks like Angular, React, Svelte, Vue, or Blazor

Typically, these frameworks often required a server-side app to serve content

Build process is powered by Oryx

Integrated authentication with flexible roles

API endpoints are serverless and powered by Azure Functions

:::

### Static Web App breakdown

![ ][images-static_web_apps_breakdown]

::: notes

Workflow modeled after common daily workflow for developers

Workflow focused on typical GitHub interactions

Upon creation, Azure Static Web Apps creates a GitHub Actions workflow

YAML file is added to ``.github/workflows`` folder

Application is built and deployed to Azure on commits and pull requests to watched branches

:::

### Github Action

:::::::::::::: {.columns}
::: {.column width="50%"}

_Static Web Apps Deploy_ GitHub Action

- Used by Azure Static Web Apps to automate deployment from GitHub
- You can use directly in any of your own workflows
- Open-source on GitHub ([github.com/azure/static-web-apps-deploy][])

:::
::: {.column width="50%"}

![ ][images-github]

:::
::::::::::::::

### Example Github Actions workflow YAML

```yaml
- uses: "Azure/static-web-apps-deploy@v0.0.1-preview"
  with:
    azure_static_web_apps_api_token: "${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}"
    repo_token: "${{ secrets.GITHUB_TOKEN }}"
    action: "upload"
    app_location: "/"
    api_location: "api"
    app_artifact_location: "out"
```

::: notes

GitHub action is still in preview

Action uses a token that's automatically saved to the repo to connect to Static Web Apps

Action specifies the location of the build artifacts, application root, and API

:::

## Demo: Deploying an Azure Static Web App from code on GitHub

::: notes

1. Use the [Azure Portal][azure-portal] to [open the "Create Static Web App (Preview)" wizard][azure-create-static-web-app].
1. In the **Basics** tab, perform the following actions:
    1. Select any subscription.
    1. Select the same resource group as you used for the previous demo.
    1. Give you static web app an easily memorized unique name.
    1. Select any region.
    1. Sign in to GitHub using the same account that you use to generate your new repository. Authorize permission to access your account and organization\[s\].
    1. Select the **Organization** and **Repository** list options that match where you generated your new repo.
    1. Select the **main** branch.
    1. In the **Build Presets** list, select **Custom**.
    1. In the **App location** box, enter **/**.
    1. In the **Api location** box, enter **api**.
    1. In the **App artifact location** box, enter **out**.
    1. Select **Review + create**.
1. In the **Review + create** tab, select **Create** to deploy the new Web App.
1. Wait for the deployment process to finish, then select **Go to resource**.
1. In the resource blade, select **Browse**.
1. Observe the deployed web application.

:::

## Wrapping up

### Review

App Service

- Web Apps
  - Container-based
  - Code-based (Oryx)

Static Web Apps

- Site content, Function, static content
- GitHub Actions

::: notes

Emphasize the difference between Web Apps and Static Web Apps

Talk about some of the things you saw in the demos

:::

### Links

Deck

- [github.com/azuretechcommunity/talks][]

Links

- [github.com/microsoft/oryx][]
- [github.com/azure/static-web-apps-deploy][]

::: notes

The deck is open-source and attendees are welcome to view the deck to get images, links, and other content they may have missed

:::

[azure-portal]: https://portal.azure.com/
[azure-create-web-app]: https://portal.azure.com/#create/microsoft.webSite
[azure-create-static-web-app]: https://portal.azure.com/#create/microsoft.staticapp
[images-app_services]: media/app_services.png
[images-docker]: media/docker.png
[images-github]: media/github.png
[images-oryx]: media/oryx.png
[images-static_web_apps]: media/static_web_apps.png
[images-static_web_apps_breakdown]: media/static_web_apps_breakdown.png
[github.com/azuretechcommunity/talks]: https://github.com/azuretechcommunity/talks
[github.com/azure/static-web-apps-deploy]: https://github.com/azure/static-web-apps-deploy
[github.com/microsoft/oryx]: https://github.com/microsoft/oryx
[github.com/msusdev/example-next-web-app]: https://github.com/msusdev/example-next-web-app
[github.com/msusdev/example-next-web-app/generate]: https://github.com/msusdev/example-next-web-app/generate
