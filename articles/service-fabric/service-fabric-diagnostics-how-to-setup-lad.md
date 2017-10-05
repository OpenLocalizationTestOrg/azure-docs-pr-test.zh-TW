---
title: "使用 Linux Azure 診斷收集記錄檔 | Microsoft Docs"
description: "本文將說明如何設定 Azure 診斷，以便從 Azure 中執行的 Service Fabric Linux 叢集收集記錄檔。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: 3e41caaeb38c55d1c6c3bfdce2f81c86b4aff4d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="07d73-103">使用 Azure 診斷收集記錄檔</span><span class="sxs-lookup"><span data-stu-id="07d73-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07d73-104">Windows</span><span class="sxs-lookup"><span data-stu-id="07d73-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="07d73-105">Linux</span><span class="sxs-lookup"><span data-stu-id="07d73-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="07d73-106">當您執行 Azure Service Fabric 叢集時，最好從中央位置的所有節點收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="07d73-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="07d73-107">只要將記錄檔集中在一個位置，不論問題發生在服務、應用程式或叢集本身，都能輕鬆分析問題並進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="07d73-107">Having the logs in a central location makes it easy to analyze and troubleshoot issues, whether they are in your services, your application, or the cluster itself.</span></span> <span data-ttu-id="07d73-108">上傳和收集記錄檔的其中一種方式就是使用「Azure 診斷」擴充功能，此擴充功能可將記錄檔上傳到「Azure 儲存體」、Azure Application Insights 或「Azure 事件中樞」。</span><span class="sxs-lookup"><span data-stu-id="07d73-108">One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage, Azure Application Insights or Azure Event Hubs.</span></span> <span data-ttu-id="07d73-109">您也可以從儲存體或「事件中樞」讀取事件，然後將它們放在 [Log Analytics](../log-analytics/log-analytics-service-fabric.md) 之類的產品或其他記錄檔剖析解決方案中。</span><span class="sxs-lookup"><span data-stu-id="07d73-109">You can also read the events from storage or Event Hubs and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="07d73-110">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 隨附完整的記錄搜尋與分析服務內建功能。</span><span class="sxs-lookup"><span data-stu-id="07d73-110">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="log-sources-that-you-might-want-to-collect"></a><span data-ttu-id="07d73-111">您可能想要收集的記錄來源</span><span class="sxs-lookup"><span data-stu-id="07d73-111">Log sources that you might want to collect</span></span>
* <span data-ttu-id="07d73-112">**Service Fabric 記錄檔**︰由平台透過 [LTTng](http://lttng.org) 所發出並上傳至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="07d73-112">**Service Fabric logs**: Emitted from the platform via [LTTng](http://lttng.org) and uploaded to your storage account.</span></span> <span data-ttu-id="07d73-113">記錄檔可能是平台所發出的操作事件或執行階段事件。</span><span class="sxs-lookup"><span data-stu-id="07d73-113">Logs can be operational events or runtime events that the platform emits.</span></span> <span data-ttu-id="07d73-114">這些記錄檔會儲存在叢集資訊清單所指定的位置。</span><span class="sxs-lookup"><span data-stu-id="07d73-114">These logs are stored in the location that the cluster manifest specifies.</span></span> <span data-ttu-id="07d73-115">(若要取得儲存體帳戶的詳細資訊，請搜尋 **AzureTableWinFabETWQueryable** 標籤並尋找 **StoreConnectionString**)。</span><span class="sxs-lookup"><span data-stu-id="07d73-115">(To get the storage account details, search for the tag **AzureTableWinFabETWQueryable** and look for **StoreConnectionString**.)</span></span>
* <span data-ttu-id="07d73-116">**應用程式事件**：從服務程式碼發出。</span><span class="sxs-lookup"><span data-stu-id="07d73-116">**Application events**: Emitted from your service's code.</span></span> <span data-ttu-id="07d73-117">您可以使用任何撰寫文字型記錄檔的記錄解決方案，例如 LTTng。</span><span class="sxs-lookup"><span data-stu-id="07d73-117">You can use any logging solution that writes text-based log files--for example, LTTng.</span></span> <span data-ttu-id="07d73-118">如需詳細資訊，請參閱 LTTng 文件中關於追蹤您應用程式的內容。</span><span class="sxs-lookup"><span data-stu-id="07d73-118">For more information, see the LTTng documentation on tracing your application.</span></span>  

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="07d73-119">部署診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="07d73-119">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="07d73-120">收集記錄檔的第一個步驟是將診斷擴充功能部署在 Service Fabric 叢集的每個 WM 上。</span><span class="sxs-lookup"><span data-stu-id="07d73-120">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="07d73-121">診斷擴充功能會收集每個 VM 上的記錄檔，並將它們上傳至您指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="07d73-121">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="07d73-122">步驟視您使用 Azure 入口網站或 Azure Resource Manager 而有所不同。</span><span class="sxs-lookup"><span data-stu-id="07d73-122">The steps vary based on whether you use the Azure portal or Azure Resource Manager.</span></span>

<span data-ttu-id="07d73-123">若要在建立叢集過程中將診斷擴充功能部署至叢集中的 VM，請將 [診斷] 設為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="07d73-123">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, set **Diagnostics** to **On**.</span></span> <span data-ttu-id="07d73-124">建立叢集之後，您就無法使用入口網站變更這項設定。</span><span class="sxs-lookup"><span data-stu-id="07d73-124">After you create the cluster, you can't change this setting by using the portal.</span></span>

<span data-ttu-id="07d73-125">接著，設定 Linux Azure 診斷 (LAD) 來收集檔案，並將它們放入您的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="07d73-125">Then, configure Linux Azure Diagnostics (LAD) to collect the files and place them into your storage account.</span></span> <span data-ttu-id="07d73-126">[使用 LAD 監視 Linux VM 的效能和診斷資料](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)一文中的案例 3 (＜上傳您自己的記錄檔＞) 將會說明這個程序。</span><span class="sxs-lookup"><span data-stu-id="07d73-126">This process is explained as scenario 3 ("Upload your own log files") in the article [Using LAD to monitor and diagnose Linux VMs](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="07d73-127">遵循這個程序就可以存取追蹤。</span><span class="sxs-lookup"><span data-stu-id="07d73-127">Following this process gets you access to the traces.</span></span> <span data-ttu-id="07d73-128">您可以將追蹤上傳到所選擇的視覺化檢視。</span><span class="sxs-lookup"><span data-stu-id="07d73-128">You can upload the traces to a visualizer of your choice.</span></span>

<span data-ttu-id="07d73-129">您也可以使用 Azure Resource Manager 來部署診斷擴充功能。</span><span class="sxs-lookup"><span data-stu-id="07d73-129">You can also deploy the Diagnostics extension by using Azure Resource Manager.</span></span> <span data-ttu-id="07d73-130">此程序在 Windows 及 Linux 上都很類似，而[如何利用 Azure 診斷收集記錄檔](service-fabric-diagnostics-how-to-setup-wad.md)中將針對 Windows 叢集提供相關說明。</span><span class="sxs-lookup"><span data-stu-id="07d73-130">The process is similar for Windows and Linux and is documented for Windows clusters in [How to collect logs with Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).</span></span>

<span data-ttu-id="07d73-131">您也可以使用 Operations Management Suite，如 [Operations Management Suite Log Analytics with Linux (搭配 Linux 使用 Operations Management Suite Log Analytics)](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/) 中所述。</span><span class="sxs-lookup"><span data-stu-id="07d73-131">You can also use Operations Management Suite, as described in [Operations Management Suite Log Analytics with Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).</span></span>

<span data-ttu-id="07d73-132">完成此設定之後，LAD 代理程式就會監視指定的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="07d73-132">After you finish this configuration, the LAD agent monitors the specified log files.</span></span> <span data-ttu-id="07d73-133">每當新的一行附加至檔案時，系統就會建立 syslog 項目並傳送至您所指定的儲存體。</span><span class="sxs-lookup"><span data-stu-id="07d73-133">Whenever a new line is appended to the file, it creates a syslog entry that is sent to the storage that you specified.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07d73-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07d73-134">Next steps</span></span>
<span data-ttu-id="07d73-135">若要更仔細了解您在進行問題的疑難排解時應該調查哪些事件，請參閱 [LTTng 文件](http://lttng.org/docs)和[使用 LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="07d73-135">To understand in more detail what events you should examine while troubleshooting issues, see [LTTng documentation](http://lttng.org/docs) and [Using LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

