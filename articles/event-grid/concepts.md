---
title: "aaaAzure 事件方格概念"
description: "說明 Azure Event Grid 與其概念。 定義 Event Grid 的數個重要元件。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a><span data-ttu-id="71c3a-104">Azure Event Grid 中的概念</span><span class="sxs-lookup"><span data-stu-id="71c3a-104">Concepts in Azure Event Grid</span></span>

<span data-ttu-id="71c3a-105">hello Azure 事件方格中的主要概念如下：</span><span class="sxs-lookup"><span data-stu-id="71c3a-105">hello main concepts in Azure Event Grid are:</span></span>

## <a name="events"></a><span data-ttu-id="71c3a-106">事件</span><span class="sxs-lookup"><span data-stu-id="71c3a-106">Events</span></span>

<span data-ttu-id="71c3a-107">事件是資訊的 hello 小量的完整描述的項目發生 hello 系統中。</span><span class="sxs-lookup"><span data-stu-id="71c3a-107">An event is hello smallest amount of information that fully describes something that happened in hello system.</span></span>  <span data-ttu-id="71c3a-108">每個事件都有類似的一般資訊： hello 事件時間 hello 事件的來源所需的位置，以及唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="71c3a-108">Every event has common information like: source of hello event, time hello event took place, and unique identifier.</span></span>  <span data-ttu-id="71c3a-109">每個事件也會有相關 toohello 特定事件的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="71c3a-109">Every event also has specific information that is only relevant toohello specific event.</span></span> <span data-ttu-id="71c3a-110">例如，在 Azure 儲存體中建立新檔案的相關事件包含 hello 檔案，例如 hello lastTimeModified 值詳細資料。</span><span class="sxs-lookup"><span data-stu-id="71c3a-110">For example, an event about a new file being created in Azure Storage contains details about hello file, such as hello lastTimeModified value.</span></span> <span data-ttu-id="71c3a-111">或者，關於虛擬機器重新開機事件包含 hello 名稱 hello 虛擬機器，以及重新開機的 hello 原因。</span><span class="sxs-lookup"><span data-stu-id="71c3a-111">Or, an event about a virtual machine rebooting contains hello name of hello virtual machine, and hello reason for reboot.</span></span>

## <a name="event-sourcespublishers"></a><span data-ttu-id="71c3a-112">事件來源/發行者</span><span class="sxs-lookup"><span data-stu-id="71c3a-112">Event sources/publishers</span></span>

<span data-ttu-id="71c3a-113">事件來源是 hello 事件發生時的所在。</span><span class="sxs-lookup"><span data-stu-id="71c3a-113">An event source is where hello event happens.</span></span> <span data-ttu-id="71c3a-114">例如，Azure 儲存體是 hello blob 建立事件的事件來源。</span><span class="sxs-lookup"><span data-stu-id="71c3a-114">For example, Azure Storage is hello event source for blob created events.</span></span> <span data-ttu-id="71c3a-115">Azure VM 網狀架構是 hello 事件來源虛擬機器的事件。</span><span class="sxs-lookup"><span data-stu-id="71c3a-115">Azure VM Fabric is hello event source for virtual machine events.</span></span> <span data-ttu-id="71c3a-116">事件來源負責發佈事件 tooEvent 方格。</span><span class="sxs-lookup"><span data-stu-id="71c3a-116">Event sources are responsible for publishing events tooEvent Grid.</span></span>

## <a name="topics"></a><span data-ttu-id="71c3a-117">主題</span><span class="sxs-lookup"><span data-stu-id="71c3a-117">Topics</span></span>

<span data-ttu-id="71c3a-118">發行者將事件分類成各主題。</span><span class="sxs-lookup"><span data-stu-id="71c3a-118">Publishers categorize events into topics.</span></span> <span data-ttu-id="71c3a-119">hello 主題包含 hello 發行者將事件的傳送位置的端點。</span><span class="sxs-lookup"><span data-stu-id="71c3a-119">hello topic includes an endpoint where hello publisher sends events.</span></span> <span data-ttu-id="71c3a-120">toorespond toocertain 類型的事件，「 訂閱者 」 會決定要哪些主題 toosubscribe。</span><span class="sxs-lookup"><span data-stu-id="71c3a-120">toorespond toocertain types of events, subscribers decide which topics toosubscribe to.</span></span> <span data-ttu-id="71c3a-121">主題也提供事件結構描述，以便 「 訂閱者 」 可以探索如何 tooconsume hello 事件適當。</span><span class="sxs-lookup"><span data-stu-id="71c3a-121">Topics also provide an event schema so that subscribers can discover how tooconsume hello events appropriately.</span></span>

<span data-ttu-id="71c3a-122">系統主題是由 Azure 服務提供的內建主題。</span><span class="sxs-lookup"><span data-stu-id="71c3a-122">System topics are built-in topics provided by Azure services.</span></span> <span data-ttu-id="71c3a-123">自訂主題是應用程式和協力廠商的主題。</span><span class="sxs-lookup"><span data-stu-id="71c3a-123">Custom topics are application and third-party topics.</span></span>

## <a name="event-subscriptions"></a><span data-ttu-id="71c3a-124">事件訂閱</span><span class="sxs-lookup"><span data-stu-id="71c3a-124">Event subscriptions</span></span>

