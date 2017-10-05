---
title: "Azure SQL Database 資源限制 | Microsoft Docs"
description: "此頁面描述一些 Azure SQL Database 常見的資源限制。"
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: e75458db79e6c15f8d5155b71f04a20fa21818ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-resource-limits"></a><span data-ttu-id="e14b9-103">Azure SQL Database 資源限制</span><span class="sxs-lookup"><span data-stu-id="e14b9-103">Azure SQL Database resource limits</span></span>
## <a name="overview"></a><span data-ttu-id="e14b9-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e14b9-104">Overview</span></span>
<span data-ttu-id="e14b9-105">Azure SQL Database 使用兩種不同機制來管理資料庫可使用的資源：**資源管理**和**限制強制執行**。</span><span class="sxs-lookup"><span data-stu-id="e14b9-105">Azure SQL Database manages the resources available to a database using two different mechanisms: **Resources Governance** and **Enforcement of Limits**.</span></span> <span data-ttu-id="e14b9-106">本主題將說明這兩種主要的資源管理方法。</span><span class="sxs-lookup"><span data-stu-id="e14b9-106">This topic explains these two main areas of resource management.</span></span>

## <a name="resource-governance"></a><span data-ttu-id="e14b9-107">資源管理</span><span class="sxs-lookup"><span data-stu-id="e14b9-107">Resource governance</span></span>
<span data-ttu-id="e14b9-108">基本、標準、進階和進階 RS 服務層的設計目的之一，是讓 Azure SQL Database 彷彿在獨立的電腦上執行，而與其他資料庫隔離。</span><span class="sxs-lookup"><span data-stu-id="e14b9-108">One of the design goals of the Basic, Standard, Premium, and Premium RS service tiers is for Azure SQL Database to behave as if the database is running on its own machine, isolated from other databases.</span></span> <span data-ttu-id="e14b9-109">資源管理便會模擬這個行為。</span><span class="sxs-lookup"><span data-stu-id="e14b9-109">Resource governance emulates this behavior.</span></span> <span data-ttu-id="e14b9-110">如果彙總的資源使用率達到可用 CPU、記憶體、記錄 I/O 和資料 I/O 資源 (指派至資料庫) 的上限，資源管理會將查詢排入執行佇列中，並在系統釋出資源時，適時將資源指派給佇列中的查詢。</span><span class="sxs-lookup"><span data-stu-id="e14b9-110">If the aggregated resource utilization reaches the maximum available CPU, Memory, Log I/O, and Data I/O resources assigned to the database, resource governance queues queries in execution and assign resources to the queued queries as they free up.</span></span>

<span data-ttu-id="e14b9-111">在專用的電腦上使用所有可用的資源，會導致目前正在執行的查詢花費更多執行時間，而這可能會使得用戶端上的命令逾時。</span><span class="sxs-lookup"><span data-stu-id="e14b9-111">As on a dedicated machine, utilizing all available resources results in a longer execution of currently executing queries, which can result in command timeouts on the client.</span></span> <span data-ttu-id="e14b9-112">具備積極重試邏輯的應用程式，以及時常對資料庫執行查詢的應用程式，若在嘗試執行新查詢時達到並行要求的上限，便可能出現錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="e14b9-112">Applications with aggressive retry logic and applications that execute queries against the database with a high frequency can encounter errors messages when trying to execute new queries when the limit of concurrent requests has been reached.</span></span>

### <a name="recommendations"></a><span data-ttu-id="e14b9-113">建議：</span><span class="sxs-lookup"><span data-stu-id="e14b9-113">Recommendations:</span></span>
<span data-ttu-id="e14b9-114">資料庫使用率接近上限時，監視資源使用率以及查詢的平均回應時間。</span><span class="sxs-lookup"><span data-stu-id="e14b9-114">Monitor the resource utilization and the average response times of queries when nearing the maximum utilization of a database.</span></span> <span data-ttu-id="e14b9-115">查詢的延遲較高時，您通常可採取三種應對方式：</span><span class="sxs-lookup"><span data-stu-id="e14b9-115">When encountering higher query latencies you generally have three options:</span></span>

