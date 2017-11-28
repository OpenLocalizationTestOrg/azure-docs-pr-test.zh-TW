---
title: "監視 XTP 記憶體內儲存體 | Microsoft Docs"
description: "估計和監視 XTP 記憶體內儲存體使用量、容量；解決容量錯誤 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: 5afb2209f18b1ba2aa0a916a439509b01afd80da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="bffd1-103">監視記憶體內部 OLTP 儲存體</span><span class="sxs-lookup"><span data-stu-id="bffd1-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="bffd1-104">使用 [記憶體內部 OLTP](sql-database-in-memory.md)時，記憶體最佳化資料表中的資料和資料表變數位於記憶體內部 OLTP 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="bffd1-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="bffd1-105">每個進階服務層都有最大的記憶體內部 OLTP 儲存體大小，如 [SQL Database 服務層文章](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)所說明。</span><span class="sxs-lookup"><span data-stu-id="bffd1-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="bffd1-106">一旦超過此限制，插入和更新作業可能會開始出錯 (錯誤碼 41823)。</span><span class="sxs-lookup"><span data-stu-id="bffd1-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="bffd1-107">屆時您將需要刪除資料以回收記憶體，或升級您的資料庫的效能層。</span><span class="sxs-lookup"><span data-stu-id="bffd1-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a><span data-ttu-id="bffd1-108">判斷資料是否在記憶體內部儲存容量上限內</span><span class="sxs-lookup"><span data-stu-id="bffd1-108">Determine whether data will fit within the in-memory storage cap</span></span>
<span data-ttu-id="bffd1-109">判斷儲存上限：如需不同進階服務層的儲存上限相關資訊，請參閱 [SQL Database 服務層文章](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) 。</span><span class="sxs-lookup"><span data-stu-id="bffd1-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span></span>

<span data-ttu-id="bffd1-110">估計記憶體最佳化資料表的記憶體需求，其方式如同在 Azure SQL Database 中估計 SQL Server 的記憶體需求。</span><span class="sxs-lookup"><span data-stu-id="bffd1-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="bffd1-111">花幾分鐘的時間來檢閱 [MSDN](https://msdn.microsoft.com/library/dn282389.aspx)上的該主題。</span><span class="sxs-lookup"><span data-stu-id="bffd1-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="bffd1-112">請注意，資料表和資料表變數資料列以及索引都會計入最大的使用者資料大小。</span><span class="sxs-lookup"><span data-stu-id="bffd1-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span></span> <span data-ttu-id="bffd1-113">此外，ALTER TABLE 需要足夠的空間來建立新版的完整資料表及其索引。</span><span class="sxs-lookup"><span data-stu-id="bffd1-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="bffd1-114">監視和警示</span><span class="sxs-lookup"><span data-stu-id="bffd1-114">Monitoring and alerting</span></span>
<span data-ttu-id="bffd1-115">您可以在 [Azure 入口網站](https://portal.azure.com/)中，透過[效能層的儲存上限](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)的百分比來監視記憶體內部儲存體使用情形：</span><span class="sxs-lookup"><span data-stu-id="bffd1-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="bffd1-116">在 [資料庫] 刀鋒視窗上，找出 [資源使用率方塊] 並按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="bffd1-116">On the Database blade, locate the Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="bffd1-117">然後選取計量 `In-Memory OLTP Storage percentage`。</span><span class="sxs-lookup"><span data-stu-id="bffd1-117">Then select the metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="bffd1-118">若要新增警示，請按一下 [資源使用率] 方塊以開啟 [計量] 刀鋒視窗，然後按一下 [新增警示]。</span><span class="sxs-lookup"><span data-stu-id="bffd1-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="bffd1-119">或使用下列查詢來顯示記憶體內部儲存體使用率：</span><span class="sxs-lookup"><span data-stu-id="bffd1-119">Or use the following query to show the in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="bffd1-120">更正記憶體不足情況 - 錯誤 41823</span><span class="sxs-lookup"><span data-stu-id="bffd1-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="bffd1-121">記憶體不足導致插入、更新和建立作業失敗，並出現錯誤訊息 41823。</span><span class="sxs-lookup"><span data-stu-id="bffd1-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="bffd1-122">錯誤訊息 41823 指出記憶體最佳化資料表和資料表變數已超過大小上限。</span><span class="sxs-lookup"><span data-stu-id="bffd1-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span></span>

<span data-ttu-id="bffd1-123">若要解決此錯誤，您可以：</span><span class="sxs-lookup"><span data-stu-id="bffd1-123">To resolve this error, either:</span></span>

* <span data-ttu-id="bffd1-124">從記憶體最佳化資料表中刪除資料，可能會將資料卸載至傳統、以磁碟為基礎的資料表；或者，</span><span class="sxs-lookup"><span data-stu-id="bffd1-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span></span>
* <span data-ttu-id="bffd1-125">將服務層升級至具有足夠記憶體內部記憶體的服務層，以便儲存您需要保留在記憶體最佳化資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="bffd1-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bffd1-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bffd1-126">Next steps</span></span>
<span data-ttu-id="bffd1-127">如需監視指引，請參閱[使用動態管理檢視監視 Azure SQL Database](sql-database-monitoring-with-dmvs.md)。</span><span class="sxs-lookup"><span data-stu-id="bffd1-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
