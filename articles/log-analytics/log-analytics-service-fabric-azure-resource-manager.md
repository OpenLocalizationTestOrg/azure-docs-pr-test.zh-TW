---
title: "使用 Azure 入口網站以 Log Analytics 評估 Service Fabric 應用程式 | Microsoft Docs"
description: "您可以在 Log Analytics 中使用 Azure 入口網站，使用 Service Fabric 解決方案評估 Service Fabric 應用程式、微服務、節點和叢集的風險和健全狀況。"
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 8c564c0dcbb2f9be286917b2f4d8a40da5406fae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-the-azure-portal"></a><span data-ttu-id="75965-103">使用 Azure 入口網站評估 Service Fabric 應用程式和微服務</span><span class="sxs-lookup"><span data-stu-id="75965-103">Assess Service Fabric applications and micro-services with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="75965-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="75965-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="75965-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="75965-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Service Fabric 符號](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="75965-107">這篇文章說明如何在 Log Analytics 中使用 Service Fabric 解決方案，協助識別整個 Service Fabric 叢集的問題並且進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="75965-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="75965-108">Service Fabric 解決方案會從 Service Fabric VM 使用 Azure 診斷資料，方法是從 Azure WAD 資料表收集此資料。</span><span class="sxs-lookup"><span data-stu-id="75965-108">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="75965-109">然後 Log Analytics 會讀取 Service Fabric 架構事件，包括**可靠的服務事件**、**動作項目事件**、**操作事件**和**自訂 ETW 事件**。</span><span class="sxs-lookup"><span data-stu-id="75965-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="75965-110">使用解決方案儀表板，就能夠檢視 Service Fabric 環境中值得注意的問題和相關事件。</span><span class="sxs-lookup"><span data-stu-id="75965-110">With the solution dashboard, you are able to view notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="75965-111">若要開始使用解決方案，您必須將 Service Fabric 叢集連接到 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="75965-111">To get started with the solution, you need to connect your Service Fabric cluster to a Log Analytics workspace.</span></span> <span data-ttu-id="75965-112">以下是三個要考量的案例：</span><span class="sxs-lookup"><span data-stu-id="75965-112">Here are three scenarios to consider:</span></span>

1. <span data-ttu-id="75965-113">如果您尚未部署 Service Fabric 叢集，使用***部署連接至 Log Analytics 工作區的 Service Fabric 叢集***中的步驟，以部署新的叢集，並將它設定為 Log Analytics 的報告。</span><span class="sxs-lookup"><span data-stu-id="75965-113">If you have not deployed your Service Fabric cluster, use the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace*** to deploy a new cluster and have it configured to report to Log Analytics.</span></span>
2. <span data-ttu-id="75965-114">如果需要從主機收集效能計數器，以在 Service Fabric 叢集上使用其他 OMS 解決方案 (例如安全性)，請遵循***針對已安裝 VM 擴充的 Log Analytics 工作區，部署連接至工作區的 Service Fabric 叢集***中的步驟。</span><span class="sxs-lookup"><span data-stu-id="75965-114">If you need to collect performance counters from your hosts to use other OMS solutions such as Security on your Service Fabric Cluster, follow the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="75965-115">如果您已部署您的 Service Fabric 叢集，並且想要將它連接到 Log Analytics，請依照***將現有的儲存體帳戶新增至 Log Analytics*** 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="75965-115">If you have already deployed your Service Fabric cluster and want to connect it to Log Analytics, follow the steps in ***Adding an existing storage account to Log Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace"></a><span data-ttu-id="75965-116">部署連接至 Log Analytics 工作區的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="75965-116">Deploy a Service Fabric Cluster connected to a Log Analytics workspace.</span></span>
<span data-ttu-id="75965-117">此範本會執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="75965-117">This template does the following:</span></span>