1. <span data-ttu-id="e14b9-116">減少資料庫的傳入要求數目，以避免逾時和要求不斷累積。</span><span class="sxs-lookup"><span data-stu-id="e14b9-116">Reduce the number of incoming requests to the database to prevent timeout and the pile up of requests.</span></span>
2. <span data-ttu-id="e14b9-117">為資料庫指派更高的效能層級。</span><span class="sxs-lookup"><span data-stu-id="e14b9-117">Assign a higher performance level to the database.</span></span>
3. <span data-ttu-id="e14b9-118">將查詢最佳化，以降低每個查詢的資源使用率。</span><span class="sxs-lookup"><span data-stu-id="e14b9-118">Optimize queries to reduce the resource utilization of each query.</span></span> <span data-ttu-id="e14b9-119">如需詳細資訊，請參閱＜Azure SQL Database 效能指南＞一文的「查詢微調/提示」章節。</span><span class="sxs-lookup"><span data-stu-id="e14b9-119">For more information, see the Query Tuning/Hinting section in the Azure SQL Database Performance Guidance article.</span></span>

## <a name="enforcement-of-limits"></a><span data-ttu-id="e14b9-120">限制強制執行</span><span class="sxs-lookup"><span data-stu-id="e14b9-120">Enforcement of limits</span></span>
<span data-ttu-id="e14b9-121">系統會在達到上限時拒絕新的要求，藉此強制執行 CPU、記憶體、記錄 I/O 和資料 I/O 以外的資源。</span><span class="sxs-lookup"><span data-stu-id="e14b9-121">Resources other than CPU, Memory, Log I/O, and Data I/O are enforced by denying new requests when limits are reached.</span></span> <span data-ttu-id="e14b9-122">當資料庫達到設定的大小上限時，會使得資料大小增加的插入與更新作業將會失敗，但選取與刪除作業仍能繼續運作。</span><span class="sxs-lookup"><span data-stu-id="e14b9-122">When a database reaches the configured maximum size limit, inserts and updates that increase data size fail, while selects and deletes continue to work.</span></span> <span data-ttu-id="e14b9-123">用戶端收到的[錯誤訊息](sql-database-develop-error-messages.md)會因達到的上限而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e14b9-123">Clients receive an [error message](sql-database-develop-error-messages.md) depending on the limit that has been reached.</span></span>

<span data-ttu-id="e14b9-124">例如，SQL Database 的連線數，以及可以處理的並行要求數目都將受到限制。</span><span class="sxs-lookup"><span data-stu-id="e14b9-124">For example, the number of connections to a SQL database and the number of concurrent requests that can be processed are restricted.</span></span> <span data-ttu-id="e14b9-125">SQL Database 可允許資料庫的連接數大於並行要求的數目，以支援連接共用。</span><span class="sxs-lookup"><span data-stu-id="e14b9-125">SQL Database allows the number of connections to the database to be greater than the number of concurrent requests to support connection pooling.</span></span> <span data-ttu-id="e14b9-126">雖然應用程式能輕易控制可用的連接數目，但平行要求的數目通常難以預估及控制。</span><span class="sxs-lookup"><span data-stu-id="e14b9-126">While the number of connections that are available can easily be controlled by the application, the number of parallel requests is often times harder to estimate and to control.</span></span> <span data-ttu-id="e14b9-127">尤其在尖峰負載期間，應用程式往往傳送過多的要求，或是資料庫在達到資源上限後，因為執行耗時較長的查詢而開始累積背景工作執行緒，此時就可能發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="e14b9-127">Especially during peak loads when the application either sends too many requests or the database reaches its resource limits and starts piling up worker threads due to longer running queries, errors can be encountered.</span></span>

## <a name="service-tiers-and-performance-levels"></a><span data-ttu-id="e14b9-128">服務層和效能等級</span><span class="sxs-lookup"><span data-stu-id="e14b9-128">Service tiers and performance levels</span></span>
<span data-ttu-id="e14b9-129">單一資料庫和彈性集區都有服務層和效能等級。</span><span class="sxs-lookup"><span data-stu-id="e14b9-129">There are service tiers and performance levels for both single database and elastic pools.</span></span>

