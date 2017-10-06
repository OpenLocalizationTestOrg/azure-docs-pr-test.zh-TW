---
title: "aaaIntroduction tooAzure 堆疊儲存體"
description: "了解 Azure Stack 儲存體"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 092aba28-04bc-44c0-90e1-e79d82f4ff42
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/19/2017
ms.author: xiaofmao
ms.openlocfilehash: 8e156584dafb8b084bfc69b9dbe7cbaa78717135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-stack-storage"></a><span data-ttu-id="53faa-103">簡介 tooAzure 堆疊儲存體</span><span class="sxs-lookup"><span data-stu-id="53faa-103">Introduction tooAzure Stack storage</span></span>

## <a name="overview"></a><span data-ttu-id="53faa-104">概觀</span><span class="sxs-lookup"><span data-stu-id="53faa-104">Overview</span></span>
<span data-ttu-id="53faa-105">Azure Stack 儲存體是一組雲端儲存體服務，包括與 Azure 儲存體服務一致的 Blob、資料表和佇列。</span><span class="sxs-lookup"><span data-stu-id="53faa-105">Azure Stack Storage is a set of cloud storage services including Blobs, Tables and Queues which are consistent with Azure Storage services.</span></span>

## <a name="azure-stack-storage-services"></a><span data-ttu-id="53faa-106">Azure Stack 儲存體服務</span><span class="sxs-lookup"><span data-stu-id="53faa-106">Azure Stack Storage services</span></span>
<span data-ttu-id="53faa-107">Azure 堆疊儲存體提供下列三項服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="53faa-107">Azure Stack storage provides hello following three services:</span></span>

* <span data-ttu-id="53faa-108">**Blob 儲存體**</span><span class="sxs-lookup"><span data-stu-id="53faa-108">**Blob Storage**</span></span> 

    <span data-ttu-id="53faa-109">Blob 儲存體可儲存非結構化物件資料。</span><span class="sxs-lookup"><span data-stu-id="53faa-109">Blob storage stores unstructured object data.</span></span> <span data-ttu-id="53faa-110">Blob 可以是任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="53faa-110">A blob can be any type of text or binary data, such as a document, media file, or application installer.</span></span>
* <span data-ttu-id="53faa-111">**資料表儲存體**</span><span class="sxs-lookup"><span data-stu-id="53faa-111">**Table Storage**</span></span> 

    <span data-ttu-id="53faa-112">資料表儲存體可儲存結構化的資料集。</span><span class="sxs-lookup"><span data-stu-id="53faa-112">Table storage stores structured datasets.</span></span> <span data-ttu-id="53faa-113">資料表儲存體是 NoSQL 索引鍵屬性的資料存放區，可快速開發和快速存取 toolarge 數量的資料。</span><span class="sxs-lookup"><span data-stu-id="53faa-113">Table storage is a NoSQL key-attribute data store, which allows for rapid development and fast access toolarge quantities of data.</span></span>
* <span data-ttu-id="53faa-114">**佇列儲存體**</span><span class="sxs-lookup"><span data-stu-id="53faa-114">**Queue Storage**</span></span> 

    <span data-ttu-id="53faa-115">佇列儲存體針對工作流程處理及雲端服務元件間的通訊，提供可靠的訊息服務。</span><span class="sxs-lookup"><span data-stu-id="53faa-115">Queue storage provides reliable messaging for workflow processing and for communication between components of cloud services.</span></span>

<span data-ttu-id="53faa-116">堆疊 Azure 儲存體帳戶是安全的帳戶，可讓您存取 tooservices Azure 堆疊儲存體中。</span><span class="sxs-lookup"><span data-stu-id="53faa-116">An Azure Stack storage account is a secure account that gives you access tooservices in Azure Stack Storage.</span></span> <span data-ttu-id="53faa-117">儲存體帳戶提供儲存體資源 hello 唯一命名空間。</span><span class="sxs-lookup"><span data-stu-id="53faa-117">Your storage account provides hello unique namespace for your storage resources.</span></span> <span data-ttu-id="53faa-118">hello 下列圖表顯示 hello 之間關聯性 hello 堆疊 Azure 儲存體資源中的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="53faa-118">hello following diagram shows hello relationships between hello Azure Stack storage resources in a storage account:</span></span>

![Azure Stack 儲存體概觀](media/azure-stack-storage-overview/AzureStackStorageOverview.png)


### <a name="blob-storage"></a><span data-ttu-id="53faa-120">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="53faa-120">Blob storage</span></span>

<span data-ttu-id="53faa-121">Blob 儲存體具有大量非結構化的物件資料 toostore hello 雲端中的使用者，提供有效率且可調整的解決方案。</span><span class="sxs-lookup"><span data-stu-id="53faa-121">For users with a large amount of unstructured object data toostore in hello cloud, Blob storage offers an effective and scalable solution.</span></span> <span data-ttu-id="53faa-122">您可以使用 Blob 儲存體 toostore 內容，例如：</span><span class="sxs-lookup"><span data-stu-id="53faa-122">You can use Blob storage toostore content such as:</span></span>

