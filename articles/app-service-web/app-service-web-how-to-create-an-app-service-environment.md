---
title: "aaaHow tooCreate App Service 環境 v1"
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
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a><span data-ttu-id="4e36c-103">如何 tooCreate App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="4e36c-103">How tooCreate an App Service Environment v1</span></span> 

> [!NOTE]
> <span data-ttu-id="4e36c-104">這篇文章是關於 hello App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="4e36c-104">This article is about hello App Service Environment v1.</span></span> <span data-ttu-id="4e36c-105">沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。</span><span class="sxs-lookup"><span data-stu-id="4e36c-105">There is a newer version of hello App Service Environment that is easier toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="4e36c-106">有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。</span><span class="sxs-lookup"><span data-stu-id="4e36c-106">toolearn more about hello new version start with hello [Introduction toohello App Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

### <a name="overview"></a><span data-ttu-id="4e36c-107">概觀</span><span class="sxs-lookup"><span data-stu-id="4e36c-107">Overview</span></span>
<span data-ttu-id="4e36c-108">hello 應用程式服務環境 (ASE) 是 Azure 應用程式服務，可提供 hello 多租用戶戳記中不提供增強的組態功能的高階服務選項。</span><span class="sxs-lookup"><span data-stu-id="4e36c-108">hello App Service Environment (ASE) is a Premium service option of Azure App Service that delivers an enhanced configuration capability that is not available in hello multi-tenant stamps.</span></span> <span data-ttu-id="4e36c-109">hello ASE 功能基本上會將部署 hello Azure 應用程式服務，在客戶的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4e36c-109">hello ASE feature essentially deploys hello Azure App Service into a customer’s virtual network.</span></span> <span data-ttu-id="4e36c-110">應用程式服務環境的 hello 功能更深入瞭解提供的 toogain 讀取 hello[何謂 App Service 環境][ WhatisASE]文件。</span><span class="sxs-lookup"><span data-stu-id="4e36c-110">toogain a greater understanding of hello capabilities offered by App Service Environments read hello [What is an App Service Environment][WhatisASE] documentation.</span></span>

### <a name="before-you-create-your-ase"></a><span data-ttu-id="4e36c-111">建立 ASE 之前</span><span class="sxs-lookup"><span data-stu-id="4e36c-111">Before you create your ASE</span></span>
<span data-ttu-id="4e36c-112">重要 toobe 留意 hello 項目，您無法變更它。</span><span class="sxs-lookup"><span data-stu-id="4e36c-112">It is important toobe aware of hello things you cannot change.</span></span> <span data-ttu-id="4e36c-113">建立後，您無法變更 ASE 的相關層面是：</span><span class="sxs-lookup"><span data-stu-id="4e36c-113">Those aspects you cannot change about your ASE after it is created are:</span></span>

* <span data-ttu-id="4e36c-114">位置</span><span class="sxs-lookup"><span data-stu-id="4e36c-114">Location</span></span>
* <span data-ttu-id="4e36c-115">訂閱</span><span class="sxs-lookup"><span data-stu-id="4e36c-115">Subscription</span></span>
* <span data-ttu-id="4e36c-116">資源群組</span><span class="sxs-lookup"><span data-stu-id="4e36c-116">Resource Group</span></span>
* <span data-ttu-id="4e36c-117">使用的 VNet</span><span class="sxs-lookup"><span data-stu-id="4e36c-117">VNet used</span></span>
* <span data-ttu-id="4e36c-118">使用的子網路</span><span class="sxs-lookup"><span data-stu-id="4e36c-118">Subnet used</span></span> 
* <span data-ttu-id="4e36c-119">子網路大小</span><span class="sxs-lookup"><span data-stu-id="4e36c-119">Subnet size</span></span>

<span data-ttu-id="4e36c-120">當挑選 VNet，然後指定子網路，請確定它是夠大 tooaccomodate 任何未來的成長。</span><span class="sxs-lookup"><span data-stu-id="4e36c-120">When picking a VNet and specifying a subnet, make sure it is large enough tooaccomodate any future growth.</span></span> 

### <a name="creating-an-app-service-environment-v1"></a><span data-ttu-id="4e36c-121">建立 App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="4e36c-121">Creating an App Service Environment v1</span></span>
<span data-ttu-id="4e36c-122">toocreate 需要 toosearch App Service 環境 v1 hello Azure Marketplace 中的***App Service 環境 v1***，或透過 新增-> Web + 行動裝置版-> App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="4e36c-122">toocreate an App Service Environment v1 you need toosearch hello Azure Marketplace for ***App Service Environment v1***, or by going through New -> Web + Mobile -> App Service Environment.</span></span> <span data-ttu-id="4e36c-123">toocreate ASEv1:</span><span class="sxs-lookup"><span data-stu-id="4e36c-123">toocreate an ASEv1:</span></span>

1. <span data-ttu-id="4e36c-124">提供您 ASE hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="4e36c-124">Provide hello name of your ASE.</span></span> <span data-ttu-id="4e36c-125">指定的 hello ASE hello 名稱將用於 hello hello ASE 中建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e36c-125">hello name that is specified for hello ASE will be used for hello apps created in hello ASE.</span></span> <span data-ttu-id="4e36c-126">如果名稱 hello ASE 是 appsvcenvdemo hello 子網域名稱就是。*appsvcenvdemo.p.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="4e36c-126">If name of hello ASE is appsvcenvdemo then hello subdomain name would be .*appsvcenvdemo.p.azurewebsites.net*.</span></span> <span data-ttu-id="4e36c-127">如果您因此建立名為 *mytestapp* 的應用程式，則可定址於 *mytestapp.appsvcenvdemo.p.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="4e36c-127">If you thus created an app named *mytestapp* then it would be addressable at *mytestapp.appsvcenvdemo.p.azurewebsites.net*.</span></span> <span data-ttu-id="4e36c-128">您無法在您 ASE hello 名稱中使用空白字元。</span><span class="sxs-lookup"><span data-stu-id="4e36c-128">You cannot use white space in hello name of your ASE.</span></span> <span data-ttu-id="4e36c-129">如果您在 hello 名稱中使用大寫字元，hello 網域名稱會 hello 總小寫的版本名稱。</span><span class="sxs-lookup"><span data-stu-id="4e36c-129">If you use upper case characters in hello name, hello domain name will be hello total lowercase version of that name.</span></span> <span data-ttu-id="4e36c-130">如果您使用 ILB，則 ASE 名稱不會用於您的子網域中，但是會在 ASE 建立期間明確指定</span><span class="sxs-lookup"><span data-stu-id="4e36c-130">If you use an ILB then your ASE name is not used in your subdomain but is instead explicitly stated during ASE creation</span></span>
   
    ![][1]
2. <span data-ttu-id="4e36c-131">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e36c-131">Select your subscription.</span></span> <span data-ttu-id="4e36c-132">用您 ASE hello 訂用帳戶也是 hello 其中一個會使用建立該 ASE 中的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e36c-132">hello subscription used for your ASE is also hello one that all apps in that ASE will be created with.</span></span> <span data-ttu-id="4e36c-133">您無法將 ASE 放在另一個訂用帳戶中的 VNet</span><span class="sxs-lookup"><span data-stu-id="4e36c-133">You cannot place your ASE in a VNet that is in another subscription</span></span>
3. <span data-ttu-id="4e36c-134">選取或指定新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4e36c-134">Select or specify a new resource group.</span></span> <span data-ttu-id="4e36c-135">用於您 ASE hello 資源群組必須 hello 用於 VNet 的相同。</span><span class="sxs-lookup"><span data-stu-id="4e36c-135">hello resource group used for your ASE must be hello same that is used for your VNet.</span></span> <span data-ttu-id="4e36c-136">如果您選取預先存在的 VNet，然後針對您 ASE hello 資源群組的選擇將會更新的 tooreflect 的 VNet。</span><span class="sxs-lookup"><span data-stu-id="4e36c-136">If you select a pre-existing VNet then hello resource group selection for your ASE will be updated tooreflect that of your VNet.</span></span>
   
    ![][2]
4. <span data-ttu-id="4e36c-137">請選取您的虛擬網路及位置選項。</span><span class="sxs-lookup"><span data-stu-id="4e36c-137">Make your Virtual Network and Location selections.</span></span> <span data-ttu-id="4e36c-138">您可以選擇 toocreate 新的 VNet，或選取現有的 VNet。</span><span class="sxs-lookup"><span data-stu-id="4e36c-138">You can choose toocreate a new VNet or select a pre-existing VNet.</span></span> <span data-ttu-id="4e36c-139">如果您選取新的 VNet，則可以指定名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="4e36c-139">If you select a new VNet then you can specify a name and location.</span></span> <span data-ttu-id="4e36c-140">hello 新的 VNet 必須 hello 位址範圍 192.168.250.0/23 和名為的子網路**預設**，定義為 192.168.250.0/24。</span><span class="sxs-lookup"><span data-stu-id="4e36c-140">hello new VNet will have hello address range 192.168.250.0/23 and a subnet named **default** that is defined as 192.168.250.0/24.</span></span> <span data-ttu-id="4e36c-141">您也可以僅選取既有的傳統或 Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="4e36c-141">You can also simply select a pre-existing Classic or Resource Manager VNet.</span></span> <span data-ttu-id="4e36c-142">hello VIP 類型選取項目可讓您判斷是否可以從 hello 直接存取您 ASE 網際網路 （外部），或者如果它會使用內部負載平衡 (ILB)。</span><span class="sxs-lookup"><span data-stu-id="4e36c-142">hello VIP Type selection determines if your ASE can be directly accessed from hello internet (External) or if it uses an Internal Load Balancer (ILB).</span></span> <span data-ttu-id="4e36c-143">詳細資訊，請閱讀 toolearn [App Service 環境中使用內部負載平衡器][ILBASE]。</span><span class="sxs-lookup"><span data-stu-id="4e36c-143">toolearn more about them read [Using an Internal Load Balancer with an App Service Environment][ILBASE].</span></span> <span data-ttu-id="4e36c-144">如果您選取的外部 VIP 類型可以選取多少外部 IP 位址 hello 系統會透過 IPSSL 用途。</span><span class="sxs-lookup"><span data-stu-id="4e36c-144">If you select a VIP type of External then you can select how many external IP addresses hello system is created with for IPSSL purposes.</span></span> <span data-ttu-id="4e36c-145">如果您選擇 [內部] 您需要將會使用您 ASE toospecify hello 子網域。</span><span class="sxs-lookup"><span data-stu-id="4e36c-145">If you select Internal then you need toospecify hello subdomain that your ASE will use.</span></span> <span data-ttu-id="4e36c-146">ASE 可以部署到使用公用位址範圍*或* RFC1918 位址空間 (也就是私人位址) 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4e36c-146">ASEs can be deployed into virtual networks that use *either* public address ranges, *or* RFC1918 address spaces (i.e. private addresses).</span></span> <span data-ttu-id="4e36c-147">在順序 toouse 具有公用位址範圍的虛擬網路，您必須事先 toocreate hello VNet。</span><span class="sxs-lookup"><span data-stu-id="4e36c-147">In order toouse a virtual network with a public address range, you will need toocreate hello VNet ahead of time.</span></span> <span data-ttu-id="4e36c-148">當您選取預先存在的 VNet 時您 ASE 建立期間需要 toocreate 新的子網路。</span><span class="sxs-lookup"><span data-stu-id="4e36c-148">When you select a pre-existing VNet you will need toocreate a new subnet during ASE creation.</span></span> <span data-ttu-id="4e36c-149">**您無法在 hello 入口網站中使用的預先建立的子網路。如果您使用 Resource Manager 範本建立 ASE，則可以使用既有的子網路建立 ASE。**</span><span class="sxs-lookup"><span data-stu-id="4e36c-149">**You cannot use a pre-created subnet in hello portal. You can create an ASE with a pre-existing subnet if you create your ASE using a resource manager template.**</span></span> <span data-ttu-id="4e36c-150">從範本 toocreate ase 中的，請使用 hello 資訊，[從範本建立 App Service 環境][ ILBAseTemplate]並在這裡， [範本，建立ILBAppService環境][ASEfromTemplate].</span><span class="sxs-lookup"><span data-stu-id="4e36c-150">toocreate an ASE from a template use hello information here, [Creating an App Service Environment from template][ILBAseTemplate] and here, [Creating an ILB App Service Environment from template][ASEfromTemplate].</span></span>

### <a name="details"></a><span data-ttu-id="4e36c-151">詳細資料</span><span class="sxs-lookup"><span data-stu-id="4e36c-151">Details</span></span>
<span data-ttu-id="4e36c-152">一個 ASE 是使用 2 個前端和 2 個背景工作角色建立。</span><span class="sxs-lookup"><span data-stu-id="4e36c-152">An ASE is created with 2 Front Ends and 2 Workers.</span></span> <span data-ttu-id="4e36c-153">hello 前端做為 hello HTTP/HTTPS 端點，並且將流量傳送 toohello 工作者都是 hello 角色裝載您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e36c-153">hello Front Ends act as hello HTTP/HTTPS endpoints and send traffic toohello Workers which are hello roles that host your apps.</span></span> <span data-ttu-id="4e36c-154">您可以調整 hello 數量 ASE 建立之後，且可以甚至是設定這些資源集區上的自動調整規模規則。</span><span class="sxs-lookup"><span data-stu-id="4e36c-154">You can adjust hello quantity after ASE creation and can even set up autoscale rules on these resource pools.</span></span> <span data-ttu-id="4e36c-155">如需詳細資訊，手動調整，App Service 環境的管理和監視這裡：[如何 tooconfigure App Service 環境][ASEConfig]</span><span class="sxs-lookup"><span data-stu-id="4e36c-155">For more details around manual scaling, management and monitoring of an App Service Environment go here: [How tooconfigure an App Service Environment][ASEConfig]</span></span> 

<span data-ttu-id="4e36c-156">Hello 一個 ASE 可以存在於 hello hello ASE 所使用的子網路。</span><span class="sxs-lookup"><span data-stu-id="4e36c-156">Only hello one ASE can exist in hello subnet used by hello ASE.</span></span> <span data-ttu-id="4e36c-157">hello 子網路不能用於 hello ASE 以外的任何項目</span><span class="sxs-lookup"><span data-stu-id="4e36c-157">hello subnet cannot be used for anything other than hello ASE</span></span>

### <a name="after-app-service-environment-v1-creation"></a><span data-ttu-id="4e36c-158">在 App Service 環境 v1 建立之後</span><span class="sxs-lookup"><span data-stu-id="4e36c-158">After App Service Environment v1 creation</span></span>
<span data-ttu-id="4e36c-159">建立 ASE 之後，您可以調整：</span><span class="sxs-lookup"><span data-stu-id="4e36c-159">After ASE creation you can adjust:</span></span>

* <span data-ttu-id="4e36c-160">前端的數量 (最小值：2)</span><span class="sxs-lookup"><span data-stu-id="4e36c-160">Quantity of Front Ends (minimum: 2)</span></span>
* <span data-ttu-id="4e36c-161">背景工作的數量 (最小值：2)</span><span class="sxs-lookup"><span data-stu-id="4e36c-161">Quantity of Workers (minimum: 2)</span></span>
* <span data-ttu-id="4e36c-162">IP SSL 可用的 IP 位址數目</span><span class="sxs-lookup"><span data-stu-id="4e36c-162">Quantity of IP addresses available for IP SSL</span></span>
* <span data-ttu-id="4e36c-163">計算 hello 前端 」 或 「 背景工作所使用的資源大小 （前端大小下限是 P2）</span><span class="sxs-lookup"><span data-stu-id="4e36c-163">Compute resource sizes used by hello Front Ends or Workers (Front End minimum size is P2)</span></span>

<span data-ttu-id="4e36c-164">有手動縮放比例、 管理和監視的應用程式服務環境這裡周圍的更多詳細資料：[如何 tooconfigure App Service 環境][ASEConfig]</span><span class="sxs-lookup"><span data-stu-id="4e36c-164">There are more details around manual scaling, management and monitoring of App Service Environments here: [How tooconfigure an App Service Environment][ASEConfig]</span></span> 

<span data-ttu-id="4e36c-165">如需自動調整資訊沒有的指南：[如何 tooconfigure 自動調整規模的 App Service 環境][ASEAutoscale]</span><span class="sxs-lookup"><span data-stu-id="4e36c-165">For information on autoscaling there is a guide here: [How tooconfigure autoscale for an App Service Environment][ASEAutoscale]</span></span>

<span data-ttu-id="4e36c-166">有沒有可用的自訂，例如 hello 資料庫和儲存體的其他相依性。</span><span class="sxs-lookup"><span data-stu-id="4e36c-166">There are additional dependencies that are not available for customization such as hello database and storage.</span></span> <span data-ttu-id="4e36c-167">這些是由 Azure 處理，而且隨附 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="4e36c-167">These are handled by Azure and come with hello system.</span></span> <span data-ttu-id="4e36c-168">向上 too500 GB hello 系統儲存體支援 hello 整個 App Service 環境並在 hello 資料庫會調整 azure hello 小數位數 hello 系統所需。</span><span class="sxs-lookup"><span data-stu-id="4e36c-168">hello system storage supports up too500 GB for hello entire App Service Environment and hello database is adjusted by Azure as needed by hello scale of hello system.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4e36c-169">開始使用</span><span class="sxs-lookup"><span data-stu-id="4e36c-169">Getting started</span></span>
<span data-ttu-id="4e36c-170">所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="4e36c-170">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="4e36c-171">請參閱 < 開始使用 App Service 環境 v1 tooget[簡介 toohello App Service 環境 v1][WhatisASE]</span><span class="sxs-lookup"><span data-stu-id="4e36c-171">tooget started with App Service Environment v1, see [Introduction toohello App Service Environment v1][WhatisASE]</span></span>

<span data-ttu-id="4e36c-172">如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="4e36c-172">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
