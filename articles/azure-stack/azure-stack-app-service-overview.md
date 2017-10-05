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
ms.openlocfilehash: 13928744e7d2fc145662c2a0d5c26d512cf02150
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="app-service-on-azure-stack-overview"></a><span data-ttu-id="fc5ec-103">Azure Stack 概觀上的 App Service</span><span class="sxs-lookup"><span data-stu-id="fc5ec-103">App Service on Azure Stack overview</span></span>

<span data-ttu-id="fc5ec-104">Azure Stack 上的 Azure App Service 是 Azure Stack 內含的 Azure 供應項目。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-104">Azure App Service on Azure Stack is the Azure offering brought to Azure Stack.</span></span> <span data-ttu-id="fc5ec-105">Azure Stack 上的 App Service 安裝程式會建立下列角色執行個體組合：</span><span class="sxs-lookup"><span data-stu-id="fc5ec-105">The App Service on Azure Stack installer creates the following set of role instances:</span></span>

*  <span data-ttu-id="fc5ec-106">Controller</span><span class="sxs-lookup"><span data-stu-id="fc5ec-106">Controller</span></span>
*  <span data-ttu-id="fc5ec-107">管理 (會建立兩個執行個體)</span><span class="sxs-lookup"><span data-stu-id="fc5ec-107">Management (two instances are created)</span></span>
*  <span data-ttu-id="fc5ec-108">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="fc5ec-108">FrontEnd</span></span>
*  <span data-ttu-id="fc5ec-109">發佈者</span><span class="sxs-lookup"><span data-stu-id="fc5ec-109">Publisher</span></span>
*  <span data-ttu-id="fc5ec-110">背景工作 (處於共用模式)</span><span class="sxs-lookup"><span data-stu-id="fc5ec-110">Worker (in Shared mode)</span></span>

<span data-ttu-id="fc5ec-111">此外，Azure Stack 上的 App Service 安裝程式也會建立檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-111">In addition, the App Service on Azure Stack installer creates a file server.</span></span>
    
## <a name="whats-new-in-the-first-release-candidate-of-app-service-on-azure-stack"></a><span data-ttu-id="fc5ec-112">Azure Stack 上之 App Service 的第一個候選版有哪些新功能？</span><span class="sxs-lookup"><span data-stu-id="fc5ec-112">What's new in the first release candidate of App Service on Azure Stack?</span></span>
![Azure Stack 上的 App Service 入口網站][1]

<span data-ttu-id="fc5ec-114">Azure Stack 上之 App Service 的第一個候選版建置於第三個預覽上，並引進了新功能與改良功能：</span><span class="sxs-lookup"><span data-stu-id="fc5ec-114">The first release candidate of App Service on Azure Stack builds on top of the third preview and brings new capabilities and improvements:</span></span>

* <span data-ttu-id="fc5ec-115">以 Active Directory 同盟服務為基礎之 Azure Stack 環境中的 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fc5ec-115">Azure Functions in Azure Stack environments based on Active Directory Federation Services</span></span> 
* <span data-ttu-id="fc5ec-116">對於 Functions 入口網站的單一登入支援以及進階開發人員工具 (Kudu)</span><span class="sxs-lookup"><span data-stu-id="fc5ec-116">Single sign-on support for the Functions portal and the advanced developer tools (Kudu)</span></span>
* <span data-ttu-id="fc5ec-117">適用於 Web、行動裝置版和 API 應用程式的 Java 支援</span><span class="sxs-lookup"><span data-stu-id="fc5ec-117">Java support for web, mobile, and API applications</span></span>
* <span data-ttu-id="fc5ec-118">依虛擬機器擴展集管理背景工作層，以改善服務管理員的相應放大功能</span><span class="sxs-lookup"><span data-stu-id="fc5ec-118">Management of worker tiers by virtual machine scale sets to improve scale-out capabilities for service administrators</span></span>
* <span data-ttu-id="fc5ec-119">將管理員體驗當地語系化</span><span class="sxs-lookup"><span data-stu-id="fc5ec-119">Localization of the admin experience</span></span>
* <span data-ttu-id="fc5ec-120">提高服務的穩定性</span><span class="sxs-lookup"><span data-stu-id="fc5ec-120">Increased stability of the service</span></span>
* <span data-ttu-id="fc5ec-121">租用戶入口網站體驗更新及安裝程序更新</span><span class="sxs-lookup"><span data-stu-id="fc5ec-121">Tenant portal experience updates and installation process updates</span></span>

## <a name="limitations-of-the-technical-preview"></a><span data-ttu-id="fc5ec-122">技術預覽的限制</span><span class="sxs-lookup"><span data-stu-id="fc5ec-122">Limitations of the technical preview</span></span>

