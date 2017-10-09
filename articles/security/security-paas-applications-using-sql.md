---
title: "在 Azure 中的 PaaS 資料庫 aaaSecuring |Microsoft 文件"
description: " 了解用來保護 PaaS Web 與行動應用程式的 Azure SQL Database 和 SQL 資料倉儲安全性最佳做法。 "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>保護 Azure 中的 PaaS 資料庫

在本文中，我們將說明用來保護 PaaS Web 與行動應用程式的 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) 和 [SQL 資料倉儲](https://azure.microsoft.com/services/sql-data-warehouse/)安全性最佳做法。 這些最佳作法從我們的經驗與 Azure 和 hello 經驗的客戶想自己。

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Azure SQL Database 和 SQL 資料倉儲
[Azure SQL Database](../sql-database/sql-database-technical-overview.md) 和 [SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)可為您的網際網路型應用程式提供關聯式資料庫服務。 讓我們來了解當使用 PaaS 部署中的 Azure SQL Database 和「SQL 資料倉儲」時，可協助保護您應用程式和資料的服務：

- Azure Active Directory 驗證 (而不是 SQL Server 驗證)
- Azure SQL 防火牆
- 透明資料加密 (TDE)

## <a name="best-practices"></a>最佳作法

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>使用集中式身分識別儲存機制來進行驗證和授權

Azure SQL 資料庫可以是下列其中一種驗證設定的 toouse:

- 「SQL 驗證」會使用使用者名稱和密碼。 當您為您的資料庫建立 hello 邏輯伺服器時，您可以指定 「 伺服器管理員 」 的登入使用者名稱和密碼。 使用這些認證時，您可以驗證該伺服器上的 tooany 資料庫 hello 資料庫擁有者。

- 「Azure Active Directory 驗證」會使用由 Azure Active Directory 管理的身分識別，並且受管理網域和整合式網域都支援此驗證。 toouse Azure Active Directory 驗證，您必須建立另一個伺服器系統管理員稱為 hello"Azure AD admin"，這允許 tooadminister Azure AD 使用者和群組。 此管理員也可以執行一般伺服器管理員可執行的所有作業。

[Azure Active Directory 驗證](../active-directory/develop/active-directory-authentication-scenarios.md)機制來使用身分識別中 Azure Active Directory (AD) 連線 tooAzure SQL Database 和 SQL 資料倉儲。 Azure AD 提供替代 tooSQL 伺服器驗證，因此您可以停止的使用者身分識別的 hello 擴散到資料庫伺服器。 Azure AD 驗證可讓您 toocentrally 管理的資料庫使用者與其他 Microsoft 服務，在單一集中位置的 hello 身分識別。 中央識別碼管理 toomanage 資料庫使用者提供單一位置，並簡化權限管理。  

使用 Azure AD 驗證而不使用 SQL Server 驗證的好處包括：

- 允許在單一位置變換密碼。
- 使用外部 Azure AD 群組來管理資料庫權限。
- 藉由啟用整合式 Windows 驗證和 Azure AD 支援的其他形式驗證來避免儲存密碼。
- 使用自主資料庫使用者 tooauthenticate 識別 hello 資料庫層級。
- 支援權杖為基礎的驗證連接 tooSQL 資料庫應用程式。
- 支援本機 Azure AD 的 ADFS (網域同盟) 或原生使用者/密碼驗證，而不需進行網域同步處理。
- 支援來自 SQL Server Management Studio 之使用「Active Directory 通用驗證」(包括 [Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md)) 的連線。 MFA 包含增強式驗證功能，其中提供一系列簡易的驗證選項，例如電話、簡訊、含有 PIN 的智慧卡或行動應用程式通知。 如需詳細資訊，請參閱 [適用於與 SQL Database 和 SQL 資料倉儲搭配使用之 Azure AD MFA 的 SSMS 支援](../sql-database/sql-database-ssms-mfa-authentication.md)。

toolearn 進一步了解 Azure AD 驗證，請參閱：

- [TooSQL 資料庫或 SQL 資料倉儲使用 Azure Active Directory 驗證連接](../sql-database/sql-database-aad-authentication.md)
- [驗證 tooAzure SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [使用 Azure AD 驗證之 Azure SQL DB 的權杖型驗證支援 (英文)](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)

> [!NOTE]
> 請參閱 Azure Active Directory 是您的環境，適合 tooensure [Azure AD 的功能和限制](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations)，具體來說 hello 其他考量。
>
>

### <a name="restrict-access-based-on-ip-address"></a>根據 IP 位址限制存取
您可以建立指定可接受之 IP 位址範圍的防火牆規則。 這些規則可以 hello 伺服器和資料庫層級上的目標。 我們建議使用資料庫層級防火牆規則時可能 tooenhance 安全性和 toomake 更容易移植您的資料庫。 伺服器層級防火牆規則最適合用於系統管理員，當您已擁有 hello 的許多資料庫相同的存取需求，但您不想 toospend 個別設定每個資料庫的時間。

SQL Database 的預設來源 IP 位址限制會允許來自任何 Azure 位址 (包括其他訂用帳戶和租用戶) 的存取。 您可以限制此 tooonly 允許您 IP 位址 tooaccess hello 執行個體。 即使在有 SQL 防火牆和 IP 位址限制的情況下，仍然需要增強式驗證。 請參閱 hello 稍早在本文中所提供的建議。

toolearn 深入了解 Azure SQL 防火牆和 IP 限制，請參閱：

- [Azure SQL Database 存取控制](../sql-database/sql-database-control-access.md)
- [設定 Azure SQL Database 防火牆規則 - 概觀](../sql-database/sql-database-firewall-configure.md)
- [設定使用 hello Azure 入口網站的 Azure SQL Database 伺服器層級防火牆規則](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>待用資料加密
[透明資料加密 (TDE)](https://msdn.microsoft.com/library/azure/bb934049) 預設為啟用。 TDE 會透明加密 SQL Server、Azure SQL Database 和 Azure SQL 資料倉儲資料和記錄檔。 TDE 會保護免於遭受洩露的直接存取 toohello 檔案或其備份。 這可讓您在靜止 tooencrypt 資料而不需要變更現有的應用程式。 TDE 一律保持啟用。不過，這不會停止攻擊者使用 hello 一般存取路徑。 TDE 會提供許多的法律、 規定與方針各種產業中建立與 hello 能力 toocomply。

Azure SQL 會管理 TDE 的金鑰相關問題。 Tde，在內部部署特殊必須特別小心 tooensure 復原能力，移動資料庫時。 在更複雜的情況下，hello 金鑰可以明確地管理 Azure 金鑰保存庫中透過可延伸金鑰管理 (請參閱[SQL Server 使用 EKM 啟用 TDE](/security/encryption/enable-tde-on-sql-server-using-ekm))。 也可以透過 Azure Key Vault BYOK 功能，實行自備金鑰 (BYOK)。

Azure SQL 可透過 [Always Encrypted](/sql/relational-databases/security/encryption/always-encrypted-database-engine) 提供資料行加密。 這可讓只有獲得授權的應用程式存取 toosensitive 資料行。 使用這類加密限於 SQL 查詢加密資料行 tooequality 為基礎的值。

應用程式層級加密也應該用於選擇性資料。 加密的資料保留在 hello 正確的國家/地區中的索引鍵有時可以減輕資料 sovereignty 考量。 這可防止甚至意外的資料傳輸造成問題，因為它是不可能 toodecrypt hello hello 索引鍵，假設較強的演算法沒有資料的使用 （例如 AES 256)。

您可以使用額外的預防措施 toohelp 安全 hello 資料庫，例如設計安全的系統、 加密機密的資產，以及 hello 資料庫伺服器周圍建立防火牆。

## <a name="next-steps"></a>後續步驟
本文介紹您 tooa 集合的 SQL Database 和 SQL 資料倉儲安全性最佳作法來保護您的 PaaS web 與行動應用程式。 toolearn 深入了解保護您的 PaaS 部署，請參閱：

- [保護 PaaS 部署](security-paas-deployments.md)
- [使用 Azure App Service 來保護 PaaS Web 與行動應用程式](security-paas-applications-using-app-services.md)
