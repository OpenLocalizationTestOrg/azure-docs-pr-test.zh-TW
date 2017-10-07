---
title: "Azure CDN 的 aaaLog 分析 |Microsoft 文件"
description: "客戶可以啟用 Azure CDN 的記錄分析功能。"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="019ee-103">Azure CDN 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="019ee-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="019ee-104">在您的應用程式啟用 CDN 之後, 將可能 toomonitor hello CDN 使用方式，檢查您傳遞的 hello 健全狀況，然後疑難排解潛在問題。</span><span class="sxs-lookup"><span data-stu-id="019ee-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="019ee-105">Azure CDN 利用 [CDN 核心分析](cdn-analyze-usage-patterns.md)和[診斷記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)來提供這些功能</span><span class="sxs-lookup"><span data-stu-id="019ee-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="019ee-106">CDN 核心分析</span><span class="sxs-lookup"><span data-stu-id="019ee-106">CDN Core Analytics</span></span>
<span data-ttu-id="019ee-107">以目前 Azure CDN 使用者與 Verizon 標準或進階設定檔，您已無法 tooview 核心分析採用 hello 補充入口網站可透過 hello 「 管理 」 選項從 hello Azure 入口網站存取。</span><span class="sxs-lookup"><span data-stu-id="019ee-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="019ee-108">Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="019ee-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="019ee-109">透過這項新功能，您現在可以檢視核心分析，並將它們儲存到一或多個目的地，包括：</span><span class="sxs-lookup"><span data-stu-id="019ee-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="019ee-110">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="019ee-110">Azure Storage account</span></span>
 - <span data-ttu-id="019ee-111">Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="019ee-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="019ee-112">OMS Log Analytics 存放庫</span><span class="sxs-lookup"><span data-stu-id="019ee-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="019ee-113">這項功能適用於所有屬於 tooVerizon （Standard 和 Premium） 和 （標準） Akamai CDN 設定檔的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="019ee-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="019ee-114">診斷記錄檔可讓您從您的 CDN 端點 tooa 不同的來源 tooexport 基本的使用計量，讓您可以使用這些自訂的方式。</span><span class="sxs-lookup"><span data-stu-id="019ee-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="019ee-115">例如，您可以執行下列類型的資料匯出 hello:</span><span class="sxs-lookup"><span data-stu-id="019ee-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="019ee-116">匯出資料 tooblob 儲存、 匯出 tooCSV，並產生圖形在 excel 中。</span><span class="sxs-lookup"><span data-stu-id="019ee-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="019ee-117">匯出資料 tooevent 中樞，並與其他 azure 服務的資料相互關聯。</span><span class="sxs-lookup"><span data-stu-id="019ee-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="019ee-118">匯出資料 toolog 分析和檢視資料在您自己的 OMS 工作空間中</span><span class="sxs-lookup"><span data-stu-id="019ee-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="019ee-119">hello 下圖顯示典型的 CDN 核心分析檢視資料。</span><span class="sxs-lookup"><span data-stu-id="019ee-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="019ee-121">*圖 1 - CDN 核心分析檢視*</span><span class="sxs-lookup"><span data-stu-id="019ee-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="019ee-122">下列逐步解說的 hello 經歷 hello 核心分析資料，在啟用 「 hello 」 功能與傳遞 toovarious 目的地，以及從這些目的地使用所需步驟的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="019ee-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="019ee-123">使用 Azure 入口網站啟用記錄</span><span class="sxs-lookup"><span data-stu-id="019ee-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="019ee-124">hello 診斷記錄檔已**關閉**預設。</span><span class="sxs-lookup"><span data-stu-id="019ee-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="019ee-125">請遵循以下 tooenable CDN 核心分析記錄 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="019ee-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="019ee-126">登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="019ee-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="019ee-127">如果您尚未為您的工作流程啟用 CDN，請先[啟用 Azure CDN](cdn-create-new-endpoint.md)，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="019ee-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="019ee-128">在 hello 入口網站中，瀏覽過**的 CDN 設定檔**。</span><span class="sxs-lookup"><span data-stu-id="019ee-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="019ee-129">選取的 CDN 設定檔，然後選取您想 tooenable hello CDN 端點**診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="019ee-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="019ee-131">跳過**診斷記錄檔**刀鋒視窗底下**監視**區段，然後變更 hello 狀態太**上**。</span><span class="sxs-lookup"><span data-stu-id="019ee-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="019ee-133">使用 Azure 儲存體來啟用記錄功能</span><span class="sxs-lookup"><span data-stu-id="019ee-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="019ee-134">toouse Azure 儲存體 toostore hello 記錄檔，選取**封存 tooa 儲存體帳戶**，選取 保留天數，然後按一下**CoreAnalytics**下**記錄**。</span><span class="sxs-lookup"><span data-stu-id="019ee-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="019ee-136">*圖 2 - 使用 Azure 儲存體進行記錄*</span><span class="sxs-lookup"><span data-stu-id="019ee-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="019ee-137">使用 OMS Log Analytics 進行記錄</span><span class="sxs-lookup"><span data-stu-id="019ee-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="019ee-138">toouse OMS 記錄分析 toostore hello 記錄檔，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="019ee-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="019ee-139">從 hello**診斷記錄檔**刀鋒視窗底下**監視**，選取**傳送 tooLog 分析**從</span><span class="sxs-lookup"><span data-stu-id="019ee-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="019ee-141">在設定，即可設定 hello 記錄分析記錄。</span><span class="sxs-lookup"><span data-stu-id="019ee-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="019ee-142">這會帶您 tooa 對話方塊，您可以在其中選取先前的工作區或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="019ee-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="019ee-144">按一下 [建立新工作區]。</span><span class="sxs-lookup"><span data-stu-id="019ee-144">Click **Create New Workspace**.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="019ee-146">接下來，您必須選取新的工作區名稱、現有的訂用帳戶、資源群組 (新的或現有的)、位置和定價層。</span><span class="sxs-lookup"><span data-stu-id="019ee-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="019ee-147">您可以釘選此組態 tooyour 儀表板的 hello 選擇。</span><span class="sxs-lookup"><span data-stu-id="019ee-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="019ee-148">按一下 [確定] toocomplete hello 組態。</span><span class="sxs-lookup"><span data-stu-id="019ee-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="019ee-149">接下來，您應該會看到工作區上顯示您的 OMS 工作區名稱與資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="019ee-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="019ee-150">這些名稱必須是唯一的，而且只能使用字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="019ee-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="019ee-151">不允許使用空格和底線。</span><span class="sxs-lookup"><span data-stu-id="019ee-151">Spaces and underscores are not allowed.</span></span> 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="019ee-153">接下來，您會取得簡短訊息，指出已建立您的工作區，並將您返回 tooyour 記錄 組態畫面中。</span><span class="sxs-lookup"><span data-stu-id="019ee-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="019ee-154">您可以確認您的記錄分析工作區的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="019ee-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="019ee-156">在您設定 hello 記錄分析設定，請確定您也檢查 CDN 記錄的 hello CoreAnalytics 方塊。</span><span class="sxs-lookup"><span data-stu-id="019ee-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="019ee-157">如果一切 tooyour 喜好，請按一下 hello**儲存**在 hello hello 組態對話方塊頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="019ee-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="019ee-159">hello**儲存**按鈕不再作用中，且該 hello 上/關閉按鈕現在是 ON，但藍色，而不是紫色。</span><span class="sxs-lookup"><span data-stu-id="019ee-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="019ee-160">如果您想 toosee 新的 OMS 工作區，移 tooyour Azure 入口網站儀表板，按一下 記錄分析工作區的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="019ee-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="019ee-161">接下來，您會看到您的工作區 （請確定 OMS 工作區會反白顯示 hello 左邊）。</span><span class="sxs-lookup"><span data-stu-id="019ee-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="019ee-162">按一下 hello OMS 入口網站磚 toosee hello OMS 儲存機制中的工作區。</span><span class="sxs-lookup"><span data-stu-id="019ee-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="019ee-164">您的 OMS 儲存機制已就緒 toolog 資料。</span><span class="sxs-lookup"><span data-stu-id="019ee-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="019ee-165">若要 tooconsume 該資料，您必須使用[項 OMS 解決方案](#consuming-oms-log-analytics-data)、 涵蓋在本文稍後。</span><span class="sxs-lookup"><span data-stu-id="019ee-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="019ee-166">如需有關記錄資料延遲的詳細資訊，請瀏覽[這裡](#log-data-delays)。</span><span class="sxs-lookup"><span data-stu-id="019ee-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="019ee-167">使用 PowerShell 啟用記錄</span><span class="sxs-lookup"><span data-stu-id="019ee-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="019ee-168">以下是有關如何透過 tooenable 和 get 診斷記錄 hello Azure PowerShell Cmdlet 的範例。</span><span class="sxs-lookup"><span data-stu-id="019ee-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="019ee-169">啟用儲存體帳戶中的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="019ee-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="019ee-170">先登入並選取訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="019ee-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="019ee-171">tooEnable 診斷記錄檔儲存體帳戶，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="019ee-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="019ee-172">tooEnable 診斷記錄檔中的 OMS 工作區中，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="019ee-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="019ee-173">從 Azure 儲存體取用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="019ee-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="019ee-174">本節描述的 hello CDN 核心分析的 hello 結構描述，這些組織內的 Azure 儲存體帳戶，並提供如何範例程式碼 toodownload hello 記錄 tooa CSV 檔案中。</span><span class="sxs-lookup"><span data-stu-id="019ee-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="019ee-175">使用 Microsoft Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="019ee-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="019ee-176">您可以從 hello Azure 儲存體帳戶存取 hello 核心分析資料之前，您必須先儲存體帳戶中的工具 tooaccess hello 內容。</span><span class="sxs-lookup"><span data-stu-id="019ee-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="019ee-177">Hello 市場中有數種工具可用，我們建議的其中一個 hello 是 hello Microsoft Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="019ee-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="019ee-178">您可以下載從 hello 工具[這裡](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="019ee-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="019ee-179">下載並安裝 hello 軟體設定之後 toouse hello 相同的 Azure 儲存體帳戶設定為目的地 toohello CDN 診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="019ee-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="019ee-180">開啟 [Microsoft Azure 儲存體總管]</span><span class="sxs-lookup"><span data-stu-id="019ee-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="019ee-181">找出 hello 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="019ee-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="019ee-182">移 toohello **[Blob 容器]**節點下這個儲存體帳戶，然後展開 [hello] 節點</span><span class="sxs-lookup"><span data-stu-id="019ee-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="019ee-183">名為選取的 hello 容器**"insights-記錄檔-coreanalytics"**然後按兩下該檔案</span><span class="sxs-lookup"><span data-stu-id="019ee-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="019ee-184">上 hello 右窗格從 hello 開始層級，如下所示，向上結果顯示**"resourceId ="**。</span><span class="sxs-lookup"><span data-stu-id="019ee-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="019ee-185">繼續按所有 hello 方法，直到您看到 hello 檔案**PT1H.json**。</span><span class="sxs-lookup"><span data-stu-id="019ee-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="019ee-186">請參閱下列附註說明 hello 路徑 hello。</span><span class="sxs-lookup"><span data-stu-id="019ee-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="019ee-187">每個 blob **PT1H.json**代表特定的 CDN 端點或自訂網域的一小時 hello 分析記錄檔。</span><span class="sxs-lookup"><span data-stu-id="019ee-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="019ee-188">hello 結構描述的 JSON 檔案的 hello 內容節將說明 hello 結構描述的 hello 核心分析記錄檔</span><span class="sxs-lookup"><span data-stu-id="019ee-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="019ee-189">**Blob 路徑格式**</span><span class="sxs-lookup"><span data-stu-id="019ee-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="019ee-190">Core Analytics 記錄每小時產生一次。</span><span class="sxs-lookup"><span data-stu-id="019ee-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="019ee-191">系統會將一小時的資料全部收集並儲存在單一 Azure Blob 內作為 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="019ee-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="019ee-192">hello 路徑 toothis Azure Blob 隨即出現，如同是階層式結構。</span><span class="sxs-lookup"><span data-stu-id="019ee-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="019ee-193">這是因為 hello 儲存體總管工具會解譯 '/' 做為目錄分隔符號，並顯示 hello 階層，為了方便起見。</span><span class="sxs-lookup"><span data-stu-id="019ee-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="019ee-194">實際上，hello 整個路徑只代表 hello blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="019ee-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="019ee-195">這個 hello blob 的名稱會遵循下列命名慣例的 hello</span><span class="sxs-lookup"><span data-stu-id="019ee-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="019ee-196">**欄位說明：**</span><span class="sxs-lookup"><span data-stu-id="019ee-196">**Description of fields:**</span></span>

|<span data-ttu-id="019ee-197">value</span><span class="sxs-lookup"><span data-stu-id="019ee-197">value</span></span>|<span data-ttu-id="019ee-198">說明</span><span class="sxs-lookup"><span data-stu-id="019ee-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="019ee-199">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="019ee-199">Subscription ID</span></span>    |<span data-ttu-id="019ee-200">Hello Azure 訂用帳戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="019ee-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="019ee-201">這是 hello Guid 格式。</span><span class="sxs-lookup"><span data-stu-id="019ee-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="019ee-202">資源</span><span class="sxs-lookup"><span data-stu-id="019ee-202">Resource</span></span> |<span data-ttu-id="019ee-203">屬於 hello 資源群組 toowhich hello CDN 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="019ee-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="019ee-204">設定檔名稱</span><span class="sxs-lookup"><span data-stu-id="019ee-204">Profile Name</span></span> |<span data-ttu-id="019ee-205">Hello 的 CDN 設定檔的名稱</span><span class="sxs-lookup"><span data-stu-id="019ee-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="019ee-206">端點名稱</span><span class="sxs-lookup"><span data-stu-id="019ee-206">Endpoint Name</span></span> |<span data-ttu-id="019ee-207">Hello CDN 端點的名稱</span><span class="sxs-lookup"><span data-stu-id="019ee-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="019ee-208">Year</span><span class="sxs-lookup"><span data-stu-id="019ee-208">Year</span></span>|  <span data-ttu-id="019ee-209">hello 年，例如 2017年 4 位數表示法</span><span class="sxs-lookup"><span data-stu-id="019ee-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="019ee-210">月</span><span class="sxs-lookup"><span data-stu-id="019ee-210">Month</span></span>| <span data-ttu-id="019ee-211">hello 月份數字 2 位數表示。</span><span class="sxs-lookup"><span data-stu-id="019ee-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="019ee-212">01 = 一月...12 =十二月</span><span class="sxs-lookup"><span data-stu-id="019ee-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="019ee-213">天</span><span class="sxs-lookup"><span data-stu-id="019ee-213">Day</span></span>|   <span data-ttu-id="019ee-214">2 位數 hello hello 月份的天數表示法</span><span class="sxs-lookup"><span data-stu-id="019ee-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="019ee-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="019ee-215">PT1H.json</span></span>| <span data-ttu-id="019ee-216">實際的 JSON 檔案儲存 hello 分析資料</span><span class="sxs-lookup"><span data-stu-id="019ee-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="019ee-217">匯出 hello 核心分析資料 tooa CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="019ee-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="019ee-218">toomake it 輕鬆 tooaccess hello 核心分析，我們提供的工具，可讓您為一般模式以逗號分隔的檔案格式，可以使用的 tooeasily 下載 hello JSON 檔案的範例程式碼建立的圖表或其他彙總。</span><span class="sxs-lookup"><span data-stu-id="019ee-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="019ee-219">以下是如何使用 hello 工具：</span><span class="sxs-lookup"><span data-stu-id="019ee-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="019ee-220">請瀏覽 hello github 連結： [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="019ee-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="019ee-221">下載 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="019ee-221">Download hello code</span></span>
3.  <span data-ttu-id="019ee-222">請依照下列指示 toocompile 和設定</span><span class="sxs-lookup"><span data-stu-id="019ee-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="019ee-223">執行 hello 工具</span><span class="sxs-lookup"><span data-stu-id="019ee-223">Run hello tool</span></span>
5.  <span data-ttu-id="019ee-224">產生的 CSV 檔案會顯示簡單的一般階層中的 hello 分析資料。</span><span class="sxs-lookup"><span data-stu-id="019ee-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="019ee-225">從 OMS Log Analytics 存放庫取用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="019ee-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="019ee-226">記錄分析是在 Operations Management Suite (OMS)，以監視您的雲端和內部部署環境 toomaintain 其可用性和效能的服務。</span><span class="sxs-lookup"><span data-stu-id="019ee-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="019ee-227">它會收集您的雲端和內部部署環境和其他監視工具 tooprovide 分析資源所產生的跨多個來源資料。</span><span class="sxs-lookup"><span data-stu-id="019ee-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="019ee-228">toouse 記錄分析，您必須[啟用記錄](#enable-logging-with-azure-storage)toohello Azure OMS 記錄分析儲存機制，這稍早在本文章中討論。</span><span class="sxs-lookup"><span data-stu-id="019ee-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="019ee-229">使用 hello OMS 儲存機制</span><span class="sxs-lookup"><span data-stu-id="019ee-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="019ee-230">下列圖表顯示 hello 架構的 hello 輸入和輸出 hello 儲存機制的 hello:</span><span class="sxs-lookup"><span data-stu-id="019ee-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![OMS Log Analytics 存放庫](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="019ee-232">*圖 3 - Log Analytics 存放庫*</span><span class="sxs-lookup"><span data-stu-id="019ee-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="019ee-233">您可以使用管理解決方案，在各種不同的方式顯示 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="019ee-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="019ee-234">您可以從 hello 取得管理解決方案[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions)。</span><span class="sxs-lookup"><span data-stu-id="019ee-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="019ee-235">您可以從 Azure marketplace 所提供安裝管理解決方案，依序按一下 hello**立即下載**在每個解決方案的 hello 底部的連結。</span><span class="sxs-lookup"><span data-stu-id="019ee-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="019ee-236">新增 OMS CDN 管理解決方案</span><span class="sxs-lookup"><span data-stu-id="019ee-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="019ee-237">請遵循這些步驟 tooadd 管理解決方案：</span><span class="sxs-lookup"><span data-stu-id="019ee-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="019ee-238">如果您尚未這樣做，請登入 toohello 使用您的 Azure 訂用帳戶的 Azure 入口網站，並移 tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="019ee-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="019ee-239">![Azure 儀表板](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="019ee-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="019ee-240">在 hello**新增**刀鋒視窗底下**Marketplace**，選取**監視 + 管理**。</span><span class="sxs-lookup"><span data-stu-id="019ee-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="019ee-242">在 hello**監視 + 管理**刀鋒視窗中，按一下 **查看所有**。</span><span class="sxs-lookup"><span data-stu-id="019ee-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="019ee-244">搜尋 hello [搜尋] 方塊中的 CDN。</span><span class="sxs-lookup"><span data-stu-id="019ee-244">Search for CDN in hello search box.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="019ee-246">選取 [Azure CDN 核心分析]。</span><span class="sxs-lookup"><span data-stu-id="019ee-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![檢視全部](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="019ee-248">按一下後**建立**，將會詢問 toocreate 新的 OMS 工作區，或使用現有的一個。</span><span class="sxs-lookup"><span data-stu-id="019ee-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![檢視全部](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="019ee-250">選取您之前建立的 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="019ee-250">Select hello workspace you created before.</span></span> <span data-ttu-id="019ee-251">然後，您會需要 tooadd 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="019ee-251">You then need tooadd an automation account.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="019ee-253">hello 下列畫面顯示 hello 自動化帳戶表單，您必須先填寫。</span><span class="sxs-lookup"><span data-stu-id="019ee-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![檢視全部](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="019ee-255">一旦您已經建立 hello 自動化帳戶，您就準備好 tooadd 您的方案。</span><span class="sxs-lookup"><span data-stu-id="019ee-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="019ee-256">按一下 hello**建立** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="019ee-256">Click hello **Create** button.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="019ee-258">您的方案現在已加入 tooyour 工作區。</span><span class="sxs-lookup"><span data-stu-id="019ee-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="019ee-259">返回 tooyour Azure 入口網站儀表板。</span><span class="sxs-lookup"><span data-stu-id="019ee-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="019ee-261">按一下 建立工作區中 tooyour toogo hello 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="019ee-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="019ee-262">按一下 hello **OMS 入口網站**磚 toosee 您 hello OMS 入口網站中的新方案。</span><span class="sxs-lookup"><span data-stu-id="019ee-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="019ee-264">您的 OMS 入口網站現在看起來應該像下列螢幕 hello:</span><span class="sxs-lookup"><span data-stu-id="019ee-264">Your OMS portal should now look like hello following screen:</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="019ee-266">為您的資料，按一下其中一個 hello 磚 toosee 數個檢視。</span><span class="sxs-lookup"><span data-stu-id="019ee-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="019ee-268">您可以向左捲動或向右 toosee 進一步磚 hello 資料表示個別的檢視。</span><span class="sxs-lookup"><span data-stu-id="019ee-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="019ee-269">按一下其中一個 hello 磚可讓您更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="019ee-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![檢視全部](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="019ee-271">優惠和定價層</span><span class="sxs-lookup"><span data-stu-id="019ee-271">Offers and pricing tiers</span></span>

<span data-ttu-id="019ee-272">您可以在[這裡](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)看到 OMS 管理解決方案的供應項目和定價層。</span><span class="sxs-lookup"><span data-stu-id="019ee-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="019ee-273">自訂檢視</span><span class="sxs-lookup"><span data-stu-id="019ee-273">Customizing views</span></span>

<span data-ttu-id="019ee-274">您可以使用來自訂 hello 檢視資料 hello**檢視表設計工具**。</span><span class="sxs-lookup"><span data-stu-id="019ee-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="019ee-275">請移 tooyour OMS 工作區，並依序按一下 hello 開始設計**檢視表設計工具**磚。</span><span class="sxs-lookup"><span data-stu-id="019ee-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![[檢視設計工具]](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="019ee-277">您可以拖曳和 hello 左從卸除類型的圖表和填入您想要上剩餘的 hello tooanalyze hello 資料詳細資料。</span><span class="sxs-lookup"><span data-stu-id="019ee-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![[檢視設計工具]](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="019ee-279">記錄資料延遲</span><span class="sxs-lookup"><span data-stu-id="019ee-279">Log data delays</span></span>

<span data-ttu-id="019ee-280">Verizon 記錄資料延遲</span><span class="sxs-lookup"><span data-stu-id="019ee-280">Verizon log data delays</span></span> | <span data-ttu-id="019ee-281">Akamai 記錄資料延遲</span><span class="sxs-lookup"><span data-stu-id="019ee-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="019ee-282">Verizon 記錄資料延遲是 1 小時，並佔用 too2 小時 toostart 端點傳播完成後出現。</span><span class="sxs-lookup"><span data-stu-id="019ee-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="019ee-283">Akamai 記錄資料是 24 小時的延遲，並會佔用 too2 小時 toostart 顯示它是建立超過 24 小時。</span><span class="sxs-lookup"><span data-stu-id="019ee-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="019ee-284">如果它最近建立的就可以在出現的 hello 記錄 toostart too25 小時。</span><span class="sxs-lookup"><span data-stu-id="019ee-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="019ee-285">CDN 核心分析的診斷記錄類型</span><span class="sxs-lookup"><span data-stu-id="019ee-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="019ee-286">目前，我們會提供僅核心分析記錄檔，其中包含顯示 HTTP 回應的統計資料和輸出統計資料從 hello CDN Pop/邊緣所見度量。</span><span class="sxs-lookup"><span data-stu-id="019ee-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="019ee-287">Core Analytics 計量詳細資料</span><span class="sxs-lookup"><span data-stu-id="019ee-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="019ee-288">下表中的 hello 顯示的 hello 核心分析記錄中可用的度量的清單。</span><span class="sxs-lookup"><span data-stu-id="019ee-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="019ee-289">並非所有提供者的所有計量皆可用，雖然這樣的差異極少。</span><span class="sxs-lookup"><span data-stu-id="019ee-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="019ee-290">hello 也下表顯示指定的度量是否可從提供者。</span><span class="sxs-lookup"><span data-stu-id="019ee-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="019ee-291">請注意 hello 度量，皆可用於在其上有流量的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="019ee-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="019ee-292">計量</span><span class="sxs-lookup"><span data-stu-id="019ee-292">Metric</span></span>                     | <span data-ttu-id="019ee-293">說明</span><span class="sxs-lookup"><span data-stu-id="019ee-293">Description</span></span>   | <span data-ttu-id="019ee-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="019ee-294">Verizon</span></span>  | <span data-ttu-id="019ee-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="019ee-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="019ee-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="019ee-296">RequestCountTotal</span></span>         |<span data-ttu-id="019ee-297">這段期間要求命中總數</span><span class="sxs-lookup"><span data-stu-id="019ee-297">Total number of request hits during this period</span></span>| <span data-ttu-id="019ee-298">是</span><span class="sxs-lookup"><span data-stu-id="019ee-298">Yes</span></span>  |<span data-ttu-id="019ee-299">是</span><span class="sxs-lookup"><span data-stu-id="019ee-299">Yes</span></span>   |
| <span data-ttu-id="019ee-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="019ee-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="019ee-301">產生 2xx HTTP 代碼 (例如 200、202) 的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="019ee-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="019ee-302">是</span><span class="sxs-lookup"><span data-stu-id="019ee-302">Yes</span></span>  |<span data-ttu-id="019ee-303">是</span><span class="sxs-lookup"><span data-stu-id="019ee-303">Yes</span></span>   |
| <span data-ttu-id="019ee-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="019ee-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="019ee-305">產生 3xx HTTP 代碼 (例如 300、302) 的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="019ee-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="019ee-306">是</span><span class="sxs-lookup"><span data-stu-id="019ee-306">Yes</span></span>  |<span data-ttu-id="019ee-307">是</span><span class="sxs-lookup"><span data-stu-id="019ee-307">Yes</span></span>   |
| <span data-ttu-id="019ee-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="019ee-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="019ee-309">產生 4xx HTTP 代碼 (例如 400、404) 的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="019ee-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="019ee-310">是</span><span class="sxs-lookup"><span data-stu-id="019ee-310">Yes</span></span>   |<span data-ttu-id="019ee-311">是</span><span class="sxs-lookup"><span data-stu-id="019ee-311">Yes</span></span>   |
| <span data-ttu-id="019ee-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="019ee-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="019ee-313">產生 5xx HTTP 代碼 (例如 500、504) 的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="019ee-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="019ee-314">是</span><span class="sxs-lookup"><span data-stu-id="019ee-314">Yes</span></span>  |<span data-ttu-id="019ee-315">是</span><span class="sxs-lookup"><span data-stu-id="019ee-315">Yes</span></span>   |
| <span data-ttu-id="019ee-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="019ee-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="019ee-317">所有其他 HTTP 代碼 (2xx-5xx 以外) 的計數</span><span class="sxs-lookup"><span data-stu-id="019ee-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="019ee-318">是</span><span class="sxs-lookup"><span data-stu-id="019ee-318">Yes</span></span>  |<span data-ttu-id="019ee-319">是</span><span class="sxs-lookup"><span data-stu-id="019ee-319">Yes</span></span>   |
| <span data-ttu-id="019ee-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="019ee-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="019ee-321">產生 200 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="019ee-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="019ee-322">否</span><span class="sxs-lookup"><span data-stu-id="019ee-322">No</span></span>   |<span data-ttu-id="019ee-323">是</span><span class="sxs-lookup"><span data-stu-id="019ee-323">Yes</span></span>   |
| <span data-ttu-id="019ee-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="019ee-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="019ee-325">產生 206 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="019ee-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="019ee-326">否</span><span class="sxs-lookup"><span data-stu-id="019ee-326">No</span></span>   |<span data-ttu-id="019ee-327">是</span><span class="sxs-lookup"><span data-stu-id="019ee-327">Yes</span></span>   |
| <span data-ttu-id="019ee-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="019ee-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="019ee-329">產生 302 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="019ee-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="019ee-330">否</span><span class="sxs-lookup"><span data-stu-id="019ee-330">No</span></span>   |<span data-ttu-id="019ee-331">是</span><span class="sxs-lookup"><span data-stu-id="019ee-331">Yes</span></span>   |
| <span data-ttu-id="019ee-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="019ee-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="019ee-333">產生 304 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="019ee-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="019ee-334">否</span><span class="sxs-lookup"><span data-stu-id="019ee-334">No</span></span>   |<span data-ttu-id="019ee-335">是</span><span class="sxs-lookup"><span data-stu-id="019ee-335">Yes</span></span>   |
| <span data-ttu-id="019ee-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="019ee-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="019ee-337">產生 404 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="019ee-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="019ee-338">否</span><span class="sxs-lookup"><span data-stu-id="019ee-338">No</span></span>   |<span data-ttu-id="019ee-339">是</span><span class="sxs-lookup"><span data-stu-id="019ee-339">Yes</span></span>   |
| <span data-ttu-id="019ee-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="019ee-340">RequestCountCacheHit</span></span> |<span data-ttu-id="019ee-341">產生快取命中的所有要求計數。</span><span class="sxs-lookup"><span data-stu-id="019ee-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="019ee-342">這表示 hello 資產處理直接從 hello POP toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="019ee-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="019ee-343">是</span><span class="sxs-lookup"><span data-stu-id="019ee-343">Yes</span></span>  |<span data-ttu-id="019ee-344">否</span><span class="sxs-lookup"><span data-stu-id="019ee-344">No</span></span>   |
| <span data-ttu-id="019ee-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="019ee-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="019ee-346">產生快取遺漏的所有要求計數。</span><span class="sxs-lookup"><span data-stu-id="019ee-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="019ee-347">這表示 hello 資產 hello POP 最接近 toohello 用戶端上，找不到，因此擷取自 hello 原點。</span><span class="sxs-lookup"><span data-stu-id="019ee-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="019ee-348">是</span><span class="sxs-lookup"><span data-stu-id="019ee-348">Yes</span></span>   | <span data-ttu-id="019ee-349">否</span><span class="sxs-lookup"><span data-stu-id="019ee-349">No</span></span>  |
| <span data-ttu-id="019ee-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="019ee-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="019ee-351">所有要求計數 tooan 資產，所以無法被快取到期 tooa hello 邊緣上的使用者設定。</span><span class="sxs-lookup"><span data-stu-id="019ee-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="019ee-352">是</span><span class="sxs-lookup"><span data-stu-id="019ee-352">Yes</span></span>   | <span data-ttu-id="019ee-353">否</span><span class="sxs-lookup"><span data-stu-id="019ee-353">No</span></span>  |
| <span data-ttu-id="019ee-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="019ee-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="019ee-355">要求 tooassets 防止 hello 資產的快取控制快取和到期標頭，這表示，它應該不會快取彈出或 hello HTTP 用戶端的所有計數</span><span class="sxs-lookup"><span data-stu-id="019ee-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="019ee-356">是</span><span class="sxs-lookup"><span data-stu-id="019ee-356">Yes</span></span>   |<span data-ttu-id="019ee-357">否</span><span class="sxs-lookup"><span data-stu-id="019ee-357">No</span></span>   |
| <span data-ttu-id="019ee-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="019ee-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="019ee-359">非上述快取狀態的所有要求計數。</span><span class="sxs-lookup"><span data-stu-id="019ee-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="019ee-360">是</span><span class="sxs-lookup"><span data-stu-id="019ee-360">Yes</span></span>   | <span data-ttu-id="019ee-361">否</span><span class="sxs-lookup"><span data-stu-id="019ee-361">No</span></span>  |
| <span data-ttu-id="019ee-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="019ee-362">EgressTotal</span></span> | <span data-ttu-id="019ee-363">輸出資料傳輸 (單位 GB)</span><span class="sxs-lookup"><span data-stu-id="019ee-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="019ee-364">是</span><span class="sxs-lookup"><span data-stu-id="019ee-364">Yes</span></span>   |<span data-ttu-id="019ee-365">是</span><span class="sxs-lookup"><span data-stu-id="019ee-365">Yes</span></span>   |
| <span data-ttu-id="019ee-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="019ee-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="019ee-367">狀態代碼為 2xx HTTP 之回應的輸出資料傳輸* (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="019ee-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="019ee-368">是</span><span class="sxs-lookup"><span data-stu-id="019ee-368">Yes</span></span>   |<span data-ttu-id="019ee-369">否</span><span class="sxs-lookup"><span data-stu-id="019ee-369">No</span></span>   |
| <span data-ttu-id="019ee-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="019ee-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="019ee-371">狀態代碼為 3xx HTTP 之回應的輸出資料傳輸 (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="019ee-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="019ee-372">是</span><span class="sxs-lookup"><span data-stu-id="019ee-372">Yes</span></span>   |<span data-ttu-id="019ee-373">否</span><span class="sxs-lookup"><span data-stu-id="019ee-373">No</span></span>   |
| <span data-ttu-id="019ee-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="019ee-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="019ee-375">狀態代碼為 4xx HTTP 之回應的輸出資料傳輸 (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="019ee-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="019ee-376">是</span><span class="sxs-lookup"><span data-stu-id="019ee-376">Yes</span></span>   | <span data-ttu-id="019ee-377">否</span><span class="sxs-lookup"><span data-stu-id="019ee-377">No</span></span>  |
| <span data-ttu-id="019ee-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="019ee-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="019ee-379">狀態代碼為 5xx HTTP 之回應的輸出資料傳輸 (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="019ee-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="019ee-380">是</span><span class="sxs-lookup"><span data-stu-id="019ee-380">Yes</span></span>   |  <span data-ttu-id="019ee-381">否</span><span class="sxs-lookup"><span data-stu-id="019ee-381">No</span></span> |
| <span data-ttu-id="019ee-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="019ee-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="019ee-383">狀態代碼為其他 HTTP 之回應的輸出資料傳輸 (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="019ee-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="019ee-384">是</span><span class="sxs-lookup"><span data-stu-id="019ee-384">Yes</span></span>   |<span data-ttu-id="019ee-385">否</span><span class="sxs-lookup"><span data-stu-id="019ee-385">No</span></span>   |
| <span data-ttu-id="019ee-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="019ee-386">EgressCacheHit</span></span> |  <span data-ttu-id="019ee-387">傳出資料傳輸所傳送的回應直接從 hello CDN 快取上 hello CDN Pop/邊緣</span><span class="sxs-lookup"><span data-stu-id="019ee-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="019ee-388">是</span><span class="sxs-lookup"><span data-stu-id="019ee-388">Yes</span></span>   |  <span data-ttu-id="019ee-389">否</span><span class="sxs-lookup"><span data-stu-id="019ee-389">No</span></span> |
| <span data-ttu-id="019ee-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="019ee-390">EgressCacheMiss</span></span> | <span data-ttu-id="019ee-391">傳出資料傳輸不上最接近的 POP 伺服器 hello 找到和擷取自 hello 來源伺服器的回應</span><span class="sxs-lookup"><span data-stu-id="019ee-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="019ee-392">是</span><span class="sxs-lookup"><span data-stu-id="019ee-392">Yes</span></span>   |  <span data-ttu-id="019ee-393">否</span><span class="sxs-lookup"><span data-stu-id="019ee-393">No</span></span> |
| <span data-ttu-id="019ee-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="019ee-394">EgressCacheNoCache</span></span> | <span data-ttu-id="019ee-395">輸出資料傳輸會禁止快取的到期 tooa hello 邊緣上的使用者設定的資產。</span><span class="sxs-lookup"><span data-stu-id="019ee-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="019ee-396">是</span><span class="sxs-lookup"><span data-stu-id="019ee-396">Yes</span></span>   |<span data-ttu-id="019ee-397">否</span><span class="sxs-lookup"><span data-stu-id="019ee-397">No</span></span>   |
| <span data-ttu-id="019ee-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="019ee-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="019ee-399">傳出資料傳輸會阻止 hello 資產的快取控制及/或 Expires 標頭，這表示，它應該不會快取彈出或 hello HTTP 用戶端快取的資產</span><span class="sxs-lookup"><span data-stu-id="019ee-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="019ee-400">是</span><span class="sxs-lookup"><span data-stu-id="019ee-400">Yes</span></span>   | <span data-ttu-id="019ee-401">否</span><span class="sxs-lookup"><span data-stu-id="019ee-401">No</span></span>  |
| <span data-ttu-id="019ee-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="019ee-402">EgressCacheOthers</span></span> |  <span data-ttu-id="019ee-403">其他快取案例的輸出資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="019ee-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="019ee-404">是</span><span class="sxs-lookup"><span data-stu-id="019ee-404">Yes</span></span>   | <span data-ttu-id="019ee-405">否</span><span class="sxs-lookup"><span data-stu-id="019ee-405">No</span></span>  |

<span data-ttu-id="019ee-406">* 連出資料傳輸是指 tootraffic 傳遞從用戶端-伺服器 toohello CDN POP。</span><span class="sxs-lookup"><span data-stu-id="019ee-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="019ee-407">Hello 核心分析記錄檔的結構描述</span><span class="sxs-lookup"><span data-stu-id="019ee-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="019ee-408">所有記錄檔會儲存在 JSON 格式，而且每個項目具有下列 hello 下列結構描述的字串欄位：</span><span class="sxs-lookup"><span data-stu-id="019ee-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="019ee-409">其中 hello 'time' 代表 hello 的 hello 小時界限 hello 統計資料報告的開始時間。</span><span class="sxs-lookup"><span data-stu-id="019ee-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="019ee-410">當 CDN 提供者不支援計量時，而非雙精確度值或整數值，則將會有 null 值。</span><span class="sxs-lookup"><span data-stu-id="019ee-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="019ee-411">這個 null 值表示度量資訊，hello 不存在，這點不同於 0 的值。</span><span class="sxs-lookup"><span data-stu-id="019ee-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="019ee-412">也請注意，將會是每個網域的 hello 結束點上設定這些度量的一組。</span><span class="sxs-lookup"><span data-stu-id="019ee-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="019ee-413">範例屬性如下︰</span><span class="sxs-lookup"><span data-stu-id="019ee-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="019ee-414">其他資源</span><span class="sxs-lookup"><span data-stu-id="019ee-414">Additional resources</span></span>

* [<span data-ttu-id="019ee-415">Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="019ee-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="019ee-416">分析 Azure CDN 使用模式</span><span class="sxs-lookup"><span data-stu-id="019ee-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="019ee-417">Azure OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="019ee-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="019ee-418">Azure Log Analytics REST API</span><span class="sxs-lookup"><span data-stu-id="019ee-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







