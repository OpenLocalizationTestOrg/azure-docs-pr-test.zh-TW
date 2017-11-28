---
title: "aaaHow tooScale App Service 環境中的應用程式"
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
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a><span data-ttu-id="2a7ce-103">在 App Service 環境中調整應用程式</span><span class="sxs-lookup"><span data-stu-id="2a7ce-103">Scaling apps in an App Service Environment</span></span>
<span data-ttu-id="2a7ce-104">Hello Azure App Service 中有正常三件事您可以調整：</span><span class="sxs-lookup"><span data-stu-id="2a7ce-104">In hello Azure App Service there are normally three things you can scale:</span></span>

* <span data-ttu-id="2a7ce-105">定價方案</span><span class="sxs-lookup"><span data-stu-id="2a7ce-105">pricing plan</span></span>
* <span data-ttu-id="2a7ce-106">背景工作角色大小</span><span class="sxs-lookup"><span data-stu-id="2a7ce-106">worker size</span></span> 
* <span data-ttu-id="2a7ce-107">執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-107">number of instances.</span></span>

<span data-ttu-id="2a7ce-108">在 ase 中沒有定價計劃需要 tooselect 或變更 hello。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-108">In an ASE there is no need tooselect or change hello pricing plan.</span></span>  <span data-ttu-id="2a7ce-109">就功能而言，它已經是 Premium 定價功能層級。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-109">In terms of capabilities it is already at a Premium pricing capability level.</span></span>  

<span data-ttu-id="2a7ce-110">尊重 tooworker 大小、 使用 hello ASE 系統管理員可以指派 hello hello 計算資源 toobe 用於每個背景工作集區大小。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-110">With respect tooworker sizes, hello ASE admin can assign hello size of hello compute resource toobe used for each worker pool.</span></span>  <span data-ttu-id="2a7ce-111">這表示您可以有具 P4 計算資源的背景工作集區 1，以及具 P1 計算資源的背景工作集區 2 (如有需要的話)。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-111">That means you can have Worker Pool 1 with P4 compute resources and Worker Pool 2 with P1 compute resources, if desired.</span></span>  <span data-ttu-id="2a7ce-112">它們並沒有 toobe 大小的順序。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-112">They do not have toobe in size order.</span></span>  <span data-ttu-id="2a7ce-113">如周圍 hello 大小和其定價的詳細資訊，請參閱 hello 文件[Azure 應用程式服務定價][AppServicePricing]。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-113">For details around hello sizes and their pricing see hello document here [Azure App Service Pricing][AppServicePricing].</span></span>  <span data-ttu-id="2a7ce-114">這會使擴充選項中的 App Service 環境 toobe web 應用程式和應用程式服務方案的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a7ce-114">This leaves hello scaling options for web apps and App Service Plans in an App Service Environment toobe:</span></span>

* <span data-ttu-id="2a7ce-115">背景工作集區選取</span><span class="sxs-lookup"><span data-stu-id="2a7ce-115">worker pool selection</span></span>
* <span data-ttu-id="2a7ce-116">執行個體數目</span><span class="sxs-lookup"><span data-stu-id="2a7ce-116">number of instances</span></span>

<span data-ttu-id="2a7ce-117">變更項目透過 hello 完成適當的顯示您 ASE 裝載應用程式服務方案的 UI。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-117">Changing either item is done through hello appropriate UI shown for your ASE hosted App Service Plans.</span></span>  

![][1]

<span data-ttu-id="2a7ce-118">您無法向上擴充您 ASP 是中的 hello 背景工作集區中的可執行的運算資源的 hello 數目超過您 ASP。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-118">You can't scale up your ASP beyond hello number of available compute resources in hello worker pool that your ASP is in.</span></span>  <span data-ttu-id="2a7ce-119">如果您需要計算該背景工作集區中的資源則需要 tooget 您 ASE 管理員 tooadd 它們。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-119">If you need compute resources in that worker pool you need tooget your ASE administrator tooadd them.</span></span>  <span data-ttu-id="2a7ce-120">資訊重新設定您 ASE 閱讀這裡 hello 資訊：[如何 tooConfigure App Service 環境][HowtoConfigureASE]。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-120">For information around re-configuring your ASE read hello information here: [How tooConfigure an App Service environment][HowtoConfigureASE].</span></span>  <span data-ttu-id="2a7ce-121">您也可以 tootake hello ASE 自動調整規模功能 tooadd 容量根據排程或度量的優點。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-121">You may also want tootake advantage of hello ASE autoscale features tooadd capacity based on schedule or metrics.</span></span>  <span data-ttu-id="2a7ce-122">設定自動調整規模的 hello ASE 環境本身的更多詳細資料請參閱的 tooget[如何 tooconfigure 自動調整規模的 App Service 環境][ASEAutoscale]。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-122">tooget more details on configuring autoscale for hello ASE environment itself see [How tooconfigure autoscale for an App Service Environment][ASEAutoscale].</span></span>

