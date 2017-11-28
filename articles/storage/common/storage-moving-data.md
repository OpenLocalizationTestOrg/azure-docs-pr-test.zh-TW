---
title: "從 Azure 中的雲端儲存體來回移動大量資料 | Microsoft Docs"
description: "從 Azure 儲存體來回移動資料之不同方法的概觀。"
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
ms.openlocfilehash: ba390a5973ad33405f1d4217d60d7989f04db3b4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="moving-data-to-and-from-azure-storage"></a><span data-ttu-id="fa552-103">從 Azure 儲存體來回移動資料</span><span class="sxs-lookup"><span data-stu-id="fa552-103">Moving data to and from Azure Storage</span></span>
<span data-ttu-id="fa552-104">如果您想要將內部部署資料移至 Azure 儲存體 (或相反)，有各種不同的方法可以辦到。</span><span class="sxs-lookup"><span data-stu-id="fa552-104">If you want to move on-premises data to Azure Storage (or vice versa), there are a variety of ways to do this.</span></span> <span data-ttu-id="fa552-105">最適合的方法將取決於您的案例。</span><span class="sxs-lookup"><span data-stu-id="fa552-105">The approach that works best for you will depend on your scenario.</span></span> <span data-ttu-id="fa552-106">本文將提供不同案例的快速概觀和每個案例的適當供應項目。</span><span class="sxs-lookup"><span data-stu-id="fa552-106">This article will provide a quick overview of different scenarios and appropriate offerings for each one.</span></span>

## <a name="building-applications"></a><span data-ttu-id="fa552-107">建置應用程式</span><span class="sxs-lookup"><span data-stu-id="fa552-107">Building Applications</span></span>
<span data-ttu-id="fa552-108">如果您要建置應用程式，針對 REST API 或許多用戶端程式庫進行開發是從 Azure 儲存體來回移動資料的好方法。</span><span class="sxs-lookup"><span data-stu-id="fa552-108">If you're building an application, developing against the REST API or one of our many client libraries is a great way to move data to and from Azure Storage.</span></span>

<span data-ttu-id="fa552-109">Azure 儲存體提供 .NET、iOS、Java、Android、通用 Windows 平台 (UWP)、Xamarin、c++、Node.JS、PHP、Ruby 和 Python 等豐富的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="fa552-109">Azure Storage provides rich client libraries for .NET, iOS, Java, Android, Universal Windows Platform (UWP), Xamarin, C++, Node.JS, PHP, Ruby, and Python.</span></span> <span data-ttu-id="fa552-110">這些用戶端程式庫提供多種進階功能，例如大重試邏輯、記錄與並行上傳等等。</span><span class="sxs-lookup"><span data-stu-id="fa552-110">The client libraries offer advanced capabilities such as retry logic, logging, and parallel uploads.</span></span> <span data-ttu-id="fa552-111">您也可以直接透過 REST API 開發，它可以透過提出 HTTP/HTTPS 要求的任何語言進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="fa552-111">You can also develop directly against the REST API, which can be called by any language that makes HTTP/HTTPS requests.</span></span>

<span data-ttu-id="fa552-112">若要深入了解，請參閱 [開始使用 Azure Blob 儲存體](../blobs/storage-dotnet-how-to-use-blobs.md) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-112">See [Get Started with Azure Blob Storage](../blobs/storage-dotnet-how-to-use-blobs.md) to learn more.</span></span>

