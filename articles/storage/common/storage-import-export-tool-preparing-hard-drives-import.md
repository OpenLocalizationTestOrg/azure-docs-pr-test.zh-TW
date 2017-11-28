---
title: "準備 Azure 匯入/匯出匯入工作的硬碟 |Microsoft Docs"
description: "了解如何使用 WAImportExport 工具準備硬碟，以建立 Azure 匯入/匯出服務的匯入工作。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: 23f2640bc71bc4eba0f3fc76014cce4a298bfcfa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a><span data-ttu-id="ee53d-103">準備匯入工作的硬碟</span><span class="sxs-lookup"><span data-stu-id="ee53d-103">Preparing hard drives for an Import Job</span></span>

<span data-ttu-id="ee53d-104">WAImportExport 工具是磁碟機準備及修復工具，可搭配 [Microsoft Azure 匯入/匯出服務](../storage-import-export-service.md)使用。</span><span class="sxs-lookup"><span data-stu-id="ee53d-104">The WAImportExport tool is the drive preparation and repair tool that you can use with the [Microsoft Azure Import/Export service](../storage-import-export-service.md).</span></span> <span data-ttu-id="ee53d-105">您可以使用此工具，將資料複製到要寄送至 Azure 資料中心的硬碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-105">You can use this tool to copy data to the hard drives you are going to ship to an Azure datacenter.</span></span> <span data-ttu-id="ee53d-106">匯入工作完成後，您可以使用此工具來修復損毀、遺漏或與其他 Blob 衝突的任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="ee53d-106">After an import job has completed, you can use this tool to repair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span> <span data-ttu-id="ee53d-107">當您收到已完成的匯出工作中的磁碟機後，您可以使用此工具來修復磁碟機上損毀或遺漏的任何檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-107">After you receive the drives from a completed export job, you can use this tool to repair any files that were corrupted or missing on the drives.</span></span> <span data-ttu-id="ee53d-108">我們會在本文中介紹此工具的使用方式。</span><span class="sxs-lookup"><span data-stu-id="ee53d-108">In this article, we go over the use of this tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee53d-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="ee53d-109">Prerequisites</span></span>

### <a name="requirements-for-waimportexportexe"></a><span data-ttu-id="ee53d-110">WAImportExport.exe 的需求</span><span class="sxs-lookup"><span data-stu-id="ee53d-110">Requirements for WAImportExport.exe</span></span>

