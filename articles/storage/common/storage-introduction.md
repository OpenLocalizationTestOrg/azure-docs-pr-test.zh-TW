---
title: "aaaIntroduction tooAzure 儲存體 |Microsoft 文件"
description: "簡介 tooAzure 儲存體，Microsoft 的 hello 雲端中的資料存放區。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a><span data-ttu-id="e63b0-103">簡介 tooMicrosoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-103">Introduction tooMicrosoft Azure Storage</span></span>

<span data-ttu-id="e63b0-104">Microsoft Azure 儲存體是 Microsoft 管理的雲端服務，可提供高度可用、安全、持久、可擴充和備援的儲存體。</span><span class="sxs-lookup"><span data-stu-id="e63b0-104">Microsoft Azure Storage is a Microsoft-managed cloud service that provides storage that is highly available, secure, durable, scalable, and redundant.</span></span> <span data-ttu-id="e63b0-105">Microsoft 會為您進行維護和處理重大問題。</span><span class="sxs-lookup"><span data-stu-id="e63b0-105">Microsoft takes care of maintenance and handles critical problems for you.</span></span> 

<span data-ttu-id="e63b0-106">Azure 儲存體包含三項資料服務：Blob 儲存體、檔案儲存體和佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="e63b0-106">Azure Storage consists of three data services: Blob storage, File storage, and Queue storage.</span></span> <span data-ttu-id="e63b0-107">Blob 儲存體支援標準和進階儲存體，使用 hello 最快的效能可能只 Ssd 的進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="e63b0-107">Blob storage supports both standard and premium storage, with premium storage using only SSDs for hello fastest performance possible.</span></span> <span data-ttu-id="e63b0-108">另一個功能是很棒的存放裝置，可讓您 toostorage 大量的較低的成本很少存取的資料。</span><span class="sxs-lookup"><span data-stu-id="e63b0-108">Another feature is cool storage, allowing you toostorage large amounts of rarely accessed data for a lower cost.</span></span>

<span data-ttu-id="e63b0-109">在本文中，您會了解 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e63b0-109">In this article, you learn about hello following:</span></span>
* <span data-ttu-id="e63b0-110">hello Azure 儲存體服務</span><span class="sxs-lookup"><span data-stu-id="e63b0-110">hello Azure Storage services</span></span>
* <span data-ttu-id="e63b0-111">hello 類型的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e63b0-111">hello types of storage accounts</span></span>
* <span data-ttu-id="e63b0-112">存取您的 blob、佇列和檔案</span><span class="sxs-lookup"><span data-stu-id="e63b0-112">accessing your blobs, queues, and files</span></span>
* <span data-ttu-id="e63b0-113">加密</span><span class="sxs-lookup"><span data-stu-id="e63b0-113">encryption</span></span>
* <span data-ttu-id="e63b0-114">複寫</span><span class="sxs-lookup"><span data-stu-id="e63b0-114">replication</span></span> 
* <span data-ttu-id="e63b0-115">將資料傳入或傳出儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-115">transferring data into or out of storage</span></span>
* <span data-ttu-id="e63b0-116">hello 許多儲存體用戶端程式庫使用。</span><span class="sxs-lookup"><span data-stu-id="e63b0-116">hello many storage client libraries available.</span></span> 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a><span data-ttu-id="e63b0-117">介紹 hello Azure 儲存體服務</span><span class="sxs-lookup"><span data-stu-id="e63b0-117">Introducing hello Azure Storage services</span></span>

<span data-ttu-id="e63b0-118">toouse 任何 hello 服務提供 Azure 儲存體-Blob 儲存體、 檔案儲存體和佇列儲存體--您先建立儲存體帳戶，再從該儲存體帳戶中的特定服務的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="e63b0-118">toouse any of hello services provided by Azure Storage -- Blob storage, File storage, and Queue storage -- you first create a storage account, and then you can transfer data to/from a specific service in that storage account.</span></span> 

## <a name="blob-storage"></a><span data-ttu-id="e63b0-119">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-119">Blob storage</span></span>

<span data-ttu-id="e63b0-120">Blob 基本上類似您在電腦 (或平板電腦、行動裝置等) 上儲存的檔案。</span><span class="sxs-lookup"><span data-stu-id="e63b0-120">Blobs are basically files like those that you store on your computer (or tablet, mobile device, and so on).</span></span> <span data-ttu-id="e63b0-121">它們可以是圖片、Microsoft Excel 檔案、HTML 檔案、虛擬硬碟 (VHD)、巨量資料 (例如記錄、資料庫備份) - 幾乎涵蓋任何項目。</span><span class="sxs-lookup"><span data-stu-id="e63b0-121">They can be pictures, Microsoft Excel files, HTML files, virtual hard disks (VHDs), big data such as logs, database backups  -- pretty much anything.</span></span> <span data-ttu-id="e63b0-122">Blob 會儲存在容器中，也就是類似 toofolders。</span><span class="sxs-lookup"><span data-stu-id="e63b0-122">Blobs are stored in containers, which are similar toofolders.</span></span> 

<span data-ttu-id="e63b0-123">之後將檔案儲存在 Blob 儲存體，您可以存取從任何地方這些中使用 Url 的 hello world，hello REST 介面，或其中一個 hello Azure SDK 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="e63b0-123">After storing files in Blob storage, you can access them from anywhere in hello world using URLs, hello REST interface, or one of hello Azure SDK storage client libraries.</span></span> <span data-ttu-id="e63b0-124">儲存體用戶端程式庫提供多種語言，包括 Node.js、Java、PHP、Ruby、Python 和 .NET。</span><span class="sxs-lookup"><span data-stu-id="e63b0-124">Storage client libraries are available for multiple languages, including Node.js, Java, PHP, Ruby, Python, and .NET.</span></span> 

<span data-ttu-id="e63b0-125">Blob 有三種類型：區塊 Blob、附加 Blob 和分頁 Blob (用於 VHD 檔案)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-125">There are three types of blobs -- block blobs, append blobs, and page blobs (used for VHD files).</span></span>

* <span data-ttu-id="e63b0-126">區塊 blob 會使用的 toohold 一般檔案出 tooabout 4.7 TB。</span><span class="sxs-lookup"><span data-stu-id="e63b0-126">Block blobs are used toohold ordinary files up tooabout 4.7 TB.</span></span> 
* <span data-ttu-id="e63b0-127">頁面 blob 是使用的 toohold 向上 too8 TB 大小的隨機存取檔案。</span><span class="sxs-lookup"><span data-stu-id="e63b0-127">Page blobs are used toohold random access files up too8 TB in size.</span></span> <span data-ttu-id="e63b0-128">這些用來備份 Vm 的 hello VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="e63b0-128">These are used for hello VHD files that back VMs.</span></span>
* <span data-ttu-id="e63b0-129">附加 blob 的區塊，就像 hello 區塊 blob，組成，但會針對最佳化附加作業。</span><span class="sxs-lookup"><span data-stu-id="e63b0-129">Append blobs are made up of blocks like hello block blobs, but are optimized for append operations.</span></span> <span data-ttu-id="e63b0-130">這些用於等記錄資訊 toohello 相同 blob 的多個 Vm。</span><span class="sxs-lookup"><span data-stu-id="e63b0-130">These are used for things like logging information toohello same blob from multiple VMs.</span></span>

