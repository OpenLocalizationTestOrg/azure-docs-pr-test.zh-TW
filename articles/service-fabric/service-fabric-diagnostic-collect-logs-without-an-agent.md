---
title: "aaaCollect 記錄直接從 Azure Service Fabric 服務處理程序 |Microsoft Azure"
description: "說明 Service Fabric 應用程式可以傳送記錄檔，直接 tooa 中央位置，例如 Azure Application Insights 或 Elasticsearch，不需依賴 Azure 診斷代理程式。"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="eafca-103">直接從 Azure Service Fabric 服務處理程序收集記錄檔</span><span class="sxs-lookup"><span data-stu-id="eafca-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="eafca-104">同處理序記錄檔收集</span><span class="sxs-lookup"><span data-stu-id="eafca-104">In-process log collection</span></span>
<span data-ttu-id="eafca-105">使用收集應用程式記錄檔[Azure 診斷擴充功能](service-fabric-diagnostics-how-to-setup-wad.md)是個不錯的選擇**Azure Service Fabric**服務如果 hello 的記錄檔來源和目的地是很小，不會變更通常也那里是 hello 來源與目的地之間的直接對應。</span><span class="sxs-lookup"><span data-stu-id="eafca-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="eafca-106">如果沒有，另一個方法是 toohave 服務傳送其記錄檔直接 tooa 中央位置。</span><span class="sxs-lookup"><span data-stu-id="eafca-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="eafca-107">此處理程序稱為「同處理序記錄檔收集」，其中提供數個潛在的優點：</span><span class="sxs-lookup"><span data-stu-id="eafca-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="eafca-108">*輕鬆設定及部署*</span><span class="sxs-lookup"><span data-stu-id="eafca-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="eafca-109">診斷資料收集的 hello 組態只是 hello 服務組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="eafca-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="eafca-110">它是簡單 tooalways 保持其 「 同步 」 以 hello 其餘部分的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eafca-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="eafca-111">輕鬆就可達成個別應用程式或個別服務的組態。</span><span class="sxs-lookup"><span data-stu-id="eafca-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="eafca-112">代理程式為基礎的記錄檔集合，通常需要不同的部署和 hello 診斷代理程式的設定，這是額外的管理工作和錯誤的潛在來源。</span><span class="sxs-lookup"><span data-stu-id="eafca-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="eafca-113">通常是允許每個虛擬機器 （節點） 的 hello 代理程式只有一個執行個體和所有應用程式和該節點上執行的服務之間共用 hello 代理程式設定。</span><span class="sxs-lookup"><span data-stu-id="eafca-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="eafca-114">*彈性*</span><span class="sxs-lookup"><span data-stu-id="eafca-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="eafca-115">hello 應用程式可以傳送 hello 資料每當需要 toogo，只要用戶端程式庫支援 hello 目標資料儲存系統。</span><span class="sxs-lookup"><span data-stu-id="eafca-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="eafca-116">您可以視需要新增新的目的地。</span><span class="sxs-lookup"><span data-stu-id="eafca-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="eafca-117">可以實作複雜的擷取、篩選和資料彙總規則。</span><span class="sxs-lookup"><span data-stu-id="eafca-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="eafca-118">代理程式為基礎的記錄檔集合通常會受限於 hello 代理程式支援的 hello 資料接收器。</span><span class="sxs-lookup"><span data-stu-id="eafca-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="eafca-119">有些代理程式是可擴充的。</span><span class="sxs-lookup"><span data-stu-id="eafca-119">Some agents are extensible.</span></span>

