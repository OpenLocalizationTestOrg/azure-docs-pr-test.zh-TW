---
title: "SQL 資料倉儲中使用者定義的結構描述 | Microsoft Docs"
description: "在 Azure SQL 資料倉儲中使用 Transact-SQL 結構描述開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: dfb58956ad6637cf0f50b4c052ab98fb7c26139d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="f5033-103">SQL 資料倉儲中使用者定義的結構描述</span><span class="sxs-lookup"><span data-stu-id="f5033-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="f5033-104">傳統資料倉儲通常使用不同的資料庫，根據工作負載、網域或安全性來建立應用程式界限。</span><span class="sxs-lookup"><span data-stu-id="f5033-104">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="f5033-105">例如，傳統 SQL Server 資料倉儲可能包含臨時資料庫、資料倉儲資料庫和某些資料市集資料庫。</span><span class="sxs-lookup"><span data-stu-id="f5033-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="f5033-106">在此拓撲中，每個資料庫均作為架構中的工作負載和安全性界限運作。</span><span class="sxs-lookup"><span data-stu-id="f5033-106">In this topology each database operates as a workload and security boundary in the architecture.</span></span>

<span data-ttu-id="f5033-107">相反地，SQL 資料倉儲會在某個資料庫中執行整個資料倉儲工作負載。</span><span class="sxs-lookup"><span data-stu-id="f5033-107">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="f5033-108">不允許跨資料庫聯結。</span><span class="sxs-lookup"><span data-stu-id="f5033-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="f5033-109">因此，SQL 資料倉儲預期倉儲使用的所有資料表都會儲存在一個資料庫內。</span><span class="sxs-lookup"><span data-stu-id="f5033-109">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span></span>

> [!NOTE]
> <span data-ttu-id="f5033-110">SQL 資料倉儲不支援任何種類的跨資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="f5033-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="f5033-111">因此，需要修改運用此模式的資料倉儲實作。</span><span class="sxs-lookup"><span data-stu-id="f5033-111">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="f5033-112">建議</span><span class="sxs-lookup"><span data-stu-id="f5033-112">Recommendations</span></span>
<span data-ttu-id="f5033-113">以下是使用使用者定義的結構描述合併工作負載、安全性、網域和功能界限時的一些建議</span><span class="sxs-lookup"><span data-stu-id="f5033-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="f5033-114">使用 SQL 資料倉儲資料庫來執行整個資料倉儲工作負載</span><span class="sxs-lookup"><span data-stu-id="f5033-114">Use one SQL Data Warehouse database to run your entire data warehouse workload</span></span>
2. <span data-ttu-id="f5033-115">合併現有的資料倉儲環境，以使用一個 SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="f5033-115">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="f5033-116">運用 **使用者定義的結構描述** 來提供先前使用資料庫實作的界限。</span><span class="sxs-lookup"><span data-stu-id="f5033-116">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span></span>

<span data-ttu-id="f5033-117">如果先前尚未使用使用者定義的結構描述，您就沒有任何記錄。</span><span class="sxs-lookup"><span data-stu-id="f5033-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="f5033-118">只需使用舊資料庫名稱作為 SQL 資料倉儲資料庫中使用者定義之結構描述的基礎。</span><span class="sxs-lookup"><span data-stu-id="f5033-118">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span></span>

<span data-ttu-id="f5033-119">如果已經使用結構描述，您有下列幾個選項可用：</span><span class="sxs-lookup"><span data-stu-id="f5033-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="f5033-120">移除舊版結構描述名稱並重新開始</span><span class="sxs-lookup"><span data-stu-id="f5033-120">Remove the legacy schema names and start fresh</span></span>
2. <span data-ttu-id="f5033-121">在資料表名稱前面附加舊版結構描述名稱，以保留舊版結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="f5033-121">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span></span>
3. <span data-ttu-id="f5033-122">在額外結構描述中的資料表上實作檢視來重建舊的結構描述結構，以保留舊版結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="f5033-122">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="f5033-123">在第一次檢查時，選項 3 似乎像是最吸引人的選項。</span><span class="sxs-lookup"><span data-stu-id="f5033-123">On first inspection option 3 may seem like the most appealing option.</span></span> <span data-ttu-id="f5033-124">不過，魔鬼就在細節裡。</span><span class="sxs-lookup"><span data-stu-id="f5033-124">However, the devil is in the detail.</span></span> <span data-ttu-id="f5033-125">SQL 資料倉儲中的檢視為唯讀狀態。</span><span class="sxs-lookup"><span data-stu-id="f5033-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="f5033-126">必須對基底資料表執行任何的資料表或資料修改。</span><span class="sxs-lookup"><span data-stu-id="f5033-126">Any data or table modification would need to be performed against the base table.</span></span> <span data-ttu-id="f5033-127">選項 3 還在您的系統中引進了一個檢視層。</span><span class="sxs-lookup"><span data-stu-id="f5033-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="f5033-128">如果您已在架構中使用檢視，您可以再仔細思考一下這個選項。</span><span class="sxs-lookup"><span data-stu-id="f5033-128">You might want to give this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="f5033-129">範例：</span><span class="sxs-lookup"><span data-stu-id="f5033-129">Examples:</span></span>
<span data-ttu-id="f5033-130">根據資料庫名稱實作使用者定義的結構描述</span><span class="sxs-lookup"><span data-stu-id="f5033-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for the data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in the stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in the edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="f5033-131">在資料表名稱前面附加舊版結構描述名稱，以保留舊版結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="f5033-131">Retain legacy schema names by pre-pending them to the table name.</span></span> <span data-ttu-id="f5033-132">使用工作負載界限的結構描述。</span><span class="sxs-lookup"><span data-stu-id="f5033-132">Use schemas for the workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines the data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend the old schema name to the table and create in the staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend the old schema name to the table and create in the data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="f5033-133">使用檢視保留舊版結構描述名稱</span><span class="sxs-lookup"><span data-stu-id="f5033-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines the data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines the legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create the base staging tables in the staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create the base data warehouse tables in the data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in the legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="f5033-134">結構描述策略如有任何變更，則需要檢閱資料庫的資訊安全模型。</span><span class="sxs-lookup"><span data-stu-id="f5033-134">Any change in schema strategy needs a review of the security model for the database.</span></span> <span data-ttu-id="f5033-135">在許多情況下，您可以在結構描述層級指派權限，以簡化資訊安全模型。</span><span class="sxs-lookup"><span data-stu-id="f5033-135">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span></span> <span data-ttu-id="f5033-136">如果需要更細微的權限，您可以使用資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="f5033-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f5033-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5033-137">Next steps</span></span>
<span data-ttu-id="f5033-138">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="f5033-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
