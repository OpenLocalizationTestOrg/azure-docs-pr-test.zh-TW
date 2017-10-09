---
title: "aaaAzure 事件方格概觀"
description: "說明 Azure Event Grid 與其概念。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="303d6-103">簡介 tooAzure 事件方格</span><span class="sxs-lookup"><span data-stu-id="303d6-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="303d6-104">Azure 事件方格可讓您以事件為基礎的架構 tooeasily 建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="303d6-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="303d6-105">您選取 hello Azure 資源，toosubscribe，然後授與 hello 事件處理常式或 WebHook 端點 toosend hello 事件。</span><span class="sxs-lookup"><span data-stu-id="303d6-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="303d6-106">對於來自 Azure 服務 (例如儲存體 Blob 和資源群組) 的事件，Event Grid 內建了支援功能。</span><span class="sxs-lookup"><span data-stu-id="303d6-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="303d6-107">對於應用程式和第三方的事件，Event Grid 也使用了自訂主題和自訂 Webhook 來提供自訂支援。</span><span class="sxs-lookup"><span data-stu-id="303d6-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="303d6-108">您可以使用篩選器 tooroute 特定事件 toodifferent 端點，多點傳送的 toomultiple 端點，並確定您的事件會可靠地傳遞。</span><span class="sxs-lookup"><span data-stu-id="303d6-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="303d6-109">Event Grid 也針對自訂和第三方的事件提供了內建支援。</span><span class="sxs-lookup"><span data-stu-id="303d6-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="303d6-110">Hello 預覽版本，支援事件方格**westus2**和**westcentralus**位置。</span><span class="sxs-lookup"><span data-stu-id="303d6-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="303d6-111">未來將會新增其他區域。</span><span class="sxs-lookup"><span data-stu-id="303d6-111">Other regions will be added.</span></span>

