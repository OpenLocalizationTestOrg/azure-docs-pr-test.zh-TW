---
title: "Azure SDK for .NET 2.8 版本資訊"
description: "Azure SDK for .NET 2.8 版本資訊"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 0b9f55d69c824e86245738a082f95fc529583f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a><span data-ttu-id="6f936-103">Azure SDK for .NET 2.8、2.8.1 和 2.8.2</span><span class="sxs-lookup"><span data-stu-id="6f936-103">Azure SDK for .NET 2.8, 2.8.1 and 2.8.2</span></span>
## <a name="overview"></a><span data-ttu-id="6f936-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6f936-104">Overview</span></span>
<span data-ttu-id="6f936-105">本文包含 Azure SDK for .NET 2.8、2.8.1 和 2.8.2 版本的版本資訊 (包含已知問題和重大變更)。</span><span class="sxs-lookup"><span data-stu-id="6f936-105">This article contains the release notes (that includes known issues and breaking changes) for the Azure SDK for .NET 2.8, 2.8.1 and 2.8.2 releases.</span></span> 

<span data-ttu-id="6f936-106">如需這一版中的新功能和更新的完整清單，請參閱 [Azure SDK 2.8 for Visual Studio 2013 and Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) 公告。</span><span class="sxs-lookup"><span data-stu-id="6f936-106">For complete list of new features and updates made in this release, see the [Azure SDK 2.8 for Visual Studio 2013 and Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) announcement.</span></span> 

