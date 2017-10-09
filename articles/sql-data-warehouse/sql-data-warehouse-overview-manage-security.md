---
title: "aaaSecure SQL 資料倉儲中的資料庫 |Microsoft 文件"
description: "保護 Azure SQL 資料倉儲中的資料庫以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>保護 SQL 資料倉儲中的資料庫
> [!div class="op_single_selector"]
> * [安全性概觀](sql-data-warehouse-overview-manage-security.md)
> * [驗證](sql-data-warehouse-authentication.md)
> * [加密 (入口網站)](sql-data-warehouse-encryption-tde.md)
> * [加密 (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

本文逐步 hello 的保護您的 Azure SQL 資料倉儲資料庫的基本概念。 本文尤其著重於協助您開始利用資源，在資料庫上限制存取、保護資料，以及監視活動。

## <a name="connection-security"></a>連接安全性
連線安全性是指的 toohow 您限制及保護 tooyour 資料庫的連接使用防火牆規則和連線加密。

防火牆規則會使用兩個 hello 伺服器與 hello 資料庫 tooreject 連線嘗試從尚未明確允許的 IP 位址。 從您的應用程式或用戶端電腦的公用 IP 位址的 tooallow 連線，您必須先建立 hello Azure 入口網站、 REST API 或 PowerShell，使用的伺服器層級防火牆規則。 最佳做法，您應該限制 hello 盡可能透過您伺服器的防火牆允許的 IP 位址範圍。  tooaccess Azure SQL 資料倉儲從本機電腦，請確定 hello 網路和本機電腦上的防火牆允許 TCP 通訊埠 1433年上的傳出通訊。  如需詳細資訊，請參閱 [Azure SQL Database 防火牆][Azure SQL Database firewall]、[sp_set_firewall_rule][sp_set_firewall_rule] 和 [sp_set_database_firewall_rule][sp_set_database_firewall_rule]。

依預設會加密連接 tooyour SQL 資料倉儲。  修改連線設定 toodisable 加密會被忽略。

## <a name="authentication"></a>驗證
驗證是指 toohow 連接 toohello 資料庫時，證明您的身分識別。 SQL 資料倉儲目前支援使用使用者名稱和密碼的 SQL Server 驗證，以及 Azure Active Directory。 

當您為您的資料庫建立 hello 邏輯伺服器時，您可以指定 「 伺服器管理員 」 的登入使用者名稱和密碼。 您可以使用這些認證，驗證 tooany hello 資料庫擁有者或透過 SQL Server 驗證的"dbo"與該伺服器上的資料庫。

不過，最佳做法，貴組織的使用者應該使用不同的帳戶 tooauthenticate。 如此一來您可以限制 hello 權限授與 toohello 應用程式，並減少惡意活動的 hello 風險，應用程式程式碼是很容易遭受 tooa SQL 資料隱碼攻擊。 

SQL Server 驗證使用者，toocreate 連接 toohello**主要**與伺服器的系統管理員登入您伺服器上的資料庫，並建立新的伺服器登入。  此外，也會建議 toocreate 使用者的 Azure SQL 資料倉儲使用者 hello master 資料庫中。 在 master 中建立使用者，可讓使用者 toologin 使用 SSMS 等工具，而不指定資料庫名稱。  它也可讓它們 toouse hello 物件總管 中 tooview SQL server 的所有資料庫。

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

然後，連接 tooyour **SQL 資料倉儲資料庫**與伺服器的系統管理員登入並建立根據 hello 伺服器登入您剛才建立的資料庫使用者。

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

如果使用者將會執行其他作業，例如建立登入或建立新的資料庫，他們也需要指派 toobe toohello`Loginmanager`和`dbmanager`hello master 資料庫中的角色。 如需有關這些其他角色和驗證 tooa SQL 資料庫的詳細資訊，請參閱[管理資料庫和 Azure SQL Database 中的登入][Managing databases and logins in Azure SQL Database]。  如需有關 SQL 資料倉儲的 Azure AD 的詳細資訊，請參閱[連接 tooSQL 資料倉儲使用 Azure Active Directory 驗證][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]。

## <a name="authorization"></a>Authorization
授權是指 toowhat，您可以在 Azure SQL 資料倉儲資料庫，以及這由使用者帳戶的角色成員資格和權限。 最佳做法，您應該授與使用者 hello 最低必要權限。 Azure SQL 資料倉儲會讓角色與此簡單 toomanage T-SQL 中：

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

hello 您所連接的伺服器系統管理員帳戶是具有授權 toodo hello 資料庫內的任何項目 db_owner 的成員。 請儲存此帳戶，以便部署結構描述升級及其他管理作業。 使用具有更多限制的權限 tooconnect 從您的應用程式 toohello 資料庫以 hello hello"ApplicationUser"帳戶應用程式所需的最低權限。

有方法 toofurther 限制使用者可以使用 Azure SQL Database:

* 細微[權限][ Permissions]可讓您控制哪些作業，您可以執行個別的資料行、 資料表、 檢視、 程序和其他 hello 資料庫中的物件。 使用細微的權限 toohave hello 最佳控制權，並授與 hello 最低必要權限。 hello 細微權限系統稍微複雜，所以需要某些研究 toouse 有效。
* [資料庫角色][ Database roles]以外 db_datareader 和 db_datawriter 可以是使用的 toocreate 功能更強大的應用程式使用者帳戶或較不強大的管理帳戶。 hello 內建的固定的資料庫角色提供簡單的方式 toogrant 權限，但可能會導致授與超出所需的權限。
* [預存程序][ Stored procedures]可以是使用的 toolimit 可以 hello 資料庫製作的 hello 動作。

從 hello Azure 傳統入口網站管理資料庫和邏輯伺服器，或使用 hello Azure 資源管理員 API 是由您的入口網站的使用者帳戶的角色指派控制。 如需有關此主題的詳細資訊，請參閱 [Azure 入口網站中的角色型存取控制][Role-based access control in Azure Portal]。

## <a name="encryption"></a>加密
Azure SQL 資料倉儲透明資料加密 (TDE) 可協助防範惡意活動的 hello 威脅所執行的即時加密與解密的靜止資料。  當您加密您的資料庫時，相關聯的備份和交易記錄檔會加密而不需要任何變更 tooyour 應用程式。 TDE 會使用對稱金鑰的呼叫的 hello 資料庫加密金鑰將整個資料庫的 hello 儲存體。 SQL Database 中 hello 資料庫加密金鑰受到由內建的伺服器憑證。 hello 內建伺服器憑證是唯一的每個 SQL Database 伺服器。 Microsoft 至少每 90 天會自動替換這些憑證。 SQL 資料倉儲所使用的 hello 加密演算法是 AES 256。 如需 TDE 的一般描述，請參閱[透明資料加密][Transparent Data Encryption]。

您可以使用加密資料庫 hello [Azure 入口網站][ Encryption with Portal]或[T-SQL][Encryption with TSQL]。

## <a name="next-steps"></a>後續步驟
如需詳細資訊和 tooyour SQL 資料倉儲連接不同的通訊協定的範例，請參閱[連接 tooSQL 資料倉儲][Connect tooSQL Data Warehouse]。

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
