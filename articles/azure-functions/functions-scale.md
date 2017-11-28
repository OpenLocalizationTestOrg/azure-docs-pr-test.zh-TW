---
title: "aaaAzure 函式耗用量和應用程式服務計劃 |Microsoft 文件"
description: "了解 Azure 函式如何縮放 toomeet hello 事件驅動工作負載的需求。"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a><span data-ttu-id="d3fc4-104">Azure Functions 取用和 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="d3fc4-104">Azure Functions Consumption and App Service plans</span></span> 

## <a name="introduction"></a><span data-ttu-id="d3fc4-105">簡介</span><span class="sxs-lookup"><span data-stu-id="d3fc4-105">Introduction</span></span>

<span data-ttu-id="d3fc4-106">Azure Functions 的執行模式有兩種︰取用方案和 Azure App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-106">You can run Azure Functions in two different modes: Consumption plan and Azure App Service plan.</span></span> <span data-ttu-id="d3fc4-107">hello 耗用量計劃您的程式碼會執行時，能有效擴充為必要 toohandle 負載，而且再按比例減少 程式碼未執行時，自動配置運算能力。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-107">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="d3fc4-108">因此，您沒有 toopay 閒置 Vm 的而且沒有 tooreserve 容量事先。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-108">So, you don't have toopay for idle VMs and don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="d3fc4-109">本文著重在 hello 耗用量計劃。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-109">This article focuses on hello Consumption plan.</span></span> <span data-ttu-id="d3fc4-110">如需 hello 應用程式服務方案的運作方式的詳細資訊，請參閱 hello [Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-110">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="d3fc4-111">如果您不熟悉 Azure 函式，請參閱 hello [Azure 函式概觀](functions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-111">If you aren't familiar with Azure Functions, see hello [Azure Functions overview](functions-overview.md).</span></span>

<span data-ttu-id="d3fc4-112">當您建立函式的應用程式時，您必須設定主控方案函式包含該 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-112">When you create a function app, you must configure a hosting plan for functions that hello app contains.</span></span> <span data-ttu-id="d3fc4-113">在任一模式中，執行個體的 hello *Azure 函式主機*執行 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-113">In either mode, an instance of hello *Azure Functions host* executes hello functions.</span></span> <span data-ttu-id="d3fc4-114">hello 計劃的控制項類型：</span><span class="sxs-lookup"><span data-stu-id="d3fc4-114">hello type of plan controls:</span></span>

* <span data-ttu-id="d3fc4-115">主控件執行個體如何向外延展。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-115">How host instances are scaled out.</span></span>
* <span data-ttu-id="d3fc4-116">hello 受到可用 tooeach 主機的資源。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-116">hello resources that are available tooeach host.</span></span>

<span data-ttu-id="d3fc4-117">目前，您必須在 hello hello 函式應用程式建立期間選擇 hello 計劃類型。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-117">Currently, you must choose hello plan type during hello creation of hello function app.</span></span> <span data-ttu-id="d3fc4-118">之後便無法更改。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-118">You can't change it afterward.</span></span> 

<span data-ttu-id="d3fc4-119">您可以在 hello 應用程式服務方案的各層之間進行調整。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-119">You can scale between tiers on hello App Service plan.</span></span> <span data-ttu-id="d3fc4-120">Hello 耗用量計畫，Azure 函式會自動處理所有的資源配置。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-120">On hello Consumption plan, Azure Functions automatically handles all resource allocation.</span></span>

## <a name="consumption-plan"></a><span data-ttu-id="d3fc4-121">取用方案</span><span class="sxs-lookup"><span data-stu-id="d3fc4-121">Consumption plan</span></span>

<span data-ttu-id="d3fc4-122">當您使用的耗用量計劃時，hello Azure 函式主控件執行個體以動態方式加入和移除根據 hello 傳入的事件數目。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-122">When you're using a Consumption plan, instances of hello Azure Functions host are dynamically added and removed based on hello number of incoming events.</span></span> <span data-ttu-id="d3fc4-123">這個方案會自動調整，您只需支付您的函式執行時使用的計算資源。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-123">This plan scales automatically, and you are charged for compute resources only when your functions are running.</span></span> <span data-ttu-id="d3fc4-124">在取用方案中，函式最多可執行 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-124">On a Consumption plan, a function can run for a maximum of 10 minutes.</span></span> 

> [!NOTE]
> <span data-ttu-id="d3fc4-125">hello 耗用量計劃的函式的預設逾時是 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-125">hello default timeout for functions on a Consumption plan is 5 minutes.</span></span> <span data-ttu-id="d3fc4-126">hello 值可以是藉由變更 hello 屬性的 hello 函式應用程式的增加的 too10 分鐘`functionTimeout`中[host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-126">hello value can be increased too10 minutes for hello Function App by changing hello property `functionTimeout` in [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

<span data-ttu-id="d3fc4-127">計費是根據執行時間和使用的記憶體，會針對函數應用程式內的所有函式加以彙總。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-127">Billing is based on execution time and memory used, and it's aggregated across all functions within a function app.</span></span> <span data-ttu-id="d3fc4-128">如需詳細資訊，請參閱 hello [Azure 函式定價頁面]。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-128">For more information, see hello [Azure Functions pricing page].</span></span>

<span data-ttu-id="d3fc4-129">hello 耗用量計劃是 hello 預設值，而且提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="d3fc4-129">hello Consumption plan is hello default and offers hello following benefits:</span></span>
- <span data-ttu-id="d3fc4-130">只有當您的函式執行時才需付費。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-130">Pay only when your functions are running.</span></span>
- <span data-ttu-id="d3fc4-131">自動調整規模，即使在高負載期間也會。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-131">Scale out automatically, even during periods of high load.</span></span>

## <a name="app-service-plan"></a><span data-ttu-id="d3fc4-132">App Service 方案</span><span class="sxs-lookup"><span data-stu-id="d3fc4-132">App Service plan</span></span>

<span data-ttu-id="d3fc4-133">Basic、 Standard 和 Premium Sku 類似 tooWeb 應用程式上的專用 Vm 上執行的應用程式函式，在 hello 應用程式服務計劃。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-133">In hello App Service plan, your function apps run on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooWeb Apps.</span></span> <span data-ttu-id="d3fc4-134">專用的 Vm 是配置的 tooyour App Service 應用程式，也就是說 hello 函式主機持續執行。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-134">Dedicated VMs are allocated tooyour App Service apps, which means hello functions host is always running.</span></span>

<span data-ttu-id="d3fc4-135">請考慮在下列情況下的 hello App Service 方案：</span><span class="sxs-lookup"><span data-stu-id="d3fc4-135">Consider an App Service plan in hello following cases:</span></span>
- <span data-ttu-id="d3fc4-136">您有現有的、使用量過低的 VM 已在執行其他 App Service 執行個體。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-136">You have existing, underutilized VMs that are already running other App Service instances.</span></span>
- <span data-ttu-id="d3fc4-137">您預期您的函式的應用程式 toorun 持續，或幾乎持續。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-137">You expect your function apps toorun continuously, or nearly continuously.</span></span>
- <span data-ttu-id="d3fc4-138">您需要更多的 CPU 或記憶體選項所提供 hello 耗用量計劃。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-138">You need more CPU or memory options than what is provided on hello Consumption plan.</span></span>
- <span data-ttu-id="d3fc4-139">您需要 toorun 超過 hello hello 耗用量計劃允許最大執行時間。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-139">You need toorun longer than hello maximum execution time allowed on hello Consumption plan.</span></span>

<span data-ttu-id="d3fc4-140">VM 會減少執行階段和記憶體大小的成本。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-140">A VM decouples cost from both runtime and memory size.</span></span> <span data-ttu-id="d3fc4-141">如此一來，您將支付超過您配置的 hello VM 執行個體的 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-141">As a result, you won't pay more than hello cost of hello VM instance that you allocate.</span></span> <span data-ttu-id="d3fc4-142">如需 hello 應用程式服務方案的運作方式的詳細資訊，請參閱 hello [Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-142">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="d3fc4-143">使用 App Service 方案時，您可以透過手動新增更多 VM 執行個體來相應放大，或者您可以啟用自動規模調整。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-143">With an App Service plan, you can manually scale out by adding more VM instances, or you can enable autoscale.</span></span> <span data-ttu-id="d3fc4-144">如需詳細資訊，請參閱[手動或自動調整執行個體計數規模](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-144">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span> <span data-ttu-id="d3fc4-145">您也可以透過選擇不同的 App Service 方案來相應增加。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-145">You can also scale up by choosing a different App Service plan.</span></span> <span data-ttu-id="d3fc4-146">如需詳細資訊，請參閱[在 Azure 中為應用程式進行相應增加](../app-service-web/web-sites-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-146">For more information, see [Scale up an app in Azure](../app-service-web/web-sites-scale.md).</span></span> <span data-ttu-id="d3fc4-147">如果您打算 toorun JavaScript 函式上的應用程式服務計劃，您應該選擇的方案有較少的核心。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-147">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan that has fewer cores.</span></span> <span data-ttu-id="d3fc4-148">如需詳細資訊，請參閱 hello [JavaScript 函式的參考](functions-reference-node.md#choose-single-core-app-service-plans)。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-148">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>  

<span data-ttu-id="d3fc4-149"><!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
###永遠開啟</span><span class="sxs-lookup"><span data-stu-id="d3fc4-149"><!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### Always On</span></span>

<span data-ttu-id="d3fc4-150">如果您執行應用程式服務方案時，您應該啟用 hello **Always On**設定，好讓您的函式應用程式能夠正確執行。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-150">If you run on an App Service plan, you should enable hello **Always On** setting so that your function app  runs correctly.</span></span> <span data-ttu-id="d3fc4-151">App Service 方案，在 hello 函式執行階段會進入閒置狀態一段時間，請稍候幾分鐘讓只有 HTTP 觸發程序將 「 喚醒 」 函式。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-151">On an App Service plan, hello functions runtime will go idle after a few minutes of inactivity, so only HTTP triggers will "wake up" your functions.</span></span> <span data-ttu-id="d3fc4-152">這是類似 toohow WebJobs 必須已啟用 Always On。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-152">This is similar toohow WebJobs must have Always On enabled.</span></span> 

<span data-ttu-id="d3fc4-153">只有 App Service 方案具備「永遠開啟」選項。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-153">Always On is available only on an App Service plan.</span></span> <span data-ttu-id="d3fc4-154">耗用量計劃，hello 平台會自動啟動函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-154">On a Consumption plan, hello platform activates function apps automatically.</span></span>

## <a name="storage-account-requirements"></a><span data-ttu-id="d3fc4-155">儲存體帳戶的需求</span><span class="sxs-lookup"><span data-stu-id="d3fc4-155">Storage account requirements</span></span>

<span data-ttu-id="d3fc4-156">不論是取用方案或 App Service 方案，函數應用程式都需要有支援 Azure Blob、佇列、表格儲存體的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-156">On either a Consumption plan or an App Service plan, a function app requires an Azure Storage account that supports Azure Blob, Queue, and Table storage.</span></span> <span data-ttu-id="d3fc4-157">Azure Functions 會在內部使用「Azure 儲存體」來進行作業，例如管理觸發程序和記錄函數執行。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-157">Internally, Azure Functions uses Azure Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="d3fc4-158">有些儲存體帳戶並不支援佇列和表格，例如僅限 Blob 的儲存體帳戶 (包括進階儲存體) 和搭配區域備援儲存體複寫的一般用途儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-158">Some storage accounts do not support queues and tables, such as blob-only storage accounts (including premium storage) and general-purpose storage accounts with zone-redundant storage replication.</span></span> <span data-ttu-id="d3fc4-159">這些帳戶會篩選從 hello**儲存體帳戶**刀鋒視窗中建立函數應用程式時。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-159">These accounts are filtered from hello **Storage Account** blade when you're creating a function app.</span></span>

<span data-ttu-id="d3fc4-160">toolearn 進一步了解儲存體帳戶類型，請參閱[簡介 hello Azure 儲存體服務](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-160">toolearn more about storage account types, see [Introducing hello Azure Storage services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span>

## <a name="how-hello-consumption-plan-works"></a><span data-ttu-id="d3fc4-161">Hello 耗用量計劃的運作方式</span><span class="sxs-lookup"><span data-stu-id="d3fc4-161">How hello Consumption plan works</span></span>

<span data-ttu-id="d3fc4-162">hello 耗用量計劃自動縮放透過加入其他執行個體的 hello 函式的主機，根據 hello 其函式觸發的事件數目的 CPU 和記憶體資源。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-162">hello Consumption plan automatically scales CPU and memory resources by adding additional instances of hello Functions host, based on hello number of events that its functions are triggered on.</span></span> <span data-ttu-id="d3fc4-163">Hello 函式主控件的每個執行個體是記憶體的有限的 too1.5 GB。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-163">Each instance of hello Functions host is limited too1.5 GB of memory.</span></span>

<span data-ttu-id="d3fc4-164">當您使用 hello 裝載計劃的耗用量，hello 主要儲存體帳戶的 Azure 檔案共用上儲存函式的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-164">When you use hello Consumption hosting plan, function code files are stored on Azure Files shares on hello main storage account.</span></span> <span data-ttu-id="d3fc4-165">當您刪除 hello 主要儲存體帳戶時，此內容會被刪除，且無法復原。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-165">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

> [!NOTE]
> <span data-ttu-id="d3fc4-166">當您使用的 blob 觸發程序消耗計劃時，可以有向上 tooa 10 分鐘的延遲處理新的 blob，如果函式應用程式已進入閒置狀態。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-166">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs if a function app has gone idle.</span></span> <span data-ttu-id="d3fc4-167">Hello 函式應用程式執行之後，blob 會立即處理。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-167">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="d3fc4-168">此初始 tooavoid 延遲，請考慮下列選項的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="d3fc4-168">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="d3fc4-169">使用 App Service 方案並啟用「永遠開啟」。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-169">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="d3fc4-170">使用處理，例如包含 hello blob 名稱的佇列訊息另一個的機制 tootrigger hello blob。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-170">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="d3fc4-171">如需範例，請參閱[具有 blob 輸入繫結的佇列觸發程序](functions-bindings-storage-blob.md#input-sample)。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-171">For an example, see [Queue trigger with blob input binding](functions-bindings-storage-blob.md#input-sample).</span></span>

### <a name="runtime-scaling"></a><span data-ttu-id="d3fc4-172">執行階段調整</span><span class="sxs-lookup"><span data-stu-id="d3fc4-172">Runtime scaling</span></span>

<span data-ttu-id="d3fc4-173">Azure 的函式會使用一種稱為 hello 元件*標尺控制器*toomonitor hello 事件的速率，並判斷是否 tooscale out 或向下調整。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-173">Azure Functions uses a component called hello *scale controller* toomonitor hello rate of events and determine whether tooscale out or scale down.</span></span> <span data-ttu-id="d3fc4-174">hello 標尺控制器會使用啟發學習法，每個觸發程序類型。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-174">hello scale controller uses heuristics for each trigger type.</span></span> <span data-ttu-id="d3fc4-175">例如，當您使用 Azure 佇列儲存體的觸發程序，它縮放根據 hello 佇列長度和 hello 最舊的佇列訊息的 hello 年齡。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-175">For example, when you're using an Azure Queue storage trigger, it scales based on hello queue length and hello age of hello oldest queue message.</span></span>

<span data-ttu-id="d3fc4-176">標尺的 hello 單位為 hello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-176">hello unit of scale is hello function app.</span></span> <span data-ttu-id="d3fc4-177">當 hello 函式應用程式會向外延展時，所需資源配置 toorun hello Azure 函式主控件的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-177">When hello function app is scaled out, more resources are allocated toorun multiple instances of hello Azure Functions host.</span></span> <span data-ttu-id="d3fc4-178">相反地，做為計算要求降低，hello 標尺控制器中移除函式主控件執行個體。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-178">Conversely, as compute demand is reduced, hello scale controller removes function host instances.</span></span> <span data-ttu-id="d3fc4-179">執行個體數目 hello 最終縮小 toozero 沒有函式函式的應用程式內執行時。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-179">hello number of instances is eventually scaled down toozero when no functions are running within a function app.</span></span>

![縮放控制器能監視事件及建立執行個體](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a><span data-ttu-id="d3fc4-181">計費模式</span><span class="sxs-lookup"><span data-stu-id="d3fc4-181">Billing model</span></span>

<span data-ttu-id="d3fc4-182">計費的詳細說明 hello 耗用量計劃在 hello [Azure 函式定價頁面]。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-182">Billing for hello Consumption plan is described in detail on hello [Azure Functions pricing page].</span></span> <span data-ttu-id="d3fc4-183">使用方式在 hello 函式應用程式層級彙總資料，並且計算只有 hello 函式程式碼正在執行的時間。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-183">Usage is aggregated at hello function app level and counts only hello time that function code is running.</span></span> <span data-ttu-id="d3fc4-184">hello 下面是計費單位：</span><span class="sxs-lookup"><span data-stu-id="d3fc4-184">hello following are units for billing:</span></span> 
* <span data-ttu-id="d3fc4-185">**以十億位元組-秒 (GB-s) 為單位的資源取用量**。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-185">**Resource consumption in gigabyte-seconds (GB-s)**.</span></span> <span data-ttu-id="d3fc4-186">會計算為在函數應用程式中執行之所有函式的記憶體大小和執行時間組合。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-186">Computed as a combination of memory size and execution time for all functions within a function app.</span></span> 
* <span data-ttu-id="d3fc4-187">**執行**。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-187">**Executions**.</span></span> <span data-ttu-id="d3fc4-188">計算每個函式會在回應 tooan 觸發的事件，繫結程序中執行的時間。</span><span class="sxs-lookup"><span data-stu-id="d3fc4-188">Counted each time a function is executed in response tooan event, triggered by a binding.</span></span>

[Azure 函式定價頁面]: https://azure.microsoft.com/pricing/details/functions
