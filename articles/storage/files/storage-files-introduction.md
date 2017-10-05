---
title: "Azure 檔案儲存體簡介 | Microsoft Docs"
description: "Azure 檔案儲存體簡介，而該儲存體可在 Microsoft Cloud 中提供網路檔案共用"
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
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 498af5cffb76e026c9a87127cab238f0f23b668a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-file-storage"></a><span data-ttu-id="63da4-103">Azure 檔案儲存體簡介</span><span class="sxs-lookup"><span data-stu-id="63da4-103">Introduction to Azure File storage</span></span>

<span data-ttu-id="63da4-104">Azure 檔案儲存體在雲端中提供網路檔案共用功能，並使用業界標準[伺服器訊息區塊 (SMB) 通訊協定](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx)和 [一般網際網路檔案系統 (CIFS)](https://technet.microsoft.com/library/cc939973.aspx)。</span><span class="sxs-lookup"><span data-stu-id="63da4-104">Azure File storage offers network file shares in the cloud using the industry standard [Server Message Block (SMB) Protocol](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) and [Common Internet File System (CIFS)](https://technet.microsoft.com/library/cc939973.aspx).</span></span> <span data-ttu-id="63da4-105">執行 Windows、macOS 或 Linux 的 Azure 虛擬機器和內部部署可同時掛接 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="63da4-105">Azure File shares can be mounted concurrently by Azure Virtual Machines and on-premises deployments running Windows, macOS, or Linux.</span></span> <span data-ttu-id="63da4-106">一般用途儲存體帳戶可讓您存取 Azure 檔案儲存體、Azure Blob 儲存體和 Azure 佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="63da4-106">A general-purpose storage account gives you access to Azure File storage, Azure Blob storage, and Azure Queue storage.</span></span>

## <a name="videos"></a><span data-ttu-id="63da4-107">影片</span><span class="sxs-lookup"><span data-stu-id="63da4-107">Videos</span></span>
| <span data-ttu-id="63da4-108">介紹 Azure 檔案儲存體 (27 分鐘)</span><span class="sxs-lookup"><span data-stu-id="63da4-108">Introducing Azure File storage (27m)</span></span> | <span data-ttu-id="63da4-109">Azure 檔案儲存體教學課程 (5 分鐘)</span><span class="sxs-lookup"><span data-stu-id="63da4-109">Azure File storage Tutorial (5 minutes)</span></span>  |
|-|-|
| <span data-ttu-id="63da4-110">[![介紹 Azure 檔案儲存體影片的螢幕錄製影片 - 按一下以播放！](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs)</span><span class="sxs-lookup"><span data-stu-id="63da4-110">[![Screencast of the Introducing Azure File storage video - click to play!](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs)</span></span> | <span data-ttu-id="63da4-111">[![Azure 檔案儲存體教學課程的螢幕錄製影片 - 按一下以播放！](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/)</span><span class="sxs-lookup"><span data-stu-id="63da4-111">[![Screencast of the Azure File storage Tutorial - click to play!](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/)</span></span> |

## <a name="why-azure-file-storage-is-useful"></a><span data-ttu-id="63da4-112">Azure 檔案儲存體為何很實用</span><span class="sxs-lookup"><span data-stu-id="63da4-112">Why Azure File storage is useful</span></span>

<span data-ttu-id="63da4-113">Azure 檔案儲存體可讓您使用沒有作業系統的雲端檔案共用，取代裝載於內部部署或在雲端中的 Windows Server、Linux 或以 NAS 為基礎的檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="63da4-113">Azure File storage allows you to replace Windows Server, Linux, or NAS-based file servers hosted on-premises or in the cloud with an OS-free cloud file share.</span></span> <span data-ttu-id="63da4-114">Azure 檔案儲存體具有下列好處：</span><span class="sxs-lookup"><span data-stu-id="63da4-114">Azure File storage has the following benefits:</span></span>

* <span data-ttu-id="63da4-115">**共用存取** Azure 檔案共用支援業界標準 SMB 通訊協定，這表示您可以使用 Azure 檔案共用順暢地取代您的內部檔案共用，而不需擔心應用程式相容性。</span><span class="sxs-lookup"><span data-stu-id="63da4-115">**Shared access** Azure File shares support the industry standard SMB protocol, meaning you can seamlessly replace your on-premises file shares with Azure File shares without worrying about application compatibility.</span></span> <span data-ttu-id="63da4-116">能夠從多部電腦和應用程式/執行個體存取檔案共用，是 Azure 檔案儲存體的重大優勢。</span><span class="sxs-lookup"><span data-stu-id="63da4-116">Being able to access a file share from multiple machines and applications/instances is a significant advantage with Azure File storage.</span></span>

* <span data-ttu-id="63da4-117">**完全受管理** 不需管理硬體或 OS，即可建立 Azure 檔案共用，這表示您不必透過重大安全性升級或替換故障硬碟來處理修補伺服器作業系統。</span><span class="sxs-lookup"><span data-stu-id="63da4-117">**Fully Managed** Azure File shares can be created without the need to manage hardware or an OS, which means you don't have to deal with patching the server OS with critical security upgrades or replacing faulty hard disks.</span></span>

* <span data-ttu-id="63da4-118">**指令碼和工具** 管理 Azure 應用程式時，可以使用 PowerShell Cmdlet 和 Azure CLI 來建立、掛接和管理 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="63da4-118">**Scripting and Tooling** PowerShell cmdlets and Azure CLI can be used to create, mount, and manage Azure File shares as part of the administration of Azure applications.</span></span> <span data-ttu-id="63da4-119">您可以使用 [Azure 入口網站](https://portal.azure.com)和 [Azure 儲存體總管](https://storageexplorer.com)來建立和管理 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="63da4-119">You can create and manage Azure File shares using the [Azure portal](https://portal.azure.com) and the [Azure Storage Explorer](https://storageexplorer.com).</span></span> 

* <span data-ttu-id="63da4-120">**復原** Azure 檔案儲存體已從頭建置，可讓您隨時使用。</span><span class="sxs-lookup"><span data-stu-id="63da4-120">**Resiliency** Azure File storage has been built from the ground up to be always available.</span></span> <span data-ttu-id="63da4-121">使用 Azure 儲存體取代內部部署檔案共用，表示您不再需要被吵醒去處理本機電源中斷或網路問題。</span><span class="sxs-lookup"><span data-stu-id="63da4-121">Replacing on-premises file shares with Azure File storage means you no longer have to wake up to deal with local power outages or network issues.</span></span> 

* <span data-ttu-id="63da4-122">**熟悉的可程式性** Azure 中執行的應用程式可透過[檔案系統 I/O API](https://msdn.microsoft.com/library/system.io.file.aspx) 來存取共用中的資料。</span><span class="sxs-lookup"><span data-stu-id="63da4-122">**Familiar Programmability** Applications running in Azure can access data on the share via [file system I/O APIs](https://msdn.microsoft.com/library/system.io.file.aspx).</span></span> <span data-ttu-id="63da4-123">因此，開發人員可利用現有的程式碼和技能來移轉現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="63da4-123">Developers can therefore leverage their existing code and skills to migrate existing applications.</span></span> <span data-ttu-id="63da4-124">除了系統 IO API，您也可以使用任何 Azure 儲存體用戶端程式庫，例如 [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet) 或 [Azure 儲存體 REST API](/rest/api/storageservices/file-service-rest-api)。</span><span class="sxs-lookup"><span data-stu-id="63da4-124">In addition to System IO APIs, you can use any of the Azure storage client Libraries, such as the one for [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet), or the [Azure Storage REST API](/rest/api/storageservices/file-service-rest-api).</span></span>

<span data-ttu-id="63da4-125">Azure 檔案共用可以用來：</span><span class="sxs-lookup"><span data-stu-id="63da4-125">Azure File shares can be used to:</span></span>

* <span data-ttu-id="63da4-126">**取代內部部署檔案伺服器** Azure 檔案儲存體可以用來完全取代傳統內部部署檔案伺服器或 NAS 裝置上的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="63da4-126">**Replace on-premises file servers** Azure File storage can be used to completely replace file shares on traditional on-premises file servers or NAS devices.</span></span> <span data-ttu-id="63da4-127">無論身在何處，熱門作業系統 (例如 Windows、macOS 和 Linux) 都可以輕鬆掛接 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="63da4-127">Popular operating systems such as Windows, macOS, and Linux can easily mount an Azure File share wherever they are in the world.</span></span>

* <span data-ttu-id="63da4-128">**「原形移轉」應用程式**</span><span class="sxs-lookup"><span data-stu-id="63da4-128">**"Lift and Shift" applications**</span></span>

    <span data-ttu-id="63da4-129">Azure 檔案儲存體使得「原形移轉」應用程式 (使用內部部署檔案共用在應用程式不同部分之間共用資料) 移轉到雲端相當容易。</span><span class="sxs-lookup"><span data-stu-id="63da4-129">Azure File storage makes it easy to "lift and shift" applications to the cloud that use on-premises file shares to share data between parts of the application.</span></span> <span data-ttu-id="63da4-130">若要實作此動作，每個 VM 會連線到檔案共用，然後可以讀取和寫入檔案，就好像它會對內部部署檔案共用所採取的動作一樣。</span><span class="sxs-lookup"><span data-stu-id="63da4-130">To implement this, each VM connects to the file share and then it can read and write files just like it would against an on-premises file share.</span></span>

* <span data-ttu-id="63da4-131">**簡化雲端開發**</span><span class="sxs-lookup"><span data-stu-id="63da4-131">**Simplify Cloud Development**</span></span>
    
    <span data-ttu-id="63da4-132">Azure 檔案儲存體可以透過數種不同的使用方式來簡化新的雲端開發專案。</span><span class="sxs-lookup"><span data-stu-id="63da4-132">Azure File storage can be used in a number of different ways to simplify new cloud development projects.</span></span>
    
    * <span data-ttu-id="63da4-133">**共用的應用程式設定**</span><span class="sxs-lookup"><span data-stu-id="63da4-133">**Shared Application Settings**</span></span>
    
        <span data-ttu-id="63da4-134">分散式應用程式的常見模式是將組態檔放在一個集中的位置，這些應用程式可從許多不同的 VM 進行存取。</span><span class="sxs-lookup"><span data-stu-id="63da4-134">A common pattern for distributed applications is to have configuration files in a centralized location where they can be accessed from many different VMs.</span></span> <span data-ttu-id="63da4-135">這些組態檔現在可以儲存在 Azure 檔案共用中，並由所有應用程式執行個體進行存取。</span><span class="sxs-lookup"><span data-stu-id="63da4-135">Such configuration files can now be stored in an Azure File share, and read by all application instances.</span></span> <span data-ttu-id="63da4-136">這些設定可以透過可允許全球存取組態檔的 REST 介面進行管理。</span><span class="sxs-lookup"><span data-stu-id="63da4-136">These settings can also be managed via the REST interface, which allows worldwide access to the configuration files.</span></span>

    * <span data-ttu-id="63da4-137">**診斷共用**</span><span class="sxs-lookup"><span data-stu-id="63da4-137">**Diagnostic Share**</span></span>
    
        <span data-ttu-id="63da4-138">您可以使用 Azure 檔案共用來儲存診斷檔案，如記錄、度量及損毀傾印。</span><span class="sxs-lookup"><span data-stu-id="63da4-138">An Azure File share can also be used to save diagnostic files like logs, metrics, and crash dumps.</span></span> <span data-ttu-id="63da4-139">透過 SMB 和 REST 介面提供這些檔案共用，可允許應用程式建立或利用各種分析工具，進而處理與分析診斷資料。</span><span class="sxs-lookup"><span data-stu-id="63da4-139">Having file shares available through both the SMB and REST interface allows applications to build or leverage a variety of analysis tools for processing and analyzing the diagnostic data.</span></span>

    * <span data-ttu-id="63da4-140">**開發/測試/偵錯**</span><span class="sxs-lookup"><span data-stu-id="63da4-140">**Dev/Test/Debug**</span></span>

        <span data-ttu-id="63da4-141">當開發人員或系統管理員在雲端的 VM 上執行作業時，他們通常需要一組工具或公用程式。</span><span class="sxs-lookup"><span data-stu-id="63da4-141">When developers or administrators are working on VMs in the cloud, they often need a set of tools or utilities.</span></span> <span data-ttu-id="63da4-142">在每台他們所需的虛擬機器上安裝與散佈這些公用程式相當費時。</span><span class="sxs-lookup"><span data-stu-id="63da4-142">Installing and distributing these utilities on each virtual machine where they are needed can be a time consuming exercise.</span></span> <span data-ttu-id="63da4-143">有了 Azure 檔案儲存體，開發人員或系統管理員可將他們最愛的工具儲存在檔案共用上，然後從任何虛擬機器輕鬆連線。</span><span class="sxs-lookup"><span data-stu-id="63da4-143">With Azure File storage, a developer or administrator can store their favorite tools on a file share, which can be easily connected to from any virtual machine.</span></span>
        
## <a name="how-does-it-work"></a><span data-ttu-id="63da4-144">運作方式</span><span class="sxs-lookup"><span data-stu-id="63da4-144">How does it work?</span></span>

<span data-ttu-id="63da4-145">管理 Azure 檔案共用會比管理內部部署檔案共用簡單許多。</span><span class="sxs-lookup"><span data-stu-id="63da4-145">Managing Azure File shares is much simpler than managing file shares on-premises.</span></span> <span data-ttu-id="63da4-146">下圖說明 Azure 檔案儲存體管理建構：</span><span class="sxs-lookup"><span data-stu-id="63da4-146">The following diagram illustrates the Azure File storage management constructs:</span></span>

![檔案結構](./media/storage-files-introduction/files-concepts.png)

* <span data-ttu-id="63da4-148">**儲存體帳戶** 一律透過儲存體帳戶來存取 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="63da4-148">**Storage Account** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="63da4-149">如需關於儲存體帳戶容量的詳細資訊，請參閱[延展性和效能目標](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="63da4-149">See [Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="63da4-150">**共用** 檔案儲存體共用是 Azure 中的 SMB 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="63da4-150">**Share** A File Storage share is an SMB file share in Azure.</span></span> <span data-ttu-id="63da4-151">所有的目錄和檔案必須在上層共用中建立。</span><span class="sxs-lookup"><span data-stu-id="63da4-151">All directories and files must be created in a parent share.</span></span> <span data-ttu-id="63da4-152">帳戶可包含無限制數目的共用，而共用可儲存無限制數目的檔案，最多可達 5 TB 總容量的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="63da4-152">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the 5 TB total capacity of the file share.</span></span>

* <span data-ttu-id="63da4-153">**目錄** 選擇性的目錄階層。</span><span class="sxs-lookup"><span data-stu-id="63da4-153">**Directory** An optional hierarchy of directories.</span></span>

* <span data-ttu-id="63da4-154">**檔案** 共用中的檔案。</span><span class="sxs-lookup"><span data-stu-id="63da4-154">**File** A file in the share.</span></span> <span data-ttu-id="63da4-155">檔案的大小可高達 1 TB。</span><span class="sxs-lookup"><span data-stu-id="63da4-155">A file may be up to 1 TB in size.</span></span>

* <span data-ttu-id="63da4-156">**URL 格式** 可利用下列 URL 定址檔案：</span><span class="sxs-lookup"><span data-stu-id="63da4-156">**URL format** Files are addressable using the following URL format:</span></span>  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```

## <a name="next-steps"></a><span data-ttu-id="63da4-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63da4-157">Next steps</span></span>

* [<span data-ttu-id="63da4-158">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="63da4-158">Create Azure File Share</span></span>](storage-how-to-create-file-share.md)
* [<span data-ttu-id="63da4-159">連線並在 Windows 上掛接</span><span class="sxs-lookup"><span data-stu-id="63da4-159">Connect and Mount on Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="63da4-160">連線並在 Linux 上掛接</span><span class="sxs-lookup"><span data-stu-id="63da4-160">Connect and Mount on Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="63da4-161">連線並在 macOS 上掛接</span><span class="sxs-lookup"><span data-stu-id="63da4-161">Connect and Mount on macOS</span></span>](storage-how-to-use-files-mac.md)
* [<span data-ttu-id="63da4-162">常見問題集</span><span class="sxs-lookup"><span data-stu-id="63da4-162">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="63da4-163">在 Windows 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="63da4-163">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)   
* [<span data-ttu-id="63da4-164">在 Linux 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="63da4-164">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   

<!-- Rena I would remove any articles from here that are more than a year old. - Robin-->
### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="63da4-165">概念性文章和影片</span><span class="sxs-lookup"><span data-stu-id="63da4-165">Conceptual articles and videos</span></span>
* [<span data-ttu-id="63da4-166">Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統</span><span class="sxs-lookup"><span data-stu-id="63da4-166">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="63da4-167">Azure 檔案儲存體的工具支援</span><span class="sxs-lookup"><span data-stu-id="63da4-167">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="63da4-168">如何搭配使用 AzCopy 與 Microsoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="63da4-168">How to use AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="63da4-169">使用 Azure CLI 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="63da4-169">Using the Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)

### <a name="blog-posts"></a><span data-ttu-id="63da4-170">部落格文章</span><span class="sxs-lookup"><span data-stu-id="63da4-170">Blog posts</span></span>
* [<span data-ttu-id="63da4-171">Azure 檔案儲存體現已公開推出</span><span class="sxs-lookup"><span data-stu-id="63da4-171">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="63da4-172">Azure 檔案儲存體內部</span><span class="sxs-lookup"><span data-stu-id="63da4-172">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="63da4-173">Microsoft Azure 檔案服務簡介</span><span class="sxs-lookup"><span data-stu-id="63da4-173">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="63da4-174">將資料移轉至 Azure 檔案</span><span class="sxs-lookup"><span data-stu-id="63da4-174">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="63da4-175">參考</span><span class="sxs-lookup"><span data-stu-id="63da4-175">Reference</span></span>
* [<span data-ttu-id="63da4-176">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="63da4-176">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="63da4-177">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="63da4-177">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
