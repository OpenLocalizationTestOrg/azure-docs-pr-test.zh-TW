---
title: "將您現有的 Azure 資料倉儲移轉到進階儲存體 | Microsoft Docs"
description: "將現有資料倉儲移轉到進階儲存體的指示"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 860e50b532b4b0a21d3be54f087730070b0e56bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-data-warehouse-to-premium-storage"></a><span data-ttu-id="c3fb9-103">將您的資料倉儲移轉到進階儲存體</span><span class="sxs-lookup"><span data-stu-id="c3fb9-103">Migrate your data warehouse to premium storage</span></span>
<span data-ttu-id="c3fb9-104">Azure SQL 資料倉儲最新引進了[進階儲存體，以獲得更高的效能可預測性][premium storage for greater performance predictability]。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="c3fb9-105">現在可以將目前在標準儲存體上的現有資料倉儲移轉至進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-105">Existing data warehouses currently on standard storage can now be migrated to premium storage.</span></span> <span data-ttu-id="c3fb9-106">您可以利用自動移轉，或如果您想要控制何時要移轉 (未包含某些停機時間)，您可以自行完成移轉。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-106">You can take advantage of automatic migration, or if you prefer to control when to migrate (which does involve some downtime), you can do the migration yourself.</span></span>

<span data-ttu-id="c3fb9-107">如果您有一個以上的資料倉儲，請使用[自動移轉排程][automatic migration schedule]來判斷它也會移轉的時間。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-107">If you have more than one data warehouse, use the [automatic migration schedule][automatic migration schedule] to determine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="c3fb9-108">決定儲存體類型</span><span class="sxs-lookup"><span data-stu-id="c3fb9-108">Determine storage type</span></span>
<span data-ttu-id="c3fb9-109">如果您在下列日期前建立資料倉儲，則您目前是使用標準儲存體。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-109">If you created a data warehouse before the following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="c3fb9-110">**區域**</span><span class="sxs-lookup"><span data-stu-id="c3fb9-110">**Region**</span></span> | <span data-ttu-id="c3fb9-111">**在此日期前建立的資料倉儲**</span><span class="sxs-lookup"><span data-stu-id="c3fb9-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="c3fb9-112">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-112">Australia East</span></span> |<span data-ttu-id="c3fb9-113">尚未提供進階儲存體</span><span class="sxs-lookup"><span data-stu-id="c3fb9-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="c3fb9-114">中國東部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-114">China East</span></span> |<span data-ttu-id="c3fb9-115">2016 年 11 月 1 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-115">November 1, 2016</span></span> |
| <span data-ttu-id="c3fb9-116">中國北部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-116">China North</span></span> |<span data-ttu-id="c3fb9-117">2016 年 11 月 1 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-117">November 1, 2016</span></span> |
| <span data-ttu-id="c3fb9-118">德國中部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-118">Germany Central</span></span> |<span data-ttu-id="c3fb9-119">2016 年 11 月 1 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-119">November 1, 2016</span></span> |
| <span data-ttu-id="c3fb9-120">德國東北部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-120">Germany Northeast</span></span> |<span data-ttu-id="c3fb9-121">2016 年 11 月 1 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-121">November 1, 2016</span></span> |
| <span data-ttu-id="c3fb9-122">印度西部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-122">India West</span></span> |<span data-ttu-id="c3fb9-123">尚未提供進階儲存體</span><span class="sxs-lookup"><span data-stu-id="c3fb9-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="c3fb9-124">日本西部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-124">Japan West</span></span> |<span data-ttu-id="c3fb9-125">尚未提供進階儲存體</span><span class="sxs-lookup"><span data-stu-id="c3fb9-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="c3fb9-126">美國中北部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-126">North Central US</span></span> |<span data-ttu-id="c3fb9-127">2016 年 11 月 10 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="c3fb9-128">自動移轉詳細資料</span><span class="sxs-lookup"><span data-stu-id="c3fb9-128">Automatic migration details</span></span>
<span data-ttu-id="c3fb9-129">根據預設，在[自動移轉排程][automatic migration schedule]期間，我們會在下午 6:00 與上午 6:00 之間 (您所在地區的當地時間) 為您移轉資料庫。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during the [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="c3fb9-130">在移轉期間，現有的資料倉儲將無法使用。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-130">Your existing data warehouse will be unusable during the migration.</span></span> <span data-ttu-id="c3fb9-131">每個資料倉儲每 TB 的儲存體需要大約一小時的時間進行移轉。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-131">The migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="c3fb9-132">在自動移轉的任何部分中，您不需支付任何費用。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-132">You will not be charged during any portion of the automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="c3fb9-133">移轉完成後，您的資料倉儲就會重新上線並可使用。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-133">When the migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="c3fb9-134">Microsoft 會採取下列步驟來完成移轉 (這些不需要您採取任何介入)。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-134">Microsoft is taking the following steps to complete the migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="c3fb9-135">在此範例中，假設您在標準儲存體上的現有資料倉儲目前名為 “MyDW”。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="c3fb9-136">Microsoft 會將 “MyDW” 重新命名為 “MyDW_DO_NOT_USE_[時間戳記]”。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-136">Microsoft renames “MyDW” to “MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="c3fb9-137">Microsoft 會暫停 “MyDW_DO_NOT_USE_[時間戳記]”。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="c3fb9-138">系統會在此期間執行備份。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-138">During this time, a backup is taken.</span></span> <span data-ttu-id="c3fb9-139">如果在過程中發生任何問題，您可能會看到多個暫停及繼續。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="c3fb9-140">Microsoft 會從步驟 2 中建立的備份，在進階儲存體上建立名為 “MyDW” 的新資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from the backup taken in step 2.</span></span> <span data-ttu-id="c3fb9-141">直到還原完成後，“MyDW” 才會出現。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-141">“MyDW” will not appear until after the restore is complete.</span></span>
4. <span data-ttu-id="c3fb9-142">還原完成後，“MyDW” 會回到相同的資料倉儲單位，以及移轉之前的狀態 (暫停或作用中)。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-142">After the restore is complete, “MyDW” returns to the same data warehouse units and state (paused or active) that it was before the migration.</span></span>
5. <span data-ttu-id="c3fb9-143">移轉完成後，Microsoft 會刪除 “MyDW_DO_NOT_USE_[時間戳記]”。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-143">After the migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="c3fb9-144">下列設定不會在移轉過程中沿用：</span><span class="sxs-lookup"><span data-stu-id="c3fb9-144">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="c3fb9-145">在資料庫層級稽核必須重新啟用。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-145">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="c3fb9-146">在資料庫層級的防火牆規則必須是已顯示。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-146">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="c3fb9-147">在伺服器層級的防火牆規則不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-147">Firewall rules at the server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="c3fb9-148">自動移轉排程</span><span class="sxs-lookup"><span data-stu-id="c3fb9-148">Automatic migration schedule</span></span>
<span data-ttu-id="c3fb9-149">自動移轉會在下列中斷排程期間發生，時間是從下午 6:00 至上午 6:00 (每個地區的當地時間)。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during the following outage schedule.</span></span>

| <span data-ttu-id="c3fb9-150">**區域**</span><span class="sxs-lookup"><span data-stu-id="c3fb9-150">**Region**</span></span> | <span data-ttu-id="c3fb9-151">**預估開始日期**</span><span class="sxs-lookup"><span data-stu-id="c3fb9-151">**Estimated start date**</span></span> | <span data-ttu-id="c3fb9-152">**預估結束日期**</span><span class="sxs-lookup"><span data-stu-id="c3fb9-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c3fb9-153">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-153">Australia East</span></span> |<span data-ttu-id="c3fb9-154">尚未決定</span><span class="sxs-lookup"><span data-stu-id="c3fb9-154">Not determined yet</span></span> |<span data-ttu-id="c3fb9-155">尚未決定</span><span class="sxs-lookup"><span data-stu-id="c3fb9-155">Not determined yet</span></span> |
| <span data-ttu-id="c3fb9-156">中國東部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-156">China East</span></span> |<span data-ttu-id="c3fb9-157">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-157">January 9, 2017</span></span> |<span data-ttu-id="c3fb9-158">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-158">January 13, 2017</span></span> |
| <span data-ttu-id="c3fb9-159">中國北部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-159">China North</span></span> |<span data-ttu-id="c3fb9-160">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-160">January 9, 2017</span></span> |<span data-ttu-id="c3fb9-161">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-161">January 13, 2017</span></span> |
| <span data-ttu-id="c3fb9-162">德國中部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-162">Germany Central</span></span> |<span data-ttu-id="c3fb9-163">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-163">January 9, 2017</span></span> |<span data-ttu-id="c3fb9-164">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-164">January 13, 2017</span></span> |
| <span data-ttu-id="c3fb9-165">德國東北部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-165">Germany Northeast</span></span> |<span data-ttu-id="c3fb9-166">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-166">January 9, 2017</span></span> |<span data-ttu-id="c3fb9-167">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-167">January 13, 2017</span></span> |
| <span data-ttu-id="c3fb9-168">印度西部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-168">India West</span></span> |<span data-ttu-id="c3fb9-169">尚未決定</span><span class="sxs-lookup"><span data-stu-id="c3fb9-169">Not determined yet</span></span> |<span data-ttu-id="c3fb9-170">尚未決定</span><span class="sxs-lookup"><span data-stu-id="c3fb9-170">Not determined yet</span></span> |
| <span data-ttu-id="c3fb9-171">日本西部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-171">Japan West</span></span> |<span data-ttu-id="c3fb9-172">尚未決定</span><span class="sxs-lookup"><span data-stu-id="c3fb9-172">Not determined yet</span></span> |<span data-ttu-id="c3fb9-173">尚未決定</span><span class="sxs-lookup"><span data-stu-id="c3fb9-173">Not determined yet</span></span> |
| <span data-ttu-id="c3fb9-174">美國中北部</span><span class="sxs-lookup"><span data-stu-id="c3fb9-174">North Central US</span></span> |<span data-ttu-id="c3fb9-175">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-175">January 9, 2017</span></span> |<span data-ttu-id="c3fb9-176">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="c3fb9-176">January 13, 2017</span></span> |

## <a name="self-migration-to-premium-storage"></a><span data-ttu-id="c3fb9-177">自行移轉至進階儲存體</span><span class="sxs-lookup"><span data-stu-id="c3fb9-177">Self-migration to premium storage</span></span>
<span data-ttu-id="c3fb9-178">如果您要控制發生停機的時間，您可以使用下列步驟，將標準儲存體上的現有資料倉儲移轉至進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-178">If you want to control when your downtime will occur, you can use the following steps to migrate an existing data warehouse on standard storage to premium storage.</span></span> <span data-ttu-id="c3fb9-179">如果您選擇此選項，必須在自動移轉於該區域中開始之前完成自我移轉。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-179">If you choose this option, you must complete the self-migration before the automatic migration begins in that region.</span></span> <span data-ttu-id="c3fb9-180">這可確保您避免任何自動移轉造成衝突的風險 (請參閱[自動移轉排程][automatic migration schedule])。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-180">This ensures that you avoid any risk of the automatic migration causing a conflict (refer to the [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="c3fb9-181">自行移轉指示</span><span class="sxs-lookup"><span data-stu-id="c3fb9-181">Self-migration instructions</span></span>
<span data-ttu-id="c3fb9-182">若要自行移轉您的資料倉儲，請使用備份和還原功能。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-182">To migrate your data warehouse yourself, use the backup and restore features.</span></span> <span data-ttu-id="c3fb9-183">每個資料倉儲每 TB 的儲存體預計需要約一小時的時間來進行移轉作業的還原部分。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-183">The restore portion of the migration is expected to take around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="c3fb9-184">如果您要在移轉完成後保留相同的名稱，請遵循[在移轉期間內重新命名的步驟][steps to rename during migration]。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-184">If you want to keep the same name after migration is complete, follow the [steps to rename during migration][steps to rename during migration].</span></span>

1. <span data-ttu-id="c3fb9-185">[暫停][Pause] 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="c3fb9-186">這會進行自動備份。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="c3fb9-187">從最新的快照集[還原][Restore]。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="c3fb9-188">刪除標準儲存體上的現有資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="c3fb9-189">**如果您無法執行此步驟，您需支付這兩個資料倉儲的費用。**</span><span class="sxs-lookup"><span data-stu-id="c3fb9-189">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="c3fb9-190">下列設定不會在移轉過程中沿用：</span><span class="sxs-lookup"><span data-stu-id="c3fb9-190">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="c3fb9-191">在資料庫層級稽核必須重新啟用。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-191">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="c3fb9-192">在資料庫層級的防火牆規則必須是已顯示。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-192">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="c3fb9-193">在伺服器層級的防火牆規則不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-193">Firewall rules at the server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="c3fb9-194">(選擇性) 在移轉期間重新命名資料倉儲</span><span class="sxs-lookup"><span data-stu-id="c3fb9-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="c3fb9-195">相同邏輯伺服器上的兩個資料庫不能具有相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-195">Two databases on the same logical server cannot have the same name.</span></span> <span data-ttu-id="c3fb9-196">SQL 資料倉儲現在支援重新命名資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-196">SQL Data Warehouse now supports the ability to rename a data warehouse.</span></span>

<span data-ttu-id="c3fb9-197">在此範例中，假設您在標準儲存體上的現有資料倉儲目前名為 “MyDW”。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="c3fb9-198">使用下列 ALTER DATABASE 命令重新命名 "MyDW"。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-198">Rename "MyDW" by using the following ALTER DATABASE command.</span></span> <span data-ttu-id="c3fb9-199">(在此範例中，我們會將它重新命名為 "MyDW_BeforeMigration") 此命令會停止所有現有的交易，且必須在主要資料庫中完成才能成功。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in the master database to succeed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="c3fb9-200">[暫停][Pause] "MyDW_BeforeMigration"。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="c3fb9-201">這會進行自動備份。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="c3fb9-202">從您最近使用的快照集搭配過去的名稱 (例如，"MyDW") 來[還原][Restore]新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-202">[Restore][Restore] from your most recent snapshot a new database with the name it used to be (for example, "MyDW").</span></span>
4. <span data-ttu-id="c3fb9-203">刪除 "MyDW_BeforeMigration"。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="c3fb9-204">**如果您無法執行此步驟，您需支付這兩個資料倉儲的費用。**</span><span class="sxs-lookup"><span data-stu-id="c3fb9-204">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="c3fb9-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3fb9-205">Next steps</span></span>
<span data-ttu-id="c3fb9-206">除了變更為進階儲存體，您也會增加資料倉儲基礎架構中的資料庫 blob 檔案數目。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-206">With the change to premium storage, you also have an increased number of database blob files in the underlying architecture of your data warehouse.</span></span> <span data-ttu-id="c3fb9-207">為獲得此變更的最佳效益，請使用下列指令碼來重建叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-207">To maximize the performance benefits of this change, rebuild your clustered columnstore indexes by using the following script.</span></span> <span data-ttu-id="c3fb9-208">此指令碼是藉由強制將某些現有資料移至其他 Blob 來運作。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-208">The script works by forcing some of your existing data to the additional blobs.</span></span> <span data-ttu-id="c3fb9-209">如果您不採取任何動作，隨著您將更多的資料載入資料表中，資料會在一段時間後自然重新分配。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-209">If you take no action, the data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="c3fb9-210">**必要條件：**</span><span class="sxs-lookup"><span data-stu-id="c3fb9-210">**Prerequisites:**</span></span>

- <span data-ttu-id="c3fb9-211">資料倉儲應以 1,000 個資料倉儲單位或更多數量來執行 (請參閱[調整計算能力][scale compute power])。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-211">The data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="c3fb9-212">執行指令碼的使用者應具有 [mediumrc 角色][mediumrc role]或更高權限。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-212">The user executing the script should be in the [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="c3fb9-213">若要將使用者新增至此角色，請執行下列作業︰````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="c3fb9-213">To add a user to this role, execute the following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table to control index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, the below can be re-run to restart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="c3fb9-214">如果您遇到任何關於資料倉儲的問題，請[建立支援票證][create a support ticket]和參考「移轉至進階儲存體」做為可能的原因。</span><span class="sxs-lookup"><span data-stu-id="c3fb9-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration to premium storage” as the possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration to Premium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps to rename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
