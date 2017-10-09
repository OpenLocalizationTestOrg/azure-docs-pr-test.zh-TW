---
title: "aaaAuthentication tooAzure SQL 資料倉儲 |Microsoft 文件"
description: "Azure Active Directory (AAD) 與 SQL Server 驗證 tooAzure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>驗證 tooAzure SQL 資料倉儲
> [!div class="op_single_selector"]
> * [安全性概觀](sql-data-warehouse-overview-manage-security.md)
> * [驗證](sql-data-warehouse-authentication.md)
> * [加密 (入口網站)](sql-data-warehouse-encryption-tde.md)
> * [加密 (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooconnect tooSQL 資料倉儲，您必須傳入安全性認證進行驗證。 建立連線時，會設定特定的連線設定，以做為建立查詢工作階段的一部分。  

如需有關安全性和如何 tooenable 連線 tooyour 資料倉儲時，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。

## <a name="sql-authentication"></a>SQL 驗證
tooconnect tooSQL 資料倉儲，您必須提供下列資訊的 hello:

* 完整伺服器名稱
* 指定 SQL 驗證
* 使用者名稱
* 密碼
* 預設資料庫 (選擇性)

依預設您的連接會連接 toohello*主要*資料庫而非您的使用者資料庫。 tooconnect tooyour 使用者資料庫中，您可以選擇 toodo 兩種情況之一：

* 以 SQL Server 物件總管在 SSDT 中，SSMS 中，或在您的應用程式的連接字串中的 hello 註冊您的伺服器時，請指定 hello 預設資料庫。 例如，包含 ODBC 連接的 hello InitialCatalog 參數。
* 在 SSDT 中建立工作階段之前，反白 hello 使用者資料庫。

> [!NOTE]
> hello TRANSACT-SQL 陳述式**使用 MyDatabase;**不支援變更 hello 連接的資料庫。 有了 SSDT 連接 tooSQL 資料倉儲的指引，請參閱 toohello [Visual Studio 中的查詢][ Query with Visual Studio]發行項。
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Azure Active Directory (AAD) 驗證
[Azure Active Directory] [ What is Azure Active Directory]驗證是一項機制的 Azure Active Directory (Azure AD) 中使用身分識別連接 tooMicrosoft Azure SQL 資料倉儲。 使用 Azure Active Directory 驗證時，您可以集中管理 hello 的資料庫使用者的身分識別和其他 Microsoft 服務在單一中央位置。 中央識別碼管理 toomanage SQL 資料倉儲使用者提供單一位置，並簡化權限管理。 

### <a name="benefits"></a>優點
Azure Active Directory 的優點包括：

* 提供的替代 tooSQL 伺服器驗證。
* 可協助停止使用者身分識別的 hello 的擴散到資料庫伺服器。
* 允許在單一位置的密碼替換
* 使用外部 (AAD) 群組管理資料庫權限。
* 藉由啟用整合式 Windows 驗證和 Azure Active Directory 支援的其他形式驗證來避免儲存密碼。
* 使用自主資料庫使用者 tooauthenticate 識別 hello 資料庫層級。
* 支援權杖為基礎的驗證連接 tooSQL 資料倉儲的應用程式。
* 透過 SQL Server Management Studio 的 Active Directory 通用驗證支援 Multi-Factor Authentication。 如需 Multi-Factor Authentication 的說明，請參閱 [適用於 Azure AD MFA 與 SQL Database 和 SQL 資料倉儲的 SSMS 支援](../sql-database/sql-database-ssms-mfa-authentication.md)。

> [!NOTE]
> Azure Active Directory 相對來說仍較新，且具有一些限制。 請參閱 Azure Active Directory 是您的環境，適合 tooensure [Azure AD 的功能和限制][Azure AD features and limitations]，具體來說 hello 其他考量。
> 
> 

### <a name="configuration-steps"></a>組態步驟
請遵循這些步驟 tooconfigure Azure Active Directory 驗證。

1. 建立和填入 Azure Active Directory
2. 選擇性： 建立關聯，或變更 hello 目前與 Azure 訂用帳戶相關聯的 active directory
3. 建立 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。
4. 設定用戶端電腦
5. 在對應資料庫 tooAzure AD 身分識別建立自主的資料庫使用者
6. 使用 Azure AD 識別身分，連接 tooyour 資料倉儲

Azure Active Directory 使用者目前不會顯示在 SSDT 物件總管中。 因應措施，檢視中的 hello 使用者[sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)。

### <a name="find-hello-details"></a>找出 hello 詳細資料
* hello 步驟 tooconfigure 和使用 Azure Active Directory 驗證是用於 Azure SQL Database 和 Azure SQL 資料倉儲幾乎完全相同。 請遵循 hello 詳細 hello 主題中的步驟[連接 tooSQL 資料庫或 SQL 資料倉儲使用 Azure Active Directory 驗證](../sql-database/sql-database-aad-authentication.md)。
* 建立自訂資料庫角色，並新增使用者 toohello 角色。 然後授與的細微權限 toohello 角色。 如需詳細資訊，請參閱 [資料庫引擎權限使用者入門](https://msdn.microsoft.com/library/mt667986.aspx)。

## <a name="next-steps"></a>後續步驟
toostart 查詢您的資料倉儲與 Visual Studio 和其他應用程式，請參閱[Visual Studio 中的查詢][Query with Visual Studio]。

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
