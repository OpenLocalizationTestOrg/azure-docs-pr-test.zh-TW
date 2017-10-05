---
title: "使用 Service Fabric 總管視覺化叢集 | Microsoft Docs"
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
ms.openlocfilehash: 789793a7f50170188d688881a9178546c3074018
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="59a20-103">使用 Service Fabric 總管視覺化叢集</span><span class="sxs-lookup"><span data-stu-id="59a20-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="59a20-104">Service Fabric 總管是一個 Web 型工具，可檢查和管理 Azure Service Fabric 叢集中的應用程式與節點。</span><span class="sxs-lookup"><span data-stu-id="59a20-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="59a20-105">Service Fabric 總管直接裝載於叢集內，因此不論您的叢集在何處執行，它都一律可供使用。</span><span class="sxs-lookup"><span data-stu-id="59a20-105">Service Fabric Explorer is hosted directly within the cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="59a20-106">影片教學課程</span><span class="sxs-lookup"><span data-stu-id="59a20-106">Video tutorial</span></span>

<span data-ttu-id="59a20-107">若要了解如何使用 Service Fabric Explorer，請觀賞下列 Microsoft Virtual Academy 影片︰</span><span class="sxs-lookup"><span data-stu-id="59a20-107">To learn how to use Service Fabric Explorer, watch the following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-to-service-fabric-explorer"></a><span data-ttu-id="59a20-108">連線到 Service Fabric 總管</span><span class="sxs-lookup"><span data-stu-id="59a20-108">Connect to Service Fabric Explorer</span></span>
<span data-ttu-id="59a20-109">如果您已依照[準備開發環境](service-fabric-get-started.md)的指示操作，可以瀏覽至 http://localhost:19080/Explorer，啟動您本機叢集上的 [Service Fabric 總管]。</span><span class="sxs-lookup"><span data-stu-id="59a20-109">If you have followed the instructions to [prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating to http://localhost:19080/Explorer.</span></span>

## <a name="understand-the-service-fabric-explorer-layout"></a><span data-ttu-id="59a20-110">了解 Service Fabric 總管配置</span><span class="sxs-lookup"><span data-stu-id="59a20-110">Understand the Service Fabric Explorer layout</span></span>
<span data-ttu-id="59a20-111">您可以使用左邊的樹狀目錄來瀏覽 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="59a20-111">You can navigate through Service Fabric Explorer by using the tree on the left.</span></span> <span data-ttu-id="59a20-112">在樹狀目錄的根目錄，叢集儀表板會提供您叢集的概觀，包括應用程式和節點健康情況的摘要。</span><span class="sxs-lookup"><span data-stu-id="59a20-112">At the root of the tree, the cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Service Fabric 總管叢集儀表板][sfx-cluster-dashboard]

### <a name="view-the-clusters-layout"></a><span data-ttu-id="59a20-114">檢視叢集的配置</span><span class="sxs-lookup"><span data-stu-id="59a20-114">View the cluster's layout</span></span>
<span data-ttu-id="59a20-115">Service Fabric 叢集中的節點會橫跨容錯網域和升級網域的二維方格放置。</span><span class="sxs-lookup"><span data-stu-id="59a20-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="59a20-116">這個位置可確保您的應用程式在發生硬體故障及應用程式升級時仍然可用。</span><span class="sxs-lookup"><span data-stu-id="59a20-116">This placement ensures that your applications remain available in the presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="59a20-117">您可以使用叢集對應檢視目前叢集的配置方式。</span><span class="sxs-lookup"><span data-stu-id="59a20-117">You can view how the current cluster is laid out by using the cluster map.</span></span>

![Service Fabric 總管叢集對應][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="59a20-119">檢視應用程式和服務</span><span class="sxs-lookup"><span data-stu-id="59a20-119">View applications and services</span></span>
<span data-ttu-id="59a20-120">叢集包含兩個樹狀子目錄：一個用於應用程式，另一個用於節點。</span><span class="sxs-lookup"><span data-stu-id="59a20-120">The cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="59a20-121">您可以使用應用程式檢視瀏覽 Service Fabric 的邏輯階層：應用程式、服務、資料分割，以及複本。</span><span class="sxs-lookup"><span data-stu-id="59a20-121">You can use the application view to navigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="59a20-122">在以下範例中，**MyApp** 應用程式是由 **MyStatefulService** 與 **WebService** 兩個服務組成。</span><span class="sxs-lookup"><span data-stu-id="59a20-122">In the example below, the application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="59a20-123">由於 **MyStatefulService** 可設定狀態，因此它包含一個具有一個主要複本和兩個次要複本的資料分割。</span><span class="sxs-lookup"><span data-stu-id="59a20-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="59a20-124">對比之下，WebSvcService 則無狀態，而且只包含單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="59a20-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Service Fabric 總管應用程式檢視][sfx-application-tree]

