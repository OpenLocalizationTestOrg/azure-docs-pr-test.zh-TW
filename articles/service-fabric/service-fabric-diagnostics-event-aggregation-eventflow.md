---
title: "使用 EventFlow 的 Azure Service Fabric 事件彙總 | Microsoft Docs"
description: "深入了解使用 EventFlow 的彙總及收集事件，監視和診斷 Azure Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 90d26a77b749e70de3a7d910f15820653e2ef39b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="c9ab3-103">使用 EventFlow 的事件彙總與集合</span><span class="sxs-lookup"><span data-stu-id="c9ab3-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="c9ab3-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) 可以將節點的事件路由傳送至一個或多個監視目的地。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node to one or more monitoring destinations.</span></span> <span data-ttu-id="c9ab3-105">由於是以 NuGet 套件形式加入服務專案中，EventFlow 程式碼和組態會隨著服務一起傳送，不會發生稍後提及有關 Azure 診斷的個別節點組態問題。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with the service, eliminating the per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="c9ab3-106">EventFlow 在您的服務處理序中執行，並直接連線到已設定的輸出。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-106">EventFlow runs within your service process, and connects directly to the configured outputs.</span></span> <span data-ttu-id="c9ab3-107">因為是直接連線，所以 EventFlow 適用於 Azure、容器和內部部署的服務部署。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-107">Because of the direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="c9ab3-108">如果您在高密度情況下執行 EventFlow，例如在容器中，請務必小心，因為每個 EventFlow 管線來建立外部連線。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="c9ab3-109">所以，如果您裝載許多處理序，就會產生大量輸出連線！</span><span class="sxs-lookup"><span data-stu-id="c9ab3-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="c9ab3-110">這對 Service Fabric 應用程式來說不會有什麼問題，因為 `ServiceType` 的所有複本都在同一處理序中執行，這會限制輸出連線的數量。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in the same process, and this limits the number of outbound connections.</span></span> <span data-ttu-id="c9ab3-111">EventFlow 也提供事件篩選，因此只會傳送符合指定篩選的事件。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-111">EventFlow also offers event filtering, so that only the events that match the specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="c9ab3-112">設定 EventFlow</span><span class="sxs-lookup"><span data-stu-id="c9ab3-112">Setting up EventFlow</span></span>

<span data-ttu-id="c9ab3-113">EventFlow 二進位檔是以一組 NuGet 套件的形式提供。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="c9ab3-114">若要將 EventFlow 新增到 Service Fabric 服務專案，請在 [方案總管] 中該專案上按一下滑鼠右鍵，然後選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-114">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="c9ab3-115">切換到 [瀏覽] 索引標籤，然後搜尋 "`Diagnostics.EventFlow`"：</span><span class="sxs-lookup"><span data-stu-id="c9ab3-115">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet 套件管理員 UI 中的 EventFlow NuGet 套件](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="c9ab3-117">您會看到一份各種各樣套件的清單，標記為「輸入」和「輸出」。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="c9ab3-118">EventFlow 支援各種不同的記錄提供者和分析器。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="c9ab3-119">視應用程式記錄檔的來源和目的地而定，裝載 EventFlow 的服務應該包含適當的套件。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-119">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="c9ab3-120">除了核心 ServiceFabric 套件，您還需要設定至少一個輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-120">In addition to the core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="c9ab3-121">例如，您可以新增下列套件，將 EventSource 事件傳送至 Application Insights：</span><span class="sxs-lookup"><span data-stu-id="c9ab3-121">For exmaple, you can add the following packages to sent EventSource events to Application Insights:</span></span>