### <a name="single-databases"></a><span data-ttu-id="e14b9-130">單一資料庫</span><span class="sxs-lookup"><span data-stu-id="e14b9-130">Single databases</span></span>
<span data-ttu-id="e14b9-131">對於單一資料庫，資料庫的限制是由服務層級和效能等級所定義。</span><span class="sxs-lookup"><span data-stu-id="e14b9-131">For a single database, the limits of a database are defined by the database service tier and performance level.</span></span> <span data-ttu-id="e14b9-132">下表說明基本、標準、進階和進階 RS 資料庫在不同效能等級的特性。</span><span class="sxs-lookup"><span data-stu-id="e14b9-132">The following table describes the characteristics of Basic, Standard, Premium, and Premium RS databases at varying performance levels.</span></span>

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> <span data-ttu-id="e14b9-133">使用 P11 和 P15 效能等級的客戶不需額外付費就能使用最多 4 TB 的內含儲存體。</span><span class="sxs-lookup"><span data-stu-id="e14b9-133">Customers using P11 and P15 performance levels can use up to 4 TB of included storage at no additional charge.</span></span> <span data-ttu-id="e14b9-134">這個 4 TB 選項目前已在下列區域提供：美國東部 2、美國西部、美國維吉尼亞州政府、西歐、德國中部、東南亞、日本東部、澳大利亞東部、加拿大中部和加拿大東部。</span><span class="sxs-lookup"><span data-stu-id="e14b9-134">This 4 TB option is currently available in the following regions: US East2, West US, US Gov Virginia, West Europe, Germany Central, South East Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>
>

### <a name="elastic-pools"></a><span data-ttu-id="e14b9-135">彈性集區</span><span class="sxs-lookup"><span data-stu-id="e14b9-135">Elastic pools</span></span>
<span data-ttu-id="e14b9-136">[彈性集區](sql-database-elastic-pool.md) 可在集區中的資料庫之間共用資源。</span><span class="sxs-lookup"><span data-stu-id="e14b9-136">[Elastic pools](sql-database-elastic-pool.md) share resources across databases in the pool.</span></span> <span data-ttu-id="e14b9-137">下表說明基本、標準、進階和進階 RS 彈性集區的特性。</span><span class="sxs-lookup"><span data-stu-id="e14b9-137">The following table describes the characteristics of Basic, Standard, Premium, and Premium RS elastic pools.</span></span>

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

