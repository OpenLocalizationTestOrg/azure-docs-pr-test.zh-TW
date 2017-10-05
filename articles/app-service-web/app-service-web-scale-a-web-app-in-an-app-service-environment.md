---
title: "如何在 App Service 環境中調整應用程式"
description: "在 App Service 環境中調整應用程式"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 240c2486c23b7cd84e2471bf5b2170e08ee1f150
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a><span data-ttu-id="4e94f-103">在 App Service 環境中調整應用程式</span><span class="sxs-lookup"><span data-stu-id="4e94f-103">Scaling apps in an App Service Environment</span></span>
<span data-ttu-id="4e94f-104">在 Azure App Service 中，您通常有三件事可以調整：</span><span class="sxs-lookup"><span data-stu-id="4e94f-104">In the Azure App Service there are normally three things you can scale:</span></span>

* <span data-ttu-id="4e94f-105">定價方案</span><span class="sxs-lookup"><span data-stu-id="4e94f-105">pricing plan</span></span>
* <span data-ttu-id="4e94f-106">背景工作角色大小</span><span class="sxs-lookup"><span data-stu-id="4e94f-106">worker size</span></span> 
* <span data-ttu-id="4e94f-107">執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="4e94f-107">number of instances.</span></span>

<span data-ttu-id="4e94f-108">在 ASE 中不需要選取或變更定價方案。</span><span class="sxs-lookup"><span data-stu-id="4e94f-108">In an ASE there is no need to select or change the pricing plan.</span></span>  <span data-ttu-id="4e94f-109">就功能而言，它已經是 Premium 定價功能層級。</span><span class="sxs-lookup"><span data-stu-id="4e94f-109">In terms of capabilities it is already at a Premium pricing capability level.</span></span>  

<span data-ttu-id="4e94f-110">關於背景工作角色大小，ASE 系統管理員可以指派要用於每個背景工作角色集區的計算資源大小。</span><span class="sxs-lookup"><span data-stu-id="4e94f-110">With respect to worker sizes, the ASE admin can assign the size of the compute resource to be used for each worker pool.</span></span>  <span data-ttu-id="4e94f-111">這表示您可以有具 P4 計算資源的背景工作集區 1，以及具 P1 計算資源的背景工作集區 2 (如有需要的話)。</span><span class="sxs-lookup"><span data-stu-id="4e94f-111">That means you can have Worker Pool 1 with P4 compute resources and Worker Pool 2 with P1 compute resources, if desired.</span></span>  <span data-ttu-id="4e94f-112">它們並沒有大小順序。</span><span class="sxs-lookup"><span data-stu-id="4e94f-112">They do not have to be in size order.</span></span>  <span data-ttu-id="4e94f-113">如需大小及其定價的詳細資訊，請參閱此處的文件 [Azure App Service 定價][AppServicePricing]。</span><span class="sxs-lookup"><span data-stu-id="4e94f-113">For details around the sizes and their pricing see the document here [Azure App Service Pricing][AppServicePricing].</span></span>  <span data-ttu-id="4e94f-114">以下是 App Service 環境中的 Web 應用程式和 App Service 方案的調整選項：</span><span class="sxs-lookup"><span data-stu-id="4e94f-114">This leaves the scaling options for web apps and App Service Plans in an App Service Environment to be:</span></span>

* <span data-ttu-id="4e94f-115">背景工作集區選取</span><span class="sxs-lookup"><span data-stu-id="4e94f-115">worker pool selection</span></span>
* <span data-ttu-id="4e94f-116">執行個體數目</span><span class="sxs-lookup"><span data-stu-id="4e94f-116">number of instances</span></span>

<span data-ttu-id="4e94f-117">如需變更任一項目，都可以透過針對 ASE 託管之 App Service 方案所顯示的適用 UI 完成。</span><span class="sxs-lookup"><span data-stu-id="4e94f-117">Changing either item is done through the appropriate UI shown for your ASE hosted App Service Plans.</span></span>  

![][1]

<span data-ttu-id="4e94f-118">ASP 相應增加的數量無法超過 ASP 所在背景工作集區中可用的計算資源數量。</span><span class="sxs-lookup"><span data-stu-id="4e94f-118">You can't scale up your ASP beyond the number of available compute resources in the worker pool that your ASP is in.</span></span>  <span data-ttu-id="4e94f-119">如果背景工作集區中需要計算資源，您必須讓 ASE 系統管理員增加資源。</span><span class="sxs-lookup"><span data-stu-id="4e94f-119">If you need compute resources in that worker pool you need to get your ASE administrator to add them.</span></span>  <span data-ttu-id="4e94f-120">如需重新設定 ASE 的資訊，請閱讀以下資訊：[如何設定 App Service 環境][HowtoConfigureASE]。</span><span class="sxs-lookup"><span data-stu-id="4e94f-120">For information around re-configuring your ASE read the information here: [How to Configure an App Service environment][HowtoConfigureASE].</span></span>  <span data-ttu-id="4e94f-121">您也可能需利用 ASE 自動調整功能，以根據排程或計量增加容量。</span><span class="sxs-lookup"><span data-stu-id="4e94f-121">You may also want to take advantage of the ASE autoscale features to add capacity based on schedule or metrics.</span></span>  <span data-ttu-id="4e94f-122">若要取得設定 ASE 環境本身自動調整的相關詳細資訊，請參閱[如何設定 App Service 環境的自動調整][ASEAutoscale]。</span><span class="sxs-lookup"><span data-stu-id="4e94f-122">To get more details on configuring autoscale for the ASE environment itself see [How to configure autoscale for an App Service Environment][ASEAutoscale].</span></span>

