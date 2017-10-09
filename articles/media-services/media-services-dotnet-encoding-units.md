---
title: "藉由加入編碼單位-Azure 處理 aaaScale 媒體 | Microsoft 文件"
description: "深入了解如何搭配.NET toohow tooadd 編碼單元"
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
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="afa42-103">如何使用.NET SDK 編碼 tooscale</span><span class="sxs-lookup"><span data-stu-id="afa42-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afa42-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="afa42-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="afa42-105">.NET</span><span class="sxs-lookup"><span data-stu-id="afa42-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="afa42-106">REST</span><span class="sxs-lookup"><span data-stu-id="afa42-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="afa42-107">Java</span><span class="sxs-lookup"><span data-stu-id="afa42-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="afa42-108">PHP</span><span class="sxs-lookup"><span data-stu-id="afa42-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="afa42-109">概觀</span><span class="sxs-lookup"><span data-stu-id="afa42-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="afa42-110">請確定 tooreview hello[概觀](media-services-scale-media-processing-overview.md)主題 tooget 調整媒體處理主題的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="afa42-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="afa42-111">toochange hello 保留單位類型及 hello 數目編碼保留的單位使用.NET SDK hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="afa42-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="afa42-112">建立支援票證</span><span class="sxs-lookup"><span data-stu-id="afa42-112">Opening a Support Ticket</span></span>
<span data-ttu-id="afa42-113">根據預設，每個 Media Services 帳戶可以調整 tooup too25 編碼和 5 個隨選串流保留單元。</span><span class="sxs-lookup"><span data-stu-id="afa42-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="afa42-114">您可以建立支援票證來要求更高的限制。</span><span class="sxs-lookup"><span data-stu-id="afa42-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="afa42-115">開啟支援票證</span><span class="sxs-lookup"><span data-stu-id="afa42-115">Open a support ticket</span></span>
<span data-ttu-id="afa42-116">請勿 hello tooopen 支援票證，遵循：</span><span class="sxs-lookup"><span data-stu-id="afa42-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="afa42-117">按一下 [取得支援](https://manage.windowsazure.com/?getsupport=true)。</span><span class="sxs-lookup"><span data-stu-id="afa42-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="afa42-118">如果您未登入，您將會提示的 tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="afa42-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="afa42-119">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="afa42-119">Select your subscription.</span></span>
3. <span data-ttu-id="afa42-120">在支援類型下，選取 [技術]。</span><span class="sxs-lookup"><span data-stu-id="afa42-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="afa42-121">按一下 [建立票證]。</span><span class="sxs-lookup"><span data-stu-id="afa42-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="afa42-122">選取 Azure Media Services"hello 產品清單中顯示 hello 下一個頁面。</span><span class="sxs-lookup"><span data-stu-id="afa42-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="afa42-123">選取適合您的問題的 [問題類型]。</span><span class="sxs-lookup"><span data-stu-id="afa42-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="afa42-124">按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="afa42-124">Click Continue.</span></span>
8. <span data-ttu-id="afa42-125">遵循下一頁的指示，然後輸入問題的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="afa42-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="afa42-126">按一下 提交 tooopen hello 票證。</span><span class="sxs-lookup"><span data-stu-id="afa42-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="afa42-127">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="afa42-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="afa42-128">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="afa42-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