- <span data-ttu-id="ee53d-111">**電腦組態**</span><span class="sxs-lookup"><span data-stu-id="ee53d-111">**Machine configuration**</span></span>
  - <span data-ttu-id="ee53d-112">Windows 7、Windows Server 2008 R2 或更新版本的 Windows 作業系統</span><span class="sxs-lookup"><span data-stu-id="ee53d-112">Windows 7, Windows Server 2008 R2, or a newer Windows operating system</span></span>
  - <span data-ttu-id="ee53d-113">必須安裝 .NET framework 4。</span><span class="sxs-lookup"><span data-stu-id="ee53d-113">.NET Framework 4 must be installed.</span></span> <span data-ttu-id="ee53d-114">請參閱[常見問題集](#faq)，了解如何檢查電腦上是否已安裝 .Net Framework。</span><span class="sxs-lookup"><span data-stu-id="ee53d-114">See [FAQ](#faq) on how to check if .Net Framework is installed on the machine.</span></span>
- <span data-ttu-id="ee53d-115">**儲存體帳戶金鑰** - 您需要至少一個儲存體帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="ee53d-115">**Storage account key** - You need at least one of the account keys for the storage account.</span></span>

### <a name="preparing-disk-for-import-job"></a><span data-ttu-id="ee53d-116">準備匯入工作的磁碟</span><span class="sxs-lookup"><span data-stu-id="ee53d-116">Preparing disk for import job</span></span>

- <span data-ttu-id="ee53d-117">**BitLocker -** 執行 WAImportExport 工具的電腦上必須啟用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="ee53d-117">**BitLocker -** BitLocker must be enabled on the machine running the WAImportExport tool.</span></span> <span data-ttu-id="ee53d-118">如需如何啟用 BitLocker 的詳細資訊，請參閱[常見問題集](#faq)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-118">See the [FAQ](#faq) for how to enable BitLocker.</span></span>
- <span data-ttu-id="ee53d-119">**磁碟**必須可從執行 WAImportExport 工具的電腦上存取。</span><span class="sxs-lookup"><span data-stu-id="ee53d-119">**Disks** accessible from machine on which WAImportExport Tool is run.</span></span> <span data-ttu-id="ee53d-120">如需磁碟規格的詳細資訊，請參閱[常見問題集](#faq)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-120">See [FAQ](#faq) for disk specification.</span></span>
- <span data-ttu-id="ee53d-121">**來源檔案** - 您想匯入的檔案必須可從複製電腦上存取，無論它們是在網路共用或本機硬碟上。</span><span class="sxs-lookup"><span data-stu-id="ee53d-121">**Source files** - The files you plan to import must be accessible from the copy machine, whether they are on a network share or a local hard drive.</span></span>

### <a name="repairing-a-partially-failed-import-job"></a><span data-ttu-id="ee53d-122">修復部分失敗的匯入工作</span><span class="sxs-lookup"><span data-stu-id="ee53d-122">Repairing a partially failed import job</span></span>

- <span data-ttu-id="ee53d-123">**複製記錄檔**，是 Azure 匯入/匯出服務在儲存體帳戶和磁碟之間複製資料時產生的。</span><span class="sxs-lookup"><span data-stu-id="ee53d-123">**Copy log file** that is generated when Azure Import/Export service copies data between Storage Account and Disk.</span></span> <span data-ttu-id="ee53d-124">此檔案位於您的目標儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee53d-124">It is located in your target storage account.</span></span>

### <a name="repairing-a-partially-failed-export-job"></a><span data-ttu-id="ee53d-125">修復部分失敗的匯出工作</span><span class="sxs-lookup"><span data-stu-id="ee53d-125">Repairing a partially failed export job</span></span>

- <span data-ttu-id="ee53d-126">**複製記錄檔**，是 Azure 匯入/匯出服務在儲存體帳戶和磁碟之間複製資料時產生的。</span><span class="sxs-lookup"><span data-stu-id="ee53d-126">**Copy log file** that is generated when Azure Import/Export service copies data between Storage Account and Disk.</span></span> <span data-ttu-id="ee53d-127">此檔案位於您的來源儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee53d-127">It is located in your source storage account.</span></span>
- <span data-ttu-id="ee53d-128">**資訊清單檔案** - [選擇性] 位於 Microsoft 寄回的匯出磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="ee53d-128">**Manifest file** - [Optional] Located on exported drive that was returned by Microsoft.</span></span>

## <a name="download-and-install-waimportexport"></a><span data-ttu-id="ee53d-129">下載和安裝 WAImportExport</span><span class="sxs-lookup"><span data-stu-id="ee53d-129">Download and install WAImportExport</span></span>

<span data-ttu-id="ee53d-130">下載[最新版的 WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-130">Download the [latest version of WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280).</span></span> <span data-ttu-id="ee53d-131">將壓縮的內容解壓縮至您電腦上的目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-131">Extract the zipped content to a directory on your computer.</span></span>

<span data-ttu-id="ee53d-132">您的下一個工作是建立 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-132">Your next task is to create CSV files.</span></span>

## <a name="prepare-the-dataset-csv-file"></a><span data-ttu-id="ee53d-133">準備資料集 CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="ee53d-133">Prepare the dataset CSV file</span></span>

### <a name="what-is-dataset-csv"></a><span data-ttu-id="ee53d-134">什麼是資料集 CSV</span><span class="sxs-lookup"><span data-stu-id="ee53d-134">What is dataset CSV</span></span>

<span data-ttu-id="ee53d-135">資料集 CSV 檔案是 /dataset 旗標的值，此 CSV 檔案包含要複製到目標磁碟機的目錄清單和/或檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ee53d-135">Dataset CSV file is the value of /dataset flag is a CSV file that contains a list of directories and/or a list of files to be copied to target drives.</span></span> <span data-ttu-id="ee53d-136">建立匯入工作的第一步是判斷您要匯入哪些目錄和檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-136">The first step to creating an import job is to determine which directories and files you are going to import.</span></span> <span data-ttu-id="ee53d-137">可以是目錄清單、唯一檔案的清單或兩者的組合。</span><span class="sxs-lookup"><span data-stu-id="ee53d-137">This can be a list of directories, a list of unique files, or a combination of those two.</span></span> <span data-ttu-id="ee53d-138">包含目錄時，目錄及其子目錄中的所有檔案都是匯入工作的一部分。</span><span class="sxs-lookup"><span data-stu-id="ee53d-138">When a directory is included, all files in the directory and its subdirectories will be part of the import job.</span></span>

<span data-ttu-id="ee53d-139">針對要匯入的每個目錄或檔案，您必須指定目的地虛擬目錄或 Azure Blob 服務中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="ee53d-139">For each directory or file to be imported, you must identify a destination virtual directory or blob in the Azure Blob service.</span></span> <span data-ttu-id="ee53d-140">您將使用這些目標做為 WAImportExport 工具的輸入。</span><span class="sxs-lookup"><span data-stu-id="ee53d-140">You will use these targets as inputs to the WAImportExport tool.</span></span> <span data-ttu-id="ee53d-141">目錄應使用斜線字元 "/" 分隔。</span><span class="sxs-lookup"><span data-stu-id="ee53d-141">Directories should be delimited with the forward slash character "/".</span></span>

<span data-ttu-id="ee53d-142">下表顯示一些 Blob 目標範例：</span><span class="sxs-lookup"><span data-stu-id="ee53d-142">The following table shows some examples of blob targets:</span></span>

| <span data-ttu-id="ee53d-143">來源檔案或目錄</span><span class="sxs-lookup"><span data-stu-id="ee53d-143">Source file or directory</span></span> | <span data-ttu-id="ee53d-144">目的地 Blob 或虛擬目錄</span><span class="sxs-lookup"><span data-stu-id="ee53d-144">Destination blob or virtual directory</span></span> |
| --- | --- |
| <span data-ttu-id="ee53d-145">H:\Video</span><span class="sxs-lookup"><span data-stu-id="ee53d-145">H:\Video</span></span> | <span data-ttu-id="ee53d-146">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="ee53d-146">https://mystorageaccount.blob.core.windows.net/video</span></span> |
| <span data-ttu-id="ee53d-147">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="ee53d-147">H:\Photo</span></span> | <span data-ttu-id="ee53d-148">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="ee53d-148">https://mystorageaccount.blob.core.windows.net/photo</span></span> |
| <span data-ttu-id="ee53d-149">K:\Temp\FavoriteVideo.ISO</span><span class="sxs-lookup"><span data-stu-id="ee53d-149">K:\Temp\FavoriteVideo.ISO</span></span> | <span data-ttu-id="ee53d-150">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO</span><span class="sxs-lookup"><span data-stu-id="ee53d-150">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO</span></span> |
| <span data-ttu-id="ee53d-151">\\myshare\john\music</span><span class="sxs-lookup"><span data-stu-id="ee53d-151">\\myshare\john\music</span></span> | <span data-ttu-id="ee53d-152">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="ee53d-152">https://mystorageaccount.blob.core.windows.net/music</span></span> |

### <a name="sample-datasetcsv"></a><span data-ttu-id="ee53d-153">範例 dataset.csv</span><span class="sxs-lookup"><span data-stu-id="ee53d-153">Sample dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a><span data-ttu-id="ee53d-154">資料集 CSV 檔案欄位</span><span class="sxs-lookup"><span data-stu-id="ee53d-154">Dataset CSV file fields</span></span>

| <span data-ttu-id="ee53d-155">欄位</span><span class="sxs-lookup"><span data-stu-id="ee53d-155">Field</span></span> | <span data-ttu-id="ee53d-156">說明</span><span class="sxs-lookup"><span data-stu-id="ee53d-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ee53d-157">基本路徑</span><span class="sxs-lookup"><span data-stu-id="ee53d-157">BasePath</span></span> | <span data-ttu-id="ee53d-158">**[必要]**</span><span class="sxs-lookup"><span data-stu-id="ee53d-158">**[Required]**</span></span><br/><span data-ttu-id="ee53d-159">此參數的值代表要匯入資料所在的來源。</span><span class="sxs-lookup"><span data-stu-id="ee53d-159">The value of this parameter represents the source where the data to be imported is located.</span></span> <span data-ttu-id="ee53d-160">此工具將以遞迴方式複製位於此路徑下的所有資料。</span><span class="sxs-lookup"><span data-stu-id="ee53d-160">The tool will recursively copy all data located under this path.</span></span><br><br/><span data-ttu-id="ee53d-161">**允許值**︰這必須是本機電腦上的有效路徑或有效的共用路徑，而且應可供使用者存取。</span><span class="sxs-lookup"><span data-stu-id="ee53d-161">**Allowed Values**: This has to be a valid path on local computer or a valid share path and should be accessible by the user.</span></span> <span data-ttu-id="ee53d-162">目錄路徑必須是絕對路徑 (而非相對路徑)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-162">The directory path must be an absolute path (not a relative path).</span></span> <span data-ttu-id="ee53d-163">如果路徑的結尾為 "\\"，即代表目錄，而結尾不是 "\\" 的路徑則代表檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-163">If the path ends with "\\", it represents a directory else a path ending without "\\" represents a file.</span></span><br/><span data-ttu-id="ee53d-164">此欄位中不允許 Regex。</span><span class="sxs-lookup"><span data-stu-id="ee53d-164">No regex is allowed in this field.</span></span> <span data-ttu-id="ee53d-165">如果路徑包含空格，請使用 "" 括住。</span><span class="sxs-lookup"><span data-stu-id="ee53d-165">If the path contains spaces, put it in "".</span></span><br><br/><span data-ttu-id="ee53d-166">**範例**："c:\Directory\c\Directory\File.txt"</span><span class="sxs-lookup"><span data-stu-id="ee53d-166">**Example**: "c:\Directory\c\Directory\File.txt"</span></span><br><span data-ttu-id="ee53d-167">"\\\\FBaseFilesharePath.domain.net\sharename\directory\"</span><span class="sxs-lookup"><span data-stu-id="ee53d-167">"\\\\FBaseFilesharePath.domain.net\sharename\directory\"</span></span>  |
| <span data-ttu-id="ee53d-168">DstBlobPathOrPrefix</span><span class="sxs-lookup"><span data-stu-id="ee53d-168">DstBlobPathOrPrefix</span></span> | <span data-ttu-id="ee53d-169">**[必要]**</span><span class="sxs-lookup"><span data-stu-id="ee53d-169">**[Required]**</span></span><br/> <span data-ttu-id="ee53d-170">Microsoft Azure 儲存體帳戶中的目的地虛擬目錄路徑。</span><span class="sxs-lookup"><span data-stu-id="ee53d-170">The path to the destination virtual directory in your Windows Azure storage account.</span></span> <span data-ttu-id="ee53d-171">虛擬目錄可能已存在或可能不存在。</span><span class="sxs-lookup"><span data-stu-id="ee53d-171">The virtual directory may or may not already exist.</span></span> <span data-ttu-id="ee53d-172">如果不存在，匯入/匯出服務將會建立一個。</span><span class="sxs-lookup"><span data-stu-id="ee53d-172">If it does not exist, Import/Export service will create one.</span></span><br/><br/><span data-ttu-id="ee53d-173">指定目的地虛擬目錄或 blob 時，請確定使用有效的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="ee53d-173">Be sure to use valid container names when specifying destination virtual directories or blobs.</span></span> <span data-ttu-id="ee53d-174">請記住容器名稱必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="ee53d-174">Keep in mind that container names must be lowercase.</span></span> <span data-ttu-id="ee53d-175">關於容器命名規則，請參閱[命名和參考容器、Blob 及中繼資料](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-175">For container naming rules, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).</span></span> <span data-ttu-id="ee53d-176">如果只指定根，即會在目的地 Blob 容器中複寫來源的目錄結構。</span><span class="sxs-lookup"><span data-stu-id="ee53d-176">If only root is specified, the directory structure of the source is replicated in the destination blob container.</span></span> <span data-ttu-id="ee53d-177">如果所需的目錄結構不在來源中，CSV 中的多個對應資料列</span><span class="sxs-lookup"><span data-stu-id="ee53d-177">If a different directory structure is desired than the one in source, multiple rows of mapping in CSV</span></span><br/><br/><span data-ttu-id="ee53d-178">您可以指定容器或 blob 首碼，如 music/70s/。</span><span class="sxs-lookup"><span data-stu-id="ee53d-178">You can specify a container, or a blob prefix like music/70s/.</span></span> <span data-ttu-id="ee53d-179">目的地目錄必須以容器名稱開頭，後面接著正斜線 "/"，並可選擇性地包含結尾是 "/" 的虛擬 Blob 目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-179">The destination directory must begin with the container name, followed by a forward slash "/", and optionally may include a virtual blob directory that ends with "/".</span></span><br/><br/><span data-ttu-id="ee53d-180">目的地容器為根容器時，您必須明確指定根容器 (包括正斜線)，例如 $root /。</span><span class="sxs-lookup"><span data-stu-id="ee53d-180">When the destination container is the root container, you must explicitly specify the root container, including the forward slash, as $root/.</span></span> <span data-ttu-id="ee53d-181">由於根容器下的 Blob 名稱中不能包含 "/"，當目的地目錄是根容器時，將不會複製來源目錄中的任何子目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-181">Since blobs under the root container cannot include "/" in their names, any subdirectories in the source directory will not be copied when the destination directory is the root container.</span></span><br/><br/><span data-ttu-id="ee53d-182">**範例**</span><span class="sxs-lookup"><span data-stu-id="ee53d-182">**Example**</span></span><br/><span data-ttu-id="ee53d-183">如果目的地 Blob 路徑是 https://mystorageaccount.blob.core.windows.net/video，這個欄位的值可以是 video/</span><span class="sxs-lookup"><span data-stu-id="ee53d-183">If the destination blob path is https://mystorageaccount.blob.core.windows.net/video, the value of this field can be video/</span></span>  |
| <span data-ttu-id="ee53d-184">BlobType</span><span class="sxs-lookup"><span data-stu-id="ee53d-184">BlobType</span></span> | <span data-ttu-id="ee53d-185">**[選用]** block &#124; page</span><span class="sxs-lookup"><span data-stu-id="ee53d-185">**[Optional]** block &#124; page</span></span><br/><span data-ttu-id="ee53d-186">目前匯入/匯出服務支援兩種 Blob。</span><span class="sxs-lookup"><span data-stu-id="ee53d-186">Currently Import/Export service supports 2 kinds of Blobs.</span></span> <span data-ttu-id="ee53d-187">分頁 blob 和區塊 Blob，所有檔案預設會匯入為區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="ee53d-187">Page blobs and Block BlobsBy default all files will be imported as Block Blobs.</span></span> <span data-ttu-id="ee53d-188">\*.vhd 和 \*.vhdx 會匯入為分頁 Blob。區塊 Blob 和分頁 Blob 允許的大小有限。</span><span class="sxs-lookup"><span data-stu-id="ee53d-188">And \*.vhd and \*.vhdx will be imported as Page BlobsThere is a limit on the block-blob and page-blob allowed size.</span></span> <span data-ttu-id="ee53d-189">如需詳細資訊，請參閱[儲存體延展性目標](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files) (英文)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-189">See [Storage scalability targets](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files) for more information.</span></span>  |
| <span data-ttu-id="ee53d-190">Disposition</span><span class="sxs-lookup"><span data-stu-id="ee53d-190">Disposition</span></span> | <span data-ttu-id="ee53d-191">**[選用]** rename &#124; no-overwrite &#124; overwrite</span><span class="sxs-lookup"><span data-stu-id="ee53d-191">**[Optional]** rename &#124; no-overwrite &#124; overwrite</span></span> <br/> <span data-ttu-id="ee53d-192">此欄位會指定匯入期間的複製行為，也就是說</span><span class="sxs-lookup"><span data-stu-id="ee53d-192">This field specifies the copy-behavior during import i.e</span></span> <span data-ttu-id="ee53d-193">正在從磁碟將資料上傳至儲存體帳戶時。</span><span class="sxs-lookup"><span data-stu-id="ee53d-193">when data is being uploaded to the storage account from the disk.</span></span> <span data-ttu-id="ee53d-194">可用的選項為：rename&#124;overwite&#124;no-overwrite。若未指定任何項目，預設值為 "rename"。</span><span class="sxs-lookup"><span data-stu-id="ee53d-194">Available options are: rename&#124;overwite&#124;no-overwrite.Defaults to "rename" if nothing specified.</span></span> <br/><br/><span data-ttu-id="ee53d-195">**Rename**︰如果已經有同名的物件，則在目的地建立複本。</span><span class="sxs-lookup"><span data-stu-id="ee53d-195">**Rename**: If an object with same name is present, creates a copy in destination.</span></span><br/><span data-ttu-id="ee53d-196">覆寫︰以較新的檔案覆寫檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-196">Overwrite: overwrites the file with newer file.</span></span> <span data-ttu-id="ee53d-197">上次修改 wins 的檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-197">The file with last-modified wins.</span></span><br/><span data-ttu-id="ee53d-198">**不要覆寫**︰如已存在則略過覆寫檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-198">**No-overwrite**: Skips writing the file if already present.</span></span>|
| <span data-ttu-id="ee53d-199">MetadataFile</span><span class="sxs-lookup"><span data-stu-id="ee53d-199">MetadataFile</span></span> | <span data-ttu-id="ee53d-200">**[選用]**</span><span class="sxs-lookup"><span data-stu-id="ee53d-200">**[Optional]**</span></span> <br/><span data-ttu-id="ee53d-201">此欄位的值為中繼資料檔案，如果需要保留物件的中繼資料或提供自訂中繼資料，則可提供這個欄位的值。</span><span class="sxs-lookup"><span data-stu-id="ee53d-201">The value to this field is the metadata file which can be provided if the one needs to preserve the metadata of the objects or provide custom metadata.</span></span> <span data-ttu-id="ee53d-202">目的地 Blob 的中繼資料檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="ee53d-202">Path to the metadata file for the destination blobs.</span></span> <span data-ttu-id="ee53d-203">如需詳細資訊，請參閱[匯入/匯出服務中繼資料和屬性檔案格式](../storage-import-export-file-format-metadata-and-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-203">See [Import/Export service Metadata and Properties File Format](../storage-import-export-file-format-metadata-and-properties.md) for more information</span></span> |
| <span data-ttu-id="ee53d-204">PropertiesFile</span><span class="sxs-lookup"><span data-stu-id="ee53d-204">PropertiesFile</span></span> | <span data-ttu-id="ee53d-205">**[選用]**</span><span class="sxs-lookup"><span data-stu-id="ee53d-205">**[Optional]**</span></span> <br/><span data-ttu-id="ee53d-206">目的地 Blob 的屬性檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="ee53d-206">Path to the property file for the destination blobs.</span></span> <span data-ttu-id="ee53d-207">如需詳細資訊，請參閱[匯入/匯出服務中繼資料和屬性檔案格式](../storage-import-export-file-format-metadata-and-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-207">See [Import/Export service Metadata and Properties File Format](../storage-import-export-file-format-metadata-and-properties.md) for more information.</span></span> |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a><span data-ttu-id="ee53d-208">準備 InitialDriveSet 或 AdditionalDriveSet CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="ee53d-208">Prepare InitialDriveSet or AdditionalDriveSet CSV file</span></span>

### <a name="what-is-driveset-csv"></a><span data-ttu-id="ee53d-209">什麼是磁碟機集 CSV</span><span class="sxs-lookup"><span data-stu-id="ee53d-209">What is driveset CSV</span></span>

<span data-ttu-id="ee53d-210">/InitialDriveSet 或 /AdditionalDriveSet 旗標的值為 CSV 檔案，其中包含磁碟機代號對應的磁碟清單，使工具可以正確挑選要準備的磁碟清單。</span><span class="sxs-lookup"><span data-stu-id="ee53d-210">The value of the /InitialDriveSet or /AdditionalDriveSet flag is a CSV file that contains the list of disks to which the drive letters are mapped so that the tool can correctly pick the list of disks to be prepared.</span></span> <span data-ttu-id="ee53d-211">如果資料大小超過單一磁碟大小，WAImportExport 工具會將資料以最佳化方式分散在此 CSV 檔案中列示的多個磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-211">If the data size is greater than a single disk size, the WAImportExport tool will distribute the data across multiple disks enlisted in this CSV file in an optimized way.</span></span>

<span data-ttu-id="ee53d-212">單一工作階段中可寫入資料的磁碟數目沒有限制。</span><span class="sxs-lookup"><span data-stu-id="ee53d-212">There is no limit on the number of disks the data can be written to in a single session.</span></span> <span data-ttu-id="ee53d-213">此工具會根據磁碟大小和資料夾大小來分配資料。</span><span class="sxs-lookup"><span data-stu-id="ee53d-213">The tool will distribute data based on disk size and folder size.</span></span> <span data-ttu-id="ee53d-214">它將選取最適合物件大小的磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-214">It will select the disk that is most optimized for the object-size.</span></span> <span data-ttu-id="ee53d-215">資料上傳至儲存體帳戶時將併回資料集檔案中指定的目錄結構。</span><span class="sxs-lookup"><span data-stu-id="ee53d-215">The data when uploaded to the storage account will be converged back to the directory structure that was specified in dataset file.</span></span> <span data-ttu-id="ee53d-216">若要建立磁碟機集 CSV，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-216">In order to create a driveset CSV, follow the steps below.</span></span>

### <a name="create-basic-volume-and-assign-drive-letter"></a><span data-ttu-id="ee53d-217">建立基本磁碟區並指派磁碟機代號</span><span class="sxs-lookup"><span data-stu-id="ee53d-217">Create basic volume and assign drive letter</span></span>

<span data-ttu-id="ee53d-218">若要建立基本磁碟區並指派磁碟機代號，請依照[磁碟管理概觀](https://technet.microsoft.com/library/cc754936.aspx)中「建立較簡易的磁碟分割」的指示進行。</span><span class="sxs-lookup"><span data-stu-id="ee53d-218">In order to create a basic volume and assign a drive letter, by following the instructions for "Simpler partition creation" given at [Overview of Disk Management](https://technet.microsoft.com/library/cc754936.aspx).</span></span>

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a><span data-ttu-id="ee53d-219">範例 InitialDriveSet 與 AdditionalDriveSet CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="ee53d-219">Sample InitialDriveSet and AdditionalDriveSet CSV file</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a><span data-ttu-id="ee53d-220">磁碟機集 CSV 檔案欄位</span><span class="sxs-lookup"><span data-stu-id="ee53d-220">Driveset CSV file fields</span></span>

| <span data-ttu-id="ee53d-221">欄位</span><span class="sxs-lookup"><span data-stu-id="ee53d-221">Fields</span></span> | <span data-ttu-id="ee53d-222">值</span><span class="sxs-lookup"><span data-stu-id="ee53d-222">Value</span></span> |
| --- | --- |
| <span data-ttu-id="ee53d-223">DriveLetter</span><span class="sxs-lookup"><span data-stu-id="ee53d-223">DriveLetter</span></span> | <span data-ttu-id="ee53d-224">**[必要]**</span><span class="sxs-lookup"><span data-stu-id="ee53d-224">**[Required]**</span></span><br/> <span data-ttu-id="ee53d-225">每個提供給工具做為目的地的磁碟機上都必須有一個簡單的 NTFS 磁碟區，並已指派磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="ee53d-225">Each drive that is being provided to the tool as the destination needs have a simple NTFS volume on it and a drive letter assigned to it.</span></span><br/> <br/><span data-ttu-id="ee53d-226">**範例**R 或 r</span><span class="sxs-lookup"><span data-stu-id="ee53d-226">**Example**: R or r</span></span> |
| <span data-ttu-id="ee53d-227">FormatOption</span><span class="sxs-lookup"><span data-stu-id="ee53d-227">FormatOption</span></span> | <span data-ttu-id="ee53d-228">**[必要]** Format &#124; AlreadyFormatted</span><span class="sxs-lookup"><span data-stu-id="ee53d-228">**[Required]** Format &#124; AlreadyFormatted</span></span><br/><br/> <span data-ttu-id="ee53d-229">**Format**︰指定這個將格式化磁碟上的所有資料。</span><span class="sxs-lookup"><span data-stu-id="ee53d-229">**Format**: Specifying this will format all the data on the disk.</span></span> <br/><span data-ttu-id="ee53d-230">**AlreadyFormatted**︰指定此值時，工具會略過格式化。</span><span class="sxs-lookup"><span data-stu-id="ee53d-230">**AlreadyFormatted**: The tool will skip formatting when this value is specified.</span></span> |
| <span data-ttu-id="ee53d-231">SilentOrPromptOnFormat</span><span class="sxs-lookup"><span data-stu-id="ee53d-231">SilentOrPromptOnFormat</span></span> | <span data-ttu-id="ee53d-232">**[必要]** SilentMode &#124; PromptOnFormat</span><span class="sxs-lookup"><span data-stu-id="ee53d-232">**[Required]** SilentMode &#124; PromptOnFormat</span></span><br/><br/><span data-ttu-id="ee53d-233">**SilentMode**︰提供這個值可讓使用者以無訊息模式執行工具。</span><span class="sxs-lookup"><span data-stu-id="ee53d-233">**SilentMode**: Providing this value will enable user to run the tool in Silent Mode.</span></span> <br/><span data-ttu-id="ee53d-234">**PromptOnFormat**︰工具會提示使用者確認針對每種格式的動作是否是想要的。</span><span class="sxs-lookup"><span data-stu-id="ee53d-234">**PromptOnFormat**: The tool will prompt the user to confirm whether the action is really intended at every format.</span></span><br/><br/><span data-ttu-id="ee53d-235">如果未設定，命令將會中止並顯示錯誤訊息："Incorrect value for SilentOrPromptOnFormat: none" \(SilentOrPromptOnFormat 的值不正確：無\)</span><span class="sxs-lookup"><span data-stu-id="ee53d-235">If not set, command will abort and display error message: "Incorrect value for SilentOrPromptOnFormat: none"</span></span> |
| <span data-ttu-id="ee53d-236">加密</span><span class="sxs-lookup"><span data-stu-id="ee53d-236">Encryption</span></span> | <span data-ttu-id="ee53d-237">**[必要]** Encrypt &#124; AlreadyEncrypted</span><span class="sxs-lookup"><span data-stu-id="ee53d-237">**[Required]** Encrypt &#124; AlreadyEncrypted</span></span><br/> <span data-ttu-id="ee53d-238">這個欄位的值決定要加密和不加密的磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-238">The value of this field decides which disk to encrypt and which not to.</span></span> <br/><br/><span data-ttu-id="ee53d-239">**Encrypt**︰工具將格式化磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ee53d-239">**Encrypt**: Tool will format the drive.</span></span> <span data-ttu-id="ee53d-240">如果 "FormatOption" 欄位的值是 "Format"，則此值需為 "Encrypt"。</span><span class="sxs-lookup"><span data-stu-id="ee53d-240">If value of "FormatOption" field is "Format" then this value is required to be "Encrypt".</span></span> <span data-ttu-id="ee53d-241">如果在此情況下指定 "AlreadyEncrypted"，則會造成下列錯誤：「指定 Format 時，也必須指定 Encrypt」。</span><span class="sxs-lookup"><span data-stu-id="ee53d-241">If "AlreadyEncrypted" is specified in this case, it will result into an error "When Format is specified, Encrypt must also be specified".</span></span><br/><span data-ttu-id="ee53d-242">**AlreadyEncrypted**︰工具將使用 "ExistingBitLockerKey" 欄位中提供的 BitLockerKey 解密磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ee53d-242">**AlreadyEncrypted**: Tool will decrypt the drive using the BitLockerKey provided in "ExistingBitLockerKey" Field.</span></span> <span data-ttu-id="ee53d-243">如果 "FormatOption" 欄位的值是 "AlreadyFormatted"，這個值可以是 "Encrypt" 或 "AlreadyEncrypted"</span><span class="sxs-lookup"><span data-stu-id="ee53d-243">If value of "FormatOption" field is "AlreadyFormatted", then this value can be either "Encrypt" or "AlreadyEncrypted"</span></span> |
| <span data-ttu-id="ee53d-244">ExistingBitLockerKey</span><span class="sxs-lookup"><span data-stu-id="ee53d-244">ExistingBitLockerKey</span></span> | <span data-ttu-id="ee53d-245">**[必要]** 如果 "Encryption" 欄位的值是 "AlreadyEncrypted"</span><span class="sxs-lookup"><span data-stu-id="ee53d-245">**[Required]** If value of "Encryption" field is "AlreadyEncrypted"</span></span><br/> <span data-ttu-id="ee53d-246">這個欄位的值是與特定磁碟相關聯的 BitLocker 金鑰。</span><span class="sxs-lookup"><span data-stu-id="ee53d-246">The value of this field is the BitLocker key that is associated with the particular disk.</span></span> <br/><br/><span data-ttu-id="ee53d-247">如果 "Encryption" 欄位的值為 "Encrypt"，此欄位應保留空白。</span><span class="sxs-lookup"><span data-stu-id="ee53d-247">This field should be left blank if the value of "Encryption" field is "Encrypt".</span></span>  <span data-ttu-id="ee53d-248">如果在此情況下指定 BitLocker 金鑰，則會造成下列錯誤：「不應指定 Bitlocker 金鑰」。</span><span class="sxs-lookup"><span data-stu-id="ee53d-248">If BitLocker Key is specified in this case, it will result into an error "Bitlocker Key should not be specified".</span></span><br/>  <span data-ttu-id="ee53d-249">**範例**：060456-014509-132033-080300-252615-584177-672089-411631</span><span class="sxs-lookup"><span data-stu-id="ee53d-249">**Example**: 060456-014509-132033-080300-252615-584177-672089-411631</span></span>|

##  <a name="preparing-disk-for-import-job"></a><span data-ttu-id="ee53d-250">準備匯入工作的磁碟</span><span class="sxs-lookup"><span data-stu-id="ee53d-250">Preparing disk for import job</span></span>

<span data-ttu-id="ee53d-251">如果要準備匯入工作的磁碟機，請使用 **PrepImport** 命令呼叫 WAImportExport 工具。</span><span class="sxs-lookup"><span data-stu-id="ee53d-251">To prepare drives for an import job, call the WAImportExport tool with the **PrepImport** command.</span></span> <span data-ttu-id="ee53d-252">您包含的參數取決於這是第一個複製工作階段或後續複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-252">Which parameters you include depends on whether this is the first copy session, or a subsequent copy session.</span></span>

### <a name="first-session"></a><span data-ttu-id="ee53d-253">第一個工作階段</span><span class="sxs-lookup"><span data-stu-id="ee53d-253">First session</span></span>

<span data-ttu-id="ee53d-254">將單一/多重目錄複製到單一/多重磁碟的第一個複製工作階段 (取決於在 CSV 檔案中指定的項目) WAImportExport 工具使用於第一個複製工作階段的 PrepImport 命令，會以新的複製工作階段複製目錄和/或檔案︰</span><span class="sxs-lookup"><span data-stu-id="ee53d-254">First Copy Session to Copy a Single/Multiple Directory to a single/multiple Disk (depending on what is specified in CSV file) WAImportExport tool PrepImport command for the first copy session to copy directories and/or files with a new copy session:</span></span>

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

<span data-ttu-id="ee53d-255">**範例：**</span><span class="sxs-lookup"><span data-stu-id="ee53d-255">**Example:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a><span data-ttu-id="ee53d-256">在後續工作階段中加入資料</span><span class="sxs-lookup"><span data-stu-id="ee53d-256">Add data in subsequent session</span></span>

<span data-ttu-id="ee53d-257">在後續的複製工作階段中，您不需要指定初始參數。</span><span class="sxs-lookup"><span data-stu-id="ee53d-257">In subsequent copy sessions, you do not need to specify the initial parameters.</span></span> <span data-ttu-id="ee53d-258">您必須使用相同的日誌檔案，讓工具能記得前一個工作階段的進度。</span><span class="sxs-lookup"><span data-stu-id="ee53d-258">You need to use the same journal file in order for the tool to remember where it left in the previous session.</span></span> <span data-ttu-id="ee53d-259">複製工作階段的狀態會寫入日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-259">The state of the copy session is written to the journal file.</span></span> <span data-ttu-id="ee53d-260">以下是複製其他目錄和/或檔案的後續複製工作階段的語法︰</span><span class="sxs-lookup"><span data-stu-id="ee53d-260">Here is the syntax for a subsequent copy session to copy additional directories and or files:</span></span>

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

<span data-ttu-id="ee53d-261">**範例：**</span><span class="sxs-lookup"><span data-stu-id="ee53d-261">**Example:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-to-latest-session"></a><span data-ttu-id="ee53d-262">將磁碟機加入最近的工作階段</span><span class="sxs-lookup"><span data-stu-id="ee53d-262">Add drives to latest session</span></span>

<span data-ttu-id="ee53d-263">如果資料無法容納於 InitialDriveset 中指定的磁碟機，可以使用工具將其他磁碟機加入同一個複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-263">If the data did not fit in specified drives in InitialDriveset, one can use the tool to add additional drives to same copy session.</span></span> 

>[!NOTE] 
><span data-ttu-id="ee53d-264">工作階段識別碼應符合前一個工作階段識別碼。日誌檔案應符合前一個工作階段中指定的日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-264">The session id should match the previous session id. Journal file should match the one specified in previous session.</span></span>
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

<span data-ttu-id="ee53d-265">**範例：**</span><span class="sxs-lookup"><span data-stu-id="ee53d-265">**Example:**</span></span>

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-the-latest-session"></a><span data-ttu-id="ee53d-266">中止最近的工作階段︰</span><span class="sxs-lookup"><span data-stu-id="ee53d-266">Abort the latest session:</span></span>

<span data-ttu-id="ee53d-267">如果複製工作階段中斷且無法繼續 (例如來源目錄已證實無法存取)，您必須中止目前的工作階段，使其可以回復並開始新的複製工作階段︰</span><span class="sxs-lookup"><span data-stu-id="ee53d-267">If a copy session is interrupted and it is not possible to resume (for example, if a source directory proved inaccessible), you must abort the current session so that it can be rolled back and new copy sessions can be started:</span></span>

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

<span data-ttu-id="ee53d-268">**範例：**</span><span class="sxs-lookup"><span data-stu-id="ee53d-268">**Example:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

<span data-ttu-id="ee53d-269">如果是異常終止，只能中止最後一個複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-269">Only the last copy session, if terminated abnormally, can be aborted.</span></span> <span data-ttu-id="ee53d-270">請注意，您無法中止磁碟機的第一個複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-270">Note that you cannot abort the first copy session for a drive.</span></span> <span data-ttu-id="ee53d-271">而是必須使用新的日誌檔案重新開始複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-271">Instead you must restart the copy session with a new journal file.</span></span>

### <a name="resume-a-latest-interrupted-session"></a><span data-ttu-id="ee53d-272">繼續最近中斷的工作階段</span><span class="sxs-lookup"><span data-stu-id="ee53d-272">Resume a latest interrupted session</span></span>

<span data-ttu-id="ee53d-273">如果複製工作階段因任何原因中斷，只要指定日誌檔案，就可以執行工具來繼續︰</span><span class="sxs-lookup"><span data-stu-id="ee53d-273">If a copy session is interrupted for any reason, you can resume it by running the tool with only the journal file specified:</span></span>

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

<span data-ttu-id="ee53d-274">**範例：**</span><span class="sxs-lookup"><span data-stu-id="ee53d-274">**Example:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> <span data-ttu-id="ee53d-275">當您繼續複製工作階段時，請勿以加入或移除檔案的方式修改來源資料檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-275">When you resume a copy session, do not modify the source data files and directories by adding or removing files.</span></span>

## <a name="waimportexport-parameters"></a><span data-ttu-id="ee53d-276">WAImportExport 參數</span><span class="sxs-lookup"><span data-stu-id="ee53d-276">WAImportExport parameters</span></span>

| <span data-ttu-id="ee53d-277">參數</span><span class="sxs-lookup"><span data-stu-id="ee53d-277">Parameters</span></span> | <span data-ttu-id="ee53d-278">說明</span><span class="sxs-lookup"><span data-stu-id="ee53d-278">Description</span></span> |
| --- | --- |
|     <span data-ttu-id="ee53d-279">/j:&lt;JournalFile&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-279">/j:&lt;JournalFile&gt;</span></span>  | <span data-ttu-id="ee53d-280">**必要**</span><span class="sxs-lookup"><span data-stu-id="ee53d-280">**Required**</span></span><br/> <span data-ttu-id="ee53d-281">日誌檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="ee53d-281">Path to the journal file.</span></span> <span data-ttu-id="ee53d-282">日誌檔案會追蹤一組磁碟機，並記錄準備這些磁碟機的進度。</span><span class="sxs-lookup"><span data-stu-id="ee53d-282">A journal file tracks a set of drives and records the progress in preparing these drives.</span></span> <span data-ttu-id="ee53d-283">日誌檔案一律需要指定。</span><span class="sxs-lookup"><span data-stu-id="ee53d-283">The journal file must always be specified.</span></span>  |
|     <span data-ttu-id="ee53d-284">/logdir:&lt;LogDirectory&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-284">/logdir:&lt;LogDirectory&gt;</span></span>  | <span data-ttu-id="ee53d-285">**選用**。</span><span class="sxs-lookup"><span data-stu-id="ee53d-285">**Optional**.</span></span> <span data-ttu-id="ee53d-286">記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-286">The log directory.</span></span><br/> <span data-ttu-id="ee53d-287">詳細資訊記錄檔及某些暫存檔案會寫入至這個目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-287">Verbose log files as well as some temporary files will be written to this directory.</span></span> <span data-ttu-id="ee53d-288">如未指定，將使用目前的目錄做為記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-288">If not specified, current directory will be used as the log directory.</span></span> <span data-ttu-id="ee53d-289">同一日誌檔案只能指定一次記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-289">The log directory can be specified only once for the same journal file.</span></span>  |
|     <span data-ttu-id="ee53d-290">/id:&lt;SessionId&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-290">/id:&lt;SessionId&gt;</span></span>  | <span data-ttu-id="ee53d-291">**必要**</span><span class="sxs-lookup"><span data-stu-id="ee53d-291">**Required**</span></span><br/> <span data-ttu-id="ee53d-292">工作階段識別碼用於識別複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-292">The session Id is used to identify a copy session.</span></span> <span data-ttu-id="ee53d-293">其用來確保正確復原中斷的複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-293">It is used to ensure accurate recovery of an interrupted copy session.</span></span>  |
|     <span data-ttu-id="ee53d-294">/ResumeSession</span><span class="sxs-lookup"><span data-stu-id="ee53d-294">/ResumeSession</span></span>  | <span data-ttu-id="ee53d-295">選用。</span><span class="sxs-lookup"><span data-stu-id="ee53d-295">Optional.</span></span> <span data-ttu-id="ee53d-296">如果最後一個複製工作階段異常終止，可以指定此參數以繼續工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-296">If the last copy session was terminated abnormally, this parameter can be specified to resume the session.</span></span>   |
|     <span data-ttu-id="ee53d-297">/AbortSession</span><span class="sxs-lookup"><span data-stu-id="ee53d-297">/AbortSession</span></span>  | <span data-ttu-id="ee53d-298">選用。</span><span class="sxs-lookup"><span data-stu-id="ee53d-298">Optional.</span></span> <span data-ttu-id="ee53d-299">如果最後一個複製工作階段異常終止，可以指定此參數以中止工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-299">If the last copy session was terminated abnormally, this parameter can be specified to abort the session.</span></span>  |
|     <span data-ttu-id="ee53d-300">/sn:&lt;StorageAccountName&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-300">/sn:&lt;StorageAccountName&gt;</span></span>  | <span data-ttu-id="ee53d-301">**必要**</span><span class="sxs-lookup"><span data-stu-id="ee53d-301">**Required**</span></span><br/> <span data-ttu-id="ee53d-302">僅適用於 RepairImport 和 RepairExport。</span><span class="sxs-lookup"><span data-stu-id="ee53d-302">Only applicable for RepairImport and RepairExport.</span></span> <span data-ttu-id="ee53d-303">儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="ee53d-303">The name of the storage account.</span></span>  |
|     <span data-ttu-id="ee53d-304">/sk:&lt;StorageAccountKey&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-304">/sk:&lt;StorageAccountKey&gt;</span></span>  | <span data-ttu-id="ee53d-305">**必要**</span><span class="sxs-lookup"><span data-stu-id="ee53d-305">**Required**</span></span><br/> <span data-ttu-id="ee53d-306">儲存體帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="ee53d-306">The key of the storage account.</span></span> |
|     <span data-ttu-id="ee53d-307">/InitialDriveSet:&lt;driveset.csv&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-307">/InitialDriveSet:&lt;driveset.csv&gt;</span></span>  | <span data-ttu-id="ee53d-308">**必要** 執行第一個複製工作階段時</span><span class="sxs-lookup"><span data-stu-id="ee53d-308">**Required** When running the first copy session</span></span><br/> <span data-ttu-id="ee53d-309">CSV 檔案，包含要準備的磁碟機清單。</span><span class="sxs-lookup"><span data-stu-id="ee53d-309">A CSV file that contains a list of drives to prepare.</span></span>  |
|     <span data-ttu-id="ee53d-310">/AdditionalDriveSet:&lt;driveset.csv&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-310">/AdditionalDriveSet:&lt;driveset.csv&gt;</span></span> | <span data-ttu-id="ee53d-311">**必要**。</span><span class="sxs-lookup"><span data-stu-id="ee53d-311">**Required**.</span></span> <span data-ttu-id="ee53d-312">將磁碟機加入目前的複製工作階段時。</span><span class="sxs-lookup"><span data-stu-id="ee53d-312">When adding drives to current copy session.</span></span> <br/> <span data-ttu-id="ee53d-313">CSV 檔案，包含要加入的其他磁碟機的清單。</span><span class="sxs-lookup"><span data-stu-id="ee53d-313">A CSV file that contains a list of additional drives to be added.</span></span>  |
|      <span data-ttu-id="ee53d-314">/r:&lt;RepairFile&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-314">/r:&lt;RepairFile&gt;</span></span> | <span data-ttu-id="ee53d-315">**必要** 僅適用於 RepairImport 和 RepairExport。</span><span class="sxs-lookup"><span data-stu-id="ee53d-315">**Required** Only applicable for RepairImport and RepairExport.</span></span><br/> <span data-ttu-id="ee53d-316">追蹤修復進度之檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="ee53d-316">Path to the file for tracking repair progress.</span></span> <span data-ttu-id="ee53d-317">每個磁碟機需要一個修復檔案，而且只能有一個。</span><span class="sxs-lookup"><span data-stu-id="ee53d-317">Each drive must have one and only one repair file.</span></span>  |
|     <span data-ttu-id="ee53d-318">/d:&lt;TargetDirectories&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-318">/d:&lt;TargetDirectories&gt;</span></span> | <span data-ttu-id="ee53d-319">**必要**。</span><span class="sxs-lookup"><span data-stu-id="ee53d-319">**Required**.</span></span> <span data-ttu-id="ee53d-320">僅適用於 RepairImport 和 RepairExport。</span><span class="sxs-lookup"><span data-stu-id="ee53d-320">Only applicable for RepairImport and RepairExport.</span></span> <span data-ttu-id="ee53d-321">用於 RepairImport 時，是要修復的一或多個目錄 (以分號分隔)；用於 RepairExport 時，是要修復的目錄，例如磁碟機根目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-321">For RepairImport, one or more semicolon-separated directories to repair; For RepairExport, one directory to repair, e.g. root directory of the drive.</span></span>  |
|     <span data-ttu-id="ee53d-322">/CopyLogFile:&lt;DriveCopyLogFile&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-322">/CopyLogFile:&lt;DriveCopyLogFile&gt;</span></span> | <span data-ttu-id="ee53d-323">**必要** 僅適用於 RepairImport 和 RepairExport。</span><span class="sxs-lookup"><span data-stu-id="ee53d-323">**Required** Only applicable for RepairImport and RepairExport.</span></span> <span data-ttu-id="ee53d-324">磁碟機複製記錄檔 (詳細資訊或錯誤) 的路徑。</span><span class="sxs-lookup"><span data-stu-id="ee53d-324">Path to the  drive copy log file (verbose or error).</span></span>  |
|     <span data-ttu-id="ee53d-325">/ManifestFile:&lt;DriveManifestFile&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-325">/ManifestFile:&lt;DriveManifestFile&gt;</span></span> | <span data-ttu-id="ee53d-326">**必要** 僅適用於 RepairExport。</span><span class="sxs-lookup"><span data-stu-id="ee53d-326">**Required** Only applicable for RepairExport.</span></span><br/> <span data-ttu-id="ee53d-327">磁碟機資訊清單檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="ee53d-327">Path to the drive manifest file.</span></span>  |
|     <span data-ttu-id="ee53d-328">/PathMapFile:&lt;DrivePathMapFile&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-328">/PathMapFile:&lt;DrivePathMapFile&gt;</span></span> | <span data-ttu-id="ee53d-329">**選用**。</span><span class="sxs-lookup"><span data-stu-id="ee53d-329">**Optional**.</span></span> <span data-ttu-id="ee53d-330">僅適用於 RepairImport。</span><span class="sxs-lookup"><span data-stu-id="ee53d-330">Only applicable for RepairImport.</span></span><br/> <span data-ttu-id="ee53d-331">包含檔案路徑對應 (相對於實際檔案位置的磁碟機根目錄) 之檔案的路徑 (以 tab 分隔)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-331">Path to the file containing mappings of file paths relative to the drive root to locations of actual files (tab-delimited).</span></span> <span data-ttu-id="ee53d-332">第一次指定時，它會填入空白目標的檔案路徑，表示在 TargetDirectories 中找不到它們、存取被拒、具有無效名稱，或它們存在多個目錄中。</span><span class="sxs-lookup"><span data-stu-id="ee53d-332">When first specified, it will be populated with file paths with empty targets, which means either they are not found in TargetDirectories, access denied, with invalid name, or they exist in multiple directories.</span></span> <span data-ttu-id="ee53d-333">路徑對應檔案可以手動編輯以包含正確的目標路徑，並可再次指定，使工具可以正確解析檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="ee53d-333">The path map file can be manually edited to include the correct target paths and  specified again for the tool to resolve the file paths correctly.</span></span>  |
|     <span data-ttu-id="ee53d-334">/ExportBlobListFile:&lt;ExportBlobListFile&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-334">/ExportBlobListFile:&lt;ExportBlobListFile&gt;</span></span> | <span data-ttu-id="ee53d-335">**必要**。</span><span class="sxs-lookup"><span data-stu-id="ee53d-335">**Required**.</span></span> <span data-ttu-id="ee53d-336">僅適用於 PreviewExport。</span><span class="sxs-lookup"><span data-stu-id="ee53d-336">Only applicable for PreviewExport.</span></span><br/> <span data-ttu-id="ee53d-337">XML 檔案的路徑，此檔案包含要匯出的 Blob 的Blob 路徑清單或 Blob 路徑前置詞。</span><span class="sxs-lookup"><span data-stu-id="ee53d-337">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span></span> <span data-ttu-id="ee53d-338">此檔案格式與匯入/匯出服務 REST API 的 Put Job 作業中的 Blob 清單 Blob 格式相同。</span><span class="sxs-lookup"><span data-stu-id="ee53d-338">The file format is the same as the blob list blob format in the Put Job operation of the Import/Export service REST API.</span></span>  |
|     <span data-ttu-id="ee53d-339">/DriveSize:&lt;DriveSize&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-339">/DriveSize:&lt;DriveSize&gt;</span></span> | <span data-ttu-id="ee53d-340">**必要**。</span><span class="sxs-lookup"><span data-stu-id="ee53d-340">**Required**.</span></span> <span data-ttu-id="ee53d-341">僅適用於 PreviewExport。</span><span class="sxs-lookup"><span data-stu-id="ee53d-341">Only applicable for PreviewExport.</span></span><br/>  <span data-ttu-id="ee53d-342">要用於匯出的磁碟機大小。</span><span class="sxs-lookup"><span data-stu-id="ee53d-342">Size of drives to be used for export.</span></span> <span data-ttu-id="ee53d-343">例如，500 GB、1.5 TB。</span><span class="sxs-lookup"><span data-stu-id="ee53d-343">For example, 500 GB, 1.5 TB.</span></span> <span data-ttu-id="ee53d-344">注意：1 GB = 1,000,000,000 個位元組 1 TB = 1,000,000,000,000 個位元組</span><span class="sxs-lookup"><span data-stu-id="ee53d-344">Note: 1 GB = 1,000,000,000 bytes1 TB = 1,000,000,000,000 bytes</span></span>  |
|     <span data-ttu-id="ee53d-345">/DataSet:&lt;dataset.csv&gt;</span><span class="sxs-lookup"><span data-stu-id="ee53d-345">/DataSet:&lt;dataset.csv&gt;</span></span> | <span data-ttu-id="ee53d-346">**必要**</span><span class="sxs-lookup"><span data-stu-id="ee53d-346">**Required**</span></span><br/> <span data-ttu-id="ee53d-347">CSV 檔案，包含要複製到目標磁碟機的目錄清單和/或檔案清單。</span><span class="sxs-lookup"><span data-stu-id="ee53d-347">A CSV file that contains a list of directories and/or a list of files to be copied to target drives.</span></span>  |
|     <span data-ttu-id="ee53d-348">/silentmode</span><span class="sxs-lookup"><span data-stu-id="ee53d-348">/silentmode</span></span>  | <span data-ttu-id="ee53d-349">**選用**。</span><span class="sxs-lookup"><span data-stu-id="ee53d-349">**Optional**.</span></span><br/> <span data-ttu-id="ee53d-350">如未指定，它會提醒您磁碟機的需求，並需要您確認才能繼續。</span><span class="sxs-lookup"><span data-stu-id="ee53d-350">If not specified, it will remind you the requirement of drives and need your confirmation to continue.</span></span>  |

## <a name="tool-output"></a><span data-ttu-id="ee53d-351">工具輸出</span><span class="sxs-lookup"><span data-stu-id="ee53d-351">Tool output</span></span>

### <a name="sample-drive-manifest-file"></a><span data-ttu-id="ee53d-352">範例磁碟機資訊清單檔案</span><span class="sxs-lookup"><span data-stu-id="ee53d-352">Sample drive manifest file</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies to all blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a><span data-ttu-id="ee53d-353">每個磁碟機的範例日誌檔案 (XML)</span><span class="sxs-lookup"><span data-stu-id="ee53d-353">Sample journal file (XML) for each drive</span></span>

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-the-trail-of-sessions"></a><span data-ttu-id="ee53d-354">工作階段的範例日誌檔案 (JRN)，此檔案會記錄工作階段的軌跡</span><span class="sxs-lookup"><span data-stu-id="ee53d-354">Sample journal file (JRN) for session that records the trail of sessions</span></span>

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a><span data-ttu-id="ee53d-355">常見問題集</span><span class="sxs-lookup"><span data-stu-id="ee53d-355">FAQ</span></span>

### <a name="general"></a><span data-ttu-id="ee53d-356">一般</span><span class="sxs-lookup"><span data-stu-id="ee53d-356">General</span></span>

#### <a name="what-is-waimportexport-tool"></a><span data-ttu-id="ee53d-357">什麼是 WAImportExport 工具？</span><span class="sxs-lookup"><span data-stu-id="ee53d-357">What is WAImportExport tool?</span></span>

<span data-ttu-id="ee53d-358">WAImportExport 工具是磁碟機準備及修復工具，可搭配 Microsoft Azure 匯入/匯出服務使用。</span><span class="sxs-lookup"><span data-stu-id="ee53d-358">The WAImportExport tool is the drive preparation and repair tool that you can use with the Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="ee53d-359">您可以使用此工具，將資料複製到要寄送至 Azure 資料中心的硬碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-359">You can use this tool to copy data to the hard drives you are going to ship to an Azure data center.</span></span> <span data-ttu-id="ee53d-360">匯入工作完成後，您可以使用此工具來修復損毀、遺漏或與其他 Blob 衝突的任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="ee53d-360">After an import job has completed, you can use this tool to repair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span> <span data-ttu-id="ee53d-361">當您收到已完成的匯出工作中的磁碟機後，您可以使用此工具來修復磁碟機上損毀或遺漏的任何檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-361">After you receive the drives from a completed export job, you can use this tool to repair any files that were corrupted or missing on the drives.</span></span>

#### <a name="how-does-the-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a><span data-ttu-id="ee53d-362">WAImportExport 工具如何在多個來源目錄和磁碟上運作？</span><span class="sxs-lookup"><span data-stu-id="ee53d-362">How does the WAImportExport tool work on multiple source dir and disks?</span></span>

<span data-ttu-id="ee53d-363">如果資料大小超過磁碟大小，WAImportExport 工具會將資料以最佳化方式分散在多個磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-363">If the data size is greater than the disk size, the WAImportExport tool will distribute the data across the disks in an optimized way.</span></span> <span data-ttu-id="ee53d-364">資料可以平行或循序方式複製到多個磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-364">The data copy to multiple disks can be done in parallel or sequentially.</span></span> <span data-ttu-id="ee53d-365">同時寫入資料的磁碟數目沒有限制。</span><span class="sxs-lookup"><span data-stu-id="ee53d-365">There is no limit on the number of disks the data can be written to simultaneously.</span></span> <span data-ttu-id="ee53d-366">此工具會根據磁碟大小和資料夾大小來分配資料。</span><span class="sxs-lookup"><span data-stu-id="ee53d-366">The tool will distribute data based on disk size and folder size.</span></span> <span data-ttu-id="ee53d-367">它將選取最適合物件大小的磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-367">It will select the disk that is most optimized for the object-size.</span></span> <span data-ttu-id="ee53d-368">資料上傳至儲存體帳戶時將併回指定的目錄結構。</span><span class="sxs-lookup"><span data-stu-id="ee53d-368">The data when uploaded to the storage account will be converged back to the specified directory structure.</span></span>

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a><span data-ttu-id="ee53d-369">哪裡可以找到舊版的 WAImportExport 工具？</span><span class="sxs-lookup"><span data-stu-id="ee53d-369">Where can I find previous version of WAImportExport tool?</span></span>

<span data-ttu-id="ee53d-370">WAImportExport 工具擁有 WAImportExport V1 工具的所有功能。</span><span class="sxs-lookup"><span data-stu-id="ee53d-370">WAImportExport tool has all functionalities that WAImportExport V1 tool had.</span></span> <span data-ttu-id="ee53d-371">WAImportExport 工具可讓使用者指定多個來源並寫入多個磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ee53d-371">WAImportExport tool allows users to specify multiple sources and write to multiple drives.</span></span> <span data-ttu-id="ee53d-372">此外，使用者可以輕鬆地管理多個來源位置 (資料必須從這些來源位置複製到單一 CSV 檔案)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-372">Additionally, one can easily manage multiple source locations from which the data needs to be copied in a single CSV file.</span></span> <span data-ttu-id="ee53d-373">不過，萬一您需要 SAS 支援或想要將單一來源複製到單一磁碟，您可以 [下載 WAImportExport V1 工具] (http://go.microsoft.com/fwlink/?LinkID=301900&amp;clcid=0x409)，並參閱 [WAImportExport V1 參考](storage-import-export-tool-how-to-v1.md) 以取得 WAImportExport V1 使用方式的說明。</span><span class="sxs-lookup"><span data-stu-id="ee53d-373">However, in case you need SAS support or want to copy single source to single disk, you can [download WAImportExport V1 Tool] (http://go.microsoft.com/fwlink/?LinkID=301900&amp;clcid=0x409) and refer to [WAImportExport V1 Reference](storage-import-export-tool-how-to-v1.md) for help with WAImportExport V1 usage.</span></span>

#### <a name="what-is-a-session-id"></a><span data-ttu-id="ee53d-374">什麼是工作階段識別碼？</span><span class="sxs-lookup"><span data-stu-id="ee53d-374">What is a session ID?</span></span>

<span data-ttu-id="ee53d-375">如果目的是要將資料分散到多個磁碟，此工具會預期複製工作階段 (/id) 參數應相同。</span><span class="sxs-lookup"><span data-stu-id="ee53d-375">The tool expects the copy session (/id) parameter to be the same if the intent is to spread the data across multiple disks.</span></span> <span data-ttu-id="ee53d-376">維持相同的複製工作階段名稱可讓使用者將資料從一或多個來源位置複製到一或多個目的地磁碟/目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-376">Maintaining the same name of the copy session will enable user to copy data from one or multiple source locations into one or multiple destination disks/directories.</span></span> <span data-ttu-id="ee53d-377">維持相同的工作階段識別碼可讓工具重新找到上次處理的檔案複本。</span><span class="sxs-lookup"><span data-stu-id="ee53d-377">Maintaining same session id enables the tool to pick up the copy of files from where it was left the last time.</span></span>

<span data-ttu-id="ee53d-378">不過，相同的複製工作階段不能用於匯入資料到不同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee53d-378">However, same copy session cannot be used to import data to different storage accounts.</span></span>

<span data-ttu-id="ee53d-379">複製工作階段名稱在工具多次執行之間都相同時，記錄檔 (/logdir) 和儲存體帳戶金鑰 (/sk) 也應該相同。</span><span class="sxs-lookup"><span data-stu-id="ee53d-379">When copy-session name is same across multiple runs of the tool, the logfile (/logdir) and storage account key (/sk) is also expected to be the same.</span></span>

<span data-ttu-id="ee53d-380">工作階段識別碼可以包含字母、0~9、底線 (\_)、虛線 (-) 或井字鍵 (#)，且其長度必須是 3~30。</span><span class="sxs-lookup"><span data-stu-id="ee53d-380">SessionId can consist of letters, 0~9, understore (\_), dash (-) or hash (#), and its length must be 3~30.</span></span>

<span data-ttu-id="ee53d-381">例如︰session-1 或 session#1 或 session\_1</span><span class="sxs-lookup"><span data-stu-id="ee53d-381">e.g. session-1 or session#1 or session\_1</span></span>

#### <a name="what-is-a-journal-file"></a><span data-ttu-id="ee53d-382">什麼是日誌檔案？</span><span class="sxs-lookup"><span data-stu-id="ee53d-382">What is a journal file?</span></span>

<span data-ttu-id="ee53d-383">每次執行 WAImportExport 工具以將檔案複製到硬碟時，工具會建立一個複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-383">Each time you run the WAImportExport tool to copy files to the hard drive, the tool creates a copy session.</span></span> <span data-ttu-id="ee53d-384">複製工作階段的狀態會寫入日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-384">The state of the copy session is written to the journal file.</span></span> <span data-ttu-id="ee53d-385">如果複製工作階段中斷 (例如，因為系統電源斷電)，可以再次執行工具並在命令列指定日誌檔案以繼續。</span><span class="sxs-lookup"><span data-stu-id="ee53d-385">If a copy session is interrupted (for example, due to a system power loss), it can be resumed by running the tool again and specifying the journal file on the command line.</span></span>

<span data-ttu-id="ee53d-386">對於您使用 Azure 匯入/匯出工具準備的每個硬碟，此工具會建立名為 "&lt;DriveID&gt;.xml" 的單一日誌檔案，其中的磁碟機識別碼是與工具從磁碟讀取的磁碟機相關聯的序號。</span><span class="sxs-lookup"><span data-stu-id="ee53d-386">For each hard drive that you prepare with the Azure Import/Export Tool, the tool will create a single journal file with name "&lt;DriveID&gt;.xml" where drive Id is the serial number associated to the drive that the tool reads from the disk.</span></span> <span data-ttu-id="ee53d-387">所有磁碟機都將需要日誌檔案，才能建立匯入工作。</span><span class="sxs-lookup"><span data-stu-id="ee53d-387">You will need the journal files from all of your drives to create the import job.</span></span> <span data-ttu-id="ee53d-388">如果工具中斷，日誌檔案也可用來繼續磁碟機準備。</span><span class="sxs-lookup"><span data-stu-id="ee53d-388">The journal file can also be used to resume drive preparation if the tool is interrupted.</span></span>

#### <a name="what-is-a-log-directory"></a><span data-ttu-id="ee53d-389">什麼是記錄檔目錄？</span><span class="sxs-lookup"><span data-stu-id="ee53d-389">What is a log directory?</span></span>

<span data-ttu-id="ee53d-390">記錄檔目錄指定要用來儲存詳細資訊記錄檔和暫存資訊清單檔案的目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-390">The log directory specifies a directory to be used to store verbose logs as well as temporary manifest files.</span></span> <span data-ttu-id="ee53d-391">如未指定，將使用目前的目錄做為記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-391">If not specified, the current directory will be used as the log directory.</span></span> <span data-ttu-id="ee53d-392">記錄是詳細資訊記錄。</span><span class="sxs-lookup"><span data-stu-id="ee53d-392">The logs are verbose logs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ee53d-393">必要條件</span><span class="sxs-lookup"><span data-stu-id="ee53d-393">Prerequisites</span></span>

#### <a name="what-are-the-specifications-of-my-disk"></a><span data-ttu-id="ee53d-394">什麼是磁碟的規格？</span><span class="sxs-lookup"><span data-stu-id="ee53d-394">What are the specifications of my disk?</span></span>

<span data-ttu-id="ee53d-395">一或多個連接至複製電腦的空白 2.5 英吋或 3.5 英吋 SATAII 或 III 或 SSD 硬碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-395">One or more empty 2.5-inch or 3.5-inch SATAII or III or SSD hard drives connected to the copy machine.</span></span>

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a><span data-ttu-id="ee53d-396">如何啟用我電腦上的 BitLocker？</span><span class="sxs-lookup"><span data-stu-id="ee53d-396">How can I enable BitLocker on my machine?</span></span>

<span data-ttu-id="ee53d-397">簡易的檢查方式是以滑鼠右鍵按一下系統磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="ee53d-397">Simple way to check is by right-clicking on System drive.</span></span> <span data-ttu-id="ee53d-398">它會顯示 Bitlocker 的選項 (如果此功能已開啟)。</span><span class="sxs-lookup"><span data-stu-id="ee53d-398">It will show you options for Bitlocker if the capability is turned on.</span></span> <span data-ttu-id="ee53d-399">如果此功能已關閉，您就不會看到它。</span><span class="sxs-lookup"><span data-stu-id="ee53d-399">If it is off, you won't see it.</span></span>

![檢查 BitLocker](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

<span data-ttu-id="ee53d-401">這裡有關於[如何啟用 BitLocker](https://technet.microsoft.com/library/cc766295.aspx)的文章</span><span class="sxs-lookup"><span data-stu-id="ee53d-401">Here is an article on [how to enable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)</span></span>

<span data-ttu-id="ee53d-402">您的電腦很可能沒有 TPM 晶片。</span><span class="sxs-lookup"><span data-stu-id="ee53d-402">It is possible that your machine does not have TPM chip.</span></span> <span data-ttu-id="ee53d-403">如果您使用 tpm.msc 並未取得輸出，請查看下一個常見問題集。</span><span class="sxs-lookup"><span data-stu-id="ee53d-403">If you do not get an output using tpm.msc, look at the next FAQ.</span></span>

#### <a name="how-to-disable-trusted-platform-module-tpm-in-bitlocker"></a><span data-ttu-id="ee53d-404">如何停用 BitLocker 中受信任的平台模組 (TPM)？</span><span class="sxs-lookup"><span data-stu-id="ee53d-404">How to disable Trusted Platform Module (TPM) in BitLocker?</span></span>
> [!NOTE]
> <span data-ttu-id="ee53d-405">只有當他們的伺服器中沒有 TPM 時，您才需要停用 TPM 原則。</span><span class="sxs-lookup"><span data-stu-id="ee53d-405">Only if there is no TPM in their servers, you need to disable TPM policy.</span></span> <span data-ttu-id="ee53d-406">如果使用者的伺服器中具有受信任的 TPM，就不需要停用 TPM。</span><span class="sxs-lookup"><span data-stu-id="ee53d-406">It is not necessary to disable TPM if there is a trusted TPM in user's server.</span></span> 
> 

<span data-ttu-id="ee53d-407">若要停用 BitLocker 中的 TPM，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ee53d-407">In order to disable TPM in BitLocker, go through the following steps:</span></span><br/>
1. <span data-ttu-id="ee53d-408">在命令提示字元中輸入 gpedit.msc 以啟動**群組原則編輯器**。</span><span class="sxs-lookup"><span data-stu-id="ee53d-408">Launch **Group Policy Editor** by typing gpedit.msc on a command prompt.</span></span> <span data-ttu-id="ee53d-409">如果**群組原則編輯器**似乎無法使用，請先啟用 BitLocker。</span><span class="sxs-lookup"><span data-stu-id="ee53d-409">If **Group Policy Editor** appears to be unavailable, for enabling BitLocker first.</span></span> <span data-ttu-id="ee53d-410">請參閱先前的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="ee53d-410">See previous FAQ.</span></span>
2. <span data-ttu-id="ee53d-411">開啟 [本機電腦原則] &gt;[電腦設定] &gt; [系統管理範本] &gt; [Windows 元件] &gt; [BitLocker 磁碟機加密] &gt; [作業系統磁碟機]。</span><span class="sxs-lookup"><span data-stu-id="ee53d-411">Open **Local Computer Policy &gt; Computer Configuration &gt; Administrative Templates &gt; Windows Components&gt; BitLocker Drive Encryption &gt; Operating System Drives**.</span></span>
3. <span data-ttu-id="ee53d-412">編輯 [啟動時需要其他驗證] 原則。</span><span class="sxs-lookup"><span data-stu-id="ee53d-412">Edit **Require additional authentication at startup** policy.</span></span>
4. <span data-ttu-id="ee53d-413">將原則設為 [啟用]，確定已核取 [在不含相容 TPM 的情形下允許使用 BitLocker]。</span><span class="sxs-lookup"><span data-stu-id="ee53d-413">Set the policy to **Enabled** and make sure **Allow BitLocker without a compatible TPM** is checked.</span></span>

####  <a name="how-to-check-if-net-4-or-higher-version-is-installed-on-my-machine"></a><span data-ttu-id="ee53d-414">如何檢查電腦上是否已安裝 .NET 4 或更新版本？</span><span class="sxs-lookup"><span data-stu-id="ee53d-414">How to check if .NET 4 or higher version is installed on my machine?</span></span>

<span data-ttu-id="ee53d-415">所有 Microsoft .NET Framework 版本均會安裝在下列目錄︰%windir%\Microsoft.NET\Framework\\</span><span class="sxs-lookup"><span data-stu-id="ee53d-415">All Microsoft .NET Framework versions are installed in following directory: %windir%\Microsoft.NET\Framework\\</span></span>

<span data-ttu-id="ee53d-416">在您的目標電腦上，瀏覽至執行工具所需的上述組件所在的位置。</span><span class="sxs-lookup"><span data-stu-id="ee53d-416">Navigate to the above mentioned part on your target machine where the tool needs to run.</span></span> <span data-ttu-id="ee53d-417">尋找開頭為 "v4" 的資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="ee53d-417">Look for folder name starting with "v4".</span></span> <span data-ttu-id="ee53d-418">如果此目錄不存在，表示您的電腦上並未安裝 .NET 4。</span><span class="sxs-lookup"><span data-stu-id="ee53d-418">Absence of such a directory means .NET 4 is not installed on your machine.</span></span> <span data-ttu-id="ee53d-419">您可以使用 [Microsoft .NET Framework 4 (Web 安裝程式)](https://www.microsoft.com/download/details.aspx?id=17851) 在您的電腦上下載 .Net 4。</span><span class="sxs-lookup"><span data-stu-id="ee53d-419">You can download .Net 4 on your machine using [Microsoft .NET Framework 4 (Web Installer)](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>

### <a name="limits"></a><span data-ttu-id="ee53d-420">限制</span><span class="sxs-lookup"><span data-stu-id="ee53d-420">Limits</span></span>

#### <a name="how-many-drives-can-i-preparesend-at-the-same-time"></a><span data-ttu-id="ee53d-421">一次可以準備/傳送多少個磁碟機？</span><span class="sxs-lookup"><span data-stu-id="ee53d-421">How many drives can I prepare/send at the same time?</span></span>

<span data-ttu-id="ee53d-422">此工具可以準備的磁碟數目沒有限制。</span><span class="sxs-lookup"><span data-stu-id="ee53d-422">There is no limit on the number of disks that the tool can prepare.</span></span> <span data-ttu-id="ee53d-423">不過，此工具需要磁碟機代號做為輸入。</span><span class="sxs-lookup"><span data-stu-id="ee53d-423">However, the tool expects drive letters as inputs.</span></span> <span data-ttu-id="ee53d-424">因此可同時準備的磁碟限制為 25 個。</span><span class="sxs-lookup"><span data-stu-id="ee53d-424">That limits it to 25 simultaneous disk preparation.</span></span> <span data-ttu-id="ee53d-425">單一工作一次最多可處理 10 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-425">A single job can handle maximum of 10 disks at a time.</span></span> <span data-ttu-id="ee53d-426">如果您有 10 個以上的磁碟都對應同一儲存體帳戶，磁碟可以分散到多個工作。</span><span class="sxs-lookup"><span data-stu-id="ee53d-426">If you prepare more than 10 disks targeting the same storage account, the disks can be distributed across multiple jobs.</span></span>

#### <a name="can-i-target-more-than-one-storage-account"></a><span data-ttu-id="ee53d-427">可以對應一個以上的儲存體帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="ee53d-427">Can I target more than one storage account?</span></span>

<span data-ttu-id="ee53d-428">每個工作只能提交一個儲存體帳戶，且一個儲存體帳戶只能用於單一複製工作階段。</span><span class="sxs-lookup"><span data-stu-id="ee53d-428">Only one storage account can be submitted per job and in single copy session.</span></span>

### <a name="capabilities"></a><span data-ttu-id="ee53d-429">功能</span><span class="sxs-lookup"><span data-stu-id="ee53d-429">Capabilities</span></span>

#### <a name="does-waimportexportexe-encrypt-my-data"></a><span data-ttu-id="ee53d-430">WAImportExport.exe 是否會加密資料？</span><span class="sxs-lookup"><span data-stu-id="ee53d-430">Does WAImportExport.exe encrypt my data?</span></span>

<span data-ttu-id="ee53d-431">是。</span><span class="sxs-lookup"><span data-stu-id="ee53d-431">Yes.</span></span> <span data-ttu-id="ee53d-432">此程序會啟用必須的 BitLocker 加密。</span><span class="sxs-lookup"><span data-stu-id="ee53d-432">BitLocker encryption is enabled and required for this process.</span></span>

#### <a name="what-will-be-the-hierarchy-of-my-data-when-it-appears-in-the-storage-account"></a><span data-ttu-id="ee53d-433">資料在儲存體帳戶中會以何種階層顯示？</span><span class="sxs-lookup"><span data-stu-id="ee53d-433">What will be the hierarchy of my data when it appears in the storage account?</span></span>

<span data-ttu-id="ee53d-434">雖然資料分散到多個磁碟，但上傳至儲存體帳戶時將併回在資料集 CSV 檔案中指定的目錄結構。</span><span class="sxs-lookup"><span data-stu-id="ee53d-434">Although data is distributed across disks, the data when uploaded to the storage account will be converged back to the directory structure specified in the dataset CSV file.</span></span>

#### <a name="how-many-of-the-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a><span data-ttu-id="ee53d-435">當複製進行時，將有多少輸入磁碟會平行擁有作用中 IO？</span><span class="sxs-lookup"><span data-stu-id="ee53d-435">How many of the input disks will have active IO in parallel, when copy is in progress?</span></span>

<span data-ttu-id="ee53d-436">工具會依據輸入檔案的大小，將資料分散到多個輸入磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-436">The tool distributes data across the input disks based on the size of the input files.</span></span> <span data-ttu-id="ee53d-437">也就是說，平行的作用中磁碟數完全取決於輸入資料的性質。</span><span class="sxs-lookup"><span data-stu-id="ee53d-437">That said, the number of active disks in parallel completely delends on the nature of the input data.</span></span> <span data-ttu-id="ee53d-438">根據輸入資料集中個別檔案的大小，一或多個磁碟可能會平行顯示作用中 IO。</span><span class="sxs-lookup"><span data-stu-id="ee53d-438">Depending on the size of individual files in the input dataset, one or more disks may show active IO in parallel.</span></span> <span data-ttu-id="ee53d-439">如需詳細資料，請參閱下一個問題。</span><span class="sxs-lookup"><span data-stu-id="ee53d-439">See next question for more details.</span></span>

#### <a name="how-does-the-tool-distribute-the-files-across-the-disks"></a><span data-ttu-id="ee53d-440">工具如何將檔案分散於多個磁碟？</span><span class="sxs-lookup"><span data-stu-id="ee53d-440">How does the tool distribute the files across the disks?</span></span>

<span data-ttu-id="ee53d-441">WAImportExport 工具會以批次方式讀取和寫入檔案，一個批次最多包含 100000 個檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-441">WAImportExport Tool reads and writes files batch by batch, one batch contains max of 100000 files.</span></span> <span data-ttu-id="ee53d-442">這表示最多可以平行寫入 100000 個檔案。</span><span class="sxs-lookup"><span data-stu-id="ee53d-442">This means that max 100000 files can be written parallel.</span></span> <span data-ttu-id="ee53d-443">如果將這 100000 個檔案分散到多個磁碟機，即會同時寫入到多個磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-443">Multiple disks are written to simultaneously if these 100000 files are distributed to multi drives.</span></span> <span data-ttu-id="ee53d-444">不過，工具要同時寫入到多個磁碟或單一磁碟，取決於批次的累計大小。</span><span class="sxs-lookup"><span data-stu-id="ee53d-444">However whether the tool writes to multiple disks simultaneously or a single disk depends on the cumulative size of the batch.</span></span> <span data-ttu-id="ee53d-445">例如，當檔案較小時，如果這 10,0000 個檔案可以全部容納於單一磁碟機，工具在此批次的處理期間將只會寫入一個磁碟。</span><span class="sxs-lookup"><span data-stu-id="ee53d-445">For instance, in case of smaller files, if all of 10,0000 files are able to fit in a single drive, tool will write to only one disk during the processing of this batch.</span></span>

### <a name="waimportexport-output"></a><span data-ttu-id="ee53d-446">WAImportExport 輸出</span><span class="sxs-lookup"><span data-stu-id="ee53d-446">WAImportExport output</span></span>

#### <a name="there-are-two-journal-files-which-one-should-i-upload-to-azure-portal"></a><span data-ttu-id="ee53d-447">有兩個日誌檔案，我應該將哪一個上傳至 Azure 入口網站？</span><span class="sxs-lookup"><span data-stu-id="ee53d-447">There are two journal files, which one should I upload to Azure portal?</span></span>

<span data-ttu-id="ee53d-448">**.xml** - 對於您使用 WAImportExport 工具準備的每個硬碟，此工具會建立名為 `<DriveID>.xml` 的單一日誌檔案，其中的磁碟機識別碼是與工具從磁碟讀取的磁碟機相關聯的序號。</span><span class="sxs-lookup"><span data-stu-id="ee53d-448">**.xml** - For each hard drive that you prepare with the WAImportExport tool, the tool will create a single journal file with name `<DriveID>.xml` where DriveID is the serial number associated to the drive that the tool reads from the disk.</span></span> <span data-ttu-id="ee53d-449">所有磁碟機都將需要日誌檔案，才能在 Azure 入口網站中建立匯入工作。</span><span class="sxs-lookup"><span data-stu-id="ee53d-449">You will need the journal files from all of your drives to create the import job in the Azure portal.</span></span> <span data-ttu-id="ee53d-450">如果工具中斷，此日誌檔案也可用來繼續磁碟機準備。</span><span class="sxs-lookup"><span data-stu-id="ee53d-450">This journal file can also be used to resume drive preparation if the tool is interrupted.</span></span>

<span data-ttu-id="ee53d-451">**.jrn** - 後置詞為 `.jrn` 的日誌檔案包含硬碟所有複製工作階段的狀態。</span><span class="sxs-lookup"><span data-stu-id="ee53d-451">**.jrn** - The journal file with suffix `.jrn` contains the status for all copy sessions for a hard drive.</span></span> <span data-ttu-id="ee53d-452">它也包含建立匯入工作所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="ee53d-452">It also contains the information needed to create the import job.</span></span> <span data-ttu-id="ee53d-453">執行 WAImportExport 工具時，永遠必須指定日誌檔案，以及複製工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="ee53d-453">You must always specify a journal file when running the WAImportExport tool, as well as a copy session ID.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee53d-454">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee53d-454">Next steps</span></span>

* [<span data-ttu-id="ee53d-455">設定 Azure 匯入/匯出工具</span><span class="sxs-lookup"><span data-stu-id="ee53d-455">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup.md)
* [<span data-ttu-id="ee53d-456">在匯入程序期間設定屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="ee53d-456">Setting properties and metadata during the import process</span></span>](storage-import-export-tool-setting-properties-metadata-import.md)
* [<span data-ttu-id="ee53d-457">針對匯入作業準備硬碟的簡單工作流程</span><span class="sxs-lookup"><span data-stu-id="ee53d-457">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [<span data-ttu-id="ee53d-458">常用命令快速參考</span><span class="sxs-lookup"><span data-stu-id="ee53d-458">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference.md) 
* [<span data-ttu-id="ee53d-459">利用複製記錄檔檢閱作業狀態</span><span class="sxs-lookup"><span data-stu-id="ee53d-459">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)
* [<span data-ttu-id="ee53d-460">修復匯入作業</span><span class="sxs-lookup"><span data-stu-id="ee53d-460">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)
* [<span data-ttu-id="ee53d-461">修復匯出作業</span><span class="sxs-lookup"><span data-stu-id="ee53d-461">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
* [<span data-ttu-id="ee53d-462">針對 Azure 匯入/匯出工具進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="ee53d-462">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
