---
title: "Azure Service Fabric aaaReport 並檢查健全狀況 |Microsoft 文件"
description: "了解 toosend 健康情況報告的方式，從您的服務程式碼，以及如何提供您的服務使用該 Azure Service Fabric hello 健全狀況監視工具 toocheck hello 健全狀況。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="7e1cb-103">回報和檢查服務健康情況</span><span class="sxs-lookup"><span data-stu-id="7e1cb-103">Report and check service health</span></span>
<span data-ttu-id="7e1cb-104">當您的服務時遇到問題時，能力 toorespond tooand 修正事件及中斷相依於您能力 toodetect hello 問題快速。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="7e1cb-105">如果您所回報的問題與失敗 toohello Azure Service Fabric 健全狀況管理員從服務程式碼，您可以使用標準的健全狀況監視 Service Fabric 提供 toocheck hello 健全狀況狀態的工具。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="7e1cb-106">有三種方式，您可以報告的 hello 服務健全狀況：</span><span class="sxs-lookup"><span data-stu-id="7e1cb-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="7e1cb-107">使用 [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) 或 [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) 物件。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="7e1cb-108">您可以使用 hello`Partition`和`CodePackageActivationContext`tooreport hello 健全狀況的項目屬於的 hello 目前內容的物件。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="7e1cb-109">比方說，做為複本的一部分執行的程式碼可以在該複本，其所屬的 hello 磁碟分割和 hello 應用程式，即屬於上報告健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="7e1cb-110">使用 `FabricClient`。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="7e1cb-111">您可以使用`FabricClient`tooreport 健全狀況從 hello 服務程式碼如果 hello 叢集不是[安全](service-fabric-cluster-security.md)或如果 hello 服務以系統管理員權限執行。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="7e1cb-112">大部分的實際案例不會使用不安全的叢集，或提供系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="7e1cb-113">與`FabricClient`，您可以報告的任何實體會屬於 hello 叢集的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="7e1cb-114">在理想情況下，不過，服務程式碼應該只能傳送相關的 tooits 自己健全狀況報表。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="7e1cb-115">使用 REST Api hello hello 叢集、 應用程式、 部署的應用程式、 服務、 服務封裝、 資料分割、 複本或節點層級。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="7e1cb-116">這可以是從容器內的使用的 tooreport 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="7e1cb-117">這篇文章會引導您從 hello 服務程式碼的健康情況報告的範例。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="7e1cb-118">hello 範例也會示範如何提供 Service Fabric hello 工具可以使用的 toocheck hello 健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="7e1cb-119">本文是快速介紹 toohello 健全狀況監視功能的 Service Fabric 預定的 toobe。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="7e1cb-120">如需詳細資訊，您可以閱讀 hello 系列有關健康情況深入開頭 hello hello 本文結尾處的連結的文件。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e1cb-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="7e1cb-121">Prerequisites</span></span>
<span data-ttu-id="7e1cb-122">您必須安裝下列元件 hello:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-122">You must have hello following installed:</span></span>

