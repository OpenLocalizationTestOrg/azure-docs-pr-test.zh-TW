---
title: "使用 .NET 將檔案上傳至媒體服務帳戶 | Microsoft Docs"
description: "了解如何建立並上傳資產，以將媒體內容移至媒體服務中。"
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
ms.openlocfilehash: ec8c1da633374ba684f6a0a895c542ee76ef73b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="09d63-103">使用 .NET 將檔案上傳至媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="09d63-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09d63-104">.NET</span><span class="sxs-lookup"><span data-stu-id="09d63-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="09d63-105">REST</span><span class="sxs-lookup"><span data-stu-id="09d63-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="09d63-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="09d63-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="09d63-107">在媒體服務中，您可以將數位檔案上傳 (或內嵌) 到資產。</span><span class="sxs-lookup"><span data-stu-id="09d63-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="09d63-108">**資產**實體可以包含視訊、音訊、影像、縮圖集合、文字播放軌及隱藏式輔助字幕檔案 (以及這些檔案的相關中繼資料)。上傳檔案之後，您的內容會安全地儲存在雲端，以進一步進行處理和串流處理。</span><span class="sxs-lookup"><span data-stu-id="09d63-108">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="09d63-109">資產中的檔案稱為 **資產檔案**。</span><span class="sxs-lookup"><span data-stu-id="09d63-109">The files in the asset are called **Asset Files**.</span></span> <span data-ttu-id="09d63-110">**AssetFile** 執行個體和實際媒體檔是兩個不同的物件。</span><span class="sxs-lookup"><span data-stu-id="09d63-110">The **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="09d63-111">AssetFile 執行個體包含媒體檔案的相關中繼資料，而媒體檔案包含實際的媒體內容。</span><span class="sxs-lookup"><span data-stu-id="09d63-111">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="09d63-112">您必須考量下列事項：</span><span class="sxs-lookup"><span data-stu-id="09d63-112">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="09d63-113">建置串流內容的 URL (例如，http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters) 時，媒體服務會使用 IAssetFile.Name 屬性的值。基於這個理由，不允許 percent-encoding。</span><span class="sxs-lookup"><span data-stu-id="09d63-113">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="09d63-114">**Name** 屬性的值不能有下列任何[百分比編碼保留字元](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters)：!*'();:@&=+$,/?%#[]"。</span><span class="sxs-lookup"><span data-stu-id="09d63-114">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="09d63-115">而且，副檔名只能有一個 '.'。</span><span class="sxs-lookup"><span data-stu-id="09d63-115">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="09d63-116">名稱長度不應超過 260 個字元。</span><span class="sxs-lookup"><span data-stu-id="09d63-116">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="09d63-117">對於在媒體服務處理檔案，支援的檔案大小有上限。</span><span class="sxs-lookup"><span data-stu-id="09d63-117">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="09d63-118">請參閱[此](media-services-quotas-and-limitations.md)主題，以取得有關檔案大小限制的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="09d63-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> * <span data-ttu-id="09d63-119">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="09d63-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="09d63-120">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="09d63-120">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="09d63-121">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="09d63-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="09d63-122">建立資產時，您可以指定下列加密選項。</span><span class="sxs-lookup"><span data-stu-id="09d63-122">When you create assets, you can specify the following encryption options.</span></span> 

