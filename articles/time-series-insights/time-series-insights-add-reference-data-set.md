---
title: "將參考資料集新增至 Azure Time Series Insights 環境 | Microsoft Docs"
description: "在本教學課程中，您會將參考資料集新增至 Time Series Insights 環境"
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
ms.openlocfilehash: 23444297b5231e6a026bcd9ce3ee9f943bf05867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="86774-103">使用 Ibiza 入口網站建立 Time Series Insights 環境的參考資料集</span><span class="sxs-lookup"><span data-stu-id="86774-103">Create a reference data set for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="86774-104">參考資料集是許多項目的集合，這些項目是從事件來源的事件擴展而來的。</span><span class="sxs-lookup"><span data-stu-id="86774-104">A Reference Data Set is a collection of items that are augmented with the events from your event source.</span></span> <span data-ttu-id="86774-105">Time Series Insights 輸入引擎會將事件來源的事件和參考資料集中的項目聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="86774-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="86774-106">然後此增強的事件可用於查詢。</span><span class="sxs-lookup"><span data-stu-id="86774-106">This augmented event is then available for query.</span></span> <span data-ttu-id="86774-107">這項聯結是以參考資料集中定義的索引鍵為基礎。</span><span class="sxs-lookup"><span data-stu-id="86774-107">This join is based on the keys defined in your reference data set.</span></span>

## <a name="steps-to-add-a-reference-data-set-to-your-environment"></a><span data-ttu-id="86774-108">將參考資料集新增至環境的步驟</span><span class="sxs-lookup"><span data-stu-id="86774-108">Steps to add a reference data set to your environment</span></span>

1. <span data-ttu-id="86774-109">登入 [Ibiza 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="86774-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="86774-110">按一下 Ibiza 入口網站左側功能表中的 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="86774-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3. <span data-ttu-id="86774-111">選取 Time Series Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="86774-111">Select your Time Series Insights environment.</span></span>

    ![建立 Time Series Insights 參考資料集](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="86774-113">選取 [參考資料集]，並按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="86774-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![建立 Time Series Insights 參考資料集 - 詳細資料](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="86774-115">指定參考資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="86774-115">Specify the name of the reference data set.</span></span>
6. <span data-ttu-id="86774-116">指定索引鍵名稱和類型。</span><span class="sxs-lookup"><span data-stu-id="86774-116">Specify the key name and its type.</span></span> <span data-ttu-id="86774-117">此名稱和類型會用來從事件來源的事件中選取正確屬性。</span><span class="sxs-lookup"><span data-stu-id="86774-117">This name and type is used to pick the correct property from the event in your event source.</span></span> <span data-ttu-id="86774-118">例如，如果提供的索引鍵名稱為 “DeviceId”，而類型為 “String”，則 Time Series Insights 輸入引擎會在輸入的事件中尋找名稱為 “DeviceId” 和類型為 “String” 的屬性。</span><span class="sxs-lookup"><span data-stu-id="86774-118">For instance, if you provide key name as “DeviceId” and type as “String”, then the Time Series Insights ingress engine looks for a property with the name “DeviceId” of type “String” in the incoming event.</span></span> <span data-ttu-id="86774-119">您可以提供一個以上的索引鍵與事件聯結。</span><span class="sxs-lookup"><span data-stu-id="86774-119">You can provide more than one key to join with the event.</span></span> <span data-ttu-id="86774-120">屬性名稱的對應會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="86774-120">The property name match is case-sensitive.</span></span>

     ![建立 Time Series Insights 參考資料集 - 詳細資料](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="86774-122">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="86774-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="86774-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86774-123">Next steps</span></span>

* <span data-ttu-id="86774-124">以程式設計的方式[管理參考資料](time-series-insights-manage-reference-data-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="86774-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="86774-125">如需完整的 API 參考，請參閱＜[參考資料 API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api)＞文件。</span><span class="sxs-lookup"><span data-stu-id="86774-125">For the complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>