<span data-ttu-id="59a20-126">在樹狀目錄的每個層級，主要窗格會顯示項目的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="59a20-126">At each level of the tree, the main pane shows pertinent information about the item.</span></span> <span data-ttu-id="59a20-127">例如，您可以看到特定服務的健康狀態和版本。</span><span class="sxs-lookup"><span data-stu-id="59a20-127">For example, you can see the health status and version for a particular service.</span></span>

![Service Fabric 總管基本資訊窗格][sfx-service-essentials]

### <a name="view-the-clusters-nodes"></a><span data-ttu-id="59a20-129">檢視叢集的節點</span><span class="sxs-lookup"><span data-stu-id="59a20-129">View the cluster's nodes</span></span>
<span data-ttu-id="59a20-130">節點檢視會顯示叢集的實體配置。</span><span class="sxs-lookup"><span data-stu-id="59a20-130">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="59a20-131">對於指定的節點，您可以檢查已經在該節點上部署程式碼的應用程式。</span><span class="sxs-lookup"><span data-stu-id="59a20-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="59a20-132">更具體地說，您可以看到目前在那裡執行的複本。</span><span class="sxs-lookup"><span data-stu-id="59a20-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="59a20-133">動作</span><span class="sxs-lookup"><span data-stu-id="59a20-133">Actions</span></span>
<span data-ttu-id="59a20-134">「Service Fabric 總管」提供一個對您叢集內的節點、應用程式及服務快速叫用動作的方式。</span><span class="sxs-lookup"><span data-stu-id="59a20-134">Service Fabric Explorer offers a quick way to invoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="59a20-135">例如，若要刪除某個應用程式執行個體，請從左邊的樹狀目錄選擇該應用程式，然後選擇 [動作] > [刪除應用程式]。</span><span class="sxs-lookup"><span data-stu-id="59a20-135">For example, to delete an application instance, choose the application from the tree on the left, and then choose **Actions** > **Delete Application**.</span></span>

