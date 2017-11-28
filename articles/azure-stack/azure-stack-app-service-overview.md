---
title: "App Service 概觀：Azure Stack | Microsoft Docs"
description: "Azure Stack 上的 App Service 概觀"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: 1d763f592212b3a2dcc2f03ebe317eed84e9e2de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-overview"></a><span data-ttu-id="68457-103">Azure Stack 概觀上的 App Service</span><span class="sxs-lookup"><span data-stu-id="68457-103">App Service on Azure Stack overview</span></span>

<span data-ttu-id="68457-104">Azure 堆疊上的 azure App Service 為 hello Azure 帶來的供應項目 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="68457-104">Azure App Service on Azure Stack is hello Azure offering brought tooAzure Stack.</span></span> <span data-ttu-id="68457-105">hello 應用程式服務在 Azure 堆疊安裝程式會建立下列角色的執行個體的 hello:</span><span class="sxs-lookup"><span data-stu-id="68457-105">hello App Service on Azure Stack installer creates hello following set of role instances:</span></span>

*  <span data-ttu-id="68457-106">Controller</span><span class="sxs-lookup"><span data-stu-id="68457-106">Controller</span></span>
*  <span data-ttu-id="68457-107">管理 (會建立兩個執行個體)</span><span class="sxs-lookup"><span data-stu-id="68457-107">Management (two instances are created)</span></span>
*  <span data-ttu-id="68457-108">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="68457-108">FrontEnd</span></span>
*  <span data-ttu-id="68457-109">發佈者</span><span class="sxs-lookup"><span data-stu-id="68457-109">Publisher</span></span>
*  <span data-ttu-id="68457-110">背景工作 (處於共用模式)</span><span class="sxs-lookup"><span data-stu-id="68457-110">Worker (in Shared mode)</span></span>

<span data-ttu-id="68457-111">此外，hello 應用程式服務在 Azure 堆疊安裝程式會建立檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="68457-111">In addition, hello App Service on Azure Stack installer creates a file server.</span></span>
    
## <a name="whats-new-in-hello-first-release-candidate-of-app-service-on-azure-stack"></a><span data-ttu-id="68457-112">什麼是 hello 第一個發行候選版本的 Azure 堆疊上的應用程式服務的新功能？</span><span class="sxs-lookup"><span data-stu-id="68457-112">What's new in hello first release candidate of App Service on Azure Stack?</span></span>
![Hello Azure 堆疊入口網站中的應用程式服務][1]

<span data-ttu-id="68457-114">hello 第一個發行候選版本的 Azure 堆疊上的應用程式服務建置在 hello 第三個 preview 之上，並使新的功能與改良功能：</span><span class="sxs-lookup"><span data-stu-id="68457-114">hello first release candidate of App Service on Azure Stack builds on top of hello third preview and brings new capabilities and improvements:</span></span>

* <span data-ttu-id="68457-115">以 Active Directory 同盟服務為基礎之 Azure Stack 環境中的 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="68457-115">Azure Functions in Azure Stack environments based on Active Directory Federation Services</span></span> 
* <span data-ttu-id="68457-116">單一登入支援 hello 函式的入口網站和 hello 進階開發人員工具 (Kudu)</span><span class="sxs-lookup"><span data-stu-id="68457-116">Single sign-on support for hello Functions portal and hello advanced developer tools (Kudu)</span></span>
* <span data-ttu-id="68457-117">適用於 Web、行動裝置版和 API 應用程式的 Java 支援</span><span class="sxs-lookup"><span data-stu-id="68457-117">Java support for web, mobile, and API applications</span></span>
* <span data-ttu-id="68457-118">背景工作層的虛擬機器規模管理服務系統管理員設定 tooimprove 擴充功能</span><span class="sxs-lookup"><span data-stu-id="68457-118">Management of worker tiers by virtual machine scale sets tooimprove scale-out capabilities for service administrators</span></span>
* <span data-ttu-id="68457-119">當地語系化的 hello 系統管理員體驗</span><span class="sxs-lookup"><span data-stu-id="68457-119">Localization of hello admin experience</span></span>
* <span data-ttu-id="68457-120">Hello 服務的更高的穩定性</span><span class="sxs-lookup"><span data-stu-id="68457-120">Increased stability of hello service</span></span>
* <span data-ttu-id="68457-121">租用戶入口網站體驗更新及安裝程序更新</span><span class="sxs-lookup"><span data-stu-id="68457-121">Tenant portal experience updates and installation process updates</span></span>

## <a name="limitations-of-hello-technical-preview"></a><span data-ttu-id="68457-122">Hello technical preview 的限制</span><span class="sxs-lookup"><span data-stu-id="68457-122">Limitations of hello technical preview</span></span>

<span data-ttu-id="68457-123">雖然我們不要監視 hello Azure 堆疊 MSDN 論壇沒有 hello 應用程式服務在 Azure 堆疊預覽版本中，支援。</span><span class="sxs-lookup"><span data-stu-id="68457-123">There is no support for hello App Service on Azure Stack preview releases, although we do monitor hello Azure Stack MSDN Forum.</span></span> <span data-ttu-id="68457-124">請勿將生產工作負載放在此預覽版本上。</span><span class="sxs-lookup"><span data-stu-id="68457-124">Do not put production workloads on this preview release.</span></span> <span data-ttu-id="68457-125">Azure Stack 上的 App Service 預覽版本之間也沒有任何升級。</span><span class="sxs-lookup"><span data-stu-id="68457-125">There is also no upgrade between App Service on Azure Stack preview releases.</span></span> <span data-ttu-id="68457-126">hello 這些預覽版本的主要目的是 tooshow 什麼我們提供和 tooobtain 意見反應。</span><span class="sxs-lookup"><span data-stu-id="68457-126">hello primary purposes of these preview releases are tooshow what we're providing and tooobtain feedback.</span></span> 

