---
title: "aaaCreate Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "在本教學課程中，您將學習如何 toocreate 時間數列環境中，將它連接 tooan 事件來源和準備 tooanalyze 事件資料，以分鐘為單位。"
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="863c5-103">在 hello Azure 入口網站中建立新的時間序列 Insights 環境</span><span class="sxs-lookup"><span data-stu-id="863c5-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="863c5-104">Time Series Insights 環境是具有輸入和儲存容量的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="863c5-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="863c5-105">客戶會使用所需的 hello 容量佈建透過 hello Azure 入口網站的環境。</span><span class="sxs-lookup"><span data-stu-id="863c5-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="863c5-106">步驟 toocreate hello 環境</span><span class="sxs-lookup"><span data-stu-id="863c5-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="863c5-107">請遵循這些步驟 toocreate 您的環境：</span><span class="sxs-lookup"><span data-stu-id="863c5-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="863c5-108">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="863c5-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="863c5-109">按一下 hello 加上正負號 （"+"） 中的 hello 左上角。</span><span class="sxs-lookup"><span data-stu-id="863c5-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="863c5-110">搜尋 「 時間序列見解"hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="863c5-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![建立 hello 時間數列 Insights 環境](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="863c5-112">選取 [Time Series Insights]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="863c5-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![建立 hello 時間數列 Insights 資源群組](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="863c5-114">指定環境名稱。</span><span class="sxs-lookup"><span data-stu-id="863c5-114">Specify environment name.</span></span> <span data-ttu-id="863c5-115">這個名稱會表示中的 hello 環境[時間數列總管](https://insights.timeseries.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="863c5-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="863c5-116">選取一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="863c5-116">Select a subscription.</span></span> <span data-ttu-id="863c5-117">請選擇包含事件來源的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="863c5-117">Choose one that contains your event source.</span></span> <span data-ttu-id="863c5-118">時間序列 Insights 可自動偵測 Azure IoT 中樞，並在現有的事件中樞資源 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="863c5-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="863c5-119">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="863c5-119">Select or create a resource group.</span></span> <span data-ttu-id="863c5-120">資源群組是一起使用之 Azure 資源的集合。</span><span class="sxs-lookup"><span data-stu-id="863c5-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="863c5-121">選取裝載位置。</span><span class="sxs-lookup"><span data-stu-id="863c5-121">Select a hosting location.</span></span> <span data-ttu-id="863c5-122">tooavoid 移動資料在資料中心中，選擇包含您的事件來源的位置。</span><span class="sxs-lookup"><span data-stu-id="863c5-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="863c5-123">選取定價層。</span><span class="sxs-lookup"><span data-stu-id="863c5-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="863c5-124">選取容量。</span><span class="sxs-lookup"><span data-stu-id="863c5-124">Select capacity.</span></span> <span data-ttu-id="863c5-125">您可以在環境建立後變更其容量。</span><span class="sxs-lookup"><span data-stu-id="863c5-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="863c5-126">建立您的環境。</span><span class="sxs-lookup"><span data-stu-id="863c5-126">Create your environment.</span></span> <span data-ttu-id="863c5-127">每當您登入，您也可以釘選環境 toohello 儀表板，以方便存取。</span><span class="sxs-lookup"><span data-stu-id="863c5-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![建立 hello 時間數列 Insights pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="863c5-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="863c5-129">Next steps</span></span>

* <span data-ttu-id="863c5-130">[定義資料存取原則](time-series-insights-data-access.md)tooaccess 您的環境中[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="863c5-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="863c5-131">建立事件來源</span><span class="sxs-lookup"><span data-stu-id="863c5-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="863c5-132">[傳送事件](time-series-insights-send-events.md)toohello 事件來源</span><span class="sxs-lookup"><span data-stu-id="863c5-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
