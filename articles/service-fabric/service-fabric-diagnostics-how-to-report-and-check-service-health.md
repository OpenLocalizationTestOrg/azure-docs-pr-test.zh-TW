---
title: "使用 Service Fabric 回報和檢查健全狀況 | Microsoft Docs"
description: "了解如何從您的服務程式碼傳送健全狀況報告，以及如何使用 Azure Service Fabric 所提供的健全狀況監視工具檢查您服務的健全狀況。"
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="da62f-103">回報和檢查服務健康情況</span><span class="sxs-lookup"><span data-stu-id="da62f-103">Report and check service health</span></span>
<span data-ttu-id="da62f-104">當您的服務發生問題時，您回應並修正事件和中斷的能力，取決於您快速偵測問題的能力。</span><span class="sxs-lookup"><span data-stu-id="da62f-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="da62f-105">如果您從服務程式碼向 Azure Service Fabric 健全狀況管理員回報問題和失敗，您便可以使用 Service Fabric 提供的標準健全狀況監視工具來檢查健全狀況。</span><span class="sxs-lookup"><span data-stu-id="da62f-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="da62f-106">有三種方式可讓您回報服務的健全狀況：</span><span class="sxs-lookup"><span data-stu-id="da62f-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="da62f-107">使用 [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) 或 [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) 物件。</span><span class="sxs-lookup"><span data-stu-id="da62f-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="da62f-108">您可以使用 `Partition` 和 `CodePackageActivationContext` 物件在屬於目前內容一部分的項目中回報健全狀況。</span><span class="sxs-lookup"><span data-stu-id="da62f-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="da62f-109">比方說，做為複本一部分執行的程式碼只能回報該複本、其所屬的分割區，以及其所屬應用程式的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="da62f-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="da62f-110">使用 `FabricClient`。</span><span class="sxs-lookup"><span data-stu-id="da62f-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="da62f-111">當叢集不是[安全的](service-fabric-cluster-security.md)或者服務是以系統管理員權限執行時，您才能使用 `FabricClient`，從服務程式碼回報健全狀況。</span><span class="sxs-lookup"><span data-stu-id="da62f-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="da62f-112">大部分的實際案例不會使用不安全的叢集，或提供系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="da62f-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="da62f-113">您可以使用 `FabricClient`，回報任何屬於叢集一部分之實體的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="da62f-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="da62f-114">然而在理想的情況下，服務程式碼應該只會傳送與其本身健全狀況相關的報告。</span><span class="sxs-lookup"><span data-stu-id="da62f-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="da62f-115">使用位於叢集、應用程式、已部署應用程式、服務、服務套件、磁碟分割、複本或節點層級的 REST API。</span><span class="sxs-lookup"><span data-stu-id="da62f-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="da62f-116">這可用來從容器內部回報健全狀況。</span><span class="sxs-lookup"><span data-stu-id="da62f-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="da62f-117">這篇文章會引導您完成從服務程式碼回報健全狀況的範例。</span><span class="sxs-lookup"><span data-stu-id="da62f-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="da62f-118">此範例也會示範如何使用 Service Fabric 提供的工具來檢查健康情況。</span><span class="sxs-lookup"><span data-stu-id="da62f-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="da62f-119">本文旨在快速介紹 Service Fabric 的健全狀況監視功能。</span><span class="sxs-lookup"><span data-stu-id="da62f-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="da62f-120">如需更詳細的資訊，您可以閱讀一系列有關健全狀況的深入文章，從本文結尾的連結開始。</span><span class="sxs-lookup"><span data-stu-id="da62f-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da62f-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="da62f-121">Prerequisites</span></span>
<span data-ttu-id="da62f-122">您必須安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="da62f-122">You must have the following installed:</span></span>

