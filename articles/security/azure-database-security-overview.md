---
title: "aaaAzure 資料庫安全性概觀 |Microsoft 文件"
description: "本文章提供 hello Azure 資料庫的安全性功能的概觀。"
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Azure 資料庫安全性概觀

安全性是管理資料庫時的最重要考量，而且向來一直是 Azure SQL Database 的優先考量。 Azure SQL Database 支援使用防火牆規則和連線加密的連線安全性。 它支援使用者名稱和密碼驗證以及 Azure Active Directory 驗證，後者使用由 Azure Active Directory 管理的身分識別。 授權使用角色型存取控制。

Azure SQL Database 支援藉由執行而不需要變更 toohello 應用程式的即時加密與解密的資料庫、 相關聯的備份和交易記錄檔在靜止的加密。

Microsoft 提供的其他方法 tooencrypt 企業資料：

-   資料格層級加密 tooencrypt 特定資料行或資料的儲存格也使用不同的加密金鑰。
-   如果您需要硬體安全模組或集中管理您的加密金鑰階層，請考慮在 Azure VM 中使用 Azure Key Vault 搭配 SQL Server。
-   一律加密 （目前處於預覽階段） 加密透明 tooapplications 並可讓用戶端 tooencrypt 用戶端應用程式內的機密資料，而不需要使用 SQL Database 共用 hello 加密金鑰。

