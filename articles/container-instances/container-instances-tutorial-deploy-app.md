---
title: "aaaAzure 容器執行個體的教學課程-應用程式部署 |Microsoft 文件"
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
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a><span data-ttu-id="8e359-103">部署容器 tooAzure 容器執行個體</span><span class="sxs-lookup"><span data-stu-id="8e359-103">Deploy a container tooAzure Container Instances</span></span>

<span data-ttu-id="8e359-104">這是 hello 三段式教學課程的最後一個。</span><span class="sxs-lookup"><span data-stu-id="8e359-104">This is hello last of a three-part tutorial.</span></span> <span data-ttu-id="8e359-105">上一節，[建立容器映像來源](container-instances-tutorial-prepare-app.md)和[推入 tooan Azure 容器登錄中](container-instances-tutorial-prepare-acr.md)。</span><span class="sxs-lookup"><span data-stu-id="8e359-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed tooan Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="8e359-106">本節藉由部署 hello 容器 tooAzure 容器執行個體完成 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="8e359-106">This section completes hello tutorial by deploying hello container tooAzure Container Instances.</span></span> <span data-ttu-id="8e359-107">完成的步驟包括：</span><span class="sxs-lookup"><span data-stu-id="8e359-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8e359-108">使用 Azure Resource Manager 範本來定義容器群組</span><span class="sxs-lookup"><span data-stu-id="8e359-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="8e359-109">部署使用 Azure CLI hello hello 容器群組</span><span class="sxs-lookup"><span data-stu-id="8e359-109">Deploying hello container group using hello Azure CLI</span></span>
> * <span data-ttu-id="8e359-110">檢視容器記錄</span><span class="sxs-lookup"><span data-stu-id="8e359-110">Viewing container logs</span></span>

## <a name="deploy-hello-container-using-hello-azure-cli"></a><span data-ttu-id="8e359-111">部署使用 Azure CLI hello hello 容器</span><span class="sxs-lookup"><span data-stu-id="8e359-111">Deploy hello container using hello Azure CLI</span></span>

<span data-ttu-id="8e359-112">hello Azure CLI 能夠部署在單一命令中的容器 tooAzure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="8e359-112">hello Azure CLI enables deployment of a container tooAzure Container Instances in a single command.</span></span> <span data-ttu-id="8e359-113">因為 hello 容器映像裝載在 hello 私人 Azure 容器登錄中，您必須包含 hello 認證需要的 tooaccess 它。</span><span class="sxs-lookup"><span data-stu-id="8e359-113">Since hello container image is hosted in hello private Azure Container Registry, you must include hello credentials required tooaccess it.</span></span> <span data-ttu-id="8e359-114">如有必要，您可以查詢這些認證，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8e359-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="8e359-115">容器登錄的登入伺服器 (以登錄名稱來更新)：</span><span class="sxs-lookup"><span data-stu-id="8e359-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="8e359-116">容器登錄密碼：</span><span class="sxs-lookup"><span data-stu-id="8e359-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="8e359-117">toodeploy 1 CPU 核心和 1 GB 的記憶體，執行下列命令的 hello 要求您從 hello 容器登錄中與資源的容器映像：</span><span class="sxs-lookup"><span data-stu-id="8e359-117">toodeploy your container image from hello container registry with a resource request of 1 CPU core and 1GB of memory, run hello following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="8e359-118">在幾秒內，您就會從 Azure Resource Manager 收到首次的回應。</span><span class="sxs-lookup"><span data-stu-id="8e359-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="8e359-119">hello 部署中，使用 tooview hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="8e359-119">tooview hello state of hello deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="8e359-120">我們可以繼續執行此命令，直到 hello 狀態變更從*暫止*太*執行*。</span><span class="sxs-lookup"><span data-stu-id="8e359-120">We can continue running this command until hello state changes from *pending* too*running*.</span></span> <span data-ttu-id="8e359-121">然後我們可以繼續進行。</span><span class="sxs-lookup"><span data-stu-id="8e359-121">Then we can proceed.</span></span>

## <a name="view-hello-application-and-container-logs"></a><span data-ttu-id="8e359-122">檢視 hello 應用程式和容器的記錄檔</span><span class="sxs-lookup"><span data-stu-id="8e359-122">View hello application and container logs</span></span>

<span data-ttu-id="8e359-123">Hello 部署成功後，開啟瀏覽器 toohello IP 位址的下列命令的 hello hello 輸出所示：</span><span class="sxs-lookup"><span data-stu-id="8e359-123">Once hello deployment succeeds, open your browser toohello IP address shown in hello output of hello following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hello 瀏覽器中的 hello world 應用程式][aci-app-browser]

<span data-ttu-id="8e359-125">您也可以檢視 hello 的 hello 容器的記錄檔輸出：</span><span class="sxs-lookup"><span data-stu-id="8e359-125">You can also view hello log output of hello container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="8e359-126">輸出：</span><span class="sxs-lookup"><span data-stu-id="8e359-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="8e359-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e359-127">Next steps</span></span>

<span data-ttu-id="8e359-128">在本教學課程中，您完成部署您的容器 tooAzure 容器執行個體的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="8e359-128">In this tutorial, you completed hello process of deploying your containers tooAzure Container Instances.</span></span> <span data-ttu-id="8e359-129">已完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e359-129">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8e359-130">部署的 hello Azure 容器登錄中使用的 hello 容器 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8e359-130">Deploying hello container from hello Azure Container Registry using hello Azure CLI</span></span>
> * <span data-ttu-id="8e359-131">在 hello 瀏覽器中檢視 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="8e359-131">Viewing hello application in hello browser</span></span>
> * <span data-ttu-id="8e359-132">檢視 hello 容器的記錄檔</span><span class="sxs-lookup"><span data-stu-id="8e359-132">Viewing hello container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
