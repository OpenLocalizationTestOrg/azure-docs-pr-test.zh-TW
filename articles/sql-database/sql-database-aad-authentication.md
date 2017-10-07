---
title: "aaaAzure Active Directory 驗證 Azure SQL （概觀） |Microsoft 文件"
description: "深入了解如何 toouse Azure Active Directory 驗證的 SQL Database 和 SQL 資料倉儲"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>利用 SQL Database 和 SQL 資料倉儲使用 Azure Active Directory 驗證來驗證
Azure Active Directory 驗證是一項機制的連接 tooMicrosoft Azure SQL Database 和[SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)使用 Azure Active Directory (Azure AD) 中的身分識別。 使用 Azure AD 驗證時，您可以集中管理 hello 的資料庫使用者的身分識別和其他 Microsoft 服務在單一中央位置。 中央識別碼管理 toomanage 資料庫使用者提供單一位置，並簡化權限管理。 優點 hello 如下：

* 它提供替代 tooSQL 伺服器驗證。
* 可協助停止使用者身分識別的 hello 的擴散到資料庫伺服器。
* 允許在單一位置的密碼替換
* 客戶可以管理使用外部 (AAD) 群組的資料庫權限。
* 它可以藉由啟用整合式 Windows 驗證和 Azure Active Directory 支援的其他形式驗證來避免儲存密碼。
* Azure AD 驗證在 hello 資料庫層級，使用自主的資料庫使用者 tooauthenticate 身分識別。
* Azure AD 支援連接 tooSQL 資料庫應用程式的權杖為基礎的驗證。
* Azure AD 驗證本機 Azure Active Directory 的 ADFS (網域同盟) 或原生使用者/密碼驗證，而不需進行網域同步處理。  
* Azure AD 支援來自 SQL Server Management Studio 的連線，其中使用包含 Multi-Factor Authentication (MFA) 的 Active Directory 通用驗證。  MFA 包含增強式驗證功能，其中提供一系列簡易的驗證選項，例如電話、簡訊、含有 PIN 的智慧卡或行動應用程式通知。 如需詳細資訊，請參閱 [適用於與 SQL Database 和 SQL 資料倉儲搭配使用之 Azure AD MFA 的 SSMS 支援](sql-database-ssms-mfa-authentication.md)。  

>  [!NOTE]  
>  連接的 tooSQL Azure VM 上執行的伺服器不支援使用 Azure Active Directory 帳戶。 請改用 Active Directory 網域帳戶。  

hello 組態步驟包含下列程序 tooconfigure hello，並使用 Azure Active Directory 驗證。

