---
title: "如何建立 App Service 環境 v1"
description: "App Service 環境 v1 的建立流程說明"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 400bcc08650f8a13911c05c8d0d04ddc22327dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-an-app-service-environment-v1"></a><span data-ttu-id="16bb4-103">如何建立 App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="16bb4-103">How to Create an App Service Environment v1</span></span> 

> [!NOTE]
> <span data-ttu-id="16bb4-104">這篇文章是關於 App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="16bb4-104">This article is about the App Service Environment v1.</span></span> <span data-ttu-id="16bb4-105">有較新版本的 App Service 環境，更易於使用，並且可以在功能更強大的基礎結構上執行。</span><span class="sxs-lookup"><span data-stu-id="16bb4-105">There is a newer version of the App Service Environment that is easier to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="16bb4-106">若要深入了解新版本，請從 [App Service 環境簡介](../app-service/app-service-environment/intro.md)開始。</span><span class="sxs-lookup"><span data-stu-id="16bb4-106">To learn more about the new version start with the [Introduction to the App Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

### <a name="overview"></a><span data-ttu-id="16bb4-107">概觀</span><span class="sxs-lookup"><span data-stu-id="16bb4-107">Overview</span></span>
<span data-ttu-id="16bb4-108">App Service 環境 (ASE) 是 Azure App Service 的進階服務選項，可提供多租用戶戳記中不提供的增強式設定功能。</span><span class="sxs-lookup"><span data-stu-id="16bb4-108">The App Service Environment (ASE) is a Premium service option of Azure App Service that delivers an enhanced configuration capability that is not available in the multi-tenant stamps.</span></span> <span data-ttu-id="16bb4-109">ASE 功能基本上會將 Azure App Service 部署到客戶的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="16bb4-109">The ASE feature essentially deploys the Azure App Service into a customer’s virtual network.</span></span> <span data-ttu-id="16bb4-110">若要更深入了解 App Service Environment 所提供的功能，請閱讀[什麼是 App Service Environment][WhatisASE] 文件。</span><span class="sxs-lookup"><span data-stu-id="16bb4-110">To gain a greater understanding of the capabilities offered by App Service Environments read the [What is an App Service Environment][WhatisASE] documentation.</span></span>

### <a name="before-you-create-your-ase"></a><span data-ttu-id="16bb4-111">建立 ASE 之前</span><span class="sxs-lookup"><span data-stu-id="16bb4-111">Before you create your ASE</span></span>
<span data-ttu-id="16bb4-112">務必注意您無法變更的項目。</span><span class="sxs-lookup"><span data-stu-id="16bb4-112">It is important to be aware of the things you cannot change.</span></span> <span data-ttu-id="16bb4-113">建立後，您無法變更 ASE 的相關層面是：</span><span class="sxs-lookup"><span data-stu-id="16bb4-113">Those aspects you cannot change about your ASE after it is created are:</span></span>

* <span data-ttu-id="16bb4-114">位置</span><span class="sxs-lookup"><span data-stu-id="16bb4-114">Location</span></span>
* <span data-ttu-id="16bb4-115">訂閱</span><span class="sxs-lookup"><span data-stu-id="16bb4-115">Subscription</span></span>
* <span data-ttu-id="16bb4-116">資源群組</span><span class="sxs-lookup"><span data-stu-id="16bb4-116">Resource Group</span></span>
* <span data-ttu-id="16bb4-117">使用的 VNet</span><span class="sxs-lookup"><span data-stu-id="16bb4-117">VNet used</span></span>
* <span data-ttu-id="16bb4-118">使用的子網路</span><span class="sxs-lookup"><span data-stu-id="16bb4-118">Subnet used</span></span> 
* <span data-ttu-id="16bb4-119">子網路大小</span><span class="sxs-lookup"><span data-stu-id="16bb4-119">Subnet size</span></span>

<span data-ttu-id="16bb4-120">挑選 VNet 然後指定子網路時，請確定它足夠大以容納未來的成長。</span><span class="sxs-lookup"><span data-stu-id="16bb4-120">When picking a VNet and specifying a subnet, make sure it is large enough to accomodate any future growth.</span></span> 

### <a name="creating-an-app-service-environment-v1"></a><span data-ttu-id="16bb4-121">建立 App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="16bb4-121">Creating an App Service Environment v1</span></span>
<span data-ttu-id="16bb4-122">若要建立 App Service 環境 v1，您必須在 Azure Marketplace 中搜尋 App Service Environment v1，或經由 [新增] -> [Web + 行動] -> [App Service 環境]，來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="16bb4-122">To create an App Service Environment v1 you need to search the Azure Marketplace for ***App Service Environment v1***, or by going through New -> Web + Mobile -> App Service Environment.</span></span> <span data-ttu-id="16bb4-123">若要建立 ASEv1：</span><span class="sxs-lookup"><span data-stu-id="16bb4-123">To create an ASEv1:</span></span>

1. <span data-ttu-id="16bb4-124">提供 ASE 的名稱。</span><span class="sxs-lookup"><span data-stu-id="16bb4-124">Provide the name of your ASE.</span></span> <span data-ttu-id="16bb4-125">針對 ASE 指定的名稱將用於在 ASE 中建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="16bb4-125">The name that is specified for the ASE will be used for the apps created in the ASE.</span></span> <span data-ttu-id="16bb4-126">如果 ASE 的名稱是 appsvcenvdemo，則子網域名稱會是 .appsvcenvdemo.p.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="16bb4-126">If name of the ASE is appsvcenvdemo then the subdomain name would be .*appsvcenvdemo.p.azurewebsites.net*.</span></span> <span data-ttu-id="16bb4-127">如果您因此建立名為 *mytestapp* 的應用程式，則可定址於 *mytestapp.appsvcenvdemo.p.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="16bb4-127">If you thus created an app named *mytestapp* then it would be addressable at *mytestapp.appsvcenvdemo.p.azurewebsites.net*.</span></span> <span data-ttu-id="16bb4-128">您無法在 ASE 的名稱中使用空白字元。</span><span class="sxs-lookup"><span data-stu-id="16bb4-128">You cannot use white space in the name of your ASE.</span></span> <span data-ttu-id="16bb4-129">如果您在名稱中使用大寫字元，則網域名稱會是該名稱的全小寫版本。</span><span class="sxs-lookup"><span data-stu-id="16bb4-129">If you use upper case characters in the name, the domain name will be the total lowercase version of that name.</span></span> <span data-ttu-id="16bb4-130">如果您使用 ILB，則 ASE 名稱不會用於您的子網域中，但是會在 ASE 建立期間明確指定</span><span class="sxs-lookup"><span data-stu-id="16bb4-130">If you use an ILB then your ASE name is not used in your subdomain but is instead explicitly stated during ASE creation</span></span>
   
    ![][1]
2. <span data-ttu-id="16bb4-131">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="16bb4-131">Select your subscription.</span></span> <span data-ttu-id="16bb4-132">用於 ASE 的訂用帳戶也是將用來在該 ASE 中建立所有應用程式的帳戶。</span><span class="sxs-lookup"><span data-stu-id="16bb4-132">The subscription used for your ASE is also the one that all apps in that ASE will be created with.</span></span> <span data-ttu-id="16bb4-133">您無法將 ASE 放在另一個訂用帳戶中的 VNet</span><span class="sxs-lookup"><span data-stu-id="16bb4-133">You cannot place your ASE in a VNet that is in another subscription</span></span>
3. <span data-ttu-id="16bb4-134">選取或指定新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="16bb4-134">Select or specify a new resource group.</span></span> <span data-ttu-id="16bb4-135">用於 ASE 的資源群組必須是與用於您的 VNet 的相同。</span><span class="sxs-lookup"><span data-stu-id="16bb4-135">The resource group used for your ASE must be the same that is used for your VNet.</span></span> <span data-ttu-id="16bb4-136">如果您選取既有的 VNet，則您的 ASE 資源群組選取項目將會更新，以反映 VNet 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="16bb4-136">If you select a pre-existing VNet then the resource group selection for your ASE will be updated to reflect that of your VNet.</span></span>
   
    ![][2]
4. <span data-ttu-id="16bb4-137">請選取您的虛擬網路及位置選項。</span><span class="sxs-lookup"><span data-stu-id="16bb4-137">Make your Virtual Network and Location selections.</span></span> <span data-ttu-id="16bb4-138">您可以選擇建立新的 VNet，或選取既有的 VNet。</span><span class="sxs-lookup"><span data-stu-id="16bb4-138">You can choose to create a new VNet or select a pre-existing VNet.</span></span> <span data-ttu-id="16bb4-139">如果您選取新的 VNet，則可以指定名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="16bb4-139">If you select a new VNet then you can specify a name and location.</span></span> <span data-ttu-id="16bb4-140">新的 VNet 會有位址範圍 192.168.250.0/23，和定義為 192.168.250.0/24 名為 **default** 的子網路。</span><span class="sxs-lookup"><span data-stu-id="16bb4-140">The new VNet will have the address range 192.168.250.0/23 and a subnet named **default** that is defined as 192.168.250.0/24.</span></span> <span data-ttu-id="16bb4-141">您也可以僅選取既有的傳統或 Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="16bb4-141">You can also simply select a pre-existing Classic or Resource Manager VNet.</span></span> <span data-ttu-id="16bb4-142">[VIP 類型] 選項會決定您的 ASE 是否可以從網際網路 (外部) 直接存取，或者它使用內部負載平衡器 (ILB)。</span><span class="sxs-lookup"><span data-stu-id="16bb4-142">The VIP Type selection determines if your ASE can be directly accessed from the internet (External) or if it uses an Internal Load Balancer (ILB).</span></span> <span data-ttu-id="16bb4-143">若要深入了解，請參閱[在 App Service 環境中使用內部負載平衡器][ILBASE]。</span><span class="sxs-lookup"><span data-stu-id="16bb4-143">To learn more about them read [Using an Internal Load Balancer with an App Service Environment][ILBASE].</span></span> <span data-ttu-id="16bb4-144">如果您選取 [外部] VIP 類型，則可以選取系統針對 IPSSL 用途會建立幾個外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="16bb4-144">If you select a VIP type of External then you can select how many external IP addresses the system is created with for IPSSL purposes.</span></span> <span data-ttu-id="16bb4-145">如果您選取 [內部]，則需要指定 ASE 將使用的子網域。</span><span class="sxs-lookup"><span data-stu-id="16bb4-145">If you select Internal then you need to specify the subdomain that your ASE will use.</span></span> <span data-ttu-id="16bb4-146">ASE 可以部署到使用公用位址範圍「或」RFC1918 位址空間 (也就是</span><span class="sxs-lookup"><span data-stu-id="16bb4-146">ASEs can be deployed into virtual networks that use *either* public address ranges, *or* RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="16bb4-147">私人位址) 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="16bb4-147">private addresses).</span></span> <span data-ttu-id="16bb4-148">若要搭配使用虛擬網路與公用位址範圍，您必須事先建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="16bb4-148">In order to use a virtual network with a public address range, you will need to create the VNet ahead of time.</span></span> <span data-ttu-id="16bb4-149">選取既有的 VNet 時，您必須在 ASE 建立期間建立新的子網路。</span><span class="sxs-lookup"><span data-stu-id="16bb4-149">When you select a pre-existing VNet you will need to create a new subnet during ASE creation.</span></span> <span data-ttu-id="16bb4-150">**您無法在入口網站中使用預先建立的子網路。如果您使用 Resource Manager 範本建立 ASE，則可以使用既有的子網路建立 ASE。**</span><span class="sxs-lookup"><span data-stu-id="16bb4-150">**You cannot use a pre-created subnet in the portal. You can create an ASE with a pre-existing subnet if you create your ASE using a resource manager template.**</span></span> <span data-ttu-id="16bb4-151">若要使用此處的資訊透過範本建立 ASE，[從範本建立 App Service 環境][ILBAseTemplate]，以及這裡[從範本建立 ILB App Service 環境][ASEfromTemplate]。</span><span class="sxs-lookup"><span data-stu-id="16bb4-151">To create an ASE from a template use the information here, [Creating an App Service Environment from template][ILBAseTemplate] and here, [Creating an ILB App Service Environment from template][ASEfromTemplate].</span></span>