* <span data-ttu-id="c9ab3-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` 從服務的 EventSource 類別以及從標準 EventSources (例如 *Microsoft-ServiceFabric-Services* 和 *Microsoft-ServiceFabric-Actors*) 擷取資料</span><span class="sxs-lookup"><span data-stu-id="c9ab3-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="c9ab3-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (我們將把記錄檔傳送給 Azure Application Insights 資源)</span><span class="sxs-lookup"><span data-stu-id="c9ab3-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going to send the logs to an Azure Application Insights resource)</span></span>
* <span data-ttu-id="c9ab3-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric` (允許從 Service Fabric 服務設定將 EventFlow 管線初始化，並以 Service Fabric 健康情況報告的形式傳送診斷資料來回報任何問題)</span><span class="sxs-lookup"><span data-stu-id="c9ab3-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="c9ab3-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` 套件會要求服務專案的目標必須是 .NET Framework 4.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="c9ab3-126">安裝此套件之前，請先確定您已在專案屬性中設定適當的目標架構。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-126">Make sure you set the appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="c9ab3-127">安裝好所有套件之後，下一個步驟就是設定及啟用服務中的 EventFlow。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-127">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="c9ab3-128">設定及啟用記錄檔收集</span><span class="sxs-lookup"><span data-stu-id="c9ab3-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="c9ab3-129">EventFlow 管線 (負責傳送記錄檔) 是從儲存在組態檔中的規格建立的。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-129">The EventFlow pipeline responsible for sending the logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="c9ab3-130">`Microsoft.Diagnostics.EventFlow.ServiceFabric` 套件會在 `PackageRoot\Config` 方案資料夾底下安裝一個起始的 EventFlow 組態檔，名為 `eventFlowConfig.json`。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-130">The `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="c9ab3-131">此組態檔必須經過修改，才能從預設服務 `EventSource` 類別和任何其他您想設定的輸入擷取資料，然後將資料傳送到適當的位置。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-131">This configuration file needs to be modified to capture data from the default service `EventSource` class, and any other inputs you want to configure, and send data to the appropriate place.</span></span>

<span data-ttu-id="c9ab3-132">以下是以前述 NuGet 套件為基礎的範例 *eventFlowConfig.json*：</span><span class="sxs-lookup"><span data-stu-id="c9ab3-132">Here is a sample *eventFlowConfig.json* based on the NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="c9ab3-133">服務的 ServiceEventSource 名稱是套用至 ServiceEventSource 類別之 `EventSourceAttribute` 的 Name 屬性值。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-133">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="c9ab3-134">全部都在 `ServiceEventSource.cs` 檔案中指定，此檔案是服務程式碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-134">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="c9ab3-135">例如，在下列程式碼片段中，ServiceEventSource 的名稱是 *MyCompany-Application1-Stateless1*：</span><span class="sxs-lookup"><span data-stu-id="c9ab3-135">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="c9ab3-136">請注意，`eventFlowConfig.json` 檔案是服務組態封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="c9ab3-137">對此檔案所做的變更可以包含在完整或僅限組態的服務升級中，並受到 Service Fabric 升級健康情況檢查和自動復原 (如果發生升級失敗) 控管。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-137">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="c9ab3-138">如需詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="c9ab3-139">組態的「篩選」區段可讓您進一步自訂經過 EventFlow 管線到輸出的資訊，讓您卸除或包含特定資訊，或變更事件資料結構。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-139">The *filters* section of the config allows you to further customize the information that is going to go through the EventFlow pipeline to the outputs, allowing you to drop or include certain information, or change the structure of the event data.</span></span> <span data-ttu-id="c9ab3-140">如需有關篩選的詳細資訊，請參閱 [EventFlow 篩選](https://github.com/Azure/diagnostics-eventflow#filters)。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="c9ab3-141">最後一個步驟是在服務的啟動程式碼 (位於 `Program.cs` 檔案中) 中將 EventFlow 管線具現化：</span><span class="sxs-lookup"><span data-stu-id="c9ab3-141">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="c9ab3-142">當作 `ServiceFabricDiagnosticsPipelineFactory` 之 `CreatePipeline` 方法的參數來傳遞的名稱是「健康情況實體」的名稱，此實體代表 EventFlow 記錄檔收集管線。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-142">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="c9ab3-143">當 EventFlow 發生錯誤並透過 Service Fabric 健康情況子系統回報錯誤時，就會使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-143">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-to-in-eventflowconfig"></a><span data-ttu-id="c9ab3-144">在 eventFlowConfig 中使用 Service Fabric 設定和應用程式參數</span><span class="sxs-lookup"><span data-stu-id="c9ab3-144">Using Service Fabric settings and application parameters to in eventFlowConfig</span></span>

<span data-ttu-id="c9ab3-145">EventFlow 支援使用 Service Fabric 設定和應用程式參數來設定 EventFlow 設定。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-145">EventFlow supports using Service Fabric settings and application paremeters to configure EventFlow settings.</span></span> <span data-ttu-id="c9ab3-146">您可以參考使用這個特殊的語法值的 Service Fabric 設定參數：</span><span class="sxs-lookup"><span data-stu-id="c9ab3-146">You can refer to Service Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="c9ab3-147">`<section-name>` 是Service Fabric 組態區段的名稱，`<setting-name>` 是提供設定 EventFlow 設定所用值的組態設定。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-147">`<section-name>` is the name of the Service Fabric configuration section, and `<setting-name>` is the configuration setting providing the value that will be used to configure an EventFlow setting.</span></span> <span data-ttu-id="c9ab3-148">若要深入了解如何作業，請移至 [Service Fabric 設定和應用程式參數的支援](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters)。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-148">To read more about how to do this, go to [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="c9ab3-149">驗證</span><span class="sxs-lookup"><span data-stu-id="c9ab3-149">Verification</span></span>

<span data-ttu-id="c9ab3-150">啟動您的服務並觀察 Visual Studio 中的 [偵錯] 輸出視窗。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-150">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="c9ab3-151">啟動服務之後，您應該會開始看到服務在向您設定的輸出傳送記錄。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-151">After the service is started, you should start seeing evidence that your service is sending records to the output that you have configured.</span></span> <span data-ttu-id="c9ab3-152">瀏覽至您的事件分析和視覺化平台，確認記錄檔已開始顯示 (可能需要幾分鐘的時間)。</span><span class="sxs-lookup"><span data-stu-id="c9ab3-152">Navigate to your event analysis and visualization platform and confirm that logs have started to show up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9ab3-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9ab3-153">Next steps</span></span>

* [<span data-ttu-id="c9ab3-154">使用 Application Insights 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="c9ab3-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="c9ab3-155">使用 OMS 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="c9ab3-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="c9ab3-156">EventFlow 文件</span><span class="sxs-lookup"><span data-stu-id="c9ab3-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)