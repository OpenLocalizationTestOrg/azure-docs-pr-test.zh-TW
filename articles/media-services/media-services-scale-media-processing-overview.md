---
title: "aaaScaling 媒體處理概觀 |Microsoft 文件"
description: "本主題為透過 Azure 媒體服務調整媒體處理的概觀。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a><span data-ttu-id="addaf-103">調整媒體處理概觀</span><span class="sxs-lookup"><span data-stu-id="addaf-103">Scaling Media Processing overview</span></span>
<span data-ttu-id="addaf-104">此頁面提供的概觀，如何及為何 tooscale 媒體處理。</span><span class="sxs-lookup"><span data-stu-id="addaf-104">This page gives an overview of how and why tooscale media processing.</span></span> 

## <a name="overview"></a><span data-ttu-id="addaf-105">概觀</span><span class="sxs-lookup"><span data-stu-id="addaf-105">Overview</span></span>
<span data-ttu-id="addaf-106">Media Services 帳戶會決定 hello 速度與媒體處理工作會處理保留單位類型相關聯。</span><span class="sxs-lookup"><span data-stu-id="addaf-106">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="addaf-107">您可以挑選之間 hello 下列保留單位類型： **S1**， **S2**，或**S3**。</span><span class="sxs-lookup"><span data-stu-id="addaf-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="addaf-108">例如，當您使用 hello 相同的編碼工作執行速度的 hello **S2**保留的單位類型比較 toohello **S1**型別。</span><span class="sxs-lookup"><span data-stu-id="addaf-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="addaf-109">如需詳細資訊，請參閱 hello[保留單位類型](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/)。</span><span class="sxs-lookup"><span data-stu-id="addaf-109">For more information, see hello [Reserved Unit Types](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).</span></span>

<span data-ttu-id="addaf-110">此外 toospecifying hello 保留單位類型，您可以指定 tooprovision 您的帳戶與保留的單位。</span><span class="sxs-lookup"><span data-stu-id="addaf-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with reserved units.</span></span> <span data-ttu-id="addaf-111">hello 佈建的保留單元數目決定 hello 可以指定帳戶中並行處理的媒體工作數目。</span><span class="sxs-lookup"><span data-stu-id="addaf-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="addaf-112">例如，如果您的帳戶有五個媒體工作將會執行同時只要 5 個保留的單位，為有工作 toobe 處理。</span><span class="sxs-lookup"><span data-stu-id="addaf-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="addaf-113">hello 其餘的工作會在 hello 佇列中等候，而且會取得收取正在執行的工作完成時，依序處理。</span><span class="sxs-lookup"><span data-stu-id="addaf-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="addaf-114">如果帳戶未佈建任何保留單元，則會循序地挑選工作。</span><span class="sxs-lookup"><span data-stu-id="addaf-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="addaf-115">在此情況下，hello 之間的等候時間一個工作完成並 hello 一開始會相依於資源的 hello 可用性 hello 系統中。</span><span class="sxs-lookup"><span data-stu-id="addaf-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

## <a name="choosing-between-different-reserved-unit-types"></a><span data-ttu-id="addaf-116">選擇不同的保留單元類型</span><span class="sxs-lookup"><span data-stu-id="addaf-116">Choosing between different reserved unit types</span></span>
<span data-ttu-id="addaf-117">下表中的 hello 可協助您選擇不同的編碼速度時做出決策。</span><span class="sxs-lookup"><span data-stu-id="addaf-117">hello following table helps you make decision when choosing between different encoding speeds.</span></span> <span data-ttu-id="addaf-118">它也提供一些基準測試案例，並提供 SAS Url，您可以使用 toodownload 視訊，您可以執行您自己的測試：</span><span class="sxs-lookup"><span data-stu-id="addaf-118">It also provides a few benchmark cases and provides SAS URLs that you can use toodownload videos on which you can perform your own tests:</span></span>

