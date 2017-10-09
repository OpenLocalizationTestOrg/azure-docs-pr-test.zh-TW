---
title: "使用 Azure Media Services.NET SDK aaaCreating 篩選"
description: "本主題描述如何 toocreate 篩選讓您的用戶端能夠使用它們 toostream 特定區段的資料流。 媒體服務會建立動態資訊清單 tooachieve 這個選擇性的資料流。"
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
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>使用 Azure 媒體服務 .NET SDK 建立篩選器
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

從 2.11 版開始，媒體服務可讓您為您資產的 toodefine 篩選器。 這些篩選條件是伺服器端規則，可讓您的客戶 toochoose toodo 等： 播放視訊 （而不是正在播放 hello 整個視訊） 的區段，或指定的音訊和視訊多種客戶的裝置可以處理 （子集而不是所有 hello 多種與相關聯 hello 資產）。 您的資產此篩選透過來達成**動態資訊清單**視訊在您的客戶要求 toostream 時所建立根據指定的篩選器。

如需詳細資訊相關的 toofilters 和動態資訊清單，請參閱[動態資訊清單概觀](media-services-dynamic-manifest-overview.md)。

本主題說明如何 toouse Media Services.NET SDK toocreate、 更新和刪除篩選。 

請注意，是否您更新篩選器，它可能會佔用 too2 分鐘的時間，資料流端點 toorefresh hello 規則。 如果 hello 內容處理使用此篩選器 （快取和 proxy 和 CDN 中快取），更新此篩選器導致播放失敗。 它是在更新 hello 篩選之後，建議 tooclear hello 快取。 如果這個選項無法執行，請考慮使用不同的篩選器。 

## <a name="types-used-toocreate-filters"></a>使用 toocreate 篩選類型。
hello 下列使用類型時建立的篩選條件： 

* **IStreamingFilter**。  此類型根據下列 REST API 的 hello[篩選](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**。 此類型根據下列 REST API 的 hello [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**。 此類型根據下列 REST API 的 hello [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** 和 **IFilterTrackPropertyCondition**。 這些類型根據下列 REST Api 的 hello [FilterTrackSelect 和 FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>建立/更新/讀取/刪除全域篩選器
hello 下列程式碼會示範 toouse.NET toocreate，如何更新、 讀取和刪除資產篩選。

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


## <a name="createupdatereaddelete-asset-filters"></a>建立/更新/讀取/刪除資產篩選器
hello 下列程式碼會示範 toouse.NET toocreate，如何更新、 讀取和刪除資產篩選。

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




## <a name="build-streaming-urls-that-use-filters"></a>建置使用篩選器的資料流 URL
如需有關如何 toopublish 及傳遞資產，請參閱詳細[傳遞內容 tooCustomers 概觀](media-services-deliver-content-overview.md)。

hello 下列範例顯示如何 tooadd 篩選 tooyour 串流 Url。

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Smooth Streaming**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>另請參閱
[動態資訊清單概觀](media-services-dynamic-manifest-overview.md)