1. <span data-ttu-id="75965-118">部署已連接至 Log Analytics 工作區的 Azure Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="75965-118">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="75965-119">您可以選擇在部署範本時建立新的工作區，或輸入現有 Log Analytics 工作區的名稱。</span><span class="sxs-lookup"><span data-stu-id="75965-119">You have the option to create a new workspace while deploying the template, or input the name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="75965-120">將診斷儲存體帳戶新增至 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="75965-120">Adds the diagnostic storage account to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="75965-121">在 Log Analytics 工作區中啟用 Service Fabric 解決方案。</span><span class="sxs-lookup"><span data-stu-id="75965-121">Enables the Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="75965-122">[![部署至 Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="75965-122">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="75965-123">一旦選取上方的部署按鈕，Azure 入口網站便會開啟，並顯示可供編輯的參數。</span><span class="sxs-lookup"><span data-stu-id="75965-123">Once you select the deploy button above, the Azure portal opens with parameters for you to edit.</span></span> <span data-ttu-id="75965-124">如果您輸入新的 Log Analytics 工作區名稱，請務必建立新的資源群組︰</span><span class="sxs-lookup"><span data-stu-id="75965-124">Be sure to create a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="75965-127">接受法律條款，然後按一下 [建立] 以開始部署。</span><span class="sxs-lookup"><span data-stu-id="75965-127">Accept the legal terms and click **Create** to start the deployment.</span></span> <span data-ttu-id="75965-128">完成部署後，您應該會看到新的工作區和叢集建立，WADServiceFabric*Event、WADWindowsEventLogs 和 WADETWEvent 資料表新增︰</span><span class="sxs-lookup"><span data-stu-id="75965-128">Once the deployment is completed, you should see the new workspace and cluster created, and the WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="75965-130">針對已安裝 VM 擴充的 Log Analytics 工作區，部署連接至工作區的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="75965-130">Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="75965-131">此範本會執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="75965-131">This template does the following:</span></span>

1. <span data-ttu-id="75965-132">部署已連接至 Log Analytics 工作區的 Azure Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="75965-132">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="75965-133">您可以建立新的工作區，或是使用現有的工作區。</span><span class="sxs-lookup"><span data-stu-id="75965-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="75965-134">將診斷儲存體帳戶新增至 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="75965-134">Adds the diagnostic storage accounts to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="75965-135">在 Log Analytics 工作區中啟用 Service Fabric 解決方案。</span><span class="sxs-lookup"><span data-stu-id="75965-135">Enables the Service Fabric solution in the Log Analytics workspace.</span></span>
4. <span data-ttu-id="75965-136">在 Service Fabric 叢集中，於每個虛擬機器擴展集中安裝 MMA 代理程式擴充。</span><span class="sxs-lookup"><span data-stu-id="75965-136">Installs the MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="75965-137">安裝 MMA 代理程式之後，您就可以檢視節點的效能度量。</span><span class="sxs-lookup"><span data-stu-id="75965-137">With the MMA agent installed, you are able to view performance metrics about your nodes.</span></span>

<span data-ttu-id="75965-138">[![部署至 Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="75965-138">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="75965-139">依照上述相同步驟，輸入必要的參數，並開始進行部署。</span><span class="sxs-lookup"><span data-stu-id="75965-139">Following the same steps above, input the necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="75965-140">同樣地，您會看到新的工作區、叢集和 WAD 資料表均已建立︰</span><span class="sxs-lookup"><span data-stu-id="75965-140">Once again you should see the new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="75965-142">檢視效能資料</span><span class="sxs-lookup"><span data-stu-id="75965-142">Viewing Performance Data</span></span>

<span data-ttu-id="75965-143">若要從您的節點檢視效能資料︰</span><span class="sxs-lookup"><span data-stu-id="75965-143">To view Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="75965-144">啟動 Azure 入口網站中的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="75965-144">Launch the Log Analytics workspace from the Azure portal.</span></span>
  <span data-ttu-id="75965-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="75965-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="75965-146">移至左窗格中的 [設定]，然後選取資料 >> Windows 效能計數器 >> [新增選取的效能計數器]：![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="75965-146">Go to Settings on the left pane, and select Data >> Windows Performance Counters >> "Add the selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="75965-147">在 [記錄搜尋] 中，使用下列查詢深入節點的關鍵度量︰</span><span class="sxs-lookup"><span data-stu-id="75965-147">In Log Search, use the following queries to delve into key metrics about your nodes:</span></span>

    <span data-ttu-id="75965-148">a.</span><span class="sxs-lookup"><span data-stu-id="75965-148">a.</span></span> <span data-ttu-id="75965-149">比較最近一個小時您所有節點的平均 CPU 使用率，以查看哪個節點有問題，以及在哪個時間間隔節點有突然增加︰</span><span class="sxs-lookup"><span data-stu-id="75965-149">Compare the average CPU Utilization across all your nodes in the last one hour to see which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="75965-151">b.</span><span class="sxs-lookup"><span data-stu-id="75965-151">b.</span></span> <span data-ttu-id="75965-152">使用此查詢檢視每個節點上可用記憶體的類似折線圖︰</span><span class="sxs-lookup"><span data-stu-id="75965-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="75965-153">若要檢視所有節點的清單，顯示每個節點的可用 Mb 的確切平均值，請使用此查詢︰</span><span class="sxs-lookup"><span data-stu-id="75965-153">To view a listing of all your nodes, showing the exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="75965-155">c.</span><span class="sxs-lookup"><span data-stu-id="75965-155">c.</span></span> <span data-ttu-id="75965-156">如果您想要藉由檢查每小時平均、最小、最大和 75 個百分位數的 CPU 使用率，以向下鑽研至特定節點，您可以使用此查詢 (取代電腦欄位) 來執行此操作︰</span><span class="sxs-lookup"><span data-stu-id="75965-156">In the case that you want to drill down into a specific node by examining the hourly average, minimum, maximum and 75-percentile CPU usage, you're able to do this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="75965-158">如需 Log Analytics 效能計量的詳細資訊，請參閱[ Operations Management Suite 部落格](https://blogs.technet.microsoft.com/msoms/tag/metrics/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="75965-158">Read more information about performance metrics in Log Analytics at the [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-to-log-analytics"></a><span data-ttu-id="75965-159">將現有的儲存體帳戶新增至 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="75965-159">Adding an existing storage account to Log Analytics</span></span>

<span data-ttu-id="75965-160">此範本僅會將現有的儲存體帳戶新增至新的或現有的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="75965-160">This template simply adds your existing storage accounts to a new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="75965-161">[![部署至 Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="75965-161">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="75965-162">在選取資源群組時，如果您正在使用現有的 Log Analytics 工作區，請選取 [使用現有]，並搜尋包含 Log Analytics 工作區的資源群組。</span><span class="sxs-lookup"><span data-stu-id="75965-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for the resource group containing the Log Analytics workspace.</span></span> <span data-ttu-id="75965-163">否則建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="75965-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="75965-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="75965-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="75965-165">部署此範本之後，您可以看見儲存體帳戶連接到您的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="75965-165">After this template has been deployed, you will be able to see the storage account connected to your Log Analytics workspace.</span></span> <span data-ttu-id="75965-166">在此例中，我多新增一個儲存體帳戶至上述所建立的 Exchange 工作區。</span><span class="sxs-lookup"><span data-stu-id="75965-166">In this instance, I added one more storage account to the Exchange workspace I created above.</span></span>
<span data-ttu-id="75965-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="75965-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="75965-168">檢視 Service Fabric 事件</span><span class="sxs-lookup"><span data-stu-id="75965-168">View Service Fabric events</span></span>

<span data-ttu-id="75965-169">一旦完成部署，並在您的工作區中啟用 Service Fabric 解決方案，請在 Log Analytics 入口網站選取 **Service Fabric** 圖格，以啟動 Service Fabric 儀表板。</span><span class="sxs-lookup"><span data-stu-id="75965-169">Once the deployments are completed and the Service Fabric solution has been enabled in your workspace, select the **Service Fabric** tile in the Log Analytics portal to launch the Service Fabric dashboard.</span></span> <span data-ttu-id="75965-170">此儀表板包含下表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="75965-170">The dashboard includes the columns in the following table.</span></span> <span data-ttu-id="75965-171">每個資料行依計數列出前 10 個事件，這幾個事件符合該資料行中指定時間範圍的準則。</span><span class="sxs-lookup"><span data-stu-id="75965-171">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="75965-172">您可以按一下每個資料行右下角的 [查看全部] ，或按一下資料行標頭，以執行記錄搜尋來提供完整清單。</span><span class="sxs-lookup"><span data-stu-id="75965-172">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="75965-173">**Service Fabric 事件**</span><span class="sxs-lookup"><span data-stu-id="75965-173">**Service Fabric event**</span></span> | <span data-ttu-id="75965-174">**description**</span><span class="sxs-lookup"><span data-stu-id="75965-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="75965-175">值得注意的問題</span><span class="sxs-lookup"><span data-stu-id="75965-175">Notable Issues</span></span> |<span data-ttu-id="75965-176">顯示問題，例如 RunAsyncFailures RunAsynCancellations 和節點關閉。</span><span class="sxs-lookup"><span data-stu-id="75965-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="75965-177">運作事件</span><span class="sxs-lookup"><span data-stu-id="75965-177">Operational Events</span></span> |<span data-ttu-id="75965-178">值得注意的運作事件，例如應用程式升級和部署。</span><span class="sxs-lookup"><span data-stu-id="75965-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="75965-179">可靠的服務事件</span><span class="sxs-lookup"><span data-stu-id="75965-179">Reliable Service Events</span></span> |<span data-ttu-id="75965-180">值得注意的可靠服務事件，例如 Runasyncinvocations。</span><span class="sxs-lookup"><span data-stu-id="75965-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="75965-181">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="75965-181">Actor Events</span></span> |<span data-ttu-id="75965-182">您的微服務產生的值得注意動作項目事件，例如動作項目方法、動作項目啟用和停用等等所擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="75965-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="75965-183">應用程式事件</span><span class="sxs-lookup"><span data-stu-id="75965-183">Application Events</span></span> |<span data-ttu-id="75965-184">您的應用程式產生的所有自訂 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="75965-184">All custom ETW events generated by your applications.</span></span> |

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="75965-187">下表顯示 Service Fabric 的資料收集方法及如何收集資料的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="75965-187">The following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="75965-188">平台</span><span class="sxs-lookup"><span data-stu-id="75965-188">platform</span></span> | <span data-ttu-id="75965-189">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="75965-189">Direct Agent</span></span> | <span data-ttu-id="75965-190">Operations Manager 代理程式</span><span class="sxs-lookup"><span data-stu-id="75965-190">Operations Manager agent</span></span> | <span data-ttu-id="75965-191">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="75965-191">Azure Storage</span></span> | <span data-ttu-id="75965-192">是否需要 Operations Manager？</span><span class="sxs-lookup"><span data-stu-id="75965-192">Operations Manager required?</span></span> | <span data-ttu-id="75965-193">透過管理群組傳送的 Operations Manager 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="75965-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="75965-194">收集頻率</span><span class="sxs-lookup"><span data-stu-id="75965-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="75965-195">Windows</span><span class="sxs-lookup"><span data-stu-id="75965-195">Windows</span></span> |  |  | <span data-ttu-id="75965-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="75965-196">&#8226;</span></span> |  |  |<span data-ttu-id="75965-197">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="75965-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="75965-198">您可以按一下儀表板頂端的 [根據最近 7 天的資料]，變更 Service Fabric 解決方案中這些事件的範圍。</span><span class="sxs-lookup"><span data-stu-id="75965-198">You can change the scope of these events in the Service Fabric solution by clicking **Data based on last 7 days** at the top of the dashboard.</span></span> <span data-ttu-id="75965-199">您也可以顯示過去七天、一天或六個小時內產生的事件。</span><span class="sxs-lookup"><span data-stu-id="75965-199">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="75965-200">或者，也可以選取 [自訂]，以指定自訂日期範圍。</span><span class="sxs-lookup"><span data-stu-id="75965-200">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="75965-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75965-201">Next steps</span></span>

* <span data-ttu-id="75965-202">使用 [Log Analytics 中的記錄檔搜尋](log-analytics-log-searches.md)，檢視詳細的 Service Fabric 事件資料。</span><span class="sxs-lookup"><span data-stu-id="75965-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
