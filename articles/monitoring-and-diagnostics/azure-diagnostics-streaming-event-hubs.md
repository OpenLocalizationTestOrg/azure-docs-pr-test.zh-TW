---
title: "使用事件中心的 hello 最忙碌路徑中的 Azure 診斷資料 aaaStreaming |Microsoft 文件"
description: "設定 Azure 診斷使用事件中心結束 tooend，包括常見案例的指引。"
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a>使用事件中心的 hello 最忙碌路徑中的資料流 Azure 診斷資料
Azure 診斷功能提供彈性的方式可以 toocollect 度量資訊，並記錄從雲端服務的虛擬機器 (Vm)，然後傳送結果 tooAzure 儲存體。 Hello 年 3 月 2016 (SDK 2.9) 的時間範圍從開始，您可以傳送診斷 toocustom 資料來源和使用，以秒為單位傳送最忙碌路徑資料[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)。

支援的資料類型包括：

* Windows 事件追蹤 (ETW) 事件
* 效能計數器
* Windows 事件記錄檔
* 應用程式記錄檔
* Azure 診斷基礎結構記錄檔

本文章將示範如何從事件中心 tooconfigure Azure 診斷結束 tooend。 也提供下列常見的案例 hello 的指導方針：

* Toocustomize hello 的記錄檔和傳送 tooEvent 集線器的度量
* 如何在每個環境中的 toochange 組態
* Tooview 事件中心資料的串流
* 如何 tootroubleshoot hello 連線  

## <a name="prerequisites"></a>必要條件
事件中心 receieving 資料從 Azure 診斷的雲端服務、 Vm、 虛擬機器擴展集及啟動 Azure SDK 2.9 hello 和 hello 對應 Azure Tools for Visual Studio 中的 Service Fabric 支援。

