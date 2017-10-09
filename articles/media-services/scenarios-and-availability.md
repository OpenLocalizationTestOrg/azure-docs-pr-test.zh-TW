---
title: "Azure Media Services aaaMicrosoft 案例和跨資料中心的功能可用性 |Microsoft 文件"
description: "本主題概述跨資料中心的 Microsoft Azure 媒體服務功能和服務情節和可用性。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>跨資料中心的媒體服務功能情節和可用性

Microsoft Azure 媒體服務 (AMS) 可讓您 toosecurely 上傳、 儲存、 編碼，和封裝視訊或音訊內容的隨選及即時串流傳遞 toovarious 用戶端 （例如，電視、 PC 和行動裝置）。

AMS hello 世界各地的多個資料中心運作。 這些資料中心會分組在 toogeographic 區域，讓您彈性選擇 where toobuild 應用程式。 您可以檢閱 hello[地區的清單以及其位置](https://azure.microsoft.com/regions/)。 

本主題說明[即時](#live_scenarios)傳遞內容或[隨選](#vod_scenarios)傳遞內容的常見情節。 hello 主題也會提供跨資料中心的媒體功能和服務的可用性相關的詳細資料。

## <a name="overview"></a>概觀

### <a name="prerequisites"></a>必要條件

toostart 使用 Azure Media Services 中，您應該有下列 hello:

* 一個 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com)。
* Azure 媒體服務帳戶。 如需詳細資訊，請參閱[建立帳戶](media-services-portal-create-account.md)。
* hello 串流的端點要從中 toostream 內容已經在 hello toobe**執行**狀態。

    建立 AMS 帳戶時，**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，串流端點的 hello toostart hello 中有 toobe**執行**狀態。

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a>通常用於針對 hello AMS OData 模型開發的物件

hello 下圖顯示一些最常用的 hello 物件對 hello 媒體服務 OData 模型進行開發時。

按一下 hello 映像 tooview 它的完整大小。  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

您可以檢視整個模型的 hello[這裡](https://media.windows.net/API/$metadata?api-version=2.15)。  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a>保護儲存體中的內容，並在 hello 傳遞串流處理媒體清除 （未加密）

![VoD 工作流程](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. 將高品質媒體檔上傳到資產。

    建議 tooapply 儲存體加密選項 tooyour 資產中您的內容期間上傳和儲存體中的待用時的順序 tooprotect。
2. 編碼 tooa 組彈性位元速率 MP4 檔案。

    建議 tooapply 儲存體加密選項 toohello 輸出資產順序 tooprotect 中的儲存的內容。
3. 設定資產傳遞原則 (用於動態封裝)。

    如果您的資產是已加密的儲存體， **必須** 設定資產傳遞原則。
4. 發佈 hello 資產建立 OnDemand 定位器。
5. 串流發佈的內容。

如需在資料中心內的可用性資訊，請參閱 hello[可用性](#availability)> 一節。

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>保護儲存體中的內容、提供動態加密串流處理媒體

![利用 PlayReady 保護](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. 將高品質媒體檔上傳到資產。 適用於儲存體加密選項 toohello 資產。
2. 編碼 tooa 組彈性位元速率 MP4 檔案。 適用於儲存體加密選項 toohello 輸出資產。
3. 建立您想要在播放期間動態加密 toobe hello 資產的加密內容金鑰。
4. 設定內容金鑰授權原則。
5. 設定資產傳遞原則 (供動態封裝和動態加密使用)。
6. 發佈 hello 資產建立 OnDemand 定位器。
7. 串流發佈的內容。

如需在資料中心內的可用性資訊，請參閱 hello[可用性](#availability)> 一節。

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a>使用媒體分析 tooderive 可付諸行動 insights 從您的視訊

媒體分析是語音和願景的元件，可讓它更容易組織和企業 tooderive 可執行的洞察力的視訊檔案的集合。 如需詳細資訊，請參閱 [Azure 媒體服務分析概觀](media-services-analytics-overview.md)。

1. 將高品質媒體檔上傳到資產。
2. 處理您的視訊與 hello 媒體 Analytics services hello 中所述的其中一個[媒體分析概觀](media-services-analytics-overview.md)> 一節。
3. 媒體分析的媒體處理器會產生 MP4 檔案或 JSON 檔案。 如果媒體處理器所產生的 MP4 檔案，您可以漸進式下載 hello 檔案。 如果媒體處理器所產生的 JSON 檔案，您可以從 hello Azure blob 儲存體下載 hello 檔案。

如需在資料中心內的可用性資訊，請參閱 hello[可用性](#availability)> 一節。

## <a name="deliver-progressive-download"></a>提供漸進式下載

1. 將高品質媒體檔上傳到資產。
2. Tooa 單一 MP4 檔案編碼。
3. 發行 hello 資產建立 OnDemand 或 SAS 定位器。

    如果使用 SAS 定位器，hello 內容從 hello Azure blob 儲存體下載。 在此情況下，您不需要 toohave 串流端點處於啟動狀態。
4. 漸進式下載內容。

## <a id="live_scenarios"></a>傳遞即時串流事件 

1. 使用各種即時串流通訊協定 (例如 RTMP 或 Smooth Streaming) 擷取即時內容。
2. (選擇性) 將您的串流編碼成調適性位元速率串流。
3. 預覽您的即時串流。
4. 傳送嗨內容透過一般串流通訊協定 （例如，MPEG DASH、 Smooth、 HLS） 直接 tooyour 客戶或 tooa 內容傳遞網路 (CDN) 進行進一步的發佈。

    -或-

    順序 toobe 中的記錄] 和 [存放區 hello 內嵌的內容資料流處理的更新版本 (Video-on-Demand)。

在執行即時資料流時，您可以選擇 hello 下列其中一種會路由傳送：

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>使用可從內部部署編碼器接收多位元速率即時串流的通道 (即時通行)

hello 下列圖表顯示 hello 涉及 hello AMS 平台的主要組件以 hello**傳遞**工作流程。

![即時工作流程](./media/scenarios-and-availability/media-services-live-streaming-current.png)

如需詳細資訊，請參閱 [使用通道，從內部部署編碼器接收多位元速率即時串流](media-services-live-streaming-with-onprem-encoders.md)。

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>使用通道啟用 tooperform 即時使用 Azure 媒體服務編碼

hello 下列圖表顯示 hello 主要一部分 hello AMS 平台的即時串流工作流程中所涉及其中通道是啟用 tooperform 即時使用媒體服務編碼。

![即時工作流程](./media/scenarios-and-availability/media-services-live-streaming-new.png)

如需詳細資訊，請參閱[使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)。

如需在資料中心內的可用性資訊，請參閱 hello[可用性](#availability)> 一節。

## <a name="consuming-content"></a>使用內容

Azure Media Services 提供 hello 工具，您需要 toocreate 豐富、 動態的用戶端播放器應用程式，用於大部分平台，包括： iOS 裝置、 Android 裝置、 Windows、 Windows Phone、 Xbox 和機上方塊。 下列主題中的 hello 提供連結 tooSDKs 和播放器架構，您可以使用 toodevelop 自己的用戶端應用程式可以取用從媒體服務串流媒體。 如需詳細資訊，請參閱[開發視訊付款人應用程式](media-services-develop-video-players.md)。

## <a name="enabling-azure-cdn"></a>啟用 Azure CDN

媒體服務支援與 Azure CDN 整合。 如需詳細資訊 tooenable Azure CDN，請參閱[如何在 Media Services 帳戶中的 tooManage 資料流端點](media-services-portal-manage-streaming-endpoints.md)。

## <a id="scaling"></a>調整媒體服務帳戶

AMS 客戶可以使用其 AMS 帳戶來調整串流端點、媒體處理和儲存體。

* 媒體服務客戶可以選擇一個**標準**串流端點或一個**進階**串流端點。 大多數的串流工作負載都適合使用**標準**串流端點。 它包含相同功能與 hello **Premium**自動串流端點與縮放比例的傳出頻寬。 

    **進階**串流端點適合進階工作負載，提供專用並能靈活調整的頻寬容量。 擁有**進階**串流端點的客戶預設會取得一個串流單位 (SU)。 可以藉由新增 SUs 調整串流端點的 hello。 每個 SU 提供額外的頻寬容量 toohello 應用程式。 如需有關調整**Premium**串流端點，請參閱 hello[調整串流端點](media-services-portal-scale-streaming-endpoints.md)主題。

* Media Services 帳戶會決定 hello 速度與媒體處理工作會處理保留單位類型相關聯。 您可以挑選之間 hello 下列保留單位類型： **S1**， **S2**，或**S3**。 例如，當您使用 hello 相同的編碼工作執行速度的 hello **S2**保留的單位類型比較 toohello **S1**型別。

    此外 toospecifying hello 保留單位類型，您可以指定 tooprovision 您帳戶的**保留單位**(RUs)。 佈建之俄文的 hello 數目會決定 hello 可以指定帳戶中並行處理的媒體工作數目。

    >[!NOTE]
    >RU 用於平行化所有媒體處理，包括使用 Azure 媒體索引器的索引作業。 不過，與編碼不同，索引工作的處理速度不會因為使用較快的保留單元而變快。

    如需詳細資訊，請參閱[調整媒體處理](media-services-portal-scale-media-processing.md)。
* 您也可以藉由新增儲存體帳戶 tooit 調整 Media Services 帳戶。 每個儲存體帳戶為有限的 too500 TB。 tooexpand hello 預設限制超過儲存體，您可以選擇 tooattach 多個儲存體帳戶 tooa 單一 Media Services 帳戶。 如需詳細資訊，請參閱[管理儲存體帳戶](meda-services-managing-multiple-storage-accounts.md)。

##<a id="availability"></a> 跨資料中心的媒體服務功能可用性

本節詳述跨資料中心的媒體服務功能可用性。

### <a name="ams-accounts"></a>AMS 帳戶

#### <a name="availability"></a>Availability

您可以建立 Media Services 帳戶，在下列區域的 hello： 北歐、 西歐、 美國西部、 美國東部、 東南亞、 東亞、 日本西部、 日本東部、 巴西南部、 印度西部、 印度南部和印度中部。 

### <a name="streaming-endpoints"></a>串流端點 

媒體服務客戶可以選擇一個**標準**串流端點或一個**進階**串流端點。 如需詳細資訊，請參閱 hello[調整](#scaling)> 一節。

#### <a name="availability"></a>Availability

|名稱|狀態|資料中心
|---|---|---|
|標準|GA|全部|
|進階|GA|全部|

### <a name="live-encoding"></a>即時編碼

#### <a name="availability"></a>Availability

所有資料中心內都提供，但不含：德國、巴西南部、印度西部、印度南部和印度中部。 

### <a name="encoding-media-processors"></a>編碼媒體處理器

AMS 提供兩個隨選編碼器：**媒體編碼器標準**和**媒體編碼器進階工作流程**。 如需詳細資訊，請參閱 [Azure 隨選媒體編碼器的概觀和比較](media-services-encode-asset.md)。 

#### <a name="availability"></a>Availability

|媒體處理器名稱|狀態|資料中心
|---|---|---|
|Media Encoder Standard|GA|全部|
|媒體編碼器高階工作流程|GA|所有區域 (中國除外)|

### <a name="analytics-media-processors"></a>分析媒體處理器

媒體分析是語音和願景的元件，讓組織和企業 tooderive 可執行的洞察力更容易從視訊檔案的集合。 如需詳細資訊，請參閱 [Azure 媒體服務分析概觀](media-services-analytics-overview.md)。

#### <a name="availability"></a>Availability

|媒體處理器名稱|狀態|資料中心
|---|---|---|
|Azure 媒體臉部偵測器|預覽|全部|
|Azure Media Hyperlapse|預覽|全部|
|Azure Media Indexer|GA|全部|
|Azure 媒體動作偵測器|預覽|全部|
|Azure 媒體 OCR|預覽|全部|
|Azure 媒體Media Redactor|預覽|全部|
|Azure Media Stabilizer|預覽|全部|
|Azure 媒體視訊縮圖|預覽|全部|
|Azure 媒體索引器 2|預覽|所有區域 (中國和美國聯邦政府區域除外)|

### <a name="protection"></a>保護

Microsoft Azure Media Services 可讓您 toosecure 離開您的電腦，透過儲存體、 處理和傳遞的 hello 時間從您的媒體。 如需詳細資訊，請參閱[保護 AMS 內容](media-services-content-protection-overview.md)。

#### <a name="availability"></a>Availability

|加密|狀態|資料中心|
|---|---|---| 
|儲存體|GA|全部|
|AES-128 金鑰|GA|全部|
|Fairplay|GA|全部|
|PlayReady|GA|全部|
|Widevine|GA|全部，但不含德國、美國聯邦政府和中國。

### <a name="reserved-units-rus"></a>保留單元 (RU)

hello 佈建的保留單元數目決定 hello 可以指定帳戶中並行處理的媒體工作數目。 

如需詳細資訊，請參閱 hello[調整](#scaling)> 一節。

#### <a name="availability"></a>Availability

所有資料中心內都提供。

### <a name="reserved-unit-ru-type"></a>保留單元 (RU) 類型

Media Services 帳戶會保留的單位類型，用來決定 hello 速度處理您的媒體處理工作的相關聯。 您可以挑選之間 hello 下列保留單位類型： S1、 S2 或 S3。

如需詳細資訊，請參閱 hello[調整](#scaling)> 一節。

#### <a name="availability"></a>Availability

|RU 類型名稱|狀態|資料中心
|---|---|---|
|S1|GA|全部|
|S2|GA|全部，但不含巴西南部和印度西部|
|S3|GA|全部，但不含印度西部|

## <a name="next-steps"></a>後續步驟

檢閱媒體服務學習路徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

