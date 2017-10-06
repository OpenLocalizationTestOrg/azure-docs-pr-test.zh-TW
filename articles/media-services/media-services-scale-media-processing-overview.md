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
# <a name="scaling-media-processing-overview"></a>調整媒體處理概觀
此頁面提供的概觀，如何及為何 tooscale 媒體處理。 

## <a name="overview"></a>概觀
Media Services 帳戶會決定 hello 速度與媒體處理工作會處理保留單位類型相關聯。 您可以挑選之間 hello 下列保留單位類型： **S1**， **S2**，或**S3**。 例如，當您使用 hello 相同的編碼工作執行速度的 hello **S2**保留的單位類型比較 toohello **S1**型別。 如需詳細資訊，請參閱 hello[保留單位類型](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/)。

此外 toospecifying hello 保留單位類型，您可以指定 tooprovision 您的帳戶與保留的單位。 hello 佈建的保留單元數目決定 hello 可以指定帳戶中並行處理的媒體工作數目。 例如，如果您的帳戶有五個媒體工作將會執行同時只要 5 個保留的單位，為有工作 toobe 處理。 hello 其餘的工作會在 hello 佇列中等候，而且會取得收取正在執行的工作完成時，依序處理。 如果帳戶未佈建任何保留單元，則會循序地挑選工作。 在此情況下，hello 之間的等候時間一個工作完成並 hello 一開始會相依於資源的 hello 可用性 hello 系統中。

## <a name="choosing-between-different-reserved-unit-types"></a>選擇不同的保留單元類型
下表中的 hello 可協助您選擇不同的編碼速度時做出決策。 它也提供一些基準測試案例，並提供 SAS Url，您可以使用 toodownload 視訊，您可以執行您自己的測試：

| 案例 | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| 預定的使用案例 |單一位元速率編碼。 <br/>在 SD或如下解決方法的檔案、對時間不敏感、低成本。 |單一位元速率和多重位元速率編碼。<br/>SD 和 HD 編碼的一般使用方式。 |單一位元速率和多重位元速率編碼。<br/>Full HD 和 4K 解析度影片。 對時間敏感、周轉時間更快的編碼。 |
| 基準測試 |[輸入檔案︰長度 5 分鐘，每秒 29.97 格畫面的解析度為 640x360p](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)。<br/><br/>編碼 tooa 單一位元速率 MP4 檔案，在 hello 相同的解析度大約需要 11 分鐘。 |[輸入檔案︰長度 5 分鐘，每秒 29.97 格畫面的解析度為 1280x720p](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)<br/><br/>具有「H264 單一位元速率 720p」預設值的編碼會花大約 5 分鐘。<br/><br/>具有「H264 多重位元速率 720p」預設值的編碼會花大約 11.5 分鐘。 |[輸入檔案︰長度 5 分鐘，每秒 29.97 格畫面的解析度為 1920x1080p](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)。 <br/><br/>具有「H264 單一位元速率 1080p」預設值的編碼會花大約 2.7 分鐘。<br/><br/>具有「H264 多重位元速率 1080p」預設值的編碼會花大約 5.7 分鐘。 |

## <a name="considerations"></a>考量
> [!IMPORTANT]
> 請檢閱本章節所述的考量。  
> 
> 

* 保留單元用於平行化所有媒體處理，包括使用 Azure 媒體索引器的索引工作。  不過，與編碼不同，索引工作的處理速度不會因為使用較快的保留單元而變快。
* 如果使用 hello 共用集區，也就是不含任何保留單位，則您的編碼工作有像使用 S1 RUs hello 相同的效能。 不過，沒有您的工作排入佇列的狀態，可以縮短對上限 toohello 時間，而且最多只有一個工作將會在任何時候執行。
* 下列資料中心的 hello 不提供 hello **S2**保留單位類型： 巴西南部和印度西部。
* hello 下列的資料中心不提供 hello **S3**保留單位類型： 印度西部。

## <a name="billing"></a>計費

您的費用取決於使用媒體保留單元的實際分鐘數。 如需詳細說明，請參閱 hello 常見問題集 > 一節的 hello [Media Services 定價](https://azure.microsoft.com/pricing/details/media-services/)頁面。   

## <a name="quotas-and-limitations"></a>配額和限制
如需配額和限制的詳細資訊和如何 tooopen 支援票證，請參閱[配額和限制](media-services-quotas-and-limitations.md)。

## <a name="next-step"></a>後續步驟
達到 hello 調整媒體處理工作使用這些技術的其中之一： 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [入口網站](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