* <span data-ttu-id="53faa-123">文件</span><span class="sxs-lookup"><span data-stu-id="53faa-123">Documents</span></span>
* <span data-ttu-id="53faa-124">社交資料 (例如照片、視訊、音樂和部落格)</span><span class="sxs-lookup"><span data-stu-id="53faa-124">Social data such as photos, videos, music, and blogs</span></span>
* <span data-ttu-id="53faa-125">檔案、電腦、資料庫和裝置的備份</span><span class="sxs-lookup"><span data-stu-id="53faa-125">Backups of files, computers, databases, and devices</span></span>
* <span data-ttu-id="53faa-126">Web 應用程式的影像和文字</span><span class="sxs-lookup"><span data-stu-id="53faa-126">Images and text for web applications</span></span>
* <span data-ttu-id="53faa-127">雲端應用程式的組態資料</span><span class="sxs-lookup"><span data-stu-id="53faa-127">Configuration data for cloud applications</span></span>
* <span data-ttu-id="53faa-128">巨量資料 (例如記錄和其他大型資料集)</span><span class="sxs-lookup"><span data-stu-id="53faa-128">Big data, such as logs and other large datasets</span></span>

<span data-ttu-id="53faa-129">每個 Blob 會組織成一個容器。</span><span class="sxs-lookup"><span data-stu-id="53faa-129">Every blob is organized into a container.</span></span> <span data-ttu-id="53faa-130">容器也會提供實用的方式 tooassign 安全性原則 toogroups 的物件。</span><span class="sxs-lookup"><span data-stu-id="53faa-130">Containers also provide a useful way tooassign security policies toogroups of objects.</span></span> <span data-ttu-id="53faa-131">儲存體帳戶可以包含任何數目的容器，以及容器可以包含任何數目的 blob，向上 toohello 限制的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="53faa-131">A storage account can contain any number of containers, and a container can contain any number of blobs, up toohello limit of storage account.</span></span>

<span data-ttu-id="53faa-132">Blob 儲存體提供三種類型的 Blob：</span><span class="sxs-lookup"><span data-stu-id="53faa-132">Blob storage offers three types of blobs:</span></span> 
* <span data-ttu-id="53faa-133">**區塊 Blob**</span><span class="sxs-lookup"><span data-stu-id="53faa-133">**Block blobs**</span></span> 

    <span data-ttu-id="53faa-134">區塊 Blob 已針對串流和儲存雲端物件進行最佳化，是儲存文件、媒體檔案、備份等的不錯選擇。</span><span class="sxs-lookup"><span data-stu-id="53faa-134">Block blobs are optimized for streaming and storing cloud objects, and are a good choice for storing documents, media files, backups etc.</span></span>
* <span data-ttu-id="53faa-135">**附加 Blob**</span><span class="sxs-lookup"><span data-stu-id="53faa-135">**Append blobs**</span></span> 

    <span data-ttu-id="53faa-136">附加 blob 類似 tooblock blob，但適合用於附加作業。</span><span class="sxs-lookup"><span data-stu-id="53faa-136">Append blobs are similar tooblock blobs, but are optimized for append operations.</span></span> <span data-ttu-id="53faa-137">附加 blob 可以只是藉由加入新的區塊 toohello 結尾更新。</span><span class="sxs-lookup"><span data-stu-id="53faa-137">An append blob can be updated only by adding a new block toohello end.</span></span> <span data-ttu-id="53faa-138">附加 blob 是不錯的選擇，例如記錄、 需要新的資料寫入只 toohello 結尾 hello blob toobe 案例。</span><span class="sxs-lookup"><span data-stu-id="53faa-138">Append blobs are a good choice for scenarios such as logging, where new data needs toobe written only toohello end of hello blob.</span></span>
* <span data-ttu-id="53faa-139">**分頁 Blob**</span><span class="sxs-lookup"><span data-stu-id="53faa-139">**Page blobs**</span></span> 

    <span data-ttu-id="53faa-140">分頁 blob 適用於代表 IaaS 磁碟，並支援隨機寫入這是總 too1 TB 的大小。</span><span class="sxs-lookup"><span data-stu-id="53faa-140">Page blobs are optimized for representing IaaS disks and supporting random writes which is up too1 TB in size.</span></span> <span data-ttu-id="53faa-141">Azure Stack 虛擬機器連結的 IaaS 磁碟是以分頁 Blob 方式儲存的 VHD。</span><span class="sxs-lookup"><span data-stu-id="53faa-141">An Azure Stack virtual machine attached IaaS disk is a VHD stored as a page blob.</span></span>


