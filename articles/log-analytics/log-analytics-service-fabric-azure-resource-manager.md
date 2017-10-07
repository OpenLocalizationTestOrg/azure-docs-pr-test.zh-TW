---
title: "Service Fabric 應用程式與記錄分析使用 aaaAssess hello Azure 入口網站 |Microsoft 文件"
description: "您可以使用 hello Service Fabric 方案中使用 hello Azure 入口網站 tooassess hello 風險和健全狀況服務的網狀架構應用程式的記錄分析微服務、 節點和叢集。"
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
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="a04cf-103">評估 Service Fabric 應用程式和以 hello Azure 入口網站的微服務</span><span class="sxs-lookup"><span data-stu-id="a04cf-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a04cf-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="a04cf-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="a04cf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a04cf-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Service Fabric 符號](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="a04cf-107">本文說明如何 toouse hello Service Fabric 方案中記錄分析 toohelp 識別及疑難排解問題跨 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="a04cf-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="a04cf-108">hello Service Fabric 解決方案會使用從您服務網狀架構的 Vm，Azure 診斷資料收集這項資料從 Azure WAD 資料表。</span><span class="sxs-lookup"><span data-stu-id="a04cf-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="a04cf-109">然後 Log Analytics 會讀取 Service Fabric 架構事件，包括**可靠的服務事件**、**動作項目事件**、**操作事件**和**自訂 ETW 事件**。</span><span class="sxs-lookup"><span data-stu-id="a04cf-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="a04cf-110">Hello 方案儀表板，您在無法 tooview 值得注意的問題和相關事件 Service Fabric 環境中。</span><span class="sxs-lookup"><span data-stu-id="a04cf-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="a04cf-111">tooget 入門 hello 方案，您需要 tooconnect Service Fabric 叢集 tooa 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="a04cf-112">以下是三個案例 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="a04cf-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="a04cf-113">如果您尚未部署 Service Fabric 叢集，使用中的 hello 步驟***部署 Service Fabric 叢集連線 tooa 記錄分析工作區***toodeploy 新叢集，而且已經設定 tooreport tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="a04cf-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="a04cf-114">如果您需要 toocollect 效能計數器從主機 toouse 其他 OMS 解決方案，例如安全性服務網狀架構叢集上，依照中的 hello 步驟***部署 VM 擴充功能的 Service Fabric 叢集連線 tooa 記錄分析工作區安裝。***</span><span class="sxs-lookup"><span data-stu-id="a04cf-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="a04cf-115">如果您已部署 Service Fabric 叢集，而且想 tooconnect 它 tooLog 分析，請依照下列中的 hello 步驟***加入現有的儲存體帳戶 tooLog 分析。***</span><span class="sxs-lookup"><span data-stu-id="a04cf-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="a04cf-116">部署 Service Fabric 叢集連線 tooa 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="a04cf-117">此範本沒有 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="a04cf-117">This template does hello following:</span></span>