* <span data-ttu-id="7e1cb-123">Visual Studio 2015 或 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7e1cb-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="7e1cb-124">Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="7e1cb-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="7e1cb-125">toocreate 安全的本機開發叢集</span><span class="sxs-lookup"><span data-stu-id="7e1cb-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="7e1cb-126">以管理員權限，開啟 PowerShell 並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e1cb-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![命令會顯示如何 toocreate 安全的開發人員叢集](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="7e1cb-128">toodeploy 應用程式並檢查其健全狀況</span><span class="sxs-lookup"><span data-stu-id="7e1cb-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="7e1cb-129">以系統管理員身分開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="7e1cb-130">建立專案使用 hello**可設定狀態服務**範本。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![建立與具狀態服務搭配使用的 Service Fabric 應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="7e1cb-132">按**F5** toorun hello 應用程式中偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="7e1cb-133">hello 應用程式是部署的 toohello 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="7e1cb-134">Hello 應用程式執行之後，hello 通知區域中的 hello 本機叢集管理員圖示上按一下滑鼠右鍵，然後選取 **管理本機叢集**從 hello 快顯功能表 tooopen Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![從通知區域開啟 Service Fabric 總管](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="7e1cb-136">如同此映像，應該會顯示 hello 應用程式健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="7e1cb-137">此時，hello 應用程式應該是狀況良好且未發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![Service Fabric 總管中狀況良好的應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="7e1cb-139">您也可以使用 PowerShell 來檢查 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="7e1cb-140">您可以使用```Get-ServiceFabricApplicationHealth```toocheck 應用程式的健全狀況，而且您可以使用```Get-ServiceFabricServiceHealth```toocheck 服務的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="7e1cb-141">hello hello PowerShell 中的相同應用程式是在這個影像的健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![PowerShell 中狀況良好的應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="7e1cb-143">tooadd 自訂健全狀況事件 tooyour 服務程式碼</span><span class="sxs-lookup"><span data-stu-id="7e1cb-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="7e1cb-144">Visual Studio 中的 hello Service Fabric 專案範本包含範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="7e1cb-145">hello 下列步驟示範如何報告自訂健全狀況事件，以及在您的服務程式碼。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="7e1cb-146">這類報表會自動顯示 hello 標準工具中的健全狀況監視，Service Fabric 提供，例如 Service Fabric 總管、 Azure 入口網站的健全狀況檢視和 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="7e1cb-147">重新開啟您先前建立在 Visual Studio 中的 hello 應用程式，或建立新的應用程式使用 hello**可設定狀態服務**Visual Studio 範本。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="7e1cb-148">開啟 hello Stateful1.cs 檔案，並尋找 hello`myDictionary.TryGetValueAsync`呼叫 hello`RunAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="7e1cb-149">您可以看到這個方法會傳回`result`保存 hello hello 計數器的目前值，因為此應用程式中的 hello 主要邏輯是 tookeep 計數執行。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="7e1cb-150">如果這是實際的應用程式，而且 hello 缺乏結果表示失敗，您會想 tooflag 該事件。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="7e1cb-151">tooreport hello 缺乏結果代表發生失敗時的健全狀況事件加入 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="7e1cb-152">a.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-152">a.</span></span> <span data-ttu-id="7e1cb-153">新增 hello`System.Fabric.Health`命名空間 toohello Stateful1.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="7e1cb-154">b.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-154">b.</span></span> <span data-ttu-id="7e1cb-155">新增下列程式碼之後 hello hello`myDictionary.TryGetValueAsync`呼叫</span><span class="sxs-lookup"><span data-stu-id="7e1cb-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="7e1cb-156">我們會回報複本健全狀況，因為它是從具狀態服務回報的。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="7e1cb-157">hello`HealthInformation`參數儲存報告的 hello 健全狀況問題的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="7e1cb-158">如果您建立無狀態服務，使用下列程式碼的 hello</span><span class="sxs-lookup"><span data-stu-id="7e1cb-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="7e1cb-159">如果您的服務正在執行以管理員權限，或如果 hello 叢集不[安全](service-fabric-cluster-security.md)，您也可以使用`FabricClient`tooreport 健全狀況 hello 步驟中所示。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="7e1cb-160">a.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-160">a.</span></span> <span data-ttu-id="7e1cb-161">建立 hello `FabricClient` hello 後的執行個體`var myDictionary`宣告。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="7e1cb-162">b.</span><span class="sxs-lookup"><span data-stu-id="7e1cb-162">b.</span></span> <span data-ttu-id="7e1cb-163">新增下列程式碼之後 hello hello`myDictionary.TryGetValueAsync`呼叫。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. <span data-ttu-id="7e1cb-164">讓我們來模擬此失敗，並查看顯示在 hello 健全狀況監視工具。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="7e1cb-165">註解 hello hello 健全狀況報告您先前加入的程式碼中的第一行 toosimulate hello 失敗。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="7e1cb-166">您標記為註解 hello 第一行之後，hello 程式碼看起來類似下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="7e1cb-167">此程式碼就會引發 hello 健康情況報告，每次`RunAsync`執行。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="7e1cb-168">Hello 變更之後，按**F5** toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="7e1cb-169">Hello 應用程式執行之後，開啟 Service Fabric 總管 toocheck hello hello 應用程式健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="7e1cb-170">目前，Service Fabric 總管會顯示 hello 應用程式狀況不良。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="7e1cb-171">這是因為已從 hello 程式碼，我們加入先前報告的 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Service Fabric 總管中狀況不良的應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="7e1cb-173">如果您選取 hello 主要複本的 Service Fabric 總管 hello 樹狀檢視中，您會看到**健全狀況狀態**太表示錯誤。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="7e1cb-174">Service Fabric 總管也會顯示 hello 健康情況報告詳細資料，加入 toohello `HealthInformation` hello 程式碼中的參數。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="7e1cb-175">您可以看到相同的健康情況報告，在 PowerShell 中的 hello 和 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Service Fabric 總管中的複本健康情況](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="7e1cb-177">除非取代為另一個報表，或刪除此複本之前，此報表會保留在 hello 健全狀況管理員。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="7e1cb-178">因為我們並未設定`TimeToLive`健全狀況報表在 hello`HealthInformation`物件 hello 報表永久有效。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="7e1cb-179">我們建議您應該在 hello 最細微的層級，即在此情況下 hello 複本回報健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="7e1cb-180">您也可以回報 `Partition`的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="7e1cb-181">tooreport 健全狀況`Application`， `DeployedApplication`，和`DeployedServicePackage`，使用`CodePackageActivationContext`。</span><span class="sxs-lookup"><span data-stu-id="7e1cb-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="7e1cb-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e1cb-182">Next steps</span></span>
* [<span data-ttu-id="7e1cb-183">深入了解 Service Fabric 健康情況</span><span class="sxs-lookup"><span data-stu-id="7e1cb-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="7e1cb-184">回報服務健全狀況的 REST API</span><span class="sxs-lookup"><span data-stu-id="7e1cb-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="7e1cb-185">回報應用程式健全狀況的 REST API</span><span class="sxs-lookup"><span data-stu-id="7e1cb-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

