---
title: "Azure Stack 儲存體簡介"
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
ms.date: 9/25/2017
ms.author: xiaofmao
ms.openlocfilehash: 8777aa486a627cf8b2d8ba443e115638354d10da
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="introduction-to-azure-stack-storage"></a><span data-ttu-id="1f029-103">Azure Stack 儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="1f029-103">Introduction to Azure Stack storage</span></span>

<span data-ttu-id="1f029-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="1f029-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

## <a name="overview"></a><span data-ttu-id="1f029-105">概觀</span><span class="sxs-lookup"><span data-stu-id="1f029-105">Overview</span></span>
<span data-ttu-id="1f029-106">Azure Stack 儲存體是一組雲端儲存體服務，包括與 Azure 儲存體服務一致的 Blob、資料表和佇列。</span><span class="sxs-lookup"><span data-stu-id="1f029-106">Azure Stack Storage is a set of cloud storage services including Blobs, Tables and Queues which are consistent with Azure Storage services.</span></span>

## <a name="azure-stack-storage-services"></a><span data-ttu-id="1f029-107">Azure Stack 儲存體服務</span><span class="sxs-lookup"><span data-stu-id="1f029-107">Azure Stack Storage services</span></span>
<span data-ttu-id="1f029-108">Azure Stack 儲存體提供下列三項服務：</span><span class="sxs-lookup"><span data-stu-id="1f029-108">Azure Stack storage provides the following three services:</span></span>

* <span data-ttu-id="1f029-109">**Blob 儲存體**</span><span class="sxs-lookup"><span data-stu-id="1f029-109">**Blob Storage**</span></span> 

    <span data-ttu-id="1f029-110">Blob 儲存體可儲存非結構化物件資料。</span><span class="sxs-lookup"><span data-stu-id="1f029-110">Blob storage stores unstructured object data.</span></span> <span data-ttu-id="1f029-111">Blob 可以是任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="1f029-111">A blob can be any type of text or binary data, such as a document, media file, or application installer.</span></span>
* <span data-ttu-id="1f029-112">**資料表儲存體**</span><span class="sxs-lookup"><span data-stu-id="1f029-112">**Table Storage**</span></span> 

    <span data-ttu-id="1f029-113">資料表儲存體可儲存結構化的資料集。</span><span class="sxs-lookup"><span data-stu-id="1f029-113">Table storage stores structured datasets.</span></span> <span data-ttu-id="1f029-114">表格儲存體屬於 NoSQL 索引鍵屬性資料儲存，可允許快速開發和迅速存取大量資料。</span><span class="sxs-lookup"><span data-stu-id="1f029-114">Table storage is a NoSQL key-attribute data store, which allows for rapid development and fast access to large quantities of data.</span></span>
* <span data-ttu-id="1f029-115">**佇列儲存體**</span><span class="sxs-lookup"><span data-stu-id="1f029-115">**Queue Storage**</span></span> 

    <span data-ttu-id="1f029-116">佇列儲存體針對工作流程處理及雲端服務元件間的通訊，提供可靠的訊息服務。</span><span class="sxs-lookup"><span data-stu-id="1f029-116">Queue storage provides reliable messaging for workflow processing and for communication between components of cloud services.</span></span>

<span data-ttu-id="1f029-117">Azure Stack 儲存體帳戶是可讓您存取 Azure Stack 儲存體服務的安全帳戶。</span><span class="sxs-lookup"><span data-stu-id="1f029-117">An Azure Stack storage account is a secure account that gives you access to services in Azure Stack Storage.</span></span> <span data-ttu-id="1f029-118">您的儲存體帳戶提供儲存體資源的唯一命名空間。</span><span class="sxs-lookup"><span data-stu-id="1f029-118">Your storage account provides the unique namespace for your storage resources.</span></span> <span data-ttu-id="1f029-119">下圖顯示儲存體帳戶中 Azure Stack 儲存體資源之間的關係：</span><span class="sxs-lookup"><span data-stu-id="1f029-119">The following diagram shows the relationships between the Azure Stack storage resources in a storage account:</span></span>

![Azure Stack 儲存體概觀](media/azure-stack-storage-overview/AzureStackStorageOverview.png)


### <a name="blob-storage"></a><span data-ttu-id="1f029-121">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="1f029-121">Blob storage</span></span>

<span data-ttu-id="1f029-122">對於擁有大量非結構化物件資料要儲存於雲端的使用者，Blob 儲存體提供有效且可調整的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1f029-122">For users with a large amount of unstructured object data to store in the cloud, Blob storage offers an effective and scalable solution.</span></span> <span data-ttu-id="1f029-123">您可以使用 Blob 儲存體來儲存如下所示的內容：</span><span class="sxs-lookup"><span data-stu-id="1f029-123">You can use Blob storage to store content such as:</span></span>