<span data-ttu-id="e14b9-138">如需上述表格所列之每項資源的擴充定義，請參閱[服務層功能和限制](sql-database-performance-guidance.md#service-tier-capabilities-and-limits)中的說明。</span><span class="sxs-lookup"><span data-stu-id="e14b9-138">For an expanded definition of each resource listed in the previous tables, see the descriptions in [Service tier capabilities and limits](sql-database-performance-guidance.md#service-tier-capabilities-and-limits).</span></span> <span data-ttu-id="e14b9-139">如需服務層的概觀，請參閱 [Azure SQL Database 服務層和效能等級](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-139">For an overview of service tiers, see [Azure SQL Database Service Tiers and Performance Levels](sql-database-service-tiers.md).</span></span>

## <a name="other-sql-database-limits"></a><span data-ttu-id="e14b9-140">其他 SQL Database 限制</span><span class="sxs-lookup"><span data-stu-id="e14b9-140">Other SQL Database limits</span></span>
| <span data-ttu-id="e14b9-141">領域</span><span class="sxs-lookup"><span data-stu-id="e14b9-141">Area</span></span> | <span data-ttu-id="e14b9-142">限制</span><span class="sxs-lookup"><span data-stu-id="e14b9-142">Limit</span></span> | <span data-ttu-id="e14b9-143">說明</span><span class="sxs-lookup"><span data-stu-id="e14b9-143">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e14b9-144">每個訂用帳戶使用自動匯出的資料庫</span><span class="sxs-lookup"><span data-stu-id="e14b9-144">Databases using Automated export per subscription</span></span> |<span data-ttu-id="e14b9-145">10</span><span class="sxs-lookup"><span data-stu-id="e14b9-145">10</span></span> |<span data-ttu-id="e14b9-146">自動匯出可讓您建立自訂排程以備份 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="e14b9-146">Automated export allows you to create a custom schedule for backing up your SQL databases.</span></span> <span data-ttu-id="e14b9-147">此功能的預覽將於 2017 年 3 月 1 日結束。</span><span class="sxs-lookup"><span data-stu-id="e14b9-147">The preview of this feature will end on March 1, 2017.</span></span>  |
| <span data-ttu-id="e14b9-148">每一伺服器的資料庫</span><span class="sxs-lookup"><span data-stu-id="e14b9-148">Databases per server</span></span> |<span data-ttu-id="e14b9-149">最多 5000 個</span><span class="sxs-lookup"><span data-stu-id="e14b9-149">Up to 5000</span></span> |<span data-ttu-id="e14b9-150">每一部伺服器最多允許 5000 個資料庫。</span><span class="sxs-lookup"><span data-stu-id="e14b9-150">Up to 5000 databases are allowed per server.</span></span> |
| <span data-ttu-id="e14b9-151">每一部伺服器的 DTU</span><span class="sxs-lookup"><span data-stu-id="e14b9-151">DTUs per server</span></span> |<span data-ttu-id="e14b9-152">45000</span><span class="sxs-lookup"><span data-stu-id="e14b9-152">45000</span></span> |<span data-ttu-id="e14b9-153">每一部伺服器允許 45000 個 DTU，以佈建獨立資料庫和彈性集區。</span><span class="sxs-lookup"><span data-stu-id="e14b9-153">45000 DTUs are allowed per server for provisioning standalone databases and elastic pools.</span></span> <span data-ttu-id="e14b9-154">每一伺服器允許的獨立資料庫和集區總數，僅受限於伺服器 DTU 數目。</span><span class="sxs-lookup"><span data-stu-id="e14b9-154">The total number of standalone databases and pools allowed per server is limited only by the number of server DTUs.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="e14b9-155">Azure SQL 資料庫自動匯出目前為預覽狀態，並會在 2017 年 3 月 1 日停用。</span><span class="sxs-lookup"><span data-stu-id="e14b9-155">Azure SQL Database Automated Export is now in preview and will be retired on March 1, 2017.</span></span> <span data-ttu-id="e14b9-156">從 2016 年 12 月 1 日開始，您將無法再於任何 SQL 資料庫上設定自動匯出。</span><span class="sxs-lookup"><span data-stu-id="e14b9-156">Starting December 1st, 2016, you will no longer be able to configure automated export on any SQL database.</span></span> <span data-ttu-id="e14b9-157">所有現有的自動匯出作業會繼續運作至 2017 年 3 月 1 日。</span><span class="sxs-lookup"><span data-stu-id="e14b9-157">All your existing automated export jobs will continue to work until March 1st, 2017.</span></span> <span data-ttu-id="e14b9-158">2016 年 12 月 1 日之後，您可以使用[長期的備份保留](sql-database-long-term-retention.md)或 [Azure 自動化](../automation/automation-intro.md)，根據您選擇的排程使用 PowerShell 定期封存 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="e14b9-158">After December 1st, 2016, you can use [long-term backup retention](sql-database-long-term-retention.md) or [Azure Automation](../automation/automation-intro.md) to archive SQL databases periodically using PowerShell periodically according to a schedule of your choice.</span></span> <span data-ttu-id="e14b9-159">如需範例指令碼，您可以[從 GitHub 下載範例指令碼](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-159">For a sample script, you can download the [sample script from GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).</span></span>
>


## <a name="resources"></a><span data-ttu-id="e14b9-160">資源</span><span class="sxs-lookup"><span data-stu-id="e14b9-160">Resources</span></span>
[<span data-ttu-id="e14b9-161">Azure 訂用帳戶和服務限制、配額與限制</span><span class="sxs-lookup"><span data-stu-id="e14b9-161">Azure Subscription and Service Limits, Quotas, and Constraints</span></span>](../azure-subscription-service-limits.md)

[<span data-ttu-id="e14b9-162">Azure SQL Database 服務層和效能層級</span><span class="sxs-lookup"><span data-stu-id="e14b9-162">Azure SQL Database Service Tiers and Performance Levels</span></span>](sql-database-service-tiers.md)

[<span data-ttu-id="e14b9-163">SQL Database 用戶端程式的錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="e14b9-163">Error messages for SQL Database client programs</span></span>](sql-database-develop-error-messages.md)
