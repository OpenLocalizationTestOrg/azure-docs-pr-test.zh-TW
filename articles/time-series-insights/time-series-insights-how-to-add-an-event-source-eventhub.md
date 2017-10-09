---
title: "aaaHow tooadd 事件中心事件來源 tooyour Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "本教學課程涵蓋如何 tooadd 事件也就是來源連接的 tooan 事件中心 tooyour 時間數列 Insights 環境"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a><span data-ttu-id="8537d-103">如何 tooadd 事件中心事件來源</span><span class="sxs-lookup"><span data-stu-id="8537d-103">How tooadd an Event Hub event source</span></span>

<span data-ttu-id="8537d-104">本教學課程涵蓋如何 toouse 會 hello Azure 入口網站 tooadd 從事件中心 tooyour 時間數列 Insights 環境中讀取事件來源。</span><span class="sxs-lookup"><span data-stu-id="8537d-104">This tutorial covers how toouse hello Azure portal tooadd an event source that reads from an Event Hub tooyour Time Series Insights environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8537d-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="8537d-105">Prerequisites</span></span>

<span data-ttu-id="8537d-106">您已建立事件中心，並在撰寫事件 tooit。</span><span class="sxs-lookup"><span data-stu-id="8537d-106">You have created an Event Hub and are writing events tooit.</span></span> <span data-ttu-id="8537d-107">如需有關事件中樞的詳細資訊，請參閱 <https://azure.microsoft.com/services/event-hubs/></span><span class="sxs-lookup"><span data-stu-id="8537d-107">For more information on Event Hubs, see <https://azure.microsoft.com/services/event-hubs/></span></span>

