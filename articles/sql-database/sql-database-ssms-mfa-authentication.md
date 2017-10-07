---
title: "aaaMulti 雙因素驗證-Azure SQL |Microsoft 文件"
description: "針對 SQL Database 和 SQL 資料倉儲，搭配使用 Multi-Factor Authentication 與 SSMS。"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)
Azure SQL Database 和 Azure SQL 資料倉儲支援使用「Active Directory 通用驗證」 ，從 SQL Server Management Studio (SSMS) 連線。 
**下載最新的 SSMS 的 hello** -hello 用戶端電腦上，從下載 hello 最新版本的 SSMS，[下載 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)。 針對所有本主題中的 hello 功能，使用至少第 2017 年 7 月版本 17.2。  hello 最新連線 對話方塊看起來像這樣： ![1mfa 通用連接](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "完成 hello 使用者名稱 方塊。")  

## <a name="hello-five-authentication-options"></a>hello 五驗證選項  
- Active Directory 通用驗證支援兩種非互動式驗證方法 hello (`Active Directory - Password`驗證和`Active Directory - Integrated`驗證)。 非互動式 `Active Directory - Password` 和 `Active Directory - Integrated` 驗證方法，可以在許多不同的應用程式 (ADO.NET、JDBC、ODBC 等) 中使用。 這兩種方法絕對不會產生快顯對話方塊。

- `Active Directory - Universal with MFA` 驗證也是支援 Azure Multi-Factor Authentication (MFA) 的互動式方法。 Azure MFA 有助於保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。 提供與一系列簡單的驗證選項 （電話、 簡訊，智慧卡 pin，或行動裝置應用程式通知），其偏好允許的使用者 toochoose hello 方法的增強式驗證。 搭配 Azure AD 使用互動式 MFA 時，會出現快顯對話方塊以進行驗證。

如需 Multi-Factor Authentication 的說明，請參閱 [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)。
如需了解組態步驟，請參閱[設定適用於 SQL Server Management Studio 的 Azure SQL Database 多重要素驗證](sql-database-ssms-mfa-authentication-configure.md)。

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Azure AD 網域名稱或租用戶 ID 參數   

