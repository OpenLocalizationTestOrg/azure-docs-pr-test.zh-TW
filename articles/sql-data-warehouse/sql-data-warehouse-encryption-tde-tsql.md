---
title: "SQL 資料倉儲 (T-SQL) 中的資料加密 aaaTransparent |Microsoft 文件"
description: "SQL 資料倉儲中的透明資料加密 (TDE) (T-SQL)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a>開始使用透明資料加密 (TDE)
> [!div class="op_single_selector"]
> * [安全性概觀](sql-data-warehouse-overview-manage-security.md)
> * [驗證](sql-data-warehouse-authentication.md)
> * [加密 (入口網站)](sql-data-warehouse-encryption-tde.md)
> * [加密 (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>需要的權限
tooenable 透明資料加密 (TDE)，您必須是系統管理員或 hello dbmanager 角色的成員。

## <a name="enabling-encryption"></a>啟用加密
SQL 資料倉儲，請遵循這些步驟 tooenable TDE:

1. 連接 toohello*主要*裝載 hello 資料庫使用的登入是系統管理員或成員的 hello 的 hello 伺服器上的資料庫**dbmanager** hello master 資料庫中的角色
2. 執行下列陳述式 tooencrypt hello 資料庫 hello。

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>停用加密
SQL 資料倉儲，請遵循這些步驟 toodisable TDE:

1. 連接 toohello*主要*資料庫使用的登入是系統管理員或成員的 hello **dbmanager** hello master 資料庫中的角色
2. 執行下列陳述式 tooencrypt hello 資料庫 hello。

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> Toohello TDE 設定進行變更之前，必須繼續暫停的 SQL 資料倉儲。
> 
> 

## <a name="verifying-encryption"></a>確認加密
SQL 資料倉儲，tooverify 加密的狀態，請遵循下列 hello 步驟：

1. 連接 toohello*主要*或執行個體資料庫使用的登入是系統管理員或成員的 hello **dbmanager** hello master 資料庫中的角色
2. 執行下列陳述式 tooencrypt hello 資料庫 hello。

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

```1``` 的結果表示加密的資料庫，```0``` 表示未加密的資料庫。

## <a name="encryption-dmvs"></a>加密 DMV
* [sys.databases][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
