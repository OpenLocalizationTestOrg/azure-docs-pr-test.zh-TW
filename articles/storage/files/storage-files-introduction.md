---
title: "aaaIntroduction tooAzure 檔案儲存體 |Microsoft 文件"
description: "簡介 tooAzure 檔案存放裝置，提供網路檔案共用在 hello Microsoft 雲端中"
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
ms.openlocfilehash: fe6826e79c364a6956831d2e273c4342a5fd47f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a><span data-ttu-id="39b1d-103">簡介 tooAzure 檔案存放裝置</span><span class="sxs-lookup"><span data-stu-id="39b1d-103">Introduction tooAzure File storage</span></span>

<span data-ttu-id="39b1d-104">Azure 檔案儲存體提供網路檔案共用使用 hello 業界標準的 hello 雲端[伺服器訊息區塊 (SMB) 通訊協定](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx)和[Common Internet File System (CIFS)](https://technet.microsoft.com/library/cc939973.aspx)。</span><span class="sxs-lookup"><span data-stu-id="39b1d-104">Azure File storage offers network file shares in hello cloud using hello industry standard [Server Message Block (SMB) Protocol](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) and [Common Internet File System (CIFS)](https://technet.microsoft.com/library/cc939973.aspx).</span></span> <span data-ttu-id="39b1d-105">執行 Windows、macOS 或 Linux 的 Azure 虛擬機器和內部部署可同時掛接 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="39b1d-105">Azure File shares can be mounted concurrently by Azure Virtual Machines and on-premises deployments running Windows, macOS, or Linux.</span></span> <span data-ttu-id="39b1d-106">一般用途儲存體帳戶可讓您存取 tooAzure 檔案儲存體、 Azure Blob 儲存體和 Azure 佇列儲存體。</span><span class="sxs-lookup"><span data-stu-id="39b1d-106">A general-purpose storage account gives you access tooAzure File storage, Azure Blob storage, and Azure Queue storage.</span></span>

## <a name="videos"></a><span data-ttu-id="39b1d-107">影片</span><span class="sxs-lookup"><span data-stu-id="39b1d-107">Videos</span></span>
| <span data-ttu-id="39b1d-108">介紹 Azure 檔案儲存體 (27 分鐘)</span><span class="sxs-lookup"><span data-stu-id="39b1d-108">Introducing Azure File storage (27m)</span></span> | <span data-ttu-id="39b1d-109">Azure 檔案儲存體教學課程 (5 分鐘)</span><span class="sxs-lookup"><span data-stu-id="39b1d-109">Azure File storage Tutorial (5 minutes)</span></span>  |
|-|-|
| <span data-ttu-id="39b1d-110">[![錄影畫面的 hello 簡介 Azure 檔案儲存體視訊-按一下 tooplay ！](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs)</span><span class="sxs-lookup"><span data-stu-id="39b1d-110">[![Screencast of hello Introducing Azure File storage video - click tooplay!](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs)</span></span> | <span data-ttu-id="39b1d-111">[![錄影畫面的 hello Azure 檔案儲存體教學課程-按一下 tooplay ！](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/)</span><span class="sxs-lookup"><span data-stu-id="39b1d-111">[![Screencast of hello Azure File storage Tutorial - click tooplay!](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/)</span></span> |

## <a name="why-azure-file-storage-is-useful"></a><span data-ttu-id="39b1d-112">Azure 檔案儲存體為何很實用</span><span class="sxs-lookup"><span data-stu-id="39b1d-112">Why Azure File storage is useful</span></span>

<span data-ttu-id="39b1d-113">Azure 檔案儲存體可讓您 tooreplace Windows Server、 Linux 或 NAS 型檔案伺服器裝載於內部，或在 hello 雲端與雲端無作業系統的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="39b1d-113">Azure File storage allows you tooreplace Windows Server, Linux, or NAS-based file servers hosted on-premises or in hello cloud with an OS-free cloud file share.</span></span> <span data-ttu-id="39b1d-114">Azure 檔案儲存體有下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="39b1d-114">Azure File storage has hello following benefits:</span></span>

* <span data-ttu-id="39b1d-115">**共用存取**Azure 檔案共用支援 hello 業界標準的 SMB 通訊協定，這表示您可以順暢地取代您的內部檔案共用 Azure 檔案共用而不需擔心應用程式相容性。</span><span class="sxs-lookup"><span data-stu-id="39b1d-115">**Shared access** Azure File shares support hello industry standard SMB protocol, meaning you can seamlessly replace your on-premises file shares with Azure File shares without worrying about application compatibility.</span></span> <span data-ttu-id="39b1d-116">無法 tooaccess 從多個機器和應用程式/執行個體的檔案共用是更大的優點，使用 Azure 檔案儲存體。</span><span class="sxs-lookup"><span data-stu-id="39b1d-116">Being able tooaccess a file share from multiple machines and applications/instances is a significant advantage with Azure File storage.</span></span>

* <span data-ttu-id="39b1d-117">**完全管理**Azure 檔案共用可以建立不含 hello 需要 toomanage 硬體或作業系統，這表示您沒有 toodeal 修補 hello 伺服器 OS 重大安全性升級或替換故障硬碟。</span><span class="sxs-lookup"><span data-stu-id="39b1d-117">**Fully Managed** Azure File shares can be created without hello need toomanage hardware or an OS, which means you don't have toodeal with patching hello server OS with critical security upgrades or replacing faulty hard disks.</span></span>

* <span data-ttu-id="39b1d-118">**指令碼和工具**PowerShell cmdlet 和 Azure CLI 可以使用的 toocreate、 裝載和管理 Azure 檔案共用做 hello 管理的 Azure 應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="39b1d-118">**Scripting and Tooling** PowerShell cmdlets and Azure CLI can be used toocreate, mount, and manage Azure File shares as part of hello administration of Azure applications.</span></span> <span data-ttu-id="39b1d-119">您可以建立和管理 Azure 檔案共用使用 hello [Azure 入口網站](https://portal.azure.com)和 hello [Azure 儲存體總管](https://storageexplorer.com)。</span><span class="sxs-lookup"><span data-stu-id="39b1d-119">You can create and manage Azure File shares using hello [Azure portal](https://portal.azure.com) and hello [Azure Storage Explorer](https://storageexplorer.com).</span></span> 

* <span data-ttu-id="39b1d-120">**恢復功能**Azure 檔案儲存體已經根據 hello toobe 永遠可使用的總接地。</span><span class="sxs-lookup"><span data-stu-id="39b1d-120">**Resiliency** Azure File storage has been built from hello ground up toobe always available.</span></span> <span data-ttu-id="39b1d-121">Azure 檔案以取代在內部部署的檔案共用儲存體，表示您不再需要 toowake 向上 toodeal 本機電源中斷或網路問題。</span><span class="sxs-lookup"><span data-stu-id="39b1d-121">Replacing on-premises file shares with Azure File storage means you no longer have toowake up toodeal with local power outages or network issues.</span></span> 

* <span data-ttu-id="39b1d-122">**熟悉的可程式性**在 Azure 中執行的應用程式可以存取透過 hello 共用上的資料[檔案系統 I/O Api](https://msdn.microsoft.com/library/system.io.file.aspx)。</span><span class="sxs-lookup"><span data-stu-id="39b1d-122">**Familiar Programmability** Applications running in Azure can access data on hello share via [file system I/O APIs](https://msdn.microsoft.com/library/system.io.file.aspx).</span></span> <span data-ttu-id="39b1d-123">開發人員因此可以利用其現有的程式碼和技術 toomigrate 現有應用程式。</span><span class="sxs-lookup"><span data-stu-id="39b1d-123">Developers can therefore leverage their existing code and skills toomigrate existing applications.</span></span> <span data-ttu-id="39b1d-124">此外 tooSystem IO Api，您可以使用任一 hello Azure 儲存體用戶端程式庫，例如其中一個 hello 的[.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet)，或使用 hello [Azure 儲存體的 REST API](/rest/api/storageservices/file-service-rest-api)。</span><span class="sxs-lookup"><span data-stu-id="39b1d-124">In addition tooSystem IO APIs, you can use any of hello Azure storage client Libraries, such as hello one for [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet), or hello [Azure Storage REST API](/rest/api/storageservices/file-service-rest-api).</span></span>

<span data-ttu-id="39b1d-125">Azure 檔案共用可以用來：</span><span class="sxs-lookup"><span data-stu-id="39b1d-125">Azure File shares can be used to:</span></span>

* <span data-ttu-id="39b1d-126">**取代內部部署檔案伺服器**Azure 檔案存放裝置可以是傳統的內部部署檔案伺服器或 NAS 裝置上使用的 toocompletely 取代檔案共用。</span><span class="sxs-lookup"><span data-stu-id="39b1d-126">**Replace on-premises file servers** Azure File storage can be used toocompletely replace file shares on traditional on-premises file servers or NAS devices.</span></span> <span data-ttu-id="39b1d-127">熱門作業系統，例如 Windows、 macOS 和 Linux 座落 hello 世界中，可以輕鬆地掛接 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="39b1d-127">Popular operating systems such as Windows, macOS, and Linux can easily mount an Azure File share wherever they are in hello world.</span></span>

* <span data-ttu-id="39b1d-128">**「原形移轉」應用程式**</span><span class="sxs-lookup"><span data-stu-id="39b1d-128">**"Lift and Shift" applications**</span></span>

    <span data-ttu-id="39b1d-129">Azure 檔案儲存體可輕鬆太 「 提起和 shift 」 的應用程式 toohello 雲端使用內部部署檔案的檔案就會共用 tooshare hello 應用程式的各部分之間的資料。</span><span class="sxs-lookup"><span data-stu-id="39b1d-129">Azure File storage makes it easy too"lift and shift" applications toohello cloud that use on-premises file shares tooshare data between parts of hello application.</span></span> <span data-ttu-id="39b1d-130">tooimplement，每個 VM 會連線 toohello 檔案共用，然後可讀取並寫入檔案，就像它會根據內部檔案共用。</span><span class="sxs-lookup"><span data-stu-id="39b1d-130">tooimplement this, each VM connects toohello file share and then it can read and write files just like it would against an on-premises file share.</span></span>

* <span data-ttu-id="39b1d-131">**簡化雲端開發**</span><span class="sxs-lookup"><span data-stu-id="39b1d-131">**Simplify Cloud Development**</span></span>
    
    <span data-ttu-id="39b1d-132">Azure 檔案儲存體可以用於許多不同的方式 toosimplify 新雲端開發專案。</span><span class="sxs-lookup"><span data-stu-id="39b1d-132">Azure File storage can be used in a number of different ways toosimplify new cloud development projects.</span></span>
    
    * <span data-ttu-id="39b1d-133">**共用的應用程式設定**</span><span class="sxs-lookup"><span data-stu-id="39b1d-133">**Shared Application Settings**</span></span>
    
        <span data-ttu-id="39b1d-134">分散式應用程式的常見模式為 toohave 組態檔，在集中位置，從許多不同的 Vm 進行存取。</span><span class="sxs-lookup"><span data-stu-id="39b1d-134">A common pattern for distributed applications is toohave configuration files in a centralized location where they can be accessed from many different VMs.</span></span> <span data-ttu-id="39b1d-135">這些組態檔現在可以儲存在 Azure 檔案共用中，並由所有應用程式執行個體進行存取。</span><span class="sxs-lookup"><span data-stu-id="39b1d-135">Such configuration files can now be stored in an Azure File share, and read by all application instances.</span></span> <span data-ttu-id="39b1d-136">這些設定也可以透過 hello REST 介面，可讓世界各地存取 toohello 組態檔來管理。</span><span class="sxs-lookup"><span data-stu-id="39b1d-136">These settings can also be managed via hello REST interface, which allows worldwide access toohello configuration files.</span></span>

    * <span data-ttu-id="39b1d-137">**診斷共用**</span><span class="sxs-lookup"><span data-stu-id="39b1d-137">**Diagnostic Share**</span></span>
    
        <span data-ttu-id="39b1d-138">Azure 檔案共用也可以使用的 toosave 診斷檔案，例如記錄、 度量和損毀傾印。</span><span class="sxs-lookup"><span data-stu-id="39b1d-138">An Azure File share can also be used toosave diagnostic files like logs, metrics, and crash dumps.</span></span> <span data-ttu-id="39b1d-139">具有檔案共用可透過 SMB 的 hello 和 REST 介面可讓應用程式 toobuild 或利用各種不同的分析工具，以處理及分析 hello 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="39b1d-139">Having file shares available through both hello SMB and REST interface allows applications toobuild or leverage a variety of analysis tools for processing and analyzing hello diagnostic data.</span></span>

    * <span data-ttu-id="39b1d-140">**開發/測試/偵錯**</span><span class="sxs-lookup"><span data-stu-id="39b1d-140">**Dev/Test/Debug**</span></span>

        <span data-ttu-id="39b1d-141">當開發人員或系統管理員使用 hello 雲端中的 Vm 上時，它們通常需要一組工具或公用程式。</span><span class="sxs-lookup"><span data-stu-id="39b1d-141">When developers or administrators are working on VMs in hello cloud, they often need a set of tools or utilities.</span></span> <span data-ttu-id="39b1d-142">在每台他們所需的虛擬機器上安裝與散佈這些公用程式相當費時。</span><span class="sxs-lookup"><span data-stu-id="39b1d-142">Installing and distributing these utilities on each virtual machine where they are needed can be a time consuming exercise.</span></span> <span data-ttu-id="39b1d-143">使用 Azure 檔案儲存體，開發人員或系統管理員可以儲存最愛的工具在檔案共用，可以輕鬆地連接的 toofrom 任何虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="39b1d-143">With Azure File storage, a developer or administrator can store their favorite tools on a file share, which can be easily connected toofrom any virtual machine.</span></span>
        
## <a name="how-does-it-work"></a><span data-ttu-id="39b1d-144">運作方式</span><span class="sxs-lookup"><span data-stu-id="39b1d-144">How does it work?</span></span>

<span data-ttu-id="39b1d-145">管理 Azure 檔案共用會比管理內部部署檔案共用簡單許多。</span><span class="sxs-lookup"><span data-stu-id="39b1d-145">Managing Azure File shares is much simpler than managing file shares on-premises.</span></span> <span data-ttu-id="39b1d-146">hello 下列圖表說明 hello Azure 檔案儲存體管理建構：</span><span class="sxs-lookup"><span data-stu-id="39b1d-146">hello following diagram illustrates hello Azure File storage management constructs:</span></span>

![檔案結構](./media/storage-files-introduction/files-concepts.png)

* <span data-ttu-id="39b1d-148">**儲存體帳戶**所有存取的 tooAzure 是儲存體透過儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="39b1d-148">**Storage Account** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="39b1d-149">如需關於儲存體帳戶容量的詳細資訊，請參閱[延展性和效能目標](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="39b1d-149">See [Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="39b1d-150">**共用** 檔案儲存體共用是 Azure 中的 SMB 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="39b1d-150">**Share** A File Storage share is an SMB file share in Azure.</span></span> <span data-ttu-id="39b1d-151">所有的目錄和檔案必須在上層共用中建立。</span><span class="sxs-lookup"><span data-stu-id="39b1d-151">All directories and files must be created in a parent share.</span></span> <span data-ttu-id="39b1d-152">帳戶可以包含無限的數目的共用，並共用可以存放無限的數量的 toohello 5TB 的總容量 hello 檔案共用上的檔案。</span><span class="sxs-lookup"><span data-stu-id="39b1d-152">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello 5 TB total capacity of hello file share.</span></span>

* <span data-ttu-id="39b1d-153">**目錄** 選擇性的目錄階層。</span><span class="sxs-lookup"><span data-stu-id="39b1d-153">**Directory** An optional hierarchy of directories.</span></span>

* <span data-ttu-id="39b1d-154">**檔案**hello 共用中的檔案。</span><span class="sxs-lookup"><span data-stu-id="39b1d-154">**File** A file in hello share.</span></span> <span data-ttu-id="39b1d-155">檔案可能是 up too1 TB 的大小。</span><span class="sxs-lookup"><span data-stu-id="39b1d-155">A file may be up too1 TB in size.</span></span>

* <span data-ttu-id="39b1d-156">**URL 格式**檔案都可使用下列 URL 格式的 hello 定址：</span><span class="sxs-lookup"><span data-stu-id="39b1d-156">**URL format** Files are addressable using hello following URL format:</span></span>  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```

## <a name="next-steps"></a><span data-ttu-id="39b1d-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39b1d-157">Next steps</span></span>

* [<span data-ttu-id="39b1d-158">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="39b1d-158">Create Azure File Share</span></span>](storage-how-to-create-file-share.md)
* [<span data-ttu-id="39b1d-159">連線並在 Windows 上掛接</span><span class="sxs-lookup"><span data-stu-id="39b1d-159">Connect and Mount on Windows</span></span>](storage-how-to-use-files-windows.md)
* [<span data-ttu-id="39b1d-160">連線並在 Linux 上掛接</span><span class="sxs-lookup"><span data-stu-id="39b1d-160">Connect and Mount on Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="39b1d-161">連線並在 macOS 上掛接</span><span class="sxs-lookup"><span data-stu-id="39b1d-161">Connect and Mount on macOS</span></span>](storage-how-to-use-files-mac.md)
* [<span data-ttu-id="39b1d-162">常見問題集</span><span class="sxs-lookup"><span data-stu-id="39b1d-162">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="39b1d-163">在 Windows 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="39b1d-163">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)   
* [<span data-ttu-id="39b1d-164">在 Linux 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="39b1d-164">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)   

<!-- Rena I would remove any articles from here that are more than a year old. - Robin-->
### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="39b1d-165">概念性文章和影片</span><span class="sxs-lookup"><span data-stu-id="39b1d-165">Conceptual articles and videos</span></span>
* [<span data-ttu-id="39b1d-166">Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統</span><span class="sxs-lookup"><span data-stu-id="39b1d-166">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="39b1d-167">Azure 檔案儲存體的工具支援</span><span class="sxs-lookup"><span data-stu-id="39b1d-167">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="39b1d-168">如何 toouse AzCopy 與 Microsoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="39b1d-168">How toouse AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="39b1d-169">使用 Azure CLI hello 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="39b1d-169">Using hello Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)

### <a name="blog-posts"></a><span data-ttu-id="39b1d-170">部落格文章</span><span class="sxs-lookup"><span data-stu-id="39b1d-170">Blog posts</span></span>
* [<span data-ttu-id="39b1d-171">Azure 檔案儲存體現已公開推出</span><span class="sxs-lookup"><span data-stu-id="39b1d-171">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="39b1d-172">Azure 檔案儲存體內部</span><span class="sxs-lookup"><span data-stu-id="39b1d-172">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="39b1d-173">Microsoft Azure 檔案服務簡介</span><span class="sxs-lookup"><span data-stu-id="39b1d-173">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="39b1d-174">移轉資料 tooAzure 檔案</span><span class="sxs-lookup"><span data-stu-id="39b1d-174">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="39b1d-175">參考</span><span class="sxs-lookup"><span data-stu-id="39b1d-175">Reference</span></span>
* [<span data-ttu-id="39b1d-176">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="39b1d-176">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="39b1d-177">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="39b1d-177">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
