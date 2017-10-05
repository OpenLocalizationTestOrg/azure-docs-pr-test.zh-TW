---
title: "Azure SQL Database 常見問題集 | Microsoft Docs"
description: "客戶詢問有關雲端資料庫與 Azure SQL Database、Microsoft 的關聯式資料庫管理系統 (RDBMS) 以及資料庫作為雲端中服務的一般問題的解答。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 1da12abc-0646-43ba-b564-e3b049a6487f
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 02/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 6ed02ead07c50b9a49e8868756b6f957d7b49b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database-faq"></a><span data-ttu-id="6930e-103">SQL Database 常見問題集</span><span class="sxs-lookup"><span data-stu-id="6930e-103">SQL Database FAQ</span></span>

## <a name="what-is-the-current-version-of-sql-database"></a><span data-ttu-id="6930e-104">最新的 SQL Database 版本為何？</span><span class="sxs-lookup"><span data-stu-id="6930e-104">What is the current version of SQL Database?</span></span>
<span data-ttu-id="6930e-105">最新的 SQL Database 版本是 V12。</span><span class="sxs-lookup"><span data-stu-id="6930e-105">The current version of SQL Database is V12.</span></span> <span data-ttu-id="6930e-106">版本 V11 已被淘汰。</span><span class="sxs-lookup"><span data-stu-id="6930e-106">Version V11 has been retired.</span></span>