<span data-ttu-id="4e94f-123">您可以使用來自不同背景工作集區或相同背景工作集區的計算資源，建立多個 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4e94f-123">You can create multiple app service plans using compute resources from different worker pools, or you can use the same worker pool.</span></span>  <span data-ttu-id="4e94f-124">例如，如果在背景工作集區 1 中有 (10) 個可用的計算資源，您可以選擇使用 (6) 個計算資源建立一個 App Service 方案，而第二個 App Service 方案使用 (4) 個計算資源。</span><span class="sxs-lookup"><span data-stu-id="4e94f-124">For example if you have (10) available compute resources in Worker Pool 1, you can choose to create one app service plan using (6) compute resources, and a second app service plan that uses (4) compute resources.</span></span>

### <a name="scaling-the-number-of-instances"></a><span data-ttu-id="4e94f-125">調整執行個體數目</span><span class="sxs-lookup"><span data-stu-id="4e94f-125">Scaling the number of instances</span></span>
<span data-ttu-id="4e94f-126">當您初次在 App Service 環境中建立 Web 應用程式時，它會從 1 個執行個體開始。</span><span class="sxs-lookup"><span data-stu-id="4e94f-126">When you first create your web app in an App Service Environment it starts with 1 instance.</span></span>  <span data-ttu-id="4e94f-127">您可以再相應放大至其他的執行個體，為應用程式提供額外的計算資源。</span><span class="sxs-lookup"><span data-stu-id="4e94f-127">You can then scale out to additional instances to provide additional compute resources for your app.</span></span>   

<span data-ttu-id="4e94f-128">如果 ASE 有足夠的容量，這就很簡單。</span><span class="sxs-lookup"><span data-stu-id="4e94f-128">If your ASE has enough capacity then this is pretty simple.</span></span>  <span data-ttu-id="4e94f-129">您可移至具有您要相應增加之站台的 App Service 方案，然後選取 [調整]。</span><span class="sxs-lookup"><span data-stu-id="4e94f-129">You go to your App Service Plan that holds the sites you want to scale up and select Scale.</span></span>  <span data-ttu-id="4e94f-130">這會開啟 UI，您可以在當中為 ASP 手動設定調整或設定自動調整規則。</span><span class="sxs-lookup"><span data-stu-id="4e94f-130">This opens the UI where you can manually set the scale for your ASP or configure autoscale rules for your ASP.</span></span>  <span data-ttu-id="4e94f-131">若要手動調整應用程式，只需將 [調整依據] 設為 [手動輸入的執行個體計數]。</span><span class="sxs-lookup"><span data-stu-id="4e94f-131">To manually scale your app simply set ***Scale by*** to ***an instance count that I enter manually***.</span></span>  <span data-ttu-id="4e94f-132">從這裡拖曳滑桿至所需的數量，或將所需數量輸入滑桿旁邊的方塊。</span><span class="sxs-lookup"><span data-stu-id="4e94f-132">From here either drag the slider to the desired quantity or enter it in the box next to the slider.</span></span>  

![][2] 

<span data-ttu-id="4e94f-133">在 ASE 中的 ASP 自動調整規則與一般運作方式相同。</span><span class="sxs-lookup"><span data-stu-id="4e94f-133">The autoscale rules for an ASP in an ASE work the same as they do normally.</span></span>  <span data-ttu-id="4e94f-134">您可以選取 [調整依據] 下方的 [CPU 百分比]，根據 CPU 百分比建立 ASP 的自動調整規則，或使用 [排程和效能規則] 建立更複雜的規則。</span><span class="sxs-lookup"><span data-stu-id="4e94f-134">You can select ***CPU Percentage*** under ***Scale by*** and create autoscale rules for your ASP based on CPU Percentage or you can create more complex rules using ***schedule and performance rules***.</span></span>  <span data-ttu-id="4e94f-135">若要查看有關設定自動調整更完整的詳細資訊，請參閱此處的指南 [Azure App Service 中調整 Web 應用程式規模][AppScale]。</span><span class="sxs-lookup"><span data-stu-id="4e94f-135">To see more complete details on configuring autoscale use the guide here [Scale an app in Azure App Service][AppScale].</span></span> 