<span data-ttu-id="fa552-113">此外，我們也提供 [Azure 儲存體資料移動程式庫](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) ，這是專為在 Azure 中高效能來回複製資料所設計。</span><span class="sxs-lookup"><span data-stu-id="fa552-113">In addition, we also offer the [Azure Storage Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) which is a library designed for high-performance copying of data to and from Azure.</span></span> <span data-ttu-id="fa552-114">若要深入了解，請參閱我們的資料移動程式庫 [文件](https://github.com/Azure/azure-storage-net-data-movement) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-114">Please refer to our Data Movement Library [documentation](https://github.com/Azure/azure-storage-net-data-movement) to learn more.</span></span> 

## <a name="quickly-viewinginteracting-with-your-data"></a><span data-ttu-id="fa552-115">快速檢視/和資料互動</span><span class="sxs-lookup"><span data-stu-id="fa552-115">Quickly viewing/interacting with your data</span></span>
<span data-ttu-id="fa552-116">如果您想要輕鬆地檢視 Azure 儲存體資料，同時有上傳和下載資料的能力，請考慮使用 Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="fa552-116">If you want an easy way to view your Azure Storage data while also having the ability to upload and download your data, then consider using an Azure Storage Explorer.</span></span>

<span data-ttu-id="fa552-117">若要深入了解，請參閱我們的 [Azure 儲存體總管](../storage-explorers.md) 清單。</span><span class="sxs-lookup"><span data-stu-id="fa552-117">Check out our list of [Azure Storage Explorers](../storage-explorers.md) to learn more.</span></span>

## <a name="system-administration"></a><span data-ttu-id="fa552-118">系統管理</span><span class="sxs-lookup"><span data-stu-id="fa552-118">System Administration</span></span>
<span data-ttu-id="fa552-119">如果您需要或比較熟悉命令列公用程式 (例如系統管理員)，以下是您應考慮的幾個選項︰</span><span class="sxs-lookup"><span data-stu-id="fa552-119">If you require or are more comfortable with a command-line utility (e.g. System Administrators), here are a few options for you to consider:</span></span>

### <a name="azcopy"></a><span data-ttu-id="fa552-120">AzCopy</span><span class="sxs-lookup"><span data-stu-id="fa552-120">AzCopy</span></span>
<span data-ttu-id="fa552-121">AzCopy 為 Windows 命令列公用程式，可以極高效能將資料複製到 Azure 儲存體，以及從 Azure 儲存體複製資料。</span><span class="sxs-lookup"><span data-stu-id="fa552-121">AzCopy is a Windows command-line utility designed for high-performance copying of data to and from Azure Storage.</span></span> <span data-ttu-id="fa552-122">您也可以複製儲存體帳戶內或不同儲存體帳戶之間的資料。</span><span class="sxs-lookup"><span data-stu-id="fa552-122">You can also copy data within a storage account, or between different storage accounts.</span></span>

<span data-ttu-id="fa552-123">若要深入了解，請參閱 [使用 AzCopy 命令列公用程式傳輸資料](storage-use-azcopy.md) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-123">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) to learn more.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="fa552-124">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa552-124">Azure PowerShell</span></span>
<span data-ttu-id="fa552-125">Azure PowerShell 模組提供 Cmdlet 讓您用於管理 Azure 上的服務。</span><span class="sxs-lookup"><span data-stu-id="fa552-125">Azure PowerShell is a module that provides cmdlets for managing services on Azure.</span></span> <span data-ttu-id="fa552-126">此模組為工作型的命令列 Shell 與指令碼語言，專為系統管理所設計。</span><span class="sxs-lookup"><span data-stu-id="fa552-126">It's a task-based command-line shell and scripting language designed especially for system administration.</span></span>

<span data-ttu-id="fa552-127">若要深入了解，請參閱 [搭配使用 Azure PowerShell 與 Azure 儲存體](storage-powershell-guide-full.md) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-127">See [Using Azure PowerShell with Azure Storage](storage-powershell-guide-full.md) to learn more.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="fa552-128">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fa552-128">Azure CLI</span></span>
<span data-ttu-id="fa552-129">Azure CLI 提供您一組開放原始碼的跨平台命令，供您使用 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="fa552-129">Azure CLI provides a set of open source, cross-platform commands for working with Azure services.</span></span> <span data-ttu-id="fa552-130">Azure CLI 可在 Windows、OSX 和 Linux 上使用。</span><span class="sxs-lookup"><span data-stu-id="fa552-130">Azure CLI is available on Windows, OSX, and Linux.</span></span>

<span data-ttu-id="fa552-131">若要深入了解，請參閱 [使用 Azure CLI 搭配 Azure 儲存體](../storage-azure-cli.md) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-131">See [Using the Azure CLI with Azure Storage](../storage-azure-cli.md) to learn more.</span></span>

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a><span data-ttu-id="fa552-132">以較慢的網路移動大量資料</span><span class="sxs-lookup"><span data-stu-id="fa552-132">Moving large amounts of data with a slow network</span></span>
<span data-ttu-id="fa552-133">與移動大量資料相關聯的最大挑戰之一是傳輸時間。</span><span class="sxs-lookup"><span data-stu-id="fa552-133">One of the biggest challenges associated with moving large amounts of data is the transfer time.</span></span> <span data-ttu-id="fa552-134">如果您想要從 Azure 儲存體來回取得資料，而不需擔心網路成本或撰寫程式碼，Azure 匯入/匯出會是適當的解決方案。</span><span class="sxs-lookup"><span data-stu-id="fa552-134">If you want to get data to/from Azure Storage without worrying about networks costs or writing code, then Azure Import/Export is an appropriate solution.</span></span>

<span data-ttu-id="fa552-135">若要深入了解，請參閱 [Azure 匯入/匯出](../storage-import-export-service.md) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-135">See [Azure Import/Export](../storage-import-export-service.md) to learn more.</span></span>

## <a name="backing-up-your-data"></a><span data-ttu-id="fa552-136">備份您的資料</span><span class="sxs-lookup"><span data-stu-id="fa552-136">Backing up your data</span></span>
<span data-ttu-id="fa552-137">如果您只需要將資料備份到 Azure 儲存體，Azure 備份是最好的選擇。</span><span class="sxs-lookup"><span data-stu-id="fa552-137">If you simply need to backup your data to Azure Storage, Azure Backup is the way to go.</span></span> <span data-ttu-id="fa552-138">對於備份內部部署資料和 Azure VM，這是功能強大的解決方案。</span><span class="sxs-lookup"><span data-stu-id="fa552-138">This is a powerful solution for backing up on-premises data and Azure VMs.</span></span>

<span data-ttu-id="fa552-139">若要深入了解，請參閱 [Azure 備份](../../backup/backup-introduction-to-azure-backup.md) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-139">See [Azure Backup](../../backup/backup-introduction-to-azure-backup.md) to learn more.</span></span>

## <a name="accessing-your-data-on-premises-and-from-the-cloud"></a><span data-ttu-id="fa552-140">存取內部部署資料和雲端的資料</span><span class="sxs-lookup"><span data-stu-id="fa552-140">Accessing your data on-premises and from the cloud</span></span>
<span data-ttu-id="fa552-141">如果您需要解決方案來存取內部部署資料和雲端的資料，您應該考慮使用 Azure 的混合式雲端儲存體解決方案，StorSimple。</span><span class="sxs-lookup"><span data-stu-id="fa552-141">If you need a solution for accessing your data on-premises and from the cloud, then you should consider using Azure's hybrid cloud storage solution, StorSimple.</span></span> <span data-ttu-id="fa552-142">此解決方案包含實體 StorSimple 裝置，以智慧方式將經常使用的資料儲存在 SSD 上，將偶爾使用的資料儲存在 HDD 上，並且將非作用中/備份/封存資料儲存在 Azure 儲存體上。</span><span class="sxs-lookup"><span data-stu-id="fa552-142">This solution consists of a physical StorSimple device that intelligently stores frequently used data on SSDs, occasionally used data on HDDs, and inactive/backup/archival data on Azure Storage.</span></span>

<span data-ttu-id="fa552-143">若要深入了解，請參閱 [StorSimple](../../storsimple/storsimple-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-143">See [StorSimple](../../storsimple/storsimple-overview.md) to learn more.</span></span>

## <a name="recovering-your-data"></a><span data-ttu-id="fa552-144">復原您的資料</span><span class="sxs-lookup"><span data-stu-id="fa552-144">Recovering your data</span></span>
<span data-ttu-id="fa552-145">當您擁有內部部署工作負載和應用程式，您需要可讓您在發生災害事件時繼續執行業務的解決方案。</span><span class="sxs-lookup"><span data-stu-id="fa552-145">When you have on-premises workloads and applications, you'll need a solution that allows your business to continue running in the event of a disaster.</span></span> <span data-ttu-id="fa552-146">Azure Site Recovery 可處理虛擬機器和實體伺服器的複寫、容錯移轉及復原作業。</span><span class="sxs-lookup"><span data-stu-id="fa552-146">Azure Site Recovery handles replication, failover, and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="fa552-147">複寫的資料會儲存在 Azure 儲存體，讓您不需要次要本地資料中心。</span><span class="sxs-lookup"><span data-stu-id="fa552-147">Replicated data is stored in Azure Storage, allowing you to eliminate the need for a secondary on-site datacenter.</span></span>

<span data-ttu-id="fa552-148">若要深入了解，請參閱 [Azure Site Recovery](../../site-recovery/site-recovery-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-148">See [Azure Site Recovery](../../site-recovery/site-recovery-overview.md) to learn more.</span></span>
### <a name="moving-data-faq"></a><span data-ttu-id="fa552-149">移動資料常見問題集︰</span><span class="sxs-lookup"><span data-stu-id="fa552-149">Moving Data FAQ:</span></span>
## <a name="can-i-migrate-vhds-from-one-region-to-another-without-copying"></a><span data-ttu-id="fa552-150">我可以在兩個區域之間移轉 VHD 而不要複製嗎？</span><span class="sxs-lookup"><span data-stu-id="fa552-150">Can I migrate VHDs from one region to another without copying?</span></span>
<span data-ttu-id="fa552-151">區域之間複製 VHD 的唯一方法是在每個區域的儲存體帳戶之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="fa552-151">The only way to copy VHDs between region is to copy the data between storage accounts on each region.</span></span> <span data-ttu-id="fa552-152">您可以使用 AZCopy 這樣做。</span><span class="sxs-lookup"><span data-stu-id="fa552-152">You can use AZCopy for this.</span></span> <span data-ttu-id="fa552-153">若要深入了解，請參閱「使用 AzCopy 命令列公用程式傳輸資料」。</span><span class="sxs-lookup"><span data-stu-id="fa552-153">See Transfer data with the AzCopy Command-Line Utility to learn more.</span></span> <span data-ttu-id="fa552-154">針對極大的資料量，您也可以使用 Azure 匯入/匯出。</span><span class="sxs-lookup"><span data-stu-id="fa552-154">For very large amounts of data, you can also Azure Import/Export.</span></span> <span data-ttu-id="fa552-155">若要深入了解，請參閱 [Azure 匯入/匯出](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) 。</span><span class="sxs-lookup"><span data-stu-id="fa552-155">See [Azure Import/Export](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) to learn more.</span></span>
