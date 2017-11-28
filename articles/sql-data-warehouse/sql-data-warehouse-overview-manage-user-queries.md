---
title: "在 Azure SQL 資料倉儲 aaaMonitor 使用者查詢 |Microsoft 文件"
description: "Hello 考量、 最佳做法及監視使用者在 Azure SQL 資料倉儲中的查詢工作的概觀"
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
ms.openlocfilehash: 67639e81b04635452e1ed844fe2d7245aa96a4fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="e17a9-103">監視 Azure SQL 資料倉儲中的使用者查詢</span><span class="sxs-lookup"><span data-stu-id="e17a9-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="e17a9-104">Hello 考量、 最佳做法及監視 SQL 資料倉儲中的使用者查詢工作的概觀。</span><span class="sxs-lookup"><span data-stu-id="e17a9-104">Overview of hello considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="e17a9-105">類別</span><span class="sxs-lookup"><span data-stu-id="e17a9-105">Category</span></span> | <span data-ttu-id="e17a9-106">工作或考量</span><span class="sxs-lookup"><span data-stu-id="e17a9-106">Task or consideration</span></span> | <span data-ttu-id="e17a9-107">說明</span><span class="sxs-lookup"><span data-stu-id="e17a9-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e17a9-108">效能變慢</span><span class="sxs-lookup"><span data-stu-id="e17a9-108">Slow performance</span></span> |<span data-ttu-id="e17a9-109">尋找長時間執行的使用者查詢</span><span class="sxs-lookup"><span data-stu-id="e17a9-109">Find a long-running user query</span></span> |<span data-ttu-id="e17a9-110">[尋找長時間執行的查詢][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="e17a9-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="e17a9-111">並行</span><span class="sxs-lookup"><span data-stu-id="e17a9-111">Concurrency</span></span> |<span data-ttu-id="e17a9-112">指派並行資源 toouser 查詢</span><span class="sxs-lookup"><span data-stu-id="e17a9-112">Assign concurrent resources toouser queries</span></span> |<span data-ttu-id="e17a9-113">[並行和工作負載管理][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="e17a9-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e17a9-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e17a9-114">Next steps</span></span>
<span data-ttu-id="e17a9-115">如需管理秘訣，前端透過 toohello[管理概觀][Management overview]。</span><span class="sxs-lookup"><span data-stu-id="e17a9-115">For more management tips, head over toohello [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