### <a name="worker-pool-selection"></a><span data-ttu-id="4e94f-136">背景工作集區選取</span><span class="sxs-lookup"><span data-stu-id="4e94f-136">Worker Pool selection</span></span>
<span data-ttu-id="4e94f-137">如前所述，背景工作角色集區選項需透過 ASP UI 存取。</span><span class="sxs-lookup"><span data-stu-id="4e94f-137">As noted earlier, the worker pool selection is accessed from the ASP UI.</span></span>  <span data-ttu-id="4e94f-138">開啟您想要調整的 ASP 刀鋒視窗，選取 [背景工作集區]。</span><span class="sxs-lookup"><span data-stu-id="4e94f-138">Open the blade for the ASP that you want to scale and select worker pool.</span></span>  <span data-ttu-id="4e94f-139">您會看到您已在 App Service 環境中設定的所有背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="4e94f-139">You will see all of the worker pools which you have configured in your App Service Environment.</span></span>  <span data-ttu-id="4e94f-140">如果您只有一個背景工作集區，您只會看到一個集區列出。</span><span class="sxs-lookup"><span data-stu-id="4e94f-140">If you have only one worker pool then you will only see the one pool listed.</span></span>  <span data-ttu-id="4e94f-141">若要變更 ASP 所在的背景工作角色集區，您只需選取 App Service 方案所要移入的背景工作角色集區。</span><span class="sxs-lookup"><span data-stu-id="4e94f-141">To change what worker pool your ASP is in, you simply select the worker pool you want your App Service Plan to move to.</span></span>  

![][3]

<span data-ttu-id="4e94f-142">將 ASP 從一個背景工作角色集區移到另一個集區之前，請務必確定您有足夠的容量可容納該 ASP。</span><span class="sxs-lookup"><span data-stu-id="4e94f-142">Before moving your ASP from one worker pool to another it is important to make sure you will have adequate capacity for your ASP.</span></span>  <span data-ttu-id="4e94f-143">在背景工作集區清單中，不只會列出背景工作集區名稱，您也可以查看該背景工作集區中有多少可用的背景工作。</span><span class="sxs-lookup"><span data-stu-id="4e94f-143">In the list of worker pools, not only is the worker pool name listed but you can also see how many workers are available in that worker pool.</span></span>  <span data-ttu-id="4e94f-144">請確定有足夠的執行個體可包含您的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4e94f-144">Make sure that there are enough instances available to contain your App Service Plan.</span></span>  <span data-ttu-id="4e94f-145">如果您需要在背景工作集區中移入更多計算資雲，則必須讓您的 ASE 系統管理員加以新增。</span><span class="sxs-lookup"><span data-stu-id="4e94f-145">If you need more compute resources in the worker pool you wish to move to, then get your ASE administrator to add them.</span></span>  

> [!NOTE]
> <span data-ttu-id="4e94f-146">從一個背景工作集區移出 ASP，會導致該 ASP 中的應用程式冷啟動。</span><span class="sxs-lookup"><span data-stu-id="4e94f-146">Moving an ASP from one worker pool will cause cold starts of the apps in that ASP.</span></span>  <span data-ttu-id="4e94f-147">這可能會導致要求的執行速度變慢，因為您的應用程式在新的計算資源上是冷啟動。</span><span class="sxs-lookup"><span data-stu-id="4e94f-147">This can cause requests to run slowly as your app is cold started on the new compute resources.</span></span>  <span data-ttu-id="4e94f-148">使用 Azure App Service 中的[應用程式準備功能][AppWarmup]可以避免冷啟動。</span><span class="sxs-lookup"><span data-stu-id="4e94f-148">The cold start can be avoided by using the [application warm up capability][AppWarmup] in Azure App Service.</span></span>  <span data-ttu-id="4e94f-149">本文所述的應用程式初始化模組對冷啟動也有作用，因為當應用程式在新的計算資源上冷啟動時，也會叫用初始化程序。</span><span class="sxs-lookup"><span data-stu-id="4e94f-149">The Application Initialization module described in the article also works for cold starts because the initialization process is also invoked when apps are cold started on new compute resources.</span></span> 
> 
> 

## <a name="getting-started"></a><span data-ttu-id="4e94f-150">開始使用</span><span class="sxs-lookup"><span data-stu-id="4e94f-150">Getting started</span></span>
<span data-ttu-id="4e94f-151">若要開始使用 App Service 環境，請參閱[如何建立 App Service 環境][HowtoCreateASE]</span><span class="sxs-lookup"><span data-stu-id="4e94f-151">To get started with App Service Environments, see [How To Create An App Service Environment][HowtoCreateASE]</span></span>

<span data-ttu-id="4e94f-152">如需有關 Azure App Service 平台的詳細資訊，請參閱 [Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="4e94f-152">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
