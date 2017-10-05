---
title: "在 App Service 環境 v1 中建立 Web 應用程式"
description: "了解如何在 App Service 環境 v1 中建立 Web 應用程式和 App Service 方案"
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
ms.openlocfilehash: 0779486b040b8dc51cdd42521ba965e58388425a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a><span data-ttu-id="4d6b0-103">在 App Service 環境 v1 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d6b0-103">Create a web app in an App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="4d6b0-104">這篇文章是關於 App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="4d6b0-105">有較新版本的 App Service 環境，更易於使用，並且可以在功能更強大的基礎結構上執行。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="4d6b0-106">若要深入了解新版本，請從 [App Service 環境簡介](../app-service/app-service-environment/intro.md)開始。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="4d6b0-107">概觀</span><span class="sxs-lookup"><span data-stu-id="4d6b0-107">Overview</span></span>
<span data-ttu-id="4d6b0-108">本教學課程說明如何在 [App Service 環境 v1](app-service-app-service-environment-intro.md) (ASE) 中建立 Web 應用程式和 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-108">This tutorial shows how to create web apps and App Service plans in an [App Service Environment v1](app-service-app-service-environment-intro.md) (ASE).</span></span> 

> [!NOTE]
> <span data-ttu-id="4d6b0-109">如果您想要了解如何建立 Web 應用程式，但不需要在 App Service 環境中加以實作，請參閱 [建立 .NET Web 應用程式](app-service-web-get-started-dotnet.md) ，或其中一個適用於其他語言和架構的相關教學課程。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-109">If you want to learn how to create a web app but don't need to do it in an App Service Environment, see [Create a .NET web app](app-service-web-get-started-dotnet.md) or one of the related tutorials for other languages and frameworks.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4d6b0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4d6b0-110">Prerequisites</span></span>
<span data-ttu-id="4d6b0-111">本教學課程假設您已建立 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-111">This tutorial assumes you have created an App Service Environment.</span></span> <span data-ttu-id="4d6b0-112">如果尚未建立，請參閱 [建立 App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-112">If you haven't done that yet, see [Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span> 

