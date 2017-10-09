---
title: "aaaMigrate 您結構描述 tooSQL 資料倉儲 |Microsoft 文件"
description: "移轉您的結構描述 tooAzure SQL 資料倉儲來開發方案的提示。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a>移轉您的結構描述 tooSQL 資料倉儲
移轉您的 SQL 結構描述 tooSQL 資料倉儲的指引。 

## <a name="plan-your-schema-migration"></a>規劃結構描述移轉

當您規劃移轉時，請參閱 hello[資料表概觀][ table overview] toobecome 熟悉例如統計資料、 發佈、 分割和索引的資料表設計考量。  它也會列出一些[不支援的資料表功能][unsupported table features]和其因應措施。

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a>使用使用者定義的結構描述 tooconsolidate 資料庫

您現有的工作負載可能有多個資料庫。 例如，SQL Server 資料倉儲可能包含臨時資料庫、資料倉儲資料庫和某些資料超市資料庫。 在此拓撲中，每個資料庫都會搭配個別的安全性原則，以個別工作負載的形式執行。

相反地，SQL 資料倉儲執行某個資料庫中的 hello 整個資料倉儲工作負載。 不允許跨資料庫聯結。 因此，SQL 資料倉儲必須要有 hello hello 某個資料庫中儲存的資料倉儲 toobe 所使用的所有資料表。

我們建議使用使用者定義的結構描述 tooconsolidate 您現有的工作負載至一個資料庫。 如需範例，請參閱[使用者定義的結構描述](sql-data-warehouse-develop-user-defined-schemas.md)

## <a name="use-compatible-data-types"></a>使用相容的資料類型
修改您與 SQL 資料倉儲相容的資料型別 toobe。 如需所有支援和不支援資料類型的清單，請參閱[資料類型][data types]。 該主題提供解決 hello 不支援的型別。 它也提供查詢 tooidentify 不支援在 SQL 資料倉儲中的現有類型。

## <a name="minimize-row-size"></a>將資料列大小最小化
為了達到最佳效能，最小化 hello 的資料表的資料列長度。 較短的資料列長度會導致 toobetter 效能，因為使用 hello 最小資料類型可為您的資料。 

針對資料表的資料列寬度，PolyBase 具有 1 MB 的限制。  如果您打算 tooload 資料到含有 PolyBase 的 SQL 資料倉儲時，更新您的資料表 toohave 最大資料列的寬度小於 1 MB。 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a>指定 hello 散發選項
SQL 資料倉儲是一種分散式資料庫系統。 每個資料表散發，或在 hello 計算節點之間複寫。 沒有選項可讓您指定如何 toodistribute hello 資料的資料表。 hello 選項包括循環複寫，或雜湊散發。 各有其優缺點。 如果您未指定 hello 散發選項，SQL 資料倉儲會使用循環配置資源為 hello 預設值。

- Hello 預設循環配置資源。 它是最簡單 toouse hello，並載入 hello 資料盡快，但聯結需要移動資料的查詢效能會變慢。
- 複寫的儲存每個計算節點上的 hello 資料表的副本。 由於複寫資料表的聯結和彙總作業並不需要移動資料，所以很有效率。 相對的，它們需要額外的儲存體，因此比較適合較小的資料表使用。
- 分散式的雜湊會將 hello 資料列分散到所有的 hello 節點，透過雜湊函式。 分散式的雜湊表是 hello 核心 SQL 資料倉儲的因為它們是大型資料表上的設計的 tooprovide 高的查詢效能。 此選項需要一些規劃 tooselect hello 最佳資料行其中 toodistribute hello 資料。 不過，如果您沒有選擇最佳資料行 hello hello 第一次，您可以輕鬆地重新散發 hello 另一個資料行的資料。 

toochoose hello 最佳散發選項針對每個資料表，請參閱[分散式資料表](sql-data-warehouse-tables-distribute.md)。


## <a name="next-steps"></a>後續步驟
一旦您已成功移轉您的資料庫結構描述 tooSQL 資料倉儲，請繼續進行 tooone 的 hello 下列文章：

* [移轉資料][Migrate your data]
* [移轉程式碼][Migrate your code]

如需有關 SQL 資料倉儲的最佳作法，請參閱 hello[最佳做法][ best practices]發行項。

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
