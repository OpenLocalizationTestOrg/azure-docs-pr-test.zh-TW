---
title: "Azure 檔案儲存體相關常見問題的 aaaFrequently |Microsoft 文件"
description: "尋找 toofrequently Azure 檔案儲存體相關常見問題的答案。"
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
ms.openlocfilehash: d8a94fdc77e928dbc6996e1e635cd3527e0c67d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a><span data-ttu-id="bbebc-103">關於 Azure 檔案儲存體的常見問題集</span><span class="sxs-lookup"><span data-stu-id="bbebc-103">Frequently Asked Questions about Azure File storage</span></span>

## <a name="general"></a><span data-ttu-id="bbebc-104">一般</span><span class="sxs-lookup"><span data-stu-id="bbebc-104">General</span></span>
* <span data-ttu-id="bbebc-105">**問：什麼是 Azure 檔案儲存體？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-105">**Q. What is Azure File storage?**</span></span>  
   
    <span data-ttu-id="bbebc-106">Azure 檔案儲存體是 Azure 中的分散式檔案系統。</span><span class="sxs-lookup"><span data-stu-id="bbebc-106">Azure File storage is a distributed file system in Azure.</span></span> <span data-ttu-id="bbebc-107">它提供可讓使用者 toomount hello 存放裝置為原生支援 Azure 虛擬機器或在內部部署電腦上共用的 SMB 通訊協定介面。</span><span class="sxs-lookup"><span data-stu-id="bbebc-107">It provides an SMB protocol interface which allows users toomount hello storage as a native share on supported Azure Virtual Machine or on-premises machine.</span></span>