### <a name="details"></a><span data-ttu-id="16bb4-152">詳細資料</span><span class="sxs-lookup"><span data-stu-id="16bb4-152">Details</span></span>
<span data-ttu-id="16bb4-153">一個 ASE 是使用 2 個前端和 2 個背景工作角色建立。</span><span class="sxs-lookup"><span data-stu-id="16bb4-153">An ASE is created with 2 Front Ends and 2 Workers.</span></span> <span data-ttu-id="16bb4-154">前端可做為 HTTP/HTTPS 端點，將流量傳送到背景工作角色 (也就是裝載您的應用程式的角色)。</span><span class="sxs-lookup"><span data-stu-id="16bb4-154">The Front Ends act as the HTTP/HTTPS endpoints and send traffic to the Workers which are the roles that host your apps.</span></span> <span data-ttu-id="16bb4-155">建立 ASE 之後，您可以調整數量，且甚至可以在這些資源集區上設定自動調整規則。</span><span class="sxs-lookup"><span data-stu-id="16bb4-155">You can adjust the quantity after ASE creation and can even set up autoscale rules on these resource pools.</span></span> <span data-ttu-id="16bb4-156">如需更多關於手動調整、管理及監視 App Service 環境的詳細資料，請前往此處：[如何設定 App Service 環境][ASEConfig]</span><span class="sxs-lookup"><span data-stu-id="16bb4-156">For more details around manual scaling, management and monitoring of an App Service Environment go here: [How to configure an App Service Environment][ASEConfig]</span></span> 

