---
title: "使用適用於.NET 的 Media Services 帳戶將 aaaUpload 檔案 |Microsoft 文件"
description: "了解如何 tooget 媒體內容至媒體服務建立和上傳資產。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="cd6bd-103">使用 .NET 將檔案上傳至媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="cd6bd-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd6bd-104">.NET</span><span class="sxs-lookup"><span data-stu-id="cd6bd-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="cd6bd-105">REST</span><span class="sxs-lookup"><span data-stu-id="cd6bd-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="cd6bd-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="cd6bd-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="cd6bd-107">在媒體服務中，您可以將數位檔案上傳 (或內嵌) 到資產。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="cd6bd-108">hello**資產**實體可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌和隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）Hello 檔案上傳，一旦您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="cd6bd-109">hello 資產中的 hello 檔案被稱為**資產檔案**。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="cd6bd-110">hello **AssetFile**執行個體與 hello 實際媒體檔案的兩個相異的物件。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="cd6bd-111">hello AssetFile 執行個體包含 hello 媒體檔案的相關中繼資料，而 hello 媒體檔案包含 hello 實際的媒體內容。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="cd6bd-112">hello 下列考量適用於：</span><span class="sxs-lookup"><span data-stu-id="cd6bd-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="cd6bd-113">Media Services 使用 hello hello IAssetFile.Name 屬性值，當建置 Url 的 hello 串流處理內容 (例如，http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters。)基於這個理由，不允許 percent-encoding。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="cd6bd-114">hello hello 值**名稱**屬性不能有 hello 下列任何一項[百分比編碼的保留字元](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ！ *' （);: @& = + $，/？ %# []"。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="cd6bd-115">此外，只能有一個 '。 ' hello 檔案名稱副檔名。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="cd6bd-116">hello hello 名稱長度不能超過 260 個字元。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="cd6bd-117">沒有支援 Media Services 中的處理限制 toohello 最大檔案大小。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="cd6bd-118">請參閱[這](media-services-quotas-and-limitations.md)hello 檔案大小限制的詳細主題。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="cd6bd-119">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="cd6bd-120">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="cd6bd-121">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="cd6bd-122">當您建立資產時，您可以指定下列加密選項的 hello。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="cd6bd-123">**None** - 不使用加密。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-123">**None** - No encryption is used.</span></span> <span data-ttu-id="cd6bd-124">這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-124">This is hello default value.</span></span> <span data-ttu-id="cd6bd-125">請注意，使用這個選項時您的內容在傳輸中或在儲存體中不受保護。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="cd6bd-126">如果您計畫使用漸進式下載 toodeliver MP4，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="cd6bd-127">**CommonEncryption** - 如果您上傳的內容已經受到一般加密或 PlayReady DRM (例如，受到 PlayReady DRM 保護的 Smooth Streaming) 的加密保護，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="cd6bd-128">**EnvelopeEncrypted** - 如果您上傳以 AES 加密的 HLS，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="cd6bd-129">請注意，hello 檔案必須具有已編碼，並由 Transform Manager 加密。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="cd6bd-130">**StorageEncrypted** -加密您清除的內容，在本機使用 AES 256 位元加密，並將其上傳 tooAzure 儲存體的方式予以儲存加密在靜止。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="cd6bd-131">使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="cd6bd-132">儲存體加密的 hello 主要使用案例是當您想的 toosecure 強式加密您高品質的輸入的媒體檔案放在磁碟。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="cd6bd-133">媒體服務可為您的資產提供磁碟上的儲存體加密，而不是在線上加密，例如數位版權管理員 (DRM)。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="cd6bd-134">如果您的資產是儲存體加密，必須設定資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="cd6bd-135">如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-dotnet-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="cd6bd-136">如果您指定與加密資產 toobe **CommonEncrypted**選項，或**EnvelopeEncypted**選項，您將需要 tooassociate 與資產**ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="cd6bd-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="cd6bd-137">如需詳細資訊，請參閱[如何 toocreate ContentKey](media-services-dotnet-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="cd6bd-138">如果您指定與加密資產 toobe **StorageEncrypted**選項，hello Media Services SDK for.NET 會建立**StorateEncrypted** **ContentKey**的程式資產。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="cd6bd-139">本主題說明如何 toouse 媒體服務.NET SDK，以及 Media Services.NET SDK 延伸模組 tooupload 檔案到 Media Services 資產。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="cd6bd-140">使用媒體服務 .NET SDK 上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="cd6bd-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="cd6bd-141">下列的 hello 範例程式碼會使用.NET SDK tooupload 單一檔案。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="cd6bd-142">hello AccessPolicy 與 Locator 建立和終結 hello 上載函式。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="cd6bd-143">使用媒體服務 .NET SDK 上傳多個檔案</span><span class="sxs-lookup"><span data-stu-id="cd6bd-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="cd6bd-144">hello 下列程式碼會示範如何 toocreate 資產及上傳多個檔案。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="cd6bd-145">hello 程式碼沒有 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="cd6bd-145">hello code does hello following:</span></span>

* <span data-ttu-id="cd6bd-146">建立空白資產使用 hello 上一個步驟中所定義的 hello CreateEmptyAsset 方法。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="cd6bd-147">建立**AccessPolicy**定義 hello 權限和存取 toohello 資產的持續時間的執行個體。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="cd6bd-148">建立**定位器**提供存取 toohello 資產的執行個體。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="cd6bd-149">建立 **BlobTransferClient** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="cd6bd-150">此類型代表的 hello Azure blob 操作的用戶端。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="cd6bd-151">在此範例中，我們會使用 hello 用戶端 toomonitor hello 上傳進度。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="cd6bd-152">列舉透過 hello 指定目錄中的檔案，並建立**AssetFile**每個檔案的執行個體。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="cd6bd-153">上傳到 Media Services 使用 hello hello 檔案**UploadAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="cd6bd-154">使用 hello UploadAsync 方法 tooensure hello 呼叫並未封鎖，以平行方式上傳 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="cd6bd-155">當上傳大型資產數目，請考慮 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="cd6bd-156">為每個執行緒建立新的 **CloudMediaContext** 物件。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="cd6bd-157">hello **CloudMediaContext**類別不是安全執行緒。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="cd6bd-158">增加 NumberOfConcurrentTransfers hello 的 2 tooa 5 像是較高值的預設值。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="cd6bd-159">設定此屬性會影響所有 **CloudMediaContext**執行個體。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="cd6bd-160">ParallelTransferThreadCount 保持 hello 預設值 10。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="cd6bd-161"><a id="ingest_in_bulk"></a>使用媒體服務 .NET SDK 大量擷取資產</span><span class="sxs-lookup"><span data-stu-id="cd6bd-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="cd6bd-162">上傳大型資產檔案可能會在建立資產期間造成瓶頸。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="cd6bd-163">擷取資產的大量或 「 大量擷取 」，牽涉到分離資產建立與 hello 上傳程序。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="cd6bd-164">toouse 大量擷取方法，建立資訊清單 (IngestManifest)，描述 hello 資產及其相關聯的檔案。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="cd6bd-165">然後使用您選擇 tooupload hello 相關聯的檔案 toohello 資訊清單的 blob 容器的 hello 上傳方法。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="cd6bd-166">Microsoft Azure Media Services 監看 hello 與 hello 資訊清單相關聯的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="cd6bd-167">一旦檔案已上傳的 toohello blob 容器，Microsoft Azure Media Services 完成 hello 資產建立根據 hello hello 資訊清單 (IngestManifestAsset) 中的 hello 資產的組態。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="cd6bd-168">toocreate 新 IngestManifest 呼叫 hello hello CloudMediaContext Ingestmanifest 集合所公開的 hello 建立方法。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="cd6bd-169">這個方法會建立新的 IngestManifest 與 hello 您所提供的資訊清單名稱。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="cd6bd-170">建立要與 hello 大量 IngestManifest 相關聯的 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="cd6bd-171">設定所需的 hello hello 大量擷取資產加密選項。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="cd6bd-172">IngestManifestAsset 會建立資產與大量 IngestManifest 的關聯，以進行大量內嵌。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="cd6bd-173">它也將會建立構成每個資產的 Assetfile hello 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="cd6bd-174">toocreate IngestManifestAsset，hello 伺服器內容上使用 hello Create 方法。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="cd6bd-175">hello 下列範例示範將先前建立 toohello 大量 hello 兩個資產產生關聯的加入兩個新 Ingestmanifestasset 內嵌資訊清單。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="cd6bd-176">每個 IngestManifestAsset 也會關聯在大量內嵌期間針對每個資產所上傳的一組檔案。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="cd6bd-177">您可以使用任何適當的高速用戶端的應用程式能夠將上傳 hello 資產檔案 toohello blob 儲存體容器 hello 所提供的 URI **IIngestManifest.BlobStorageUriForUpload** hello IngestManifest 的屬性。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="cd6bd-178">一個著名的高速上傳服務是 [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="cd6bd-179">您也可以撰寫程式碼 tooupload hello 資產檔案中 hello 下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

<span data-ttu-id="cd6bd-180">hello hello 範例使用本主題中的 hello 資產檔案上傳的程式碼所示 hello 下列程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="cd6bd-181">您可以判斷 hello hello 與相關聯的所有資產的大量擷取進度**IngestManifest**藉由輪詢 hello 統計資料屬性的 hello **IngestManifest**。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="cd6bd-182">在訂單 tooupdate 進度資訊，您必須使用新**CloudMediaContext**每次輪詢 hello 統計資料屬性。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="cd6bd-183">hello 下列範例示範如何輪詢 IngestManifest 的其**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="cd6bd-184">使用 .NET SDK 延伸模組上傳檔案</span><span class="sxs-lookup"><span data-stu-id="cd6bd-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="cd6bd-185">下列的 hello 範例示範如何 tooupload 的單一檔案使用.NET SDK 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="cd6bd-186">在此情況下 hello **CreateFromFile**方法會使用，但也會提供 hello 非同步版本 (**CreateFromFileAsync**)。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="cd6bd-187">hello **CreateFromFile**方法可讓您指定 hello 檔案名稱、 加密 選項，以及的回呼順序 tooreport hello 中上傳 hello 檔案的進度。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

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

<span data-ttu-id="cd6bd-188">hello 下列範例會呼叫 UploadFile 函式並指定儲存體加密為 hello 資產建立選項。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="cd6bd-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cd6bd-189">Next steps</span></span>

<span data-ttu-id="cd6bd-190">您現在可以將上傳的資產編碼。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="cd6bd-191">如需詳細資訊，請參閱 [為資產編碼](media-services-portal-encode.md)。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="cd6bd-192">您也可以使用 Azure 函式 tootrigger 抵達 hello 設定容器中的檔案為基礎的編碼工作。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="cd6bd-193">如需詳細資訊，請參閱[此範例](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="cd6bd-194">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="cd6bd-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cd6bd-195">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="cd6bd-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="cd6bd-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cd6bd-196">Next step</span></span>
<span data-ttu-id="cd6bd-197">既然您已上傳資產 tooMedia 服務移 toohello[如何 tooGet 媒體處理器][ How tooGet a Media Processor]主題。</span><span class="sxs-lookup"><span data-stu-id="cd6bd-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

