---
title: "視使用.NET 傳遞內容入門 aaaGet |Microsoft 文件"
description: "本教學課程會引導您使用適用於.NET 的 Azure Media services 實作上的要求內容傳遞應用程式的 hello 步驟。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a>使用 .NET SDK 傳遞點播內容入門
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

本教學課程會引導您實作基本的 Video-on-Demand (VoD) 內容傳遞服務與 Azure 媒體服務 (AMS) 應用程式使用 hello Azure Media Services.NET SDK 的 hello 步驟。

## <a name="prerequisites"></a>必要條件

hello 下面是必要的 toocomplete hello 教學課程：

* 一個 Azure 帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* 媒體服務帳戶。 toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。
* .NET Framework 4.0 或更新版本。
* Visual Studio。

這個教學課程包括下列工作的 hello:

1. 啟動串流端點 （使用 hello Azure 入口網站）。
2. 建立和設定 Visual Studio 專案。
3. Toohello Media Services 帳戶連接。
2. 上傳視訊檔案。
3. Hello 原始程式檔編碼為一組彈性位元速率 MP4 檔案。
4. 發佈 hello 資產和取得資料流和漸進式下載 Url。  
5. 播放您的內容。

## <a name="overview"></a>概觀
本教學課程將引導您完成 hello 步驟實作 Video-on-Demand (VoD) 傳遞內容的應用程式，使用 Azure 媒體服務 (AMS) SDK for.NET。

hello 教學課程介紹 hello 基本 Media Services 工作流程和 hello 最常見的程式設計物件，以及 Media Services 開發所需的工作。 在 hello 完成 hello 教學課程，您將會是能 toostream 或漸進式下載範例媒體檔案，您可以上傳、 編碼，以及下載。

### <a name="ams-model"></a>AMS 模型

hello 下圖顯示一些最常用的 hello 物件開發 VoD 針對 hello 媒體服務 OData 模型的應用程式時。

按一下 hello 映像 tooview 它的完整大小。  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

