---
title: "aaaHow toomonitor 雲端服務 |Microsoft 文件"
description: "了解如何 toomonitor 使用 hello Azure 傳統入口網站的雲端服務。"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a><span data-ttu-id="5869e-103">如何 tooMonitor 雲端服務</span><span class="sxs-lookup"><span data-stu-id="5869e-103">How tooMonitor Cloud Services</span></span>
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

<span data-ttu-id="5869e-104">您可以監視`key`hello Azure 傳統入口網站中的雲端服務的效能度量。</span><span class="sxs-lookup"><span data-stu-id="5869e-104">You can monitor `key` performance metrics for your cloud services in hello Azure classic portal.</span></span> <span data-ttu-id="5869e-105">您可以設定 hello，層級的監視 toominimal 和每個服務角色的詳細資訊，並且可以自訂監視顯示 hello。</span><span class="sxs-lookup"><span data-stu-id="5869e-105">You can set hello level of monitoring toominimal and verbose for each service role, and can customize hello monitoring displays.</span></span> <span data-ttu-id="5869e-106">詳細資訊監視資料會儲存在儲存體帳戶，您可以存取外部 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5869e-106">Verbose monitoring data is stored in a storage account, which you can access outside hello portal.</span></span> 

<span data-ttu-id="5869e-107">監視的顯示 hello Azure 傳統入口網站中可高度設定。</span><span class="sxs-lookup"><span data-stu-id="5869e-107">Monitoring displays in hello Azure classic portal are highly configurable.</span></span> <span data-ttu-id="5869e-108">您可以選擇 hello 度量 toomonitor hello hello 度量清單中的要**監視器** 頁面上，而且您可以選擇在度量圖表上 hello 哪些度量 tooplot**監視器**頁面和 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="5869e-108">You can choose hello metrics you want toomonitor in hello metrics list on hello **Monitor** page, and you can choose which metrics tooplot in metrics charts on hello **Monitor** page and hello dashboard.</span></span> 

## <a name="concepts"></a><span data-ttu-id="5869e-109">概念</span><span class="sxs-lookup"><span data-stu-id="5869e-109">Concepts</span></span>
<span data-ttu-id="5869e-110">根據預設，使用 hello hello 角色執行個體 （虛擬機器） 的主機作業系統所收集的效能計數器的新雲端服務提供最低監視。</span><span class="sxs-lookup"><span data-stu-id="5869e-110">By default, minimal monitoring is provided for a new cloud service using performance counters gathered from hello host operating system for hello roles instances (virtual machines).</span></span> <span data-ttu-id="5869e-111">hello 最小度量是有限的 tooCPU 百分比、 資料、 資料輸出、 磁碟讀取輸送量和磁碟寫入輸送量。</span><span class="sxs-lookup"><span data-stu-id="5869e-111">hello minimal metrics are limited tooCPU Percentage, Data In, Data Out, Disk Read Throughput, and Disk Write Throughput.</span></span> <span data-ttu-id="5869e-112">藉由設定詳細資訊監視，您可以收到 hello 虛擬機器 （角色執行個體） 內的效能資料為基礎的其他度量。</span><span class="sxs-lookup"><span data-stu-id="5869e-112">By configuring verbose monitoring, you can receive additional metrics based on performance data within hello virtual machines (role instances).</span></span> <span data-ttu-id="5869e-113">hello 詳細資訊度量啟用進一步分析的應用程式作業期間發生的問題。</span><span class="sxs-lookup"><span data-stu-id="5869e-113">hello verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="5869e-114">預設會從角色執行個體的效能計數器資料取樣，並每隔 3 分鐘傳送 hello 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="5869e-114">By default performance counter data from role instances is sampled and transferred from hello role instance at 3-minute intervals.</span></span> <span data-ttu-id="5869e-115">當您啟用詳細資訊監視時，hello 原始效能計數器資料是彙總每個角色執行個體和每個角色的角色執行個體之間的 5 分鐘、 1 小時和 12 小時的間隔。</span><span class="sxs-lookup"><span data-stu-id="5869e-115">When you enable verbose monitoring, hello raw performance counter data is aggregated for each role instance and across role instances for each role at intervals of 5 minutes, 1 hour, and 12 hours.</span></span> <span data-ttu-id="5869e-116">hello 彙總的資料都會被清除之後 10 天。</span><span class="sxs-lookup"><span data-stu-id="5869e-116">hello aggregated data is purged after 10 days.</span></span>