* <span data-ttu-id="eafca-120">*存取 toointernal 應用程式資料和內容*</span><span class="sxs-lookup"><span data-stu-id="eafca-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="eafca-121">hello hello 應用程式/服務處理序內執行的診斷子系統可以輕鬆地擴大 hello 與內容資訊的追蹤。</span><span class="sxs-lookup"><span data-stu-id="eafca-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="eafca-122">代理程式為基礎的記錄檔集合與 hello 必須傳送資料 tooan 代理程式，透過某種處理序間通訊機制，例如 Windows 事件追蹤。</span><span class="sxs-lookup"><span data-stu-id="eafca-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="eafca-123">此機制可能會造成額外的限制。</span><span class="sxs-lookup"><span data-stu-id="eafca-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="eafca-124">它也可能 toocombine 這兩個集合的方法而獲益。</span><span class="sxs-lookup"><span data-stu-id="eafca-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="eafca-125">事實上，它可能 hello 對於許多應用程式的最佳解決方案。</span><span class="sxs-lookup"><span data-stu-id="eafca-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="eafca-126">代理程式為基礎的集合是用來收集記錄檔相關的 toohello 整個叢集和個別叢集節點的自然解決方案。</span><span class="sxs-lookup"><span data-stu-id="eafca-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="eafca-127">這是更可靠的方式，比同處理序記錄檔收集、 toodiagnose 服務啟動問題和當機。</span><span class="sxs-lookup"><span data-stu-id="eafca-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="eafca-128">此外，Service Fabric 叢集內執行的許多服務，以執行它自己的處理序記錄檔收集每個服務會導致從 hello 叢集中的多個傳出連線。</span><span class="sxs-lookup"><span data-stu-id="eafca-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="eafca-129">Hello 網路子系統和 hello 記錄目的地，會消耗大量的連出連線。</span><span class="sxs-lookup"><span data-stu-id="eafca-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="eafca-130">[**Azure 診斷**](../cloud-services/cloud-services-dotnet-diagnostics.md)之類的代理程式可以從多個服務收集資料，然後透過幾條連線傳送所有資料，藉此改善輸送量。</span><span class="sxs-lookup"><span data-stu-id="eafca-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="eafca-131">在本文中，我們會示範 tooset 向上同處理序記錄的集合使用[ **EventFlow 開放原始碼程式庫**](https://github.com/Azure/diagnostics-eventflow)。</span><span class="sxs-lookup"><span data-stu-id="eafca-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="eafca-132">可能使用其他程式庫 hello 相同目的，但 EventFlow 具有 hello 優點需要同處理序記錄檔收集和 toosupport Service Fabric 服務專用的設計。</span><span class="sxs-lookup"><span data-stu-id="eafca-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="eafca-133">我們使用[ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/)做為 hello 記錄目的地。</span><span class="sxs-lookup"><span data-stu-id="eafca-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="eafca-134">其他像是[**事件中樞**](https://azure.microsoft.com/services/event-hubs/)或 [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) 也都是支援的目的地。</span><span class="sxs-lookup"><span data-stu-id="eafca-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="eafca-135">它是只安裝適當的 NuGet 封裝和設定 hello 目的地 hello EventFlow 組態檔中的問題。</span><span class="sxs-lookup"><span data-stu-id="eafca-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="eafca-136">如需有關 Application Insights 以外之記錄檔目的地的詳細資訊，請參閱 [EventFlow 文件](https://github.com/Azure/diagnostics-eventflow)。</span><span class="sxs-lookup"><span data-stu-id="eafca-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="eafca-137">加入 EventFlow 庫 tooa Service Fabric 服務專案</span><span class="sxs-lookup"><span data-stu-id="eafca-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="eafca-138">EventFlow 二進位檔是以一組 NuGet 套件的形式提供。</span><span class="sxs-lookup"><span data-stu-id="eafca-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="eafca-139">tooadd EventFlow tooa Service Fabric 服務專案中，hello 方案總管 中的 hello 專案上按一下滑鼠右鍵，然後選擇 「 管理 NuGet 套件 」。</span><span class="sxs-lookup"><span data-stu-id="eafca-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="eafca-140">切換 toohello [瀏覽] 索引標籤，並搜尋"`Diagnostics.EventFlow`」:</span><span class="sxs-lookup"><span data-stu-id="eafca-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet 套件管理員 UI 中的 EventFlow NuGet 套件][1]

<span data-ttu-id="eafca-142">hello 服務裝載 EventFlow 應該包含適當的封裝，根據 hello 來源和目的地 hello 應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="eafca-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="eafca-143">新增下列封裝的 hello:</span><span class="sxs-lookup"><span data-stu-id="eafca-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="eafca-144">(從 hello 服務 EventSource 類別，以及從這類的標準 EventSources toocapture 資料*Microsoft ServiceFabric 服務*和*Microsoft-ServiceFabric 演員*)</span><span class="sxs-lookup"><span data-stu-id="eafca-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="eafca-145">（我們 toosend hello 記錄 tooan Azure Application Insights 資源）</span><span class="sxs-lookup"><span data-stu-id="eafca-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="eafca-146">（可讓 hello EventFlow 管線就會從 Service Fabric 服務組態的初始化和報告與 Service Fabric 健康情況報告的形式傳送診斷資料的任何問題）</span><span class="sxs-lookup"><span data-stu-id="eafca-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="eafca-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`封裝需要 hello 服務專案 tootarget.NET Framework 4.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="eafca-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="eafca-148">請確定您在專案屬性中設定 hello 適當的目標 framework 之前安裝此套件。</span><span class="sxs-lookup"><span data-stu-id="eafca-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="eafca-149">在所有 hello 已安裝的套件，hello 下一個步驟是 tooconfigure 和啟用 EventFlow hello 服務中。</span><span class="sxs-lookup"><span data-stu-id="eafca-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="eafca-150">設定及啟用記錄檔收集</span><span class="sxs-lookup"><span data-stu-id="eafca-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="eafca-151">EventFlow 管線，負責傳送嗨記錄檔，會建立從儲存在組態檔中的規格。</span><span class="sxs-lookup"><span data-stu-id="eafca-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="eafca-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` 套件會在 `PackageRoot\Config` 方案資料夾底下安裝一個起始的 EventFlow 組態檔。</span><span class="sxs-lookup"><span data-stu-id="eafca-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="eafca-153">hello 檔案名稱為`eventFlowConfig.json`。</span><span class="sxs-lookup"><span data-stu-id="eafca-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="eafca-154">此組態檔必須 hello 預設服務的修改 toobe toocapture 資料`EventSource`類別，並傳送資料 tooApplication Insights 服務。</span><span class="sxs-lookup"><span data-stu-id="eafca-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="eafca-155">我們假設您已熟悉**Azure Application Insights**服務，而且您擁有您規劃 toouse toomonitor Service Fabric 服務的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="eafca-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="eafca-156">如需詳細資訊，請參閱[建立 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="eafca-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="eafca-157">開啟 hello `eventFlowConfig.json` hello 編輯器中的檔案，並變更其內容，如下所示。</span><span class="sxs-lookup"><span data-stu-id="eafca-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="eafca-158">請確定 tooreplace hello ServiceEventSource 名稱並根據 toocomments Application Insights 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="eafca-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> <span data-ttu-id="eafca-159">服務的 ServiceEventSource hello 名稱是 hello hello hello 名稱屬性值`EventSourceAttribute`套用 toohello ServiceEventSource 類別。</span><span class="sxs-lookup"><span data-stu-id="eafca-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="eafca-160">它內指定 all hello`ServiceEventSource.cs`屬於 hello 服務程式碼的檔案。</span><span class="sxs-lookup"><span data-stu-id="eafca-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="eafca-161">例如，在 hello hello ServiceEventSource 的下列程式碼片段 hello 名稱是*MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="eafca-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="eafca-162">請注意，`eventFlowConfig.json` 檔案是服務組態封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="eafca-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="eafca-163">變更 toothis 檔案可以包含在完整或組態-僅限 hello 服務的升級，則主體 tooService 網狀架構升級健全狀況檢查和自動回復升級失敗時。</span><span class="sxs-lookup"><span data-stu-id="eafca-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="eafca-164">如需詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="eafca-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="eafca-165">hello 最後一個步驟是在服務的啟動程式碼，位於 tooinstantiate EventFlow 管線`Program.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="eafca-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="eafca-166">在 hello 新增下列範例 EventFlow 相關項目都以註解的開頭標示`****`:</span><span class="sxs-lookup"><span data-stu-id="eafca-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    
                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

<span data-ttu-id="eafca-167">hello 名稱傳遞為 hello hello 參數`CreatePipeline`方法 hello `ServiceFabricDiagnosticsPipelineFactory` hello hello 名稱*健全狀況實體*代表 hello EventFlow 記錄集合管線。</span><span class="sxs-lookup"><span data-stu-id="eafca-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="eafca-168">如果 EventFlow 遇到，會使用這個名稱和錯誤，並報告透過 hello 服務網狀架構健全狀況子系統。</span><span class="sxs-lookup"><span data-stu-id="eafca-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="eafca-169">驗證</span><span class="sxs-lookup"><span data-stu-id="eafca-169">Verification</span></span>
<span data-ttu-id="eafca-170">啟動您的服務，並觀察 hello 偵錯 Visual Studio 中的 [輸出] 視窗。</span><span class="sxs-lookup"><span data-stu-id="eafca-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="eafca-171">Hello 服務啟動之後，您應該會開始看到您的服務將 「 Application Insights 遙測 」 資料錄的辨識項。</span><span class="sxs-lookup"><span data-stu-id="eafca-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="eafca-172">開啟網頁瀏覽器並瀏覽移 tooyour Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="eafca-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="eafca-173">開啟 「 搜尋 」 索引標籤 （在 hello hello 預設 「 概觀 」 刀鋒視窗頂端）。</span><span class="sxs-lookup"><span data-stu-id="eafca-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="eafca-174">您應該在短暫延遲之後會開始看到您在 hello Application Insights 入口網站中的追蹤：</span><span class="sxs-lookup"><span data-stu-id="eafca-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![顯示來自 Service Fabric 應用程式之記錄檔的 Application Insights 入口網站][2]

## <a name="next-steps"></a><span data-ttu-id="eafca-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eafca-176">Next steps</span></span>
* [<span data-ttu-id="eafca-177">深入了解診斷和監視 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="eafca-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="eafca-178">EventFlow 文件</span><span class="sxs-lookup"><span data-stu-id="eafca-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
