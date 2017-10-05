---
title: "在 Azure SQL 資料倉儲中監視使用者查詢 | Microsoft Docs"
description: "監視 Azure SQL 資料倉儲中使用者查詢之考量、最佳做法及工作的概觀。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 65509a65c2b34553822cc02d7a7fa5a614adc57f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="4b2f9-103">監視 Azure SQL 資料倉儲中的使用者查詢</span><span class="sxs-lookup"><span data-stu-id="4b2f9-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="4b2f9-104">監視 SQL 資料倉儲中使用者查詢之考量、最佳做法及工作的概觀。</span><span class="sxs-lookup"><span data-stu-id="4b2f9-104">Overview of the considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="4b2f9-105">類別</span><span class="sxs-lookup"><span data-stu-id="4b2f9-105">Category</span></span> | <span data-ttu-id="4b2f9-106">工作或考量</span><span class="sxs-lookup"><span data-stu-id="4b2f9-106">Task or consideration</span></span> | <span data-ttu-id="4b2f9-107">說明</span><span class="sxs-lookup"><span data-stu-id="4b2f9-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4b2f9-108">效能變慢</span><span class="sxs-lookup"><span data-stu-id="4b2f9-108">Slow performance</span></span> |<span data-ttu-id="4b2f9-109">尋找長時間執行的使用者查詢</span><span class="sxs-lookup"><span data-stu-id="4b2f9-109">Find a long-running user query</span></span> |<span data-ttu-id="4b2f9-110">[尋找長時間執行的查詢][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="4b2f9-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="4b2f9-111">並行</span><span class="sxs-lookup"><span data-stu-id="4b2f9-111">Concurrency</span></span> |<span data-ttu-id="4b2f9-112">指派並行資源給使用者查詢</span><span class="sxs-lookup"><span data-stu-id="4b2f9-112">Assign concurrent resources to user queries</span></span> |<span data-ttu-id="4b2f9-113">[並行和工作負載管理][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="4b2f9-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4b2f9-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b2f9-114">Next steps</span></span>
<span data-ttu-id="4b2f9-115">如需更多管理祕訣，請移至[管理概觀][Management overview]。</span><span class="sxs-lookup"><span data-stu-id="4b2f9-115">For more management tips, head over to the [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
