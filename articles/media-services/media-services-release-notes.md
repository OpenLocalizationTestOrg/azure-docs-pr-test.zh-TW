---
title: "aaaMedia 服務版本資訊 |Microsoft 文件"
description: "媒體服務版本資訊"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Azure 媒體服務版本資訊
這些版本資訊彙總了舊版的變更和已知問題。

> [!NOTE]
> 我們想 toohear 從我們的客戶，並專注於修正影響您的問題。 tooreport 問題或提出問題，請張貼在 hello [Azure 媒體服務 MSDN 論壇]。
> 
> 

## <a id="issues"></a>目前的已知問題
### <a id="general_issues"></a>媒體服務一般問題
| 問題 | 說明 |
| --- | --- |
| Hello REST API 中，不會提供數個常見的 HTTP 標頭。 |如果您開發使用 hello REST API 的媒體服務應用程式，您會發現一些常見的 HTTP 標頭欄位 (包括用戶端要求識別碼，要求識別碼，並傳回用戶端的要求 ID) 不支援。 在未來的更新中，將會加入 hello 標頭。 |
| 不允許 percent-encoding。 |Media Services 使用 hello hello IAssetFile.Name 屬性值，當建置 Url 的 hello 串流處理內容 (例如，http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters。)基於這個理由，不允許 percent-encoding。 hello hello 值**名稱**屬性不能有 hello 下列任何一項[百分比編碼的保留字元](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ！ *' （);: @& = + $，/？ %# []"。 此外，只能有一個 ‘.’ hello 檔案名稱副檔名。 |
| hello ListBlobs 方法屬於 hello Azure 儲存體 SDK 版本 3.x 會失敗。 |媒體服務會產生 SAS Url 根據 hello [2012年-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12)版本。 如果您想 toouse Azure 儲存體 SDK toolist blob 的 blob 容器中，使用 hello [CloudBlobContainer.ListBlobs](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx)方法屬於 Azure 儲存體 SDK 版本 2.x。 hello ListBlobs 方法屬於 hello Azure 儲存體 SDK 版本 3.x 將會失敗。 |
| 媒體服務節流機制會限制應用程式而言過多要求 toohello 服務 hello 資源使用的狀況。 hello 服務可能傳回 hello 服務無法使用 (503) HTTP 狀態碼。 |如需詳細資訊，請參閱 hello 中的 hello 503 HTTP 狀態碼 hello 描述[Azure 媒體服務錯誤碼](media-services-encoding-error-codes.md)主題。 |
| 當查詢實體，就會限制為 1000年因為公用 REST v2 限制查詢結果 too1000 結果一次傳回的實體。 |您需要 toouse**略過**和**採取**(.NET) /**頂端**(REST) 中所述[.NET 本例](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities)和[這個 REST API範例](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)。 |
| 某些用戶端可以來自跨 hello Smooth Streaming 資訊清單中的重複標記問題。 |如需詳細資訊，請參閱 [本節](media-services-deliver-content-overview.md#known-issues) 。 |
| Azure 媒體服務 .NET SDK 物件無法序列化，因此無法與 Azure 快取搭配運作。 |如果您嘗試 tooserialize hello SDK AssetCollection 物件 tooadd 它 tooAzure 快取，例外狀況就會擲回。 |
| 編碼工作失敗，並顯示訊息字串「階段︰DownloadFile。 代碼：System.NullReferenceException」。 |tooupload 輸入視訊檔案 tooan 輸入資產，並提交一個或多個編碼工作的輸入資產，而不需要進一步修改輸入資產的 hello 一般編碼工作流程。 不過，如果您修改 hello 輸入資產 （例如藉由加入/刪除/重新命名檔案內 hello 資產），則後續的工作可能會因 DownloadFile 錯誤。 hello 因應措施是 toodelete hello 輸入資產，並重新上傳輸入檔案 tooa 新資產。 |

## <a id="rest_version_history"></a>REST API 版本歷程記錄
如需 hello 媒體服務 REST API 版本歷程記錄資訊，請參閱[Azure 媒體服務 REST API 參考]。

## <a name="june-2017-release"></a>2017 年 6 月版本

媒體服務現在支援 [Azure Active Directory (Azure AD) 型驗證](media-services-use-aad-auth-to-access-ams-api.md)。

> [!IMPORTANT]
> 目前，Media Services 支援 hello Azure 存取控制服務驗證模型。 不過，存取控制授權將在 2018 年 6 月 1 日被取代。 我們建議您儘速移轉 toohello Azure AD 驗證模型。

## <a name="march-2017-release"></a>2017 年 3 月版本

您現在可以使用 Azure 媒體標準太[自動產生的位元速率階梯](media-services-autogen-bitrate-ladder-with-mes.md)藉由指定 hello 「 彈性資料流 」 的預設字串建立編碼工作時。 「 自動調整串流處理 」 是 hello 建議的預設，如果您想 tooencode 視訊串流處理媒體服務。 如果您需要的編碼方式的預設的 toocustomize 您特定案例，您可以開始使用[這些](media-services-mes-presets-overview.md)預設值。

您現在可以使用標準 Azure 媒體或媒體編碼器高階工作流程太[建立編碼工作，會產生 fMP4 區塊](media-services-generate-fmp4-chunks.md)。 


## <a name="febuary-2017-release"></a>2017 年 2 月版本

啟動年 4 月 1，2017，超過 90 天您帳戶中的任何工作記錄將會自動刪除，以及其相關聯的工作記錄，即使 hello 的總記錄數低於 hello 配額上限。 如果您需要 tooarchive hello 作業/工作資訊時，您可以使用所述的 hello 碼[這裡](media-services-dotnet-manage-entities.md)。

## <a name="january-2017-release"></a>2017 年 1 月版本

在 「 Microsoft Azure 媒體服務 」 (AMS)**串流端點**表示串流服務，以便可以將內容直接 tooa 用戶端播放器應用程式或 tooa 內容傳遞網路 (CDN) 進行進一步的發佈。 媒體服務也提供順暢的 Azure CDN 整合。 hello StreamingEndpoint 服務的輸出資料流可以是資產的即時資料流、 隨選，或您，Media Services 帳戶中的漸進式下載的視訊。 每個「Azure 媒體服務」帳戶皆包含一個預設的 StreamingEndpoint。 Hello 帳戶下，可以建立其他的 Streamingendpoint。 StreamingEndpoint 有 1.0 和 2.0 兩個版本。 從 2017 年 1 月 10 日開始，所有新建立的 AMS 帳戶都會包含 2.0 版**預設** StreamingEndpoint。 其他串流端點，您將加入 toothis 帳戶也會是 2.0 版。 這項變更不會影響現有帳戶 hello;現有的 Streamingendpoint 將 1.0 版，而且可以升級的 tooversion 2.0。 隨著這項變更，將會有行為、計費及功能變更 (如需詳細資訊，請參閱[這個](media-services-streaming-endpoints-overview.md)主題)。

Azure Media Services 此外，從 hello 2.15 版開始，加入下列屬性 toohello 串流端點實體 hello: **CdnProvider**， **CdnProfile**， **FreeTrialEndTime**， **StreamingEndpointVersion**。 如需這些屬性的詳細概觀，請參閱[這裡](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)。 

## <a name="december-2016-release"></a>2016 年 12 月版本

Azure 媒體服務現在可讓您的服務 tooaccess 遙測/度量資料。 hello AMS 目前版本可讓您即時通道，StreamingEndpoint，收集遙測資料和即時封存實體。 如需詳細資訊，請參閱 [這個](media-services-telemetry-overview.md) 主題。

## <a id="july_changes16"></a>2016 年 7 月版本
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>更新 toomanifest 檔案 (*。ISM) 產生的編碼工作
Hello 編碼工作提交的 tooMedia 編碼器標準或 Azure 媒體編碼程式編碼的工作時，會產生[串流資訊清單檔案](media-services-deliver-content-overview.md)(*.ism) 檔案中 hello 輸出資產。 Hello 最新服務版本中，已更新此資料流的資訊清單檔案的 hello 語法。

> [!NOTE]
> hello 的 hello 串流資訊清單 (.ism) 檔案的語法已保留供內部使用，且主體 toochange 在未來的版本。 請不要修改或操作 hello 這個檔案的內容。
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>新的用戶端資訊清單 (*。Hello 中產生 ISMC) 檔案的編碼工作會輸出一或多個 MP4 檔案時，將輸出資產
Hello 工作完成的編碼方式，會產生一個以上的 MP4 檔案之後, 開始 hello 最新版本更新服務，hello 輸出資產也會包含資料流的用戶端資訊清單 (*.ismc) 檔案。 hello.ismc 檔案可協助改善 hello 效能動態串流。 

> [!NOTE]
> hello 用戶端資訊清單 (.ismc) 檔案的 hello 語法已保留供內部使用，且主體 toochange 在未來的版本。 請不要修改或操作 hello 這個檔案的內容。
> 
> 

如需詳細資訊，請參閱 [此部落格](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) 。

### <a name="known-issues"></a>已知問題
某些用戶端可以來自跨 hello Smooth Streaming 資訊清單中的重複標記問題。 如需詳細資訊，請參閱 [本節](media-services-deliver-content-overview.md#known-issues) 。

## <a id="apr_changes16"></a>2016 年 4 月版本
### <a name="azure-media-analytics"></a>Azure 媒體分析
Azure 媒體服務引進了 Azure 媒體分析，提供功能強大的視訊智慧。 如需詳細資訊，請參閱 [Azure 媒體服務分析概觀](media-services-analytics-overview.md)。

### <a name="apple-fairplay-preview"></a>Apple FairPlay (預覽)
Azure 媒體服務現在使用 Apple FairPlay 內容可讓您 toodynamically 加密您 HTTP Live Streaming (HLS)。 您也可以使用 AMS 授權傳遞服務 toodeliver FairPlay 授權 tooclients。 如需詳細資訊，請參閱[使用 Azure Media Services tooStream Apple FairPlay 保護 HLS 內容](media-services-protect-hls-with-fairplay.md)。

## <a id="feb_changes16"></a>2016 年 2 月版本
Azure Media Services SDK for.NET (3.5.3) hello 最新版本包含 Widevine 相關的錯誤修復。 hello 問題是： AssetDeliveryPolicy 無法重複用於多個以 Widevine 加密的資產。 為這個 bug 修正 hello 一部分在下列屬性已加入 toohello SDK: **WidevineBaseLicenseAcquisitionUrl**。

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>2016 年 1 月版本
編碼保留單元重新命名 tooreduce 混淆編碼器的名稱。

hello Basic、 Standard 和 Premium 的編碼保留的單元會重新命名的 tooS1，S2 和 S3 分別保留單位。  使用基本編碼 Ru 現今的客戶會看到 hello 在 Azure 入口網站 （和標籤 hello bill），S1 時標準，而且 Premium 會分別看到 hello 標籤 S2 和 S3。 

## <a id="dec_changes_15"></a>2015 年 12 月版本

### <a name="azure-media-encoder-deprecation-announcement"></a>Azure 媒體編碼器淘汰通知

Azure 媒體編碼程式會啟動大約 12 個月的媒體編碼器 Standard hello 版本中被取代。

### <a name="azure-sdk-for-php"></a>Azure SDK for PHP
hello Azure SDK 小組發行新版的 hello [Azure SDK for PHP](http://github.com/Azure/azure-sdk-for-php)套件，其中包含 Microsoft Azure 媒體服務的更新和新功能。 特別是，hello Azure Media Services SDK for PHP，現在支援最新 hello[內容保護](media-services-content-protection-overview.md)功能： 動態加密使用 AES 和 DRM （PlayReady 和 Widevine） 逾時或無限制的語彙基元。 它也支援調整 [編碼單位](media-services-dotnet-encoding-units.md)大小。

如需詳細資訊，請參閱：

* hello [Microsoft Azure Media Services SDK for PHP](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/)部落格。
* hello 下列[程式碼範例](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)toohelp 可讓您快速入門：
  * **vodworkflow_aes.php**： 這是 PHP 檔案，其中顯示如何 toouse aes-128 動態加密和金鑰傳遞服務。 它根據所述的 hello.NET 範例[這](media-services-protect-with-aes128.md)發行項。
  * **vodworkflow_aes.php**： 這是 PHP 檔案，其中顯示如何 toouse PlayReady 動態加密和授權傳遞服務。 它根據所述的 hello.NET 範例[這](media-services-protect-with-drm.md)發行項。
  * **scale_encoding_units.php**： 這是示範如何 tooscale 編碼保留單元的 PHP 檔案。

## <a id="nov_changes_15"></a>2015 年 11 月版本
Azure 媒體服務現在提供 hello 雲端中的 Google Widevine 授權傳遞服務。 如需詳細資訊，請參閱太[此公告部落格](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/)。 同時也參閱[本教學課程](media-services-protect-with-drm.md)和 [GitHub 儲存機制](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm)。 

請注意，Azure 媒體服務所提供的 Widevine 授權傳遞服務為預覽狀態。 如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/)。

## <a id="oct_changes_15"></a>2015 年 10 月版本
Azure 媒體服務 (AMS) 現在是即時中下列資料中心的 hello： 巴西南部、 印度西部、 印度南部及印度中部。 現在您可以使用 Azure 入口網站 hello 太[建立媒體服務帳戶](media-services-portal-create-account.md)並執行各種工作所述[這裡](https://azure.microsoft.com/documentation/services/media-services/)。 不過，這些資料中心不會啟用即時編碼。 此外，並非所有類型的編碼保留單元都可用於這些資料中心。

* 巴西南部：只可以使用標準和基本編碼保留單元
* 印度西部、印度南部和印度中部：只可以使用基本編碼保留單元

## <a id="september_changes_15"></a>2015 年 9 月版本
* 現在提供 hello 能力 tooprotect AMS Video-On-Demand (VOD) 和 Widevine 模組化 DRM 技術的即時資料流。 您可以使用下列傳遞 Widevine 授權傳遞服務夥伴 toohelp hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/)， [EZDRM](http://ezdrm.com/)， [castLabs](http://castlabs.com/company/partners/azure/)。 如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)。
  
    您可以使用[AMS.NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) （起 hello 版本 3.5.1） 或 REST API tooconfigure 您 AssetDeliveryConfiguration toouse Widevine。  
* AMS 已新增對 Apple ProRes 影片的支援。 您現在可以上傳使用 Apple ProRes 或其他轉碼器的 QuickTime 來源視訊檔案。 如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/)。
* 您現在可以使用標準的媒體編碼器 toodo 子裁剪和即時封存 」 擷取。 如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/)。
* 進行下列篩選更新 hello: 
  
  * 您現在可以使用 Apple HTTP Live Streaming (HLS) 格式搭配僅限音訊的篩選條件。 這項更新可讓您 tooremove 純音訊播放軌藉由指定 (僅限音訊 = false) hello URL 中。
  * 時定義為您資產的篩選器，您現在可以將單一 URL 中的多個 (最新 too3) 篩選器的能力 toocombine。
    
    如需詳細資訊，請參閱 [此](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) 部落格。
* AMS 現在支援 HLS v4 的 I-Frames。 I-Frames 支援最佳化向前快轉和倒轉的作業。 根據預設，所有 HLS v4 輸出都包含 I-Frames 播放清單 (EXT-X-I-FRAME-STREAM-INF)。
  
    如需詳細資訊，請參閱 [此](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) 部落格。

## <a id="august_changes_15"></a>2015 年 8 月版本
* 現在已有適用於 Java 0.8.0 版本的 Azure 媒體服務 SDK 以及新的範例可用。 如需詳細資訊，請參閱：
  
  * [部落格文章](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Java 範例存放庫](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* 含有多重音訊串流支援的 Azure 媒體播放器更新。 如需詳細資訊，請參閱：
  * [部落格文章](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>2015 年 7 月版本
* 宣告媒體編碼器 Standard hello 一般的可用性。 如需詳細資訊，請參閱 [此部落格文章](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)。
  
    Media Encoder Standard 使用 [本節](http://go.microsoft.com/fwlink/?LinkId=618336) 描述的預設值。 請注意，當針對 4k 編碼，請使用預設值，您應該取得 hello **Premium**保留單位類型。 如需詳細資訊，請參閱[如何 tooScale 編碼](media-services-scale-media-processing-overview.md)。
* 直播即時字幕與 Azure 媒體服務和播放器。 如需詳細資訊，請參閱[此部落格文章](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/)

### <a name="media-services-net-sdk-updates"></a>媒體服務 .NET SDK 更新
Azure 媒體服務 .NET SDK 現在是版本 3.4.0.0。 在此版本中加入下列功能的 hello:  

* 即時封存的實作支援。 請注意，您無法下載包含即時封存的資產。
* 動態篩選的實作支援。
* 可讓使用者 tookeep 儲存體容器刪除資產時的實作的功能。
* Bug 修正相關 tooretry 通道中的原則。
* 已啟用的 **Media Encoder Premium 工作流程**。

## <a id="june_changes_15"></a>2015 年 6 月版本
### <a name="media-services-net-sdk-updates"></a>媒體服務 .NET SDK 更新
Azure 媒體服務 .NET SDK 現在是版本 3.3.0.0。 在此版本中加入下列功能的 hello:  

* 支援 OpenId Connect 探索規格
* 支援處理識別提供者端的金鑰變換 

如果您使用識別提供者會公開 OpenID Connect 探索文件 (下列提供者是否為 hello: Azure Active Directory、 Google、 Salesforce)，您可以指示 Azure Media Services tooobtain 簽章驗證的 JWT 權杖的金鑰OpenID 連線探索規格。 

如需詳細資訊，請參閱[使用 Json Web 金鑰從 OpenID Connect 探索規格 toowork 使用 JWT 權杖中 Azure Media Services 驗證](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/)。

## <a id="may_changes_15"></a>2015 年 5 月版本
發表 hello 下列新功能：

* [使用媒體服務進行即時編碼的預覽功能](media-services-manage-live-encoder-enabled-channels.md)
* [動態資訊清單](media-services-dynamic-manifest-overview.md)
* [Azure Media Hyperlapse 媒體處理器的預覽功能](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>2015 年 4 月版本
### <a name="general-media-services-updates"></a>一般媒體服務更新
* [發表 Azure Media Player](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)。
* 從媒體服務 REST 2.10，設定的 tooingest RTMP 通訊協定通道會建立主要和次要內嵌 Url。 如需詳細資訊，請參閱 [通道擷取組態](media-services-live-streaming-with-onprem-encoders.md#channel_input)
* Azure 媒體索引器更新
* 支援西班牙文語言
* 新的組態 xml 格式

如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/)。

### <a name="media-services-net-sdk-updates"></a>媒體服務 .NET SDK 更新
Azure 媒體服務 .NET SDK 現在是版本 3.2.0.0。

hello 以下是一些 hello 客戶對向的更新：

* **中斷變更**： 變更**TokenRestrictionTemplate.Issuer**和**TokenRestrictionTemplate.Audience** toobe 是字串型別。
* 更新相關 toocreating 自訂的重試原則。
* Bug 修正相關 toouploading/下載檔案。
* hello **MediaServicesCredentials**類別現在會接受針對主要和次要存取控制端點 tooauthenticate。

## <a id="march_changes_15"></a>2015 年 3 月版本
### <a name="general-media-services-updates"></a>一般媒體服務更新
* 媒體服務也提供 Azure CDN 整合。 toosupport hello 整合，hello **CdnEnabled**屬性已新增過**StreamingEndpoint**。  **CdnEnabled** 可以與 REST API 搭配使用 (如需詳細資訊，請參閱 [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint))。  從版本 3.1.0.2 開始，**CdnEnabled** 可以與 .NET SDK 搭配使用 (如需詳細資訊，請參閱 [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx))。
* 發表 **媒體編碼器高階工作流程**。 如需詳細資訊，請參閱 [介紹 Azure 媒體服務中的高階編碼](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)(英文)。

## <a id="february_changes_15"></a>2015 年 2 月版本
### <a name="general-media-services-updates"></a>一般媒體服務更新
媒體服務 REST API 目前的版本為 2.9。 從這個版本開始，您可以啟用 hello 與資料流端點的 Azure CDN 整合。 如需詳細資訊，請參閱 [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx)。

## <a id="january_changes_15"></a>2015 年 1 月版本
### <a name="general-media-services-updates"></a>一般媒體服務更新
內容保護與動態加密通用版本上市 (GA) 的公告。 如需詳細資訊，請參閱 [Azure 媒體服務以正式推出的 DRM 技術增強串流安全性](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/)(英文)。

### <a name="media-services-net-sdk-updates"></a>媒體服務 .NET SDK 更新
Azure 媒體服務 .NET SDK 現在是版本 3.1.0.1。

此版本會標示 hello 預設 Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate 建構函式為已過時。 hello 新建構函式會採用 TokenType 做為引數。

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>2014 年 12 月版本
### <a name="general-media-services-updates"></a>一般媒體服務更新
* 某些更新和新功能已新增 toohello Azure Indexer 媒體處理器。 如需詳細資訊，請參閱 [Azure 媒體索引器 1.1.6.7 的版本資訊](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/)(英文)。
* 已加入新的 REST API，可讓您編碼保留的單位 tooupdate:[與其餘 EncodingReservedUnitType](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)。
* 已加入金鑰傳遞服務的 CORS 支援。
* 已完成查詢授權原則選項的效能改進。
* 在中國的資料中心，hello[金鑰傳遞 URL](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url)現在是每個客戶 （就像在其他資料中心）。
* 已加入 HLS 自動目標持續時間。 在執行即時資料流時，會一律動態封裝 HLS。 根據預設，媒體服務會自動計算 HLS 區段封裝比率 (FragmentsPerSegment) 根據 hello 主要畫面格間隔 (KeyFrameInterval)，也稱為 tooas 圖片群組 – 接收來自即時編碼程式 hello 的 GOP。 如需詳細資訊，請參閱 [使用 Azure 媒體服務即時資料流]。

### <a name="media-services-net-sdk-updates"></a>媒體服務 .NET SDK 更新
* [Azure 媒體服務 .NET SDK](http://www.nuget.org/packages/windowsazure.mediaservices/) 現在是版本 3.1.0.0。
* 升級 hello.Net SDK 相依性 too.NET 4.5 Framework。
* 加入新的 API，可讓您 tooupdate 編碼保留的單位。 如需詳細資訊，請參閱 [使用.NET 更新保留單元類型和增加編碼 RU](media-services-dotnet-encoding-units.md)。
* 已加入權杖驗證的 JWT (JSON Web 權杖) 支援。 如需詳細資訊，請參閱 [Azure 媒體服務和動態加密中的 JWT 權杖驗證](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)(英文)。
* 加入的相對位移 BeginDate 和 ExpirationDate hello PlayReady 授權範本中。

## <a id="november_changes_14"></a>2014 年 11 月版本
* 媒體服務現在可讓您即時 Smooth Streaming (FMP4) 內容的 tooingest 透過 SSL 連線。 tooingest over SSL，請確定 tooupdate hello 內嵌 URL tooHTTPS。  請注意，目前 AMS 不支援使用 SSL 搭配自訂網域。  如需即時資料流的詳細資訊，請參閱[使用 Azure 媒體服務即時資料流]。
* 目前您無法透過 SSL 連線內嵌 RTMP 即時資料流。
* 如果 hello 串流的端點，您可以從中傳遞內容建立在 2014 年 9 月 10 日之後，您只可以串流 over SSL。 如果您的串流 Url 根據串流端點建立年 9 月 10 日以後的 hello，hello URL 包含"streaming.mediaservices.windows.net 」 （hello 新格式）。 包含"origin.mediaservices.windows.net 」 （hello 舊格式） 的串流 Url 不支援 SSL。 如果您的 URL 的 hello 舊格式，而且要透過 SSL，toobe 無法 toostream[建立新的串流端點](media-services-portal-manage-streaming-endpoints.md)。 使用根據新端點 toostream 將內容串流透過 SSL 的 hello 建立 Url。

## <a id="october_changes_14"></a>2014 年 10 月版本
### <a id="new_encoder_release"></a>Media Services Encoder 版本
發表新版的 Media Services Azure 媒體編碼器 hello。 Hello 與最新的 Azure 媒體編碼程式，您只需要付費針對輸出 Gb，但是否則 hello 新的編碼器是與 hello 先前編碼器相容的功能。 如需詳細資訊，請參閱 [行動服務定價詳細資料])。

### <a id="oct_sdk"></a>媒體服務 .NET SDK
Media Services SDK for .NET 延伸目前的版本為 2.0.0.3。

Media Services SDK for .NET 目前的版本為 3.0.0.8。

進行下列變更 hello:

* 重試原則類別中的重整。
* 新增使用者代理程式字串 toohttp 要求標頭。
* 新增 nuget 還原建置步驟。
* 修正案例測試 toouse x509 憑證從儲存機制。
* 更新通道和串流結束時，驗證設定。

### <a name="new-github-repository-toohost-media-services-samples"></a>新的 GitHub 儲存機制 toohost 媒體服務範例
範例位於 [Azure 媒體服務範例 GitHub 儲存機制](https://github.com/Azure/Azure-Media-Services-Samples)。

## <a id="september_changes_14"></a>2014 年 9 月版本
媒體服務 REST 中繼資料目前的版本為 2.7。 如需最新 REST 更新 hello 的詳細資訊，請參閱[Azure 媒體服務 REST API 參考]。

Media Services SDK for .NET 目前的版本為 3.0.0.7。

### <a id="sept_14_breaking_changes"></a>重大變更
* **原始**太已重新命名[StreamingEndpoint]。
* Hello 預設行為時使用 hello 變更**Azure 入口網站**tooencode 後發行 MP4 檔案。

先前，當使用 hello Azure 傳統入口網站 toopublish 單一檔案 MP4 視訊資產 SAS URL 就會建立 (SAS Url 可讓您 toodownload hello 視訊從 blob 儲存體）。 目前，使用 hello Azure 傳統入口網站 tooencode 然後發行單一檔案 MP4 視訊資產時，hello 產生 URL 點 tooan Azure 媒體服務串流端點。  這項變更不會影響直接上傳的 tooMedia Services，並且發行，但不由 Azure Media Services 編碼的 MP4 視訊。

目前，您有下列兩個選項 toosolve hello 問題 hello。

* 啟用資料流處理單位，並使用動態封裝 toostream hello.mp4 資產為 smooth streaming 展示檔。
* 建立 SAS url toodownload （或逐漸播放） hello.mp4。 如需有關如何 toocreate SAS 定位器，請參閱[傳遞內容]。

### <a id="sept_14_GA_changes"></a>GA 版本中的新功能/案例
* **索引器媒體處理器**。 如需詳細資訊，請參閱 [使用 Azure 媒體索引器編製媒體檔案的索引]。
* hello [StreamingEndpoint]實體現在可讓您 tooadd （主機） 的自訂網域名稱。
  
    自訂網域名稱 toobe，做為 hello Media Services 串流端點名稱，您需要 tooadd 自訂主機名稱 tooyour 串流端點。 使用 hello Media Services REST Api 或.NET SDK tooadd 自訂主機名稱。
  
    hello 下列考量適用於：
  
  * 您必須擁有 hello hello 自訂網域名稱擁有權。
  * hello hello 網域名稱擁有權必須經過 Azure 媒體服務。 toovalidate hello 網域建立 CName 對應<MediaServicesAccountId>。<parent domain> tooverifydns。 < mediaservices-dns 區域的 >。 
  * 您必須建立另一個 CName 對應 hello 自訂主機名稱 (例如，sports.contoso.com) tooyour 媒體服務 StreamingEndpont 的主機名稱 (例如，amstest.streaming.mediaservices.windows.net)。

    如需詳細資訊，請參閱 hello **CustomHostNames**屬性在 hello [StreamingEndpoint]主題。

### <a id="sept_14_preview_changes"></a>新功能/案例屬於 hello 公開預覽版本
* 即時資料流預覽。 如需詳細資訊，請參閱 [使用 Azure 媒體服務即時資料流]。
* 金鑰傳遞服務。 如需詳細資訊，請參閱 [使用 AES-128 動態加密和金鑰傳遞服務]。
* AES 動態加密。 如需詳細資訊，請參閱 [使用 AES-128 動態加密和金鑰傳遞服務]。
* PlayReady 授權傳遞服務。 如需詳細資訊，請參閱 [使用 PlayReady 動態加密和授權傳遞服務]。
* PlayReady 動態加密。 如需詳細資訊，請參閱 [使用 PlayReady 動態加密和授權傳遞服務]。
* 媒體服務 PlayReady 授權範本。 如需詳細資訊，請參閱 [媒體服務 PlayReady 授權範本概觀]。
* 串流儲存體加密資產。 如需詳細資訊，請參閱 [串流儲存體加密內容]。

## <a id="august_changes_14"></a>2014 年 8 月版本
當您編碼資產時，hello 編碼作業完成時產生輸出資產。 在此版本之前，Azure Media Services Encoder 會產生輸出資產的相關中繼資料。 從這個版本 hello 編碼器也會產生有關輸入資產的中繼資料。 如需詳細資訊，請參閱 hello[輸入中繼資料]和[輸出中繼資料]主題。

## <a id="july_changes_14"></a>2014 年 7 月版本
hello 遵循 bug 修正進行 hello Azure 媒體服務封裝程式及加密程式：

* 唯一的音訊播放時多工傳輸即時封存資產 tooHTTP 即時資料流-此問題已修正並立即播放音訊與視訊。
* 當封裝資產 tooHTTP 即時資料流與 AES 128 位元信封加密，hello 封裝資料流無法播放在 Android 裝置上 – 已修正這個 bug 並 hello 封裝資料流支援 HTTP 即時資料流的 Android 裝置上播放。

## <a id="may_changes_14"></a>2014 年 5 月版本
### <a id="may_14_changes"></a>一般媒體服務更新
您現在可以使用[動態封裝]toostream HTTP Live Streaming (HLS) v3。 toostream HLS v3，新增下列格式 toohello 原始定位器路徑 hello: *.ism/manifest(format=m3u8-aapl-v3)。 如需詳細資訊，請參閱 [Nick Drouin 的部落格]。

動態封裝現在也支援根據使用 PlayReady 靜態加密的 Smooth Streaming，來傳遞使用 PlayReady 加密的 HLS (v3 和 v4)。 如需詳細資訊請參閱 tooencrypt Smooth Streaming with PlayReady，[以 PlayReady 保護 Smooth Stream]。

### <a name="may_14_donnet_changes"></a>媒體服務 .NET SDK 更新
hello 媒體服務.NET SDK 3.0.0.5 版本包含下列增強功能的 hello:

* 上傳/下載媒體資產的速度和恢復能力優於以往。
* 重試邏輯和暫時性例外狀況處理已有改善： 
  
  * 因查詢、儲存變更、上傳或下載檔案而造成的例外狀況，在暫時性錯誤偵測和重試邏輯方面已有改善。 
  * 當 Web 例外狀況出現時 (例如，在 ACS 權杖要求期間)，您會發現嚴重錯誤現在的失效速度已變快。

如需詳細資訊，請參閱[hello Media Services SDK for.NET 中的重試邏輯]。

## <a id="april_changes_14"></a>2014 年 4 月編碼器版本
### <a name="april_14_enocer_changes"></a>Media Services Encoder 更新
* 使用 Grass Valley 總部/HQX 轉碼器壓縮新增擷取 AVI 檔案使用 hello Grass Valley 進行 EDIUS 非線性編輯器，撰寫其中 hello 視訊是輕量的支援。 如需詳細資訊，請參閱[Grass Valley 宣佈進行 EDIUS 7 串流透過 hello 雲端]。
* 指定 hello hello hello Media 編碼器所產生的檔案命名慣例新增的支援。 如需詳細資訊，請參閱 [控制 Media Service Encoder 輸出檔案名稱]。
* 新增了視訊和 (或) 音訊重疊的支援。 如需詳細資訊，請參閱 [建立重疊]。
* 新增了結合多個視訊片段的支援。 如需詳細資訊，請參閱 [結合視訊片段]。
* 修正的 bug 相關 tootranscoding 的 mp4 hello 音訊已編碼與 mpeg-1 Audio layer 3 (aka MP3)。

## <a id="jan_feb_changes_14"></a>2014 年 1/2 月版本
### <a name="jan_fab_14_donnet_changes"></a>Azure 媒體服務 .NET SDK 3.0.0.1、3.0.0.2 和 3.0.0.3
3.0.0.1 和 3.0.0.2 中的 hello 變更包括：

* 已修正的問題相關 toousage LINQ 查詢使用 OrderBy 陳述式。
* 將 [GitHub] 中的測試方案分成單元測試和案例測試。

如需 hello 變更的詳細資訊，請參閱： [Azure 媒體服務.NET SDK 3.0.0.1 和 3.0.0.2 版本]。

在 3.0.0.3 中進行下列變更 hello:

* 升級 Azure 儲存體相依性 toouse 版本 3.0.3.0。 
* 已修正 3中貼文。0中貼文。*中貼文。* 版的回溯相容性問題。 

## <a id="december_changes_13"></a>2013 年 12 月版本
### <a name="dec_13_donnet_changes"></a>Azure 媒體服務 .NET SDK 3.0.0.0
> [!NOTE]
> 3.0.x.x 版本沒有與 2.4.x.x 版本回溯相容。
> 
> 

hello 最新版 hello Media Services SDK 現在是 3.0.0.0。 您可以從 Nuget 下載 hello 最新的封裝，或取得 hello 位元[GitHub]。

從 hello Media Services SDK 版本 3.0.0.0 開始，您可以重複使用 hello [Azure Active Directory 存取控制服務 (ACS)]語彙基元。 如需詳細資訊，請參閱 hello 」 重複使用存取控制服務權杖 」 一節中 hello[連接 hello Media Services SDK for.NET tooMedia 服務]主題。

### <a name="dec_13_donnet_ext_changes"></a>Azure 媒體服務 .NET SDK 延伸模組 2.0.0.0
hello Azure Media Services.NET SDK Extensions 是一組延伸方法和協助程式功能，能夠簡化您的程式碼，並使其更容易 toodevelop 透過 Azure Media Services。 您可以取得 hello 從最新的 bits [Azure Media Services.NET SDK Extensions]。

## <a id="november_changes_13"></a>2013 年 11 月版本
### <a name="nov_13_donnet_changes"></a>Azure 媒體服務 .NET SDK 變更
從這個版本開始，hello Media Services SDK for.NET 會處理呼叫 toohello 媒體服務 REST API 層時可能發生的暫時性失敗錯誤。

## <a id="august_changes_13"></a>2013 年 8 月版本
### <a name="aug_13_powershell_changes"></a>Azure SDK 工具中包含的媒體服務 PowerShell Cmdlet
現在包含下列媒體服務 PowerShell cmdlet 的 hello [azure sdk 工具]。

* Get-AzureMediaServices 
  
    例如， `Get-AzureMediaServicesAccount`。
* New-AzureMediaServicesAccount 
  
    例如， `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`。
* New-AzureMediaServicesKey 
  
    例如， `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`。
* Remove-AzureMediaServicesAccount 
  
    例如， `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`。

## <a id="june_changes_13"></a>2013 年 6 月版本
### <a name="june_13_general_changes"></a>Azure 媒體服務變更
這一節所提到的 hello 變更都是包含在 hello 年 6 月的 2013年媒體服務版本的更新。

* 能力 toolink 多個儲存體帳戶 tooa Media Service 帳戶。 
  
    StorageAccount
  
    Asset.StorageAccountName 和 Asset.StorageAccount
* 能力 tooupdate Job.Priority。 
* 實體和屬性的相關通知： 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    工作 (Job)
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Azure 媒體服務 .NET SDK 變更
hello 下列變更會包含在 2013 年 6 月的媒體服務 SDK 版本。 hello 最新的媒體服務 SDK 是可在 GitHub 上取得。

* 啟動與 hello 版本 2.3.0.0，hello Media Services SDK 支援連結多個儲存體帳戶 tooa Media Services 帳戶。 hello 下列 Api 支援這項功能：
  
    hello IStorageAccount 型別。
  
    hello Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts 屬性。
  
    hello StorageAccount 屬性。
  
    hello StorageAccountName 屬性。
  
    如需詳細資訊，請參閱 [管理多個儲存體帳戶間的媒體服務資產]。
* API 的相關通知。 開頭 hello 版本 2.2.0.0 開始，您有 hello 能力 toolisten tooAzure 佇列儲存體通知。 如需詳細資訊，請參閱 [處理媒體服務工作通知]。
  
    hello Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions 屬性。
  
    hello Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint 型別。
  
    hello Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription 型別。
  
    hello Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection 型別。
  
    hello Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType 型別。
  
    hello Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState 型別。
* 在 hello Azure 儲存體用戶端 SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll) 上的相依性。
* 對 OData 5.5 (Microsoft.Data.OData.dll) 的相依性。

## <a id="december_changes_12"></a>2012 年 12 月版本
### <a name="dec_12_dotnet_changes"></a>Azure 媒體服務 .NET SDK 變更
* Intellisense：針對許多類型新增了遺漏的 Intellisense 文件。
* Microsoft.Practices.TransientFaultHandling.Core： 已修正下列問題其中 hello SDK 仍然有此組件的相依性 tooan 舊版本。 hello SDK 現在這個組件的參考版本 5.1.1209.1。

發現的 hello 年 11 月 2012 SDK 問題修正：

* IAsset.Locators.Count：現在，當所有定位器刪除後，此計數已會正確地在新的 IAsset 介面上報告。
* IAssetFile.ContentFileSize：現在，當 IAssetFile.Upload(filepath) 完成上傳後，會正確設定此值。
* IAssetFile.ContentFileSize：現已可在建立資產檔案後設定此屬性。 此檔案過去是唯讀的。
* Iassetfile.upload （filepath）： 已修正的問題，此同步上傳方法所擲回下列錯誤上, 傳多個檔案 toohello 資產時的 hello。 hello 錯誤為 「 伺服器無法 tooauthenticate hello 要求。 請確定 hello 的授權標頭的值格式正確並包含 hello 簽章 」。
* IAssetFile.UploadAsync：已修正無法同時上傳超過 5 個檔案的問題。
* IAssetFile.UploadProgressChanged: Hello SDK 現在提供這個事件。
* IAssetFile.DownloadAsync(string, BlobTransferClient, ILocator, CancellationToken)：現在提供此方法多載。
* IAssetFile.DownloadAsync：已修正無法同時下載超過 5 個檔案的問題。
* IAssetFile.Delete()： 修正的問題，其中呼叫 delete 可能會擲回例外狀況如果 hello IAssetFile 已上不傳任何檔案。
* 作業： 已修正下列問題其中鏈結 「 MP4 tooSmooth 資料流工作 」 與 「 PlayReady 保護 」 工作使用工作範本也不會建立任何工作完全。
* EncryptionUtils.GetCertificateFromStore()： 這個方法將不再擲回的 null 參考例外狀況，因為 tooa 失敗尋找 hello 憑證認證設定問題。

## <a id="november_changes_12"></a>2012 年 11 月版本
hello 這一節所述的變更已包含在 hello 年 11 月 2012 （版本 2.0.0.0） 的更新 SDK。 這些變更可能需要針對 hello 2012 年 6 月預覽 SDK 版本 toobe 修改或重新撰寫撰寫任何程式碼。

* Assets
  
    Iasset.create （assetname） 是 hello 只資產建立函式。 IAsset.Create 不再上傳檔案做為 hello 方法呼叫的一部分。 請使用 IAssetFile 進行上傳。
  
    已從 Services SDK hello 移除 hello IAsset.Publish 方法和 hello AssetState.Publish 列舉值。 任何依存於此值的程式碼都必須重寫。
* FileInfo
  
    此類別已移除，並由 IAssetFile 取代。
  
    IAssetFiles
  
    IAssetFile 已取代 FileInfo，且具有不同的行為。 toouse，具現化 hello IAssetFiles 物件，後面接著檔案上傳使用 hello Media Services SDK 或 hello Azure 儲存體 SDK。 可以使用下列 iassetfile.upload hello:
  
  * Iassetfile.upload （filepath）： 同步方法會封鎖 hello 執行緒，而且只有在上傳一個檔案時，才建議。
  * IAssetFile.UploadAsync(filePath, blobTransferClient, locator, cancellationToken)：非同步方法。 這是慣用的 hello 上傳機制。 
    
    已知的 bug： 使用 hello cancellationToken 確實會取消 hello 上傳。不過，hello 工作 hello 取消狀態可以是任何數目的狀態。 您必須正確捕捉並處理例外狀況。
* 定位器
  
    已移除 hello 原生指定版本。 hello SAS 特定內容。已被取代，或由 GA 移除，將會標示 Locators.CreateSasLocator （asset、 accessPolicy） 請參閱 hello 定位器區段下的新功能更新的行為。

## <a id="june_changes_12"></a>2012 年 6 月預覽版本
hello 下列功能是 hello 的一項新 hello 年 11 月版 SDK。

* 刪除實體
  
    IAsset、 IAssetFile、 Locator、 IAccessPolicy 和 Contentkey 物件目前已在 hello 物件層級，也就是 IObject.Delete()，而不需要在 hello cloudmediacontext.objcollection.delete （objinstance） 的集合中刪除。
* 定位器
  
    定位器必須立即使用建立 hello CreateLocator 方法，並使用 hello LocatorType.SAS 或 LocatorType.OnDemandOrigin 列舉值為 hello 定位器指定類型的引數中，您想 toocreate。
  
    已加入新屬性 tooLocators toomake 它更容易 tooobtain 可用內容的 Uri。 這次的定位器是提供未來第三方擴充性是 tooprovide 更大的彈性和增加的便利媒體用戶端應用程式。
* 非同步方法支援
  
    Tooall 方法已加入非同步支援。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[Azure 媒體服務 MSDN 論壇]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[Azure 媒體服務 REST API 參考]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[行動服務定價詳細資料]: http://azure.microsoft.com/pricing/details/media-services/
[輸入中繼資料]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[輸出中繼資料]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[傳遞內容]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[使用 Azure 媒體索引器編製媒體檔案的索引]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[StreamingEndpoint]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[使用 Azure 媒體服務即時資料流]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[使用 AES-128 動態加密和金鑰傳遞服務]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[使用 PlayReady 動態加密和授權傳遞服務]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[媒體服務 PlayReady 授權範本概觀]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[串流儲存體加密內容]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[動態封裝]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[Nick Drouin 的部落格]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[以 PlayReady 保護 Smooth Stream]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[hello Media Services SDK for.NET 中的重試邏輯]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[Grass Valley 宣佈進行 EDIUS 7 串流透過 hello 雲端]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[控制 Media Service Encoder 輸出檔案名稱]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[建立重疊]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[結合視訊片段]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[Azure 媒體服務.NET SDK 3.0.0.1 和 3.0.0.2 版本]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory 存取控制服務 (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[連接 hello Media Services SDK for.NET tooMedia 服務]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[Azure Media Services.NET SDK Extensions]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure sdk 工具]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[管理多個儲存體帳戶間的媒體服務資產]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[處理媒體服務工作通知]: http://msdn.microsoft.com/library/azure/dn261241.aspx

