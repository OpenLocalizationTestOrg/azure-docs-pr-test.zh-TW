---
title: "安裝 StorSimple Adapter for SharePoint | Microsoft Docs"
description: "描述如何在 SharePoint 伺服器陣列中安裝、設定或移除 StorSimple Adapter for SharePoint。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 8910471e09b9ecc797005818538ccfc6a91c68a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-the-storsimple-adapter-for-sharepoint"></a><span data-ttu-id="89152-103">安裝和設定 StorSimple Adapter for SharePoint</span><span class="sxs-lookup"><span data-stu-id="89152-103">Install and configure the StorSimple Adapter for SharePoint</span></span>
## <a name="overview"></a><span data-ttu-id="89152-104">Overview</span><span class="sxs-lookup"><span data-stu-id="89152-104">Overview</span></span>
<span data-ttu-id="89152-105">StorSimple Adapter for SharePoint 是可讓您提供 Microsoft Azure StorSimple 彈性儲存和資料保護給 SharePoint 伺服器陣列的元件。</span><span class="sxs-lookup"><span data-stu-id="89152-105">The StorSimple Adapter for SharePoint is a component that lets you provide Microsoft Azure StorSimple flexible storage and data protection to SharePoint server farms.</span></span> <span data-ttu-id="89152-106">您可以使用配接器將二進位大型物件 (BLOB) 內容從 SQL Server 內容資料庫移至 Microsoft Azure StorSimple 混合雲端儲存體裝置。</span><span class="sxs-lookup"><span data-stu-id="89152-106">You can use the adapter to move Binary Large Object (BLOB) content from the SQL Server content databases to the Microsoft Azure StorSimple hybrid cloud storage device.</span></span>

<span data-ttu-id="89152-107">StorSimple Adapter for SharePoint 作為遠端 BLOB 儲存 (RBS) 提供者，使用 SQL Server 遠端 BLOB 儲存功能將非結構化 SharePoint 內容 (以 BLOB 形式)，儲存在 StorSimple 裝置所支援的檔案伺服器上。</span><span class="sxs-lookup"><span data-stu-id="89152-107">The StorSimple Adapter for SharePoint functions as a Remote BLOB Storage (RBS) provider and uses the SQL Server Remote BLOB Storage feature to store unstructured SharePoint content (in the form of BLOBs) on a file server that is backed by a StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="89152-108">StorSimple Adapter for SharePoint 支援 SharePoint Server 2010 遠端 BLOB 儲存 (RBS)。</span><span class="sxs-lookup"><span data-stu-id="89152-108">The StorSimple Adapter for SharePoint supports SharePoint Server 2010 Remote BLOB Storage (RBS).</span></span> <span data-ttu-id="89152-109">它不支援 SharePoint Server 2010 外部 BLOB 儲存體 (EBS)。</span><span class="sxs-lookup"><span data-stu-id="89152-109">It does not support SharePoint Server 2010 External BLOB Storage (EBS).</span></span>


* <span data-ttu-id="89152-110">若要下載 StorSimple Adapter for SharePoint，請移至 Microsoft 下載中心的 [StorSimple Adapter for SharePoint][1]。</span><span class="sxs-lookup"><span data-stu-id="89152-110">To download the StorSimple Adapter for SharePoint, go to [StorSimple Adapter for SharePoint][1] in the Microsoft Download Center.</span></span>
* <span data-ttu-id="89152-111">如需有關規劃 RBS 和 RBS 限制的資訊，請移至[決定在 SharePoint 2013 中使用 RBS][2] 或[規劃 RBS (SharePoint Server 2010)][3]。</span><span class="sxs-lookup"><span data-stu-id="89152-111">For information about planning for RBS and RBS limitations, go to [Deciding to use RBS in SharePoint 2013][2] or [Plan for RBS (SharePoint Server 2010)][3].</span></span>

