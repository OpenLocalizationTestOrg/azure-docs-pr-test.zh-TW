---
title: "aaaAzure Media Services 概念 |Microsoft 文件"
description: "本主題提供 Azure 媒體服務概念的概觀"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: dcefc8bc-e2ea-4b38-a643-9010f4436fb5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: juliako
ms.openlocfilehash: 0a45deff32336dfcf778552f720c1ea21927951b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-concepts"></a>Azure 媒體服務概念
本主題提供 hello 最重要的 Media Services 概念的概觀。

## <a id="assets"></a>資產和儲存體
### <a name="assets"></a>Assets
[資產](https://docs.microsoft.com/rest/api/media/operations/asset)包含數位檔案 （包括視訊、 音訊、 影像、 縮圖集合、 文字播放軌及隱藏式的字幕檔案） 和 hello 這些檔案的相關中繼資料。 Hello 數位檔案上傳到資產之後，它們無法用於 hello Media Services 編碼和串流工作流程。

資產是對應的 tooa hello Azure 儲存體帳戶中的 blob 容器和 hello 資產中的 hello 檔案會儲存成該容器中的區塊 blob。 「Azure 媒體服務」不支援分頁 Blob。

在決定哪些媒體內容 tooupload 和存放區中的資產，hello 下列考量適用於：

* 資產應該只包含一個唯一的媒體內容執行個體。 例如，一份電視影集、電影或廣告的剪輯。
* 資產不應包含多份視聽檔案的轉譯或剪輯。 一個以上的電視影集、 廣告或來自資產內部單一生產的多個相機角度，不當使用的資產的其中一個範例會嘗試 toostore。 儲存多種轉譯或編輯視聽檔案的資產中可能會導致提交編碼工作、 串流和保護 hello 稍後 hello 工作流程中的 hello 資產傳遞時發生困難。  

### <a name="asset-file"></a>資產檔案
[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 代表儲存在 blob 容器中的實際視訊或音訊檔案。 資產檔案一律會與資產相關聯，一個資產可包含一或多個檔案。 如果資產檔案物件不是 blob 容器中的數位檔案相關聯，hello Media Services 編碼器工作會失敗。

hello **AssetFile**執行個體與 hello 實際媒體檔案的兩個相異的物件。 hello AssetFile 執行個體包含 hello 媒體檔案的相關中繼資料，而 hello 媒體檔案包含 hello 實際的媒體內容。

您不應嘗試 toochange hello 內容的 blob 容器所產生的 Media Services，而不使用媒體服務應用程式開發介面。

### <a name="asset-encryption-options"></a>資產加密選項
Hello 的內容類型根據您想 tooupload、 市集和傳遞，Media Services 提供各種加密選項，您可以選擇。

>[!NOTE]
>不使用加密。 這是 hello 預設值。 使用此選項時，您的內容在傳輸或儲存體中靜止時不會受到保護。

如果您計畫使用漸進式下載 toodeliver MP4，請使用此選項 tooupload 您的內容。

**StorageEncrypted** – 使用此選項 tooencrypt 您清除的內容，在本機使用 AES 256 位元加密，然後將它上傳 tooAzure 儲存體的方式予以儲存加密在靜止。 使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。 儲存體加密的 hello 主要使用案例是當您想的 toosecure 強式加密您高品質的輸入的媒體檔案放在磁碟。 

在順序 toodeliver 儲存體加密資產，您必須設定 hello 資產的傳遞原則，讓媒體服務知道要如何 toodeliver 您的內容。 在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則 （例如 AES、 PlayReady 或不加密）。 

**CommonEncryptionProtected** -使用此選項，如果您要 tooencrypt （或上傳已加密） 內容使用一般加密或 PlayReady DRM (例如，Smooth Streaming 使用 PlayReady DRM 保護)。

**EnvelopeEncryptionProtected** – 使用此選項，如果您想 tooprotect （或上傳已受到保護） HTTP Live Streaming (HLS) 透過進階加密標準 (AES) 加密。 如果您上傳已透過 AES 加密的 HLS，它必須是由 Transform Manager 加密。

### <a name="access-policy"></a>存取原則
[AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)定義權限 （例如讀取、 寫入和清單） 和存取 tooan 資產的持續時間。 您通常會傳送就可以使用的 tooaccess hello 檔案資產中包含 AccessPolicy 物件 tooa 定位器。

>[!NOTE]
>對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。 您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。 如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。

### <a name="blob-container"></a>Blob 容器
Blob 容器提供一組 blob。 Blob 容器在媒體服務中是做為存取控制的分界點，以及資產上的共用存取簽章 (SAS) 定位器。 Azure 儲存體帳戶可以包含無限多個 blob 容器。 容器可以儲存無限制的 Blob。

>[!NOTE]
> 您不應嘗試 toochange hello 內容的 blob 容器所產生的 Media Services，而不使用媒體服務應用程式開發介面。
> 
> 

### <a id="locators"></a>定位器
[定位器](https://docs.microsoft.com/rest/api/media/operations/locator)s 提供項目點 tooaccess hello 資產中包含的檔案。 存取原則是使用的 toodefine hello 權限與用戶端有提供資產存取 tooa 的持續時間。 定位器可以有許多 tooone 關聯性存取原則，例如不同的定位器可以提供不同的開始時間，以及連線類型 toodifferent 用戶端，而所有使用 hello 相同的權限和持續時間設定;不過，由於 Azure 儲存體服務所設定的共用的存取原則限制，您不能有超過五個與指定之資產一次相關聯的唯一定位器。 

Media Services 支援兩種類型的定位器： OnDemandOrigin 定位器，使用 toostream 媒體 （例如，MPEG DASH、 HLS 或 Smooth Streaming） 或漸進式下載媒體和 SAS URL 定位器，使用的 tooupload 或下載媒體檔案 to\from Azure 儲存體。 

>[!NOTE]
>建立 OnDemandOrigin 定位器時，不應該使用 hello 清單權限 (AccessPermissions.List)。 

### <a name="storage-account"></a>儲存體帳戶
所有存取 tooAzure 存放裝置是都透過儲存體帳戶。 媒體服務帳戶可以與一個或多個儲存體帳戶產生關聯。 帳戶可以包含不限數目的容器，只要它們的大小總計低於每個儲存體帳戶 500TB 即可。  Media Services 提供 SDK 層級工具 tooallow 您 toomanage 多個儲存體帳戶和負載平衡期間根據計量或隨機發佈上傳 toothese 帳戶資產的 hello 發佈。 如需詳細資訊，請參閱「使用 [Azure 儲存體](https://msdn.microsoft.com/library/azure/dn767951.aspx)」。 

## <a name="jobs-and-tasks"></a>工作 (Job) 和工作 (Task)
A[作業](https://https://docs.microsoft.com/rest/api/media/operations/job)是常用的 tooprocess （例如，索引或編碼） 的音訊/視訊簡報。 如果您要處理多個視訊，建立每個視訊 toobe 編碼的工作。

工作包含執行 hello 處理 toobe 相關中繼資料。 每個工作 (Job) 包含一或多個 [工作 (Task)](https://docs.microsoft.com/rest/api/media/operations/task)，該工作 (Task) 指定不可部分完成的處理工作、該處理工作的輸入資產、輸出資產、媒體處理器和其相關設定。 在作業內的工作可以鏈結在一起，其中為指定 hello hello 輸出資產的一項工作輸入資產 toohello 下一項工作。 以這種方式一個工作可以包含所有必要媒體展示的 hello 處理。

## <a id="encoding"></a>編碼
Azure Media Services 提供多個 hello 編碼媒體 hello 雲端中的選項。

開始使用 Media Services，很重要的 toounderstand hello 差異轉碼器與檔案格式。
轉碼器是實作 hello 壓縮/解壓縮演算法，而檔案格式是保留 hello 壓縮視訊的容器的 hello 軟體。

Media Services 提供動態封裝可讓您 toodeliver MP4 或 Smooth Streaming 您彈性位元速率編碼格式 （MPEG DASH、 HLS、 Smooth Streaming） 的 Media Services 支援的資料流處理中的內容，而不必 toore 封裝至您串流格式。

tootake 利用[動態封裝](media-services-dynamic-packaging-overview.md)，您需要 tooencode 夾層 （來源） 檔案到一組彈性位元速率 MP4 檔案或彈性位元速率 Smooth Streaming 檔案，且有至少一個標準或進階串流端點在啟動狀態。

Media Services 支援下列隨編碼器這篇文章中所述的 hello:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium Workflow](media-services-encode-asset.md#media-encoder-premium-workflow)

如需支援編碼器的相關資訊，請參閱「 [編碼器](media-services-encode-asset.md)」。

## <a name="live-streaming"></a>即時資料流
在 Azure 媒體服務中，通道代表處理即時串流內容的管線。 通道會以兩種方式之一收到即時輸入串流：

* 在內部部署即時編碼器會傳送多位元速率 RTMP 或 Smooth Streaming (分散 MP4) toohello 通道。 您可以使用下列輸出多位元速率 Smooth Streaming 的即時編碼器的 hello: MediaExcel、 Ateme、 想像通訊、 Envivio、 Cisco 和元素。 hello 下列即時編碼器都會輸出 RTMP: Adobe Flash Live 編碼器、 Telestream wirecast 編碼、 Teradek、 Haivision 和 tricaster 轉錄編碼器。 hello 內嵌的串流可以通過通道而不需要任何進一步轉碼和編碼方式。 要求時，媒體服務會傳送 hello 資料流 toocustomers。
* 單一位元速率資料流 (其中一種 hello 下列格式： RTP (MPEG-TS))，RTMP，或 Smooth Streaming (分散 MP4)) 會傳送 toohello 通道啟用 tooperform 即時使用媒體服務編碼。 hello 通道，然後執行即時編碼的 hello 連入單一位元速率串流 tooa 多位元速率 （自動調整） 視訊資料流。 要求時，媒體服務會傳送 hello 資料流 toocustomers。

### <a name="channel"></a>通道
在媒體服務中， [通道](https://docs.microsoft.com/rest/api/media/operations/channel)負責處理即時資料流內容。 通道所提供的輸入的端點 （內嵌 URL），然後提供 tooa 即時轉碼程式。 hello 通道會從 hello 即時轉碼程式接收即時輸入的串流，並使其可用於透過一或多個 Streamingendpoint 進行串流。 頻道也提供預覽端點 (預覽 URL) toopreview 並驗證您的資料流，然後再進一步處理和傳遞。

您可以取得 hello 內嵌 URL 和 hello 預覽 URL，當您建立 hello 通道。 tooget 這些 Url，hello 通道中並沒有 toobe hello 啟動狀態。 當您準備好 toostart 將資料從即時轉碼程式推送至 hello 通道時，必須先啟動 hello 通道。 一旦 hello 即時轉碼程式開始擷取資料，您可以預覽您的資料流。

每個媒體服務帳戶可以包含多個通道、多個程式和多個 StreamingEndpoints。 根據 hello 頻寬和安全性需求，StreamingEndpoint 服務可以是專用的 tooone 或多個通道。 任何 StreamingEndpoint 可以從任何通道中提取。

### <a name="program-event"></a>程式 (事件)
A[程式 （事件）](https://docs.microsoft.com/rest/api/media/operations/program)可讓您 toocontrol hello 發行和即時串流片段的儲存體。 通道會管理程式 (事件)。 hello 通道和程式的關聯性是內容的類似 tootraditional 媒體其中通道具有常數資料流，而程式是內容的該頻道上的已設定領域的 toosome 逾時事件。
您可以指定您想要 tooretain hello 記錄內容 hello 程式設定 hello 的 hello 數**ArchiveWindowLength**屬性。 這個值可以設定為 5 分鐘 tooa 最多 25 個小時的最小值。

ArchiveWindowLength 也規定 hello 最大用戶端可以從 hello 目前即時位置搜尋的時間量。 程式可以透過 hello 指定時間內，執行但落後 hello 時間長度的內容會持續遭到捨棄。 這個屬性的值也會決定資訊清單所能成長的時間長度 hello 用戶端。

每個程式 (事件) 都是與「資產」相關聯。 您必須建立 hello 定位器 toopublish hello 程式相關聯的資產。 擁有這個定位器，可讓您 toobuild 您可以提供 tooyour 用戶端的串流 URL。

一個通道可支援同時執行的程式，因此您可以建立多個封存 hello toothree 註冊相同的傳入資料流。 這可讓您 toopublish 和封存的事件所需的不同部分。 例如，您的商務需求是 tooarchive 6 小時的程式，但 toobroadcast 最後的 10 分鐘。 tooaccomplish，您需要 toocreate 兩個同時執行的程式。 一個程式設 tooarchive 6 小時的 hello 事件，但 hello 程式不會發行。 hello 其他程式的組 tooarchive 為 10 分鐘並發佈此程式。

如需詳細資訊，請參閱：

* [使用通道，會啟用 tooPerform Live 使用 Azure 媒體服務編碼](media-services-manage-live-encoder-enabled-channels.md)
* [使用通道，從內部部署編碼器接收多位元速率即時串流](media-services-live-streaming-with-onprem-encoders.md)
* [配額和限制](media-services-quotas-and-limitations.md)。

## <a name="protecting-content"></a>保護內容
### <a name="dynamic-encryption"></a>動態加密
Azure Media Services 可讓您 toosecure 離開您的電腦，透過儲存體、 處理和傳遞的 hello 時間從您的媒體。 Media Services 可讓您的內容動態加密使用進階加密標準 (AES) （使用 128 位元加密金鑰） 和一般加密 (CENC) 使用 PlayReady 和/或 Widevine DRM toodeliver。 Media Services 也提供傳遞 AES 金鑰和 PlayReady 授權 tooauthorized 用戶端的服務。

目前，您可以加密 hello 下列資料流的格式： HLS、 MPEG DASH 和 Smooth Streaming。 您無法加密漸進式下載。

如果想要讓 Media Services tooencrypt 資產，您需要與您的 asset tooassociate 加密金鑰 （「 CommonEncryption 」 或 「 EnvelopeEncryption 」），並也可以設定 hello 金鑰授權原則。

如果您想 toostream 儲存體加密資產時，您必須設定 hello 資產的傳遞原則順序 toospecify 中您要如何 toodeliver 資產。

Media Services 時，播放程式要求串流時，使用指定的 hello 金鑰 toodynamically 加密使用信封加密 （使用 AES) 或一般加密 （具有 PlayReady 或 Widevine） 的內容。 toodecrypt hello 資料流，hello 播放程式會要求 hello 金鑰從 hello 金鑰傳遞服務。 toodecide hello 使用者獲授權 tooget hello 索引鍵，hello 服務會評估您指定 hello 索引鍵的 hello 授權原則。

### <a name="token-restriction"></a>權杖限制
hello 內容金鑰授權原則可能會有一或多個授權限制： 開放、 權杖限制或 IP 限制。 hello 權杖限制的原則必須隨附由安全權杖服務 (STS) 發行的權杖。 Media Services 支援 hello 簡易 Web 權杖 (SWT) 格式和 JSON Web Token (JWT) 格式的權杖。 媒體服務不提供安全權杖服務。 您可以建立自訂的 STS，或利用 Microsoft Azure ACS tooissue 語彙基元。 hello STS 必須設定以指定的 hello 簽署權杖的 toocreate hello 權杖限制組態中指定的索引鍵和問題的宣告。 hello Media Services 金鑰傳遞服務會傳回 hello 要求金鑰 （或授權） toohello 用戶端 hello 語彙基元是否有效並 hello 宣告 hello 語彙基元在比對中所設定的 hello 金鑰 （或授權）。

在設定 hello 權杖限制的原則時，您必須指定 hello 主要驗證金鑰、 簽發者和對象的參數。 hello 主要驗證金鑰包含 hello 確認 hello 權杖簽署，而且發行者是 hello 安全權杖服務發行 hello 權杖的金鑰。 hello 對象 （有時稱為 「 範圍 」） 說明的 hello 語彙基元的 hello 意圖或 hello 資源 hello 權杖授與存取權。 hello Media Services 金鑰傳遞服務會驗證這些 hello 權杖中的值符合 hello 範本中的 hello 值。

如需詳細資訊，請參閱下列文章 hello:

[保護內容概觀](media-services-content-protection-overview.md)
[使用 AES-128 保護](media-services-protect-with-aes128.md)
[使用 DRM 保護](media-services-protect-with-drm.md)

## <a name="delivering"></a>傳遞
### <a id="dynamic_packaging"></a>動態封裝
當使用 Media Services，我們建議的 tooencode 彈性位元速率 MP4 夾層檔案設定，然後將轉換 hello 設定 toohello 所要的格式，使用 hello[動態封裝](media-services-dynamic-packaging-overview.md)。

### <a name="streaming-endpoint"></a>串流端點
StreamingEndpoint 表示串流服務，以便可以將內容直接 tooa 用戶端播放器應用程式或 tooa 內容傳遞網路 (CDN) 進行進一步的發佈 （Azure 媒體服務現在提供 hello Azure CDN 整合）。 hello從資料流的端點服務的輸出資料流可以是即時資料流或您的 Media Services 帳戶中的視訊隨資產。 媒體服務客戶選擇**標準**串流端點或一或多個**Premium**串流端點，根據 tootheir 需求。 大多數的串流工作負載都適合使用標準串流端點。 

大多數的串流工作負載都適合使用標準串流端點。 標準資料流端點提供 hello 彈性 toodeliver 您內容的 toovirtually 每個裝置透過動態封裝 HLS、 MPEG-DASH 以及 Smooth Streaming 到以及 Microsoft PlayReady、 Google Widevine、 Apple Fairplay 動態加密與 AES128。  它們也會縮放從數千個並行的檢視器，透過 Azure CDN 整合非常小 toovery 大型的對象。 如果您有進階的工作負載或資料流的容量需求不符合 toostandard 串流端點輸送量目標或您想要的 toocontrol hello 容量 hello StreamingEndpoint 服務 toohandle 持續成長的頻寬需求建議tooallocate 縮放單位 （也稱為進階串流單位）。

建議 toouse 動態封裝及/或動態加密。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。 

如需詳細資訊，請參閱 [這個](media-services-portal-manage-streaming-endpoints.md) 主題。

依預設您最多可以有 too2 串流端點 Media Services 帳戶中。 toorequest 更高的限制，請參閱[配額和限制](media-services-quotas-and-limitations.md)。

只有 StreamingEndpoint 處於執行中狀態時，才會向您收取費用。

### <a name="asset-delivery-policy"></a>資產傳遞原則
其中一個 hello hello 媒體服務設定內容傳遞工作流程中的步驟[資產的傳遞原則](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy)想 toobe 資料流處理。 hello 資產傳遞原則會告知 Media Services 方式如您傳遞的資產 toobe： 成哪一個資料流通訊協定應在您的資產動態封裝 （適用於例如 MPEG DASH、 HLS、 Smooth Streaming 或全部），是否要 toodynamically加密您的資產和方式 （信封或一般加密）。

如果您有儲存體加密的資產，才能進行串流處理您的資產，使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 會指定傳遞原則。 例如，toodeliver 資產加密使用進階加密標準 (AES) 加密金鑰組 hello 原則類型 tooDynamicEnvelopeEncryption。 設定 hello 原則類型 tooNoDynamicEncryption tooremove 儲存體加密和 hello 清除 中的資料流 hello 資產。

### <a name="progressive-download"></a>漸進式下載
漸進式下載可讓您 toostart hello 整個檔案下載前播放媒體。 只能漸進式下載 MP4 檔案。

>[!NOTE]
>您必須解密加密的資產，如果您希望可以漸進式下載 toobe。

tooprovide 使用者漸進式下載 Url，您必須先建立 OnDemandOrigin 定位器。 建立 hello 定位器，可讓您 hello 基底路徑 toohello 資產。 然後，您會需要 tooappend hello MP4 檔案名稱。 例如：

http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>串流 URL
您的內容 tooclients 的串流處理。 具有串流 Url 的 tooprovide 使用者，您首先必須建立 OnDemandOrigin 定位器。 建立 hello 定位器，可讓您 hello 包含您想要 toostream hello 內容的基底路徑 toohello 資產。 不過，此內容需要此路徑進一步 toomodify toobe 無法 toostream。 完整的 URL toohello 串流資訊清單檔案，您必須串連 hello 定位器路徑 tooconstruct 值和 hello 資訊清單 (filename.ism) 檔名。 然後，附加 /Manifest 和適當的格式 （如有需要） toohello 定位器路徑。

您也可以透過 SSL 連線串流您的內容。 toodo，請確定您串流 Url 開頭 HTTPS。 目前 AMS 不支援使用 SSL 搭配自訂網域。  

>[!NOTE]
>如果 hello 串流的端點，您可以從中傳遞內容建立在 2014 年 9 月 10 日之後，您只可以串流 over SSL。 如果您的串流 Url 根據串流端點建立年 9 月 10 日以後的 hello，hello URL 包含"streaming.mediaservices.windows.net 」 （hello 新格式）。 包含"origin.mediaservices.windows.net 」 （hello 舊格式） 的串流 Url 不支援 SSL。 如果您的 URL 的 hello 舊格式，而且要透過 SSL toobe 無法 toostream，建立新的串流端點。 使用根據新端點 toostream 將內容串流透過 SSL 的 hello 建立 Url。

hello 下列清單描述不同的串流格式，並提供範例：

* Smooth Streaming

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

* MPEG DASH

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

* Apple HTTP 即時資料流 (HLS) V4

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

* Apple HTTP 即時資料流 (HLS) V3

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

