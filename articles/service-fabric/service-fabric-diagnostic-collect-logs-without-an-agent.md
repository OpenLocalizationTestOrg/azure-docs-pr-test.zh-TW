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
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a>直接從 Azure Service Fabric 服務處理程序收集記錄檔
## <a name="in-process-log-collection"></a>同處理序記錄檔收集
使用收集應用程式記錄檔[Azure 診斷擴充功能](service-fabric-diagnostics-how-to-setup-wad.md)是個不錯的選擇**Azure Service Fabric**服務如果 hello 的記錄檔來源和目的地是很小，不會變更通常也那里是 hello 來源與目的地之間的直接對應。 如果沒有，另一個方法是 toohave 服務傳送其記錄檔直接 tooa 中央位置。 此處理程序稱為「同處理序記錄檔收集」，其中提供數個潛在的優點：

* *輕鬆設定及部署*

    * 診斷資料收集的 hello 組態只是 hello 服務組態的一部分。 它是簡單 tooalways 保持其 「 同步 」 以 hello 其餘部分的 hello 應用程式。
    * 輕鬆就可達成個別應用程式或個別服務的組態。
        * 代理程式為基礎的記錄檔集合，通常需要不同的部署和 hello 診斷代理程式的設定，這是額外的管理工作和錯誤的潛在來源。 通常是允許每個虛擬機器 （節點） 的 hello 代理程式只有一個執行個體和所有應用程式和該節點上執行的服務之間共用 hello 代理程式設定。 

* *彈性*
   
    * hello 應用程式可以傳送 hello 資料每當需要 toogo，只要用戶端程式庫支援 hello 目標資料儲存系統。 您可以視需要新增新的目的地。
    * 可以實作複雜的擷取、篩選和資料彙總規則。
    * 代理程式為基礎的記錄檔集合通常會受限於 hello 代理程式支援的 hello 資料接收器。 有些代理程式是可擴充的。

* *存取 toointernal 應用程式資料和內容*
   
    * hello hello 應用程式/服務處理序內執行的診斷子系統可以輕鬆地擴大 hello 與內容資訊的追蹤。
    * 代理程式為基礎的記錄檔集合與 hello 必須傳送資料 tooan 代理程式，透過某種處理序間通訊機制，例如 Windows 事件追蹤。 此機制可能會造成額外的限制。

它也可能 toocombine 這兩個集合的方法而獲益。 事實上，它可能 hello 對於許多應用程式的最佳解決方案。 代理程式為基礎的集合是用來收集記錄檔相關的 toohello 整個叢集和個別叢集節點的自然解決方案。 這是更可靠的方式，比同處理序記錄檔收集、 toodiagnose 服務啟動問題和當機。 此外，Service Fabric 叢集內執行的許多服務，以執行它自己的處理序記錄檔收集每個服務會導致從 hello 叢集中的多個傳出連線。 Hello 網路子系統和 hello 記錄目的地，會消耗大量的連出連線。 [**Azure 診斷**](../cloud-services/cloud-services-dotnet-diagnostics.md)之類的代理程式可以從多個服務收集資料，然後透過幾條連線傳送所有資料，藉此改善輸送量。 

