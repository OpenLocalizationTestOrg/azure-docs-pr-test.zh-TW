---
title: "Azure 容器執行個體教學課程 - 部署應用程式 | Microsoft Docs"
description: "Azure 容器執行個體教學課程 - 部署應用程式"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 54151a5c1850ab7120fe666a46dc5dc99c0f5157
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-to-azure-container-instances"></a><span data-ttu-id="ae257-103">將容器部署至 Azure 容器執行個體</span><span class="sxs-lookup"><span data-stu-id="ae257-103">Deploy a container to Azure Container Instances</span></span>

<span data-ttu-id="ae257-104">這是三段式教學課程的最後一段。</span><span class="sxs-lookup"><span data-stu-id="ae257-104">This is the last of a three-part tutorial.</span></span> <span data-ttu-id="ae257-105">在前面幾節中，我們[已建立容器映像](container-instances-tutorial-prepare-app.md)並[推送至 Azure Container Registry](container-instances-tutorial-prepare-acr.md)。</span><span class="sxs-lookup"><span data-stu-id="ae257-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed to an Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="ae257-106">本節會將容器部署至 Azure 容器執行個體，以完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="ae257-106">This section completes the tutorial by deploying the container to Azure Container Instances.</span></span> <span data-ttu-id="ae257-107">完成的步驟包括：</span><span class="sxs-lookup"><span data-stu-id="ae257-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae257-108">使用 Azure Resource Manager 範本來定義容器群組</span><span class="sxs-lookup"><span data-stu-id="ae257-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="ae257-109">使用 Azure CLI 來部署容器群組</span><span class="sxs-lookup"><span data-stu-id="ae257-109">Deploying the container group using the Azure CLI</span></span>
> * <span data-ttu-id="ae257-110">檢視容器記錄</span><span class="sxs-lookup"><span data-stu-id="ae257-110">Viewing container logs</span></span>

## <a name="deploy-the-container-using-the-azure-cli"></a><span data-ttu-id="ae257-111">使用 Azure CLI 來部署容器</span><span class="sxs-lookup"><span data-stu-id="ae257-111">Deploy the container using the Azure CLI</span></span>

<span data-ttu-id="ae257-112">Azure CLI 能夠透過單一命令將容器部署至 Azure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="ae257-112">The Azure CLI enables deployment of a container to Azure Container Instances in a single command.</span></span> <span data-ttu-id="ae257-113">由於容器映像裝載在私人 Azure Container Registry 中，因此您必須納入所需的認證才能存取該映像。</span><span class="sxs-lookup"><span data-stu-id="ae257-113">Since the container image is hosted in the private Azure Container Registry, you must include the credentials required to access it.</span></span> <span data-ttu-id="ae257-114">如有必要，您可以查詢這些認證，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ae257-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="ae257-115">容器登錄的登入伺服器 (以登錄名稱來更新)：</span><span class="sxs-lookup"><span data-stu-id="ae257-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="ae257-116">容器登錄密碼：</span><span class="sxs-lookup"><span data-stu-id="ae257-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="ae257-117">若要從容器登錄中使用 1 個 CPU 核心和 1 GB 記憶體的資源要求來部署您的容器映像，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ae257-117">To deploy your container image from the container registry with a resource request of 1 CPU core and 1GB of memory, run the following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="ae257-118">在幾秒內，您就會從 Azure Resource Manager 收到首次的回應。</span><span class="sxs-lookup"><span data-stu-id="ae257-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="ae257-119">若要檢視部署的狀態，請使用：</span><span class="sxs-lookup"><span data-stu-id="ae257-119">To view the state of the deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="ae257-120">我們可以繼續執行此命令，直到狀態從*擱置*變更為*執行中*。</span><span class="sxs-lookup"><span data-stu-id="ae257-120">We can continue running this command until the state changes from *pending* to *running*.</span></span> <span data-ttu-id="ae257-121">然後我們可以繼續進行。</span><span class="sxs-lookup"><span data-stu-id="ae257-121">Then we can proceed.</span></span>

## <a name="view-the-application-and-container-logs"></a><span data-ttu-id="ae257-122">檢視應用程式和容器記錄</span><span class="sxs-lookup"><span data-stu-id="ae257-122">View the application and container logs</span></span>

<span data-ttu-id="ae257-123">部署成功後，開啟瀏覽器以進入下列命令的輸出所顯示的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="ae257-123">Once the deployment succeeds, open your browser to the IP address shown in the output of the following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![瀏覽器中的 Hello World 應用程式][aci-app-browser]

<span data-ttu-id="ae257-125">您也可以檢視容器的記錄輸出：</span><span class="sxs-lookup"><span data-stu-id="ae257-125">You can also view the log output of the container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="ae257-126">輸出：</span><span class="sxs-lookup"><span data-stu-id="ae257-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="ae257-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae257-127">Next steps</span></span>

<span data-ttu-id="ae257-128">在本教學課程中，您已完成將容器部署至 Azure 容器執行個體的程序。</span><span class="sxs-lookup"><span data-stu-id="ae257-128">In this tutorial, you completed the process of deploying your containers to Azure Container Instances.</span></span> <span data-ttu-id="ae257-129">已完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ae257-129">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae257-130">使用 Azure CLI 從 Azure Container Registry 部署容器</span><span class="sxs-lookup"><span data-stu-id="ae257-130">Deploying the container from the Azure Container Registry using the Azure CLI</span></span>
> * <span data-ttu-id="ae257-131">在瀏覽器中檢視應用程式</span><span class="sxs-lookup"><span data-stu-id="ae257-131">Viewing the application in the browser</span></span>
> * <span data-ttu-id="ae257-132">檢視容器記錄</span><span class="sxs-lookup"><span data-stu-id="ae257-132">Viewing the container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
