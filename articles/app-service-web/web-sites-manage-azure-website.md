---
title: "在 Azure App Service 中管理 Web 應用程式"
description: "適用於在 Azure App Service 中管理 Web 應用程式之資源的連結。"
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="1ecee-103">在 Azure App Service 中管理 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ecee-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="1ecee-104">本主題含有適合用來在 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)中管理 Web 應用程式之資源的連結。</span><span class="sxs-lookup"><span data-stu-id="1ecee-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="1ecee-105">所謂的管理包括所有維持 Web 應用程式順暢運作的工作。</span><span class="sxs-lookup"><span data-stu-id="1ecee-105">Management includes all of the tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="1ecee-106">在 Web 應用程式的生命週期內，從初始部署到正常運作、維護及更新，都需要執行不同的管理工作。</span><span class="sxs-lookup"><span data-stu-id="1ecee-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span></span>

<span data-ttu-id="1ecee-107">您可以在 Azure 入口網站中執行許多 Web 應用程式管理工作。</span><span class="sxs-lookup"><span data-stu-id="1ecee-107">Many web app management tasks can be performed in the Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-to-production"></a><span data-ttu-id="1ecee-108">將 Web 應用程式部署到生產環境之前</span><span class="sxs-lookup"><span data-stu-id="1ecee-108">Before you deploy your web app to production</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="1ecee-109">選擇階層。</span><span class="sxs-lookup"><span data-stu-id="1ecee-109">Choose a tier</span></span>
<span data-ttu-id="1ecee-110">Azure App Service 提供了五種階層：免費、共用、基本、標準和高階。</span><span class="sxs-lookup"><span data-stu-id="1ecee-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="1ecee-111">如需各階層之功能和定價的相關資訊，請參閱 [網站定價詳細資料](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="1ecee-112">[應用程式服務方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) 可讓您將多個 Web 應用程式分組在同一個階層下。</span><span class="sxs-lookup"><span data-stu-id="1ecee-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span></span>
* <span data-ttu-id="1ecee-113">建立 Web 應用程式之後，您可以隨時 [切換階層](web-sites-scale.md) 。</span><span class="sxs-lookup"><span data-stu-id="1ecee-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="1ecee-114">組態</span><span class="sxs-lookup"><span data-stu-id="1ecee-114">Configuration</span></span>
<span data-ttu-id="1ecee-115">使用 [Azure 入口網站](https://portal.azure.com/) 來設定各種組態選項。</span><span class="sxs-lookup"><span data-stu-id="1ecee-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span></span> <span data-ttu-id="1ecee-116">如需詳細資料，請參閱 [在 Azure App Service 中設定 Web 應用程式](web-sites-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="1ecee-117">以下是簡短的檢查清單：</span><span class="sxs-lookup"><span data-stu-id="1ecee-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="1ecee-118">視需要選取 .NET、PHP、Java 或 Python 的 **執行階段版本** 。</span><span class="sxs-lookup"><span data-stu-id="1ecee-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="1ecee-119">如果您的 Web 應用程式使用 WebSocket 通訊協定，請啟用 **WebSockets** 。</span><span class="sxs-lookup"><span data-stu-id="1ecee-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span></span> <span data-ttu-id="1ecee-120">(這包括使用 [ASP.NET SignalR](http://www.asp.net/signalr) (英文) 或 [socket.io](web-sites-nodejs-chat-app-socketio.md) 的應用程式)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="1ecee-121">您是否執行連續性的 Web 工作？</span><span class="sxs-lookup"><span data-stu-id="1ecee-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="1ecee-122">如果是的話，請啟用 [Always On] 。</span><span class="sxs-lookup"><span data-stu-id="1ecee-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="1ecee-123">設定 **預設文件**(如 index.html)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-123">Set the **default document**, such as index.html.</span></span>

<span data-ttu-id="1ecee-124">除了以上基本組態設定之外，您也許還想要設定以下各項：</span><span class="sxs-lookup"><span data-stu-id="1ecee-124">In addition to these basic configuration settings, you may want to configure the following:</span></span>

* <span data-ttu-id="1ecee-125">**安全通訊端層 (SSL)** 加密。</span><span class="sxs-lookup"><span data-stu-id="1ecee-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="1ecee-126">若要使用 SSL 搭配自訂網域名稱，您必須取得 SSL 憑證並設定 Web 應用程式來加以使用。</span><span class="sxs-lookup"><span data-stu-id="1ecee-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span></span> <span data-ttu-id="1ecee-127">請參閱 [針對 Azure App Service 中的 Web 應用程式啟用 HTTPS](app-service-web-tutorial-custom-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="1ecee-128">**自訂網域名稱。**</span><span class="sxs-lookup"><span data-stu-id="1ecee-128">**Custom domain name.**</span></span> <span data-ttu-id="1ecee-129">您的 Web 應用程式會自動取得 azurewebsites.net 下的子網域。</span><span class="sxs-lookup"><span data-stu-id="1ecee-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="1ecee-130">您可以使其與自訂網域名稱 (如 contoso.com) 相關聯。</span><span class="sxs-lookup"><span data-stu-id="1ecee-130">You can associate a custom domain name, such as contoso.com.</span></span> <span data-ttu-id="1ecee-131">請參閱 [在 Azure App Service 中設定自訂網域名稱](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-131">See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="1ecee-132">語言特有組態：</span><span class="sxs-lookup"><span data-stu-id="1ecee-132">Language-specific configuration:</span></span>

* <span data-ttu-id="1ecee-133">**PHP**： [在 Azure App Service Web Apps 中設定 PHP](web-sites-php-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="1ecee-134">**Python**： [使用 Azure App Service Web Apps 設定 Python](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="1ecee-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="1ecee-135">當 Web 應用程式執行時</span><span class="sxs-lookup"><span data-stu-id="1ecee-135">While your web app is running</span></span>
<span data-ttu-id="1ecee-136">當 Web 應用程式執行時，您會想要確認 Web 應用程式是否可供使用，以及是否能根據使用者流量而調整。</span><span class="sxs-lookup"><span data-stu-id="1ecee-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span></span> <span data-ttu-id="1ecee-137">您可能也需要疑難排解錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ecee-137">You may also need to troubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="1ecee-138">監視</span><span class="sxs-lookup"><span data-stu-id="1ecee-138">Monitoring</span></span>
* <span data-ttu-id="1ecee-139">您可以透過 Azure 入口網站來 [新增效能度量](web-sites-monitor.md) (如 CPU 使用率和用戶端要求數目)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="1ecee-140">[調整 Web 應用程式](web-sites-scale.md) 以因應流量變化。</span><span class="sxs-lookup"><span data-stu-id="1ecee-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span></span> <span data-ttu-id="1ecee-141">您可以根據階層來調整 VM 的數目和/或 VM 執行個體的大小。</span><span class="sxs-lookup"><span data-stu-id="1ecee-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span></span> <span data-ttu-id="1ecee-142">在標準和高階階層中，您還可以設定自動調整，使 Web 應用程式得以按照固定排程或根據負載自動調整。</span><span class="sxs-lookup"><span data-stu-id="1ecee-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span></span>  

### <a name="backups"></a><span data-ttu-id="1ecee-143">備份</span><span class="sxs-lookup"><span data-stu-id="1ecee-143">Backups</span></span>
* <span data-ttu-id="1ecee-144">設定 Web 應用程式的 [自動備份](web-sites-backup.md) 。</span><span class="sxs-lookup"><span data-stu-id="1ecee-144">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="1ecee-145">透過 [本視訊](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/)深入了解備份。</span><span class="sxs-lookup"><span data-stu-id="1ecee-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="1ecee-146">深入了解 Azure SQL Database 中的 [資料庫復原](../sql-database/sql-database-business-continuity.md) 選項。</span><span class="sxs-lookup"><span data-stu-id="1ecee-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="1ecee-147">疑難排解</span><span class="sxs-lookup"><span data-stu-id="1ecee-147">Troubleshooting</span></span>
* <span data-ttu-id="1ecee-148">發生問題時，您可以在雲端使用診斷記錄和即時偵錯，以 [在 Visual Studio 中疑難排解 Azure 網站](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span></span> 
* <span data-ttu-id="1ecee-149">在 Visual Studio 之外，還有各種方法可用來收集診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="1ecee-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span></span> <span data-ttu-id="1ecee-150">請參閱 [在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能](web-sites-enable-diagnostic-log.md)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="1ecee-151">若是 Node.js 應用程式，請參閱 [如何在 Azure App Service 中偵錯 Node.js Web 應用程式](web-sites-nodejs-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="1ecee-152">還原資料</span><span class="sxs-lookup"><span data-stu-id="1ecee-152">Restoring Data</span></span>
* <span data-ttu-id="1ecee-153">[還原](web-sites-restore.md) 先前已備份的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ecee-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="1ecee-154">更新 Web 應用程式時</span><span class="sxs-lookup"><span data-stu-id="1ecee-154">When you update your web app</span></span>
<span data-ttu-id="1ecee-155">如果您尚未啟用自動備份，可以建立 [手動備份](web-sites-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="1ecee-156">請考慮使用 [預備部署](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="1ecee-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="1ecee-157">此選項可讓您將更新發佈到與生產部署並行運作的預備部署。</span><span class="sxs-lookup"><span data-stu-id="1ecee-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