在本文中，我們會示範 tooset 向上同處理序記錄的集合使用[ **EventFlow 開放原始碼程式庫**](https://github.com/Azure/diagnostics-eventflow)。 可能使用其他程式庫 hello 相同目的，但 EventFlow 具有 hello 優點需要同處理序記錄檔收集和 toosupport Service Fabric 服務專用的設計。 我們使用[ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/)做為 hello 記錄目的地。 其他像是[**事件中樞**](https://azure.microsoft.com/services/event-hubs/)或 [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) 也都是支援的目的地。 它是只安裝適當的 NuGet 封裝和設定 hello 目的地 hello EventFlow 組態檔中的問題。 如需有關 Application Insights 以外之記錄檔目的地的詳細資訊，請參閱 [EventFlow 文件](https://github.com/Azure/diagnostics-eventflow)。

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a>加入 EventFlow 庫 tooa Service Fabric 服務專案
EventFlow 二進位檔是以一組 NuGet 套件的形式提供。 tooadd EventFlow tooa Service Fabric 服務專案中，hello 方案總管 中的 hello 專案上按一下滑鼠右鍵，然後選擇 「 管理 NuGet 套件 」。 切換 toohello [瀏覽] 索引標籤，並搜尋"`Diagnostics.EventFlow`」:

![Visual Studio NuGet 套件管理員 UI 中的 EventFlow NuGet 套件][1]

hello 服務裝載 EventFlow 應該包含適當的封裝，根據 hello 來源和目的地 hello 應用程式記錄檔。 新增下列封裝的 hello: 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * (從 hello 服務 EventSource 類別，以及從這類的標準 EventSources toocapture 資料*Microsoft ServiceFabric 服務*和*Microsoft-ServiceFabric 演員*)
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * （我們 toosend hello 記錄 tooan Azure Application Insights 資源）  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * （可讓 hello EventFlow 管線就會從 Service Fabric 服務組態的初始化和報告與 Service Fabric 健康情況報告的形式傳送診斷資料的任何問題）

> [!NOTE]
> `Microsoft.Diagnostics.EventFlow.Inputs.EventSource`封裝需要 hello 服務專案 tootarget.NET Framework 4.6 或更新版本。 請確定您在專案屬性中設定 hello 適當的目標 framework 之前安裝此套件。 

在所有 hello 已安裝的套件，hello 下一個步驟是 tooconfigure 和啟用 EventFlow hello 服務中。

## <a name="configuring-and-enabling-log-collection"></a>設定及啟用記錄檔收集
EventFlow 管線，負責傳送嗨記錄檔，會建立從儲存在組態檔中的規格。 `Microsoft.Diagnostics.EventFlow.ServiceFabric` 套件會在 `PackageRoot\Config` 方案資料夾底下安裝一個起始的 EventFlow 組態檔。 hello 檔案名稱為`eventFlowConfig.json`。 此組態檔必須 hello 預設服務的修改 toobe toocapture 資料`EventSource`類別，並傳送資料 tooApplication Insights 服務。

> [!NOTE]
> 我們假設您已熟悉**Azure Application Insights**服務，而且您擁有您規劃 toouse toomonitor Service Fabric 服務的 Application Insights 資源。 如需詳細資訊，請參閱[建立 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。

開啟 hello `eventFlowConfig.json` hello 編輯器中的檔案，並變更其內容，如下所示。 請確定 tooreplace hello ServiceEventSource 名稱並根據 toocomments Application Insights 檢測金鑰。 

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
> 服務的 ServiceEventSource hello 名稱是 hello hello hello 名稱屬性值`EventSourceAttribute`套用 toohello ServiceEventSource 類別。 它內指定 all hello`ServiceEventSource.cs`屬於 hello 服務程式碼的檔案。 例如，在 hello hello ServiceEventSource 的下列程式碼片段 hello 名稱是*MyCompany-Application1-Stateless1*:
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

請注意，`eventFlowConfig.json` 檔案是服務組態封裝的一部分。 變更 toothis 檔案可以包含在完整或組態-僅限 hello 服務的升級，則主體 tooService 網狀架構升級健全狀況檢查和自動回復升級失敗時。 如需詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。

hello 最後一個步驟是在服務的啟動程式碼，位於 tooinstantiate EventFlow 管線`Program.cs`檔案。 在 hello 新增下列範例 EventFlow 相關項目都以註解的開頭標示`****`:

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

hello 名稱傳遞為 hello hello 參數`CreatePipeline`方法 hello `ServiceFabricDiagnosticsPipelineFactory` hello hello 名稱*健全狀況實體*代表 hello EventFlow 記錄集合管線。 如果 EventFlow 遇到，會使用這個名稱和錯誤，並報告透過 hello 服務網狀架構健全狀況子系統。

## <a name="verification"></a>驗證
啟動您的服務，並觀察 hello 偵錯 Visual Studio 中的 [輸出] 視窗。 Hello 服務啟動之後，您應該會開始看到您的服務將 「 Application Insights 遙測 」 資料錄的辨識項。 開啟網頁瀏覽器並瀏覽移 tooyour Application Insights 資源。 開啟 「 搜尋 」 索引標籤 （在 hello hello 預設 「 概觀 」 刀鋒視窗頂端）。 您應該在短暫延遲之後會開始看到您在 hello Application Insights 入口網站中的追蹤：

![顯示來自 Service Fabric 應用程式之記錄檔的 Application Insights 入口網站][2]

## <a name="next-steps"></a>後續步驟
* [深入了解診斷和監視 Service Fabric 服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [EventFlow 文件](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
