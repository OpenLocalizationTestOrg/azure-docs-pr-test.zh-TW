---
title: "使用事件中樞串流最忙碌路徑中的 Azure 診斷資料 | Microsoft Docs"
description: "使用事件中樞設定 Azure 診斷的完整步驟，包括常見案例的指引。"
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
ms.openlocfilehash: 1c05bd6dc4c4d394aa043b9995de9c184e4f14c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a><span data-ttu-id="c2340-103">使用事件中樞串流最忙碌路徑中的 Azure 診斷資料</span><span class="sxs-lookup"><span data-stu-id="c2340-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span></span>
<span data-ttu-id="c2340-104">Azure 診斷會提供彈性的方法，用來收集來自雲端服務虛擬機器 (VM) 的度量和記錄檔，再將結果傳輸至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c2340-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span></span> <span data-ttu-id="c2340-105">從 2016 年 3 月 (SDK 2.9) 的時間範圍開始，您可以使用 [Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)，將 Azure 診斷傳送至自訂的資料來源，並立即傳輸最忙碌路徑資料。</span><span class="sxs-lookup"><span data-stu-id="c2340-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="c2340-106">支援的資料類型包括：</span><span class="sxs-lookup"><span data-stu-id="c2340-106">Supported data types include:</span></span>

* <span data-ttu-id="c2340-107">Windows 事件追蹤 (ETW) 事件</span><span class="sxs-lookup"><span data-stu-id="c2340-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="c2340-108">效能計數器</span><span class="sxs-lookup"><span data-stu-id="c2340-108">Performance counters</span></span>
* <span data-ttu-id="c2340-109">Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="c2340-109">Windows event logs</span></span>
* <span data-ttu-id="c2340-110">應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="c2340-110">Application logs</span></span>
* <span data-ttu-id="c2340-111">Azure 診斷基礎結構記錄檔</span><span class="sxs-lookup"><span data-stu-id="c2340-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="c2340-112">本文說明如何使用事件中樞從端對端設定 Azure 診斷。</span><span class="sxs-lookup"><span data-stu-id="c2340-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span></span> <span data-ttu-id="c2340-113">另提供以下常見案例的指引：</span><span class="sxs-lookup"><span data-stu-id="c2340-113">Guidance is also provided for the following common scenarios:</span></span>