<span data-ttu-id="89152-112">此概觀的其餘部分簡短說明 StorSimple Adapter for SharePoint 的角色，以及您在安裝和設定配接器之前，應該注意的 SharePoint 容量和效能限制。</span><span class="sxs-lookup"><span data-stu-id="89152-112">The rest of this overview briefly describes the role of the StorSimple Adapter for SharePoint and the SharePoint capacity and performance limits that you should be aware of before you install and configure the adapter.</span></span> <span data-ttu-id="89152-113">檢閱此資訊之後，請移至 [StorSimple Adapter for SharePoint 安裝](#storsimple-adapter-for-sharepoint-installation) 開始設定配接器。</span><span class="sxs-lookup"><span data-stu-id="89152-113">After you review this information, go to [StorSimple Adapter for SharePoint installation](#storsimple-adapter-for-sharepoint-installation) to begin setting up the adapter.</span></span>

### <a name="storsimple-adapter-for-sharepoint-benefits"></a><span data-ttu-id="89152-114">StorSimple Adapter for SharePoint 優點</span><span class="sxs-lookup"><span data-stu-id="89152-114">StorSimple Adapter for SharePoint benefits</span></span>
<span data-ttu-id="89152-115">在 SharePoint 網站中，內容會在一個或多個內容資料庫中儲存為非結構化 BLOB 資料。</span><span class="sxs-lookup"><span data-stu-id="89152-115">In a SharePoint site, content is stored as unstructured BLOB data in one or more content databases.</span></span> <span data-ttu-id="89152-116">根據預設，這些資料庫裝載於執行 SQL Server 且位於 SharePoint 伺服器陣列中的電腦上。</span><span class="sxs-lookup"><span data-stu-id="89152-116">By default, these databases are hosted on computers that are running SQL Server and are located in the SharePoint server farm.</span></span> <span data-ttu-id="89152-117">BLOB 可能快速增大，耗用大量的內部部署儲存體。</span><span class="sxs-lookup"><span data-stu-id="89152-117">BLOBs can rapidly increase in size, consuming large amounts of on-premises storage.</span></span> <span data-ttu-id="89152-118">因此，您可能想要尋找另一個較便宜的儲存體解決方案。</span><span class="sxs-lookup"><span data-stu-id="89152-118">For this reason, you might want to find another, less-expensive storage solution.</span></span> <span data-ttu-id="89152-119">SQL Server 提供一種稱為遠端 Blob 儲存 (RBS) 的技術，可讓您將 BLOB 內容儲存在檔案系統 (在 SQL Server 資料庫之外)。</span><span class="sxs-lookup"><span data-stu-id="89152-119">SQL Server provides a technology called Remote Blob Storage (RBS) that lets you store BLOB content in the file system, outside the SQL Server database.</span></span> <span data-ttu-id="89152-120">運用 RBS 時，Blob 可以位於執行 SQL Server 的電腦上的檔案系統，或儲存在另一部伺服器電腦上的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="89152-120">With RBS, BLOBs can reside in the file system on the computer that is running SQL Server, or they can be stored in the file system on another server computer.</span></span>

<span data-ttu-id="89152-121">RBS 要求您必須使用 RBS 提供者，例如 StorSimple Adapter for SharePoint，才能在 SharePoint 中啟用 RBS。</span><span class="sxs-lookup"><span data-stu-id="89152-121">RBS requires that you use an RBS provider, such as the StorSimple Adapter for SharePoint, to enable RBS in SharePoint.</span></span> <span data-ttu-id="89152-122">StorSimple Adapter for SharePoint 可搭配 RBS，讓您將 BLOB 移至 Microsoft Azure StorSimple 系統所支援的伺服器。</span><span class="sxs-lookup"><span data-stu-id="89152-122">The StorSimple Adapter for SharePoint works with RBS, letting you move BLOBs to a server backed up by the Microsoft Azure StorSimple system.</span></span> <span data-ttu-id="89152-123">Microsoft Azure StorSimple 接著可根據使用方式，在本機或在雲端中儲存 BLOB 資料。</span><span class="sxs-lookup"><span data-stu-id="89152-123">Microsoft Azure StorSimple then stores the BLOB data locally or in the cloud, based on usage.</span></span> <span data-ttu-id="89152-124">非常活躍的 BLOB (通常稱為第 1 層或熱門資料) 位在本機。</span><span class="sxs-lookup"><span data-stu-id="89152-124">BLOBs that are very active (typically referred to as Tier 1 or hot data) reside locally.</span></span> <span data-ttu-id="89152-125">較不活躍的資料和封存資料則位於雲端。</span><span class="sxs-lookup"><span data-stu-id="89152-125">Less active data and archival data reside in the cloud.</span></span> <span data-ttu-id="89152-126">在內容資料庫上啟用 RBS 之後，任何在 SharePoint 中建立的新 BLOB 內容會儲存在 StorSimple 裝置上，而不是在內容資料庫中。</span><span class="sxs-lookup"><span data-stu-id="89152-126">After you enable RBS on a content database, any new BLOB content created in SharePoint is stored on the StorSimple device and not in the content database.</span></span>

<span data-ttu-id="89152-127">RBS 的 Microsoft Azure StorSimple 實作提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="89152-127">The Microsoft Azure StorSimple implementation of RBS provides the following benefits:</span></span>

* <span data-ttu-id="89152-128">將 BLOB 內容移至另一個伺服器可以減輕 SQL Server 上的查詢負荷，改善 SQL Server 的回應能力。</span><span class="sxs-lookup"><span data-stu-id="89152-128">By moving BLOB content to a separate server, you can reduce the query load on SQL Server, which can improve SQL Server responsiveness.</span></span> 
* <span data-ttu-id="89152-129">Azure StorSimple 使用重複資料刪除和壓縮來減少資料大小。</span><span class="sxs-lookup"><span data-stu-id="89152-129">Azure StorSimple uses deduplication and compression to reduce data size.</span></span>
* <span data-ttu-id="89152-130">Azure StorSimple 以本機和雲端快照集的形式提供資料保護。</span><span class="sxs-lookup"><span data-stu-id="89152-130">Azure StorSimple provides data protection in the form of local and cloud snapshots.</span></span> <span data-ttu-id="89152-131">此外，如果您將資料庫本身放在 StorSimple 裝置，您可以用當機時保持一致的方式將內容資料庫和 BLOB 備份在一起。</span><span class="sxs-lookup"><span data-stu-id="89152-131">Also, if you place the database itself on the StorSimple device, you can back up the content database and BLOBs together in a crash consistent way.</span></span> <span data-ttu-id="89152-132">(僅 StorSimple 8000 系列裝置支援將內容資料庫移至裝置。</span><span class="sxs-lookup"><span data-stu-id="89152-132">(Moving the content database to the device is only supported for the StorSimple 8000 series device.</span></span> <span data-ttu-id="89152-133">5000 或 7000 系列不支援這項功能。)</span><span class="sxs-lookup"><span data-stu-id="89152-133">This feature is not supported for the 5000 or 7000 series.)</span></span>
* <span data-ttu-id="89152-134">Azure StorSimple 包含災害復原功能，包括容錯移轉、檔案和磁碟區復原 (包括測試復原) 及快速還原資料。</span><span class="sxs-lookup"><span data-stu-id="89152-134">Azure StorSimple includes disaster recovery features including failover, file and volume recovery (including test recovery), and rapid restoration of data.</span></span>
* <span data-ttu-id="89152-135">您可以使用資料復原軟體，例如 Kroll Ontrack PowerControls，並搭配 BLOB 資料的 StorSimple 快照集，在項目層級復原 SharePoint 內容。</span><span class="sxs-lookup"><span data-stu-id="89152-135">You can use data recovery software, such as Kroll Ontrack PowerControls, with StorSimple snapshots of BLOB data to perform item-level recovery of SharePoint content.</span></span> <span data-ttu-id="89152-136">(此資料復原軟體需另外購買)。</span><span class="sxs-lookup"><span data-stu-id="89152-136">(This data recovery software is a separate purchase.)</span></span>
* <span data-ttu-id="89152-137">StorSimple Adapter for SharePoint 外掛到 SharePoint 管理中心入口網站，可讓您從中央位置管理整個 SharePoint 解決方案。</span><span class="sxs-lookup"><span data-stu-id="89152-137">The StorSimple Adapter for SharePoint plugs into the SharePoint Central Administration portal, allowing you to manage your entire SharePoint solution from a central location.</span></span>

<span data-ttu-id="89152-138">將 BLOB 內容移至檔案系統可以節省更多成本並提供其他優點。</span><span class="sxs-lookup"><span data-stu-id="89152-138">Moving BLOB content to the file system can provide other cost savings and benefits.</span></span> <span data-ttu-id="89152-139">例如，使用 RBS 就不需要購買昂貴的第 1 層儲存體，也而因為它會縮小內容資料庫，RBS 可減少 SharePoint 伺服器陣列中所需的資料庫數目。</span><span class="sxs-lookup"><span data-stu-id="89152-139">For example, using RBS can reduce the need for expensive Tier 1 storage and, because it shrinks the content database, RBS can reduce the number of databases required in the SharePoint server farm.</span></span> <span data-ttu-id="89152-140">不過，其他因素也會影響儲存需求，例如資料庫大小限制和非 RBS 內容數量。</span><span class="sxs-lookup"><span data-stu-id="89152-140">However, other factors, such as database size limits and the amount of non-RBS content, can also affect storage requirements.</span></span> <span data-ttu-id="89152-141">如需有關使用 RBS 的優點與成本的詳細資訊，請參閱[規劃 RBS (SharePoint Foundation 2010)][4] 和[決定在 SharePoint 2013 中使用 RBS][5]。</span><span class="sxs-lookup"><span data-stu-id="89152-141">For more information about the costs and benefits of using RBS, see [Plan for RBS (SharePoint Foundation 2010)][4] and [Deciding to use RBS in SharePoint 2013][5].</span></span>

### <a name="capacity-and-performance-limits"></a><span data-ttu-id="89152-142">容量和效能限制</span><span class="sxs-lookup"><span data-stu-id="89152-142">Capacity and performance limits</span></span>
<span data-ttu-id="89152-143">在考慮於 SharePoint 解決方案中使用 RBS 之前，您應該注意 SharePoint Server 2010 和 SharePoint Server 2013 已測試的效能和容量限制，以及這些限制與可接受的效能有何關係。</span><span class="sxs-lookup"><span data-stu-id="89152-143">Before you consider using RBS in your SharePoint solution, you should be aware of the tested performance and capacity limits of SharePoint Server 2010 and SharePoint Server 2013, and how these limits relate to acceptable performance.</span></span> <span data-ttu-id="89152-144">如需詳細資訊，請參閱 [SharePoint 2013 的軟體界限及限制](https://technet.microsoft.com/library/cc262787.aspx)。</span><span class="sxs-lookup"><span data-stu-id="89152-144">For more information, see [Software Boundaries and Limits for SharePoint 2013](https://technet.microsoft.com/library/cc262787.aspx).</span></span>

<span data-ttu-id="89152-145">設定 RBS 之前，請檢閱下列事項：</span><span class="sxs-lookup"><span data-stu-id="89152-145">Review the following before you configure RBS:</span></span>

* <span data-ttu-id="89152-146">請確定內容的大小總計 (內容資料庫大小，加上任何相關聯的外部化 BLOB 大小) 不超過 SharePoint 所支援的 RBS 大小限制。</span><span class="sxs-lookup"><span data-stu-id="89152-146">Make sure that the total size of the content (the size of a content database plus the size of any associated externalized BLOBs) does not exceed the RBS size limit supported by SharePoint.</span></span> <span data-ttu-id="89152-147">這項限制為 200 GB。</span><span class="sxs-lookup"><span data-stu-id="89152-147">This limit is 200 GB.</span></span> 
  
    <span data-ttu-id="89152-148">**測量內容資料庫和 BLOB 大小**</span><span class="sxs-lookup"><span data-stu-id="89152-148">**To measure content database and BLOB size**</span></span>
  
  1. <span data-ttu-id="89152-149">在中央管理 WFE 上執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="89152-149">Run this query on the Central Administration WFE.</span></span> <span data-ttu-id="89152-150">啟動 SharePoint 管理命令介面，然後輸入下列 Windows PowerShell 命令來取得內容資料庫的大小：</span><span class="sxs-lookup"><span data-stu-id="89152-150">Start the SharePoint Management Shell, and then enter the following Windows PowerShell command to get the size of the content databases:</span></span>
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      <span data-ttu-id="89152-151">此步驟取得磁碟上的內容資料庫大小。</span><span class="sxs-lookup"><span data-stu-id="89152-151">This step gets the size of the content database on the disk.</span></span>
  2. <span data-ttu-id="89152-152">SQL Management Studio 的 SQL Server 方塊中，對每個內容資料庫執行下列 SQL 查詢，然後將結果和步驟 1 取得的數字相加。</span><span class="sxs-lookup"><span data-stu-id="89152-152">Run one of the following SQL queries in SQL Management Studio on the SQL server box on each content database, and add the result to the number obtained in step 1.</span></span>
     
     <span data-ttu-id="89152-153">在 SharePoint 2013 內容資料庫中，輸入：</span><span class="sxs-lookup"><span data-stu-id="89152-153">On SharePoint 2013 content databases, enter:</span></span>
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     <span data-ttu-id="89152-154">在 SharePoint 2010 內容資料庫中，輸入：</span><span class="sxs-lookup"><span data-stu-id="89152-154">On SharePoint 2010 content databases, enter:</span></span>
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     <span data-ttu-id="89152-155">此步驟取得已外部化的 BLOB 大小。</span><span class="sxs-lookup"><span data-stu-id="89152-155">This step gets the size of the BLOBs that have been externalized.</span></span>
* <span data-ttu-id="89152-156">我們建議您將所有 BLOB 和資料庫內容儲存在 StorSimple 裝置本機。</span><span class="sxs-lookup"><span data-stu-id="89152-156">We recommend that you store all BLOB and database content locally on the StorSimple device.</span></span> <span data-ttu-id="89152-157">StorSimple 裝置是提供高可用性的雙節點叢集。</span><span class="sxs-lookup"><span data-stu-id="89152-157">The StorSimple device is a two-node cluster for high availability.</span></span> <span data-ttu-id="89152-158">將內容資料庫和 BLOB 放在 StorSimple 裝置上提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="89152-158">Placing the content databases and BLOBs on the StorSimple device provides high availability.</span></span>
  
    <span data-ttu-id="89152-159">使用傳統的 SQL Server 移轉最佳作法，將內容資料庫移至 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="89152-159">Use traditional SQL Server migration best practices to move the content database to the StorSimple device.</span></span> <span data-ttu-id="89152-160">只有在資料庫的所有 BLOB 內容，都透過 RBS 移至檔案共用之後，才移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="89152-160">Move the database only after all BLOB content from the database has been moved to the file share via RBS.</span></span> <span data-ttu-id="89152-161">如果您選擇將內容資料庫移至 StorSimple 裝置，我們建議您在裝置上將內容資料庫儲存體設定為主要磁碟區。</span><span class="sxs-lookup"><span data-stu-id="89152-161">If you choose to move the content database to the StorSimple device, we recommend that you configure the content database storage on the device as a primary volume.</span></span>
* <span data-ttu-id="89152-162">在 Microsoft Azure StorSimple 中，如果使用分層磁碟區，則無法保證儲存在 StorSimple 裝置本機的內容不會移至 Microsoft Azure 雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="89152-162">In Microsoft Azure StorSimple, if using tiered volumes, there is no way to guarantee that content stored locally on the StorSimple device will not be tiered to Microsoft Azure cloud storage.</span></span> <span data-ttu-id="89152-163">因此，建議您搭配 SharePoint RBS 使用 StorSimple 本機固定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="89152-163">Hence, we recommend using StorSimple locally pinned volumes in conjunction with SharePoint RBS.</span></span> <span data-ttu-id="89152-164">這可確保所有 BLOB 內容保留在本機 StorSimple 裝置上，而不會移至 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="89152-164">This will ensure that all BLOB content remains locally on the StorSimple device, and is not moved to Microsoft Azure.</span></span>
* <span data-ttu-id="89152-165">如果您不在 StorSimple 裝置上儲存的內容資料庫，請使用支援 RBS 的傳統 SQL Server 高可用性最佳作法。</span><span class="sxs-lookup"><span data-stu-id="89152-165">If you do not store the content databases on the StorSimple device, use traditional SQL Server high availability best practices that support RBS.</span></span> <span data-ttu-id="89152-166">SQL Server 叢集支援 RBS，而 SQL Server 鏡像不支援 RBS。</span><span class="sxs-lookup"><span data-stu-id="89152-166">SQL Server clustering supports RBS, while SQL Server mirroring does not.</span></span> 

> [!WARNING]
> <span data-ttu-id="89152-167">如果您尚未啟用 RBS，我們不建議您將內容資料庫移至 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="89152-167">If you have not enabled RBS, we do not recommend moving the content database to the StorSimple device.</span></span> <span data-ttu-id="89152-168">這是未經過測試的設定。</span><span class="sxs-lookup"><span data-stu-id="89152-168">This is an untested configuration.</span></span>

## <a name="storsimple-adapter-for-sharepoint-installation"></a><span data-ttu-id="89152-169">StorSimple Adapter for SharePoint 安裝</span><span class="sxs-lookup"><span data-stu-id="89152-169">StorSimple Adapter for SharePoint installation</span></span>
<span data-ttu-id="89152-170">您必須設定 StorSimple 裝置，並確定 SharePoint 伺服器陣列和 SQL Server 具現化符合所有必要條件，才能安裝 StorSimple Adapter for SharePoint。</span><span class="sxs-lookup"><span data-stu-id="89152-170">Before you can install the StorSimple Adapter for SharePoint, you must configure the StorSimple device and make sure that the SharePoint server farm and SQL Server instantiation meet all prerequisites.</span></span> <span data-ttu-id="89152-171">本教學課程描述 StorSimple Adapter for SharePoint 的組態需求，以及安裝和升級程序。</span><span class="sxs-lookup"><span data-stu-id="89152-171">This tutorial describes configuration requirements, as well as procedures for installing and upgrading the StorSimple Adapter for SharePoint.</span></span>

## <a name="configure-prerequisites"></a><span data-ttu-id="89152-172">設定必要條件</span><span class="sxs-lookup"><span data-stu-id="89152-172">Configure prerequisites</span></span>
<span data-ttu-id="89152-173">您必須確定 StorSimple 裝置、SharePoint 伺服器陣列和 SQL Server 具現化符合下列必要條件，才能安裝 StorSimple Adapter for SharePoint。</span><span class="sxs-lookup"><span data-stu-id="89152-173">Before you can install the StorSimple Adapter for SharePoint, make sure that the StorSimple device, SharePoint server farm, and SQL Server instantiation meet the following prerequisites.</span></span>

### <a name="system-requirements"></a><span data-ttu-id="89152-174">系統需求</span><span class="sxs-lookup"><span data-stu-id="89152-174">System requirements</span></span>
<span data-ttu-id="89152-175">StorSimple Adapter for SharePoint 適用於下列的硬體和軟體：</span><span class="sxs-lookup"><span data-stu-id="89152-175">The StorSimple Adapter for SharePoint works with the following hardware and software:</span></span>

* <span data-ttu-id="89152-176">支援的作業系統 – Windows Server 2008 R2 SP1、Windows Server 2012 或 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="89152-176">Supported operating system – Windows Server 2008 R2 SP1, Windows Server 2012, or Windows Server 2012 R2</span></span>
* <span data-ttu-id="89152-177">支援的 SharePoint 版本 – SharePoint Server 2010 或 SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="89152-177">Supported SharePoint versions – SharePoint Server 2010 or SharePoint Server 2013</span></span>
* <span data-ttu-id="89152-178">支援的 SQL Server 版本 – SQL Server 2008 Enterprise Edition、SQL Server 2008 R2 Enterprise Edition 或 SQL Server 2012 Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="89152-178">Supported SQL Server versions – SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition, or SQL Server 2012 Enterprise Edition</span></span>
* <span data-ttu-id="89152-179">支援的 StorSimple 裝置 – StorSimple 8000 系列、StorSimple 7000 系列或 StorSimple 5000 系列。</span><span class="sxs-lookup"><span data-stu-id="89152-179">Supported StorSimple devices – StorSimple 8000 series, StorSimple 7000 series, or StorSimple 5000 series.</span></span>

### <a name="storsimple-device-configuration-prerequisites"></a><span data-ttu-id="89152-180">StorSimple 裝置組態必要條件</span><span class="sxs-lookup"><span data-stu-id="89152-180">StorSimple device configuration prerequisites</span></span>
<span data-ttu-id="89152-181">StorSimple 裝置是一種區塊裝置，因此需要可裝載資料的檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="89152-181">The StorSimple device is a block device and as such requires a file server on which the data can be hosted.</span></span> <span data-ttu-id="89152-182">我們建議您使用另外的伺服器，而不是 SharePoint 伺服器陣列中現有的伺服器。</span><span class="sxs-lookup"><span data-stu-id="89152-182">We recommend that you use a separate server rather than an existing server from the SharePoint farm.</span></span> <span data-ttu-id="89152-183">此檔案伺服器必須與裝載內容資料庫的 SQL Server 電腦位於相同的區域網路 (LAN)。</span><span class="sxs-lookup"><span data-stu-id="89152-183">This file server must be on the same local area network (LAN) as the SQL Server computer that hosts the content databases.</span></span>

> [!TIP]
> * <span data-ttu-id="89152-184">如果您為了高可用性而設定 SharePoint 伺服器陣列，則也應該為了高可用性而部署檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="89152-184">If you configure your SharePoint farm for high availability, you should deploy the file server for high availability also.</span></span>
> * <span data-ttu-id="89152-185">如果您不在 StorSimple 裝置上儲存的內容資料庫，請使用支援 RBS 的傳統高可用性最佳作法。</span><span class="sxs-lookup"><span data-stu-id="89152-185">If you do not store the content database on the StorSimple device, use traditional high availability best practices that support RBS.</span></span> <span data-ttu-id="89152-186">SQL Server 叢集支援 RBS，而 SQL Server 鏡像不支援 RBS。</span><span class="sxs-lookup"><span data-stu-id="89152-186">SQL Server clustering supports RBS, while SQL Server mirroring does not.</span></span> 


<span data-ttu-id="89152-187">請確定您的 StorSimple 裝置已正確設定，也已設定適當的磁碟區來支援 SharePoint 部署，且可以從 SQL Server 電腦存取。</span><span class="sxs-lookup"><span data-stu-id="89152-187">Make sure that your StorSimple device is configured correctly, and that appropriate volumes to support your SharePoint deployment are configured and accessible from your SQL Server computer.</span></span> <span data-ttu-id="89152-188">如果您尚未部署和設定您的 StorSimple 裝置，請移至 [部署內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md) 。</span><span class="sxs-lookup"><span data-stu-id="89152-188">Go to [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md) if you have not yet deployed and configured your StorSimple device.</span></span> <span data-ttu-id="89152-189">請記下 StorSimple 裝置的 IP 位址，StorSimple Adapter for SharePoint 安裝期間需要用到。</span><span class="sxs-lookup"><span data-stu-id="89152-189">Note the IP address of the StorSimple device; you will need it during StorSimple Adapter for SharePoint installation.</span></span>

<span data-ttu-id="89152-190">此外，請確定要用於 BLOB 外部化的磁碟區符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="89152-190">In addition, make sure that the volume to be used for BLOB externalization meets the following requirements:</span></span>

* <span data-ttu-id="89152-191">此磁碟區必須使用 64 KB 配置單位大小格式化。</span><span class="sxs-lookup"><span data-stu-id="89152-191">The volume must be formatted with a 64 KB allocation unit size.</span></span>
* <span data-ttu-id="89152-192">Web 前端 (WFE) 和應用程式伺服器必須能夠透過通用命名慣例 (UNC) 路徑來存取此磁碟區。</span><span class="sxs-lookup"><span data-stu-id="89152-192">Your web front end (WFE) and application servers must be able to access the volume via a Universal Naming Convention (UNC) path.</span></span>
* <span data-ttu-id="89152-193">SharePoint 伺服器陣列必須設定為寫入此磁碟區。</span><span class="sxs-lookup"><span data-stu-id="89152-193">The SharePoint server farm must be configured to write to the volume.</span></span>

> [!NOTE]
> <span data-ttu-id="89152-194">安裝和設定配接器之後，所有 BLOB 外部化都必須透過 StorSimple 裝置進行 (此裝置會向 SQL Server 呈現磁碟區並管理儲存層)。</span><span class="sxs-lookup"><span data-stu-id="89152-194">After you install and configure the adapter, all BLOB externalization must go through the StorSimple device (the device will present the volumes to SQL Server and manage the storage tiers).</span></span> <span data-ttu-id="89152-195">您無法使用任何其他目標進行 BLOB 外部化。</span><span class="sxs-lookup"><span data-stu-id="89152-195">You cannot use any other targets for BLOB externalization.</span></span>


<span data-ttu-id="89152-196">如果您打算使用 StorSimple Snapshot Manager 建立 BLOB 和資料庫資料的快照集，務必將 StorSimple Snapshot Manager 安裝在資料庫伺服器上，它才能使用 SQL 寫入器服務來實作 Windows 磁碟區陰影複製服務 (VSS)。</span><span class="sxs-lookup"><span data-stu-id="89152-196">If you plan to use StorSimple Snapshot Manager to take snapshots of the BLOB and database data, be sure to install StorSimple Snapshot Manager on the database server so that it can use the SQL Writer Service to implement the Windows Volume Shadow Copy Service (VSS).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89152-197">StorSimple Snapshot Manager 不支援 SharePoint VSS 寫入器，無法建立 SharePoint 資料的應用程式一致快照集。</span><span class="sxs-lookup"><span data-stu-id="89152-197">StorSimple Snapshot Manager does not support the SharePoint VSS Writer and cannot take application-consistent snapshots of SharePoint data.</span></span> <span data-ttu-id="89152-198">在 SharePoint 案例中，StorSimple Snapshot Manager 只提供當機時保持一致的備份。</span><span class="sxs-lookup"><span data-stu-id="89152-198">In a SharePoint scenario, StorSimple Snapshot Manager provides only crash-consistent backups.</span></span>


## <a name="sharepoint-farm-configuration-prerequisites"></a><span data-ttu-id="89152-199">SharePoint 伺服器陣列組態必要條件</span><span class="sxs-lookup"><span data-stu-id="89152-199">SharePoint farm configuration prerequisites</span></span>
<span data-ttu-id="89152-200">請確定您的 SharePoint 伺服器陣列已正確設定，如下：</span><span class="sxs-lookup"><span data-stu-id="89152-200">Make sure that your SharePoint server farm is correctly configured, as follows:</span></span>

* <span data-ttu-id="89152-201">確認您的 SharePoint 伺服器陣列處於良好狀態，並檢查下列項目:</span><span class="sxs-lookup"><span data-stu-id="89152-201">Verify that your SharePoint server farm is in a healthy state, and check the following:</span></span>
* <span data-ttu-id="89152-202">所有在伺服陣列中註冊的 SharePoint WFE 和應用程式伺服器正在執行，而且可以從您將安裝 StorSimple Adapter for SharePoint 伺服器進行 Ping。</span><span class="sxs-lookup"><span data-stu-id="89152-202">All SharePoint WFE and application servers registered in the farm are running and can be pinged from the server on which you will be installing the StorSimple Adapter for SharePoint.</span></span>
* <span data-ttu-id="89152-203">SharePoint 計時器服務 (SPTimerV3 或 SPTimerV4) 正在每一部 WFE 伺服器和應用程式伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="89152-203">The SharePoint Timer service (SPTimerV3 or SPTimerV4) is running on each WFE server and application server.</span></span>
* <span data-ttu-id="89152-204">SharePoint 計時器服務和用來執行 SharePoint 管理中心網站的 IIS 應用程式集區，具有系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="89152-204">Both the SharePoint Timer service and the IIS application pool under which the SharePoint Central Administration site is running have administrative privileges.</span></span>
* <span data-ttu-id="89152-205">請確定已停用 Internet Explorer 增強式安全性內容 (IE ESC)。</span><span class="sxs-lookup"><span data-stu-id="89152-205">Make sure that Internet Explorer Enhanced Security Context (IE ESC) is disabled.</span></span> <span data-ttu-id="89152-206">請遵循下列步驟來停用 IE ESC：</span><span class="sxs-lookup"><span data-stu-id="89152-206">Follow these steps to disable IE ESC:</span></span>
  
  1. <span data-ttu-id="89152-207">關閉 Internet Explorer 的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="89152-207">Close all instances of Internet Explorer.</span></span>
  2. <span data-ttu-id="89152-208">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="89152-208">Start the Server Manager.</span></span>
  3. <span data-ttu-id="89152-209">在左窗格中按一下 [本機伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="89152-209">In the left pane, click **Local Server**.</span></span>
  4. <span data-ttu-id="89152-210">在右窗格中，按一下 [IE 增強式安全性設定] 旁邊的 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="89152-210">On the right pane, next to **IE Enhanced Security Configuration**, click **On**.</span></span>
  5. <span data-ttu-id="89152-211">在 [系統管理員] 下，按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="89152-211">Under **Administrators**, click **Off**.</span></span>
  6. <span data-ttu-id="89152-212">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="89152-212">Click **OK**.</span></span>

## <a name="remote-blob-storage-rbs-prerequisites"></a><span data-ttu-id="89152-213">遠端 BLOB 儲存 (RBS) 必要條件</span><span class="sxs-lookup"><span data-stu-id="89152-213">Remote BLOB Storage (RBS) prerequisites</span></span>
<span data-ttu-id="89152-214">請確定您使用支援的 SQL Server 版本。</span><span class="sxs-lookup"><span data-stu-id="89152-214">Make sure that you are using a supported version of SQL Server.</span></span> <span data-ttu-id="89152-215">僅下列版本才支援和能夠使用 RBS：</span><span class="sxs-lookup"><span data-stu-id="89152-215">Only the following versions are supported and able to use RBS:</span></span>

* <span data-ttu-id="89152-216">SQL Server 2008 Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="89152-216">SQL Server 2008 Enterprise Edition</span></span>
* <span data-ttu-id="89152-217">SQL Server 2008 R2 Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="89152-217">SQL Server 2008 R2 Enterprise Edition</span></span>
* <span data-ttu-id="89152-218">SQL Server 2012 Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="89152-218">SQL Server 2012 Enterprise Edition</span></span>

<span data-ttu-id="89152-219">只有在 StorSimple 裝置向 SQL Server 呈現的磁碟區上，才能外部化 BLOB。</span><span class="sxs-lookup"><span data-stu-id="89152-219">BLOBs can be externalized on only those volumes that the StorSimple device presents to SQL Server.</span></span> <span data-ttu-id="89152-220">不支援在其他目標上進行 BLOB 外部化。</span><span class="sxs-lookup"><span data-stu-id="89152-220">No other targets for BLOB externalization are supported.</span></span>

<span data-ttu-id="89152-221">當您完成所有必要條件設定步驟後，請移至 [安裝 StorSimple Adapter for SharePoint](#install-the-storsimple-adapter-for-sharepoint)。</span><span class="sxs-lookup"><span data-stu-id="89152-221">When you have completed all prerequisite configuration steps, go to [Install the StorSimple Adapter for SharePoint](#install-the-storsimple-adapter-for-sharepoint).</span></span>

## <a name="install-the-storsimple-adapter-for-sharepoint"></a><span data-ttu-id="89152-222">安裝 StorSimple Adapter for SharePoint</span><span class="sxs-lookup"><span data-stu-id="89152-222">Install the StorSimple Adapter for SharePoint</span></span>
<span data-ttu-id="89152-223">使用下列步驟來安裝 StorSimple Adapter for SharePoint。</span><span class="sxs-lookup"><span data-stu-id="89152-223">Use the following steps to install the StorSimple Adapter for SharePoint.</span></span> <span data-ttu-id="89152-224">如果您要重新安裝軟體，請參閱 [升級或重新安裝 StorSimple Adapter for SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint)。</span><span class="sxs-lookup"><span data-stu-id="89152-224">If you are reinstalling the software, see [Upgrade or reinstall the StorSimple Adapter for SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint).</span></span> <span data-ttu-id="89152-225">安裝所需的時間取決於您的 SharePoint 伺服器陣列中的 SharePoint 資料庫總數。</span><span class="sxs-lookup"><span data-stu-id="89152-225">The time required for the installation depends on the total number of SharePoint databases in your SharePoint server farm.</span></span>

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a><span data-ttu-id="89152-226">設定 RBS</span><span class="sxs-lookup"><span data-stu-id="89152-226">Configure RBS</span></span>
<span data-ttu-id="89152-227">安裝 StorSimple Adapter for SharePoint 之後，請依下列程序設定 RBS。</span><span class="sxs-lookup"><span data-stu-id="89152-227">After you install the StorSimple Adapter for SharePoint, configure RBS as described in the following procedure.</span></span>

> [!TIP]
> <span data-ttu-id="89152-228">StorSimple Adapter for SharePoint 外掛到 SharePoint 管理中心入口網站頁面，可讓您在 SharePoint 伺服器陣列中的每個內容資料庫上啟用或停用 RBS。</span><span class="sxs-lookup"><span data-stu-id="89152-228">The StorSimple Adapter for SharePoint plugs into the SharePoint Central Administration page, allowing RBS to be enabled or disabled on each content database in the SharePoint farm.</span></span> <span data-ttu-id="89152-229">不過，在內容資料庫上啟用或停用 RBS 會導致 IIS 重設，而且根據您的伺服器陣列設定，可能會短暫地中斷 SharePoint Web 前端 (WFE) 的可用性。</span><span class="sxs-lookup"><span data-stu-id="89152-229">However, enabling or disabling RBS on the content database causes an IIS reset, which, depending on your farm configuration, can momentarily disrupt the availability of the SharePoint web front end (WFE).</span></span> <span data-ttu-id="89152-230">(有一些因素可以限制或避免此中斷狀況，例如使用前端負載平衡器、目前的伺服器工作負載等等)。為了避免使用者因為中斷而受影響，建議您只在規劃的維護期間啟用或停用 RBS。</span><span class="sxs-lookup"><span data-stu-id="89152-230">(Factors such as the use of a front-end load balancer, the current server workload, and so on, can limit or eliminate this disruption.) To protect users from a disruption, we recommend that you enable or disable RBS only during a planned maintenance window.</span></span>


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a><span data-ttu-id="89152-231">設定記憶體回收</span><span class="sxs-lookup"><span data-stu-id="89152-231">Configure garbage collection</span></span>
<span data-ttu-id="89152-232">從 SharePoint 網站刪除物件時，不會自動從 RBS 存放磁碟區刪除這些物件。</span><span class="sxs-lookup"><span data-stu-id="89152-232">When objects are deleted from a SharePoint site, they are not automatically deleted from the RBS store volume.</span></span> <span data-ttu-id="89152-233">而是由一個非同步的背景維護程式，從檔案存放區刪除被遺棄的 BLOB。</span><span class="sxs-lookup"><span data-stu-id="89152-233">Instead, an asynchronous, background maintenance program deletes orphaned BLOBs from the file store.</span></span> <span data-ttu-id="89152-234">系統管理員可以排程定期執行此程序，或需要時才啟動此程序。</span><span class="sxs-lookup"><span data-stu-id="89152-234">System administrators can schedule this process to run periodically or they can start it whenever necessary.</span></span>

<span data-ttu-id="89152-235">當您啟用 RBS 時，此維護程式 (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) 會自動安裝在所有 SharePoint WFE 伺服器和應用程式伺服器上。</span><span class="sxs-lookup"><span data-stu-id="89152-235">This maintenance program (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) is automatically installed on all SharePoint WFE servers and application servers when you enable RBS.</span></span> <span data-ttu-id="89152-236">此程式安裝在以下位置：*開機磁碟機*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\\</span><span class="sxs-lookup"><span data-stu-id="89152-236">The program is installed in the following location: *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\\</span></span>

<span data-ttu-id="89152-237">如需設定和使用維護程式的相關資訊，請參閱[在 SharePoint Server 2013 中維護 RBS][8]。</span><span class="sxs-lookup"><span data-stu-id="89152-237">For information about configuring and using the maintenance program, see [Maintain RBS in SharePoint Server 2013][8].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89152-238">RBS 維護程式會消耗大量資源。</span><span class="sxs-lookup"><span data-stu-id="89152-238">The RBS maintainer program is resource intensive.</span></span> <span data-ttu-id="89152-239">您應該將它排程在 SharePoint 伺服器陣列的活動量較少期間執行。</span><span class="sxs-lookup"><span data-stu-id="89152-239">You should schedule it to run only during periods of light activity on the SharePoint farm.</span></span>


### <a name="delete-orphaned-blobs-immediately"></a><span data-ttu-id="89152-240">立即刪除被遺棄的 BLOB</span><span class="sxs-lookup"><span data-stu-id="89152-240">Delete orphaned BLOBs immediately</span></span>
<span data-ttu-id="89152-241">如果您需要立即刪除被遺棄的 BLOB，您可以使用下列指示。</span><span class="sxs-lookup"><span data-stu-id="89152-241">If you need to delete orphaned BLOBs immediately, you can use the following instructions.</span></span> <span data-ttu-id="89152-242">請注意，這些指示是如何在具有下列元件的 SharePoint 2013 環境中完成此作業的範例：</span><span class="sxs-lookup"><span data-stu-id="89152-242">Note that these instructions are an example of how this can be done in a SharePoint 2013 environment with the following components:</span></span>

* <span data-ttu-id="89152-243">內容資料庫名稱是 WSS_Content。</span><span class="sxs-lookup"><span data-stu-id="89152-243">The content database name is WSS_Content.</span></span>
* <span data-ttu-id="89152-244">SQL Server 名稱是 SHRPT13-SQL12\SHRPT13。</span><span class="sxs-lookup"><span data-stu-id="89152-244">The SQL Server name is SHRPT13-SQL12\SHRPT13.</span></span>
* <span data-ttu-id="89152-245">Web 應用程式名稱是 SharePoint–80。</span><span class="sxs-lookup"><span data-stu-id="89152-245">The web application name is SharePoint – 80.</span></span>

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint"></a><span data-ttu-id="89152-246">升級或重新安裝 StorSimple Adapter for SharePoint</span><span class="sxs-lookup"><span data-stu-id="89152-246">Upgrade or reinstall the StorSimple Adapter for SharePoint</span></span>
<span data-ttu-id="89152-247">使用下列程序升級 SharePoint 伺服器，再重新安裝 StorSimple Adapter for SharePoint，或只是在現有的 SharePoint 伺服器陣列中升級或重新安裝配接器。</span><span class="sxs-lookup"><span data-stu-id="89152-247">Use the following procedure to upgrade SharePoint server and then reinstall StorSimple Adapter for SharePoint or to simply upgrade or reinstall the adapter in an existing SharePoint server farm.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89152-248">在嘗試升級 SharePoint 軟體和 (或) 升級或重新安裝 StorSimple Adapter for SharePoint 之前，請檢閱下列資訊：</span><span class="sxs-lookup"><span data-stu-id="89152-248">Review the following information before you attempt to upgrade your SharePoint software and/or upgrade or reinstall the StorSimple Adapter for SharePoint:</span></span>
> 
> * <span data-ttu-id="89152-249">先前透過 RBS 移到外部儲存體的任何檔案，必須等到重新安裝完成並重新啟用 RBS 功能之後才能使用。</span><span class="sxs-lookup"><span data-stu-id="89152-249">Any files that were previously moved to external storage via RBS will not be available until the reinstallation is finished and the RBS feature is enabled again.</span></span> <span data-ttu-id="89152-250">為了限制使用者受影響的程度，請在規劃的維護期間執行任何升級或重新安裝。</span><span class="sxs-lookup"><span data-stu-id="89152-250">To limit user impact, perform any upgrade or reinstallation during a planned maintenance window.</span></span>
> * <span data-ttu-id="89152-251">根據 SharePoint 伺服器陣列中的 SharePoint 資料庫總數而定，升級/重新安裝所需的時間可能不同。</span><span class="sxs-lookup"><span data-stu-id="89152-251">The time required for the upgrade/reinstallation can vary, depending on the total number of SharePoint databases in the SharePoint server farm.</span></span>
> * <span data-ttu-id="89152-252">升級/重新安裝完成之後，您需要針對內容資料庫啟用 RBS。</span><span class="sxs-lookup"><span data-stu-id="89152-252">After the upgrade/reinstallation is complete, you need to enable RBS for the content databases.</span></span> <span data-ttu-id="89152-253">如需詳細資訊，請參閱 [設定 RBS](#configure-rbs) 。</span><span class="sxs-lookup"><span data-stu-id="89152-253">See [Configure RBS](#configure-rbs) for more information.</span></span>
> * <span data-ttu-id="89152-254">如果要設定 RBS 的 SharePoint 伺服器陣列有非常大量的資料庫 (超過 200 個)，則 [SharePoint 管理中心]  頁面可能會逾時。</span><span class="sxs-lookup"><span data-stu-id="89152-254">If you are configuring RBS for a SharePoint farm that has a very large number of databases (greater than 200), the **SharePoint Central Administration** page might time out.</span></span> <span data-ttu-id="89152-255">如果發生這種情況，請重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="89152-255">If that occurs, refresh the page.</span></span> <span data-ttu-id="89152-256">這不會影響設定程序。</span><span class="sxs-lookup"><span data-stu-id="89152-256">This does not affect the configuration process.</span></span>


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a><span data-ttu-id="89152-257">移除 StorSimple Adapter for SharePoint</span><span class="sxs-lookup"><span data-stu-id="89152-257">StorSimple Adapter for SharePoint removal</span></span>
<span data-ttu-id="89152-258">下列程序描述如何先將 Blob 移回 SQL Server 內容資料庫，然後再解除安裝 StorSimple Adapter for SharePoint。</span><span class="sxs-lookup"><span data-stu-id="89152-258">The following procedures describe how to move the BLOBs back to the SQL Server content databases and then uninstall the StorSimple Adapter for SharePoint.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="89152-259">您必須先將 Blob 移回內容資料庫，才能解除安裝配接器軟體。</span><span class="sxs-lookup"><span data-stu-id="89152-259">You have to move the BLOBs back to the content databases before you uninstall the adapter software.</span></span>


### <a name="before-you-begin"></a><span data-ttu-id="89152-260">開始之前</span><span class="sxs-lookup"><span data-stu-id="89152-260">Before you begin</span></span>
<span data-ttu-id="89152-261">在將資料移回 SQL Server 內容資料庫並開始配接器移除程序之前，請先收集下列資訊：</span><span class="sxs-lookup"><span data-stu-id="89152-261">Collect the following information before you move the data back to the SQL Server content databases and begin the adapter removal process:</span></span>

* <span data-ttu-id="89152-262">已啟用 RBS 之所有資料庫的名稱</span><span class="sxs-lookup"><span data-stu-id="89152-262">The names of all the databases for which RBS is enabled</span></span>
* <span data-ttu-id="89152-263">已設定的 Blob 存放區 UNC 路徑</span><span class="sxs-lookup"><span data-stu-id="89152-263">The UNC path of the configured BLOB store</span></span>

### <a name="move-the-blobs-back-to-the-content-databases"></a><span data-ttu-id="89152-264">將 Blob 移回內容資料庫</span><span class="sxs-lookup"><span data-stu-id="89152-264">Move the BLOBs back to the content databases</span></span>
<span data-ttu-id="89152-265">在解除安裝 StorSimple Adapter for SharePoint 軟體之前，必須將所有已外部化的 Blob 移轉回 SQL Server 內容資料庫中。</span><span class="sxs-lookup"><span data-stu-id="89152-265">Before you uninstall the StorSimple Adapter for SharePoint software, you must migrate all of the BLOBs that were externalized back to the SQL Server content databases.</span></span> <span data-ttu-id="89152-266">如果您在將所有 Blob 移回內容資料庫之前就先嘗試解除安裝 StorSimple Adapter for SharePoint，則會看到下列警告訊息。</span><span class="sxs-lookup"><span data-stu-id="89152-266">If you attempt to uninstall the StorSimple Adapter for SharePoint before you move all the BLOBs back to the content databases, you will see the following warning message.</span></span>

![警告訊息](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="to-move-the-blobs-back-to-the-content-databases"></a><span data-ttu-id="89152-268">將 Blob 移回內容資料庫</span><span class="sxs-lookup"><span data-stu-id="89152-268">To move the BLOBs back to the content databases</span></span>
1. <span data-ttu-id="89152-269">下載每個已外部化的物件。</span><span class="sxs-lookup"><span data-stu-id="89152-269">Download each of the externalized objects.</span></span>
2. <span data-ttu-id="89152-270">開啟 [SharePoint 管理中心] 頁面，並瀏覽至 [系統設定]。</span><span class="sxs-lookup"><span data-stu-id="89152-270">Open the **SharePoint Central Administration** page, and browse to **System Settings**.</span></span>
3. <span data-ttu-id="89152-271">在 [Azure StorSimple] 下方，按一下 [設定 StorSimple Adapter]。</span><span class="sxs-lookup"><span data-stu-id="89152-271">Under **Azure StorSimple**, click **Configure StorSimple Adapter**.</span></span>
4. <span data-ttu-id="89152-272">在 [設定 StorSimple Adapter] 頁面上，針對您想要從外部 Blob 儲存體移除的每個內容資料庫下方，按一下 [停用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="89152-272">On the **Configure StorSimple Adapter** page, click the **Disable** button below each of the content databases that you want to remove from external BLOB storage.</span></span> 
5. <span data-ttu-id="89152-273">從 SharePoint 中刪除物件，然後重新上傳。</span><span class="sxs-lookup"><span data-stu-id="89152-273">Delete the objects from SharePoint, and then upload them again.</span></span>

<span data-ttu-id="89152-274">或者，您可以使用 SharePoint 隨附的 Microsoft` RBS Migrate()` PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="89152-274">Alternatively, you can use the Microsoft` RBS Migrate()` PowerShell cmdlet included with SharePoint.</span></span> <span data-ttu-id="89152-275">如需詳細資訊，請參閱 [將內容移入或移出 RBS](https://technet.microsoft.com/library/ff628255.aspx)。</span><span class="sxs-lookup"><span data-stu-id="89152-275">For more information, see [Migrate content into or out of RBS](https://technet.microsoft.com/library/ff628255.aspx).</span></span>

<span data-ttu-id="89152-276">將 Blob 移回內容資料庫之後，請移至下一個步驟： [解除安裝配接器](#uninstall-the-adapter)。</span><span class="sxs-lookup"><span data-stu-id="89152-276">After you move the BLOBs back to the content database, go to the next step: [Uninstall the adapter](#uninstall-the-adapter).</span></span>

### <a name="uninstall-the-adapter"></a><span data-ttu-id="89152-277">解除安裝配接器</span><span class="sxs-lookup"><span data-stu-id="89152-277">Uninstall the adapter</span></span>
<span data-ttu-id="89152-278">將 Blob 移回 SQL Server 內容資料庫之後，請使用下列其中一個選項，解除安裝 StorSimple Adapter for SharePoint。</span><span class="sxs-lookup"><span data-stu-id="89152-278">After you move the BLOBs back to the SQL Server content databases, use one of the following options to uninstall the StorSimple Adapter for SharePoint.</span></span>

#### <a name="to-use-the-installation-program-to-uninstall-the-adapter"></a><span data-ttu-id="89152-279">使用安裝程式來解除安裝配接器</span><span class="sxs-lookup"><span data-stu-id="89152-279">To use the installation program to uninstall the adapter</span></span>
1. <span data-ttu-id="89152-280">使用具有系統管理員權限的帳戶登入 Web 前端 (WFE) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="89152-280">Use an account with administrator privileges to log on to the web front-end (WFE) server.</span></span>
2. <span data-ttu-id="89152-281">按兩下 StorSimple Adapter for SharePoint。</span><span class="sxs-lookup"><span data-stu-id="89152-281">Double-click the StorSimple Adapter for SharePoint installer.</span></span> <span data-ttu-id="89152-282">安裝精靈隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="89152-282">The Setup Wizard starts.</span></span>
   
    ![安裝精靈](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. <span data-ttu-id="89152-284">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="89152-284">Click **Next**.</span></span> <span data-ttu-id="89152-285">下列頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="89152-285">The following page appears.</span></span>
   
    ![安裝精靈移除頁面](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. <span data-ttu-id="89152-287">按一下 [移除]  以選取移除程序。</span><span class="sxs-lookup"><span data-stu-id="89152-287">Click **Remove** to select the removal process.</span></span> <span data-ttu-id="89152-288">下列頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="89152-288">The following page appears.</span></span>
   
    ![安裝精靈確認頁面](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. <span data-ttu-id="89152-290">按一下 [移除]  確認移除。</span><span class="sxs-lookup"><span data-stu-id="89152-290">Click **Remove** to confirm the removal.</span></span> <span data-ttu-id="89152-291">下列進度頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="89152-291">The following progress page appears.</span></span>
   
    ![安裝精靈進度頁面](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. <span data-ttu-id="89152-293">移除完成後，會出現完成頁面。</span><span class="sxs-lookup"><span data-stu-id="89152-293">When the removal is complete, the finish page appears.</span></span> <span data-ttu-id="89152-294">按一下 [完成] 以關閉安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="89152-294">Click **Finish** to close the Setup Wizard.</span></span>

#### <a name="to-use-the-control-panel-to-uninstall-the-adapter"></a><span data-ttu-id="89152-295">使用控制台來解除安裝配接器</span><span class="sxs-lookup"><span data-stu-id="89152-295">To use the Control Panel to uninstall the adapter</span></span>
1. <span data-ttu-id="89152-296">開啟 [控制台]，然後按一下 [程式和功能] 。</span><span class="sxs-lookup"><span data-stu-id="89152-296">Open the Control Panel, and then click **Programs and Features**.</span></span>
2. <span data-ttu-id="89152-297">選取 **StorSimple Adapter for SharePoint**，然後按一下 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="89152-297">Select **StorSimple Adapter for SharePoint**, and then click **Uninstall**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89152-298">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89152-298">Next steps</span></span>
<span data-ttu-id="89152-299">[深入了解 StorSimple](storsimple-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="89152-299">[Learn more about StorSimple](storsimple-overview.md).</span></span>

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
