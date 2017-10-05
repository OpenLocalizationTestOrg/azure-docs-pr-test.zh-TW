---
title: "Azure 容器登錄存放庫 | Microsoft Docs"
description: "如何使用 Docker 映像的 Azure 容器登錄存放庫"
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
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="09bb4-103">Azure 容器登錄存放庫</span><span class="sxs-lookup"><span data-stu-id="09bb4-103">Azure container registry repositories</span></span>

<span data-ttu-id="09bb4-104">Azure Container Registry 與許多服務和 Orchestrator 相容。</span><span class="sxs-lookup"><span data-stu-id="09bb4-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="09bb4-105">為了更輕鬆地追蹤在其中使用 ACR 的來源服務及代理程式，我們已開始在 Docker.config 檔案中使用 Docker 標頭欄位。</span><span class="sxs-lookup"><span data-stu-id="09bb4-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="09bb4-106">在入口網站中檢視存放庫</span><span class="sxs-lookup"><span data-stu-id="09bb4-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="09bb4-107">ACR 標頭遵循下列格式：</span><span class="sxs-lookup"><span data-stu-id="09bb4-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="09bb4-108">雲端：Azure、Azure Stack 或是其他政府或國家/地區特定的 Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="09bb4-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="09bb4-109">雖然目前不支援 Azure Stack 和政府雲端，此參數未來可允許支援。</span><span class="sxs-lookup"><span data-stu-id="09bb4-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="09bb4-110">服務：服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="09bb4-110">Service: name of the service.</span></span>
* <span data-ttu-id="09bb4-111">Optionalservicename：具有子服務的服務選擇性參數，或指定 SKU (例如：Web 應用程式與 Azure/app-service/web-apps 對應)。</span><span class="sxs-lookup"><span data-stu-id="09bb4-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="09bb4-112">建議夥伴服務和 Orchestrator 使用特定的標頭值，以協助我們的遙測。</span><span class="sxs-lookup"><span data-stu-id="09bb4-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="09bb4-113">使用者也可以修改傳遞至標頭的值 (如需要)。</span><span class="sxs-lookup"><span data-stu-id="09bb4-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="09bb4-114">我們需要 ACR 夥伴用來填入 "X-Meta-Source-Client" 欄位的值如下所示：</span><span class="sxs-lookup"><span data-stu-id="09bb4-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="09bb4-115">服務名稱</span><span class="sxs-lookup"><span data-stu-id="09bb4-115">Service Name</span></span>              | <span data-ttu-id="09bb4-116">頁首</span><span class="sxs-lookup"><span data-stu-id="09bb4-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="09bb4-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="09bb4-117">Azure Container Service</span></span>   | <span data-ttu-id="09bb4-118">azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="09bb4-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="09bb4-119">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="09bb4-119">App Service - Web Apps</span></span>    | <span data-ttu-id="09bb4-120">azure/app-service/web-apps</span><span class="sxs-lookup"><span data-stu-id="09bb4-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="09bb4-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="09bb4-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="09bb4-122">azure/app-service/logic-apps</span><span class="sxs-lookup"><span data-stu-id="09bb4-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="09bb4-123">批次</span><span class="sxs-lookup"><span data-stu-id="09bb4-123">Batch</span></span>                     | <span data-ttu-id="09bb4-124">azure/compute/batch</span><span class="sxs-lookup"><span data-stu-id="09bb4-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="09bb4-125">雲端主控台</span><span class="sxs-lookup"><span data-stu-id="09bb4-125">Cloud Console</span></span>             | <span data-ttu-id="09bb4-126">azure/cloud-console</span><span class="sxs-lookup"><span data-stu-id="09bb4-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="09bb4-127">Functions</span><span class="sxs-lookup"><span data-stu-id="09bb4-127">Functions</span></span>                 | <span data-ttu-id="09bb4-128">azure/compute/functions</span><span class="sxs-lookup"><span data-stu-id="09bb4-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="09bb4-129">物聯網 - 中樞</span><span class="sxs-lookup"><span data-stu-id="09bb4-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="09bb4-130">azure/iot/hub</span><span class="sxs-lookup"><span data-stu-id="09bb4-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="09bb4-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="09bb4-131">HDInsight</span></span>                 | <span data-ttu-id="09bb4-132">azure/data/hdinsight</span><span class="sxs-lookup"><span data-stu-id="09bb4-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="09bb4-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="09bb4-133">Jenkins</span></span>                   | <span data-ttu-id="09bb4-134">azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="09bb4-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="09bb4-135">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="09bb4-135">Machine Learning</span></span>          | <span data-ttu-id="09bb4-136">azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="09bb4-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="09bb4-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="09bb4-137">Service Fabric</span></span>            | <span data-ttu-id="09bb4-138">azure/compute/service-fabric</span><span class="sxs-lookup"><span data-stu-id="09bb4-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="09bb4-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="09bb4-139">VSTS</span></span>                      | <span data-ttu-id="09bb4-140">azure/vsts</span><span class="sxs-lookup"><span data-stu-id="09bb4-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="09bb4-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09bb4-141">Next steps</span></span>
[<span data-ttu-id="09bb4-142">深入了解登錄和支援的服務與 Orchestrator</span><span class="sxs-lookup"><span data-stu-id="09bb4-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
