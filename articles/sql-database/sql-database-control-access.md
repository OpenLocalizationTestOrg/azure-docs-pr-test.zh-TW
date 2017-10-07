---
title: "aaaGranting 存取 tooAzure SQL 資料庫 |Microsoft 文件"
description: "深入了解授與存取 tooMicrosoft Azure SQL Database。"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Azure SQL Database 存取控制
tooprovide 安全性，SQL Database 與防火牆規則，以限制連線 IP 位址驗證機制需要使用者 tooprove 控制存取他們的身分識別和授權機制限制使用者 toospecific 動作和資料。 

> [!IMPORTANT]
> 如需 hello SQL Database 安全性功能的概觀，請參閱[SQL 安全性概觀](sql-database-security-overview.md)。 如需教學課程，請參閱[保護 Azure SQL Database](sql-database-security-tutorial.md)。

## <a name="firewall-and-firewall-rules"></a>防火牆與防火牆規則
Microsoft Azure SQL Database 為 Azure 和其他網際網路式應用程式提供關聯式資料庫服務。 toohelp 保護您的資料，防火牆會阻止所有存取 tooyour 資料庫伺服器，直到您指定哪些電腦有權限。 hello 防火牆會授與存取 toodatabases hello 來自每個要求的 IP 位址為基礎。 如需詳細資訊，請參閱 [Azure SQL Database 防火牆規則概觀](sql-database-firewall-configure.md)

hello Azure SQL Database 服務僅透過 TCP 通訊埠 1433年提供。 tooaccess SQL 資料庫，從您的電腦，請確定您的用戶端電腦防火牆允許 TCP 通訊埠 1433年上的傳出 TCP 通訊。 如果其他應用程式不需要，請封鎖 TCP 通訊埠 1433 的傳入連線。 

Hello 連線程序的一部分，從 Azure 虛擬機器的連線會重新導向的 tooa 不同的 IP 位址和連接埠，唯一的每個工作者角色。 hello 連接埠號碼是在 11000 too11999 hello 範圍。 如需 TCP 連接埠的詳細資訊，請參閱[適用於 ADO.NET 4.5 及 SQL Database 的 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)。

## <a name="authentication"></a>驗證

SQL Database 支援兩種驗證類型：

* **SQL 驗證**，其需要使用者名稱和密碼。 當您為您的資料庫建立 hello 邏輯伺服器時，您可以指定 「 伺服器管理員 」 的登入使用者名稱和密碼。 使用這些認證時，您可以驗證 tooany 為 hello 資料庫擁有者或"dbo"。 該伺服器上的資料庫 
* **Azure Active Directory 驗證**，它會使用由 Azure Active Directory 管理的身分識別，並支援受管理和整合的網域。 [盡可能](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode)使用 Active Directory 驗證 (整合式安全性)。 如果您想 toouse Azure Active Directory 驗證時，您必須建立另一個伺服器系統管理員稱為 hello"Azure AD admin"，這允許 tooadminister Azure AD 使用者和群組。 此管理員也可以執行一般伺服器管理員可執行的所有作業。 請參閱[連接 tooSQL 資料庫使用 Azure Active Directory 驗證](sql-database-aad-authentication.md)方式的逐步解說 toocreate Azure AD 管理員 tooenable Azure Active Directory 驗證。

hello Database Engine 關閉連接閒置超過 30 分鐘。 hello 連線一次必須登入，才能使用。 作用中連線 tooSQL 資料庫需要重新授權 （hello database engine 所執行） 的持續至少每隔 10 小時。 hello 資料庫引擎會嘗試重新授權使用 hello 最初提交的密碼並不需要使用者輸入。 基於效能考量，密碼重設 SQL Database 中時 hello 連接不是重新驗證，即使 hello 重設連接因為 tooconnection 共用。 這點不同於在內部部署 SQL Server hello 行為。 如果之後 hello 連接一開始授權 hello 密碼已經變更，必須終止 hello 連線，並使用 hello 新密碼建立新的連接。 使用者以 hello`KILL DATABASE CONNECTION`權限可以明確地結束連接 tooSQL 資料庫使用 hello [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql)命令。

使用者帳戶可建立 hello master 資料庫中，可以在 hello 伺服器上所有資料庫的權限授與或也可以建立在 hello 資料庫本身 （稱為包含的使用者）。 如需建立和管理登入的資訊，請參閱[管理登入](sql-database-manage-logins.md)。 tooenhance 可攜性和 scalabilty，使用自主的資料庫使用者 tooenhance 延展性。 如需自主使用者的詳細資訊，請參閱[自主的資料庫使用者 - 使資料庫可攜](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable)、[CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) 及[自主資料庫](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases)。

最佳作法是您的應用程式應該使用的專用的帳戶 tooauthenticate-如此一來，您可以限制 hello 權限授與 toohello 應用程式，並減少惡意活動的 hello 風險，應用程式程式碼是很容易遭受 tooa SQL 資料隱碼攻擊。 hello 建議的作法是 toocreate[自主的資料庫使用者](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable)，可讓您的應用程式 tooauthenticate 直接 toohello 資料庫。 

## <a name="authorization"></a>Authorization

授權是指 toowhat 使用者可以在 Azure SQL Database 中執行，這由您的使用者帳戶資料庫[角色成員資格](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles)和[物件層級權限](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine)。 最佳做法，您應該授與使用者 hello 最低必要權限。 hello 您所連接的伺服器系統管理員帳戶是具有授權 toodo hello 資料庫內的任何項目 db_owner 的成員。 請儲存此帳戶，以便部署結構描述升級及其他管理作業。 使用具有更多限制的權限 tooconnect 從您的應用程式 toohello 資料庫以 hello hello"ApplicationUser"帳戶應用程式所需的最低權限。 如需詳細資訊，請參閱[管理登入](sql-database-manage-logins.md)。

通常，只有系統管理員需要存取 toohello`master`資料庫。 透過建立每個資料庫中的非系統管理員的自主的資料庫使用者應該常式存取 tooeach 使用者資料庫。 當您使用自主的資料庫使用者時，您不需要在 hello toocreate 登入`master`資料庫。 如需詳細資訊，請參閱 [自主資料庫使用者 - 讓資料庫具有可攜性](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable)。

您應該熟悉下列功能，可使用的 toolimit 或提高權限的 hello:   
* [模擬](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server)和[模組簽署](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server)可以是使用的 toosecurely 將提高權限暫時。
* [資料列層級安全性](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) 可用於使用者可存取資料列的限制。
* [資料遮罩](sql-database-dynamic-data-masking-get-started.md)可以是使用的 toolimit 公開機密資料。
* [預存程序](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine)可以是使用的 toolimit 可以 hello 資料庫製作的 hello 動作。

## <a name="next-steps"></a>後續步驟

- 如需 hello SQL Database 安全性功能的概觀，請參閱[SQL 安全性概觀](sql-database-security-overview.md)。
- toolearn 進一步了解防火牆規則，請參閱[防火牆規則](sql-database-firewall-configure.md)。
- toolearn 有關使用者和登入，請參閱[管理登入](sql-database-manage-logins.md)。 
- 關於主動式監視的討論，請參閱[資料庫稽核](sql-database-auditing.md)和 [SQL Database 威脅偵測](sql-database-threat-detection.md)。
- 如需教學課程，請參閱[保護 Azure SQL Database](sql-database-security-tutorial.md)。
