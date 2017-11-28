---
title: "在 Visual Studio 中進行應用程式偵錯 | Microsoft Docs"
description: "利用本機開發叢集上的 Visual Studio 來開發服務及為服務偵錯，以便改善您服務的可靠性和效能。"
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
ms.openlocfilehash: 2459025899a7f5ffebf44fa104ed112c0eb99dfa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="41d92-103">使用 Visual Studio 偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="41d92-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41d92-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="41d92-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="41d92-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="41d92-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="41d92-106">偵錯本機 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="41d92-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="41d92-107">您可以在本機電腦開發叢集中開發和偵錯 Azure Service Fabric 應用程式來節省時間和金錢。</span><span class="sxs-lookup"><span data-stu-id="41d92-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="41d92-108">Visual Studio 2017 或 Visual Studio 2015 可以將應用程式部署至本機叢集，並自動將偵錯工具連線至您應用程式的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="41d92-108">Visual Studio 2017 or Visual Studio 2015 can deploy the application to the local cluster and automatically connect the debugger to all instances of your application.</span></span>

1. <span data-ttu-id="41d92-109">遵循 [設定 Service Fabric 開發環境](service-fabric-get-started.md)中的步驟來啟動本機開發叢集。</span><span class="sxs-lookup"><span data-stu-id="41d92-109">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="41d92-110">按 **F5** 或按一下 [偵錯]  >  [開始偵錯]。</span><span class="sxs-lookup"><span data-stu-id="41d92-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![開始偵錯應用程式][startdebugging]
3. <span data-ttu-id="41d92-112">透過按一下 [偵錯]  功能表中的命令，在您的程式碼中設定中斷點並逐步執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="41d92-112">Set breakpoints in your code and step through the application by clicking commands in the **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41d92-113">Visual Studio 將附加至您應用程式的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="41d92-113">Visual Studio attaches to all instances of your application.</span></span> <span data-ttu-id="41d92-114">當您逐步執行程式碼時，系統可能會透過多個程序叫用中斷點而導致並行工作階段。</span><span class="sxs-lookup"><span data-stu-id="41d92-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="41d92-115">若要嘗試在叫用中斷點之後停用它們，請在執行緒識別碼上條件化每個中斷點，或使用診斷事件。</span><span class="sxs-lookup"><span data-stu-id="41d92-115">Try disabling the breakpoints after they're hit, by making each breakpoint conditional on the thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="41d92-116">[診斷事件] 視窗會自動開啟，讓您可以即時檢視診斷事件。</span><span class="sxs-lookup"><span data-stu-id="41d92-116">The **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![即時檢視診斷事件][diagnosticevents]
5. <span data-ttu-id="41d92-118">您也可以在 [雲端總管] 開啟 [診斷事件] 視窗。</span><span class="sxs-lookup"><span data-stu-id="41d92-118">You can also open the **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="41d92-119">在 [Service Fabric] 之下，以滑鼠右鍵按一下任何節點，然後選擇 [檢視串流追蹤]。</span><span class="sxs-lookup"><span data-stu-id="41d92-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![開啟診斷事件視窗][viewdiagnosticevents]
   
    <span data-ttu-id="41d92-121">如果您想要將追蹤篩選為特定的服務或應用程式，只要對該特定服務或應用程式啟用資料串流追蹤。</span><span class="sxs-lookup"><span data-stu-id="41d92-121">If you want to filter your traces to a specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="41d92-122">您可以在自動產生的 **ServiceEventSource.cs** 檔案中查看診斷事件，並從應用程式程式碼進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="41d92-122">The diagnostic events can be seen in the automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="41d92-123">[診斷事件] 視窗支援篩選、暫停和即時檢查事件。</span><span class="sxs-lookup"><span data-stu-id="41d92-123">The **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="41d92-124">篩選是事件訊息的簡易字串搜尋，包括其內容。</span><span class="sxs-lookup"><span data-stu-id="41d92-124">The filter is a simple string search of the event message, including its contents.</span></span>
   
    ![篩選、暫停和繼續，或即時檢查事件][diagnosticeventsactions]
