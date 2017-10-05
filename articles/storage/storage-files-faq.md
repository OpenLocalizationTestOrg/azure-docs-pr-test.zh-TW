---
title: "關於 Azure 檔案儲存體的常見問題集 | Microsoft Docs"
description: "尋找關於 Azure 檔案儲存體之常見問題集的解答。"
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: cb2134502a585c4f9772e594f635c10f1841e46f
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a><span data-ttu-id="86a83-103">關於 Azure 檔案儲存體的常見問題集</span><span class="sxs-lookup"><span data-stu-id="86a83-103">Frequently Asked Questions about Azure File storage</span></span>

## <a name="general"></a><span data-ttu-id="86a83-104">一般</span><span class="sxs-lookup"><span data-stu-id="86a83-104">General</span></span>
* <span data-ttu-id="86a83-105">**問：什麼是 Azure 檔案儲存體？**</span><span class="sxs-lookup"><span data-stu-id="86a83-105">**Q. What is Azure File storage?**</span></span>  
   
    <span data-ttu-id="86a83-106">Azure 檔案儲存體是 Azure 中的分散式檔案系統。</span><span class="sxs-lookup"><span data-stu-id="86a83-106">Azure File storage is a distributed file system in Azure.</span></span> <span data-ttu-id="86a83-107">其所提供的 SMB 通訊協定介面可讓使用者將儲存體當做原生共用，掛接到支援的 Azure 虛擬機器或內部部署機器上。</span><span class="sxs-lookup"><span data-stu-id="86a83-107">It provides an SMB protocol interface which allows users to mount the storage as a native share on supported Azure Virtual Machine or on-premises machine.</span></span>

