---
title: "aaaCreate Azure Service Fabric 可靠的服務使用 C#"
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
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="bbdfc-103">建立第一個 C# Service Fabric 具狀態 Reliable Services 應用程式</span><span class="sxs-lookup"><span data-stu-id="bbdfc-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="bbdfc-104">深入了解如何 toodeploy 第一個 Service Fabric 應用程式在 Windows 上的.net 在短短幾分鐘內。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="bbdfc-105">當您完成時，將會有以可靠服務應用程式執行的本機叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbdfc-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="bbdfc-106">Prerequisites</span></span>

<span data-ttu-id="bbdfc-107">開始之前，請確定您已 [設定開發環境](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="bbdfc-108">這包括安裝 hello Service Fabric SDK 及 Visual Studio 2017 或 2015年。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="bbdfc-109">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bbdfc-109">Create hello application</span></span>

<span data-ttu-id="bbdfc-110">以**系統管理員**身分啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="bbdfc-111">使用 `CTRL`+`SHIFT`+`N` 建立專案</span><span class="sxs-lookup"><span data-stu-id="bbdfc-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="bbdfc-112">在 [hello**新專案**] 對話方塊中，選擇**雲端 > Service Fabric 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="bbdfc-113">Hello 應用程式命名**MyApplication**按**確定**。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Visual Studio 中的新增專案對話方塊][1]

<span data-ttu-id="bbdfc-115">您可以從 hello 下一步 對話方塊建立 Service Fabric 應用程式的任何型別。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="bbdfc-116">在本快速入門中，選擇 [具狀態服務]。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="bbdfc-117">Hello 服務名稱**MyStatefulService**按**確定**。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Visual Studio 中的新增服務對話方塊][2]


<span data-ttu-id="bbdfc-119">Visual Studio 會建立 hello 應用程式專案和 hello 可設定狀態的服務專案，並顯示在 [方案總管] 中。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![使用具狀態服務建立應用程式後的方案總管][3]

<span data-ttu-id="bbdfc-121">hello 應用程式專案 (**MyApplication**) 直接不包含任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="bbdfc-122">它反而會參考一組服務專案。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="bbdfc-123">此外，它包含三種其他類型的內容：</span><span class="sxs-lookup"><span data-stu-id="bbdfc-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="bbdfc-124">**發佈設定檔**</span><span class="sxs-lookup"><span data-stu-id="bbdfc-124">**Publish profiles**</span></span>  
<span data-ttu-id="bbdfc-125">部署 toodifferent 環境的設定檔。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="bbdfc-126">**指令碼**</span><span class="sxs-lookup"><span data-stu-id="bbdfc-126">**Scripts**</span></span>  
<span data-ttu-id="bbdfc-127">包含用來部署/升級應用程式的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="bbdfc-128">**應用程式定義**</span><span class="sxs-lookup"><span data-stu-id="bbdfc-128">**Application definition**</span></span>  
<span data-ttu-id="bbdfc-129">包含下的 hello ApplicationManifest.xml 檔案*ApplicationPackageRoot*用來描述應用程式的組合。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="bbdfc-130">相關聯的應用程式參數檔案受到*ApplicationParameters*，它可以是使用的 toospecify 環境特有的參數。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="bbdfc-131">Hello 中指定的應用程式參數檔案相關聯的 visual Studio 選取 tooa 特定環境時，部署期間發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="bbdfc-132">如需 hello hello 服務專案內容的概觀，請參閱[可靠的服務入門](service-fabric-reliable-services-quick-start.md)。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="bbdfc-133">部署和偵錯 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bbdfc-133">Deploy and debug hello application</span></span>

<span data-ttu-id="bbdfc-134">請執行您現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="bbdfc-135">在 Visual Studio 中，按`F5`toodeploy hello 應用程式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="bbdfc-136">hello 第一次執行，並部署 hello 應用程式在本機，Visual Studio 會建立偵錯的本機叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="bbdfc-137">這可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-137">This may take some time.</span></span> <span data-ttu-id="bbdfc-138">hello Visual Studio 輸出 視窗中會顯示 hello 叢集建立狀態。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="bbdfc-139">Hello 叢集就緒時，您會收到通知，從 hello 本機叢集系統匣管理員應用程式隨附 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![本機叢集系統匣通知][4]

