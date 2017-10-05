---
title: "使用 .NET 傳遞點播內容入門 | Microsoft Docs"
description: "本教學課程會逐步完成使用 .NET 實作含 Azure 媒體服務的點播內容傳遞應用程式。"
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
ms.openlocfilehash: f0be787ba1ccee067fb1d7e6a6554be32f886089
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="94beb-103">使用 .NET SDK 傳遞點播內容入門</span><span class="sxs-lookup"><span data-stu-id="94beb-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="94beb-104">本教學課程會逐步引導您使用 Azure 媒體服務 .NET SDK 實作含 Azure 媒體服務 (AMS) 應用程式的基本點播視訊 (VoD) 內容傳遞服務。</span><span class="sxs-lookup"><span data-stu-id="94beb-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94beb-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="94beb-105">Prerequisites</span></span>

<span data-ttu-id="94beb-106">需要有下列項目，才能完成教學課程：</span><span class="sxs-lookup"><span data-stu-id="94beb-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="94beb-107">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="94beb-107">An Azure account.</span></span> <span data-ttu-id="94beb-108">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="94beb-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="94beb-109">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="94beb-109">A Media Services account.</span></span> <span data-ttu-id="94beb-110">若要建立媒體服務帳戶，請參閱[如何建立媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="94beb-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="94beb-111">.NET Framework 4.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="94beb-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="94beb-112">Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="94beb-112">Visual Studio.</span></span>

<span data-ttu-id="94beb-113">本教學課程內容包括以下工作：</span><span class="sxs-lookup"><span data-stu-id="94beb-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="94beb-114">啟動串流端點 (使用 Azure 入口網站)。</span><span class="sxs-lookup"><span data-stu-id="94beb-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="94beb-115">建立和設定 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="94beb-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="94beb-116">連線到媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="94beb-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="94beb-117">上傳視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="94beb-117">Upload a video file.</span></span>
3. <span data-ttu-id="94beb-118">將來源檔案編碼為一組自適性 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="94beb-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="94beb-119">發佈資產並取得串流和漸進式下載 URL。</span><span class="sxs-lookup"><span data-stu-id="94beb-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="94beb-120">播放您的內容。</span><span class="sxs-lookup"><span data-stu-id="94beb-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="94beb-121">概觀</span><span class="sxs-lookup"><span data-stu-id="94beb-121">Overview</span></span>
<span data-ttu-id="94beb-122">本教學課程會逐步完成使用 Azure Media Services (AMS) SDK for .NET 實作點播視訊 (VoD) 內容傳遞應用程式。</span><span class="sxs-lookup"><span data-stu-id="94beb-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="94beb-123">教學課程中介紹基本的媒體服務工作流程，以及媒體服務開發最常用的程式設計物件和必要工作。</span><span class="sxs-lookup"><span data-stu-id="94beb-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="94beb-124">完成本教學課程時，您將能夠串流或漸進式下載您已上傳、編碼和下載的範例媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="94beb-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="94beb-125">AMS 模型</span><span class="sxs-lookup"><span data-stu-id="94beb-125">AMS model</span></span>

<span data-ttu-id="94beb-126">下列影像顯示針對媒體服務 OData 模型開發 VoD 應用程式時一些最常用的物件。</span><span class="sxs-lookup"><span data-stu-id="94beb-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="94beb-127">按一下影像可以完整大小檢視。</span><span class="sxs-lookup"><span data-stu-id="94beb-127">Click the image to view it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="94beb-128">您可以[在此](https://media.windows.net/API/$metadata?api-version=2.15)檢視整個模型。</span><span class="sxs-lookup"><span data-stu-id="94beb-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="94beb-129">使用 Azure 入口網站開始串流端點</span><span class="sxs-lookup"><span data-stu-id="94beb-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="94beb-130">使用 Azure 媒體服務時，其中一個最常見的案例是透過自適性串流提供影片。</span><span class="sxs-lookup"><span data-stu-id="94beb-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="94beb-131">媒體服務提供動態封裝，這讓您以媒體服務即時支援的串流格式 (MPEG DASH、HLS、Smooth Streaming) 提供自適性 MP4 編碼內容，而不必儲存這些串流格式個別的預先封裝版本。</span><span class="sxs-lookup"><span data-stu-id="94beb-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="94beb-132">建立 AMS 帳戶時，**預設**串流端點會新增至 [已停止] 狀態的帳戶。</span><span class="sxs-lookup"><span data-stu-id="94beb-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="94beb-133">若要開始串流內容並利用動態封裝和動態加密功能，您想要串流內容的串流端點必須處於 [執行中] 狀態。</span><span class="sxs-lookup"><span data-stu-id="94beb-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="94beb-134">若要啟動串流端點，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="94beb-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="94beb-135">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="94beb-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="94beb-136">在 [設定] 視窗中，按一下 [串流端點]。</span><span class="sxs-lookup"><span data-stu-id="94beb-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="94beb-137">按一下預設串流端點。</span><span class="sxs-lookup"><span data-stu-id="94beb-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="94beb-138">[預設串流端點詳細資料] 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="94beb-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="94beb-139">按一下 [啟動] 圖示。</span><span class="sxs-lookup"><span data-stu-id="94beb-139">Click the Start icon.</span></span>
5. <span data-ttu-id="94beb-140">按一下 [儲存] 按鈕以儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="94beb-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="94beb-141">建立和設定 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="94beb-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="94beb-142">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)所述。</span><span class="sxs-lookup"><span data-stu-id="94beb-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="94beb-143">建立新的資料夾 (資料夾可在本機磁碟機上任意處)，並複製您想要編碼和串流處理或漸進式下載的 .mp4 檔案。</span><span class="sxs-lookup"><span data-stu-id="94beb-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="94beb-144">在此範例中，使用 "C:\VideoFiles" 路徑。</span><span class="sxs-lookup"><span data-stu-id="94beb-144">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="94beb-145">連線到媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="94beb-145">Connect to the Media Services account</span></span>

