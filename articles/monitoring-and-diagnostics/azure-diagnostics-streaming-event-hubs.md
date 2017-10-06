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
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="248aa-103">使用事件中心的 hello 最忙碌路徑中的資料流 Azure 診斷資料</span><span class="sxs-lookup"><span data-stu-id="248aa-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="248aa-104">Azure 診斷功能提供彈性的方式可以 toocollect 度量資訊，並記錄從雲端服務的虛擬機器 (Vm)，然後傳送結果 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="248aa-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="248aa-105">Hello 年 3 月 2016 (SDK 2.9) 的時間範圍從開始，您可以傳送診斷 toocustom 資料來源和使用，以秒為單位傳送最忙碌路徑資料[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="248aa-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="248aa-106">支援的資料類型包括：</span><span class="sxs-lookup"><span data-stu-id="248aa-106">Supported data types include:</span></span>

* <span data-ttu-id="248aa-107">Windows 事件追蹤 (ETW) 事件</span><span class="sxs-lookup"><span data-stu-id="248aa-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="248aa-108">效能計數器</span><span class="sxs-lookup"><span data-stu-id="248aa-108">Performance counters</span></span>
* <span data-ttu-id="248aa-109">Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="248aa-109">Windows event logs</span></span>
* <span data-ttu-id="248aa-110">應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="248aa-110">Application logs</span></span>
* <span data-ttu-id="248aa-111">Azure 診斷基礎結構記錄檔</span><span class="sxs-lookup"><span data-stu-id="248aa-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="248aa-112">本文章將示範如何從事件中心 tooconfigure Azure 診斷結束 tooend。</span><span class="sxs-lookup"><span data-stu-id="248aa-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="248aa-113">也提供下列常見的案例 hello 的指導方針：</span><span class="sxs-lookup"><span data-stu-id="248aa-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="248aa-114">Toocustomize hello 的記錄檔和傳送 tooEvent 集線器的度量</span><span class="sxs-lookup"><span data-stu-id="248aa-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="248aa-115">如何在每個環境中的 toochange 組態</span><span class="sxs-lookup"><span data-stu-id="248aa-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="248aa-116">Tooview 事件中心資料的串流</span><span class="sxs-lookup"><span data-stu-id="248aa-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="248aa-117">如何 tootroubleshoot hello 連線</span><span class="sxs-lookup"><span data-stu-id="248aa-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="248aa-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="248aa-118">Prerequisites</span></span>
<span data-ttu-id="248aa-119">事件中心 receieving 資料從 Azure 診斷的雲端服務、 Vm、 虛擬機器擴展集及啟動 Azure SDK 2.9 hello 和 hello 對應 Azure Tools for Visual Studio 中的 Service Fabric 支援。</span><span class="sxs-lookup"><span data-stu-id="248aa-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="248aa-120">Azure 診斷擴充 1.6 ([Azure SDK for. NET 2.9 或更新版本](https://azure.microsoft.com/downloads/) 預設以此為目標)</span><span class="sxs-lookup"><span data-stu-id="248aa-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="248aa-121">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="248aa-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="248aa-122">Azure 診斷的應用程式使用中的現有組態*.wadcfgx*檔案以及其中一個 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="248aa-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="248aa-123">Visual Studio： [為 Azure 雲端服務和虛擬機器設定診斷功能](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="248aa-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="248aa-124">Windows PowerShell： [使用 PowerShell 在 Azure 雲端服務中啟用診斷](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="248aa-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="248aa-125">事件中樞命名空間佈建每個 hello 發行項，[事件中心快速入門](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="248aa-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="248aa-126">連接 Azure 診斷 tooEvent 中心接收</span><span class="sxs-lookup"><span data-stu-id="248aa-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="248aa-127">根據預設，Azure 診斷一律會傳送記錄檔和度量 tooan Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="248aa-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="248aa-128">應用程式可能還會傳送資料 tooEvent 中心透過新增**接收**下 hello 區段**PublicConfig** / **WadCfg** hello元素*.wadcfgx*檔案。</span><span class="sxs-lookup"><span data-stu-id="248aa-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="248aa-129">在 Visual Studio 中的 hello *.wadcfgx*檔案會儲存在下列路徑的 hello:**雲端服務專案** > **角色** > **(RoleName)** > **diagnostics.wadcfgx**檔案。</span><span class="sxs-lookup"><span data-stu-id="248aa-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="248aa-130">在此範例中，hello 事件中樞設定 URL，將 toohello 完整限定的 hello 事件中樞命名空間： 事件中樞命名空間 +"/"+ 事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="248aa-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="248aa-131">URL 會顯示在 hello hello 事件中心[Azure 入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)hello 事件中心儀表板上。</span><span class="sxs-lookup"><span data-stu-id="248aa-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="248aa-132">hello **Sink**可以設定名稱 tooany 有效的字串，只要 hello 相同的值一致使用整個 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="248aa-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="248aa-133">此區段中可能有其他設定的接收，例如 *applicationInsights* 。</span><span class="sxs-lookup"><span data-stu-id="248aa-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="248aa-134">Azure 診斷可讓一或多個接收 toobe 定義每個接收也已經宣告在 hello **PrivateConfig** > 一節。</span><span class="sxs-lookup"><span data-stu-id="248aa-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="248aa-135">hello 事件中心接收必須也要宣告和定義在 hello **PrivateConfig**區段 hello *.wadcfgx*組態檔。</span><span class="sxs-lookup"><span data-stu-id="248aa-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="248aa-136">hello`SharedAccessKeyName`值必須符合共用存取簽章 (SAS) 金鑰和 hello 中已定義的原則**事件中心**命名空間。</span><span class="sxs-lookup"><span data-stu-id="248aa-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="248aa-137">瀏覽 toohello 事件中心儀表板中 hello [Azure 入口網站](https://manage.windowsazure.com)，按一下 hello**設定**索引標籤，然後設定具名原則 (例如，"SendRule") 具有*傳送*權限。</span><span class="sxs-lookup"><span data-stu-id="248aa-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="248aa-138">hello **StorageAccount**也已經宣告在**PrivateConfig**。</span><span class="sxs-lookup"><span data-stu-id="248aa-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="248aa-139">無須 toochange 值如果其正常運作。</span><span class="sxs-lookup"><span data-stu-id="248aa-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="248aa-140">在此範例中，我們將保留 hello 值空白，這是下游的資產會設定 hello 值的正負號。</span><span class="sxs-lookup"><span data-stu-id="248aa-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="248aa-141">例如，hello *ServiceConfiguration.Cloud.cscfg*環境組態檔設定 hello 適當環境的名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="248aa-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="248aa-142">hello 事件中樞的 SAS 金鑰儲存在純文字格式 hello *.wadcfgx*檔案。</span><span class="sxs-lookup"><span data-stu-id="248aa-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="248aa-143">通常，此機碼已簽入 toosource 控制或是可從您的組建伺服器中的資產，因此您應該適當地保護。</span><span class="sxs-lookup"><span data-stu-id="248aa-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="248aa-144">我們建議您使用與此處的 SAS 金鑰*僅傳送*權限，讓惡意使用者可以寫入 toohello 事件中心，但不是接聽 tooit 或管理它。</span><span class="sxs-lookup"><span data-stu-id="248aa-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="248aa-145">設定 Azure 診斷 toosend 記錄檔和度量 tooEvent 集線器</span><span class="sxs-lookup"><span data-stu-id="248aa-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="248aa-146">如前所述，所有的預設和自訂診斷資料，也就是標準和記錄檔，會自動傳送 tooAzure 儲存體以 hello 設定的間隔。</span><span class="sxs-lookup"><span data-stu-id="248aa-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="248aa-147">事件中樞與任何其他的接收，您可以指定 hello 階層 toobe 傳送 toohello 事件中樞的任何根或分葉節點。</span><span class="sxs-lookup"><span data-stu-id="248aa-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="248aa-148">這包括 ETW 事件、效能計數器、Windows 事件記錄檔和應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="248aa-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="248aa-149">請務必的 tooconsider 多少資料點實際上應該傳送 tooEvent 集線器。</span><span class="sxs-lookup"><span data-stu-id="248aa-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="248aa-150">一般而言，開發人員會傳輸必須快速取用及解譯的低延遲忙碌路徑資料。</span><span class="sxs-lookup"><span data-stu-id="248aa-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="248aa-151">監視警示或自動調整規則的系統即是一例。</span><span class="sxs-lookup"><span data-stu-id="248aa-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="248aa-152">開發人員也會設定替代分析存放區或搜尋存放區；例如，Azure 串流分析、Elasticsearch、自訂監視系統，或最愛的他牌監視系統。</span><span class="sxs-lookup"><span data-stu-id="248aa-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="248aa-153">hello 下面是一些範例設定。</span><span class="sxs-lookup"><span data-stu-id="248aa-153">hello following are some example configurations.</span></span>

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

<span data-ttu-id="248aa-154">在上述範例中的 hello，hello 接收器是套用的 toohello 父**PerformanceCounters** hello 在階層中，這表示所有的子節點**PerformanceCounters**傳送 tooEvent 集線器。</span><span class="sxs-lookup"><span data-stu-id="248aa-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

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

<span data-ttu-id="248aa-155">Hello 前一個範例中的 hello 接收是套用的 tooonly 三個計數器：**要求排入佇列**，**要求遭到拒絕**，和**%Processor time**。</span><span class="sxs-lookup"><span data-stu-id="248aa-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="248aa-156">hello 下列範例示範如何開發人員可以限制傳送的資料 toobe hello 重要度量資訊會用於此服務的健全狀況的 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="248aa-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="248aa-157">在此範例中，hello 接收器是套用的 toologs，篩選僅 tooerror 層級的追蹤。</span><span class="sxs-lookup"><span data-stu-id="248aa-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="248aa-158">部署和更新雲端服務應用程式和診斷設定</span><span class="sxs-lookup"><span data-stu-id="248aa-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="248aa-159">Visual Studio 提供 hello 最簡單路徑 toodeploy hello 應用程式和事件中心接收設定。</span><span class="sxs-lookup"><span data-stu-id="248aa-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="248aa-160">tooview 和編輯 hello 檔案中，開啟 hello *.wadcfgx* Visual Studio 中的檔案、 加以編輯，然後將其儲存。</span><span class="sxs-lookup"><span data-stu-id="248aa-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="248aa-161">hello 路徑**雲端服務專案** > **角色** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="248aa-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="248aa-162">此時，所有部署和部署都更新動作，在 Visual Studio、 Visual Studio Team System，和所有命令或指令碼，MSBuild 會根據，使用 hello **/t： 發行**目標包括 hello *.wadcfgx* hello 封裝程序中。</span><span class="sxs-lookup"><span data-stu-id="248aa-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="248aa-163">此外，部署和更新 hello 檔案 tooAzure 使用部署 hello 適當 Azure 診斷代理程式擴充功能在您的 Vm 上。</span><span class="sxs-lookup"><span data-stu-id="248aa-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="248aa-164">您部署 hello 應用程式與 Azure 診斷組態後，您會立即看到 hello hello 事件中樞的儀表板中的活動。</span><span class="sxs-lookup"><span data-stu-id="248aa-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="248aa-165">這表示您已準備好 toomove tooviewing hello 熱路徑中的資料 hello 接聽程式用戶端或分析工具的選擇。</span><span class="sxs-lookup"><span data-stu-id="248aa-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="248aa-166">在下列圖 hello，hello 事件中心儀表板會顯示狀況良好傳送診斷資料 toohello 事件中樞一段時間之後開始晚上 11 點。</span><span class="sxs-lookup"><span data-stu-id="248aa-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="248aa-167">這是當 hello 應用程式部署與更新*.wadcfgx*檔案，然後 hello 接收的設定正確。</span><span class="sxs-lookup"><span data-stu-id="248aa-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="248aa-168">當您進行更新 toohello Azure 診斷組態檔 (.wadcfgx) 時，建議使用 Visual Studio 發行或 Windows PowerShell 指令碼推送 hello 更新 toohello 整個應用程式，以及 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="248aa-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="248aa-169">檢視忙碌路徑資料</span><span class="sxs-lookup"><span data-stu-id="248aa-169">View hot-path data</span></span>
<span data-ttu-id="248aa-170">如先前所討論，有許多接聽 tooand 處理事件中心資料的使用案例。</span><span class="sxs-lookup"><span data-stu-id="248aa-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="248aa-171">一個簡單的方法是 toocreate 小型測試主控台應用程式 toolisten toohello 事件中樞和列印 hello 輸出資料流。</span><span class="sxs-lookup"><span data-stu-id="248aa-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="248aa-172">您可以將下列程式碼，更詳細地說明 hello[開始使用事件中心](../event-hubs/event-hubs-csharp-ephcs-getstarted.md))，在主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="248aa-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="248aa-173">請注意，hello 主控台應用程式必須包含 hello[事件處理器主機 NuGet 封裝](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)。</span><span class="sxs-lookup"><span data-stu-id="248aa-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="248aa-174">請記得在角括號中 hello tooreplace hello 值**Main**函式，以您的資源的值。</span><span class="sxs-lookup"><span data-stu-id="248aa-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

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

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="248aa-175">針對事件中樞接收進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="248aa-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="248aa-176">hello 事件中心不會顯示如預期般的內送或外寄事件活動。</span><span class="sxs-lookup"><span data-stu-id="248aa-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="248aa-177">檢查已成功佈建您的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="248aa-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="248aa-178">Hello 中的所有連接資訊**PrivateConfig**區段*.wadcfgx* hello 入口網站中所見，必須符合您的資源 hello 值。</span><span class="sxs-lookup"><span data-stu-id="248aa-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="248aa-179">請確定您有 SAS 原則定義 (在 hello 範例為"SendRule 」) hello 入口網站，而且*傳送*授與權限。</span><span class="sxs-lookup"><span data-stu-id="248aa-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="248aa-180">更新之後，hello 事件中心不會再顯示內送或外寄事件 」 活動。</span><span class="sxs-lookup"><span data-stu-id="248aa-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="248aa-181">首先，請確定 hello 事件中樞與組態資訊正確，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="248aa-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="248aa-182">有時 hello **PrivateConfig**重設部署更新。</span><span class="sxs-lookup"><span data-stu-id="248aa-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="248aa-183">hello 建議的修正程式是的 toomake 過的所有變更*.wadcfgx*在 hello 專案，並再推送的完整應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="248aa-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="248aa-184">如果不可行，請確定該 hello 診斷更新推播通知的完整**PrivateConfig**包含 hello SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="248aa-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="248aa-185">我已嘗試過 hello 建議和 hello 事件中心仍然無法運作。</span><span class="sxs-lookup"><span data-stu-id="248aa-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="248aa-186">請試著查看在 hello Azure 儲存體資料表，其中包含本身的 Azure 診斷的記錄檔和錯誤： **WADDiagnosticInfrastructureLogsTable**。</span><span class="sxs-lookup"><span data-stu-id="248aa-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="248aa-187">其中一個選項是 toouse 工具，例如[Azure 儲存體總管](http://www.storageexplorer.com)tooconnect toothis 儲存體帳戶，來檢視此資料表，並加入查詢的時間戳記在 hello 過去 24 小時。</span><span class="sxs-lookup"><span data-stu-id="248aa-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="248aa-188">您可以使用 hello 工具 tooexport.csv 檔案，並開啟 Microsoft Excel 之類的應用程式。</span><span class="sxs-lookup"><span data-stu-id="248aa-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="248aa-189">Excel 就可輕鬆 toosearch 電話卡字串，例如**EventHubs**，toosee 報告哪些錯誤。</span><span class="sxs-lookup"><span data-stu-id="248aa-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="248aa-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="248aa-190">Next steps</span></span>
<span data-ttu-id="248aa-191">•    [深入了解事件中樞](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="248aa-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="248aa-192">附錄：完成 Azure 診斷組態檔 (.wadcfgx) 範例</span><span class="sxs-lookup"><span data-stu-id="248aa-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="248aa-193">hello 互補*ServiceConfiguration.Cloud.cscfg*針對此範例看起來像下列 hello。</span><span class="sxs-lookup"><span data-stu-id="248aa-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

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

<span data-ttu-id="248aa-194">虛擬機器上對等的 JSON 型設定如下所示：</span><span class="sxs-lookup"><span data-stu-id="248aa-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="248aa-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="248aa-195">Next steps</span></span>
<span data-ttu-id="248aa-196">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="248aa-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="248aa-197">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="248aa-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="248aa-198">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="248aa-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="248aa-199">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="248aa-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