<span data-ttu-id="e63b0-131">對於網路條件約束而進行上傳或下載資料 tooBlob 儲存體上提出 hello 傳輸的資料集非常大，您可以寄送的硬碟機 tooMicrosoft tooimport 一組或匯出資料直接從 hello 資料中心。</span><span class="sxs-lookup"><span data-stu-id="e63b0-131">For very large datasets where network constraints make uploading or downloading data tooBlob storage over hello wire unrealistic, you can ship a set of hard drives tooMicrosoft tooimport or export data directly from hello data center.</span></span> <span data-ttu-id="e63b0-132">請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](../storage-import-export-service.md)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-132">See [Use hello Microsoft Azure Import/Export Service tooTransfer Data tooBlob Storage](../storage-import-export-service.md).</span></span>

## <a name="file-storage"></a><span data-ttu-id="e63b0-133">檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-133">File storage</span></span>

<span data-ttu-id="e63b0-134">hello Azure 檔案服務可讓您可以使用 hello 標準伺服器訊息區塊 (SMB) 通訊協定來存取的高可用性的網路檔案共用上的 tooset。</span><span class="sxs-lookup"><span data-stu-id="e63b0-134">hello Azure Files service enables you tooset up highly available network file shares that can be accessed by using hello standard Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="e63b0-135">Hello 表示多個 Vm 可以共用相同的檔案具有讀取和寫入權限。</span><span class="sxs-lookup"><span data-stu-id="e63b0-135">That means that multiple VMs can share hello same files with both read and write access.</span></span> <span data-ttu-id="e63b0-136">您也可以讀取 hello 檔案使用 hello REST 介面或 hello 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="e63b0-136">You can also read hello files using hello REST interface or hello storage client libraries.</span></span> 

<span data-ttu-id="e63b0-137">區分 Azure 檔案儲存體從公司檔案共用上的一件事是您可以從任何地方存取 hello 檔案中使用的 URL，指向 toohello 檔案，並且包含共用的存取簽章 (SAS) token 的 hello world。</span><span class="sxs-lookup"><span data-stu-id="e63b0-137">One thing that distinguishes Azure File storage from files on a corporate file share is that you can access hello files from anywhere in hello world using a URL that points toohello file and includes a shared access signature (SAS) token.</span></span> <span data-ttu-id="e63b0-138">您可以產生 SAS 權杖。它們允許特定存取 tooa 私人資產一段特定時間。</span><span class="sxs-lookup"><span data-stu-id="e63b0-138">You can generate SAS tokens; they allow specific access tooa private asset for a specific amount of time.</span></span> 

<span data-ttu-id="e63b0-139">檔案共用可以用於許多常見案例：</span><span class="sxs-lookup"><span data-stu-id="e63b0-139">File shares can be used for many common scenarios:</span></span> 

* <span data-ttu-id="e63b0-140">許多內部部署應用程式會使用檔案共用。</span><span class="sxs-lookup"><span data-stu-id="e63b0-140">Many on-premises applications use file shares.</span></span> <span data-ttu-id="e63b0-141">這項功能可讓您更輕鬆 toomigrate 共用資料 tooAzure 這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="e63b0-141">This feature makes it easier toomigrate those applications that share data tooAzure.</span></span> <span data-ttu-id="e63b0-142">如果您裝載 hello 檔案共用 toohello 相同磁碟機代號，hello 內部應用程式會使用，hello 屬於您存取 hello 檔案共用的應用程式應該使用最少，如果有的話，變更。</span><span class="sxs-lookup"><span data-stu-id="e63b0-142">If you mount hello file share toohello same drive letter that hello on-premises application uses, hello part of your application that accesses hello file share should work with minimal, if any, changes.</span></span>

* <span data-ttu-id="e63b0-143">組態檔可以儲存在檔案共用上並從多個 VM 進行存取。</span><span class="sxs-lookup"><span data-stu-id="e63b0-143">Configuration files can be stored on a file share and accessed from multiple VMs.</span></span> <span data-ttu-id="e63b0-144">工具和公用程式使用多個群組中的開發人員可以儲存在檔案共用，確保所有人都可以找到它們，和他們使用 hello 相同版本。</span><span class="sxs-lookup"><span data-stu-id="e63b0-144">Tools and utilities used by multiple developers in a group can be stored on a file share, ensuring that everybody can find them, and that they use hello same version.</span></span>

* <span data-ttu-id="e63b0-145">診斷記錄檔、 度量和損毀傾印是只有三個範例的資料可以寫入 tooa 檔案共用和處理或稍後分析。</span><span class="sxs-lookup"><span data-stu-id="e63b0-145">Diagnostic logs, metrics, and crash dumps are just three examples of data that can be written tooa file share and processed or analyzed later.</span></span>

<span data-ttu-id="e63b0-146">在這個階段，Active Directory 為基礎的驗證和存取控制清單 (Acl) 不支援，但會在未來的 hello 中一些時間。</span><span class="sxs-lookup"><span data-stu-id="e63b0-146">At this time, Active Directory-based authentication and access control lists (ACLs) are not supported, but they will be at some time in hello future.</span></span> <span data-ttu-id="e63b0-147">hello 儲存體帳戶認證是使用的 tooprovide 驗證存取 toohello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="e63b0-147">hello storage account credentials are used tooprovide authentication for access toohello file share.</span></span> <span data-ttu-id="e63b0-148">這表示具有 hello 共用裝載的任何人都會有完整讀取/寫入存取 toohello 共用。</span><span class="sxs-lookup"><span data-stu-id="e63b0-148">This means anybody with hello share mounted will have full read/write access toohello share.</span></span>

## <a name="queue-storage"></a><span data-ttu-id="e63b0-149">佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-149">Queue storage</span></span>