* <span data-ttu-id="da62f-123">Visual Studio 2015 或 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="da62f-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="da62f-124">Service Fabric SDK</span><span class="sxs-lookup"><span data-stu-id="da62f-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="da62f-125">建立本機的安全開發人員叢集</span><span class="sxs-lookup"><span data-stu-id="da62f-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="da62f-126">以系統管理員權限開啟 PowerShell 並執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="da62f-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![示範如何建立安全開發人員叢集的命令](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="da62f-128">部署應用程式並檢查其健康情況</span><span class="sxs-lookup"><span data-stu-id="da62f-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="da62f-129">以系統管理員身分開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="da62f-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="da62f-130">使用 **具狀態服務** 範本建立專案。</span><span class="sxs-lookup"><span data-stu-id="da62f-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![建立與具狀態服務搭配使用的 Service Fabric 應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="da62f-132">按 **F5** 以在偵錯模式中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="da62f-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="da62f-133">應用程式會部署至本機叢集。</span><span class="sxs-lookup"><span data-stu-id="da62f-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="da62f-134">應用程式執行之後，在通知區域中的本機叢集管理員圖示上按一下滑鼠右鍵，然後從捷徑功能表選取 管理本機叢集  ，以開啟 Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="da62f-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![從通知區域開啟 Service Fabric 總管](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="da62f-136">應用程式健全狀況應該會如此圖所示。</span><span class="sxs-lookup"><span data-stu-id="da62f-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="da62f-137">此時，應用程式應該狀況良好而沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="da62f-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![Service Fabric 總管中狀況良好的應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="da62f-139">您也可以使用 PowerShell 來檢查健康情況。</span><span class="sxs-lookup"><span data-stu-id="da62f-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="da62f-140">您可以使用 ```Get-ServiceFabricApplicationHealth``` 檢查應用程式的健全狀況，而且您可以使用 ```Get-ServiceFabricServiceHealth``` 來檢查服務的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="da62f-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="da62f-141">在 PowerShell 中適用於相同應用程式的健全狀況報告位於此圖中。</span><span class="sxs-lookup"><span data-stu-id="da62f-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![PowerShell 中狀況良好的應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="da62f-143">將自訂健康情況事件新增至您的服務程式碼</span><span class="sxs-lookup"><span data-stu-id="da62f-143">To add custom health events to your service code</span></span>
<span data-ttu-id="da62f-144">Visual Studio 中的 Service Fabric 專案範本包含範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="da62f-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="da62f-145">以下步驟說明如何從您的服務程式碼回報自訂健全狀況事件。</span><span class="sxs-lookup"><span data-stu-id="da62f-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="da62f-146">這類報告會自動顯示在 Service Fabric 所提供之健康情況監視的標準工具中，例如 Service Fabric Explorer、Azure 入口網站健康情況檢視以及 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="da62f-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="da62f-147">在 Visual Studio 中重新開啟您先前建立的應用程式，或使用 **具狀態服務** Visual Studio 範本建立新應用程式。</span><span class="sxs-lookup"><span data-stu-id="da62f-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="da62f-148">開啟 Stateful1.cs 檔案，並尋找 `RunAsync` 方法中的 `myDictionary.TryGetValueAsync` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="da62f-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="da62f-149">您可以看到這個方法傳回存放目前計數器值的 `result` ，因為此應用程式的主要邏輯是要讓計數能夠執行。</span><span class="sxs-lookup"><span data-stu-id="da62f-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="da62f-150">如果這是一個實際的應用程式，且缺乏結果代表失敗，您會想要標示該事件。</span><span class="sxs-lookup"><span data-stu-id="da62f-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="da62f-151">若要在缺乏結果代表失敗時回報健全狀況事件，請新增下列步驟。</span><span class="sxs-lookup"><span data-stu-id="da62f-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="da62f-152">a.</span><span class="sxs-lookup"><span data-stu-id="da62f-152">a.</span></span> <span data-ttu-id="da62f-153">請將 `System.Fabric.Health` 命名空間新增至 Stateful1.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="da62f-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="da62f-154">b.</span><span class="sxs-lookup"><span data-stu-id="da62f-154">b.</span></span> <span data-ttu-id="da62f-155">在 `myDictionary.TryGetValueAsync` 呼叫之後新增下列程式碼</span><span class="sxs-lookup"><span data-stu-id="da62f-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="da62f-156">我們會回報複本健全狀況，因為它是從具狀態服務回報的。</span><span class="sxs-lookup"><span data-stu-id="da62f-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="da62f-157">`HealthInformation` 參數會儲存所要回報之健全狀況問題的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="da62f-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="da62f-158">如果您已建立無狀態服務，請使用下列程式碼</span><span class="sxs-lookup"><span data-stu-id="da62f-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="da62f-159">如果您的服務是以系統管理員權限執行，或者叢集不是[安全的](service-fabric-cluster-security.md)，您也可以使用 `FabricClient` 來回報健全狀況，如下列步驟所示。</span><span class="sxs-lookup"><span data-stu-id="da62f-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="da62f-160">a.</span><span class="sxs-lookup"><span data-stu-id="da62f-160">a.</span></span> <span data-ttu-id="da62f-161">在 `var myDictionary` 宣告之後建立 `FabricClient`。</span><span class="sxs-lookup"><span data-stu-id="da62f-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="da62f-162">b.</span><span class="sxs-lookup"><span data-stu-id="da62f-162">b.</span></span> <span data-ttu-id="da62f-163">在 `myDictionary.TryGetValueAsync` 呼叫之後新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="da62f-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="da62f-164">讓我們來模擬此失敗並看它顯示在健康情況監視工具中。</span><span class="sxs-lookup"><span data-stu-id="da62f-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="da62f-165">若要模擬此失敗，請將您稍早新增的健全狀況回報程式碼中的第一行標記成註解。</span><span class="sxs-lookup"><span data-stu-id="da62f-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="da62f-166">將第一行標記成註解之後，程式碼會看起來如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="da62f-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="da62f-167">此程式碼會在每次 `RunAsync` 執行時引發健康情況報告。</span><span class="sxs-lookup"><span data-stu-id="da62f-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="da62f-168">在您進行變更之後，請按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="da62f-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="da62f-169">在應用程式執行之後，開啟 [Service Fabric 總管] 來檢查應用程式的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="da62f-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="da62f-170">這次，[Service Fabric Explorer] 會將應用程式顯示為健康情況不良。</span><span class="sxs-lookup"><span data-stu-id="da62f-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="da62f-171">這是因為我們先前新增的程式碼所回報的錯誤所致。</span><span class="sxs-lookup"><span data-stu-id="da62f-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Service Fabric 總管中狀況不良的應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="da62f-173">如果您在 [Service Fabric 總管] 的樹狀結構檢視中選取主要複本，您將會看到 **健全狀態** 也顯示為發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="da62f-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="da62f-174">[Service Fabric 總管] 也會顯示已新增至程式碼中 `HealthInformation` 參數的健全狀況報告詳細資料。</span><span class="sxs-lookup"><span data-stu-id="da62f-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="da62f-175">您可以在 PowerShell 和 Azure 入口網站中看到相同的健全狀況報告。</span><span class="sxs-lookup"><span data-stu-id="da62f-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Service Fabric 總管中的複本健康情況](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="da62f-177">此報告會保留在健康情況管理員中，直到被另一份報告取代或直到此複本被刪除為止。</span><span class="sxs-lookup"><span data-stu-id="da62f-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="da62f-178">因為我們並未在 `HealthInformation` 物件中設定此健康情況報告的 `TimeToLive`，所以報告永遠不會到期。</span><span class="sxs-lookup"><span data-stu-id="da62f-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="da62f-179">建議您應該在最細微的層級上回報健全狀況，在此案例中為複本。</span><span class="sxs-lookup"><span data-stu-id="da62f-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="da62f-180">您也可以回報 `Partition`的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="da62f-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="da62f-181">若要回報 `Application`、`DeployedApplication`、`DeployedServicePackage` 的健全狀況，請使用 `CodePackageActivationContext`。</span><span class="sxs-lookup"><span data-stu-id="da62f-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="da62f-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da62f-182">Next steps</span></span>
* [<span data-ttu-id="da62f-183">深入了解 Service Fabric 健康情況</span><span class="sxs-lookup"><span data-stu-id="da62f-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="da62f-184">回報服務健全狀況的 REST API</span><span class="sxs-lookup"><span data-stu-id="da62f-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="da62f-185">回報應用程式健全狀況的 REST API</span><span class="sxs-lookup"><span data-stu-id="da62f-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

