---
title: "aaaAzure SQL 登入和使用者 |Microsoft 文件"
description: "深入了解有關 SQL Database 安全性管理，特別是如何 toomanage 資料庫存取與登入安全性透過 hello 伺服器層級主體帳戶。"
keywords: "sql 資料庫安全性, 資料庫安全性管理, 登入安全性, 資料庫安全性, 資料庫存取權"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>控制和授與資料庫存取權

當已設定防火牆規則時，人員可以連接 tooa SQL 資料庫，做為其中一個 hello 系統管理員帳戶、 hello 資料庫擁有者，或 hello 資料庫中的資料庫使用者。  

>  [!NOTE]  
>  本主題適用於 tooAzure SQL server 及 hello Azure SQL server 所建立的 tooboth SQL Database 和 SQL 資料倉儲資料庫。 為了簡單起見，tooboth SQL Database 和 SQL 資料倉儲時，就會使用 SQL Database。 
>

> [!TIP]
> 如需教學課程，請參閱[保護 Azure SQL Database](sql-database-security-tutorial.md)。
>


## <a name="unrestricted-administrative-accounts"></a>不受限制的系統管理帳戶
做為系統管理員的系統管理帳戶有兩個 (**伺服器管理員**和**Active Directory 管理員**)。 tooidentify SQL server，這些系統管理員帳戶開啟 hello Azure 入口網站，並瀏覽 SQL server toohello 屬性。

![SQL Server 系統管理員](./media/sql-database-manage-logins/sql-admins.png)

- **伺服器管理員**   
當您建立 Azure SQL server 時，您必須指定**伺服器管理員登入**。 SQL server 會建立該帳戶做為登入 hello master 資料庫中。 此帳戶會使用 SQL Server 驗證 (使用者名稱和密碼) 連接。 只有其中一個帳戶可以存在。   
- **Azure Active Directory 管理員**   
一個 Azure Active Directory 帳戶 (個人或安全性群組帳戶) 也可以設定為系統管理員。 選擇性 tooconfigure 為 Azure AD 系統管理員，但如果您想要 toouse Azure AD 帳戶 tooconnect tooSQL 資料庫必須設定 Azure AD 系統管理員。 如需有關如何設定 Azure Active Directory 存取的詳細資訊，請參閱[連接 tooSQL 資料庫或 SQL 資料倉儲使用 Azure Active Directory 驗證](sql-database-aad-authentication.md)和[SSMS 支援使用 SQL Azure AD MFA資料庫和 SQL 資料倉儲](sql-database-ssms-mfa-authentication.md)。
 

hello**伺服器管理員**和**Azure AD 管理員**帳戶具有下列特性的 hello:
- 這些是可以自動連線 hello 伺服器上的 SQL Database tooany hello 僅帳戶。 (tooconnect tooa 使用者資料庫，其他帳戶必須是 hello hello 擁有者資料庫，或在 hello 使用者資料庫中擁有使用者帳戶。)
- 這些帳戶輸入使用者資料庫作為 hello`dbo`使用者，而且它們有 hello 的所有權限 hello 使用者資料庫中。 (hello 使用者資料庫的擁有者也會進入 hello 資料庫成為 hello`dbo`使用者。) 
- 這些帳戶不會進入 hello`master`資料庫做為 hello`dbo`使用者，而且具有有限的權限在 master 中的。 
- 這些帳戶不是成員的 hello 標準的 SQL Server`sysadmin`固定的伺服器角色，但沒有 SQL 資料庫中。  
- 這些帳戶可以建立、改變和卸除 master 中的資料庫、登入、使用者，以及伺服器層級防火牆規則。
- 這些帳戶可以加入和移除成員 toohello`dbmanager`和`loginmanager`角色。
- 這些帳戶可以檢視 hello`sys.sql_logins`系統資料表。

### <a name="configuring-hello-firewall"></a>Hello 防火牆設定
當 hello 伺服器層級防火牆設定為個別的 IP 位址或範圍時，hello **SQL server 系統管理員**和 hello **Azure Active Directory 系統管理員**toohello master 資料庫和所有 hello 可連接使用者資料庫。 可以透過 hello 設定初始伺服器層級防火牆 hello [Azure 入口網站](sql-database-get-started-portal.md)，並使用[PowerShell](sql-database-get-started-powershell.md)或使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx)。 建立連線之後，也可以藉由使用 [Transact-SQL](sql-database-configure-firewall-settings.md) 來設定其他伺服器層級防火牆規則。