1. 建立和填入 Azure AD。
2. 選擇性： 產生關聯，或變更 hello 目前與 Azure 訂用帳戶相關聯的 active directory。
3. 建立 Azure SQL 伺服器或 [Azure SQL 資料倉儲](https://azure.microsoft.com/services/sql-data-warehouse/)的 Azure Active Directory 系統管理員。
4. 設定用戶端電腦。
5. 在對應資料庫 tooAzure AD 身分識別建立自主的資料庫使用者。
6. 使用 Azure AD 識別身分，連接 tooyour 資料庫。

> [!NOTE]
> toolearn 如何 toocreate 和填入 Azure AD 中，並接著設定 Azure AD 與 Azure SQL Database 和 SQL 資料倉儲，請參閱[設定使用 Azure SQL Database 的 Azure AD](sql-database-aad-authentication-configure.md)。
>

## <a name="trust-architecture"></a>信認架構
hello 下列概要圖摘要說明 hello 方案架構使用 Azure AD 驗證搭配 Azure SQL Database。 hello 相同的概念套用 tooSQL 資料倉儲。 會被視為 toosupport Azure AD 原生使用者密碼，只有 hello 雲端部分和 Azure AD/Azure SQL Database。 toosupport 同盟驗證 （或 Windows 認證的使用者/密碼），無須 hello 通訊與 ADFS 區塊。 hello 箭號表示通訊路徑。

![aad 驗證圖表][1]

hello 圖指出 hello 同盟、 信任，以及裝載可讓用戶端所送出語彙基元 tooconnect tooa 資料庫關聯性。 hello 權杖由 Azure AD 中，驗證，而且信任 hello 資料庫。 客戶 1 可以代表具有原生使用者的 Azure AD 或具有同盟使用者的 Azure Active Directory。 客戶 2 代表包含已匯入使用者的可能解決方案；在此範例中，來自同盟 Azure Active Directory 且 ADFS 正與 Azure Active Directory 進行同步處理。 請務必 toounderstand 存取 tooa 資料庫使用 Azure AD 驗證需要該 hello 裝載訂用帳戶相關聯的 toohello Azure AD。 hello 相同訂用帳戶必須是使用的 toocreate hello SQL Server 裝載 hello Azure SQL Database 或 SQL 資料倉儲。

![訂用帳戶關聯性][2]

## <a name="administrator-structure"></a>系統管理員結構
使用 Azure AD 驗證時，有兩個的系統管理員帳戶，以 hello SQL Database 伺服器;hello 原始的 SQL Server 系統管理員 」 和 「 hello Azure AD 系統管理員。 hello 相同的概念套用 tooSQL 資料倉儲。 只根據 Azure AD 帳戶的 hello 系統管理員可以在使用者資料庫中建立 hello 第一個 Azure AD 包含資料庫使用者。 hello Azure AD 系統管理員身分登入可以是 Azure AD 使用者或 Azure AD 群組。 群組帳戶 hello 系統管理員時，它可供任何群組的成員，讓 hello SQL Server 執行個體的多個 Azure AD 系統管理員。 使用系統管理員可讓您 toocentrally 增強管理功能的群組帳戶新增，並在 Azure AD 中移除群組成員，而不變更 hello 使用者或 SQL Database 中的權限。 一律只能設定一個 Azure AD 系統管理員 (使用者或群組)。

![系統管理員結構][3]

## <a name="permissions"></a>權限
toocreate 新使用者，您必須擁有 hello `ALTER ANY USER` hello 資料庫的權限。 hello`ALTER ANY USER`權限可以授與 tooany 資料庫使用者。 hello`ALTER ANY USER`權限也由 hello 伺服器系統管理員帳戶和資料庫使用者與 hello`CONTROL ON DATABASE`或`ALTER ON DATABASE`權限，該資料庫，以及成員 hello`db_owner`資料庫角色。

toocreate Azure SQL Database 或 SQL 資料倉儲中的自主的資料庫使用者，您必須連接 toohello 資料庫使用 Azure AD 身分識別。 toocreate hello 第一個自主的資料庫使用者，您必須使用 Azure AD 管理員 （hello hello 資料庫擁有者） 來連接 toohello 資料庫。 如以下步驟 4 和 5 所示。 只有進行 hello Azure AD 管理員已針對 Azure SQL Database 或 SQL 資料倉儲的伺服器建立任何 Azure AD 驗證。 如果 hello Azure Active Directory 系統管理員已從 hello 伺服器移除，在 SQL Server 內先前建立的現有 Azure Active Directory 使用者無法再連接 toohello 資料庫使用其 Azure Active Directory 認證。

## <a name="azure-ad-features-and-limitations"></a>Azure AD 功能和限制
hello 下列 Azure AD 的成員可以佈建 Azure SQL server 或 SQL 資料倉儲中：

* 原生成員： hello 受管理的網域或位於客戶網域中建立 Azure AD 中的成員。 如需詳細資訊，請參閱[加入您自己的網域名稱 tooAzure AD](../active-directory/active-directory-add-domain.md)。
* 同盟網域成員：利用同盟網域在 Azure AD 中建立的成員。 如需詳細資訊，請參閱 [Microsoft Azure 現在支援 Windows Server Active Directory 的同盟](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)。
* 從其他 Azure AD 匯入，且為原生網域或同盟網域成員者。
* 建立 Active Directory 群組作為安全性群組。

不支援 Microsoft 帳戶 (例如 outlook.com、hotmail.com、live.com) 或其他來賓帳戶 (例如 gmail.com、yahoo.com)。 如果可以登入太[https://login.live.com](https://login.live.com)使用 hello 帳戶和密碼，然後您使用 Microsoft 帳戶，不支援的 Azure SQL Database 或 Azure SQL 資料倉儲的 Azure AD 驗證。

## <a name="connecting-using-azure-ad-identities"></a>使用 Azure AD 身分識別連接

Azure Active Directory 驗證支援下列方法，使用 Azure AD 身分識別連接 tooa 資料庫的 hello:

* 使用整合式 Windows 驗證
* 使用 Azure AD 主體名稱和密碼
* 使用應用程式權杖驗證

### <a name="additional-considerations"></a>其他考量

* tooenhance 管理性，我們建議您佈建專用的 Azure AD 以系統管理員群組。   
* 一個 Azure SQL 伺服器或 Azure SQL 資料倉儲一律只能設定一個 Azure AD 系統管理員 (使用者或群組)。   
* 只有 SQL Server 的 Azure AD 系統管理員可以一開始連接 toohello Azure SQL server 或 Azure SQL 資料倉儲使用的 Azure Active Directory 帳戶。 hello Active Directory 系統管理員可以設定後續的 Azure AD 資料庫使用者。   
* 我們建議您設定 hello 連接逾時 too30 秒數。   
* SQL Server 2016 Management Studio 和 SQL Server Data Tools for Visual Studio 2015 (版本 14.0.60311.1 (2016 年 4 月) 或更新版本) 支援 Azure Active Directory 驗證。 (Azure AD 驗證受到 hello **.NET Framework Data Provider for SqlServer**; 至少版本.NET Framework 4.6)。 因此 hello 最新版本的這些工具和資料層應用程式 （DAC 和.bacpac） 可以使用 Azure AD 驗證。   
* [ODBC 13.1 版](https://www.microsoft.com/download/details.aspx?id=53339)支援 Azure Active Directory 驗證，不過，`bcp.exe` 無法使用 Azure Active Directory 驗證進行連線，因為它們使用較舊的 ODBC 提供者。   
* `sqlcmd`支援 Azure Active Directory 驗證版開始為可從 hello 13.1[下載中心](http://go.microsoft.com/fwlink/?LinkID=825643)。   
* 至少需要 SQL Server Data Tools for Visual Studio 2015 hello 2016 年 4 月版的 hello Data Tools （版本 14.0.60311.1）。 Azure AD 使用者目前不會顯示在 SSDT 物件總管中。 因應措施，檢視中的 hello 使用者[sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)。   
* [Microsoft JDBC Driver 6.0 for SQL Server](https://www.microsoft.com/download/details.aspx?id=11774) 支援 Azure AD 驗證。 此外，請參閱[設定 hello 連接屬性](https://msdn.microsoft.com/library/ms378988.aspx)。   
* PolyBase 無法使用 Azure AD 驗證進行驗證。   
* Hello Azure 入口網站支援 azure AD 驗證 SQL database**匯入資料庫**和**匯出資料庫**刀鋒視窗。 從 hello PowerShell 命令也支援匯入和匯出使用 Azure AD 驗證。   
* SQL Database 和 SQL 資料倉儲 (使用 CLI) 支援 Azure AD 驗證。 如需詳細資訊，請參閱[使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證](sql-database-aad-authentication-configure.md)和 [SQL Server - az sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server)。

## <a name="next-steps"></a>後續步驟
- toolearn 如何 toocreate 和填入 Azure AD 中，並接著設定 Azure AD 與 Azure SQL Database 或 Azure SQL 資料倉儲，請參閱[設定和管理 Azure Active Directory 驗證與 SQL Database 或 SQL 資料倉儲](sql-database-aad-authentication-configure.md)。
- 如需 SQL Database 中存取權和控制權的概觀，請參閱 [SQL Database 的存取權和控制權](sql-database-control-access.md)。
- 如需 SQL Database 中登入、使用者和資料庫角色的概觀，請參閱[登入、使用者和資料庫角色](sql-database-manage-logins.md)。
- 如需資料庫主體的詳細資訊，請參閱[主體](https://msdn.microsoft.com/library/ms181127.aspx)。
- 如需資料庫角色的詳細資訊，請參閱[資料庫角色](https://msdn.microsoft.com/library/ms189121.aspx)。
- 如需 SQL Database 中防火牆規則的詳細資訊，請參閱 [SQL Database 防火牆規則](sql-database-firewall-configure.md)。

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

