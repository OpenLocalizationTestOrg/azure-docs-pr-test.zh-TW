---
title: "aaaAdd 參考資料集 tooyour Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "在本教學課程中，您會新增參考資料集 tooyour 時間數列 Insights 環境"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="35ed9-103">建立時間序列 Insights 環境使用 hello Ibiza 入口網站參考資料集</span><span class="sxs-lookup"><span data-stu-id="35ed9-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="35ed9-104">參考資料集是會夾帶 hello 事件來自事件來源的項目集合。</span><span class="sxs-lookup"><span data-stu-id="35ed9-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="35ed9-105">Time Series Insights 輸入引擎會將事件來源的事件和參考資料集中的項目聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="35ed9-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="35ed9-106">然後此增強的事件可用於查詢。</span><span class="sxs-lookup"><span data-stu-id="35ed9-106">This augmented event is then available for query.</span></span> <span data-ttu-id="35ed9-107">這項聯結根據參考資料集中定義的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="35ed9-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="35ed9-108">步驟 tooadd 參考資料集 tooyour 環境</span><span class="sxs-lookup"><span data-stu-id="35ed9-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="35ed9-109">登入 toohello [Ibiza 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="35ed9-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="35ed9-110">按一下 [所有資源] 功能表中的 hello 左邊 hello hello Ibiza 入口網站。</span><span class="sxs-lookup"><span data-stu-id="35ed9-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="35ed9-111">選取 Time Series Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="35ed9-111">Select your Time Series Insights environment.</span></span>

    ![建立 hello 時間數列 Insights 參考資料集](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="35ed9-113">選取 [參考資料集]，並按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="35ed9-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![建立 hello 時間數列 Insights 參考資料集詳細資料](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="35ed9-115">指定 hello hello 參考資料集名稱。</span><span class="sxs-lookup"><span data-stu-id="35ed9-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="35ed9-116">指定 hello 索引鍵名稱和型別。</span><span class="sxs-lookup"><span data-stu-id="35ed9-116">Specify hello key name and its type.</span></span> <span data-ttu-id="35ed9-117">這個名稱和型別是使用的 toopick hello 正確屬性從事件來源中的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="35ed9-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="35ed9-118">比方說，如果您提供為"DeviceId"的索引鍵名稱和類型為 「 字串 」，然後 hello 時間數列 Insights ingress 引擎會尋找具有 hello 名稱"DeviceId"hello 內送事件中的 「 字串 」 類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="35ed9-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="35ed9-119">您可以提供一個以上的索引鍵 toojoin 與 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="35ed9-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="35ed9-120">hello 屬性名稱比對會區分大小寫的。</span><span class="sxs-lookup"><span data-stu-id="35ed9-120">hello property name match is case-sensitive.</span></span>

     ![建立 hello 時間數列 Insights 參考資料集詳細資料](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="35ed9-122">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="35ed9-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="35ed9-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35ed9-123">Next steps</span></span>

* <span data-ttu-id="35ed9-124">以程式設計的方式[管理參考資料](time-series-insights-manage-reference-data-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="35ed9-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="35ed9-125">Hello 完整的 API 參考，請參閱[參考資料 API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api)文件。</span><span class="sxs-lookup"><span data-stu-id="35ed9-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