<span data-ttu-id="e63b0-150">hello Azure 佇列服務是使用的 toostore 並擷取訊息。</span><span class="sxs-lookup"><span data-stu-id="e63b0-150">hello Azure Queue service is used toostore and retrieve messages.</span></span> <span data-ttu-id="e63b0-151">佇列訊息可以是 too64 KB 的大小，up，佇列可以包含數百萬個訊息。</span><span class="sxs-lookup"><span data-stu-id="e63b0-151">Queue messages can be up too64 KB in size, and a queue can contain millions of messages.</span></span> <span data-ttu-id="e63b0-152">佇列是以非同步方式處理訊息 toobe 通常使用的 toostore 清單。</span><span class="sxs-lookup"><span data-stu-id="e63b0-152">Queues are generally used toostore lists of messages toobe processed asynchronously.</span></span> 

<span data-ttu-id="e63b0-153">例如，假設您想客戶 toobe 無法 tooupload 圖片，而且您想 toocreate 縮圖的每張圖片。</span><span class="sxs-lookup"><span data-stu-id="e63b0-153">For example, say you want your customers toobe able tooupload pictures, and you want toocreate thumbnails for each picture.</span></span> <span data-ttu-id="e63b0-154">您可以讓您上傳 hello 圖片時等候您 toocreate hello 縮圖的客戶。</span><span class="sxs-lookup"><span data-stu-id="e63b0-154">You could have your customer wait for you toocreate hello thumbnails while uploading hello pictures.</span></span> <span data-ttu-id="e63b0-155">另外也可以 toouse 佇列。</span><span class="sxs-lookup"><span data-stu-id="e63b0-155">An alternative would be toouse a queue.</span></span> <span data-ttu-id="e63b0-156">當 hello 客戶完成他的上傳時，寫入訊息 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="e63b0-156">When hello customer finishes his upload, write a message toohello queue.</span></span> <span data-ttu-id="e63b0-157">然後有 Azure 函式從 hello 佇列擷取 hello 訊息，並建立 hello 縮圖。</span><span class="sxs-lookup"><span data-stu-id="e63b0-157">Then have an Azure Function retrieve hello message from hello queue and create hello thumbnails.</span></span> <span data-ttu-id="e63b0-158">Hello 組件，這項處理可以調整個別提供您更多控制微調您的使用量時。</span><span class="sxs-lookup"><span data-stu-id="e63b0-158">Each of hello parts of this processing can be scaled separately, giving you more control when tuning it for your usage.</span></span>

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a><span data-ttu-id="e63b0-159">表格儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-159">Table storage</span></span>
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
<span data-ttu-id="e63b0-160">標準 Azure 表格儲存體現在屬於 Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="e63b0-160">Standard Azure Table Storage is now part of Cosmos DB.</span></span> <span data-ttu-id="e63b0-161">Azure 表格儲存體也有進階資料表，可提供輸送量最佳化的資料表、全域發佈，以及自動次要索引。</span><span class="sxs-lookup"><span data-stu-id="e63b0-161">Also available is Premium Tables for Azure Table storage, offering throughput-optimized tables, global distribution, and automatic secondary indexes.</span></span> <span data-ttu-id="e63b0-162">toolearn 詳細並再試一次出 hello 新 premium 體驗，請簽出[Azure Cosmos DB： 表格 API](https://aka.ms/premiumtables)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-162">toolearn more and try out hello new premium experience, please check out [Azure Cosmos DB: Table API](https://aka.ms/premiumtables).</span></span>

## <a name="disk-storage"></a><span data-ttu-id="e63b0-163">磁碟儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-163">Disk storage</span></span>

<span data-ttu-id="e63b0-164">hello Azure 儲存體團隊也擁有的磁碟，包括所有 hello managed 和 unmanaged 的磁碟功能可供虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e63b0-164">hello Azure Storage team also owns Disks, which includes all of hello managed and unmanaged disk capabilities used by virtual machines.</span></span> <span data-ttu-id="e63b0-165">如需有關這些功能的詳細資訊，請參閱 hello[計算服務文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-165">For more information about these features, please see hello [Compute Service documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>

## <a name="types-of-storage-accounts"></a><span data-ttu-id="e63b0-166">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="e63b0-166">Types of storage accounts</span></span> 

<span data-ttu-id="e63b0-167">下表顯示 hello 各種類型的儲存體帳戶，以及與每個可用的物件。</span><span class="sxs-lookup"><span data-stu-id="e63b0-167">This table shows hello various kinds of storage accounts and which objects can be used with each.</span></span>

|<span data-ttu-id="e63b0-168">**儲存體帳戶的類型**</span><span class="sxs-lookup"><span data-stu-id="e63b0-168">**Type of storage account**</span></span>|<span data-ttu-id="e63b0-169">**一般用途：標準**</span><span class="sxs-lookup"><span data-stu-id="e63b0-169">**General-purpose Standard**</span></span>|<span data-ttu-id="e63b0-170">**一般用途：進階**</span><span class="sxs-lookup"><span data-stu-id="e63b0-170">**General-purpose Premium**</span></span>|<span data-ttu-id="e63b0-171">**Blob 儲存體、經常性存取和非經常性存取層**</span><span class="sxs-lookup"><span data-stu-id="e63b0-171">**Blob storage, hot and cool access tiers**</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="e63b0-172">**支援的服務**</span><span class="sxs-lookup"><span data-stu-id="e63b0-172">**Services supported**</span></span>| <span data-ttu-id="e63b0-173">Blob、檔案、佇列服務</span><span class="sxs-lookup"><span data-stu-id="e63b0-173">Blob, File, Queue Services</span></span> | <span data-ttu-id="e63b0-174">Blob 服務</span><span class="sxs-lookup"><span data-stu-id="e63b0-174">Blob Service</span></span> | <span data-ttu-id="e63b0-175">Blob 服務</span><span class="sxs-lookup"><span data-stu-id="e63b0-175">Blob Service</span></span>|
|<span data-ttu-id="e63b0-176">**支援的 Blob 類型**</span><span class="sxs-lookup"><span data-stu-id="e63b0-176">**Types of blobs supported**</span></span>|<span data-ttu-id="e63b0-177">區塊 Blob、分頁 Blob 及附加 Blob</span><span class="sxs-lookup"><span data-stu-id="e63b0-177">Block blobs, page blobs, and append blobs</span></span> | <span data-ttu-id="e63b0-178">分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="e63b0-178">Page blobs</span></span> | <span data-ttu-id="e63b0-179">區塊 Blob 和附加 Blob</span><span class="sxs-lookup"><span data-stu-id="e63b0-179">Block blobs and append blobs</span></span>|

### <a name="general-purpose-storage-accounts"></a><span data-ttu-id="e63b0-180">一般用途的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e63b0-180">General-purpose storage accounts</span></span>

<span data-ttu-id="e63b0-181">一般用途的儲存體帳戶有兩種。</span><span class="sxs-lookup"><span data-stu-id="e63b0-181">There are two kinds of general-purpose storage accounts.</span></span> 

#### <a name="standard-storage"></a><span data-ttu-id="e63b0-182">標準儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-182">Standard storage</span></span> 

<span data-ttu-id="e63b0-183">hello 最常使用的儲存體帳戶是標準儲存體帳戶，可用於所有類型的資料。</span><span class="sxs-lookup"><span data-stu-id="e63b0-183">hello most widely used storage accounts are standard storage accounts, which can be used for all types of data.</span></span> <span data-ttu-id="e63b0-184">標準儲存體帳戶使用磁性媒體 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="e63b0-184">Standard storage accounts use magnetic media toostore data.</span></span>

#### <a name="premium-storage"></a><span data-ttu-id="e63b0-185">進階儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-185">Premium storage</span></span>

<span data-ttu-id="e63b0-186">進階儲存體可為分頁 blob 提供高效能儲存體，主要用於 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="e63b0-186">Premium storage provides high-performance storage for page blobs, which are primarily used for VHD files.</span></span> <span data-ttu-id="e63b0-187">進階儲存體帳戶使用 SSD toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="e63b0-187">Premium storage accounts use SSD toostore data.</span></span> <span data-ttu-id="e63b0-188">Microsoft 建議對所有 VM 使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="e63b0-188">Microsoft recommends using Premium Storage for all of your VMs.</span></span>

### <a name="blob-storage-accounts"></a><span data-ttu-id="e63b0-189">Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e63b0-189">Blob Storage accounts</span></span>

<span data-ttu-id="e63b0-190">專門儲存體帳戶用於 toostore 區塊 blob，而且附加 blob hello Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e63b0-190">hello Blob Storage account is a specialized storage account used toostore block blobs and append blobs.</span></span> <span data-ttu-id="e63b0-191">您無法將分頁 blob 儲存在這些帳戶中，因此無法儲存 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="e63b0-191">You can't store page blobs in these accounts, therefore you can't store VHD files.</span></span> <span data-ttu-id="e63b0-192">這些帳戶可讓您存取層 tooHot tooset 或 Cool;hello 層可以隨時變更。</span><span class="sxs-lookup"><span data-stu-id="e63b0-192">These accounts allow you tooset an access tier tooHot or Cool; hello tier can be changed at any time.</span></span> 

<span data-ttu-id="e63b0-193">hello 作用的存取層使用，針對經常存取的檔案-支付較高的成本，如存放裝置，但 hello 成本存取 hello blob 是低很多。</span><span class="sxs-lookup"><span data-stu-id="e63b0-193">hello hot access tier is used for files that are accessed frequently -- you pay a higher cost for storage, but hello cost of accessing hello blobs is much lower.</span></span> <span data-ttu-id="e63b0-194">對儲存在 hello 酷炫的存取層中的 blob，支付較高的成本，用於存取 hello blob 但 hello 儲存體的成本更低。</span><span class="sxs-lookup"><span data-stu-id="e63b0-194">For blobs stored in hello cool access tier, you pay a higher cost for accessing hello blobs, but hello cost of storage is much lower.</span></span>

## <a name="accessing-your-blobs-files-and-queues"></a><span data-ttu-id="e63b0-195">存取您的 blob、檔案和佇列</span><span class="sxs-lookup"><span data-stu-id="e63b0-195">Accessing your blobs, files, and queues</span></span>

<span data-ttu-id="e63b0-196">每個儲存體帳戶都有兩種驗證金鑰，任一種金鑰均可用於任何作業。</span><span class="sxs-lookup"><span data-stu-id="e63b0-196">Each storage account has two authentication keys, either of which can be used for any operation.</span></span> <span data-ttu-id="e63b0-197">有兩個索引鍵，因此您可以換 hello 偶爾金鑰 tooenhance 安全性。</span><span class="sxs-lookup"><span data-stu-id="e63b0-197">There are two keys so you can roll over hello keys occasionally tooenhance security.</span></span> <span data-ttu-id="e63b0-198">就非常重要，這些機碼保持安全狀態因為持有者，以及 hello 帳戶名稱，允許無限制的存取 tooall 資料 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="e63b0-198">It is critical that these keys be kept secure because their possession, along with hello account name, allows unlimited access tooall data in hello storage account.</span></span> 

<span data-ttu-id="e63b0-199">本節查看兩個方式 toosecure hello 儲存體帳戶，以及其資料。</span><span class="sxs-lookup"><span data-stu-id="e63b0-199">This section looks two ways toosecure hello storage account and its data.</span></span> <span data-ttu-id="e63b0-200">如需保護您資料的儲存體帳戶的詳細資訊，請參閱 hello [Azure 儲存體安全性指南 》](storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-200">For detailed information about securing your storage account and your data, see hello [Azure Storage security guide](storage-security-guide.md).</span></span>

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a><span data-ttu-id="e63b0-201">Toostorage 帳戶使用 Azure AD 保護的存取</span><span class="sxs-lookup"><span data-stu-id="e63b0-201">Securing access toostorage accounts using Azure AD</span></span>

<span data-ttu-id="e63b0-202">其中一種方式 toosecure 存取 tooyour 存放的資料是控制存取 toohello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e63b0-202">One way toosecure access tooyour storage data is by controlling access toohello storage account keys.</span></span> <span data-ttu-id="e63b0-203">使用資源管理員角色型存取控制 (RBAC)，您可以指派角色 toousers、 群組或應用程式。</span><span class="sxs-lookup"><span data-stu-id="e63b0-203">With Resource Manager Role-Based Access Control (RBAC), you can assign roles toousers, groups, or applications.</span></span> <span data-ttu-id="e63b0-204">這些角色會繫結 tooa 組特定的允許或不允許的動作。</span><span class="sxs-lookup"><span data-stu-id="e63b0-204">These roles are tied tooa specific set of actions that are allowed or disallowed.</span></span> <span data-ttu-id="e63b0-205">使用 RBAC toogrant 存取 tooa 儲存體帳戶只會處理該儲存體帳戶，例如變更 hello 存取層的 hello 管理作業。</span><span class="sxs-lookup"><span data-stu-id="e63b0-205">Using RBAC toogrant access tooa storage account only handles hello management operations for that storage account, such as changing hello access tier.</span></span> <span data-ttu-id="e63b0-206">您無法使用 RBAC toogrant 存取 toodata 物件與特定的容器或檔案共用。</span><span class="sxs-lookup"><span data-stu-id="e63b0-206">You can't use RBAC toogrant access toodata objects like a specific container or file share.</span></span> <span data-ttu-id="e63b0-207">不過，您可以使用 RBAC toogrant 存取 toohello 儲存體帳戶金鑰 」，接著可以使用的 tooread hello 資料物件。</span><span class="sxs-lookup"><span data-stu-id="e63b0-207">You can, however, use RBAC toogrant access toohello storage account keys, which can then be used tooread hello data objects.</span></span> 

### <a name="securing-access-using-shared-access-signatures"></a><span data-ttu-id="e63b0-208">使用共用存取簽章保護存取權</span><span class="sxs-lookup"><span data-stu-id="e63b0-208">Securing access using shared access signatures</span></span> 

<span data-ttu-id="e63b0-209">您可以使用共用的存取簽章和預存存取原則 toosecure 資料物件。</span><span class="sxs-lookup"><span data-stu-id="e63b0-209">You can use shared access signatures and stored access policies toosecure your data objects.</span></span> <span data-ttu-id="e63b0-210">共用的存取簽章 (SAS) 是字串，包含可能是安全性權杖附加 toohello URI toodelegate 存取 toospecific 儲存物件和 toospecify 條件約束，例如權限和存取 hello 日期/時間範圍，可讓您的資產。</span><span class="sxs-lookup"><span data-stu-id="e63b0-210">A shared access signature (SAS) is a string containing a security token that can be attached toohello URI for an asset that allows you toodelegate access toospecific storage objects and toospecify constraints such as permissions and hello date/time range of access.</span></span> <span data-ttu-id="e63b0-211">這項功能有廣泛的功能。</span><span class="sxs-lookup"><span data-stu-id="e63b0-211">This feature has extensive capabilities.</span></span> <span data-ttu-id="e63b0-212">如需詳細資訊，請參閱太[使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-212">For detailed information, refer too[Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="public-access-tooblobs"></a><span data-ttu-id="e63b0-213">公用存取 tooblobs</span><span class="sxs-lookup"><span data-stu-id="e63b0-213">Public access tooblobs</span></span>

<span data-ttu-id="e63b0-214">hello Blob 服務可讓您 tooprovide 公用存取 tooa 容器和其 blob 或特定的 blob。</span><span class="sxs-lookup"><span data-stu-id="e63b0-214">hello Blob Service allows you tooprovide public access tooa container and its blobs, or a specific blob.</span></span> <span data-ttu-id="e63b0-215">當您將容器或 Blob 指定為公用時，任何人都可以進行匿名讀取；不需要驗證。</span><span class="sxs-lookup"><span data-stu-id="e63b0-215">When you indicate that a container or blob is public, anyone can read it anonymously; no authentication is required.</span></span> <span data-ttu-id="e63b0-216">舉例來說，當您會想 toodo 這是當您有使用影像、 視訊或從 Blob 儲存體的文件的網站。</span><span class="sxs-lookup"><span data-stu-id="e63b0-216">An example of when you would want toodo this is when you have a website that is using images, video, or documents from Blob storage.</span></span> <span data-ttu-id="e63b0-217">如需詳細資訊，請參閱[管理匿名讀取權限 toocontainers 和 blob](../blobs/storage-manage-access-to-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e63b0-217">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md)</span></span> 

## <a name="encryption"></a><span data-ttu-id="e63b0-218">加密</span><span class="sxs-lookup"><span data-stu-id="e63b0-218">Encryption</span></span>

<span data-ttu-id="e63b0-219">有幾個基本類型的加密 hello 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="e63b0-219">There are a couple of basic kinds of encryption available for hello Storage services.</span></span> 

### <a name="encryption-at-rest"></a><span data-ttu-id="e63b0-220">待用加密</span><span class="sxs-lookup"><span data-stu-id="e63b0-220">Encryption at rest</span></span> 

<span data-ttu-id="e63b0-221">您可以在任一 hello 檔案服務 （預覽） 上啟用儲存體服務加密 (SSE) 或 hello Azure 儲存體帳戶的 Blob 服務。</span><span class="sxs-lookup"><span data-stu-id="e63b0-221">You can enable Storage Service Encryption (SSE) on either hello Files service (preview) or hello Blob service for an Azure storage account.</span></span> <span data-ttu-id="e63b0-222">如果啟用，就會加密寫入 toohello 特定服務的所有資料寫入之前。</span><span class="sxs-lookup"><span data-stu-id="e63b0-222">If enabled, all data written toohello specific service is encrypted before written.</span></span> <span data-ttu-id="e63b0-223">當您讀取 hello 資料時，會先解密，傳回之前。</span><span class="sxs-lookup"><span data-stu-id="e63b0-223">When you read hello data, it is decrypted before returned.</span></span> 

### <a name="client-side-encryption"></a><span data-ttu-id="e63b0-224">用戶端加密</span><span class="sxs-lookup"><span data-stu-id="e63b0-224">Client-side encryption</span></span>

<span data-ttu-id="e63b0-225">hello 儲存體用戶端程式庫有的方法可以呼叫 tooprogrammatically 再將它傳送嗨網路跨 hello 用戶端 tooAzure 從加密資料。</span><span class="sxs-lookup"><span data-stu-id="e63b0-225">hello storage client libraries have methods you can call tooprogrammatically encrypt data before sending it across hello wire from hello client tooAzure.</span></span> <span data-ttu-id="e63b0-226">它會以加密方式儲存，這表示待用時也會加密。</span><span class="sxs-lookup"><span data-stu-id="e63b0-226">It is stored encrypted, which means it also is encrypted at rest.</span></span> <span data-ttu-id="e63b0-227">讀取回 hello 資料時，會解密 hello 資訊在收到之後。</span><span class="sxs-lookup"><span data-stu-id="e63b0-227">When reading hello data back, you decrypt hello information after receiving it.</span></span> 

### <a name="encryption-in-transit-with-azure-file-shares"></a><span data-ttu-id="e63b0-228">透過 Azure 檔案共用進行傳輸時加密</span><span class="sxs-lookup"><span data-stu-id="e63b0-228">Encryption in transit with Azure File Shares</span></span>

<span data-ttu-id="e63b0-229">如需共用存取簽章的詳細資訊，請參閱 [使用共用存取簽章 (SAS)](../storage-dotnet-shared-access-signature-part-1.md) 。</span><span class="sxs-lookup"><span data-stu-id="e63b0-229">See [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) for more information on shared access signatures.</span></span> <span data-ttu-id="e63b0-230">請參閱[管理匿名讀取權限 toocontainers 和 blob](../blobs/storage-manage-access-to-resources.md)和[hello Azure 儲存體服務驗證](https://msdn.microsoft.com/library/azure/dd179428.aspx)如安全存取 tooyour 儲存體帳戶的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e63b0-230">See [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md) and [Authentication for hello Azure Storage Services](https://msdn.microsoft.com/library/azure/dd179428.aspx) for more information on secure access tooyour storage account.</span></span>

<span data-ttu-id="e63b0-231">如需有關如何保護您的儲存體帳戶和加密的詳細資訊，請參閱 hello [Azure 儲存體安全性指南 》](storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-231">For more details about securing your storage account and encryption, see hello [Azure Storage security guide](storage-security-guide.md).</span></span>

## <a name="replication"></a><span data-ttu-id="e63b0-232">複寫</span><span class="sxs-lookup"><span data-stu-id="e63b0-232">Replication</span></span>

<span data-ttu-id="e63b0-233">在您的資料是持久的順序 tooensure，Azure 儲存體具有 hello 能力 tookeep （和管理） 資料的多個複本。</span><span class="sxs-lookup"><span data-stu-id="e63b0-233">In order tooensure that your data is durable, Azure Storage has hello ability tookeep (and manage) multiple copies of your data.</span></span> <span data-ttu-id="e63b0-234">這稱為複寫，有時候稱為備援。</span><span class="sxs-lookup"><span data-stu-id="e63b0-234">This is called replication, or sometimes redundancy.</span></span> <span data-ttu-id="e63b0-235">當您設定儲存體帳戶時，您可選取複寫類型。</span><span class="sxs-lookup"><span data-stu-id="e63b0-235">When you set up your storage account, you select replication type.</span></span> <span data-ttu-id="e63b0-236">在大部分情況下，可以在 hello 儲存體帳戶設定之後修改此設定。</span><span class="sxs-lookup"><span data-stu-id="e63b0-236">In most cases, this setting can be modified after hello storage account is set up.</span></span> 

<span data-ttu-id="e63b0-237">所有儲存體帳戶都有**本機備援儲存體 (LRS)**。</span><span class="sxs-lookup"><span data-stu-id="e63b0-237">All storage accounts have **locally redundant storage (LRS)**.</span></span> <span data-ttu-id="e63b0-238">這表示您資料的三個複本都受 hello 資料中心內的 Azure 儲存體指定 hello 儲存體帳戶已設定時。</span><span class="sxs-lookup"><span data-stu-id="e63b0-238">This means three copies of your data are managed by Azure Storage in hello data center specified when hello storage account was set up.</span></span> <span data-ttu-id="e63b0-239">當變更都會認可的 tooone 複製、 hello 其他兩個複本會更新後再傳回成功。</span><span class="sxs-lookup"><span data-stu-id="e63b0-239">When changes are committed tooone copy, hello other two copies are updated before returning success.</span></span> <span data-ttu-id="e63b0-240">這表示 hello 三個複本都保持同步。此外，hello 三個複本位於不同的容錯網域和升級網域，這表示您的資料可用，即使保存您資料的儲存體節點失敗或更新時所建立的離線 toobe。</span><span class="sxs-lookup"><span data-stu-id="e63b0-240">This means hello three replicas are always in sync. Also, hello three copies reside in separate fault domains and upgrade domains, which means your data is available even if a storage node holding your data fails or is taken offline toobe updated.</span></span> 

<span data-ttu-id="e63b0-241">**本地備援儲存體 (LRS)**</span><span class="sxs-lookup"><span data-stu-id="e63b0-241">**Locally redundant storage (LRS)**</span></span>

<span data-ttu-id="e63b0-242">如上所述，使用 LRS，您在單一資料中心內有三個資料複本。</span><span class="sxs-lookup"><span data-stu-id="e63b0-242">As explained above, with LRS you have three copies of your data in a single datacenter.</span></span> <span data-ttu-id="e63b0-243">這個方法會處理 hello 問題的資料變成無法使用，如果儲存體節點失敗或被更新，離線 toobe，但不是 hello 變得無法使用整個資料中心的大小寫。</span><span class="sxs-lookup"><span data-stu-id="e63b0-243">This handles hello problem of data becoming unavailable if a storage node fails or is taken offline toobe updated, but not hello case of an entire datacenter becoming unavailable.</span></span>

<span data-ttu-id="e63b0-244">**區域備援儲存體 (ZRS)**</span><span class="sxs-lookup"><span data-stu-id="e63b0-244">**Zone redundant storage (ZRS)**</span></span>

<span data-ttu-id="e63b0-245">區域備援儲存體 (ZRS) 維護 hello 三個區域的資料複本，以及另一組的三份資料。</span><span class="sxs-lookup"><span data-stu-id="e63b0-245">Zone-redundant storage (ZRS) maintains hello three local copies of your data as well as another set of three copies of your data.</span></span> <span data-ttu-id="e63b0-246">hello 的三個複本的第二個集合會以非同步方式複寫跨越一或兩個區域內的資料中心。</span><span class="sxs-lookup"><span data-stu-id="e63b0-246">hello second set of three copies is replicated asynchronously across datacenters within one or two regions.</span></span> <span data-ttu-id="e63b0-247">請注意，ZRS 僅適用於一般用途的儲存體帳戶中的區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="e63b0-247">Note that ZRS is only available for block blobs in general-purpose storage accounts.</span></span> <span data-ttu-id="e63b0-248">此外，一旦您已建立儲存體帳戶，並選取 ZRS，您無法將它轉換 toouse tooany 其他類型的複寫，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="e63b0-248">Also, once you have created your storage account and selected ZRS, you cannot convert it toouse tooany other type of replication, or vice versa.</span></span>

<span data-ttu-id="e63b0-249">ZRS 帳戶可提供比 LRS 更高的持久性，但 ZRS 帳戶並沒有計量或記錄功能。</span><span class="sxs-lookup"><span data-stu-id="e63b0-249">ZRS accounts provide higher durability than LRS, but ZRS accounts do not have metrics or logging capability.</span></span> 

<span data-ttu-id="e63b0-250">**異地備援儲存體 (GRS)**</span><span class="sxs-lookup"><span data-stu-id="e63b0-250">**Geo-redundant storage (GRS)**</span></span>

<span data-ttu-id="e63b0-251">地理備援儲存體 (GRS) 維護 hello 三個區域的資料複本主要區域中加上另一組次要區域數百甚遠 hello 主要區域中資料的三個複本。</span><span class="sxs-lookup"><span data-stu-id="e63b0-251">Geo-redundant storage (GRS) maintains hello three local copies of your data in a primary region plus another set of three copies of your data in a secondary region hundreds of miles away from hello primary region.</span></span> <span data-ttu-id="e63b0-252">在 hello 事件中的 hello 主要區域故障，Azure 儲存體將容錯移轉 toohello 次要區域。</span><span class="sxs-lookup"><span data-stu-id="e63b0-252">In hello event of a failure at hello primary region, Azure Storage will fail over toohello secondary region.</span></span> 

<span data-ttu-id="e63b0-253">**讀取權限異地備援儲存體 (RA-GRS)**</span><span class="sxs-lookup"><span data-stu-id="e63b0-253">**Read-access geo-redundant storage (RA-GRS)**</span></span> 

<span data-ttu-id="e63b0-254">讀取權限的地理備援儲存體是與 GRS 完全相同，不同之處在於您 hello 次要位置中取得讀取權限 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="e63b0-254">Read-access geo-redundant storage is exactly like GRS except that you get read access toohello data in hello secondary location.</span></span> <span data-ttu-id="e63b0-255">如果 hello 主要資料中心變成暫時無法使用，您可以繼續 tooread hello 資料從 hello 次要位置。</span><span class="sxs-lookup"><span data-stu-id="e63b0-255">If hello primary data center becomes unavailable temporarily, you can continue tooread hello data from hello secondary location.</span></span> <span data-ttu-id="e63b0-256">這很有幫助。</span><span class="sxs-lookup"><span data-stu-id="e63b0-256">This can be very helpful.</span></span> <span data-ttu-id="e63b0-257">例如，您可能會變更為唯讀模式，並指出 toohello 次要複本的 web 應用程式允許某些存取，即使沒有更新。</span><span class="sxs-lookup"><span data-stu-id="e63b0-257">For example, you could have a web application that changes into read-only mode and points toohello secondary copy, allowing some access even though updates are not available.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e63b0-258">您可以變更您的資料複寫方式建立儲存體帳戶後，除非建立 hello 帳戶時，指定 ZRS。</span><span class="sxs-lookup"><span data-stu-id="e63b0-258">You can change how your data is replicated after your storage account has been created, unless you specified ZRS when you created hello account.</span></span> <span data-ttu-id="e63b0-259">不過請注意，您可能會造成的額外的單次資料傳輸成本如果您從 LRS tooGRS 或 RA-GRS 切換。</span><span class="sxs-lookup"><span data-stu-id="e63b0-259">However, note that you may incur an additional one-time data transfer cost if you switch from LRS tooGRS or RA-GRS.</span></span>
>

<span data-ttu-id="e63b0-260">如需有關複寫的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-260">For more information about replication, see [Azure Storage replication](storage-redundancy.md).</span></span>

<span data-ttu-id="e63b0-261">嚴重損壞修復資訊，請參閱[如果 Azure 儲存體中斷，就會發生何種 toodo](storage-disaster-recovery-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-261">For disaster recovery information, see [What toodo if an Azure Storage outage occurs](storage-disaster-recovery-guidance.md).</span></span>

<span data-ttu-id="e63b0-262">如需如何 tooleverage RA-GRS 儲存體 tooensure 高可用性，請參閱[設計高可用的應用程式使用 RA-GRS](storage-designing-ha-apps-with-ragrs.md)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-262">For an example of how tooleverage RA-GRS storage tooensure high availability, see [Designing Highly Available Applications using RA-GRS](storage-designing-ha-apps-with-ragrs.md).</span></span>

## <a name="transferring-data-tooand-from-azure-storage"></a><span data-ttu-id="e63b0-263">從 Azure 儲存體傳輸資料 tooand</span><span class="sxs-lookup"><span data-stu-id="e63b0-263">Transferring data tooand from Azure Storage</span></span>

<span data-ttu-id="e63b0-264">儲存體帳戶中或跨儲存體帳戶，您可以使用 hello AzCopy 命令列公用程式 toocopy blob 和檔案資料。</span><span class="sxs-lookup"><span data-stu-id="e63b0-264">You can use hello AzCopy command-line utility toocopy blob, and file data within your storage account or across storage accounts.</span></span> <span data-ttu-id="e63b0-265">Hello 下列其中一種文件的說明，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e63b0-265">See one of hello following articles for help:</span></span>

* [<span data-ttu-id="e63b0-266">使用適用於 Windows 的 AzCopy 傳輸資料</span><span class="sxs-lookup"><span data-stu-id="e63b0-266">Transfer data with AzCopy for Windows</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="e63b0-267">使用適用於 Linux 的 AzCopy 傳輸資料</span><span class="sxs-lookup"><span data-stu-id="e63b0-267">Transfer data with AzCopy for Linux</span></span>](storage-use-azcopy-linux.md)

<span data-ttu-id="e63b0-268">AzCopy 之上 hello [Azure 資料移動文件庫](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)，這是目前可供預覽。</span><span class="sxs-lookup"><span data-stu-id="e63b0-268">AzCopy is built on top of hello [Azure Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), which is currently available in preview.</span></span>

<span data-ttu-id="e63b0-269">hello Azure 匯入/匯出服務可使用的 tooimport 或匯出大量的 blob 資料 tooor 從儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e63b0-269">hello Azure Import/Export service can be used tooimport or export large amounts of blob data tooor from your storage account.</span></span> <span data-ttu-id="e63b0-270">您準備從 hello 硬碟 hello 資料郵件多個硬碟 tooan Azure 資料中心，將傳送的位置和傳送嗨硬碟回 tooyou。</span><span class="sxs-lookup"><span data-stu-id="e63b0-270">You prepare and mail multiple hard drives tooan Azure data center, where they will transfer hello data to/from hello hard drives and send hello hard drives back tooyou.</span></span> <span data-ttu-id="e63b0-271">如需 hello 匯入/匯出服務的詳細資訊，請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](../storage-import-export-service.md)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-271">For more information about hello Import/Export service, see [Use hello Microsoft Azure Import/Export Service tooTransfer Data tooBlob Storage](../storage-import-export-service.md).</span></span>

## <a name="pricing"></a><span data-ttu-id="e63b0-272">價格</span><span class="sxs-lookup"><span data-stu-id="e63b0-272">Pricing</span></span>

<span data-ttu-id="e63b0-273">如需 Azure 儲存體定價的詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage/blobs/)。</span><span class="sxs-lookup"><span data-stu-id="e63b0-273">For detailed information about pricing for Azure Storage, see hello [Pricing page](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>

## <a name="storage-apis-libraries-and-tools"></a><span data-ttu-id="e63b0-274">儲存體 API、程式庫和工具</span><span class="sxs-lookup"><span data-stu-id="e63b0-274">Storage APIs, libraries, and tools</span></span>
<span data-ttu-id="e63b0-275">任何可提出 HTTP/HTTPS 要求的語言皆可存取 Azure 儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="e63b0-275">Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests.</span></span> <span data-ttu-id="e63b0-276">另外，Azure 儲存體還提供了幾種熱門語言的程式設計程式庫。</span><span class="sxs-lookup"><span data-stu-id="e63b0-276">Additionally, Azure Storage offers programming libraries for several popular languages.</span></span> <span data-ttu-id="e63b0-277">這些程式庫可透過處理詳細資料 (例如同步和非同步叫用、進行批次作業、例外狀況管理、自動重試、運作方式等等) 來簡化使用 Azure 儲存體的許多項目。</span><span class="sxs-lookup"><span data-stu-id="e63b0-277">These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior, and so forth.</span></span> <span data-ttu-id="e63b0-278">程式庫目前可提供下列語言的 hello，而且平台，使用與其他人 hello 管線：</span><span class="sxs-lookup"><span data-stu-id="e63b0-278">Libraries are currently available for hello following languages and platforms, with others in hello pipeline:</span></span>

### <a name="azure-storage-data-services"></a><span data-ttu-id="e63b0-279">Azure 儲存體資料服務</span><span class="sxs-lookup"><span data-stu-id="e63b0-279">Azure Storage data services</span></span>
* [<span data-ttu-id="e63b0-280">儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="e63b0-280">Storage Services REST API</span></span>](/rest/api/storageservices/)
* [<span data-ttu-id="e63b0-281">適用於 .NET 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e63b0-281">Storage Client Library for .NET</span></span>](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [<span data-ttu-id="e63b0-282">Storage Client Library for C++</span><span class="sxs-lookup"><span data-stu-id="e63b0-282">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* [<span data-ttu-id="e63b0-283">適用於 Java/Android 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e63b0-283">Storage Client Library for Java/Android</span></span>](https://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="e63b0-284">適用於 Node.js 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e63b0-284">Storage Client Library for Node.js</span></span>](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [<span data-ttu-id="e63b0-285">適用於 PHP 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e63b0-285">Storage Client Library for PHP</span></span>](https://azure.microsoft.com/develop/php/)
* [<span data-ttu-id="e63b0-286">適用於 Python 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e63b0-286">Storage Client Library for Python</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="e63b0-287">適用於 Ruby 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e63b0-287">Storage Client Library for Ruby</span></span>](https://azure.microsoft.com/develop/ruby/)
* [<span data-ttu-id="e63b0-288">適用於 PowerShell 的儲存體 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e63b0-288">Storage Cmdlets for PowerShell</span></span>](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [<span data-ttu-id="e63b0-289">適用於 CLI 2.0 的儲存體命令</span><span class="sxs-lookup"><span data-stu-id="e63b0-289">Storage Commands for CLI 2.0</span></span>](/cli/azure/storage)

## <a name="next-steps"></a><span data-ttu-id="e63b0-290">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e63b0-290">Next steps</span></span>

* [<span data-ttu-id="e63b0-291">深入了解 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-291">Learn more about Blob storage</span></span>](../blobs/storage-blobs-introduction.md)
* [<span data-ttu-id="e63b0-292">深入了解檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-292">Learn more about File storage</span></span>](../storage-files-introduction.md)
* [<span data-ttu-id="e63b0-293">深入了解佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-293">Learn more about Queue storage</span></span>](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a><span data-ttu-id="e63b0-294">針對系統管理員</span><span class="sxs-lookup"><span data-stu-id="e63b0-294">For administrators</span></span>
* [<span data-ttu-id="e63b0-295">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-295">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="e63b0-296">使用 Azure CLI 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-296">Using Azure CLI with Azure Storage</span></span>](../storage-azure-cli.md)

### <a name="for-net-developers"></a><span data-ttu-id="e63b0-297">針對 .NET 開發人員</span><span class="sxs-lookup"><span data-stu-id="e63b0-297">For .NET developers</span></span>
* [<span data-ttu-id="e63b0-298">以 .NET 開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-298">Get started with Azure Blob storage using .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="e63b0-299">以 .NET 開始使用 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-299">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="e63b0-300">以 .NET 開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-300">Get started with Azure Queue storage using .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="e63b0-301">在 Windows 上開始使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-301">Get started with Azure File storage on Windows</span></span>](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a><span data-ttu-id="e63b0-302">針對 Java/Android 開發人員</span><span class="sxs-lookup"><span data-stu-id="e63b0-302">For Java/Android developers</span></span>
* [<span data-ttu-id="e63b0-303">如何從 Java 的 Blob 儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="e63b0-303">How toouse Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="e63b0-304">如何從 Java 資料表儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="e63b0-304">How toouse Table storage from Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="e63b0-305">如何從 Java 佇列儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="e63b0-305">How toouse Queue storage from Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="e63b0-306">如何從 Java 檔案儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="e63b0-306">How toouse File storage from Java</span></span>](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a><span data-ttu-id="e63b0-307">針對 Node.js 開發人員</span><span class="sxs-lookup"><span data-stu-id="e63b0-307">For Node.js developers</span></span>
* [<span data-ttu-id="e63b0-308">如何 toouse Node.js 從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-308">How toouse Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="e63b0-309">如何 toouse 從 Node.js 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-309">How toouse Table storage from Node.js</span></span>](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="e63b0-310">如何 toouse 從 Node.js 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-310">How toouse Queue storage from Node.js</span></span>](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a><span data-ttu-id="e63b0-311">針對 PHP 開發人員</span><span class="sxs-lookup"><span data-stu-id="e63b0-311">For PHP developers</span></span>
* [<span data-ttu-id="e63b0-312">如何 toouse 來自 PHP 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-312">How toouse Blob storage from PHP</span></span>](../blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="e63b0-313">如何 toouse 來自 PHP 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-313">How toouse Table storage from PHP</span></span>](../../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="e63b0-314">如何 toouse 來自 PHP 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-314">How toouse Queue storage from PHP</span></span>](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a><span data-ttu-id="e63b0-315">針對 Ruby 開發人員</span><span class="sxs-lookup"><span data-stu-id="e63b0-315">For Ruby developers</span></span>
* [<span data-ttu-id="e63b0-316">如何 toouse Ruby 從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-316">How toouse Blob storage from Ruby</span></span>](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [<span data-ttu-id="e63b0-317">如何 toouse Ruby 從資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-317">How toouse Table storage from Ruby</span></span>](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [<span data-ttu-id="e63b0-318">如何 toouse Ruby 從佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-318">How toouse Queue storage from Ruby</span></span>](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a><span data-ttu-id="e63b0-319">針對 Python 開發人員</span><span class="sxs-lookup"><span data-stu-id="e63b0-319">For Python developers</span></span>
* [<span data-ttu-id="e63b0-320">如何 toouse 來自 Python 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-320">How toouse Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="e63b0-321">如何 toouse 來自 Python 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-321">How toouse Table storage from Python</span></span>](../../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="e63b0-322">如何 toouse 來自 Python 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="e63b0-322">How toouse Queue storage from Python</span></span>](../storage-python-how-to-use-queue-storage.md)   
* <span data-ttu-id="e63b0-323">[如何 toouse 來自 Python 的檔案存放裝置](../storage-python-how-to-use-file-storage.md) 
--></span><span class="sxs-lookup"><span data-stu-id="e63b0-323">[How toouse File storage from Python](../storage-python-how-to-use-file-storage.md) 
--></span></span>