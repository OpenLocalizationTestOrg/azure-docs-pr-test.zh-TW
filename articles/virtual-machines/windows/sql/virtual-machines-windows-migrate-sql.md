---
title: "伺服器在 VM 上的 SQL Server 資料庫 tooSQL aaaMigrate |Microsoft 文件"
description: "深入了解如何 toomigrate 在內部部署使用者資料庫 tooSQL 伺服器在 Azure 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a><span data-ttu-id="b6bf6-103">移轉 SQL Server 資料庫 tooSQL Azure VM 中的伺服器</span><span class="sxs-lookup"><span data-stu-id="b6bf6-103">Migrate a SQL Server database tooSQL Server in an Azure VM</span></span>

<span data-ttu-id="b6bf6-104">有許多方法 toomigrate 在內部部署 SQL Server 使用者資料庫 tooSQL Azure VM 中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-104">There are a number of methods toomigrate an on-premises SQL Server user database tooSQL Server in an Azure VM.</span></span> <span data-ttu-id="b6bf6-105">這篇文章會簡要討論各種方法，並建議 hello 用於各種案例的最佳方法。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-105">This article will briefly discuss various methods and recommend hello best method for various scenarios.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a><span data-ttu-id="b6bf6-106">Hello 主要移轉方法有哪些？</span><span class="sxs-lookup"><span data-stu-id="b6bf6-106">What are hello primary migration methods?</span></span>
<span data-ttu-id="b6bf6-107">hello 移轉主要方法如下：</span><span class="sxs-lookup"><span data-stu-id="b6bf6-107">hello primary migration methods are:</span></span>

