---
title: "aaaDebug Visual Studio 中的應用程式 |Microsoft 文件"
description: "開發和偵錯在 Visual Studio 在本機開發叢集改進 hello 可靠性和效能，您的服務。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="a1983-103">使用 Visual Studio 偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="a1983-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1983-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="a1983-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="a1983-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="a1983-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="a1983-106">偵錯本機 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="a1983-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="a1983-107">您可以在本機電腦開發叢集中開發和偵錯 Azure Service Fabric 應用程式來節省時間和金錢。</span><span class="sxs-lookup"><span data-stu-id="a1983-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="a1983-108">Visual Studio 2017 或 Visual Studio 2015 可以部署 hello 應用程式 toohello 本機叢集，並自動連接 hello 偵錯工具 tooall 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="a1983-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="a1983-109">中的 hello 步驟來啟動本機開發叢集[設定 Service Fabric 開發環境](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a1983-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="a1983-110">按 **F5** 或按一下 [偵錯]  >  [開始偵錯]。</span><span class="sxs-lookup"><span data-stu-id="a1983-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![開始偵錯應用程式][startdebugging]
3. <span data-ttu-id="a1983-112">您的程式碼和逐步執行 hello 應用程式中設定中斷點，即可在 hello 命令**偵錯**功能表。</span><span class="sxs-lookup"><span data-stu-id="a1983-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1983-113">Visual Studio 會將附加 tooall 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="a1983-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="a1983-114">當您逐步執行程式碼時，系統可能會透過多個程序叫用中斷點而導致並行工作階段。</span><span class="sxs-lookup"><span data-stu-id="a1983-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="a1983-115">請嘗試停用 hello 中斷點之後就叫用，讓每個中斷點條件上 hello 執行緒 ID 或使用診斷事件。</span><span class="sxs-lookup"><span data-stu-id="a1983-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="a1983-116">hello**診斷事件**視窗會自動開啟，讓您即時檢視診斷事件。</span><span class="sxs-lookup"><span data-stu-id="a1983-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![即時檢視診斷事件][diagnosticevents]
5. <span data-ttu-id="a1983-118">您也可以開啟 hello**診斷事件**在 Cloud Explorer 中的視窗。</span><span class="sxs-lookup"><span data-stu-id="a1983-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="a1983-119">在 [Service Fabric] 之下，以滑鼠右鍵按一下任何節點，然後選擇 [檢視串流追蹤]。</span><span class="sxs-lookup"><span data-stu-id="a1983-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![開啟 hello 診斷事件視窗][viewdiagnosticevents]
   
    <span data-ttu-id="a1983-121">如果您想 toofilter 追蹤 tooa 特定服務或應用程式，只要啟用該特定服務或應用程式上的資料流追蹤。</span><span class="sxs-lookup"><span data-stu-id="a1983-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="a1983-122">自動產生的 hello 中可以看到 hello 診斷事件**ServiceEventSource.cs**檔案，並從應用程式程式碼呼叫。</span><span class="sxs-lookup"><span data-stu-id="a1983-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="a1983-123">hello**診斷事件**視窗支援篩選、 暫停與檢查即時事件。</span><span class="sxs-lookup"><span data-stu-id="a1983-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="a1983-124">hello 篩選器是簡單的字串搜尋 hello 事件訊息，包括其內容。</span><span class="sxs-lookup"><span data-stu-id="a1983-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![篩選、暫停和繼續，或即時檢查事件][diagnosticeventsactions]
8. <span data-ttu-id="a1983-126">偵錯服務如同偵錯任何其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1983-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="a1983-127">您通常可以透過 Visual Studio 設定中斷點，以便進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="a1983-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="a1983-128">即使可靠集合會在多個節點上複寫，它們仍會實作 IEnumerable。</span><span class="sxs-lookup"><span data-stu-id="a1983-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="a1983-129">這表示您可以使用 hello 結果檢視 Visual Studio 中偵錯 toosee 時已儲存在內部。</span><span class="sxs-lookup"><span data-stu-id="a1983-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="a1983-130">您可以在程式碼中的任何位置輕鬆設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="a1983-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![開始偵錯應用程式][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="a1983-132">偵錯遠端 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="a1983-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="a1983-133">如果您的 Service Fabric 應用程式在 Azure 中的 Service Fabric 叢集上執行，也可以 tooremotely 偵錯這些項目，直接從 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a1983-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="a1983-134">hello 功能需要[Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015)和[Azure SDK for.NET 2.9](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="a1983-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="a1983-135">遠端偵錯適用於開發/測試案例和 toobe 用在實際執行環境，因為 hello hello 執行應用程式的影響。</span><span class="sxs-lookup"><span data-stu-id="a1983-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="a1983-136">瀏覽 tooyour 叢集中**Cloud Explorer**，以滑鼠右鍵按一下，然後選擇 **啟用偵錯**</span><span class="sxs-lookup"><span data-stu-id="a1983-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![啟用遠端偵錯][enableremotedebugging]
   
    <span data-ttu-id="a1983-138">這會啟動啟用遠端偵錯您的叢集節點上的擴充功能的 hello 的 hello 程序，以及所需的網路組態。</span><span class="sxs-lookup"><span data-stu-id="a1983-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="a1983-139">中的以滑鼠右鍵按一下 hello 叢集節點**Cloud Explorer**，然後選擇 **附加偵錯工具**</span><span class="sxs-lookup"><span data-stu-id="a1983-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![連結偵錯工具][attachdebugger]
3. <span data-ttu-id="a1983-141">在 [hello**附加 tooprocess** ] 對話方塊中，選擇 toodebug，然後按一下 「 hello 」 處理序**附加**</span><span class="sxs-lookup"><span data-stu-id="a1983-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![選擇程序][chooseprocess]
   
    <span data-ttu-id="a1983-143">hello 名稱 hello 程序中，您想以 tooattach，等於 hello 程式的服務專案的組件名稱。</span><span class="sxs-lookup"><span data-stu-id="a1983-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="a1983-144">hello 偵錯工具會附加 tooall 節點執行 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="a1983-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="a1983-145">在您將正在偵錯的無狀態服務的 hello 情況下，hello 服務的所有節點上的所有執行個體是 hello 偵錯工作階段的一部分。</span><span class="sxs-lookup"><span data-stu-id="a1983-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="a1983-146">如果您正在偵錯的可設定狀態的服務，只有 hello 主要複本的任何資料分割將作用中和 hello 偵錯工具，因此已攔截。</span><span class="sxs-lookup"><span data-stu-id="a1983-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="a1983-147">如果 hello 主要複本移 hello 偵錯工作階段期間，該複本的 hello 處理仍會 hello 偵錯工作階段的一部分。</span><span class="sxs-lookup"><span data-stu-id="a1983-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="a1983-148">在訂單 tooonly catch 相關的資料分割或特定服務的執行個體中，您可以使用條件式中斷點 tooonly 中斷特定分割區或執行個體。</span><span class="sxs-lookup"><span data-stu-id="a1983-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![條件式中斷點][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="a1983-150">目前我們不支援偵錯多個執行個體的 hello Service Fabric 叢集相同的服務可執行檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="a1983-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="a1983-151">一旦您完成偵錯您的應用程式，您可以停用 hello 遠端偵錯延伸模組中的 hello 叢集上按一下滑鼠右鍵**Cloud Explorer**選擇**停用偵錯**</span><span class="sxs-lookup"><span data-stu-id="a1983-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![停用遠端偵錯][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="a1983-153">從遠端叢集節點串流追蹤</span><span class="sxs-lookup"><span data-stu-id="a1983-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="a1983-154">您也會直接從遠端叢集節點 tooVisual Studio 能夠 toostream 追蹤。</span><span class="sxs-lookup"><span data-stu-id="a1983-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="a1983-155">這項功能可讓您 toostream ETW 追蹤事件，產生的 Service Fabric 叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="a1983-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="a1983-156">此功能需要 [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 和 [Azure SDK for.NET 2.9](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="a1983-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="a1983-157">這項功能僅支援在 Azure 中執行的叢集。</span><span class="sxs-lookup"><span data-stu-id="a1983-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="a1983-158">資料流追蹤適用於開發/測試案例和 toobe 用在實際執行環境，因為 hello hello 執行應用程式的影響。</span><span class="sxs-lookup"><span data-stu-id="a1983-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="a1983-159">在生產案例中，您應依賴使用 Azure 診斷轉送事件。</span><span class="sxs-lookup"><span data-stu-id="a1983-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="a1983-160">瀏覽 tooyour 叢集中**Cloud Explorer**，以滑鼠右鍵按一下，然後選擇 **啟用資料流追蹤**</span><span class="sxs-lookup"><span data-stu-id="a1983-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![啟用遠端串流追蹤][enablestreamingtraces]
   
    <span data-ttu-id="a1983-162">這會啟動啟用 hello 串流處理您的叢集節點上的追蹤延伸模組的 hello 程序，以及所需的網路組態。</span><span class="sxs-lookup"><span data-stu-id="a1983-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="a1983-163">展開 hello**節點**中的項目**Cloud Explorer**，以滑鼠右鍵按一下您想要從 toostream 追蹤，並選擇 hello 節點**檢視資料流追蹤**</span><span class="sxs-lookup"><span data-stu-id="a1983-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![檢視遠端串流追蹤][viewremotestreamingtraces]
   
    <span data-ttu-id="a1983-165">您想要從 toosee 追蹤的許多節點重複步驟 2。</span><span class="sxs-lookup"><span data-stu-id="a1983-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="a1983-166">每個節點串流會顯示在專用視窗中。</span><span class="sxs-lookup"><span data-stu-id="a1983-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="a1983-167">現在您已經準備 Service Fabric 和您的服務所發出的能 toosee hello 追蹤。</span><span class="sxs-lookup"><span data-stu-id="a1983-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="a1983-168">如果您想 toofilter hello 事件 tooonly 顯示特定應用程式，只要輸入 hello hello 篩選中的 hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="a1983-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![檢視串流追蹤][viewingstreamingtraces]
3. <span data-ttu-id="a1983-170">在您完成從叢集中的資料流處理的追蹤，您可以停用遠端資料流處理的追蹤，以滑鼠右鍵按一下中的 hello 叢集**Cloud Explorer**選擇**停用資料流追蹤**</span><span class="sxs-lookup"><span data-stu-id="a1983-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![停用遠端串流追蹤][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="a1983-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1983-172">Next steps</span></span>
* <span data-ttu-id="a1983-173">[測試 Service Fabric 服務](service-fabric-testability-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a1983-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="a1983-174">[在 Visual Studio 中管理 Service Fabric 應用程式](service-fabric-manage-application-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="a1983-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
