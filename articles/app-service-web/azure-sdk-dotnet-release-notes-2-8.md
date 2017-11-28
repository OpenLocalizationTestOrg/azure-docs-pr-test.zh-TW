---
title: "aaaAzure SDK for.NET 2.8 版本資訊"
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
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a><span data-ttu-id="eaf92-103">Azure SDK for .NET 2.8、2.8.1 和 2.8.2</span><span class="sxs-lookup"><span data-stu-id="eaf92-103">Azure SDK for .NET 2.8, 2.8.1 and 2.8.2</span></span>
## <a name="overview"></a><span data-ttu-id="eaf92-104">概觀</span><span class="sxs-lookup"><span data-stu-id="eaf92-104">Overview</span></span>
<span data-ttu-id="eaf92-105">這篇文章包含 hello 版本資訊 （其中包含已知的問題和重大變更） hello Azure SDK for.NET 2.8，2.8.1 和 2.8.2 釋放。</span><span class="sxs-lookup"><span data-stu-id="eaf92-105">This article contains hello release notes (that includes known issues and breaking changes) for hello Azure SDK for .NET 2.8, 2.8.1 and 2.8.2 releases.</span></span> 

<span data-ttu-id="eaf92-106">新功能和更新在此版本中所做的完整清單，請參閱 hello [Azure SDK 2.8 的 Visual Studio 2013 和 Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)公告。</span><span class="sxs-lookup"><span data-stu-id="eaf92-106">For complete list of new features and updates made in this release, see hello [Azure SDK 2.8 for Visual Studio 2013 and Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) announcement.</span></span> 

