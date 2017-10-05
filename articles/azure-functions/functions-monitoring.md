---
title: "監視 Azure Functions | Microsoft Docs"
description: "了解如何監視 Azure Functions。"
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="895b2-104">監視 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="895b2-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="895b2-105">概觀</span><span class="sxs-lookup"><span data-stu-id="895b2-105">Overview</span></span> 


<span data-ttu-id="895b2-106">每個函式的 [監視] 索引標籤可讓您檢閱每次函式執行。</span><span class="sxs-lookup"><span data-stu-id="895b2-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Azure Functions 監視索引標籤](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="895b2-108">按一下執行，您即可檢閱持續時間、輸入資料、錯誤和相關聯的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="895b2-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="895b2-109">這對於函式的偵錯和效能調整很實用。</span><span class="sxs-lookup"><span data-stu-id="895b2-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="895b2-110">使用 Azure Functions 的[取用主控方案](functions-overview.md#pricing)時，函式應用程式 [概觀] 刀鋒視窗中的 [監視] 圖格不會顯示任何資料。</span><span class="sxs-lookup"><span data-stu-id="895b2-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="895b2-111">這是因為平台為您動態調整和管理計算執行個體，所以這些計量對取用方案而言沒有意義。</span><span class="sxs-lookup"><span data-stu-id="895b2-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="895b2-112">若要監視函式應用程式的使用量，您應該改用本文中的指引。</span><span class="sxs-lookup"><span data-stu-id="895b2-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="895b2-113">以下螢幕擷取畫面顯示一個範例︰</span><span class="sxs-lookup"><span data-stu-id="895b2-113">The following screen-shot shows an example:</span></span>
> 
> ![在主要資源刀鋒視窗上監視](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="895b2-115">即時監視</span><span class="sxs-lookup"><span data-stu-id="895b2-115">Real-time monitoring</span></span>

<span data-ttu-id="895b2-116">按一下如下所示的 [即時事件串流]，即可進行即時監視。</span><span class="sxs-lookup"><span data-stu-id="895b2-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![監視索引標籤的即時事件串流選項](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="895b2-118">即時事件串流會在新的瀏覽器索引標籤中以圖表呈現，如下所示。</span><span class="sxs-lookup"><span data-stu-id="895b2-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![即時事件串流範例](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="895b2-120">有個已知問題可能會導致您的資料填入失敗。</span><span class="sxs-lookup"><span data-stu-id="895b2-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="895b2-121">如果您遇到此種情況，您可能需要關閉包含即時事件串流的瀏覽器索引標籤，然後再按一次 [即時事件串流]，使其正確地填入您的事件串流資料。</span><span class="sxs-lookup"><span data-stu-id="895b2-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="895b2-122">即時事件串流將以圖形呈現函式的下列統計資料︰</span><span class="sxs-lookup"><span data-stu-id="895b2-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="895b2-123">每秒啟動的執行數</span><span class="sxs-lookup"><span data-stu-id="895b2-123">Executions started per second</span></span>
* <span data-ttu-id="895b2-124">每秒完成的執行數</span><span class="sxs-lookup"><span data-stu-id="895b2-124">Executions completed per second</span></span>
* <span data-ttu-id="895b2-125">每秒失敗的執行數</span><span class="sxs-lookup"><span data-stu-id="895b2-125">Executions failed per second</span></span>
* <span data-ttu-id="895b2-126">平均執行時間 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="895b2-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="895b2-127">這些統計資料是即時的，但是執行資料的實際圖表可能會延遲大約 10 秒。</span><span class="sxs-lookup"><span data-stu-id="895b2-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="895b2-128">從命令列監視記錄檔</span><span class="sxs-lookup"><span data-stu-id="895b2-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="895b2-129">您可以使用 Azure 命令列介面 (CLI) 或 PowerShell，在本機工作站上將記錄檔串流處理至命令列工作階段。</span><span class="sxs-lookup"><span data-stu-id="895b2-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="895b2-130">使用 Azure CLI 監視函式應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="895b2-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="895b2-131">首先，請[安裝 Azure CLI](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="895b2-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="895b2-132">使用下列命令，或[從 Azure CLI 登入 Azure](../xplat-cli-connect.md)中涵蓋的任何其他選項，登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="895b2-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="895b2-133">使用下列命令來啟用 Azure CLI 服務管理 (ASM) 模式：</span><span class="sxs-lookup"><span data-stu-id="895b2-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="895b2-134">如果您有多個訂用帳戶，請使用下列命令來列出訂用帳戶，並將目前的訂用帳戶設定為包含函式應用程式的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="895b2-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="895b2-135">下列命令會將函式應用程式的記錄檔串流處理至命令列︰</span><span class="sxs-lookup"><span data-stu-id="895b2-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="895b2-136">使用 PowerShell 監視函式應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="895b2-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="895b2-137">首先，請[安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="895b2-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="895b2-138">執行下列命令來新增您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="895b2-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="895b2-139">如果您有多個訂用帳戶，您可以使用下列命令依照名稱加以列出，以查看目前是否根據 `IsCurrent` 屬性選取正確的訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="895b2-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="895b2-140">如果您需要將作用中的訂用帳戶設定為包含函式應用程式的訂用帳戶，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="895b2-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="895b2-141">使用下列命令將記錄檔串流處理至您的 PowerShell 工作階段︰</span><span class="sxs-lookup"><span data-stu-id="895b2-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="895b2-142">如需詳細資訊，請參閱[作法︰串流處理 Web 應用程式的記錄檔](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs)。</span><span class="sxs-lookup"><span data-stu-id="895b2-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="895b2-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="895b2-143">Next steps</span></span>
<span data-ttu-id="895b2-144">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="895b2-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="895b2-145">測試函數</span><span class="sxs-lookup"><span data-stu-id="895b2-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="895b2-146">調整函數</span><span class="sxs-lookup"><span data-stu-id="895b2-146">Scale a function</span></span>](functions-scale.md)

