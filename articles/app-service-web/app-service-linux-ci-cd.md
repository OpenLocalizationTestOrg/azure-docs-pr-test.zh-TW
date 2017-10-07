---
title: "aaaContinuous on Linux 的 Azure Web 應用程式部署 |Microsoft 文件"
description: "如何在 Linux 上的 Azure Web 應用程式中的 toosetup 連續部署。"
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
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="48e35-104">在 Linux 上使用 Azure Web 應用程式連續部署</span><span class="sxs-lookup"><span data-stu-id="48e35-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="48e35-105">在本教學課程中，您可以從受控的 [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) 存放庫或 [Docker 中樞](https://hub.docker.com)設定自訂容器映像的連續部署。</span><span class="sxs-lookup"><span data-stu-id="48e35-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="48e35-106">步驟 1-登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="48e35-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="48e35-107">登入 toohello http://portal.azure.com 在 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="48e35-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="48e35-108">步驟 2 - 啟用容器連續部署功能</span><span class="sxs-lookup"><span data-stu-id="48e35-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="48e35-109">您可以使用的 hello 持續部署功能啟用[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)並執行下列命令的 hello</span><span class="sxs-lookup"><span data-stu-id="48e35-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="48e35-110">在 hello  **[Azure 入口網站](https://portal.azure.com/)**，按一下 hello **App Service** hello 左側的 hello 頁面的選項。</span><span class="sxs-lookup"><span data-stu-id="48e35-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="48e35-111">按一下您想要的 tooconfigure Docker Hub 連續部署的應用程式的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="48e35-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="48e35-112">在 hello**應用程式設定**，新增應用程式稱為`DOCKER_ENABLE_CI`hello 值`true`。</span><span class="sxs-lookup"><span data-stu-id="48e35-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![將應用程式設定的影像插入](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="48e35-114">步驟 3 - 準備 Webhook URL</span><span class="sxs-lookup"><span data-stu-id="48e35-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="48e35-115">您可以取得 hello Webhook URL 使用[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)並執行下列命令的 hello</span><span class="sxs-lookup"><span data-stu-id="48e35-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="48e35-116">Hello Webhook URL，您需要下列端點 toohave hello: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`。</span><span class="sxs-lookup"><span data-stu-id="48e35-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="48e35-117">您可以取得您`publishingusername`和`publishingpwd`下載 hello web 應用程式發行設定檔使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="48e35-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![將新增 webhook 2 的映像插入](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="48e35-119">步驟 4：新增 Web Hook</span><span class="sxs-lookup"><span data-stu-id="48e35-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="48e35-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="48e35-120">Azure Container Registry</span></span>

<span data-ttu-id="48e35-121">在您的登錄入口網站刀鋒視窗中，按一下 [Webhook]，按一下 [新增] 以建立新的 webhook。</span><span class="sxs-lookup"><span data-stu-id="48e35-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="48e35-122">在 hello**建立 webhook**刀鋒視窗中，提供您的 webhook 名稱。</span><span class="sxs-lookup"><span data-stu-id="48e35-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="48e35-123">Hello Webhook URI，您需要從取得的 tooprovide hello URL**步驟 3**</span><span class="sxs-lookup"><span data-stu-id="48e35-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="48e35-124">請確定您定義 hello 範圍，如 hello 包含您的容器映像儲存機制。</span><span class="sxs-lookup"><span data-stu-id="48e35-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![插入 webhook 的映像](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="48e35-126">取得更新 hello 映像，hello web 應用程式會自動更新會自動 hello 新映像。</span><span class="sxs-lookup"><span data-stu-id="48e35-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="48e35-127">Docker 中樞</span><span class="sxs-lookup"><span data-stu-id="48e35-127">Docker Hub</span></span>

<span data-ttu-id="48e35-128">在您的 [Docker 中樞] 頁面上，依序按一下 [Webhook]、[建立 WEBHOOK]。</span><span class="sxs-lookup"><span data-stu-id="48e35-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![將新增 webhook 1 的映像插入](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="48e35-130">Hello Webhook URL，您需要從取得的 tooprovide hello URL**步驟 3**</span><span class="sxs-lookup"><span data-stu-id="48e35-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![將新增 webhook 2 的映像插入](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="48e35-132">取得更新 hello 映像，hello web 應用程式會自動更新會自動 hello 新映像。</span><span class="sxs-lookup"><span data-stu-id="48e35-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48e35-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48e35-133">Next steps</span></span>
* [<span data-ttu-id="48e35-134">什麼是 Linux 上的 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="48e35-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="48e35-135">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="48e35-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="48e35-136">在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態</span><span class="sxs-lookup"><span data-stu-id="48e35-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="48e35-137">在 Linux 上的 Azure Web 應用程式中使用 .NET Core</span><span class="sxs-lookup"><span data-stu-id="48e35-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="48e35-138">在 Linux 上的 Azure Web 應用程式中使用 Ruby</span><span class="sxs-lookup"><span data-stu-id="48e35-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="48e35-139">Toouse 自訂的 Docker 的 Linux 上的 Azure Web 應用程式的映像</span><span class="sxs-lookup"><span data-stu-id="48e35-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="48e35-140">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="48e35-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="48e35-141">在 Linux 上使用 Azure CLI 2.0 管理 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="48e35-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



