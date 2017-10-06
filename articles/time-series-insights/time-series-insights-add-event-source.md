---
title: "aaaAdd 事件來源 tooyour Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "在此教學課程中，您要連接的事件來源 tooyour 時間數列 Insights 環境"
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
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="9d1cb-103">建立時間序列 Insights 環境使用 hello Ibiza 入口網站事件來源</span><span class="sxs-lookup"><span data-stu-id="9d1cb-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="9d1cb-104">Time Series Insights 事件來源衍生自事件代理程式，例如 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="9d1cb-105">時間序列 Insights 直接連接 tooEvent 來源，而不需要使用者 toowrite 一行程式碼擷取 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="9d1cb-106">目前，Time Series Insights 支援 Azure 事件中樞與 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="9d1cb-107">在未來的 hello，將會加入更多的事件來源。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="9d1cb-108">步驟 tooadd 事件來源 tooyour 環境</span><span class="sxs-lookup"><span data-stu-id="9d1cb-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="9d1cb-109">登入 toohello [Ibiza 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="9d1cb-110">按一下 [所有資源] 功能表中的 hello 左邊 hello hello Ibiza 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="9d1cb-111">選取 Time Series Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-111">Select your Time Series Insights environment.</span></span>

  ![建立 hello 時間數列 Insights 事件來源](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="9d1cb-113">選取 [事件來源]，按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![建立 hello 時間數列 Insights 事件來源的詳細資料](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="9d1cb-115">指定 hello hello 事件來源名稱。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="9d1cb-116">此名稱與來自此事件來源的所有事件相關聯，並可在查詢時使用。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="9d1cb-117">從事件中心中的資源 hello 目前訂用帳戶的 hello 清單中選取事件中心。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="9d1cb-118">否則選擇 匯入選項 」 提供事件中樞設定手動"toospecify 另一個訂用帳戶中的事件中心。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="9d1cb-119">事件必須以 JSON 格式發佈。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="9d1cb-120">選取具有讀取權限在 hello 事件中樞的原則。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="9d1cb-121">指定事件中樞取用者群組。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9d1cb-122">確定任何其他服務 (例如串流分析作業或其他 Time Series Insights 環境) 均未使用此取用者群組。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="9d1cb-123">如果取用者群組由其他服務，讀取作業造成負面影響此環境並 hello 其他服務。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="9d1cb-124">如果您使用 「 $Default"作為 hello 取用者群組，可能導致 toopotential 重複使用其他讀取器。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="9d1cb-125">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-125">Click “Create.”</span></span>

<span data-ttu-id="9d1cb-126">建立之後的 hello 事件來源，時間序列 Insights 將自動啟動資料流處理到您環境的資料。</span><span class="sxs-lookup"><span data-stu-id="9d1cb-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d1cb-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d1cb-127">Next steps</span></span>

* <span data-ttu-id="9d1cb-128">[傳送事件](time-series-insights-send-events.md)toohello 事件來源</span><span class="sxs-lookup"><span data-stu-id="9d1cb-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="9d1cb-129">在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中檢視您的環境</span><span class="sxs-lookup"><span data-stu-id="9d1cb-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