## <a name="azure-sdk-for-net-28"></a><span data-ttu-id="6f936-107">Azure SDK for .NET 2.8</span><span class="sxs-lookup"><span data-stu-id="6f936-107">Azure SDK for .NET 2.8</span></span>
### <a name="download-azure-sdk-for-net-28"></a><span data-ttu-id="6f936-108">下載 Azure SDK for .NET 2.8</span><span class="sxs-lookup"><span data-stu-id="6f936-108">Download Azure SDK for .NET 2.8</span></span>
[<span data-ttu-id="6f936-109">Azure SDK for .NET 2.8 for Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="6f936-109">Azure SDK for .NET 2.8 for Visual Studio 2015</span></span>](http://go.microsoft.com/fwlink/?LinkId=699285) 

[<span data-ttu-id="6f936-110">Azure SDK for .NET 2.8 for Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6f936-110">Azure SDK for .NET 2.8 for Visual Studio 2013</span></span>](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a><span data-ttu-id="6f936-111">.NET 4.5.2 支援</span><span class="sxs-lookup"><span data-stu-id="6f936-111">.NET 4.5.2 support</span></span>
#### <a name="known-issues"></a><span data-ttu-id="6f936-112">已知問題</span><span class="sxs-lookup"><span data-stu-id="6f936-112">Known issues</span></span>
<span data-ttu-id="6f936-113">Azure.NET SDK 2.8 可讓您建立 .NET 4.5.2 雲端服務套件。</span><span class="sxs-lookup"><span data-stu-id="6f936-113">Azure .NET SDK 2.8 allows you to create .NET 4.5.2 Cloud Service packages.</span></span> <span data-ttu-id="6f936-114">不過，.NET 4.5.2 Framework 要到 2016 年 1 月的客體作業系統版本，才會安裝在預設的客體作業系統映像上。</span><span class="sxs-lookup"><span data-stu-id="6f936-114">However .NET 4.5.2 framework will not be installed on the default Guest OS images until January 2016 Guest OS release.</span></span> <span data-ttu-id="6f936-115">在這之前，可以透過獨立的客體作業系統版本 November 2015-02 取得 .NET 4.5.2 Framework。</span><span class="sxs-lookup"><span data-stu-id="6f936-115">Before that, .NET 4.5.2 framework will be available through a separate Guest OS release version – November 2015-02.</span></span> <span data-ttu-id="6f936-116">請參閱 [Azure 客體 OS 版本與 SDK 相容性矩陣](../cloud-services/cloud-services-guestos-update-matrix.md) 頁面以追蹤該映像何時發行。</span><span class="sxs-lookup"><span data-stu-id="6f936-116">See the [Azure Guest OS Releases and SDK Compatibility Matrix](../cloud-services/cloud-services-guestos-update-matrix.md) page to track when the image will be released.</span></span>  <span data-ttu-id="6f936-117">一旦 November 2015-02 映像發行，您便可選擇透過更新您的雲端服務組態檔 (.cscfg) 來使用該映像。</span><span class="sxs-lookup"><span data-stu-id="6f936-117">Once the November 2015-02 image is released you can choose to use that image by updating your Cloud Service configuration file (.cscfg) file.</span></span> <span data-ttu-id="6f936-118">在服務組態檔中，將 ServiceConfiguration 項目的 osVersion 屬性設定為字串 "WA-GUEST-OS-4.26_201511-02"。</span><span class="sxs-lookup"><span data-stu-id="6f936-118">In the service configuration file set the osVersion attribute of the ServiceConfiguration element to the string "WA-GUEST-OS-4.26_201511-02".</span></span> <span data-ttu-id="6f936-119">如果您選擇加入以使用此映像，那麼您將不會再收到客體 OS 的自動更新。</span><span class="sxs-lookup"><span data-stu-id="6f936-119">If you choose to opt in to use this image then you will no longer get automatic updates to the Guest OS.</span></span> <span data-ttu-id="6f936-120">若要取得自動更新，osVersion 必須設為 “*”，且 .NET 4.5.2 將只能在 2016 年 1 月透過自動更新取得。</span><span class="sxs-lookup"><span data-stu-id="6f936-120">To get the automatic updates the osVersion must be set to “*” and .NET 4.5.2 will only be available through automatic updates in January 2016.</span></span>

### <a name="azure-data-factory"></a><span data-ttu-id="6f936-121">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6f936-121">Azure Data Factory</span></span>
#### <a name="known-issues"></a><span data-ttu-id="6f936-122">已知問題</span><span class="sxs-lookup"><span data-stu-id="6f936-122">Known issues</span></span>
<span data-ttu-id="6f936-123">如果電腦上安裝的 Azure Power Shell 版本比 0.9.8 新，則在與範例資料相關的 **Data Factory 範本** 專案建立期間，Azure Power Shell 指令碼可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="6f936-123">During a **Data Factory Template** project creation involving sample data, azure power shell script may fail if azure power shell version installed on the machine is after 0.9.8.</span></span>

<span data-ttu-id="6f936-124">若要順利地建立這種類型的專案，您必須安裝 [Azure Power Shell 0.9.8 版](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi)。</span><span class="sxs-lookup"><span data-stu-id="6f936-124">In order to successfully create this type of project, you must install [azure power shell version  0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).</span></span>

### <a name="azure-resource-manager-tools"></a><span data-ttu-id="6f936-125">Azure 資源管理員工具</span><span class="sxs-lookup"><span data-stu-id="6f936-125">Azure Resource Manager Tools</span></span>
#### <a name="breaking-changes"></a><span data-ttu-id="6f936-126">重大變更</span><span class="sxs-lookup"><span data-stu-id="6f936-126">Breaking changes</span></span>
<span data-ttu-id="6f936-127">Azure 資源群組專案提供的 PowerShell 指令碼在這個版本中已更新，以搭配新的 Azure PowerShell Cmdlet 1.0 版使用。</span><span class="sxs-lookup"><span data-stu-id="6f936-127">The PowerShell script provided by the Azure Resource Group project has been updated in this release to work with the new Azure PowerShell cmdlets version 1.0.</span></span>  <span data-ttu-id="6f936-128">使用 2.8 以前的 SDK 版本時，將無法從 Visual Studio 使用這個新的指令碼。</span><span class="sxs-lookup"><span data-stu-id="6f936-128">This new script will not work from with Visual Studio when using a version of the SDK prior to 2.8.</span></span>  

<span data-ttu-id="6f936-129">使用 2.8 SDK 時，將無法從 Visual Studio 執行在舊版 SDK 建立的專案中的指令碼。</span><span class="sxs-lookup"><span data-stu-id="6f936-129">Scripts from projects created in earlier versions of the SDK will not run from within Visual Studio when using the 2.8 SDK.</span></span>  <span data-ttu-id="6f936-130">使用適當的 Azure PowerShell Cmdlet 版本，所有指令碼將可繼續在 Visual Studio 以外使用。</span><span class="sxs-lookup"><span data-stu-id="6f936-130">All scripts will continue to work outside of Visual Studio with the appropriate version of the Azure PowerShell cmdlets.</span></span>  

<span data-ttu-id="6f936-131">2.8 SDK 需要 1.0 版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6f936-131">The 2.8 SDK requires version 1.0 of the Azure PowerShell cmdlets.</span></span>  <span data-ttu-id="6f936-132">所有其他版本的 SDK 則需要 0.9.8 版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6f936-132">All other versions of the SDK require version 0.9.8 of the Azure PowerShell cmdlets.</span></span>  <span data-ttu-id="6f936-133">如需詳細資訊，請參閱 [此部落格](http://go.microsoft.com/fwlink/?LinkID=623011) 。</span><span class="sxs-lookup"><span data-stu-id="6f936-133">For more information see [this](http://go.microsoft.com/fwlink/?LinkID=623011) blog.</span></span>

### <a name="web-tools-extensions"></a><span data-ttu-id="6f936-134">Web 工具擴充功能</span><span class="sxs-lookup"><span data-stu-id="6f936-134">Web Tools Extensions</span></span>
#### <a name="known-issues"></a><span data-ttu-id="6f936-135">已知問題</span><span class="sxs-lookup"><span data-stu-id="6f936-135">Known issues</span></span>
<span data-ttu-id="6f936-136">下列版本將解決下列已知問題。</span><span class="sxs-lookup"><span data-stu-id="6f936-136">The following known issues will be addressed in the following release.</span></span>

* <span data-ttu-id="6f936-137">非生產環境 (例如 Azure China 或 Azure Stack 客戶) 的 App Service 相關雲端與伺服器總管筆勢無效。</span><span class="sxs-lookup"><span data-stu-id="6f936-137">App Service related Cloud and Server Explorer gesture for non-production environments (like Azure China or Azure Stack customers) do not work.</span></span> <span data-ttu-id="6f936-138">對於這些受影響區域中的客戶，從 Azure 入口網站下載發行設定檔就能發行。</span><span class="sxs-lookup"><span data-stu-id="6f936-138">For customers in these impacted areas, downloading the publish profile from the Azure portal will enable publishing ability.</span></span> <span data-ttu-id="6f936-139">未來版本將為 Azure China 或 Azure Stack 客戶修復筆勢，例如「連結偵錯工具」和「檢視資料流記錄」。</span><span class="sxs-lookup"><span data-stu-id="6f936-139">A future release will repair gestures such as “Attach Debugger” and “View Streaming Logs” for Azure China and Stack customers.</span></span> 
* <span data-ttu-id="6f936-140">客戶在建立 App Service 時，若要部署的目標 App Insights 執行個體位於美國東部以外的區域，他們可能會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f936-140">Customers may see errors during App Service creation when the App Insights instance to which they are deploying is in a region other than East US.</span></span> <span data-ttu-id="6f936-141">在這些情況下，在入口網站建立 App Service 和下載發行設定檔就能發行。</span><span class="sxs-lookup"><span data-stu-id="6f936-141">In these scenarios, creating an App Service in the portal and downloading the publish profile will enable publishing scenarios.</span></span> 

### <a name="azure-hdinsight-tools"></a><span data-ttu-id="6f936-142">Azure HDInsight 工具</span><span class="sxs-lookup"><span data-stu-id="6f936-142">Azure HDInsight Tools</span></span>
#### <a name="new-updates"></a><span data-ttu-id="6f936-143">新的更新</span><span class="sxs-lookup"><span data-stu-id="6f936-143">New updates</span></span>
* <span data-ttu-id="6f936-144">您可以透過 HiveServer2 在叢集中執行 Hive 查詢，而且幾乎不需要額外支出，並可即時查看工作記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6f936-144">You can execute your Hive query in the cluster via HiveServer2 with almost no overhead and see the job logs in real-time.</span></span>
* <span data-ttu-id="6f936-145">使用新的 Hive 工作執行檢視，您可以深入探究您的工作、尋找更多詳細資料和識別潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="6f936-145">Using the new Hive Task Execution View you can dig into your job deeper, find more details, and identify potential issues.</span></span>

<span data-ttu-id="6f936-146">如需詳細資訊，請參閱 [適用於 Visual Studio 2013 和 Visual Studio 2015 的 Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)。</span><span class="sxs-lookup"><span data-stu-id="6f936-146">For information, see [Azure SDK 2.8 for Visual Studio 2013 and Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span> 

## <a name="azure-sdk-for-net-281"></a><span data-ttu-id="6f936-147">Azure SDK for .NET 2.8.1</span><span class="sxs-lookup"><span data-stu-id="6f936-147">Azure SDK for .NET 2.8.1</span></span>
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="6f936-148">Visual Studio 2013 和 Visual Studio 2015 的已知問題</span><span class="sxs-lookup"><span data-stu-id="6f936-148">Known Issues for Visual Studio 2013 and Visual Studio 2015</span></span>
1. <span data-ttu-id="6f936-149">以位置為目標的觸發 WebJob 發佈會顯示錯誤，並且不會設定排程，不過它會將 WebJob 推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="6f936-149">Triggered WebJob publishes to slots will show and error and won’t set a schedule, but it will push the WebJob to Azure.</span></span> <span data-ttu-id="6f936-150">需要已排程工作的客戶可以使用 Azure 入口網站來設定 WebJob 的排程。</span><span class="sxs-lookup"><span data-stu-id="6f936-150">Customers who are in need of a Scheduled job can then use the Azure Portal to set up the schedule for the WebJob.</span></span> 
2. <span data-ttu-id="6f936-151">Python 客戶可能會遭遇到偵錯工具問題。</span><span class="sxs-lookup"><span data-stu-id="6f936-151">Python customers may experience debugger issues.</span></span> <span data-ttu-id="6f936-152">服務小組即將推出此問題的修正，不過如果客戶受到影響，請透過論壇、公告部落格或版本資訊意見區段知會 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="6f936-152">Service team is rolling out a fix for this but if customers are affected, please let Microsoft know in the forums or on the announcement blog or release notes comments section.</span></span> 
3. <span data-ttu-id="6f936-153">某些區域 (如印度南部) 的客戶將遭遇 App Service 佈建錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f936-153">Customers in certain regions (such as South India) will experience App Service provisioning errors.</span></span> <span data-ttu-id="6f936-154">這個情況與入口網站相符，遭遇這個問題的客戶可以使用 Azure 入口網站來要求這些地理區域的發佈權限。</span><span class="sxs-lookup"><span data-stu-id="6f936-154">This is consistent with the portal, and customers who experience this issue can use the Azure portal to request access to publish to these geo-regions.</span></span> <span data-ttu-id="6f936-155">一旦使用 Azure 入口網站來要求這些區域的存取權限後，佈建應該能正常運作。</span><span class="sxs-lookup"><span data-stu-id="6f936-155">Once they request access to these regions using the Azure portal provisioning should work.</span></span> 

## <a name="azure-sdk-for-net-282"></a><span data-ttu-id="6f936-156">Azure SDK for .NET 2.8.2</span><span class="sxs-lookup"><span data-stu-id="6f936-156">Azure SDK for .NET 2.8.2</span></span>
<span data-ttu-id="6f936-157">在安裝 2.8.2 工具之後，客戶可能會遇到下列問題。</span><span class="sxs-lookup"><span data-stu-id="6f936-157">Following the installation of the 2.8.2 tools, customers may experience the following issue.</span></span>         

* <span data-ttu-id="6f936-158">如果您使用 Windows 10，且尚未安裝 Internet Explorer，您可能會收到「找不到 Internet Explorer」的錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f936-158">If you are using Windows 10 and have not installed Internet Explorer, you may get an "Internet Explorer could not be found" error.</span></span>
  <span data-ttu-id="6f936-159">若要解決此問題，請使用 [新增/移除 Windows 元件] 對話方塊來安裝 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="6f936-159">To resolve the issue, install Internet Explorer using the Add/Remove Windows Components dialog.</span></span>

<span data-ttu-id="6f936-160">如果您發現這個問題，請使用 [傳送笑臉] 功能來報告它。</span><span class="sxs-lookup"><span data-stu-id="6f936-160">If you observe this issue, use the Send-a-smile feature to report it.</span></span>

<span data-ttu-id="6f936-161">如需詳細資訊，請參閱 [這篇](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) 文章。</span><span class="sxs-lookup"><span data-stu-id="6f936-161">For more information, see [this](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) post.</span></span>

## <a name="other-updates"></a><span data-ttu-id="6f936-162">其他更新</span><span class="sxs-lookup"><span data-stu-id="6f936-162">Other updates</span></span>
<span data-ttu-id="6f936-163">如需其他更新，請參閱 [Azure SDK 2.8 公告文章](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)。</span><span class="sxs-lookup"><span data-stu-id="6f936-163">For other updates, see [Azure SDK 2.8 announcement post](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="also-see"></a><span data-ttu-id="6f936-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6f936-164">Also see</span></span>
[<span data-ttu-id="6f936-165">Azure SDK 2.8 公告文章</span><span class="sxs-lookup"><span data-stu-id="6f936-165">Azure SDK 2.8 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[<span data-ttu-id="6f936-166">Azure SDK for .NET 和 API 的支援和停用資訊</span><span class="sxs-lookup"><span data-stu-id="6f936-166">Support and Retirement Information for the Azure SDK for .NET and APIs</span></span>](https://msdn.microsoft.com/library/azure/dn479282.aspx)