* <span data-ttu-id="1f029-124">文件</span><span class="sxs-lookup"><span data-stu-id="1f029-124">Documents</span></span>
* <span data-ttu-id="1f029-125">社交資料 (例如照片、視訊、音樂和部落格)</span><span class="sxs-lookup"><span data-stu-id="1f029-125">Social data such as photos, videos, music, and blogs</span></span>
* <span data-ttu-id="1f029-126">檔案、電腦、資料庫和裝置的備份</span><span class="sxs-lookup"><span data-stu-id="1f029-126">Backups of files, computers, databases, and devices</span></span>
* <span data-ttu-id="1f029-127">Web 應用程式的影像和文字</span><span class="sxs-lookup"><span data-stu-id="1f029-127">Images and text for web applications</span></span>
* <span data-ttu-id="1f029-128">雲端應用程式的組態資料</span><span class="sxs-lookup"><span data-stu-id="1f029-128">Configuration data for cloud applications</span></span>
* <span data-ttu-id="1f029-129">巨量資料 (例如記錄和其他大型資料集)</span><span class="sxs-lookup"><span data-stu-id="1f029-129">Big data, such as logs and other large datasets</span></span>

<span data-ttu-id="1f029-130">每個 Blob 會組織成一個容器。</span><span class="sxs-lookup"><span data-stu-id="1f029-130">Every blob is organized into a container.</span></span> <span data-ttu-id="1f029-131">容器也提供對物件群組指派安全原則的實用方式。</span><span class="sxs-lookup"><span data-stu-id="1f029-131">Containers also provide a useful way to assign security policies to groups of objects.</span></span> <span data-ttu-id="1f029-132">儲存體帳戶可包含任意數目的容器，而容器可包含任意數目的 Blob，最高可達儲存體帳戶的限制。</span><span class="sxs-lookup"><span data-stu-id="1f029-132">A storage account can contain any number of containers, and a container can contain any number of blobs, up to the limit of storage account.</span></span>

<span data-ttu-id="1f029-133">Blob 儲存體提供三種類型的 Blob：</span><span class="sxs-lookup"><span data-stu-id="1f029-133">Blob storage offers three types of blobs:</span></span> 
* <span data-ttu-id="1f029-134">**區塊 Blob**</span><span class="sxs-lookup"><span data-stu-id="1f029-134">**Block blobs**</span></span> 

    <span data-ttu-id="1f029-135">區塊 Blob 已針對串流和儲存雲端物件進行最佳化，是儲存文件、媒體檔案、備份等的不錯選擇。</span><span class="sxs-lookup"><span data-stu-id="1f029-135">Block blobs are optimized for streaming and storing cloud objects, and are a good choice for storing documents, media files, backups etc.</span></span>
* <span data-ttu-id="1f029-136">**附加 Blob**</span><span class="sxs-lookup"><span data-stu-id="1f029-136">**Append blobs**</span></span> 

    <span data-ttu-id="1f029-137">附加 Blob 和區塊 Blob 類似，但已針對附加作業最佳化。</span><span class="sxs-lookup"><span data-stu-id="1f029-137">Append blobs are similar to block blobs, but are optimized for append operations.</span></span> <span data-ttu-id="1f029-138">附加 Blob 只能透過在結尾新增新的區塊來更新。</span><span class="sxs-lookup"><span data-stu-id="1f029-138">An append blob can be updated only by adding a new block to the end.</span></span> <span data-ttu-id="1f029-139">對於如記錄等僅需要將新資料寫入 Blob 結尾的情況，附加 Blob 是不錯的選擇。</span><span class="sxs-lookup"><span data-stu-id="1f029-139">Append blobs are a good choice for scenarios such as logging, where new data needs to be written only to the end of the blob.</span></span>
* <span data-ttu-id="1f029-140">**分頁 Blob**</span><span class="sxs-lookup"><span data-stu-id="1f029-140">**Page blobs**</span></span> 

    <span data-ttu-id="1f029-141">分頁 Blob 已針對代表 IaaS 磁碟與支援隨機寫入進行最佳化，且大小可以高達 1 TB。</span><span class="sxs-lookup"><span data-stu-id="1f029-141">Page blobs are optimized for representing IaaS disks and supporting random writes which is up to 1 TB in size.</span></span> <span data-ttu-id="1f029-142">Azure Stack 虛擬機器連結的 IaaS 磁碟是以分頁 Blob 方式儲存的 VHD。</span><span class="sxs-lookup"><span data-stu-id="1f029-142">An Azure Stack virtual machine attached IaaS disk is a VHD stored as a page blob.</span></span>


