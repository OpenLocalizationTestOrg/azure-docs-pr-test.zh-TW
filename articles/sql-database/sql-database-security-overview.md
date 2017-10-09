---
title: "aaaAzure SQL Database 安全性概觀 |Microsoft 文件"
description: "深入了解 Azure SQL Database 和 SQL Server 安全性，包括 hello hello 雲端和內部 SQL Server 之間的差異，當 tooauthentication、 授權、 連線安全性、 加密和相容性。"
services: sql-database
documentationcenter: 
author: tmullaney
manager: jhubbard
editor: 
ms.assetid: a012bb85-7fb4-4fde-a2fc-cf426c0a56bb
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 7b0b0d1b59ec4018d9fb668bc8b6b56c9907e982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-your-sql-database"></a>保護您的 SQL Database

本文逐步 hello 保護 hello 資料層應用程式使用 Azure SQL Database 的基本概念。 本文尤其著重於協助您開始利用資源來保護資料、控制存取，以及進行主動式監視。 

SQL 的所有版本上使用的安全性功能的完整概觀，請參閱 hello [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](https://msdn.microsoft.com/library/bb510589)。 其他資訊也會提供 hello[安全性和 Azure SQL Database 技術的白皮書](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf)(PDF)。

## <a name="protect-data"></a>保護資料
SQL Database 會使用[傳輸層安全性](https://support.microsoft.com/kb/3135244)為移動中的資料提供加密、使用[透明資料加密](http://go.microsoft.com/fwlink/?LinkId=526242)為待用資料提供加密，使用[一律加密](https://msdn.microsoft.com/library/mt163865.aspx)為使用中的資料提供加密，進而保護您的資料。 

> [!IMPORTANT]
>所有連線 tooAzure SQL 資料庫都需要加密 (SSL/TLS) 在所有時間資料從 hello 資料庫的 「 在傳輸"tooand 時發生。 在您的應用程式連接字串中，您必須指定參數 tooencrypt hello 連接和*不*tootrust hello 的伺服器憑證 （這是針對您如果複製您的連接字串，超出 hello Azure 傳統入口網站），否則 hello 連接將不會驗證 hello 伺服器 hello 身分識別，而且將會受到影響太"中--攔截 」 攻擊。 Hello ADO.NET 驅動程式，比方說，這些連接字串參數則都**Encrypt = True**和**TrustServerCertificate = False**。 

其他方式 tooencrypt 您的資料，請考慮：

* [資料格層級加密](https://msdn.microsoft.com/library/ms179331.aspx)tooencrypt 特定資料行或甚至是資料格具有不同的加密金鑰的資料。
* 如果您需要硬體安全性模組或集中管理您的加密金鑰階層，請考慮 [在 Azure VM 中使用 Azure 金鑰保存庫搭配 SQL Server](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx)。

## <a name="control-access"></a>控制存取
SQL Database，方法是限制存取 tooyour 資料庫使用的防火牆規則，驗證其身分識別及授權 toodata 透過以角色為基礎的成員資格和權限，以及透過需要使用者 tooprove 的機制保護您的資料資料列層級安全性和動態資料遮罩。 如需 hello 使用 SQL Database 中的存取控制功能的討論，請參閱[控制存取](sql-database-control-access.md)。

> [!IMPORTANT]
> 在 Azure 內管理資料庫和邏輯伺服器，是由入口網站使用者帳戶的角色指派所控制。 如需有關此主題的詳細資訊，請參閱 [Azure 入口網站中的角色型存取控制](../active-directory/role-based-access-control-what-is.md)。
>

### <a name="firewall-and-firewall-rules"></a>防火牆與防火牆規則
toohelp 保護您的資料，防火牆會阻止所有存取 tooyour 資料庫伺服器，您必須先指定哪些電腦有權限使用[防火牆規則](sql-database-firewall-configure.md)。 hello 防火牆會授與存取 toodatabases hello 來自每個要求的 IP 位址為基礎。

### <a name="authentication"></a>驗證
SQL database 驗證是指 toohow 連接 toohello 資料庫時，證明您的身分識別。 SQL Database 支援兩種驗證類型：

* **SQL 驗證**，其需要使用者名稱和密碼。 當您為您的資料庫建立 hello 邏輯伺服器時，您可以指定 「 伺服器管理員 」 的登入使用者名稱和密碼。 使用這些認證時，您可以驗證 tooany 為 hello 資料庫擁有者或"dbo"。 該伺服器上的資料庫 
* **Azure Active Directory 驗證**，它會使用由 Azure Active Directory 管理的身分識別，並支援受管理和整合的網域。 [盡可能](https://msdn.microsoft.com/library/ms144284.aspx)使用 Active Directory 驗證 (整合式安全性)。 如果您想 toouse Azure Active Directory 驗證時，您必須建立另一個伺服器系統管理員稱為 hello"Azure AD admin"，這允許 tooadminister Azure AD 使用者和群組。 此管理員也可以執行一般伺服器管理員可執行的所有作業。 請參閱[連接 tooSQL 資料庫使用 Azure Active Directory 驗證](sql-database-aad-authentication.md)方式的逐步解說 toocreate Azure AD 管理員 tooenable Azure Active Directory 驗證。

### <a name="authorization"></a>Authorization
授權是指的 toowhat 使用者可以在 Azure SQL Database 中執行，這是由使用者帳戶的資料庫角色成員資格控制和物件層級權限。 最佳做法，您應該授與使用者 hello 最低必要權限。 hello 您所連接的伺服器系統管理員帳戶是具有授權 toodo hello 資料庫內的任何項目 db_owner 的成員。 請儲存此帳戶，以便部署結構描述升級及其他管理作業。 使用具有更多限制的權限 tooconnect 從您的應用程式 toohello 資料庫以 hello hello"ApplicationUser"帳戶應用程式所需的最低權限。

### <a name="row-level-security"></a>資料列層級安全性
資料列層級安全性可讓客戶 toocontrol 存取 toorows 根據 hello 特性 hello 使用者執行查詢 （例如，群組成員資格或執行內容） 的資料庫資料表中。 如需詳細資訊，請參閱[資料列層級安全性](https://msdn.microsoft.com/library/dn765131)。

### <a name="data-masking"></a>資料遮罩 
SQL Database 動態資料遮罩會限制機密資料暴露其 toonon 權限的使用者。 動態資料遮罩會自動探索 Azure SQL Database 中的敏感性資料，並提供可採取動作的建議 toomask 的設定，這些欄位，與 hello 應用程式層上的影響降到最低。 其運作方式是在指定的資料庫欄位模糊化 hello hello 查詢結果集內的機密資料，而 hello 資料庫中的 hello 資料不會變更。 如需詳細資訊，請參閱[開始使用 SQL Database 動態資料遮罩](sql-database-dynamic-data-masking-get-started.md)可以是使用的 toolimit 公開機密資料。

## <a name="proactive-monitoring"></a>主動監視
SQL Database 可藉由提供稽核和威脅偵測功能來保護您的資料。 

### <a name="auditing"></a>稽核
SQL Database 稽核會追蹤資料庫活動，並協助您 toomaintain 法規相符性，錄製您的 Azure 儲存體帳戶中的資料庫事件 tooan 稽核記錄檔。 稽核 toounderstand 進行中的資料庫活動，可讓您，以及分析和調查 tooidentify 潛在威脅時，歷程記錄活動或可疑的濫用和安全性違規。 如需其他資訊，請參閱[開始使用 SQL Database 稽核](sql-database-auditing.md)。  

### <a name="threat-detection"></a>威脅偵測
威脅偵測補充稽核，藉由提供額外的安全性，偵測到不尋常和有害嘗試 tooaccess 或利用資料庫 hello Azure SQL Database 服務內建的智慧。 系統會警示您有關可疑活動、潛在弱點、SQL 插入式攻擊和異常資料庫存取模式。 可以從檢視威脅偵測警示[Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)提供可疑活動的詳細資訊和建議動作如何 tooinvestigate 和降低 hello 威脅。 每部伺服器的威脅偵測費用為每個月 $15 元。 它會將沒有 hello 前 60 天。 如需詳細資訊，請參閱 [開始使用 SQL Database 威脅偵測](sql-database-threat-detection.md)。
 
### <a name="data-masking"></a>資料遮罩 
SQL Database 動態資料遮罩會限制機密資料暴露其 toonon 權限的使用者。 動態資料遮罩會自動探索 Azure SQL Database 中的敏感性資料，並提供可採取動作的建議 toomask 的設定，這些欄位，與 hello 應用程式層上的影響降到最低。 其運作方式是在指定的資料庫欄位模糊化 hello hello 查詢結果集內的機密資料，而 hello 資料庫中的 hello 資料不會變更。 如需詳細資訊，請參閱[開始使用 SQL Database 動態資料遮罩](sql-database-dynamic-data-masking-get-started.md)
 
## <a name="compliance"></a>法規遵循
此外上方特性與功能，可協助您的應用程式也符合各種安全性需求，Azure SQL Database toohello 參與定期的稽核，而且已經過認證可針對許多規範標準。 如需詳細資訊，請參閱 hello [Microsoft Azure 信任中心](https://azure.microsoft.com/support/trust-center/)，您可以找到 hello 最新的清單其中[SQL 資料庫相容性認證](https://azure.microsoft.com/support/trust-center/services/)。

## <a name="next-steps"></a>後續步驟

- 如需 hello 使用 SQL Database 中的存取控制功能的討論，請參閱[控制存取](sql-database-control-access.md)。
- 如需資料庫稽核的相關討論，請參閱 [SQL Database 稽核 (英文)](sql-database-auditing.md)。
- 如需威脅偵測的相關討論，請參閱 [SQL Database 威脅偵測](sql-database-threat-detection.md)。
