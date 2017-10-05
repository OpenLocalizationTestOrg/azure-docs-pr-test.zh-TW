---
title: "Azure CDN 的記錄分析 | Microsoft Docs"
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
ms.openlocfilehash: 03ff74ae4e40d3f2279caaf4f73e9b4aac6a2ebb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="e104a-103">Azure CDN 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="e104a-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="e104a-104">啟用應用程式的 CDN 後，您可能會想要監視 CDN 使用情況、檢查傳遞的健康情況，並為可能的問題疑難排解。</span><span class="sxs-lookup"><span data-stu-id="e104a-104">After enabling CDN for your application, you will likely want to monitor the CDN usage, check the health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="e104a-105">Azure CDN 利用 [CDN 核心分析](cdn-analyze-usage-patterns.md)和[診斷記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)來提供這些功能</span><span class="sxs-lookup"><span data-stu-id="e104a-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="e104a-106">CDN 核心分析</span><span class="sxs-lookup"><span data-stu-id="e104a-106">CDN Core Analytics</span></span>
<span data-ttu-id="e104a-107">若您身為採用 Verizon 標準或進階設定檔的目前 Azure CDN 使用者，則已能夠在補充入口網站中檢視核心分析；透過 Azure 入口網站的 [管理] 選項可存取補充入口網站。</span><span class="sxs-lookup"><span data-stu-id="e104a-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able to view core analytics in the supplemental portal accessible via the "Manage" option from the Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="e104a-108">Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="e104a-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="e104a-109">透過這項新功能，您現在可以檢視核心分析，並將它們儲存到一或多個目的地，包括：</span><span class="sxs-lookup"><span data-stu-id="e104a-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="e104a-110">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e104a-110">Azure Storage account</span></span>
 - <span data-ttu-id="e104a-111">Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="e104a-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="e104a-112">OMS Log Analytics 存放庫</span><span class="sxs-lookup"><span data-stu-id="e104a-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="e104a-113">這項功能適用於所有屬於 Verizon (標準與進階) 及 Akamai (標準) CDN 設定檔的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="e104a-113">This feature is available for all CDN endpoints belonging to Verizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="e104a-114">診斷記錄可讓您將 CDN 端點的基本使用情況計量匯出到各種來源，讓您可以使用自訂的方式取用。</span><span class="sxs-lookup"><span data-stu-id="e104a-114">Diagnostics logs allow you to export basic usage metrics from your CDN endpoint to a variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="e104a-115">例如，您可以執行下列幾種資料匯出作業：</span><span class="sxs-lookup"><span data-stu-id="e104a-115">For example, you can do the following types of data export:</span></span>

- <span data-ttu-id="e104a-116">匯出資料至 Blob 儲存體、匯出至 CSV，以及在 Excel 中產生圖表。</span><span class="sxs-lookup"><span data-stu-id="e104a-116">Export data to blob storage, export to CSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="e104a-117">匯出資料至事件中樞，並將資料與其他 Azure 服務相互關聯。</span><span class="sxs-lookup"><span data-stu-id="e104a-117">Export data to event hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="e104a-118">匯出資料至 Log Analytics，並在您自己的 OMS 工作區中檢視資料</span><span class="sxs-lookup"><span data-stu-id="e104a-118">Export data to log analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="e104a-119">下圖顯示典型的 CDN 核心分析資料檢視。</span><span class="sxs-lookup"><span data-stu-id="e104a-119">The following figure shows a typical CDN Core Analytics view into data.</span></span>

