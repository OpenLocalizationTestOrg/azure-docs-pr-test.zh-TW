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
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="f7aa4-103">傳送雲端服務、 虛擬機器或 Service Fabric 診斷資料 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="f7aa4-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="f7aa4-104">雲端服務，虛擬機器、 虛擬機器擴展集和 Service Fabric 所有使用 hello Azure 診斷延伸 toocollect 資料。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="f7aa4-105">Azure 診斷會傳送資料 tooAzure 儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="f7aa4-106">不過，您也可以所有管道或 hello 資料 tooother 位置使用 1.5 或更新版本的 Azure 診斷擴充功能的子集。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="f7aa4-107">本文說明如何從 toosend 資料 hello Azure 診斷擴充功能 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="f7aa4-108">說明診斷組態</span><span class="sxs-lookup"><span data-stu-id="f7aa4-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="f7aa4-109">hello Azure 診斷延伸模組 1.5 導入接收，您可以在其中傳送診斷資料的其他位置。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="f7aa4-110">Application Insights 的接收器組態範例：</span><span class="sxs-lookup"><span data-stu-id="f7aa4-110">Example configuration of a sink for Application Insights:</span></span>

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
- <span data-ttu-id="f7aa4-111">hello**接收***名稱*屬性是可唯一識別 hello 接收一個字串值。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="f7aa4-112">hello **ApplicationInsights**項目會指定 hello hello Azure 診斷資料的傳送目標的 Application insights 資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="f7aa4-113">如果您沒有現有的 Application Insights 資源，請參閱[建立新的 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)如需有關建立資源，並取得 hello 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="f7aa4-114">如果您以 Azure SDK 2.8 和更新版本開發雲端服務，則會自動填入此檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="f7aa4-115">hello 值根據 hello **APPINSIGHTS_INSTRUMENTATIONKEY**封裝 hello 雲端服務專案時，服務組態設定。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="f7aa4-116">請參閱[使用 Application Insights 使用 Azure 診斷 tootroubleshoot 雲端服務發出](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md)。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="f7aa4-117">hello**通道**元素包含一或多個**通道**項目。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="f7aa4-118">hello*名稱*屬性唯一參考 toothat 通道。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="f7aa4-119">hello *loglevel*屬性可讓您指定允許 hello 通道的 hello 記錄層級。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="f7aa4-120">hello 可用記錄層級，依照順序最多 tooleast 資訊如下：</span><span class="sxs-lookup"><span data-stu-id="f7aa4-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="f7aa4-121">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f7aa4-121">Verbose</span></span>
        - <span data-ttu-id="f7aa4-122">資訊</span><span class="sxs-lookup"><span data-stu-id="f7aa4-122">Information</span></span>
        - <span data-ttu-id="f7aa4-123">警告</span><span class="sxs-lookup"><span data-stu-id="f7aa4-123">Warning</span></span>
        - <span data-ttu-id="f7aa4-124">錯誤</span><span class="sxs-lookup"><span data-stu-id="f7aa4-124">Error</span></span>
        - <span data-ttu-id="f7aa4-125">重要</span><span class="sxs-lookup"><span data-stu-id="f7aa4-125">Critical</span></span>

<span data-ttu-id="f7aa4-126">通道的作用就像篩選器，並可讓您 tooselect 特定的記錄層級 toosend toohello 目標接收。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="f7aa4-127">例如，您可以收集詳細的記錄檔和傳送它們 toostorage，但傳送錯誤 toohello 接收。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="f7aa4-128">hello 下圖顯示此關聯性。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-128">hello following graphic shows this relationship.</span></span>

![診斷公用組態](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="f7aa4-130">下列圖形的 hello 摘要 hello 組態值，以及如何運作。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="f7aa4-131">您可以包含多個接收 hello hello 階層中的不同層級的組態中。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="f7aa4-132">在 hello 上層 hello 接收器做為全域設定，並 hello 指定其中一個在 hello 個別項目就像是覆寫 toothat 全域設定。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![診斷接收器組態和 Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="f7aa4-134">完整接收器組態範例</span><span class="sxs-lookup"><span data-stu-id="f7aa4-134">Complete sink configuration example</span></span>
<span data-ttu-id="f7aa4-135">以下是完整的範例的 hello 公用組態檔</span><span class="sxs-lookup"><span data-stu-id="f7aa4-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="f7aa4-136">傳送所有錯誤 tooApplication Insights (指定在 hello **DiagnosticMonitorConfiguration**節點)</span><span class="sxs-lookup"><span data-stu-id="f7aa4-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="f7aa4-137">也會傳送 hello 應用程式記錄檔的詳細資訊層級的記錄檔 (在 hello 指定**記錄**節點)。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

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
<span data-ttu-id="f7aa4-138">Hello 先前的設定，在下列幾行的 hello 會有 hello 下列意義：</span><span class="sxs-lookup"><span data-stu-id="f7aa4-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="f7aa4-139">傳送 Azure 診斷所收集的所有 hello 資料</span><span class="sxs-lookup"><span data-stu-id="f7aa4-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="f7aa4-140">傳送只錯誤記錄檔 toohello Application Insights 接收</span><span class="sxs-lookup"><span data-stu-id="f7aa4-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="f7aa4-141">傳送詳細資訊的應用程式記錄檔 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="f7aa4-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="f7aa4-142">限制</span><span class="sxs-lookup"><span data-stu-id="f7aa4-142">Limitations</span></span>

- <span data-ttu-id="f7aa4-143">**通道只記錄類型，不記錄效能計數器。**</span><span class="sxs-lookup"><span data-stu-id="f7aa4-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="f7aa4-144">如果您在通道中指定效能計數器元素，將會忽略。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="f7aa4-145">**hello 通道的記錄層級不能超過 hello 的項目會由 Azure 診斷收集的記錄層級。**</span><span class="sxs-lookup"><span data-stu-id="f7aa4-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="f7aa4-146">例如，您無法收集 hello 記錄檔項目中的應用程式記錄檔錯誤，然後再次嘗試 toosend 詳細資訊記錄檔 toohello Application Insight 接收。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="f7aa4-147">hello *scheduledTransferLogLevelFilter*屬性必須永遠收集相等或更多的記錄檔比 hello 記錄您正嘗試 toosend tooa 接收。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="f7aa4-148">**您無法傳送 Azure 診斷擴充功能 tooApplication Insights 所收集的 blob 資料。**</span><span class="sxs-lookup"><span data-stu-id="f7aa4-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="f7aa4-149">比方說，任何項目底下 hello 指定*目錄*節點。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="f7aa4-150">損毀傾印 hello 實際損毀傾印傳送 tooblob 儲存體，並產生 hello 損毀傾印的通知會傳送 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7aa4-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7aa4-151">Next Steps</span></span>
* <span data-ttu-id="f7aa4-152">了解如何太[檢視您的 Azure 診斷資訊](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events)Application Insights 中。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="f7aa4-153">使用[PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure 診斷擴充功能，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7aa4-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="f7aa4-154">使用[Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure 診斷擴充功能，您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f7aa4-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
