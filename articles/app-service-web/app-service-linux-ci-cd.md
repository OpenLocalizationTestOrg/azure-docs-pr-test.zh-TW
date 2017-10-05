---
title: "在 Linux 上使用 Azure Web 應用程式連續部署 | Microsoft Docs"
description: "如何在 Linux 的 Azure Web 應用程式中設定連續部署。"
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f8f7d51003f8a55b7f51e8cc2cea838e8e5a6196
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="f0481-104">在 Linux 上使用 Azure Web 應用程式連續部署</span><span class="sxs-lookup"><span data-stu-id="f0481-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="f0481-105">在本教學課程中，您可以從受控的 [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) 存放庫或 [Docker 中樞](https://hub.docker.com)設定自訂容器映像的連續部署。</span><span class="sxs-lookup"><span data-stu-id="f0481-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-to-azure"></a><span data-ttu-id="f0481-106">步驟 1 - 登入 Azure</span><span class="sxs-lookup"><span data-stu-id="f0481-106">Step 1 - Sign in to Azure</span></span>

<span data-ttu-id="f0481-107">登入 Azure 入口網站 (網址是 http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f0481-107">Sign in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="f0481-108">步驟 2 - 啟用容器連續部署功能</span><span class="sxs-lookup"><span data-stu-id="f0481-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="f0481-109">您可以使用 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) 並執行下列命令來啟用持續部署功能</span><span class="sxs-lookup"><span data-stu-id="f0481-109">You can enable the continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="f0481-110">在 **[Azure 入口網站](https://portal.azure.com/)**中，按一下頁面左側的 [App Service] 選項。</span><span class="sxs-lookup"><span data-stu-id="f0481-110">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="f0481-111">按一下您想要設定 Docker 中樞連續部署的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="f0481-111">Click on the name of your app that you want to configure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="f0481-112">在 [應用程式設定] 中，新增名為 `DOCKER_ENABLE_CI` 且包含 `true` 值的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="f0481-112">In the **App settings**, add an app setting called `DOCKER_ENABLE_CI` with the value `true`.</span></span>

![將應用程式設定的影像插入](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="f0481-114">步驟 3 - 準備 Webhook URL</span><span class="sxs-lookup"><span data-stu-id="f0481-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="f0481-115">您可以使用 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) 並執行下列命令來取得 Webhook URL</span><span class="sxs-lookup"><span data-stu-id="f0481-115">You can obtain the Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="f0481-116">針對 Webhook URL，您必須擁有下列端點︰`https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`。</span><span class="sxs-lookup"><span data-stu-id="f0481-116">For the Webhook URL, you need to have the following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="f0481-117">您可以取得 `publishingusername` 和 `publishingpwd`，方法是使用 Azure 入口網站來下載 Web 應用程式發佈設定檔。</span><span class="sxs-lookup"><span data-stu-id="f0481-117">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span></span>

![將新增 webhook 2 的映像插入](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="f0481-119">步驟 4：新增 Web Hook</span><span class="sxs-lookup"><span data-stu-id="f0481-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="f0481-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="f0481-120">Azure Container Registry</span></span>

<span data-ttu-id="f0481-121">在您的登錄入口網站刀鋒視窗中，按一下 [Webhook]，按一下 [新增] 以建立新的 webhook。</span><span class="sxs-lookup"><span data-stu-id="f0481-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="f0481-122">在 [建立 webhook] 刀鋒視窗中，提供您的 webhook 名稱。</span><span class="sxs-lookup"><span data-stu-id="f0481-122">In the **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="f0481-123">在 Webhook URI 中，您需要提供從**步驟 3** 取得的 URL。</span><span class="sxs-lookup"><span data-stu-id="f0481-123">For the Webhook URI, you need to provide the URL obtained from **Step 3**</span></span>

<span data-ttu-id="f0481-124">請確定您將範圍定義為包含您的容器映像的存放庫。</span><span class="sxs-lookup"><span data-stu-id="f0481-124">Make sure that you define the scope as the repo that contains your container image.</span></span>

![插入 webhook 的映像](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="f0481-126">當更新映像時，Web 應用程式會以新的映像自動進行更新。</span><span class="sxs-lookup"><span data-stu-id="f0481-126">When the image gets updated, the web app get updated automatically with the new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="f0481-127">Docker 中樞</span><span class="sxs-lookup"><span data-stu-id="f0481-127">Docker Hub</span></span>

<span data-ttu-id="f0481-128">在您的 [Docker 中樞] 頁面上，依序按一下 [Webhook]、[建立 WEBHOOK]。</span><span class="sxs-lookup"><span data-stu-id="f0481-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![將新增 webhook 1 的映像插入](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="f0481-130">在 Webhook URL 中，您需要提供從**步驟 3** 取得的 URL。</span><span class="sxs-lookup"><span data-stu-id="f0481-130">For the Webhook URL, you need to provide the URL obtained from **Step 3**</span></span>

![將新增 webhook 2 的映像插入](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="f0481-132">當更新映像時，Web 應用程式會以新的映像自動進行更新。</span><span class="sxs-lookup"><span data-stu-id="f0481-132">When the image gets updated, the web app get updated automatically with the new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0481-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0481-133">Next steps</span></span>
* [<span data-ttu-id="f0481-134">什麼是 Linux 上的 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="f0481-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="f0481-135">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="f0481-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="f0481-136">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="f0481-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="f0481-137">在 Linux 上的 Azure Web 應用程式中使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="f0481-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="f0481-138">在 Linux 上的 Azure Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="f0481-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="f0481-139">如何針對 Linux 上的 Azure Web 應用程式使用自訂 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="f0481-139">How to use a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="f0481-140">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="f0481-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="f0481-141">在 Linux 上使用 Azure CLI 2.0 管理 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f0481-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



