---
title: "aaaMonitoring Azure 函式 |Microsoft 文件"
description: "深入了解如何 toomonitor Azure 函式。"
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="4c48e-104">監視 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="4c48e-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="4c48e-105">概觀</span><span class="sxs-lookup"><span data-stu-id="4c48e-105">Overview</span></span> 


<span data-ttu-id="4c48e-106">hello**監視器**索引標籤上，每個函式可讓您 tooreview 函式的每個執行。</span><span class="sxs-lookup"><span data-stu-id="4c48e-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Azure Functions 監視索引標籤](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="4c48e-108">按一下 執行可讓您 tooreview hello 持續期間、 輸入的資料、 錯誤和關聯的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4c48e-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="4c48e-109">這對於函式的偵錯和效能調整很實用。</span><span class="sxs-lookup"><span data-stu-id="4c48e-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="4c48e-110">當使用 hello[裝載計劃的耗用量](functions-overview.md#pricing)對於 Azure 函式，hello**監視**hello 函式應用程式概觀刀鋒視窗中的磚將不會顯示任何資料。</span><span class="sxs-lookup"><span data-stu-id="4c48e-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="4c48e-111">這是因為 hello 平台動態調整，以及讓這些計量並沒有意義耗用量計劃，為您管理運算執行個體。</span><span class="sxs-lookup"><span data-stu-id="4c48e-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="4c48e-112">toomonitor hello 函式應用程式，您應該改為使用 hello 指引本文中。</span><span class="sxs-lookup"><span data-stu-id="4c48e-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="4c48e-113">下列螢幕擷取畫面的 hello 顯示範例：</span><span class="sxs-lookup"><span data-stu-id="4c48e-113">hello following screen-shot shows an example:</span></span>
> 
> ![Hello 主要資源刀鋒視窗上的監視](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="4c48e-115">即時監視</span><span class="sxs-lookup"><span data-stu-id="4c48e-115">Real-time monitoring</span></span>

<span data-ttu-id="4c48e-116">按一下如下所示的 [即時事件串流]，即可進行即時監視。</span><span class="sxs-lookup"><span data-stu-id="4c48e-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![即時事件資料流 hello 監視 索引標籤選項](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="4c48e-118">將新的瀏覽器索引標籤以繪製 hello 即時事件資料流，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4c48e-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![即時事件串流範例](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="4c48e-120">沒有已知的問題，可能會造成填入您資料 toofail toobe。</span><span class="sxs-lookup"><span data-stu-id="4c48e-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="4c48e-121">如果您遇到的情況，您可能需要 tooclose hello 瀏覽器索引標籤包含 hello 即時事件資料流，然後按一下**即時事件資料流**再次 tooallow 它 tooproperly 填入事件資料流資料。</span><span class="sxs-lookup"><span data-stu-id="4c48e-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="4c48e-122">hello 即時事件資料流將圖形 hello 遵循您的函式的統計資料：</span><span class="sxs-lookup"><span data-stu-id="4c48e-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="4c48e-123">每秒啟動的執行數</span><span class="sxs-lookup"><span data-stu-id="4c48e-123">Executions started per second</span></span>
* <span data-ttu-id="4c48e-124">每秒完成的執行數</span><span class="sxs-lookup"><span data-stu-id="4c48e-124">Executions completed per second</span></span>
* <span data-ttu-id="4c48e-125">每秒失敗的執行數</span><span class="sxs-lookup"><span data-stu-id="4c48e-125">Executions failed per second</span></span>
* <span data-ttu-id="4c48e-126">平均執行時間 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="4c48e-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="4c48e-127">這些統計資料是即時但是 hello 實際 hello 執行資料的圖形可能會有約 10 秒的延遲。</span><span class="sxs-lookup"><span data-stu-id="4c48e-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="4c48e-128">從命令列監視記錄檔</span><span class="sxs-lookup"><span data-stu-id="4c48e-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="4c48e-129">您可以使用 hello Azure 命令列介面 (CLI) 或 PowerShell 在本機工作站串流記錄檔案 tooa 命令列工作階段。</span><span class="sxs-lookup"><span data-stu-id="4c48e-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="4c48e-130">監視以 hello Azure CLI 函式應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="4c48e-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="4c48e-131">啟動，tooget[安裝 hello Azure CLI](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="4c48e-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="4c48e-132">登入您的 Azure 帳戶使用 hello 下列命令，或任何 hello 涵蓋，其他選項[登入從 hello Azure CLI tooAzure](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="4c48e-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="4c48e-133">使用 hello 下列命令 tooenable Azure CLI 服務管理 (ASM) 模式:。</span><span class="sxs-lookup"><span data-stu-id="4c48e-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="4c48e-134">如果您有多個訂閱，使用下列命令 toolist hello，您的訂用帳戶和設定 hello 目前訂用帳戶 toohello 訂用帳戶，其中包含應用程式函式。</span><span class="sxs-lookup"><span data-stu-id="4c48e-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="4c48e-135">hello 下列命令會串流 hello 記錄檔的函式應用程式 toohello 命令列：</span><span class="sxs-lookup"><span data-stu-id="4c48e-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="4c48e-136">使用 PowerShell 監視函式應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="4c48e-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="4c48e-137">啟動，tooget[安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4c48e-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="4c48e-138">加入您的 Azure 帳戶執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c48e-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="4c48e-139">如果您有多個訂閱，您可以列出名稱以下列命令 toosee，如果正確的訂用帳戶為目前選取的 hello hello 為基礎的 hello`IsCurrent`屬性：</span><span class="sxs-lookup"><span data-stu-id="4c48e-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="4c48e-140">如果您需要 tooset hello 作用中訂用帳戶 toohello 一個包含您的函式應用程式，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c48e-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="4c48e-141">資料流 hello 記錄 tooyour PowerShell 工作階段以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="4c48e-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="4c48e-142">如需詳細資訊，請參閱太[How to： 在 web 應用程式記錄檔資料流](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs)。</span><span class="sxs-lookup"><span data-stu-id="4c48e-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4c48e-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c48e-143">Next steps</span></span>
<span data-ttu-id="4c48e-144">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c48e-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="4c48e-145">測試函數</span><span class="sxs-lookup"><span data-stu-id="4c48e-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="4c48e-146">調整函數</span><span class="sxs-lookup"><span data-stu-id="4c48e-146">Scale a function</span></span>](functions-scale.md)