<span data-ttu-id="2a7ce-123">您可以建立多個應用程式服務方案使用不同的背景工作集區，從運算資源，或者您可以使用 hello 相同的背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-123">You can create multiple app service plans using compute resources from different worker pools, or you can use hello same worker pool.</span></span>  <span data-ttu-id="2a7ce-124">範例如果您在背景工作 (10) 的可執行的運算資源集區 1，則您可以選擇 toocreate 一個應用程式服務計劃使用 (6) 的計算資源，且第二個應用程式服務計劃，則會使用 (4) 的計算資源。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-124">For example if you have (10) available compute resources in Worker Pool 1, you can choose toocreate one app service plan using (6) compute resources, and a second app service plan that uses (4) compute resources.</span></span>

### <a name="scaling-hello-number-of-instances"></a><span data-ttu-id="2a7ce-125">調整執行個體的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="2a7ce-125">Scaling hello number of instances</span></span>
<span data-ttu-id="2a7ce-126">當您初次在 App Service 環境中建立 Web 應用程式時，它會從 1 個執行個體開始。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-126">When you first create your web app in an App Service Environment it starts with 1 instance.</span></span>  <span data-ttu-id="2a7ce-127">接著，您可以向外延展 tooadditional 執行個體 tooprovide 其他運算資源應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-127">You can then scale out tooadditional instances tooprovide additional compute resources for your app.</span></span>   

<span data-ttu-id="2a7ce-128">如果 ASE 有足夠的容量，這就很簡單。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-128">If your ASE has enough capacity then this is pretty simple.</span></span>  <span data-ttu-id="2a7ce-129">您移 tooyour App Service 方案保存您想 tooscale 和選取標尺的 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-129">You go tooyour App Service Plan that holds hello sites you want tooscale up and select Scale.</span></span>  <span data-ttu-id="2a7ce-130">這會開啟 hello 其中您可以手動設定您的 ASP hello 比例或您 asp 設定自動調整規模規則的 UI。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-130">This opens hello UI where you can manually set hello scale for your ASP or configure autoscale rules for your ASP.</span></span>  <span data-ttu-id="2a7ce-131">只要設定您的應用程式的 toomanually 標尺***縮放***太***手動輸入執行個體計數***。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-131">toomanually scale your app simply set ***Scale by*** too***an instance count that I enter manually***.</span></span>  <span data-ttu-id="2a7ce-132">從這裡拖曳 hello 滑桿 toohello 預期數量或是輸入 hello 方塊下一步 toohello 滑桿。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-132">From here either drag hello slider toohello desired quantity or enter it in hello box next toohello slider.</span></span>  

![][2] 

<span data-ttu-id="2a7ce-133">如同通常是 ASP 在 ASE 工作中的 hello 自動調整規模規則 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-133">hello autoscale rules for an ASP in an ASE work hello same as they do normally.</span></span>  <span data-ttu-id="2a7ce-134">您可以選取 [調整依據] 下方的 [CPU 百分比]，根據 CPU 百分比建立 ASP 的自動調整規則，或使用 [排程和效能規則] 建立更複雜的規則。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-134">You can select ***CPU Percentage*** under ***Scale by*** and create autoscale rules for your ASP based on CPU Percentage or you can create more complex rules using ***schedule and performance rules***.</span></span>  <span data-ttu-id="2a7ce-135">toosee 更完成詳細資料，設定自動調整規模使用 hello 指南此處[調整 Azure App Service 中的應用程式][AppScale]。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-135">toosee more complete details on configuring autoscale use hello guide here [Scale an app in Azure App Service][AppScale].</span></span> 

