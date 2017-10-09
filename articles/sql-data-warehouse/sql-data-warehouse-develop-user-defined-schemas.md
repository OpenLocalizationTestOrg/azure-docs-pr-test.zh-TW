---
title: "aaaUser 定義 SQL 資料倉儲中的結構描述 |Microsoft 文件"
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
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>SQL 資料倉儲中使用者定義的結構描述
傳統資料倉儲工作負載、 網域或安全性基礎通常使用不同的資料庫 toocreate 應用程式界限。 例如，傳統 SQL Server 資料倉儲可能包含臨時資料庫、資料倉儲資料庫和某些資料市集資料庫。 在此拓撲中每個資料庫會作為工作負載和 hello 架構中的安全性界限運作。

相反地，SQL 資料倉儲執行某個資料庫中的 hello 整個資料倉儲工作負載。 不允許跨資料庫聯結。 因此 SQL 資料倉儲必須要有儲存 hello 某個資料庫中的 hello 倉儲 toobe 所使用的所有資料表。

> [!NOTE]
> SQL 資料倉儲不支援任何種類的跨資料庫查詢。 因此，利用這種模式的資料倉儲實作需要 toobe 修訂。
> 
> 

## <a name="recommendations"></a>建議
以下是使用使用者定義的結構描述合併工作負載、安全性、網域和功能界限時的一些建議

1. 使用一個 SQL 資料倉儲資料庫 toorun 您整個資料倉儲工作負載
2. 合併現有資料倉儲環境 toouse 一個 SQL 資料倉儲資料庫
3. 運用**使用者定義的結構描述**tooprovide hello 界限先前使用資料庫來實作。

如果先前尚未使用使用者定義的結構描述，您就沒有任何記錄。 只要使用 hello 舊的資料庫名稱作為 hello 基礎您 hello SQL 資料倉儲資料庫中使用者定義的結構描述。

如果已經使用結構描述，您有下列幾個選項可用：

1. 移除 hello 舊版結構描述名稱，然後重新開始
2. 保留 hello 舊版結構描述名稱，以預先暫止 hello 舊版結構描述名稱 toohello 資料表名稱
3. 藉由實作額外的結構描述 toore 中的 hello 資料表檢視中保留 hello 舊版結構描述名稱-建立 hello 舊的結構描述結構。

> [!NOTE]
> 在第一個檢查選項 3 看起來好像 hello 最具吸引力的選項。 不過，hello 捲風處於 hello 詳細資料。 SQL 資料倉儲中的檢視為唯讀狀態。 任何資料或資料表的修改需要 toobe 針對 hello 基底資料表執行。 選項 3 還在您的系統中引進了一個檢視層。 如果您使用您的架構中檢視已您可能想指定 toogive 這個部分的其他想法。
> 
> 

### <a name="examples"></a>範例：
根據資料庫名稱實作使用者定義的結構描述

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

保留舊版的結構描述名稱所預先暫止它們 toohello 資料表名稱。 使用結構描述 hello 工作負載的界限。

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

使用檢視保留舊版結構描述名稱

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> 結構描述策略中的任何變更需要 hello 資料庫建立 hello 安全性模型的檢閱。 在許多情況下您可能無法 toosimplify hello 安全性模型在 hello 結構描述層級的權限指派。 如果需要更細微的權限，您可以使用資料庫角色。
> 
> 

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱[開發概觀][development overview]。

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
