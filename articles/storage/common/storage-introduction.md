---
title: "Azure 儲存體簡介 | Microsoft Docs"
description: "Azure 儲存體 (Microsoft 的雲端資料儲存體) 簡介。"
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
ms.openlocfilehash: 163f35682a4fdaa971f715c7429153bfdcf6a584
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
<!-- this is the same version that is in the MVC branch -->
# <a name="introduction-to-microsoft-azure-storage"></a><span data-ttu-id="ea959-103">Microsoft Azure 儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="ea959-103">Introduction to Microsoft Azure Storage</span></span>

<span data-ttu-id="ea959-104">Microsoft Azure 儲存體是 Microsoft 管理的雲端服務，可提供高度可用、安全、持久、可擴充和備援的儲存體。</span><span class="sxs-lookup"><span data-stu-id="ea959-104">Microsoft Azure Storage is a Microsoft-managed cloud service that provides storage that is highly available, secure, durable, scalable, and redundant.</span></span> <span data-ttu-id="ea959-105">Microsoft 會為您進行維護和處理重大問題。</span><span class="sxs-lookup"><span data-stu-id="ea959-105">Microsoft takes care of maintenance and handles critical problems for you.</span></span> 

<span data-ttu-id="ea959-106">Azure 儲存體包含三項資料服務：Blob 儲存體、檔案儲存體和佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="ea959-106">Azure Storage consists of three data services: Blob storage, File storage, and Queue storage.</span></span> <span data-ttu-id="ea959-107">Blob 儲存體同時支援標準和進階儲存體，而進階儲存體僅使用 SSD 以取得可能最快的效能。</span><span class="sxs-lookup"><span data-stu-id="ea959-107">Blob storage supports both standard and premium storage, with premium storage using only SSDs for the fastest performance possible.</span></span> <span data-ttu-id="ea959-108">另一項功能是非經常性存取儲存體，可讓您以較低的成本儲存大量很少存取的資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-108">Another feature is cool storage, allowing you to storage large amounts of rarely accessed data for a lower cost.</span></span>

<span data-ttu-id="ea959-109">您會在本文中了解下列各項：</span><span class="sxs-lookup"><span data-stu-id="ea959-109">In this article, you learn about the following:</span></span>
* <span data-ttu-id="ea959-110">Azure 儲存體服務</span><span class="sxs-lookup"><span data-stu-id="ea959-110">the Azure Storage services</span></span>
* <span data-ttu-id="ea959-111">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="ea959-111">the types of storage accounts</span></span>
* <span data-ttu-id="ea959-112">存取您的 blob、佇列和檔案</span><span class="sxs-lookup"><span data-stu-id="ea959-112">accessing your blobs, queues, and files</span></span>
* <span data-ttu-id="ea959-113">加密</span><span class="sxs-lookup"><span data-stu-id="ea959-113">encryption</span></span>
* <span data-ttu-id="ea959-114">複寫</span><span class="sxs-lookup"><span data-stu-id="ea959-114">replication</span></span> 
* <span data-ttu-id="ea959-115">將資料傳入或傳出儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-115">transferring data into or out of storage</span></span>
* <span data-ttu-id="ea959-116">許多可用的儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="ea959-116">the many storage client libraries available.</span></span> 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
To get up and running with Azure Storage quickly, check out one of the following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-the-azure-storage-services"></a><span data-ttu-id="ea959-117">Azure 儲存體服務簡介</span><span class="sxs-lookup"><span data-stu-id="ea959-117">Introducing the Azure Storage services</span></span>

<span data-ttu-id="ea959-118">若要使用 Azure 儲存體所提供的任何服務 (Blob 儲存體、檔案儲存體和佇列儲存體)，請先建立儲存體帳戶，再從該儲存體帳戶中的特定服務傳入/出資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-118">To use any of the services provided by Azure Storage -- Blob storage, File storage, and Queue storage -- you first create a storage account, and then you can transfer data to/from a specific service in that storage account.</span></span> 

## <a name="blob-storage"></a><span data-ttu-id="ea959-119">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-119">Blob storage</span></span>

<span data-ttu-id="ea959-120">Blob 基本上類似您在電腦 (或平板電腦、行動裝置等) 上儲存的檔案。</span><span class="sxs-lookup"><span data-stu-id="ea959-120">Blobs are basically files like those that you store on your computer (or tablet, mobile device, and so on).</span></span> <span data-ttu-id="ea959-121">它們可以是圖片、Microsoft Excel 檔案、HTML 檔案、虛擬硬碟 (VHD)、巨量資料 (例如記錄、資料庫備份) - 幾乎涵蓋任何項目。</span><span class="sxs-lookup"><span data-stu-id="ea959-121">They can be pictures, Microsoft Excel files, HTML files, virtual hard disks (VHDs), big data such as logs, database backups  -- pretty much anything.</span></span> <span data-ttu-id="ea959-122">Blob 會儲存在容器 (類似於資料夾) 中。</span><span class="sxs-lookup"><span data-stu-id="ea959-122">Blobs are stored in containers, which are similar to folders.</span></span> 

<span data-ttu-id="ea959-123">在 Blob 儲存體中儲存檔案之後，您可以從世界各地使用 URL、REST 介面，或其中一個 Azure SDK 儲存體用戶端程式庫存取這些檔案。</span><span class="sxs-lookup"><span data-stu-id="ea959-123">After storing files in Blob storage, you can access them from anywhere in the world using URLs, the REST interface, or one of the Azure SDK storage client libraries.</span></span> <span data-ttu-id="ea959-124">儲存體用戶端程式庫提供多種語言，包括 Node.js、Java、PHP、Ruby、Python 和 .NET。</span><span class="sxs-lookup"><span data-stu-id="ea959-124">Storage client libraries are available for multiple languages, including Node.js, Java, PHP, Ruby, Python, and .NET.</span></span> 

<span data-ttu-id="ea959-125">Blob 有三種類型：區塊 Blob、附加 Blob 和分頁 Blob (用於 VHD 檔案)。</span><span class="sxs-lookup"><span data-stu-id="ea959-125">There are three types of blobs -- block blobs, append blobs, and page blobs (used for VHD files).</span></span>