* Azure 診斷擴充 1.6 ([Azure SDK for. NET 2.9 或更新版本](https://azure.microsoft.com/downloads/) 預設以此為目標)
* [Visual Studio 2013 或更新版本](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* Azure 診斷的應用程式使用中的現有組態*.wadcfgx*檔案以及其中一個 hello 下列方法：
  * Visual Studio： [為 Azure 雲端服務和虛擬機器設定診斷功能](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Windows PowerShell： [使用 PowerShell 在 Azure 雲端服務中啟用診斷](../cloud-services/cloud-services-diagnostics-powershell.md)
* 事件中樞命名空間佈建每個 hello 發行項，[事件中心快速入門](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a>連接 Azure 診斷 tooEvent 中心接收
根據預設，Azure 診斷一律會傳送記錄檔和度量 tooan Azure 儲存體帳戶。 應用程式可能還會傳送資料 tooEvent 中心透過新增**接收**下 hello 區段**PublicConfig** / **WadCfg** hello元素*.wadcfgx*檔案。 在 Visual Studio 中的 hello *.wadcfgx*檔案會儲存在下列路徑的 hello:**雲端服務專案** > **角色** > **(RoleName)** > **diagnostics.wadcfgx**檔案。

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

在此範例中，hello 事件中樞設定 URL，將 toohello 完整限定的 hello 事件中樞命名空間： 事件中樞命名空間 +"/"+ 事件中樞名稱。  

URL 會顯示在 hello hello 事件中心[Azure 入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)hello 事件中心儀表板上。  

hello **Sink**可以設定名稱 tooany 有效的字串，只要 hello 相同的值一致使用整個 hello 設定檔。

> [!NOTE]
> 此區段中可能有其他設定的接收，例如 *applicationInsights* 。 Azure 診斷可讓一或多個接收 toobe 定義每個接收也已經宣告在 hello **PrivateConfig** > 一節。  
>
>

hello 事件中心接收必須也要宣告和定義在 hello **PrivateConfig**區段 hello *.wadcfgx*組態檔。

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

hello`SharedAccessKeyName`值必須符合共用存取簽章 (SAS) 金鑰和 hello 中已定義的原則**事件中心**命名空間。 瀏覽 toohello 事件中心儀表板中 hello [Azure 入口網站](https://manage.windowsazure.com)，按一下 hello**設定**索引標籤，然後設定具名原則 (例如，"SendRule") 具有*傳送*權限。 hello **StorageAccount**也已經宣告在**PrivateConfig**。 無須 toochange 值如果其正常運作。 在此範例中，我們將保留 hello 值空白，這是下游的資產會設定 hello 值的正負號。 例如，hello *ServiceConfiguration.Cloud.cscfg*環境組態檔設定 hello 適當環境的名稱和金鑰。  

> [!WARNING]
> hello 事件中樞的 SAS 金鑰儲存在純文字格式 hello *.wadcfgx*檔案。 通常，此機碼已簽入 toosource 控制或是可從您的組建伺服器中的資產，因此您應該適當地保護。 我們建議您使用與此處的 SAS 金鑰*僅傳送*權限，讓惡意使用者可以寫入 toohello 事件中心，但不是接聽 tooit 或管理它。
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a>設定 Azure 診斷 toosend 記錄檔和度量 tooEvent 集線器
如前所述，所有的預設和自訂診斷資料，也就是標準和記錄檔，會自動傳送 tooAzure 儲存體以 hello 設定的間隔。 事件中樞與任何其他的接收，您可以指定 hello 階層 toobe 傳送 toohello 事件中樞的任何根或分葉節點。 這包括 ETW 事件、效能計數器、Windows 事件記錄檔和應用程式記錄檔。   

請務必的 tooconsider 多少資料點實際上應該傳送 tooEvent 集線器。 一般而言，開發人員會傳輸必須快速取用及解譯的低延遲忙碌路徑資料。 監視警示或自動調整規則的系統即是一例。 開發人員也會設定替代分析存放區或搜尋存放區；例如，Azure 串流分析、Elasticsearch、自訂監視系統，或最愛的他牌監視系統。

hello 下面是一些範例設定。

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

在上述範例中的 hello，hello 接收器是套用的 toohello 父**PerformanceCounters** hello 在階層中，這表示所有的子節點**PerformanceCounters**傳送 tooEvent 集線器。  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

Hello 前一個範例中的 hello 接收是套用的 tooonly 三個計數器：**要求排入佇列**，**要求遭到拒絕**，和**%Processor time**。  

hello 下列範例示範如何開發人員可以限制傳送的資料 toobe hello 重要度量資訊會用於此服務的健全狀況的 hello 數量。  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

在此範例中，hello 接收器是套用的 toologs，篩選僅 tooerror 層級的追蹤。

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>部署和更新雲端服務應用程式和診斷設定
Visual Studio 提供 hello 最簡單路徑 toodeploy hello 應用程式和事件中心接收設定。 tooview 和編輯 hello 檔案中，開啟 hello *.wadcfgx* Visual Studio 中的檔案、 加以編輯，然後將其儲存。 hello 路徑**雲端服務專案** > **角色** > **(RoleName)** > **diagnostics.wadcfgx**.  

此時，所有部署和部署都更新動作，在 Visual Studio、 Visual Studio Team System，和所有命令或指令碼，MSBuild 會根據，使用 hello **/t： 發行**目標包括 hello *.wadcfgx* hello 封裝程序中。 此外，部署和更新 hello 檔案 tooAzure 使用部署 hello 適當 Azure 診斷代理程式擴充功能在您的 Vm 上。

您部署 hello 應用程式與 Azure 診斷組態後，您會立即看到 hello hello 事件中樞的儀表板中的活動。 這表示您已準備好 toomove tooviewing hello 熱路徑中的資料 hello 接聽程式用戶端或分析工具的選擇。  

在下列圖 hello，hello 事件中心儀表板會顯示狀況良好傳送診斷資料 toohello 事件中樞一段時間之後開始晚上 11 點。 這是當 hello 應用程式部署與更新*.wadcfgx*檔案，然後 hello 接收的設定正確。

![][0]  

> [!NOTE]
> 當您進行更新 toohello Azure 診斷組態檔 (.wadcfgx) 時，建議使用 Visual Studio 發行或 Windows PowerShell 指令碼推送 hello 更新 toohello 整個應用程式，以及 hello 組態。  
>
>

## <a name="view-hot-path-data"></a>檢視忙碌路徑資料
如先前所討論，有許多接聽 tooand 處理事件中心資料的使用案例。

一個簡單的方法是 toocreate 小型測試主控台應用程式 toolisten toohello 事件中樞和列印 hello 輸出資料流。 您可以將下列程式碼，更詳細地說明 hello[開始使用事件中心](../event-hubs/event-hubs-csharp-ephcs-getstarted.md))，在主控台應用程式。  

請注意，hello 主控台應用程式必須包含 hello[事件處理器主機 NuGet 封裝](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)。  

請記得在角括號中 hello tooreplace hello 值**Main**函式，以您的資源的值。   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a>針對事件中樞接收進行疑難排解
* hello 事件中心不會顯示如預期般的內送或外寄事件活動。

    檢查已成功佈建您的事件中樞。 Hello 中的所有連接資訊**PrivateConfig**區段*.wadcfgx* hello 入口網站中所見，必須符合您的資源 hello 值。 請確定您有 SAS 原則定義 (在 hello 範例為"SendRule 」) hello 入口網站，而且*傳送*授與權限。  
* 更新之後，hello 事件中心不會再顯示內送或外寄事件 」 活動。

    首先，請確定 hello 事件中樞與組態資訊正確，如先前所述。 有時 hello **PrivateConfig**重設部署更新。 hello 建議的修正程式是的 toomake 過的所有變更*.wadcfgx*在 hello 專案，並再推送的完整應用程式更新。 如果不可行，請確定該 hello 診斷更新推播通知的完整**PrivateConfig**包含 hello SAS 金鑰。  
* 我已嘗試過 hello 建議和 hello 事件中心仍然無法運作。

    請試著查看在 hello Azure 儲存體資料表，其中包含本身的 Azure 診斷的記錄檔和錯誤： **WADDiagnosticInfrastructureLogsTable**。 其中一個選項是 toouse 工具，例如[Azure 儲存體總管](http://www.storageexplorer.com)tooconnect toothis 儲存體帳戶，來檢視此資料表，並加入查詢的時間戳記在 hello 過去 24 小時。 您可以使用 hello 工具 tooexport.csv 檔案，並開啟 Microsoft Excel 之類的應用程式。 Excel 就可輕鬆 toosearch 電話卡字串，例如**EventHubs**，toosee 報告哪些錯誤。  

## <a name="next-steps"></a>後續步驟
•    [深入了解事件中樞](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>附錄：完成 Azure 診斷組態檔 (.wadcfgx) 範例
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

hello 互補*ServiceConfiguration.Cloud.cscfg*針對此範例看起來像下列 hello。

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

虛擬機器上對等的 JSON 型設定如下所示：
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞概觀](../event-hubs/event-hubs-what-is-event-hubs.md)
* [建立事件中樞](../event-hubs/event-hubs-create.md)
* [事件中樞常見問題集](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
