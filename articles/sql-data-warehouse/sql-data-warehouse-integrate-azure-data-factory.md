---
title: "SQL 資料倉儲與 Azure Data Factory aaaUse |Microsoft 文件"
description: "搭配使用 Azure Data Factory (ADF) 與 SQL 資料倉儲以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="351d9-103">搭配使用 Azure Data Factory 與 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="351d9-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="351d9-104">Azure Data Factory 提供完全受管理的方法，來協調 hello 傳輸資料及執行 SQL 資料倉儲上的預存程序。</span><span class="sxs-lookup"><span data-stu-id="351d9-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="351d9-105">這可讓您 toomore 輕鬆地設定和排程複雜擷取轉換和載入 (ETL) 程序到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="351d9-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="351d9-106">如需更完整的 Azure Data Factory 概觀，請參閱 hello [Azure Data Factory 文件][Azure Data Factory documentation]。</span><span class="sxs-lookup"><span data-stu-id="351d9-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="351d9-107">資料移動</span><span class="sxs-lookup"><span data-stu-id="351d9-107">Data Movement</span></span>
<span data-ttu-id="351d9-108">Azure Data Factory 可讓資料在內部部署來源與不同的 Azure 服務之間移動。</span><span class="sxs-lookup"><span data-stu-id="351d9-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="351d9-109">目前的整體整合，使用 Azure Data Factory 支援的資料移動 tooand 從下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="351d9-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="351d9-110">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="351d9-110">Azure blob storage</span></span>
* <span data-ttu-id="351d9-111">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="351d9-111">Azure SQL Database</span></span>
* <span data-ttu-id="351d9-112">內部部署 SQL Server</span><span class="sxs-lookup"><span data-stu-id="351d9-112">On-premises SQL Server</span></span>
* <span data-ttu-id="351d9-113">IaaS 上的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="351d9-113">SQL Server on IaaS</span></span>

<span data-ttu-id="351d9-114">資料備份 tooset 如何複製活動的詳細資訊請參閱[複製資料與 Azure Data Factory][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="351d9-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="351d9-115">預存程序</span><span class="sxs-lookup"><span data-stu-id="351d9-115">Stored Procedures</span></span>
 <span data-ttu-id="351d9-116">在 hello 相同方式，會使用 tooschedule 資料傳輸，Azure Data Factory 可以也使用的 tooorchestrate hello 執行預存程序。</span><span class="sxs-lookup"><span data-stu-id="351d9-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="351d9-117">這允許更複雜的管線 toobe 建立，並擴充 Azure Data Factory 的能力 tooleverage hello 運算能力更佳的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="351d9-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="351d9-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="351d9-118">Next steps</span></span>
<span data-ttu-id="351d9-119">如需整合概觀，請參閱 [SQL 資料倉儲整合概觀][SQL Data Warehouse integration overview]。</span><span class="sxs-lookup"><span data-stu-id="351d9-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="351d9-120">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="351d9-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