## <a name="create-a-web-app"></a><span data-ttu-id="4d6b0-113">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d6b0-113">Create a web app</span></span>
1. <span data-ttu-id="4d6b0-114">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [新增] > [Web + 行動] > [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-114">In the [Azure Portal](https://portal.azure.com/), click **New > Web + Mobile > Web App**.</span></span> 
   
    ![][1]
2. <span data-ttu-id="4d6b0-115">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-115">Select your subscription.</span></span>  
   
    <span data-ttu-id="4d6b0-116">如果您有多個訂用帳戶，請注意，若要在您的 App Service 環境中建立應用程式，必須使用您在建立環境時所使用訂用帳戶來建立。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-116">If you have multiple subscriptions be aware that to create an app in your App Service Environment, you need to use the same subscription that you used when creating the environment.</span></span> 
3. <span data-ttu-id="4d6b0-117">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-117">Select or create a resource group.</span></span>
   
    <span data-ttu-id="4d6b0-118">*資源群組*可讓您以單位的形式管理相關的 Azure 資源，並可在您為應用程式建立*角色型存取控制* (RBAC) 規則時發揮效用。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-118">*Resource groups* enable you to manage related Azure resources as a unit and are useful when establishing *role-based access control* (RBAC) rules for your apps.</span></span> <span data-ttu-id="4d6b0-119">如需詳細資訊，請參閱 [Azure Resource Manager概觀][ResourceGroups]。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-119">For more information, see [Azure Resource Manager overview][ResourceGroups].</span></span> 
4. <span data-ttu-id="4d6b0-120">選取或建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-120">Select or create an App Service plan.</span></span>
   
    <span data-ttu-id="4d6b0-121"> 是受管理的 Web 應用程式集。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-121">*App Service plans* are managed sets of web apps.</span></span>  <span data-ttu-id="4d6b0-122">當您選取價格時，支付的價格通常會套用到 App Service 方案，而非個別的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-122">Normally when you select pricing, the price charged is applied to the App Service plan rather than to the individual apps.</span></span> <span data-ttu-id="4d6b0-123">在 ASE 中，您需對配置給 ASE 的計算執行個體付費，而不需對與您的 ASP 一起列出的項目付費。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-123">In an ASE you pay for the compute instances allocated to the ASE rather than what you have listed with your ASP.</span></span>  <span data-ttu-id="4d6b0-124">若要相應增加 Web 應用程式的執行個體數目，您可相應增加 App Service 方案的執行個體，這會影響該方案中的所有 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-124">To scale up the number of instances of a web app you scale up the instances of your App Service plan and it affects all of the web apps in that plan.</span></span>  <span data-ttu-id="4d6b0-125">方案中的某些功能 (例如網站位置或 VNET 整合) 也有數量限制。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-125">Some features such as site slots or VNET Integration also have quantity restrictions within the plan.</span></span>  <span data-ttu-id="4d6b0-126">如需詳細資訊，請參閱 [Azure App Service 方案概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4d6b0-126">For more information, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>
   
    <span data-ttu-id="4d6b0-127">您可以藉由查看方案名稱下加註的位置，來識別 ASE 中的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-127">You can identify the App Service plans in your ASE by looking at the location that is noted under the plan name.</span></span>  
   
    ![][5]
   
    <span data-ttu-id="4d6b0-128">如果您想要使用已存在於 App Service 環境中的 App Service 方案，請選取該方案。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-128">If you want to use an App Service plan that already exists in your App Service Environment, select that plan.</span></span> <span data-ttu-id="4d6b0-129">如果您想要建立新的 App Service 方案，請參閱本教學課程的下一節： [在 App Service 環境中建立 App Service 方案](#createplan)。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-129">If you want to create a new App Service plan, see the following section of this tutorial, [Create an App Service plan in an App Service Environment](#createplan).</span></span>
5. <span data-ttu-id="4d6b0-130">輸入 Web 應用程式的名稱，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-130">Enter the name for your web app, and then click **Create**.</span></span> 
   
    <span data-ttu-id="4d6b0-131">如果 ASE 使用外部 VIP，則 ASE 中應用程式的 URL 為：[*網站名稱*].[*App Service 環境的名稱*].p.azurewebsites.net，而非 [*網站名稱*].azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="4d6b0-131">If your ASE uses an External VIP the URL of an app in an ASE is:  [*sitename*].[*name of your App Service Environment*].p.azurewebsites.net  instead of  [*sitename*].azurewebsites.net</span></span>
   
    <span data-ttu-id="4d6b0-132">如果 ASE 使用內部 VIP，則該 ASE 中應用程式的 URL 為：[*網站名稱*].[*在 ASE 建立期間指定的子網域*]</span><span class="sxs-lookup"><span data-stu-id="4d6b0-132">If your ASE uses an Internal VIP then the URL of an app in that ASE is: [*sitename*].[*subdomain specified during ASE creation*]</span></span>   
    <span data-ttu-id="4d6b0-133">在 ASE 建立期間選取您的 ASP 後，您會在 [名稱] 之下看到子網域更新</span><span class="sxs-lookup"><span data-stu-id="4d6b0-133">After you select your ASP during ASE creation you will see the subdomain update below **Name**</span></span>

## <span data-ttu-id="4d6b0-134"><a name="createplan"></a> 建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="4d6b0-134"><a name="createplan"></a> Create an App Service plan</span></span>
<span data-ttu-id="4d6b0-135">當您在 App Service 環境中建立 App Service 方案時，您的背景工作角色選擇會因為在 ASE 中沒有共用的背景工作角色而有所不同。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-135">When you create an App Service plan in an App Service Environment, your worker choices are different as there are no shared workers in an ASE.</span></span>  <span data-ttu-id="4d6b0-136">您必須使用的背景工作角色也就是由系統管理員配置給 ASE 的背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-136">The workers you have to use are the ones that have been allocated to the ASE by the admin.</span></span>  <span data-ttu-id="4d6b0-137">這代表在建立新的方案時，配置給 ASE 背景工作集區的背景工作角色數目，必須超過該背景工作集區中所有方案的執行個體總數。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-137">This means that to create a new plan, you need to have more workers allocated to your ASE worker pool than the total number of instances across all of your plans already in that worker pool.</span></span>  <span data-ttu-id="4d6b0-138">如果您的 ASE 背景工作集區中沒有足夠的背景工作角色來建立方案，則您需要與 ASE 系統管理員合作來新增背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-138">If you don't have enough workers in your ASE worker pool to create your plan, you need to work with your ASE admin to get them added.</span></span>

<span data-ttu-id="4d6b0-139">而 App Service 環境所裝載的 App Service 方案還有另一項差異，那就是缺少價格選取項目。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-139">Another difference with App Service plans hosted by an App Service Environment is the lack of pricing selection.</span></span>  <span data-ttu-id="4d6b0-140">當您有 App Service 環境時，您會支付系統所使用的計算資源費用，但該環境中的方案不會有附加的費用。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-140">When you have an App Service Environment you are paying for compute resources used by the system and do not have added charges for the plans in that environment.</span></span>  <span data-ttu-id="4d6b0-141">當您建立 App Service 方案時，您通常會選取決定費率的價格方案。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-141">Normally when you create an App Service plan you select a pricing plan which determines your billing.</span></span>  <span data-ttu-id="4d6b0-142">App Service 環境基本上是您可以在其中建立內容的私人位置。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-142">An App Service Environment is essentially a private location where you can create content.</span></span>  <span data-ttu-id="4d6b0-143">您可支付環境費用，而非裝載您的內容。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-143">You pay for the environment and not to host your content.</span></span>

<span data-ttu-id="4d6b0-144">下列指示說明如何在您依照本教學課程的上一節所說明來建立 Web 應用程式時，建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-144">The following instructions show how to create an App Service plan while you are creating a web app as explained in the previous section of the tutorial.</span></span>

1. <span data-ttu-id="4d6b0-145">在方案選取 UI 中按一下 [建立新項目]  ，並提供方案的名稱，就跟您平常在 ASE 以外的地方所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-145">Click **Create New** in the plan selection UI and provide a name for your plan just as you normally would outside of an ASE.</span></span>
2. <span data-ttu-id="4d6b0-146">選取您想要從位置選擇器中使用的 ASE。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-146">Select the ASE that you want to use from your location picker.</span></span>
   
    <span data-ttu-id="4d6b0-147">因為 App Service 環境基本上是專用部署位置，所以它會顯示在 [位置] 下。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-147">Because an App Service Environment is essentially a private deployment location, it shows under Location.</span></span> 
   
    ![][2]
   
    <span data-ttu-id="4d6b0-148">在位置選擇器中選取 ASE 之後，App Service 方案建立 UI 將會更新。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-148">After selection of an ASE in the location picker, the App Service plan creation UI updates.</span></span>  <span data-ttu-id="4d6b0-149">位置現在會顯示 ASE 系統的位置及其所在區域，而背景工作集區選擇器會取代價格方案選擇器。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-149">The location now shows the name of the ASE system and the region it is in, and the pricing plan picker is replaced with a worker pool picker.</span></span>  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a><span data-ttu-id="4d6b0-150">選取背景工作集區</span><span class="sxs-lookup"><span data-stu-id="4d6b0-150">Selecting a worker pool</span></span>
<span data-ttu-id="4d6b0-151">通常在 Azure App Service 中和 App Service 環境以外的地方，專用價格方案通常會有 3 種計算大小可供選擇。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-151">Normally in Azure App Service and outside of an App Service Environment, there are 3 compute sizes that are available with the selection of a dedicated price plan.</span></span>  <span data-ttu-id="4d6b0-152">同樣地，對於 ASE 您最多可以定義 3 個背景工作集區，並指定用於該背景工作集區的計算大小。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-152">In a similar fashion, for an ASE you can define up to 3 pools of workers and specify the compute size that is used for that worker pool.</span></span>  <span data-ttu-id="4d6b0-153">對 ASE 的租用戶來說，這代表租用戶並非根據 App Service 方案的計算大小來選取價格方案，而是選取所謂的「背景工作集區」 。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-153">What that means for tenants of the ASE is that instead of selecting a pricing plan with compute size for your App Service plan, you select what is called a *worker pool*.</span></span>  

<span data-ttu-id="4d6b0-154">背景工作角色集區選取 UI 會在名稱下方顯示該背景工作集區角色使用的運算大小。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-154">The worker pool selection UI shows the compute size used for that worker pool below the name.</span></span>  <span data-ttu-id="4d6b0-155">可用數量是指有多少運算執行個體可使用於該集區。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-155">The quantity available refers to how many compute instances are available for use in that pool.</span></span>  <span data-ttu-id="4d6b0-156">總計集區實際上可能有超過這個數字的執行個體，但這個值只是指未使用的數量。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-156">The total pool may actually have more instances than this number but this value refers to simply how many are not in use.</span></span>  <span data-ttu-id="4d6b0-157">如果您需要調整 App Service 環境以新增更多計算資源，請參閱 [設定 App Service 環境](app-service-web-configure-an-app-service-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-157">If you need to adjust your App Service Environment to add more compute resources see [Configuring your App Service Environment](app-service-web-configure-an-app-service-environment.md).</span></span>

![][4]

<span data-ttu-id="4d6b0-158">在此範例中，您只會看到兩個可用的背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-158">In this example you see only two worker pools available.</span></span> <span data-ttu-id="4d6b0-159">這是因為 ASE 系統管理員只會將主機配置到這兩個背景工作角色集區中。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-159">That is because the ASE administrator only allocated hosts into those two worker pools.</span></span>  <span data-ttu-id="4d6b0-160">第三個集區會在有 VM 配置到其中時出現。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-160">The third would show up when there are VMs allocated into it.</span></span>  

## <a name="after-web-app-creation"></a><span data-ttu-id="4d6b0-161">建立 Web 應用程式之後</span><span class="sxs-lookup"><span data-stu-id="4d6b0-161">After web app creation</span></span>
<span data-ttu-id="4d6b0-162">在 ASE 中執行 Web 應用程式及管理 App Service 方案時，有幾件事需要列入考量。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-162">There are a few considerations for running web apps and managing App Service plans in an ASE that need to be taken into account.</span></span>  

<span data-ttu-id="4d6b0-163">如先前所述，ASE 的擁有者必須負責系統大小，因此他們也必須負責確保有足夠的容量來裝載所需的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-163">As noted earlier, the owner of the ASE is responsible for the size of the system and as a result they are also responsible for ensuring that there is sufficient capacity to host the desired App Service plans.</span></span> <span data-ttu-id="4d6b0-164">如果沒有可用的背景工作角色，您將無法建立您的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-164">If there are no available workers, you will not be able to create your App Service plan.</span></span>  <span data-ttu-id="4d6b0-165">也就無法相應增加您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-165">This is also true to scaling up your web app.</span></span>  <span data-ttu-id="4d6b0-166">如果您需要更多執行個體，您必須讓您的 App Service 環境的系統管理員新增更多的背景工作。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-166">If you need more instances then you would have to get your App Service Environment admin to add more workers.</span></span>

<span data-ttu-id="4d6b0-167">當您建立 Web 應用程式和 App Service 方案之後，最好能夠相應增加該方案的內容。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-167">After creating your web app and App Service plan it is a good idea to scale it up.</span></span>  <span data-ttu-id="4d6b0-168">在 ASE 中，您一定需要至少 2 個 App Service 方案執行個體，才能為您的應用程式提供容錯功能。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-168">In an ASE you always need to have at least 2 instances of your App Service plan to provide fault tolerance for your apps.</span></span>  <span data-ttu-id="4d6b0-169">在 ASE 中調整 App Service 方案的方式，就跟一般透過 App Service 方案 UI 來進行的方式相同。</span><span class="sxs-lookup"><span data-stu-id="4d6b0-169">Scaling an App Service plan in an ASE is the same as normal through the App Service plan UI.</span></span>  <span data-ttu-id="4d6b0-170">如需關於調整的詳細資訊，請參閱 [如何在 App Service 環境中調整 Web 應用程式](app-service-web-scale-a-web-app-in-an-app-service-environment.md)</span><span class="sxs-lookup"><span data-stu-id="4d6b0-170">For more information about scaling, [How to scale a web app in an App Service Environment](app-service-web-scale-a-web-app-in-an-app-service-environment.md)</span></span>

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
