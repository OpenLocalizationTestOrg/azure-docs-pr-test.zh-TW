---
title: "直接從 Azure Service Fabric 服務處理程序收集記錄檔 | Microsoft Azure"
description: "說明 Service Fabric 應用程式可以將記錄檔直接傳送到中央位置 (例如 Azure Application Insights 或 Elasticsearch)，而不需倚賴「Azure 診斷」代理程式。"
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
ms.openlocfilehash: b7d2541928f4248750417a77d99033c8b4354dcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="9fb74-103">直接從 Azure Service Fabric 服務處理程序收集記錄檔</span><span class="sxs-lookup"><span data-stu-id="9fb74-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="9fb74-104">同處理序記錄檔收集</span><span class="sxs-lookup"><span data-stu-id="9fb74-104">In-process log collection</span></span>
<span data-ttu-id="9fb74-105">如果記錄檔來源與目的地的集合都很小、不常變更，並且來源與其目的地之間有直接的對應，則使用 [Azure 診斷擴充功能](service-fabric-diagnostics-how-to-setup-wad.md)來收集應用程式記錄檔，對 **Azure Service Fabric** 服務來說是一個好選項。</span><span class="sxs-lookup"><span data-stu-id="9fb74-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if the set of log sources and destinations is small, does not change often, and there is a straightforward mapping between the sources and their destinations.</span></span> <span data-ttu-id="9fb74-106">如果不是上述情況，替代方式是讓服務將其記錄檔直接傳送到一個中央位置。</span><span class="sxs-lookup"><span data-stu-id="9fb74-106">If not, an alternative is to have services send their logs directly to a central location.</span></span> <span data-ttu-id="9fb74-107">此處理程序稱為「同處理序記錄檔收集」，其中提供數個潛在的優點：</span><span class="sxs-lookup"><span data-stu-id="9fb74-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="9fb74-108">*輕鬆設定及部署*</span><span class="sxs-lookup"><span data-stu-id="9fb74-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="9fb74-109">診斷資料收集組態只是服務組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="9fb74-109">The configuration of diagnostic data collection is just part of the service configuration.</span></span> <span data-ttu-id="9fb74-110">將其與應用程式的其餘部分始終保持「同步」很簡單。</span><span class="sxs-lookup"><span data-stu-id="9fb74-110">It is easy to always keep it "in sync" with the rest of the application.</span></span>
    * <span data-ttu-id="9fb74-111">輕鬆就可達成個別應用程式或個別服務的組態。</span><span class="sxs-lookup"><span data-stu-id="9fb74-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="9fb74-112">代理程式型記錄檔收集通常需要個別部署和設定診斷代理程式，這是額外的系統管理工作，也是可能的錯誤來源。</span><span class="sxs-lookup"><span data-stu-id="9fb74-112">Agent-based log collection usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="9fb74-113">通常，每一虛擬機器 (節點) 只允許一個代理程式執行個體，而在該節點上執行的所有應用程式和服務會共用代理程式組態。</span><span class="sxs-lookup"><span data-stu-id="9fb74-113">Often there is only one instance of the agent allowed per virtual machine (node) and the agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="9fb74-114">*彈性*</span><span class="sxs-lookup"><span data-stu-id="9fb74-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="9fb74-115">只要用戶端程式庫支援目標資料儲存系統，應用程式可以將資料傳送至任何需要的地方。</span><span class="sxs-lookup"><span data-stu-id="9fb74-115">The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system.</span></span> <span data-ttu-id="9fb74-116">您可以視需要新增新的目的地。</span><span class="sxs-lookup"><span data-stu-id="9fb74-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="9fb74-117">可以實作複雜的擷取、篩選和資料彙總規則。</span><span class="sxs-lookup"><span data-stu-id="9fb74-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="9fb74-118">代理程式型記錄檔收集通常會受限於代理程式所支援的資料接收器。</span><span class="sxs-lookup"><span data-stu-id="9fb74-118">Agent-based log collection is often limited by the data sinks that the agent supports.</span></span> <span data-ttu-id="9fb74-119">有些代理程式是可擴充的。</span><span class="sxs-lookup"><span data-stu-id="9fb74-119">Some agents are extensible.</span></span>