![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="e104a-121">*圖 1 - CDN 核心分析檢視*</span><span class="sxs-lookup"><span data-stu-id="e104a-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="e104a-122">以下逐步解說會說明核心資料的結構描述，以及啟用功能、將功能傳遞至各種目的地、從這些目的地取用功能的步驟。</span><span class="sxs-lookup"><span data-stu-id="e104a-122">The following walkthrough goes through the schema of the core analytics data, steps involved in enabling the feature and delivering them to various destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="e104a-123">使用 Azure 入口網站啟用記錄</span><span class="sxs-lookup"><span data-stu-id="e104a-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="e104a-124">診斷記錄預設為 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="e104a-124">The diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="e104a-125">請遵循下列步驟，以使用 CDN 核心分析來啟用記錄功能：</span><span class="sxs-lookup"><span data-stu-id="e104a-125">Follow the steps below to enable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="e104a-126">登入 [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e104a-126">Sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="e104a-127">如果您尚未為您的工作流程啟用 CDN，請先[啟用 Azure CDN](cdn-create-new-endpoint.md)，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="e104a-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="e104a-128">在入口網站中，瀏覽至 [CDN 設定檔]。</span><span class="sxs-lookup"><span data-stu-id="e104a-128">In the portal, navigate to **CDN profile**.</span></span>
2. <span data-ttu-id="e104a-129">選取 CDN 設定檔，然後選取您想要啟用 [診斷記錄] 的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="e104a-129">Select a CDN profile, then select the CDN endpoint that you want to enable **Diagnostics Logs**.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="e104a-131">移至 [監視] 區段下方的 [診斷記錄] 刀鋒視窗，然後將狀態變更為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="e104a-131">Go to **Diagnostics Logs** blade Under **Monitoring** section, then change the status to **On**.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="e104a-133">使用 Azure 儲存體來啟用記錄功能</span><span class="sxs-lookup"><span data-stu-id="e104a-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="e104a-134">若要使用 Azure 儲存體來儲存記錄，請選取 [封存至儲存體帳戶]，選取保留天數，然後按一下 [記錄] 下方的 [CoreAnalytics]。</span><span class="sxs-lookup"><span data-stu-id="e104a-134">To use Azure Storage to store the logs, select **Archive to a storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="e104a-136">*圖 2 - 使用 Azure 儲存體進行記錄*</span><span class="sxs-lookup"><span data-stu-id="e104a-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="e104a-137">使用 OMS Log Analytics 進行記錄</span><span class="sxs-lookup"><span data-stu-id="e104a-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="e104a-138">若要使用 OMS Log Analytics 來儲存記錄，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e104a-138">To use OMS Log Analytics to store the logs, follow these steps:</span></span>

1. <span data-ttu-id="e104a-139">從 [診斷記錄] 刀鋒視窗的 [監視] 底下，選取 [傳送至 Log Analytics]</span><span class="sxs-lookup"><span data-stu-id="e104a-139">From the **Diagnostics Logs** blade Under **Monitoring**, select **Send to Log Analytics** from</span></span> 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="e104a-141">按一下 [設定] 來設定 Log Analytics 記錄功能。</span><span class="sxs-lookup"><span data-stu-id="e104a-141">Configure the Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="e104a-142">這個動作會帶出對話方塊，以供您選取先前的工作區或建立新的工作區。</span><span class="sxs-lookup"><span data-stu-id="e104a-142">This takes you to a dialog where you can select a previous workspace or create a new one.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="e104a-144">按一下 [建立新工作區]。</span><span class="sxs-lookup"><span data-stu-id="e104a-144">Click **Create New Workspace**.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="e104a-146">接下來，您必須選取新的工作區名稱、現有的訂用帳戶、資源群組 (新的或現有的)、位置和定價層。</span><span class="sxs-lookup"><span data-stu-id="e104a-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="e104a-147">您可以選擇將此設定釘選到儀表板上。</span><span class="sxs-lookup"><span data-stu-id="e104a-147">You have the option of pinning this configuration to your dashboard.</span></span> <span data-ttu-id="e104a-148">按一下 [確定] 來完成設定。</span><span class="sxs-lookup"><span data-stu-id="e104a-148">Click OK to complete the configuration.</span></span>

    <span data-ttu-id="e104a-149">接下來，您應該會看到工作區上顯示您的 OMS 工作區名稱與資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="e104a-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="e104a-150">這些名稱必須是唯一的，而且只能使用字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="e104a-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="e104a-151">不允許使用空格和底線。</span><span class="sxs-lookup"><span data-stu-id="e104a-151">Spaces and underscores are not allowed.</span></span> 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="e104a-153">接下來，您會收到簡短訊息，其中的內容指出您的工作區已建立完成，系統將會讓您回到記錄功能的設定畫面。</span><span class="sxs-lookup"><span data-stu-id="e104a-153">You next get a short message saying that your workspace has been created and you are returned to your logging configuration screen.</span></span> <span data-ttu-id="e104a-154">您可以確認您的 Log Analytics 工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="e104a-154">You can confirm the name of your Log Analytics workspace.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="e104a-156">在設定好 Log Analytics 設定後，請確定您也勾選了 CDN 記錄功能的 [CoreAnalytics] 方塊。</span><span class="sxs-lookup"><span data-stu-id="e104a-156">Once you have set up the Log Analytics configuration, make sure you also check the CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="e104a-157">如果所有的設定皆符合您的需要，請按一下設定對話方塊頂端的 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e104a-157">If everything is to your liking, click the **Save** button at the top of the configuration dialog.</span></span>

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="e104a-159">[儲存] 按鈕將會失去作用，而且 [開啟/關閉] 按鈕現在是 [開啟]，但顏色是藍色而非紫色。</span><span class="sxs-lookup"><span data-stu-id="e104a-159">The **Save** button is no longer active and that the ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="e104a-160">如果您想要查看新的 OMS 工作區，請前往 Azure 入口網站的儀表板，按一下 Log Analytics 工作區的名稱。</span><span class="sxs-lookup"><span data-stu-id="e104a-160">If you want to see your new OMS workspace, go to your Azure portal Dashboard, click the name of your Log Analytics workspace.</span></span> <span data-ttu-id="e104a-161">接下來，您就會看到您的工作區 (請確定 OMS 工作區已在左邊呈現醒目提示狀態)。</span><span class="sxs-lookup"><span data-stu-id="e104a-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on the left).</span></span> <span data-ttu-id="e104a-162">按一下 [OMS 入口網站] 圖格，以查看您在 OMS 存放庫中的工作區。</span><span class="sxs-lookup"><span data-stu-id="e104a-162">Click on the OMS Portal tile to see your workspace in the OMS repository.</span></span> 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="e104a-164">您的 OMS 存放庫現已可供記錄資料。</span><span class="sxs-lookup"><span data-stu-id="e104a-164">Your OMS repository is now ready to log data.</span></span> <span data-ttu-id="e104a-165">若要取用該資料，您必須使用 [OMS 解決方案](#consuming-oms-log-analytics-data) (本文稍後會有說明)。</span><span class="sxs-lookup"><span data-stu-id="e104a-165">In order to consume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="e104a-166">如需有關記錄資料延遲的詳細資訊，請瀏覽[這裡](#log-data-delays)。</span><span class="sxs-lookup"><span data-stu-id="e104a-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="e104a-167">使用 PowerShell 啟用記錄</span><span class="sxs-lookup"><span data-stu-id="e104a-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="e104a-168">以下範例說明如何透過 Azure PowerShell Cmdlet 啟用與取得診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="e104a-168">Below is an example on how to enable and get Diagnostic Logs via the Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="e104a-169">啟用儲存體帳戶中的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="e104a-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="e104a-170">先登入並選取訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="e104a-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="e104a-171">若要啟用儲存體帳戶中的診斷記錄，請使用此命令︰</span><span class="sxs-lookup"><span data-stu-id="e104a-171">To Enable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="e104a-172">若要啟用 OMS 工作區中的診斷記錄，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="e104a-172">To Enable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="e104a-173">從 Azure 儲存體取用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="e104a-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="e104a-174">本節說明 CDN 核心分析的結構描述、其在 Azure 儲存體帳戶內的組織方式，並提供範例程式碼將記錄下載至 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="e104a-174">This section describes the schema of the CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code to download the logs in to a CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="e104a-175">使用 Microsoft Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="e104a-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="e104a-176">首先您需要一個可存取儲存體帳戶中內容的工具，才能夠存取 Azure 儲存體帳戶的核心分析資料。</span><span class="sxs-lookup"><span data-stu-id="e104a-176">Before you can access the core analytics data from the Azure Storage Account, you first need a tool to access the contents in a storage account.</span></span> <span data-ttu-id="e104a-177">雖然市場中有數種工具可使用，但我們建議使用 Microsoft Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="e104a-177">While there are several tools available in the market, the one that we recommend is the Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="e104a-178">您可以從[這裡](http://storageexplorer.com/)下載該工具。</span><span class="sxs-lookup"><span data-stu-id="e104a-178">You can download the tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="e104a-179">下載並安裝軟體後，請將其設定為使用同一個已設定為 CDN 診斷記錄檔目的地的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e104a-179">After downloading and installing the software, configure it to use the same Azure Storage Account that was configured as a destination to the CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="e104a-180">開啟 [Microsoft Azure 儲存體總管]</span><span class="sxs-lookup"><span data-stu-id="e104a-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="e104a-181">找到儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e104a-181">Locate the storage account</span></span>
3.  <span data-ttu-id="e104a-182">移至此儲存體帳戶下方的 [Blob 容器] 節點，然後展開該節點</span><span class="sxs-lookup"><span data-stu-id="e104a-182">Go to the **“Blob Containers”** node under this storage account and expand the node</span></span>
4.  <span data-ttu-id="e104a-183">選取名為 [insights-logs-coreanalytics] 的容器，然後對它按兩下</span><span class="sxs-lookup"><span data-stu-id="e104a-183">Select the container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="e104a-184">結果會顯示在右側窗格，開頭的第一層顯示 [resourceId=]。</span><span class="sxs-lookup"><span data-stu-id="e104a-184">Results show up on the right-hand pane starting with the first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="e104a-185">一直按一下 [繼續]，直到您看到 PT1H.json 檔案為止。</span><span class="sxs-lookup"><span data-stu-id="e104a-185">Continue clicking all the way until you see the file **PT1H.json**.</span></span> <span data-ttu-id="e104a-186">請參閱下列附註以取得路徑的說明。</span><span class="sxs-lookup"><span data-stu-id="e104a-186">See the following note for explanation of the path.</span></span>
6.  <span data-ttu-id="e104a-187">每個 blob PT1H.json 代表特定 CDN 端點或其自訂網域一小時的分析記錄。</span><span class="sxs-lookup"><span data-stu-id="e104a-187">Each blob **PT1H.json** represents the analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="e104a-188">此 JSON 檔案內容的結構描述如＜Core Analytics 記錄結構描述＞一節所述</span><span class="sxs-lookup"><span data-stu-id="e104a-188">The schema of the contents of this JSON file is described in the section Schema of the Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="e104a-189">**Blob 路徑格式**</span><span class="sxs-lookup"><span data-stu-id="e104a-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="e104a-190">Core Analytics 記錄每小時產生一次。</span><span class="sxs-lookup"><span data-stu-id="e104a-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="e104a-191">系統會將一小時的資料全部收集並儲存在單一 Azure Blob 內作為 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="e104a-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="e104a-192">此 Azure Blob 的路徑會顯示成如同有階層式結構一般。</span><span class="sxs-lookup"><span data-stu-id="e104a-192">The path to this Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="e104a-193">這是因為儲存體總管工具會將 '/' 解譯為目錄分隔符號，並顯示成階層以供方便檢視。</span><span class="sxs-lookup"><span data-stu-id="e104a-193">This is because the Storage explorer tool interprets '/' as a directory separator and shows the hierarchy for convenience.</span></span> <span data-ttu-id="e104a-194">事實上，整個路徑只代表 blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="e104a-194">Actually, the whole path just represents the blob name.</span></span> <span data-ttu-id="e104a-195">此 blob 名稱遵循下列命名慣例</span><span class="sxs-lookup"><span data-stu-id="e104a-195">This name of the blob follows the following naming convention</span></span>   
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="e104a-196">**欄位說明：**</span><span class="sxs-lookup"><span data-stu-id="e104a-196">**Description of fields:**</span></span>

|<span data-ttu-id="e104a-197">value</span><span class="sxs-lookup"><span data-stu-id="e104a-197">value</span></span>|<span data-ttu-id="e104a-198">說明</span><span class="sxs-lookup"><span data-stu-id="e104a-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="e104a-199">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="e104a-199">Subscription ID</span></span>    |<span data-ttu-id="e104a-200">Azure 訂用帳戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e104a-200">ID of the Azure Subscription.</span></span> <span data-ttu-id="e104a-201">採用 Guid 格式。</span><span class="sxs-lookup"><span data-stu-id="e104a-201">This is in the Guid format.</span></span>|
|<span data-ttu-id="e104a-202">資源</span><span class="sxs-lookup"><span data-stu-id="e104a-202">Resource</span></span> |<span data-ttu-id="e104a-203">群組名稱   CDN 資源所屬資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="e104a-203">Group Name   Name of the resource group to which the CDN resources belong.</span></span>|
|<span data-ttu-id="e104a-204">設定檔名稱</span><span class="sxs-lookup"><span data-stu-id="e104a-204">Profile Name</span></span> |<span data-ttu-id="e104a-205">CDN 設定檔名稱</span><span class="sxs-lookup"><span data-stu-id="e104a-205">Name of the CDN Profile</span></span>|
|<span data-ttu-id="e104a-206">端點名稱</span><span class="sxs-lookup"><span data-stu-id="e104a-206">Endpoint Name</span></span> |<span data-ttu-id="e104a-207">CDN 端點名稱</span><span class="sxs-lookup"><span data-stu-id="e104a-207">Name of the CDN Endpoint</span></span>|
|<span data-ttu-id="e104a-208">Year</span><span class="sxs-lookup"><span data-stu-id="e104a-208">Year</span></span>|  <span data-ttu-id="e104a-209">4 位數的年份表示法，例如 2017</span><span class="sxs-lookup"><span data-stu-id="e104a-209">4-digit representation of the year for example, 2017</span></span>|
|<span data-ttu-id="e104a-210">月</span><span class="sxs-lookup"><span data-stu-id="e104a-210">Month</span></span>| <span data-ttu-id="e104a-211">2 位數的月份表示法。</span><span class="sxs-lookup"><span data-stu-id="e104a-211">2-digit representation of the month number.</span></span> <span data-ttu-id="e104a-212">01 = 一月...12 =十二月</span><span class="sxs-lookup"><span data-stu-id="e104a-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="e104a-213">天</span><span class="sxs-lookup"><span data-stu-id="e104a-213">Day</span></span>|   <span data-ttu-id="e104a-214">2 位數當月日期表示法</span><span class="sxs-lookup"><span data-stu-id="e104a-214">2 digit representation of the day of the month</span></span>|
|<span data-ttu-id="e104a-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="e104a-215">PT1H.json</span></span>| <span data-ttu-id="e104a-216">儲存分析資料的實際 JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="e104a-216">Actual JSON file where the analytics data is stored</span></span>|

### <a name="exporting-the-core-analytics-data-to-a-csv-file"></a><span data-ttu-id="e104a-217">匯出 Core Analytics 資料至 CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="e104a-217">Exporting the Core Analytics Data to a CSV File</span></span>

<span data-ttu-id="e104a-218">為了能輕鬆存取 Core Analytics，我們提供工具範例程式碼，以供將 JSON 檔案下載至以逗號分隔的一般檔案格式，此格式可讓您輕鬆地建立圖表或其他彙總。</span><span class="sxs-lookup"><span data-stu-id="e104a-218">To make it easy to access the Core Analytics, we provide a sample code for a tool, which allows downloading the JSON files into a flat comma-separated file format, which can be used to easily create charts or other aggregations.</span></span>

<span data-ttu-id="e104a-219">以下為使用此工具的方式：</span><span class="sxs-lookup"><span data-stu-id="e104a-219">Here is how you can use the tool:</span></span>

1.  <span data-ttu-id="e104a-220">造訪 github 連結：[https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="e104a-220">Visit the github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="e104a-221">下載程式碼</span><span class="sxs-lookup"><span data-stu-id="e104a-221">Download the code</span></span>
3.  <span data-ttu-id="e104a-222">依照指示編譯與設定</span><span class="sxs-lookup"><span data-stu-id="e104a-222">Follow instructions to compile and configure</span></span>
4.  <span data-ttu-id="e104a-223">執行工具</span><span class="sxs-lookup"><span data-stu-id="e104a-223">Run the tool</span></span>
5.  <span data-ttu-id="e104a-224">產生的 CSV 檔案會以簡單的平面階層顯示分析資料。</span><span class="sxs-lookup"><span data-stu-id="e104a-224">Resulting CSV file shows the analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="e104a-225">從 OMS Log Analytics 存放庫取用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="e104a-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="e104a-226">Log Analytics 是 Operations Management Suite (OMS) 中的一項服務，可監視您的雲端和內部部署環境，以維護其可用性和效能。</span><span class="sxs-lookup"><span data-stu-id="e104a-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments to maintain their availability and performance.</span></span> <span data-ttu-id="e104a-227">它會收集您的雲端和內部部署環境中的資源所產生的資料，以及從其他監視工具提供橫跨多個來源的分析。</span><span class="sxs-lookup"><span data-stu-id="e104a-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools to provide analysis across multiple sources.</span></span> 

<span data-ttu-id="e104a-228">若要使用 Log Analytics，您必須對 Azure OMS Log Analytics 存放庫[啟用記錄功能](#enable-logging-with-azure-storage) (本文前面已討論過)。</span><span class="sxs-lookup"><span data-stu-id="e104a-228">To use Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) to the Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-the-oms-repository"></a><span data-ttu-id="e104a-229">使用 OMS 存放庫</span><span class="sxs-lookup"><span data-stu-id="e104a-229">Using the OMS Repository</span></span>

 <span data-ttu-id="e104a-230">下圖顯示存放庫的輸入和輸出架構：</span><span class="sxs-lookup"><span data-stu-id="e104a-230">The following diagram shows the architecture of the inputs and outputs of the repository:</span></span>

![OMS Log Analytics 存放庫](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="e104a-232">*圖 3 - Log Analytics 存放庫*</span><span class="sxs-lookup"><span data-stu-id="e104a-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="e104a-233">您可以使用管理解決方案，以各種方式顯示資料。</span><span class="sxs-lookup"><span data-stu-id="e104a-233">You can display the data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="e104a-234">您可以從 [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions) 取得管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="e104a-234">You can obtain Management Solutions from the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="e104a-235">按一下每個解決方案底部的 [立刻取得] 連結，即可從 Azure marketplace 安裝管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="e104a-235">You can install management solutions from Azure marketplace by clicking the **Get it now** link at the bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="e104a-236">新增 OMS CDN 管理解決方案</span><span class="sxs-lookup"><span data-stu-id="e104a-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="e104a-237">請遵循下列步驟來新增管理解決方案：</span><span class="sxs-lookup"><span data-stu-id="e104a-237">Follow these steps to add a Management Solution:</span></span>

1.   <span data-ttu-id="e104a-238">如果您尚未這麼做，請使用 Azure 訂用帳戶登入 Azure 入口網站，然後前往您的儀表板。</span><span class="sxs-lookup"><span data-stu-id="e104a-238">If you haven't already done so, sign in to the Azure portal using your Azure subscription and go to your Dashboard.</span></span>
    <span data-ttu-id="e104a-239">![Azure 儀表板](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="e104a-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="e104a-240">在 [新增] 刀鋒視窗的 [Marketplace] 底下，選取 [監視 + 管理]。</span><span class="sxs-lookup"><span data-stu-id="e104a-240">In the **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="e104a-242">在 [監視 + 管理] 刀鋒視窗中，按一下 [檢視全部]。</span><span class="sxs-lookup"><span data-stu-id="e104a-242">In the **Monitoring + management** blade, click **See all**.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="e104a-244">在搜尋方塊中搜尋 CDN。</span><span class="sxs-lookup"><span data-stu-id="e104a-244">Search for CDN in the search box.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="e104a-246">選取 [Azure CDN 核心分析]。</span><span class="sxs-lookup"><span data-stu-id="e104a-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![檢視全部](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="e104a-248">在按一下 [建立] 後，系統會詢問您是要建立新的 OMS 工作區，還是使用現有工作區。</span><span class="sxs-lookup"><span data-stu-id="e104a-248">After clicking **Create**, you will be asked to create a new OMS workspace or use an existing one.</span></span> 

    ![檢視全部](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="e104a-250">選取您之前建立的工作區。</span><span class="sxs-lookup"><span data-stu-id="e104a-250">Select the workspace you created before.</span></span> <span data-ttu-id="e104a-251">然後，您必須新增自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="e104a-251">You then need to add an automation account.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="e104a-253">下列畫面顯示您必須填寫的自動化帳戶表單。</span><span class="sxs-lookup"><span data-stu-id="e104a-253">The following screen shows the automation account form you must fill out.</span></span> 

    ![檢視全部](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="e104a-255">在建立好自動化帳戶後，您即可新增您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="e104a-255">Once you have created the automation account, you are ready to add your solution.</span></span> <span data-ttu-id="e104a-256">按一下 [ **建立** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e104a-256">Click the **Create** button.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="e104a-258">您的解決方案現已新增至工作區。</span><span class="sxs-lookup"><span data-stu-id="e104a-258">Your solution has now been added to your workspace.</span></span> <span data-ttu-id="e104a-259">回到 Azure 入口網站的儀表板。</span><span class="sxs-lookup"><span data-stu-id="e104a-259">Go back to your Azure portal Dashboard.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="e104a-261">按一下您所建立的 Log Analytics 工作區以前往您的工作區。</span><span class="sxs-lookup"><span data-stu-id="e104a-261">Click the Log Analytics workspace you created to go to your workspace.</span></span> 

11. <span data-ttu-id="e104a-262">按一下 [OMS 入口網站] 圖格，以查看您在 OMS 入口網站的新解決方案。</span><span class="sxs-lookup"><span data-stu-id="e104a-262">Click the **OMS Portal** tile to see your new solution in the OMS portal.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="e104a-264">您的 OMS 入口網站現在看起來應該類似下列畫面︰</span><span class="sxs-lookup"><span data-stu-id="e104a-264">Your OMS portal should now look like the following screen:</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="e104a-266">按一下其中一個圖格以查看您資料的幾個檢視。</span><span class="sxs-lookup"><span data-stu-id="e104a-266">Click one of the tiles to see several views into your data.</span></span>

    ![檢視全部](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="e104a-268">您可以向左或向右捲動來看到更多代表個別資料檢視的圖格。</span><span class="sxs-lookup"><span data-stu-id="e104a-268">You can scroll left or right to see further tiles representing individual views into the data.</span></span> 

    <span data-ttu-id="e104a-269">按一下其中一個圖格，您就會看到資料的更多細節。</span><span class="sxs-lookup"><span data-stu-id="e104a-269">Clicking one of the tiles gives you more details about your data.</span></span>

     ![檢視全部](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="e104a-271">優惠和定價層</span><span class="sxs-lookup"><span data-stu-id="e104a-271">Offers and pricing tiers</span></span>

<span data-ttu-id="e104a-272">您可以在[這裡](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)看到 OMS 管理解決方案的供應項目和定價層。</span><span class="sxs-lookup"><span data-stu-id="e104a-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="e104a-273">自訂檢視</span><span class="sxs-lookup"><span data-stu-id="e104a-273">Customizing views</span></span>

<span data-ttu-id="e104a-274">您可以使用**檢視設計工具**來自訂資料的檢視。</span><span class="sxs-lookup"><span data-stu-id="e104a-274">You can customize the view into your data by using the **View Designer**.</span></span> <span data-ttu-id="e104a-275">請前往您的 OMS 工作區，然後按一下 [檢視設計工具] 圖格來開始設計。</span><span class="sxs-lookup"><span data-stu-id="e104a-275">Go to your OMS workspace and begin designing by clicking the **View Designer** tile.</span></span>

![[檢視設計工具]](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="e104a-277">您可以從左邊拖放各種圖表類型，然後在左邊填入您想要分析的資料細節。</span><span class="sxs-lookup"><span data-stu-id="e104a-277">You can drag and drop types of charts from the left and fill in the data details you want to analyze on the left.</span></span>

![[檢視設計工具]](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="e104a-279">記錄資料延遲</span><span class="sxs-lookup"><span data-stu-id="e104a-279">Log data delays</span></span>

<span data-ttu-id="e104a-280">Verizon 記錄資料延遲</span><span class="sxs-lookup"><span data-stu-id="e104a-280">Verizon log data delays</span></span> | <span data-ttu-id="e104a-281">Akamai 記錄資料延遲</span><span class="sxs-lookup"><span data-stu-id="e104a-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="e104a-282">Verizon 記錄資料會延遲 1 小時，端點傳播完成後需花費最多 2 小時才會開始出現。</span><span class="sxs-lookup"><span data-stu-id="e104a-282">Verizon log data is 1 hour delayed, and take up to 2 hours to start appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="e104a-283">Akamai 記錄資料會延遲 24 小時，如果資料是在 24 小時前建立的，則需花費最多 2 小時才會開始出現。</span><span class="sxs-lookup"><span data-stu-id="e104a-283">Akamai log data is 24 hours delayed, and takes up to 2 hours to start appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="e104a-284">如果記錄是剛建立的，則最多需要 25 小時才會開始出現。</span><span class="sxs-lookup"><span data-stu-id="e104a-284">If it was recently created, it can take up to 25 hours for the logs to start appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="e104a-285">CDN 核心分析的診斷記錄類型</span><span class="sxs-lookup"><span data-stu-id="e104a-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="e104a-286">我們目前僅提供 Core Analytics 記錄，其中包含的計量會顯示 HTTP 回應統計資料和輸出統計資料，如從 CDN POP/邊緣所見。</span><span class="sxs-lookup"><span data-stu-id="e104a-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from the CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="e104a-287">Core Analytics 計量詳細資料</span><span class="sxs-lookup"><span data-stu-id="e104a-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="e104a-288">下表顯示核心分析記錄中可用計量的清單。</span><span class="sxs-lookup"><span data-stu-id="e104a-288">The following table shows a list of metrics available in the Core Analytics logs.</span></span> <span data-ttu-id="e104a-289">並非所有提供者的所有計量皆可用，雖然這樣的差異極少。</span><span class="sxs-lookup"><span data-stu-id="e104a-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="e104a-290">下表也會顯示某個提供者是否有提供指定的計量。</span><span class="sxs-lookup"><span data-stu-id="e104a-290">The following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="e104a-291">請注意，計量僅適用於有流量的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="e104a-291">Please note that the metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="e104a-292">度量</span><span class="sxs-lookup"><span data-stu-id="e104a-292">Metric</span></span>                     | <span data-ttu-id="e104a-293">說明</span><span class="sxs-lookup"><span data-stu-id="e104a-293">Description</span></span>   | <span data-ttu-id="e104a-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="e104a-294">Verizon</span></span>  | <span data-ttu-id="e104a-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="e104a-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="e104a-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="e104a-296">RequestCountTotal</span></span>         |<span data-ttu-id="e104a-297">這段期間要求命中總數</span><span class="sxs-lookup"><span data-stu-id="e104a-297">Total number of request hits during this period</span></span>| <span data-ttu-id="e104a-298">是</span><span class="sxs-lookup"><span data-stu-id="e104a-298">Yes</span></span>  |<span data-ttu-id="e104a-299">是</span><span class="sxs-lookup"><span data-stu-id="e104a-299">Yes</span></span>   |
| <span data-ttu-id="e104a-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="e104a-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="e104a-301">產生 2xx HTTP 代碼 (例如 200、202) 的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="e104a-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="e104a-302">是</span><span class="sxs-lookup"><span data-stu-id="e104a-302">Yes</span></span>  |<span data-ttu-id="e104a-303">是</span><span class="sxs-lookup"><span data-stu-id="e104a-303">Yes</span></span>   |
| <span data-ttu-id="e104a-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="e104a-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="e104a-305">產生 3xx HTTP 代碼 (例如 300、302) 的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="e104a-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="e104a-306">是</span><span class="sxs-lookup"><span data-stu-id="e104a-306">Yes</span></span>  |<span data-ttu-id="e104a-307">是</span><span class="sxs-lookup"><span data-stu-id="e104a-307">Yes</span></span>   |
| <span data-ttu-id="e104a-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="e104a-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="e104a-309">產生 4xx HTTP 代碼 (例如 400、404) 的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="e104a-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="e104a-310">是</span><span class="sxs-lookup"><span data-stu-id="e104a-310">Yes</span></span>   |<span data-ttu-id="e104a-311">是</span><span class="sxs-lookup"><span data-stu-id="e104a-311">Yes</span></span>   |
| <span data-ttu-id="e104a-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="e104a-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="e104a-313">產生 5xx HTTP 代碼 (例如 500、504) 的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="e104a-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="e104a-314">是</span><span class="sxs-lookup"><span data-stu-id="e104a-314">Yes</span></span>  |<span data-ttu-id="e104a-315">是</span><span class="sxs-lookup"><span data-stu-id="e104a-315">Yes</span></span>   |
| <span data-ttu-id="e104a-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="e104a-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="e104a-317">所有其他 HTTP 代碼 (2xx-5xx 以外) 的計數</span><span class="sxs-lookup"><span data-stu-id="e104a-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="e104a-318">是</span><span class="sxs-lookup"><span data-stu-id="e104a-318">Yes</span></span>  |<span data-ttu-id="e104a-319">是</span><span class="sxs-lookup"><span data-stu-id="e104a-319">Yes</span></span>   |
| <span data-ttu-id="e104a-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="e104a-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="e104a-321">產生 200 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="e104a-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="e104a-322">否</span><span class="sxs-lookup"><span data-stu-id="e104a-322">No</span></span>   |<span data-ttu-id="e104a-323">是</span><span class="sxs-lookup"><span data-stu-id="e104a-323">Yes</span></span>   |
| <span data-ttu-id="e104a-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="e104a-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="e104a-325">產生 206 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="e104a-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="e104a-326">否</span><span class="sxs-lookup"><span data-stu-id="e104a-326">No</span></span>   |<span data-ttu-id="e104a-327">是</span><span class="sxs-lookup"><span data-stu-id="e104a-327">Yes</span></span>   |
| <span data-ttu-id="e104a-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="e104a-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="e104a-329">產生 302 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="e104a-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="e104a-330">否</span><span class="sxs-lookup"><span data-stu-id="e104a-330">No</span></span>   |<span data-ttu-id="e104a-331">是</span><span class="sxs-lookup"><span data-stu-id="e104a-331">Yes</span></span>   |
| <span data-ttu-id="e104a-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="e104a-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="e104a-333">產生 304 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="e104a-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="e104a-334">否</span><span class="sxs-lookup"><span data-stu-id="e104a-334">No</span></span>   |<span data-ttu-id="e104a-335">是</span><span class="sxs-lookup"><span data-stu-id="e104a-335">Yes</span></span>   |
| <span data-ttu-id="e104a-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="e104a-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="e104a-337">產生 404 HTTP 代碼回應的所有要求計數</span><span class="sxs-lookup"><span data-stu-id="e104a-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="e104a-338">否</span><span class="sxs-lookup"><span data-stu-id="e104a-338">No</span></span>   |<span data-ttu-id="e104a-339">是</span><span class="sxs-lookup"><span data-stu-id="e104a-339">Yes</span></span>   |
| <span data-ttu-id="e104a-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="e104a-340">RequestCountCacheHit</span></span> |<span data-ttu-id="e104a-341">產生快取命中的所有要求計數。</span><span class="sxs-lookup"><span data-stu-id="e104a-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="e104a-342">這表示資產是從 POP 直接提供給用戶端。</span><span class="sxs-lookup"><span data-stu-id="e104a-342">This means the asset was served directly from the POP to the Client.</span></span>               | <span data-ttu-id="e104a-343">是</span><span class="sxs-lookup"><span data-stu-id="e104a-343">Yes</span></span>  |<span data-ttu-id="e104a-344">否</span><span class="sxs-lookup"><span data-stu-id="e104a-344">No</span></span>   |
| <span data-ttu-id="e104a-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="e104a-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="e104a-346">產生快取遺漏的所有要求計數。</span><span class="sxs-lookup"><span data-stu-id="e104a-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="e104a-347">這表示最靠近用戶端的 POP 上找不到資產，且因此從來源擷取。</span><span class="sxs-lookup"><span data-stu-id="e104a-347">This means the asset was not found on the POP closest to the client, and therefore was retrieved from the Origin.</span></span>              |<span data-ttu-id="e104a-348">是</span><span class="sxs-lookup"><span data-stu-id="e104a-348">Yes</span></span>   | <span data-ttu-id="e104a-349">否</span><span class="sxs-lookup"><span data-stu-id="e104a-349">No</span></span>  |
| <span data-ttu-id="e104a-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="e104a-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="e104a-351">因為邊緣上的使用者組態之故，而無法予以快取的所有資產要求計數。</span><span class="sxs-lookup"><span data-stu-id="e104a-351">Count of all requests to an asset that are prevented from being cached due to a user configuration on the edge.</span></span>              |<span data-ttu-id="e104a-352">是</span><span class="sxs-lookup"><span data-stu-id="e104a-352">Yes</span></span>   | <span data-ttu-id="e104a-353">否</span><span class="sxs-lookup"><span data-stu-id="e104a-353">No</span></span>  |
| <span data-ttu-id="e104a-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="e104a-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="e104a-355">無法由資產的 Cache-Control 與 Expires 標頭快取的所有資產要求計數，這表示不應在 POP 上或由 HTTP 用戶端快取要求</span><span class="sxs-lookup"><span data-stu-id="e104a-355">Count of all requests to assets that are prevented from being cached by the asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                |<span data-ttu-id="e104a-356">是</span><span class="sxs-lookup"><span data-stu-id="e104a-356">Yes</span></span>   |<span data-ttu-id="e104a-357">否</span><span class="sxs-lookup"><span data-stu-id="e104a-357">No</span></span>   |
| <span data-ttu-id="e104a-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="e104a-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="e104a-359">非上述快取狀態的所有要求計數。</span><span class="sxs-lookup"><span data-stu-id="e104a-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="e104a-360">是</span><span class="sxs-lookup"><span data-stu-id="e104a-360">Yes</span></span>   | <span data-ttu-id="e104a-361">否</span><span class="sxs-lookup"><span data-stu-id="e104a-361">No</span></span>  |
| <span data-ttu-id="e104a-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="e104a-362">EgressTotal</span></span> | <span data-ttu-id="e104a-363">輸出資料傳輸 (單位 GB)</span><span class="sxs-lookup"><span data-stu-id="e104a-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="e104a-364">是</span><span class="sxs-lookup"><span data-stu-id="e104a-364">Yes</span></span>   |<span data-ttu-id="e104a-365">是</span><span class="sxs-lookup"><span data-stu-id="e104a-365">Yes</span></span>   |
| <span data-ttu-id="e104a-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="e104a-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="e104a-367">狀態代碼為 2xx HTTP 之回應的輸出資料傳輸* (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="e104a-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="e104a-368">是</span><span class="sxs-lookup"><span data-stu-id="e104a-368">Yes</span></span>   |<span data-ttu-id="e104a-369">否</span><span class="sxs-lookup"><span data-stu-id="e104a-369">No</span></span>   |
| <span data-ttu-id="e104a-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="e104a-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="e104a-371">狀態代碼為 3xx HTTP 之回應的輸出資料傳輸 (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="e104a-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="e104a-372">是</span><span class="sxs-lookup"><span data-stu-id="e104a-372">Yes</span></span>   |<span data-ttu-id="e104a-373">否</span><span class="sxs-lookup"><span data-stu-id="e104a-373">No</span></span>   |
| <span data-ttu-id="e104a-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="e104a-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="e104a-375">狀態代碼為 4xx HTTP 之回應的輸出資料傳輸 (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="e104a-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="e104a-376">是</span><span class="sxs-lookup"><span data-stu-id="e104a-376">Yes</span></span>   | <span data-ttu-id="e104a-377">否</span><span class="sxs-lookup"><span data-stu-id="e104a-377">No</span></span>  |
| <span data-ttu-id="e104a-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="e104a-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="e104a-379">狀態代碼為 5xx HTTP 之回應的輸出資料傳輸 (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="e104a-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="e104a-380">是</span><span class="sxs-lookup"><span data-stu-id="e104a-380">Yes</span></span>   |  <span data-ttu-id="e104a-381">否</span><span class="sxs-lookup"><span data-stu-id="e104a-381">No</span></span> |
| <span data-ttu-id="e104a-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="e104a-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="e104a-383">狀態代碼為其他 HTTP 之回應的輸出資料傳輸 (單位為 GB)</span><span class="sxs-lookup"><span data-stu-id="e104a-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="e104a-384">是</span><span class="sxs-lookup"><span data-stu-id="e104a-384">Yes</span></span>   |<span data-ttu-id="e104a-385">否</span><span class="sxs-lookup"><span data-stu-id="e104a-385">No</span></span>   |
| <span data-ttu-id="e104a-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="e104a-386">EgressCacheHit</span></span> |  <span data-ttu-id="e104a-387">直接從 CDN POP/邊緣上 CDN 快取所傳遞回應的輸出資料傳輸</span><span class="sxs-lookup"><span data-stu-id="e104a-387">Outbound data transfer for responses that were delivered directly from the CDN cache on the CDN POPs/Edges</span></span>  |<span data-ttu-id="e104a-388">是</span><span class="sxs-lookup"><span data-stu-id="e104a-388">Yes</span></span>   |  <span data-ttu-id="e104a-389">否</span><span class="sxs-lookup"><span data-stu-id="e104a-389">No</span></span> |
| <span data-ttu-id="e104a-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="e104a-390">EgressCacheMiss</span></span> | <span data-ttu-id="e104a-391">在最靠近的 POP 伺服器上找不到和從原始伺服器擷取之回應的輸出資料傳輸</span><span class="sxs-lookup"><span data-stu-id="e104a-391">Outbound data transfer for responses that were not found on the nearest POP server, and retrieved from the origin server</span></span>              |<span data-ttu-id="e104a-392">是</span><span class="sxs-lookup"><span data-stu-id="e104a-392">Yes</span></span>   |  <span data-ttu-id="e104a-393">否</span><span class="sxs-lookup"><span data-stu-id="e104a-393">No</span></span> |
| <span data-ttu-id="e104a-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="e104a-394">EgressCacheNoCache</span></span> | <span data-ttu-id="e104a-395">因為邊緣上使用者組態之故而無法予以快取的資產輸出資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="e104a-395">Outbound data transfer for assets that are prevented from being cached due to a user configuration on the edge.</span></span>                |<span data-ttu-id="e104a-396">是</span><span class="sxs-lookup"><span data-stu-id="e104a-396">Yes</span></span>   |<span data-ttu-id="e104a-397">否</span><span class="sxs-lookup"><span data-stu-id="e104a-397">No</span></span>   |
| <span data-ttu-id="e104a-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="e104a-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="e104a-399">無法由資產的 Cache-Control 和/或 Expires 標頭快取的資產輸出資料傳輸，這表示不應在 POP 上或由 HTTP 用戶端快取要求</span><span class="sxs-lookup"><span data-stu-id="e104a-399">Outbound data transfer for assets that are prevented from being cached by the asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                    |<span data-ttu-id="e104a-400">是</span><span class="sxs-lookup"><span data-stu-id="e104a-400">Yes</span></span>   | <span data-ttu-id="e104a-401">否</span><span class="sxs-lookup"><span data-stu-id="e104a-401">No</span></span>  |
| <span data-ttu-id="e104a-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="e104a-402">EgressCacheOthers</span></span> |  <span data-ttu-id="e104a-403">其他快取案例的輸出資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="e104a-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="e104a-404">是</span><span class="sxs-lookup"><span data-stu-id="e104a-404">Yes</span></span>   | <span data-ttu-id="e104a-405">否</span><span class="sxs-lookup"><span data-stu-id="e104a-405">No</span></span>  |

<span data-ttu-id="e104a-406">*輸出資料傳輸是指從 CDN POP 伺服器傳遞到用戶端的流量。</span><span class="sxs-lookup"><span data-stu-id="e104a-406">*Outbound data transfer refers to traffic delivered from CDN POP servers to the client.</span></span>


### <a name="schema-of-the-core-analytics-logs"></a><span data-ttu-id="e104a-407">Core Analytics 記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="e104a-407">Schema of the Core Analytics Logs</span></span> 

<span data-ttu-id="e104a-408">所有記錄都以 JSON 格式儲存，且每個項目都有遵循下列結構描述的字串欄位：</span><span class="sxs-lookup"><span data-stu-id="e104a-408">All logs are stored in JSON format and each entry has string fields following the below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of the CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of the domain for which the statistics is reported>",
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

<span data-ttu-id="e104a-409">其中 ‘time’ 代表報告某段時間統計資料時該時間範圍的開始時間。</span><span class="sxs-lookup"><span data-stu-id="e104a-409">Where the ‘time’ represents the start time of the hour boundary for which the statistics is reported.</span></span> <span data-ttu-id="e104a-410">當 CDN 提供者不支援計量時，而非雙精確度值或整數值，則將會有 null 值。</span><span class="sxs-lookup"><span data-stu-id="e104a-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="e104a-411">此 null 值表示沒有計量，且這與 0 值不同。</span><span class="sxs-lookup"><span data-stu-id="e104a-411">This null value indicates the absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="e104a-412">亦請注意，各網域將會有一組這類計量設定在端點上。</span><span class="sxs-lookup"><span data-stu-id="e104a-412">Also note that there will be one set of these metrics per domain configured on the endpoint.</span></span>

<span data-ttu-id="e104a-413">範例屬性如下︰</span><span class="sxs-lookup"><span data-stu-id="e104a-413">Example properties below:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="e104a-414">其他資源</span><span class="sxs-lookup"><span data-stu-id="e104a-414">Additional resources</span></span>

* [<span data-ttu-id="e104a-415">Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="e104a-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="e104a-416">分析 Azure CDN 使用模式</span><span class="sxs-lookup"><span data-stu-id="e104a-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="e104a-417">Azure OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e104a-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="e104a-418">Azure Log Analytics REST API</span><span class="sxs-lookup"><span data-stu-id="e104a-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







