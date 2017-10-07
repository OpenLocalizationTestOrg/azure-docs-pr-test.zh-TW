---
title: "服務網狀架構事件彙總與 EventFlow aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="2d490-103">使用 EventFlow 的事件彙總與集合</span><span class="sxs-lookup"><span data-stu-id="2d490-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="2d490-104">[Microsoft 診斷 EventFlow](https://github.com/Azure/diagnostics-eventflow)可以路由傳送來自節點 tooone 或多個監視的目的地事件。</span><span class="sxs-lookup"><span data-stu-id="2d490-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="2d490-105">因為它包含您的服務專案中的 NuGet 套件的形式，所以 EventFlow 程式碼和組態周遊 hello 服務時，排除先前所述，Azure 診斷的相關 hello 每個節點組態問題。</span><span class="sxs-lookup"><span data-stu-id="2d490-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="2d490-106">EventFlow 服務程序中執行，並直接連接 toohello 設定輸出。</span><span class="sxs-lookup"><span data-stu-id="2d490-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="2d490-107">Hello 直接連線，因為 EventFlow 適用於 Azure、 容器和內部部署服務部署。</span><span class="sxs-lookup"><span data-stu-id="2d490-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="2d490-108">如果您在高密度情況下執行 EventFlow，例如在容器中，請務必小心，因為每個 EventFlow 管線來建立外部連線。</span><span class="sxs-lookup"><span data-stu-id="2d490-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="2d490-109">所以，如果您裝載許多處理序，就會產生大量輸出連線！</span><span class="sxs-lookup"><span data-stu-id="2d490-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="2d490-110">這不是 Service Fabric 應用程式，最多的問題，因為所有複本的`ServiceType`執行 hello 中相同的處理序，而且這會限制 hello 的傳出連線數目。</span><span class="sxs-lookup"><span data-stu-id="2d490-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="2d490-111">EventFlow 也提供事件篩選，以便符合指定篩選條件 hello hello 事件將會傳送。</span><span class="sxs-lookup"><span data-stu-id="2d490-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="2d490-112">設定 EventFlow</span><span class="sxs-lookup"><span data-stu-id="2d490-112">Setting up EventFlow</span></span>

<span data-ttu-id="2d490-113">EventFlow 二進位檔是以一組 NuGet 套件的形式提供。</span><span class="sxs-lookup"><span data-stu-id="2d490-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="2d490-114">tooadd EventFlow tooa Service Fabric 服務專案中，hello 方案總管 中的 hello 專案上按一下滑鼠右鍵，然後選擇 「 管理 NuGet 套件 」。</span><span class="sxs-lookup"><span data-stu-id="2d490-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="2d490-115">切換 toohello [瀏覽] 索引標籤，並搜尋"`Diagnostics.EventFlow`」:</span><span class="sxs-lookup"><span data-stu-id="2d490-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet 套件管理員 UI 中的 EventFlow NuGet 套件](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="2d490-117">您會看到一份各種各樣套件的清單，標記為「輸入」和「輸出」。</span><span class="sxs-lookup"><span data-stu-id="2d490-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="2d490-118">EventFlow 支援各種不同的記錄提供者和分析器。</span><span class="sxs-lookup"><span data-stu-id="2d490-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="2d490-119">hello 服務裝載 EventFlow 應該包含適當的封裝，根據 hello 來源和目的地 hello 應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2d490-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="2d490-120">此外 toohello 核心 ServiceFabric 封裝，您也必須至少一個輸入和輸出設定。</span><span class="sxs-lookup"><span data-stu-id="2d490-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="2d490-121">為 pester.cat，您可以加入下列封裝 toosent EventSource 事件 tooApplication Insights hello:</span><span class="sxs-lookup"><span data-stu-id="2d490-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="2d490-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture 資料從 hello 服務 EventSource 類別，以及從這類的標準 EventSources *Microsoft ServiceFabric 服務*和*Microsoft-ServiceFabric 演員*)</span><span class="sxs-lookup"><span data-stu-id="2d490-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="2d490-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`（我們 toosend hello 記錄 tooan Azure Application Insights 資源）</span><span class="sxs-lookup"><span data-stu-id="2d490-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="2d490-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`（可讓 hello EventFlow 管線就會從 Service Fabric 服務組態的初始化和報告與 Service Fabric 健康情況報告的形式傳送診斷資料的任何問題）</span><span class="sxs-lookup"><span data-stu-id="2d490-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="2d490-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`封裝需要 hello 服務專案 tootarget.NET Framework 4.6 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2d490-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="2d490-126">請確定您在專案屬性中設定 hello 適當的目標 framework 之前安裝此套件。</span><span class="sxs-lookup"><span data-stu-id="2d490-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="2d490-127">在所有 hello 已安裝的套件，hello 下一個步驟是 tooconfigure 和啟用 EventFlow hello 服務中。</span><span class="sxs-lookup"><span data-stu-id="2d490-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="2d490-128">設定及啟用記錄檔收集</span><span class="sxs-lookup"><span data-stu-id="2d490-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="2d490-129">儲存在組態檔中的規格來建立 hello EventFlow 管線負責傳送嗨記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2d490-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="2d490-130">hello`Microsoft.Diagnostics.EventFlow.ServiceFabric`套件會安裝在起始 EventFlow 組態檔`PackageRoot\Config`方案資料夾中，名為`eventFlowConfig.json`。</span><span class="sxs-lookup"><span data-stu-id="2d490-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="2d490-131">此組態檔必須 hello 預設服務的修改 toobe toocapture 資料`EventSource`類別，而任何其他輸入您想 tooconfigure，並將傳送資料 toohello 適當位置。</span><span class="sxs-lookup"><span data-stu-id="2d490-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="2d490-132">以下是範例*eventFlowConfig.json*根據上面所述的 hello NuGet 封裝：</span><span class="sxs-lookup"><span data-stu-id="2d490-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="2d490-133">服務的 ServiceEventSource hello 名稱是 hello hello hello 名稱屬性值`EventSourceAttribute`套用 toohello ServiceEventSource 類別。</span><span class="sxs-lookup"><span data-stu-id="2d490-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="2d490-134">它內指定 all hello`ServiceEventSource.cs`屬於 hello 服務程式碼的檔案。</span><span class="sxs-lookup"><span data-stu-id="2d490-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="2d490-135">例如，在 hello hello ServiceEventSource 的下列程式碼片段 hello 名稱是*MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="2d490-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="2d490-136">請注意，`eventFlowConfig.json` 檔案是服務組態封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="2d490-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="2d490-137">變更 toothis 檔案可以包含在完整或組態-僅限 hello 服務的升級，則主體 tooService 網狀架構升級健全狀況檢查和自動回復升級失敗時。</span><span class="sxs-lookup"><span data-stu-id="2d490-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="2d490-138">如需詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="2d490-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="2d490-139">hello*篩選*hello 組態區段可讓您 toofurther 自訂 hello 資訊是透過 hello EventFlow 管線 toohello 輸出，可讓您 toodrop 進行 toogo 或包含特定資訊，或變更 hellohello 事件資料的結構。</span><span class="sxs-lookup"><span data-stu-id="2d490-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="2d490-140">如需有關篩選的詳細資訊，請參閱 [EventFlow 篩選](https://github.com/Azure/diagnostics-eventflow#filters)。</span><span class="sxs-lookup"><span data-stu-id="2d490-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="2d490-141">hello 最後一個步驟是在服務的啟動程式碼，位於 tooinstantiate EventFlow 管線`Program.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="2d490-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="2d490-142">hello 名稱傳遞為 hello hello 參數`CreatePipeline`方法 hello `ServiceFabricDiagnosticsPipelineFactory` hello hello 名稱*健全狀況實體*代表 hello EventFlow 記錄集合管線。</span><span class="sxs-lookup"><span data-stu-id="2d490-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="2d490-143">如果 EventFlow 遇到，會使用這個名稱和錯誤，並報告透過 hello 服務網狀架構健全狀況子系統。</span><span class="sxs-lookup"><span data-stu-id="2d490-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="2d490-144">使用 Service Fabric 設定和應用程式參數 tooin eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="2d490-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="2d490-145">使用 Service Fabric 設定和應用程式設定的參數 tooconfigure EventFlow 設定 EventFlow 支援。</span><span class="sxs-lookup"><span data-stu-id="2d490-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="2d490-146">您可以參考 tooService 網狀架構設定參數值中使用這個特殊的語法：</span><span class="sxs-lookup"><span data-stu-id="2d490-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="2d490-147">`<section-name>`hello hello Service Fabric 組態區段中，名稱和`<setting-name>`是 hello 提供 hello 值將會使用的 tooconfigure EventFlow 設定的組態設定。</span><span class="sxs-lookup"><span data-stu-id="2d490-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="2d490-148">深入了解如何 tooread toodo，請移過[服務網狀架構設定和應用程式參數的支援](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters)。</span><span class="sxs-lookup"><span data-stu-id="2d490-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="2d490-149">驗證</span><span class="sxs-lookup"><span data-stu-id="2d490-149">Verification</span></span>

<span data-ttu-id="2d490-150">啟動您的服務，並觀察 hello 偵錯 Visual Studio 中的 [輸出] 視窗。</span><span class="sxs-lookup"><span data-stu-id="2d490-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="2d490-151">Hello 服務啟動之後，您應該會開始看到您的服務傳送的辨識項會記錄已設定的 toohello 輸出。</span><span class="sxs-lookup"><span data-stu-id="2d490-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="2d490-152">瀏覽 tooyour 事件分析和視覺效果平台，並確認記錄已經啟動 tooshow 向上 （可能需要幾分鐘的時間）。</span><span class="sxs-lookup"><span data-stu-id="2d490-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d490-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d490-153">Next steps</span></span>

* [<span data-ttu-id="2d490-154">使用 Application Insights 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="2d490-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="2d490-155">使用 OMS 進行事件分析和視覺效果</span><span class="sxs-lookup"><span data-stu-id="2d490-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="2d490-156">EventFlow 文件</span><span class="sxs-lookup"><span data-stu-id="2d490-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)