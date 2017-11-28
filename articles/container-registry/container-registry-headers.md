---
title: "aaaAzure 容器登錄儲存機制 |Microsoft 文件"
description: "如何針對 Docker 映像 toouse Azure 容器登錄中儲存機制"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="e7c36-103">Azure 容器登錄存放庫</span><span class="sxs-lookup"><span data-stu-id="e7c36-103">Azure container registry repositories</span></span>

<span data-ttu-id="e7c36-104">Azure Container Registry 與許多服務和 Orchestrator 相容。</span><span class="sxs-lookup"><span data-stu-id="e7c36-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="e7c36-105">toomake 它更容易 tootrack hello 來源服務和代理程式從中使用 ACR，我們已開始使用 hello Docker.config 檔案中的 hello Docker 標頭欄位。</span><span class="sxs-lookup"><span data-stu-id="e7c36-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="e7c36-106">在 hello 入口網站中檢視儲存機制</span><span class="sxs-lookup"><span data-stu-id="e7c36-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="e7c36-107">hello ACR 標頭，請遵循 hello 格式：</span><span class="sxs-lookup"><span data-stu-id="e7c36-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="e7c36-108">雲端：Azure、Azure Stack 或是其他政府或國家/地區特定的 Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="e7c36-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="e7c36-109">雖然目前不支援 Azure Stack 和政府雲端，此參數未來可允許支援。</span><span class="sxs-lookup"><span data-stu-id="e7c36-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="e7c36-110">服務： hello 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="e7c36-110">Service: name of hello service.</span></span>
* <span data-ttu-id="e7c36-111">Optionalservicename： 服務與子服務或 toospecify SKU 選擇性參數 (例如： web 應用程式會與 Azure/應用程式層服務/web 層應用程式的對應)。</span><span class="sxs-lookup"><span data-stu-id="e7c36-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="e7c36-112">協力廠商服務和 orchestrators 是鼓勵的 toouse 特定標頭值 toohelp 與我們的遙測。</span><span class="sxs-lookup"><span data-stu-id="e7c36-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="e7c36-113">使用者也可以修改 hello 依需要傳遞 toohello 標頭的值。</span><span class="sxs-lookup"><span data-stu-id="e7c36-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="e7c36-114">hello 我們想要的 ACR 夥伴 toouse toopopulate hello 「 X-中繼-來源-用戶端 」 欄位的值如下：</span><span class="sxs-lookup"><span data-stu-id="e7c36-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="e7c36-115">服務名稱</span><span class="sxs-lookup"><span data-stu-id="e7c36-115">Service Name</span></span>              | <span data-ttu-id="e7c36-116">頁首</span><span class="sxs-lookup"><span data-stu-id="e7c36-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="e7c36-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="e7c36-117">Azure Container Service</span></span>   | <span data-ttu-id="e7c36-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="e7c36-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="e7c36-119">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="e7c36-119">App Service - Web Apps</span></span>    | <span data-ttu-id="e7c36-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="e7c36-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="e7c36-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e7c36-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="e7c36-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="e7c36-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="e7c36-123">批次</span><span class="sxs-lookup"><span data-stu-id="e7c36-123">Batch</span></span>                     | <span data-ttu-id="e7c36-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="e7c36-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="e7c36-125">雲端主控台</span><span class="sxs-lookup"><span data-stu-id="e7c36-125">Cloud Console</span></span>             | <span data-ttu-id="e7c36-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="e7c36-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="e7c36-127">Functions</span><span class="sxs-lookup"><span data-stu-id="e7c36-127">Functions</span></span>                 | <span data-ttu-id="e7c36-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="e7c36-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="e7c36-129">物聯網 - 中樞</span><span class="sxs-lookup"><span data-stu-id="e7c36-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="e7c36-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="e7c36-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="e7c36-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7c36-131">HDInsight</span></span>                 | <span data-ttu-id="e7c36-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="e7c36-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="e7c36-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="e7c36-133">Jenkins</span></span>                   | <span data-ttu-id="e7c36-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="e7c36-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="e7c36-135">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="e7c36-135">Machine Learning</span></span>          | <span data-ttu-id="e7c36-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="e7c36-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="e7c36-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e7c36-137">Service Fabric</span></span>            | <span data-ttu-id="e7c36-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="e7c36-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="e7c36-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="e7c36-139">VSTS</span></span>                      | <span data-ttu-id="e7c36-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="e7c36-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="e7c36-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7c36-141">Next steps</span></span>
[<span data-ttu-id="e7c36-142">深入了解登錄和 orchestrators hello 支援服務</span><span class="sxs-lookup"><span data-stu-id="e7c36-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
