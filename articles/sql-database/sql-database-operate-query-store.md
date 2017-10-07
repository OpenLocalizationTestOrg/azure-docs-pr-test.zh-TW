---
title: "aaaOperating Azure SQL Database 中的查詢存放區"
description: "了解如何 toooperate hello Azure SQL Database 中的查詢存放區"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a><span data-ttu-id="5e5b4-103">作業 hello Azure SQL Database 中的查詢存放區</span><span class="sxs-lookup"><span data-stu-id="5e5b4-103">Operating hello Query Store in Azure SQL Database</span></span>
<span data-ttu-id="5e5b4-104">Azure 中的查詢存放區是完全受管理的資料庫功能，可持續收集及呈現有關所有查詢的詳細歷程記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-104">Query Store in Azure is a fully managed database feature that continuously collects and presents detailed historic information about all queries.</span></span> <span data-ttu-id="5e5b4-105">您可以將有關查詢存放區視為類似 tooan 飛機的飛行資料記錄器，大幅簡化了查詢效能進行疑難排解的雲端和內部部署客戶。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-105">You can think about Query Store as similar tooan airplane's flight data recorder that significantly simplifies query performance troubleshooting both for cloud and on-premises customers.</span></span> <span data-ttu-id="5e5b4-106">這篇文章說明在 Azure 中操作查詢存放區的特定層面。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-106">This article explains specific aspects of operating Query Store in Azure.</span></span> <span data-ttu-id="5e5b4-107">您可以使用此預先收集的查詢資料，快速地診斷並解決效能問題，因此能夠花更多時間專注於業務上。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-107">Using this pre-collected query data, you can quickly diagnose and resolve performance problems and thus spend more time focusing on their business.</span></span> 

