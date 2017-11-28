---
title: "aaaAzure SDK for.NET 2.6 版本資訊"
description: "Azure SDK for .NET 2.6 版本資訊"
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a><span data-ttu-id="413fa-103">Azure SDK for .NET 2.6 版本資訊</span><span class="sxs-lookup"><span data-stu-id="413fa-103">Azure SDK for .NET 2.6 Release Notes</span></span>
<span data-ttu-id="413fa-104">本文件包含 hello hello Azure SDK for.NET 2.6 版的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="413fa-104">This document contains hello release notes for hello Azure SDK for .NET 2.6 release.</span></span> 

<span data-ttu-id="413fa-105">Azure SDK 2.6 中，您可以開發雲端服務 (PaaS) 為目標應用程式.NET 4.5.2 或.NET 4.6 前提是您手動安裝 hello 目標.NET Framework 上 hello 雲端服務角色。</span><span class="sxs-lookup"><span data-stu-id="413fa-105">With Azure SDK 2.6 you can develop cloud service applications (PaaS) targeting .NET 4.5.2 or .NET 4.6 provided that you manually install hello target .NET Framework on hello Cloud Service Role.</span></span> <span data-ttu-id="413fa-106">請參閱 [在雲端服務角色上安裝 .NET](http://go.microsoft.com/fwlink/?LinkID=309796)。</span><span class="sxs-lookup"><span data-stu-id="413fa-106">See [Install .NET on a Cloud Service Role](http://go.microsoft.com/fwlink/?LinkID=309796).</span></span>

## <a name="service-bus-updates"></a><span data-ttu-id="413fa-107">服務匯流排更新</span><span class="sxs-lookup"><span data-stu-id="413fa-107">Service Bus updates</span></span>
* <span data-ttu-id="413fa-108">事件中心：</span><span class="sxs-lookup"><span data-stu-id="413fa-108">Event Hubs:</span></span> 
  
  * <span data-ttu-id="413fa-109">現在藉由公開事件中心的其他發行者端點，可在傳送事件時提供目標存取控制。</span><span class="sxs-lookup"><span data-stu-id="413fa-109">Now allows targeted access control when sending events by exposing additional publisher endpoint for Event Hubs.</span></span>
  * <span data-ttu-id="413fa-110">其他的穩定性和改進加入 tooEvent 中心功能。</span><span class="sxs-lookup"><span data-stu-id="413fa-110">Additional stability and improvement added tooEvent Hubs feature.</span></span>
  * <span data-ttu-id="413fa-111">在訊息和事件中心內，加入 WebSocket 上的 Amqp 通訊協定支援。</span><span class="sxs-lookup"><span data-stu-id="413fa-111">Adding support of Amqp protocol over WebSocket for messaging and Event Hubs.</span></span>

## <a name="hdinsight-tools-for-visual-studio-updates"></a><span data-ttu-id="413fa-112">HDInsight Tools for Visual Studio 更新</span><span class="sxs-lookup"><span data-stu-id="413fa-112">HDInsight Tools for Visual Studio updates</span></span>
* <span data-ttu-id="413fa-113">**IntelliSense 的增強功能**：遠端中繼資料建議</span><span class="sxs-lookup"><span data-stu-id="413fa-113">**IntelliSense enhancement**: remote metadata suggestion</span></span>
  
    <span data-ttu-id="413fa-114">HDInsight Tools for Visual Studio 現在支援在編輯 Hive 指令碼時取得遠端中繼資料。</span><span class="sxs-lookup"><span data-stu-id="413fa-114">Now HDInsight Tools for Visual Studio supports getting remote metadata when you are editing your Hive script.</span></span> <span data-ttu-id="413fa-115">例如，您可以輸入**選取 * FROM**且將顯示所有 hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="413fa-115">For example, you can type **SELECT * FROM** and all hello table names will be shown.</span></span> <span data-ttu-id="413fa-116">此外，指定資料表之後將會顯示 hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="413fa-116">Also, hello column names will be shown after specifying a table.</span></span>
* <span data-ttu-id="413fa-117">**HDInsight 模擬器支援**</span><span class="sxs-lookup"><span data-stu-id="413fa-117">**HDInsight emulator support**</span></span>
  
    <span data-ttu-id="413fa-118">現在 HDInsight Tools for Visual Studio 支援連接 tooHDInsight 模擬器中，因此您無法在本機開發您的 Hive 指令碼，而不會引進任何費用，再執行這些指令碼，針對您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="413fa-118">Now HDInsight Tools for Visual Studio support connecting tooHDInsight emulator, so you could develop your Hive scripts locally without introducing any cost, then execute those scripts against your HDInsight clusters.</span></span> 
  
    <span data-ttu-id="413fa-119">如需詳細資訊，請參閱太[此手冊](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="413fa-119">For more information, refer too[this manual](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).</span></span>
* <span data-ttu-id="413fa-120">**HDInsight Tools for Visual Studio 支援一般的 Hadoop 叢集** (預覽)</span><span class="sxs-lookup"><span data-stu-id="413fa-120">**HDInsight Tools for Visual Studio support for generic Hadoop clusters** (Preview)</span></span>
  
    <span data-ttu-id="413fa-121">現在 HDInsight Tools for Visual Studio 支援一般的 Hadoop 叢集，因此您可以使用 HDInsight Tools for Visual Studio toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="413fa-121">Now HDInsight Tools for Visual Studio support generic Hadoop clusters, so you can use HDInsight Tools for Visual Studio toodo hello following:</span></span>
  
  * <span data-ttu-id="413fa-122">tooyour 叢集連線</span><span class="sxs-lookup"><span data-stu-id="413fa-122">connect tooyour cluster,</span></span> 
  * <span data-ttu-id="413fa-123">使用增強式 IntelliSense/自動完成支援來撰寫 Hive 查詢、</span><span class="sxs-lookup"><span data-stu-id="413fa-123">write Hive query with enhanced IntelliSense/auto-completion support,</span></span> 
  * <span data-ttu-id="413fa-124">檢視您的叢集與直覺的 UI 中所有的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="413fa-124">view all hello jobs in your cluster with an intuitive UI.</span></span> 
    
    <span data-ttu-id="413fa-125">如需詳細資訊，請參閱太[此手冊](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="413fa-125">For more information, refer too[this manual](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).</span></span>

## <a name="in-role-cache-updates"></a><span data-ttu-id="413fa-126">角色中快取更新</span><span class="sxs-lookup"><span data-stu-id="413fa-126">In-Role Cache updates</span></span>
* <span data-ttu-id="413fa-127">**角色中快取**已更新的 toouse **Microsoft Azure 儲存體 SDK** 4.3 版。</span><span class="sxs-lookup"><span data-stu-id="413fa-127">**In-Role Cache** was updated toouse **Microsoft Azure Storage SDK** version 4.3.</span></span> <span data-ttu-id="413fa-128">到目前為止，hello **In-role Cache**已使用 Azure 儲存體 SDK 1.7 版。</span><span class="sxs-lookup"><span data-stu-id="413fa-128">Until now, hello **In-Role Cache** was using Azure Storage SDK version 1.7.</span></span>
  
    <span data-ttu-id="413fa-129">客戶使用 Azure SDK 2.5 或以下應該更新 tooAzure SDK 2.6 和移動 toohello 新版的 Azure 儲存體 SDK。</span><span class="sxs-lookup"><span data-stu-id="413fa-129">Customers using Azure SDK 2.5 or below should update tooAzure SDK 2.6 and move toohello new version of Azure Storage SDK.</span></span> 
  
    <span data-ttu-id="413fa-130">在此時間的 Azure 儲存體版本 2011年-08-18 是排程的 toobe 移除 2016 年 8 月 1 日。</span><span class="sxs-lookup"><span data-stu-id="413fa-130">At this time Azure Storage version 2011-08-18 is scheduled toobe removed August 1, 2016.</span></span> <span data-ttu-id="413fa-131">此時必須完成從 Azure SDK 2.5 或低於 too2.6 的角色中快取的任何移轉作業。</span><span class="sxs-lookup"><span data-stu-id="413fa-131">Any migrations of In-Role Cache from Azure SDK 2.5 or below too2.6 must be complete by this time.</span></span> <span data-ttu-id="413fa-132">如需有關 Azure 儲存體 2011年-08-18 版的 hello 淘汰的詳細資訊，請參閱[Microsoft Azure 儲存體服務版本移除的更新： 副檔名 too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx)。</span><span class="sxs-lookup"><span data-stu-id="413fa-132">For more information on hello retirement of Azure Storage version 2011-08-18, see [Microsoft Azure Storage Service Version Removal Update: Extension too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="413fa-133">我們將發表 hello 2016 年 11 月 30 日，停用 Azure 受管理快取服務與 Azure 角色中快取。</span><span class="sxs-lookup"><span data-stu-id="413fa-133">We’re announcing hello November 30, 2016, retirement for Azure Managed Cache Service and Azure In-Role Cache.</span></span> <span data-ttu-id="413fa-134">我們建議您移轉 tooAzure Redis 快取在此停用的準備。</span><span class="sxs-lookup"><span data-stu-id="413fa-134">We recommend that you migrate tooAzure Redis Cache in preparation for this retirement.</span></span> <span data-ttu-id="413fa-135">如需日期和移轉指南的詳細資訊，請參閱 [我適合使用哪個 Azure 快取服務？](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)</span><span class="sxs-lookup"><span data-stu-id="413fa-135">For more information on dates and migration guidance, see [Which Azure Cache offering is right for me?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)</span></span>
> 
> 

## <a name="azure-app-service-tools"></a><span data-ttu-id="413fa-136">Azure App Service 工具</span><span class="sxs-lookup"><span data-stu-id="413fa-136">Azure App Service Tools</span></span>
<span data-ttu-id="413fa-137">hello 下列項目已更新在 hello Azure SDK 2.6 版本。</span><span class="sxs-lookup"><span data-stu-id="413fa-137">hello following items were updated in hello Azure SDK 2.6 release.</span></span>

* <span data-ttu-id="413fa-138">Azure 發行增強 tooinclude Azure API 應用程式做為部署目標。</span><span class="sxs-lookup"><span data-stu-id="413fa-138">Azure publishing enhanced tooinclude Azure API Apps as a deployment target.</span></span>
* <span data-ttu-id="413fa-139">API 的應用程式佈建功能 tooenable 使用者與應用程式開發介面應用程式建立佈建功能。</span><span class="sxs-lookup"><span data-stu-id="413fa-139">API Apps provisioning functionality tooenable users with API App creation and provisioning functionality.</span></span>
* <span data-ttu-id="413fa-140">伺服器總管變更 tooreflect 新應用程式服務 節點，依資源群組分組的 Web、 行動裝置版和 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="413fa-140">Server Explorer changed tooreflect new App Service node, with Web, Mobile, and API apps grouped by Resource Group.</span></span>
* <span data-ttu-id="413fa-141">加入 Azure API 應用程式用戶端軌跡加入 toomost C# 專案，將會啟用自動產生的 Swagger 啟用 API 應用程式在使用者的 Azure 訂用帳戶中執行。</span><span class="sxs-lookup"><span data-stu-id="413fa-141">Add Azure API App Client gesture added toomost C# projects that will enable automatic generation of Swagger-enabled API Apps running in a user’s Azure subscription.</span></span>
* <span data-ttu-id="413fa-142">[伺服器總管] 中的 API Apps 工具和 App Service 節點僅可以在 Visual Studio 2013 中使用。</span><span class="sxs-lookup"><span data-stu-id="413fa-142">API Apps tooling and App Service nodes in Server Explorer are available in Visual Studio 2013 only.</span></span> 

## <a name="azure-resource-manager-tools-updates"></a><span data-ttu-id="413fa-143">Azure 資源管理員工具更新</span><span class="sxs-lookup"><span data-stu-id="413fa-143">Azure Resource Manager Tools updates</span></span>
<span data-ttu-id="413fa-144">hello Azure 資源管理員工具已更新的 tooinclude 範本的虛擬機器、 網路和存放裝置。</span><span class="sxs-lookup"><span data-stu-id="413fa-144">hello Azure resource manager tools have been updated tooinclude templates for Virtual Machines, Networking and Storage.</span></span> <span data-ttu-id="413fa-145">hello JSON 的編輯體驗已經更新的 tooinclude 新大綱檢視的範本與 hello 能力 tooedit hello 範本使用 JSON 片段。</span><span class="sxs-lookup"><span data-stu-id="413fa-145">hello JSON editing experience has been updated tooinclude a new outline view for templates and hello ability tooedit hello templates using JSON snippets.</span></span> <span data-ttu-id="413fa-146">從 Visual Studio 部署的範本會使用與 hello 專案提供，因此 toohello 指令碼所做的變更將會使用由 Visual Studio 的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="413fa-146">Templates deployed from Visual Studio use a PowerShell script provided with hello project, so any changes made toohello script will be used by Visual Studio.</span></span>

## <a name="diagnostics-improvements-for-cloud-services"></a><span data-ttu-id="413fa-147">雲端服務的診斷改良功能</span><span class="sxs-lookup"><span data-stu-id="413fa-147">Diagnostics improvements for Cloud Services</span></span>
<span data-ttu-id="413fa-148">Azure SDK 2.6 再度支援收集 hello Azure 計算模擬器中的診斷記錄檔，並傳送 toodevelopment 儲存體。</span><span class="sxs-lookup"><span data-stu-id="413fa-148">Azure SDK 2.6 brings back support for collecting diagnostics logs in hello Azure compute emulator and transferring them toodevelopment storage.</span></span> <span data-ttu-id="413fa-149">任何診斷記錄 （包括應用程式追蹤記錄檔，追蹤 Windows (ETW) 記錄檔、 效能計數器、 基礎結構記錄檔和 windows 事件記錄檔的事件） 產生 hello 應用程式在 hello 模擬器中執行時可以是轉移的 toodevelopment診斷記錄正在本機電腦的儲存體 tooverify。</span><span class="sxs-lookup"><span data-stu-id="413fa-149">Any diagnostics logs (including application trace Logs, Event Tracing for Windows (ETW) logs, performance counters, infrastructure logs and windows event logs) generated when hello application is running in hello emulator can be transferred toodevelopment storage tooverify that your diagnostics logging is working on your local machine.</span></span> 

<span data-ttu-id="413fa-150">現在可以讓您更輕鬆 toouse 不同診斷儲存體帳戶不同環境的 hello 服務組態 (.cscfg) 檔中指定 hello 診斷儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="413fa-150">hello Diagnostics storage account can now be specified in hello service configuration (.cscfg) file making it easier toouse different diagnostics storage accounts for different environments.</span></span> <span data-ttu-id="413fa-151">有一些值得注意的差異之間 hello 連接字串在 Azure SDK 2.4 和 Azure SDK 2.6 中的運作方式。</span><span class="sxs-lookup"><span data-stu-id="413fa-151">There are some notable differences between how hello connection string worked in Azure SDK 2.4 and Azure SDK 2.6.</span></span> <span data-ttu-id="413fa-152">如需有關如何 toouse hello 診斷儲存體連接字串，以及它如何影響您的專案，請參閱[設定 Azure 雲端服務的診斷功能](http://go.microsoft.com/fwlink/?LinkID=532784)。</span><span class="sxs-lookup"><span data-stu-id="413fa-152">For more information on how toouse hello Diagnostics Storage connection string and how it impacts your projects see [Configuring Diagnostics for Azure Cloud Services](http://go.microsoft.com/fwlink/?LinkID=532784).</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="413fa-153">重大變更</span><span class="sxs-lookup"><span data-stu-id="413fa-153">Breaking changes</span></span>
### <a name="azure-resource-manager-tools"></a><span data-ttu-id="413fa-154">Azure 資源管理員工具</span><span class="sxs-lookup"><span data-stu-id="413fa-154">Azure Resource Manager Tools</span></span>
* <span data-ttu-id="413fa-155">hello**雲端部署專案**專案類型提供 hello Azure SDK 2.5 已重新命名過**Azure 資源群組**。</span><span class="sxs-lookup"><span data-stu-id="413fa-155">hello **Cloud Deployment Projects** project type available in hello Azure SDK 2.5 has been renamed too**Azure Resource Group**.</span></span>
* <span data-ttu-id="413fa-156">**雲端部署專案**2.6 中可用的 hello Azure SDK 2.5 中建立的專案類型，但從 Visual Studio 部署的 hello 範本將會失敗。</span><span class="sxs-lookup"><span data-stu-id="413fa-156">**Cloud Deployment Projects** type of projects created in hello Azure SDK 2.5 can be used in 2.6 but deploying hello template from Visual Studio will fail.</span></span> <span data-ttu-id="413fa-157">不過，部署以 hello PowerShell 指令碼仍可正常之前一樣。</span><span class="sxs-lookup"><span data-stu-id="413fa-157">However, deploying with hello PowerShell script will still work as it did previously.</span></span>  <span data-ttu-id="413fa-158">如需詳細資訊 toouse**雲端部署專案**在閱讀本 2.6[張貼](http://go.microsoft.com/fwlink/?LinkID=534086)。</span><span class="sxs-lookup"><span data-stu-id="413fa-158">For information on how toouse **Cloud Deployment Projects** in 2.6 read this [post](http://go.microsoft.com/fwlink/?LinkID=534086).</span></span>

## <a name="known-issues"></a><span data-ttu-id="413fa-159">已知問題</span><span class="sxs-lookup"><span data-stu-id="413fa-159">Known issues</span></span>
* <span data-ttu-id="413fa-160">收集診斷記錄檔中 hello 模擬器需要 64 位元作業系統。</span><span class="sxs-lookup"><span data-stu-id="413fa-160">Collecting diagnostics logs in hello emulator requires a 64-bit operating system.</span></span> <span data-ttu-id="413fa-161">在 32 位元的作業系統上執行時，將無法收集診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="413fa-161">Diagnostics logs will not be collected when running on a 32-bit operating system.</span></span> <span data-ttu-id="413fa-162">這並不會影響任何其他模擬器功能。</span><span class="sxs-lookup"><span data-stu-id="413fa-162">This does not affect any other emulator functionality.</span></span> 
* <span data-ttu-id="413fa-163">2015 年 4 月 29 日發行的 Azure SDK 2.6 有兩個問題：</span><span class="sxs-lookup"><span data-stu-id="413fa-163">Azure SDK 2.6 released on 4/29/2015 had two issues:</span></span> 
  
  * <span data-ttu-id="413fa-164">通用應用程式無法載入 Visual Studio 2015 中，hello 機器上安裝 Azure SDK 2.6 時。</span><span class="sxs-lookup"><span data-stu-id="413fa-164">Universal App could not be loaded in Visual Studio 2015 when Azure SDK 2.6 was installed on hello machine.</span></span>
  * <span data-ttu-id="413fa-165">在 Visual Studio 2013 和 Visual Studio 2015 的 Visual Studio 變得沒有回應，並損毀時顯示以 hello 訊息 「 模擬器設定診斷 」 對話方塊，偵錯雲端服務專案會失敗。</span><span class="sxs-lookup"><span data-stu-id="413fa-165">Debugging a Cloud Service project would fail in Visual Studio 2013 and Visual Studio 2015 where Visual Studio becomes unresponsive and crashes while displaying a dialog box with hello message "Configuring diagnostics for emulator".</span></span>
    
    <span data-ttu-id="413fa-166">更新 tooAzure SDK 2.6 已於 2015 年 5 月 18 日發行。</span><span class="sxs-lookup"><span data-stu-id="413fa-166">An update tooAzure SDK 2.6 was released on 5/18/2015.</span></span> <span data-ttu-id="413fa-167">hello 更新的版本是 2.6.30508.1601;它包含如上面所述的兩個問題的修正程式。</span><span class="sxs-lookup"><span data-stu-id="413fa-167">hello updated version is 2.6.30508.1601; it contains fixes for two issues described above.</span></span> <span data-ttu-id="413fa-168">您可以識別 hello hello 組建 SDK，從 控制台-> 程式和功能-> Microsoft Azure Tools for Microsoft 的 Visual Studio 2013 – 而 v 2.6。</span><span class="sxs-lookup"><span data-stu-id="413fa-168">You can identify hello build of hello SDK from Control Panel -> Programs and Features -> Microsoft Azure Tools for Microsoft Visual Studio 2013 – v 2.6.</span></span> <span data-ttu-id="413fa-169">hello 版本 欄會顯示 hello 組建編號。</span><span class="sxs-lookup"><span data-stu-id="413fa-169">hello Version column will display hello build number.</span></span>
    
    <span data-ttu-id="413fa-170">如果您仍然遇到 hello 上述問題，安裝 hello 最新版本的 hello Azure SDK 2.6 [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409)， [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)或[VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="413fa-170">If you are still facing hello above issues, install hello latest version of hello Azure 2.6 SDK for [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).</span></span>

## <a name="see-also"></a><span data-ttu-id="413fa-171">另請參閱</span><span class="sxs-lookup"><span data-stu-id="413fa-171">See Also</span></span>
[<span data-ttu-id="413fa-172">支援和 hello Azure SDK for.NET 和 Api 的停用資訊</span><span class="sxs-lookup"><span data-stu-id="413fa-172">Support and Retirement Information for hello Azure SDK for .NET and APIs</span></span>](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

