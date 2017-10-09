---
title: "Azure SQL database aaaCopy |Microsoft 文件"
description: "建立 Azure SQL Database 的複本"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>複製 Azure SQL Database

Azure SQL Database 提供數種方法來建立交易一致的複本的現有的 Azure SQL 資料庫上任一 hello 相同伺服器或不同的伺服器。 您可以使用 hello Azure 入口網站、 PowerShell 或 T-SQL 複製 SQL database。 

## <a name="overview"></a>概觀

資料庫複本是 hello hello 的 hello 複製要求的時間為準的來源資料庫的快照集。 您可以選取相同的伺服器或另一部伺服器、 其服務層和效能層級或不同的效能層級內 hello hello 相同服務層 （版本）。 Hello 複製程序完成之後，它會變成完全正常運作且獨立的資料庫。 此時，您可以升級或降級 tooany 版本。 hello 登入、 使用者和權限可以分開管理。  

## <a name="logins-in-hello-database-copy"></a>Hello 資料庫副本中的登入

當您複製資料庫 toohello 相同邏輯伺服器，可以使用相同的登入，這兩個資料庫的 hello。 hello 安全性主體使用 toocopy hello 資料庫變成 hello hello 新資料庫上的資料庫擁有者。 所有資料庫使用者、 其權限，以及它們的安全性識別碼 (Sid) 被複製 toohello 資料庫副本。  

當您複製資料庫 tooa 不同的邏輯伺服器時，hello 安全性主體 hello 新的伺服器上會變成 hello hello 新資料庫上的資料庫擁有者。 如果您使用[自主資料庫使用者](sql-database-manage-logins.md)資料存取，請確定兩者 hello 主要，以及次要資料庫一律會有相同的使用者認證，因此，hello 複製完成後您可以立即存取的 hello 與 hello 相同認證。 

如果您使用[Azure Active Directory](../active-directory/active-directory-whatis.md)，您可以完全排除 hello 需要管理 hello 複本中的認證。 不過，當您複製 hello 資料庫 tooa 新伺服器，hello 登入為基礎的存取可能無法運作，因為 hello 登入不存在 hello 新的伺服器上。 toolearn 有關管理登入，當您複製資料庫 tooa 不同的邏輯伺服器，請參閱[toomanage Azure SQL 資料庫安全性之後嚴重損壞修復](sql-database-geo-replication-security-config.md)。 

