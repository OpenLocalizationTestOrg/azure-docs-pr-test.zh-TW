---
title: "建立 Azure Time Series Insights 環境 | Microsoft Docs"
description: "在本教學課程中，您將了解如何迅速建立時間序列環境、將它連線到事件來源，以及做好準備以分析事件資料。"
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
ms.openlocfilehash: eb710795916a2d7beea75a6408a0982fb4dc8750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-time-series-insights-environment-in-the-azure-portal"></a><span data-ttu-id="13244-103">在 Azure 入口網站中建立新的 Time Series Insights 環境</span><span class="sxs-lookup"><span data-stu-id="13244-103">Create a new Time Series Insights environment in the Azure portal</span></span>

<span data-ttu-id="13244-104">Time Series Insights 環境是具有輸入和儲存容量的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="13244-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="13244-105">客戶需透過 Azure 入口網站來佈建環境和所需容量。</span><span class="sxs-lookup"><span data-stu-id="13244-105">Customers provision environments via the Azure portal with the required capacity.</span></span>

## <a name="steps-to-create-the-environment"></a><span data-ttu-id="13244-106">用以建立環境的步驟</span><span class="sxs-lookup"><span data-stu-id="13244-106">Steps to create the environment</span></span>

<span data-ttu-id="13244-107">請遵循下列步驟來建立環境：</span><span class="sxs-lookup"><span data-stu-id="13244-107">Follow these steps to create your environment:</span></span>

1.  <span data-ttu-id="13244-108">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="13244-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="13244-109">按一下左上角的加號 (“+”)。</span><span class="sxs-lookup"><span data-stu-id="13244-109">Click the plus sign (“+”) in the top left corner.</span></span>
3.  <span data-ttu-id="13244-110">在搜尋方塊中搜尋「Time Series Insights」。</span><span class="sxs-lookup"><span data-stu-id="13244-110">Search for “Time Series Insights” in the search box.</span></span>

  ![建立 Time Series Insights 環境](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="13244-112">選取 [Time Series Insights]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="13244-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![建立 Time Series Insights 資源群組](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="13244-114">指定環境名稱。</span><span class="sxs-lookup"><span data-stu-id="13244-114">Specify environment name.</span></span> <span data-ttu-id="13244-115">此名稱會代表[時間序列總管](https://insights.timeseries.azure.com)中的環境。</span><span class="sxs-lookup"><span data-stu-id="13244-115">This name will represent the environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="13244-116">選取一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="13244-116">Select a subscription.</span></span> <span data-ttu-id="13244-117">請選擇包含事件來源的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="13244-117">Choose one that contains your event source.</span></span> <span data-ttu-id="13244-118">Time Series Insights 可以自動偵測相同訂用帳戶中現有的 Azure IoT 中樞與事件中樞資源。</span><span class="sxs-lookup"><span data-stu-id="13244-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in the same subscription.</span></span>
7.  <span data-ttu-id="13244-119">選取或建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="13244-119">Select or create a resource group.</span></span> <span data-ttu-id="13244-120">資源群組是一起使用之 Azure 資源的集合。</span><span class="sxs-lookup"><span data-stu-id="13244-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="13244-121">選取裝載位置。</span><span class="sxs-lookup"><span data-stu-id="13244-121">Select a hosting location.</span></span> <span data-ttu-id="13244-122">若要避免在資料中心之間移動資料，請選擇事件來源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="13244-122">To avoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="13244-123">選取定價層。</span><span class="sxs-lookup"><span data-stu-id="13244-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="13244-124">選取容量。</span><span class="sxs-lookup"><span data-stu-id="13244-124">Select capacity.</span></span> <span data-ttu-id="13244-125">您可以在環境建立後變更其容量。</span><span class="sxs-lookup"><span data-stu-id="13244-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="13244-126">建立您的環境。</span><span class="sxs-lookup"><span data-stu-id="13244-126">Create your environment.</span></span> <span data-ttu-id="13244-127">您也可以將環境釘選到儀表板，以方便在登入時存取。</span><span class="sxs-lookup"><span data-stu-id="13244-127">You can also pin your environment to the dashboard for easy access whenever you sign in.</span></span>

  ![建立 Time Series Insights [釘選到儀表板]](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="13244-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13244-129">Next steps</span></span>

* <span data-ttu-id="13244-130">[定義資料存取原則](time-series-insights-data-access.md)以在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中存取您的環境</span><span class="sxs-lookup"><span data-stu-id="13244-130">[Define data access policies](time-series-insights-data-access.md) to access your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="13244-131">建立事件來源</span><span class="sxs-lookup"><span data-stu-id="13244-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="13244-132">[將事件傳送](time-series-insights-send-events.md)到事件來源</span><span class="sxs-lookup"><span data-stu-id="13244-132">[Send events](time-series-insights-send-events.md) to the event source</span></span>