開頭為[SSMS 版本 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)，匯入至 hello 使用者目前的 Active Directory 與其他 Azure Active Directory，為 guest 使用者，可以提供 hello Azure AD 網域名稱，或連線時，租用戶識別碼。 來賓使用者包括從其他 Azure AD、Microsoft 帳戶 (例如 outlook.com、hotmail.com、live.com) 或其他帳戶 (例如 gmail.com) 邀請的使用者。這項資訊，可讓**Active Directory 萬用透過 MFA 驗證**tooidentify hello 正確驗證授權單位。 此選項也是必要的 toosupport Microsoft 帳戶 (MSA) 例如 outlook.com、 hotmail.com、 live.com 或非 MSA 帳戶。 所有這些使用者想要使用通用驗證進行驗證的 toobe 必須輸入他們的 Azure AD 網域名稱或租用戶識別碼。 這個參數代表 hello 目前的 Azure AD 網域名稱/租用戶識別碼 hello 與 Azure 伺服器相連結。 例如，如果 Azure 伺服器與 Azure AD 網域相關聯`contosotest.onmicrosoft.com`其中使用者`joe@contosodev.onmicrosoft.com`裝載為匯入的使用者，從 Azure AD 網域`contosodev.onmicrosoft.com`，hello 這個使用者的網域必須有名稱 tooauthenticate `contosotest.onmicrosoft.com`。 Hello 使用者是原生使用者的 hello 連結的 Azure AD tooAzure 伺服器，而非 MSA 帳戶，沒有網域名稱或租用戶識別碼時，所需。 在 hello tooenter hello 參數 （開始使用 SSMS 版本 17.2）**連接 tooDatabase**對話方塊中，完成 hello 對話方塊中，選取**Active Directory-通用 mfa**驗證，按一下**選項**，完成 hello**使用者名**方塊，然後再按一下 hello**連接屬性** 索引標籤。檢查 hello **AD 網域名稱或租用戶識別碼**方塊，並提供驗證授權單位，例如 hello 網域名稱 (**contosotest.onmicrosoft.com**) 或 hello hello 租用戶識別碼的 GUID  
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Azure AD 商務 toobusiness 支援   
支援的 Azure AD B2B 案例為 guest 使用者的 azure AD 使用者 (請參閱[什麼是 Azure B2B 共同作業](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) 可以只做為目前的 Azure AD 中建立與手動對應群組的成員一部分連接 tooSQL 資料庫和 SQL 資料倉儲使用 hello TRANSACT-SQL`CREATE USER`給定資料庫中的陳述式。 例如，如果`steve@gmail.com`會受邀的 tooAzure AD `contosotest` (hello Azure Ad 網域與`contosotest.onmicrosoft.com`)，Azure AD 群組，例如`usergroup`必須在 hello 包含 hello 的 Azure AD 中建立`steve@gmail.com`成員。 然後，Azure AD SQL 系統管理員或 Azure AD DBO 必須藉由執行 Transact-SQL `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` 陳述式，針對特定資料庫 (也就是 MyDatabase) 建立此群組。 建立 hello 資料庫使用者之後，再 hello 使用者`steve@gmail.com`太可以登入`MyDatabase`使用 hello SSMS 驗證選項`Active Directory – Universal with MFA support`。 hello usergroup，根據預設，具有連接權限，以及需要 toobe hello 中授與任何其他資料存取的 hello 一般的方式。 請注意該使用者`steve@gmail.com`必須核取方塊 hello guest 使用者，並將 hello AD 網域名稱新增`contosotest.onmicrosoft.com`hello SSMS 中**連接屬性** 對話方塊。 hello **AD 網域名稱或租用戶識別碼**hello Universal MFA 連接選項只支援選項，否則它會呈現灰色。

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>適用於 SQL Database 和 SQL 資料倉儲的通用驗證限制
* SSMS 和 SqlPackage.exe 是 hello 只有工具目前為透過 Active Directory 通用驗證的 MFA 進行啟用。
* SSMS 17.2 版支援使用通用驗證搭配 MFA 的多使用者同時存取。 版本 17.0 和 17.1，僅限 SSMS 使用通用驗證 tooa 單一 Azure Active Directory 帳戶的執行個體的登入。 toolog 中的做為另一個 Azure AD 帳戶，您必須使用另一個 SSMS 執行個體。 （這項限制是有限的 tooActive Directory 通用驗證，您可以登入 toodifferent 伺服器使用 Active Directory 密碼驗證、 Active Directory 整合式驗證或 SQL Server 驗證）。
* SSMS 支援 Active Directory 通用驗證，可使用物件總管、查詢編輯器及查詢存放區視覺效果。
* SSMS 17.2 版針對匯出/擷取/部署資料資料庫提供 DacFx 精靈支援。 透過使用通用驗證 hello 初始驗證對話方塊會驗證特定的使用者，一旦 hello DacFx 精靈函式 hello 相同方式，它會為所有其他驗證方法。
* hello SSMS 資料表設計工具不支援通用驗證。
* 除了您必須使用支援的 SSMS 版本之外，Active Directory 通用驗證並沒有其他軟體需求。  
* 通用驗證的 hello Active Directory 驗證程式庫 (ADAL) 版本已更新的 tooits 最新發行的 ADAL.dll 3.13.9 可用版本。 請參閱 [Active Directory Authentication Library 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/)。


## <a name="next-steps"></a>後續步驟

- 如需了解組態步驟，請參閱[設定適用於 SQL Server Management Studio 的 Azure SQL Database 多重要素驗證](sql-database-ssms-mfa-authentication-configure.md)。
- 授與其他人存取 tooyour 資料庫： [SQL Database 驗證和授權： 授與存取權](sql-database-manage-logins.md)  
- 請確定其他人可以透過 hello 防火牆連線：[設定 Azure SQL Database 伺服器層級防火牆規則使用 hello Azure 入口網站](sql-database-configure-firewall-settings.md)  
- [使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證](sql-database-aad-authentication-configure.md)  
- [Microsoft SQL Server Data-Tier Application Framework (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [匯入 BACPAC 檔案 tooa 新的 Azure SQL Database](../sql-database/sql-database-import.md)  
- [Azure SQL database tooa BACPAC 檔案匯出](../sql-database/sql-database-export.md)  
- C# 介面 [IUniversalAuthProvider 介面](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