## <a name="azure-sdk-for-net-28"></a><span data-ttu-id="eaf92-107">Azure SDK for .NET 2.8</span><span class="sxs-lookup"><span data-stu-id="eaf92-107">Azure SDK for .NET 2.8</span></span>
### <a name="download-azure-sdk-for-net-28"></a><span data-ttu-id="eaf92-108">下載 Azure SDK for .NET 2.8</span><span class="sxs-lookup"><span data-stu-id="eaf92-108">Download Azure SDK for .NET 2.8</span></span>
[<span data-ttu-id="eaf92-109">Azure SDK for .NET 2.8 for Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="eaf92-109">Azure SDK for .NET 2.8 for Visual Studio 2015</span></span>](http://go.microsoft.com/fwlink/?LinkId=699285) 

[<span data-ttu-id="eaf92-110">Azure SDK for .NET 2.8 for Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="eaf92-110">Azure SDK for .NET 2.8 for Visual Studio 2013</span></span>](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a><span data-ttu-id="eaf92-111">.NET 4.5.2 支援</span><span class="sxs-lookup"><span data-stu-id="eaf92-111">.NET 4.5.2 support</span></span>
#### <a name="known-issues"></a><span data-ttu-id="eaf92-112">已知問題</span><span class="sxs-lookup"><span data-stu-id="eaf92-112">Known issues</span></span>
<span data-ttu-id="eaf92-113">Azure.NET SDK 2.8 可讓您 toocreate.NET 4.5.2 的雲端服務封裝。</span><span class="sxs-lookup"><span data-stu-id="eaf92-113">Azure .NET SDK 2.8 allows you toocreate .NET 4.5.2 Cloud Service packages.</span></span> <span data-ttu-id="eaf92-114">不過.NET 4.5.2 hello 預設客體 OS 映像，直到年 1 月 2016 客體作業系統版本上，未安裝 framework。</span><span class="sxs-lookup"><span data-stu-id="eaf92-114">However .NET 4.5.2 framework will not be installed on hello default Guest OS images until January 2016 Guest OS release.</span></span> <span data-ttu-id="eaf92-115">在這之前，可以透過獨立的客體作業系統版本 November 2015-02 取得 .NET 4.5.2 Framework。</span><span class="sxs-lookup"><span data-stu-id="eaf92-115">Before that, .NET 4.5.2 framework will be available through a separate Guest OS release version – November 2015-02.</span></span> <span data-ttu-id="eaf92-116">請參閱 hello [Azure 客體 OS 版本與 SDK 相容性比較表](../cloud-services/cloud-services-guestos-update-matrix.md)頁面 tootrack 時就會釋出 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="eaf92-116">See hello [Azure Guest OS Releases and SDK Compatibility Matrix](../cloud-services/cloud-services-guestos-update-matrix.md) page tootrack when hello image will be released.</span></span>  <span data-ttu-id="eaf92-117">一旦解除 hello 年 11 月 2015年-02 映像您可以選擇 toouse 該映像更新您的雲端服務組態檔 (.cscfg) 檔。</span><span class="sxs-lookup"><span data-stu-id="eaf92-117">Once hello November 2015-02 image is released you can choose toouse that image by updating your Cloud Service configuration file (.cscfg) file.</span></span> <span data-ttu-id="eaf92-118">Hello 服務組態中設定檔的 hello ServiceConfiguration 項目 toohello 字串 hello osVersion 屬性"WA-客體-OS-4.26_201511-02"。</span><span class="sxs-lookup"><span data-stu-id="eaf92-118">In hello service configuration file set hello osVersion attribute of hello ServiceConfiguration element toohello string "WA-GUEST-OS-4.26_201511-02".</span></span> <span data-ttu-id="eaf92-119">如果您選擇 tooopt toouse 此映像您會不會再收到自動更新 toohello 客體 OS。</span><span class="sxs-lookup"><span data-stu-id="eaf92-119">If you choose tooopt in toouse this image then you will no longer get automatic updates toohello Guest OS.</span></span> <span data-ttu-id="eaf92-120">tooget hello 自動更新 hello osVersion 必須設定得"*"和.NET 4.5.2 才會透過自動更新在 2016 年 1 月。</span><span class="sxs-lookup"><span data-stu-id="eaf92-120">tooget hello automatic updates hello osVersion must be set too“*” and .NET 4.5.2 will only be available through automatic updates in January 2016.</span></span>

### <a name="azure-data-factory"></a><span data-ttu-id="eaf92-121">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="eaf92-121">Azure Data Factory</span></span>
#### <a name="known-issues"></a><span data-ttu-id="eaf92-122">已知問題</span><span class="sxs-lookup"><span data-stu-id="eaf92-122">Known issues</span></span>
<span data-ttu-id="eaf92-123">期間**資料 Factory 範本**專案建立涉及範例資料，而 azure power shell 指令碼可能會失敗 hello 電腦上安裝 azure power shell 的版本為 0.9.8 之後。</span><span class="sxs-lookup"><span data-stu-id="eaf92-123">During a **Data Factory Template** project creation involving sample data, azure power shell script may fail if azure power shell version installed on hello machine is after 0.9.8.</span></span>

<span data-ttu-id="eaf92-124">為了 toosuccessfully 建立這種類型的專案，您必須安裝[azure power shell 0.9.8 版雖](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi)。</span><span class="sxs-lookup"><span data-stu-id="eaf92-124">In order toosuccessfully create this type of project, you must install [azure power shell version  0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).</span></span>

### <a name="azure-resource-manager-tools"></a><span data-ttu-id="eaf92-125">Azure 資源管理員工具</span><span class="sxs-lookup"><span data-stu-id="eaf92-125">Azure Resource Manager Tools</span></span>
#### <a name="breaking-changes"></a><span data-ttu-id="eaf92-126">重大變更</span><span class="sxs-lookup"><span data-stu-id="eaf92-126">Breaking changes</span></span>
<span data-ttu-id="eaf92-127">已經在 hello 新 Azure PowerShell 指令程式 1.0 版與此版本 toowork 更新 hello hello Azure 資源群組專案所提供的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="eaf92-127">hello PowerShell script provided by hello Azure Resource Group project has been updated in this release toowork with hello new Azure PowerShell cmdlets version 1.0.</span></span>  <span data-ttu-id="eaf92-128">這個新的指令碼不適用於從 Visual Studio 時使用的 hello SDK 先前 too2.8 版本。</span><span class="sxs-lookup"><span data-stu-id="eaf92-128">This new script will not work from with Visual Studio when using a version of hello SDK prior too2.8.</span></span>  

<span data-ttu-id="eaf92-129">從在舊版的 hello SDK 建立的專案的指令碼時不執行從 Visual Studio 內使用 hello 2.8 SDK。</span><span class="sxs-lookup"><span data-stu-id="eaf92-129">Scripts from projects created in earlier versions of hello SDK will not run from within Visual Studio when using hello 2.8 SDK.</span></span>  <span data-ttu-id="eaf92-130">所有指令碼會繼續與 hello Azure PowerShell cmdlet hello 適當版本 Visual Studio 外部 toowork。</span><span class="sxs-lookup"><span data-stu-id="eaf92-130">All scripts will continue toowork outside of Visual Studio with hello appropriate version of hello Azure PowerShell cmdlets.</span></span>  

<span data-ttu-id="eaf92-131">hello 2.8 SDK 需要 1.0 版的 hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="eaf92-131">hello 2.8 SDK requires version 1.0 of hello Azure PowerShell cmdlets.</span></span>  <span data-ttu-id="eaf92-132">所有其他版本的 hello SDK 需要 0.9.8 版的 hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="eaf92-132">All other versions of hello SDK require version 0.9.8 of hello Azure PowerShell cmdlets.</span></span>  <span data-ttu-id="eaf92-133">如需詳細資訊，請參閱 [此](http://go.microsoft.com/fwlink/?LinkID=623011) 部落格。</span><span class="sxs-lookup"><span data-stu-id="eaf92-133">For more information see [this](http://go.microsoft.com/fwlink/?LinkID=623011) blog.</span></span>

### <a name="web-tools-extensions"></a><span data-ttu-id="eaf92-134">Web 工具擴充功能</span><span class="sxs-lookup"><span data-stu-id="eaf92-134">Web Tools Extensions</span></span>
#### <a name="known-issues"></a><span data-ttu-id="eaf92-135">已知問題</span><span class="sxs-lookup"><span data-stu-id="eaf92-135">Known issues</span></span>
<span data-ttu-id="eaf92-136">hello： 發行中，就會解決下列已知的問題的 hello。</span><span class="sxs-lookup"><span data-stu-id="eaf92-136">hello following known issues will be addressed in hello following release.</span></span>

* <span data-ttu-id="eaf92-137">非生產環境 (例如 Azure China 或 Azure Stack 客戶) 的 App Service 相關雲端與伺服器總管筆勢無效。</span><span class="sxs-lookup"><span data-stu-id="eaf92-137">App Service related Cloud and Server Explorer gesture for non-production environments (like Azure China or Azure Stack customers) do not work.</span></span> <span data-ttu-id="eaf92-138">客戶在這些受影響的區域中下載 hello 發行設定檔與 hello Azure 入口網站將會啟用發行的功能。</span><span class="sxs-lookup"><span data-stu-id="eaf92-138">For customers in these impacted areas, downloading hello publish profile from hello Azure portal will enable publishing ability.</span></span> <span data-ttu-id="eaf92-139">未來版本將為 Azure China 或 Azure Stack 客戶修復筆勢，例如「連結偵錯工具」和「檢視資料流記錄」。</span><span class="sxs-lookup"><span data-stu-id="eaf92-139">A future release will repair gestures such as “Attach Debugger” and “View Streaming Logs” for Azure China and Stack customers.</span></span> 
* <span data-ttu-id="eaf92-140">客戶可能會在建立時 hello App Insights 執行個體的 toowhich 它們部署為美國東部以外的區域中的應用程式服務時看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="eaf92-140">Customers may see errors during App Service creation when hello App Insights instance toowhich they are deploying is in a region other than East US.</span></span> <span data-ttu-id="eaf92-141">在這些情況下，hello 入口網站中建立應用程式服務，以及下載 hello 發行設定檔將會啟用發行的案例。</span><span class="sxs-lookup"><span data-stu-id="eaf92-141">In these scenarios, creating an App Service in hello portal and downloading hello publish profile will enable publishing scenarios.</span></span> 

### <a name="azure-hdinsight-tools"></a><span data-ttu-id="eaf92-142">Azure HDInsight 工具</span><span class="sxs-lookup"><span data-stu-id="eaf92-142">Azure HDInsight Tools</span></span>
#### <a name="new-updates"></a><span data-ttu-id="eaf92-143">新的更新</span><span class="sxs-lookup"><span data-stu-id="eaf92-143">New updates</span></span>
* <span data-ttu-id="eaf92-144">您可以透過 HiveServer2 幾乎沒有的額外負荷的 hello 叢集中執行 Hive 查詢，並查看記錄中的 hello 作業即時。</span><span class="sxs-lookup"><span data-stu-id="eaf92-144">You can execute your Hive query in hello cluster via HiveServer2 with almost no overhead and see hello job logs in real-time.</span></span>
* <span data-ttu-id="eaf92-145">使用 hello 新 Hive 工作執行檢視可以發掘更深入，您的工作尋找詳細資訊，並識別潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="eaf92-145">Using hello new Hive Task Execution View you can dig into your job deeper, find more details, and identify potential issues.</span></span>

<span data-ttu-id="eaf92-146">如需詳細資訊，請參閱 [適用於 Visual Studio 2013 和 Visual Studio 2015 的 Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)。</span><span class="sxs-lookup"><span data-stu-id="eaf92-146">For information, see [Azure SDK 2.8 for Visual Studio 2013 and Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span> 

## <a name="azure-sdk-for-net-281"></a><span data-ttu-id="eaf92-147">Azure SDK for .NET 2.8.1</span><span class="sxs-lookup"><span data-stu-id="eaf92-147">Azure SDK for .NET 2.8.1</span></span>
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="eaf92-148">Visual Studio 2013 和 Visual Studio 2015 的已知問題</span><span class="sxs-lookup"><span data-stu-id="eaf92-148">Known Issues for Visual Studio 2013 and Visual Studio 2015</span></span>
1. <span data-ttu-id="eaf92-149">觸發的 WebJob 發行 tooslots 會顯示和錯誤，並不會設定排程，但它將推送 hello WebJob tooAzure。</span><span class="sxs-lookup"><span data-stu-id="eaf92-149">Triggered WebJob publishes tooslots will show and error and won’t set a schedule, but it will push hello WebJob tooAzure.</span></span> <span data-ttu-id="eaf92-150">需要已排程作業的客戶可以使用 hello WebJob hello Azure 入口網站 tooset hello 排程。</span><span class="sxs-lookup"><span data-stu-id="eaf92-150">Customers who are in need of a Scheduled job can then use hello Azure Portal tooset up hello schedule for hello WebJob.</span></span> 
2. <span data-ttu-id="eaf92-151">Python 客戶可能會遭遇到偵錯工具問題。</span><span class="sxs-lookup"><span data-stu-id="eaf92-151">Python customers may experience debugger issues.</span></span> <span data-ttu-id="eaf92-152">服務小組這個時推出修正，但如果影響客戶，請讓 Microsoft 知道 hello 論壇中或 hello 公告部落格上，或釋放提示註解 > 一節。</span><span class="sxs-lookup"><span data-stu-id="eaf92-152">Service team is rolling out a fix for this but if customers are affected, please let Microsoft know in hello forums or on hello announcement blog or release notes comments section.</span></span> 
3. <span data-ttu-id="eaf92-153">某些區域 (如印度南部) 的客戶將遭遇 App Service 佈建錯誤。</span><span class="sxs-lookup"><span data-stu-id="eaf92-153">Customers in certain regions (such as South India) will experience App Service provisioning errors.</span></span> <span data-ttu-id="eaf92-154">這是與 hello 入口網站中，相同，而且會發生此問題的客戶可以使用 Azure 入口網站 toorequest 存取 toopublish toothese 地區 hello。</span><span class="sxs-lookup"><span data-stu-id="eaf92-154">This is consistent with hello portal, and customers who experience this issue can use hello Azure portal toorequest access toopublish toothese geo-regions.</span></span> <span data-ttu-id="eaf92-155">一旦要求存取 toothese 區域使用 Azure 入口網站佈建的 hello 應該會運作。</span><span class="sxs-lookup"><span data-stu-id="eaf92-155">Once they request access toothese regions using hello Azure portal provisioning should work.</span></span> 

## <a name="azure-sdk-for-net-282"></a><span data-ttu-id="eaf92-156">Azure SDK for .NET 2.8.2</span><span class="sxs-lookup"><span data-stu-id="eaf92-156">Azure SDK for .NET 2.8.2</span></span>
<span data-ttu-id="eaf92-157">下列的 hello 2.8.2 工具 hello 安裝，客戶可能會遇到下列問題的 hello。</span><span class="sxs-lookup"><span data-stu-id="eaf92-157">Following hello installation of hello 2.8.2 tools, customers may experience hello following issue.</span></span>         

* <span data-ttu-id="eaf92-158">如果您使用 Windows 10，且尚未安裝 Internet Explorer，您可能會收到「找不到 Internet Explorer」的錯誤。</span><span class="sxs-lookup"><span data-stu-id="eaf92-158">If you are using Windows 10 and have not installed Internet Explorer, you may get an "Internet Explorer could not be found" error.</span></span>
  <span data-ttu-id="eaf92-159">tooresolve hello 問題，請安裝 Internet Explorer 使用 hello 新增/移除 Windows 元件 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="eaf92-159">tooresolve hello issue, install Internet Explorer using hello Add/Remove Windows Components dialog.</span></span>

<span data-ttu-id="eaf92-160">如果您發現這個問題，請使用 hello 傳送笑臉 的功能 tooreport 它。</span><span class="sxs-lookup"><span data-stu-id="eaf92-160">If you observe this issue, use hello Send-a-smile feature tooreport it.</span></span>

<span data-ttu-id="eaf92-161">如需詳細資訊，請參閱 [這篇](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) 文章。</span><span class="sxs-lookup"><span data-stu-id="eaf92-161">For more information, see [this](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) post.</span></span>

## <a name="other-updates"></a><span data-ttu-id="eaf92-162">其他更新</span><span class="sxs-lookup"><span data-stu-id="eaf92-162">Other updates</span></span>
<span data-ttu-id="eaf92-163">如需其他更新，請參閱 [Azure SDK 2.8 公告文章](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)。</span><span class="sxs-lookup"><span data-stu-id="eaf92-163">For other updates, see [Azure SDK 2.8 announcement post](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="also-see"></a><span data-ttu-id="eaf92-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="eaf92-164">Also see</span></span>
[<span data-ttu-id="eaf92-165">Azure SDK 2.8 公告文章</span><span class="sxs-lookup"><span data-stu-id="eaf92-165">Azure SDK 2.8 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[<span data-ttu-id="eaf92-166">支援和 hello Azure SDK for.NET 和 Api 的停用資訊</span><span class="sxs-lookup"><span data-stu-id="eaf92-166">Support and Retirement Information for hello Azure SDK for .NET and APIs</span></span>](https://msdn.microsoft.com/library/azure/dn479282.aspx)