Azure SQL Database 稽核可讓企業 toorecord 事件 tooan 稽核登入 Azure 儲存體。 SQL Database 稽核也會整合 Microsoft Power BI toofacilitate 向下鑽研報表和分析。

 SQL Azure 資料庫可以緊密安全的 toosatisfy 最法規或安全性需求，包括 HIPAA、 ISO 27001/27002 和 PCI DSS 層級 1、 和其他項目。 目前的安全性相容性認證清單位於 hello [Microsoft Azure 信任中心網站](http://azure.microsoft.com/support/trust-center/services/)。

本文逐步 hello 的保護 Microsoft Azure SQL Database 的結構化，表格式和關聯式資料的基本概念。 本文尤其著重於協助您開始利用資源來保護資料、控制存取，以及進行主動式監視。

Azure 資料庫安全性概觀本文著重於 hello 下列區域：

-   保護資料
-   存取控制
-   主動監視
-   集中式安全性管理
-   Azure Marketplace

## <a name="protect-data"></a>保護資料

SQL Database 會使用[傳輸層安全性](https://support.microsoft.com/kb/3135244)為移動中的資料提供加密、使用[透明資料加密](http://go.microsoft.com/fwlink/?LinkId=526242)為待用資料提供加密，使用 [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) 為使用中的資料提供加密，進而保護您的資料。

在本節中，我們討論：

-   移動中加密
-   待用加密
-   使用中加密 (用戶端)

其他方式 tooencrypt 您的資料，請考慮：

-   [資料格層級加密](https://msdn.microsoft.com/library/ms179331.aspx)tooencrypt 特定資料行或甚至是資料格具有不同的加密金鑰的資料。
-   如果您需要硬體安全性模組或集中管理您的加密金鑰階層，請考慮 [在 Azure VM 中使用 Azure 金鑰保存庫搭配 SQL Server](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx)。

### <a name="encryption-in-motion"></a>移動中加密

常見的問題，所有用戶端/伺服器應用程式資料移至公用及私人網路為 hello 隱私權需求。 如果未加密透過網路移動資料，但沒有 hello 機率，可以擷取該資料並遭竊未經授權的使用者。 當處理資料庫服務，您會需要 toomake 確定 hello 資料庫用戶端與伺服器之間，以及資料庫的伺服器之間進行通訊與彼此、 與中介層應用程式資料都會經過加密。

當您管理網路時，其中一個問題就是保護在不受信任網路上的應用程式之間傳送的資料。 您可以使用[TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate 伺服器和用戶端，然後使用它 tooencrypt hello 驗證合作對象之間的訊息。

Hello 驗證程序，TLS/SSL 用戶端傳送訊息 tooa TLS/SSL 伺服器，且 hello 伺服器會回應 hello hello 伺服器需要 tooauthenticate 本身的資訊。 hello 用戶端與伺服器執行其他工作階段金鑰交換和 hello 驗證對話方塊結束。 完成驗證之後，可以開始 hello 伺服器和使用 hello hello 驗證程序期間建立的對稱式加密金鑰的 hello 用戶端之間的 SSL 安全保護的通訊。

所有連線 tooAzure SQL 資料庫都需要加密 (SSL/TLS) 在所有時間資料從 hello 資料庫的 「 在傳輸"tooand 時發生。 SQL Azure 使用 TLS/SSL tooauthenticate 伺服器和用戶端，然後再使用它 tooencrypt hello 驗證合作對象之間的訊息。 在您的應用程式連接字串中，您必須指定參數 tooencrypt hello 連接和不 tootrust hello 伺服器憑證 （這基於您如果複製您的連接字串，超出 hello Azure 傳統入口網站），否則 hello 連線將驗證 hello 伺服器 hello 身分識別，且會受到影響太"中--攔截 」 攻擊。 Hello ADO.NET 驅動程式，比方說，這些連接字串參數為 Encrypt = True 和 TrustServerCertificate = False。

### <a name="encryption-at-rest"></a>待用加密
您可以採取幾個預防措施 toohelp 安全 hello 資料庫，例如設計安全的系統、 加密機密的資產，以及 hello 資料庫伺服器周圍建立防火牆。 不過，在此案例中 hello 實體媒體 （例如磁碟機或備份磁帶） 遭竊的地方，惡意的合作對象可以只還原或附加 hello 資料庫並瀏覽 hello 資料。

其中一種解決方案是在資料庫中的 hello tooencrypt hello 機密資料，並保護 hello 索引鍵，則使用的 tooencrypt hello 資料使用的憑證。 這可防止沒有 hello 索引鍵的任何人使用 hello 資料，但這種防護類型必須規劃。

這個問題，SQL Server 和 Azure SQL 支援的 toosolve[透明資料加密 (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde)。 TDE 會加密 SQL Server 和 Azure SQL Database 資料檔案，也稱為待用資料加密。

Azure SQL Database 的透明資料加密可協助防範惡意活動的 hello 威脅，藉由執行 hello 資料庫、 相關聯的備份和靜止的交易記錄檔的即時加密與解密，而不需要變更toohello 應用程式。  

TDE 會使用對稱金鑰的呼叫的 hello 資料庫加密金鑰將整個資料庫的 hello 儲存體。 SQL Database 中 hello 資料庫加密金鑰受到由內建的伺服器憑證。 hello 內建伺服器憑證是唯一的每個 SQL Database 伺服器。

如果資料庫在 GeoDR 關聯性中，則是由每部伺服器上的不同金鑰保護。 如果兩個資料庫連接的 toohello 它們共用相同的伺服器 hello 同一個內建的憑證。 Microsoft 至少每 90 天會自動替換這些憑證。 如需 TDE 的一般描述，請參閱 [透明資料加密 (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde)。

### <a name="encryption-in-use-client"></a>使用中加密 (用戶端)

大部分資料缺口，這牽涉到 hello 竊取的重要資料，例如信用卡號碼或個人識別資訊。 資料庫可能富藏機密資訊。 其中可能包含客戶的個人資料、具競爭力的機密資訊及智慧財產權。 資料遺失或遭竊，特別是客戶資料，可能會導致品牌受損、競爭不利及大量罰金，甚至是訴訟。

![一律加密](./media/azure-databse-security-overview/azure-database-fig1.png)

[永遠加密](https://msdn.microsoft.com/library/mt163865.aspx)是設計的功能 tooprotect 機密資料，像是信用卡號碼或國家身分證字號 （例如美國社會安全號碼），儲存在 Azure SQL Database 或 SQL Server 資料庫中。 一律加密可讓用戶端 tooencrypt 用戶端應用程式內的機密資料，並永遠不會顯示 hello 加密金鑰 toohello Database Engine （SQL Database 或 SQL Server）。

永遠加密提供者擁有 hello 資料 （且可以檢視） 之間的區隔和管理者 hello 資料 （但應該不具備存取權）。 透過確定內部部署資料庫系統管理員，雲端資料庫操作員，或其他具備高權限但未經授權的使用者無法存取加密的 hello 資料

此外，永遠加密可讓加密透明 tooapplications。 啟用永遠加密的驅動程式安裝在 hello 用戶端電腦上，使其自動加密和解密 hello 用戶端應用程式中的機密資料。 hello 驅動程式會傳送嗨資料 toohello Database Engine 之前加密敏感資料行中的 hello 資料，並保留 hello 語意 toohello 應用程式的自動重寫查詢。 同樣地，hello 驅動程式會明確地解密儲存在加密的資料庫資料行，查詢結果中的資料。

## <a name="access-control"></a>存取控制
tooprovide 安全性，SQL Database 與防火牆規則，以限制連線 IP 位址驗證機制需要使用者 tooprove 控制存取他們的身分識別和授權機制限制使用者 toospecific 動作和資料。

### <a name="database-access"></a>資料庫存取

與可控制存取 tooyour 資料會開始資料保護。 hello 資料中心裝載您的資料管理的實體存取，雖然您可以設定防火牆 toomanage 安全性 hello 網路層級。 您也可以藉由設定驗證登入，並定義伺服器和資料庫角色的權限，來控制存取。

在本節中，我們討論：

-   防火牆與防火牆規則
-   驗證
-   Authorization

#### <a name="firewall-and-firewall-rules"></a>防火牆與防火牆規則

Microsoft Azure SQL Database 為 Azure 和其他網際網路式應用程式提供關聯式資料庫服務。 toohelp 保護您的資料，防火牆會阻止所有存取 tooyour 資料庫伺服器，直到您指定哪些電腦有權限。 hello 防火牆會授與存取 toodatabases hello 來自每個要求的 IP 位址為基礎。 如需詳細資訊，請參閱 [Azure SQL Database 防火牆規則概觀](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)。

hello [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)服務僅透過 TCP 通訊埠 1433年提供。 tooaccess SQL 資料庫，從您的電腦，請確定您的用戶端電腦防火牆允許 TCP 通訊埠 1433年上的傳出 TCP 通訊。 如果其他應用程式不需要，請封鎖 TCP 通訊埠 1433 的傳入連線。

#### <a name="authentication"></a>驗證

SQL database 驗證是指 toohow 連接 toohello 資料庫時，證明您的身分識別。 SQL Database 支援兩種驗證類型：

-   **SQL 驗證：**建立的邏輯 SQL 執行個體時，呼叫 hello SQL 資料庫的訂閱者帳戶，會建立單一登入帳戶。 此帳戶會使用 [SQL Server 驗證](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview) (使用者名稱和密碼) 連線。 此帳戶是系統管理員 hello 邏輯伺服器執行個體以及所有使用者資料庫會附加 toothat 執行個體。 hello hello 「 訂閱者 」 帳戶權限不能限制。 只有其中一個帳戶可以存在。
-   **Azure Active Directory 驗證：** [Azure Active Directory 驗證](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)是一種機制，利用 Azure Active Directory （身分識別連接 tooMicrosoft Azure SQL Database 和 SQL 資料倉儲Azure AD)。 這樣做可讓您 toocentrally 管理的資料庫使用者的身分識別。

![驗證](./media/azure-databse-security-overview/azure-database-fig2.png)

 Azure Active Directory 驗證的優點包括：
  - 它提供替代 tooSQL 伺服器驗證。
  - 它也有助於阻止的使用者身分識別的 hello 擴散到資料庫伺服器 （& s) 允許在單一位置的密碼旋轉。
  - 您可以管理使用外部 (Azure Active Directory) 群組的資料庫權限。
  - 它可以藉由啟用整合式 Windows 驗證和 Azure Active Directory 支援的其他形式驗證來避免儲存密碼。

#### <a name="authorization"></a>Authorization
[授權](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)參考 toowhat 使用者可以在 Azure SQL Database 中執行，這由您的使用者帳戶資料庫[角色成員資格](https://msdn.microsoft.com/library/ms189121)和[物件層級權限](https://msdn.microsoft.com/library/ms191291.aspx)。 授權是 hello 程序可決定哪些安全性實體的資源，主體可存取，以及哪些作業允許針對這些資源。

### <a name="application-access"></a>應用程式存取

在本節中，我們討論：

-   動態資料遮罩
-   資料列層級安全性

#### <a name="dynamic-data-masking"></a>動態資料遮罩
撥接中心的服務代表可能會找出呼叫者的社會安全號碼或信用卡號碼其中幾個數字，但這些項目不應該是完整的資料公開 toohello 服務人員。

所有的遮罩，但 hello 最後四位數的任何社會安全號碼或信用卡號碼 hello 結果集中的任何查詢可以定義遮罩規則。

![動態資料遮罩](./media/azure-databse-security-overview/azure-database-fig3.png)

另舉一例，適當的資料遮罩可以是定義的 tooprotect 個人識別資訊 (PII) 資料，以便開發人員可以查詢生產環境，供疑難排解之用，而不會違反法務遵循規定。

[SQL 資料庫動態資料遮罩](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started)會限制機密資料暴露其 toonon 權限的使用者。 Hello Azure SQL Database V12 版支援動態資料遮罩。

[動態資料遮罩](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking)有助於防止未經授權的存取 toosensitive 資料，讓您 toodesignate 多少 hello 敏感性資料 tooreveal hello 應用程式層上的影響降至最低。 這是 hello hello 查詢結果集內的機密資料隱藏在指定的資料庫欄位，而 hello 資料庫中的 hello 資料不會變更以原則為基礎的安全性功能。


> [!Note]
> Hello Azure 資料庫系統管理員、 伺服器管理員或安全性主管人員角色可以設定動態資料遮罩。

#### <a name="row-level-security"></a>資料列層級安全性
多租用戶資料庫的另一個常見安全性需求是[資料列層級安全性](https://msdn.microsoft.com/library/dn765131.aspx)。 這項功能可讓您將存取 toorows toocontrol 根據 hello 特性 hello 使用者執行查詢 （例如，群組成員資格或執行內容） 的資料庫資料表中。

![資料列層級安全性](./media/azure-databse-security-overview/azure-database-fig4.png)

hello 存取限制邏輯是位於 hello 資料庫層，而不是離開 hello 資料，另一個應用程式層。 hello 資料庫系統會在每次從任何層嘗試存取該資料套用 hello 存取限制。 這讓您安全性系統更可靠且健全透過減少安全性系統的 hello 介面區。

資料列層級安全性引進述詞型存取控制。 其特色為彈性、 集中式、 述詞架構評估，可以考量中繼資料或其他 hello 系統管理員決定的準則依適當情況。 hello 述詞作為準則 toodetermine hello 使用者有 hello 適當的存取權 toohello 資料是根據使用者屬性。 標籤型存取控制可透過述詞型存取控制來實作。

## <a name="proactive-monitoring"></a>主動監視
SQL Database 可藉由提供**稽核**和**威脅偵測**功能來保護您的資料。

### <a name="auditing"></a>稽核
SQL Database 稽核會增加您能力 toogain 深入了解事件以及 hello 資料庫，包括更新和查詢 hello 資料內所發生的變更。

[Azure SQL Database 稽核](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started)追蹤資料庫事件並將事件寫入 Azure 儲存體帳戶中 tooan 稽核記錄檔。 稽核可協助您保持法規遵循、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。 稽核可讓和有助於遵循 toocompliance 標準但並不保證相容性。

SQL Database 稽核可讓您：

-   **保留** 所選事件的稽核記錄。 您可以定義資料庫動作 toobe 稽核的類別。
-   **報告** 資料庫活動。 您可以使用預先設定的報表和儀表板 tooget 快速地開始使用活動和事件報告。
-   **分析** 報告。 您可以尋找可疑事件、異常活動及趨勢。

稽核方法有兩種：

-   **Blob 稽核**-記錄檔寫入 tooAzure Blob 儲存體。 這是一個較新的稽核方法，可提供更高效能、支援更高資料粒度物件層級稽核，以及更符合成本效益。
-   **資料表稽核**-記錄檔寫入 tooAzure 資料表儲存體。

### <a name="threat-detection"></a>威脅偵測
[Azure SQL Database 威脅偵測](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection)會偵測可疑的活動，指出潛在的安全性威脅。 威脅偵測可讓您在 hello 資料庫，SQL 資料隱碼攻擊，例如 toorespond toosuspicious 事件發生時。 它會發出警示，並允許 hello 使用 Azure SQL Database 稽核 tooexplore hello 可疑事件。

![威脅偵測](./media/azure-databse-security-overview/azure-database-fig5.jpg)

例如，SQL 資料隱碼是 hello 一般 Web 應用程式安全性問題 hello 網際網路，使用的 tooattack 資料導向應用程式上的其中一個。 攻擊者利用的應用程式的弱點可能會 tooinject 惡意的 SQL 陳述式到應用程式項目欄位中，違反或修改 hello 資料庫中的資料。

資訊安全人員或其他指定的系統管理員可以在發生可疑的資料庫活動時立即取得通知。 每個通知提供 hello 可疑活動的詳細資料，並建議 toofurther 調查並降低 hello 威脅的方式。        

## <a name="centralized-security-management"></a>集中式安全性管理

[Azure 資訊安全中心](https://azure.microsoft.com/documentation/services/security-center/)可協助您防止、 偵測，並回應 toothreats。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

[資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-sql-database)可協助您藉由提供可見性的所有伺服器和資料庫的 hello 安全性保護 SQL 資料庫中的資料。 使用資訊安全中心，您可以︰

-   定義 SQL Database 加密和稽核原則。
-   監視 SQL Database 資源 hello 安全性在所有訂閱。
-   快速找出並修復安全性問題。
-   整合 [Azure SQL Database 威脅偵測](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection)所提供的警示。
-   資訊安全中心支援角色型存取。

## <a name="azure-marketplace"></a>Azure Marketplace

hello Azure Marketplace 是啟用創和獨立軟體廠商 (Isv) toooffer 解決方案 tooAzure 客戶 hello 世界各地的線上應用程式和服務 marketplace。
hello Azure Marketplace 結合成單一、 統一的平台 toobetter Microsoft Azure 合作夥伴生態系統提供我們的客戶和合作夥伴。 按一下[這裡](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1)tooglance Azure 商場上可用的資料庫安全性產品。

## <a name="next-steps"></a>後續步驟

- 深入了解如何[保護 Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial)。
- 深入了解 [Azure 資訊安全中心和 Azure SQL Database 服務](https://docs.microsoft.com/azure/security-center/security-center-sql-database)。
- toolearn 進一步了解威脅偵測，請參閱[SQL Database 威脅偵測](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection)。
- 詳細資訊，請參閱 toolearn[改善 SQL database 效能](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial)。 
