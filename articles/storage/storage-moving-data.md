---
title: "aaaMoving 大量資料至 azure 或從 Azure 中的雲端儲存體 |Microsoft 文件"
description: "Hello 不同的方法來移動資料 tooand 從 Azure 儲存體的概觀。"
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 8f7105fea7c2d28ba9954898743070d338f46a37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a><span data-ttu-id="1d6ca-103">從 Azure 儲存體移動資料 tooand</span><span class="sxs-lookup"><span data-stu-id="1d6ca-103">Moving data tooand from Azure Storage</span></span>
<span data-ttu-id="1d6ca-104">如果您想 toomove 在內部部署資料 tooAzure 儲存體 （反之亦然），有各種不同的方式 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-104">If you want toomove on-premises data tooAzure Storage (or vice versa), there are a variety of ways toodo this.</span></span> <span data-ttu-id="1d6ca-105">最適合您的 hello 方法將取決於您的案例。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-105">hello approach that works best for you will depend on your scenario.</span></span> <span data-ttu-id="1d6ca-106">本文將提供不同案例的快速概觀和每個案例的適當供應項目。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-106">This article will provide a quick overview of different scenarios and appropriate offerings for each one.</span></span>

## <a name="building-applications"></a><span data-ttu-id="1d6ca-107">建置應用程式</span><span class="sxs-lookup"><span data-stu-id="1d6ca-107">Building Applications</span></span>
<span data-ttu-id="1d6ca-108">如果您正在建置應用程式，針對 hello REST API 或其中一個我們許多用戶端程式庫開發是從 Azure 儲存體的絕佳方式，toomove 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-108">If you're building an application, developing against hello REST API or one of our many client libraries is a great way toomove data tooand from Azure Storage.</span></span>

<span data-ttu-id="1d6ca-109">Azure 儲存體提供 .NET、iOS、Java、Android、通用 Windows 平台 (UWP)、Xamarin、c++、Node.JS、PHP、Ruby 和 Python 等豐富的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-109">Azure Storage provides rich client libraries for .NET, iOS, Java, Android, Universal Windows Platform (UWP), Xamarin, C++, Node.JS, PHP, Ruby, and Python.</span></span> <span data-ttu-id="1d6ca-110">hello 用戶端程式庫提供進階的功能，例如重試邏輯、 記錄和並行上傳。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-110">hello client libraries offer advanced capabilities such as retry logic, logging, and parallel uploads.</span></span> <span data-ttu-id="1d6ca-111">您也可以直接對 hello REST API，可以呼叫任何提出 HTTP/HTTPS 要求的語言所開發。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-111">You can also develop directly against hello REST API, which can be called by any language that makes HTTP/HTTPS requests.</span></span>