<span data-ttu-id="bbdfc-141">一次 hello 應用程式啟動時，Visual Studio 會自動顯示 hello**診斷事件檢視器**，您可以在其中看到與您的服務追蹤輸出。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![診斷事件檢視器][5]

<span data-ttu-id="bbdfc-143">hello 我們使用的可設定狀態的服務範本只會顯示計數器值遞增中 hello`RunAsync`方法**MyStatefulService.cs**。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="bbdfc-144">展開其中一個 hello 事件 toosee 更多詳細資料，包括 hello hello 程式碼執行所在的節點。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="bbdfc-145">在此情況下是 \_Node\_2，但在您的電腦上可能會是其他節點。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![診斷事件檢視器詳細資訊][6]

<span data-ttu-id="bbdfc-147">hello 本機叢集包含五個節點裝載在同一部電腦。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="bbdfc-148">在生產環境中，每個節點會裝載於不同的實體或虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="bbdfc-149">toosimulate hello 遺失機器時執行 hello Visual Studio 的偵錯工具在 hello 相同時間，讓我們來看下一個 hello hello 本機叢集上的節點。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="bbdfc-150">在 [hello**方案總管] 中**視窗中，開啟**MyStatefulService.cs**。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="bbdfc-151">尋找 hello`RunAsync`方法並將 hello hello 方法第一行上的中斷點。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![具狀態服務 RunAsync 方法的中斷點][7]

<span data-ttu-id="bbdfc-153">啟動 hello **Service Fabric 總管**工具，以滑鼠右鍵按一下 hello**本機叢集管理員**系統匣應用程式，然後選擇 **管理本機叢集**。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![從 hello 本機叢集管理員啟動 Service Fabric 總管][systray-launch-sfx]

<span data-ttu-id="bbdfc-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) 會提供叢集的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="bbdfc-156">它包含部署的應用程式 tooit hello 組和它構成實體節點的 hello 組。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="bbdfc-157">Hello 左窗格中，展開 **叢集 > 節點**和尋找 hello 節點正在您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="bbdfc-158">按一下**動作 > 停用 （重新啟動）** toosimulate 機器重新啟動。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![在 Service Fabric Explorer 中停止節點][sfx-stop-node]

<span data-ttu-id="bbdfc-160">您應該會立即看到中斷點為 hello 計算您順暢地執行其中一個節點容錯移轉 tooanother Visual Studio 中叫用。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="bbdfc-161">接下來，傳回 toohello 診斷事件檢視器，並觀察 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="bbdfc-162">hello 計數器一直在遞增，即使 hello 事件實際上來自不同的節點。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![容錯移轉之後的診斷事件檢視器][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="bbdfc-164">清除 hello 本機叢集 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="bbdfc-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="bbdfc-165">請記住，此本機叢集是真實的叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="bbdfc-166">停止 hello 偵錯工具會移除您的應用程式執行個體，並取消註冊 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="bbdfc-167">不過，hello 叢集會繼續 toorun hello 背景執行。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="bbdfc-168">當您準備好 toostop hello 本機叢集時，有幾個選項。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="bbdfc-169">保留應用程式和追蹤資料</span><span class="sxs-lookup"><span data-stu-id="bbdfc-169">Keep application and trace data</span></span>

<span data-ttu-id="bbdfc-170">關閉 hello 叢集，以滑鼠右鍵按一下 hello**本機叢集管理員**系統匣應用程式，然後選擇 **停止本機叢集**。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="bbdfc-171">資料刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="bbdfc-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="bbdfc-172">以滑鼠右鍵按一下 hello 移除 hello 叢集**本機叢集管理員**系統匣應用程式，然後選擇 **移除本機叢集**。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="bbdfc-173">如果您選擇此選項時，Visual Studio 重新部署 hello 叢集 hello 下次您執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="bbdfc-174">如果您不想 toouse hello 本機叢集段時間，或如果您需要 tooreclaim 資源，請選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbdfc-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bbdfc-175">Next steps</span></span>
<span data-ttu-id="bbdfc-176">深入了解 [Reliable Services](service-fabric-reliable-services-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="bbdfc-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
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
