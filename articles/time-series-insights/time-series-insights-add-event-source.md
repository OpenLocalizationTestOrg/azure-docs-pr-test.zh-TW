---
title: "將事件來源新增至 Azure Time Series Insights 環境 | Microsoft Docs"
description: "在本教學課程中，您會將事件來源連線至 Time Series Insights 環境"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: ffa2eaf3680e68ac14aabf49b6308caeb173fd43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="b9b19-103">使用 Ibiza 入口網站建立 Time Series Insights 環境的事件來源</span><span class="sxs-lookup"><span data-stu-id="b9b19-103">Create an event source for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="b9b19-104">Time Series Insights 事件來源衍生自事件代理程式，例如 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="b9b19-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="b9b19-105">Time Series Insights 會直接連線到事件來源，並內嵌資料流，而不需要使用者撰寫一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="b9b19-105">Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code.</span></span> <span data-ttu-id="b9b19-106">目前，Time Series Insights 支援 Azure 事件中樞與 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b9b19-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="b9b19-107">未來將會新增更多事件來源。</span><span class="sxs-lookup"><span data-stu-id="b9b19-107">In the future, more Event Sources will be added.</span></span>

## <a name="steps-to-add-an-event-source-to-your-environment"></a><span data-ttu-id="b9b19-108">將事件來源新增至您的環境的步驟</span><span class="sxs-lookup"><span data-stu-id="b9b19-108">Steps to add an event source to your environment</span></span>

1.  <span data-ttu-id="b9b19-109">登入 [Ibiza 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b9b19-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="b9b19-110">按一下 Ibiza 入口網站左側功能表中的 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="b9b19-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3.  <span data-ttu-id="b9b19-111">選取 Time Series Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="b9b19-111">Select your Time Series Insights environment.</span></span>

  ![建立 Time Series Insights 事件來源](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="b9b19-113">選取 [事件來源]，按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="b9b19-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![建立 Time Series Insights 事件來源 - 詳細資料](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="b9b19-115">指定事件來源的名稱。</span><span class="sxs-lookup"><span data-stu-id="b9b19-115">Specify the name of the event source.</span></span> <span data-ttu-id="b9b19-116">此名稱與來自此事件來源的所有事件相關聯，並可在查詢時使用。</span><span class="sxs-lookup"><span data-stu-id="b9b19-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="b9b19-117">從目前訂用帳戶的事件中樞資源清單選取事件中樞。</span><span class="sxs-lookup"><span data-stu-id="b9b19-117">Select an event hub from the list of Event Hub resources in the current subscription.</span></span> <span data-ttu-id="b9b19-118">否則請選擇匯入選項「手動提供事件中樞設定」來指定另一個訂用帳戶的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="b9b19-118">Otherwise choose import option "Provide Event Hub settings manually” to specify an event hub in another subscription.</span></span> <span data-ttu-id="b9b19-119">事件必須以 JSON 格式發佈。</span><span class="sxs-lookup"><span data-stu-id="b9b19-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="b9b19-120">選取具有事件中樞讀取權限的原則。</span><span class="sxs-lookup"><span data-stu-id="b9b19-120">Select policy that has read permission in the event hub.</span></span>
8.  <span data-ttu-id="b9b19-121">指定事件中樞取用者群組。</span><span class="sxs-lookup"><span data-stu-id="b9b19-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b9b19-122">確定任何其他服務 (例如串流分析作業或其他 Time Series Insights 環境) 均未使用此取用者群組。</span><span class="sxs-lookup"><span data-stu-id="b9b19-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="b9b19-123">如果有其他服務使用此取用者群組，讀取作業會對此環境和其他服務造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="b9b19-123">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="b9b19-124">如果您使用 “$Default” 作為取用者群組，有可能會導致其他讀取者重複使用。</span><span class="sxs-lookup"><span data-stu-id="b9b19-124">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

9.  <span data-ttu-id="b9b19-125">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b9b19-125">Click “Create.”</span></span>

<span data-ttu-id="b9b19-126">建立事件來源之後，Time Series Insights 會自動開始將資料串流處理至您的環境。</span><span class="sxs-lookup"><span data-stu-id="b9b19-126">After creation of the event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9b19-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9b19-127">Next steps</span></span>

* <span data-ttu-id="b9b19-128">[將事件傳送](time-series-insights-send-events.md)到事件來源</span><span class="sxs-lookup"><span data-stu-id="b9b19-128">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="b9b19-129">在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中檢視您的環境</span><span class="sxs-lookup"><span data-stu-id="b9b19-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
