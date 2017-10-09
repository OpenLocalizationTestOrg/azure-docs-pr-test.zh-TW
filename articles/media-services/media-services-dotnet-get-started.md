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
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="6736c-103">使用 .NET SDK 傳遞點播內容入門</span><span class="sxs-lookup"><span data-stu-id="6736c-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="6736c-104">本教學課程會引導您實作基本的 Video-on-Demand (VoD) 內容傳遞服務與 Azure 媒體服務 (AMS) 應用程式使用 hello Azure Media Services.NET SDK 的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="6736c-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6736c-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="6736c-105">Prerequisites</span></span>

<span data-ttu-id="6736c-106">hello 下面是必要的 toocomplete hello 教學課程：</span><span class="sxs-lookup"><span data-stu-id="6736c-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="6736c-107">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6736c-107">An Azure account.</span></span> <span data-ttu-id="6736c-108">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6736c-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6736c-109">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="6736c-109">A Media Services account.</span></span> <span data-ttu-id="6736c-110">toocreate Media Services 帳戶，請參閱[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="6736c-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="6736c-111">.NET Framework 4.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6736c-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="6736c-112">Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6736c-112">Visual Studio.</span></span>

<span data-ttu-id="6736c-113">這個教學課程包括下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="6736c-113">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="6736c-114">啟動串流端點 （使用 hello Azure 入口網站）。</span><span class="sxs-lookup"><span data-stu-id="6736c-114">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="6736c-115">建立和設定 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="6736c-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="6736c-116">Toohello Media Services 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="6736c-116">Connect toohello Media Services account.</span></span>
2. <span data-ttu-id="6736c-117">上傳視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="6736c-117">Upload a video file.</span></span>
3. <span data-ttu-id="6736c-118">Hello 原始程式檔編碼為一組彈性位元速率 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="6736c-118">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="6736c-119">發佈 hello 資產和取得資料流和漸進式下載 Url。</span><span class="sxs-lookup"><span data-stu-id="6736c-119">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="6736c-120">播放您的內容。</span><span class="sxs-lookup"><span data-stu-id="6736c-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="6736c-121">概觀</span><span class="sxs-lookup"><span data-stu-id="6736c-121">Overview</span></span>
<span data-ttu-id="6736c-122">本教學課程將引導您完成 hello 步驟實作 Video-on-Demand (VoD) 傳遞內容的應用程式，使用 Azure 媒體服務 (AMS) SDK for.NET。</span><span class="sxs-lookup"><span data-stu-id="6736c-122">This tutorial walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="6736c-123">hello 教學課程介紹 hello 基本 Media Services 工作流程和 hello 最常見的程式設計物件，以及 Media Services 開發所需的工作。</span><span class="sxs-lookup"><span data-stu-id="6736c-123">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="6736c-124">在 hello 完成 hello 教學課程，您將會是能 toostream 或漸進式下載範例媒體檔案，您可以上傳、 編碼，以及下載。</span><span class="sxs-lookup"><span data-stu-id="6736c-124">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="6736c-125">AMS 模型</span><span class="sxs-lookup"><span data-stu-id="6736c-125">AMS model</span></span>

