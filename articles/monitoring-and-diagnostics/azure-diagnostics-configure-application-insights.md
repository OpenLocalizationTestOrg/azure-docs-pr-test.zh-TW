---
title: "aaaConfigure Azure 診斷 toosend 資料 tooApplication Insights |Microsoft 文件"
description: "更新 hello Azure 診斷公用組態 toosend 資料 tooApplication 深入資訊。"
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>傳送雲端服務、 虛擬機器或 Service Fabric 診斷資料 tooApplication Insights
雲端服務，虛擬機器、 虛擬機器擴展集和 Service Fabric 所有使用 hello Azure 診斷延伸 toocollect 資料。  Azure 診斷會傳送資料 tooAzure 儲存體資料表。  不過，您也可以所有管道或 hello 資料 tooother 位置使用 1.5 或更新版本的 Azure 診斷擴充功能的子集。

本文說明如何從 toosend 資料 hello Azure 診斷擴充功能 tooApplication 深入資訊。

## <a name="diagnostics-configuration-explained"></a>說明診斷組態
hello Azure 診斷延伸模組 1.5 導入接收，您可以在其中傳送診斷資料的其他位置。

Application Insights 的接收器組態範例：

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- hello**接收***名稱*屬性是可唯一識別 hello 接收一個字串值。

- hello **ApplicationInsights**項目會指定 hello hello Azure 診斷資料的傳送目標的 Application insights 資源的檢測金鑰。
    - 如果您沒有現有的 Application Insights 資源，請參閱[建立新的 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)如需有關建立資源，並取得 hello 檢測金鑰。
    - 如果您以 Azure SDK 2.8 和更新版本開發雲端服務，則會自動填入此檢測金鑰。 hello 值根據 hello **APPINSIGHTS_INSTRUMENTATIONKEY**封裝 hello 雲端服務專案時，服務組態設定。 請參閱[使用 Application Insights 使用 Azure 診斷 tootroubleshoot 雲端服務發出](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md)。

- hello**通道**元素包含一或多個**通道**項目。
    - hello*名稱*屬性唯一參考 toothat 通道。
    - hello *loglevel*屬性可讓您指定允許 hello 通道的 hello 記錄層級。 hello 可用記錄層級，依照順序最多 tooleast 資訊如下：
        - 詳細資訊
        - 資訊
        - 警告
        - 錯誤
        - 重要

通道的作用就像篩選器，並可讓您 tooselect 特定的記錄層級 toosend toohello 目標接收。 例如，您可以收集詳細的記錄檔和傳送它們 toostorage，但傳送錯誤 toohello 接收。

hello 下圖顯示此關聯性。

![診斷公用組態](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

下列圖形的 hello 摘要 hello 組態值，以及如何運作。 您可以包含多個接收 hello hello 階層中的不同層級的組態中。 在 hello 上層 hello 接收器做為全域設定，並 hello 指定其中一個在 hello 個別項目就像是覆寫 toothat 全域設定。

![診斷接收器組態和 Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>完整接收器組態範例
以下是完整的範例的 hello 公用組態檔
1. 傳送所有錯誤 tooApplication Insights (指定在 hello **DiagnosticMonitorConfiguration**節點)
2. 也會傳送 hello 應用程式記錄檔的詳細資訊層級的記錄檔 (在 hello 指定**記錄**節點)。

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
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
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
Hello 先前的設定，在下列幾行的 hello 會有 hello 下列意義：

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>傳送 Azure 診斷所收集的所有 hello 資料

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>傳送只錯誤記錄檔 toohello Application Insights 接收

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>傳送詳細資訊的應用程式記錄檔 tooApplication Insights

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>限制

- **通道只記錄類型，不記錄效能計數器。** 如果您在通道中指定效能計數器元素，將會忽略。
- **hello 通道的記錄層級不能超過 hello 的項目會由 Azure 診斷收集的記錄層級。** 例如，您無法收集 hello 記錄檔項目中的應用程式記錄檔錯誤，然後再次嘗試 toosend 詳細資訊記錄檔 toohello Application Insight 接收。 hello *scheduledTransferLogLevelFilter*屬性必須永遠收集相等或更多的記錄檔比 hello 記錄您正嘗試 toosend tooa 接收。
- **您無法傳送 Azure 診斷擴充功能 tooApplication Insights 所收集的 blob 資料。** 比方說，任何項目底下 hello 指定*目錄*節點。 損毀傾印 hello 實際損毀傾印傳送 tooblob 儲存體，並產生 hello 損毀傾印的通知會傳送 tooApplication 深入資訊。

## <a name="next-steps"></a>後續步驟
* 了解如何太[檢視您的 Azure 診斷資訊](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events)Application Insights 中。
* 使用[PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure 診斷擴充功能，您的應用程式。
* 使用[Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure 診斷擴充功能，您的應用程式