<span data-ttu-id="16bb4-157">只有一個 ASE 可以存在於 ASE 所使用的子網路中。</span><span class="sxs-lookup"><span data-stu-id="16bb4-157">Only the one ASE can exist in the subnet used by the ASE.</span></span> <span data-ttu-id="16bb4-158">子網路無法用於 ASE 以外的任何項目</span><span class="sxs-lookup"><span data-stu-id="16bb4-158">The subnet cannot be used for anything other than the ASE</span></span>

### <a name="after-app-service-environment-v1-creation"></a><span data-ttu-id="16bb4-159">在 App Service 環境 v1 建立之後</span><span class="sxs-lookup"><span data-stu-id="16bb4-159">After App Service Environment v1 creation</span></span>
<span data-ttu-id="16bb4-160">建立 ASE 之後，您可以調整：</span><span class="sxs-lookup"><span data-stu-id="16bb4-160">After ASE creation you can adjust:</span></span>

* <span data-ttu-id="16bb4-161">前端的數量 (最小值：2)</span><span class="sxs-lookup"><span data-stu-id="16bb4-161">Quantity of Front Ends (minimum: 2)</span></span>
* <span data-ttu-id="16bb4-162">背景工作的數量 (最小值：2)</span><span class="sxs-lookup"><span data-stu-id="16bb4-162">Quantity of Workers (minimum: 2)</span></span>
* <span data-ttu-id="16bb4-163">IP SSL 可用的 IP 位址數目</span><span class="sxs-lookup"><span data-stu-id="16bb4-163">Quantity of IP addresses available for IP SSL</span></span>
* <span data-ttu-id="16bb4-164">前端或背景工作所使用的計算資源大小 (前端大小下限為 P2)</span><span class="sxs-lookup"><span data-stu-id="16bb4-164">Compute resource sizes used by the Front Ends or Workers (Front End minimum size is P2)</span></span>

