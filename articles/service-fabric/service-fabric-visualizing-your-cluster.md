---
title: "aaaVisualizing 叢集使用 Service Fabric 總管 |Microsoft 文件"
description: "Service Fabric 總管是一種 Web 型工具，可檢查和管理 Microsoft Azure Service Fabric 叢集中的雲端應用程式和節點。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="85c78-103">使用 Service Fabric 總管視覺化叢集</span><span class="sxs-lookup"><span data-stu-id="85c78-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="85c78-104">Service Fabric 總管是一個 Web 型工具，可檢查和管理 Azure Service Fabric 叢集中的應用程式與節點。</span><span class="sxs-lookup"><span data-stu-id="85c78-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="85c78-105">Service Fabric 總管是直接叢集中裝載 hello，因此永遠可使用，不論執行您的叢集。</span><span class="sxs-lookup"><span data-stu-id="85c78-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="85c78-106">影片教學課程</span><span class="sxs-lookup"><span data-stu-id="85c78-106">Video tutorial</span></span>

<span data-ttu-id="85c78-107">Service Fabric 總管，toouse 的監看的 toolearn hello 遵循 Microsoft Virtual Academy 視訊：</span><span class="sxs-lookup"><span data-stu-id="85c78-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="85c78-108">連接 tooService 網狀架構總管</span><span class="sxs-lookup"><span data-stu-id="85c78-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="85c78-109">如果您已依照 hello 指示太[準備開發環境](service-fabric-get-started.md)，您可以在本機叢集上啟動 Service Fabric 總管瀏覽 toohttp://localhost:19080 / 總管。</span><span class="sxs-lookup"><span data-stu-id="85c78-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="85c78-110">了解 hello Service Fabric 總管版面配置</span><span class="sxs-lookup"><span data-stu-id="85c78-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="85c78-111">您可以在 hello 左邊使用 hello 樹狀結構來巡覽 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="85c78-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="85c78-112">Hello hello 樹狀結構根目錄之，在 hello 叢集儀表板會提供您的叢集，包括應用程式和節點健全狀況摘要的概觀。</span><span class="sxs-lookup"><span data-stu-id="85c78-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Service Fabric 總管叢集儀表板][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="85c78-114">檢視 hello 叢集配置</span><span class="sxs-lookup"><span data-stu-id="85c78-114">View hello cluster's layout</span></span>
<span data-ttu-id="85c78-115">Service Fabric 叢集中的節點會橫跨容錯網域和升級網域的二維方格放置。</span><span class="sxs-lookup"><span data-stu-id="85c78-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="85c78-116">這個位置可確保您的應用程式仍可在硬體故障和應用程式升級 hello 存在。</span><span class="sxs-lookup"><span data-stu-id="85c78-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="85c78-117">您可以檢視如何使用 hello 叢集對應配置 hello 目前的叢集。</span><span class="sxs-lookup"><span data-stu-id="85c78-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![Service Fabric 總管叢集對應][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="85c78-119">檢視應用程式和服務</span><span class="sxs-lookup"><span data-stu-id="85c78-119">View applications and services</span></span>
<span data-ttu-id="85c78-120">hello 叢集包含兩個子樹： 一個適用於應用程式，而另一個節點。</span><span class="sxs-lookup"><span data-stu-id="85c78-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="85c78-121">您可以使用透過 Service Fabric 的邏輯階層 hello 應用程式檢視 toonavigate： 應用程式、 服務、 資料分割和複本。</span><span class="sxs-lookup"><span data-stu-id="85c78-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="85c78-122">Hello 下列範例中，在 hello 應用程式**MyApp**包含兩個服務， **MyStatefulService**和**WebService**。</span><span class="sxs-lookup"><span data-stu-id="85c78-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="85c78-123">由於 **MyStatefulService** 可設定狀態，因此它包含一個具有一個主要複本和兩個次要複本的資料分割。</span><span class="sxs-lookup"><span data-stu-id="85c78-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="85c78-124">對比之下，WebSvcService 則無狀態，而且只包含單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="85c78-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Service Fabric 總管應用程式檢視][sfx-application-tree]

<span data-ttu-id="85c78-126">在 hello 樹狀結構的每個層級，hello 主窗格會顯示 hello 項目相關資訊。</span><span class="sxs-lookup"><span data-stu-id="85c78-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="85c78-127">例如，您可以看到 hello 健康狀態，以及針對特定服務的版本。</span><span class="sxs-lookup"><span data-stu-id="85c78-127">For example, you can see hello health status and version for a particular service.</span></span>

