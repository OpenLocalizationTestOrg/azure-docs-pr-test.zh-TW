---
title: "aaaCreate App Service 環境 v1 中的 web 應用程式"
description: "了解如何 toocreate web 應用程式和 App Service 環境 v1 中的 app service 方案"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a><span data-ttu-id="bc80c-103">在 App Service 環境 v1 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc80c-103">Create a web app in an App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="bc80c-104">這篇文章是關於 hello App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="bc80c-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="bc80c-105">沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。</span><span class="sxs-lookup"><span data-stu-id="bc80c-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="bc80c-106">有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。</span><span class="sxs-lookup"><span data-stu-id="bc80c-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="bc80c-107">概觀</span><span class="sxs-lookup"><span data-stu-id="bc80c-107">Overview</span></span>
<span data-ttu-id="bc80c-108">本教學課程示範如何 toocreate web 應用程式和應用程式服務計劃中[App Service 環境 v1](app-service-app-service-environment-intro.md) (ASE)。</span><span class="sxs-lookup"><span data-stu-id="bc80c-108">This tutorial shows how toocreate web apps and App Service plans in an [App Service Environment v1](app-service-app-service-environment-intro.md) (ASE).</span></span> 

> [!NOTE]
> <span data-ttu-id="bc80c-109">如果您想如何 toolearn toocreate web 應用程式，但不需要 toodo 它在應用程式服務環境中，請參閱[建立.NET web 應用程式](app-service-web-get-started-dotnet.md)或其中一個 hello 相關的其他語言和架構教學課程。</span><span class="sxs-lookup"><span data-stu-id="bc80c-109">If you want toolearn how toocreate a web app but don't need toodo it in an App Service Environment, see [Create a .NET web app](app-service-web-get-started-dotnet.md) or one of hello related tutorials for other languages and frameworks.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bc80c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bc80c-110">Prerequisites</span></span>
<span data-ttu-id="bc80c-111">本教學課程假設您已建立 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="bc80c-111">This tutorial assumes you have created an App Service Environment.</span></span> <span data-ttu-id="bc80c-112">如果尚未建立，請參閱 [建立 App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="bc80c-112">If you haven't done that yet, see [Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span> 

## <a name="create-a-web-app"></a><span data-ttu-id="bc80c-113">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="bc80c-113">Create a web app</span></span>
1. <span data-ttu-id="bc80c-114">在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增 > Web + 行動 > Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bc80c-114">In hello [Azure Portal](https://portal.azure.com/), click **New > Web + Mobile > Web App**.</span></span> 
   
    ![][1]
2. <span data-ttu-id="bc80c-115">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc80c-115">Select your subscription.</span></span>  
   
    <span data-ttu-id="bc80c-116">如果您有多個訂用帳戶請注意該 toocreate App Service 環境中的應用程式中，您需要 toouse hello 建立 hello 環境時所使用的相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc80c-116">If you have multiple subscriptions be aware that toocreate an app in your App Service Environment, you need toouse hello same subscription that you used when creating hello environment.</span></span> 
3. <span data-ttu-id="bc80c-117">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="bc80c-117">Select or create a resource group.</span></span>
   
    <span data-ttu-id="bc80c-118">*資源群組*您 toomanage 做為一個單位相關的 Azure 資源，有助於建立時啟用*角色型存取控制*(RBAC) 規則，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc80c-118">*Resource groups* enable you toomanage related Azure resources as a unit and are useful when establishing *role-based access control* (RBAC) rules for your apps.</span></span> <span data-ttu-id="bc80c-119">如需詳細資訊，請參閱 [Azure Resource Manager概觀][ResourceGroups]。</span><span class="sxs-lookup"><span data-stu-id="bc80c-119">For more information, see [Azure Resource Manager overview][ResourceGroups].</span></span> 
4. <span data-ttu-id="bc80c-120">選取或建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="bc80c-120">Select or create an App Service plan.</span></span>
   
    <span data-ttu-id="bc80c-121"> 是受管理的 Web 應用程式集。</span><span class="sxs-lookup"><span data-stu-id="bc80c-121">*App Service plans* are managed sets of web apps.</span></span>  <span data-ttu-id="bc80c-122">通常當您選取定價，hello 價格收費是套用的 toohello 應用程式服務方案而不是 toohello 個別的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc80c-122">Normally when you select pricing, hello price charged is applied toohello App Service plan rather than toohello individual apps.</span></span> <span data-ttu-id="bc80c-123">在 ase 中，您需支付 hello 計算執行個體配置 toohello ASE 而不是已列出您 asp。</span><span class="sxs-lookup"><span data-stu-id="bc80c-123">In an ASE you pay for hello compute instances allocated toohello ASE rather than what you have listed with your ASP.</span></span>  <span data-ttu-id="bc80c-124">您的應用程式服務方案的 hello 執行個體向上延展 tooscale hello 數字的 web 應用程式的執行個體而且會影響所有 hello web 應用程式在該計劃中。</span><span class="sxs-lookup"><span data-stu-id="bc80c-124">tooscale up hello number of instances of a web app you scale up hello instances of your App Service plan and it affects all of hello web apps in that plan.</span></span>  <span data-ttu-id="bc80c-125">某些功能，例如網站位置或 VNET 整合也有 hello 計劃中的數量限制。</span><span class="sxs-lookup"><span data-stu-id="bc80c-125">Some features such as site slots or VNET Integration also have quantity restrictions within hello plan.</span></span>  <span data-ttu-id="bc80c-126">如需詳細資訊，請參閱 [Azure App Service 方案概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bc80c-126">For more information, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>
   
    <span data-ttu-id="bc80c-127">您可以查看 hello 位置記下 hello 計劃名稱，您 ASE 中識別應用程式服務計劃的 hello。</span><span class="sxs-lookup"><span data-stu-id="bc80c-127">You can identify hello App Service plans in your ASE by looking at hello location that is noted under hello plan name.</span></span>  
   
    ![][5]
   
    <span data-ttu-id="bc80c-128">如果您想 toouse App Service 方案已存在您的 App Service 環境中，選取該計劃。</span><span class="sxs-lookup"><span data-stu-id="bc80c-128">If you want toouse an App Service plan that already exists in your App Service Environment, select that plan.</span></span> <span data-ttu-id="bc80c-129">如果您想 toocreate 新的 App Service 方案，請參閱 hello 遵循此教學課程中，區段[App Service 環境中建立 App Service 方案](#createplan)。</span><span class="sxs-lookup"><span data-stu-id="bc80c-129">If you want toocreate a new App Service plan, see hello following section of this tutorial, [Create an App Service plan in an App Service Environment](#createplan).</span></span>
5. <span data-ttu-id="bc80c-130">輸入 hello web 應用程式的名稱，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="bc80c-130">Enter hello name for your web app, and then click **Create**.</span></span> 
   
    <span data-ttu-id="bc80c-131">如果您 ASE 在 ase 中使用外部 VIP hello 應用程式的 URL 是: [*sitename*]。 [*的 App Service 環境名稱*]。 p.azurewebsites.net 而不是 [*sitename*]。 名稱是.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="bc80c-131">If your ASE uses an External VIP hello URL of an app in an ASE is:  [*sitename*].[*name of your App Service Environment*].p.azurewebsites.net  instead of  [*sitename*].azurewebsites.net</span></span>
   
    <span data-ttu-id="bc80c-132">如果您 ASE ASE 是，請使用內部 VIP 然後 hello 應用程式的 URL: [*sitename*]。 [*ASE 建立期間所指定的子網域*]</span><span class="sxs-lookup"><span data-stu-id="bc80c-132">If your ASE uses an Internal VIP then hello URL of an app in that ASE is: [*sitename*].[*subdomain specified during ASE creation*]</span></span>   
    <span data-ttu-id="bc80c-133">您可以選取您 ASP ASE 建立期間之後，您會看到更新以下的 hello 子網域**名稱**</span><span class="sxs-lookup"><span data-stu-id="bc80c-133">After you select your ASP during ASE creation you will see hello subdomain update below **Name**</span></span>

## <span data-ttu-id="bc80c-134"><a name="createplan"></a> 建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="bc80c-134"><a name="createplan"></a> Create an App Service plan</span></span>
<span data-ttu-id="bc80c-135">當您在 App Service 環境中建立 App Service 方案時，您的背景工作角色選擇會因為在 ASE 中沒有共用的背景工作角色而有所不同。</span><span class="sxs-lookup"><span data-stu-id="bc80c-135">When you create an App Service plan in an App Service Environment, your worker choices are different as there are no shared workers in an ASE.</span></span>  <span data-ttu-id="bc80c-136">您有 toouse hello 工作者是 hello 的已配置 toohello ASE hello 系統管理員。這表示該 toocreate 新計劃，您在所有您已在該背景工作集區的計劃需要 toohave 多個工作者配置 tooyour ASE 背景工作集區的執行個體的 hello 總數比。</span><span class="sxs-lookup"><span data-stu-id="bc80c-136">hello workers you have toouse are hello ones that have been allocated toohello ASE by hello admin.  This means that toocreate a new plan, you need toohave more workers allocated tooyour ASE worker pool than hello total number of instances across all of your plans already in that worker pool.</span></span>  <span data-ttu-id="bc80c-137">如果您沒有足夠的背景工作中您 ASE 背景工作集區 toocreate 您計劃，您會需要使用它們加入您 ASE admin tooget toowork。</span><span class="sxs-lookup"><span data-stu-id="bc80c-137">If you don't have enough workers in your ASE worker pool toocreate your plan, you need toowork with your ASE admin tooget them added.</span></span>

<span data-ttu-id="bc80c-138">App Service 環境所裝載的應用程式服務計劃與另一項差異是 hello 缺乏定價選取項目。</span><span class="sxs-lookup"><span data-stu-id="bc80c-138">Another difference with App Service plans hosted by an App Service Environment is hello lack of pricing selection.</span></span>  <span data-ttu-id="bc80c-139">當您 App Service 環境您支付 hello 系統所使用的計算資源，並且在該環境中沒有加入的費用 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="bc80c-139">When you have an App Service Environment you are paying for compute resources used by hello system and do not have added charges for hello plans in that environment.</span></span>  <span data-ttu-id="bc80c-140">當您建立 App Service 方案時，您通常會選取決定費率的價格方案。</span><span class="sxs-lookup"><span data-stu-id="bc80c-140">Normally when you create an App Service plan you select a pricing plan which determines your billing.</span></span>  <span data-ttu-id="bc80c-141">App Service 環境基本上是您可以在其中建立內容的私人位置。</span><span class="sxs-lookup"><span data-stu-id="bc80c-141">An App Service Environment is essentially a private location where you can create content.</span></span>  <span data-ttu-id="bc80c-142">您需支付 hello 環境與不 toohost 您的內容。</span><span class="sxs-lookup"><span data-stu-id="bc80c-142">You pay for hello environment and not toohost your content.</span></span>

<span data-ttu-id="bc80c-143">hello 下列指示說明 toocreate 應用程式服務計劃建立 hello hello 教學課程的上一節中所述的 web 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="bc80c-143">hello following instructions show how toocreate an App Service plan while you are creating a web app as explained in hello previous section of hello tutorial.</span></span>

1. <span data-ttu-id="bc80c-144">按一下**新建**在 hello 計劃選擇 UI，並提供您計劃的名稱，就像平常一樣 ASE 之外。</span><span class="sxs-lookup"><span data-stu-id="bc80c-144">Click **Create New** in hello plan selection UI and provide a name for your plan just as you normally would outside of an ASE.</span></span>
2. <span data-ttu-id="bc80c-145">選取您想 toouse，從您位置選擇器的 hello ASE。</span><span class="sxs-lookup"><span data-stu-id="bc80c-145">Select hello ASE that you want toouse from your location picker.</span></span>
   
    <span data-ttu-id="bc80c-146">因為 App Service 環境基本上是專用部署位置，所以它會顯示在 [位置] 下。</span><span class="sxs-lookup"><span data-stu-id="bc80c-146">Because an App Service Environment is essentially a private deployment location, it shows under Location.</span></span> 
   
    ![][2]
   
    <span data-ttu-id="bc80c-147">在選擇器中的位置 hello ase 中的選取範圍之後, hello 應用程式服務計劃建立 UI 更新。</span><span class="sxs-lookup"><span data-stu-id="bc80c-147">After selection of an ASE in hello location picker, hello App Service plan creation UI updates.</span></span>  <span data-ttu-id="bc80c-148">hello 位置現在會顯示 hello hello ASE 系統名稱與 hello 區域，而且要更換 hello 定價計劃選擇器使用背景工作集區選取器。</span><span class="sxs-lookup"><span data-stu-id="bc80c-148">hello location now shows hello name of hello ASE system and hello region it is in, and hello pricing plan picker is replaced with a worker pool picker.</span></span>  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a><span data-ttu-id="bc80c-149">選取背景工作集區</span><span class="sxs-lookup"><span data-stu-id="bc80c-149">Selecting a worker pool</span></span>
<span data-ttu-id="bc80c-150">通常 Azure App Service 中和外部 App Service 環境中，有 3 hello 選取範圍的固定的價格計劃中的可用的運算大小。</span><span class="sxs-lookup"><span data-stu-id="bc80c-150">Normally in Azure App Service and outside of an App Service Environment, there are 3 compute sizes that are available with hello selection of a dedicated price plan.</span></span>  <span data-ttu-id="bc80c-151">以類似的方式，為 ase 中可以定義總 too3 集區的背景工作，並且指定 hello 運算大小所使用的背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="bc80c-151">In a similar fashion, for an ASE you can define up too3 pools of workers and specify hello compute size that is used for that worker pool.</span></span>  <span data-ttu-id="bc80c-152">這表示租用戶的 hello ASE 是而不需要選取與您的應用程式服務方案的運算大小的定價方案，您要選取的名為*背景工作集區*。</span><span class="sxs-lookup"><span data-stu-id="bc80c-152">What that means for tenants of hello ASE is that instead of selecting a pricing plan with compute size for your App Service plan, you select what is called a *worker pool*.</span></span>  

<span data-ttu-id="bc80c-153">hello 背景工作集區選取 UI 會顯示 hello 運算大小 hello 名稱下方的背景工作集區使用。</span><span class="sxs-lookup"><span data-stu-id="bc80c-153">hello worker pool selection UI shows hello compute size used for that worker pool below hello name.</span></span>  <span data-ttu-id="bc80c-154">hello 可用數量是指 toohow 許多計算執行個體可供該集區中使用。</span><span class="sxs-lookup"><span data-stu-id="bc80c-154">hello quantity available refers toohow many compute instances are available for use in that pool.</span></span>  <span data-ttu-id="bc80c-155">hello 總集區實際上可能會有比這個數字的多個執行個體，但此值是指 toosimply 多少未處於使用中。</span><span class="sxs-lookup"><span data-stu-id="bc80c-155">hello total pool may actually have more instances than this number but this value refers toosimply how many are not in use.</span></span>  <span data-ttu-id="bc80c-156">如果您需要 tooadjust App Service 環境 tooadd 更多計算資源，請參閱[設定 App Service 環境](app-service-web-configure-an-app-service-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="bc80c-156">If you need tooadjust your App Service Environment tooadd more compute resources see [Configuring your App Service Environment](app-service-web-configure-an-app-service-environment.md).</span></span>

![][4]

<span data-ttu-id="bc80c-157">在此範例中，您只會看到兩個可用的背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="bc80c-157">In this example you see only two worker pools available.</span></span> <span data-ttu-id="bc80c-158">這是因為 hello ASE 系統管理員只能組成的兩個背景工作集區配置的主機。</span><span class="sxs-lookup"><span data-stu-id="bc80c-158">That is because hello ASE administrator only allocated hosts into those two worker pools.</span></span>  <span data-ttu-id="bc80c-159">hello 第三步會顯示配置到其中的 Vm 時。</span><span class="sxs-lookup"><span data-stu-id="bc80c-159">hello third would show up when there are VMs allocated into it.</span></span>  

## <a name="after-web-app-creation"></a><span data-ttu-id="bc80c-160">建立 Web 應用程式之後</span><span class="sxs-lookup"><span data-stu-id="bc80c-160">After web app creation</span></span>
<span data-ttu-id="bc80c-161">有幾個考量執行 web 應用程式及管理應用程式服務計劃在 ase 中需要 toobe 列入考量。</span><span class="sxs-lookup"><span data-stu-id="bc80c-161">There are a few considerations for running web apps and managing App Service plans in an ASE that need toobe taken into account.</span></span>  

<span data-ttu-id="bc80c-162">如前文所述，hello ASE hello 擁有者會負責 hello hello 系統大小，因此它們也是負責確保足夠的容量 toohost hello 預期應用程式服務方案的。</span><span class="sxs-lookup"><span data-stu-id="bc80c-162">As noted earlier, hello owner of hello ASE is responsible for hello size of hello system and as a result they are also responsible for ensuring that there is sufficient capacity toohost hello desired App Service plans.</span></span> <span data-ttu-id="bc80c-163">如果沒有可用的背景工作，將不會無法 toocreate 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="bc80c-163">If there are no available workers, you will not be able toocreate your App Service plan.</span></span>  <span data-ttu-id="bc80c-164">這也是 true tooscaling 設定您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc80c-164">This is also true tooscaling up your web app.</span></span>  <span data-ttu-id="bc80c-165">如果您需要更多執行個體，則您會有 tooget 您 App Service 環境管理 tooadd 更多背景工作。</span><span class="sxs-lookup"><span data-stu-id="bc80c-165">If you need more instances then you would have tooget your App Service Environment admin tooadd more workers.</span></span>

<span data-ttu-id="bc80c-166">建立您的 web 應用程式和應用程式服務方案之後，它是個不錯的主意 tooscale 它。</span><span class="sxs-lookup"><span data-stu-id="bc80c-166">After creating your web app and App Service plan it is a good idea tooscale it up.</span></span>  <span data-ttu-id="bc80c-167">在 ase 中您一律需要應用程式服務計劃 tooprovide 容錯能力的 toohave 至少 2 個應用程式。</span><span class="sxs-lookup"><span data-stu-id="bc80c-167">In an ASE you always need toohave at least 2 instances of your App Service plan tooprovide fault tolerance for your apps.</span></span>  <span data-ttu-id="bc80c-168">調整應用程式服務計劃在 ase 中是正常透過 hello 應用程式服務方案 UI hello 相同。</span><span class="sxs-lookup"><span data-stu-id="bc80c-168">Scaling an App Service plan in an ASE is hello same as normal through hello App Service plan UI.</span></span>  <span data-ttu-id="bc80c-169">如需有關調整[如何 tooscale App Service 環境中的 web 應用程式](app-service-web-scale-a-web-app-in-an-app-service-environment.md)</span><span class="sxs-lookup"><span data-stu-id="bc80c-169">For more information about scaling, [How tooscale a web app in an App Service Environment](app-service-web-scale-a-web-app-in-an-app-service-environment.md)</span></span>

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