<span data-ttu-id="1d6ca-112">請參閱[開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-112">See [Get Started with Azure Blob Storage](storage-dotnet-how-to-use-blobs.md) toolearn more.</span></span>

<span data-ttu-id="1d6ca-113">此外，我們也提供 hello [Azure 儲存體的資料移動程式庫](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement)這是專為高效能從 Azure 複製的資料 tooand 所設計的程式庫。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-113">In addition, we also offer hello [Azure Storage Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) which is a library designed for high-performance copying of data tooand from Azure.</span></span> <span data-ttu-id="1d6ca-114">請參閱 tooour 資料移動文件庫[文件](https://github.com/Azure/azure-storage-net-data-movement)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-114">Please refer tooour Data Movement Library [documentation](https://github.com/Azure/azure-storage-net-data-movement) toolearn more.</span></span> 

## <a name="quickly-viewinginteracting-with-your-data"></a><span data-ttu-id="1d6ca-115">快速檢視/和資料互動</span><span class="sxs-lookup"><span data-stu-id="1d6ca-115">Quickly viewing/interacting with your data</span></span>
<span data-ttu-id="1d6ca-116">如果您想要輕鬆 tooview 您 Azure 儲存體的資料，同時也擁有 hello 能力 tooupload 並下載您的資料，請考慮使用 Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-116">If you want an easy way tooview your Azure Storage data while also having hello ability tooupload and download your data, then consider using an Azure Storage Explorer.</span></span>

<span data-ttu-id="1d6ca-117">簽出的清單[Azure 儲存體總管](storage-explorers.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-117">Check out our list of [Azure Storage Explorers](storage-explorers.md) toolearn more.</span></span>

## <a name="system-administration"></a><span data-ttu-id="1d6ca-118">系統管理</span><span class="sxs-lookup"><span data-stu-id="1d6ca-118">System Administration</span></span>
<span data-ttu-id="1d6ca-119">如果您需要或更熟悉的命令列公用程式 （例如系統管理員），以下是一些您 tooconsider 選項：</span><span class="sxs-lookup"><span data-stu-id="1d6ca-119">If you require or are more comfortable with a command-line utility (e.g. System Administrators), here are a few options for you tooconsider:</span></span>

### <a name="azcopy"></a><span data-ttu-id="1d6ca-120">AzCopy</span><span class="sxs-lookup"><span data-stu-id="1d6ca-120">AzCopy</span></span>
<span data-ttu-id="1d6ca-121">AzCopy 是專為高效能的資料 tooand 複製從 Azure 儲存體設計的 Windows 命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-121">AzCopy is a Windows command-line utility designed for high-performance copying of data tooand from Azure Storage.</span></span> <span data-ttu-id="1d6ca-122">您也可以複製儲存體帳戶內或不同儲存體帳戶之間的資料。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-122">You can also copy data within a storage account, or between different storage accounts.</span></span>

<span data-ttu-id="1d6ca-123">請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-123">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) toolearn more.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="1d6ca-124">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d6ca-124">Azure PowerShell</span></span>
<span data-ttu-id="1d6ca-125">Azure PowerShell 模組提供 Cmdlet 讓您用於管理 Azure 上的服務。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-125">Azure PowerShell is a module that provides cmdlets for managing services on Azure.</span></span> <span data-ttu-id="1d6ca-126">此模組為工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-126">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

<span data-ttu-id="1d6ca-127">請參閱[與 Azure 儲存體使用 Azure PowerShell](storage-powershell-guide-full.md) toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-127">See [Using Azure PowerShell with Azure Storage](storage-powershell-guide-full.md) toolearn more.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="1d6ca-128">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1d6ca-128">Azure CLI</span></span>
<span data-ttu-id="1d6ca-129">Azure CLI 提供您一組開放原始碼的跨平台命令，供您使用 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-129">Azure CLI provides a set of open source, cross-platform commands for working with Azure services.</span></span> <span data-ttu-id="1d6ca-130">Azure CLI 可在 Windows、OSX 和 Linux 上使用。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-130">Azure CLI is available on Windows, OSX, and Linux.</span></span>

<span data-ttu-id="1d6ca-131">請參閱[使用 hello 與 Azure 儲存體的 Azure CLI](storage-azure-cli.md) toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-131">See [Using hello Azure CLI with Azure Storage](storage-azure-cli.md) toolearn more.</span></span>

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a><span data-ttu-id="1d6ca-132">以較慢的網路移動大量資料</span><span class="sxs-lookup"><span data-stu-id="1d6ca-132">Moving large amounts of data with a slow network</span></span>
<span data-ttu-id="1d6ca-133">Hello 與移動大量資料相關聯的最大挑戰之一是 hello 傳輸時間。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-133">One of hello biggest challenges associated with moving large amounts of data is hello transfer time.</span></span> <span data-ttu-id="1d6ca-134">如果您想 tooget 資料從 Azure 儲存體不需要擔心網路成本或撰寫程式碼時，Azure 匯入/匯出就會是適當的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-134">If you want tooget data to/from Azure Storage without worrying about networks costs or writing code, then Azure Import/Export is an appropriate solution.</span></span>

<span data-ttu-id="1d6ca-135">請參閱[Azure 匯入/匯出](storage-import-export-service.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-135">See [Azure Import/Export](storage-import-export-service.md) toolearn more.</span></span>

## <a name="backing-up-your-data"></a><span data-ttu-id="1d6ca-136">備份您的資料</span><span class="sxs-lookup"><span data-stu-id="1d6ca-136">Backing up your data</span></span>
<span data-ttu-id="1d6ca-137">如果您只需要 toobackup 您資料 tooAzure 儲存體，Azure 備份是 hello 方式 toogo。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-137">If you simply need toobackup your data tooAzure Storage, Azure Backup is hello way toogo.</span></span> <span data-ttu-id="1d6ca-138">對於備份內部部署資料和 Azure VM，這是功能強大的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-138">This is a powerful solution for backing up on-premises data and Azure VMs.</span></span>

<span data-ttu-id="1d6ca-139">請參閱[Azure Backup](../backup/backup-introduction-to-azure-backup.md) toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-139">See [Azure Backup](../backup/backup-introduction-to-azure-backup.md) toolearn more.</span></span>

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a><span data-ttu-id="1d6ca-140">存取您資料的內部與 hello 雲端</span><span class="sxs-lookup"><span data-stu-id="1d6ca-140">Accessing your data on-premises and from hello cloud</span></span>
<span data-ttu-id="1d6ca-141">如果您需要一個解決方案，來存取您資料內部及從 hello 雲端，您應該考慮使用 Azure 的混合式雲端儲存體解決方案，StorSimple。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-141">If you need a solution for accessing your data on-premises and from hello cloud, then you should consider using Azure's hybrid cloud storage solution, StorSimple.</span></span> <span data-ttu-id="1d6ca-142">此解決方案包含實體 StorSimple 裝置，以智慧方式將經常使用的資料儲存在 SSD 上，將偶爾使用的資料儲存在 HDD 上，並且將非作用中/備份/封存資料儲存在 Azure 儲存體上。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-142">This solution consists of a physical StorSimple device that intelligently stores frequently used data on SSDs, occasionally used data on HDDs, and inactive/backup/archival data on Azure Storage.</span></span>

<span data-ttu-id="1d6ca-143">請參閱[StorSimple](../storsimple/storsimple-overview.md) toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-143">See [StorSimple](../storsimple/storsimple-overview.md) toolearn more.</span></span>

## <a name="recovering-your-data"></a><span data-ttu-id="1d6ca-144">復原您的資料</span><span class="sxs-lookup"><span data-stu-id="1d6ca-144">Recovering your data</span></span>
<span data-ttu-id="1d6ca-145">當您擁有內部部署工作負載和應用程式時，您將需要一個解決方案，讓您的商務 toocontinue hello 災害事件中執行。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-145">When you have on-premises workloads and applications, you'll need a solution that allows your business toocontinue running in hello event of a disaster.</span></span> <span data-ttu-id="1d6ca-146">Azure Site Recovery 可處理虛擬機器和實體伺服器的複寫、容錯移轉及復原作業。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-146">Azure Site Recovery handles replication, failover, and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="1d6ca-147">複寫的資料會儲存在 Azure 儲存體，讓您 tooeliminate hello 需要次要站上的資料中心。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-147">Replicated data is stored in Azure Storage, allowing you tooeliminate hello need for a secondary on-site datacenter.</span></span>

<span data-ttu-id="1d6ca-148">請參閱[Azure Site Recovery](../site-recovery/site-recovery-overview.md) toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-148">See [Azure Site Recovery](../site-recovery/site-recovery-overview.md) toolearn more.</span></span>
### <a name="moving-data-faq"></a><span data-ttu-id="1d6ca-149">移動資料常見問題集︰</span><span class="sxs-lookup"><span data-stu-id="1d6ca-149">Moving Data FAQ:</span></span>
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a><span data-ttu-id="1d6ca-150">我可以移轉 Vhd 從一個區域 tooanother 無需先行複製嗎？</span><span class="sxs-lookup"><span data-stu-id="1d6ca-150">Can I migrate VHDs from one region tooanother without copying?</span></span>
<span data-ttu-id="1d6ca-151">hello 只方式 toocopy Vhd 區域之間是每個區域上的儲存體帳戶之間 toocopy hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-151">hello only way toocopy VHDs between region is toocopy hello data between storage accounts on each region.</span></span> <span data-ttu-id="1d6ca-152">您可以使用 AZCopy 這樣做。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-152">You can use AZCopy for this.</span></span> <span data-ttu-id="1d6ca-153">請參閱與 hello 更多的 AzCopy 命令列公用程式 toolearn 傳輸資料。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-153">See Transfer data with hello AzCopy Command-Line Utility toolearn more.</span></span> <span data-ttu-id="1d6ca-154">針對極大的資料量，您也可以使用 Azure 匯入/匯出。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-154">For very large amounts of data, you can also Azure Import/Export.</span></span> <span data-ttu-id="1d6ca-155">請參閱[Azure 匯入/匯出](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="1d6ca-155">See [Azure Import/Export](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn more.</span></span>