### <a name="worker-pool-selection"></a><span data-ttu-id="2a7ce-136">背景工作集區選取</span><span class="sxs-lookup"><span data-stu-id="2a7ce-136">Worker Pool selection</span></span>
<span data-ttu-id="2a7ce-137">如前文所述，從 hello ASP UI 存取 hello 背景工作集區選取範圍。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-137">As noted earlier, hello worker pool selection is accessed from hello ASP UI.</span></span>  <span data-ttu-id="2a7ce-138">開啟 hello ASP tooscale 並選取 背景工作集區的 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-138">Open hello blade for hello ASP that you want tooscale and select worker pool.</span></span>  <span data-ttu-id="2a7ce-139">您會看到所有您已設定您的 App Service 環境中的 hello 背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-139">You will see all of hello worker pools which you have configured in your App Service Environment.</span></span>  <span data-ttu-id="2a7ce-140">如果您有只有一個背景工作集區然後您只會看到列出 hello 一個集區。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-140">If you have only one worker pool then you will only see hello one pool listed.</span></span>  <span data-ttu-id="2a7ce-141">toochange 哪些背景工作集區您 ASP 中，您只需選取您想要您 App Service 方案 toomove hello 背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-141">toochange what worker pool your ASP is in, you simply select hello worker pool you want your App Service Plan toomove to.</span></span>  

![][3]

<span data-ttu-id="2a7ce-142">從一個背景工作集區 tooanother 移動您 ASP 之前很重要 toomake 確定您將必須針對您 ASP 適當的容量。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-142">Before moving your ASP from one worker pool tooanother it is important toomake sure you will have adequate capacity for your ASP.</span></span>  <span data-ttu-id="2a7ce-143">在 hello 清單中的背景工作集區，不只列出 hello 背景工作集區名稱，但您也可以查看多少的背景工作的背景工作集區中可用。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-143">In hello list of worker pools, not only is hello worker pool name listed but you can also see how many workers are available in that worker pool.</span></span>  <span data-ttu-id="2a7ce-144">請確定有足夠的執行個體可用 toocontain 您 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-144">Make sure that there are enough instances available toocontain your App Service Plan.</span></span>  <span data-ttu-id="2a7ce-145">如果您需要更多計算 hello 背景工作集區中的資源您想要然後取得您 ASE 管理員 tooadd toomove 它們。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-145">If you need more compute resources in hello worker pool you wish toomove to, then get your ASE administrator tooadd them.</span></span>  

> [!NOTE]
> <span data-ttu-id="2a7ce-146">移動 ASP 從一個背景工作集區會導致冷啟動 hello 該 ASP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-146">Moving an ASP from one worker pool will cause cold starts of hello apps in that ASP.</span></span>  <span data-ttu-id="2a7ce-147">這可能會導致要求 toorun 緩時變您的應用程式是冷啟動 hello 新的計算資源。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-147">This can cause requests toorun slowly as your app is cold started on hello new compute resources.</span></span>  <span data-ttu-id="2a7ce-148">hello 冷啟動可以避免使用 hello[熱機功能的應用程式][ AppWarmup] Azure App Service 中。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-148">hello cold start can be avoided by using hello [application warm up capability][AppWarmup] in Azure App Service.</span></span>  <span data-ttu-id="2a7ce-149">hello hello 文章所述的應用程式初始化模組也適用於冷啟動因為 hello 初始化處理程序也會叫用應用程式時冷啟動新的計算資源。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-149">hello Application Initialization module described in hello article also works for cold starts because hello initialization process is also invoked when apps are cold started on new compute resources.</span></span> 
> 
> 

## <a name="getting-started"></a><span data-ttu-id="2a7ce-150">開始使用</span><span class="sxs-lookup"><span data-stu-id="2a7ce-150">Getting started</span></span>
<span data-ttu-id="2a7ce-151">tooget 開始使用應用程式服務環境中，請參閱[如何 tooCreate App Service 環境][HowtoCreateASE]</span><span class="sxs-lookup"><span data-stu-id="2a7ce-151">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowtoCreateASE]</span></span>

<span data-ttu-id="2a7ce-152">如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="2a7ce-152">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