* <span data-ttu-id="bbebc-108">**問：Azure 檔案儲存體為何很實用？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-108">**Q. Why is Azure File storage useful?**</span></span>  
   
    <span data-ttu-id="bbebc-109">Azure 檔案儲存體可跨多部 VM 和平台存取共用資料。</span><span class="sxs-lookup"><span data-stu-id="bbebc-109">Azure File storage provides shared data access across multiple VMs and platforms.</span></span> <span data-ttu-id="bbebc-110">請參閱太[為什麼 Azure 檔案儲存是很有用](storage-files-introduction.md#why-azure-file-storage-is-useful)。</span><span class="sxs-lookup"><span data-stu-id="bbebc-110">Refer too[Why Azure File storage is useful](storage-files-introduction.md#why-azure-file-storage-is-useful).</span></span>

* <span data-ttu-id="bbebc-111">**問：何時應該使用 Azure 檔案、Azure Blob 或 Azure 磁碟？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-111">**Q. When should I use Azure File vs Azure Blob vs Azure Disk ?**</span></span>  
   
    <span data-ttu-id="bbebc-112">Microsoft Azure 提供數種方式 hello 雲端 toostore 及存取資料。</span><span class="sxs-lookup"><span data-stu-id="bbebc-112">Microsoft Azure provides several ways toostore and access data in hello cloud.</span></span>  
   
    <span data-ttu-id="bbebc-113">Azure 檔案儲存體-提供 SMB 介面、 用戶端程式庫和 REST 介面，允許從任何位置輕鬆地存取 toostored 檔案。</span><span class="sxs-lookup"><span data-stu-id="bbebc-113">Azure File storage - Provides an SMB interface, client libraries, and a REST interface that allows easy access from anywhere toostored files.</span></span>  
   
    <span data-ttu-id="bbebc-114">Azure Blob-提供用戶端程式庫和 REST 介面，可讓非結構化的資料 toobe 存放及存取大規模區塊 blob 中。</span><span class="sxs-lookup"><span data-stu-id="bbebc-114">Azure Blobs - Provides client libraries and a REST interface that allows unstructured data toobe stored and accessed at a massive scale in block blobs.</span></span>  
   
    <span data-ttu-id="bbebc-115">Azure 資料磁碟-提供用戶端程式庫和 REST 介面，可讓資料 toobe 持續儲存和存取從連接的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="bbebc-115">Azure Data Disks - Provides client libraries and a REST interface that allows data toobe persistently stored and accessed from an attached virtual hard disk.</span></span>  
   
    <span data-ttu-id="bbebc-116">進一步了解上[制定時 toouse Azure Blob、 Azure 或 Azure 資料磁碟](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bbebc-116">Learn more on [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)</span></span>

* <span data-ttu-id="bbebc-117">**問：如何開始使用 Azure 檔案儲存體？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-117">**Q. How do I get started using Azure File storage?**</span></span>  
   
    <span data-ttu-id="bbebc-118">您可以從建立 Azure 檔案共用開始。</span><span class="sxs-lookup"><span data-stu-id="bbebc-118">You can start by creating an Azure file share.</span></span> <span data-ttu-id="bbebc-119">您可以建立使用 Azure 入口網站、 hello Azure 儲存體 PowerShell cmdlet、 hello Azure 儲存體用戶端程式庫或 hello Azure 儲存體的 REST API 的 Azure 檔案共用。在本教學課程中，您將學習：</span><span class="sxs-lookup"><span data-stu-id="bbebc-119">You can create Azure File shares using Azure Portal, hello Azure Storage PowerShell cmdlets, hello Azure Storage client libraries, or hello Azure Storage REST API.In this tutorial, you will learn:</span></span>

    * [<span data-ttu-id="bbebc-120">了解如何 toocreate Azure 檔案共用使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="bbebc-120">Learn how toocreate Azure File share using hello Portal</span></span>](storage-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [<span data-ttu-id="bbebc-121">了解如何 toocreate Azure 檔案共用使用 Powershell</span><span class="sxs-lookup"><span data-stu-id="bbebc-121">Learn how toocreate Azure File share using Powershell</span></span>](storage-how-to-create-file-share.md#create-file-share-through-powershell)
    * [<span data-ttu-id="bbebc-122">了解如何 toocreate Azure 檔案共用使用 CLI</span><span class="sxs-lookup"><span data-stu-id="bbebc-122">Learn how toocreate Azure File share using CLI</span></span>](storage-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* <span data-ttu-id="bbebc-123">**問：Azure 檔案儲存體支援何種複寫？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-123">**Q. What replications are supported by Azure File storage?**</span></span>  
   
    <span data-ttu-id="bbebc-124">Azure 檔案儲存體目前只支援 LRS 或 GRS。</span><span class="sxs-lookup"><span data-stu-id="bbebc-124">Azure File storage only supports LRS or GRS right now.</span></span> <span data-ttu-id="bbebc-125">我們計劃 toosupport RA-GRS，但尚無時間表 tooshare。</span><span class="sxs-lookup"><span data-stu-id="bbebc-125">We plan toosupport RA-GRS but there is no timeline tooshare yet.</span></span>

## <a name="security-authentication-and-access-control"></a><span data-ttu-id="bbebc-126">安全性、驗證和存取控制</span><span class="sxs-lookup"><span data-stu-id="bbebc-126">Security, Authentication and Access Control</span></span>

* <span data-ttu-id="bbebc-127">**問：什麼是 Azure 檔案儲存體中的不同方式 tooaccess 檔案？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-127">**Q. What are different ways tooaccess files in Azure File storage?**</span></span>
    
    <span data-ttu-id="bbebc-128">您可以使用 SMB 3.0 通訊協定在本機電腦上掛接 hello 檔案共用，或使用的工具，例如[存放裝置總管](http://storageexplorer.com/)tooaccess 檔案在檔案共用。</span><span class="sxs-lookup"><span data-stu-id="bbebc-128">You can mount hello file share on your local machine using SMB 3.0 protocol or use tools like [Storage Explorer](http://storageexplorer.com/) tooaccess files in your file share.</span></span> <span data-ttu-id="bbebc-129">從您的應用程式，您可以使用儲存體用戶端程式庫、 REST Api 或 Powershell tooaccess Azure 檔案中的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="bbebc-129">From your application, you can use storage client libraries, REST APIs or Powershell tooaccess your files in Azure File share.</span></span>

* <span data-ttu-id="bbebc-130">**問：如何提供使用 web 瀏覽器存取 tooa 特定檔案？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-130">**Q. How can I provide access tooa specific file using a web browser?**</span></span>
    
    <span data-ttu-id="bbebc-131">使用 SAS 時，您可以產生在一段時間內都是有效的具有特定權限的權杖。</span><span class="sxs-lookup"><span data-stu-id="bbebc-131">Using SAS, you can generate tokens with specific permissions that are valid for a specified time interval.</span></span> <span data-ttu-id="bbebc-132">比方說，您可以產生具有唯讀存取 tooa 特定檔案的語彙基元，特定的一段時間。</span><span class="sxs-lookup"><span data-stu-id="bbebc-132">For example, you can generate a token with read-only access tooa particular file for a specific period of time.</span></span> <span data-ttu-id="bbebc-133">擁有此 url 的任何人可以直接從任何網頁瀏覽器存取 hello 檔案，而它有效。</span><span class="sxs-lookup"><span data-stu-id="bbebc-133">Anyone who possesses this url can access hello file directly from any web browser while it is valid.</span></span> <span data-ttu-id="bbebc-134">從儲存體總管之類的 UI 就能輕鬆產生 SAS 金鑰。</span><span class="sxs-lookup"><span data-stu-id="bbebc-134">SAS keys can be easily generated from UI like Storage Explorer.</span></span>

* <span data-ttu-id="bbebc-135">**問：它是可能 toospecify 唯讀或唯寫的資料夾權限內 hello 共用嗎？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-135">**Q. Is it possible toospecify read-only or write-only permissions on folders within hello share?**</span></span>
    
    <span data-ttu-id="bbebc-136">如果裝載 hello 透過 SMB 的檔案共用，您不需要此層級的權限控制。</span><span class="sxs-lookup"><span data-stu-id="bbebc-136">You don't have this level of control over permissions if you mount hello file share via SMB.</span></span> <span data-ttu-id="bbebc-137">不過，您可以達到此目的建立共用的存取簽章 (SAS) 透過 hello REST API 或用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="bbebc-137">However, you can achieve this by creating a shared access signature (SAS) via hello REST API or client libraries.</span></span>  

* <span data-ttu-id="bbebc-138">**問：如何啟用 Azure 檔案儲存體的伺服器端加密？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-138">**Q. How can I enable Server Side encryption for Azure File storage?**</span></span>

    <span data-ttu-id="bbebc-139">Azure 檔案儲存體的[伺服器端加密](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)在所有區域和公用與國內雲端公開上市。</span><span class="sxs-lookup"><span data-stu-id="bbebc-139">[Server Side Encryption](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) for Azure File storage is generally available in all regions and public and national clouds.</span></span> <span data-ttu-id="bbebc-140">您可以使用 [Azure 入口網站](https://portal.azure.com/)、[Microsoft Azure 儲存體資源提供者 API](/rest/api/storagerp/storageaccounts)、[Azure PowerShell](https://msdn.microsoft.com/library/azure/mt607151.aspx) 或 [Azure CLI](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)，為 Azure 檔案儲存體啟用 SSE。</span><span class="sxs-lookup"><span data-stu-id="bbebc-140">You can enable SSE for Azure File storage using [Azure portal](https://portal.azure.com/),[Microsoft Azure Storage Resource Provider API](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) or [Azure CLI](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>
    
    <span data-ttu-id="bbebc-141">啟用 SSE 上 Azure 檔案儲存體之後, 將會自動加密任何新資料寫入 toohello 檔案儲存在該儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bbebc-141">After enabling SSE on Azure File storage, any new data written toohello file storage in that storage account will be automatically encrypted.</span></span> <span data-ttu-id="bbebc-142">這項功能適用於所有新的資料寫入 tooexisting 或新的共用中的現有或新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bbebc-142">This feature is available for all new data written tooexisting or new shares in an existing or new storage account.</span></span> <span data-ttu-id="bbebc-143">此用此功能不會額外收費。</span><span class="sxs-lookup"><span data-stu-id="bbebc-143">There is no additional charge for enabling this feature.</span></span> <span data-ttu-id="bbebc-144">進一步了解上[如何在 Azure 檔案儲存體 tooenable SSE](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bbebc-144">Learn more on [how tooenable SSE on Azure File storage](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

* <span data-ttu-id="bbebc-145">**問：Azure 檔案儲存體是否支援 Active Directory 型驗證？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-145">**Q. Is Active Directory-based authentication supported by Azure File storage?**</span></span>
   
    <span data-ttu-id="bbebc-146">我們目前不支援 AD 式驗證或 ACL，但在我們的功能要求清單中卻有它。</span><span class="sxs-lookup"><span data-stu-id="bbebc-146">We currently do not support AD-based authentication or ACLs, but do have it in our list of feature requests.</span></span> <span data-ttu-id="bbebc-147">現在，hello Azure 儲存體帳戶金鑰是使用的 tooprovide 驗證 toohello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="bbebc-147">For now, hello Azure Storage account keys are used tooprovide authentication toohello file share.</span></span> <span data-ttu-id="bbebc-148">我們提供透過 hello REST API 或 hello 用戶端程式庫中使用共用的存取簽章 (SAS) 因應措施。</span><span class="sxs-lookup"><span data-stu-id="bbebc-148">We do offer a workaround using shared access signatures (SAS) via hello REST API or hello client libraries.</span></span> <span data-ttu-id="bbebc-149">使用 SAS 時，您可以產生在一段時間內都是有效的具有特定權限的權杖。</span><span class="sxs-lookup"><span data-stu-id="bbebc-149">Using SAS, you can generate tokens with specific permissions that are valid for a specified time interval.</span></span> <span data-ttu-id="bbebc-150">例如，您可以產生語彙基元具有唯讀存取 tooa 提供與 10 分鐘過期的檔案。</span><span class="sxs-lookup"><span data-stu-id="bbebc-150">For example, you can generate a token with read-only access tooa given file with 10 minutes expiry.</span></span> <span data-ttu-id="bbebc-151">擁有這個語彙基元有效時的任何人都有唯讀存取 toothat 檔案的 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="bbebc-151">Anyone who possesses this token while it is valid has read-only access toothat file for those 10 minutes.</span></span>
   
    <span data-ttu-id="bbebc-152">透過 hello REST API 或用戶端程式庫只支援 SAS。</span><span class="sxs-lookup"><span data-stu-id="bbebc-152">SAS is only supported via hello REST API or client libraries.</span></span> <span data-ttu-id="bbebc-153">當您掛接 hello 透過 hello SMB 通訊協定的檔案共用時，您無法使用 SAS toodelegate 存取 tooits 內容。</span><span class="sxs-lookup"><span data-stu-id="bbebc-153">When you mount hello file share via hello SMB protocol, you can't use a SAS toodelegate access tooits contents.</span></span> 
    
* <span data-ttu-id="bbebc-154">**問：什麼是 Azure 檔案儲存體支援 hello 資料相容性原則？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-154">**Q. What are hello data compliance policies supported for Azure File storage?**</span></span>

   <span data-ttu-id="bbebc-155">Azure 檔案儲存體執行最上層的其他儲存體服務在 Azure 儲存體和適用於 hello hello 相同的儲存體架構相同的資料相容性原則。</span><span class="sxs-lookup"><span data-stu-id="bbebc-155">Azure File Storage runs on top of hello same storage architecture as other storage services in Azure Storage and applies hello same data compliance policies.</span></span> <span data-ttu-id="bbebc-156">Azure 儲存體資料相容性的詳細資訊，您可以下載並參照太[Microsoft Azure 資料保護文件](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="bbebc-156">More information on Azure Storage data compliance, you can download and refer too[Microsoft Azure Data Protection document](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).</span></span>

## <a name="on-premises-access"></a><span data-ttu-id="bbebc-157">內部部署存取</span><span class="sxs-lookup"><span data-stu-id="bbebc-157">On-Premises Access</span></span>

* <span data-ttu-id="bbebc-158">**我有 toouse Azure ExpressRoute tooconnect tooAzure 檔案存放裝置從內部部署 VM 的 Q.Do 嗎？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-158">**Q.Do I have toouse Azure ExpressRoute tooconnect tooAzure File storage from an on-premises VM?**</span></span>
   
    <span data-ttu-id="bbebc-159">否。</span><span class="sxs-lookup"><span data-stu-id="bbebc-159">No.</span></span> <span data-ttu-id="bbebc-160">如果您不需要 ExpressRoute，您仍可存取 hello 檔案共用從內部部署，只要您有連接埠 445 （TCP 輸出） 開放網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="bbebc-160">If you don't have ExpressRoute, you can still access hello file share from on-premises as long as you have port 445 (TCP Outbound) open for Internet access.</span></span> <span data-ttu-id="bbebc-161">不過，您可以搭配使用 ExpressRoute 與 Azure 檔案儲存體 (如果需要)。</span><span class="sxs-lookup"><span data-stu-id="bbebc-161">However, you can use ExpressRoute with Azure File storage if you like.</span></span>

* <span data-ttu-id="bbebc-162">**問：如何在本機電腦上掛接 Azure 檔案共用？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-162">**Q. How can I mount an Azure File share on my local machine?**</span></span> 
    
    <span data-ttu-id="bbebc-163">您可以掛接 hello 透過 hello SMB 通訊協定的檔案共用，只要已開啟連接埠 445 （TCP 輸出），而且您的用戶端支援 hello SMB 3.0 通訊協定 （例如，您使用 Windows 10 或 Windows Server 2012）。</span><span class="sxs-lookup"><span data-stu-id="bbebc-163">You can mount hello file share via hello SMB protocol as long as port 445 (TCP Outbound) is open and your client supports hello SMB 3.0 protocol (for example, you're using Windows 10 or Windows Server 2012).</span></span> <span data-ttu-id="bbebc-164">請使用本機 ISP 提供者 toounblock hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="bbebc-164">Please work with your local ISP provider toounblock hello port.</span></span> <span data-ttu-id="bbebc-165">在 hello 過渡版，您可以檢視您使用的檔案[存放裝置總管](../../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents)。</span><span class="sxs-lookup"><span data-stu-id="bbebc-165">In hello interim, you can view your files using [Storage Explorer](../../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).</span></span>


## <a name="billing-and-pricing"></a><span data-ttu-id="bbebc-166">計費和定價</span><span class="sxs-lookup"><span data-stu-id="bbebc-166">Billing and Pricing</span></span>
* <span data-ttu-id="bbebc-167">**問：沒有外部 toohello 訂用帳戶計費的頻寬 hello Azure VM 與檔案共用計數之間的網路流量？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-167">**Q. Does hello network traffic between an Azure VM and a file share count as external bandwidth that is charged toohello subscription?**</span></span>
   
    <span data-ttu-id="bbebc-168">如果 hello 檔案共用和 VM 在 hello 相同 Azure 地區，hello 兩者間傳輸是免費的。</span><span class="sxs-lookup"><span data-stu-id="bbebc-168">If hello file share and VM are in hello same Azure region, hello traffic between them is free.</span></span> <span data-ttu-id="bbebc-169">如果它們是在不同的區域，hello 它們之間的流量將支付外部頻寬。</span><span class="sxs-lookup"><span data-stu-id="bbebc-169">If they are in different regions, hello traffic between them will be charged as external bandwidth.</span></span>

## <a name="backup"></a><span data-ttu-id="bbebc-170">備份</span><span class="sxs-lookup"><span data-stu-id="bbebc-170">Backup</span></span>

* <span data-ttu-id="bbebc-171">**問：如何備份我的 Azure 檔案共用？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-171">**Q. How do I backup my Azure File Share?**</span></span>
    
    <span data-ttu-id="bbebc-172">您可以使用 AzCopy、RoboCopy，或是可備份已掛接檔案共用的協力廠商備份工具。</span><span class="sxs-lookup"><span data-stu-id="bbebc-172">You can use AzCopy, RoboCopy, or a 3rd party backup tool that can backup a mounted file share.</span></span> <span data-ttu-id="bbebc-173">我們預期未來; 接近 hello toohave hello 能力 tootake 的快照集檔案共用您將會無法 toouse 此功能 toobackup Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="bbebc-173">We expect toohave hello ability tootake snapshots of File shares in hello near future; you will be able toouse this feature toobackup your Azure File share.</span></span>

## <a name="performance"></a><span data-ttu-id="bbebc-174">效能</span><span class="sxs-lookup"><span data-stu-id="bbebc-174">Performance</span></span>

* <span data-ttu-id="bbebc-175">**問：什麼是 Azure 檔案儲存體的 hello 規模限制？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-175">**Q. What are hello scale limits of Azure File storage?**</span></span>
    <span data-ttu-id="bbebc-176">如需 Azure 檔案儲存體延展性和效能目標的資訊，請參閱 [Azure 儲存體延展性和效能目標](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#scalability-targets-for-blobs-queues-tables-and-files)。</span><span class="sxs-lookup"><span data-stu-id="bbebc-176">For information on scalability and performance targets of Azure File storage, see [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#scalability-targets-for-blobs-queues-tables-and-files).</span></span>

* <span data-ttu-id="bbebc-177">**問：嘗試 toounzip 檔案到 Azure 檔案儲存體時，我效能而變慢。我該怎麼辦？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-177">**Q. My performance was slow when trying toounzip files into Azure File storage. What should I do?**</span></span>
    
    <span data-ttu-id="bbebc-178">tootransfer 大量的檔案到 Azure 檔案儲存體，我們建議為這些工具都已最佳化的網路傳輸使用 AzCopy （Windows、 Linux/Unix 的預覽） 或 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="bbebc-178">tootransfer large numbers of files into Azure File storage, we recommend that you use AzCopy(Windows, Preview for Linux/Unix) or Azure Powershell as these tools have been optimized for network transfer.</span></span>

* <span data-ttu-id="bbebc-179">**問：修補程式已被釋放 toofix 緩慢效能問題，Azure 檔案儲存體？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-179">**Q. What patches has been released toofix slow-performance issue with Azure File storage?**</span></span>
    
    <span data-ttu-id="bbebc-180">hello 客戶從 Windows 8.1 或 Windows Server 2012 R2 來存取 Azure 檔案儲存體時，hello Windows 小組最近已發行的修補程式 toofix 效能降低的問題。</span><span class="sxs-lookup"><span data-stu-id="bbebc-180">hello Windows team recently released a patch toofix a slow performance issue when hello customer accesses Azure File storage from Windows 8.1 or Windows Server 2012 R2.</span></span> <span data-ttu-id="bbebc-181">如需詳細資訊，請簽出 hello 相關知識庫文章[降低效能，當您從 Windows 8.1 或 Server 2012 R2 中存取 Azure 檔案儲存體](https://support.microsoft.com/kb/3114025)。</span><span class="sxs-lookup"><span data-stu-id="bbebc-181">For more information, please check out hello associated KB article, [Slow performance when you access Azure File storage from Windows 8.1 or Server 2012 R2](https://support.microsoft.com/kb/3114025).</span></span>

## <a name="features-and-interoperability-with-other-services"></a><span data-ttu-id="bbebc-182">與其他服務的功能互通性</span><span class="sxs-lookup"><span data-stu-id="bbebc-182">Features and Interoperability with other services</span></span>
* <span data-ttu-id="bbebc-183">**問：是 「 檔案共用見證"hello 的其中一個容錯移轉叢集的 Azure 檔案儲存體的使用案例？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-183">**Q. Is a "File Share Witness" for a failover cluster one of hello use cases for Azure File storage?**</span></span>
   
    <span data-ttu-id="bbebc-184">目前不受支援。</span><span class="sxs-lookup"><span data-stu-id="bbebc-184">This is not currently supported.</span></span>

* <span data-ttu-id="bbebc-185">**問：有 hello REST API 中的重新命名作業嗎？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-185">**Q. Is there a rename operation in hello REST API?**</span></span>
   
    <span data-ttu-id="bbebc-186">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="bbebc-186">Not at this time.</span></span>

* <span data-ttu-id="bbebc-187">**問：可以有巢狀共用，換句話說，共用下的共用嗎？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-187">**Q. Can you have nested shares, in other words, a share under a share?**</span></span>
    
    <span data-ttu-id="bbebc-188">否。</span><span class="sxs-lookup"><span data-stu-id="bbebc-188">No.</span></span> <span data-ttu-id="bbebc-189">hello 檔案共用是 hello 虛擬驅動程式，您可以掛接，因此不支援巢狀的共用。</span><span class="sxs-lookup"><span data-stu-id="bbebc-189">hello file share is hello virtual driver that you can mount, so nested shares are not supported.</span></span>

* <span data-ttu-id="bbebc-190">**問：搭配 IBM MQ 使用 Azure 檔案儲存體**</span><span class="sxs-lookup"><span data-stu-id="bbebc-190">**Q. Using Azure File storage with IBM MQ**</span></span>
    
    <span data-ttu-id="bbebc-191">設定 Azure 檔案儲存體服務時，IBM 已發行的文件 tooguide IBM MQ 客戶。</span><span class="sxs-lookup"><span data-stu-id="bbebc-191">IBM has released a document tooguide IBM MQ customers when configuring Azure File storage with their service.</span></span> <span data-ttu-id="bbebc-192">如需詳細資訊，請簽出[如何 toosetup IBM MQ 多重執行個體使用 Microsoft Azure 檔案服務的佇列管理員](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service)。</span><span class="sxs-lookup"><span data-stu-id="bbebc-192">For more information, please check out [How toosetup IBM MQ Multi instance queue manager with Microsoft Azure File Service](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="bbebc-193">疑難排解</span><span class="sxs-lookup"><span data-stu-id="bbebc-193">Troubleshooting</span></span>
* <span data-ttu-id="bbebc-194">**問：如何針對 Azure 檔案儲存體錯誤進行疑難排解？**</span><span class="sxs-lookup"><span data-stu-id="bbebc-194">**Q. How do I troubleshoot Azure File storage errors?**</span></span>
    
    <span data-ttu-id="bbebc-195">您可以使用參照太[Azure 檔案儲存體疑難排解文章](storage-troubleshoot-windows-file-connection-problems.md)的端對端疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="bbebc-195">You can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-windows-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span> 


## <a name="see-also"></a><span data-ttu-id="bbebc-196">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bbebc-196">See also</span></span>
<span data-ttu-id="bbebc-197">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bbebc-197">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="bbebc-198">概念性文章和影片</span><span class="sxs-lookup"><span data-stu-id="bbebc-198">Conceptual articles and videos</span></span>
* [<span data-ttu-id="bbebc-199">Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統</span><span class="sxs-lookup"><span data-stu-id="bbebc-199">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="bbebc-200">如何 toouse Linux 的 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="bbebc-200">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="bbebc-201">檔案儲存體的工具支援</span><span class="sxs-lookup"><span data-stu-id="bbebc-201">Tooling support for File storage</span></span>
* [<span data-ttu-id="bbebc-202">如何 toouse AzCopy 與 Microsoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="bbebc-202">How toouse AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="bbebc-203">使用 Azure CLI hello 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="bbebc-203">Using hello Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="bbebc-204">針對 Azure 檔案儲存體的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="bbebc-204">Troubleshooting Azure File storage problems</span></span>](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a><span data-ttu-id="bbebc-205">部落格文章</span><span class="sxs-lookup"><span data-stu-id="bbebc-205">Blog posts</span></span>
* [<span data-ttu-id="bbebc-206">Azure 檔案儲存體現已公開推出</span><span class="sxs-lookup"><span data-stu-id="bbebc-206">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="bbebc-207">Azure 檔案儲存體內部</span><span class="sxs-lookup"><span data-stu-id="bbebc-207">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="bbebc-208">Microsoft Azure 檔案服務簡介</span><span class="sxs-lookup"><span data-stu-id="bbebc-208">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="bbebc-209">移轉資料 tooAzure 檔案存放裝置</span><span class="sxs-lookup"><span data-stu-id="bbebc-209">Migrating data tooAzure File storage</span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="bbebc-210">參考</span><span class="sxs-lookup"><span data-stu-id="bbebc-210">Reference</span></span>
* [<span data-ttu-id="bbebc-211">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="bbebc-211">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="bbebc-212">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="bbebc-212">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
