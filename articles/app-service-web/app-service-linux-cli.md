---
title: "使用 Azure CLI 2.0 Linux 上的 Web 應用程式 aaaManage |Microsoft 文件"
description: "在 Linux 上使用 Azure CLI 管理 Web 應用程式。"
keywords: "azure app service, web 應用程式, cli, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="b3a55-104">在 Linux 上使用 Azure CLI 管理 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b3a55-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="b3a55-105">您使用本文章中的 hello 命令都能 toocreate 和管理使用 Azure CLI 2.0 Linux 上的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3a55-105">Using hello commands in this article you are able toocreate and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="b3a55-106">您可以開始使用 hello 新 hello CLI 有兩種版本：</span><span class="sxs-lookup"><span data-stu-id="b3a55-106">You can start using hello new version of hello CLI in two ways:</span></span>

* <span data-ttu-id="b3a55-107">在您的電腦上[安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="b3a55-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="b3a55-108">使用 [Azure Cloud Shell (預覽)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="b3a55-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="b3a55-109">建立 Linux App Service 方案</span><span class="sxs-lookup"><span data-stu-id="b3a55-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="b3a55-110">toocreate Linux 應用程式服務方案，您可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3a55-110">toocreate a Linux App Service Plan, you can use hello following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="b3a55-111">建立自訂 Docker 容器 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b3a55-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="b3a55-112">toocreate web 應用程式並將它設定為 toorun 自訂的 Docker 容器，您可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3a55-112">toocreate a web app and configuring it toorun a custom Docker container, you can use hello following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a><span data-ttu-id="b3a55-113">啟動 hello Docker 容器的記錄</span><span class="sxs-lookup"><span data-stu-id="b3a55-113">Activate hello Docker container logging</span></span>

<span data-ttu-id="b3a55-114">tooactivate hello Docker 容器的記錄，您可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3a55-114">tooactivate hello Docker container logging, you can use hello following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="b3a55-115">Linux 應用程式上的現有 Web 應用程式變更 hello 自訂的 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="b3a55-115">Change hello custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="b3a55-116">toochange 先前建立的應用程式，從 hello 目前 Docker 映像 tooa 新映像，您可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3a55-116">toochange a previously created app, from hello current Docker image tooa new image, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="b3a55-117">使用私人登錄中的 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="b3a55-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="b3a55-118">您可以設定您的應用程式 toouse 映像從私用的登錄。</span><span class="sxs-lookup"><span data-stu-id="b3a55-118">You can configure your app toouse images from a private registry.</span></span> <span data-ttu-id="b3a55-119">您需要 tooprovide hello url 登錄、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b3a55-119">You need tooprovide hello url for your registry, user name, and password.</span></span> <span data-ttu-id="b3a55-120">這可以使用下列命令的 hello 來達成：</span><span class="sxs-lookup"><span data-stu-id="b3a55-120">This can be achieved using hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="b3a55-121">啟用自訂 Docker 映像的連續部署</span><span class="sxs-lookup"><span data-stu-id="b3a55-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="b3a55-122">以下列的命令，您可以啟用 hello hello CD 功能，並取得 hello webhook url。</span><span class="sxs-lookup"><span data-stu-id="b3a55-122">With hello following command you can enable hello CD functionality, and get hello webhook url.</span></span> <span data-ttu-id="b3a55-123">這個 url 可以是使用的 tooconfigure 您 DockerHub 或 Azure 容器登錄中儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b3a55-123">This url can be used tooconfigure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="b3a55-124">在 Linux 上使用其中一個內建執行階段架構來建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b3a55-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="b3a55-125">toocreate PHP 5.6 Web 應用程式，您可以使用下列命令的 hello Linux 應用程式上。</span><span class="sxs-lookup"><span data-stu-id="b3a55-125">toocreate a PHP 5.6 Web App on Linux App that, you can use hello following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="b3a55-126">在 Linux 應用程式上變更現有 Web 應用程式的架構版本</span><span class="sxs-lookup"><span data-stu-id="b3a55-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="b3a55-127">toochange 先前建立的應用程式，從目前架構版本 tooNode.js hello 6.11，您可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3a55-127">toochange a previously created app, from hello current framework version tooNode.js 6.11, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="b3a55-128">為您的 Web 應用程式設定 Git 部署</span><span class="sxs-lookup"><span data-stu-id="b3a55-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="b3a55-129">tooset 向上 Git 部署應用程式，您可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3a55-129">tooset up Git deployments for your app, you can use hello following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="b3a55-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3a55-130">Next steps</span></span>
* [<span data-ttu-id="b3a55-131">什麼是 Linux 上的 Azure Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="b3a55-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="b3a55-132">安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b3a55-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="b3a55-133">Azure Cloud Shell (預覽)</span><span class="sxs-lookup"><span data-stu-id="b3a55-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="b3a55-134">在 Azure App Service 中設定預備環境</span><span class="sxs-lookup"><span data-stu-id="b3a55-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="b3a55-135">在 Linux 上使用 Azure Web 應用程式持續部署</span><span class="sxs-lookup"><span data-stu-id="b3a55-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
