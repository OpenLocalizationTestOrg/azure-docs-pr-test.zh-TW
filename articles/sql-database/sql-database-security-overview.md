---
title: "Azure SQL Database 安全性概觀 | Microsoft Docs"
description: "了解 Azure SQL Database 和 SQL Server 的 安全性，包含雲端和 SQL Server 內部部署之間的差異。"
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
ms.workload: On Demand
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 14a7fdb304e90aec10bee9167817f564870cd6c1
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="securing-your-sql-database"></a>保護您的 SQL Database

本篇文章逐步說明使用 Azure SQL Database 保護應用程式資料層的基本概念。 本文尤其著重於協助您開始利用資源來保護資料、控制存取，以及進行主動式監視。 

如需各種 SQL 上可用的完整安全性功能概觀，請參閱 [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](https://msdn.microsoft.com/library/bb510589)。 同時您也可於 [安全性和 Azure SQL Database 技術白皮書](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF) 中取得其他資訊。

## <a name="protect-data"></a>保護資料
SQL Database 會使用[傳輸層安全性](https://support.microsoft.com/kb/3135244)為移動中的資料提供加密、使用[透明資料加密](/sql/relational-databases/security/encryption/transparent-data-encryption-azure-sql)為待用資料提供加密，使用[一律加密](https://msdn.microsoft.com/library/mt163865.aspx)為使用中的資料提供加密，進而保護您的資料。 

> [!IMPORTANT]
>Azure SQL Database 的所有連線，也就是任何時候只要資料需要「傳輸」進出資料庫時，都需要加密 (SSL/TLS)。 在您的應用程式連接字串中，您必須指定要加密的連接參數和*不*信任伺服器憑證 （這基於您如果複製您從 Azure 入口網站的連接字串），否則為連接將不會驗證伺服器身分識別，且會受到"中--攔截 」 攻擊。 例如對於 ADO.NET 驅動程式，這些連接字串參數是 **Encrypt=True** 和 **TrustServerCertificate=False**。 

如需其他的資料加密方式，請考慮：

* [儲存格層級加密](https://msdn.microsoft.com/library/ms179331.aspx) ，可利用不同的加密金鑰來加密特定的資料行或甚至是資料儲存格。
* 如果您需要硬體安全性模組或集中管理您的加密金鑰階層，請考慮 [在 Azure VM 中使用 Azure 金鑰保存庫搭配 SQL Server](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx)。

## <a name="control-access"></a>控制存取
SQL Database 使用防火牆規則、要求使用者證明其身分的驗證機制，以及透過角色型成員資格與權限和透過資料列層級安全性與動態資料遮罩的資料授權來限制資料庫的存取，進而保護您的資料。 如需在 SQL Database 中使用存取控制功能的討論，請參閱[控制存取](sql-database-control-access.md)。

> [!IMPORTANT]
> 在 Azure 內管理資料庫和邏輯伺服器，是由入口網站使用者帳戶的角色指派所控制。 如需有關本主題的詳細資訊，請參閱[Azure 入口網站中的角色型存取控制](../active-directory/role-based-access-control-what-is.md)。
>

### <a name="firewall-and-firewall-rules"></a>防火牆與防火牆規則
為了協助保護您的資料，防火牆會防止對您的資料庫伺服器的所有存取，直到您使用[防火牆規則](sql-database-firewall-configure.md)指定哪些電腦擁有權限。 此防火牆會根據每一個要求的來源 IP 位址來授與資料庫存取權。

### <a name="authentication"></a>驗證
SQL Database 驗證是指連線到資料庫時如何證明身分識別。 SQL Database 支援兩種驗證類型：

* **SQL 驗證**，其需要使用者名稱和密碼。 當您為資料庫建立邏輯伺服器時，採取使用者名稱和密碼指定了「伺服器管理員」登入。 使用這些認證，您就可以使用資料庫擁有者或 "dbo" 的身分驗證該伺服器上的任何資料庫。 
* 
            **Azure Active Directory 驗證**，它會使用由 Azure Active Directory 管理的身分識別，並支援受控和整合的網域。 [盡可能](https://msdn.microsoft.com/library/ms144284.aspx)使用 Active Directory 驗證 (整合式安全性)。 如果您想要使用 Azure Active Directory 驗證，就必須建立另一個名為「Azure AD 管理員」的伺服器管理員，其能夠管理 Azure AD 使用者和群組。 此管理員也可以執行一般伺服器管理員可執行的所有作業。 如需如何建立 Azure AD 管理員以啟用 Azure Active Directory 驗證的逐步解說，請參閱 [使用 Azure Active Directory 驗證連線到 SQL Database](sql-database-aad-authentication.md) 。

### <a name="authorization"></a>Authorization
授權是指使用者可以在 Azure SQL Database 內執行的動作，這是由使用者帳戶的資料庫角色成員資格和物件層級權限所控制。 最好的作法是，您應該授與使用者所需的最低權限。 您所連線的伺服器管理員帳戶是 db_owner 的成員，有權限在資料庫中執行任何動作。 請儲存此帳戶，以便部署結構描述升級及其他管理作業。 請使用具更多有限權限的 "ApplicationUser" 帳戶，從應用程式連線到具應用程式所需之最低權限的資料庫。

### <a name="row-level-security"></a>資料列層級安全性
資料列層級安全性讓客戶能夠根據執行查詢之使用者的特性 (例如，群組成員資格或執行內容) 來控制資料庫資料表中的資料列存取。 如需詳細資訊，請參閱[資料列層級安全性](https://msdn.microsoft.com/library/dn765131)。

### <a name="data-masking"></a>資料遮罩 
SQL Database 動態資料遮罩可藉由遮罩處理，使不具權限的使用者無法看見機密資料。 動態資料遮罩會自動探索 Azure SQL Database 中的可能敏感性資料，並提供可動作的建議來為這些欄位加上遮罩，盡量避免對應用程式層造成影響。 其運作方式為針對指定的資料庫欄位隱匿查詢結果集中的敏感性資料，而不變更資料庫中的資料。 如需詳細資訊，請參閱[開始使用 SQL Database 動態資料遮罩](sql-database-dynamic-data-masking-get-started.md)，其可以用來限制敏感性資料的公開。

## <a name="proactive-monitoring"></a>主動監視
SQL Database 可藉由提供稽核和威脅偵測功能來保護您的資料。 

### <a name="auditing"></a>稽核
SQL Database 稽核會將資料庫事件記錄到 Azure 儲存體帳戶中的稽核記錄檔，藉此追蹤資料庫活動並協助您維護法規相符性。 稽核可讓您了解進行中的資料庫活動，以及分析和調查歷史活動，以找出潛在威脅或可疑的濫用和安全性違規。 如需其他資訊，請參閱[開始使用 SQL Database 稽核](sql-database-auditing.md)。  

### <a name="threat-detection"></a>威脅偵測
威脅偵測會提供 Azure SQL Database 服務內建的額外安全情報層，此情報層可偵測到不尋常且有危害的資料庫存取或攻擊動作，藉此補充稽核的不足之處。 系統會警示您有關可疑活動、潛在弱點、SQL 插入式攻擊和異常資料庫存取模式。 您可以從 [Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)檢視威脅偵測警示，該警示會提供可疑活動的詳細資料，以及如何調查與降低威脅的建議。 每部伺服器的威脅偵測費用為每個月 $15 元。 前 60 天免費。 如需詳細資訊，請參閱 [開始使用 SQL Database 威脅偵測](sql-database-threat-detection.md)。
 
### <a name="data-masking"></a>資料遮罩 
SQL Database 動態資料遮罩可藉由遮罩處理，使不具權限的使用者無法看見機密資料。 動態資料遮罩會自動探索 Azure SQL Database 中的可能敏感性資料，並提供可動作的建議來為這些欄位加上遮罩，盡量避免對應用程式層造成影響。 其運作方式為針對指定的資料庫欄位隱匿查詢結果集中的敏感性資料，而不變更資料庫中的資料。 如需詳細資訊，請參閱[開始使用 SQL Database 動態資料遮罩](sql-database-dynamic-data-masking-get-started.md)
 
## <a name="compliance"></a>法規遵循
除了上述可協助您的應用程式符合各種安全性需求的特色和功能之外，Azure SQL Database 也定期參與稽核，並且經過認證符合許多法規標準。 如需詳細資訊，請參閱 [Microsoft Azure 信任中心](https://azure.microsoft.com/support/trust-center/)，您可以在當中找到 [SQL Database 法規認證](https://azure.microsoft.com/support/trust-center/services/)的最新清單。

## <a name="next-steps"></a>後續步驟

- 如需在 SQL Database 中使用存取控制功能的討論，請參閱[控制存取](sql-database-control-access.md)。
- 如需資料庫稽核的相關討論，請參閱 [SQL Database 稽核 (英文)](sql-database-auditing.md)。
- 如需威脅偵測的相關討論，請參閱 [SQL Database 威脅偵測](sql-database-threat-detection.md)。