<span data-ttu-id="5869e-117">啟用詳細資訊監視，彙總的 hello 之後監視資料會儲存在儲存體帳戶中的資料表。</span><span class="sxs-lookup"><span data-stu-id="5869e-117">After you enable verbose monitoring, hello aggregated monitoring data is stored in tables in your storage account.</span></span> <span data-ttu-id="5869e-118">tooenable 監視角色的詳細資訊，您必須設定連結 toohello 儲存體帳戶的診斷連接字串。</span><span class="sxs-lookup"><span data-stu-id="5869e-118">tooenable verbose monitoring for a role, you must configure a diagnostics connection string that links toohello storage account.</span></span> <span data-ttu-id="5869e-119">您可以對於不同的角色使用不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5869e-119">You can use different storage accounts for different roles.</span></span>

<span data-ttu-id="5869e-120">啟用詳細資訊監視會增加儲存成本相關 toodata 儲存體、 資料傳輸和儲存體交易。</span><span class="sxs-lookup"><span data-stu-id="5869e-120">Enabling verbose monitoring increases your storage costs related toodata storage, data transfer, and storage transactions.</span></span> <span data-ttu-id="5869e-121">最小監視不需要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5869e-121">Minimal monitoring does not require a storage account.</span></span> <span data-ttu-id="5869e-122">會公開在 hello 最小監視層級的 hello 度量的 hello 資料不儲存在儲存體帳戶，即使您設定監視層級 tooverbose hello。</span><span class="sxs-lookup"><span data-stu-id="5869e-122">hello data for hello metrics that are exposed at hello minimal monitoring level are not stored in your storage account, even if you set hello monitoring level tooverbose.</span></span>

## <a name="how-to-configure-monitoring-for-cloud-services"></a><span data-ttu-id="5869e-123">做法：為雲端服務設定監視功能</span><span class="sxs-lookup"><span data-stu-id="5869e-123">How to: Configure monitoring for cloud services</span></span>
<span data-ttu-id="5869e-124">使用下列程序 tooconfigure 詳細資訊或最小監視 hello Azure 傳統入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="5869e-124">Use hello following procedures tooconfigure verbose or minimal monitoring in hello Azure classic portal.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="5869e-125">開始之前</span><span class="sxs-lookup"><span data-stu-id="5869e-125">Before you begin</span></span>
* <span data-ttu-id="5869e-126">建立*傳統*監視資料的儲存體帳戶 toostore hello。</span><span class="sxs-lookup"><span data-stu-id="5869e-126">Create a *classic* storage account toostore hello monitoring data.</span></span> <span data-ttu-id="5869e-127">您可以對於不同的角色使用不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5869e-127">You can use different storage accounts for different roles.</span></span> <span data-ttu-id="5869e-128">如需詳細資訊，請參閱[如何 toocreate 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="5869e-128">For more information, see [How toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="5869e-129">對於雲端服務角色啟用 Azure 診斷。</span><span class="sxs-lookup"><span data-stu-id="5869e-129">Enable Azure Diagnostics for your cloud service roles.</span></span> <span data-ttu-id="5869e-130">請參閱「 [為雲端服務設定診斷功能](cloud-services-dotnet-diagnostics.md)」。</span><span class="sxs-lookup"><span data-stu-id="5869e-130">See [Configuring Diagnostics for Cloud Services](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="5869e-131">請確認 hello 診斷連接字串中已有 hello 角色組態。</span><span class="sxs-lookup"><span data-stu-id="5869e-131">Ensure that hello diagnostics connection string is present in hello Role configuration.</span></span> <span data-ttu-id="5869e-132">您無法開啟詳細資訊監視，直到您啟用 Azure 診斷，並包含在 hello 角色設定中的診斷連接字串。</span><span class="sxs-lookup"><span data-stu-id="5869e-132">You cannot turn on verbose monitoring until you enable Azure Diagnostics and include a diagnostics connection string in hello Role configuration.</span></span>   

