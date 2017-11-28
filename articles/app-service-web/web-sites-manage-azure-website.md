---
title: "aaaManage Azure App Service 中的 web 應用程式"
description: "管理 Azure App Service 中的 web 應用程式的連結 tooresources。"
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
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="49f8b-103">在 Azure App Service 中管理 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="49f8b-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="49f8b-104">本主題包含管理 web 應用程式中的連結 tooresources [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="49f8b-105">管理包含所有保留順暢執行您 web 應用程式的 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="49f8b-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="49f8b-106">Hello 存留期的 web 應用程式，您將執行不同的管理工作，當您移動從初始部署 toonormal 操作、 維護和更新。</span><span class="sxs-lookup"><span data-stu-id="49f8b-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="49f8b-107">許多 web 應用程式管理工作，可以在 hello Azure 入口網站中執行。</span><span class="sxs-lookup"><span data-stu-id="49f8b-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="49f8b-108">部署您的 web 應用程式 tooproduction 之前</span><span class="sxs-lookup"><span data-stu-id="49f8b-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="49f8b-109">選擇階層。</span><span class="sxs-lookup"><span data-stu-id="49f8b-109">Choose a tier</span></span>
<span data-ttu-id="49f8b-110">Azure App Service 提供了五種階層：免費、共用、基本、標準和高階。</span><span class="sxs-lookup"><span data-stu-id="49f8b-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="49f8b-111">Hello 功能和定價的每一層的相關資訊，請參閱[定價詳細資料](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="49f8b-112">[應用程式服務計劃](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)可以讓您將多個 web 應用程式在 hello 同一層。</span><span class="sxs-lookup"><span data-stu-id="49f8b-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="49f8b-113">建立 Web 應用程式之後，您可以隨時 [切換階層](web-sites-scale.md) 。</span><span class="sxs-lookup"><span data-stu-id="49f8b-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="49f8b-114">組態</span><span class="sxs-lookup"><span data-stu-id="49f8b-114">Configuration</span></span>
<span data-ttu-id="49f8b-115">使用 hello [Azure 入口網站](https://portal.azure.com/)tooset 各種組態選項。</span><span class="sxs-lookup"><span data-stu-id="49f8b-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="49f8b-116">如需詳細資料，請參閱 [在 Azure App Service 中設定 Web 應用程式](web-sites-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="49f8b-117">以下是簡短的檢查清單：</span><span class="sxs-lookup"><span data-stu-id="49f8b-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="49f8b-118">視需要選取 .NET、PHP、Java 或 Python 的 **執行階段版本** 。</span><span class="sxs-lookup"><span data-stu-id="49f8b-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="49f8b-119">啟用**WebSockets**如果您的 web 應用程式使用 hello WebSocket 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="49f8b-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="49f8b-120">(這包括使用 [ASP.NET SignalR](http://www.asp.net/signalr) (英文) 或 [socket.io](web-sites-nodejs-chat-app-socketio.md) 的應用程式)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="49f8b-121">您是否執行連續性的 Web 工作？</span><span class="sxs-lookup"><span data-stu-id="49f8b-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="49f8b-122">如果是的話，請啟用 [Always On] 。</span><span class="sxs-lookup"><span data-stu-id="49f8b-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="49f8b-123">設定 hello**預設文件**，例如 index.html。</span><span class="sxs-lookup"><span data-stu-id="49f8b-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="49f8b-124">在加法 toothese 基本組態設定，您可能想 tooconfigure hello 下列：</span><span class="sxs-lookup"><span data-stu-id="49f8b-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="49f8b-125">**安全通訊端層 (SSL)** 加密。</span><span class="sxs-lookup"><span data-stu-id="49f8b-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="49f8b-126">toouse SSL 的自訂網域名稱，您必須取得 SSL 憑證，並設定您的 web 應用程式 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="49f8b-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="49f8b-127">請參閱 [針對 Azure App Service 中的 Web 應用程式啟用 HTTPS](app-service-web-tutorial-custom-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="49f8b-128">**自訂網域名稱。**</span><span class="sxs-lookup"><span data-stu-id="49f8b-128">**Custom domain name.**</span></span> <span data-ttu-id="49f8b-129">您的 Web 應用程式會自動取得 azurewebsites.net 下的子網域。</span><span class="sxs-lookup"><span data-stu-id="49f8b-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="49f8b-130">您可以使其與自訂網域名稱 (如 contoso.com) 相關聯。請參閱 [在 Azure App Service 中設定自訂網域名稱](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="49f8b-131">語言特有組態：</span><span class="sxs-lookup"><span data-stu-id="49f8b-131">Language-specific configuration:</span></span>

* <span data-ttu-id="49f8b-132">**PHP**： [在 Azure App Service Web Apps 中設定 PHP](web-sites-php-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="49f8b-133">**Python**： [使用 Azure App Service Web Apps 設定 Python](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="49f8b-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="49f8b-134">當 Web 應用程式執行時</span><span class="sxs-lookup"><span data-stu-id="49f8b-134">While your web app is running</span></span>
<span data-ttu-id="49f8b-135">執行您 web 應用程式時，您會想 toomake 確定可用，但它縮放 toomeet 使用者流量。</span><span class="sxs-lookup"><span data-stu-id="49f8b-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="49f8b-136">您可能也需要 tootroubleshoot 錯誤。</span><span class="sxs-lookup"><span data-stu-id="49f8b-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="49f8b-137">監視</span><span class="sxs-lookup"><span data-stu-id="49f8b-137">Monitoring</span></span>
* <span data-ttu-id="49f8b-138">您可以透過 hello Azure 入口網站，[新增效能度量](web-sites-monitor.md)CPU 使用狀況等用戶端要求數量。</span><span class="sxs-lookup"><span data-stu-id="49f8b-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="49f8b-139">[調整您的 web 應用程式](web-sites-scale.md)回應 tootraffic 中。</span><span class="sxs-lookup"><span data-stu-id="49f8b-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="49f8b-140">根據您的層，您可以調整 Vm 的 hello 數目及/或 hello hello VM 執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="49f8b-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="49f8b-141">在 hello Standard 和 Premium 層，您也可以設定自動調整，讓您 web 應用程式在固定排程，或在回應 tooload 自動縮放。</span><span class="sxs-lookup"><span data-stu-id="49f8b-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="49f8b-142">備份</span><span class="sxs-lookup"><span data-stu-id="49f8b-142">Backups</span></span>
* <span data-ttu-id="49f8b-143">設定 Web 應用程式的 [自動備份](web-sites-backup.md) 。</span><span class="sxs-lookup"><span data-stu-id="49f8b-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="49f8b-144">透過 [本視訊](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/)深入了解備份。</span><span class="sxs-lookup"><span data-stu-id="49f8b-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="49f8b-145">了解如何 hello 方式[資料庫復原](../sql-database/sql-database-business-continuity.md)Azure SQL Database 中。</span><span class="sxs-lookup"><span data-stu-id="49f8b-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="49f8b-146">疑難排解</span><span class="sxs-lookup"><span data-stu-id="49f8b-146">Troubleshooting</span></span>
* <span data-ttu-id="49f8b-147">如果發生錯誤，您可以[Visual Studio 中疑難排解](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)、 使用 診斷記錄檔，以及即時偵錯 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="49f8b-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="49f8b-148">外部 Visual Studio 中，有各種方式 toocollect 診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="49f8b-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="49f8b-149">請參閱 [在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能](web-sites-enable-diagnostic-log.md)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="49f8b-150">Node.js 應用程式，請參閱[toodebug Node.js web 應用程式在 Azure App Service 中的](web-sites-nodejs-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="49f8b-151">還原資料</span><span class="sxs-lookup"><span data-stu-id="49f8b-151">Restoring Data</span></span>
* <span data-ttu-id="49f8b-152">[還原](web-sites-restore.md) 先前已備份的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="49f8b-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="49f8b-153">更新 Web 應用程式時</span><span class="sxs-lookup"><span data-stu-id="49f8b-153">When you update your web app</span></span>
<span data-ttu-id="49f8b-154">如果您尚未啟用自動備份，可以建立 [手動備份](web-sites-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="49f8b-155">請考慮使用 [預備部署](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="49f8b-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="49f8b-156">此選項可讓您發行更新 tooa 預備環境部署執行的並行與生產環境部署。</span><span class="sxs-lookup"><span data-stu-id="49f8b-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