![Service Fabric 總管基本資訊窗格][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="85c78-129">檢視 hello 叢集節點</span><span class="sxs-lookup"><span data-stu-id="85c78-129">View hello cluster's nodes</span></span>
<span data-ttu-id="85c78-130">hello 節點檢視會顯示 hello 實體 hello 叢集配置。</span><span class="sxs-lookup"><span data-stu-id="85c78-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="85c78-131">對於指定的節點，您可以檢查已經在該節點上部署程式碼的應用程式。</span><span class="sxs-lookup"><span data-stu-id="85c78-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="85c78-132">更具體地說，您可以看到目前在那裡執行的複本。</span><span class="sxs-lookup"><span data-stu-id="85c78-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="85c78-133">動作</span><span class="sxs-lookup"><span data-stu-id="85c78-133">Actions</span></span>
<span data-ttu-id="85c78-134">Service Fabric 總管提供快速的方式 tooinvoke 節點、 應用程式，以及在您的叢集服務的動作。</span><span class="sxs-lookup"><span data-stu-id="85c78-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="85c78-135">例如，toodelete 應用程式執行個體中，選擇 hello 應用程式從 hello hello 左側的樹狀結構，然後選擇**動作** > **刪除應用程式**。</span><span class="sxs-lookup"><span data-stu-id="85c78-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![在 Service Fabric 總管中刪除應用程式][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="85c78-137">您可以執行相同動作 hello 按一下 hello 省略符號 下一步 tooeach 項目。</span><span class="sxs-lookup"><span data-stu-id="85c78-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="85c78-138">hello 下表列出可用的每個實體的 hello 動作：</span><span class="sxs-lookup"><span data-stu-id="85c78-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="85c78-139">**實體**</span><span class="sxs-lookup"><span data-stu-id="85c78-139">**Entity**</span></span> | <span data-ttu-id="85c78-140">**動作**</span><span class="sxs-lookup"><span data-stu-id="85c78-140">**Action**</span></span> | <span data-ttu-id="85c78-141">**說明**</span><span class="sxs-lookup"><span data-stu-id="85c78-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85c78-142">應用程式類型</span><span class="sxs-lookup"><span data-stu-id="85c78-142">Application type</span></span> |<span data-ttu-id="85c78-143">解除佈建類型</span><span class="sxs-lookup"><span data-stu-id="85c78-143">Unprovision type</span></span> |<span data-ttu-id="85c78-144">移除 hello 叢集映像存放區中的 hello 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="85c78-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="85c78-145">需要先移除該型別 toobe 的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="85c78-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="85c78-146">應用程式</span><span class="sxs-lookup"><span data-stu-id="85c78-146">Application</span></span> |<span data-ttu-id="85c78-147">刪除應用程式</span><span class="sxs-lookup"><span data-stu-id="85c78-147">Delete Application</span></span> |<span data-ttu-id="85c78-148">刪除 hello 應用程式，包括所有服務和其狀態 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="85c78-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="85c78-149">服務</span><span class="sxs-lookup"><span data-stu-id="85c78-149">Service</span></span> |<span data-ttu-id="85c78-150">刪除服務</span><span class="sxs-lookup"><span data-stu-id="85c78-150">Delete Service</span></span> |<span data-ttu-id="85c78-151">刪除 hello 服務和其狀態 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="85c78-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="85c78-152">節點</span><span class="sxs-lookup"><span data-stu-id="85c78-152">Node</span></span> |<span data-ttu-id="85c78-153">啟動</span><span class="sxs-lookup"><span data-stu-id="85c78-153">Activate</span></span> |<span data-ttu-id="85c78-154">啟動 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="85c78-154">Activate hello node.</span></span> |
| <span data-ttu-id="85c78-155">節點</span><span class="sxs-lookup"><span data-stu-id="85c78-155">Node</span></span> | <span data-ttu-id="85c78-156">停用 (暫停)</span><span class="sxs-lookup"><span data-stu-id="85c78-156">Deactivate (pause)</span></span> | <span data-ttu-id="85c78-157">暫停 hello 節點處於目前狀態。</span><span class="sxs-lookup"><span data-stu-id="85c78-157">Pause hello node in its current state.</span></span> <span data-ttu-id="85c78-158">服務繼續 toorun，但 Service Fabric 不會主動移動任何項目拖曳至或關閉它除非它是必要的 tooprevent 中斷或資料不一致。</span><span class="sxs-lookup"><span data-stu-id="85c78-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="85c78-159">這個動作是常用的 tooenable 偵錯不會移動期間檢查特定節點 tooensure 上的服務。</span><span class="sxs-lookup"><span data-stu-id="85c78-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="85c78-160">節點</span><span class="sxs-lookup"><span data-stu-id="85c78-160">Node</span></span> | <span data-ttu-id="85c78-161">停用 (重新啟動)</span><span class="sxs-lookup"><span data-stu-id="85c78-161">Deactivate (restart)</span></span> | <span data-ttu-id="85c78-162">安全地移除所有記憶體內部服務，並關閉持續性服務。</span><span class="sxs-lookup"><span data-stu-id="85c78-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="85c78-163">通常 hello 主機處理序或電腦需要 toobe 重新啟動時使用。</span><span class="sxs-lookup"><span data-stu-id="85c78-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="85c78-164">節點</span><span class="sxs-lookup"><span data-stu-id="85c78-164">Node</span></span> | <span data-ttu-id="85c78-165">停用 (移除資料)</span><span class="sxs-lookup"><span data-stu-id="85c78-165">Deactivate (remove data)</span></span> | <span data-ttu-id="85c78-166">安全地關閉 hello 節點上執行建置足夠的備援複本之後的所有服務。</span><span class="sxs-lookup"><span data-stu-id="85c78-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="85c78-167">通常於節點 (或至少其儲存體) 永久性地移除委任時使用。</span><span class="sxs-lookup"><span data-stu-id="85c78-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="85c78-168">節點</span><span class="sxs-lookup"><span data-stu-id="85c78-168">Node</span></span> | <span data-ttu-id="85c78-169">移除節點狀態</span><span class="sxs-lookup"><span data-stu-id="85c78-169">Remove node state</span></span> | <span data-ttu-id="85c78-170">從 hello 叢集移除節點的複本的知識。</span><span class="sxs-lookup"><span data-stu-id="85c78-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="85c78-171">通常在已失敗的節點被視為無法回復時使用。</span><span class="sxs-lookup"><span data-stu-id="85c78-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="85c78-172">節點</span><span class="sxs-lookup"><span data-stu-id="85c78-172">Node</span></span> | <span data-ttu-id="85c78-173">重新啟動</span><span class="sxs-lookup"><span data-stu-id="85c78-173">Restart</span></span> | <span data-ttu-id="85c78-174">重新啟動 hello 節點，以模擬在節點失敗。</span><span class="sxs-lookup"><span data-stu-id="85c78-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="85c78-175">如需詳細資訊，請參閱[這裡](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="85c78-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="85c78-176">由於許多動作所破壞性，您可能會要求您 tooconfirm 您的意圖 hello 動作完成之前。</span><span class="sxs-lookup"><span data-stu-id="85c78-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="85c78-177">可透過 Service Fabric 總管來執行每個動作也可以透過 PowerShell 或 REST API，tooenable 自動化來執行。</span><span class="sxs-lookup"><span data-stu-id="85c78-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="85c78-178">您也可以使用指定的應用程式類型和版本的 Service Fabric 總管 toocreate 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="85c78-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="85c78-179">在 hello 樹狀結構檢視中，選擇 hello 應用程式類型，然後按一下 hello**建立應用程式執行個體**連結 hello 右窗格中，您想要 下一步 toohello 版本。</span><span class="sxs-lookup"><span data-stu-id="85c78-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![在 Service Fabric Explorer 中建立應用程式執行個體][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="85c78-181">透過 Service Fabric Explorer 建立的應用程式執行個體目前無法參數化。</span><span class="sxs-lookup"><span data-stu-id="85c78-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="85c78-182">會使用預設參數值來建立它們。</span><span class="sxs-lookup"><span data-stu-id="85c78-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="85c78-183">連接 tooa 遠端 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="85c78-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="85c78-184">如果您知道 hello 叢集端點，且有足夠的權限可以從任何瀏覽器來存取 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="85c78-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="85c78-185">這是因為 Service Fabric 總管 hello 叢集中執行的只是另一個服務。</span><span class="sxs-lookup"><span data-stu-id="85c78-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="85c78-186">探索遠端叢集的 hello Service Fabric 總管端點</span><span class="sxs-lookup"><span data-stu-id="85c78-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="85c78-187">指定的叢集，tooreach Service Fabric 總管指向您的瀏覽器：</span><span class="sxs-lookup"><span data-stu-id="85c78-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="85c78-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="85c78-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="85c78-189">Azure 的叢集，hello 完整的 URL 也會提供在 hello 叢集 essentials 窗格中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="85c78-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="85c78-190">Tooa 安全叢集連線</span><span class="sxs-lookup"><span data-stu-id="85c78-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="85c78-191">您可以控制用戶端存取 tooyour Service Fabric 叢集可以使用憑證或使用 Azure Active Directory (AAD)。</span><span class="sxs-lookup"><span data-stu-id="85c78-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="85c78-192">如果您嘗試在安全的叢集上的 tooconnect tooService Fabric 總管，然後根據 hello 叢集設定您將會是需要的 toopresent 用戶端憑證或使用 AAD 登入。</span><span class="sxs-lookup"><span data-stu-id="85c78-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85c78-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85c78-193">Next steps</span></span>
* [<span data-ttu-id="85c78-194">Testability 概觀</span><span class="sxs-lookup"><span data-stu-id="85c78-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="85c78-195">在 Visual Studio 中管理 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="85c78-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="85c78-196">使用 PowerShell 部署 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="85c78-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