| <span data-ttu-id="addaf-119">案例</span><span class="sxs-lookup"><span data-stu-id="addaf-119">Scenarios</span></span> | <span data-ttu-id="addaf-120">**S1**</span><span class="sxs-lookup"><span data-stu-id="addaf-120">**S1**</span></span> | <span data-ttu-id="addaf-121">**S2**</span><span class="sxs-lookup"><span data-stu-id="addaf-121">**S2**</span></span> | <span data-ttu-id="addaf-122">**S3**</span><span class="sxs-lookup"><span data-stu-id="addaf-122">**S3**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="addaf-123">預定的使用案例</span><span class="sxs-lookup"><span data-stu-id="addaf-123">Intended use case</span></span> |<span data-ttu-id="addaf-124">單一位元速率編碼。</span><span class="sxs-lookup"><span data-stu-id="addaf-124">Single bitrate encoding.</span></span> <br/><span data-ttu-id="addaf-125">在 SD或如下解決方法的檔案、對時間不敏感、低成本。</span><span class="sxs-lookup"><span data-stu-id="addaf-125">Files at SD or below resolutions, not time sensitive, low cost.</span></span> |<span data-ttu-id="addaf-126">單一位元速率和多重位元速率編碼。</span><span class="sxs-lookup"><span data-stu-id="addaf-126">Single bitrate and multiple bitrate encoding.</span></span><br/><span data-ttu-id="addaf-127">SD 和 HD 編碼的一般使用方式。</span><span class="sxs-lookup"><span data-stu-id="addaf-127">Normal usage for both SD and HD encoding.</span></span> |<span data-ttu-id="addaf-128">單一位元速率和多重位元速率編碼。</span><span class="sxs-lookup"><span data-stu-id="addaf-128">Single bitrate and multiple bitrate encoding.</span></span><br/><span data-ttu-id="addaf-129">Full HD 和 4K 解析度影片。</span><span class="sxs-lookup"><span data-stu-id="addaf-129">Full HD and 4K resolution videos.</span></span> <span data-ttu-id="addaf-130">對時間敏感、周轉時間更快的編碼。</span><span class="sxs-lookup"><span data-stu-id="addaf-130">Time sensitive, faster turnaround encoding.</span></span> |
| <span data-ttu-id="addaf-131">基準測試</span><span class="sxs-lookup"><span data-stu-id="addaf-131">Benchmark</span></span> |<span data-ttu-id="addaf-132">[輸入檔案︰長度 5 分鐘，每秒 29.97 格畫面的解析度為 640x360p](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)。</span><span class="sxs-lookup"><span data-stu-id="addaf-132">[Input file: 5 minutes long 640x360p at 29.97 frames/second](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).</span></span><br/><br/><span data-ttu-id="addaf-133">編碼 tooa 單一位元速率 MP4 檔案，在 hello 相同的解析度大約需要 11 分鐘。</span><span class="sxs-lookup"><span data-stu-id="addaf-133">Encoding tooa single bitrate MP4 file, at hello same resolution, takes approximately 11 minutes.</span></span> |[<span data-ttu-id="addaf-134">輸入檔案︰長度 5 分鐘，每秒 29.97 格畫面的解析度為 1280x720p</span><span class="sxs-lookup"><span data-stu-id="addaf-134">Input file: 5 minutes long 1280x720p at 29.97 frames/second</span></span>](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)<br/><br/><span data-ttu-id="addaf-135">具有「H264 單一位元速率 720p」預設值的編碼會花大約 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="addaf-135">Encoding with "H264 Single Bitrate 720p" preset takes approximately 5 minutes.</span></span><br/><br/><span data-ttu-id="addaf-136">具有「H264 多重位元速率 720p」預設值的編碼會花大約 11.5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="addaf-136">Encoding with "H264 Multiple Bitrate 720p" preset takes approximately 11.5 minutes.</span></span> |<span data-ttu-id="addaf-137">[輸入檔案︰長度 5 分鐘，每秒 29.97 格畫面的解析度為 1920x1080p](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)。</span><span class="sxs-lookup"><span data-stu-id="addaf-137">[Input file: 5 minutes long 1920x1080p at 29.97 frames/second](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).</span></span> <br/><br/><span data-ttu-id="addaf-138">具有「H264 單一位元速率 1080p」預設值的編碼會花大約 2.7 分鐘。</span><span class="sxs-lookup"><span data-stu-id="addaf-138">Encoding with "H264 Single Bitrate 1080p" preset takes approximately 2.7 minutes.</span></span><br/><br/><span data-ttu-id="addaf-139">具有「H264 多重位元速率 1080p」預設值的編碼會花大約 5.7 分鐘。</span><span class="sxs-lookup"><span data-stu-id="addaf-139">Encoding with "H264 Multiple Bitrate 1080p" preset takes approximately 5.7 minutes.</span></span> |