您可以檢視整個模型的 hello[這裡](https://media.windows.net/API/$metadata?api-version=2.15)。  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>啟動串流端點使用 hello Azure 入口網站

當使用 Azure Media Services hello 最常見的案例的其中一個會將視訊透過串流處理的彈性位元速率。 Media Services 提供的動態封裝，可讓您 toodeliver 您彈性位元速率編碼的 MP4 內容串流處理媒體服務 (MPEG DASH、 HLS、 Smooth Streaming) 在 just-in-time，支援不需要您 toostore 預先封裝格式每種串流處理格式的版本。

>[!NOTE]
>AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。 串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。

toostart hello 串流端點，請執行下列 hello:

1. 在 hello 登入[Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 設定視窗中，按一下 串流端點。
3. 按一下 hello 預設串流端點。

    hello 預設串流端點詳細資料 視窗隨即出現。

4. 按一下 hello 入門圖示。
5. 按一下 hello 儲存按鈕 toosave 您的變更。

## <a name="create-and-configure-a-visual-studio-project"></a>建立和設定 Visual Studio 專案

1. 設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。 
2. 建立新的資料夾 （資料夾可以是任何位置在本機磁碟機上），並將您想要 tooencode 和資料流或漸進式下載.mp4 檔案複製。 在此範例中，會使用 hello"C:\VideoFiles 」 路徑。

## <a name="connect-toohello-media-services-account"></a>Toohello Media Services 帳戶連接

當搭配.NET 使用 Media Services，您必須使用 hello **CloudMediaContext**大部分的 Media Services 程式設計工作的類別： 連接 tooMedia 服務帳戶; 建立、 更新、 存取和刪除 hello 下列物件： 資產、 資產檔案、 作業、 存取原則、 locator、 等等。

下列程式碼的 hello，覆寫 hello 預設程式類別。 hello 程式碼會示範如何從 hello App.config 檔案的 tooread hello 連接值以及如何 toocreate hello **CloudMediaContext**順序 tooconnect tooMedia 中的物件會服務。 如需詳細資訊，請參閱[連接 toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md)。

請確定 tooupdate hello 檔案名稱和路徑 toowhere 您擁有您的媒體檔案。

hello **Main**函式呼叫將會定義的方法進一步這一節。

> [!NOTE]
> 您將會發生編譯錯誤直到新增所有的 hello 函式的定義。

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a>建立新資產並上傳視訊檔案

在媒體服務中，您可以將數位檔案上傳 (或內嵌) 到資產。 hello**資產**實體可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌及隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）Hello 檔案上傳，一旦您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。 hello 資產中的 hello 檔案被稱為**資產檔案**。

hello **UploadFile**方法呼叫底下定義**CreateFromFile** （定義於.NET SDK 延伸模組）。 **CreateFromFile**建立指定的來源檔案上傳到哪個 hello 新資產。

hello **CreateFromFile**方法會採用**AssetCreationOptions**可讓您指定 hello 下列資產建立選項的其中一個：

* **None** - 不使用加密。 這是 hello 預設值。 請注意，使用此選項時，您的內容在傳輸或儲存體中靜止時不會受到保護。
  如果您計畫使用漸進式下載 toodeliver MP4，請使用此選項。
* **StorageEncrypted** -使用此選項 tooencrypt 您使用進階加密標準 (AES)-256 位元加密，然後將它上載 tooAzure 儲存體的方式予以儲存加密在靜止在本機的清除內容。 使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。 儲存體加密的 hello 主要使用案例是當您想 toosecure 強式加密在靜止高品質的輸入的媒體檔案在磁碟上。
* **CommonEncryptionProtected** - 如果您要上傳已經使用一般加密或 PlayReady DRM (例如使用 PlayReady DRM 保護的 Smooth Streaming) 加密及保護的內容，請使用這個選項。
* **EnvelopeEncryptionProtected** – 如果您要上傳使用 AES 加密的 HLS，請使用這個選項。 請注意，hello 檔案必須具有已編碼，並由 Transform Manager 加密。

hello **CreateFromFile**方法也可讓您指定的回呼順序 tooreport hello 上傳進度的 hello 檔案中。

下列範例的 hello，指定**無**hello 資產選項。

新增下列方法 toohello Program 類別的 hello。

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a>Hello 原始程式檔編碼一組彈性位元速率 MP4 檔案
資產擷取到 Media Services 之後, 可以媒體編碼、 轉碼多工處理，浮水印等，再傳遞 tooclients。 這些活動均已排程，並針對多種背景角色執行個體 tooensure 高效能、 可用性執行。 這些活動稱為工作，以及每項作業是不可部分完成的工作，請勿 hello hello 資產檔案上的實際工作所組成。

如已先前所述，使用 Azure Media Services 時，其中一個 hello 最常見的案例會將自動調整位元速率串流 tooyour 用戶端。 Media Services 可以動態封裝成 hello 下列格式的其中一個的一組彈性位元速率 MP4 檔案： HTTP Live Streaming (HLS)、 Smooth Streaming 和 MPEG DASH。

tootake 利用動態封裝，您需要 tooencode 或轉碼夾層 （來源） 檔案到一組彈性位元速率 MP4 檔案或彈性位元速率 Smooth Streaming 檔案。  

下列程式碼的 hello 顯示 toosubmit 的編碼方式的工作。 hello 作業包含一項工作，指定成一組彈性位元速率 mp4 集使用 tootranscode hello 夾層檔**媒體編碼器標準**。 hello 程式碼會送出 hello 作業並等待直到完成為止。

Hello 作業完成後，您要能夠 toostream 資產或漸進式下載 MP4 檔案轉碼之後所建立。

新增下列方法 toohello Program 類別的 hello。

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a>發行 hello 資產，並取得資料流和漸進式下載 Url

toostream 或下載資產，您首先需要太 「 發行 」 它藉由建立定位器。 定位器提供存取 toofiles hello 資產中所包含。 Media Services 支援兩種類型的定位器： OnDemandOrigin 定位器，使用的 toostream 媒體 （例如，MPEG DASH、 HLS 或 Smooth Streaming） 和存取簽章 (SAS) 定位器，使用 （如需 SAS 定位器請參閱toodownload媒體檔案[這](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)部落格)。

### <a name="some-details-about-url-formats"></a>URL 格式的相關詳細資料

建立 hello 定位器之後，您可以建立要使用的 toostream 或下載檔案的 hello Url。 在此教學課程中的 hello 範例會輸出，您可以在適當的瀏覽器中貼上 Url。 本節只會提供不同格式外觀的簡短範例。

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a>適用於 MPEG DASH 串流 URL 具有下列格式的 hello:

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest**(format=mpd-time-csf)**

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a>HLS 的串流 URL 具有下列格式的 hello:

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest**(format=m3u8-aapl)**

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a>Smooth Streaming 的串流 URL 具有下列格式的 hello:

{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a>使用 SAS URL toodownload 檔案具有下列格式的 hello:

{blob 容器名稱}/{資產名稱}/{檔案名稱}/{SAS 簽章}

Media Services.NET SDK 延伸模組會提供便利的協助程式方法，傳回格式化 Url 的 hello 發行資產。

hello 下列程式碼使用.NET SDK Extensions toocreate 定位器、 tooget 串流和漸進式下載 Url。 hello 程式碼也會示範如何 toodownload 檔案 tooa 本機資料夾。

新增下列方法 toohello Program 類別的 hello。

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a>播放您的內容以進行測試

一旦您執行 hello 程式 hello 上一節中所定義，hello 類似 toohello 下列將顯示 hello 主控台視窗中的 Url。

調適性串流 URL：

Smooth Streaming

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

漸進式下載 URL (音訊和視訊)。

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


toostream 視訊中的 hello hello URL 文字方塊中貼上您的 URL [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。

tootest 漸進式下載，將 URL 貼到瀏覽器 （例如，Internet Explorer、 Chrome 或 Safari）。

如需詳細資訊，請參閱下列主題中的 hello:

- [使用現有播放器來播放您的內容](media-services-playback-content-with-existing-players.md)
- [開發視訊播放程式應用程式](media-services-develop-video-players.md)
- [透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a>下載範例
hello 下列程式碼範例包含您在本教學課程中建立的 hello 程式碼：[範例](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/)。

## <a name="next-steps"></a>後續步驟

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