Hello 複製成功之後，會重新對應其他使用者之前，只有 hello 起始登入複製的 hello hello 資料庫擁有者，可以登入 toohello 新資料庫。 tooresolve 登入之後 hello 複製作業已完成，請參閱[解決登入](#resolve-logins)。

## <a name="copy-a-database-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站中複製資料庫

使用資料庫 hello Azure 入口網站，為您的資料庫中，開啟 hello 頁面，然後按一下的 toocopy**複製**。 

   ![資料庫複本](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>使用 PowerShell 來複製資料庫

使用 PowerShell，使用 hello 資料庫 toocopy[新增 AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet。 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

如需完整的範例指令碼，請參閱[複製 tooa 新資料庫的伺服器](scripts/sql-database-copy-database-to-new-server-powershell.md)。

## <a name="copy-a-database-by-using-transact-sql"></a>使用 Transact-SQL 來複製資料庫

登入 toohello master 資料庫與 hello 伺服器層級主體登入或建立您想要 toocopy hello 資料庫 hello 登入。 資料庫複製 toosucceed，不是 hello 伺服器層級主體登入必須 hello dbmanager 角色的成員。 如需登入和連線 toohello 伺服器的詳細資訊，請參閱[管理登入](sql-database-manage-logins.md)。

開始複製 hello 來源資料庫與 hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx)陳述式。 執行這個陳述式會起始 hello 資料庫複製程序。 複製資料庫是非同步程序，因為 hello CREATE DATABASE 陳述式會傳回前 hello 資料庫複製便已完成。

### <a name="copy-a-sql-database-toohello-same-server"></a>複製 SQL 資料庫 toohello 相同的伺服器
登入 toohello master 資料庫與 hello 伺服器層級主體登入或建立您想要 toocopy hello 資料庫 hello 登入。 資料庫複製 toosucceed，不是 hello 伺服器層級主體登入必須 hello dbmanager 角色的成員。

此命令會將複製 hello 上名為 Database2 Database1 tooa 新資料庫相同的伺服器。 根據資料庫的 hello 大小，hello 複製作業可能需要一些時間 toocomplete。

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>複製 SQL database tooa 不同伺服器

登入 toohello master hello 目的地伺服器 hello 新資料庫所在 toobe 建立 hello SQL 資料庫伺服器的資料庫。 使用具有相同名稱和密碼 hello hello hello hello 來源 SQL 資料庫伺服器上的來源資料庫的資料庫擁有者的登入。 hello hello 目的地伺服器上的登入也必須是 hello dbmanager 角色的成員，或者是 hello 伺服器層級主體登入。

這個命令會將 Database1 server2 上名為 Database2 server1 tooa 新資料庫上。 根據資料庫的 hello 大小，hello 複製作業可能需要一些時間 toocomplete。

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>監視複製作業的 hello hello 進度

監視複製程序 hello hello sys.databases 和 sys.dm_database_copies 檢視進行查詢。 Hello 複製正在進行時，hello **state_desc** hello 新資料庫的 hello sys.databases 檢視資料行設定得**複製**。

* 如果 hello 複製失敗，hello **state_desc** hello 新資料庫的 hello sys.databases 檢視資料行設定得**懷疑**。 Hello 新的資料庫上執行 hello DROP 陳述式，並再試一次。
* 如果 hello 複製成功，hello **state_desc** hello 新資料庫的 hello sys.databases 檢視資料行設定得**線上**。 hello 複製已完成，且 hello 新的資料庫是可以變更不會影響 hello 來源資料庫的一般資料庫。

> [!NOTE]
> 如果您決定 toocancel hello 複製正在進行時，執行 hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) hello 新資料庫上的陳述式。 或者，在 hello 來源資料庫上執行 hello DROP DATABASE 陳述式也會取消複製程序的 hello。
> 

## <a name="resolve-logins"></a>解析登入

Hello 新資料庫在線上 hello 目的地伺服器上之後，請使用 hello [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) hello 陳述式 tooremap hello 使用者新資料庫 toologins hello 目的地伺服器上的。 tooresolve 被遺棄使用者，請參閱[被遺棄使用者疑難排解](https://msdn.microsoft.com/library/ms175475.aspx)。 另請參閱[toomanage Azure SQL 資料庫安全性之後嚴重損壞修復](sql-database-geo-replication-security-config.md)。

Hello 新資料庫中的所有使用者都保有 hello 來源資料庫中的 hello 權限。 起始 hello 資料庫副本的 hello 使用者成為 hello hello 新資料庫的資料庫擁有者，並指派新的安全性識別碼 (SID)。 Hello 複製成功之後，會重新對應其他使用者之前，只有 hello 起始登入複製的 hello hello 資料庫擁有者，可以登入 toohello 新資料庫。

toolearn 有關管理使用者與登入，當您複製資料庫 tooa 不同的邏輯伺服器，請參閱[toomanage Azure SQL 資料庫安全性之後嚴重損壞修復](sql-database-geo-replication-security-config.md)。

## <a name="next-steps"></a>後續步驟

* 如需登入資訊，請參閱[管理登入](sql-database-manage-logins.md)和[toomanage Azure SQL 資料庫安全性之後嚴重損壞修復](sql-database-geo-replication-security-config.md)。
* tooexport 資料庫，請參閱[匯出 hello 資料庫 tooa BACPAC](sql-database-export.md)。
