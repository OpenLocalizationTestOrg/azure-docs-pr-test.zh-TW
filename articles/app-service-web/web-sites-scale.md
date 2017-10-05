---
title: "在 Azure 中相應增加應用程式的規模 | Microsoft Docs"
description: "了解如何在 Azure App Service 中相應增加應用程式的規模，以增加容量和功能。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="c05f0-103">在 Azure 中相應增加應用程式的規模</span><span class="sxs-lookup"><span data-stu-id="c05f0-103">Scale up an app in Azure</span></span>
<span data-ttu-id="c05f0-104">本文將說明如何在 Azure App Service 中相應增加應用程式的規模。</span><span class="sxs-lookup"><span data-stu-id="c05f0-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="c05f0-105">有兩個工作流程適合用來相應增加和相應放大規模，而本文說明相應增加工作流程。</span><span class="sxs-lookup"><span data-stu-id="c05f0-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="c05f0-106">[相應增加](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling)︰取得更多的 CPU、記憶體、磁碟空間和額外的功能，例如專用虛擬機器 (VM)、自訂網域和憑證、預備位置，以及自動調整等等。</span><span class="sxs-lookup"><span data-stu-id="c05f0-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="c05f0-107">您可以藉由變更應用程式所屬的 App Service 方案定價層來相應增加。</span><span class="sxs-lookup"><span data-stu-id="c05f0-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="c05f0-108">[相應放大](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling)︰增加執行您的應用程式的 VM 執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="c05f0-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="c05f0-109">視您的定價層而定，最多可以相應放大至 20 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="c05f0-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="c05f0-110">[進階](../app-service/app-service-app-service-environments-readme.md) 層中的 **App Service 環境** ，可進一步將您的相應放大計數增加到 50 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="c05f0-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="c05f0-111">如需相應放大的詳細資訊，請參閱[手動或自動調整執行個體計數](../monitoring-and-diagnostics/insights-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="c05f0-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="c05f0-112">您可以在該文章中了解如何使用自動調整，也就是根據預先定義的規則與排程，自動調整執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="c05f0-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="c05f0-113">這些調整設定只需幾秒鐘便能套用，且影響範圍遍及 [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)內的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05f0-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="c05f0-114">在此過程中，您不需要變更程式碼或重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05f0-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="c05f0-115">如需各 App Service 方案價格資訊及功能的詳細資訊，請參閱 [App Service 價格詳細資料](https://azure.microsoft.com/pricing/details/web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="c05f0-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="c05f0-116">從 **免費** 層切換 App Service 方案之前，您必須先適當地移除 Azure 訂用帳戶的 [消費限制](https://azure.microsoft.com/pricing/spending-limits/) 。</span><span class="sxs-lookup"><span data-stu-id="c05f0-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="c05f0-117">若要檢視或變更 Microsoft Azure App Service 訂用帳戶的選項，請參閱 [Microsoft Azure 訂訂用帳戶][azuresubscriptions]。</span><span class="sxs-lookup"><span data-stu-id="c05f0-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="c05f0-118">相應增加您的定價層</span><span class="sxs-lookup"><span data-stu-id="c05f0-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="c05f0-119">在瀏覽器中，開啟 [Azure 入口網站][portal]。</span><span class="sxs-lookup"><span data-stu-id="c05f0-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="c05f0-120">在應用程式的刀鋒視窗中，按一下 [所有設定]，然後按一下 [相應增加]。</span><span class="sxs-lookup"><span data-stu-id="c05f0-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![瀏覽以相應增加您的 Azure 應用程式規模。][ChooseWHP]
3. <span data-ttu-id="c05f0-122">選擇您的定價層，然後按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="c05f0-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="c05f0-123">當操作完成時，[通知] 索引標籤會有綠色的「成功」字樣閃爍顯示。</span><span class="sxs-lookup"><span data-stu-id="c05f0-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="c05f0-124">調整相關資源</span><span class="sxs-lookup"><span data-stu-id="c05f0-124">Scale related resources</span></span>
<span data-ttu-id="c05f0-125">如果您的應用程式相依於其他服務 (如 Azure SQL Database 或 Azure 儲存體)，您也可以根據需求相應增加這些服務。</span><span class="sxs-lookup"><span data-stu-id="c05f0-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="c05f0-126">這些資源無法透過 App Service 方案進行調整，且必須分開調整。</span><span class="sxs-lookup"><span data-stu-id="c05f0-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="c05f0-127">在 [基本功能] 中，按一下 [資源群組] 連結。</span><span class="sxs-lookup"><span data-stu-id="c05f0-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![相應增加 Azure 應用程式的相關資源](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="c05f0-129">在 [資源群組] 刀鋒視窗的 [摘要] 組件中，按一下您想要調整的資源。</span><span class="sxs-lookup"><span data-stu-id="c05f0-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="c05f0-130">以下螢幕擷取畫面顯示 SQL Database 資源和 Azure 儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="c05f0-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![瀏覽到資源群組刀鋒視窗以相應增加 Azure 應用程式的規模](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="c05f0-132">針對 SQL Database 資源，按一下 [設定]  >  [定價層] 來調整定價層。</span><span class="sxs-lookup"><span data-stu-id="c05f0-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![相應增加 Azure 應用程式的 SQL Database 後端](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="c05f0-134">您也可以針對 SQL 資料庫執行個體開啟 [異地複寫](../sql-database/sql-database-geo-replication-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="c05f0-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="c05f0-135">針對 Azure 儲存體資源，按一下 [設定]  >  [組態]，以便相應增加您的儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="c05f0-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![相應增加您 Azure 應用程式所使用的 Azure 儲存體帳戶](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="c05f0-137">了解開發人員功能</span><span class="sxs-lookup"><span data-stu-id="c05f0-137">Learn about developer features</span></span>
<span data-ttu-id="c05f0-138">視定價層而定，可使用下列以開發人員為導向的功能：</span><span class="sxs-lookup"><span data-stu-id="c05f0-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="c05f0-139">位元</span><span class="sxs-lookup"><span data-stu-id="c05f0-139">Bitness</span></span>
* <span data-ttu-id="c05f0-140">[基本]、[標準] 及 [進階] 層支援 64 位元和 32 位元的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05f0-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="c05f0-141">[免費] 和 [共用] 方案層僅支援 32 位元的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05f0-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="c05f0-142">偵錯工具支援</span><span class="sxs-lookup"><span data-stu-id="c05f0-142">Debugger support</span></span>
* <span data-ttu-id="c05f0-143">在每個 App Service 方案一個連線的情況下，偵錯工具支援適用於 [免費]、[共用] 及 [基本] 模式。</span><span class="sxs-lookup"><span data-stu-id="c05f0-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="c05f0-144">在每個 App Service 方案有 5 個同時連線的情況下，偵錯工具支援適用於 [標準] 和 [進階] 模式。</span><span class="sxs-lookup"><span data-stu-id="c05f0-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="c05f0-145">了解其他功能</span><span class="sxs-lookup"><span data-stu-id="c05f0-145">Learn about other features</span></span>
* <span data-ttu-id="c05f0-146">如需 App Service 方案其他所有功能的詳細資訊，包括所有使用者 (包括開發人員) 關心的定價和功能，請參閱 [App Service 定價詳細資料](https://azure.microsoft.com/pricing/details/web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="c05f0-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="c05f0-147">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/) ，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c05f0-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c05f0-148">不需要信用卡，無需承諾。</span><span class="sxs-lookup"><span data-stu-id="c05f0-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="c05f0-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c05f0-149">Next steps</span></span>
* <span data-ttu-id="c05f0-150">若要開始使用 Azure，請參閱 [Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="c05f0-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c05f0-151">如需價格、支援及 SLA 的相關資訊，請參閱以下連結：</span><span class="sxs-lookup"><span data-stu-id="c05f0-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="c05f0-152">資料傳輸定價詳細資料</span><span class="sxs-lookup"><span data-stu-id="c05f0-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="c05f0-153">Microsoft Azure 支援方案</span><span class="sxs-lookup"><span data-stu-id="c05f0-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="c05f0-154">服務等級協定</span><span class="sxs-lookup"><span data-stu-id="c05f0-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="c05f0-155">SQL Database 定價詳細資料</span><span class="sxs-lookup"><span data-stu-id="c05f0-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="c05f0-156">[Microsoft Azure 的虛擬機器和雲端服務大小][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="c05f0-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="c05f0-157">App Service 定價詳細資料</span><span class="sxs-lookup"><span data-stu-id="c05f0-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="c05f0-158">App Service 定價詳細資料 - SSL 連線</span><span class="sxs-lookup"><span data-stu-id="c05f0-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="c05f0-159">如需 Azure App Service 最佳作法 (包括建置可調整且具彈性的架構) 的詳細資訊，請參閱 [最佳作法：Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c05f0-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="c05f0-160">如需調整 App Service 應用程式的相關影片，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="c05f0-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="c05f0-161">何時該調整 Azure 網站 - Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="c05f0-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="c05f0-162">自動調整 Azure 網站、CPU 或排程 - Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="c05f0-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="c05f0-163">如何調整 Azure 網站 - Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="c05f0-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