![在 Service Fabric 總管中刪除應用程式][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="59a20-137">您可以按下每個元素旁邊的省略符號來執行相同動作。</span><span class="sxs-lookup"><span data-stu-id="59a20-137">You can perform the same actions by clicking the ellipsis next to each element.</span></span>
>
>

<span data-ttu-id="59a20-138">下表列出每個實體的可用動作：</span><span class="sxs-lookup"><span data-stu-id="59a20-138">The following table lists the actions available for each entity:</span></span>

| <span data-ttu-id="59a20-139">**實體**</span><span class="sxs-lookup"><span data-stu-id="59a20-139">**Entity**</span></span> | <span data-ttu-id="59a20-140">**動作**</span><span class="sxs-lookup"><span data-stu-id="59a20-140">**Action**</span></span> | <span data-ttu-id="59a20-141">**說明**</span><span class="sxs-lookup"><span data-stu-id="59a20-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="59a20-142">應用程式類型</span><span class="sxs-lookup"><span data-stu-id="59a20-142">Application type</span></span> |<span data-ttu-id="59a20-143">解除佈建類型</span><span class="sxs-lookup"><span data-stu-id="59a20-143">Unprovision type</span></span> |<span data-ttu-id="59a20-144">從叢集的映像存放區中移除應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="59a20-144">Removes the application package from the cluster's image store.</span></span> <span data-ttu-id="59a20-145">需要先移除該類型的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="59a20-145">Requires all applications of that type to be removed first.</span></span> |
| <span data-ttu-id="59a20-146">應用程式</span><span class="sxs-lookup"><span data-stu-id="59a20-146">Application</span></span> |<span data-ttu-id="59a20-147">刪除應用程式</span><span class="sxs-lookup"><span data-stu-id="59a20-147">Delete Application</span></span> |<span data-ttu-id="59a20-148">刪除應用程式，包括其所有的服務，以及狀態 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="59a20-148">Delete the application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="59a20-149">服務</span><span class="sxs-lookup"><span data-stu-id="59a20-149">Service</span></span> |<span data-ttu-id="59a20-150">刪除服務</span><span class="sxs-lookup"><span data-stu-id="59a20-150">Delete Service</span></span> |<span data-ttu-id="59a20-151">刪除服務和其狀態 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="59a20-151">Delete the service and its state (if any).</span></span> |
| <span data-ttu-id="59a20-152">節點</span><span class="sxs-lookup"><span data-stu-id="59a20-152">Node</span></span> |<span data-ttu-id="59a20-153">啟動</span><span class="sxs-lookup"><span data-stu-id="59a20-153">Activate</span></span> |<span data-ttu-id="59a20-154">啟動節點。</span><span class="sxs-lookup"><span data-stu-id="59a20-154">Activate the node.</span></span> |
| <span data-ttu-id="59a20-155">節點</span><span class="sxs-lookup"><span data-stu-id="59a20-155">Node</span></span> | <span data-ttu-id="59a20-156">停用 (暫停)</span><span class="sxs-lookup"><span data-stu-id="59a20-156">Deactivate (pause)</span></span> | <span data-ttu-id="59a20-157">在其目前的狀態中暫停節點。</span><span class="sxs-lookup"><span data-stu-id="59a20-157">Pause the node in its current state.</span></span> <span data-ttu-id="59a20-158">服務會繼續執行，但 Service Fabric 不會主動在節點上移入或移出任何項目，除非有需要這樣做來避免服務中斷或資料不一致的問題。</span><span class="sxs-lookup"><span data-stu-id="59a20-158">Services continue to run but Service Fabric does not proactively move anything onto or off it unless it is required to prevent an outage or data inconsistency.</span></span> <span data-ttu-id="59a20-159">這個動作通常用來在特定節點上啟用偵錯服務，以確保它們不會在檢查期間移動。</span><span class="sxs-lookup"><span data-stu-id="59a20-159">This action is typically used to enable debugging services on a specific node to ensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="59a20-160">節點</span><span class="sxs-lookup"><span data-stu-id="59a20-160">Node</span></span> | <span data-ttu-id="59a20-161">停用 (重新啟動)</span><span class="sxs-lookup"><span data-stu-id="59a20-161">Deactivate (restart)</span></span> | <span data-ttu-id="59a20-162">安全地移除所有記憶體內部服務，並關閉持續性服務。</span><span class="sxs-lookup"><span data-stu-id="59a20-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="59a20-163">通常會在主機處理或電腦必須重新啟動時使用。</span><span class="sxs-lookup"><span data-stu-id="59a20-163">Typically used when the host processes or machine need to be restarted.</span></span> | |
| <span data-ttu-id="59a20-164">節點</span><span class="sxs-lookup"><span data-stu-id="59a20-164">Node</span></span> | <span data-ttu-id="59a20-165">停用 (移除資料)</span><span class="sxs-lookup"><span data-stu-id="59a20-165">Deactivate (remove data)</span></span> | <span data-ttu-id="59a20-166">在建置足夠的備援複本之後，安全地關閉節點上執行的所有服務。</span><span class="sxs-lookup"><span data-stu-id="59a20-166">Safely close all services running on the node after building sufficient spare replicas.</span></span> <span data-ttu-id="59a20-167">通常於節點 (或至少其儲存體) 永久性地移除委任時使用。</span><span class="sxs-lookup"><span data-stu-id="59a20-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="59a20-168">節點</span><span class="sxs-lookup"><span data-stu-id="59a20-168">Node</span></span> | <span data-ttu-id="59a20-169">移除節點狀態</span><span class="sxs-lookup"><span data-stu-id="59a20-169">Remove node state</span></span> | <span data-ttu-id="59a20-170">從叢集移除節點複本的知識。</span><span class="sxs-lookup"><span data-stu-id="59a20-170">Remove knowledge of a node's replicas from the cluster.</span></span> <span data-ttu-id="59a20-171">通常在已失敗的節點被視為無法回復時使用。</span><span class="sxs-lookup"><span data-stu-id="59a20-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="59a20-172">節點</span><span class="sxs-lookup"><span data-stu-id="59a20-172">Node</span></span> | <span data-ttu-id="59a20-173">重新啟動</span><span class="sxs-lookup"><span data-stu-id="59a20-173">Restart</span></span> | <span data-ttu-id="59a20-174">藉由重新啟動節點，模擬節點失敗。</span><span class="sxs-lookup"><span data-stu-id="59a20-174">Simulate a node failure by restarting the node.</span></span> <span data-ttu-id="59a20-175">如需詳細資訊，請參閱[這裡](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)。</span><span class="sxs-lookup"><span data-stu-id="59a20-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="59a20-176">由於許多動作都具有破壞性，因此在完成動作之前，系統可能會要求您確認您的意圖。</span><span class="sxs-lookup"><span data-stu-id="59a20-176">Since many actions are destructive, you may be asked to confirm your intent before the action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="59a20-177">可以透過 Service Fabric 總管執行的每個動作也都可以透過 PowerShell 或 REST API 執行，以實現自動化。</span><span class="sxs-lookup"><span data-stu-id="59a20-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, to enable automation.</span></span>
>
>

<span data-ttu-id="59a20-178">您也可以使用 Service Fabric Explorer，為指定的應用程式類型和版本建立應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="59a20-178">You can also use Service Fabric Explorer to create application instances for a given application type and version.</span></span> <span data-ttu-id="59a20-179">在樹狀檢視中選擇應用程式類型，然後在右邊窗格中按一下您想要的版本旁邊的 [建立應用程式執行個體]  連結。</span><span class="sxs-lookup"><span data-stu-id="59a20-179">Choose the application type in the tree view, then click the **Create app instance** link next to the version you'd like in the right pane.</span></span>

![在 Service Fabric Explorer 中建立應用程式執行個體][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="59a20-181">透過 Service Fabric Explorer 建立的應用程式執行個體目前無法參數化。</span><span class="sxs-lookup"><span data-stu-id="59a20-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="59a20-182">會使用預設參數值來建立它們。</span><span class="sxs-lookup"><span data-stu-id="59a20-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-to-a-remote-service-fabric-cluster"></a><span data-ttu-id="59a20-183">連線至遠端 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="59a20-183">Connect to a remote Service Fabric cluster</span></span>
<span data-ttu-id="59a20-184">如果您知道叢集的端點並有足夠的權限，您就可以從任何瀏覽器存取 Service Fabric Explorer。</span><span class="sxs-lookup"><span data-stu-id="59a20-184">If you know the cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="59a20-185">這是因為 Service Fabric Explorer 只是另一個在叢集中執行的服務。</span><span class="sxs-lookup"><span data-stu-id="59a20-185">This is because Service Fabric Explorer is just another service that runs in the cluster.</span></span>

### <a name="discover-the-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="59a20-186">探索遠端叢集的 Service Fabric 總管端點</span><span class="sxs-lookup"><span data-stu-id="59a20-186">Discover the Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="59a20-187">若要連線到所指定叢集的 Service Fabric Explorer，請將您的瀏覽器指向：</span><span class="sxs-lookup"><span data-stu-id="59a20-187">To reach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="59a20-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="59a20-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="59a20-189">在 Azure 入口網站的叢集基本資訊窗格中，也有提供 Azure 叢集的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="59a20-189">For Azure clusters, the full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="59a20-190">連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="59a20-190">Connect to a secure cluster</span></span>
<span data-ttu-id="59a20-191">您可以為使用憑證或使用 Azure Active Directory (AAD) 來控制用戶端對您 Service Fabric 叢集的存取。</span><span class="sxs-lookup"><span data-stu-id="59a20-191">You can control client access to your Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="59a20-192">如果您嘗試連線到安全叢集上的 Service Fabric Explorer，則視叢集的組態而定，您將必須出示用戶端憑證或使用 AAD 來登入。</span><span class="sxs-lookup"><span data-stu-id="59a20-192">If you attempt to connect to Service Fabric Explorer on a secure cluster, then depending on the cluster's configuration you'll be required to present a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59a20-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59a20-193">Next steps</span></span>
* [<span data-ttu-id="59a20-194">Testability 概觀</span><span class="sxs-lookup"><span data-stu-id="59a20-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="59a20-195">在 Visual Studio 中管理 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="59a20-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="59a20-196">使用 PowerShell 部署 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="59a20-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
