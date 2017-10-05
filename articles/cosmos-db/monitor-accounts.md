---
title: "監視 Azure Cosmos DB 要求及儲存體 | Microsoft Docs"
description: "了解如何監視 Azure Cosmos DB 帳戶的效能計量 (如要求和伺服器錯誤) 和使用量計量 (如儲存體耗用量)。"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: 0ca652d31d6c50124f87916b4486d8279075f106
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a><span data-ttu-id="9c589-103">監視 Azure Cosmos DB 要求、使用量及儲存體</span><span class="sxs-lookup"><span data-stu-id="9c589-103">Monitor Azure Cosmos DB requests, usage, and storage</span></span>
<span data-ttu-id="9c589-104">您可以在 [Azure 入口網站](https://portal.azure.com/)中監視 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c589-104">You can monitor your Azure Cosmos DB accounts in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="9c589-105">每一個 Azure Cosmos DB 帳戶都有效能計量 (例如要求和伺服器錯誤) 和使用量計量 (例如儲存體耗用量) 可供使用。</span><span class="sxs-lookup"><span data-stu-id="9c589-105">For each Azure Cosmos DB account, both performance metrics, such as requests and server errors, and usage metrics, such as storage consumption, are available.</span></span>

<span data-ttu-id="9c589-106">您可以在 [帳戶] 刀鋒視窗、新的 [度量] 刀鋒視窗、或 Azure 監視器中檢閱度量。</span><span class="sxs-lookup"><span data-stu-id="9c589-106">Metrics can be reviewed on the Account blade, the new Metrics blade, or in Azure Monitor.</span></span>

## <a name="view-performance-metrics-on-the-metrics-blade"></a><span data-ttu-id="9c589-107">在度量刀鋒視窗上檢視效能度量</span><span class="sxs-lookup"><span data-stu-id="9c589-107">View performance metrics on the Metrics blade</span></span>
1. <span data-ttu-id="9c589-108">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [更多服務]，捲動至 [資料庫]，按一下 [Azure Cosmos DB]，然後按一下您想要檢視其效能計量的 Azure Cosmos DB 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9c589-108">In the [Azure portal](https://portal.azure.com/), click **More Services**, scroll to **Databases**, click **Azure Cosmos DB**, and then click the name of the Azure Cosmos DB account for which you would like to view performance metrics.</span></span>
2. <span data-ttu-id="9c589-109">在資源功能表中，按一下 [監視] 下的 [度量]。</span><span class="sxs-lookup"><span data-stu-id="9c589-109">In the resource menu, under **Monitoring**, click **Metrics**.</span></span>

<span data-ttu-id="9c589-110">[度量] 刀鋒視窗隨即開啟，您可以選取要檢閱的集合。</span><span class="sxs-lookup"><span data-stu-id="9c589-110">The Metrics blade opens, and you can select the collection to review.</span></span> <span data-ttu-id="9c589-111">您可以檢閱「可用性」、「要求」、「輸送量」及「儲存體」計量，並將它們與 Azure Cosmos DB SLA 做比較。</span><span class="sxs-lookup"><span data-stu-id="9c589-111">You can review Availability, Requests, Throughput, and Storage metrics and compare them to the Azure Cosmos DB SLAs.</span></span>

## <a name="view-performance-metrics-by-using-azure-monitoring"></a><span data-ttu-id="9c589-112">使用 Azure 監視器檢視效能度量</span><span class="sxs-lookup"><span data-stu-id="9c589-112">View performance metrics by using Azure Monitoring</span></span>
1. <span data-ttu-id="9c589-113">在 [Azure 入口網站](https://portal.azure.com/)，按一下動態工具列中的 [NoSQL (DocumentDB)]。</span><span class="sxs-lookup"><span data-stu-id="9c589-113">In the [Azure portal](https://portal.azure.com/), click **Monitor** on the Jumpbar.</span></span>
2. <span data-ttu-id="9c589-114">在資源功能表中，按一下 [度量]。</span><span class="sxs-lookup"><span data-stu-id="9c589-114">In the resource menu, click **Metrics**.</span></span>
3. <span data-ttu-id="9c589-115">在 [監視 - 計量] 視窗的 [資源群組] 下拉式功能表中，選取與您要監視的 Azure Cosmos DB 帳戶相關聯的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9c589-115">In the **Monitor - Metrics** window, in the **esource group** drop-down menu, select the resource group associated with the Azure Cosmos DB account that you'd like to monitor.</span></span> 
4. <span data-ttu-id="9c589-116">在 [資源] 下拉式功能表中，選取要監視的資料庫帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c589-116">In the **Resource** drop-down menu, select the database account to monitor.</span></span>
5. <span data-ttu-id="9c589-117">在 [可用的度量] 清單中，選取要顯示的度量。</span><span class="sxs-lookup"><span data-stu-id="9c589-117">In the list of **Available metrics**, select the metrics to display.</span></span> <span data-ttu-id="9c589-118">使用 CTRL 按鈕同時選取多項。</span><span class="sxs-lookup"><span data-stu-id="9c589-118">Use the CTRL button to multi-select.</span></span> 

    <span data-ttu-id="9c589-119">您的度量會顯示在 [繪製] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="9c589-119">Your metrics are displayed on in the **Plot** window.</span></span> 

## <a name="view-performance-metrics-on-the-account-blade"></a><span data-ttu-id="9c589-120">在帳戶刀鋒視窗上檢視效能度量</span><span class="sxs-lookup"><span data-stu-id="9c589-120">View performance metrics on the account blade</span></span>
1. <span data-ttu-id="9c589-121">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [更多服務]，捲動至 [資料庫]，按一下 [Azure Cosmos DB]，然後按一下您想要檢視其效能計量的 Azure Cosmos DB 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9c589-121">In the [Azure portal](https://portal.azure.com/), click **More Services**, scroll to **Databases**, click **Azure Cosmos DB**, and then click the name of the Azure Cosmos DB account for which you would like to view performance metrics.</span></span>
2. <span data-ttu-id="9c589-122">[監視]  功能濾鏡預設會顯示以下圖格：</span><span class="sxs-lookup"><span data-stu-id="9c589-122">The **Monitoring** lens displays the following tiles by default:</span></span>
   
   * <span data-ttu-id="9c589-123">當日的要求總數。</span><span class="sxs-lookup"><span data-stu-id="9c589-123">Total requests for the current day.</span></span>
   * <span data-ttu-id="9c589-124">已使用儲存體。</span><span class="sxs-lookup"><span data-stu-id="9c589-124">Storage used.</span></span>
   
   <span data-ttu-id="9c589-125">如果您的表格顯示 [沒有可用的資料]  ，但您認為資料庫中有資料，請參閱 [疑難排解](#troubleshooting) 一節。</span><span class="sxs-lookup"><span data-stu-id="9c589-125">If your table displays **No data available** and you believe there is data in your database, see the [Troubleshooting](#troubleshooting) section.</span></span>
   
   ![[監視] 功能濾鏡的螢幕擷取畫面，可顯示要求和儲存體使用量](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. <span data-ttu-id="9c589-127">按一下 [要求] 或 [使用配額] 圖格，即會開啟詳細的 [度量] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c589-127">Clicking on the **Requests** or **Usage Quota** tile opens a detailed **Metric** blade.</span></span>
4. <span data-ttu-id="9c589-128">[ **度量** ] 刀鋒視窗會顯示您已選取之度量的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9c589-128">The **Metric** blade shows you details about the metrics you have selected.</span></span>  <span data-ttu-id="9c589-129">刀鋒視窗上方是每小時繪製為圖表的要求圖形，而下方表格會顯示已節流處理的要求和要求總數的彙總值。</span><span class="sxs-lookup"><span data-stu-id="9c589-129">At the top of the blade is a graph of requests charted hourly, and below that is table that shows aggregation values for throttled and total requests.</span></span>  <span data-ttu-id="9c589-130">度量刀鋒視窗也會顯示已定義的警示清單，且依目前度量刀鋒視窗上出現的度量來篩選 (因此，如果您有許多警示，只會看到此處顯示相關的警示)。</span><span class="sxs-lookup"><span data-stu-id="9c589-130">The metric blade also shows the list of alerts which have been defined, filtered to the metrics that appear on the current metric blade (this way, if you have a number of alerts, you'll only see the relevant ones presented here).</span></span>   
   
   ![[度量] 刀鋒視窗的螢幕擷取畫面，其中包已節流處理的要求](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-the-portal"></a><span data-ttu-id="9c589-132">在入口網站中自訂效能度量檢視</span><span class="sxs-lookup"><span data-stu-id="9c589-132">Customize performance metric views in the portal</span></span>
1. <span data-ttu-id="9c589-133">若要自訂在特定圖表中顯示的度量，請按一下圖表以在 [度量] 刀鋒視窗中開啟該圖表，然後按一下 [編輯圖表]。</span><span class="sxs-lookup"><span data-stu-id="9c589-133">To customize the metrics that display in a particular chart, click the chart to open it in the **Metric** blade, and then click **Edit chart**.</span></span>  
   <span data-ttu-id="9c589-134">![[度量] 刀鋒視窗控制項的螢幕擷取畫面，其中已將 [編輯圖表] 反白顯示](./media/monitor-accounts/madocdb3.png)</span><span class="sxs-lookup"><span data-stu-id="9c589-134">![Screen shot of the Metric blade controls, with Edit chart highlighted](./media/monitor-accounts/madocdb3.png)</span></span>
2. <span data-ttu-id="9c589-135">在 [編輯圖表]  刀鋒視窗上，會提供選項來修改圖表中顯示的度量及其時間範圍。</span><span class="sxs-lookup"><span data-stu-id="9c589-135">On the **Edit Chart** blade, there are options to modify the metrics that display in the chart, as well as their time range.</span></span>  
   <span data-ttu-id="9c589-136">![[編輯圖表] 刀鋒視窗的螢幕擷取畫面](./media/monitor-accounts/madocdb4.png)</span><span class="sxs-lookup"><span data-stu-id="9c589-136">![Screen shot of the Edit Chart blade](./media/monitor-accounts/madocdb4.png)</span></span>
3. <span data-ttu-id="9c589-137">若要變更組件中顯示的度量，只需選取或清除可用的效能度量，然後按一下刀鋒視窗底部的 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="9c589-137">To change the metrics displayed in the part, simply select or clear the available performance metrics, and then click **OK** at the bottom of the blade.</span></span>  
4. <span data-ttu-id="9c589-138">若要變更時間範圍，請選擇不同的範圍 (例如 [自訂])，然後按一下刀鋒視窗底部的 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9c589-138">To change the time range, choose a different range (for example, **Custom**), and then click **OK** at the bottom of the blade.</span></span>  
   
   ![[編輯圖表] 刀鋒視窗的 [時間範圍] 部分螢幕擷取畫面，顯示如何輸入自訂時間範圍](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-the-portal"></a><span data-ttu-id="9c589-140">在入口網站中建立並排圖表</span><span class="sxs-lookup"><span data-stu-id="9c589-140">Create side-by-side charts in the portal</span></span>
<span data-ttu-id="9c589-141">Azure 入口網站可讓您建立並排度量圖表。</span><span class="sxs-lookup"><span data-stu-id="9c589-141">The Azure Portal allows you to create side-by-side metric charts.</span></span>  

1. <span data-ttu-id="9c589-142">首先，以滑鼠右鍵按一下要複製的圖表，然後選取 [自訂] 。</span><span class="sxs-lookup"><span data-stu-id="9c589-142">First, right-click on the chart you want to copy and select **Customize**.</span></span>
   
   ![包含反白顯示 [自訂] 選項的 [要求總數] 圖表螢幕擷取畫面](./media/monitor-accounts/madocdb6.png)
2. <span data-ttu-id="9c589-144">在功能表上按一下 [複製] 以複製組件，然後按一下 [自訂完成]。</span><span class="sxs-lookup"><span data-stu-id="9c589-144">Click **Clone** on the menu to copy the part and then click **Done customizing**.</span></span>
   
   ![包含反白顯示 [複製] 與 [自訂完成] 選項的 [要求總數] 圖表螢幕擷取畫面](./media/monitor-accounts/madocdb7.png)  

<span data-ttu-id="9c589-146">現在，您可以將此組件視為其他任何度量組件，並自訂該組件中顯示的度量和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="9c589-146">You may now treat this part as any other metric part, customizing the metrics and time range displayed in the part.</span></span>  <span data-ttu-id="9c589-147">如此一來，您可以同時看到兩個不同的度量圖表並排出現。</span><span class="sxs-lookup"><span data-stu-id="9c589-147">By doing this, you can see two different metrics chart side-by-side at the same time.</span></span>  
    ![[要求總數] 圖表和全新 [要求總數] 前一個小時圖表的螢幕擷取畫面](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-the-portal"></a><span data-ttu-id="9c589-149">在入口網站中設定警示</span><span class="sxs-lookup"><span data-stu-id="9c589-149">Set up alerts in the portal</span></span>
1. <span data-ttu-id="9c589-150">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [更多服務]，按一下 [Azure Cosmos DB]，然後按一下您想要設定其效能計量警示的 Azure Cosmos DB 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9c589-150">In the [Azure portal](https://portal.azure.com/), click **More Services**, click **Azure Cosmos DB**, and then click the name of the Azure Cosmos DB account for which you would like to setup performance metric alerts.</span></span>
2. <span data-ttu-id="9c589-151">在資源功能表中，按一下 [警示規則]  以開啟 [警示規則] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c589-151">In the resource menu, click **Alert Rules** to open the Alert rules blade.</span></span>  
   <span data-ttu-id="9c589-152">![已選取 [警示規則] 組件的螢幕擷取畫面](./media/monitor-accounts/madocdb10.5.png)</span><span class="sxs-lookup"><span data-stu-id="9c589-152">![Screen shot of the Alert rules part selected](./media/monitor-accounts/madocdb10.5.png)</span></span>
3. <span data-ttu-id="9c589-153">在 [警示規則] 刀鋒視窗中，按一下 [新增警示]。</span><span class="sxs-lookup"><span data-stu-id="9c589-153">In the **Alert rules** blade, click **Add alert**.</span></span>  
   <span data-ttu-id="9c589-154">![包含反白顯示 [新增警示] 按鈕的 [警示規則] 刀鋒視窗螢幕擷取畫面](./media/monitor-accounts/madocdb11.png)</span><span class="sxs-lookup"><span data-stu-id="9c589-154">![Screenshot of the Alert Rules blade, with the Add Alert button highlighted](./media/monitor-accounts/madocdb11.png)</span></span>
4. <span data-ttu-id="9c589-155">在 [Add an alert rule]  刀鋒視窗中，指定：</span><span class="sxs-lookup"><span data-stu-id="9c589-155">In the **Add an alert rule** blade, specify:</span></span>
   
   * <span data-ttu-id="9c589-156">您設定之警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="9c589-156">The name of the alert rule you are setting up.</span></span>
   * <span data-ttu-id="9c589-157">新警示規則的描述。</span><span class="sxs-lookup"><span data-stu-id="9c589-157">A description of the new alert rule.</span></span>
   * <span data-ttu-id="9c589-158">警示規則的度量。</span><span class="sxs-lookup"><span data-stu-id="9c589-158">The metric for the alert rule.</span></span>
   * <span data-ttu-id="9c589-159">決定警示何時啟動的條件、臨界值和期間。</span><span class="sxs-lookup"><span data-stu-id="9c589-159">The condition, threshold, and period that determine when the alert activates.</span></span> <span data-ttu-id="9c589-160">例如，過去 15 分鐘伺服器錯誤計算大於 5。</span><span class="sxs-lookup"><span data-stu-id="9c589-160">For example, a server error count greater than 5 over the last 15 minutes.</span></span>
   * <span data-ttu-id="9c589-161">警示引發時是否傳送電子郵件給服務管理員和共同管理員。</span><span class="sxs-lookup"><span data-stu-id="9c589-161">Whether the service administrator and coadministrators are emailed when the alert fires.</span></span>
   * <span data-ttu-id="9c589-162">警示通知的其他電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9c589-162">Additional email addresses for alert notifications.</span></span>  
     ![[新增警示規則] 刀鋒視窗的螢幕擷取畫面](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a><span data-ttu-id="9c589-164">以程式設計方式監視 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9c589-164">Monitor Azure Cosmos DB programatically</span></span>
<span data-ttu-id="9c589-165">可在入口網站中取得的帳戶層級度量 (例如，帳戶儲存體使用量和要求總數) 無法透過 DocumentDB API 取得。</span><span class="sxs-lookup"><span data-stu-id="9c589-165">The account level metrics available in the portal, such as account storage usage and total requests, are not available via the DocumentDB APIs.</span></span> <span data-ttu-id="9c589-166">不過，您可以使用 DocumentDB API 來擷取集合層級的使用量資料。</span><span class="sxs-lookup"><span data-stu-id="9c589-166">However, you can retrieve usage data at the collection level by using the DocumentDB APIs.</span></span> <span data-ttu-id="9c589-167">若要擷取集合層級的資料，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9c589-167">To retrieve collection level data, do the following:</span></span>

* <span data-ttu-id="9c589-168">若要使用 REST API，請 [在集合上執行 GET](https://msdn.microsoft.com/library/mt489073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9c589-168">To use the REST API, [perform a GET on the collection](https://msdn.microsoft.com/library/mt489073.aspx).</span></span> <span data-ttu-id="9c589-169">集合的配額和使用量資訊會在回應的 x-ms-resource-quota 和 x-ms-resource-usage 標頭中傳回。</span><span class="sxs-lookup"><span data-stu-id="9c589-169">The quota and usage information for the collection is returned in the x-ms-resource-quota and x-ms-resource-usage headers in the response.</span></span>
* <span data-ttu-id="9c589-170">若要使用 .NET SDK，請使用 [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) 方法，此方法會傳回包含 **CollectionSizeUsage**、**DatabaseUsage**、**DocumentUsage** 等幾個使用量屬性的 [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9c589-170">To use the .NET SDK, use the [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) method, which returns a [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) that contains a number of usage properties such as **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**, and more.</span></span>

<span data-ttu-id="9c589-171">若要存取其他度量，請使用 [Azure 監視器 SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights)。</span><span class="sxs-lookup"><span data-stu-id="9c589-171">To access additional metrics, use the [Azure Monitor SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights).</span></span> <span data-ttu-id="9c589-172">您可以呼叫下列程式碼來擷取可用的度量定義：</span><span class="sxs-lookup"><span data-stu-id="9c589-172">Available metric definitions can be retrieved by calling:</span></span>

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

<span data-ttu-id="9c589-173">擷取個別度量的查詢會使用下列格式：</span><span class="sxs-lookup"><span data-stu-id="9c589-173">Queries to retrieve individual metrics use the following format:</span></span>

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

<span data-ttu-id="9c589-174">如需詳細資訊，請參閱 [Retrieving Resource Metrics via the Azure Monitor REST API (透過 Azure 監視器 API 擷取資源度量)](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/)。</span><span class="sxs-lookup"><span data-stu-id="9c589-174">For more information, see [Retrieving Resource Metrics via the Azure Monitor REST API](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/).</span></span> <span data-ttu-id="9c589-175">請注意，"Azure Inights" 已重新命名為「Azure 監視器」。</span><span class="sxs-lookup"><span data-stu-id="9c589-175">Note that "Azure Inights" was renamed "Azure Monitor".</span></span>  <span data-ttu-id="9c589-176">此部落格項目參考的是舊名稱。</span><span class="sxs-lookup"><span data-stu-id="9c589-176">This blog entry refers to the older name.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9c589-177">疑難排解</span><span class="sxs-lookup"><span data-stu-id="9c589-177">Troubleshooting</span></span>
<span data-ttu-id="9c589-178">如果您的監視圖格顯示 [沒有可用的資料]  訊息，而您最近曾提出要求或將資料新增到資料庫，您就能編輯圖格以反映最近的使用量。</span><span class="sxs-lookup"><span data-stu-id="9c589-178">If your monitoring tiles display the **No data available** message, and you recently made requests or added data to the database, you can edit the tile to reflect the recent usage.</span></span>

### <a name="edit-a-tile-to-refresh-current-data"></a><span data-ttu-id="9c589-179">編輯磚以重新整理目前的資料</span><span class="sxs-lookup"><span data-stu-id="9c589-179">Edit a tile to refresh current data</span></span>
1. <span data-ttu-id="9c589-180">若要自訂在特定組件中顯示的度量，請按一下圖表以開啟 [度量] 刀鋒視窗，然後按一下 [編輯圖表]。</span><span class="sxs-lookup"><span data-stu-id="9c589-180">To customize the metrics that display in a particular part, click the chart to open the **Metric** blade, and then click **Edit Chart**.</span></span>  
   <span data-ttu-id="9c589-181">![[度量] 刀鋒視窗控制項的螢幕擷取畫面，其中已將 [編輯圖表] 反白顯示](./media/monitor-accounts/madocdb3.png)</span><span class="sxs-lookup"><span data-stu-id="9c589-181">![Screen shot of the Metric blade controls, with Edit chart highlighted](./media/monitor-accounts/madocdb3.png)</span></span>
2. <span data-ttu-id="9c589-182">在 [編輯圖表] 刀鋒視窗的 [時間範圍] 區段中，按一下 [過去 1 小時]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9c589-182">On the **Edit Chart** blade, in the **Time Range** section, click **past hour**, and then click **OK**.</span></span>  
   <span data-ttu-id="9c589-183">![已選取過去 1 小時的 [編輯圖表] 刀鋒視窗螢幕擷取畫面](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)</span><span class="sxs-lookup"><span data-stu-id="9c589-183">![Screen shot of the Edit Chart blade with past hour selected](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)</span></span>
3. <span data-ttu-id="9c589-184">您的圖格現在應該會重新整理，以顯示您目前的資料和使用量。</span><span class="sxs-lookup"><span data-stu-id="9c589-184">Your tile should now refresh showing your current data and usage.</span></span>  
   ![過去 1 小時已更新的要求總數磚的的螢幕擷取畫面](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a><span data-ttu-id="9c589-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c589-186">Next steps</span></span>
<span data-ttu-id="9c589-187">若要深入了解 Azure Cosmos DB 容量規劃，請參閱 [Azure Cosmos DB 容量規劃工具計算機 (英文)](https://www.documentdb.com/capacityplanner)。</span><span class="sxs-lookup"><span data-stu-id="9c589-187">To learn more about Azure Cosmos DB capacity planning, see the [Azure Cosmos DB capacity planner calculator](https://www.documentdb.com/capacityplanner).</span></span>