* <span data-ttu-id="c2340-114">如何自訂傳送到事件中樞的記錄檔和計量</span><span class="sxs-lookup"><span data-stu-id="c2340-114">How to customize the logs and metrics that get sent to Event Hubs</span></span>
* <span data-ttu-id="c2340-115">如何變更每個環境中的組態</span><span class="sxs-lookup"><span data-stu-id="c2340-115">How to change configurations in each environment</span></span>
* <span data-ttu-id="c2340-116">如何檢視事件中樞串流資料</span><span class="sxs-lookup"><span data-stu-id="c2340-116">How to view Event Hubs stream data</span></span>
* <span data-ttu-id="c2340-117">如何針對連線問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="c2340-117">How to troubleshoot the connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c2340-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="c2340-118">Prerequisites</span></span>
<span data-ttu-id="c2340-119">雲端服務、VM、虛擬機器擴展集，以及 Azure SDK 2.9 開始的 Service Fabric 和對應的 Azure Tools for Visual Studio，皆支援從 Azure 診斷接收資料的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="c2340-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="c2340-120">Azure 診斷擴充 1.6 ([Azure SDK for. NET 2.9 或更新版本](https://azure.microsoft.com/downloads/) 預設以此為目標)</span><span class="sxs-lookup"><span data-stu-id="c2340-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="c2340-121">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="c2340-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="c2340-122">在應用程式中使用 *.wadcfgx* 檔案和以下任一方法的 Azure 診斷現有組態：</span><span class="sxs-lookup"><span data-stu-id="c2340-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span></span>
  * <span data-ttu-id="c2340-123">Visual Studio： [為 Azure 雲端服務和虛擬機器設定診斷功能](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="c2340-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="c2340-124">Windows PowerShell： [使用 PowerShell 在 Azure 雲端服務中啟用診斷](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c2340-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="c2340-125">文章中佈建的事件中樞命名空間，[開始使用事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="c2340-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a><span data-ttu-id="c2340-126">將 Azure 診斷連接至事件中樞接收</span><span class="sxs-lookup"><span data-stu-id="c2340-126">Connect Azure Diagnostics to Event Hubs sink</span></span>
<span data-ttu-id="c2340-127">根據預設，Azure 診斷一律會將記錄檔和計量傳送至 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c2340-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span></span> <span data-ttu-id="c2340-128">應用程式可能會將資料傳送至事件中樞，方法是將新的 [接收] 區段新增至 *.wadcfgx* 檔案的 **PublicConfig** / **WadCfg** 元素底下。</span><span class="sxs-lookup"><span data-stu-id="c2340-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span></span> <span data-ttu-id="c2340-129">在 Visual Studio 中，*.wadcfgx* 檔案會儲存在以下路徑：[雲端服務專案] > [角色] > **(RoleName)** > **diagnostics.wadcfgx** 檔案。</span><span class="sxs-lookup"><span data-stu-id="c2340-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="c2340-130">在此範例中，事件中樞 URL 設定為事件中樞的完整命名空間：事件中樞命名空間 + "/" + 事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="c2340-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="c2340-131">事件中樞 URL 會在 [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkID=213885) 中的 [事件中樞] 儀表板上顯示。</span><span class="sxs-lookup"><span data-stu-id="c2340-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span></span>  

<span data-ttu-id="c2340-132">[接收]  名稱可以設定為任何有效的字串，只要在整個組態檔一致使用相同的值即可。</span><span class="sxs-lookup"><span data-stu-id="c2340-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span></span>

> [!NOTE]
> <span data-ttu-id="c2340-133">此區段中可能有其他設定的接收，例如 *applicationInsights* 。</span><span class="sxs-lookup"><span data-stu-id="c2340-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="c2340-134">Azure 診斷可以定義一或多個接收，前提是每個接收也在 **PrivateConfig** 區段中宣告。</span><span class="sxs-lookup"><span data-stu-id="c2340-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="c2340-135">事件中樞接收也必須宣告並定義於 **.wadcfgx** 組態檔的 *PrivateConfig* 區段。</span><span class="sxs-lookup"><span data-stu-id="c2340-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="c2340-136">`SharedAccessKeyName` 值必須符合共用存取簽章 (SAS) 金鑰，以及**事件中樞**命名空間中已定義的原則。</span><span class="sxs-lookup"><span data-stu-id="c2340-136">The `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in the **Event Hubs** namespace.</span></span> <span data-ttu-id="c2340-137">在 [Azure 入口網站](https://manage.windowsazure.com)中瀏覽至 [事件中樞] 儀表板，按一下 [設定] 索引標籤，然後設定具有*傳送*權限的具名原則 (如 "SendRule")。</span><span class="sxs-lookup"><span data-stu-id="c2340-137">Browse to the Event Hubs dashboard in the [Azure portal](https://manage.windowsazure.com), click the **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="c2340-138">**StorageAccount** 也已經在 **PrivateConfig** 中宣告。</span><span class="sxs-lookup"><span data-stu-id="c2340-138">The **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="c2340-139">如果這裡的值可以運作，就不需要變更。</span><span class="sxs-lookup"><span data-stu-id="c2340-139">There is no need to change values here if they are working.</span></span> <span data-ttu-id="c2340-140">在此範例中，我們保留空白的值，這代表下游資產將會設定值。</span><span class="sxs-lookup"><span data-stu-id="c2340-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span></span> <span data-ttu-id="c2340-141">例如，*ServiceConfiguration.Cloud.cscfg* 環境組態檔會設定適合環境的名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="c2340-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="c2340-142">事件中樞 SAS 金鑰會以純文字儲存在 *.wadcfgx* 檔案中。</span><span class="sxs-lookup"><span data-stu-id="c2340-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span></span> <span data-ttu-id="c2340-143">有時候，系統會將該金鑰簽入原始程式碼控制，或做為組建伺服器中的資產提供，因此您應該適當地保護它。</span><span class="sxs-lookup"><span data-stu-id="c2340-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="c2340-144">建議您在這裡使用具有「僅限傳送」  權限的 SAS 金鑰，讓惡意使用者只能寫入事件中樞，而無法接聽或加以管理。</span><span class="sxs-lookup"><span data-stu-id="c2340-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a><span data-ttu-id="c2340-145">設定 Azure 診斷將記錄檔和計量傳送至事件中樞</span><span class="sxs-lookup"><span data-stu-id="c2340-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span></span>
<span data-ttu-id="c2340-146">如前文所述，所有預設和自訂診斷資料 (亦即，計量和記錄檔) 會以設定的間隔自動傳送到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c2340-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span></span> <span data-ttu-id="c2340-147">您可以藉由事件中樞和任何其他接收，指定要傳送至事件中樞的階層中任何根節點或分葉節點。</span><span class="sxs-lookup"><span data-stu-id="c2340-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span></span> <span data-ttu-id="c2340-148">這包括 ETW 事件、效能計數器、Windows 事件記錄檔和應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c2340-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="c2340-149">請務必考慮實際上應該將多少資料點傳輸至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="c2340-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span></span> <span data-ttu-id="c2340-150">一般而言，開發人員會傳輸必須快速取用及解譯的低延遲忙碌路徑資料。</span><span class="sxs-lookup"><span data-stu-id="c2340-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="c2340-151">監視警示或自動調整規則的系統即是一例。</span><span class="sxs-lookup"><span data-stu-id="c2340-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="c2340-152">開發人員也會設定替代分析存放區或搜尋存放區；例如，Azure 串流分析、Elasticsearch、自訂監視系統，或最愛的他牌監視系統。</span><span class="sxs-lookup"><span data-stu-id="c2340-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="c2340-153">以下是一些範例組態。</span><span class="sxs-lookup"><span data-stu-id="c2340-153">The following are some example configurations.</span></span>

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

<span data-ttu-id="c2340-154">在上述範例中，接收會套用至階層中的父 **PerformanceCounters**，這表示所有子 **PerformanceCounters** 將傳送至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="c2340-154">In the above example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span></span>  

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

<span data-ttu-id="c2340-155">在上述範例中，接收只會套用至三個計數器︰**已排入佇列的要求**、**遭拒絕的要求**和 **% 處理器時間**。</span><span class="sxs-lookup"><span data-stu-id="c2340-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="c2340-156">下列範例示範開發人員如何將傳送的資料量，限制為用於此服務之健全狀況的關鍵度量。</span><span class="sxs-lookup"><span data-stu-id="c2340-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="c2340-157">在此範例中，接收會套用至記錄檔，並且只篩選為「錯誤」層級追蹤。</span><span class="sxs-lookup"><span data-stu-id="c2340-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="c2340-158">部署和更新雲端服務應用程式和診斷設定</span><span class="sxs-lookup"><span data-stu-id="c2340-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="c2340-159">Visual Studio 提供最簡單的路徑供您部署應用程式和事件中樞接收組態。</span><span class="sxs-lookup"><span data-stu-id="c2340-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span></span> <span data-ttu-id="c2340-160">若要檢視及編輯檔案，請在 Visual Studio 中開啟 *.wadcfgx* 檔案，然後再加以編輯和儲存。</span><span class="sxs-lookup"><span data-stu-id="c2340-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="c2340-161">其路徑為 [雲端服務專案] > [角色] > (RoleName) > diagnostics.wadcfgx。</span><span class="sxs-lookup"><span data-stu-id="c2340-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="c2340-162">此時，Visual Studio、Visual Studio Team System 中的所有部署和部署更新動作，以及所有根據 MSBuild 和使用 **/t:publish** 目標的命令或指令碼，都會在封裝程序中納入 *.wadcfgx* 。</span><span class="sxs-lookup"><span data-stu-id="c2340-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span></span> <span data-ttu-id="c2340-163">此外，部署和更新會使用 VM 上適當的 Azure 診斷代理程式擴充功能將檔案部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="c2340-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="c2340-164">在部署應用程式和 Azure 診斷組態後，您會立即在事件中樞的儀表板中看到活動。</span><span class="sxs-lookup"><span data-stu-id="c2340-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span></span> <span data-ttu-id="c2340-165">這表示您已準備就緒，可以繼續在接聽程式用戶端或所選的分析工具中檢視最忙碌路徑資料。</span><span class="sxs-lookup"><span data-stu-id="c2340-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="c2340-166">在下圖中，事件中樞儀表板會顯示從晚上 11 點之後開始傳送到事件中樞，而且狀況良好的診斷資料傳送作業。</span><span class="sxs-lookup"><span data-stu-id="c2340-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="c2340-167">也就是使用更新的 *.wadcfgx* 檔案部署應用程式，而且已正確設定接收的時候。</span><span class="sxs-lookup"><span data-stu-id="c2340-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="c2340-168">當您更新 Azure Diagnostics 組態檔 (.wadcfgx) 時，建議您透過使用 Visual Studio 發行或 Windows PowerShell 指令碼，將更新推送至整個應用程式以及組態。</span><span class="sxs-lookup"><span data-stu-id="c2340-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="c2340-169">檢視忙碌路徑資料</span><span class="sxs-lookup"><span data-stu-id="c2340-169">View hot-path data</span></span>
<span data-ttu-id="c2340-170">如前文所述，接聽和處理事件中樞資料有許多使用案例。</span><span class="sxs-lookup"><span data-stu-id="c2340-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span></span>

<span data-ttu-id="c2340-171">一個簡單的作法是建立小型測試主控台應用程式，接聽事件中樞並列印輸出串流。</span><span class="sxs-lookup"><span data-stu-id="c2340-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span></span> <span data-ttu-id="c2340-172">您可以將下列程式碼 (會在[開始使用事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)中詳細說明) 放置在主控台應用程式中。</span><span class="sxs-lookup"><span data-stu-id="c2340-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="c2340-173">請注意，主控台應用程式必須包含 [Event Processor Host NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)。</span><span class="sxs-lookup"><span data-stu-id="c2340-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="c2340-174">請記得使用您資源的值取代 **Main** 函式中角括弧裡面的值。</span><span class="sxs-lookup"><span data-stu-id="c2340-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span></span>   

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

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="c2340-175">針對事件中樞接收進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="c2340-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="c2340-176">事件中樞不會如預期般顯示傳入或傳出事件活動。</span><span class="sxs-lookup"><span data-stu-id="c2340-176">The event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="c2340-177">檢查已成功佈建您的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="c2340-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="c2340-178">**.wadcfgx** 中 *PrivateConfig* 區段的所有連接資訊必須符合在入口網站中所示的資源的值。</span><span class="sxs-lookup"><span data-stu-id="c2340-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span></span> <span data-ttu-id="c2340-179">請確定您已在入口網站中定義 SAS 原則 (此範例中為 “SendRule”)，並且對其授與「傳送」  權限。</span><span class="sxs-lookup"><span data-stu-id="c2340-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="c2340-180">執行更新之後，事件中樞不會再顯示傳入或傳出事件活動。</span><span class="sxs-lookup"><span data-stu-id="c2340-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="c2340-181">首先，請確定事件中樞和組態資訊正確，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="c2340-181">First, make sure that the event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="c2340-182">有時候，系統會在部署更新時重設 **PrivateConfig** 。</span><span class="sxs-lookup"><span data-stu-id="c2340-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="c2340-183">建議的修正方式是對專案中的 *.wadcfgx* 進行所有變更，然後再推送完整的應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="c2340-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span></span> <span data-ttu-id="c2340-184">如果不可行，請確定診斷更新推送完整的 **PrivateConfig** ，包括 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c2340-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span></span>  
* <span data-ttu-id="c2340-185">我試過上述建議，不過事件中樞仍然無法運作。</span><span class="sxs-lookup"><span data-stu-id="c2340-185">I tried the suggestions, and the event hub is still not working.</span></span>

    <span data-ttu-id="c2340-186">請嘗試查看 Azure 儲存體資料表，其中包含記錄檔和 Azure 診斷本身的錯誤︰ **WADDiagnosticInfrastructureLogsTable**。</span><span class="sxs-lookup"><span data-stu-id="c2340-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="c2340-187">其中一個選項是使用類似 [Azure 儲存體總管](http://www.storageexplorer.com) 的工具連接到此儲存體帳戶、檢視此資料表，並且新增過去 24 小時內時間戳記的查詢。</span><span class="sxs-lookup"><span data-stu-id="c2340-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span></span> <span data-ttu-id="c2340-188">您可以使用此工具來匯出 .csv 檔案，並在 Microsoft Excel 之類的應用程式中開啟。</span><span class="sxs-lookup"><span data-stu-id="c2340-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="c2340-189">Excel 能輕鬆地搜尋電話卡字串 (如 **EventHubs**)，以便查看系統回報了哪些錯誤。</span><span class="sxs-lookup"><span data-stu-id="c2340-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c2340-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2340-190">Next steps</span></span>
<span data-ttu-id="c2340-191">•    [深入了解事件中樞](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="c2340-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="c2340-192">附錄：完成 Azure 診斷組態檔 (.wadcfgx) 範例</span><span class="sxs-lookup"><span data-stu-id="c2340-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="c2340-193">此範例的補充 *ServiceConfiguration.Cloud.cscfg* 如下所示。</span><span class="sxs-lookup"><span data-stu-id="c2340-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span></span>

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

<span data-ttu-id="c2340-194">虛擬機器上對等的 JSON 型設定如下所示：</span><span class="sxs-lookup"><span data-stu-id="c2340-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="c2340-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2340-195">Next steps</span></span>
<span data-ttu-id="c2340-196">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="c2340-196">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="c2340-197">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="c2340-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="c2340-198">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="c2340-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="c2340-199">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="c2340-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
