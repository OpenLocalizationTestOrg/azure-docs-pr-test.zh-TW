---
title: "藉由新增編碼單元來調整媒體處理的規模 - Azure | Microsoft Docs"
description: "了解如何使用 .NET 新增編碼單元"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: 72a8729d22a9e76c8076d7a3347619a2163e4f09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-scale-encoding-with-net-sdk"></a><span data-ttu-id="17b7c-103">如何使用 .NET SDK 調整編碼</span><span class="sxs-lookup"><span data-stu-id="17b7c-103">How to scale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="17b7c-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="17b7c-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="17b7c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="17b7c-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="17b7c-106">REST</span><span class="sxs-lookup"><span data-stu-id="17b7c-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="17b7c-107">Java</span><span class="sxs-lookup"><span data-stu-id="17b7c-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="17b7c-108">PHP</span><span class="sxs-lookup"><span data-stu-id="17b7c-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="17b7c-109">Overview</span><span class="sxs-lookup"><span data-stu-id="17b7c-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="17b7c-110">請務必檢閱 [概觀](media-services-scale-media-processing-overview.md) 主題，以取得調整媒體處理主題的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="17b7c-110">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="17b7c-111">若要使用 .NET SDK　變更保留單元類型以及編碼保留單元數目，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="17b7c-111">To change the reserved unit type and the number of encoding reserved units using .NET SDK, do the following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="17b7c-112">建立支援票證</span><span class="sxs-lookup"><span data-stu-id="17b7c-112">Opening a Support Ticket</span></span>
<span data-ttu-id="17b7c-113">依預設，每一個媒體服務帳戶可調整為最多 25 個編碼保留單元和 5 個隨選串流保留單元。</span><span class="sxs-lookup"><span data-stu-id="17b7c-113">By default every Media Services account can scale to up to 25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="17b7c-114">您可以建立支援票證來要求更高的限制。</span><span class="sxs-lookup"><span data-stu-id="17b7c-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="17b7c-115">開啟支援票證</span><span class="sxs-lookup"><span data-stu-id="17b7c-115">Open a support ticket</span></span>
<span data-ttu-id="17b7c-116">若要建立支援票證，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="17b7c-116">To open a support ticket do the following:</span></span>

1. <span data-ttu-id="17b7c-117">按一下 [取得支援](https://manage.windowsazure.com/?getsupport=true)。</span><span class="sxs-lookup"><span data-stu-id="17b7c-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="17b7c-118">如果您未登入，系統會提示您輸入認證。</span><span class="sxs-lookup"><span data-stu-id="17b7c-118">If you are not logged in, you will be prompted to enter your credentials.</span></span>
2. <span data-ttu-id="17b7c-119">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="17b7c-119">Select your subscription.</span></span>
3. <span data-ttu-id="17b7c-120">在支援類型下，選取 [技術]。</span><span class="sxs-lookup"><span data-stu-id="17b7c-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="17b7c-121">按一下 [建立票證]。</span><span class="sxs-lookup"><span data-stu-id="17b7c-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="17b7c-122">在下一頁顯示的產品清單中，選取 [Azure 媒體服務]。</span><span class="sxs-lookup"><span data-stu-id="17b7c-122">Select "Azure Media Services" in the product list presented on the next page.</span></span>
6. <span data-ttu-id="17b7c-123">選取適合您的問題的 [問題類型]。</span><span class="sxs-lookup"><span data-stu-id="17b7c-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="17b7c-124">按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="17b7c-124">Click Continue.</span></span>
8. <span data-ttu-id="17b7c-125">遵循下一頁的指示，然後輸入問題的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="17b7c-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="17b7c-126">按一下 [提交] 來建立票證。</span><span class="sxs-lookup"><span data-stu-id="17b7c-126">Click submit to open the ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="17b7c-127">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="17b7c-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="17b7c-128">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="17b7c-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

