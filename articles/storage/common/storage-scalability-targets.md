---
title: "Azure 儲存體延展性和效能目標 | Microsoft Docs"
description: "了解 Azure 儲存體的延展性和效能目標，包括標準和進階儲存體帳戶的容量、要求率以及輸入和輸出頻寬。 了解每一項 Azure 儲存體服務內分割的效能目標。"
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 47a1d2b87269d40716b3dae02276207060b41c24
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a><span data-ttu-id="fca05-104">Azure 儲存體延展性和效能目標</span><span class="sxs-lookup"><span data-stu-id="fca05-104">Azure Storage Scalability and Performance Targets</span></span>
## <a name="overview"></a><span data-ttu-id="fca05-105">Overview</span><span class="sxs-lookup"><span data-stu-id="fca05-105">Overview</span></span>
<span data-ttu-id="fca05-106">本主題描述 Microsoft Azure 儲存體的延展性和效能。</span><span class="sxs-lookup"><span data-stu-id="fca05-106">This topic describes the scalability and performance topics for Microsoft Azure Storage.</span></span> <span data-ttu-id="fca05-107">如需其他 Azure 限制的摘要，請參閱 [Azure 訂用帳戶和服務限制、配額及條件約束](../../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="fca05-107">For a summary of other Azure limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fca05-108">所有儲存體帳戶都能在一般網路拓撲上執行，並支援下面說明的延展性和效能目標，無論它們在何時建立。</span><span class="sxs-lookup"><span data-stu-id="fca05-108">All storage accounts run on the new flat network topology and support the scalability and performance targets outlined below, regardless of when they were created.</span></span> <span data-ttu-id="fca05-109">如需 Azure 儲存體平面網路架構及延展性的詳細資訊，請參閱 [Microsoft Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fca05-109">For more information on the Azure Storage flat network architecture and on scalability, see [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span></span>
> 
> [!IMPORTANT]
> <span data-ttu-id="fca05-110">列於此處的延展性和效能目標都是高階目標，但仍可達成。</span><span class="sxs-lookup"><span data-stu-id="fca05-110">The scalability and performance targets listed here are high-end targets, but are achievable.</span></span> <span data-ttu-id="fca05-111">在所有情況下，您的儲存體帳戶所達到的要求率和頻寬取決於已儲存物件的大小、使用的存取模式、應用程式執行的工作負載類型。</span><span class="sxs-lookup"><span data-stu-id="fca05-111">In all cases, the request rate and bandwidth achieved by your storage account depends upon the size of objects stored, the access patterns utilized, and the type of workload your application performs.</span></span> <span data-ttu-id="fca05-112">請務必測試您的服務，以判斷效能是否達到您的要求。</span><span class="sxs-lookup"><span data-stu-id="fca05-112">Be sure to test your service to determine whether its performance meets your requirements.</span></span> <span data-ttu-id="fca05-113">如果可能，請避免流量率突增，確保流量在不同分割之間妥善分散。</span><span class="sxs-lookup"><span data-stu-id="fca05-113">If possible, avoid sudden spikes in the rate of traffic and ensure that traffic is well-distributed across partitions.</span></span>
> 
> <span data-ttu-id="fca05-114">當您的應用程式達到分割處理工作負載的限制時，Azure 儲存體會開始傳回錯誤碼 503 (伺服器忙碌) 或錯誤碼 500 (作業逾時) 回應。</span><span class="sxs-lookup"><span data-stu-id="fca05-114">When your application reaches the limit of what a partition can handle for your workload, Azure Storage will begin to return error code 503 (Server Busy) or error code 500 (Operation Timeout) responses.</span></span> <span data-ttu-id="fca05-115">當發生這種情況時，應用程式應該使用指數輪詢重試原則。</span><span class="sxs-lookup"><span data-stu-id="fca05-115">When this occurs, the application should use an exponential backoff policy for retries.</span></span> <span data-ttu-id="fca05-116">指數輪詢讓分割的負載減少，也能減輕該分割流量的尖峰。</span><span class="sxs-lookup"><span data-stu-id="fca05-116">The exponential backoff allows the load on the partition to decrease, and to ease out spikes in traffic to that partition.</span></span>
> 
> 

<span data-ttu-id="fca05-117">如果您的應用程式需求超出單一儲存體帳戶的延展性目標，您可以建置可使用多個儲存體帳戶的應用程式，並將資料物件分割到那些儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="fca05-117">If the needs of your application exceed the scalability targets of a single storage account, you can build your application to use multiple storage accounts, and partition your data objects across those storage accounts.</span></span> <span data-ttu-id="fca05-118">如需批量價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/) 。</span><span class="sxs-lookup"><span data-stu-id="fca05-118">See [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/) for information on volume pricing.</span></span>

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a><span data-ttu-id="fca05-119">Blob、佇列、資料表和檔案的延展性目標</span><span class="sxs-lookup"><span data-stu-id="fca05-119">Scalability targets for blobs, queues, tables, and files</span></span>
[!INCLUDE [azure-storage-limits](../../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a><span data-ttu-id="fca05-120">虛擬機器磁碟的延展性目標</span><span class="sxs-lookup"><span data-stu-id="fca05-120">Scalability targets for virtual machine disks</span></span>
[!INCLUDE [azure-storage-limits-vm-disks](../../../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="fca05-121">如需詳細資訊，請參閱 [Windows VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或 [Linux VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fca05-121">See [Windows VM sizes](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Linux VM sizes](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

## <a name="managed-virtual-machine-disks"></a><span data-ttu-id="fca05-122">受管理的虛擬機器磁碟</span><span class="sxs-lookup"><span data-stu-id="fca05-122">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="fca05-123">未受管理的虛擬機器磁碟</span><span class="sxs-lookup"><span data-stu-id="fca05-123">Unmanaged virtual machine disks</span></span>
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a><span data-ttu-id="fca05-124">Azure Resource Manager 的延展性目標</span><span class="sxs-lookup"><span data-stu-id="fca05-124">Scalability targets for Azure resource manager</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a><span data-ttu-id="fca05-125">Azure 儲存體中的分割</span><span class="sxs-lookup"><span data-stu-id="fca05-125">Partitions in Azure Storage</span></span>
<span data-ttu-id="fca05-126">每個在 Azure 儲存體中保存資料的物件 (Blob、訊息、實體和檔案) 都屬於分割，也都由分割索引鍵所識別。</span><span class="sxs-lookup"><span data-stu-id="fca05-126">Every object that holds data that is stored in Azure Storage (blobs, messages, entities, and files) belongs to a partition, and is identified by a partition key.</span></span> <span data-ttu-id="fca05-127">分割會判斷 Azure 儲存體要如何在伺服器間取得 Blob、訊息、實體和檔案的負載平衡，以滿足這些物件的流量需求。</span><span class="sxs-lookup"><span data-stu-id="fca05-127">The partition determines how Azure Storage load balances blobs, messages, entities, and files across servers to meet the traffic needs of those objects.</span></span> <span data-ttu-id="fca05-128">分割索引鍵是唯一的，用於尋找 Blob、訊息或實體。</span><span class="sxs-lookup"><span data-stu-id="fca05-128">The partition key is unique and is used to locate a blob, message, or entity.</span></span>

<span data-ttu-id="fca05-129">上方位於 [標準儲存體帳戶的延展性目標](#standard-storage-accounts) 中的表格，列出每個服務的單一分割效能目標。</span><span class="sxs-lookup"><span data-stu-id="fca05-129">The table shown above in [Scalability Targets for Standard Storage Accounts](#standard-storage-accounts) lists the performance targets for a single partition for each service.</span></span>

<span data-ttu-id="fca05-130">分割會影響每個儲存體服務的負載平衡和延展性，方式如下：</span><span class="sxs-lookup"><span data-stu-id="fca05-130">Partitions affect load balancing and scalability for each of the storage services in the following ways:</span></span>

* <span data-ttu-id="fca05-131">**Blob**：Blob 的分割索引鍵為帳戶名稱 + 容器名稱 + Blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="fca05-131">**Blobs**: The partition key for a blob is account name + container name + blob name.</span></span> <span data-ttu-id="fca05-132">這表示每個 Blob 都可以有其專屬分割區 (Blob 上的負載需要它時)。</span><span class="sxs-lookup"><span data-stu-id="fca05-132">This means that each blob can have its own partition if load on the blob demands it.</span></span> <span data-ttu-id="fca05-133">Blob 可以分散到多部伺服器，以相應放大對它們的存取，但是單一伺服器只能服務單一 Blob。</span><span class="sxs-lookup"><span data-stu-id="fca05-133">Blobs can be distributed across many servers in order to scale out access to them, but a single blob can only be served by a single server.</span></span> <span data-ttu-id="fca05-134">雖然 Blog 可以在 Blog 容器中邏輯分組，但這種分組方式的意涵卻非分割。</span><span class="sxs-lookup"><span data-stu-id="fca05-134">While blobs can be logically grouped in blob containers, there are no partitioning implications from this grouping.</span></span>
* <span data-ttu-id="fca05-135">**檔案**：檔案的分割索引鍵是帳戶名稱 + 檔案共用名稱。</span><span class="sxs-lookup"><span data-stu-id="fca05-135">**Files**: The partition key for a file is account name + file share name.</span></span> <span data-ttu-id="fca05-136">這表示檔案共用中的所有檔案也都位於單一分割區中。</span><span class="sxs-lookup"><span data-stu-id="fca05-136">This means all files in a file share are also in a single partition.</span></span>
* <span data-ttu-id="fca05-137">**訊息**：訊息的分割索引鍵為帳戶名稱 + 佇列名稱，所以所有佇列中的訊息都能分組到單一分割，並由單一伺服器所服務。</span><span class="sxs-lookup"><span data-stu-id="fca05-137">**Messages**: The partition key for a message is the account name + queue name, so all messages in a queue are grouped into a single partition and are served by a single server.</span></span> <span data-ttu-id="fca05-138">不同佇列可能由不同伺服器所處理以平衡負載，無論儲存體帳戶可能有多少佇列。</span><span class="sxs-lookup"><span data-stu-id="fca05-138">Different queues may be processed by different servers to balance the load for however many queues a storage account may have.</span></span>
* <span data-ttu-id="fca05-139">**實體**：實體的分割索引鍵為帳戶名稱 + 資料表名稱 + 分割索引鍵，其中分割索引鍵是該實體由使用者定義的 **PartitionKey** 屬性所需的值。</span><span class="sxs-lookup"><span data-stu-id="fca05-139">**Entities**: The partition key for an entity is account name + table name + partition key, where the partition key is the value of the required user-defined **PartitionKey** property for the entity.</span></span> <span data-ttu-id="fca05-140">所有具有相同分割區索引鍵的實體都分組成一個相同的分割，並由相同的分割伺服器服務。</span><span class="sxs-lookup"><span data-stu-id="fca05-140">All entities with the same partition key value are grouped into the same partition and are served by the same partition server.</span></span> <span data-ttu-id="fca05-141">在設計您的應用程式時，這是要了解的重點。</span><span class="sxs-lookup"><span data-stu-id="fca05-141">This is an important point to understand in designing your application.</span></span> <span data-ttu-id="fca05-142">藉由將實體分組到單一分割的資料存取優勢，您的應用程式應該會在多個分割中分配實體時取得延展性優勢的平衡。</span><span class="sxs-lookup"><span data-stu-id="fca05-142">Your application should balance the scalability benefits of spreading entities across multiple partitions with the data access advantages of grouping entities in a single partition.</span></span>  

<span data-ttu-id="fca05-143">將資料表中的一組實體分組成一個單一分割的主要優點在於，這能讓它在相同分割中的實體之間執行不可部分完成的批次作業，因為單一伺服器上存有一個分割。</span><span class="sxs-lookup"><span data-stu-id="fca05-143">A key advantage to grouping a set of entities in a table into a single partition is that it's possible to perform atomic batch operations across entities in the same partition, since a partition exists on a single server.</span></span> <span data-ttu-id="fca05-144">因此，如果您想要對一組實體執行批次作業，請考慮使用相同的分割索引鍵將它們分組在一起。</span><span class="sxs-lookup"><span data-stu-id="fca05-144">Therefore, if you wish to perform batch operations on a group of entities, consider grouping them with the same partition key.</span></span> 

<span data-ttu-id="fca05-145">另一方面，位於相同資料表但具有不同分割索引鍵的實體，可在不同伺服器之間達到負載平衡，這可以具有較大的延展性。</span><span class="sxs-lookup"><span data-stu-id="fca05-145">On the other hand, entities that are in the same table but have different partition keys can be load balanced across different servers, making it possible to have greater scalability.</span></span>

<span data-ttu-id="fca05-146">[這裡](https://msdn.microsoft.com/library/azure/hh508997.aspx)可以找到設計資料表分割策略的詳細建議。</span><span class="sxs-lookup"><span data-stu-id="fca05-146">Detailed recommendations for designing partitioning strategy for tables can be found [here](https://msdn.microsoft.com/library/azure/hh508997.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="fca05-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fca05-147">See Also</span></span>
* [<span data-ttu-id="fca05-148">儲存體定價詳細資料</span><span class="sxs-lookup"><span data-stu-id="fca05-148">Storage Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/storage/)
* [<span data-ttu-id="fca05-149">Azure 訂用帳戶和服務限制、配額與限制</span><span class="sxs-lookup"><span data-stu-id="fca05-149">Azure Subscription and Service Limits, Quotas, and Constraints</span></span>](../../azure-subscription-service-limits.md)
* [<span data-ttu-id="fca05-150">Premium 儲存體：Azure 虛擬機器工作負載適用的高效能儲存體</span><span class="sxs-lookup"><span data-stu-id="fca05-150">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](../storage-premium-storage.md)
* [<span data-ttu-id="fca05-151">Azure 儲存體複寫</span><span class="sxs-lookup"><span data-stu-id="fca05-151">Azure Storage Replication</span></span>](../storage-redundancy.md)
* [<span data-ttu-id="fca05-152">Microsoft Azure 儲存體效能與延展性檢查清單</span><span class="sxs-lookup"><span data-stu-id="fca05-152">Microsoft Azure Storage Performance and Scalability Checklist</span></span>](../storage-performance-checklist.md)
* [<span data-ttu-id="fca05-153">Microsoft Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="fca05-153">Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

