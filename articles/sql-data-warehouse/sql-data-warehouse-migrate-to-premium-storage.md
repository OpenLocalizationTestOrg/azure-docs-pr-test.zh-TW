---
title: "aaaMigrate 您現有的 Azure 資料倉儲 toopremium 儲存體 |Microsoft 文件"
description: "移轉現有的資料倉儲 toopremium 存放裝置的指示"
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
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="142d6-103">將資料倉儲 toopremium 存放裝置移轉</span><span class="sxs-lookup"><span data-stu-id="142d6-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="142d6-104">Azure SQL 資料倉儲最新引進了[進階儲存體，以獲得更高的效能可預測性][premium storage for greater performance predictability]。</span><span class="sxs-lookup"><span data-stu-id="142d6-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="142d6-105">現在可以在標準儲存體目前的倉儲的現有資料移轉 toopremium 儲存體。</span><span class="sxs-lookup"><span data-stu-id="142d6-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="142d6-106">您可以利用自動移轉，或如果您偏好 toocontrol 時 toomigrate （其中並未包含一些停機時間），您可以自行 hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="142d6-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="142d6-107">如果您有一個以上的資料倉儲時，使用 hello[自動移轉排程][ automatic migration schedule] toodetermine 時也將會移轉。</span><span class="sxs-lookup"><span data-stu-id="142d6-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="142d6-108">決定儲存體類型</span><span class="sxs-lookup"><span data-stu-id="142d6-108">Determine storage type</span></span>
<span data-ttu-id="142d6-109">如果您建立資料倉儲 hello 下列日期之前，您目前使用標準儲存體。</span><span class="sxs-lookup"><span data-stu-id="142d6-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="142d6-110">**區域**</span><span class="sxs-lookup"><span data-stu-id="142d6-110">**Region**</span></span> | <span data-ttu-id="142d6-111">**在此日期前建立的資料倉儲**</span><span class="sxs-lookup"><span data-stu-id="142d6-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="142d6-112">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="142d6-112">Australia East</span></span> |<span data-ttu-id="142d6-113">尚未提供進階儲存體</span><span class="sxs-lookup"><span data-stu-id="142d6-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="142d6-114">中國東部</span><span class="sxs-lookup"><span data-stu-id="142d6-114">China East</span></span> |<span data-ttu-id="142d6-115">2016 年 11 月 1 日</span><span class="sxs-lookup"><span data-stu-id="142d6-115">November 1, 2016</span></span> |
| <span data-ttu-id="142d6-116">中國北部</span><span class="sxs-lookup"><span data-stu-id="142d6-116">China North</span></span> |<span data-ttu-id="142d6-117">2016 年 11 月 1 日</span><span class="sxs-lookup"><span data-stu-id="142d6-117">November 1, 2016</span></span> |
| <span data-ttu-id="142d6-118">德國中部</span><span class="sxs-lookup"><span data-stu-id="142d6-118">Germany Central</span></span> |<span data-ttu-id="142d6-119">2016 年 11 月 1 日</span><span class="sxs-lookup"><span data-stu-id="142d6-119">November 1, 2016</span></span> |
| <span data-ttu-id="142d6-120">德國東北部</span><span class="sxs-lookup"><span data-stu-id="142d6-120">Germany Northeast</span></span> |<span data-ttu-id="142d6-121">2016 年 11 月 1 日</span><span class="sxs-lookup"><span data-stu-id="142d6-121">November 1, 2016</span></span> |
| <span data-ttu-id="142d6-122">印度西部</span><span class="sxs-lookup"><span data-stu-id="142d6-122">India West</span></span> |<span data-ttu-id="142d6-123">尚未提供進階儲存體</span><span class="sxs-lookup"><span data-stu-id="142d6-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="142d6-124">日本西部</span><span class="sxs-lookup"><span data-stu-id="142d6-124">Japan West</span></span> |<span data-ttu-id="142d6-125">尚未提供進階儲存體</span><span class="sxs-lookup"><span data-stu-id="142d6-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="142d6-126">美國中北部</span><span class="sxs-lookup"><span data-stu-id="142d6-126">North Central US</span></span> |<span data-ttu-id="142d6-127">2016 年 11 月 10 日</span><span class="sxs-lookup"><span data-stu-id="142d6-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="142d6-128">自動移轉詳細資料</span><span class="sxs-lookup"><span data-stu-id="142d6-128">Automatic migration details</span></span>
<span data-ttu-id="142d6-129">根據預設，我們將您的資料庫，下午 6:00 和上午 6:00 地區的當地時間之間期間移轉 hello[自動移轉排程][automatic migration schedule]。</span><span class="sxs-lookup"><span data-stu-id="142d6-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="142d6-130">Hello 移轉期間將無法使用現有的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="142d6-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="142d6-131">hello 移轉每個資料倉儲會每 tb 的儲存空間大約一小時。</span><span class="sxs-lookup"><span data-stu-id="142d6-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="142d6-132">您不收費 hello 自動移轉的任何部份。</span><span class="sxs-lookup"><span data-stu-id="142d6-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="142d6-133">Hello 移轉完成時，您的資料倉儲會回線上和可用性。</span><span class="sxs-lookup"><span data-stu-id="142d6-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="142d6-134">Microsoft 正在 hello 遷移步驟 toocomplete hello （這些不需要您採取任何介入）。</span><span class="sxs-lookup"><span data-stu-id="142d6-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="142d6-135">在此範例中，假設您在標準儲存體上的現有資料倉儲目前名為 “MyDW”。</span><span class="sxs-lookup"><span data-stu-id="142d6-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="142d6-136">Microsoft 會重新命名 「 MyDW 」 太"MyDW_DO_NOT_USE_ [時間戳記]"。</span><span class="sxs-lookup"><span data-stu-id="142d6-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="142d6-137">Microsoft 會暫停 “MyDW_DO_NOT_USE_[時間戳記]”。</span><span class="sxs-lookup"><span data-stu-id="142d6-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="142d6-138">系統會在此期間執行備份。</span><span class="sxs-lookup"><span data-stu-id="142d6-138">During this time, a backup is taken.</span></span> <span data-ttu-id="142d6-139">如果在過程中發生任何問題，您可能會看到多個暫停及繼續。</span><span class="sxs-lookup"><span data-stu-id="142d6-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="142d6-140">Microsoft 會建立名為"MyDW"高階儲存體的 hello 備份在步驟 2 中所採取的新資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="142d6-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="142d6-141">不會出現 「 MyDW"直到 hello 還原完成之後。</span><span class="sxs-lookup"><span data-stu-id="142d6-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="142d6-142">「 MyDW"hello 還原完成後，傳回的 toohello 相同的資料倉儲單位和狀態 （已暫停或使用中） 並將該 hello 移轉之前。</span><span class="sxs-lookup"><span data-stu-id="142d6-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="142d6-143">Hello 移轉完成之後，Microsoft 便會刪除 「 MyDW_DO_NOT_USE_ [時間戳記]"。</span><span class="sxs-lookup"><span data-stu-id="142d6-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="142d6-144">hello 下列設定不會延續 hello 移轉的一部分：</span><span class="sxs-lookup"><span data-stu-id="142d6-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="142d6-145">Hello 資料庫層級稽核需要 toobe 重新啟用。</span><span class="sxs-lookup"><span data-stu-id="142d6-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="142d6-146">Hello 資料庫層級防火牆規則需要 toobe 重新加入。</span><span class="sxs-lookup"><span data-stu-id="142d6-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="142d6-147">不會影響 hello 伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="142d6-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="142d6-148">自動移轉排程</span><span class="sxs-lookup"><span data-stu-id="142d6-148">Automatic migration schedule</span></span>
<span data-ttu-id="142d6-149">期間之後中斷排程 hello，下午 6:00 和上午 6:00 （每個區域的本機時間） 之間發生自動移轉。</span><span class="sxs-lookup"><span data-stu-id="142d6-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="142d6-150">**區域**</span><span class="sxs-lookup"><span data-stu-id="142d6-150">**Region**</span></span> | <span data-ttu-id="142d6-151">**預估開始日期**</span><span class="sxs-lookup"><span data-stu-id="142d6-151">**Estimated start date**</span></span> | <span data-ttu-id="142d6-152">**預估結束日期**</span><span class="sxs-lookup"><span data-stu-id="142d6-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="142d6-153">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="142d6-153">Australia East</span></span> |<span data-ttu-id="142d6-154">尚未決定</span><span class="sxs-lookup"><span data-stu-id="142d6-154">Not determined yet</span></span> |<span data-ttu-id="142d6-155">尚未決定</span><span class="sxs-lookup"><span data-stu-id="142d6-155">Not determined yet</span></span> |
| <span data-ttu-id="142d6-156">中國東部</span><span class="sxs-lookup"><span data-stu-id="142d6-156">China East</span></span> |<span data-ttu-id="142d6-157">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="142d6-157">January 9, 2017</span></span> |<span data-ttu-id="142d6-158">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="142d6-158">January 13, 2017</span></span> |
| <span data-ttu-id="142d6-159">中國北部</span><span class="sxs-lookup"><span data-stu-id="142d6-159">China North</span></span> |<span data-ttu-id="142d6-160">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="142d6-160">January 9, 2017</span></span> |<span data-ttu-id="142d6-161">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="142d6-161">January 13, 2017</span></span> |
| <span data-ttu-id="142d6-162">德國中部</span><span class="sxs-lookup"><span data-stu-id="142d6-162">Germany Central</span></span> |<span data-ttu-id="142d6-163">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="142d6-163">January 9, 2017</span></span> |<span data-ttu-id="142d6-164">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="142d6-164">January 13, 2017</span></span> |
| <span data-ttu-id="142d6-165">德國東北部</span><span class="sxs-lookup"><span data-stu-id="142d6-165">Germany Northeast</span></span> |<span data-ttu-id="142d6-166">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="142d6-166">January 9, 2017</span></span> |<span data-ttu-id="142d6-167">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="142d6-167">January 13, 2017</span></span> |
| <span data-ttu-id="142d6-168">印度西部</span><span class="sxs-lookup"><span data-stu-id="142d6-168">India West</span></span> |<span data-ttu-id="142d6-169">尚未決定</span><span class="sxs-lookup"><span data-stu-id="142d6-169">Not determined yet</span></span> |<span data-ttu-id="142d6-170">尚未決定</span><span class="sxs-lookup"><span data-stu-id="142d6-170">Not determined yet</span></span> |
| <span data-ttu-id="142d6-171">日本西部</span><span class="sxs-lookup"><span data-stu-id="142d6-171">Japan West</span></span> |<span data-ttu-id="142d6-172">尚未決定</span><span class="sxs-lookup"><span data-stu-id="142d6-172">Not determined yet</span></span> |<span data-ttu-id="142d6-173">尚未決定</span><span class="sxs-lookup"><span data-stu-id="142d6-173">Not determined yet</span></span> |
| <span data-ttu-id="142d6-174">美國中北部</span><span class="sxs-lookup"><span data-stu-id="142d6-174">North Central US</span></span> |<span data-ttu-id="142d6-175">2017 年 1 月 9 日</span><span class="sxs-lookup"><span data-stu-id="142d6-175">January 9, 2017</span></span> |<span data-ttu-id="142d6-176">2017 年 1 月 13 日</span><span class="sxs-lookup"><span data-stu-id="142d6-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="142d6-177">自我移轉 toopremium 儲存體</span><span class="sxs-lookup"><span data-stu-id="142d6-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="142d6-178">如果您想 toocontrol 將停機時間將會發生時，您可以使用下列步驟 toomigrate 現有的資料倉儲標準儲存體 toopremium 存放裝置上的 hello。</span><span class="sxs-lookup"><span data-stu-id="142d6-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="142d6-179">如果您選擇此選項時，您必須先完成 hello 自我移轉，才能開始在該區域中的 hello 自動移轉。</span><span class="sxs-lookup"><span data-stu-id="142d6-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="142d6-180">這可確保您避免 hello 自動移轉造成衝突的任何風險 (請參閱 toohello[自動移轉排程][automatic migration schedule])。</span><span class="sxs-lookup"><span data-stu-id="142d6-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="142d6-181">自行移轉指示</span><span class="sxs-lookup"><span data-stu-id="142d6-181">Self-migration instructions</span></span>
<span data-ttu-id="142d6-182">toomigrate 資料倉儲自行、 使用 hello 備份和還原功能。</span><span class="sxs-lookup"><span data-stu-id="142d6-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="142d6-183">hello 還原 hello 移轉部分是預期的 tootake 每 tb 的資料倉儲儲存空間大約一小時。</span><span class="sxs-lookup"><span data-stu-id="142d6-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="142d6-184">如果您想 tookeep hello 相同的名稱，在移轉完成之後，請遵循 hello[移轉期間的步驟 toorename][steps toorename during migration]。</span><span class="sxs-lookup"><span data-stu-id="142d6-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="142d6-185">[暫停][Pause] 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="142d6-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="142d6-186">這會進行自動備份。</span><span class="sxs-lookup"><span data-stu-id="142d6-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="142d6-187">從最新的快照集[還原][Restore]。</span><span class="sxs-lookup"><span data-stu-id="142d6-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="142d6-188">刪除標準儲存體上的現有資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="142d6-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="142d6-189">**如果您無法 toodo 此步驟中，您將支付這兩個資料倉儲。**</span><span class="sxs-lookup"><span data-stu-id="142d6-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="142d6-190">hello 下列設定不會延續 hello 移轉的一部分：</span><span class="sxs-lookup"><span data-stu-id="142d6-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="142d6-191">Hello 資料庫層級稽核需要 toobe 重新啟用。</span><span class="sxs-lookup"><span data-stu-id="142d6-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="142d6-192">Hello 資料庫層級防火牆規則需要 toobe 重新加入。</span><span class="sxs-lookup"><span data-stu-id="142d6-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="142d6-193">不會影響 hello 伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="142d6-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="142d6-194">(選擇性) 在移轉期間重新命名資料倉儲</span><span class="sxs-lookup"><span data-stu-id="142d6-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="142d6-195">兩個資料庫上不能有相同的邏輯伺服器 hello hello 相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="142d6-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="142d6-196">SQL 資料倉儲現在支援 hello 能力 toorename 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="142d6-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="142d6-197">在此範例中，假設您在標準儲存體上的現有資料倉儲目前名為 “MyDW”。</span><span class="sxs-lookup"><span data-stu-id="142d6-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="142d6-198">使用下列 ALTER DATABASE 命令的 hello 重新命名 「 MyDW"。</span><span class="sxs-lookup"><span data-stu-id="142d6-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="142d6-199">（在此範例中，我們會將它重新命名 「 MyDW_BeforeMigration。"） 此命令會停止所有現有的交易，並必須 hello master 資料庫 toosucceed 中完成。</span><span class="sxs-lookup"><span data-stu-id="142d6-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="142d6-200">[暫停][Pause] "MyDW_BeforeMigration"。</span><span class="sxs-lookup"><span data-stu-id="142d6-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="142d6-201">這會進行自動備份。</span><span class="sxs-lookup"><span data-stu-id="142d6-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="142d6-202">[還原][ Restore]從最新快照集 hello 名稱的新資料庫，它使用 toobe (例如，"MyDW")。</span><span class="sxs-lookup"><span data-stu-id="142d6-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="142d6-203">刪除 "MyDW_BeforeMigration"。</span><span class="sxs-lookup"><span data-stu-id="142d6-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="142d6-204">**如果您無法 toodo 此步驟中，您將支付這兩個資料倉儲。**</span><span class="sxs-lookup"><span data-stu-id="142d6-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="142d6-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="142d6-205">Next steps</span></span>
<span data-ttu-id="142d6-206">以 hello toopremium 存放裝置的變更，您也可以在 hello 基礎架構中的資料倉儲資料庫的 blob 檔案的數目會增加。</span><span class="sxs-lookup"><span data-stu-id="142d6-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="142d6-207">toomaximize hello 效能優勢，這項變更，使用下列指令碼的 hello 來重建叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="142d6-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="142d6-208">hello 指令碼的運作方式強制執行某些現有的資料 toohello 其他 blob。</span><span class="sxs-lookup"><span data-stu-id="142d6-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="142d6-209">如果您不採取任何動作，hello 資料經過一段時間自然會重新發佈，當您將更多的資料載入資料表。</span><span class="sxs-lookup"><span data-stu-id="142d6-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="142d6-210">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="142d6-210">**Prerequisites:**</span></span>

- <span data-ttu-id="142d6-211">hello 資料倉儲應執行 1,000 資料倉儲單位或更高版本 (請參閱[標尺的計算能力][scale compute power])。</span><span class="sxs-lookup"><span data-stu-id="142d6-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="142d6-212">hello 執行 hello 指令碼的使用者應該在 hello [mediumrc 角色][ mediumrc role]或更高版本。</span><span class="sxs-lookup"><span data-stu-id="142d6-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="142d6-213">tooadd 使用者 toothis 角色，執行下列 hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="142d6-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
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
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
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

<span data-ttu-id="142d6-214">如果您遇到任何問題，與您的資料倉儲[建立支援票證][ create a support ticket]以及參考 「 移轉 toopremium 儲存體 」 為 hello 可能的原因。</span><span class="sxs-lookup"><span data-stu-id="142d6-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