8. <span data-ttu-id="41d92-126">偵錯服務如同偵錯任何其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="41d92-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="41d92-127">您通常可以透過 Visual Studio 設定中斷點，以便進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="41d92-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="41d92-128">即使可靠集合會在多個節點上複寫，它們仍會實作 IEnumerable。</span><span class="sxs-lookup"><span data-stu-id="41d92-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="41d92-129">這表示您可以在 Visual Studio 中使用 [結果檢視]，同時進行偵錯以查看已在內部儲存的內容。</span><span class="sxs-lookup"><span data-stu-id="41d92-129">This means that you can use the Results View in Visual Studio while debugging to see what you've stored inside.</span></span> <span data-ttu-id="41d92-130">您可以在程式碼中的任何位置輕鬆設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="41d92-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![開始偵錯應用程式][breakpoint]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="41d92-132">偵錯遠端 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="41d92-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="41d92-133">如果您的 Service Fabric 應用程式是在 Azure 中的 Service Fabric 叢集上執行，則可直接從 Visual Studio 進行其遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="41d92-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able to remotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="41d92-134">此功能需要 [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 和 [Azure SDK for.NET 2.9](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="41d92-134">The feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="41d92-135">遠端偵錯適用於開發/測試案例，而非用於生產環境中，因為會對執行中的應用程式造成影響。</span><span class="sxs-lookup"><span data-stu-id="41d92-135">Remote debugging is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> 
> 

1. <span data-ttu-id="41d92-136">在 [雲端總管] 中瀏覽至您的叢集，以滑鼠右鍵按一下並選擇 [啟用偵錯]</span><span class="sxs-lookup"><span data-stu-id="41d92-136">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![啟用遠端偵錯][enableremotedebugging]
   
    <span data-ttu-id="41d92-138">這麼做會開始在您的叢集節點上啟用遠端偵錯擴充功能的程序，也會啟用所需的網路組態。</span><span class="sxs-lookup"><span data-stu-id="41d92-138">This will kick off the process of enabling the remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="41d92-139">在 [雲端總管] 中的叢集節點上按一下滑鼠右鍵，然後選擇 [附加偵錯工具]</span><span class="sxs-lookup"><span data-stu-id="41d92-139">Right-click the cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![連結偵錯工具][attachdebugger]
3. <span data-ttu-id="41d92-141">在 [附加至程序] 對話方塊中，選擇您要偵錯的處理序，然後按一下 [附加]</span><span class="sxs-lookup"><span data-stu-id="41d92-141">In the **Attach to process** dialog, choose the process you want to debug, and click **Attach**</span></span>
   
    ![選擇程序][chooseprocess]
   
    <span data-ttu-id="41d92-143">您想要附加至的處理序名稱等於您的服務專案組件名稱。</span><span class="sxs-lookup"><span data-stu-id="41d92-143">The name of the process you want to attach to, equals the name of your service project assembly name.</span></span>
   
    <span data-ttu-id="41d92-144">偵錯工具將會複製至執行處理序的所有節點。</span><span class="sxs-lookup"><span data-stu-id="41d92-144">The debugger will attach to all nodes running the process.</span></span>
   
   * <span data-ttu-id="41d92-145">在偵錯無狀態服務的情況下，所有節點上此服務的所有執行個體都是偵錯工作階段的一部分。</span><span class="sxs-lookup"><span data-stu-id="41d92-145">In the case where you are debugging a stateless service, all instances of the service on all nodes are part of the debug session.</span></span>
   * <span data-ttu-id="41d92-146">如果您正在偵錯具狀態服務，任何分割區都只有主要複本會是作用中，因而遭到偵錯工具攔截。</span><span class="sxs-lookup"><span data-stu-id="41d92-146">If you are debugging a stateful service, only the primary replica of any partition will be active and therefore caught by the debugger.</span></span> <span data-ttu-id="41d92-147">如果在偵錯工作階段期間移動主要複本，仍會在偵錯工作階段內處理該複本。</span><span class="sxs-lookup"><span data-stu-id="41d92-147">If the primary replica moves during the debug session, the processing of that replica will still be part of the debug session.</span></span>
   * <span data-ttu-id="41d92-148">若只要攔截特定服務的相關分割區或執行個體，您可以使用條件式中斷點只中斷特定的分割區或執行個體。</span><span class="sxs-lookup"><span data-stu-id="41d92-148">In order to only catch relevant partitions or instances of a given service, you can use conditional breakpoints to only break a specific partition or instance.</span></span>
     
     ![條件式中斷點][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="41d92-150">我們目前不支援對多個執行個體具有相同服務可執行檔名稱的 Service Fabric 叢集進行。</span><span class="sxs-lookup"><span data-stu-id="41d92-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of the same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="41d92-151">一旦完成應用程式的偵錯，在 [雲端總管] 中以滑鼠右鍵按一下叢集，然後選擇 [停用偵錯]，即可停用遠端偵錯延伸模組</span><span class="sxs-lookup"><span data-stu-id="41d92-151">Once you finish debugging your application, you can disable the remote debugging extension by right-clicking the cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![停用遠端偵錯][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="41d92-153">從遠端叢集節點串流追蹤</span><span class="sxs-lookup"><span data-stu-id="41d92-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="41d92-154">您也可以直接從遠端叢集節點將追蹤串流至 Visual studio。</span><span class="sxs-lookup"><span data-stu-id="41d92-154">You are also able to stream traces directly from a remote cluster node to Visual Studio.</span></span> <span data-ttu-id="41d92-155">這項功能可讓您串流在 Service Fabric 叢集節點上產生的 ETW 追蹤事件。</span><span class="sxs-lookup"><span data-stu-id="41d92-155">This feature allows you to stream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="41d92-156">此功能需要 [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) 和 [Azure SDK for.NET 2.9](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="41d92-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="41d92-157">這項功能僅支援在 Azure 中執行的叢集。</span><span class="sxs-lookup"><span data-stu-id="41d92-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="41d92-158">串流追蹤適用於開發/測試案例，而非用於生產環境中，因為會對執行中的應用程式造成影響。</span><span class="sxs-lookup"><span data-stu-id="41d92-158">Streaming traces is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.</span></span>
> <span data-ttu-id="41d92-159">在生產案例中，您應依賴使用 Azure 診斷轉送事件。</span><span class="sxs-lookup"><span data-stu-id="41d92-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="41d92-160">在 [雲端總管] 中瀏覽至您的叢集，以滑鼠右鍵按一下並選擇 [啟用串流追蹤]</span><span class="sxs-lookup"><span data-stu-id="41d92-160">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![啟用遠端串流追蹤][enablestreamingtraces]
   
    <span data-ttu-id="41d92-162">這麼做會開始在您的叢集節點上啟用串流追蹤擴充功能的程序，也會啟用所需的網路組態。</span><span class="sxs-lookup"><span data-stu-id="41d92-162">This will kick off the process of enabling the streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="41d92-163">展開 [雲端總管] 中的 [節點] 元素，以滑鼠右鍵按一下您要串流追蹤的節點，然後選擇 [檢視串流追蹤]</span><span class="sxs-lookup"><span data-stu-id="41d92-163">Expand the **Nodes** element in **Cloud Explorer**, right-click the node you want to stream traces from and choose **View Streaming Traces**</span></span>
   
    ![檢視遠端串流追蹤][viewremotestreamingtraces]
   
    <span data-ttu-id="41d92-165">對您想要查看其追蹤的任意數目的節點，重複執行步驟 2。</span><span class="sxs-lookup"><span data-stu-id="41d92-165">Repeat step 2 for as many nodes as you want to see traces from.</span></span> <span data-ttu-id="41d92-166">每個節點串流會顯示在專用視窗中。</span><span class="sxs-lookup"><span data-stu-id="41d92-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="41d92-167">您現在可以查看 Service Fabric 所發出的追蹤，以及您的服務。</span><span class="sxs-lookup"><span data-stu-id="41d92-167">You are now able to see the traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="41d92-168">如果您想要篩選事件，只顯示特定的應用程式，只要在篩選器中輸入應用程式的名稱即可。</span><span class="sxs-lookup"><span data-stu-id="41d92-168">If you want to filter the events to only show a specific application, simply type in the name of the application in the filter.</span></span>
   
    ![檢視串流追蹤][viewingstreamingtraces]
3. <span data-ttu-id="41d92-170">完成從您的叢集串流追蹤後，在 [雲端總管] 中以滑鼠右鍵按一下此叢集，選擇 [停用串流追蹤]，即可停用遠端串流追蹤</span><span class="sxs-lookup"><span data-stu-id="41d92-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking the cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![停用遠端串流追蹤][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="41d92-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41d92-172">Next steps</span></span>
* <span data-ttu-id="41d92-173">[測試 Service Fabric 服務](service-fabric-testability-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="41d92-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="41d92-174">[在 Visual Studio 中管理 Service Fabric 應用程式](service-fabric-manage-application-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="41d92-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

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
