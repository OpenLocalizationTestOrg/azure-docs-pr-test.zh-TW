---
title: "使用 C# 建立 Azure Service Fabric 可靠服務"
description: "使用 Visual Studio，建立、部署和偵錯以 Azure Service Fabric 為建置基礎的 Reliable Service 應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: f93298e6483fd8c9dfda835964aeebd1a430af69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="b2c3b-103">建立第一個 C# Service Fabric 具狀態 Reliable Services 應用程式</span><span class="sxs-lookup"><span data-stu-id="b2c3b-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="b2c3b-104">了解如何在短短幾分鐘內在 Windows 上部署適用於 .NET 的第一個 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-104">Learn how to deploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="b2c3b-105">當您完成時，將會有以可靠服務應用程式執行的本機叢集。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2c3b-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="b2c3b-106">Prerequisites</span></span>

<span data-ttu-id="b2c3b-107">開始之前，請確定您已 [設定開發環境](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="b2c3b-108">這包括安裝 Service Fabric SDK 及 Visual Studio 2017 或 2015。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-108">This includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="b2c3b-109">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="b2c3b-109">Create the application</span></span>

<span data-ttu-id="b2c3b-110">以**系統管理員**身分啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="b2c3b-111">使用 `CTRL`+`SHIFT`+`N` 建立專案</span><span class="sxs-lookup"><span data-stu-id="b2c3b-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="b2c3b-112">在 [新增專案]  對話方塊中，選擇 [雲端] > [Service Fabric 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-112">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="b2c3b-113">將應用程式命名為 **MyApplication**，然後按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-113">Name the application **MyApplication** and press **OK**.</span></span>

   
![Visual Studio 中的新增專案對話方塊][1]

<span data-ttu-id="b2c3b-115">您可以從下一個對話方塊建立任何類型的 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-115">You can create any type of Service Fabric application from the next dialog.</span></span> <span data-ttu-id="b2c3b-116">在本快速入門中，選擇 [具狀態服務]。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="b2c3b-117">將服務命名為 **MyStatefulService**，然後按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-117">Name the service **MyStatefulService** and press **OK**.</span></span>

![Visual Studio 中的新增服務對話方塊][2]


<span data-ttu-id="b2c3b-119">Visual Studio 會建立應用程式專案和具狀態服務專案，並在 [方案總管] 中加以顯示。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-119">Visual Studio creates the application project and the stateful service project and displays them in Solution Explorer.</span></span>

![使用具狀態服務建立應用程式後的方案總管][3]

<span data-ttu-id="b2c3b-121">應用程式專案 (**MyApplication**) 未直接包含任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-121">The application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="b2c3b-122">它反而會參考一組服務專案。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="b2c3b-123">此外，它包含三種其他類型的內容：</span><span class="sxs-lookup"><span data-stu-id="b2c3b-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="b2c3b-124">**發佈設定檔**</span><span class="sxs-lookup"><span data-stu-id="b2c3b-124">**Publish profiles**</span></span>  
<span data-ttu-id="b2c3b-125">可供部署至不同環境的設定檔。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-125">Profiles for deploying to different environments.</span></span>

* <span data-ttu-id="b2c3b-126">**指令碼**</span><span class="sxs-lookup"><span data-stu-id="b2c3b-126">**Scripts**</span></span>  
<span data-ttu-id="b2c3b-127">包含用來部署/升級應用程式的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="b2c3b-128">**應用程式定義**</span><span class="sxs-lookup"><span data-stu-id="b2c3b-128">**Application definition**</span></span>  
<span data-ttu-id="b2c3b-129">包含 ApplicationPackageRoot 之下的 ApplicationManifest.xml 檔案，其描述您的應用程式組合。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-129">Includes the ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="b2c3b-130">相關聯的應用程式參數檔案位於 ApplicationParameters 之下，其可用來指定指定環境特有參數。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-130">Associated application parameter files are under *ApplicationParameters*, which can be used to specify environment-specific parameters.</span></span> <span data-ttu-id="b2c3b-131">Visual Studio 會在部署至特定環境的期間，選取相關聯的發行設定檔中指定的應用程式參數檔案。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-131">Visual Studio selects an application parameter file that's specified in the associated publish profile during deployment to a specific environment.</span></span>
    
<span data-ttu-id="b2c3b-132">如需服務專案的內容概觀，請參閱 [開始使用 Reliable Services](service-fabric-reliable-services-quick-start.md)。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-132">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-the-application"></a><span data-ttu-id="b2c3b-133">部署和偵錯應用程式</span><span class="sxs-lookup"><span data-stu-id="b2c3b-133">Deploy and debug the application</span></span>

<span data-ttu-id="b2c3b-134">請執行您現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="b2c3b-135">在 Visual Studio 中，按 `F5` 部署應用程式以供偵錯。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-135">In Visual Studio, press `F5` to deploy the application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="b2c3b-136">您第一次在本機執行及部署應用程式時，Visual Studio 會建立本機叢集以供偵錯。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-136">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="b2c3b-137">這可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-137">This may take some time.</span></span> <span data-ttu-id="b2c3b-138">叢集建立狀態會顯示在 Visual Studio 輸出視窗中。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-138">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="b2c3b-139">備妥叢集時，您會收到來自 SDK 隨附的本機叢集系統匣管理員應用程式的通知。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-139">When the cluster is ready, you get a notification from the local cluster system tray manager application included with the SDK.</span></span>
   
![本機叢集系統匣通知][4]

<span data-ttu-id="b2c3b-141">啟動應用程式後，Visual Studio 會自動顯示 [診斷事件檢視器]，以便查看服務的追蹤輸出。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-141">Once the application starts, Visual Studio automatically brings up the **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![診斷事件檢視器][5]

<span data-ttu-id="b2c3b-143">我們使用的具狀態服務範本只會顯示在 **MyStatefulService.cs** 的 `RunAsync` 方法中遞增的計數器值。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-143">The stateful service template we used simply shows a counter value incrementing in the `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="b2c3b-144">展開其中一個事件以查看更多詳細資料，包括程式碼執行所在的節點。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-144">Expand one of the events to see more details, including the node where the code is running.</span></span> <span data-ttu-id="b2c3b-145">在此情況下是 \_Node\_2，但在您的電腦上可能會是其他節點。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![診斷事件檢視器詳細資訊][6]

<span data-ttu-id="b2c3b-147">本機叢集包含五個裝載於單一電腦上的節點。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-147">The local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="b2c3b-148">在生產環境中，每個節點會裝載於不同的實體或虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="b2c3b-149">讓我們取下本機叢集上的其中一個節點來模擬遺失機器，以及在相同的時間運用 Visual Studio 偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-149">To simulate the loss of a machine while exercising the Visual Studio debugger at the same time, let's take down one of the nodes on the local cluster.</span></span>

<span data-ttu-id="b2c3b-150">在 [方案總管] 視窗中，開啟 **MyStatefulService.cs**。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-150">In the **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="b2c3b-151">尋找 `RunAsync` 方法，並在方法的第一行上設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-151">Find the `RunAsync` method and set a breakpoint on the first line of the method.</span></span>

![具狀態服務 RunAsync 方法的中斷點][7]

<span data-ttu-id="b2c3b-153">以滑鼠右鍵按一下 [本機叢集管理員] 系統匣應用程式並選擇 [管理本機叢集]，以啟動 [Service Fabric Explorer] 工具。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-153">Launch the **Service Fabric Explorer** tool by right-clicking on the **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![從本機叢集管理員啟動 Service Fabric Explorer][systray-launch-sfx]

<span data-ttu-id="b2c3b-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) 會提供叢集的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="b2c3b-156">其中包括部署至叢集的應用程式集以及構成叢集的實體節點集合。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-156">It includes the set of applications deployed to it and the set of physical nodes that make it up.</span></span>

<span data-ttu-id="b2c3b-157">在左窗格中展開 [叢集] > [節點]，並尋找您的程式碼執行所在的節點。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-157">In the left pane, expand **Cluster > Nodes** and find the node where your code is running.</span></span>

<span data-ttu-id="b2c3b-158">按一下 [動作] > [停用 (重新啟動)] 來模擬電腦重新啟動。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-158">Click **Actions > Deactivate (Restart)** to simulate a machine restarting.</span></span>

![在 Service Fabric Explorer 中停止節點][sfx-stop-node]

<span data-ttu-id="b2c3b-160">您應該會在 Visual Studio 中短暫看見達到您的中斷點，因為您一個節點上所做的計算完美地容錯移轉至另一個節點。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-160">Momentarily, you should see your breakpoint hit in Visual Studio as the computation you were doing on one node seamlessly fails over to another.</span></span>


<span data-ttu-id="b2c3b-161">接下來，返回 [診斷事件檢視器] 並觀察訊息。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-161">Next, return to the Diagnostic Events Viewer and observe the messages.</span></span> <span data-ttu-id="b2c3b-162">計數器已繼續遞增，即使事件實際上來自不同的節點。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-162">The counter has continued incrementing, even though the events are actually coming from a different node.</span></span>

![容錯移轉之後的診斷事件檢視器][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-the-local-cluster-optional"></a><span data-ttu-id="b2c3b-164">清除本機叢集 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="b2c3b-164">Cleaning up the local cluster (optional)</span></span>

<span data-ttu-id="b2c3b-165">請記住，此本機叢集是真實的叢集。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="b2c3b-166">停止偵錯工具將會移除應用程式執行個體，並取消註冊應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-166">Stopping the debugger removes your application instance and unregisters the application type.</span></span> <span data-ttu-id="b2c3b-167">不過，叢集會繼續在背景中執行。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-167">However, the cluster continues to run in the background.</span></span> <span data-ttu-id="b2c3b-168">當您準備要停止本機叢集時，有幾個選項可用。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-168">When you're ready to stop the local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="b2c3b-169">保留應用程式和追蹤資料</span><span class="sxs-lookup"><span data-stu-id="b2c3b-169">Keep application and trace data</span></span>

<span data-ttu-id="b2c3b-170">以滑鼠右鍵按一下 [本機叢集管理員] 系統匣應用程式，然後選擇 [停止本機叢集]，以關閉叢集。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-170">Shut down the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-the-cluster-and-all-data"></a><span data-ttu-id="b2c3b-171">刪除叢集和所有資料</span><span class="sxs-lookup"><span data-stu-id="b2c3b-171">Delete the cluster and all data</span></span>

<span data-ttu-id="b2c3b-172">以滑鼠右鍵按一下 [本機叢集管理員] 系統匣應用程式，然後選擇 [移除本機叢集]，以移除叢集。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-172">Remove the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="b2c3b-173">如果您選擇此選項，Visual Studio 會在您下一次執行應用程式時重新部署叢集。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-173">If you choose this option, Visual Studio will redeploy the cluster the next time your run the application.</span></span> <span data-ttu-id="b2c3b-174">如果您打算停用本機叢集一陣子或需要回收資源，請選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-174">Choose this option if you don't intend to use the local cluster for some time or if you need to reclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2c3b-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2c3b-175">Next steps</span></span>
<span data-ttu-id="b2c3b-176">深入了解 [Reliable Services](service-fabric-reliable-services-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b2c3b-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
