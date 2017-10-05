---
title: "設定 Azure 診斷以將資料傳送至 Application Insights | Microsoft Docs"
description: "更新 Azure 診斷公用組態以傳送資料至 Application Insights。"
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
ms.openlocfilehash: 67dc2d5bbfa2012e4e098616edda593d023c4c1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="7c73f-103">將雲端服務、虛擬機器或 Service Fabric 診斷資料傳送至 Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c73f-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="7c73f-104">雲端服務、虛擬機器、虛擬機器擴展集和 Service Fabric 全都使用 Azure 診斷擴充功能來收集資料。</span><span class="sxs-lookup"><span data-stu-id="7c73f-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="7c73f-105">Azure 診斷會將資料傳送至 Azure 儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="7c73f-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="7c73f-106">不過，您也可以使用 Azure 診斷擴充功能 1.5 或更新版本，將所有資料或一部分資料傳送至其他位置。</span><span class="sxs-lookup"><span data-stu-id="7c73f-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="7c73f-107">本文說明如何將資料從 Azure 診斷擴充功能傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="7c73f-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="7c73f-108">說明診斷組態</span><span class="sxs-lookup"><span data-stu-id="7c73f-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="7c73f-109">Azure 診斷擴充功能 1.5 引進接收器，這些是可供您傳送診斷資料的其他位置。</span><span class="sxs-lookup"><span data-stu-id="7c73f-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="7c73f-110">Application Insights 的接收器組態範例：</span><span class="sxs-lookup"><span data-stu-id="7c73f-110">Example configuration of a sink for Application Insights:</span></span>

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
- <span data-ttu-id="7c73f-111">**Sink** name 屬性是可唯一識別接收器的字串值。</span><span class="sxs-lookup"><span data-stu-id="7c73f-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="7c73f-112">**ApplicationInsights** 元素指定 Azure 診斷資料送出的 Application Insights 資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="7c73f-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="7c73f-113">如果您沒有現有的 Application Insights 資源，請參閱[建立新的 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)，以取得建立資源及取得檢測金鑰的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7c73f-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="7c73f-114">如果您以 Azure SDK 2.8 和更新版本開發雲端服務，則會自動填入此檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="7c73f-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="7c73f-115">這個值是根據封裝雲端服務專案時的 **APPINSIGHTS_INSTRUMENTATIONKEY** 服務組態設定。</span><span class="sxs-lookup"><span data-stu-id="7c73f-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="7c73f-116">請參閱[使用 Application Insights 搭配 Azure 診斷來針對雲端服務問題進行疑難排解](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md)。</span><span class="sxs-lookup"><span data-stu-id="7c73f-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="7c73f-117">**Channels** 元素包含一個或多個 **Channel** 元素。</span><span class="sxs-lookup"><span data-stu-id="7c73f-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="7c73f-118">name屬性可唯一參考該通道。</span><span class="sxs-lookup"><span data-stu-id="7c73f-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="7c73f-119">loglevel  屬性可讓您指定通道允許的記錄等級。</span><span class="sxs-lookup"><span data-stu-id="7c73f-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="7c73f-120">可用的記錄等級從最多到最少資訊依序為：</span><span class="sxs-lookup"><span data-stu-id="7c73f-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="7c73f-121">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="7c73f-121">Verbose</span></span>
        - <span data-ttu-id="7c73f-122">資訊</span><span class="sxs-lookup"><span data-stu-id="7c73f-122">Information</span></span>
        - <span data-ttu-id="7c73f-123">警告</span><span class="sxs-lookup"><span data-stu-id="7c73f-123">Warning</span></span>
        - <span data-ttu-id="7c73f-124">錯誤</span><span class="sxs-lookup"><span data-stu-id="7c73f-124">Error</span></span>
        - <span data-ttu-id="7c73f-125">重要</span><span class="sxs-lookup"><span data-stu-id="7c73f-125">Critical</span></span>

<span data-ttu-id="7c73f-126">通道就像篩選條件，可讓您選取要傳送至目標接收器的特定記錄等級。</span><span class="sxs-lookup"><span data-stu-id="7c73f-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="7c73f-127">例如，您可以收集詳細記錄，將它們傳送至儲存體，但只將「錯誤」傳送至接收器。</span><span class="sxs-lookup"><span data-stu-id="7c73f-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="7c73f-128">下圖顯示此關聯性。</span><span class="sxs-lookup"><span data-stu-id="7c73f-128">The following graphic shows this relationship.</span></span>