> [!NOTE]
> <span data-ttu-id="5869e-133">目標為 Azure SDK 2.5 專案未自動 hello 診斷連接字串中包含 hello 專案範本。</span><span class="sxs-lookup"><span data-stu-id="5869e-133">Projects targeting Azure SDK 2.5 did not automatically include hello diagnostics connection string in hello project template.</span></span> <span data-ttu-id="5869e-134">這些專案，您需要 toomanually 新增 hello 診斷連接字串 toohello 角色組態。</span><span class="sxs-lookup"><span data-stu-id="5869e-134">For these projects, you need toomanually add hello diagnostics connection string toohello Role configuration.</span></span>
> 
> 

<span data-ttu-id="5869e-135">**toomanually 新增診斷連接字串 tooRole 組態**</span><span class="sxs-lookup"><span data-stu-id="5869e-135">**toomanually add diagnostics connection string tooRole configuration**</span></span>

1. <span data-ttu-id="5869e-136">在 Visual Studio 中開啟 hello 雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="5869e-136">Open hello Cloud Service project in Visual Studio</span></span>
2. <span data-ttu-id="5869e-137">按兩下 hello**角色**tooopen hello 角色設計工具，然後選取 hello**設定** 索引標籤</span><span class="sxs-lookup"><span data-stu-id="5869e-137">Double-click on hello **Role** tooopen hello Role designer and select hello **Settings** tab</span></span>
3. <span data-ttu-id="5869e-138">尋找名為 **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**的設定。</span><span class="sxs-lookup"><span data-stu-id="5869e-138">Look for a setting named **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**.</span></span> 
4. <span data-ttu-id="5869e-139">如果此設定不存在，按一下 上 hello**加入設定**按鈕 tooadd 它 toohello 設定及變更 hello 類型 hello 新設定太**ConnectionString**</span><span class="sxs-lookup"><span data-stu-id="5869e-139">If this setting is not present, click on hello **Add Setting** button tooadd it toohello configuration and change hello type for hello new setting too**ConnectionString**</span></span>
5. <span data-ttu-id="5869e-140">Hello 上的 [設定連接字串 hello hello 值**...** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5869e-140">Set hello value for connection string hello by clicking on hello **...** button.</span></span> <span data-ttu-id="5869e-141">儲存體帳戶，這會開啟一個對話方塊，可讓您 tooselect 中。</span><span class="sxs-lookup"><span data-stu-id="5869e-141">This will open up a dialog allowing you tooselect a storage account.</span></span>
   
    ![Visual Studio 設定](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a><span data-ttu-id="5869e-143">監視層級 tooverbose toochange hello 或最小</span><span class="sxs-lookup"><span data-stu-id="5869e-143">toochange hello monitoring level tooverbose or minimal</span></span>
1. <span data-ttu-id="5869e-144">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，開啟 hello**設定**hello 雲端服務部署的頁面。</span><span class="sxs-lookup"><span data-stu-id="5869e-144">In hello [Azure classic portal](https://manage.windowsazure.com/), open hello **Configure** page for hello cloud service deployment.</span></span>
2. <span data-ttu-id="5869e-145">在 [層級] 中，按一下 [詳細資訊] 或 [最小]。</span><span class="sxs-lookup"><span data-stu-id="5869e-145">In **Level**, click **Verbose** or **Minimal**.</span></span> 
3. <span data-ttu-id="5869e-146">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5869e-146">Click **Save**.</span></span>

<span data-ttu-id="5869e-147">開啟詳細資訊監視之後，您應該會開始看到 hello hello 一小時內監視 hello Azure 傳統入口網站中的資料。</span><span class="sxs-lookup"><span data-stu-id="5869e-147">After you turn on verbose monitoring, you should start seeing hello monitoring data in hello Azure classic portal within hello hour.</span></span>

<span data-ttu-id="5869e-148">hello 原始效能計數器資料和彙總監視的資料會儲存在 hello hello 部署識別碼 hello 角色所限定的資料表中的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5869e-148">hello raw performance counter data and aggregated monitoring data are stored in hello storage account in tables qualified by hello deployment ID for hello roles.</span></span> 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a><span data-ttu-id="5869e-149">做法：接收雲端服務計量的警示</span><span class="sxs-lookup"><span data-stu-id="5869e-149">How to: Receive alerts for cloud service metrics</span></span>
<span data-ttu-id="5869e-150">您可以按照雲端服務監視度量接收警示。</span><span class="sxs-lookup"><span data-stu-id="5869e-150">You can receive alerts based on your cloud service monitoring metrics.</span></span> <span data-ttu-id="5869e-151">在 hello**管理服務**頁面 hello Azure 傳統入口網站，您可以建立規則 tootrigger 警示，當您選擇的 hello 度量到達您所指定的值。</span><span class="sxs-lookup"><span data-stu-id="5869e-151">On hello **Management Services** page of hello Azure classic portal, you can create a rule tootrigger an alert when hello metric you choose reaches a value that you specify.</span></span> <span data-ttu-id="5869e-152">您也可以選擇傳送嗨在警示觸發時 toohave 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="5869e-152">You can also choose toohave email sent when hello alert is triggered.</span></span> <span data-ttu-id="5869e-153">如需詳細資訊，請參閱 [做法：在 Azure 中接收警示通知及管理警示規則](http://go.microsoft.com/fwlink/?LinkId=309356)。</span><span class="sxs-lookup"><span data-stu-id="5869e-153">For more information, see [How to: Receive Alert Notifications and Manage Alert Rules in Azure](http://go.microsoft.com/fwlink/?LinkId=309356).</span></span>

## <a name="how-to-add-metrics-toohello-metrics-table"></a><span data-ttu-id="5869e-154">如何： 加入度量 toohello 度量資料表</span><span class="sxs-lookup"><span data-stu-id="5869e-154">How to: Add metrics toohello metrics table</span></span>
1. <span data-ttu-id="5869e-155">在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，開啟 hello**監視器**hello 雲端服務的頁面。</span><span class="sxs-lookup"><span data-stu-id="5869e-155">In hello [Azure classic portal](http://manage.windowsazure.com/), open hello **Monitor** page for hello cloud service.</span></span>
   
    <span data-ttu-id="5869e-156">根據預設，hello 度量表會顯示 hello 可用度量的子集。</span><span class="sxs-lookup"><span data-stu-id="5869e-156">By default, hello metrics table displays a subset of hello available metrics.</span></span> <span data-ttu-id="5869e-157">hello 圖會顯示 hello 預設詳細資訊度量的雲端服務，也就是限制的 toohello Memory\Available MBytes 效能計數器，其中在 hello 角色層級彙總的資料。</span><span class="sxs-lookup"><span data-stu-id="5869e-157">hello illustration shows hello default verbose metrics for a cloud service, which is limited toohello Memory\Available MBytes performance counter, with data aggregated at hello role level.</span></span> <span data-ttu-id="5869e-158">使用**加入度量**tooselect 其他彙總並在角色層級度量 toomonitor hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="5869e-158">Use **Add Metrics** tooselect additional aggregate and role-level metrics toomonitor in hello Azure classic portal.</span></span>
   
    ![詳細資訊顯示](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. <span data-ttu-id="5869e-160">tooadd 度量 toohello 計量表：</span><span class="sxs-lookup"><span data-stu-id="5869e-160">tooadd metrics toohello metrics table:</span></span>
   
   1. <span data-ttu-id="5869e-161">按一下**加入度量**tooopen **選擇度量**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5869e-161">Click **Add Metrics** tooopen **Choose Metrics**, shown below.</span></span>
      
       <span data-ttu-id="5869e-162">hello 第一個可用的度量是展開的 tooshow 可用的選項。</span><span class="sxs-lookup"><span data-stu-id="5869e-162">hello first available metric is expanded tooshow options that are available.</span></span> <span data-ttu-id="5869e-163">每個度量，hello top 選項會顯示所有角色的彙總監視資料。</span><span class="sxs-lookup"><span data-stu-id="5869e-163">For each metric, hello top option displays aggregated monitoring data for all roles.</span></span> <span data-ttu-id="5869e-164">此外，您可以選擇個別角色 toodisplay 資料。</span><span class="sxs-lookup"><span data-stu-id="5869e-164">In addition, you can choose individual roles toodisplay data for.</span></span>
      
       ![Add metrics](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. <span data-ttu-id="5869e-166">tooselect 度量 toodisplay</span><span class="sxs-lookup"><span data-stu-id="5869e-166">tooselect metrics toodisplay</span></span>
      
      * <span data-ttu-id="5869e-167">按一下向下箭號的 hello 的 hello 度量 tooexpand hello 監視選項。</span><span class="sxs-lookup"><span data-stu-id="5869e-167">Click hello down arrow by hello metric tooexpand hello monitoring options.</span></span>
      * <span data-ttu-id="5869e-168">選取 hello 核取方塊，每個監視您想要 toodisplay 選項。</span><span class="sxs-lookup"><span data-stu-id="5869e-168">Select hello check box for each monitoring option you want toodisplay.</span></span>
        
        <span data-ttu-id="5869e-169">您可以向上 too50 度量 hello 度量資料表中顯示。</span><span class="sxs-lookup"><span data-stu-id="5869e-169">You can display up too50 metrics in hello metrics table.</span></span>
        
        > [!TIP]
        > <span data-ttu-id="5869e-170">在設定監視的詳細資訊，hello 度量清單可以包含數十個度量。</span><span class="sxs-lookup"><span data-stu-id="5869e-170">In verbose monitoring, hello metrics list can contain dozens of metrics.</span></span> <span data-ttu-id="5869e-171">toodisplay 捲軸，暫留在 [hello] 對話方塊中的 hello 右側。</span><span class="sxs-lookup"><span data-stu-id="5869e-171">toodisplay a scrollbar, hover over hello right side of hello dialog box.</span></span> <span data-ttu-id="5869e-172">toofilter hello 清單中，按一下 hello 搜尋圖示，並在 hello 搜尋方塊中輸入文字，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5869e-172">toofilter hello list, click hello search icon, and enter text in hello search box, as shown below.</span></span>
        > 
        > 
        
        ![加入度量搜尋](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. <span data-ttu-id="5869e-174">完成選取度量後，按一下 [確定] \(核取記號)。</span><span class="sxs-lookup"><span data-stu-id="5869e-174">After you finish selecting metrics, click OK (checkmark).</span></span>
   
    <span data-ttu-id="5869e-175">hello 選定的度量會加入 toohello 度量資料表，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5869e-175">hello selected metrics are added toohello metrics table, as shown below.</span></span>
   
    ![監視度量](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. <span data-ttu-id="5869e-177">toodelete 度量，以從 hello 度量資料表中，按一下 hello 度量 tooselect，再按**刪除度量**。</span><span class="sxs-lookup"><span data-stu-id="5869e-177">toodelete a metric from hello metrics table, click hello metric tooselect it, and then click **Delete Metric**.</span></span> <span data-ttu-id="5869e-178">(只有在您選取度量時，才會看見 [刪除度量]。)</span><span class="sxs-lookup"><span data-stu-id="5869e-178">(You only see **Delete Metric** when you have a metric selected.)</span></span>

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a><span data-ttu-id="5869e-179">tooadd 自訂度量 toohello 度量資料表</span><span class="sxs-lookup"><span data-stu-id="5869e-179">tooadd custom metrics toohello metrics table</span></span>
<span data-ttu-id="5869e-180">hello **Verbose**監視層級提供一份您可以監視的預設計量 hello 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="5869e-180">hello **Verbose** monitoring level provides a list of default metrics that you can monitor on hello portal.</span></span> <span data-ttu-id="5869e-181">此外 toothese 您可以監視的任何自訂的度量或透過 hello 入口網站應用程式所定義的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="5869e-181">In addition toothese you can monitor any custom metrics or performance counters defined by your application through hello portal.</span></span>

<span data-ttu-id="5869e-182">hello 下列步驟假設您已開啟**Verbose**監視層級，並且已設定您的應用程式 toocollect 和傳送自訂效能計數器。</span><span class="sxs-lookup"><span data-stu-id="5869e-182">hello following steps assume that you have turned on **Verbose** monitoring level and have configured your application toocollect and transfer custom performance counters.</span></span> 

<span data-ttu-id="5869e-183">toodisplay hello 自訂效能計數器中的 hello 需要 tooupdate hello 設定 wad 控制項容器中的入口網站：</span><span class="sxs-lookup"><span data-stu-id="5869e-183">toodisplay hello custom performance counters in hello portal you need tooupdate hello configuration in wad-control-container:</span></span>

1. <span data-ttu-id="5869e-184">開啟您的診斷儲存體帳戶中的 hello wad 控制項容器的 blob。</span><span class="sxs-lookup"><span data-stu-id="5869e-184">Open hello wad-control-container blob in your diagnostics storage account.</span></span> <span data-ttu-id="5869e-185">您可以使用 Visual Studio 或任何其他儲存體總管 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="5869e-185">You can use Visual Studio or any other storage explorer toodo this.</span></span>
   
    ![Visual Studio 伺服器總管](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. <span data-ttu-id="5869e-187">瀏覽 hello blob 路徑使用 hello 模式**DeploymentId/RoleName/RoleInstance** toofind hello 設定角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="5869e-187">Navigate hello blob path using hello pattern **DeploymentId/RoleName/RoleInstance** toofind hello configuration for your role instance.</span></span> 
   
    ![Visual Studio 儲存體總管](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. <span data-ttu-id="5869e-189">下載您的角色執行個體的 hello 組態檔，並更新 tooinclude 任何自訂效能計數器。</span><span class="sxs-lookup"><span data-stu-id="5869e-189">Download hello configuration file for your role instance and update it tooinclude any custom performance counters.</span></span> <span data-ttu-id="5869e-190">例如 toomonitor *Disk Write Bytes/sec* hello *C 磁碟機*新增下的 hello 下列**PerformanceCounters\Subscriptions**節點</span><span class="sxs-lookup"><span data-stu-id="5869e-190">For example toomonitor *Disk Write Bytes/sec* for hello *C drive* add hello following under **PerformanceCounters\Subscriptions** node</span></span>
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. <span data-ttu-id="5869e-191">儲存 hello 變更以及上傳 hello 設定檔後 toohello 相同的位置覆寫 hello hello blob 中現有的檔案。</span><span class="sxs-lookup"><span data-stu-id="5869e-191">Save hello changes and upload hello configuration file back toohello same location overwriting hello existing file in hello blob.</span></span>
5. <span data-ttu-id="5869e-192">切換 tooVerbose hello Azure 傳統入口網站設定中的模式。</span><span class="sxs-lookup"><span data-stu-id="5869e-192">Toggle tooVerbose mode in hello Azure classic portal configuration.</span></span> <span data-ttu-id="5869e-193">如果您已經以詳細資訊模式將會有 tootoggle toominimal 來回 tooverbose。</span><span class="sxs-lookup"><span data-stu-id="5869e-193">If you were in Verbose mode already you will have tootoggle toominimal and back tooverbose.</span></span>
6. <span data-ttu-id="5869e-194">hello 自訂效能計數器將會出現在 [hello**加入度量**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5869e-194">hello custom performance counter will now be available in hello **Add Metrics** dialog box.</span></span> 

## <a name="how-to-customize-hello-metrics-chart"></a><span data-ttu-id="5869e-195">如何： 自訂 hello 度量圖表</span><span class="sxs-lookup"><span data-stu-id="5869e-195">How to: Customize hello metrics chart</span></span>
1. <span data-ttu-id="5869e-196">在 hello 度量資料表中，選取 too6 度量 tooplot hello 度量圖表上。</span><span class="sxs-lookup"><span data-stu-id="5869e-196">In hello metrics table, select up too6 metrics tooplot on hello metrics chart.</span></span> <span data-ttu-id="5869e-197">tooselect 公制，請按一下左側的 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5869e-197">tooselect a metric, click hello check box on its left side.</span></span> <span data-ttu-id="5869e-198">tooremove hello 度量圖表中，從度量資訊，請清除其 hello 度量資料表中的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5869e-198">tooremove a metric from hello metrics chart, clear its check box in hello metrics table.</span></span>
   
    <span data-ttu-id="5869e-199">當您 hello 度量資料表中選取度量，hello 度量隨即新增 toohello 度量圖表。</span><span class="sxs-lookup"><span data-stu-id="5869e-199">As you select metrics in hello metrics table, hello metrics are added toohello metrics chart.</span></span> <span data-ttu-id="5869e-200">在窄的顯示器上**多個 n**下拉式清單包含標準標頭不適合 hello 顯示。</span><span class="sxs-lookup"><span data-stu-id="5869e-200">On a narrow display, an **n more** drop-down list contains metric headers that won't fit hello display.</span></span>
2. <span data-ttu-id="5869e-201">相對的值 （只針對每個標準的最終值） 和絕對值 （Y 軸顯示） 顯示之間 tooswitch 選取相對或絕對頂端 hello hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="5869e-201">tooswitch between displaying relative values (final value only for each metric) and absolute values (Y axis displayed), select Relative or Absolute at hello top of hello chart.</span></span>
   
    ![相對或絕對](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. <span data-ttu-id="5869e-203">toochange hello 時間範圍 hello 度量圖表會顯示中，選取 1 小時、 24 小時或 7 天在 hello hello 圖表的頂端。</span><span class="sxs-lookup"><span data-stu-id="5869e-203">toochange hello time range hello metrics chart displays, select 1 hour, 24 hours, or 7 days at hello top of hello chart.</span></span>
   
    ![監視顯示期間](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    <span data-ttu-id="5869e-205">在 hello 儀表板的度量圖表上繪製的度量的 hello 方法會不同。</span><span class="sxs-lookup"><span data-stu-id="5869e-205">On hello dashboard metrics chart, hello method for plotting metrics is different.</span></span> <span data-ttu-id="5869e-206">一組標準度量可和度量資訊會加入或移除選取 hello 度量標頭。</span><span class="sxs-lookup"><span data-stu-id="5869e-206">A standard set of metrics is available, and metrics are added or removed by selecting hello metric header.</span></span>

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a><span data-ttu-id="5869e-207">hello 儀表板上 toocustomize hello 度量圖表</span><span class="sxs-lookup"><span data-stu-id="5869e-207">toocustomize hello metrics chart on hello dashboard</span></span>
1. <span data-ttu-id="5869e-208">開啟 hello 雲端服務的 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="5869e-208">Open hello dashboard for hello cloud service.</span></span>
2. <span data-ttu-id="5869e-209">從新增或移除度量 hello 圖表：</span><span class="sxs-lookup"><span data-stu-id="5869e-209">Add or remove metrics from hello chart:</span></span>
   
   * <span data-ttu-id="5869e-210">tooplot hello 圖表標頭中的 hello 度量新 hello 度量，請選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5869e-210">tooplot a new metric, select hello check box for hello metric in hello chart headers.</span></span> <span data-ttu-id="5869e-211">窄的顯示畫面中，按一下向下箭號的 hello  ***n* ??度量**tooplot 度量 hello 圖表標頭區域無法顯示。</span><span class="sxs-lookup"><span data-stu-id="5869e-211">On a narrow display, click hello down arrow by ***n*??metrics** tooplot a metric hello chart header area can't display.</span></span>
   * <span data-ttu-id="5869e-212">toodelete 在 hello 圖上，清除 hello 核取方塊，其標頭所繪製的度量。</span><span class="sxs-lookup"><span data-stu-id="5869e-212">toodelete a metric that is plotted on hello chart, clear hello check box by its header.</span></span>
   
3. <span data-ttu-id="5869e-213">切換 [相對] 和 [絕對] 顯示。</span><span class="sxs-lookup"><span data-stu-id="5869e-213">Switch between **Relative** and **Absolute** displays.</span></span>
4. <span data-ttu-id="5869e-214">選擇 1 小時、 24 小時或 7 天的資料 toodisplay。</span><span class="sxs-lookup"><span data-stu-id="5869e-214">Choose 1 hour, 24 hours, or 7 days of data toodisplay.</span></span>

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a><span data-ttu-id="5869e-215">如何： 存取外部 hello Azure 傳統入口網站的詳細資訊監視資料</span><span class="sxs-lookup"><span data-stu-id="5869e-215">How to: Access verbose monitoring data outside hello Azure classic portal</span></span>
<span data-ttu-id="5869e-216">詳細資訊監視資料會儲存在您指定每個角色的 hello 儲存體帳戶中的資料表。</span><span class="sxs-lookup"><span data-stu-id="5869e-216">Verbose monitoring data is stored in tables in hello storage accounts that you specify for each role.</span></span> <span data-ttu-id="5869e-217">每個雲端服務部署中，六個資料表會針對建立 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="5869e-217">For each cloud service deployment, six tables are created for hello role.</span></span> <span data-ttu-id="5869e-218">個別 (5 分鐘、1 小時和 12 小時) 建立 2 個表格。</span><span class="sxs-lookup"><span data-stu-id="5869e-218">Two tables are created for each (5 minutes, 1 hour, and 12 hours).</span></span> <span data-ttu-id="5869e-219">其中一個資料表會儲存角色層級彙總。hello 角色執行個體的其他資料表存放區的彙總。</span><span class="sxs-lookup"><span data-stu-id="5869e-219">One of these tables stores role-level aggregations; hello other table stores aggregations for role instances.</span></span> 

<span data-ttu-id="5869e-220">hello 資料表名稱具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="5869e-220">hello table names have hello following format:</span></span>

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

<span data-ttu-id="5869e-221">其中：</span><span class="sxs-lookup"><span data-stu-id="5869e-221">where:</span></span>

* <span data-ttu-id="5869e-222">*deploymentID*為 hello 分派 toohello 雲端服務部署的 GUID</span><span class="sxs-lookup"><span data-stu-id="5869e-222">*deploymentID* is hello GUID assigned toohello cloud service deployment</span></span>
* <span data-ttu-id="5869e-223">aggregation_interval = 5M、1H 或 12H</span><span class="sxs-lookup"><span data-stu-id="5869e-223">*aggregation_interval* = 5M, 1H, or 12H</span></span>
* <span data-ttu-id="5869e-224">角色層級彙總 = R</span><span class="sxs-lookup"><span data-stu-id="5869e-224">role-level aggregations = R</span></span>
* <span data-ttu-id="5869e-225">角色執行個體彙總 = RI</span><span class="sxs-lookup"><span data-stu-id="5869e-225">aggregations for role instances = RI</span></span>

<span data-ttu-id="5869e-226">例如，hello 下列資料表會儲存在 1 小時的時間間隔的彙總資料的詳細資訊監視資料：</span><span class="sxs-lookup"><span data-stu-id="5869e-226">For example, hello following tables would store verbose monitoring data aggregated at 1-hour intervals:</span></span>

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