<span data-ttu-id="94beb-146">搭配使用媒體服務與 .NET 時，您必須將 **CloudMediaContext** 類別用於大部分的媒體服務程式設計工作：連線到媒體服務帳戶；建立、更新、存取和刪除下列物件：資產、資產檔案、工作、存取原則、定位器等。</span><span class="sxs-lookup"><span data-stu-id="94beb-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="94beb-147">將預設 Program 類別覆寫為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="94beb-147">Overwrite the default Program class with the following code.</span></span> <span data-ttu-id="94beb-148">此程式碼示範如何讀取 App.config 檔案中的連線值，以及如何建立 **CloudMediaContext** 物件來連線到媒體服務。</span><span class="sxs-lookup"><span data-stu-id="94beb-148">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="94beb-149">如需詳細資訊，請參閱[連線至媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="94beb-149">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="94beb-150">務必更新您的媒體檔案的檔案名稱和路徑。</span><span class="sxs-lookup"><span data-stu-id="94beb-150">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="94beb-151">**Main** 函數會呼叫未來將在此區段中定義的方法。</span><span class="sxs-lookup"><span data-stu-id="94beb-151">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="94beb-152">除非您加入所有函式的定義，否則將會出現編譯錯誤。</span><span class="sxs-lookup"><span data-stu-id="94beb-152">You will be getting compilation errors until you add definitions for all the functions.</span></span>

    class Program
    {
        // Read values from the App.config file.
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

            // Add calls to methods defined in this section.
            // Make sure to update the file name and path to where you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse the XML error message in the Media Services response and create a new
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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="94beb-153">建立新資產並上傳視訊檔案</span><span class="sxs-lookup"><span data-stu-id="94beb-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="94beb-154">在媒體服務中，您可以將數位檔案上傳 (或內嵌) 到資產。</span><span class="sxs-lookup"><span data-stu-id="94beb-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="94beb-155">**資產**實體可以包含視訊、音訊、影像、縮圖集合、文字播放軌及隱藏式輔助字幕檔案 (以及這些檔案的相關中繼資料)。上傳檔案之後，您的內容會安全地儲存在雲端，以進一步進行處理和串流處理。</span><span class="sxs-lookup"><span data-stu-id="94beb-155">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="94beb-156">資產中的檔案稱為 **資產檔案**。</span><span class="sxs-lookup"><span data-stu-id="94beb-156">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="94beb-157">下面所定義的 **UploadFile** 方法會呼叫 **CreateFromFile** (定義於 .NET SDK 延伸模組中)。</span><span class="sxs-lookup"><span data-stu-id="94beb-157">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="94beb-158">**CreateFromFile** 會建立要在其中上傳指定來源檔案的新資產。</span><span class="sxs-lookup"><span data-stu-id="94beb-158">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="94beb-159">**CreateFromFile** 方法會採用 **AssetCreationOptions**，以讓您指定下列其中一個資產建立選項：</span><span class="sxs-lookup"><span data-stu-id="94beb-159">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="94beb-160">**None** - 不使用加密。</span><span class="sxs-lookup"><span data-stu-id="94beb-160">**None** - No encryption is used.</span></span> <span data-ttu-id="94beb-161">這是預設值。</span><span class="sxs-lookup"><span data-stu-id="94beb-161">This is the default value.</span></span> <span data-ttu-id="94beb-162">請注意，使用此選項時，您的內容在傳輸或儲存體中靜止時不會受到保護。</span><span class="sxs-lookup"><span data-stu-id="94beb-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="94beb-163">如果您計劃使用漸進式下載傳遞 MP4，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="94beb-163">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="94beb-164">**StorageEncrypted** - 請使用此選項來利用進階加密標準 (AES) 256 位元加密，對您的純文字內容進行本機加密，然後會將它上傳到已靜止加密儲存的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="94beb-164">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="94beb-165">以儲存體加密保護的資產會自動解除加密並在編碼前放置在加密的檔案系統中，並且會在上傳為新輸出資產之前選擇性地重新編碼。</span><span class="sxs-lookup"><span data-stu-id="94beb-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="94beb-166">儲存體加密的主要使用案例是讓您可以使用強式加密來保護磁碟中靜止的高品質輸入媒體檔。</span><span class="sxs-lookup"><span data-stu-id="94beb-166">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="94beb-167">**CommonEncryptionProtected** - 如果您要上傳已經使用一般加密或 PlayReady DRM (例如使用 PlayReady DRM 保護的 Smooth Streaming) 加密及保護的內容，請使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="94beb-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="94beb-168">**EnvelopeEncryptionProtected** – 如果您要上傳使用 AES 加密的 HLS，請使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="94beb-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="94beb-169">請注意，檔案必須已由 Transform Manager 編碼和加密。</span><span class="sxs-lookup"><span data-stu-id="94beb-169">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="94beb-170">**CreateFromFile** 方法也可讓您指定回呼，以報告檔案的上傳進度。</span><span class="sxs-lookup"><span data-stu-id="94beb-170">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="94beb-171">在下列範例中，我們將資產選項指定為 **None** 。</span><span class="sxs-lookup"><span data-stu-id="94beb-171">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="94beb-172">將下列方法新增至 Program 類別。</span><span class="sxs-lookup"><span data-stu-id="94beb-172">Add the following method to the Program class.</span></span>

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


## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="94beb-173">將來源檔案編碼為一組調適性位元速率 MP4 檔案</span><span class="sxs-lookup"><span data-stu-id="94beb-173">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="94beb-174">將資產內嵌到媒體服務之後，可以先將媒體編碼、轉碼多工處理、加上浮水印等，再傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="94beb-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="94beb-175">這些活動會針對多個背景角色執行個體排定和執行，以確保高效能與可用性。</span><span class="sxs-lookup"><span data-stu-id="94beb-175">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="94beb-176">這些活動稱為作業，每個作業包含對資產檔案執行實際工作的不可部分完成的工作。</span><span class="sxs-lookup"><span data-stu-id="94beb-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="94beb-177">如稍早所提及，使用 Azure 媒體服務時，其中一個最常見的案例是將調適性位元速率串流傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="94beb-177">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="94beb-178">媒體服務可以以下列其中一種格式動態封裝一組可調位元速率 MP4 檔案：HTTP 即時串流 (HLS)、Smooth Streaming 和 MPEG DASH。</span><span class="sxs-lookup"><span data-stu-id="94beb-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="94beb-179">若要利用動態封裝功能，您必須將您的夾層 (來源) 檔編碼或轉換為一組調適性位元速率 MP4 檔案或調適性位元速率 Smooth Streaming 檔案。</span><span class="sxs-lookup"><span data-stu-id="94beb-179">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="94beb-180">下列程式碼顯示如何提交編碼工作。</span><span class="sxs-lookup"><span data-stu-id="94beb-180">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="94beb-181">此工作包含一項作業，指定使用 **媒體編碼器標準**，將夾層檔轉碼為一組調適性位元速率 MP4。</span><span class="sxs-lookup"><span data-stu-id="94beb-181">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="94beb-182">此程式碼會提交工作，並等到工作完成。</span><span class="sxs-lookup"><span data-stu-id="94beb-182">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="94beb-183">工作完成之後，就可以串流處理資產，或漸進式下載轉碼後所建立的 MP4 檔案。</span><span class="sxs-lookup"><span data-stu-id="94beb-183">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="94beb-184">將下列方法新增至 Program 類別。</span><span class="sxs-lookup"><span data-stu-id="94beb-184">Add the following method to the Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task to transcode the specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit the job and wait until it is completed.
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

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="94beb-185">發佈資產並取得串流和漸進式下載 URL。</span><span class="sxs-lookup"><span data-stu-id="94beb-185">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="94beb-186">若要串流處理或下載資產，您必須先建立定位器來「發佈」它。</span><span class="sxs-lookup"><span data-stu-id="94beb-186">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="94beb-187">定位器提供對於資產中包含之檔案的存取。</span><span class="sxs-lookup"><span data-stu-id="94beb-187">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="94beb-188">媒體服務支援兩種類型的定位器：OnDemandOrigin 定位器，用於串流媒體 (例如，MPEG DASH、HLS 或 Smooth Streaming) 和存取簽章 (SAS) 定位器，用來下載媒體檔案 (如需 SAS 定位器的詳細資訊，請參閱[這個](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)部落格)。</span><span class="sxs-lookup"><span data-stu-id="94beb-188">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="94beb-189">URL 格式的相關詳細資料</span><span class="sxs-lookup"><span data-stu-id="94beb-189">Some details about URL formats</span></span>

<span data-ttu-id="94beb-190">建立定位器之後，您便可以建立用來串流或下載檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="94beb-190">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="94beb-191">本教學課程中的範例會輸出您可貼在適當瀏覽器中的 URL。</span><span class="sxs-lookup"><span data-stu-id="94beb-191">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="94beb-192">本節只會提供不同格式外觀的簡短範例。</span><span class="sxs-lookup"><span data-stu-id="94beb-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="94beb-193">MPEG DASH 的串流 URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="94beb-193">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="94beb-194">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="94beb-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="94beb-195">HLS 的串流 URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="94beb-195">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="94beb-196">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="94beb-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="94beb-197">Smooth Streaming 的串流 URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="94beb-197">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="94beb-198">{串流端點名稱-媒體服務帳戶名稱}.streaming.mediaservices.windows.net/{定位器識別碼}/{檔案名稱}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="94beb-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="94beb-199">用來下載檔案的 SAS URL 具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="94beb-199">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="94beb-200">{blob 容器名稱}/{資產名稱}/{檔案名稱}/{SAS 簽章}</span><span class="sxs-lookup"><span data-stu-id="94beb-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="94beb-201">Media Services .NET SDK 延伸模組提供便利的協助程式方法，來傳回所發佈資產的格式化 URL。</span><span class="sxs-lookup"><span data-stu-id="94beb-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="94beb-202">下列程式碼使用 .NET SDK 延伸模組來建立定位器、取得串流，以及漸進式下載 URL。</span><span class="sxs-lookup"><span data-stu-id="94beb-202">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="94beb-203">此程式碼也會顯示如何將檔案下載到本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="94beb-203">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="94beb-204">將下列方法新增至 Program 類別。</span><span class="sxs-lookup"><span data-stu-id="94beb-204">Add the following method to the Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish the output asset by creating an Origin locator for adaptive streaming,
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

        // Get the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and the Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get the URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  the streaming URLs.
        Console.WriteLine("Use the following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display the URLs for progressive download.
        Console.WriteLine("Use the following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download the output asset to a local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files to a local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="94beb-205">播放您的內容以進行測試</span><span class="sxs-lookup"><span data-stu-id="94beb-205">Test by playing your content</span></span>

<span data-ttu-id="94beb-206">執行上一節中所定義的程式之後，主控台視窗中會顯示與下面類似的 URL。</span><span class="sxs-lookup"><span data-stu-id="94beb-206">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="94beb-207">調適性串流 URL：</span><span class="sxs-lookup"><span data-stu-id="94beb-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="94beb-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="94beb-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="94beb-209">HLS</span><span class="sxs-lookup"><span data-stu-id="94beb-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="94beb-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="94beb-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="94beb-211">漸進式下載 URL (音訊和視訊)。</span><span class="sxs-lookup"><span data-stu-id="94beb-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="94beb-212">若要串流處理視訊，請將您的 URL 貼在 [Azure 媒體服務播放器](http://amsplayer.azurewebsites.net/azuremediaplayer.html)的 [URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="94beb-212">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="94beb-213">若要測試漸進式下載，請將 URL 貼入瀏覽器 (例如，Internet Explorer、Chrome 或 Safari)。</span><span class="sxs-lookup"><span data-stu-id="94beb-213">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="94beb-214">如需詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="94beb-214">For more information, see the following topics:</span></span>

- [<span data-ttu-id="94beb-215">使用現有播放器來播放您的內容</span><span class="sxs-lookup"><span data-stu-id="94beb-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="94beb-216">開發視訊播放程式應用程式</span><span class="sxs-lookup"><span data-stu-id="94beb-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="94beb-217">透過 DASH.js 將 MPEG-DASH 彈性資料流視訊嵌入到 HTML5 應用程式</span><span class="sxs-lookup"><span data-stu-id="94beb-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="94beb-218">下載範例</span><span class="sxs-lookup"><span data-stu-id="94beb-218">Download sample</span></span>
<span data-ttu-id="94beb-219">下列程式碼範例包含您在本教學課程中建立的程式碼︰[範例](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/)。</span><span class="sxs-lookup"><span data-stu-id="94beb-219">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="94beb-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94beb-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="94beb-221">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="94beb-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