<span data-ttu-id="6736c-126">hello 下圖顯示一些最常用的 hello 物件開發 VoD 針對 hello 媒體服務 OData 模型的應用程式時。</span><span class="sxs-lookup"><span data-stu-id="6736c-126">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="6736c-127">按一下 hello 映像 tooview 它的完整大小。</span><span class="sxs-lookup"><span data-stu-id="6736c-127">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="6736c-128">您可以檢視整個模型的 hello[這裡](https://media.windows.net/API/$metadata?api-version=2.15)。</span><span class="sxs-lookup"><span data-stu-id="6736c-128">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="6736c-129">啟動串流端點使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6736c-129">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="6736c-130">當使用 Azure Media Services hello 最常見的案例的其中一個會將視訊透過串流處理的彈性位元速率。</span><span class="sxs-lookup"><span data-stu-id="6736c-130">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="6736c-131">Media Services 提供的動態封裝，可讓您 toodeliver 您彈性位元速率編碼的 MP4 內容串流處理媒體服務 (MPEG DASH、 HLS、 Smooth Streaming) 在 just-in-time，支援不需要您 toostore 預先封裝格式每種串流處理格式的版本。</span><span class="sxs-lookup"><span data-stu-id="6736c-131">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="6736c-132">AMS 帳戶建立時**預設**串流端點就會加入 tooyour 帳戶 hello**已停止**狀態。</span><span class="sxs-lookup"><span data-stu-id="6736c-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="6736c-133">串流處理您的內容，並採取利用動態封裝和動態加密，toostart hello 串流端點，您想要從中 toostream 內容已經在 hello toobe**執行**狀態。</span><span class="sxs-lookup"><span data-stu-id="6736c-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="6736c-134">toostart hello 串流端點，請執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="6736c-134">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="6736c-135">在 hello 登入[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6736c-135">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6736c-136">在 hello 設定視窗中，按一下 串流端點。</span><span class="sxs-lookup"><span data-stu-id="6736c-136">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="6736c-137">按一下 hello 預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="6736c-137">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="6736c-138">hello 預設串流端點詳細資料 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6736c-138">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="6736c-139">按一下 hello 入門圖示。</span><span class="sxs-lookup"><span data-stu-id="6736c-139">Click hello Start icon.</span></span>
5. <span data-ttu-id="6736c-140">按一下 hello 儲存按鈕 toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="6736c-140">Click hello Save button toosave your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="6736c-141">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="6736c-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="6736c-142">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="6736c-142">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="6736c-143">建立新的資料夾 （資料夾可以是任何位置在本機磁碟機上），並將您想要 tooencode 和資料流或漸進式下載.mp4 檔案複製。</span><span class="sxs-lookup"><span data-stu-id="6736c-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="6736c-144">在此範例中，會使用 hello"C:\VideoFiles 」 路徑。</span><span class="sxs-lookup"><span data-stu-id="6736c-144">In this example, hello "C:\VideoFiles" path is used.</span></span>

## <a name="connect-toohello-media-services-account"></a><span data-ttu-id="6736c-145">Toohello Media Services 帳戶連接</span><span class="sxs-lookup"><span data-stu-id="6736c-145">Connect toohello Media Services account</span></span>

<span data-ttu-id="6736c-146">當搭配.NET 使用 Media Services，您必須使用 hello **CloudMediaContext**大部分的 Media Services 程式設計工作的類別： 連接 tooMedia 服務帳戶; 建立、 更新、 存取和刪除 hello 下列物件： 資產、 資產檔案、 作業、 存取原則、 locator、 等等。</span><span class="sxs-lookup"><span data-stu-id="6736c-146">When using Media Services with .NET, you must use hello **CloudMediaContext** class for most Media Services programming tasks: connecting tooMedia Services account; creating, updating, accessing, and deleting hello following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="6736c-147">下列程式碼的 hello，覆寫 hello 預設程式類別。</span><span class="sxs-lookup"><span data-stu-id="6736c-147">Overwrite hello default Program class with hello following code.</span></span> <span data-ttu-id="6736c-148">hello 程式碼會示範如何從 hello App.config 檔案的 tooread hello 連接值以及如何 toocreate hello **CloudMediaContext**順序 tooconnect tooMedia 中的物件會服務。</span><span class="sxs-lookup"><span data-stu-id="6736c-148">hello code demonstrates how tooread hello connection values from hello App.config file and how toocreate hello **CloudMediaContext** object in order tooconnect tooMedia Services.</span></span> <span data-ttu-id="6736c-149">如需詳細資訊，請參閱[連接 toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="6736c-149">For more information, see [connecting toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="6736c-150">請確定 tooupdate hello 檔案名稱和路徑 toowhere 您擁有您的媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="6736c-150">Make sure tooupdate hello file name and path toowhere you have your media file.</span></span>

<span data-ttu-id="6736c-151">hello **Main**函式呼叫將會定義的方法進一步這一節。</span><span class="sxs-lookup"><span data-stu-id="6736c-151">hello **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="6736c-152">您將會發生編譯錯誤直到新增所有的 hello 函式的定義。</span><span class="sxs-lookup"><span data-stu-id="6736c-152">You will be getting compilation errors until you add definitions for all hello functions.</span></span>

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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="6736c-153">建立新資產並上傳視訊檔案</span><span class="sxs-lookup"><span data-stu-id="6736c-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="6736c-154">在媒體服務中，您可以將數位檔案上傳 (或內嵌) 到資產。</span><span class="sxs-lookup"><span data-stu-id="6736c-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="6736c-155">hello**資產**實體可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌及隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）Hello 檔案上傳，一旦您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。</span><span class="sxs-lookup"><span data-stu-id="6736c-155">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> <span data-ttu-id="6736c-156">hello 資產中的 hello 檔案被稱為**資產檔案**。</span><span class="sxs-lookup"><span data-stu-id="6736c-156">hello files in hello asset are called **Asset Files**.</span></span>

<span data-ttu-id="6736c-157">hello **UploadFile**方法呼叫底下定義**CreateFromFile** （定義於.NET SDK 延伸模組）。</span><span class="sxs-lookup"><span data-stu-id="6736c-157">hello **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="6736c-158">**CreateFromFile**建立指定的來源檔案上傳到哪個 hello 新資產。</span><span class="sxs-lookup"><span data-stu-id="6736c-158">**CreateFromFile** creates a new asset into which hello specified source file is uploaded.</span></span>

<span data-ttu-id="6736c-159">hello **CreateFromFile**方法會採用**AssetCreationOptions**可讓您指定 hello 下列資產建立選項的其中一個：</span><span class="sxs-lookup"><span data-stu-id="6736c-159">hello **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of hello following asset creation options:</span></span>

* <span data-ttu-id="6736c-160">**None** - 不使用加密。</span><span class="sxs-lookup"><span data-stu-id="6736c-160">**None** - No encryption is used.</span></span> <span data-ttu-id="6736c-161">這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="6736c-161">This is hello default value.</span></span> <span data-ttu-id="6736c-162">請注意，使用此選項時，您的內容在傳輸或儲存體中靜止時不會受到保護。</span><span class="sxs-lookup"><span data-stu-id="6736c-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="6736c-163">如果您計畫使用漸進式下載 toodeliver MP4，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="6736c-163">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="6736c-164">**StorageEncrypted** -使用此選項 tooencrypt 您使用進階加密標準 (AES)-256 位元加密，然後將它上載 tooAzure 儲存體的方式予以儲存加密在靜止在本機的清除內容。</span><span class="sxs-lookup"><span data-stu-id="6736c-164">**StorageEncrypted** - Use this option tooencrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="6736c-165">使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。</span><span class="sxs-lookup"><span data-stu-id="6736c-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="6736c-166">儲存體加密的 hello 主要使用案例是當您想 toosecure 強式加密在靜止高品質的輸入的媒體檔案在磁碟上。</span><span class="sxs-lookup"><span data-stu-id="6736c-166">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="6736c-167">**CommonEncryptionProtected** - 如果您要上傳已經使用一般加密或 PlayReady DRM (例如使用 PlayReady DRM 保護的 Smooth Streaming) 加密及保護的內容，請使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="6736c-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="6736c-168">**EnvelopeEncryptionProtected** – 如果您要上傳使用 AES 加密的 HLS，請使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="6736c-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="6736c-169">請注意，hello 檔案必須具有已編碼，並由 Transform Manager 加密。</span><span class="sxs-lookup"><span data-stu-id="6736c-169">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="6736c-170">hello **CreateFromFile**方法也可讓您指定的回呼順序 tooreport hello 上傳進度的 hello 檔案中。</span><span class="sxs-lookup"><span data-stu-id="6736c-170">hello **CreateFromFile** method also lets you specify a callback in order tooreport hello upload progress of hello file.</span></span>

<span data-ttu-id="6736c-171">下列範例的 hello，指定**無**hello 資產選項。</span><span class="sxs-lookup"><span data-stu-id="6736c-171">In hello following example, we specify **None** for hello asset options.</span></span>

<span data-ttu-id="6736c-172">新增下列方法 toohello Program 類別的 hello。</span><span class="sxs-lookup"><span data-stu-id="6736c-172">Add hello following method toohello Program class.</span></span>

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


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="6736c-173">Hello 原始程式檔編碼一組彈性位元速率 MP4 檔案</span><span class="sxs-lookup"><span data-stu-id="6736c-173">Encode hello source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="6736c-174">資產擷取到 Media Services 之後, 可以媒體編碼、 轉碼多工處理，浮水印等，再傳遞 tooclients。</span><span class="sxs-lookup"><span data-stu-id="6736c-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="6736c-175">這些活動均已排程，並針對多種背景角色執行個體 tooensure 高效能、 可用性執行。</span><span class="sxs-lookup"><span data-stu-id="6736c-175">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="6736c-176">這些活動稱為工作，以及每項作業是不可部分完成的工作，請勿 hello hello 資產檔案上的實際工作所組成。</span><span class="sxs-lookup"><span data-stu-id="6736c-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do hello actual work on hello Asset file.</span></span>

<span data-ttu-id="6736c-177">如已先前所述，使用 Azure Media Services 時，其中一個 hello 最常見的案例會將自動調整位元速率串流 tooyour 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6736c-177">As was mentioned earlier, when working with Azure Media Services, one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="6736c-178">Media Services 可以動態封裝成 hello 下列格式的其中一個的一組彈性位元速率 MP4 檔案： HTTP Live Streaming (HLS)、 Smooth Streaming 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="6736c-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="6736c-179">tootake 利用動態封裝，您需要 tooencode 或轉碼夾層 （來源） 檔案到一組彈性位元速率 MP4 檔案或彈性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="6736c-179">tootake advantage of dynamic packaging, you need tooencode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="6736c-180">下列程式碼的 hello 顯示 toosubmit 的編碼方式的工作。</span><span class="sxs-lookup"><span data-stu-id="6736c-180">hello following code shows how toosubmit an encoding job.</span></span> <span data-ttu-id="6736c-181">hello 作業包含一項工作，指定成一組彈性位元速率 mp4 集使用 tootranscode hello 夾層檔**媒體編碼器標準**。</span><span class="sxs-lookup"><span data-stu-id="6736c-181">hello job contains one task that specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="6736c-182">hello 程式碼會送出 hello 作業並等待直到完成為止。</span><span class="sxs-lookup"><span data-stu-id="6736c-182">hello code submits hello job and waits until it is completed.</span></span>

<span data-ttu-id="6736c-183">Hello 作業完成後，您要能夠 toostream 資產或漸進式下載 MP4 檔案轉碼之後所建立。</span><span class="sxs-lookup"><span data-stu-id="6736c-183">Once hello job is completed, you would be able toostream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="6736c-184">新增下列方法 toohello Program 類別的 hello。</span><span class="sxs-lookup"><span data-stu-id="6736c-184">Add hello following method toohello Program class.</span></span>

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

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="6736c-185">發行 hello 資產，並取得資料流和漸進式下載 Url</span><span class="sxs-lookup"><span data-stu-id="6736c-185">Publish hello asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="6736c-186">toostream 或下載資產，您首先需要太 「 發行 」 它藉由建立定位器。</span><span class="sxs-lookup"><span data-stu-id="6736c-186">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="6736c-187">定位器提供存取 toofiles hello 資產中所包含。</span><span class="sxs-lookup"><span data-stu-id="6736c-187">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="6736c-188">Media Services 支援兩種類型的定位器： OnDemandOrigin 定位器，使用的 toostream 媒體 （例如，MPEG DASH、 HLS 或 Smooth Streaming） 和存取簽章 (SAS) 定位器，使用 （如需 SAS 定位器請參閱toodownload媒體檔案[這](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)部落格)。</span><span class="sxs-lookup"><span data-stu-id="6736c-188">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="6736c-189">URL 格式的相關詳細資料</span><span class="sxs-lookup"><span data-stu-id="6736c-189">Some details about URL formats</span></span>

<span data-ttu-id="6736c-190">建立 hello 定位器之後，您可以建立要使用的 toostream 或下載檔案的 hello Url。</span><span class="sxs-lookup"><span data-stu-id="6736c-190">After you create hello locators, you can build hello URLs that would be used toostream or download your files.</span></span> <span data-ttu-id="6736c-191">在此教學課程中的 hello 範例會輸出，您可以在適當的瀏覽器中貼上 Url。</span><span class="sxs-lookup"><span data-stu-id="6736c-191">hello sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="6736c-192">本節只會提供不同格式外觀的簡短範例。</span><span class="sxs-lookup"><span data-stu-id="6736c-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a><span data-ttu-id="6736c-193">適用於 MPEG DASH 串流 URL 具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="6736c-193">A streaming URL for MPEG DASH has hello following format:</span></span>

<span data-ttu-id="6736c-194">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="6736c-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a><span data-ttu-id="6736c-195">HLS 的串流 URL 具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="6736c-195">A streaming URL for HLS has hello following format:</span></span>

<span data-ttu-id="6736c-196">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="6736c-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a><span data-ttu-id="6736c-197">Smooth Streaming 的串流 URL 具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="6736c-197">A streaming URL for Smooth Streaming has hello following format:</span></span>

<span data-ttu-id="6736c-198">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="6736c-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a><span data-ttu-id="6736c-199">使用 SAS URL toodownload 檔案具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="6736c-199">A SAS URL used toodownload files has hello following format:</span></span>

<span data-ttu-id="6736c-200">{blob 容器名稱}/{資產名稱}/{檔案名稱}/{SAS 簽章}</span><span class="sxs-lookup"><span data-stu-id="6736c-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="6736c-201">Media Services.NET SDK 延伸模組會提供便利的協助程式方法，傳回格式化 Url 的 hello 發行資產。</span><span class="sxs-lookup"><span data-stu-id="6736c-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for hello published asset.</span></span>

<span data-ttu-id="6736c-202">hello 下列程式碼使用.NET SDK Extensions toocreate 定位器、 tooget 串流和漸進式下載 Url。</span><span class="sxs-lookup"><span data-stu-id="6736c-202">hello following code uses .NET SDK Extensions toocreate locators and tooget streaming and progressive download URLs.</span></span> <span data-ttu-id="6736c-203">hello 程式碼也會示範如何 toodownload 檔案 tooa 本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="6736c-203">hello code also shows how toodownload files tooa local folder.</span></span>

<span data-ttu-id="6736c-204">新增下列方法 toohello Program 類別的 hello。</span><span class="sxs-lookup"><span data-stu-id="6736c-204">Add hello following method toohello Program class.</span></span>

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

## <a name="test-by-playing-your-content"></a><span data-ttu-id="6736c-205">播放您的內容以進行測試</span><span class="sxs-lookup"><span data-stu-id="6736c-205">Test by playing your content</span></span>

<span data-ttu-id="6736c-206">一旦您執行 hello 程式 hello 上一節中所定義，hello 類似 toohello 下列將顯示 hello 主控台視窗中的 Url。</span><span class="sxs-lookup"><span data-stu-id="6736c-206">Once you run hello program defined in hello previous section, hello URLs similar toohello following will be displayed in hello console window.</span></span>

<span data-ttu-id="6736c-207">調適性串流 URL：</span><span class="sxs-lookup"><span data-stu-id="6736c-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="6736c-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="6736c-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="6736c-209">HLS</span><span class="sxs-lookup"><span data-stu-id="6736c-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="6736c-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="6736c-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="6736c-211">漸進式下載 URL (音訊和視訊)。</span><span class="sxs-lookup"><span data-stu-id="6736c-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="6736c-212">toostream 視訊中的 hello hello URL 文字方塊中貼上您的 URL [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)。</span><span class="sxs-lookup"><span data-stu-id="6736c-212">toostream your video, paste your URL in hello URL textbox in hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="6736c-213">tootest 漸進式下載，將 URL 貼到瀏覽器 （例如，Internet Explorer、 Chrome 或 Safari）。</span><span class="sxs-lookup"><span data-stu-id="6736c-213">tootest progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="6736c-214">如需詳細資訊，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="6736c-214">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="6736c-215">使用現有播放器來播放您的內容</span><span class="sxs-lookup"><span data-stu-id="6736c-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="6736c-216">開發視訊播放程式應用程式</span><span class="sxs-lookup"><span data-stu-id="6736c-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="6736c-217">透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式</span><span class="sxs-lookup"><span data-stu-id="6736c-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="6736c-218">下載範例</span><span class="sxs-lookup"><span data-stu-id="6736c-218">Download sample</span></span>
<span data-ttu-id="6736c-219">hello 下列程式碼範例包含您在本教學課程中建立的 hello 程式碼：[範例](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/)。</span><span class="sxs-lookup"><span data-stu-id="6736c-219">hello following code sample contains hello code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6736c-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6736c-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6736c-221">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="6736c-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