* <span data-ttu-id="ea959-126">區塊 Blob 用來保存高達 4.7 TB 的一般檔案。</span><span class="sxs-lookup"><span data-stu-id="ea959-126">Block blobs are used to hold ordinary files up to about 4.7 TB.</span></span> 
* <span data-ttu-id="ea959-127">分頁 Blob 用來保存隨機存取檔案 (大小上限為 8 TB)。</span><span class="sxs-lookup"><span data-stu-id="ea959-127">Page blobs are used to hold random access files up to 8 TB in size.</span></span> <span data-ttu-id="ea959-128">這些用來備份 VM 的 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="ea959-128">These are used for the VHD files that back VMs.</span></span>
* <span data-ttu-id="ea959-129">附加 Blob 和區塊 Blob 相似，由區塊所組成，但已針對附加作業最佳化。</span><span class="sxs-lookup"><span data-stu-id="ea959-129">Append blobs are made up of blocks like the block blobs, but are optimized for append operations.</span></span> <span data-ttu-id="ea959-130">這些 Blob 用於將資訊記錄至多個 VM 中的相同 Blob 之類的事情。</span><span class="sxs-lookup"><span data-stu-id="ea959-130">These are used for things like logging information to the same blob from multiple VMs.</span></span>

<span data-ttu-id="ea959-131">若是超大型資料集，網路限制會使得透過線路上傳或下載資料至 Blob 儲存體變得不切實際，您可以將一組硬碟送至 Microsoft，以便直接從資料中心匯入或匯出資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-131">For very large datasets where network constraints make uploading or downloading data to Blob storage over the wire unrealistic, you can ship a set of hard drives to Microsoft to import or export data directly from the data center.</span></span> <span data-ttu-id="ea959-132">請參閱 [使用 Microsoft Azure 匯入/匯出服務將資料移轉至 Blob 儲存體](../storage-import-export-service.md)。</span><span class="sxs-lookup"><span data-stu-id="ea959-132">See [Use the Microsoft Azure Import/Export Service to Transfer Data to Blob Storage](../storage-import-export-service.md).</span></span>

## <a name="file-storage"></a><span data-ttu-id="ea959-133">檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-133">File storage</span></span>

<span data-ttu-id="ea959-134">Azure 檔案服務可讓您設定高可用性網路檔案共用，其可使用標準伺服器訊息區塊 (SMB) 通訊協定來存取。</span><span class="sxs-lookup"><span data-stu-id="ea959-134">The Azure Files service enables you to set up highly available network file shares that can be accessed by using the standard Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="ea959-135">這表示多個 VM 可以透過讀取和寫入權限共用相同的檔案。</span><span class="sxs-lookup"><span data-stu-id="ea959-135">That means that multiple VMs can share the same files with both read and write access.</span></span> <span data-ttu-id="ea959-136">您也可以使用 REST 介面或儲存體用戶端程式庫來讀取檔案。</span><span class="sxs-lookup"><span data-stu-id="ea959-136">You can also read the files using the REST interface or the storage client libraries.</span></span> 

<span data-ttu-id="ea959-137">區分 Azure 檔案儲存體與公司檔案共用上的檔案的方法之一，就是您可以使用指向檔案並包含共用存取簽章 (SAS) 權杖的 URL，從世界各地存取檔案。</span><span class="sxs-lookup"><span data-stu-id="ea959-137">One thing that distinguishes Azure File storage from files on a corporate file share is that you can access the files from anywhere in the world using a URL that points to the file and includes a shared access signature (SAS) token.</span></span> <span data-ttu-id="ea959-138">您可以產生 SAS 權杖；SAS 權杖可允許特定一段時間內私人資產的特定存取。</span><span class="sxs-lookup"><span data-stu-id="ea959-138">You can generate SAS tokens; they allow specific access to a private asset for a specific amount of time.</span></span> 

<span data-ttu-id="ea959-139">檔案共用可以用於許多常見案例：</span><span class="sxs-lookup"><span data-stu-id="ea959-139">File shares can be used for many common scenarios:</span></span> 

* <span data-ttu-id="ea959-140">許多內部部署應用程式會使用檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ea959-140">Many on-premises applications use file shares.</span></span> <span data-ttu-id="ea959-141">這項功能可讓您更輕鬆地將共用資料的應用程式移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="ea959-141">This feature makes it easier to migrate those applications that share data to Azure.</span></span> <span data-ttu-id="ea959-142">如果您將檔案共用掛接至內部部署應用程式使用的相同磁碟機代號，則存取檔案共用的應用程式部分應會在變動最小 (如果有的話) 的情況下運作。</span><span class="sxs-lookup"><span data-stu-id="ea959-142">If you mount the file share to the same drive letter that the on-premises application uses, the part of your application that accesses the file share should work with minimal, if any, changes.</span></span>

* <span data-ttu-id="ea959-143">組態檔可以儲存在檔案共用上並從多個 VM 進行存取。</span><span class="sxs-lookup"><span data-stu-id="ea959-143">Configuration files can be stored on a file share and accessed from multiple VMs.</span></span> <span data-ttu-id="ea959-144">由群組中多個開發人員所用的工具和公用程式可以儲存於檔案共用，確保所有人都可以找到它們並使用相同的版本。</span><span class="sxs-lookup"><span data-stu-id="ea959-144">Tools and utilities used by multiple developers in a group can be stored on a file share, ensuring that everybody can find them, and that they use the same version.</span></span>

* <span data-ttu-id="ea959-145">可以寫入檔案共用且稍後進行處理或分析的資料範例有三個：診斷記錄、計量和損毀傾印。</span><span class="sxs-lookup"><span data-stu-id="ea959-145">Diagnostic logs, metrics, and crash dumps are just three examples of data that can be written to a file share and processed or analyzed later.</span></span>

<span data-ttu-id="ea959-146">這個階段不支援以 Active Directory 為基礎的驗證和存取控制清單 (ACL)，但未來將會提供支援。</span><span class="sxs-lookup"><span data-stu-id="ea959-146">At this time, Active Directory-based authentication and access control lists (ACLs) are not supported, but they will be at some time in the future.</span></span> <span data-ttu-id="ea959-147">儲存體帳戶認證用來提供檔案共用存取權的驗證。</span><span class="sxs-lookup"><span data-stu-id="ea959-147">The storage account credentials are used to provide authentication for access to the file share.</span></span> <span data-ttu-id="ea959-148">這表示任何掛接共用的人員都具有共用的完整讀取/寫入權限。</span><span class="sxs-lookup"><span data-stu-id="ea959-148">This means anybody with the share mounted will have full read/write access to the share.</span></span>

## <a name="queue-storage"></a><span data-ttu-id="ea959-149">佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-149">Queue storage</span></span>