### <a name="table-storage"></a><span data-ttu-id="53faa-142">表格儲存體</span><span class="sxs-lookup"><span data-stu-id="53faa-142">Table storage</span></span>
<span data-ttu-id="53faa-143">新式應用程式通常會要求以超越前幾代軟體需求的延伸性和彈性儲存資料。</span><span class="sxs-lookup"><span data-stu-id="53faa-143">Modern applications often demand data stores with greater scalability and flexibility than previous generations of software required.</span></span> <span data-ttu-id="53faa-144">資料表儲存體提供高可用性、 可大幅擴充的儲存體，讓您的應用程式可以自動調整 toomeet 使用者需求。</span><span class="sxs-lookup"><span data-stu-id="53faa-144">Table storage offers highly available, massively scalable storage, so that your application can automatically scale toomeet user demand.</span></span> <span data-ttu-id="53faa-145">表格儲存體屬於 Microsoft 的 NoSQL 索引鍵屬性儲存，它的無結構描述設計讓它有別於傳統的關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="53faa-145">Table storage is Microsoft's NoSQL key/attribute store – it has a schemaless design, making it different from traditional relational databases.</span></span> <span data-ttu-id="53faa-146">Schemaless 資料存放區中，很容易 tooadapt 資料做為 hello 需要的應用程式 evolve。</span><span class="sxs-lookup"><span data-stu-id="53faa-146">With a schemaless data store, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="53faa-147">資料表儲存體是簡單 toouse，因此開發人員可以快速建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="53faa-147">Table storage is easy toouse, so developers can create applications quickly.</span></span>

<span data-ttu-id="53faa-148">表格儲存體屬於索引鍵屬性儲存，代表資料表中的每個值會與具型別的屬性名稱一起儲存。</span><span class="sxs-lookup"><span data-stu-id="53faa-148">Table storage is a key-attribute store, meaning that every value in a table is stored with a typed property name.</span></span> <span data-ttu-id="53faa-149">hello 屬性名稱可以用於篩選和指定選取準則。</span><span class="sxs-lookup"><span data-stu-id="53faa-149">hello property name can be used for filtering and specifying selection criteria.</span></span> <span data-ttu-id="53faa-150">一組屬性及其值就構成一個實體。</span><span class="sxs-lookup"><span data-stu-id="53faa-150">A collection of properties and their values comprise an entity.</span></span> <span data-ttu-id="53faa-151">由於 schemaless 資料表儲存體，在兩個實體 hello 相同資料表可以包含不同集合的屬性，而這些屬性可以屬於不同的類型。</span><span class="sxs-lookup"><span data-stu-id="53faa-151">Since Table storage is schemaless, two entities in hello same table can contain different collections of properties, and those properties can be of different types.</span></span>

<span data-ttu-id="53faa-152">您可以使用資料表儲存體 toostore 彈性的資料集，例如 web 應用程式、 通訊錄，裝置資訊和任何其他類型的中繼資料服務所需的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="53faa-152">You can use Table storage toostore flexible datasets, such as user data for web applications, address books, device information, and any other type of metadata that your service requires.</span></span> <span data-ttu-id="53faa-153">現今的以網際網路為基礎的應用程式對於類似資料表儲存體的 NoSQL 資料庫會提供常用的替代 tootraditional 關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="53faa-153">For today's Internet-based applications, NoSQL databases like Table storage offer a popular alternative tootraditional relational databases.</span></span>

<span data-ttu-id="53faa-154">儲存體帳戶可以包含任何數量的資料表，以及資料表可以包含任意數目的實體，向上 toohello hello 儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="53faa-154">A storage account can contain any number of tables, and a table can contain any number of entities, up toohello capacity limit of hello storage account.</span></span>

### <a name="queue-storage"></a><span data-ttu-id="53faa-155">佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="53faa-155">Queue storage</span></span>
<span data-ttu-id="53faa-156">設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。</span><span class="sxs-lookup"><span data-stu-id="53faa-156">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="53faa-157">佇列儲存體提供可靠的傳訊解決方案的應用程式元件之間的非同步通訊，不論它們是在 hello 雲端中，hello 桌面、 內部部署伺服器，或行動裝置。</span><span class="sxs-lookup"><span data-stu-id="53faa-157">Queue storage provides a reliable messaging solution for asynchronous communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="53faa-158">佇列儲存體也支援管理非同步工作並建置處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="53faa-158">Queue storage also supports managing asynchronous tasks and building process workflows.</span></span>

<span data-ttu-id="53faa-159">儲存體帳戶可以包含任何數目的佇列，並佇列可以包含任意數目的訊息，向上 toohello hello 儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="53faa-159">A storage account can contain any number of queues, and a queue can contain any number of messages, up toohello capacity limit of hello storage account.</span></span> <span data-ttu-id="53faa-160">個別訊息可能是 up too64 KB 的大小。</span><span class="sxs-lookup"><span data-stu-id="53faa-160">Individual messages may be up too64 KB in size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53faa-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53faa-161">Next steps</span></span>
* [<span data-ttu-id="53faa-162">與 Azure 一致的儲存體：差異與注意事項</span><span class="sxs-lookup"><span data-stu-id="53faa-162">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)

* <span data-ttu-id="53faa-163">toolearn 進一步了解 Azure 儲存體，請參閱[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="53faa-163">toolearn more about Azure Storage, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md)</span></span>

