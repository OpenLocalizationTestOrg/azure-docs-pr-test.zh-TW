---
title: "aaaDelivering 內容 toocustomers |Microsoft 文件"
description: "本主題簡介當您利用 Azure 媒體服務傳遞內容時會涉及各個方面。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>傳遞內容 toocustomers
當提供資料流或 video-on-demand 內容 toocustomers 時，您的目標是在不同的網路狀況下 toodeliver 高品質的視訊 toovarious 裝置。

tooachieve 達成此目標，您可以：

* 編碼的資料流 tooa 多位元速率 （彈性位元速率） 視訊資料流。 這會負責處理品質和網路狀況。
* 使用 Microsoft Azure Media Services[動態封裝](media-services-dynamic-packaging-overview.md)toodynamically 重新封裝您的資料流成不同的通訊協定。 這會負責處理不同裝置上的串流處理。 Media Services 支援的下列彈性位元速率串流技術的 hello 傳遞： HTTP Live Streaming (HLS)、 Smooth Streaming 和 MPEG DASH。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 

本文提供內容傳遞概念的重要概觀。

toocheck 已知問題，請參閱[已知問題](media-services-deliver-content-overview.md#known-issues)。

## <a name="dynamic-packaging"></a>動態封裝
Hello 動態封裝與該媒體服務提供，您可以提供您彈性位元速率 MP4 或 Smooth Streaming 編碼內容，在資料流中支援的媒體服務 （MPEG DASH、 HLS、 Smooth Streaming） 格式而不需要 toore 套件的這些資料流的格式。 我們建議您利用動態封裝傳遞內容。

tootake 利用動態封裝，您需要 tooencode （來源） 夾層檔為一組彈性位元速率 MP4 檔案或彈性位元速率 Smooth Streaming 檔案。

使用動態封裝，您可以儲存並支付一種儲存格式中的 hello 檔案。 媒體服務會建立及傳遞 hello 適當的回應，根據您的要求。

動態封裝適用於標準和高階串流端點。 

如需詳細資訊，請參閱 [動態封裝](media-services-dynamic-packaging-overview.md)。

## <a name="filters-and-dynamic-manifests"></a>篩選器與動態資訊清單
您可以使用媒體服務為資產定義篩選器。 這些篩選都是伺服器端規則可幫助您執行一些作業，例如播放視訊的特定區段，或指定的音訊和視訊客戶的裝置可以處理 （而不是與 hello 資產相關聯的所有 hello 轉譯的轉譯子集的客戶). 此篩選透過來達成*動態資訊清單*會在您的客戶要求 toostream 視訊以其中一個或多個指定的篩選條件時建立。

如需詳細資訊，請參閱 [篩選器與動態資訊清單](media-services-dynamic-manifest-overview.md)。

## <a name="locators"></a>定位器
tooprovide 您的使用者可以使用的 toostream 或下載您的內容的 url，您必須先 toopublish 資產建立定位器。 定位器提供項目點 tooaccess hello 資產中包含的檔案。 媒體服務支援兩種類型的定位器：

* OnDemandOrigin 定位器。 這些是使用的 toostream 媒體 （例如，MPEG DASH、 HLS 或 Smooth Streaming），或漸進式下載檔案。
* 共用存取簽章 (SAS) URL 定位器。 這些是使用的 toodownload 媒體檔案 tooyour 本機電腦。

*存取原則*是使用的 toodefine hello 權限 （例如讀取、 寫入和清單） 和用戶端具有存取特定資產的持續時間。 請注意 hello 清單權限 (AccessPermissions.List) 不應該用在建立 OrDemandOrigin 定位器。

定位器有到期日。 hello Azure 入口網站設定到期日 100 年 hello 未來的定位器。

> [!NOTE]
> 如果您使用 hello Azure 入口網站 toocreate 定位器 2015 年 3 月之前，這些定位器設定 tooexpire 兩年之後。
> 
> 