<span data-ttu-id="ea959-150">Azure 佇列服務用來儲存及擷取訊息。</span><span class="sxs-lookup"><span data-stu-id="ea959-150">The Azure Queue service is used to store and retrieve messages.</span></span> <span data-ttu-id="ea959-151">佇列訊息的大小上限為 64 KB，而一個佇列可以包含數百萬則訊息。</span><span class="sxs-lookup"><span data-stu-id="ea959-151">Queue messages can be up to 64 KB in size, and a queue can contain millions of messages.</span></span> <span data-ttu-id="ea959-152">佇列通常用來儲存要以非同步方式處理的訊息清單。</span><span class="sxs-lookup"><span data-stu-id="ea959-152">Queues are generally used to store lists of messages to be processed asynchronously.</span></span> 

<span data-ttu-id="ea959-153">例如，假設您希望客戶能夠上傳圖片，而且要建立每張圖片的縮圖。</span><span class="sxs-lookup"><span data-stu-id="ea959-153">For example, say you want your customers to be able to upload pictures, and you want to create thumbnails for each picture.</span></span> <span data-ttu-id="ea959-154">您可以讓客戶在上傳圖片時等候您建立縮圖。</span><span class="sxs-lookup"><span data-stu-id="ea959-154">You could have your customer wait for you to create the thumbnails while uploading the pictures.</span></span> <span data-ttu-id="ea959-155">另外，也可以使用佇列。</span><span class="sxs-lookup"><span data-stu-id="ea959-155">An alternative would be to use a queue.</span></span> <span data-ttu-id="ea959-156">當客戶完成上傳時，將訊息寫入佇列。</span><span class="sxs-lookup"><span data-stu-id="ea959-156">When the customer finishes his upload, write a message to the queue.</span></span> <span data-ttu-id="ea959-157">然後讓 Azure Function 從佇列擷取訊息並建立縮圖。</span><span class="sxs-lookup"><span data-stu-id="ea959-157">Then have an Azure Function retrieve the message from the queue and create the thumbnails.</span></span> <span data-ttu-id="ea959-158">這項處理的每個部分都可以個別調整，讓您在針對您的使用量進行微調時有更多控制權。</span><span class="sxs-lookup"><span data-stu-id="ea959-158">Each of the parts of this processing can be scaled separately, giving you more control when tuning it for your usage.</span></span>