* <span data-ttu-id="9fb74-120">*存取內部應用程式資料與內容*</span><span class="sxs-lookup"><span data-stu-id="9fb74-120">*Access to internal application data and context*</span></span>
   
    * <span data-ttu-id="9fb74-121">應用程式/服務處理序內執行的診斷子系統可以輕鬆地隨著內容資訊而擴大追蹤。</span><span class="sxs-lookup"><span data-stu-id="9fb74-121">The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.</span></span>
    * <span data-ttu-id="9fb74-122">使用代理程式型記錄檔收集時，必須透過某種處理序間的通訊機制 (例如 Windows 的「事件追蹤」) 將資料傳送給代理程式。</span><span class="sxs-lookup"><span data-stu-id="9fb74-122">With agent-based log collection, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="9fb74-123">此機制可能會造成額外的限制。</span><span class="sxs-lookup"><span data-stu-id="9fb74-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="9fb74-124">您可以結合這兩種收集方法來充分運用其優點。</span><span class="sxs-lookup"><span data-stu-id="9fb74-124">It is possible to combine and benefit from both collection methods.</span></span> <span data-ttu-id="9fb74-125">事實上，它可能是許多應用程式的最佳解決方案。</span><span class="sxs-lookup"><span data-stu-id="9fb74-125">Indeed, it might be the best solution for many applications.</span></span> <span data-ttu-id="9fb74-126">代理程式型收集是一個自然解決方案，適用於收集與整個叢集和個別叢集節點相關的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9fb74-126">Agent-based collection is a natural solution for collecting logs related to the whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="9fb74-127">與同處理序記錄檔收集相比，它是可診斷服務啟動問題和當機的較可靠方法。</span><span class="sxs-lookup"><span data-stu-id="9fb74-127">It is much more reliable way, than in-process log collection, to diagnose service startup problems and crashes.</span></span> <span data-ttu-id="9fb74-128">此外，在有許多服務在 Service Fabric 叢集內執行的情況下，如果每個服務都執行自己的同處理序記錄檔收集，將會導致從叢集傳出無數的連線。</span><span class="sxs-lookup"><span data-stu-id="9fb74-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from the cluster.</span></span> <span data-ttu-id="9fb74-129">大量的傳出連線會同時為網路子系統和記錄檔目的地帶來負擔。</span><span class="sxs-lookup"><span data-stu-id="9fb74-129">Large number of outgoing connections is taxing both for the network subsystem and for the log destination.</span></span> <span data-ttu-id="9fb74-130">[**Azure 診斷**](../cloud-services/cloud-services-dotnet-diagnostics.md)之類的代理程式可以從多個服務收集資料，然後透過幾條連線傳送所有資料，藉此改善輸送量。</span><span class="sxs-lookup"><span data-stu-id="9fb74-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="9fb74-131">在本文中，我們將說明如何使用 [**EventFlow 開放原始碼程式庫**](https://github.com/Azure/diagnostics-eventflow)來設定同處理序記錄檔收集。</span><span class="sxs-lookup"><span data-stu-id="9fb74-131">In this article, we show how to set up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="9fb74-132">其他程式庫或許可以用於相同的目的，但 EventFlow 的優點在於它是專門針對同處理序記錄檔收集而設計，並且支援 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="9fb74-132">Other libraries might be used for the same purpose, but EventFlow has the benefit of having been designed specifically for in-process log collection and to support Service Fabric services.</span></span> <span data-ttu-id="9fb74-133">我們將使用 [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) 作為記錄檔目的地。</span><span class="sxs-lookup"><span data-stu-id="9fb74-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as the log destination.</span></span> <span data-ttu-id="9fb74-134">其他像是[**事件中樞**](https://azure.microsoft.com/services/event-hubs/)或 [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) 也都是支援的目的地。</span><span class="sxs-lookup"><span data-stu-id="9fb74-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="9fb74-135">所要做的就是安裝適當的 NuGet 套件，並在 EventFlow 組態檔中設定目的地。</span><span class="sxs-lookup"><span data-stu-id="9fb74-135">It is just a question of installing appropriate NuGet package and configuring the destination in the EventFlow configuration file.</span></span> <span data-ttu-id="9fb74-136">如需有關 Application Insights 以外之記錄檔目的地的詳細資訊，請參閱 [EventFlow 文件](https://github.com/Azure/diagnostics-eventflow)。</span><span class="sxs-lookup"><span data-stu-id="9fb74-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-to-a-service-fabric-service-project"></a><span data-ttu-id="9fb74-137">將 EventFlow 程式庫新增到 Service Fabric 服務專案</span><span class="sxs-lookup"><span data-stu-id="9fb74-137">Adding EventFlow library to a Service Fabric service project</span></span>
<span data-ttu-id="9fb74-138">EventFlow 二進位檔是以一組 NuGet 套件的形式提供。</span><span class="sxs-lookup"><span data-stu-id="9fb74-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="9fb74-139">若要將 EventFlow 新增到 Service Fabric 服務專案，請在 [方案總管] 中該專案上按一下滑鼠右鍵，然後選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="9fb74-139">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="9fb74-140">切換到 [瀏覽] 索引標籤，然後搜尋 "`Diagnostics.EventFlow`"：</span><span class="sxs-lookup"><span data-stu-id="9fb74-140">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet 套件管理員 UI 中的 EventFlow NuGet 套件][1]

<span data-ttu-id="9fb74-142">視應用程式記錄檔的來源和目的地而定，裝載 EventFlow 的服務應該包含適當的套件。</span><span class="sxs-lookup"><span data-stu-id="9fb74-142">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="9fb74-143">請新增下列套件：</span><span class="sxs-lookup"><span data-stu-id="9fb74-143">Add the following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="9fb74-144">(用來從服務的 EventSource 類別以及從標準 EventSources (例如 *Microsoft-ServiceFabric-Services* 和 *Microsoft-ServiceFabric-Actors*) 擷取資料)</span><span class="sxs-lookup"><span data-stu-id="9fb74-144">(to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="9fb74-145">(我們將把記錄檔傳送給 Azure Application Insights 資源)</span><span class="sxs-lookup"><span data-stu-id="9fb74-145">(we are going to send the logs to an Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="9fb74-146">(允許從 Service Fabric 服務組態將 EventFlow 管線初始化，並以 Service Fabric 健康情況報告的形式傳送診斷資料來回報任何問題)</span><span class="sxs-lookup"><span data-stu-id="9fb74-146">(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="9fb74-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 套件會要求服務專案的目標必須是 .NET Framework 4.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9fb74-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="9fb74-148">安裝此套件之前，請先確定您已在專案屬性中設定適當的目標架構。</span><span class="sxs-lookup"><span data-stu-id="9fb74-148">Make sure you set the appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="9fb74-149">安裝好所有套件之後，下一個步驟就是設定及啟用服務中的 EventFlow。</span><span class="sxs-lookup"><span data-stu-id="9fb74-149">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="9fb74-150">設定及啟用記錄檔收集</span><span class="sxs-lookup"><span data-stu-id="9fb74-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="9fb74-151">EventFlow 管線 (負責傳送記錄檔) 是從儲存在組態檔中的規格建立的。</span><span class="sxs-lookup"><span data-stu-id="9fb74-151">EventFlow pipeline, responsible for sending the logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="9fb74-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` 套件會在 `PackageRoot\Config` 方案資料夾底下安裝一個起始的 EventFlow 組態檔。</span><span class="sxs-lookup"><span data-stu-id="9fb74-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="9fb74-153">檔案名稱是 `eventFlowConfig.json`。</span><span class="sxs-lookup"><span data-stu-id="9fb74-153">The file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="9fb74-154">此組態檔必須經過修改，才能從預設服務 `EventSource` 類別擷取資料，然後將資料傳送給 Application Insights 服務。</span><span class="sxs-lookup"><span data-stu-id="9fb74-154">This configuration file needs to be modified to capture data from the default service `EventSource` class and send data to Application Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="9fb74-155">我們假設您已熟悉 **Azure Application Insights** 服務，並且具有要用來監視 Service Fabric 服務的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="9fb74-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan to use to monitor your Service Fabric service.</span></span> <span data-ttu-id="9fb74-156">如需詳細資訊，請參閱[建立 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="9fb74-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="9fb74-157">在編輯器中開啟 `eventFlowConfig.json` 檔案，並依照以下所示變更其內容。</span><span class="sxs-lookup"><span data-stu-id="9fb74-157">Open the `eventFlowConfig.json` file in the editor and change its content as shown below.</span></span> <span data-ttu-id="9fb74-158">請務必根據註解取代 ServiceEventSource 名稱和 Application Insights 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="9fb74-158">Make sure to replace the ServiceEventSource name and Application Insights instrumentation key according to comments.</span></span> 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
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
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> <span data-ttu-id="9fb74-159">服務的 ServiceEventSource 名稱是套用至 ServiceEventSource 類別之 `EventSourceAttribute` 的 Name 屬性值。</span><span class="sxs-lookup"><span data-stu-id="9fb74-159">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="9fb74-160">全部都在 `ServiceEventSource.cs` 檔案中指定，此檔案是服務程式碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="9fb74-160">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="9fb74-161">例如，在下列程式碼片段中，ServiceEventSource 的名稱是 *MyCompany-Application1-Stateless1*：</span><span class="sxs-lookup"><span data-stu-id="9fb74-161">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="9fb74-162">請注意，`eventFlowConfig.json` 檔案是服務組態封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="9fb74-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="9fb74-163">對此檔案所做的變更可以包含在完整或僅限組態的服務升級中，並受到 Service Fabric 升級健康情況檢查和自動復原 (如果發生升級失敗) 控管。</span><span class="sxs-lookup"><span data-stu-id="9fb74-163">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="9fb74-164">如需詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="9fb74-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="9fb74-165">最後一個步驟是在服務的啟動程式碼 (位於 `Program.cs` 檔案中) 中將 EventFlow 管線具現化。</span><span class="sxs-lookup"><span data-stu-id="9fb74-165">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="9fb74-166">在下列範例中，EventFlow 相關的新增皆有開頭為 `****` 的註解標示：</span><span class="sxs-lookup"><span data-stu-id="9fb74-166">In the following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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
        /// This is the entry point of the service host process.
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

<span data-ttu-id="9fb74-167">當作 `ServiceFabricDiagnosticsPipelineFactory` 之 `CreatePipeline` 方法的參數來傳遞的名稱是「健康情況實體」的名稱，此實體代表 EventFlow 記錄檔收集管線。</span><span class="sxs-lookup"><span data-stu-id="9fb74-167">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="9fb74-168">當 EventFlow 發生錯誤並透過 Service Fabric 健康情況子系統回報錯誤時，就會使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="9fb74-168">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="9fb74-169">驗證</span><span class="sxs-lookup"><span data-stu-id="9fb74-169">Verification</span></span>
<span data-ttu-id="9fb74-170">啟動您的服務並觀察 Visual Studio 中的 [偵錯] 輸出視窗。</span><span class="sxs-lookup"><span data-stu-id="9fb74-170">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="9fb74-171">啟動服務之後，您應該會開始看到服務傳送「Application Insights 遙測」記錄的證據。</span><span class="sxs-lookup"><span data-stu-id="9fb74-171">After the service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="9fb74-172">開啟網頁瀏覽器，然後瀏覽至您的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="9fb74-172">Open a web browser and navigate go to your Application Insights resource.</span></span> <span data-ttu-id="9fb74-173">開啟 [搜尋] 索引標籤 (在預設的 [概觀] 刀鋒視窗頂端)。</span><span class="sxs-lookup"><span data-stu-id="9fb74-173">Open "Search" tab (at the top of the default "Overview" blade).</span></span> <span data-ttu-id="9fb74-174">在短暫延遲之後，您應該會開始在 Application Insights 入口網站中看到您的追蹤：</span><span class="sxs-lookup"><span data-stu-id="9fb74-174">After a short delay you should start seeing your traces in the Application Insights portal:</span></span>

![顯示來自 Service Fabric 應用程式之記錄檔的 Application Insights 入口網站][2]

## <a name="next-steps"></a><span data-ttu-id="9fb74-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9fb74-176">Next steps</span></span>
* [<span data-ttu-id="9fb74-177">深入了解診斷和監視 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="9fb74-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="9fb74-178">EventFlow 文件</span><span class="sxs-lookup"><span data-stu-id="9fb74-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