定位器時，使用上的到期日 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator)或[.NET](http://go.microsoft.com/fwlink/?LinkID=533259)應用程式開發介面。 請注意，當您更新的 SAS 定位器的 hello 到期日，hello URL 就會變更。

定位器並非設計 toomanage 每位使用者存取控制。 您可以使用數位版權管理 (DRM) 解決方案提供不同的存取權限 tooindividual 的使用者。 如需詳細資訊，請參閱 [保護媒體](http://msdn.microsoft.com/library/azure/dn282272.aspx)。

當您建立定位器時，可能會有 30 秒的延遲，因為 Azure 儲存體中 toorequired 儲存體和傳播程序。

## <a name="adaptive-streaming"></a>調適性串流處理
彈性位元速率技術 toodetermine 網路條件允許影片播放器應用程式，並選取從幾種位元。 當降低網路通訊時，請 hello 用戶端可以選取較低的位元速率，因此具有較低的視訊品質，可以繼續播放。 當網路狀況的改善，hello 用戶端可以切換 tooa 高位元速率以提高視訊品質。 Azure Media Services 支援下列彈性位元速率技術 hello: HTTP Live Streaming (HLS)、 Smooth Streaming 和 MPEG DASH。

具有串流 Url 的 tooprovide 使用者，您首先必須建立 OnDemandOrigin 定位器。 建立 hello hello 包含 hello 內容的基底路徑 toohello 資產的定位器可讓您 toostream。 不過，此內容，您需要進一步此路徑 toomodify toobe 無法 toostream。 完整的 URL toohello 串流資訊清單檔案，您必須串連 hello 定位器路徑 tooconstruct 值和 hello 資訊清單 (filename.ism) 檔名。 然後附加**/資訊清單**和適當的格式 （如有需要） toohello 定位器路徑。

> [!NOTE]
> 您也可以透過 SSL 連線串流您的內容。 toodo，請確定您串流 Url 開頭 HTTPS。 請注意，目前 AMS 不支援使用 SSL 搭配自訂網域。  
> 


如果 hello 串流的端點，您可以從中傳遞內容建立在 2014 年 9 月 10 日之後，您只可以串流 over SSL。 如果您的串流 Url 根據串流端點的 2014 年 9 月 10 日之後建立的 hello hello URL 包含"streaming.mediaservices.windows.net。 」 包含"origin.mediaservices.windows.net 」 （hello 舊格式） 的串流 Url 不支援 SSL。 如果您的 URL 的 hello 舊格式，而且要透過 SSL toobe 無法 toostream，建立新的串流端點。 使用基礎 hello 新端點 toostream 將內容串流透過 SSL 的 Url。

## <a name="streaming-url-formats"></a>Streaming URL 格式
### <a name="mpeg-dash-format"></a>MPEG-DASH 格式
{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Apple HTTP Live Streaming (HLS) V4 格式
{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Apple HTTP Live Streaming (HLS) V3 格式
{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>Apple HTTP Live Streaming (HLS) 格式搭配僅限音訊的篩選條件
根據預設，僅限音訊播放軌併入的 hello HLS 資訊清單。 這對於行動電話通訊網路的 Apple Store 認證是必要條件。 在此情況下，如果用戶端沒有足夠的頻寬或連線透過 2g 連線，播放會切換 tooaudio 專用。 這有助於 tookeep 內容資料流不進行緩衝處理，但沒有影像。 在某些情況中，播放程式緩衝處理可能比只有音訊更好。 如果您想 tooremove hello 純音訊播放軌時，將**碴錼 = false** toohello URL。

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)

如需詳細資訊，請參閱 [Dynamic Manifest Composition support and HLS output additional features (動態資訊清單組合支援和 HLS 輸出額外功能)](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/)。

### <a name="smooth-streaming-format"></a>Smooth Streaming 格式
{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest

範例：

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

### <a id="fmp4_v20"></a>Smooth Streaming 2.0 資訊清單 (舊版資訊清單)
根據預設，Smooth Streaming 資訊清單的格式包含 hello 重複標記 (r tag)。 不過，有些播放程式不支援 hello r 標記。 這些播放程式的用戶端可以使用停用 hello r 標記的格式：

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=fmp4-v20)

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>漸進式下載
漸進式下載，您可以開始播放媒體之前已下載 hello 整個檔案。 您無法漸進式下載 .ism* (ismv、isma、ismt 或 ismc) 檔案。

tooprogressively 下載內容時，使用 hello OnDemandOrigin 定位器類型。 hello 下列範例顯示 hello hello OnDemandOrigin 定位器類型為基礎的 URL:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

您必須解密想 toostream 漸進式下載的 hello origin 服務的任何儲存體加密資產。

## <a name="download"></a>下載
toodownload 內容 tooa 用戶端裝置，您必須建立 SAS 定位器。 hello SAS 定位器可讓您存取您的檔案所在位置的 toohello Azure 儲存體容器。 toobuild hello 下載 URL，您有 hello 主機與 SAS 簽章之間的 tooembed hello 檔案名稱。

hello 下列範例會顯示 hello URL 為基礎的 hello SAS 定位器：

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

hello 下列考量適用於：

* 您必須解密想 toostream 漸進式下載的 hello origin 服務的任何儲存體加密資產。
* 未在 12 小時內完成的下載，最後一定會失敗。

## <a name="streaming-endpoints"></a>串流端點

串流端點，代表可以將內容傳遞直接 tooa 用戶端播放器應用程式或 tooa 內容傳遞網路 (CDN) 的進一步發佈的串流服務。 從資料流的端點服務的 hello 輸出資料流可以是即時資料流或 video-on-demand 資產 Media Services 帳戶中。 串流端點有兩種類型：「標準」和「進階」。 如需詳細資訊，請參閱[串流端點概觀](media-services-streaming-endpoints-overview.md)。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 

## <a name="known-issues"></a>已知問題
### <a name="changes-toosmooth-streaming-manifest-version"></a>變更 tooSmooth Streaming 資訊清單版本
在傳回 hello 2016 年 7 月版本更新服務-時所產生的媒體編碼器 Standard、 媒體編碼器高階工作流程或 hello 較早的 Azure 媒體編碼程式使用動態封裝-hello Smooth Streaming 資料流處理的資產資訊清單會符合tooversion 2.0。 在 2.0 版中，hello 片段期間不要使用 hello 所謂重複 ('r') 標記。 例如：

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

Hello 2016 年 7 月的服務版本中，在產生 hello Smooth Streaming 資訊清單會搭配使用重複的標記的片段持續時間符合 tooversion 2.2。 例如：

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

某些 hello 舊版 Smooth Streaming 用戶端可能不支援 hello 重複標記，且將會失敗 tooload hello 資訊清單。 toomitigate 這個問題，您可以使用 hello 傳統資訊清單的格式參數**(格式 = fmp4 v20)**或更新您的用戶端 toohello 最新版本可支援重複的標記。 如需詳細資訊，請參閱 [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>相關主題
[啟動儲存體金鑰之後更新媒體服務定位器](media-services-roll-storage-access-keys.md)

