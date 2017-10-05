---
title: "Azure SDK for .NET 2.6 版本資訊"
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
ms.openlocfilehash: 21817b09440fc98a54dc45c9129d104b01fa387d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a><span data-ttu-id="73ca3-103">Azure SDK for .NET 2.6 版本資訊</span><span class="sxs-lookup"><span data-stu-id="73ca3-103">Azure SDK for .NET 2.6 Release Notes</span></span>
<span data-ttu-id="73ca3-104">本文件包含 Azure SDK for .NET 2.6 版的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="73ca3-104">This document contains the release notes for the Azure SDK for .NET 2.6 release.</span></span> 

<span data-ttu-id="73ca3-105">您可以使用 Azure SDK 2.6 開發以 .NET 4.5.2 或.NET 4.6 為目標的雲端服務應用程式 (PaaS)，前提是您必須在雲端服務角色上手動安裝目標 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="73ca3-105">With Azure SDK 2.6 you can develop cloud service applications (PaaS) targeting .NET 4.5.2 or .NET 4.6 provided that you manually install the target .NET Framework on the Cloud Service Role.</span></span> <span data-ttu-id="73ca3-106">請參閱 [在雲端服務角色上安裝 .NET](http://go.microsoft.com/fwlink/?LinkID=309796)。</span><span class="sxs-lookup"><span data-stu-id="73ca3-106">See [Install .NET on a Cloud Service Role](http://go.microsoft.com/fwlink/?LinkID=309796).</span></span>

## <a name="service-bus-updates"></a><span data-ttu-id="73ca3-107">服務匯流排更新</span><span class="sxs-lookup"><span data-stu-id="73ca3-107">Service Bus updates</span></span>
* <span data-ttu-id="73ca3-108">事件中心：</span><span class="sxs-lookup"><span data-stu-id="73ca3-108">Event Hubs:</span></span> 
  
  * <span data-ttu-id="73ca3-109">現在藉由公開事件中心的其他發行者端點，可在傳送事件時提供目標存取控制。</span><span class="sxs-lookup"><span data-stu-id="73ca3-109">Now allows targeted access control when sending events by exposing additional publisher endpoint for Event Hubs.</span></span>
  * <span data-ttu-id="73ca3-110">其他加入至事件中心功能的穩定性和改良。</span><span class="sxs-lookup"><span data-stu-id="73ca3-110">Additional stability and improvement added to Event Hubs feature.</span></span>
  * <span data-ttu-id="73ca3-111">在訊息和事件中心內，加入 WebSocket 上的 Amqp 通訊協定支援。</span><span class="sxs-lookup"><span data-stu-id="73ca3-111">Adding support of Amqp protocol over WebSocket for messaging and Event Hubs.</span></span>

## <a name="hdinsight-tools-for-visual-studio-updates"></a><span data-ttu-id="73ca3-112">HDInsight Tools for Visual Studio 更新</span><span class="sxs-lookup"><span data-stu-id="73ca3-112">HDInsight Tools for Visual Studio updates</span></span>
* <span data-ttu-id="73ca3-113">**IntelliSense 的增強功能**：遠端中繼資料建議</span><span class="sxs-lookup"><span data-stu-id="73ca3-113">**IntelliSense enhancement**: remote metadata suggestion</span></span>
  
    <span data-ttu-id="73ca3-114">HDInsight Tools for Visual Studio 現在支援在編輯 Hive 指令碼時取得遠端中繼資料。</span><span class="sxs-lookup"><span data-stu-id="73ca3-114">Now HDInsight Tools for Visual Studio supports getting remote metadata when you are editing your Hive script.</span></span> <span data-ttu-id="73ca3-115">例如，您可以輸入**選取 * FROM**且將顯示所有資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="73ca3-115">For example, you can type **SELECT * FROM** and all the table names will be shown.</span></span> <span data-ttu-id="73ca3-116">此外，資料行名稱會在指定資料表之後顯示。</span><span class="sxs-lookup"><span data-stu-id="73ca3-116">Also, the column names will be shown after specifying a table.</span></span>
* <span data-ttu-id="73ca3-117">**HDInsight 模擬器支援**</span><span class="sxs-lookup"><span data-stu-id="73ca3-117">**HDInsight emulator support**</span></span>
  
    <span data-ttu-id="73ca3-118">HDInsight Tools for Visual Studio 現在支援連接到 HDInsight 模擬器，方便您在不產生任何費用的情況下本機開發 Hive 指令碼，然後對您的 HDInsight 叢集執行這些指令碼。</span><span class="sxs-lookup"><span data-stu-id="73ca3-118">Now HDInsight Tools for Visual Studio support connecting to HDInsight emulator, so you could develop your Hive scripts locally without introducing any cost, then execute those scripts against your HDInsight clusters.</span></span> 
  
    <span data-ttu-id="73ca3-119">如需詳細資訊，請參閱 [本手冊](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="73ca3-119">For more information, refer to [this manual](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).</span></span>
* <span data-ttu-id="73ca3-120">**HDInsight Tools for Visual Studio 支援一般的 Hadoop 叢集** (預覽)</span><span class="sxs-lookup"><span data-stu-id="73ca3-120">**HDInsight Tools for Visual Studio support for generic Hadoop clusters** (Preview)</span></span>
  
    <span data-ttu-id="73ca3-121">HDInsight Tools for Visual Studio 現在支援一般的 Hadoop 叢集，因此您可以使用 HDInsight Tools for Visual Studio 來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="73ca3-121">Now HDInsight Tools for Visual Studio support generic Hadoop clusters, so you can use HDInsight Tools for Visual Studio to do the following:</span></span>
  
  * <span data-ttu-id="73ca3-122">連接到您的叢集、</span><span class="sxs-lookup"><span data-stu-id="73ca3-122">connect to your cluster,</span></span> 
  * <span data-ttu-id="73ca3-123">使用增強式 IntelliSense/自動完成支援來撰寫 Hive 查詢、</span><span class="sxs-lookup"><span data-stu-id="73ca3-123">write Hive query with enhanced IntelliSense/auto-completion support,</span></span> 
  * <span data-ttu-id="73ca3-124">使用直覺式 UI 來檢視叢集中的所有工作。</span><span class="sxs-lookup"><span data-stu-id="73ca3-124">view all the jobs in your cluster with an intuitive UI.</span></span> 
    
    <span data-ttu-id="73ca3-125">如需詳細資訊，請參閱 [本手冊](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="73ca3-125">For more information, refer to [this manual](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).</span></span>

## <a name="in-role-cache-updates"></a><span data-ttu-id="73ca3-126">角色中快取更新</span><span class="sxs-lookup"><span data-stu-id="73ca3-126">In-Role Cache updates</span></span>
* <span data-ttu-id="73ca3-127">**In-Role Cache** 已更新為使用 **Microsoft Azure 儲存體 SDK** 4.3 版本。</span><span class="sxs-lookup"><span data-stu-id="73ca3-127">**In-Role Cache** was updated to use **Microsoft Azure Storage SDK** version 4.3.</span></span> <span data-ttu-id="73ca3-128">過去， **角色中快取** 一直是使用 Azure 儲存體 SDK 1.7 版本。</span><span class="sxs-lookup"><span data-stu-id="73ca3-128">Until now, the **In-Role Cache** was using Azure Storage SDK version 1.7.</span></span>
  
    <span data-ttu-id="73ca3-129">使用 Azure SDK 2.5 或更低版本的客戶應該更新到 Azure SDK 2.6，並移至新的 Azure 儲存體 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="73ca3-129">Customers using Azure SDK 2.5 or below should update to Azure SDK 2.6 and move to the new version of Azure Storage SDK.</span></span> 
  
    <span data-ttu-id="73ca3-130">目前 Azure 儲存體版本 2011-08-18 己預計於 2016 年 8 月 1 日移除。</span><span class="sxs-lookup"><span data-stu-id="73ca3-130">At this time Azure Storage version 2011-08-18 is scheduled to be removed August 1, 2016.</span></span> <span data-ttu-id="73ca3-131">任何將 In-Role Cache 從 Azure SDK 2.5 或較低版本移轉到 Azure SDK 2.6 的作業都必須在這個時間前完成。</span><span class="sxs-lookup"><span data-stu-id="73ca3-131">Any migrations of In-Role Cache from Azure SDK 2.5 or below to 2.6 must be complete by this time.</span></span> <span data-ttu-id="73ca3-132">如需 版本 Azure 儲存體版本 2011-08-18 的詳細資訊，請參閱 [Microsoft Azure 儲存體服務版本移除更新：延期到 2016 年](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx)。</span><span class="sxs-lookup"><span data-stu-id="73ca3-132">For more information on the retirement of Azure Storage version 2011-08-18, see [Microsoft Azure Storage Service Version Removal Update: Extension to 2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73ca3-133">我們現在宣布將在 2016 年 11 月 30 日淘汰「Azure 受管理的快取服務」和 Azure In-Role Cache。</span><span class="sxs-lookup"><span data-stu-id="73ca3-133">We’re announcing the November 30, 2016, retirement for Azure Managed Cache Service and Azure In-Role Cache.</span></span> <span data-ttu-id="73ca3-134">我們建議您移轉到 Azure Redis Cache 以為這次淘汰做準備。</span><span class="sxs-lookup"><span data-stu-id="73ca3-134">We recommend that you migrate to Azure Redis Cache in preparation for this retirement.</span></span> <span data-ttu-id="73ca3-135">如需日期和移轉指南的詳細資訊，請參閱 [我適合使用哪個 Azure 快取服務？](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)</span><span class="sxs-lookup"><span data-stu-id="73ca3-135">For more information on dates and migration guidance, see [Which Azure Cache offering is right for me?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)</span></span>
> 
> 

## <a name="azure-app-service-tools"></a><span data-ttu-id="73ca3-136">Azure App Service 工具</span><span class="sxs-lookup"><span data-stu-id="73ca3-136">Azure App Service Tools</span></span>
<span data-ttu-id="73ca3-137">Azure SDK 2.6 版中已更新下列項目。</span><span class="sxs-lookup"><span data-stu-id="73ca3-137">The following items were updated in the Azure SDK 2.6 release.</span></span>

* <span data-ttu-id="73ca3-138">已增強 Azure 發行的功能，以將 Azure API Apps 納為部署目標。</span><span class="sxs-lookup"><span data-stu-id="73ca3-138">Azure publishing enhanced to include Azure API Apps as a deployment target.</span></span>
* <span data-ttu-id="73ca3-139">API Apps 佈建功能提供使用者 API 應用程式的建立和佈建功能。</span><span class="sxs-lookup"><span data-stu-id="73ca3-139">API Apps provisioning functionality to enable users with API App creation and provisioning functionality.</span></span>
* <span data-ttu-id="73ca3-140">將 [伺服器總管] 使用按資源群組分組的 Web、行動及 API 應用程式加以變更，以反映新的 App Service 節點。</span><span class="sxs-lookup"><span data-stu-id="73ca3-140">Server Explorer changed to reflect new App Service node, with Web, Mobile, and API apps grouped by Resource Group.</span></span>
* <span data-ttu-id="73ca3-141">加入已新增至大部分 C# 專案的 Azure API Apps 用戶端手勢，將可自動產生啟用 Swagger 功能並可在使用者的 Azure 訂用帳戶中執行的 API Apps。</span><span class="sxs-lookup"><span data-stu-id="73ca3-141">Add Azure API App Client gesture added to most C# projects that will enable automatic generation of Swagger-enabled API Apps running in a user’s Azure subscription.</span></span>
* <span data-ttu-id="73ca3-142">[伺服器總管] 中的 API Apps 工具和 App Service 節點僅可以在 Visual Studio 2013 中使用。</span><span class="sxs-lookup"><span data-stu-id="73ca3-142">API Apps tooling and App Service nodes in Server Explorer are available in Visual Studio 2013 only.</span></span> 

## <a name="azure-resource-manager-tools-updates"></a><span data-ttu-id="73ca3-143">Azure 資源管理員工具更新</span><span class="sxs-lookup"><span data-stu-id="73ca3-143">Azure Resource Manager Tools updates</span></span>
<span data-ttu-id="73ca3-144">Azure 資源管理員工具已經更新，以納入虛擬機器、網路和儲存體的範本。</span><span class="sxs-lookup"><span data-stu-id="73ca3-144">The Azure resource manager tools have been updated to include templates for Virtual Machines, Networking and Storage.</span></span> <span data-ttu-id="73ca3-145">JSON 編輯體驗已經更新，以納入新的範本大綱檢視以及使用 JSON 程式碼片段編輯範本的能力。</span><span class="sxs-lookup"><span data-stu-id="73ca3-145">The JSON editing experience has been updated to include a new outline view for templates and the ability to edit the templates using JSON snippets.</span></span> <span data-ttu-id="73ca3-146">從 Visual Studio 部署的範本會使用專案所提供的 PowerShell 指令碼，以便 Visual Studio 使用針對指令碼所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="73ca3-146">Templates deployed from Visual Studio use a PowerShell script provided with the project, so any changes made to the script will be used by Visual Studio.</span></span>

## <a name="diagnostics-improvements-for-cloud-services"></a><span data-ttu-id="73ca3-147">雲端服務的診斷改良功能</span><span class="sxs-lookup"><span data-stu-id="73ca3-147">Diagnostics improvements for Cloud Services</span></span>
<span data-ttu-id="73ca3-148">Azure SDK 2.6 重新提供針對收集 Azure 計算模擬器中的診斷記錄檔，並將它們傳送到開發儲存體的支援。</span><span class="sxs-lookup"><span data-stu-id="73ca3-148">Azure SDK 2.6 brings back support for collecting diagnostics logs in the Azure compute emulator and transferring them to development storage.</span></span> <span data-ttu-id="73ca3-149">在模擬器中執行應用程式時所產生的任何診斷記錄檔 (包括應用程式追蹤記錄檔、Windows 事件追蹤 (ETW) 記錄檔、效能計數器、基礎結構記錄檔和 Windows 事件記錄檔) 會被傳輸到開發儲存體，以確認診斷記錄功能可在本機電腦上運作。</span><span class="sxs-lookup"><span data-stu-id="73ca3-149">Any diagnostics logs (including application trace Logs, Event Tracing for Windows (ETW) logs, performance counters, infrastructure logs and windows event logs) generated when the application is running in the emulator can be transferred to development storage to verify that your diagnostics logging is working on your local machine.</span></span> 

<span data-ttu-id="73ca3-150">您現在可以在服務組態 (.cscfg) 檔中指定診斷儲存體帳戶，讓您輕而易舉便可在不同的環境中使用不同的診斷儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="73ca3-150">The Diagnostics storage account can now be specified in the service configuration (.cscfg) file making it easier to use different diagnostics storage accounts for different environments.</span></span> <span data-ttu-id="73ca3-151">連接字串在 Azure SDK 2.4 和 Azure SDK 2.6 中的運作方式有一些顯著的差異。</span><span class="sxs-lookup"><span data-stu-id="73ca3-151">There are some notable differences between how the connection string worked in Azure SDK 2.4 and Azure SDK 2.6.</span></span> <span data-ttu-id="73ca3-152">如需有關如何使用診斷儲存體連接字串，以及它會如何影響您的專案等詳細資訊，請參閱 [設定 Azure 雲端服務的診斷](http://go.microsoft.com/fwlink/?LinkID=532784)。</span><span class="sxs-lookup"><span data-stu-id="73ca3-152">For more information on how to use the Diagnostics Storage connection string and how it impacts your projects see [Configuring Diagnostics for Azure Cloud Services](http://go.microsoft.com/fwlink/?LinkID=532784).</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="73ca3-153">重大變更</span><span class="sxs-lookup"><span data-stu-id="73ca3-153">Breaking changes</span></span>
### <a name="azure-resource-manager-tools"></a><span data-ttu-id="73ca3-154">Azure 資源管理員工具</span><span class="sxs-lookup"><span data-stu-id="73ca3-154">Azure Resource Manager Tools</span></span>
* <span data-ttu-id="73ca3-155">Azure SDK 2.5 所提供的**雲端部署專案**專案類型已重新命名為 **Azure 資源群組**。</span><span class="sxs-lookup"><span data-stu-id="73ca3-155">The **Cloud Deployment Projects** project type available in the Azure SDK 2.5 has been renamed to **Azure Resource Group**.</span></span>
* <span data-ttu-id="73ca3-156">**雲端部署專案**  專案類型仍然可以在 2.6 中使用，但從 Visual Studio 部署範本將會失敗。</span><span class="sxs-lookup"><span data-stu-id="73ca3-156">**Cloud Deployment Projects** type of projects created in the Azure SDK 2.5 can be used in 2.6 but deploying the template from Visual Studio will fail.</span></span> <span data-ttu-id="73ca3-157">不過，使用 PowerShell 指令碼進行部署仍可像先前一樣運作。</span><span class="sxs-lookup"><span data-stu-id="73ca3-157">However, deploying with the PowerShell script will still work as it did previously.</span></span>  <span data-ttu-id="73ca3-158">如需如何在 2.6 中使用 **雲端部署專案** 的相關資訊，請閱讀 [本文](http://go.microsoft.com/fwlink/?LinkID=534086)。</span><span class="sxs-lookup"><span data-stu-id="73ca3-158">For information on how to use **Cloud Deployment Projects** in 2.6 read this [post](http://go.microsoft.com/fwlink/?LinkID=534086).</span></span>

## <a name="known-issues"></a><span data-ttu-id="73ca3-159">已知問題</span><span class="sxs-lookup"><span data-stu-id="73ca3-159">Known issues</span></span>
* <span data-ttu-id="73ca3-160">收集模擬器中的診斷記錄檔需要 64 位元的作業系統。</span><span class="sxs-lookup"><span data-stu-id="73ca3-160">Collecting diagnostics logs in the emulator requires a 64-bit operating system.</span></span> <span data-ttu-id="73ca3-161">在 32 位元的作業系統上執行時，將無法收集診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="73ca3-161">Diagnostics logs will not be collected when running on a 32-bit operating system.</span></span> <span data-ttu-id="73ca3-162">這並不會影響任何其他模擬器功能。</span><span class="sxs-lookup"><span data-stu-id="73ca3-162">This does not affect any other emulator functionality.</span></span> 
* <span data-ttu-id="73ca3-163">2015 年 4 月 29 日發行的 Azure SDK 2.6 有兩個問題：</span><span class="sxs-lookup"><span data-stu-id="73ca3-163">Azure SDK 2.6 released on 4/29/2015 had two issues:</span></span> 
  
  * <span data-ttu-id="73ca3-164">電腦上安裝有 Azure SDK 2.6 時無法在 Visual Studio 2015 載入通用應用程式。</span><span class="sxs-lookup"><span data-stu-id="73ca3-164">Universal App could not be loaded in Visual Studio 2015 when Azure SDK 2.6 was installed on the machine.</span></span>
  * <span data-ttu-id="73ca3-165">在 Visual Studio 2013 和 Visual Studio 2015 偵錯雲端服務專案將會失敗，此時 Visual Studio 會變得沒有回應並當機，同時還會顯示內有「正在設定模擬器的診斷」訊息的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="73ca3-165">Debugging a Cloud Service project would fail in Visual Studio 2013 and Visual Studio 2015 where Visual Studio becomes unresponsive and crashes while displaying a dialog box with the message "Configuring diagnostics for emulator".</span></span>
    
    <span data-ttu-id="73ca3-166">2015 年 5 月 18 日發行了 Azure SDK 2.6 的更新。</span><span class="sxs-lookup"><span data-stu-id="73ca3-166">An update to Azure SDK 2.6 was released on 5/18/2015.</span></span> <span data-ttu-id="73ca3-167">更新的版本是 2.6.30508.1601；內含上述兩個問題的修正程式。</span><span class="sxs-lookup"><span data-stu-id="73ca3-167">The updated version is 2.6.30508.1601; it contains fixes for two issues described above.</span></span> <span data-ttu-id="73ca3-168">您可以從 [控制台] -> [程式和功能]-> [Microsoft Azure Tools for Microsoft Visual Studio 2013 – v 2.6] 識別 SDK 的組建。</span><span class="sxs-lookup"><span data-stu-id="73ca3-168">You can identify the build of the SDK from Control Panel -> Programs and Features -> Microsoft Azure Tools for Microsoft Visual Studio 2013 – v 2.6.</span></span> <span data-ttu-id="73ca3-169">[版本] 欄中會顯示組建編號。</span><span class="sxs-lookup"><span data-stu-id="73ca3-169">The Version column will display the build number.</span></span>
    
    <span data-ttu-id="73ca3-170">如果您仍會遇到上述問題，請為 [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409)、[VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) 或 [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409) 安裝最新版的 Azure 2.6 SDK。</span><span class="sxs-lookup"><span data-stu-id="73ca3-170">If you are still facing the above issues, install the latest version of the Azure 2.6 SDK for [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).</span></span>

## <a name="see-also"></a><span data-ttu-id="73ca3-171">另請參閱</span><span class="sxs-lookup"><span data-stu-id="73ca3-171">See Also</span></span>
[<span data-ttu-id="73ca3-172">Azure SDK for .NET 和 API 的支援和停用資訊</span><span class="sxs-lookup"><span data-stu-id="73ca3-172">Support and Retirement Information for the Azure SDK for .NET and APIs</span></span>](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