<span data-ttu-id="fc5ec-123">儘管我們確實監看了 Azure Stack MSDN 論壇，但沒有任何對於 Azure Stack 上之 App Service 預覽版本的支援。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-123">There is no support for the App Service on Azure Stack preview releases, although we do monitor the Azure Stack MSDN Forum.</span></span> <span data-ttu-id="fc5ec-124">請勿將生產工作負載放在此預覽版本上。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-124">Do not put production workloads on this preview release.</span></span> <span data-ttu-id="fc5ec-125">Azure Stack 上的 App Service 預覽版本之間也沒有任何升級。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-125">There is also no upgrade between App Service on Azure Stack preview releases.</span></span> <span data-ttu-id="fc5ec-126">這些預覽版本的主要目的是顯示我們所提供的內容，並取得意見反應。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-126">The primary purposes of these preview releases are to show what we're providing and to obtain feedback.</span></span> 

## <a name="what-is-an-app-service-plan"></a><span data-ttu-id="fc5ec-127">什麼是 App Service 方案？</span><span class="sxs-lookup"><span data-stu-id="fc5ec-127">What is an App Service plan?</span></span>

<span data-ttu-id="fc5ec-128">App Service 資源提供者所使用的程式碼與 Azure App Service 使用的一樣。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-128">The App Service resource provider uses the same code that Azure App Service uses.</span></span> <span data-ttu-id="fc5ec-129">因此，有些通用概念值得一提。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-129">As a result, some common concepts are worth describing.</span></span> <span data-ttu-id="fc5ec-130">在 App Service 中，應用程式的定價容器稱為 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-130">In App Service, the pricing container for applications is called the App Service plan.</span></span> <span data-ttu-id="fc5ec-131">它代表用來保存您應用程式的專用虛擬機器組。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-131">It represents the set of dedicated virtual machines used to hold your apps.</span></span> <span data-ttu-id="fc5ec-132">在指定訂用帳戶內，您可以有多個 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-132">Within a given subscription, you can have multiple App Service plans.</span></span> 

<span data-ttu-id="fc5ec-133">在 Azure 中，有共用和專用背景工作。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-133">In Azure, there are shared and dedicated workers.</span></span> <span data-ttu-id="fc5ec-134">共用背景工作支援裝載高密度的多租用戶應用程式，而且只有一組共用背景工作。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-134">A shared worker supports high-density multitenant app hosting, and there is only one set of shared workers.</span></span> <span data-ttu-id="fc5ec-135">專用伺服器只可供一個租用戶使用且分成三種大小：小型、中型和大型。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-135">Dedicated servers are used by only one tenant and come in three sizes: small, medium, and large.</span></span> <span data-ttu-id="fc5ec-136">內部部署客戶的需求永遠無法使用這些詞彙來描述。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-136">The needs of on-premises customers can't always be described by using those terms.</span></span> <span data-ttu-id="fc5ec-137">在 Azure Stack 上的 App Service 中，資源提供者系統管理員可以定義他們想要提供的背景工作層。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-137">In App Service on Azure Stack, resource provider administrators can define the worker tiers they want to make available.</span></span> <span data-ttu-id="fc5ec-138">系統管理員可以根據其獨特的裝載需求，來定義多組共用背景工作或不同的專用背景工作組。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-138">Administrators can define multiple sets of shared workers or different sets of dedicated workers based on their unique hosting needs.</span></span> <span data-ttu-id="fc5ec-139">透過使用這些背景工作層定義，他們接著就能定義自己的定價 SKU。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-139">By using those worker-tier definitions, they can then define their own pricing SKUs.</span></span>

## <a name="portal-features"></a><span data-ttu-id="fc5ec-140">入口網站功能</span><span class="sxs-lookup"><span data-stu-id="fc5ec-140">Portal features</span></span>

<span data-ttu-id="fc5ec-141">Azure Stack 上的 App Service 所使用的 UI 與 Azure App Service 使用的相同，後端也是如此。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-141">App Service on Azure Stack uses the same UI that Azure App Service uses, as is true with the back end.</span></span> <span data-ttu-id="fc5ec-142">某些功能已停用且無法在 Azure Stack 中運作。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-142">Some features are disabled and aren't functional in Azure Stack.</span></span> <span data-ttu-id="fc5ec-143">Azure Stack 中尚未提供那些功能所需的 Azure 特有預期或服務。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-143">The Azure-specific expectations or services that those features require aren't yet available in Azure Stack.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fc5ec-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc5ec-144">Next steps</span></span>

- [<span data-ttu-id="fc5ec-145">開始使用 Azure Stack 上的 App Service 之前</span><span class="sxs-lookup"><span data-stu-id="fc5ec-145">Before you get started with App Service on Azure Stack</span></span>](azure-stack-app-service-before-you-get-started.md)
- [<span data-ttu-id="fc5ec-146">安裝 App Service 資源提供者</span><span class="sxs-lookup"><span data-stu-id="fc5ec-146">Install the App Service resource provider</span></span>](azure-stack-app-service-deploy.md)

<span data-ttu-id="fc5ec-147">您也可以嘗試其他[平台即服務 (PaaS) 服務](azure-stack-tools-paas-services.md)，例如 [SQL Server 資源提供者](azure-stack-sql-resource-provider-deploy.md)和 [MySQL 資源提供者](azure-stack-mysql-resource-provider-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="fc5ec-147">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md), like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and the [MySQL resource provider](azure-stack-mysql-resource-provider-deploy.md).</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-overview/AppService_Portal.png