<!-- this bookmark is used by other articles; you'll need to update them before this goes into production ROBIN-->
## <a name="table-storage"></a><span data-ttu-id="ea959-159">表格儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-159">Table storage</span></span>
<!-- add a link to the old table storage to this paragraph once it's moved -->
<span data-ttu-id="ea959-160">標準 Azure 表格儲存體現在屬於 Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="ea959-160">Standard Azure Table Storage is now part of Cosmos DB.</span></span> <span data-ttu-id="ea959-161">Azure 表格儲存體也有進階資料表，可提供輸送量最佳化的資料表、全域發佈，以及自動次要索引。</span><span class="sxs-lookup"><span data-stu-id="ea959-161">Also available is Premium Tables for Azure Table storage, offering throughput-optimized tables, global distribution, and automatic secondary indexes.</span></span> <span data-ttu-id="ea959-162">若要深入了解並試用新的進階體驗，請查看 [Azure Cosmos DB：資料表 API](https://aka.ms/premiumtables)。</span><span class="sxs-lookup"><span data-stu-id="ea959-162">To learn more and try out the new premium experience, please check out [Azure Cosmos DB: Table API](https://aka.ms/premiumtables).</span></span>

## <a name="disk-storage"></a><span data-ttu-id="ea959-163">磁碟儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-163">Disk storage</span></span>

<span data-ttu-id="ea959-164">Azure 儲存體小組也擁有磁碟，其中包含虛擬機器所使用的所有受控和非受控磁碟功能。</span><span class="sxs-lookup"><span data-stu-id="ea959-164">The Azure Storage team also owns Disks, which includes all of the managed and unmanaged disk capabilities used by virtual machines.</span></span> <span data-ttu-id="ea959-165">如需有關這些功能的詳細資訊，請參閱[計算服務文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。</span><span class="sxs-lookup"><span data-stu-id="ea959-165">For more information about these features, please see the [Compute Service documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>

## <a name="types-of-storage-accounts"></a><span data-ttu-id="ea959-166">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="ea959-166">Types of storage accounts</span></span> 

<span data-ttu-id="ea959-167">下表顯示各種儲存體帳戶，以及各自可以使用的物件。</span><span class="sxs-lookup"><span data-stu-id="ea959-167">This table shows the various kinds of storage accounts and which objects can be used with each.</span></span>

|<span data-ttu-id="ea959-168">**儲存體帳戶的類型**</span><span class="sxs-lookup"><span data-stu-id="ea959-168">**Type of storage account**</span></span>|<span data-ttu-id="ea959-169">**一般用途：標準**</span><span class="sxs-lookup"><span data-stu-id="ea959-169">**General-purpose Standard**</span></span>|<span data-ttu-id="ea959-170">**一般用途：進階**</span><span class="sxs-lookup"><span data-stu-id="ea959-170">**General-purpose Premium**</span></span>|<span data-ttu-id="ea959-171">**Blob 儲存體、經常性存取和非經常性存取層**</span><span class="sxs-lookup"><span data-stu-id="ea959-171">**Blob storage, hot and cool access tiers**</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="ea959-172">**支援的服務**</span><span class="sxs-lookup"><span data-stu-id="ea959-172">**Services supported**</span></span>| <span data-ttu-id="ea959-173">Blob、檔案、佇列服務</span><span class="sxs-lookup"><span data-stu-id="ea959-173">Blob, File, Queue Services</span></span> | <span data-ttu-id="ea959-174">Blob 服務</span><span class="sxs-lookup"><span data-stu-id="ea959-174">Blob Service</span></span> | <span data-ttu-id="ea959-175">Blob 服務</span><span class="sxs-lookup"><span data-stu-id="ea959-175">Blob Service</span></span>|
|<span data-ttu-id="ea959-176">**支援的 Blob 類型**</span><span class="sxs-lookup"><span data-stu-id="ea959-176">**Types of blobs supported**</span></span>|<span data-ttu-id="ea959-177">區塊 Blob、分頁 Blob 及附加 Blob</span><span class="sxs-lookup"><span data-stu-id="ea959-177">Block blobs, page blobs, and append blobs</span></span> | <span data-ttu-id="ea959-178">分頁 Blob</span><span class="sxs-lookup"><span data-stu-id="ea959-178">Page blobs</span></span> | <span data-ttu-id="ea959-179">區塊 Blob 和附加 Blob</span><span class="sxs-lookup"><span data-stu-id="ea959-179">Block blobs and append blobs</span></span>|

### <a name="general-purpose-storage-accounts"></a><span data-ttu-id="ea959-180">一般用途的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ea959-180">General-purpose storage accounts</span></span>

<span data-ttu-id="ea959-181">一般用途的儲存體帳戶有兩種。</span><span class="sxs-lookup"><span data-stu-id="ea959-181">There are two kinds of general-purpose storage accounts.</span></span> 

#### <a name="standard-storage"></a><span data-ttu-id="ea959-182">標準儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-182">Standard storage</span></span> 

<span data-ttu-id="ea959-183">標準儲存體帳戶是最廣泛使用的儲存體帳戶，可用於所有類型的資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-183">The most widely used storage accounts are standard storage accounts, which can be used for all types of data.</span></span> <span data-ttu-id="ea959-184">標準儲存體帳戶會使用磁性媒體來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-184">Standard storage accounts use magnetic media to store data.</span></span>

#### <a name="premium-storage"></a><span data-ttu-id="ea959-185">進階儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-185">Premium storage</span></span>

<span data-ttu-id="ea959-186">進階儲存體可為分頁 blob 提供高效能儲存體，主要用於 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="ea959-186">Premium storage provides high-performance storage for page blobs, which are primarily used for VHD files.</span></span> <span data-ttu-id="ea959-187">進階儲存體帳戶使用 SSD 來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-187">Premium storage accounts use SSD to store data.</span></span> <span data-ttu-id="ea959-188">Microsoft 建議對所有 VM 使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="ea959-188">Microsoft recommends using Premium Storage for all of your VMs.</span></span>

### <a name="blob-storage-accounts"></a><span data-ttu-id="ea959-189">Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ea959-189">Blob Storage accounts</span></span>

<span data-ttu-id="ea959-190">Blob 儲存體帳戶是專門的儲存體帳戶，用來儲存區塊 blob 和附加 blob。</span><span class="sxs-lookup"><span data-stu-id="ea959-190">The Blob Storage account is a specialized storage account used to store block blobs and append blobs.</span></span> <span data-ttu-id="ea959-191">您無法將分頁 blob 儲存在這些帳戶中，因此無法儲存 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="ea959-191">You can't store page blobs in these accounts, therefore you can't store VHD files.</span></span> <span data-ttu-id="ea959-192">這些帳戶允許您將存取層設定為經常性存取或非經常性存取；存取層可以隨時變更。</span><span class="sxs-lookup"><span data-stu-id="ea959-192">These accounts allow you to set an access tier to Hot or Cool; the tier can be changed at any time.</span></span> 

<span data-ttu-id="ea959-193">經常性存取層用於經常存取的檔案 - 您需支付較高的儲存體成本，但存取 blob 的成本低很多。</span><span class="sxs-lookup"><span data-stu-id="ea959-193">The hot access tier is used for files that are accessed frequently -- you pay a higher cost for storage, but the cost of accessing the blobs is much lower.</span></span> <span data-ttu-id="ea959-194">對於非經常性存取層中儲存的 blob，您需支付較高的 blob 存取成本，但儲存體的成本低很多。</span><span class="sxs-lookup"><span data-stu-id="ea959-194">For blobs stored in the cool access tier, you pay a higher cost for accessing the blobs, but the cost of storage is much lower.</span></span>

## <a name="accessing-your-blobs-files-and-queues"></a><span data-ttu-id="ea959-195">存取您的 blob、檔案和佇列</span><span class="sxs-lookup"><span data-stu-id="ea959-195">Accessing your blobs, files, and queues</span></span>

<span data-ttu-id="ea959-196">每個儲存體帳戶都有兩種驗證金鑰，任一種金鑰均可用於任何作業。</span><span class="sxs-lookup"><span data-stu-id="ea959-196">Each storage account has two authentication keys, either of which can be used for any operation.</span></span> <span data-ttu-id="ea959-197">金鑰有兩個，所以您可以偶爾變換金鑰以增強安全性。</span><span class="sxs-lookup"><span data-stu-id="ea959-197">There are two keys so you can roll over the keys occasionally to enhance security.</span></span> <span data-ttu-id="ea959-198">務必將金鑰放在安全的地方，因為其擁有權 (連同帳戶名稱) 允許無限制存取儲存體帳戶中的所有資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-198">It is critical that these keys be kept secure because their possession, along with the account name, allows unlimited access to all data in the storage account.</span></span> 

<span data-ttu-id="ea959-199">本節說明保護儲存體帳戶及其資料的兩種方式。</span><span class="sxs-lookup"><span data-stu-id="ea959-199">This section looks two ways to secure the storage account and its data.</span></span> <span data-ttu-id="ea959-200">如需保護儲存體帳戶和資料的詳細資訊，請參閱 [Azure 儲存體安全性指南](storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="ea959-200">For detailed information about securing your storage account and your data, see the [Azure Storage security guide](storage-security-guide.md).</span></span>

### <a name="securing-access-to-storage-accounts-using-azure-ad"></a><span data-ttu-id="ea959-201">使用 Azure AD 保護儲存體帳戶的存取權</span><span class="sxs-lookup"><span data-stu-id="ea959-201">Securing access to storage accounts using Azure AD</span></span>

<span data-ttu-id="ea959-202">控制儲存體帳戶金鑰的存取權，是保護儲存體資料存取的其中一種方式。</span><span class="sxs-lookup"><span data-stu-id="ea959-202">One way to secure access to your storage data is by controlling access to the storage account keys.</span></span> <span data-ttu-id="ea959-203">使用 Resource Manager 角色型存取控制 (RBAC)，您可以將角色指派給使用者、群組或應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea959-203">With Resource Manager Role-Based Access Control (RBAC), you can assign roles to users, groups, or applications.</span></span> <span data-ttu-id="ea959-204">這些角色會繫結至特定一組允許或不允許的動作。</span><span class="sxs-lookup"><span data-stu-id="ea959-204">These roles are tied to a specific set of actions that are allowed or disallowed.</span></span> <span data-ttu-id="ea959-205">使用 RBAC 授與儲存體帳戶存取權時，只會處理該儲存體帳戶的管理作業，例如變更存取層。</span><span class="sxs-lookup"><span data-stu-id="ea959-205">Using RBAC to grant access to a storage account only handles the management operations for that storage account, such as changing the access tier.</span></span> <span data-ttu-id="ea959-206">您無法使用 RBAC 來授與資料物件 (如特定容器或檔案共用) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="ea959-206">You can't use RBAC to grant access to data objects like a specific container or file share.</span></span> <span data-ttu-id="ea959-207">不過，您可以使用 RBAC 授與儲存體帳戶金鑰的存取權，而這些金鑰可用來讀取資料物件。</span><span class="sxs-lookup"><span data-stu-id="ea959-207">You can, however, use RBAC to grant access to the storage account keys, which can then be used to read the data objects.</span></span> 

### <a name="securing-access-using-shared-access-signatures"></a><span data-ttu-id="ea959-208">使用共用存取簽章保護存取權</span><span class="sxs-lookup"><span data-stu-id="ea959-208">Securing access using shared access signatures</span></span> 

<span data-ttu-id="ea959-209">您可以使用共用存取簽章和預存存取原則來保護您的資料物件。</span><span class="sxs-lookup"><span data-stu-id="ea959-209">You can use shared access signatures and stored access policies to secure your data objects.</span></span> <span data-ttu-id="ea959-210">共用存取簽章 (SAS) 是一個字串，包含可附加至資產 URI 的安全性權杖，可讓您委派特定儲存體物件的存取權，以及指定存取的權限和日期/時間範圍之類的限制。</span><span class="sxs-lookup"><span data-stu-id="ea959-210">A shared access signature (SAS) is a string containing a security token that can be attached to the URI for an asset that allows you to delegate access to specific storage objects and to specify constraints such as permissions and the date/time range of access.</span></span> <span data-ttu-id="ea959-211">這項功能有廣泛的功能。</span><span class="sxs-lookup"><span data-stu-id="ea959-211">This feature has extensive capabilities.</span></span> <span data-ttu-id="ea959-212">如需詳細資訊，請參閱[使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="ea959-212">For detailed information, refer to [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="public-access-to-blobs"></a><span data-ttu-id="ea959-213">公開存取 Blob</span><span class="sxs-lookup"><span data-stu-id="ea959-213">Public access to blobs</span></span>

<span data-ttu-id="ea959-214">Blob 服務可讓您提供容器與其 Blob 或特定 Blob 的公開存取權。</span><span class="sxs-lookup"><span data-stu-id="ea959-214">The Blob Service allows you to provide public access to a container and its blobs, or a specific blob.</span></span> <span data-ttu-id="ea959-215">當您將容器或 Blob 指定為公用時，任何人都可以進行匿名讀取；不需要驗證。</span><span class="sxs-lookup"><span data-stu-id="ea959-215">When you indicate that a container or blob is public, anyone can read it anonymously; no authentication is required.</span></span> <span data-ttu-id="ea959-216">例如，當您有網站使用 Blob 儲存體中的影像、影片或文件時，您會想要執行此動作。</span><span class="sxs-lookup"><span data-stu-id="ea959-216">An example of when you would want to do this is when you have a website that is using images, video, or documents from Blob storage.</span></span> <span data-ttu-id="ea959-217">如需詳細資訊，請參閱[管理對容器與 Blob 的匿名讀取權限](../blobs/storage-manage-access-to-resources.md)</span><span class="sxs-lookup"><span data-stu-id="ea959-217">For more information, see [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md)</span></span> 

## <a name="encryption"></a><span data-ttu-id="ea959-218">加密</span><span class="sxs-lookup"><span data-stu-id="ea959-218">Encryption</span></span>

<span data-ttu-id="ea959-219">有一些基本加密類型可用於儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="ea959-219">There are a couple of basic kinds of encryption available for the Storage services.</span></span> 

### <a name="encryption-at-rest"></a><span data-ttu-id="ea959-220">待用加密</span><span class="sxs-lookup"><span data-stu-id="ea959-220">Encryption at rest</span></span> 

<span data-ttu-id="ea959-221">您可以在 Azure 儲存體帳戶的檔案服務 (預覽) 或 Blob 服務上啟用儲存體服務加密 (SSE)。</span><span class="sxs-lookup"><span data-stu-id="ea959-221">You can enable Storage Service Encryption (SSE) on either the Files service (preview) or the Blob service for an Azure storage account.</span></span> <span data-ttu-id="ea959-222">若已啟用，寫入特定服務的所有資料會在寫入之前加密。</span><span class="sxs-lookup"><span data-stu-id="ea959-222">If enabled, all data written to the specific service is encrypted before written.</span></span> <span data-ttu-id="ea959-223">當您讀取資料時，資料會在傳回之前解密。</span><span class="sxs-lookup"><span data-stu-id="ea959-223">When you read the data, it is decrypted before returned.</span></span> 

### <a name="client-side-encryption"></a><span data-ttu-id="ea959-224">用戶端加密</span><span class="sxs-lookup"><span data-stu-id="ea959-224">Client-side encryption</span></span>

<span data-ttu-id="ea959-225">儲存體用戶端程式庫具有您可以呼叫的方法，在透過網路將資料從用戶端傳送到 Azure 之前，可以程式設計方式將資料加密。</span><span class="sxs-lookup"><span data-stu-id="ea959-225">The storage client libraries have methods you can call to programmatically encrypt data before sending it across the wire from the client to Azure.</span></span> <span data-ttu-id="ea959-226">它會以加密方式儲存，這表示待用時也會加密。</span><span class="sxs-lookup"><span data-stu-id="ea959-226">It is stored encrypted, which means it also is encrypted at rest.</span></span> <span data-ttu-id="ea959-227">讀回資料時，您會在接收資訊之後加以解密。</span><span class="sxs-lookup"><span data-stu-id="ea959-227">When reading the data back, you decrypt the information after receiving it.</span></span> 

### <a name="encryption-in-transit-with-azure-file-shares"></a><span data-ttu-id="ea959-228">透過 Azure 檔案共用進行傳輸時加密</span><span class="sxs-lookup"><span data-stu-id="ea959-228">Encryption in transit with Azure File Shares</span></span>

<span data-ttu-id="ea959-229">如需共用存取簽章的詳細資訊，請參閱 [使用共用存取簽章 (SAS)](../storage-dotnet-shared-access-signature-part-1.md) 。</span><span class="sxs-lookup"><span data-stu-id="ea959-229">See [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) for more information on shared access signatures.</span></span> <span data-ttu-id="ea959-230">如需安全存取儲存體帳戶的詳細資訊，請參閱[管理對容器與 Blob 的匿名讀取權限](../blobs/storage-manage-access-to-resources.md)和 [Azure 儲存體服務的驗證](https://msdn.microsoft.com/library/azure/dd179428.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ea959-230">See [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md) and [Authentication for the Azure Storage Services](https://msdn.microsoft.com/library/azure/dd179428.aspx) for more information on secure access to your storage account.</span></span>

<span data-ttu-id="ea959-231">如需保護儲存體帳戶和加密的詳細資訊，請參閱 [Azure 儲存體安全性指南](storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="ea959-231">For more details about securing your storage account and encryption, see the [Azure Storage security guide](storage-security-guide.md).</span></span>

## <a name="replication"></a><span data-ttu-id="ea959-232">複寫</span><span class="sxs-lookup"><span data-stu-id="ea959-232">Replication</span></span>

<span data-ttu-id="ea959-233">為了確保您資料的持久性，Azure 儲存體能夠保持 (及管理) 多個資料複本。</span><span class="sxs-lookup"><span data-stu-id="ea959-233">In order to ensure that your data is durable, Azure Storage has the ability to keep (and manage) multiple copies of your data.</span></span> <span data-ttu-id="ea959-234">這稱為複寫，有時候稱為備援。</span><span class="sxs-lookup"><span data-stu-id="ea959-234">This is called replication, or sometimes redundancy.</span></span> <span data-ttu-id="ea959-235">當您設定儲存體帳戶時，您可選取複寫類型。</span><span class="sxs-lookup"><span data-stu-id="ea959-235">When you set up your storage account, you select replication type.</span></span> <span data-ttu-id="ea959-236">在大部分情況下，在設定儲存體帳戶之後可以修改此設定。</span><span class="sxs-lookup"><span data-stu-id="ea959-236">In most cases, this setting can be modified after the storage account is set up.</span></span> 

<span data-ttu-id="ea959-237">所有儲存體帳戶都有**本機備援儲存體 (LRS)**。</span><span class="sxs-lookup"><span data-stu-id="ea959-237">All storage accounts have **locally redundant storage (LRS)**.</span></span> <span data-ttu-id="ea959-238">這表示 Azure 儲存體會在設定儲存體帳戶時指定的資料中心管理三個資料複本。</span><span class="sxs-lookup"><span data-stu-id="ea959-238">This means three copies of your data are managed by Azure Storage in the data center specified when the storage account was set up.</span></span> <span data-ttu-id="ea959-239">將變更認可至一個複本時，系統會在傳回成功前更新其他兩個複本。</span><span class="sxs-lookup"><span data-stu-id="ea959-239">When changes are committed to one copy, the other two copies are updated before returning success.</span></span> <span data-ttu-id="ea959-240">這表示三個複本一直都保持同步。此外，這三個複本位於不同的容錯網域和升級網域中，這表示即使保留資料的儲存體節點失敗或已離線進行更新，仍可使用資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-240">This means the three replicas are always in sync. Also, the three copies reside in separate fault domains and upgrade domains, which means your data is available even if a storage node holding your data fails or is taken offline to be updated.</span></span> 

<span data-ttu-id="ea959-241">**本地備援儲存體 (LRS)**</span><span class="sxs-lookup"><span data-stu-id="ea959-241">**Locally redundant storage (LRS)**</span></span>

<span data-ttu-id="ea959-242">如上所述，使用 LRS，您在單一資料中心內有三個資料複本。</span><span class="sxs-lookup"><span data-stu-id="ea959-242">As explained above, with LRS you have three copies of your data in a single datacenter.</span></span> <span data-ttu-id="ea959-243">如果儲存體節點失敗或已離線進行更新，這會處理資料變得無法使用的問題，但不是整個資料中心變得無法使用的情況。</span><span class="sxs-lookup"><span data-stu-id="ea959-243">This handles the problem of data becoming unavailable if a storage node fails or is taken offline to be updated, but not the case of an entire datacenter becoming unavailable.</span></span>

<span data-ttu-id="ea959-244">**區域備援儲存體 (ZRS)**</span><span class="sxs-lookup"><span data-stu-id="ea959-244">**Zone redundant storage (ZRS)**</span></span>

<span data-ttu-id="ea959-245">區域備援儲存體 (ZRS) 會維護三個本機資料複本，以及另一組的三個資料複本。</span><span class="sxs-lookup"><span data-stu-id="ea959-245">Zone-redundant storage (ZRS) maintains the three local copies of your data as well as another set of three copies of your data.</span></span> <span data-ttu-id="ea959-246">第二組的三個複本會以非同步方式、跨一或兩個區域內的資料中心複寫。</span><span class="sxs-lookup"><span data-stu-id="ea959-246">The second set of three copies is replicated asynchronously across datacenters within one or two regions.</span></span> <span data-ttu-id="ea959-247">請注意，ZRS 僅適用於一般用途的儲存體帳戶中的區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="ea959-247">Note that ZRS is only available for block blobs in general-purpose storage accounts.</span></span> <span data-ttu-id="ea959-248">此外，建立儲存體帳戶並選取 ZRS 後，就無法轉換為採用任何其他類型的複寫，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="ea959-248">Also, once you have created your storage account and selected ZRS, you cannot convert it to use to any other type of replication, or vice versa.</span></span>

<span data-ttu-id="ea959-249">ZRS 帳戶可提供比 LRS 更高的持久性，但 ZRS 帳戶並沒有計量或記錄功能。</span><span class="sxs-lookup"><span data-stu-id="ea959-249">ZRS accounts provide higher durability than LRS, but ZRS accounts do not have metrics or logging capability.</span></span> 

<span data-ttu-id="ea959-250">**異地備援儲存體 (GRS)**</span><span class="sxs-lookup"><span data-stu-id="ea959-250">**Geo-redundant storage (GRS)**</span></span>

<span data-ttu-id="ea959-251">異地備援儲存體 (GRS) 會在主要區域中維護三個本機資料複本，加上在距離主要區域數百哩的次要區域中維護另一組的三個資料複本。</span><span class="sxs-lookup"><span data-stu-id="ea959-251">Geo-redundant storage (GRS) maintains the three local copies of your data in a primary region plus another set of three copies of your data in a secondary region hundreds of miles away from the primary region.</span></span> <span data-ttu-id="ea959-252">在主要區域發生問題時，Azure 儲存體將會容錯移轉至次要區域。</span><span class="sxs-lookup"><span data-stu-id="ea959-252">In the event of a failure at the primary region, Azure Storage will fail over to the secondary region.</span></span> 

<span data-ttu-id="ea959-253">**讀取權限異地備援儲存體 (RA-GRS)**</span><span class="sxs-lookup"><span data-stu-id="ea959-253">**Read-access geo-redundant storage (RA-GRS)**</span></span> 

<span data-ttu-id="ea959-254">除了您取得次要位置中資料的讀取權限以外，讀取權限的異地備援儲存體與 GRS 完全相同。</span><span class="sxs-lookup"><span data-stu-id="ea959-254">Read-access geo-redundant storage is exactly like GRS except that you get read access to the data in the secondary location.</span></span> <span data-ttu-id="ea959-255">如果主要資料中心暫時變得無法使用，您可以繼續從次要位置讀取資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-255">If the primary data center becomes unavailable temporarily, you can continue to read the data from the secondary location.</span></span> <span data-ttu-id="ea959-256">這很有幫助。</span><span class="sxs-lookup"><span data-stu-id="ea959-256">This can be very helpful.</span></span> <span data-ttu-id="ea959-257">例如，您可能有變更為唯讀模式並指向次要複本的 Web 應用程式，允許即使無法取得更新也可進行某些存取。</span><span class="sxs-lookup"><span data-stu-id="ea959-257">For example, you could have a web application that changes into read-only mode and points to the secondary copy, allowing some access even though updates are not available.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ea959-258">除非您建立帳戶時指定了 ZRS，否則就可以在建立儲存體帳戶之後，變更資料的複寫方式。</span><span class="sxs-lookup"><span data-stu-id="ea959-258">You can change how your data is replicated after your storage account has been created, unless you specified ZRS when you created the account.</span></span> <span data-ttu-id="ea959-259">不過請注意，從 LRS 切換到 GRS 或 RA-GRS 時，可能必須支付額外的單次資料傳輸成本。</span><span class="sxs-lookup"><span data-stu-id="ea959-259">However, note that you may incur an additional one-time data transfer cost if you switch from LRS to GRS or RA-GRS.</span></span>
>

<span data-ttu-id="ea959-260">如需有關複寫的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="ea959-260">For more information about replication, see [Azure Storage replication](storage-redundancy.md).</span></span>

<span data-ttu-id="ea959-261">如需災害復原資訊，請參閱[如果 Azure 儲存體發生中斷怎麼辦](storage-disaster-recovery-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="ea959-261">For disaster recovery information, see [What to do if an Azure Storage outage occurs](storage-disaster-recovery-guidance.md).</span></span>

<span data-ttu-id="ea959-262">如需有關如何利用 RA-GRS 儲存體來確保高可用性的範例，請參閱[使用 RA-GRS 設計高可用性應用程式](storage-designing-ha-apps-with-ragrs.md)。</span><span class="sxs-lookup"><span data-stu-id="ea959-262">For an example of how to leverage RA-GRS storage to ensure high availability, see [Designing Highly Available Applications using RA-GRS](storage-designing-ha-apps-with-ragrs.md).</span></span>

## <a name="transferring-data-to-and-from-azure-storage"></a><span data-ttu-id="ea959-263">從 Azure 儲存體來回傳輸資料</span><span class="sxs-lookup"><span data-stu-id="ea959-263">Transferring data to and from Azure Storage</span></span>

<span data-ttu-id="ea959-264">您可以使用 AzCopy 命令列公用程式，在儲存體帳戶內或跨儲存體帳戶複製 Blob 和檔案資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-264">You can use the AzCopy command-line utility to copy blob, and file data within your storage account or across storage accounts.</span></span> <span data-ttu-id="ea959-265">請參閱下列其中一篇文章中的說明：</span><span class="sxs-lookup"><span data-stu-id="ea959-265">See one of the following articles for help:</span></span>

* [<span data-ttu-id="ea959-266">使用適用於 Windows 的 AzCopy 傳輸資料</span><span class="sxs-lookup"><span data-stu-id="ea959-266">Transfer data with AzCopy for Windows</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="ea959-267">使用適用於 Linux 的 AzCopy 傳輸資料</span><span class="sxs-lookup"><span data-stu-id="ea959-267">Transfer data with AzCopy for Linux</span></span>](storage-use-azcopy-linux.md)

<span data-ttu-id="ea959-268">AzCopy 建置於 [Azure 資料移動程式庫](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)之上，其目前可供預覽。</span><span class="sxs-lookup"><span data-stu-id="ea959-268">AzCopy is built on top of the [Azure Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), which is currently available in preview.</span></span>

<span data-ttu-id="ea959-269">Azure 匯入/匯出服務可用於從儲存體帳戶匯入或匯出大量 blob 資料。</span><span class="sxs-lookup"><span data-stu-id="ea959-269">The Azure Import/Export service can be used to import or export large amounts of blob data to or from your storage account.</span></span> <span data-ttu-id="ea959-270">您可準備多個硬碟並將其郵寄至 Azure 資料中心，這些硬碟會在其中從硬碟機傳入/傳出資料並將硬碟機傳送給您。</span><span class="sxs-lookup"><span data-stu-id="ea959-270">You prepare and mail multiple hard drives to an Azure data center, where they will transfer the data to/from the hard drives and send the hard drives back to you.</span></span> <span data-ttu-id="ea959-271">如需匯入/匯出服務的詳細資訊，請參閱 [使用 Microsoft Azure 匯入/匯出服務將資料傳輸至 Blob 儲存體](../storage-import-export-service.md)。</span><span class="sxs-lookup"><span data-stu-id="ea959-271">For more information about the Import/Export service, see [Use the Microsoft Azure Import/Export Service to Transfer Data to Blob Storage](../storage-import-export-service.md).</span></span>

## <a name="pricing"></a><span data-ttu-id="ea959-272">價格</span><span class="sxs-lookup"><span data-stu-id="ea959-272">Pricing</span></span>

<span data-ttu-id="ea959-273">如需 Azure 儲存體價格的詳細資訊，請參閱[價格頁面](https://azure.microsoft.com/pricing/details/storage/blobs/)。</span><span class="sxs-lookup"><span data-stu-id="ea959-273">For detailed information about pricing for Azure Storage, see the [Pricing page](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>

## <a name="storage-apis-libraries-and-tools"></a><span data-ttu-id="ea959-274">儲存體 API、程式庫和工具</span><span class="sxs-lookup"><span data-stu-id="ea959-274">Storage APIs, libraries, and tools</span></span>
<span data-ttu-id="ea959-275">任何可提出 HTTP/HTTPS 要求的語言皆可存取 Azure 儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="ea959-275">Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests.</span></span> <span data-ttu-id="ea959-276">另外，Azure 儲存體還提供了幾種熱門語言的程式設計程式庫。</span><span class="sxs-lookup"><span data-stu-id="ea959-276">Additionally, Azure Storage offers programming libraries for several popular languages.</span></span> <span data-ttu-id="ea959-277">這些程式庫可透過處理詳細資料 (例如同步和非同步叫用、進行批次作業、例外狀況管理、自動重試、運作方式等等) 來簡化使用 Azure 儲存體的許多項目。</span><span class="sxs-lookup"><span data-stu-id="ea959-277">These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior, and so forth.</span></span> <span data-ttu-id="ea959-278">程式庫目前適用於下列語言和平台，以及正在研發的其他語言和平台：</span><span class="sxs-lookup"><span data-stu-id="ea959-278">Libraries are currently available for the following languages and platforms, with others in the pipeline:</span></span>

### <a name="azure-storage-data-services"></a><span data-ttu-id="ea959-279">Azure 儲存體資料服務</span><span class="sxs-lookup"><span data-stu-id="ea959-279">Azure Storage data services</span></span>
* [<span data-ttu-id="ea959-280">儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="ea959-280">Storage Services REST API</span></span>](/rest/api/storageservices/)
* [<span data-ttu-id="ea959-281">適用於 .NET 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="ea959-281">Storage Client Library for .NET</span></span>](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [<span data-ttu-id="ea959-282">Storage Client Library for C++</span><span class="sxs-lookup"><span data-stu-id="ea959-282">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* [<span data-ttu-id="ea959-283">適用於 Java/Android 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="ea959-283">Storage Client Library for Java/Android</span></span>](https://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="ea959-284">適用於 Node.js 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="ea959-284">Storage Client Library for Node.js</span></span>](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [<span data-ttu-id="ea959-285">適用於 PHP 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="ea959-285">Storage Client Library for PHP</span></span>](https://azure.microsoft.com/develop/php/)
* [<span data-ttu-id="ea959-286">適用於 Python 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="ea959-286">Storage Client Library for Python</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="ea959-287">適用於 Ruby 的儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="ea959-287">Storage Client Library for Ruby</span></span>](https://azure.microsoft.com/develop/ruby/)
* [<span data-ttu-id="ea959-288">適用於 PowerShell 的儲存體 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="ea959-288">Storage Cmdlets for PowerShell</span></span>](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [<span data-ttu-id="ea959-289">適用於 CLI 2.0 的儲存體命令</span><span class="sxs-lookup"><span data-stu-id="ea959-289">Storage Commands for CLI 2.0</span></span>](/cli/azure/storage)

## <a name="next-steps"></a><span data-ttu-id="ea959-290">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea959-290">Next steps</span></span>

* [<span data-ttu-id="ea959-291">深入了解 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-291">Learn more about Blob storage</span></span>](../blobs/storage-blobs-introduction.md)
* [<span data-ttu-id="ea959-292">深入了解檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-292">Learn more about File storage</span></span>](../storage-files-introduction.md)
* [<span data-ttu-id="ea959-293">深入了解佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-293">Learn more about Queue storage</span></span>](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
To get up and running with Azure Storage quickly, check out one of the following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT TO DO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for the following languages and platforms, with others in the pipeline:

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
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
To learn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link to one of those. 
Had to remove this article, it refers to the VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a><span data-ttu-id="ea959-294">針對系統管理員</span><span class="sxs-lookup"><span data-stu-id="ea959-294">For administrators</span></span>
* [<span data-ttu-id="ea959-295">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-295">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="ea959-296">使用 Azure CLI 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-296">Using Azure CLI with Azure Storage</span></span>](../storage-azure-cli.md)

### <a name="for-net-developers"></a><span data-ttu-id="ea959-297">針對 .NET 開發人員</span><span class="sxs-lookup"><span data-stu-id="ea959-297">For .NET developers</span></span>
* [<span data-ttu-id="ea959-298">以 .NET 開始使用 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-298">Get started with Azure Blob storage using .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="ea959-299">以 .NET 開始使用 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-299">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="ea959-300">以 .NET 開始使用 Azure 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-300">Get started with Azure Queue storage using .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="ea959-301">在 Windows 上開始使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-301">Get started with Azure File storage on Windows</span></span>](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a><span data-ttu-id="ea959-302">針對 Java/Android 開發人員</span><span class="sxs-lookup"><span data-stu-id="ea959-302">For Java/Android developers</span></span>
* [<span data-ttu-id="ea959-303">如何使用 Java 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-303">How to use Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="ea959-304">如何使用 Java 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-304">How to use Table storage from Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="ea959-305">如何使用 Java 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-305">How to use Queue storage from Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="ea959-306">如何使用 Java 的檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-306">How to use File storage from Java</span></span>](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a><span data-ttu-id="ea959-307">針對 Node.js 開發人員</span><span class="sxs-lookup"><span data-stu-id="ea959-307">For Node.js developers</span></span>
* [<span data-ttu-id="ea959-308">如何使用 Node.js 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-308">How to use Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="ea959-309">如何使用 Node.js 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-309">How to use Table storage from Node.js</span></span>](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="ea959-310">如何使用 Node.js 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-310">How to use Queue storage from Node.js</span></span>](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a><span data-ttu-id="ea959-311">針對 PHP 開發人員</span><span class="sxs-lookup"><span data-stu-id="ea959-311">For PHP developers</span></span>
* [<span data-ttu-id="ea959-312">如何使用 PHP 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-312">How to use Blob storage from PHP</span></span>](../blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="ea959-313">如何使用 PHP 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-313">How to use Table storage from PHP</span></span>](../../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="ea959-314">如何使用 PHP 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-314">How to use Queue storage from PHP</span></span>](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a><span data-ttu-id="ea959-315">針對 Ruby 開發人員</span><span class="sxs-lookup"><span data-stu-id="ea959-315">For Ruby developers</span></span>
* [<span data-ttu-id="ea959-316">如何使用 Ruby 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-316">How to use Blob storage from Ruby</span></span>](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [<span data-ttu-id="ea959-317">如何使用 Ruby 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-317">How to use Table storage from Ruby</span></span>](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [<span data-ttu-id="ea959-318">如何使用 Ruby 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-318">How to use Queue storage from Ruby</span></span>](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a><span data-ttu-id="ea959-319">針對 Python 開發人員</span><span class="sxs-lookup"><span data-stu-id="ea959-319">For Python developers</span></span>
* [<span data-ttu-id="ea959-320">如何使用 Python 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-320">How to use Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="ea959-321">如何使用 Python 的表格儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-321">How to use Table storage from Python</span></span>](../../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="ea959-322">如何使用 Python 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="ea959-322">How to use Queue storage from Python</span></span>](../storage-python-how-to-use-queue-storage.md)   
* <span data-ttu-id="ea959-323">[如何使用 Python 的檔案儲存體](../storage-python-how-to-use-file-storage.md) 
--></span><span class="sxs-lookup"><span data-stu-id="ea959-323">[How to use File storage from Python](../storage-python-how-to-use-file-storage.md) 
--></span></span>