<span data-ttu-id="303d6-112">本文提供 Azure Event Grid 的概觀。</span><span class="sxs-lookup"><span data-stu-id="303d6-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="303d6-113">如果您想 tooget 與事件方格啟動，請參閱[建立和路由的自訂事件，與 Azure 事件方格](custom-event-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="303d6-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Event Grid 運作模型](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="303d6-115">目前，Blob 儲存體未公開作為發行者。</span><span class="sxs-lookup"><span data-stu-id="303d6-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="303d6-116">概念</span><span class="sxs-lookup"><span data-stu-id="303d6-116">Concepts</span></span>

<span data-ttu-id="303d6-117">Azure Event Grid 中有五個概念可讓您開始進行：</span><span class="sxs-lookup"><span data-stu-id="303d6-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="303d6-118">**事件** - 發生了什麼事。</span><span class="sxs-lookup"><span data-stu-id="303d6-118">**Events** - What happened.</span></span>
* <span data-ttu-id="303d6-119">**事件來源發行者**-hello 事件發生。</span><span class="sxs-lookup"><span data-stu-id="303d6-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="303d6-120">**主題**-hello 的端點的 「 發行者 」 傳送事件的位置。</span><span class="sxs-lookup"><span data-stu-id="303d6-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="303d6-121">**事件訂閱**-hello 端點或內建機制 tooroute 事件，有時候 toomultiple 處理常式。</span><span class="sxs-lookup"><span data-stu-id="303d6-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="303d6-122">訂用帳戶也會使用處理常式 toointelligently 篩選內送事件。</span><span class="sxs-lookup"><span data-stu-id="303d6-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="303d6-123">**事件處理常式**-hello 應用程式或服務對回應 toohello 事件。</span><span class="sxs-lookup"><span data-stu-id="303d6-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="303d6-124">如需這些概念的詳細資訊，請參閱 [Azure Event Grid 中的概念](concepts.md)。</span><span class="sxs-lookup"><span data-stu-id="303d6-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="303d6-125">功能</span><span class="sxs-lookup"><span data-stu-id="303d6-125">Capabilities</span></span>

<span data-ttu-id="303d6-126">以下是一些 Azure 事件方格的 hello 重要功能：</span><span class="sxs-lookup"><span data-stu-id="303d6-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="303d6-127">**為了簡單起見**-從您的 Azure 資源 tooany 事件處理常式或端點的點，並按一下 tooaim 事件。</span><span class="sxs-lookup"><span data-stu-id="303d6-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="303d6-128">**進階篩選**-篩選事件類型或事件發行路徑 tooensure 事件處理常式只會接收相關的事件。</span><span class="sxs-lookup"><span data-stu-id="303d6-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="303d6-129">**展開傳送**-訂閱多個端點 toohello 相同事件 toosend 複製 hello 事件 tooas 的許多地方視。</span><span class="sxs-lookup"><span data-stu-id="303d6-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="303d6-130">**可靠性**-利用使用指數型輪詢 tooensure 事件傳遞的 24 小時重試。</span><span class="sxs-lookup"><span data-stu-id="303d6-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="303d6-131">**支付每一個事件**-付費 hello 數量僅供您使用事件方格。</span><span class="sxs-lookup"><span data-stu-id="303d6-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="303d6-132">**高輸送量** - 在每秒支援數百萬個事件的 Event Grid 上建置大量的工作負載。</span><span class="sxs-lookup"><span data-stu-id="303d6-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="303d6-133">**內建事件** - 利用資源定義的內建事件來快速地啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="303d6-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="303d6-134">**自訂事件** - 使用 Event Grid 路由、篩選並在應用程式中可靠地傳遞自訂事件。</span><span class="sxs-lookup"><span data-stu-id="303d6-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="303d6-135">內建的發行者和處理常式整合</span><span class="sxs-lookup"><span data-stu-id="303d6-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="303d6-136">Azure 使用多項服務 (包括發行者和處理常式) 來提供內建的事件支援。</span><span class="sxs-lookup"><span data-stu-id="303d6-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="303d6-137">發行者</span><span class="sxs-lookup"><span data-stu-id="303d6-137">Publishers</span></span>

<span data-ttu-id="303d6-138">目前，hello 下列 Azure 服務都有內建的 「 發行者 」 支援的事件方格：</span><span class="sxs-lookup"><span data-stu-id="303d6-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="303d6-139">資源群組 (管理作業)</span><span class="sxs-lookup"><span data-stu-id="303d6-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="303d6-140">Azure 訂用帳戶 (管理作業)</span><span class="sxs-lookup"><span data-stu-id="303d6-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="303d6-141">事件中樞</span><span class="sxs-lookup"><span data-stu-id="303d6-141">Event Hubs</span></span>
* <span data-ttu-id="303d6-142">自訂主題</span><span class="sxs-lookup"><span data-stu-id="303d6-142">Custom Topics</span></span>

<span data-ttu-id="303d6-143">今年將會新增其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="303d6-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="303d6-144">處理常式</span><span class="sxs-lookup"><span data-stu-id="303d6-144">Handlers</span></span>

<span data-ttu-id="303d6-145">目前，hello 下列 Azure 服務都有內建的處理常式的事件方格支援：</span><span class="sxs-lookup"><span data-stu-id="303d6-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="303d6-146">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="303d6-146">Azure Functions</span></span>
* <span data-ttu-id="303d6-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="303d6-147">Logic Apps</span></span>
* <span data-ttu-id="303d6-148">Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="303d6-148">Azure Automation</span></span>
* <span data-ttu-id="303d6-149">Webhook</span><span class="sxs-lookup"><span data-stu-id="303d6-149">WebHooks</span></span>

<span data-ttu-id="303d6-150">今年將會新增其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="303d6-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="303d6-151">我可以用 Event Grid 來做什麼？</span><span class="sxs-lookup"><span data-stu-id="303d6-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="303d6-152">Azure Event Grid 提供好幾種功能，可大幅提升無伺服器、作業自動化和整合工作：</span><span class="sxs-lookup"><span data-stu-id="303d6-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="303d6-153">無伺服器應用程式架構</span><span class="sxs-lookup"><span data-stu-id="303d6-153">Serverless application architectures</span></span>

![無伺服器應用程式](./media/overview/serverless_web_app.png)

<span data-ttu-id="303d6-155">Event Grid 可連線資料來源與事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="303d6-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="303d6-156">例如，使用事件方格 tooinstantly 觸發程序無伺服器函式 toorun 映像分析新相片是每次加入 tooa blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="303d6-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="303d6-157">作業自動化</span><span class="sxs-lookup"><span data-stu-id="303d6-157">Ops Automation</span></span>

![作業自動化](./media/overview/Ops_automation.png)

<span data-ttu-id="303d6-159">事件方格可讓您 toospeed 自動化，並簡化原則強制執行。</span><span class="sxs-lookup"><span data-stu-id="303d6-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="303d6-160">例如，Event Grid 可以在虛擬機器建立或 SQL Database 啟動時通知 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="303d6-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="303d6-161">可以使用這些事件 tooautomatically 檢查服務組態是否符合標準，將中繼資料放入作業的工具、 標記的虛擬機器或檔案的工作項目。</span><span class="sxs-lookup"><span data-stu-id="303d6-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="303d6-162">應用程式整合</span><span class="sxs-lookup"><span data-stu-id="303d6-162">Application integration</span></span>

![應用程式整合](./media/overview/app_integration.png)

<span data-ttu-id="303d6-164">Event Grid 可連線您的應用程式與其他服務。</span><span class="sxs-lookup"><span data-stu-id="303d6-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="303d6-165">比方說，您的應用程式事件資料 tooEvent 方格中，建立自訂主題 toosend 充分利用其可靠的傳遞，進階路由，並直接與 Azure 的整合。</span><span class="sxs-lookup"><span data-stu-id="303d6-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="303d6-166">或者，您可以使用的任何地方、 Logic Apps tooprocess 資料的事件方格，而不需要撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="303d6-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="303d6-167">Event Grid 與其他 Azure 整合服務有何不同？</span><span class="sxs-lookup"><span data-stu-id="303d6-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="303d6-168">Event Grid 是可供進行回應式事件導向程式設計的事件背板。</span><span class="sxs-lookup"><span data-stu-id="303d6-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="303d6-169">它不僅與 Azure 服務緊密整合，並可與第三方服務整合。</span><span class="sxs-lookup"><span data-stu-id="303d6-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="303d6-170">hello 事件訊息包含您需要 tooreact toochanges 服務和應用程式中的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="303d6-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="303d6-171">事件方格不是在資料管線，並不會傳遞 hello 已更新的實際物件。</span><span class="sxs-lookup"><span data-stu-id="303d6-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="303d6-172">服務匯流排很適合需要交易、排序、重複偵測和瞬間一致性的傳統企業應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="303d6-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="303d6-173">Event Grid 則是設計來為回應式模型提供速度、擴充性、廣度和低成本。</span><span class="sxs-lookup"><span data-stu-id="303d6-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="303d6-174">它是適合的 tooserverless 架構。</span><span class="sxs-lookup"><span data-stu-id="303d6-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="303d6-175">Event Grid 可彌補其他 Azure 服務 (例如 Logic Apps 和事件中樞) 的不足。</span><span class="sxs-lookup"><span data-stu-id="303d6-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="303d6-176">事件方格觸發程序 hello 邏輯應用程式 toobegin 其工作流程。</span><span class="sxs-lookup"><span data-stu-id="303d6-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="303d6-177">事件中心會讓您從事件中心擷取並建置資料輸入和轉換管線 tooreact tooevents 搭配事件方格。</span><span class="sxs-lookup"><span data-stu-id="303d6-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="303d6-178">Event Grid 的費用有多少？</span><span class="sxs-lookup"><span data-stu-id="303d6-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="303d6-179">Azure Event Grid 使用依事件支付計價模式，因此您只需就使用量來付費。</span><span class="sxs-lookup"><span data-stu-id="303d6-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="303d6-180">事件方格成本 $0.60 每百萬個作業 (0.30 美元在預覽期間)，而且可用 hello 每月的第一次 100,000 作業。</span><span class="sxs-lookup"><span data-stu-id="303d6-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="303d6-181">作業的定義是事件輸入、進階比對、傳遞嘗試及管理呼叫。</span><span class="sxs-lookup"><span data-stu-id="303d6-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="303d6-182">更多詳細資料位於 hello[定價頁面](https://azure.microsoft.com/pricing/details/event-grid/)。</span><span class="sxs-lookup"><span data-stu-id="303d6-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="303d6-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="303d6-183">Next steps</span></span>

* <span data-ttu-id="303d6-184">[建立並訂閱 toocustom 事件](custom-event-quickstart.md)直接並開始傳送您自己的自訂事件 tooany 端點使用 hello Azure 事件方格快速入門。</span><span class="sxs-lookup"><span data-stu-id="303d6-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="303d6-185">[使用邏輯應用程式做為事件處理常式](monitor-virtual-machine-changes-event-grid-logic-app.md)的教學課程建置應用程式使用 Logic Apps tooreact tooevents 推入的事件方格。</span><span class="sxs-lookup"><span data-stu-id="303d6-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="303d6-186">Event Grid REST API 參考</span><span class="sxs-lookup"><span data-stu-id="303d6-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="303d6-187">提供管理事件訂閱 hello Azure 事件方格中的其他技術資訊和參考路由及篩選。</span><span class="sxs-lookup"><span data-stu-id="303d6-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