> <span data-ttu-id="8537d-108">[取用者群組]每個時間序列 Insights 事件來源必須 toohave 未與任何其他取用者共用其自己專用的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="8537d-108">[Consumer Groups] Each Time Series Insights event source needs toohave its own dedicated consumer group that is not shared with any other consumers.</span></span> <span data-ttu-id="8537d-109">如果多個讀取器會使用來自事件 hello 相同取用者群組，所有的讀取器都可能 toosee 失敗。</span><span class="sxs-lookup"><span data-stu-id="8537d-109">If multiple readers consume events from hello same consumer group, all readers are likely toosee failures.</span></span> <span data-ttu-id="8537d-110">請注意，每一個事件中樞另外還有 20 個用戶群組的限制。</span><span class="sxs-lookup"><span data-stu-id="8537d-110">Note that there is also a limit of 20 consumer groups per Event Hub.</span></span> <span data-ttu-id="8537d-111">如需詳細資訊，請參閱 hello[事件中心程式設計指南](../event-hubs/event-hubs-programming-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="8537d-111">For details, see hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span>

## <a name="choose-an-import-option"></a><span data-ttu-id="8537d-112">選擇匯入選項</span><span class="sxs-lookup"><span data-stu-id="8537d-112">Choose an Import option</span></span>

<span data-ttu-id="8537d-113">您可以手動輸入 hello hello 事件來源的設定或事件中心可以選取從可用 tooyou 的 hello 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="8537d-113">hello settings for hello event source can be entered manually or an event hub can be selected from hello event hubs that are available tooyou.</span></span>
<span data-ttu-id="8537d-114">在 hello**匯入選項**選取器選擇其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="8537d-114">In hello **Import Option** selector, choose one of hello following options:</span></span>

* <span data-ttu-id="8537d-115">手動提供事件中樞設定</span><span class="sxs-lookup"><span data-stu-id="8537d-115">Provide Event Hub settings manually</span></span>
* <span data-ttu-id="8537d-116">從可用的訂用帳戶使用事件中樞</span><span class="sxs-lookup"><span data-stu-id="8537d-116">Use Event Hub from available subscriptions</span></span>

### <a name="select-an-available-event-hub"></a><span data-ttu-id="8537d-117">選取可用的事件中樞</span><span class="sxs-lookup"><span data-stu-id="8537d-117">Select an available Event Hub</span></span>

<span data-ttu-id="8537d-118">hello 下表說明包含其描述的 hello 新的事件來源 索引標籤中的每個選項做為事件來源中選取可用的事件中樞時：</span><span class="sxs-lookup"><span data-stu-id="8537d-118">hello following table explains each option in hello New Event Source tab with its description when selecting an available Event Hub as an event source:</span></span>

| <span data-ttu-id="8537d-119">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="8537d-119">PROPERTY NAME</span></span> | <span data-ttu-id="8537d-120">說明</span><span class="sxs-lookup"><span data-stu-id="8537d-120">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="8537d-121">事件來源名稱</span><span class="sxs-lookup"><span data-stu-id="8537d-121">Event source name</span></span> | <span data-ttu-id="8537d-122">hello 事件來源名稱。</span><span class="sxs-lookup"><span data-stu-id="8537d-122">hello name of your event source.</span></span> <span data-ttu-id="8537d-123">此名稱在 Time Series Insights 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="8537d-123">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="8537d-124">來源</span><span class="sxs-lookup"><span data-stu-id="8537d-124">Source</span></span> | <span data-ttu-id="8537d-125">選擇**事件中心**toocreate 事件中心事件來源。</span><span class="sxs-lookup"><span data-stu-id="8537d-125">Choose **Event Hub** toocreate an Event Hub event source.</span></span>
| <span data-ttu-id="8537d-126">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="8537d-126">Subscription Id</span></span> | <span data-ttu-id="8537d-127">選取在其中建立此事件中心的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8537d-127">Select hello subscription in which this event hub was created.</span></span>
| <span data-ttu-id="8537d-128">服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="8537d-128">Service bus namespace</span></span> | <span data-ttu-id="8537d-129">選取包含 hello 事件中心的 hello 服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="8537d-129">Select hello Service Bus namespace that contains hello Event Hub.</span></span>
| <span data-ttu-id="8537d-130">事件中樞名稱</span><span class="sxs-lookup"><span data-stu-id="8537d-130">Event hub name</span></span> | <span data-ttu-id="8537d-131">選取 hello hello 事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="8537d-131">Select hello name of hello Event Hub.</span></span>
| <span data-ttu-id="8537d-132">事件中樞原則名稱</span><span class="sxs-lookup"><span data-stu-id="8537d-132">Event hub policy name</span></span> | <span data-ttu-id="8537d-133">選取 hello 共用存取原則，可以建立 hello 事件中樞設定 索引標籤。每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="8537d-133">Select hello shared access policy, which can be created on hello Event Hub Configure tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="8537d-134">hello 共用存取原則的事件來源*必須*有**讀取**權限。</span><span class="sxs-lookup"><span data-stu-id="8537d-134">hello shared access policy for your event source *must* have **read** permissions.</span></span>
| <span data-ttu-id="8537d-135">事件中樞取用者群組</span><span class="sxs-lookup"><span data-stu-id="8537d-135">Event hub consumer group</span></span> | <span data-ttu-id="8537d-136">hello hello 事件中樞取用者群組 tooread 事件。</span><span class="sxs-lookup"><span data-stu-id="8537d-136">hello Consumer Group tooread events from hello Event Hub.</span></span> <span data-ttu-id="8537d-137">它強烈建議 toouse 事件來源的專用的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="8537d-137">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

### <a name="provide-event-hub-settings-manually"></a><span data-ttu-id="8537d-138">手動提供事件中樞設定</span><span class="sxs-lookup"><span data-stu-id="8537d-138">Provide Event Hub settings manually</span></span>

<span data-ttu-id="8537d-139">hello 下列資料表說明 hello 其描述與新的事件來源 索引標籤中的每個屬性輸入的設定時以手動方式：</span><span class="sxs-lookup"><span data-stu-id="8537d-139">hello following table explains each property in hello New Event Source tab with its description when entering settings manually:</span></span>

| <span data-ttu-id="8537d-140">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="8537d-140">PROPERTY NAME</span></span> | <span data-ttu-id="8537d-141">說明</span><span class="sxs-lookup"><span data-stu-id="8537d-141">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="8537d-142">事件來源名稱</span><span class="sxs-lookup"><span data-stu-id="8537d-142">Event source name</span></span> | <span data-ttu-id="8537d-143">hello 事件來源名稱。</span><span class="sxs-lookup"><span data-stu-id="8537d-143">hello name of your event source.</span></span> <span data-ttu-id="8537d-144">此名稱在 Time Series Insights 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="8537d-144">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="8537d-145">來源</span><span class="sxs-lookup"><span data-stu-id="8537d-145">Source</span></span> | <span data-ttu-id="8537d-146">選擇**事件中心**toocreate 事件中心事件來源。</span><span class="sxs-lookup"><span data-stu-id="8537d-146">Choose **Event Hub** toocreate an Event Hub event source.</span></span>
| <span data-ttu-id="8537d-147">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="8537d-147">Subscription Id</span></span> | <span data-ttu-id="8537d-148">在其中建立此事件中心的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8537d-148">hello subscription in which this event hub was created.</span></span>
| <span data-ttu-id="8537d-149">資源群組</span><span class="sxs-lookup"><span data-stu-id="8537d-149">Resource group</span></span> | <span data-ttu-id="8537d-150">在其中建立此事件中心的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8537d-150">hello subscription in which this event hub was created.</span></span>
| <span data-ttu-id="8537d-151">服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="8537d-151">Service bus namespace</span></span> | <span data-ttu-id="8537d-152">服務匯流排命名空間是一個容器，包含一組訊息實體。</span><span class="sxs-lookup"><span data-stu-id="8537d-152">A Service Bus namespace is a container for a set of messaging entities.</span></span> <span data-ttu-id="8537d-153">建立新的事件中樞時，也會建立服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="8537d-153">When you created a new Event Hub, you also created a Service Bus namespace.</span></span>
| <span data-ttu-id="8537d-154">事件中樞名稱</span><span class="sxs-lookup"><span data-stu-id="8537d-154">Event hub name</span></span> | <span data-ttu-id="8537d-155">hello 的事件中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="8537d-155">hello name of your Event Hub.</span></span> <span data-ttu-id="8537d-156">當您建立事件中心時，您也會指定特定名稱</span><span class="sxs-lookup"><span data-stu-id="8537d-156">When you created your event hub, you also gave it a specific name</span></span>
| <span data-ttu-id="8537d-157">事件中樞原則名稱</span><span class="sxs-lookup"><span data-stu-id="8537d-157">Event hub policy name</span></span> | <span data-ttu-id="8537d-158">hello 共用的存取原則，可以建立 hello 事件中樞設定 索引標籤。每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="8537d-158">hello shared access policy, which can be created on hello Event Hub Configure tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="8537d-159">hello 共用存取原則的事件來源*必須*有**讀取**權限。</span><span class="sxs-lookup"><span data-stu-id="8537d-159">hello shared access policy for your event source *must* have **read** permissions.</span></span>
| <span data-ttu-id="8537d-160">事件中樞原則金鑰</span><span class="sxs-lookup"><span data-stu-id="8537d-160">Event hub policy key</span></span> | <span data-ttu-id="8537d-161">使用 tooauthenticate 存取 toohello 服務匯流排命名空間的 hello 共用存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="8537d-161">hello Shared Access key used tooauthenticate access toohello Service Bus namespace.</span></span> <span data-ttu-id="8537d-162">輸入 hello 主要或次要金鑰這裡。</span><span class="sxs-lookup"><span data-stu-id="8537d-162">Type hello primary or secondary key here.</span></span>
| <span data-ttu-id="8537d-163">事件中樞取用者群組</span><span class="sxs-lookup"><span data-stu-id="8537d-163">Event hub consumer group</span></span> | <span data-ttu-id="8537d-164">hello hello 事件中樞取用者群組 tooread 事件。</span><span class="sxs-lookup"><span data-stu-id="8537d-164">hello Consumer Group tooread events from hello Event Hub.</span></span> <span data-ttu-id="8537d-165">它強烈建議 toouse 事件來源的專用的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="8537d-165">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8537d-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8537d-166">Next steps</span></span>

1. <span data-ttu-id="8537d-167">新增資料存取原則 tooyour 環境[定義資料存取原則](time-series-insights-data-access.md)</span><span class="sxs-lookup"><span data-stu-id="8537d-167">Add a data access policy tooyour environment [Define data access policies](time-series-insights-data-access.md)</span></span>
1. <span data-ttu-id="8537d-168">存取您的環境中 hello[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="8537d-168">Access your environment in hello [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