### <a name="administrator-access-path"></a>系統管理員存取路徑
當 hello 伺服器層級防火牆設定是否正確 hello **SQL server 系統管理員**和 hello **Azure Active Directory 系統管理員**可以使用 SQL Server Management Studio 或 SQL 之類的用戶端工具連接Server Data Tools。 Hello 最新工具提供所有 hello 特色與功能。 hello 下列圖表顯示 hello 的一般組態兩個系統管理員帳戶。

![系統管理員存取路徑](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

當使用 hello 伺服器層級防火牆中開啟的連接埠時，系統管理員可以連線 tooany SQL 資料庫。

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 連接 tooa 資料庫
如需建立伺服器、 資料庫、 伺服器層級防火牆規則和使用 SQL Server Management Studio tooquery 資料庫的逐步解說，請參閱[使用 hello Azure 入口網站開始使用 Azure SQL Database 伺服器、 資料庫和防火牆規則和 SQL Server Management Studio](sql-database-get-started-portal.md)。

> [!IMPORTANT]
> 建議您一律使用 hello 與更新 tooMicrosoft 同步處理最新版本的 Management Studio tooremain Azure 和 SQL Database。 [更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。


## <a name="additional-server-level-administrative-roles"></a>其他伺服器層級系統管理角色
此外 toohello 伺服器層級系統管理角色先前所討論，SQL Database 提供可加入 hello master 資料庫 toowhich 使用者帳戶中的兩個限制系統管理角色，授與權限 tooeither 建立資料庫，或管理登入。

### <a name="database-creators"></a>資料庫建立者
這些系統管理角色的其中一個是 hello **dbmanager**角色。 此角色的成員可以建立新的資料庫。 toouse 此角色，您建立使用者在 hello`master`資料庫，然後再加入 hello 使用者 toohello **dbmanager**資料庫角色。 toocreate 資料庫，hello 使用者必須是使用者根據 hello master 資料庫中的 SQL Server 登入或自主資料庫使用者，根據 Azure Active Directory 的使用者。

1. 使用系統管理員帳戶，連線 toohello master 資料庫。
2. 選擇性步驟： 建立 SQL Server 驗證登入，使用 hello [CREATE LOGIN](https://msdn.microsoft.com/library/ms189751.aspx)陳述式。 範例陳述式︰
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > 建立登入或自主資料庫使用者時，請使用強式密碼。 如需詳細資訊，請參閱 [增強式密碼](https://msdn.microsoft.com/library/ms161962.aspx)。
    
   tooimprove 效能 hello 資料庫層級會暫時快取登入 （伺服器層級主體）。 toorefresh hello 驗證快取，請參閱[DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx)。

3. Hello master 資料庫中，建立使用者使用 hello [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx)陳述式。 hello 使用者可以是 Azure Active Directory 驗證的自主資料庫使用者 （如果您已設定您的 Azure AD 驗證的環境），或 SQL Server 驗證自主資料庫使用者或 SQL 為基礎的 SQL Server 驗證使用者伺服器驗證登入 （建立 hello 上一個步驟中）。範例陳述式︰
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. 加入 hello 新使用者，toohello **dbmanager**資料庫角色使用 hello [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx)陳述式。 範例陳述式︰
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > hello dbmanager master 資料庫中是資料庫角色，好讓您只可以加入資料庫使用者 toohello dbmanager 角色。 您無法加入伺服器層級登入 toodatabase 層級角色。
    
5. 如有必要，設定防火牆規則 tooallow hello 新使用者 tooconnect。 （根據現有的防火牆規則可能會涵蓋 hello 新使用者）。

現在 hello 使用者可以連接 toohello master 資料庫，而且可以建立新的資料庫。 hello 帳戶建立 hello 資料庫會變成 hello hello 資料庫擁有者。

### <a name="login-managers"></a>登入管理員
hello 其他系統管理角色是 hello 登入管理員角色。 此角色的成員可以在 hello master 資料庫中建立新的登入。 如果您希望，您可以完成 hello 相同的步驟 (建立登入和使用者，並加入使用者 toohello **loginmanager**角色) tooenable 使用者 toocreate hello master 中的新登入。 通常不需要為 Microsoft 建議使用自主的資料庫使用者，在 hello 驗證資料庫層級而不是使用登入為基礎的使用者登入。 如需詳細資訊，請參閱 [自主資料庫使用者 - 讓資料庫具有可攜性](https://msdn.microsoft.com/library/ff929188.aspx)。

## <a name="non-administrator-users"></a>非系統管理員的使用者
一般而言，非系統管理員帳戶不需要存取 toohello master 資料庫。 建立自主的資料庫使用者在 hello 資料庫層級使用 hello [CREATE USER (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms173463.aspx)陳述式。 hello 使用者可以是 Azure Active Directory 驗證的自主資料庫使用者 （如果您已設定您的 Azure AD 驗證的環境），或 SQL Server 驗證自主資料庫使用者或 SQL 為基礎的 SQL Server 驗證使用者伺服器驗證登入 （建立 hello 上一個步驟中）。如需詳細資訊，請參閱 [自主資料庫使用者 - 讓資料庫具有可攜性](https://msdn.microsoft.com/library/ff929188.aspx)。 

toocreate 使用者連接 toohello 資料庫，並執行陳述式類似 toohello 遵循範例：

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

一開始，只有其中一個 hello 系統管理員或 hello hello 資料庫擁有者可以建立使用者。 tooauthorize 其他使用者 toocreate 新使用者，授與該選取的使用者 hello`ALTER ANY USER`權限，例如使用陳述式：

```
GRANT ALTER ANY USER tooMary;
```

toogive 其他使用者的 完全控制 hello 資料庫，使其成員的 hello **db_owner**固定的資料庫角色使用 hello`ALTER ROLE`陳述式。

> [!NOTE]
> hello 根據登入，最常見的原因 toocreate 資料庫使用者時，需要存取 toomultiple 資料庫的 SQL Server 驗證使用者。 登入為基礎的使用者會繫結的 toohello 登入，並只有一個維護為該登入的密碼。 在個別資料庫中的自主資料庫使用者是個別的實體，而且各個都會維護它自己的密碼。 如果它們不會維護各自的密碼相同，會造成自主資料庫使用者的混淆。

### <a name="configuring-hello-database-level-firewall"></a>Hello 資料庫層級防火牆設定
最佳做法，非管理員使用者應該只有透過 hello 防火牆 toohello 資料庫所使用的存取。 而不是授權其 IP 位址 hello 伺服器層級透過防火牆和存取 tooall 資料庫中給予他們使用 hello [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx)陳述式 tooconfigure hello 資料庫層級防火牆。 無法設定 hello 資料庫層級防火牆使用 hello 入口網站。

### <a name="non-administrator-access-path"></a>非系統管理員存取路徑
當 hello 資料庫層級防火牆設定正確，就可以使用用戶端工具，例如 SQL Server Management Studio 或 SQL Server Data Tools 連接 hello 資料庫使用者。 Hello 最新工具提供所有 hello 特色與功能。 hello 下列圖表顯示一般的非系統管理員存取路徑。

![非系統管理員存取路徑](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>群組和角色
能夠有效率地存取管理使用 toogroups 和而不是個別使用者的角色指派的權限。 

- 使用 Azure Active Directory 驗證時，將 Azure Active Directory 使用者放入 Azure Active Directory 群組中。 建立自主的資料庫使用者 hello 群組。 將放入一個或多個資料庫使用者[資料庫角色](https://msdn.microsoft.com/library/ms189121)然後指派[權限](https://msdn.microsoft.com/library/ms191291.aspx)toohello 資料庫角色。

- 使用 SQL Server 驗證時，請在 hello 資料庫中建立自主的資料庫使用者。 將放入一個或多個資料庫使用者[資料庫角色](https://msdn.microsoft.com/library/ms189121)然後指派[權限](https://msdn.microsoft.com/library/ms191291.aspx)toohello 資料庫角色。

hello 資料庫角色可以是 hello 內建的角色，例如**db_owner**， **db_ddladmin**， **db_datawriter**， **db_datareader**， **db_denydatawriter**，和**db_denydatareader**。 **db_owner**是常用的 toogrant 的完整權限 tooonly 少數使用者。 hello 其他固定的資料庫角色可用於取得簡單的資料庫開發中，快速，但不是建議針對大部分的實際執行資料庫。 例如，hello **db_datareader**固定的資料庫角色授與讀取權限 tooevery 資料表在 hello 資料庫中，通常是多個是絕對必要。 它是比較好的 toouse hello [CREATE ROLE](https://msdn.microsoft.com/library/ms187936.aspx)陳述式 toocreate 自己使用者定義資料庫角色，並仔細授與每個角色 hello hello 的商務需求所需的最低權限。 當使用者是多個角色的成員時，它們彙總全部 hello 權的限。

## <a name="permissions"></a>權限
有超過 100 個權限可在 SQL Database 中分別授與或拒絕。 這些權限有許多為巢狀。 例如，hello`UPDATE`結構描述上的權限會包含 hello`UPDATE`結構描述中的每個資料表的權限。 如同大部分的權限系統，hello 拒絕權限會覆寫 grant。 由於巢狀的 hello 本質與的權限的 hello 數目，可能需要仔細研究 toodesign 適當的權限系統 tooproperly 保護您的資料庫。 Hello 的權限清單的開頭[權限 (Database Engine)](https://msdn.microsoft.com/library/ms191291.aspx)並檢閱 hello[海報大小圖形](http://go.microsoft.com/fwlink/?LinkId=229142)hello 權限。


### <a name="considerations-and-restrictions"></a>考量和限制
當管理登入和 SQL 資料庫中的使用者，請考慮下列 hello:

* 您必須是連接的 toohello**主要**資料庫時執行 hello`CREATE/ALTER/DROP DATABASE`陳述式。   
* hello 資料庫使用者對應 toohello**伺服器管理員**無法改變或卸除登入。 
* 英文 （美國） 是 hello hello 預設語言**伺服器管理員**登入。
* 只有 hello 系統管理員 (**伺服器管理員**登入或 Azure AD 系統管理員) 和 hello hello 成員**dbmanager**資料庫角色中的 hello**主要**資料庫有權限 tooexecute hello`CREATE DATABASE`和`DROP DATABASE`陳述式。
* 您必須連接的 toohello master 資料庫執行 hello 時`CREATE/ALTER/DROP LOGIN`陳述式。 不過，不建議使用登入。 請改為使用自主資料庫使用者。
* tooconnect tooa 使用者資料庫中，您必須提供 hello hello 連接字串中的 hello 資料庫名稱。
* 只有 hello 伺服器層級主體登入和 hello 成員 hello **loginmanager**資料庫角色中 hello**主要**資料庫擁有權限 tooexecute hello `CREATE LOGIN`， `ALTER LOGIN`，和`DROP LOGIN`陳述式。
* 當執行 hello`CREATE/ALTER/DROP LOGIN`和`CREATE/ALTER/DROP DATABASE`ADO.NET 應用程式中的陳述式，不允許使用參數化的命令。 如需詳細資訊，請參閱 [命令和參數](https://msdn.microsoft.com/library/ms254953.aspx)。
* 當執行 hello`CREATE/ALTER/DROP DATABASE`和`CREATE/ALTER/DROP LOGIN`陳述式，每個這些陳述式必須是 hello TRANSACT-SQL 批次中的陳述式。 否則便會發生錯誤。 例如，hello 下列 TRANSACT-SQL 會檢查 hello 資料庫是否存在。 如果存在的話， `DROP DATABASE` tooremove hello 資料庫呼叫陳述式。 因為 hello`DROP DATABASE`陳述式不是唯一的陳述式 hello hello 批次中，執行 hello 下列 TRANSACT-SQL 陳述式會導致錯誤。

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* 當執行 hello`CREATE USER`陳述式以 hello`FOR/FROM LOGIN`選項，它必須是 hello TRANSACT-SQL 批次中的陳述式。
* 當執行 hello`ALTER USER`陳述式以 hello`WITH LOGIN`選項，它必須是 hello TRANSACT-SQL 批次中的陳述式。
* 太`CREATE/ALTER/DROP`使用者必須擁有 hello `ALTER ANY USER` hello 資料庫的權限。
* 當資料庫角色的 hello 擁有者嘗試 tooadd] 或 [移除其他資料庫使用者 tooor 從該資料庫角色時，可能會發生 hello 下列錯誤：**使用者或角色 'Name' 不存在於此資料庫。** 因為 hello 使用者不可見的 toohello 擁有者，就會發生此錯誤。 tooresolve 這個問題，請授與 hello 角色擁有者 hello `VIEW DEFINITION` hello 使用者權限。 


## <a name="next-steps"></a>後續步驟

- toolearn 進一步了解防火牆規則，請參閱[Azure SQL Database 防火牆](sql-database-firewall-configure.md)。
- 如需所有 hello SQL Database 安全性功能的概觀，請參閱[SQL 安全性概觀](sql-database-security-overview.md)。
- 如需教學課程，請參閱[保護 Azure SQL Database](sql-database-security-tutorial.md)。
- 如需檢視和預存程序的相關資訊，請參閱[建立檢視和預存程序](https://msdn.microsoft.com/library/ms365311.aspx)
- 如需授與存取 tooa 資料庫物件資訊，請參閱[授與存取 tooa 資料庫物件](https://msdn.microsoft.com/library/ms365327.aspx)
