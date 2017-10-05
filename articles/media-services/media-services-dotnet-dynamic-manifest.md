---
title: "使用 Azure 媒體服務 .NET SDK 建立篩選器"
description: "本主題說明如何建立篩選器，讓您的用戶端可以使用篩選器來串流特定的資料流區段。 媒體服務會建立動態資訊清單來完成此選擇性資料流。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 6c43473b86c14679ace558de478bd95f41d476da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="2c404-104">使用 Azure 媒體服務 .NET SDK 建立篩選器</span><span class="sxs-lookup"><span data-stu-id="2c404-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c404-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2c404-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="2c404-106">REST</span><span class="sxs-lookup"><span data-stu-id="2c404-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="2c404-107">從 2.11 版開始，媒體服務可讓您為資產定義篩選器。</span><span class="sxs-lookup"><span data-stu-id="2c404-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="2c404-108">這些篩選器是伺服器端規則，可讓您的客戶選擇執行如下的動作：只播放一段視訊 (而非播放完整視訊)，或只指定您客戶裝置可以處理的一部分音訊和視訊轉譯 (而非與該資產相關的所有轉譯)。</span><span class="sxs-lookup"><span data-stu-id="2c404-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="2c404-109">透過在您客戶要求下建立的 **動態資訊清單**可達成對資訊進行這樣的篩選，藉此根據指定的篩選器來串流視訊。</span><span class="sxs-lookup"><span data-stu-id="2c404-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="2c404-110">如需篩選器與動態資訊清單的詳細資訊，請參閱 [動態資訊清單概觀](media-services-dynamic-manifest-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2c404-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="2c404-111">本主題說明如何使用媒體服務 .NET SDK 建立、更新與刪除篩選器。</span><span class="sxs-lookup"><span data-stu-id="2c404-111">This topic shows how to use Media Services .NET SDK to create, update, and delete filters.</span></span> 

<span data-ttu-id="2c404-112">請注意，如果您更新篩選器，則資料流端點最多需要 2 分鐘的時間來重新整理規則。</span><span class="sxs-lookup"><span data-stu-id="2c404-112">Note if you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="2c404-113">如果內容是使用此篩選器提供的 (並快取在 Proxy 與 CDN 快取中)，則更新此篩選器會造成播放程式失敗。</span><span class="sxs-lookup"><span data-stu-id="2c404-113">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="2c404-114">建議在更新篩選器之後清除快取。</span><span class="sxs-lookup"><span data-stu-id="2c404-114">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="2c404-115">如果這個選項無法執行，請考慮使用不同的篩選器。</span><span class="sxs-lookup"><span data-stu-id="2c404-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="2c404-116">用於建立篩選器的類型</span><span class="sxs-lookup"><span data-stu-id="2c404-116">Types used to create filters</span></span>
<span data-ttu-id="2c404-117">建立篩選器時會使用下列類型：</span><span class="sxs-lookup"><span data-stu-id="2c404-117">The following types are used when creating filters:</span></span> 

* <span data-ttu-id="2c404-118">**IStreamingFilter**。</span><span class="sxs-lookup"><span data-stu-id="2c404-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="2c404-119">此類型是基於下列的 REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="2c404-119">This type is based on the following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="2c404-120">**IStreamingAssetFilter**。</span><span class="sxs-lookup"><span data-stu-id="2c404-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="2c404-121">此類型是基於下列的 REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="2c404-121">This type is based on the following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="2c404-122">**PresentationTimeRange**。</span><span class="sxs-lookup"><span data-stu-id="2c404-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="2c404-123">此類型是基於下列的 REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="2c404-123">This type is based on the following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="2c404-124">**FilterTrackSelectStatement** 和 **IFilterTrackPropertyCondition**。</span><span class="sxs-lookup"><span data-stu-id="2c404-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="2c404-125">這些類型是基於下列的 REST API [FilterTrackSelect 和 FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="2c404-125">These types are based on the following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="2c404-126">建立/更新/讀取/刪除全域篩選器</span><span class="sxs-lookup"><span data-stu-id="2c404-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="2c404-127">下列程式碼示範如何使用.NET 來建立、更新、讀取和刪除資產篩選器。</span><span class="sxs-lookup"><span data-stu-id="2c404-127">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="2c404-128">建立/更新/讀取/刪除資產篩選器</span><span class="sxs-lookup"><span data-stu-id="2c404-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="2c404-129">下列程式碼示範如何使用.NET 來建立、更新、讀取和刪除資產篩選器。</span><span class="sxs-lookup"><span data-stu-id="2c404-129">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="2c404-130">建置使用篩選器的資料流 URL</span><span class="sxs-lookup"><span data-stu-id="2c404-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="2c404-131">如需如何發佈與傳遞資產的相關資訊，請參閱 [將內容傳遞給客戶概觀](media-services-deliver-content-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2c404-131">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="2c404-132">下列範例顯示如何將篩選器新增至資料流 URL。</span><span class="sxs-lookup"><span data-stu-id="2c404-132">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="2c404-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="2c404-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="2c404-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="2c404-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="2c404-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="2c404-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="2c404-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="2c404-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="2c404-137">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="2c404-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2c404-138">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="2c404-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2c404-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2c404-139">See Also</span></span>
[<span data-ttu-id="2c404-140">動態資訊清單概觀</span><span class="sxs-lookup"><span data-stu-id="2c404-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

