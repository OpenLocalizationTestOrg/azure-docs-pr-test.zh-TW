---
title: "透明資料加密，為 Stretch Database TSQL Azure aaaEnable |Microsoft 文件"
description: "為 Azure TSQL 上的 SQL Server Stretch Database 啟用透明資料加密 (TDE)"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>為 Azure 上的 Stretch Database 啟用透明資料加密 (TDE) (Transact-SQL)
> [!div class="op_single_selector"]
> * [Azure 入口網站](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

透明資料加密 (TDE) 可協助防範惡意活動的 hello 威脅，藉由執行 hello 資料庫、 相關聯的備份和靜止的交易記錄檔的即時加密與解密，而不需要變更 toohello應用程式。

TDE 會使用對稱金鑰的呼叫的 hello 資料庫加密金鑰將整個資料庫的 hello 儲存體。 hello 資料庫加密金鑰受到由內建的伺服器憑證。 hello 內建伺服器憑證是唯一的每個 Azure 伺服器。 Microsoft 至少每 90 天會自動替換這些憑證。 如需 TDE 的一般描述，請參閱 [透明資料加密 (TDE)]。

## <a name="enabling-encryption"></a>啟用加密
正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫的 TDE tooenable hello 下列事項：

1. 連接 toohello*主要*hello Azure 伺服器主控 hello 資料庫上使用的登入是系統管理員或成員的 hello 資料庫**dbmanager** hello master 資料庫中的角色
2. 執行下列陳述式 tooencrypt hello 資料庫 hello。

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>停用加密
正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫的 TDE toodisable hello 下列事項：

1. 連接 toohello*主要*資料庫使用的登入是系統管理員或成員的 hello **dbmanager** hello master 資料庫中的角色
2. 執行下列陳述式 tooencrypt hello 資料庫 hello。

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>確認加密
正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫 tooverify 加密的狀態 hello 下列事項：

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

<!--Anchors-->
[透明資料加密 (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