* <span data-ttu-id="b6bf6-108">執行內部部署備份使用壓縮，並手動複製 hello 備份檔案到 hello Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b6bf6-108">Perform on-premises backup using compression and manually copy hello backup file into hello Azure virtual machine</span></span>
* <span data-ttu-id="b6bf6-109">執行備份 tooURL 和還原成 hello hello URL 從 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b6bf6-109">Perform a backup tooURL and restore into hello Azure virtual machine from hello URL</span></span>
* <span data-ttu-id="b6bf6-110">卸離然後複製 hello 資料和記錄檔 tooAzure blob 儲存體，並從 URL 將 tooSQL Azure VM 中的伺服器</span><span class="sxs-lookup"><span data-stu-id="b6bf6-110">Detach and then copy hello data and log files tooAzure blob storage and then attach tooSQL Server in Azure VM from URL</span></span>
* <span data-ttu-id="b6bf6-111">轉換在內部部署實體機器 tooHyper V VHD、 上傳 tooAzure Blob 儲存體，並再部署新的 VM 使用上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="b6bf6-111">Convert on-premises physical machine tooHyper-V VHD, upload tooAzure Blob storage, and then deploy as new VM using uploaded VHD</span></span>
* <span data-ttu-id="b6bf6-112">使用 Windows 匯入/匯出服務寄送硬碟機</span><span class="sxs-lookup"><span data-stu-id="b6bf6-112">Ship hard drive using Windows Import/Export Service</span></span>
* <span data-ttu-id="b6bf6-113">如果您有 AlwaysOn 部署內部部署，請使用 hello[加入 Azure 複本精靈](../classic/sql-onprem-availability.md)toocreate Azure，然後容錯移轉，指向使用者 toohello Azure 的資料庫執行個體的複本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-113">If you have an AlwaysOn deployment on-premises, use hello [Add Azure Replica Wizard](../classic/sql-onprem-availability.md) toocreate a replica in Azure and then failover, pointing users toohello Azure database instance</span></span>
* <span data-ttu-id="b6bf6-114">使用 SQL Server[異動複寫](https://msdn.microsoft.com/library/ms151176.aspx)tooconfigure hello Azure SQL Server 執行個體標示為 「 訂閱者 」，然後再停用複寫，指向使用者 toohello Azure 的資料庫執行個體</span><span class="sxs-lookup"><span data-stu-id="b6bf6-114">Use SQL Server [transactional replication](https://msdn.microsoft.com/library/ms151176.aspx) tooconfigure hello Azure SQL Server instance as a subscriber and then disable replication, pointing users toohello Azure database instance</span></span>

> [!TIP]
> <span data-ttu-id="b6bf6-115">您也可以使用 Azure 中的 SQL Server Vm 之間的這些相同的技巧 toomove 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-115">You can also use these same techniques toomove databases between SQL Server VMs in Azure.</span></span> <span data-ttu-id="b6bf6-116">例如，沒有任何支援的方法 tooupgrade 從一個版本/版 tooanother 的 SQL Server 資源庫映像 VM。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-116">For example, there is no supported way tooupgrade a SQL Server gallery-image VM from one version/edition tooanother.</span></span> <span data-ttu-id="b6bf6-117">在此情況下，您應該使用 hello 新版本/版時，建立新的 SQL Server VM，然後使用 hello 移轉技術在此發行項 toomove 您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-117">In this case, you should create a new SQL Server VM with hello new version/edition, and then use one of hello migration techniques in this article toomove your databases.</span></span> 

## <a name="choosing-your-migration-method"></a><span data-ttu-id="b6bf6-118">選擇您的移轉方法</span><span class="sxs-lookup"><span data-stu-id="b6bf6-118">Choosing your migration method</span></span>
<span data-ttu-id="b6bf6-119">最佳的資料傳輸效能，如 hello 將資料庫檔案移轉到 hello Azure VM 使用壓縮的備份檔案。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-119">For optimum data transfer performance, migrate hello database files into hello Azure VM using a compressed backup file.</span></span>

<span data-ttu-id="b6bf6-120">toominimize hello 資料庫移轉程序期間的停機時間使用 hello AlwaysOn 選項或 hello 異動複寫選項。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-120">toominimize downtime during hello database migration process, use either hello AlwaysOn option or hello transactional replication option.</span></span>

<span data-ttu-id="b6bf6-121">如果不可能 toouse hello 上述方法，以手動方式移轉您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-121">If it is not possible toouse hello above methods, manually migrate your database.</span></span> <span data-ttu-id="b6bf6-122">使用此方法，您將通常開頭後面接著一份 hello 資料庫備份至 Azure 的資料庫備份，並執行資料庫還原。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-122">Using this method, you will generally start with a database backup followed by a copy of hello database backup into Azure and then perform a database restore.</span></span> <span data-ttu-id="b6bf6-123">您可以也將本身 hello 資料庫檔案複製到 Azure，然後將其連接。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-123">You can also copy hello database files themselves into Azure and then attach them.</span></span> <span data-ttu-id="b6bf6-124">若要將資料庫移轉到 Azure VM，有數種方法可以完成此手動程序。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-124">There are several methods by which you can accomplish this manual process of migrating a database into an Azure VM.</span></span>

> [!NOTE]
> <span data-ttu-id="b6bf6-125">當您從舊版 SQL Server 升級 tooSQL Server 2014 或 SQL Server 2016 時，您應該考慮是否需要變更。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-125">When you upgrade tooSQL Server 2014 or SQL Server 2016 from older versions of SQL Server, you should consider whether changes are needed.</span></span> <span data-ttu-id="b6bf6-126">我們建議您解決所有功能的相依性不支援 hello 新版本的 SQL Server 移轉專案的一部分。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-126">We recommend that you address all dependencies on features not supported by hello new version of SQL Server as part of your migration project.</span></span> <span data-ttu-id="b6bf6-127">如需支援的 hello 版本和案例的詳細資訊，請參閱[升級 tooSQL 伺服器](https://msdn.microsoft.com/library/bb677622.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-127">For more information on hello supported editions and scenarios, see [Upgrade tooSQL Server](https://msdn.microsoft.com/library/bb677622.aspx).</span></span>

<span data-ttu-id="b6bf6-128">hello 下表列出每個 hello 主要移轉方法，並討論 hello 使用每一種方法最適合。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-128">hello following table lists each of hello primary migration methods and discusses when hello use of each method is most appropriate.</span></span>

| <span data-ttu-id="b6bf6-129">方法</span><span class="sxs-lookup"><span data-stu-id="b6bf6-129">Method</span></span> | <span data-ttu-id="b6bf6-130">來源資料庫版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-130">Source database version</span></span> | <span data-ttu-id="b6bf6-131">目的地資料庫版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-131">Destination database version</span></span> | <span data-ttu-id="b6bf6-132">來源資料庫備份的大小條件約束</span><span class="sxs-lookup"><span data-stu-id="b6bf6-132">Source database backup size constraint</span></span> | <span data-ttu-id="b6bf6-133">注意事項</span><span class="sxs-lookup"><span data-stu-id="b6bf6-133">Notes</span></span> |
| --- | --- | --- | --- | --- |
| [<span data-ttu-id="b6bf6-134">執行內部部署備份使用壓縮，並手動複製 hello 備份檔案到 hello Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b6bf6-134">Perform on-premises backup using compression and manually copy hello backup file into hello Azure virtual machine</span></span>](#backup-and-restore) |<span data-ttu-id="b6bf6-135">SQL Server 2005 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-135">SQL Server 2005 or greater</span></span> |<span data-ttu-id="b6bf6-136">SQL Server 2005 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-136">SQL Server 2005 or greater</span></span> |[<span data-ttu-id="b6bf6-137">Azure VM 儲存體限制</span><span class="sxs-lookup"><span data-stu-id="b6bf6-137">Azure VM storage limit</span></span>](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | <span data-ttu-id="b6bf6-138">對於在電腦之間移動資料庫，這是非常簡單且通過完善測試的技術。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-138">This is a very simple and well-tested technique for moving databases across machines.</span></span> |
| [<span data-ttu-id="b6bf6-139">執行備份 tooURL 和還原成 hello hello URL 從 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b6bf6-139">Perform a backup tooURL and restore into hello Azure virtual machine from hello URL</span></span>](#backup-to-url-and-restore) |<span data-ttu-id="b6bf6-140">SQL Server 2012 SP1 CU2 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-140">SQL Server 2012 SP1 CU2 or greater</span></span> |<span data-ttu-id="b6bf6-141">SQL Server 2012 SP1 CU2 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-141">SQL Server 2012 SP1 CU2 or greater</span></span> |<span data-ttu-id="b6bf6-142">< 12.8 TB 適用於 SQL Server 2016，否則為 < 1 TB</span><span class="sxs-lookup"><span data-stu-id="b6bf6-142">< 12.8 TB for SQL Server 2016, otherwise < 1 TB</span></span> | <span data-ttu-id="b6bf6-143">這個方法是只是另一個方式 toomove hello 備份檔案 toohello VM 使用 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-143">This method is just another way toomove hello backup file toohello VM using Azure storage.</span></span> |
| [<span data-ttu-id="b6bf6-144">卸離然後複製 hello 資料和記錄檔 tooAzure blob 儲存體，並從 URL 將 Azure 虛擬機器中的 tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="b6bf6-144">Detach and then copy hello data and log files tooAzure blob storage and then attach tooSQL Server in Azure virtual machine from URL</span></span>](#detach-and-attach-from-url) |<span data-ttu-id="b6bf6-145">SQL Server 2005 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-145">SQL Server 2005 or greater</span></span> |<span data-ttu-id="b6bf6-146">SQL Server 2014 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-146">SQL Server 2014 or greater</span></span> |[<span data-ttu-id="b6bf6-147">Azure VM 儲存體限制</span><span class="sxs-lookup"><span data-stu-id="b6bf6-147">Azure VM storage limit</span></span>](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |<span data-ttu-id="b6bf6-148">使用這個方法，當您計劃太[儲存這些檔案的使用 hello Azure Blob 儲存體服務](https://msdn.microsoft.com/library/dn385720.aspx)並且將它們附加 tooSQL 伺服器執行於 Azure VM，特別是使用非常龐大的資料庫</span><span class="sxs-lookup"><span data-stu-id="b6bf6-148">Use this method when you plan too[store these files using hello Azure Blob storage service](https://msdn.microsoft.com/library/dn385720.aspx) and attach them tooSQL Server running in an Azure VM, particularly with very large databases</span></span> |
| [<span data-ttu-id="b6bf6-149">轉換在內部部署機器 tooHyper V Vhd 上傳 tooAzure Blob 儲存體，，然後部署新的虛擬機器使用上傳的 VHD</span><span class="sxs-lookup"><span data-stu-id="b6bf6-149">Convert on-premises machine tooHyper-V VHDs, upload tooAzure Blob storage, and then deploy a new virtual machine using uploaded VHD</span></span>](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |<span data-ttu-id="b6bf6-150">SQL Server 2005 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-150">SQL Server 2005 or greater</span></span> |<span data-ttu-id="b6bf6-151">SQL Server 2005 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-151">SQL Server 2005 or greater</span></span> |[<span data-ttu-id="b6bf6-152">Azure VM 儲存體限制</span><span class="sxs-lookup"><span data-stu-id="b6bf6-152">Azure VM storage limit</span></span>](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |<span data-ttu-id="b6bf6-153">使用時機[攜帶您自己的 SQL Server 授權](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md)，當您將較舊版本的 SQL Server 執行的資料庫移轉時，或移轉的系統和使用者資料庫的一部分的方式一起 hello 相依於其他資料庫的移轉使用者資料庫和/或系統資料庫。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-153">Use when [bringing your own SQL Server license](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), when migrating a database that you will run on an older version of SQL Server, or when migrating system and user databases together as part of hello migration of database dependent on other user databases and/or system databases.</span></span> |
| [<span data-ttu-id="b6bf6-154">使用 Windows 匯入/匯出服務寄送硬碟機</span><span class="sxs-lookup"><span data-stu-id="b6bf6-154">Ship hard drive using Windows Import/Export Service</span></span>](#ship-hard-drive) |<span data-ttu-id="b6bf6-155">SQL Server 2005 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-155">SQL Server 2005 or greater</span></span> |<span data-ttu-id="b6bf6-156">SQL Server 2005 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-156">SQL Server 2005 or greater</span></span> |[<span data-ttu-id="b6bf6-157">Azure VM 儲存體限制</span><span class="sxs-lookup"><span data-stu-id="b6bf6-157">Azure VM storage limit</span></span>](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |<span data-ttu-id="b6bf6-158">使用 hello [Windows 匯入/匯出服務](../../../storage/common/storage-import-export-service.md)時速度太慢，例如非常大型的資料庫手動複製方法</span><span class="sxs-lookup"><span data-stu-id="b6bf6-158">Use hello [Windows Import/Export Service](../../../storage/common/storage-import-export-service.md) when manual copy method is too slow, such as with very large databases</span></span> |
| [<span data-ttu-id="b6bf6-159">使用 hello 加入 Azure 複本精靈</span><span class="sxs-lookup"><span data-stu-id="b6bf6-159">Use hello Add Azure Replica Wizard</span></span>](../classic/sql-onprem-availability.md) |<span data-ttu-id="b6bf6-160">SQL Server 2012 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-160">SQL Server 2012 or greater</span></span> |<span data-ttu-id="b6bf6-161">SQL Server 2012 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-161">SQL Server 2012 or greater</span></span> |[<span data-ttu-id="b6bf6-162">Azure VM 儲存體限制</span><span class="sxs-lookup"><span data-stu-id="b6bf6-162">Azure VM storage limit</span></span>](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |<span data-ttu-id="b6bf6-163">可將停機時間縮到最短，請在您有內部部署的 AlwaysOn 部署時使用</span><span class="sxs-lookup"><span data-stu-id="b6bf6-163">Minimizes downtime, use when you have an AlwaysOn on-premises deployment</span></span> |
| [<span data-ttu-id="b6bf6-164">使用 SQL Server 異動複寫</span><span class="sxs-lookup"><span data-stu-id="b6bf6-164">Use SQL Server transactional replication</span></span>](https://msdn.microsoft.com/library/ms151176.aspx) |<span data-ttu-id="b6bf6-165">SQL Server 2005 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-165">SQL Server 2005 or greater</span></span> |<span data-ttu-id="b6bf6-166">SQL Server 2005 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b6bf6-166">SQL Server 2005 or greater</span></span> |[<span data-ttu-id="b6bf6-167">Azure VM 儲存體限制</span><span class="sxs-lookup"><span data-stu-id="b6bf6-167">Azure VM storage limit</span></span>](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |<span data-ttu-id="b6bf6-168">當您需要 toominimize 停機時間，而且沒有 AlwaysOn 之內部部署的使用</span><span class="sxs-lookup"><span data-stu-id="b6bf6-168">Use when you need toominimize downtime and do not have an AlwaysOn on-premises deployment</span></span> |

## <a name="backup-and-restore"></a><span data-ttu-id="b6bf6-169">備份與還原</span><span class="sxs-lookup"><span data-stu-id="b6bf6-169">Backup and restore</span></span>
<span data-ttu-id="b6bf6-170">備份壓縮資料庫，複製 hello 備份 toohello VM，並再還原 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-170">Back up your database with compression, copy hello backup toohello VM, and then restore hello database.</span></span> <span data-ttu-id="b6bf6-171">如果您的備份檔案是大於 1 TB，您必須等量分割它因為 hello VM 磁碟的大小上限為 1 TB。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-171">If your backup file is larger than 1 TB, you must stripe it because hello maximum size of a VM disk is 1 TB.</span></span> <span data-ttu-id="b6bf6-172">使用下列一般步驟 toomigrate 使用者資料庫，使用此手動方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6bf6-172">Use hello following general steps toomigrate a user database using this manual method:</span></span>

1. <span data-ttu-id="b6bf6-173">執行完整資料庫備份 tooan 在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-173">Perform a full database backup tooan on-premises location.</span></span>
2. <span data-ttu-id="b6bf6-174">建立或上傳具有 hello 版本的 SQL Server 所需的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-174">Create or upload a virtual machine with hello version of SQL Server desired.</span></span>
3. <span data-ttu-id="b6bf6-175">根據您的需求設定連線。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-175">Setup connectivity based on your requirements.</span></span> <span data-ttu-id="b6bf6-176">請參閱[連接 tooa Azure （資源管理員） 上的 SQL Server 虛擬機器](virtual-machines-windows-sql-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-176">See [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>
4. <span data-ttu-id="b6bf6-177">複製您的備份檔案 tooyour VM 使用遠端桌面、 Windows 檔案總管或 hello 複製命令的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-177">Copy your backup file(s) tooyour VM using remote desktop, Windows Explorer or hello copy command from a command prompt.</span></span>

## <a name="backup-toourl-and-restore"></a><span data-ttu-id="b6bf6-178">TooURL 備份與還原</span><span class="sxs-lookup"><span data-stu-id="b6bf6-178">Backup tooURL and restore</span></span>
<span data-ttu-id="b6bf6-179">而不是備份 tooa 本機檔案，您可以使用 hello[備份 tooURL](https://msdn.microsoft.com/library/dn435916.aspx)然後從 URL toohello VM 還原。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-179">Instead of backing up tooa local file, you can use hello [backup tooURL](https://msdn.microsoft.com/library/dn435916.aspx) and then restore from URL toohello VM.</span></span> <span data-ttu-id="b6bf6-180">SQL Server 2016，等量備份組、 的效能，建議使用和支援所需的每個 blob tooexceed hello 大小限制。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-180">With SQL Server 2016, striped backup sets are supported, are recommended for performance, and required tooexceed hello size limits per blob.</span></span> <span data-ttu-id="b6bf6-181">對於大型資料庫，hello 使用 hello [Windows 匯入/匯出服務](../../../storage/common/storage-import-export-service.md)建議。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-181">For very large databases, hello use of hello [Windows Import/Export Service](../../../storage/common/storage-import-export-service.md) is recommended.</span></span>

## <a name="detach-and-attach-from-url"></a><span data-ttu-id="b6bf6-182">從 URL 中斷連結和從 URL 連結</span><span class="sxs-lookup"><span data-stu-id="b6bf6-182">Detach and attach from URL</span></span>
<span data-ttu-id="b6bf6-183">卸離您的資料庫和記錄檔，並將它們傳送到太[Azure Blob 儲存體](https://msdn.microsoft.com/library/dn385720.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-183">Detach your database and log files and transfer them too[Azure Blob storage](https://msdn.microsoft.com/library/dn385720.aspx).</span></span> <span data-ttu-id="b6bf6-184">從 Azure VM 上的 hello URL，然後附加 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-184">Then attach hello database from hello URL on your Azure VM.</span></span> <span data-ttu-id="b6bf6-185">如果您想要在 Blob 儲存體中的 hello 實體資料庫檔案 tooreside，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-185">Use this if you want hello physical database files tooreside in Blob storage.</span></span> <span data-ttu-id="b6bf6-186">這對於非常大型的資料庫很實用。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-186">This might be useful for very large databases.</span></span> <span data-ttu-id="b6bf6-187">使用下列一般步驟 toomigrate 使用者資料庫，使用此手動方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6bf6-187">Use hello following general steps toomigrate a user database using this manual method:</span></span>

1. <span data-ttu-id="b6bf6-188">卸離 hello hello 在內部部署資料庫執行個體中的資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-188">Detach hello database files from hello on-premises database instance.</span></span>
2. <span data-ttu-id="b6bf6-189">Hello 卸離資料庫檔案複製到 Azure blob 儲存體使用 hello [AZCopy 命令列公用程式](../../../storage/common/storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-189">Copy hello detached database files into Azure blob storage using hello [AZCopy command-line utility](../../../storage/common/storage-use-azcopy.md).</span></span>
3. <span data-ttu-id="b6bf6-190">附加從 hello Azure URL toohello SQL Server 執行個體 hello Azure VM 中的 hello 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-190">Attach hello database files from hello Azure URL toohello SQL Server instance in hello Azure VM.</span></span>

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a><span data-ttu-id="b6bf6-191">轉換 tooVM 並上傳 tooURL 以及部署為新的 VM</span><span class="sxs-lookup"><span data-stu-id="b6bf6-191">Convert tooVM and upload tooURL and deploy as new VM</span></span>
<span data-ttu-id="b6bf6-192">在內部部署 SQL Server 執行個體 tooAzure 虛擬機器中使用此方法 toomigrate 所有系統和使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-192">Use this method toomigrate all system and user databases in an on-premises SQL Server instance tooAzure virtual machine.</span></span> <span data-ttu-id="b6bf6-193">使用下列一般步驟 toomigrate 整個 SQL Server 執行個體使用此手動方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6bf6-193">Use hello following general steps toomigrate an entire SQL Server instance using this manual method:</span></span>

1. <span data-ttu-id="b6bf6-194">轉換實體或虛擬機器使用 tooHyper V Vhd [Microsoft 虛擬機器轉換器](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-194">Convert physical or virtual machines tooHyper-V VHDs by using [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).</span></span>
2. <span data-ttu-id="b6bf6-195">上傳 VHD 檔案 tooAzure 儲存體使用 hello [Add-azurevhd cmdlet](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-195">Upload VHD files tooAzure Storage by using hello [Add-AzureVHD cmdlet](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).</span></span>
3. <span data-ttu-id="b6bf6-196">部署新虛擬機器使用 hello 上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-196">Deploy a new virtual machine by using hello uploaded VHD.</span></span>

> [!NOTE]
> <span data-ttu-id="b6bf6-197">toomigrate 整個應用程式，請考慮使用[Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)]。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-197">toomigrate an entire application, consider using [Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].</span></span>

## <a name="ship-hard-drive"></a><span data-ttu-id="b6bf6-198">寄送硬碟機</span><span class="sxs-lookup"><span data-stu-id="b6bf6-198">Ship hard drive</span></span>
<span data-ttu-id="b6bf6-199">使用 hello [Windows 匯入/匯出服務方法](../../../storage/common/storage-import-export-service.md)tootransfer 大量檔案資料 tooAzure Blob 儲存體中的情況下透過 hello 網路上傳極為耗費資源或不可行。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-199">Use hello [Windows Import/Export Service method](../../../storage/common/storage-import-export-service.md) tootransfer large amounts of file data tooAzure Blob storage in situations where uploading over hello network is prohibitively expensive or not feasible.</span></span> <span data-ttu-id="b6bf6-200">與此服務，您將一或多個硬碟機，包含該資料 tooan Azure 資料中心，將您的資料上傳 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-200">With this service, you send one or more hard drives containing that data tooan Azure data center, where your data will be uploaded tooyour storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6bf6-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6bf6-201">Next Steps</span></span>
<span data-ttu-id="b6bf6-202">如需在 Azure 虛擬機器上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-202">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="b6bf6-203">如需從擷取的映像建立 Azure SQL Server 虛擬機器的指示，請參閱[秘訣和訣竅上複製 Azure SQL 虛擬機器擷取映像從](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/)hello CSS SQL Server 工程師部落格上。</span><span class="sxs-lookup"><span data-stu-id="b6bf6-203">For instructions on creating an Azure SQL Server Virtual Machine from a captured image, see [Tips & Tricks on ‘cloning’ Azure SQL virtual machines from captured images](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) on hello CSS SQL Server Engineers blog.</span></span>