<span data-ttu-id="71c3a-125">訂用帳戶指示 Event Grid 訂閱者有興趣接收主題上的何種事件。</span><span class="sxs-lookup"><span data-stu-id="71c3a-125">A subscription instructs Event Grid on which events on a topic a subscriber is interested in receiving.</span></span>  <span data-ttu-id="71c3a-126">訂用帳戶也會包含有關如何事件應傳遞 toohello 訂閱者。</span><span class="sxs-lookup"><span data-stu-id="71c3a-126">A subscription also holds information on how events should be delivered toohello subscriber.</span></span>

## <a name="event-handlers"></a><span data-ttu-id="71c3a-127">事件處理常式</span><span class="sxs-lookup"><span data-stu-id="71c3a-127">Event handlers</span></span>

<span data-ttu-id="71c3a-128">從事件方格的觀點而言，事件處理常式會是 hello 位置的傳送嗨事件。</span><span class="sxs-lookup"><span data-stu-id="71c3a-128">From an Event Grid perspective, an event handler is hello place where hello event is sent.</span></span> <span data-ttu-id="71c3a-129">hello 處理常式會接受一些進一步的動作 tooprocess hello 事件。</span><span class="sxs-lookup"><span data-stu-id="71c3a-129">hello handler takes some further action tooprocess hello event.</span></span>  <span data-ttu-id="71c3a-130">Event Grid 支援多個訂閱者類型。</span><span class="sxs-lookup"><span data-stu-id="71c3a-130">Event Grid supports multiple subscriber types.</span></span> <span data-ttu-id="71c3a-131">Hello 的訂閱者的類型，根據事件方格會遵循不同的機制 tooguarantee hello 傳遞 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="71c3a-131">Depending on hello type of subscriber, Event Grid follows different mechanisms tooguarantee hello delivery of hello event.</span></span>  <span data-ttu-id="71c3a-132">HTTP webhook 事件處理常式的 hello 事件會重試直到 hello 處理常式會傳回狀態碼`200 – OK`。</span><span class="sxs-lookup"><span data-stu-id="71c3a-132">For HTTP webhook event handlers, hello event is retried until hello handler returns a status code of `200 – OK`.</span></span> <span data-ttu-id="71c3a-133">Azure 儲存體佇列，直到 hello 佇列服務無法 toosuccessfully 程序 hello 訊息發送到 hello 佇列，會重試 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="71c3a-133">For Azure Storage Queue, hello events are retried until hello Queue service is able toosuccessfully process hello message push into hello queue.</span></span>

## <a name="filters"></a><span data-ttu-id="71c3a-134">篩選器</span><span class="sxs-lookup"><span data-stu-id="71c3a-134">Filters</span></span>

<span data-ttu-id="71c3a-135">訂閱時 tooa 主題，您可以篩選 toohello 端點傳送的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="71c3a-135">When subscribing tooa topic, you can filter hello events that are sent toohello endpoint.</span></span> <span data-ttu-id="71c3a-136">您可以依事件類型或主旨模式進行篩選。</span><span class="sxs-lookup"><span data-stu-id="71c3a-136">You can filter by event type, or subject pattern.</span></span> <span data-ttu-id="71c3a-137">如需詳細資訊，請參閱 [Event Grid 訂用帳戶結構描述](subscription-creation-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="71c3a-137">For more information, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>

## <a name="security"></a><span data-ttu-id="71c3a-138">安全性</span><span class="sxs-lookup"><span data-stu-id="71c3a-138">Security</span></span>

<span data-ttu-id="71c3a-139">事件提供安全性訂閱 tootopics，和發佈主題。</span><span class="sxs-lookup"><span data-stu-id="71c3a-139">Event provides security for subscribing tootopics, and publishing topics.</span></span> <span data-ttu-id="71c3a-140">訂閱時，您必須在 hello 資源或主題上的適當權限。</span><span class="sxs-lookup"><span data-stu-id="71c3a-140">When subscribing, you must have adequate permissions on hello resource or topic.</span></span> <span data-ttu-id="71c3a-141">發行時，您必須具有 SAS 權杖或金鑰驗證 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="71c3a-141">When publishing, you must have a SAS token or key authentication for hello topic.</span></span> <span data-ttu-id="71c3a-142">如需詳細資訊，請參閱 [Event Grid 安全性和驗證](security-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="71c3a-142">For more information, see [Event Grid security and authentication](security-authentication.md).</span></span>

## <a name="failed-delivery"></a><span data-ttu-id="71c3a-143">傳遞失敗</span><span class="sxs-lookup"><span data-stu-id="71c3a-143">Failed delivery</span></span>

<span data-ttu-id="71c3a-144">當事件方格而無法確認 hello 訂閱者的端點已收到事件時，它會 redelivers hello 事件。</span><span class="sxs-lookup"><span data-stu-id="71c3a-144">When Event Grid cannot confirm that an event has been received by hello subscriber's endpoint, it redelivers hello event.</span></span> <span data-ttu-id="71c3a-145">如需詳細資訊，請參閱 [Event Grid 訊息傳遞與重試](delivery-and-retry.md)。</span><span class="sxs-lookup"><span data-stu-id="71c3a-145">For more information, see [Event Grid message delivery and retry](delivery-and-retry.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="71c3a-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71c3a-146">Next steps</span></span>

* <span data-ttu-id="71c3a-147">如簡介 tooEvent 格線，請參閱[有關事件方格](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="71c3a-147">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="71c3a-148">使用事件方格啟動 tooquickly，請參閱[建立和路由的自訂事件，與 Azure 事件方格](custom-event-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="71c3a-148">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