* <span data-ttu-id="09d63-123">**None** - 不使用加密。</span><span class="sxs-lookup"><span data-stu-id="09d63-123">**None** - No encryption is used.</span></span> <span data-ttu-id="09d63-124">這是預設值。</span><span class="sxs-lookup"><span data-stu-id="09d63-124">This is the default value.</span></span> <span data-ttu-id="09d63-125">請注意，使用這個選項時您的內容在傳輸中或在儲存體中不受保護。</span><span class="sxs-lookup"><span data-stu-id="09d63-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="09d63-126">如果您計劃使用漸進式下載傳遞 MP4，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="09d63-126">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="09d63-127">**CommonEncryption** - 如果您上傳的內容已經受到一般加密或 PlayReady DRM (例如，受到 PlayReady DRM 保護的 Smooth Streaming) 的加密保護，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="09d63-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="09d63-128">**EnvelopeEncrypted** - 如果您上傳以 AES 加密的 HLS，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="09d63-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="09d63-129">請注意，檔案必須已由 Transform Manager 編碼和加密。</span><span class="sxs-lookup"><span data-stu-id="09d63-129">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="09d63-130">**StorageEncrypted** - 使用 AES-256 位元加密對您的內容進行本機加密，接著上傳到已靜止加密儲存的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="09d63-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="09d63-131">以儲存體加密保護的資產會自動解除加密並在編碼前放置在加密的檔案系統中，並且會在上傳為新輸出資產之前選擇性地重新編碼。</span><span class="sxs-lookup"><span data-stu-id="09d63-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="09d63-132">儲存體加密的主要使用案例是讓您可以使用強式加密來保護磁碟中靜止的高品質輸入媒體檔。</span><span class="sxs-lookup"><span data-stu-id="09d63-132">The primary use case for Storage Encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="09d63-133">媒體服務可為您的資產提供磁碟上的儲存體加密，而不是在線上加密，例如數位版權管理員 (DRM)。</span><span class="sxs-lookup"><span data-stu-id="09d63-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="09d63-134">如果您的資產是儲存體加密，必須設定資產傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="09d63-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="09d63-135">如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-dotnet-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="09d63-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="09d63-136">如果您指定使用 **CommonEncrypted** 選項或 **EnvelopeEncypted** 選項加密資產，則需要建立資產與 **ContentKey** 的關聯。</span><span class="sxs-lookup"><span data-stu-id="09d63-136">If you specify for your asset to be encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need to associate your asset with a **ContentKey**.</span></span> <span data-ttu-id="09d63-137">如需詳細資訊，請參閱 [如何建立 ContentKey](media-services-dotnet-create-contentkey.md)。</span><span class="sxs-lookup"><span data-stu-id="09d63-137">For more information, see [How to create a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="09d63-138">如果您指定使用 **StorageEncrypted** 選項來加密資產，則 Media Services SDK for .NET 會建立資產的 **StorateEncrypted** 和 **ContentKey**。</span><span class="sxs-lookup"><span data-stu-id="09d63-138">If you specify for your asset to be encrypted with a **StorageEncrypted** option, the Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="09d63-139">本主題顯示如何使用 Media Services .NET SDK 以及 Media Services .NET SDK 延伸模組，以將檔案上傳到媒體服務資產。</span><span class="sxs-lookup"><span data-stu-id="09d63-139">This topic shows how to use Media Services .NET SDK as well as Media Services .NET SDK extensions to upload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="09d63-140">使用媒體服務 .NET SDK 上傳單一檔案</span><span class="sxs-lookup"><span data-stu-id="09d63-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="09d63-141">以下範例程式碼會使用 .NET SDK 來上傳一個檔案。</span><span class="sxs-lookup"><span data-stu-id="09d63-141">The sample code below uses .NET SDK to upload a single file.</span></span> <span data-ttu-id="09d63-142">AccessPolicy 與定位器會由所上傳的函式建立並終結。</span><span class="sxs-lookup"><span data-stu-id="09d63-142">The AccessPolicy and Locator are created and destroyed by the Upload function.</span></span> 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="09d63-143">使用媒體服務 .NET SDK 上傳多個檔案</span><span class="sxs-lookup"><span data-stu-id="09d63-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="09d63-144">下列程式碼將說明如何建立資產並上傳多個檔案。</span><span class="sxs-lookup"><span data-stu-id="09d63-144">The following code shows how to create an asset and upload multiple files.</span></span>

<span data-ttu-id="09d63-145">此程式碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="09d63-145">The code does the following:</span></span>

* <span data-ttu-id="09d63-146">使用上一個步驟中所定義的 CreateEmptyAsset 方法，來建立空白資產。</span><span class="sxs-lookup"><span data-stu-id="09d63-146">Creates an empty asset using the CreateEmptyAsset method defined in the previous step.</span></span>
* <span data-ttu-id="09d63-147">建立 **AccessPolicy** 執行個體，以定義存取資產所需的權限和規定期間。</span><span class="sxs-lookup"><span data-stu-id="09d63-147">Creates an **AccessPolicy** instance that defines the permissions and duration of access to the asset.</span></span>
* <span data-ttu-id="09d63-148">建立可用來存取資產的 **Locator** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="09d63-148">Creates a **Locator** instance that provides access to the asset.</span></span>
* <span data-ttu-id="09d63-149">建立 **BlobTransferClient** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="09d63-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="09d63-150">此類型代表在 Azure Blob 上作業的用戶端。</span><span class="sxs-lookup"><span data-stu-id="09d63-150">This type represents a client that operates on the Azure blobs.</span></span> <span data-ttu-id="09d63-151">在此範例中，我們會使用用戶端來監視上傳進度。</span><span class="sxs-lookup"><span data-stu-id="09d63-151">In this example we use the client to monitor the upload progress.</span></span> 
* <span data-ttu-id="09d63-152">逐一列舉所指定目錄中的檔案，並建立每個檔案的 **AssetFile** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="09d63-152">Enumerates through files in the specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="09d63-153">使用 **UploadAsync** 方法，將檔案上傳到媒體服務。</span><span class="sxs-lookup"><span data-stu-id="09d63-153">Uploads the files into Media Services using the **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="09d63-154">使用 UploadAsync 方法確保未封鎖呼叫，並且平行上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="09d63-154">Use the UploadAsync method to ensure that the calls are not blocking and the files are uploaded in parallel.</span></span>
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

                // It is recommended to validate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading the files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as the upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="09d63-155">上傳大量資產時，請考慮下列項目。</span><span class="sxs-lookup"><span data-stu-id="09d63-155">When uploading a large number of assets, consider the following.</span></span>

* <span data-ttu-id="09d63-156">為每個執行緒建立新的 **CloudMediaContext** 物件。</span><span class="sxs-lookup"><span data-stu-id="09d63-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="09d63-157">**CloudMediaContext** 類別不具備執行緒安全。</span><span class="sxs-lookup"><span data-stu-id="09d63-157">The **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="09d63-158">將 NumberOfConcurrentTransfers 從預設值 2 增加為較高的值 (例如 5)。</span><span class="sxs-lookup"><span data-stu-id="09d63-158">Increase NumberOfConcurrentTransfers from the default value of 2 to a higher value like 5.</span></span> <span data-ttu-id="09d63-159">設定此屬性會影響所有 **CloudMediaContext**執行個體。</span><span class="sxs-lookup"><span data-stu-id="09d63-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="09d63-160">將 ParallelTransferThreadCount 保持為預設值 10。</span><span class="sxs-lookup"><span data-stu-id="09d63-160">Keep ParallelTransferThreadCount at the default value of 10.</span></span>

## <span data-ttu-id="09d63-161"><a id="ingest_in_bulk"></a>使用媒體服務 .NET SDK 大量擷取資產</span><span class="sxs-lookup"><span data-stu-id="09d63-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="09d63-162">上傳大型資產檔案可能會在建立資產期間造成瓶頸。</span><span class="sxs-lookup"><span data-stu-id="09d63-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="09d63-163">大量內嵌資產或「大量內嵌」包含透過上傳程序來解除結合資產建立。</span><span class="sxs-lookup"><span data-stu-id="09d63-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from the upload process.</span></span> <span data-ttu-id="09d63-164">若要使用大量內嵌方式，請建立可描述資產及其相關檔案的資訊清單 (IngestManifest)。</span><span class="sxs-lookup"><span data-stu-id="09d63-164">To use a bulk ingesting approach, create a manifest (IngestManifest) that describes the asset and its associated files.</span></span> <span data-ttu-id="09d63-165">然後使用您選擇的上傳方法，將相關的檔案上傳至資訊清單的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="09d63-165">Then use the upload method of your choice to upload the associated files to the manifest’s blob container.</span></span> <span data-ttu-id="09d63-166">Microsoft Azure 媒體服務會監看與資訊清單相關聯的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="09d63-166">Microsoft Azure Media Services watches the blob container associated with the manifest.</span></span> <span data-ttu-id="09d63-167">將檔案上傳至 Blob 容器之後，Microsoft Azure 媒體服務會根據資訊清單 (IngestManifestAsset) 中的資產組態來完成資產建立。</span><span class="sxs-lookup"><span data-stu-id="09d63-167">Once a file is uploaded to the blob container, Microsoft Azure Media Services completes the asset creation based on the configuration of the asset in the manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="09d63-168">若要建立新的 IngestManifest，請呼叫 CloudMediaContext 上 IngestManifests 集合所公開的 Create 方法。</span><span class="sxs-lookup"><span data-stu-id="09d63-168">To create a new IngestManifest call the Create method exposed by the IngestManifests collection on the CloudMediaContext.</span></span> <span data-ttu-id="09d63-169">此方法會使用您提供的資訊清單名稱來建立新的 IngestManifest。</span><span class="sxs-lookup"><span data-stu-id="09d63-169">This method will create a new IngestManifest with the manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="09d63-170">建立將與大量 IngestManifest 相關聯的資產。</span><span class="sxs-lookup"><span data-stu-id="09d63-170">Create the assets that will be associated with the bulk IngestManifest.</span></span> <span data-ttu-id="09d63-171">對資產設定想要的加密選項，以進行大量內嵌。</span><span class="sxs-lookup"><span data-stu-id="09d63-171">Configure the desired encryption options on the asset for bulk ingesting.</span></span>

    // Create the assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="09d63-172">IngestManifestAsset 會建立資產與大量 IngestManifest 的關聯，以進行大量內嵌。</span><span class="sxs-lookup"><span data-stu-id="09d63-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="09d63-173">它也會建立構成每個資產之 AssetFile 的關聯。</span><span class="sxs-lookup"><span data-stu-id="09d63-173">It also associates the AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="09d63-174">若要建立 IngestManifestAsset，請在伺服器內容上使用 Create 方法。</span><span class="sxs-lookup"><span data-stu-id="09d63-174">To create an IngestManifestAsset, use the Create method on the server context.</span></span>

<span data-ttu-id="09d63-175">下列範例示範如何新增兩個新的 IngestManifestAsset，以建立先前建立之兩個資產與大量內嵌資訊清單的關聯。</span><span class="sxs-lookup"><span data-stu-id="09d63-175">The following example demonstrates adding two new IngestManifestAssets that associate the two assets previously created to the bulk ingest manifest.</span></span> <span data-ttu-id="09d63-176">每個 IngestManifestAsset 也會關聯在大量內嵌期間針對每個資產所上傳的一組檔案。</span><span class="sxs-lookup"><span data-stu-id="09d63-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="09d63-177">您可以使用任何高速用戶端應用程式，而高速用戶端應用程式可以將資產檔案上傳至 IngestManifest 之 **IIngestManifest.BlobStorageUriForUpload** 屬性所提供的 Blob 儲存體容器 URI。</span><span class="sxs-lookup"><span data-stu-id="09d63-177">You can use any high speed client application capable of uploading the asset files to the blob storage container URI provided by the **IIngestManifest.BlobStorageUriForUpload** property of the IngestManifest.</span></span> <span data-ttu-id="09d63-178">一個著名的高速上傳服務是 [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)。</span><span class="sxs-lookup"><span data-stu-id="09d63-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="09d63-179">您也可以撰寫程式碼來上傳資產檔案 (如下列程式碼範例所示)。</span><span class="sxs-lookup"><span data-stu-id="09d63-179">You can also write code to upload the assets files as shown in the following code example.</span></span>

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

<span data-ttu-id="09d63-180">下列程式碼範例顯示上傳本主題中所用範例之資產檔案的程式碼。</span><span class="sxs-lookup"><span data-stu-id="09d63-180">The code for uploading the asset files for the sample used in this topic is shown in the following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="09d63-181">輪詢 **IngestManifest** 的 Statistics 屬性，即可判斷與 **IngestManifest** 相關聯之所有資產的大量內嵌進度。</span><span class="sxs-lookup"><span data-stu-id="09d63-181">You can determine the progress of the bulk ingesting for all assets associated with an **IngestManifest** by polling the Statistics property of the **IngestManifest**.</span></span> <span data-ttu-id="09d63-182">若要更新進度資訊，每次輪詢 Statistics 屬性時，都必須使用新的 **CloudMediaContext** 。</span><span class="sxs-lookup"><span data-stu-id="09d63-182">In order to update progress information, you must use a new **CloudMediaContext** each time you poll the Statistics property.</span></span>

<span data-ttu-id="09d63-183">下列範例示範如何依 **Id**輪詢 IngestManifest。</span><span class="sxs-lookup"><span data-stu-id="09d63-183">The following example demonstrates polling an IngestManifest by its **Id**.</span></span>

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



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="09d63-184">使用 .NET SDK 延伸模組上傳檔案</span><span class="sxs-lookup"><span data-stu-id="09d63-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="09d63-185">下列範例顯示如何使用 .NET SDK 延伸模組上傳單一檔案。</span><span class="sxs-lookup"><span data-stu-id="09d63-185">The example below shows how to upload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="09d63-186">在此情況下，會使用 **CreateFromFile** 方法，但也會提供非同步版本 (**CreateFromFileAsync**)。</span><span class="sxs-lookup"><span data-stu-id="09d63-186">In this case the **CreateFromFile** method is used, but the asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="09d63-187">**CreateFromFile** 方法可讓您指定檔案名稱、加密選項和回呼，以報告檔案的上傳進度。</span><span class="sxs-lookup"><span data-stu-id="09d63-187">The **CreateFromFile** method lets you specify the file name, encryption option, and a callback in order to report the upload progress of the file.</span></span>

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

<span data-ttu-id="09d63-188">下列範例會呼叫 UploadFile 函數，並指定儲存體加密做為資產建立選項。</span><span class="sxs-lookup"><span data-stu-id="09d63-188">The following example calls UploadFile function and specifies storage encryption as the asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="09d63-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09d63-189">Next steps</span></span>

<span data-ttu-id="09d63-190">您現在可以將上傳的資產編碼。</span><span class="sxs-lookup"><span data-stu-id="09d63-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="09d63-191">如需詳細資訊，請參閱 [為資產編碼](media-services-portal-encode.md)。</span><span class="sxs-lookup"><span data-stu-id="09d63-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="09d63-192">您也可以使用 Azure Functions，以根據在所設定容器到達的檔案來觸發編碼作業。</span><span class="sxs-lookup"><span data-stu-id="09d63-192">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="09d63-193">如需詳細資訊，請參閱[此範例](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )。</span><span class="sxs-lookup"><span data-stu-id="09d63-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="09d63-194">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="09d63-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="09d63-195">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="09d63-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="09d63-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09d63-196">Next step</span></span>
<span data-ttu-id="09d63-197">您已將資產上傳至媒體服務，現在請移至 [如何取得媒體處理器][How to Get a Media Processor]主題。</span><span class="sxs-lookup"><span data-stu-id="09d63-197">Now that you have uploaded an asset to Media Services, go to the [How to Get a Media Processor][How to Get a Media Processor] topic.</span></span>

[How to Get a Media Processor]: media-services-get-media-processor.md