1. <span data-ttu-id="a04cf-118">部署 Azure Service Fabric 叢集已連線 tooa 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="a04cf-119">您擁有 hello 選項 toocreate 新的工作區部署 hello 範本或輸入的 hello 名稱已存在的記錄分析工作區時。</span><span class="sxs-lookup"><span data-stu-id="a04cf-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="a04cf-120">新增 hello 診斷儲存體帳戶 toohello 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="a04cf-121">可讓您記錄分析工作區中的 hello Service Fabric 方案。</span><span class="sxs-lookup"><span data-stu-id="a04cf-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="a04cf-122">[![部署 tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a04cf-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="a04cf-123">一旦您選取 hello 部署按鈕上方，hello Azure 入口網站的開啟與您 tooedit 的參數。</span><span class="sxs-lookup"><span data-stu-id="a04cf-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="a04cf-124">如果您輸入新的記錄分析工作區名稱，是確定 toocreate 新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="a04cf-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="a04cf-127">接受 hello 法律條款，然後按一下**建立**toostart hello 部署。</span><span class="sxs-lookup"><span data-stu-id="a04cf-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="a04cf-128">Hello 部署完成後，您應看到 hello 新工作區，然後建立、 叢集及 hello WADServiceFabric * 加入的事件、 WADWindowsEventLogs 及 WADETWEvent 資料表：</span><span class="sxs-lookup"><span data-stu-id="a04cf-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="a04cf-130">VM 擴充功能安裝與部署 Service Fabric 叢集連線 tooa 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="a04cf-131">此範本沒有 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="a04cf-131">This template does hello following:</span></span>

1. <span data-ttu-id="a04cf-132">部署 Azure Service Fabric 叢集已連線 tooa 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="a04cf-133">您可以建立新的工作區，或是使用現有的工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="a04cf-134">新增 hello 診斷儲存體帳戶 toohello 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="a04cf-135">可讓 hello 記錄分析工作區中的 hello Service Fabric 方案。</span><span class="sxs-lookup"><span data-stu-id="a04cf-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="a04cf-136">安裝集合 Service Fabric 叢集中的每個虛擬機器規模 hello MMA 代理程式延伸。</span><span class="sxs-lookup"><span data-stu-id="a04cf-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="a04cf-137">Hello MMA 安裝有代理程式，就能 tooview 效能度量有關您的節點。</span><span class="sxs-lookup"><span data-stu-id="a04cf-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="a04cf-138">[![部署 tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a04cf-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="a04cf-139">以下 hello 相同的步驟上方輸入的 hello 必要的參數，並開始進行部署。</span><span class="sxs-lookup"><span data-stu-id="a04cf-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="a04cf-140">同樣地，您應該看到 hello 新的工作區、 叢集和所有建立的 WAD 資料表：</span><span class="sxs-lookup"><span data-stu-id="a04cf-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="a04cf-142">檢視效能資料</span><span class="sxs-lookup"><span data-stu-id="a04cf-142">Viewing Performance Data</span></span>

<span data-ttu-id="a04cf-143">從您的節點 tooview 的效能資料：</span><span class="sxs-lookup"><span data-stu-id="a04cf-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="a04cf-144">啟動 hello 從 hello Azure 入口網站的記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="a04cf-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="a04cf-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="a04cf-146">在 hello 左窗格中，移 tooSettings，然後選取資料 >> Windows 效能計數器 >> 」 新增 hello 選取效能計數器 」: ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="a04cf-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="a04cf-147">在記錄搜尋中，使用下列查詢 toodelve 到您的節點有關的關鍵計量 hello:</span><span class="sxs-lookup"><span data-stu-id="a04cf-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="a04cf-148">a.</span><span class="sxs-lookup"><span data-stu-id="a04cf-148">a.</span></span> <span data-ttu-id="a04cf-149">比較您的所有節點中 hello 哪些節點時發生問題過去一小時 toosee hello 平均 CPU 使用率，但在哪個時間間隔節點突然增加：</span><span class="sxs-lookup"><span data-stu-id="a04cf-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="a04cf-151">b.</span><span class="sxs-lookup"><span data-stu-id="a04cf-151">b.</span></span> <span data-ttu-id="a04cf-152">使用此查詢檢視每個節點上可用記憶體的類似折線圖︰</span><span class="sxs-lookup"><span data-stu-id="a04cf-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="a04cf-153">tooview 您的所有節點，每個節點，並顯示 Available MBytes hello 的平均實際值的清單會使用下列查詢：</span><span class="sxs-lookup"><span data-stu-id="a04cf-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="a04cf-155">c.</span><span class="sxs-lookup"><span data-stu-id="a04cf-155">c.</span></span> <span data-ttu-id="a04cf-156">萬一 hello 到特定節點想 toodrill 向下的，藉由檢查 hello 每小時平均值、 最小、 最大和 75 個百分位數的 CPU 使用量，您可以 toodo 藉由使用這個查詢 （取代電腦欄位）：</span><span class="sxs-lookup"><span data-stu-id="a04cf-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="a04cf-158">閱讀詳細資訊記錄分析中的效能標準，在 hello [Operations Management Suite 部落格](https://blogs.technet.microsoft.com/msoms/tag/metrics/)。</span><span class="sxs-lookup"><span data-stu-id="a04cf-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="a04cf-159">加入現有的儲存體帳戶 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="a04cf-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="a04cf-160">這個範本只會加入您現有儲存體帳戶 tooa 新的或現有記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="a04cf-161">[![部署 tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a04cf-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="a04cf-162">在 選取資源群組，如果您正在使用現有的記錄分析工作區，選取 「 使用現有 」，並搜尋 hello 資源群組中包含的 hello 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="a04cf-163">否則建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="a04cf-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="a04cf-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="a04cf-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="a04cf-165">在部署此範本之後，您將無法 toosee hello 儲存體帳戶連接 tooyour 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a04cf-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="a04cf-166">在本例中，我可以加入多個儲存體帳戶 toohello Exchange 工作區上面所建立。</span><span class="sxs-lookup"><span data-stu-id="a04cf-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="a04cf-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="a04cf-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="a04cf-168">檢視 Service Fabric 事件</span><span class="sxs-lookup"><span data-stu-id="a04cf-168">View Service Fabric events</span></span>

<span data-ttu-id="a04cf-169">Hello 部署已完成並已啟用工作區中的 hello Service Fabric 方案，請選取 hello **Service Fabric**磚 hello 記錄分析入口網站 toolaunch hello Service Fabric 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="a04cf-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="a04cf-170">hello 儀表板會納入 hello 下表中的 hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="a04cf-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="a04cf-171">每個資料行計數對應資料行的準則 hello 指定時間範圍列出 hello 前 10 個事件。</span><span class="sxs-lookup"><span data-stu-id="a04cf-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="a04cf-172">您可以執行，即可提供 hello 整個清單的記錄搜尋**查看所有**在 hello 右下的每個資料行，或按一下 hello 資料行標頭。</span><span class="sxs-lookup"><span data-stu-id="a04cf-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="a04cf-173">**Service Fabric 事件**</span><span class="sxs-lookup"><span data-stu-id="a04cf-173">**Service Fabric event**</span></span> | <span data-ttu-id="a04cf-174">**description**</span><span class="sxs-lookup"><span data-stu-id="a04cf-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="a04cf-175">值得注意的問題</span><span class="sxs-lookup"><span data-stu-id="a04cf-175">Notable Issues</span></span> |<span data-ttu-id="a04cf-176">顯示問題，例如 RunAsyncFailures RunAsynCancellations 和節點關閉。</span><span class="sxs-lookup"><span data-stu-id="a04cf-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="a04cf-177">運作事件</span><span class="sxs-lookup"><span data-stu-id="a04cf-177">Operational Events</span></span> |<span data-ttu-id="a04cf-178">值得注意的運作事件，例如應用程式升級和部署。</span><span class="sxs-lookup"><span data-stu-id="a04cf-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="a04cf-179">可靠的服務事件</span><span class="sxs-lookup"><span data-stu-id="a04cf-179">Reliable Service Events</span></span> |<span data-ttu-id="a04cf-180">值得注意的可靠服務事件，例如 Runasyncinvocations。</span><span class="sxs-lookup"><span data-stu-id="a04cf-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="a04cf-181">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="a04cf-181">Actor Events</span></span> |<span data-ttu-id="a04cf-182">您的微服務產生的值得注意動作項目事件，例如動作項目方法、動作項目啟用和停用等等所擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a04cf-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="a04cf-183">應用程式事件</span><span class="sxs-lookup"><span data-stu-id="a04cf-183">Application Events</span></span> |<span data-ttu-id="a04cf-184">您的應用程式產生的所有自訂 ETW 事件。</span><span class="sxs-lookup"><span data-stu-id="a04cf-184">All custom ETW events generated by your applications.</span></span> |

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="a04cf-187">hello 下表顯示資料收集方法，以及適用於 Service Fabric 如何收集資料的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a04cf-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="a04cf-188">平台</span><span class="sxs-lookup"><span data-stu-id="a04cf-188">platform</span></span> | <span data-ttu-id="a04cf-189">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="a04cf-189">Direct Agent</span></span> | <span data-ttu-id="a04cf-190">Operations Manager 代理程式</span><span class="sxs-lookup"><span data-stu-id="a04cf-190">Operations Manager agent</span></span> | <span data-ttu-id="a04cf-191">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="a04cf-191">Azure Storage</span></span> | <span data-ttu-id="a04cf-192">是否需要 Operations Manager？</span><span class="sxs-lookup"><span data-stu-id="a04cf-192">Operations Manager required?</span></span> | <span data-ttu-id="a04cf-193">透過管理群組傳送的 Operations Manager 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="a04cf-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="a04cf-194">收集頻率</span><span class="sxs-lookup"><span data-stu-id="a04cf-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="a04cf-195">Windows</span><span class="sxs-lookup"><span data-stu-id="a04cf-195">Windows</span></span> |  |  | <span data-ttu-id="a04cf-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a04cf-196">&#8226;</span></span> |  |  |<span data-ttu-id="a04cf-197">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="a04cf-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="a04cf-198">您可以按一下來變更 hello Service Fabric 方案中的這些事件 hello 範圍**資料根據過去 7 天**在 hello hello 儀表板的頂端。</span><span class="sxs-lookup"><span data-stu-id="a04cf-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="a04cf-199">您也可以顯示 hello 內產生過去七天一天或六個小時的事件。</span><span class="sxs-lookup"><span data-stu-id="a04cf-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="a04cf-200">或者，您可以選取**自訂**toospecify 自訂日期範圍。</span><span class="sxs-lookup"><span data-stu-id="a04cf-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a04cf-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a04cf-201">Next steps</span></span>

* <span data-ttu-id="a04cf-202">使用[中記錄分析記錄搜尋](log-analytics-log-searches.md)tooview 詳細 Service Fabric 事件資料。</span><span class="sxs-lookup"><span data-stu-id="a04cf-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
