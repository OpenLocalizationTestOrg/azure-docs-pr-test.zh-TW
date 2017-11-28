---
title: "服務網狀架構事件彙總使用 Linux Azure 診斷 aaaAzure |Microsoft 文件"
description: "了解如何使用 LAD 彙總及收集事件，來監視和診斷 Azure Service Fabric 叢集。"
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a><span data-ttu-id="57261-103">使用 Linux Azure 診斷的事件彙總和收集</span><span class="sxs-lookup"><span data-stu-id="57261-103">Event aggregation and collection using Linux Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57261-104">Windows</span><span class="sxs-lookup"><span data-stu-id="57261-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="57261-105">Linux</span><span class="sxs-lookup"><span data-stu-id="57261-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="57261-106">執行 Azure Service Fabric 叢集時，它是個不錯的主意 toocollect hello 記錄檔儲存在集中位置的所有 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="57261-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="57261-107">在中央位置擁有 hello 記錄檔可協助您分析和疑難排解問題在叢集中或在 hello 應用程式和服務在該叢集中執行的問題。</span><span class="sxs-lookup"><span data-stu-id="57261-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="57261-108">其中一種方式 tooupload 及收集記錄檔是 toouse hello Linux Azure 診斷 （年輕人） 延伸，其中上傳記錄檔 tooAzure 存放裝置，而且也 hello 選項 toosend 記錄 tooAzure Application Insights 或事件中心。</span><span class="sxs-lookup"><span data-stu-id="57261-108">One way tooupload and collect logs is toouse hello Linux Azure Diagnostics (LAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="57261-109">您也可以使用外部處理序 tooread hello 事件從儲存體，並放在中，已分析的平台產品，例如[OMS 記錄分析](../log-analytics/log-analytics-service-fabric.md)或另一個記錄檔剖析方案。</span><span class="sxs-lookup"><span data-stu-id="57261-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="log-and-event-sources"></a><span data-ttu-id="57261-110">記錄和事件來源</span><span class="sxs-lookup"><span data-stu-id="57261-110">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="57261-111">Service Fabric 平台事件</span><span class="sxs-lookup"><span data-stu-id="57261-111">Service Fabric platform events</span></span>
<span data-ttu-id="57261-112">Service Fabric 會透過 [LTTng](http://lttng.org) 發出少數的現成記錄，包括運作事件或執行階段事件。</span><span class="sxs-lookup"><span data-stu-id="57261-112">Service Fabric emits a few out-of-the-box logs via [LTTng](http://lttng.org), including operational events or runtime events.</span></span> <span data-ttu-id="57261-113">這些記錄會儲存在 hello hello 叢集的資源管理員範本指定的位置。</span><span class="sxs-lookup"><span data-stu-id="57261-113">These logs are stored in hello location that hello cluster's Resource Manager template specifies.</span></span> <span data-ttu-id="57261-114">tooget 或設定 hello 儲存體帳戶的詳細資訊，請搜尋 hello 標記**AzureTableWinFabETWQueryable**並尋找**StoreConnectionString**。</span><span class="sxs-lookup"><span data-stu-id="57261-114">tooget or set hello storage account details, search for hello tag **AzureTableWinFabETWQueryable** and look for **StoreConnectionString**.</span></span>

### <a name="application-events"></a><span data-ttu-id="57261-115">應用程式事件</span><span class="sxs-lookup"><span data-stu-id="57261-115">Application events</span></span>
 <span data-ttu-id="57261-116">檢測軟體時，會如您在應用程式和服務的程式碼中所指定的，發出事件。</span><span class="sxs-lookup"><span data-stu-id="57261-116">Events emitted from your applications' and services' code as specified by you when instrumenting your software.</span></span> <span data-ttu-id="57261-117">您可以使用任何撰寫文字型記錄檔的記錄解決方案，例如 LTTng。</span><span class="sxs-lookup"><span data-stu-id="57261-117">You can use any logging solution that writes text-based log files--for example, LTTng.</span></span> <span data-ttu-id="57261-118">如需詳細資訊，請參閱 hello LTTng 文件上追蹤您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="57261-118">For more information, see hello LTTng documentation on tracing your application.</span></span>

<span data-ttu-id="57261-119">[監視和診斷本機開發設定中的服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。</span><span class="sxs-lookup"><span data-stu-id="57261-119">[Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="57261-120">Hello 診斷延伸模組部署</span><span class="sxs-lookup"><span data-stu-id="57261-120">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="57261-121">hello 收集記錄檔中的第一個步驟是 toodeploy hello 診斷延伸模組，每個 hello Service Fabric 叢集中的 hello Vm 上。</span><span class="sxs-lookup"><span data-stu-id="57261-121">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="57261-122">hello 診斷延伸模組會收集每個 VM 上的記錄檔，並將其上傳 toohello 您指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="57261-122">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="57261-123">hello 步驟會根據您使用 hello Azure 入口網站或 Azure 資源管理員而有所不同。</span><span class="sxs-lookup"><span data-stu-id="57261-123">hello steps vary based on whether you use hello Azure portal or Azure Resource Manager.</span></span>

<span data-ttu-id="57261-124">toodeploy hello 診斷延伸模組 toohello Vm 做為叢集建立一部分的 hello 叢集中設定**診斷**太**上**。</span><span class="sxs-lookup"><span data-stu-id="57261-124">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, set **Diagnostics** too**On**.</span></span> <span data-ttu-id="57261-125">建立 hello 叢集之後，您無法使用 hello 入口網站來變更此設定。</span><span class="sxs-lookup"><span data-stu-id="57261-125">After you create hello cluster, you can't change this setting by using hello portal.</span></span>

<span data-ttu-id="57261-126">然後，設定 Linux Azure 診斷 （年輕人） toocollect hello 檔案，並將它們放入您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="57261-126">Then, configure Linux Azure Diagnostics (LAD) toocollect hello files and place them into your storage account.</span></span> <span data-ttu-id="57261-127">此程序會說明案例 （[上傳您自己的記錄檔]） hello 文件中的 3[使用年輕人 toomonitor 及診斷 Linux Vm](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="57261-127">This process is explained as scenario 3 ("Upload your own log files") in hello article [Using LAD toomonitor and diagnose Linux VMs](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="57261-128">遵循此程序取得，存取 toohello 追蹤。</span><span class="sxs-lookup"><span data-stu-id="57261-128">Following this process gets you access toohello traces.</span></span> <span data-ttu-id="57261-129">您可以上傳您所選擇的 hello 追蹤 tooa 視覺化檢視。</span><span class="sxs-lookup"><span data-stu-id="57261-129">You can upload hello traces tooa visualizer of your choice.</span></span>

<span data-ttu-id="57261-130">您也可以使用 Azure Resource Manager 部署 hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="57261-130">You can also deploy hello Diagnostics extension by using Azure Resource Manager.</span></span> <span data-ttu-id="57261-131">hello 程序類似於 Windows 及 Linux 與 Windows 叢集的已記錄[toocollect 使用 Azure 診斷的記錄方式](service-fabric-diagnostics-how-to-setup-wad.md)。</span><span class="sxs-lookup"><span data-stu-id="57261-131">hello process is similar for Windows and Linux and is documented for Windows clusters in [How toocollect logs with Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).</span></span>

<span data-ttu-id="57261-132">您也可以使用 Operations Management Suite，如 [Operations Management Suite Log Analytics with Linux (搭配 Linux 使用 Operations Management Suite Log Analytics)](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/) 中所述。</span><span class="sxs-lookup"><span data-stu-id="57261-132">You can also use Operations Management Suite, as described in [Operations Management Suite Log Analytics with Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).</span></span>

<span data-ttu-id="57261-133">完成這項設定之後，hello 年輕人代理程式監視 hello 指定的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="57261-133">After you finish this configuration, hello LAD agent monitors hello specified log files.</span></span> <span data-ttu-id="57261-134">每當新的一行時附加的 toohello 檔案，它會建立可供您指定傳送的 toohello 儲存體的 syslog 項目。</span><span class="sxs-lookup"><span data-stu-id="57261-134">Whenever a new line is appended toohello file, it creates a syslog entry that is sent toohello storage that you specified.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57261-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57261-135">Next steps</span></span>

<span data-ttu-id="57261-136">請參閱詳細 toounderstand 問題，問題進行疑難排解時，您應該檢查哪些事件[LTTng 文件](http://lttng.org/docs)和[使用年輕人](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="57261-136">toounderstand in more detail what events you should examine while troubleshooting issues, see [LTTng documentation](http://lttng.org/docs) and [Using LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>
