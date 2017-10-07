---
title: "設定應用程式的 Azure 中的 aaaScale |Microsoft 文件"
description: "深入了解如何設定應用程式的 Azure App Service tooadd 容量和功能 中的 tooscale。"
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
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="ae2c8-103">在 Azure 中相應增加應用程式的規模</span><span class="sxs-lookup"><span data-stu-id="ae2c8-103">Scale up an app in Azure</span></span>
<span data-ttu-id="ae2c8-104">本文章將示範如何 tooscale Azure App Service 中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-104">This article shows you how tooscale your app in Azure App Service.</span></span> <span data-ttu-id="ae2c8-105">有了縮放、 小數位數的兩個工作流程，並向外的延展和這篇文章說明 hello 調整工作流程。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-105">There are two workflows for scaling, scale up and scale out, and this article explains hello scale up workflow.</span></span>

* <span data-ttu-id="ae2c8-106">[相應增加](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling)︰取得更多的 CPU、記憶體、磁碟空間和額外的功能，例如專用虛擬機器 (VM)、自訂網域和憑證、預備位置，以及自動調整等等。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="ae2c8-107">向上擴充藉由變更定價層應用程式服務計劃您的應用程式所屬的 hello。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-107">You scale up by changing hello pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="ae2c8-108">[向外延展](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): hello 執行您的應用程式的 VM 執行個體數目增加。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase hello number of VM instances that run your app.</span></span>
  <span data-ttu-id="ae2c8-109">您可以向外延展 tooas 許多與 20 的執行個體，視您的定價層而定。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-109">You can scale out tooas many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="ae2c8-110">[應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)中**Premium**層會進一步增加您的向外延展計數 too50 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count too50 instances.</span></span> <span data-ttu-id="ae2c8-111">如需相應放大的詳細資訊，請參閱[手動或自動調整執行個體計數](../monitoring-and-diagnostics/insights-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="ae2c8-112">您會發現那里 out 方式 toouse 自動調整，也就是 tooscale 執行個體計數會自動根據預先定義的規則和排程。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-112">There you will find out how toouse autoscaling, which is tooscale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="ae2c8-113">hello 小數位數設定採用唯一秒 tooapply 和會影響所有的應用程式在您[App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-113">hello scale settings take only seconds tooapply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="ae2c8-114">它們不需要您 toochange 您的程式碼或重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-114">They do not require you toochange your code or redeploy your application.</span></span>

<span data-ttu-id="ae2c8-115">Hello 價格和功能的個別的應用程式服務方案的相關資訊，請參閱[應用程式服務定價詳細資料](https://azure.microsoft.com/pricing/details/web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-115">For information about hello pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="ae2c8-116">切換 hello 從 App Service 方案之前**免費**層，您必須先移除 hello[消費限制](https://azure.microsoft.com/pricing/spending-limits/)備妥您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-116">Before you switch an App Service plan from hello **Free** tier, you must first remove hello [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="ae2c8-117">Microsoft Azure 應用程式服務訂用帳戶，tooview 或變更選項，請參閱[Microsoft Azure 訂用帳戶][azuresubscriptions]。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-117">tooview or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="ae2c8-118">相應增加您的定價層</span><span class="sxs-lookup"><span data-stu-id="ae2c8-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="ae2c8-119">在瀏覽器中，開啟 hello [Azure 入口網站][portal]。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-119">In your browser, open hello [Azure portal][portal].</span></span>
2. <span data-ttu-id="ae2c8-120">在應用程式的刀鋒視窗中，按一下 所有設定，然後按一下相應增加。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![瀏覽 tooscale 備份您的 Azure 應用程式。][ChooseWHP]
3. <span data-ttu-id="ae2c8-122">選擇您的定價層，然後按一下選取 。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="ae2c8-123">hello**通知** 索引標籤將會閃爍綠色**成功**hello 作業完成之後。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-123">hello **Notifications** tab will flash a green **SUCCESS** after hello operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="ae2c8-124">調整相關資源</span><span class="sxs-lookup"><span data-stu-id="ae2c8-124">Scale related resources</span></span>
<span data-ttu-id="ae2c8-125">如果您的應用程式相依於其他服務 (如 Azure SQL Database 或 Azure 儲存體)，您也可以根據需求相應增加這些服務。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="ae2c8-126">這些資源不會縮放以 hello App Service 方案，因此必須分別擴充。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-126">These resources are not scaled with hello App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="ae2c8-127">在**Essentials**，按一下 hello**資源群組**連結。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-127">In **Essentials**, click hello **Resource group** link.</span></span>
   
    ![相應增加 Azure 應用程式的相關資源](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="ae2c8-129">在 hello**摘要**屬於 hello**資源群組**刀鋒視窗中，按一下您想 tooscale 資源。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-129">In hello **Summary** part of hello **Resource group** blade, click a resource that you want tooscale.</span></span> <span data-ttu-id="ae2c8-130">hello 下列螢幕擷取畫面會顯示 SQL Database 資源和 Azure 儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-130">hello following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![瀏覽 tooresource 群組刀鋒視窗 tooscale 備份您的 Azure 應用程式](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="ae2c8-132">SQL Database 資源，請按一下**設定** > **定價層**tooscale hello 定價層。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-132">For a SQL Database resource, click **Settings** > **Pricing tier** tooscale hello pricing tier.</span></span>
   
    ![向上擴充 hello SQL Database 的後端 Azure 應用程式](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="ae2c8-134">您也可以針對 SQL 資料庫執行個體開啟 [異地複寫](../sql-database/sql-database-geo-replication-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="ae2c8-135">Azure 儲存體資源，請按一下**設定** > **組態**tooscale 儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-135">For an Azure Storage resource, click **Settings** > **Configuration** tooscale up your storage options.</span></span>
   
    ![向上擴充 hello Azure 應用程式所使用的 Azure 儲存體帳戶](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="ae2c8-137">了解開發人員功能</span><span class="sxs-lookup"><span data-stu-id="ae2c8-137">Learn about developer features</span></span>
<span data-ttu-id="ae2c8-138">根據 hello 定價層，hello 開發人員導向的可用功能如下：</span><span class="sxs-lookup"><span data-stu-id="ae2c8-138">Depending on hello pricing tier, hello following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="ae2c8-139">位元</span><span class="sxs-lookup"><span data-stu-id="ae2c8-139">Bitness</span></span>
* <span data-ttu-id="ae2c8-140">hello**基本**，**標準**，和**Premium**層支援 64 位元和 32 位元應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-140">hello **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="ae2c8-141">hello**免費**和**共用**層支援 32 位元應用程式只計劃。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-141">hello **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="ae2c8-142">偵錯工具支援</span><span class="sxs-lookup"><span data-stu-id="ae2c8-142">Debugger support</span></span>
* <span data-ttu-id="ae2c8-143">偵錯工具支援適用於 hello**免費**，**共用**，和**基本**在每個應用程式服務方案的單一連接模式。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-143">Debugger support is available for hello **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="ae2c8-144">偵錯工具支援適用於 hello**標準**和**Premium**在每個應用程式服務方案的五個並行連線的模式。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-144">Debugger support is available for hello **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="ae2c8-145">了解其他功能</span><span class="sxs-lookup"><span data-stu-id="ae2c8-145">Learn about other features</span></span>
* <span data-ttu-id="ae2c8-146">如需所有 hello 剩餘 hello App Service 中的功能的詳細資訊計劃，包括定價和功能感興趣 tooall 使用者 （包括開發人員），請參閱[應用程式服務定價詳細資料](https://azure.microsoft.com/pricing/details/web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-146">For detailed information about all of hello remaining features in hello App Service plans, including pricing and features of interest tooall users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="ae2c8-147">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務已啟動，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-147">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ae2c8-148">不需要信用卡，無需承諾。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="ae2c8-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae2c8-149">Next steps</span></span>
* <span data-ttu-id="ae2c8-150">tooget 開始使用 Azure，請參閱[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-150">tooget started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ae2c8-151">如需定價、 支援和 SLA 資訊，請造訪下列連結查看 hello。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-151">For information about pricing, support, and SLA, visit hello following links.</span></span>
  
    [<span data-ttu-id="ae2c8-152">資料傳輸定價詳細資料</span><span class="sxs-lookup"><span data-stu-id="ae2c8-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="ae2c8-153">Microsoft Azure 支援方案</span><span class="sxs-lookup"><span data-stu-id="ae2c8-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="ae2c8-154">服務等級協定</span><span class="sxs-lookup"><span data-stu-id="ae2c8-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="ae2c8-155">SQL Database 定價詳細資料</span><span class="sxs-lookup"><span data-stu-id="ae2c8-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="ae2c8-156">[Microsoft Azure 的虛擬機器和雲端服務大小][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="ae2c8-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="ae2c8-157">App Service 定價詳細資料</span><span class="sxs-lookup"><span data-stu-id="ae2c8-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="ae2c8-158">App Service 定價詳細資料 - SSL 連線</span><span class="sxs-lookup"><span data-stu-id="ae2c8-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="ae2c8-159">如需 Azure App Service 最佳作法 (包括建置可調整且具彈性的架構) 的詳細資訊，請參閱 [最佳作法：Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ae2c8-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="ae2c8-160">調整 App Service 應用程式的相關影片，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae2c8-160">For videos about scaling App Service apps, see hello following resources:</span></span>
  
  * [<span data-ttu-id="ae2c8-161">當 Azure 網站-Stefan Schackow tooScale</span><span class="sxs-lookup"><span data-stu-id="ae2c8-161">When tooScale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="ae2c8-162">自動調整 Azure 網站、CPU 或排程 - Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="ae2c8-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="ae2c8-163">如何調整 Azure 網站 - Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="ae2c8-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