## <a name="what-is-the-sla-for-sql-database"></a><span data-ttu-id="6930e-107">SQL Database 的 SLA 是什麼？</span><span class="sxs-lookup"><span data-stu-id="6930e-107">What is the SLA for SQL Database?</span></span>
<span data-ttu-id="6930e-108">我們保證客戶在基本層、標準層或進階層中之單一或彈性 Microsoft Azure SQL Database 可與我們網際網路閘道正常連線的時間，至少須達 99.99%。</span><span class="sxs-lookup"><span data-stu-id="6930e-108">We guarantee at least 99.99% of the time customers will have connectivity between their single or elastic Basic, Standard, or Premium Microsoft Azure SQL Database and our Internet gateway.</span></span> <span data-ttu-id="6930e-109">如需詳細資訊，請參閱 [SLA](http://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="6930e-109">For more information, see [SLA](http://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="how-do-i-reset-the-password-for-the-server-admin"></a><span data-ttu-id="6930e-110">如何重設伺服器系統管理員的密碼？</span><span class="sxs-lookup"><span data-stu-id="6930e-110">How do I reset the password for the server admin?</span></span>
<span data-ttu-id="6930e-111">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [SQL Server]、從清單中選取伺服器，然後按一下 [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="6930e-111">In the [Azure portal](https://portal.azure.com) click **SQL Servers**, select the server from the list, and then click **Reset Password**.</span></span>

## <a name="how-do-i-manage-databases-and-logins"></a><span data-ttu-id="6930e-112">如何管理資料庫與登入？</span><span class="sxs-lookup"><span data-stu-id="6930e-112">How do I manage databases and logins?</span></span>
<span data-ttu-id="6930e-113">請參閱[管理資料庫與登入](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="6930e-113">See [Managing databases and logins](sql-database-manage-logins.md).</span></span>

## <a name="how-do-i-make-sure-only-authorized-ip-addresses-are-allowed-to-access-a-server"></a><span data-ttu-id="6930e-114">如何確保只有授權的 IP 位址可以存取伺服器？</span><span class="sxs-lookup"><span data-stu-id="6930e-114">How do I make sure only authorized IP addresses are allowed to access a server?</span></span>
<span data-ttu-id="6930e-115">請參閱 [如何：在 SQL Database 上進行防火牆設定](sql-database-configure-firewall-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="6930e-115">See [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md).</span></span>

## <a name="how-does-the-usage-of-sql-database-show-up-on-my-bill"></a><span data-ttu-id="6930e-116">我的帳單上會用什麼方式顯示 SQL Database 的使用量？</span><span class="sxs-lookup"><span data-stu-id="6930e-116">How does the usage of SQL Database show up on my bill?</span></span>
<span data-ttu-id="6930e-117">SQL Database 是以可預測的每小時費率收費，同時根據服務層 + 單一資料庫的效能等級或每一彈性集區的 eDTU。</span><span class="sxs-lookup"><span data-stu-id="6930e-117">SQL Database bills on a predictable hourly rate based on both the service tier + performance level for single databases or eDTUs per elastic pool.</span></span> <span data-ttu-id="6930e-118">實際使用量會每小時依比例分配的方式計算，因此有可能會出現不滿一小時的帳單。</span><span class="sxs-lookup"><span data-stu-id="6930e-118">Actual usage is computed and pro-rated hourly, so your bill might show fractions of an hour.</span></span> <span data-ttu-id="6930e-119">例如，如果資料庫在一個月內的存在時間是 12 個小時，則您的帳單會顯示 0.5 天的使用量。</span><span class="sxs-lookup"><span data-stu-id="6930e-119">For example, if a database exists for 12 hours in a month, your bill shows usage of 0.5 days.</span></span> <span data-ttu-id="6930e-120">此外，服務層 + 效能等級和每一集區 eDTU 會在帳單中劃分，以讓您方便看到在單一月份中每個所使用的資料庫天數。</span><span class="sxs-lookup"><span data-stu-id="6930e-120">Additionally, service tiers + performance level and eDTUs per pool are broken out in the bill to make it easier to see the number of database days you used for each in a single month.</span></span>

## <a name="what-if-a-single-database-is-active-for-less-than-an-hour-or-uses-a-higher-service-tier-for-less-than-an-hour"></a><span data-ttu-id="6930e-121">如果單一資料庫作用中的時間少於一小時，或使用更高服務層的時間少於一小時，會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="6930e-121">What if a single database is active for less than an hour or uses a higher service tier for less than an hour?</span></span>
<span data-ttu-id="6930e-122">您需要支付使用最高服務層資料庫存在的時數 + 在該小時適用的效能等級，不論使用方式或資料庫是否在作用中少於一小時。</span><span class="sxs-lookup"><span data-stu-id="6930e-122">You are billed for each hour a database exists using the highest service tier + performance level that applied during that hour, regardless of usage or whether the database was active for less than an hour.</span></span> <span data-ttu-id="6930e-123">例如，假設您建立了單一資料庫並在五分鐘後刪除，您的帳單就會反映一個資料庫時數的費用。</span><span class="sxs-lookup"><span data-stu-id="6930e-123">For example, if you create a single database and delete it five minutes later your bill reflects a charge for one database hour.</span></span> 

<span data-ttu-id="6930e-124">範例</span><span class="sxs-lookup"><span data-stu-id="6930e-124">Examples</span></span>

* <span data-ttu-id="6930e-125">如果您建立 Basic 資料庫，並立即將它升級到 Standard S1，則我們會以 Standard S1 的費率向您收取第一個小時的費用。</span><span class="sxs-lookup"><span data-stu-id="6930e-125">If you create a Basic database and then immediately upgrade it to Standard S1, you are charged at the Standard S1 rate for the first hour.</span></span>
* <span data-ttu-id="6930e-126">如果您在下午 10:00 將資料庫從「基本」升級為「進階」，</span><span class="sxs-lookup"><span data-stu-id="6930e-126">If you upgrade a database from Basic to Premium at 10:00 p.m.</span></span> <span data-ttu-id="6930e-127">在隔天上午 1:35 完成升級，</span><span class="sxs-lookup"><span data-stu-id="6930e-127">and upgrade completes at 1:35 a.m.</span></span> <span data-ttu-id="6930e-128">則會從上午 1:00 開始「進階」費率計費。</span><span class="sxs-lookup"><span data-stu-id="6930e-128">on the following day, you are charged at the Premium rate starting at 1:00 a.m.</span></span> 
* <span data-ttu-id="6930e-129">如果您在上午 11:00 將資料庫從「進階」降級為「基本」，</span><span class="sxs-lookup"><span data-stu-id="6930e-129">If you downgrade a database from Premium to Basic at 11:00 a.m.</span></span> <span data-ttu-id="6930e-130">且該作業在下午 2:15 完成，則會針對資料庫以「進階」費率收費到下午 3:00，之後便以「基本」費率收費。</span><span class="sxs-lookup"><span data-stu-id="6930e-130">and it completes at 2:15 p.m., then the database is charged at the Premium rate until 3:00 p.m., after which it is charged at the Basic rates.</span></span>

## <a name="how-does-elastic-pool-usage-show-up-on-my-bill-and-what-happens-when-i-change-edtus-per-pool"></a><span data-ttu-id="6930e-131">彈性集區使用量如何在我的帳單上顯示，以及變更每個集區的 eDTU 時會發生什麼？</span><span class="sxs-lookup"><span data-stu-id="6930e-131">How does elastic pool usage show up on my bill and what happens when I change eDTUs per pool?</span></span>
<span data-ttu-id="6930e-132">在您的帳單上，彈性集區收費顯示為彈性 DTU (eDTU)，並在[價格頁面](https://azure.microsoft.com/pricing/details/sql-database/)上以每一集區 eDTU 遞增顯示。</span><span class="sxs-lookup"><span data-stu-id="6930e-132">Elastic pool charges show up on your bill as Elastic DTUs (eDTUs) in the increments shown under eDTUs per pool on [the pricing page](https://azure.microsoft.com/pricing/details/sql-database/).</span></span> <span data-ttu-id="6930e-133">彈性集區沒有每一資料庫的費用。</span><span class="sxs-lookup"><span data-stu-id="6930e-133">There is no per-database charge for elastic pools.</span></span> <span data-ttu-id="6930e-134">對集區存在的每個小時，您均需要支付最高的 eDTU，不論使用方式或集區是否作用中少於一小時。</span><span class="sxs-lookup"><span data-stu-id="6930e-134">You are billed for each hour a pool exists at the highest eDTU, regardless of usage or whether the pool was active for less than an hour.</span></span> 

<span data-ttu-id="6930e-135">範例</span><span class="sxs-lookup"><span data-stu-id="6930e-135">Examples</span></span>

* <span data-ttu-id="6930e-136">如果您在上午 11:18 以 200 個 eDTU 建立「標準」彈性集區，將五個資料庫加入至集區，則會向您收取該小時 200 個 eDTU 的費用，從上午 11:00 開始。</span><span class="sxs-lookup"><span data-stu-id="6930e-136">If you create a Standard elastic pool with 200 eDTUs at 11:18 a.m., adding five databases to the pool, you are charged for 200 eDTUs for the whole hour, beginning at 11 a.m.</span></span> <span data-ttu-id="6930e-137">到當天剩餘的時間。</span><span class="sxs-lookup"><span data-stu-id="6930e-137">through the remainder of the day.</span></span>
* <span data-ttu-id="6930e-138">在第 2 天上午 5:05，資料庫 1 開始取用 50 eDTU 並穩定持有一天。</span><span class="sxs-lookup"><span data-stu-id="6930e-138">On Day 2, at 5:05 a.m., Database 1 begins consuming 50 eDTUs and holds steady through the day.</span></span> <span data-ttu-id="6930e-139">資料庫 2-5 會在 0 和 80 eDTU 之間波動。</span><span class="sxs-lookup"><span data-stu-id="6930e-139">Databases 2-5 fluctuate between 0 and 80 eDTUs.</span></span> <span data-ttu-id="6930e-140">在當天，您加入全天取用不同 eDTU 的其他五個資料庫。</span><span class="sxs-lookup"><span data-stu-id="6930e-140">During the day, you add five other databases that consume varying eDTUs throughout the day.</span></span> <span data-ttu-id="6930e-141">第 2 天是全天，以 200 eDTU 計費。</span><span class="sxs-lookup"><span data-stu-id="6930e-141">Day 2 is a full day billed at 200 eDTU.</span></span> 
* <span data-ttu-id="6930e-142">在第 3 天上午 5:00，</span><span class="sxs-lookup"><span data-stu-id="6930e-142">On Day 3, at 5 a.m.</span></span> <span data-ttu-id="6930e-143">您加入另外 15 個資料庫。</span><span class="sxs-lookup"><span data-stu-id="6930e-143">you add another 15 databases.</span></span> <span data-ttu-id="6930e-144">資料庫使用量全天增加，到下午 8:05 您決定將集區的 eDTU 從 200 增加為 400。</span><span class="sxs-lookup"><span data-stu-id="6930e-144">Database usage increases throughout the day to the point where you decide to increase eDTUs for the pool from 200 to 400 at 8:05 p.m.</span></span> <span data-ttu-id="6930e-145">以 200 個 eDTU 等級收費的有效期間是到下午 8:00，並針對其餘的四小時增加至 400 個 eDTU。</span><span class="sxs-lookup"><span data-stu-id="6930e-145">Charges at the 200 eDTU level were in effect until 8 pm and increases to 400 eDTUs for the remaining four hours.</span></span> 

## <a name="elastic-pool-billing-and-pricing-information"></a><span data-ttu-id="6930e-146">彈性集區的計費和定價資訊</span><span class="sxs-lookup"><span data-stu-id="6930e-146">Elastic pool billing and pricing information</span></span>
<span data-ttu-id="6930e-147">彈性集區會依據下列特性計費：</span><span class="sxs-lookup"><span data-stu-id="6930e-147">Elastic pools are billed per the following characteristics:</span></span>

* <span data-ttu-id="6930e-148">彈性集區在建立時就會開始計費，即使集區中沒有資料庫也一樣。</span><span class="sxs-lookup"><span data-stu-id="6930e-148">An elastic pool is billed upon its creation, even when there are no databases in the pool.</span></span>
* <span data-ttu-id="6930e-149">彈性集區會以每小時計費。</span><span class="sxs-lookup"><span data-stu-id="6930e-149">An elastic pool is billed hourly.</span></span> <span data-ttu-id="6930e-150">這和單一資料庫效能等級的計量頻率相同。</span><span class="sxs-lookup"><span data-stu-id="6930e-150">This is the same metering frequency as for performance levels of single databases.</span></span>
* <span data-ttu-id="6930e-151">如果彈性集區調整為新的 eDTU 數目，則在調整作業完成之前，不會根據新的 eDTU 量來計算集區費用。</span><span class="sxs-lookup"><span data-stu-id="6930e-151">If an elastic pool is resized to a new number of eDTUs, then the pool is not billed according to the new amount of eDTUS until the resizing operation completes.</span></span> <span data-ttu-id="6930e-152">這會遵循與變更單一資料庫的效能等級相同的模式。</span><span class="sxs-lookup"><span data-stu-id="6930e-152">This follows the same pattern as changing the performance level of single databases.</span></span>
* <span data-ttu-id="6930e-153">彈性集區的價格是以集區的 eDTU 數為計算基礎。</span><span class="sxs-lookup"><span data-stu-id="6930e-153">The price of an elastic pool is based on the number of eDTUs of the pool.</span></span> <span data-ttu-id="6930e-154">彈性集區的價格與其中之彈性資料庫的數目和使用量無關。</span><span class="sxs-lookup"><span data-stu-id="6930e-154">The price of an elastic pool is independent of the number and utilization of the elastic databases within it.</span></span>
* <span data-ttu-id="6930e-155">價格的計算方式為 (集區的 eDTU 數) x (每 eDTU 的單價)。</span><span class="sxs-lookup"><span data-stu-id="6930e-155">Price is computed by (number of pool eDTUs)x(unit price per eDTU).</span></span>

<span data-ttu-id="6930e-156">在同一個服務層中，彈性集區的 eDTU 單價大於單一資料庫的 DTU 單價。</span><span class="sxs-lookup"><span data-stu-id="6930e-156">The unit eDTU price for an elastic pool is higher than the unit DTU price for a single database in the same service tier.</span></span> <span data-ttu-id="6930e-157">如需詳細資訊，請參閱 [SQL Database 定價](https://azure.microsoft.com/pricing/details/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="6930e-157">For details, see [SQL Database pricing](https://azure.microsoft.com/pricing/details/sql-database/).</span></span> 

<span data-ttu-id="6930e-158">若要了解 eDTU 及服務層，請參閱 [SQL Database 選項和效能](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="6930e-158">To understand the eDTUs and service tiers, see [SQL Database options and performance](sql-database-service-tiers.md).</span></span>

## <a name="how-does-the-use-of-active-geo-replication-in-an-elastic-pool-show-up-on-my-bill"></a><span data-ttu-id="6930e-159">在彈性集區中使用作用中異地複寫會在我的帳單上如何顯示？</span><span class="sxs-lookup"><span data-stu-id="6930e-159">How does the use of active geo-replication in an elastic pool show up on my bill?</span></span>
<span data-ttu-id="6930e-160">與單一資料庫不同，搭配彈性資料庫使用[作用中異地複寫](sql-database-geo-replication-overview.md)對計費並沒有直接的影響。</span><span class="sxs-lookup"><span data-stu-id="6930e-160">Unlike single databases, using [active geo-replication](sql-database-geo-replication-overview.md) with elastic databases doesn't have a direct billing impact.</span></span>  <span data-ttu-id="6930e-161">您只需支付對每個集區佈建的 eDTU (主要集區和次要集區)</span><span class="sxs-lookup"><span data-stu-id="6930e-161">You are only charged for the eDTUs provisioned for each of the pools (primary pool and secondary pool)</span></span>

## <a name="how-does-the-use-of-the-auditing-feature-impact-my-bill"></a><span data-ttu-id="6930e-162">使用稽核功能會如何影響帳單？</span><span class="sxs-lookup"><span data-stu-id="6930e-162">How does the use of the auditing feature impact my bill?</span></span>
<span data-ttu-id="6930e-163">稽核內建在 SQL Database 服務供免費使用，且基本、標準、進階和進階 RS 資料庫皆可使用。</span><span class="sxs-lookup"><span data-stu-id="6930e-163">Auditing is built into the SQL Database service at no extra cost and is available to Basic, Standard, Premium, and Premium RS databases.</span></span> <span data-ttu-id="6930e-164">但是，為了儲存稽核記錄檔，稽核功能會使用 Azure 儲存體帳戶，而 Azure 儲存體的費率資料表和佇列 會根據稽核記錄檔的大小套用。</span><span class="sxs-lookup"><span data-stu-id="6930e-164">However, to store the audit logs, the auditing feature uses an Azure Storage account, and rates for tables and queues in Azure Storage apply based on the size of your audit log.</span></span>

## <a name="how-do-i-find-the-right-service-tier-and-performance-level-for-single-databases-and-elastic-pools"></a><span data-ttu-id="6930e-165">我如何找到單一資料庫和彈性集區的正確服務層和效能等級？</span><span class="sxs-lookup"><span data-stu-id="6930e-165">How do I find the right service tier and performance level for single databases and elastic pools?</span></span>
<span data-ttu-id="6930e-166">有幾個工具可供您使用。</span><span class="sxs-lookup"><span data-stu-id="6930e-166">There are a few tools available to you.</span></span> 

* <span data-ttu-id="6930e-167">針對內部部署資料庫，請使用 [DTU 大小建議器](http://dtucalculator.azurewebsites.net/) 來建議需要的資料庫和 DTU，並針對彈性集區評估多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="6930e-167">For on-premises databases, use the [DTU sizing advisor](http://dtucalculator.azurewebsites.net/) to recommend the databases and DTUs required, and evaluate multiple databases for elastic pools.</span></span>
* <span data-ttu-id="6930e-168">如果單一資料庫會因集區而受益，Azure 的智慧型引擎如果發現必要的歷程使用模式，就會建議彈性集區。</span><span class="sxs-lookup"><span data-stu-id="6930e-168">If a single database would benefit from being in a pool, Azure's intelligent engine recommends an elastic pool if it sees a historical usage pattern that warrants it.</span></span> <span data-ttu-id="6930e-169">請參閱[使用 Azure 入口網站監視和管理彈性集區](sql-database-elastic-pool-manage-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6930e-169">See [Monitor and manage an elastic pool with the Azure portal](sql-database-elastic-pool-manage-portal.md).</span></span> <span data-ttu-id="6930e-170">如需有關如何自己進行數學計算的詳細資訊，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool.md)</span><span class="sxs-lookup"><span data-stu-id="6930e-170">For details about how to do the math yourself, see [Price and performance considerations for an elastic pool](sql-database-elastic-pool.md)</span></span>
* <span data-ttu-id="6930e-171">若要查看您是否需要向上或向下調整單一資料庫，請參閱 [單一資料庫的效能指引](sql-database-performance-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="6930e-171">To see whether you need to dial a single database up or down, see [performance guidance for single databases](sql-database-performance-guidance.md).</span></span>

## <a name="how-often-can-i-change-the-service-tier-or-performance-level-of-a-single-database"></a><span data-ttu-id="6930e-172">變更單一資料庫的服務層或效能等級可以多久進行一次？</span><span class="sxs-lookup"><span data-stu-id="6930e-172">How often can I change the service tier or performance level of a single database?</span></span>
<span data-ttu-id="6930e-173">您可以隨意且不限次數地，變更服務層 (在基本、標準、進階和進階 RS 之間) 或服務層內的效能等級 (例如 S1 到 S2)。</span><span class="sxs-lookup"><span data-stu-id="6930e-173">You can change the service tier (between Basic, Standard, Premium, and Premium RS) or the performance level within a service tier (for example, S1 to S2) as often as you want.</span></span> <span data-ttu-id="6930e-174">若為較早版本的資料庫，在 24 小時內，您總計只可以變更服務層或效能層級四次。</span><span class="sxs-lookup"><span data-stu-id="6930e-174">For earlier version databases, you can change the service tier or performance level a total of four times in a 24-hour period.</span></span>

## <a name="how-often-can-i-adjust-the-edtus-per-pool"></a><span data-ttu-id="6930e-175">調整每一集區 eDTU 頻率為何？</span><span class="sxs-lookup"><span data-stu-id="6930e-175">How often can I adjust the eDTUs per pool?</span></span>
<span data-ttu-id="6930e-176">視您所需，不限次數。</span><span class="sxs-lookup"><span data-stu-id="6930e-176">As often as you want.</span></span>

## <a name="how-long-does-it-take-to-change-the-service-tier-or-performance-level-of-a-single-database-or-move-a-database-in-and-out-of-an-elastic-pool"></a><span data-ttu-id="6930e-177">變更單一資料庫的服務層次或效能等級，或將資料庫移入和移出彈性集區需要多久的時間？</span><span class="sxs-lookup"><span data-stu-id="6930e-177">How long does it take to change the service tier or performance level of a single database or move a database in and out of an elastic pool?</span></span>
<span data-ttu-id="6930e-178">變更資料庫的服務層和移入和移出集區需要在平台上複製資料庫做為背景作業。</span><span class="sxs-lookup"><span data-stu-id="6930e-178">Changing the service tier of a database and moving in and out of a pool requires the database to be copied on the platform as a background operation.</span></span> <span data-ttu-id="6930e-179">視資料庫的大小而定，變更服務層可能需要數分鐘到數小時的時間不等。</span><span class="sxs-lookup"><span data-stu-id="6930e-179">Changing the service tier can take from a few minutes to several hours depending on the size of the databases.</span></span> <span data-ttu-id="6930e-180">在這兩種情況下，在移動期間，資料庫將維持完全連線且可供使用的狀態。</span><span class="sxs-lookup"><span data-stu-id="6930e-180">In both cases, the databases remain online and available during the move.</span></span> <span data-ttu-id="6930e-181">如需變更單一資料庫的詳細資訊，請參閱 [變更資料庫的服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="6930e-181">For details on changing single databases, see [Change the service tier of a database](sql-database-service-tiers.md).</span></span> 

## <a name="when-should-i-use-a-single-database-vs-elastic-databases"></a><span data-ttu-id="6930e-182">何時應該使用單一資料庫與彈性資料庫？</span><span class="sxs-lookup"><span data-stu-id="6930e-182">When should I use a single database vs. elastic databases?</span></span>
<span data-ttu-id="6930e-183">一般而言，彈性集區是專為一般 [軟體即服務 (SaaS) 應用程式模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)而設計，其中每一客戶或租用戶會有一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="6930e-183">In general, elastic pools are designed for a typical [software-as-a-service (SaaS) application pattern](sql-database-design-patterns-multi-tenancy-saas-applications.md), where there is one database per customer or tenant.</span></span> <span data-ttu-id="6930e-184">購買個別資料庫並為了符合每個資料庫的變動尖峰需求而進行超規空間管理，通常不具成本效益。</span><span class="sxs-lookup"><span data-stu-id="6930e-184">Purchasing individual databases and overprovisioning to meet the variable and peak demand for each database is often not cost efficient.</span></span> <span data-ttu-id="6930e-185">利用集區，您可管理集區的集體效能，而資料庫會自動相應增加和相應減少。</span><span class="sxs-lookup"><span data-stu-id="6930e-185">With pools, you manage the collective performance of the pool, and the databases scale up and down automatically.</span></span> <span data-ttu-id="6930e-186">Azure 的智慧型引擎如果發現必要的使用模式，就會對資料庫建議集區。</span><span class="sxs-lookup"><span data-stu-id="6930e-186">Azure's intelligent engine recommends a pool for databases when a usage pattern warrants it.</span></span> <span data-ttu-id="6930e-187">如需詳細資訊，請參閱[彈性集區指引](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="6930e-187">For details, see [Elastic pool guidance](sql-database-elastic-pool.md).</span></span>

## <a name="what-does-it-mean-to-have-up-to-200-of-your-maximum-provisioned-database-storage-for-backup-storage"></a><span data-ttu-id="6930e-188">備份儲存體可高達 200% 的最大可佈建資料庫儲存體，這是什麼意思？</span><span class="sxs-lookup"><span data-stu-id="6930e-188">What does it mean to have up to 200% of your maximum provisioned database storage for backup storage?</span></span>
<span data-ttu-id="6930e-189">備份儲存體是與自動資料庫備份相關聯的儲存體，可用於[還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)和[異地還原](sql-database-recovery-using-backups.md#geo-restore)。</span><span class="sxs-lookup"><span data-stu-id="6930e-189">Backup storage is the storage associated with your automated database backups that are used for [Point-In-Time-Restore](sql-database-recovery-using-backups.md#point-in-time-restore) and [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="6930e-190">Microsoft Azure SQL Database 提供的備份儲存體可高達 200% 的最大可佈建資料庫儲存體，且不須支付額外費用。</span><span class="sxs-lookup"><span data-stu-id="6930e-190">Microsoft Azure SQL Database provides up to 200% of your maximum provisioned database storage of backup storage at no additional cost.</span></span> <span data-ttu-id="6930e-191">例如，如果您擁有可佈建 DB 大小為 250 GB 的標準 DB 執行個體，您就能免費獲得 500 GB 的備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="6930e-191">For example, if you have a Standard DB instance with a provisioned DB size of 250 GB, you are provided with 500 GB of backup storage at no additional charge.</span></span> <span data-ttu-id="6930e-192">若您的資料庫超過所提供的備份儲存體，您可以連絡 Azure 支援部門，選擇縮短保留期限，或是以標準讀取存取地理備援儲存體 (RA-GRS) 費率，另購額外的備份儲存體。</span><span class="sxs-lookup"><span data-stu-id="6930e-192">If your database exceeds the provided backup storage, you can choose to reduce the retention period by contacting Azure Support or pay for the extra backup storage billed at standard Read-Access Geographically Redundant Storage (RA-GRS) rate.</span></span> <span data-ttu-id="6930e-193">如需 RA-GRS 計費的詳細資訊，請參閱儲存體價格詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6930e-193">For more information on RA-GRS billing, see Storage Pricing Details.</span></span>

## <a name="im-moving-from-webbusiness-to-the-new-service-tiers-what-do-i-need-to-know"></a><span data-ttu-id="6930e-194">我正從 Web/Business 移到新的服務層，我應該知道什麼？</span><span class="sxs-lookup"><span data-stu-id="6930e-194">I'm moving from Web/Business to the new service tiers, what do I need to know?</span></span>
<span data-ttu-id="6930e-195">Azure SQL Web 和 Business 資料庫現已淘汰。</span><span class="sxs-lookup"><span data-stu-id="6930e-195">Azure SQL Web and Business databases are now retired.</span></span> <span data-ttu-id="6930e-196">基本、標準、進階、進階 RS 和彈性層取代淘汰 Web 和商務資料庫。</span><span class="sxs-lookup"><span data-stu-id="6930e-196">The Basic, Standard, Premium, Premium RS, and Elastic tiers replace the retiring Web and Business databases.</span></span> 

## <a name="what-is-an-expected-replication-lag-when-geo-replicating-a-database-between-two-regions-within-the-same-azure-geography"></a><span data-ttu-id="6930e-197">在兩個 Azure 地理位置相同的區域之間，針對資料庫進行異地複寫時，預期的複寫延遲是多久？</span><span class="sxs-lookup"><span data-stu-id="6930e-197">What is an expected replication lag when geo-replicating a database between two regions within the same Azure geography?</span></span>
<span data-ttu-id="6930e-198">我們目前支援五秒的 RPO，而且當地區次要資料庫裝載於 Azure 建議的配對區域中且位於同一服務層，複寫延遲便會小於五秒。</span><span class="sxs-lookup"><span data-stu-id="6930e-198">We are currently supporting an RPO of five seconds and the replication lag has been less than that when the geo-secondary is hosted in the Azure recommended paired region and at the same service tier.</span></span>

## <a name="what-is-an-expected-replication-lag-when-geo-secondary-is-created-in-the-same-region-as-the-primary-database"></a><span data-ttu-id="6930e-199">若地區次要資料庫建立於主要資料庫相同的區域中，預期的複寫延遲是多少？</span><span class="sxs-lookup"><span data-stu-id="6930e-199">What is an expected replication lag when geo-secondary is created in the same region as the primary database?</span></span>
<span data-ttu-id="6930e-200">根據實證資料，若使用 Azure 建議配對區域，區域內部和區域之間的複寫延遲不會有太大差異。</span><span class="sxs-lookup"><span data-stu-id="6930e-200">Based on empirical data, there is not too much difference between intra-region and inter-region replication lag when the Azure recommended paired region is used.</span></span> 

## <a name="if-there-is-a-network-failure-between-two-regions-how-does-the-retry-logic-work-when-geo-replication-is-set-up"></a><span data-ttu-id="6930e-201">如果兩個區域之間網路故障，在已設定異地複寫的情況下，重試邏輯如何運作？</span><span class="sxs-lookup"><span data-stu-id="6930e-201">If there is a network failure between two regions, how does the retry logic work when geo-replication is set up?</span></span>
<span data-ttu-id="6930e-202">如果中斷連線，我們會每隔 10 秒重試，以便重新建立連線。</span><span class="sxs-lookup"><span data-stu-id="6930e-202">If there is a disconnect, we retry every 10 seconds to re-establish connections.</span></span>

## <a name="what-can-i-do-to-guarantee-that-a-critical-change-on-the-primary-database-is-replicated"></a><span data-ttu-id="6930e-203">我該如何保證主要資料庫上的重大變更能夠確實複寫？</span><span class="sxs-lookup"><span data-stu-id="6930e-203">What can I do to guarantee that a critical change on the primary database is replicated?</span></span>
<span data-ttu-id="6930e-204">地區次要資料庫為非同步複本，我們不會嘗試將該資料庫與主要資料庫維持完整同步。</span><span class="sxs-lookup"><span data-stu-id="6930e-204">The geo-secondary is an async replica and we do not try to keep it in full sync with the primary.</span></span> <span data-ttu-id="6930e-205">但是，我們會提供方法來強制進行同步處理，以確保重大變更 (例如，密碼更新) 的複寫。</span><span class="sxs-lookup"><span data-stu-id="6930e-205">But we provide a method to force synchronization to ensure the replication of critical changes (for example, password updates).</span></span> <span data-ttu-id="6930e-206">強制進行同步處理會對效能產生影響，因為它會封鎖呼叫執行緒，直到所有認可的交易都完成複寫為止。</span><span class="sxs-lookup"><span data-stu-id="6930e-206">Forced synchronization impacts performance because it blocks the calling thread until all committed transactions are replicated.</span></span> <span data-ttu-id="6930e-207">如需詳細資訊，請參閱 [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6930e-207">For details, see [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx).</span></span> 

## <a name="what-tools-are-available-to-monitor-the-replication-lag-between-the-primary-database-and-geo-secondary"></a><span data-ttu-id="6930e-208">若要監視主要資料庫和地區資料庫之間的複寫延遲，有哪些工具可以使用？</span><span class="sxs-lookup"><span data-stu-id="6930e-208">What tools are available to monitor the replication lag between the primary database and geo-secondary?</span></span>
<span data-ttu-id="6930e-209">我們會透過 DMV 將主要資料庫和地區次要資料庫之間的即時複寫延遲公開。</span><span class="sxs-lookup"><span data-stu-id="6930e-209">We expose the real-time replication lag between the primary database and geo-secondary through a DMV.</span></span> <span data-ttu-id="6930e-210">如需詳細資訊，請參閱 [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6930e-210">For details, see [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx).</span></span>

## <a name="to-move-a-database-to-a-different-server-in-the-same-subscription"></a><span data-ttu-id="6930e-211">將資料庫移到相同訂用帳戶中的不同伺服器</span><span class="sxs-lookup"><span data-stu-id="6930e-211">To move a database to a different server in the same subscription</span></span>
* <span data-ttu-id="6930e-212">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [SQL Database]、從清單中選取資料庫，然後按一下 [複製]。</span><span class="sxs-lookup"><span data-stu-id="6930e-212">In the [Azure portal](https://portal.azure.com), click **SQL databases**, select a database from the list, and then click **Copy**.</span></span> <span data-ttu-id="6930e-213">如需詳細資訊，請參閱 [複製 Azure SQL Database](sql-database-copy.md) 。</span><span class="sxs-lookup"><span data-stu-id="6930e-213">See [Copy an Azure SQL database](sql-database-copy.md) for more detail.</span></span>

## <a name="to-move-a-database-between-subscriptions"></a><span data-ttu-id="6930e-214">在訂用帳戶之間移動資料庫</span><span class="sxs-lookup"><span data-stu-id="6930e-214">To move a database between subscriptions</span></span>
* <span data-ttu-id="6930e-215">在 [Azure 入口網站](https://portal.azure.com)中，按一下 [SQL Server]，然後從清單中選取裝載您資料庫的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6930e-215">In the [Azure portal](https://portal.azure.com), click **SQL servers** and then select the server that hosts your database from the list.</span></span> <span data-ttu-id="6930e-216">按一下 [移動] ，然後挑選要移動的資源以及要移入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6930e-216">Click **Move**, and then pick the resources to move and the subscription to move to.</span></span>