## <a name="considerations"></a><span data-ttu-id="addaf-140">考量</span><span class="sxs-lookup"><span data-stu-id="addaf-140">Considerations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="addaf-141">請檢閱本章節所述的考量。</span><span class="sxs-lookup"><span data-stu-id="addaf-141">Review considerations described in this section.</span></span>  
> 
> 

* <span data-ttu-id="addaf-142">保留單元用於平行化所有媒體處理，包括使用 Azure 媒體索引器的索引工作。</span><span class="sxs-lookup"><span data-stu-id="addaf-142">Reserved Units work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span>  <span data-ttu-id="addaf-143">不過，與編碼不同，索引工作的處理速度不會因為使用較快的保留單元而變快。</span><span class="sxs-lookup"><span data-stu-id="addaf-143">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>
* <span data-ttu-id="addaf-144">如果使用 hello 共用集區，也就是不含任何保留單位，則您的編碼工作有像使用 S1 RUs hello 相同的效能。</span><span class="sxs-lookup"><span data-stu-id="addaf-144">If using hello shared pool, that is, without any reserved units, then your encode tasks have hello same performance as with S1 RUs.</span></span> <span data-ttu-id="addaf-145">不過，沒有您的工作排入佇列的狀態，可以縮短對上限 toohello 時間，而且最多只有一個工作將會在任何時候執行。</span><span class="sxs-lookup"><span data-stu-id="addaf-145">However, there is no upper bound toohello time your Tasks can spend in queued state, and at any given time, at most only one Task will be running.</span></span>
* <span data-ttu-id="addaf-146">下列資料中心的 hello 不提供 hello **S2**保留單位類型： 巴西南部和印度西部。</span><span class="sxs-lookup"><span data-stu-id="addaf-146">hello following data centers do not offer hello **S2** reserved unit type: Brazil South, and India West.</span></span>
* <span data-ttu-id="addaf-147">hello 下列的資料中心不提供 hello **S3**保留單位類型： 印度西部。</span><span class="sxs-lookup"><span data-stu-id="addaf-147">hello following data center does not offer hello **S3** reserved unit type: India West.</span></span>

## <a name="billing"></a><span data-ttu-id="addaf-148">計費</span><span class="sxs-lookup"><span data-stu-id="addaf-148">Billing</span></span>

<span data-ttu-id="addaf-149">您的費用取決於使用媒體保留單元的實際分鐘數。</span><span class="sxs-lookup"><span data-stu-id="addaf-149">You are charged based on actual minutes of usage of Media Reserved Units.</span></span> <span data-ttu-id="addaf-150">如需詳細說明，請參閱 hello 常見問題集 > 一節的 hello [Media Services 定價](https://azure.microsoft.com/pricing/details/media-services/)頁面。</span><span class="sxs-lookup"><span data-stu-id="addaf-150">For a detailed explanation, see hello FAQ section of hello [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/) page.</span></span>   

## <a name="quotas-and-limitations"></a><span data-ttu-id="addaf-151">配額和限制</span><span class="sxs-lookup"><span data-stu-id="addaf-151">Quotas and limitations</span></span>
<span data-ttu-id="addaf-152">如需配額和限制的詳細資訊和如何 tooopen 支援票證，請參閱[配額和限制](media-services-quotas-and-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="addaf-152">For information about quotas and limitations and how tooopen a support ticket, see [Quotas and limitations](media-services-quotas-and-limitations.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="addaf-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="addaf-153">Next step</span></span>
<span data-ttu-id="addaf-154">達到 hello 調整媒體處理工作使用這些技術的其中之一：</span><span class="sxs-lookup"><span data-stu-id="addaf-154">Achieve hello scaling media processing task with one of these technologies:</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="addaf-155">.NET</span><span class="sxs-lookup"><span data-stu-id="addaf-155">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="addaf-156">入口網站</span><span class="sxs-lookup"><span data-stu-id="addaf-156">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="addaf-157">REST</span><span class="sxs-lookup"><span data-stu-id="addaf-157">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="addaf-158">Java</span><span class="sxs-lookup"><span data-stu-id="addaf-158">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="addaf-159">PHP</span><span class="sxs-lookup"><span data-stu-id="addaf-159">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="addaf-160">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="addaf-160">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="addaf-161">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="addaf-161">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