<span data-ttu-id="16bb4-165">以下有更多關於手動調整、管理及監視 App Service 環境的詳細資料：[如何設定 App Service 環境][ASEConfig]</span><span class="sxs-lookup"><span data-stu-id="16bb4-165">There are more details around manual scaling, management and monitoring of App Service Environments here: [How to configure an App Service Environment][ASEConfig]</span></span> 

<span data-ttu-id="16bb4-166">如需自動調整的相關資訊，請參閱：[如何設定 App Service 環境的自動調整][ASEAutoscale]</span><span class="sxs-lookup"><span data-stu-id="16bb4-166">For information on autoscaling there is a guide here: [How to configure autoscale for an App Service Environment][ASEAutoscale]</span></span>

<span data-ttu-id="16bb4-167">有其他無法自訂的相依性，例如資料庫和儲存體。</span><span class="sxs-lookup"><span data-stu-id="16bb4-167">There are additional dependencies that are not available for customization such as the database and storage.</span></span> <span data-ttu-id="16bb4-168">這些都是由 Azure 處理並由系統隨附。</span><span class="sxs-lookup"><span data-stu-id="16bb4-168">These are handled by Azure and come with the system.</span></span> <span data-ttu-id="16bb4-169">系統儲存體對於整個 App Service 環境最多可支援 500 GB，且 Azure 會根據系統規模的需要來調整資料庫。</span><span class="sxs-lookup"><span data-stu-id="16bb4-169">The system storage supports up to 500 GB for the entire App Service Environment and the database is adjusted by Azure as needed by the scale of the system.</span></span>

## <a name="getting-started"></a><span data-ttu-id="16bb4-170">開始使用</span><span class="sxs-lookup"><span data-stu-id="16bb4-170">Getting started</span></span>
<span data-ttu-id="16bb4-171">您可以在 [應用程式服務環境的讀我檔案](../app-service/app-service-app-service-environments-readme.md)中取得 App Service 環境的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="16bb4-171">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="16bb4-172">若要開始使用 App Service 環境 v1，請參閱 [App Service 環境 v1 簡介][WhatisASE]</span><span class="sxs-lookup"><span data-stu-id="16bb4-172">To get started with App Service Environment v1, see [Introduction to the App Service Environment v1][WhatisASE]</span></span>

<span data-ttu-id="16bb4-173">如需有關 Azure App Service 平台的詳細資訊，請參閱 [Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="16bb4-173">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