<span data-ttu-id="5e5b4-108">查詢存放區已自 2015 年 11 月在 Azure SQL Database 中 [通用版本上市](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) 。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-108">Query Store has been [globally available](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) in Azure SQL Database since November, 2015.</span></span> <span data-ttu-id="5e5b4-109">查詢存放區是 hello 基礎效能分析及調整功能，例如[SQL 資料庫建議程式與效能儀表板](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-109">Query Store is hello foundation for performance analysis and tuning features, such as [SQL Database Advisor and Performance Dashboard](https://azure.microsoft.com/updates/sqldatabaseadvisorga/).</span></span> <span data-ttu-id="5e5b4-110">在發行這篇文章的 hello 時刻，查詢存放區正在執行中 200,000 以上的使用者資料庫，在 Azure 中，收集查詢相關的幾個月，而不中斷的資訊。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-110">At hello moment of publishing this article, Query Store is running in more than 200,000 user databases in Azure, collecting query-related information for several months, without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e5b4-111">Microsoft 是啟用查詢存放區的所有 Azure SQL 資料庫 （現有和新） hello 處理程序中。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-111">Microsoft is in hello process of activating Query Store for all Azure SQL databases (existing and new).</span></span> 
> 
> 

## <a name="optimal-query-store-configuration"></a><span data-ttu-id="5e5b4-112">最佳查詢存放區組態</span><span class="sxs-lookup"><span data-stu-id="5e5b4-112">Optimal Query Store Configuration</span></span>
<span data-ttu-id="5e5b4-113">本章節描述最佳組態的預設值設計的 tooensure 作業可靠的 hello 查詢存放區和相依的功能，例如[SQL 資料庫建議程式與效能儀表板](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-113">This section describes optimal configuration defaults that are designed tooensure reliable operation of hello Query Store and dependent features, such as [SQL Database Advisor and Performance Dashboard](https://azure.microsoft.com/updates/sqldatabaseadvisorga/).</span></span> <span data-ttu-id="5e5b4-114">預設組態已針對持續收集資料最佳化，也就是在 OFF/READ_ONLY 狀態花費最少的時間。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-114">Default configuration is optimized for continuous data collection, that is minimal time spent in OFF/READ_ONLY states.</span></span>

| <span data-ttu-id="5e5b4-115">組態</span><span class="sxs-lookup"><span data-stu-id="5e5b4-115">Configuration</span></span> | <span data-ttu-id="5e5b4-116">說明</span><span class="sxs-lookup"><span data-stu-id="5e5b4-116">Description</span></span> | <span data-ttu-id="5e5b4-117">預設值</span><span class="sxs-lookup"><span data-stu-id="5e5b4-117">Default</span></span> | <span data-ttu-id="5e5b4-118">註解</span><span class="sxs-lookup"><span data-stu-id="5e5b4-118">Comment</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e5b4-119">MAX_STORAGE_SIZE_MB</span><span class="sxs-lookup"><span data-stu-id="5e5b4-119">MAX_STORAGE_SIZE_MB</span></span> |<span data-ttu-id="5e5b4-120">指定查詢存放區可能需要 z 客戶資料庫內部的 hello 資料空間的 hello 上限</span><span class="sxs-lookup"><span data-stu-id="5e5b4-120">Specifies hello limit for hello data space that Query Store can take inside z customer database</span></span> |<span data-ttu-id="5e5b4-121">100</span><span class="sxs-lookup"><span data-stu-id="5e5b4-121">100</span></span> |<span data-ttu-id="5e5b4-122">對新資料庫強制執行</span><span class="sxs-lookup"><span data-stu-id="5e5b4-122">Enforced for new databases</span></span> |
| <span data-ttu-id="5e5b4-123">INTERVAL_LENGTH_MINUTES</span><span class="sxs-lookup"><span data-stu-id="5e5b4-123">INTERVAL_LENGTH_MINUTES</span></span> |<span data-ttu-id="5e5b4-124">定義彙總和保存查詢計畫所收集到的執行階段統計資料的時段大小。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-124">Defines size of time window during which collected runtime statistics for query plans are aggregated and persisted.</span></span> <span data-ttu-id="5e5b4-125">對於此組態定義的一段時間，每個使用中的查詢計劃最多會有一個資料列</span><span class="sxs-lookup"><span data-stu-id="5e5b4-125">Every active query plan has at most one row for a period of time defined with this configuration</span></span> |<span data-ttu-id="5e5b4-126">60</span><span class="sxs-lookup"><span data-stu-id="5e5b4-126">60</span></span> |<span data-ttu-id="5e5b4-127">對新資料庫強制執行</span><span class="sxs-lookup"><span data-stu-id="5e5b4-127">Enforced for new databases</span></span> |
| <span data-ttu-id="5e5b4-128">STALE_QUERY_THRESHOLD_DAYS</span><span class="sxs-lookup"><span data-stu-id="5e5b4-128">STALE_QUERY_THRESHOLD_DAYS</span></span> |<span data-ttu-id="5e5b4-129">以時間為基礎的清除原則，可控制保存的執行階段統計資料和非使用中查詢的 hello 保留期限</span><span class="sxs-lookup"><span data-stu-id="5e5b4-129">Time-based cleanup policy that controls hello retention period of persisted runtime statistics and inactive queries</span></span> |<span data-ttu-id="5e5b4-130">30</span><span class="sxs-lookup"><span data-stu-id="5e5b4-130">30</span></span> |<span data-ttu-id="5e5b4-131">對新資料庫和具有先前的預設值 (367) 的資料庫強制執行</span><span class="sxs-lookup"><span data-stu-id="5e5b4-131">Enforced for new databases and databases with previous default (367)</span></span> |
| <span data-ttu-id="5e5b4-132">SIZE_BASED_CLEANUP_MODE</span><span class="sxs-lookup"><span data-stu-id="5e5b4-132">SIZE_BASED_CLEANUP_MODE</span></span> |<span data-ttu-id="5e5b4-133">指定是否自動清除資料都發生在查詢存放區資料的大小接近 hello 限制</span><span class="sxs-lookup"><span data-stu-id="5e5b4-133">Specifies whether automatic data cleanup takes place when Query Store data size approaches hello limit</span></span> |<span data-ttu-id="5e5b4-134">AUTO</span><span class="sxs-lookup"><span data-stu-id="5e5b4-134">AUTO</span></span> |<span data-ttu-id="5e5b4-135">對所有資料庫強制執行</span><span class="sxs-lookup"><span data-stu-id="5e5b4-135">Enforced for all databases</span></span> |
| <span data-ttu-id="5e5b4-136">QUERY_CAPTURE_MODE</span><span class="sxs-lookup"><span data-stu-id="5e5b4-136">QUERY_CAPTURE_MODE</span></span> |<span data-ttu-id="5e5b4-137">指定是否會追蹤所有查詢或只有查詢的子集</span><span class="sxs-lookup"><span data-stu-id="5e5b4-137">Specifies whether all queries or only a subset of queries are tracked</span></span> |<span data-ttu-id="5e5b4-138">AUTO</span><span class="sxs-lookup"><span data-stu-id="5e5b4-138">AUTO</span></span> |<span data-ttu-id="5e5b4-139">對所有資料庫強制執行</span><span class="sxs-lookup"><span data-stu-id="5e5b4-139">Enforced for all databases</span></span> |
| <span data-ttu-id="5e5b4-140">FLUSH_INTERVAL_SECONDS</span><span class="sxs-lookup"><span data-stu-id="5e5b4-140">FLUSH_INTERVAL_SECONDS</span></span> |<span data-ttu-id="5e5b4-141">指定最長期間的擷取執行階段統計資料會保留在記憶體中之前排清 toodisk</span><span class="sxs-lookup"><span data-stu-id="5e5b4-141">Specifies maximum period during which captured runtime statistics are kept in memory, before flushing toodisk</span></span> |<span data-ttu-id="5e5b4-142">900</span><span class="sxs-lookup"><span data-stu-id="5e5b4-142">900</span></span> |<span data-ttu-id="5e5b4-143">對新資料庫強制執行</span><span class="sxs-lookup"><span data-stu-id="5e5b4-143">Enforced for new databases</span></span> |
|  | | | |

> [!IMPORTANT]
> <span data-ttu-id="5e5b4-144">在查詢存放區啟用 （請參閱上述的重要附註） 的所有 Azure SQL 資料庫中的 hello 最後階段中，會自動套用這些預設值。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-144">These defaults are automatically applied in hello final stage of Query Store activation in all Azure SQL databases (see preceding important note).</span></span> <span data-ttu-id="5e5b4-145">之後設定此燈，Azure SQL Database 不變更組態值設定的客戶，除非它們產生負面影響主要工作負載或可靠的 hello 查詢存放區的作業。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-145">After this light up, Azure SQL Database won’t be changing configuration values set by customers, unless they negatively impact primary workload or reliable operations of hello Query Store.</span></span>
> 
> 

<span data-ttu-id="5e5b4-146">如果您想 toostay 的自訂設定，請使用[使用查詢存放區選項的 ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) toorevert 組態 toohello 先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-146">If you want toostay with your custom settings, use [ALTER DATABASE with Query Store options](https://msdn.microsoft.com/library/bb522682.aspx) toorevert configuration toohello previous state.</span></span> <span data-ttu-id="5e5b4-147">簽出[hello 查詢存放區的最佳做法](https://msdn.microsoft.com/library/mt604821.aspx)順序 toolearn 如何頂端選擇最佳的組態參數。</span><span class="sxs-lookup"><span data-stu-id="5e5b4-147">Check out [Best Practices with hello Query Store](https://msdn.microsoft.com/library/mt604821.aspx) in order toolearn how top chose optimal configuration parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e5b4-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e5b4-148">Next steps</span></span>
[<span data-ttu-id="5e5b4-149">SQL Database 效能深入解析</span><span class="sxs-lookup"><span data-stu-id="5e5b4-149">SQL Database Performance Insight</span></span>](sql-database-performance.md)

## <a name="additional-resources"></a><span data-ttu-id="5e5b4-150">其他資源</span><span class="sxs-lookup"><span data-stu-id="5e5b4-150">Additional resources</span></span>
<span data-ttu-id="5e5b4-151">詳細的資訊簽出 hello 下列文章：</span><span class="sxs-lookup"><span data-stu-id="5e5b4-151">For more information check out hello following articles:</span></span>

* [<span data-ttu-id="5e5b4-152">您的資料庫的航班資料錄製器</span><span class="sxs-lookup"><span data-stu-id="5e5b4-152">A flight data recorder for your database</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [<span data-ttu-id="5e5b4-153">監視效能所使用的 hello 查詢存放區</span><span class="sxs-lookup"><span data-stu-id="5e5b4-153">Monitoring Performance By Using hello Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="5e5b4-154">查詢存放區使用案例</span><span class="sxs-lookup"><span data-stu-id="5e5b4-154">Query Store Usage Scenarios</span></span>](https://msdn.microsoft.com/library/mt614796.aspx)
* [<span data-ttu-id="5e5b4-155">監視效能所使用的 hello 查詢存放區</span><span class="sxs-lookup"><span data-stu-id="5e5b4-155">Monitoring Performance By Using hello Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx) 