* <span data-ttu-id="86a83-108">**問：Azure 檔案儲存體為何很實用？**</span><span class="sxs-lookup"><span data-stu-id="86a83-108">**Q. Why is Azure File storage useful?**</span></span>  
   
    <span data-ttu-id="86a83-109">Azure 檔案儲存體可跨多部 VM 和平台存取共用資料。</span><span class="sxs-lookup"><span data-stu-id="86a83-109">Azure File storage provides shared data access across multiple VMs and platforms.</span></span> <span data-ttu-id="86a83-110">請參閱 [Azure 檔案儲存體為何很實用](storage-files-introduction.md#why-azure-file-storage-is-useful)。</span><span class="sxs-lookup"><span data-stu-id="86a83-110">Refer to [Why Azure File storage is useful](storage-files-introduction.md#why-azure-file-storage-is-useful).</span></span>

* <span data-ttu-id="86a83-111">**問：何時應該使用 Azure 檔案、Azure Blob 或 Azure 磁碟？**</span><span class="sxs-lookup"><span data-stu-id="86a83-111">**Q. When should I use Azure File vs Azure Blob vs Azure Disk ?**</span></span>  
   
    <span data-ttu-id="86a83-112">Microsoft Azure 提供在雲端中儲存及存取資料的幾種方式。</span><span class="sxs-lookup"><span data-stu-id="86a83-112">Microsoft Azure provides several ways to store and access data in the cloud.</span></span>  
   
    <span data-ttu-id="86a83-113">Azure 檔案儲存體 - 提供 SMB 介面、用戶端程式庫和 REST 介面，允許從任何位置輕鬆存取儲存的檔案。</span><span class="sxs-lookup"><span data-stu-id="86a83-113">Azure File storage - Provides an SMB interface, client libraries, and a REST interface that allows easy access from anywhere to stored files.</span></span>  
   
    <span data-ttu-id="86a83-114">Azure Blob - 提供用戶端程式庫和 REST 介面，允許在區塊 Blob 中大規模地儲存及存取非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="86a83-114">Azure Blobs - Provides client libraries and a REST interface that allows unstructured data to be stored and accessed at a massive scale in block blobs.</span></span>  
   
    <span data-ttu-id="86a83-115">Azure 資料磁碟 - 提供用戶端程式庫和 REST 介面，允許持續從連結的虛擬硬碟儲存和存取資料。</span><span class="sxs-lookup"><span data-stu-id="86a83-115">Azure Data Disks - Provides client libraries and a REST interface that allows data to be persistently stored and accessed from an attached virtual hard disk.</span></span>  
   
    <span data-ttu-id="86a83-116">如需詳細資訊，請參閱[決定何時使用 Azure Blob、Azure 檔案或 Azure 資料磁碟](storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="86a83-116">Learn more on [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](storage-decide-blobs-files-disks.md)</span></span>

* <span data-ttu-id="86a83-117">**問：如何開始使用 Azure 檔案儲存體？**</span><span class="sxs-lookup"><span data-stu-id="86a83-117">**Q. How do I get started using Azure File storage?**</span></span>  
   
    <span data-ttu-id="86a83-118">您可以從建立 Azure 檔案共用開始。</span><span class="sxs-lookup"><span data-stu-id="86a83-118">You can start by creating an Azure file share.</span></span> <span data-ttu-id="86a83-119">您可以使用 Azure 入口網站、Azure 儲存體 PowerShell Cmdlet、Azure 儲存體用戶端程式庫或 Azure 儲存體 REST API 來建立 Azure 檔案共用。在本教學課程中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="86a83-119">You can create Azure File shares using Azure Portal, the Azure Storage PowerShell cmdlets, the Azure Storage client libraries, or the Azure Storage REST API.In this tutorial, you will learn:</span></span>

    * [<span data-ttu-id="86a83-120">了解如何使用入口網站建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="86a83-120">Learn how to create Azure File share using the Portal</span></span>](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [<span data-ttu-id="86a83-121">了解如何使用 PowerShell 建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="86a83-121">Learn how to create Azure File share using Powershell</span></span>](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [<span data-ttu-id="86a83-122">了解如何使用 CLI 建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="86a83-122">Learn how to create Azure File share using CLI</span></span>](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* <span data-ttu-id="86a83-123">**問：Azure 檔案儲存體支援何種複寫？**</span><span class="sxs-lookup"><span data-stu-id="86a83-123">**Q. What replications are supported by Azure File storage?**</span></span>  
   
    <span data-ttu-id="86a83-124">Azure 檔案儲存體目前只支援 LRS 或 GRS。</span><span class="sxs-lookup"><span data-stu-id="86a83-124">Azure File storage only supports LRS or GRS right now.</span></span> <span data-ttu-id="86a83-125">我們打算支援 RA-GRS，但時程尚未決定。</span><span class="sxs-lookup"><span data-stu-id="86a83-125">We plan to support RA-GRS but there is no timeline to share yet.</span></span>

## <a name="security-authentication-and-access-control"></a><span data-ttu-id="86a83-126">安全性、驗證和存取控制</span><span class="sxs-lookup"><span data-stu-id="86a83-126">Security, Authentication and Access Control</span></span>

* <span data-ttu-id="86a83-127">**問：有哪些不同方式可在 Azure 檔案儲存體中存取檔案？**</span><span class="sxs-lookup"><span data-stu-id="86a83-127">**Q. What are different ways to access files in Azure File storage?**</span></span>
    
    <span data-ttu-id="86a83-128">您可以使用 SMB 3.0 通訊協定或使用[儲存體總管](http://storageexplorer.com/)之類的工具，在本機電腦上掛接檔案共用以存取檔案共用中的檔案。</span><span class="sxs-lookup"><span data-stu-id="86a83-128">You can mount the file share on your local machine using SMB 3.0 protocol or use tools like [Storage Explorer](http://storageexplorer.com/) to access files in your file share.</span></span> <span data-ttu-id="86a83-129">從您的應用程式中，您可以使用儲存體用戶端程式庫、REST API 或 PowerShell 來存取 Azure 檔案共用中的檔案。</span><span class="sxs-lookup"><span data-stu-id="86a83-129">From your application, you can use storage client libraries, REST APIs or Powershell to access your files in Azure File share.</span></span>

* <span data-ttu-id="86a83-130">**問：要如何提供透過網頁瀏覽器對特定檔案的存取權？**</span><span class="sxs-lookup"><span data-stu-id="86a83-130">**Q. How can I provide access to a specific file using a web browser?**</span></span>
    
    <span data-ttu-id="86a83-131">使用 SAS 時，您可以產生在一段時間內都是有效的具有特定權限的權杖。</span><span class="sxs-lookup"><span data-stu-id="86a83-131">Using SAS, you can generate tokens with specific permissions that are valid for a specified time interval.</span></span> <span data-ttu-id="86a83-132">例如，您可以產生可在一段特定時間內對特定檔案進行唯讀存取的權杖。</span><span class="sxs-lookup"><span data-stu-id="86a83-132">For example, you can generate a token with read-only access to a particular file for a specific period of time.</span></span> <span data-ttu-id="86a83-133">任何人只要擁有此 URL，就可以在其有效時間內，直接從任何網頁瀏覽器存取檔案。</span><span class="sxs-lookup"><span data-stu-id="86a83-133">Anyone who possesses this url can access the file directly from any web browser while it is valid.</span></span> <span data-ttu-id="86a83-134">從儲存體總管之類的 UI 就能輕鬆產生 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="86a83-134">SAS keys can be easily generated from UI like Storage Explorer.</span></span>

* <span data-ttu-id="86a83-135">**問：可以對共用內的資料夾指定唯讀或唯寫權限嗎？**</span><span class="sxs-lookup"><span data-stu-id="86a83-135">**Q. Is it possible to specify read-only or write-only permissions on folders within the share?**</span></span>
    
    <span data-ttu-id="86a83-136">如果是透過 SMB 掛接檔案共用，則您對權限沒有此層級的控制。</span><span class="sxs-lookup"><span data-stu-id="86a83-136">You don't have this level of control over permissions if you mount the file share via SMB.</span></span> <span data-ttu-id="86a83-137">不過，您可以透過 REST API 或用戶端程式庫來建立共用存取簽章 (SAS)，以達到此目的。</span><span class="sxs-lookup"><span data-stu-id="86a83-137">However, you can achieve this by creating a shared access signature (SAS) via the REST API or client libraries.</span></span>  

* <span data-ttu-id="86a83-138">**問：如何啟用 Azure 檔案儲存體的伺服器端加密？**</span><span class="sxs-lookup"><span data-stu-id="86a83-138">**Q. How can I enable Server Side encryption for Azure File storage?**</span></span>

    <span data-ttu-id="86a83-139">Azure 檔案儲存體的[伺服器端加密](storage-service-encryption.md)在所有區域和公用與國內雲端公開上市。</span><span class="sxs-lookup"><span data-stu-id="86a83-139">[Server Side Encryption](storage-service-encryption.md) for Azure File storage is generally available in all regions and public and national clouds.</span></span> <span data-ttu-id="86a83-140">您可以使用 [Azure 入口網站](https://portal.azure.com/)、[Microsoft Azure 儲存體資源提供者 API](/rest/api/storagerp/storageaccounts)、[Azure PowerShell](https://msdn.microsoft.com/library/azure/mt607151.aspx) 或 [Azure CLI](storage-azure-cli.md)，為 Azure 檔案儲存體啟用 SSE。</span><span class="sxs-lookup"><span data-stu-id="86a83-140">You can enable SSE for Azure File storage using [Azure portal](https://portal.azure.com/),[Microsoft Azure Storage Resource Provider API](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) or [Azure CLI](storage-azure-cli.md).</span></span>
    
    <span data-ttu-id="86a83-141">啟用 Azure 檔案儲存體上的 SSE 之後，該儲存體帳戶中寫入檔案儲存體的所有新資料將會自動加密。</span><span class="sxs-lookup"><span data-stu-id="86a83-141">After enabling SSE on Azure File storage, any new data written to the file storage in that storage account will be automatically encrypted.</span></span> <span data-ttu-id="86a83-142">這項功能適用於現有或新的儲存體帳戶中，寫入現有或新共用的所有新資料。</span><span class="sxs-lookup"><span data-stu-id="86a83-142">This feature is available for all new data written to existing or new shares in an existing or new storage account.</span></span> <span data-ttu-id="86a83-143">此用此功能不會額外收費。</span><span class="sxs-lookup"><span data-stu-id="86a83-143">There is no additional charge for enabling this feature.</span></span> <span data-ttu-id="86a83-144">深入了解[如何在 Azure 檔案儲存體上啟用 SSE](storage-service-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="86a83-144">Learn more on [how to enable SSE on Azure File storage](storage-service-encryption.md).</span></span>

* <span data-ttu-id="86a83-145">**問：Azure 檔案儲存體是否支援 Active Directory 型驗證？**</span><span class="sxs-lookup"><span data-stu-id="86a83-145">**Q. Is Active Directory-based authentication supported by Azure File storage?**</span></span>
   
    <span data-ttu-id="86a83-146">我們目前不支援 AD 式驗證或 ACL，但在我們的功能要求清單中卻有它。</span><span class="sxs-lookup"><span data-stu-id="86a83-146">We currently do not support AD-based authentication or ACLs, but do have it in our list of feature requests.</span></span> <span data-ttu-id="86a83-147">目前，Azure 儲存體帳戶金鑰可用來提供檔案共用的驗證。</span><span class="sxs-lookup"><span data-stu-id="86a83-147">For now, the Azure Storage account keys are used to provide authentication to the file share.</span></span> <span data-ttu-id="86a83-148">我們的確提供透過 REST API 或用戶端程式庫使用共用存取簽章 (SAS) 的因應措施。</span><span class="sxs-lookup"><span data-stu-id="86a83-148">We do offer a workaround using shared access signatures (SAS) via the REST API or the client libraries.</span></span> <span data-ttu-id="86a83-149">使用 SAS 時，您可以產生在一段時間內都是有效的具有特定權限的權杖。</span><span class="sxs-lookup"><span data-stu-id="86a83-149">Using SAS, you can generate tokens with specific permissions that are valid for a specified time interval.</span></span> <span data-ttu-id="86a83-150">例如，您可以產生具有指定檔案唯讀存取權並在 10 分鐘到期的權杖。</span><span class="sxs-lookup"><span data-stu-id="86a83-150">For example, you can generate a token with read-only access to a given file with 10 minutes expiry.</span></span> <span data-ttu-id="86a83-151">擁有此權杖的任何人，在 10 分鐘的有效時間內具有該檔案的唯讀存取權。</span><span class="sxs-lookup"><span data-stu-id="86a83-151">Anyone who possesses this token while it is valid has read-only access to that file for those 10 minutes.</span></span>
   
    <span data-ttu-id="86a83-152">僅透過 REST API 或用戶端程式庫才支援 SAS。</span><span class="sxs-lookup"><span data-stu-id="86a83-152">SAS is only supported via the REST API or client libraries.</span></span> <span data-ttu-id="86a83-153">透過 SMB 通訊協定掛接檔案共用時，您無法使用 SAS 來委派其內容的存取。</span><span class="sxs-lookup"><span data-stu-id="86a83-153">When you mount the file share via the SMB protocol, you can't use a SAS to delegate access to its contents.</span></span> 
    
* <span data-ttu-id="86a83-154">**問：Azure 檔案儲存體支援哪些資料合規性原則？**</span><span class="sxs-lookup"><span data-stu-id="86a83-154">**Q. What are the data compliance policies supported for Azure File storage?**</span></span>

   <span data-ttu-id="86a83-155">Azure 檔案儲存體會在與 Azure 儲存體中其他儲存體服務相同的儲存體架構之上執行，並套用相同的資料合規性原則。</span><span class="sxs-lookup"><span data-stu-id="86a83-155">Azure File Storage runs on top of the same storage architecture as other storage services in Azure Storage and applies the same data compliance policies.</span></span> <span data-ttu-id="86a83-156">如需 Azure 儲存體資料合規性的詳細資訊，您可以下載並參考 [Microsoft Azure 資料保護文件](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="86a83-156">More information on Azure Storage data compliance, you can download and refer to [Microsoft Azure Data Protection document](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).</span></span>

## <a name="on-premises-access"></a><span data-ttu-id="86a83-157">內部部署存取</span><span class="sxs-lookup"><span data-stu-id="86a83-157">On-Premises Access</span></span>

* <span data-ttu-id="86a83-158">**問：必須使用 Azure ExpressRoute 從內部部署 VM 連線到 Azure 檔案儲存體嗎？**</span><span class="sxs-lookup"><span data-stu-id="86a83-158">**Q.Do I have to use Azure ExpressRoute to connect to Azure File storage from an on-premises VM?**</span></span>
   
    <span data-ttu-id="86a83-159">編號</span><span class="sxs-lookup"><span data-stu-id="86a83-159">No.</span></span> <span data-ttu-id="86a83-160">如果沒有 ExpressRoute，您仍然可以從內部部署存取檔案共用，只要將連接埠 445 (TCP 輸出) 開啟供網際網路存取即可。</span><span class="sxs-lookup"><span data-stu-id="86a83-160">If you don't have ExpressRoute, you can still access the file share from on-premises as long as you have port 445 (TCP Outbound) open for Internet access.</span></span> <span data-ttu-id="86a83-161">不過，您可以搭配使用 ExpressRoute 與 Azure 檔案儲存體 (如果需要)。</span><span class="sxs-lookup"><span data-stu-id="86a83-161">However, you can use ExpressRoute with Azure File storage if you like.</span></span>

* <span data-ttu-id="86a83-162">**問：如何在本機電腦上掛接 Azure 檔案共用？**</span><span class="sxs-lookup"><span data-stu-id="86a83-162">**Q. How can I mount an Azure File share on my local machine?**</span></span> 
    
    <span data-ttu-id="86a83-163">只要已開啟連接埠 445 (TCP 輸出) 且您的用戶端支援 SMB 3.0 通訊協定 (例如使用 Windows 10 或 Windows Server 2012)，即可透過 SMB 通訊協定掛接檔案共用。</span><span class="sxs-lookup"><span data-stu-id="86a83-163">You can mount the file share via the SMB protocol as long as port 445 (TCP Outbound) is open and your client supports the SMB 3.0 protocol (for example, you're using Windows 10 or Windows Server 2012).</span></span> <span data-ttu-id="86a83-164">請與您的當地 ISP 提供者合作，以將連接埠解除封鎖。</span><span class="sxs-lookup"><span data-stu-id="86a83-164">Please work with your local ISP provider to unblock the port.</span></span> <span data-ttu-id="86a83-165">同時，您可以使用[儲存體總管](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents)檢視檔案。</span><span class="sxs-lookup"><span data-stu-id="86a83-165">In the interim, you can view your files using [Storage Explorer](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).</span></span>


## <a name="billing-and-pricing"></a><span data-ttu-id="86a83-166">計費和定價</span><span class="sxs-lookup"><span data-stu-id="86a83-166">Billing and Pricing</span></span>
* <span data-ttu-id="86a83-167">**問：Azure VM 和檔案共用之間的網路流量，會計算為向訂用帳戶收費的外部頻寬嗎？**</span><span class="sxs-lookup"><span data-stu-id="86a83-167">**Q. Does the network traffic between an Azure VM and a file share count as external bandwidth that is charged to the subscription?**</span></span>
   
    <span data-ttu-id="86a83-168">如果檔案共用和 VM 位於相同的 Azure 區域，兩者之間的流量是免費的。</span><span class="sxs-lookup"><span data-stu-id="86a83-168">If the file share and VM are in the same Azure region, the traffic between them is free.</span></span> <span data-ttu-id="86a83-169">如果位於不同的區域，兩者之間的流量會以外部頻寬收費。</span><span class="sxs-lookup"><span data-stu-id="86a83-169">If they are in different regions, the traffic between them will be charged as external bandwidth.</span></span>

## <a name="backup"></a><span data-ttu-id="86a83-170">備份</span><span class="sxs-lookup"><span data-stu-id="86a83-170">Backup</span></span>

* <span data-ttu-id="86a83-171">**問：如何備份我的 Azure 檔案共用？**</span><span class="sxs-lookup"><span data-stu-id="86a83-171">**Q. How do I backup my Azure File Share?**</span></span>
    
    <span data-ttu-id="86a83-172">您可以使用 AzCopy、RoboCopy，或是可備份已掛接檔案共用的協力廠商備份工具。</span><span class="sxs-lookup"><span data-stu-id="86a83-172">You can use AzCopy, RoboCopy, or a 3rd party backup tool that can backup a mounted file share.</span></span> <span data-ttu-id="86a83-173">我們預期在不久的將來能夠擷取檔案共用的快照，您將能夠使用這項功能來備份 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="86a83-173">We expect to have the ability to take snapshots of File shares in the near future; you will be able to use this feature to backup your Azure File share.</span></span>

## <a name="performance"></a><span data-ttu-id="86a83-174">效能</span><span class="sxs-lookup"><span data-stu-id="86a83-174">Performance</span></span>

* <span data-ttu-id="86a83-175">**問：Azure 檔案儲存體的調整限制有哪些？**</span><span class="sxs-lookup"><span data-stu-id="86a83-175">**Q. What are the scale limits of Azure File storage?**</span></span>
    <span data-ttu-id="86a83-176">如需 Azure 檔案儲存體延展性和效能目標的資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files)。</span><span class="sxs-lookup"><span data-stu-id="86a83-176">For information on scalability and performance targets of Azure File storage, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).</span></span>

* <span data-ttu-id="86a83-177">**問：嘗試將檔案解壓縮到 Azure 檔案儲存體時，執行速度很緩慢。我該怎麼辦？**</span><span class="sxs-lookup"><span data-stu-id="86a83-177">**Q. My performance was slow when trying to unzip files into Azure File storage. What should I do?**</span></span>
    
    <span data-ttu-id="86a83-178">若要將大量檔案傳輸到 Azure 檔案儲存體，建議您使用 AzCopy (Windows、Linux/Unix 預覽版) 或 Azure PowerShell，因為這些工具已針對網路傳輸最佳化。</span><span class="sxs-lookup"><span data-stu-id="86a83-178">To transfer large numbers of files into Azure File storage, we recommend that you use AzCopy(Windows, Preview for Linux/Unix) or Azure Powershell as these tools have been optimized for network transfer.</span></span>

* <span data-ttu-id="86a83-179">**問：已發行哪些修補程式來修正 Azure 檔案儲存體的效能變慢問題？**</span><span class="sxs-lookup"><span data-stu-id="86a83-179">**Q. What patches has been released to fix slow-performance issue with Azure File storage?**</span></span>
    
    <span data-ttu-id="86a83-180">Windows 小組最近發行了修補程式，以修正當客戶從 Windows 8.1 或 Windows Server 2012 R2 存取 Azure 檔案儲存體時效能變慢的問題。</span><span class="sxs-lookup"><span data-stu-id="86a83-180">The Windows team recently released a patch to fix a slow performance issue when the customer accesses Azure File storage from Windows 8.1 or Windows Server 2012 R2.</span></span> <span data-ttu-id="86a83-181">如需詳細資訊，請查看相關聯的知識庫文章：[當您從 Windows 8.1 或 Server 2012 R2 存取 Azure 檔案儲存體時效能變慢](https://support.microsoft.com/kb/3114025)。</span><span class="sxs-lookup"><span data-stu-id="86a83-181">For more information, please check out the associated KB article, [Slow performance when you access Azure File storage from Windows 8.1 or Server 2012 R2](https://support.microsoft.com/kb/3114025).</span></span>

## <a name="features-and-interoperability-with-other-services"></a><span data-ttu-id="86a83-182">與其他服務的功能互通性</span><span class="sxs-lookup"><span data-stu-id="86a83-182">Features and Interoperability with other services</span></span>
* <span data-ttu-id="86a83-183">**問：容錯移轉叢集的「檔案共用見證」是否為 Azure 檔案儲存體的其中一個使用案例？**</span><span class="sxs-lookup"><span data-stu-id="86a83-183">**Q. Is a "File Share Witness" for a failover cluster one of the use cases for Azure File storage?**</span></span>
   
    <span data-ttu-id="86a83-184">目前不受支援。</span><span class="sxs-lookup"><span data-stu-id="86a83-184">This is not currently supported.</span></span>

* <span data-ttu-id="86a83-185">**問：REST API 中是否有重新命名作業？**</span><span class="sxs-lookup"><span data-stu-id="86a83-185">**Q. Is there a rename operation in the REST API?**</span></span>
   
    <span data-ttu-id="86a83-186">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="86a83-186">Not at this time.</span></span>

* <span data-ttu-id="86a83-187">**問：可以有巢狀共用，換句話說，共用下的共用嗎？**</span><span class="sxs-lookup"><span data-stu-id="86a83-187">**Q. Can you have nested shares, in other words, a share under a share?**</span></span>
    
    <span data-ttu-id="86a83-188">編號</span><span class="sxs-lookup"><span data-stu-id="86a83-188">No.</span></span> <span data-ttu-id="86a83-189">檔案共用是您可以掛接的虛擬驅動程式，因此不支援巢狀共用。</span><span class="sxs-lookup"><span data-stu-id="86a83-189">The file share is the virtual driver that you can mount, so nested shares are not supported.</span></span>

* <span data-ttu-id="86a83-190">**問：搭配 IBM MQ 使用 Azure 檔案儲存體**</span><span class="sxs-lookup"><span data-stu-id="86a83-190">**Q. Using Azure File storage with IBM MQ**</span></span>
    
    <span data-ttu-id="86a83-191">IBM 已發行文件來指引 IBM MQ 客戶設定 Azure 檔案儲存體與其服務。</span><span class="sxs-lookup"><span data-stu-id="86a83-191">IBM has released a document to guide IBM MQ customers when configuring Azure File storage with their service.</span></span> <span data-ttu-id="86a83-192">如需詳細資訊，請查看 [如何使用 Microsoft Azure 檔案服務來設定 IBM MQ 多重執行個體佇列管理員](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service)。</span><span class="sxs-lookup"><span data-stu-id="86a83-192">For more information, please check out [How to setup IBM MQ Multi instance queue manager with Microsoft Azure File Service](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="86a83-193">疑難排解</span><span class="sxs-lookup"><span data-stu-id="86a83-193">Troubleshooting</span></span>
* <span data-ttu-id="86a83-194">**問：如何針對 Azure 檔案儲存體錯誤進行疑難排解？**</span><span class="sxs-lookup"><span data-stu-id="86a83-194">**Q. How do I troubleshoot Azure File storage errors?**</span></span>
    
    <span data-ttu-id="86a83-195">您可以參考 [Azure 檔案儲存體疑難排解文章](storage-troubleshoot-file-connection-problems.md)以取得端對端疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="86a83-195">You can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span> 


## <a name="see-also"></a><span data-ttu-id="86a83-196">另請參閱</span><span class="sxs-lookup"><span data-stu-id="86a83-196">See also</span></span>
<span data-ttu-id="86a83-197">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="86a83-197">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="86a83-198">概念性文章和影片</span><span class="sxs-lookup"><span data-stu-id="86a83-198">Conceptual articles and videos</span></span>
* [<span data-ttu-id="86a83-199">Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統</span><span class="sxs-lookup"><span data-stu-id="86a83-199">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="86a83-200">如何搭配使用 Azure 檔案儲存體與 Linux</span><span class="sxs-lookup"><span data-stu-id="86a83-200">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="86a83-201">檔案儲存體的工具支援</span><span class="sxs-lookup"><span data-stu-id="86a83-201">Tooling support for File storage</span></span>
* [<span data-ttu-id="86a83-202">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="86a83-202">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="86a83-203">如何搭配使用 AzCopy 與 Microsoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="86a83-203">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="86a83-204">使用 Azure CLI 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="86a83-204">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="86a83-205">針對 Azure 檔案儲存體的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="86a83-205">Troubleshooting Azure File storage problems</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a><span data-ttu-id="86a83-206">部落格文章</span><span class="sxs-lookup"><span data-stu-id="86a83-206">Blog posts</span></span>
* [<span data-ttu-id="86a83-207">Azure 檔案儲存體現已公開推出</span><span class="sxs-lookup"><span data-stu-id="86a83-207">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="86a83-208">Azure 檔案儲存體內部</span><span class="sxs-lookup"><span data-stu-id="86a83-208">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="86a83-209">Microsoft Azure 檔案服務簡介</span><span class="sxs-lookup"><span data-stu-id="86a83-209">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* <span data-ttu-id="86a83-210">[Migrating data to Azure File storage](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/) (將資料移轉至 Azure 檔案儲存體)</span><span class="sxs-lookup"><span data-stu-id="86a83-210">[Migrating data to Azure File storage](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)</span></span>

### <a name="reference"></a><span data-ttu-id="86a83-211">參考</span><span class="sxs-lookup"><span data-stu-id="86a83-211">Reference</span></span>
* [<span data-ttu-id="86a83-212">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="86a83-212">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="86a83-213">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="86a83-213">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