![診斷公用組態](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="7c73f-130">下圖摘要說明設定值及其運作方式。</span><span class="sxs-lookup"><span data-stu-id="7c73f-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="7c73f-131">您可以在組態中的不同階層等級中包含多個接收器。</span><span class="sxs-lookup"><span data-stu-id="7c73f-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="7c73f-132">在最上層指定的接收器會成為全域設定，而在個別元素指定的接收器就形同覆寫該全域設定。</span><span class="sxs-lookup"><span data-stu-id="7c73f-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![診斷接收器組態和 Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="7c73f-134">完整接收器組態範例</span><span class="sxs-lookup"><span data-stu-id="7c73f-134">Complete sink configuration example</span></span>
<span data-ttu-id="7c73f-135">以下是完整的公用組態檔範例，可以</span><span class="sxs-lookup"><span data-stu-id="7c73f-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="7c73f-136">將所有錯誤傳送至 Application Insights (在 **DiagnosticMonitorConfiguration** 節點上指定)</span><span class="sxs-lookup"><span data-stu-id="7c73f-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="7c73f-137">也會傳送應用程式記錄 (在 **Logs** 節點上指定) 的「詳細資訊」等級記錄。</span><span class="sxs-lookup"><span data-stu-id="7c73f-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
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
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
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
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
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
<span data-ttu-id="7c73f-138">在先前的組態中，下列幾行的意義如下︰</span><span class="sxs-lookup"><span data-stu-id="7c73f-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="7c73f-139">傳送 Azure 診斷收集的所有資料</span><span class="sxs-lookup"><span data-stu-id="7c73f-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="7c73f-140">只將錯誤資料傳送至 Application Insights 接收器</span><span class="sxs-lookup"><span data-stu-id="7c73f-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="7c73f-141">將「詳細資訊」應用程式記錄傳送至 Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c73f-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="7c73f-142">限制</span><span class="sxs-lookup"><span data-stu-id="7c73f-142">Limitations</span></span>

- <span data-ttu-id="7c73f-143">**通道只記錄類型，不記錄效能計數器。**</span><span class="sxs-lookup"><span data-stu-id="7c73f-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="7c73f-144">如果您在通道中指定效能計數器元素，將會忽略。</span><span class="sxs-lookup"><span data-stu-id="7c73f-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="7c73f-145">**通道的記錄等級不能超過 Azure 診斷收集的記錄等級。**</span><span class="sxs-lookup"><span data-stu-id="7c73f-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="7c73f-146">例如，您不能在 Logs 元素中收集「應用程式記錄」錯誤，也無法嘗試將「詳細資訊」記錄傳送至 Application Insight 接收器。</span><span class="sxs-lookup"><span data-stu-id="7c73f-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="7c73f-147">*ScheduledTransferLogLevelFilter* 屬性一律必須收集與您正嘗試傳送到接收器的記錄相等或更多個記錄。</span><span class="sxs-lookup"><span data-stu-id="7c73f-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="7c73f-148">**您無法將 Azure 診斷擴充功能收集的 blob 資料傳送至 Application Insights。**</span><span class="sxs-lookup"><span data-stu-id="7c73f-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="7c73f-149">例如，Directories 節點下指定的任何項目。</span><span class="sxs-lookup"><span data-stu-id="7c73f-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="7c73f-150">針對損毀傾印，實際損毀傾印會傳送至 blob 儲存體，並只會將損毀傾印所產生的通知傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="7c73f-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c73f-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7c73f-151">Next Steps</span></span>
* <span data-ttu-id="7c73f-152">了解如何在 Application Insights 中[檢視您的 Azure 診斷資訊](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events)。</span><span class="sxs-lookup"><span data-stu-id="7c73f-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="7c73f-153">使用 [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) 來為您的應用程式啟用 Azure 診斷擴充。</span><span class="sxs-lookup"><span data-stu-id="7c73f-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="7c73f-154">使用 [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 來為您的應用程式啟用 Azure 診斷擴充</span><span class="sxs-lookup"><span data-stu-id="7c73f-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>