### <a name="table-storage"></a><span data-ttu-id="1f029-143">表格儲存體</span><span class="sxs-lookup"><span data-stu-id="1f029-143">Table storage</span></span>
<span data-ttu-id="1f029-144">新式應用程式通常會要求以超越前幾代軟體需求的延伸性和彈性儲存資料。</span><span class="sxs-lookup"><span data-stu-id="1f029-144">Modern applications often demand data stores with greater scalability and flexibility than previous generations of software required.</span></span> <span data-ttu-id="1f029-145">表格儲存體提供高可用性且可大幅擴充的儲存體，方便您的應用程式自動擴充以滿足使用者需求。</span><span class="sxs-lookup"><span data-stu-id="1f029-145">Table storage offers highly available, massively scalable storage, so that your application can automatically scale to meet user demand.</span></span> <span data-ttu-id="1f029-146">表格儲存體屬於 Microsoft 的 NoSQL 索引鍵屬性儲存，它的無結構描述設計讓它有別於傳統的關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f029-146">Table storage is Microsoft's NoSQL key/attribute store – it has a schemaless design, making it different from traditional relational databases.</span></span> <span data-ttu-id="1f029-147">透過無結構描述資料儲存，便可輕易隨著應用程式發展需求改寫資料。</span><span class="sxs-lookup"><span data-stu-id="1f029-147">With a schemaless data store, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="1f029-148">表格儲存體非常容易使用，方便開發人員可以快速建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f029-148">Table storage is easy to use, so developers can create applications quickly.</span></span>

<span data-ttu-id="1f029-149">資料表儲存體屬於索引鍵屬性儲存，代表資料表中的每個值會與具型別的屬性名稱一起儲存。</span><span class="sxs-lookup"><span data-stu-id="1f029-149">Table storage is a key-attribute store, meaning that every value in a table is stored with a typed property name.</span></span> <span data-ttu-id="1f029-150">屬性名稱可用來篩選與指定選取條件。</span><span class="sxs-lookup"><span data-stu-id="1f029-150">The property name can be used for filtering and specifying selection criteria.</span></span> <span data-ttu-id="1f029-151">一組屬性及其值就構成一個實體。</span><span class="sxs-lookup"><span data-stu-id="1f029-151">A collection of properties and their values comprise an entity.</span></span> <span data-ttu-id="1f029-152">因為表格儲存體沒有結構描述，因此相同資料表中的兩個實體可包含不同屬性集合，且這些屬性可以是不同類型。</span><span class="sxs-lookup"><span data-stu-id="1f029-152">Since Table storage is schemaless, two entities in the same table can contain different collections of properties, and those properties can be of different types.</span></span>

<span data-ttu-id="1f029-153">您可以使用表格儲存體來儲存具彈性的資料集，例如 Web 應用程式的使用者資料、通訊錄、裝置資訊，以及服務所需的任何其他中繼資料類型。</span><span class="sxs-lookup"><span data-stu-id="1f029-153">You can use Table storage to store flexible datasets, such as user data for web applications, address books, device information, and any other type of metadata that your service requires.</span></span> <span data-ttu-id="1f029-154">在現今的網際網路架構應用程式中，NoSQL 資料庫 (如表格儲存體) 提供傳統關聯式資料庫的熱門替代方式。</span><span class="sxs-lookup"><span data-stu-id="1f029-154">For today's Internet-based applications, NoSQL databases like Table storage offer a popular alternative to traditional relational databases.</span></span>

<span data-ttu-id="1f029-155">儲存體帳戶可包含任意數目的資料表，而資料表可包含任意數目的實體，最高可達儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="1f029-155">A storage account can contain any number of tables, and a table can contain any number of entities, up to the capacity limit of the storage account.</span></span>

### <a name="queue-storage"></a><span data-ttu-id="1f029-156">佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="1f029-156">Queue storage</span></span>
<span data-ttu-id="1f029-157">設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。</span><span class="sxs-lookup"><span data-stu-id="1f029-157">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="1f029-158">佇列儲存體針對應用程式元件間的非同步通訊，提供可靠的訊息服務解決方案，無論應用程式元件是在雲端、桌面、內部部署伺服器或行動裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="1f029-158">Queue storage provides a reliable messaging solution for asynchronous communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="1f029-159">佇列儲存體也支援管理非同步工作並建置處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="1f029-159">Queue storage also supports managing asynchronous tasks and building process workflows.</span></span>

<span data-ttu-id="1f029-160">儲存體帳戶可包含任意數目的佇列，而佇列可包含任意數目的訊息，最高可達儲存體帳戶的容量限制。</span><span class="sxs-lookup"><span data-stu-id="1f029-160">A storage account can contain any number of queues, and a queue can contain any number of messages, up to the capacity limit of the storage account.</span></span> <span data-ttu-id="1f029-161">個別訊息的大小可能高達 64 KB。</span><span class="sxs-lookup"><span data-stu-id="1f029-161">Individual messages may be up to 64 KB in size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f029-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f029-162">Next steps</span></span>
* [<span data-ttu-id="1f029-163">與 Azure 一致的儲存體：差異與注意事項</span><span class="sxs-lookup"><span data-stu-id="1f029-163">Azure-consistent storage: differences and considerations</span></span>](azure-stack-acs-differences.md)

* <span data-ttu-id="1f029-164">若要深入了解 Azure 儲存體，請參閱 [Microsoft Azure 儲存體簡介](../../storage/common/storage-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1f029-164">To learn more about Azure Storage, see [Introduction to Microsoft Azure Storage](../../storage/common/storage-introduction.md)</span></span>