## <a name="what-is-an-app-service-plan"></a><span data-ttu-id="68457-127">什麼是 App Service 方案？</span><span class="sxs-lookup"><span data-stu-id="68457-127">What is an App Service plan?</span></span>

<span data-ttu-id="68457-128">hello 應用程式服務資源提供者會使用相同的程式碼，會使用 Azure App Service 的 hello。</span><span class="sxs-lookup"><span data-stu-id="68457-128">hello App Service resource provider uses hello same code that Azure App Service uses.</span></span> <span data-ttu-id="68457-129">因此，有些通用概念值得一提。</span><span class="sxs-lookup"><span data-stu-id="68457-129">As a result, some common concepts are worth describing.</span></span> <span data-ttu-id="68457-130">在應用程式服務定價應用程式容器中的 hello 稱為 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="68457-130">In App Service, hello pricing container for applications is called hello App Service plan.</span></span> <span data-ttu-id="68457-131">它代表使用專用的虛擬機器 toohold hello 組您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="68457-131">It represents hello set of dedicated virtual machines used toohold your apps.</span></span> <span data-ttu-id="68457-132">在指定訂用帳戶內，您可以有多個 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="68457-132">Within a given subscription, you can have multiple App Service plans.</span></span> 

<span data-ttu-id="68457-133">在 Azure 中，有共用和專用背景工作。</span><span class="sxs-lookup"><span data-stu-id="68457-133">In Azure, there are shared and dedicated workers.</span></span> <span data-ttu-id="68457-134">共用背景工作支援裝載高密度的多租用戶應用程式，而且只有一組共用背景工作。</span><span class="sxs-lookup"><span data-stu-id="68457-134">A shared worker supports high-density multitenant app hosting, and there is only one set of shared workers.</span></span> <span data-ttu-id="68457-135">專用伺服器只可供一個租用戶使用且分成三種大小：小型、中型和大型。</span><span class="sxs-lookup"><span data-stu-id="68457-135">Dedicated servers are used by only one tenant and come in three sizes: small, medium, and large.</span></span> <span data-ttu-id="68457-136">在內部部署客戶的 hello 需求永遠無法使用這些詞彙所述。</span><span class="sxs-lookup"><span data-stu-id="68457-136">hello needs of on-premises customers can't always be described by using those terms.</span></span> <span data-ttu-id="68457-137">在 Azure 堆疊上的應用程式服務，資源提供者系統管理員可以定義他們想要使用 toomake hello 背景工作層。</span><span class="sxs-lookup"><span data-stu-id="68457-137">In App Service on Azure Stack, resource provider administrators can define hello worker tiers they want toomake available.</span></span> <span data-ttu-id="68457-138">系統管理員可以根據其獨特的裝載需求，來定義多組共用背景工作或不同的專用背景工作組。</span><span class="sxs-lookup"><span data-stu-id="68457-138">Administrators can define multiple sets of shared workers or different sets of dedicated workers based on their unique hosting needs.</span></span> <span data-ttu-id="68457-139">透過使用這些背景工作層定義，他們接著就能定義自己的定價 SKU。</span><span class="sxs-lookup"><span data-stu-id="68457-139">By using those worker-tier definitions, they can then define their own pricing SKUs.</span></span>

## <a name="portal-features"></a><span data-ttu-id="68457-140">入口網站功能</span><span class="sxs-lookup"><span data-stu-id="68457-140">Portal features</span></span>

<span data-ttu-id="68457-141">Azure 堆疊上的應用程式服務會使用相同的 UI，Azure 應用程式服務所使用，如為 true 以 hello 回結束的 hello。</span><span class="sxs-lookup"><span data-stu-id="68457-141">App Service on Azure Stack uses hello same UI that Azure App Service uses, as is true with hello back end.</span></span> <span data-ttu-id="68457-142">某些功能已停用且無法在 Azure Stack 中運作。</span><span class="sxs-lookup"><span data-stu-id="68457-142">Some features are disabled and aren't functional in Azure Stack.</span></span> <span data-ttu-id="68457-143">hello Azure 特有的期望，或服務，這些功能都需要尚無法使用 Azure 堆疊中。</span><span class="sxs-lookup"><span data-stu-id="68457-143">hello Azure-specific expectations or services that those features require aren't yet available in Azure Stack.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="68457-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68457-144">Next steps</span></span>

- [<span data-ttu-id="68457-145">開始使用 Azure Stack 上的 App Service 之前</span><span class="sxs-lookup"><span data-stu-id="68457-145">Before you get started with App Service on Azure Stack</span></span>](azure-stack-app-service-before-you-get-started.md)
- [<span data-ttu-id="68457-146">安裝 hello 應用程式服務資源提供者</span><span class="sxs-lookup"><span data-stu-id="68457-146">Install hello App Service resource provider</span></span>](azure-stack-app-service-deploy.md)

<span data-ttu-id="68457-147">您也可以嘗試出其他[平台即服務 (PaaS) 服務](azure-stack-tools-paas-services.md)，像是 hello [SQL Server 資源提供者](azure-stack-sql-resource-provider-deploy.md)和 hello [MySQL 資源提供者](azure-stack-mysql-resource-provider-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="68457-147">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md), like hello [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and hello [MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-overview/AppService_Portal.png
