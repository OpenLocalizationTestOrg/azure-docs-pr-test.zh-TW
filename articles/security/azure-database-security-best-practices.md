---
title: "aaaAzure 資料庫安全性最佳作法 |Microsoft 文件"
description: "本文章提供一組 Azure 資料庫安全性的最佳做法。"
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: tomsh
ms.openlocfilehash: 78984291e8f74879c7f738e2ce3176c4be18d154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-best-practices"></a>Azure 資料庫安全性最佳做法

安全性是管理資料庫時的最重要考量，而且向來一直是 Azure SQL Database 的優先考量。 您的資料庫可以是緊密安全的 toohelp 滿足最法規或安全性需求，包括 HIPAA、 ISO 27001/27002 和 PCI DSS 層級 1、 和其他項目。 目前的安全性相容性認證清單位於 hello [Microsoft 信任中心網站](http://azure.microsoft.com/support/trust-center/services/)。 您也可以選擇您的資料庫中特定的 Azure 資料中心根據法規 tooplace。

本文將討論 Azure 資料庫安全性最佳做法的集合。 這些最佳作法與 Azure 的資料庫安全性衍生自我們的經驗，hello 經驗的客戶想自己。

針對每個最佳做法，我們會說明︰

-   哪些 hello 最佳作法是
-   為什麼要 tooenable 該最佳作法
-   如果您無法 tooenable hello 最佳作法，可能 hello 結果
-   如何了解 tooenable hello 最佳作法

本文的 Azure 資料庫的安全性最佳作法根據共識意見和 Azure 平台功能與功能設定存在於 hello 撰寫本文時的時間。 隨時間變更的意見和技術，且這篇文章會定期 tooreflect 上更新這些變更。

本文討論的 Azure 資料庫安全性最佳做法包括︰

-   使用防火牆規則 toorestrict 資料庫存取權
-   啟用資料庫驗證
-   使用加密來保護您的資料
-   保護傳輸中的資料
-   啟用資料庫稽核
-   啟用資料庫威脅偵測


## <a name="use-firewall-rules-toorestrict-database-access"></a>使用防火牆規則 toorestrict 資料庫存取權

Microsoft Azure SQL Database 為 Azure 和其他網際網路式應用程式提供關聯式資料庫服務。 tooprovide 存取安全性，SQL Database 與防火牆規則，以限制連線 IP 位址驗證機制需要使用者 tooprove 控制存取他們的身分識別和授權機制限制使用者 toospecific 動作和資料。 防火牆會阻止所有存取 tooyour 資料庫伺服器，直到您指定哪些電腦有權限。 hello 防火牆會授與存取 toodatabases hello 來自每個要求的 IP 位址為基礎。

![防火牆規則](./media/azure-database-security-best-practices/azure-database-security-best-practices-Fig1.png)

hello Azure SQL Database 服務僅透過 TCP 通訊埠 1433年提供。 tooaccess SQL 資料庫，從您的電腦，請確定您的用戶端電腦防火牆允許 TCP 通訊埠 1433年上的傳出 TCP 通訊。 如果其他應用程式不需要，請使用防火牆規則來封鎖 TCP 通訊埠 1433 的傳入連線。

Hello 連線程序的一部分，從 Azure 虛擬機器的連線會重新導向的 tooa 不同的 IP 位址和連接埠，唯一的每個工作者角色。 hello 連接埠號碼是在 11000 too11999 hello 範圍。 如需 TCP 連接埠的詳細資訊，請參閱[適用於 ADO.NET 4.5 及 SQL Database 的 1433 以外的連接埠](https://docs.microsoft.com/azure/sql-database/sql-database-develop-direct-route-ports-adonet-v12)。

> [!Note]
> 如需 SQL Database 中防火牆規則的詳細資訊，請參閱 [SQL Database 防火牆規則](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)。

## <a name="enable-database-authentication"></a>啟用資料庫驗證
SQL Database 支援兩種類型的驗證，SQL 驗證和 Azure Active Directory 驗證 (Azure AD 驗證)。

下列情況下，建議使用 **SQL 驗證**：

-   它可讓 SQL Azure toosupport 環境具有混合作業系統，其中所有使用者無法都驗證 Windows 網域。
-   允許 SQL Azure toosupport 舊版應用程式和應用程式需要 SQL Server 驗證的協力廠商所提供。
-   可讓使用者從未知或不受信任網域的 tooconnect。 例如，既有客戶連接與應用程式指定 SQL Server 登入 tooreceive hello 訂單狀態。
-   可讓 SQL Azure toosupport Web 應用程式讓使用者建立自己的識別。
-   可讓軟體開發人員 toodistribute 使用複雜的權限階層其應用程式根據已知，預設 SQL Server 登入。

> [!Note]
> 不過，SQL Server 驗證無法使用 Kerberos 安全性通訊協定。

如果您是使用 **SQL 驗證**，就必須：

-   自行管理 hello 強式認證。
-   保護 hello hello 連接字串中的憑證。
-   （可能） 來保護從 hello Web server toohello 資料庫 hello 網路上傳送的 hello 認證。 如需詳細資訊，請參閱[如何： 連接 tooSQL Server ASP.NET 2.0 中，使用 SQL 驗證](https://msdn.microsoft.com/library/ms998300.aspx)。

**Azure Active Directory 驗證**是一項機制的連接 tooMicrosoft Azure SQL Database 和[SQL 資料倉儲](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)使用 Azure Active Directory (Azure AD) 中的身分識別。 使用 Azure AD 驗證時，您可以集中管理 hello 的資料庫使用者的身分識別和其他 Microsoft 服務在單一中央位置。 中央識別碼管理 toomanage 資料庫使用者提供單一位置，並簡化權限管理。 優點 hello 如下：

-   它提供替代 tooSQL 伺服器驗證。
-   可協助停止使用者身分識別的 hello 的擴散到資料庫伺服器。
-   允許在單一位置變換密碼。
-   客戶可以管理使用外部 (AAD) 群組的資料庫權限。
-   它可以藉由啟用整合式 Windows 驗證和 Azure Active Directory 支援的其他形式驗證來避免儲存密碼。
-   Azure AD 驗證在 hello 資料庫層級，使用自主的資料庫使用者 tooauthenticate 身分識別。
-   Azure AD 支援連接 tooSQL 資料庫應用程式的權杖為基礎的驗證。
-   Azure AD 驗證本機 Azure Active Directory 的 ADFS (網域同盟) 或原生使用者/密碼驗證，而不需進行網域同步處理。
-   Azure AD 支援來自 SQL Server Management Studio 的連線，其中使用包含 Multi-Factor Authentication (MFA) 的 Active Directory 通用驗證。 MFA 包含增強式驗證功能，其中提供一系列簡易的驗證選項，例如電話、簡訊、含有 PIN 的智慧卡或行動應用程式通知。 如需詳細資訊，請參閱 [適用於與 SQL Database 和 SQL 資料倉儲搭配使用之 Azure AD MFA 的 SSMS 支援](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。

hello 組態步驟包含下列程序 tooconfigure hello，並使用 Azure Active Directory 驗證。

-   建立和填入 Azure AD。
-   選擇性： 產生關聯，或變更 hello 目前與 Azure 訂用帳戶相關聯的 active directory。
-   建立 Azure SQL 伺服器或 [Azure SQL 資料倉儲](https://azure.microsoft.com/services/sql-data-warehouse/)的 Azure Active Directory 系統管理員。
- 設定用戶端電腦。
-   在對應資料庫 tooAzure AD 身分識別建立自主的資料庫使用者。
-   使用 Azure AD 識別身分，連接 tooyour 資料庫。

您可以在[這裡](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)找到詳細資訊。

## <a name="protect-your-data-using-encryption"></a>使用加密來保護您的資料

[Azure SQL Database 透明資料加密 (TDE)](https://msdn.microsoft.com/library/dn948096.aspx)有助於保護 hello 威脅惡意活動所執行的即時加密與解密的 hello 資料庫相關聯的備份和交易記錄檔不含靜止需要變更 toohello 應用程式。 TDE 會使用對稱金鑰的呼叫的 hello 資料庫加密金鑰將整個資料庫的 hello 儲存體。

Hello 整個儲存已加密，即使它是非常重要 tooalso 加密資料庫本身。 這是 hello 防禦保護資料的深度方法的實作。 如果您使用 Azure SQL Database，並想 tooprotect 敏感性資料，例如信用卡或身分證號碼，您可以加密的資料庫與 FIPS 140-2 驗證 256 位元 AES 加密符合許多業界標準 (例如，HIPAA 的 hello 要求PCI）)。

很重要檔案的 toounderstand 太相關[緩衝集區擴充 (BPE)](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension)使用 TDE 加密資料庫時，不會加密。 您必須使用檔案系統層級加密工具[BitLocker](https://technet.microsoft.com/library/cc732774)或 hello[加密檔案系統 (EFS)](https://technet.microsoft.com/library/cc700811.aspx)針對 BPE 相關檔案。

因為授權的使用者等安全性系統管理員或資料庫管理員可以存取 hello 資料即使 hello 資料庫經過加密與 TDE，您也應該遵循下列的 hello 建議：

-   啟用 hello 資料庫層級 SQL 驗證。
-   使用 [RBAC 角色](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)的 Azure AD 驗證。
-   使用者和應用程式應該使用不同的帳戶 tooauthenticate。 如此一來您可以限制 hello toousers 和應用程式授與的權限，並降低 hello 風險的惡意活動。
-   實作資料庫層級安全性使用固定的資料庫角色 （例如 db_datareader 或 db_datawriter），或者您可以建立自訂角色的應用程式 toogrant 明確權限 tooselected 資料庫物件。

其他方式 tooencrypt 您的資料，請考慮：

-   [資料格層級加密](https://msdn.microsoft.com/library/ms179331.aspx)tooencrypt 特定資料行或甚至是資料格具有不同的加密金鑰的資料。
-   使用 永遠加密的使用中的加密：[永遠加密](https://msdn.microsoft.com/library/mt163865.aspx)可讓用戶端 tooencrypt 敏感性資料用戶端應用程式內，但絕不會顯示 hello 加密金鑰 toohello Database Engine （SQL Database 或 SQL Server）。 如此一來，「 永遠加密 」 的區隔擁有者 hello 資料 （且可以檢視） 和管理者 hello 資料 （但應該不具備存取權）。
-   使用資料列層級安全性： 資料列層級安全性可讓客戶 toocontrol 存取 toorows 根據 hello 特性 hello 使用者執行查詢 （例如，群組成員資格或執行內容） 的資料庫資料表中。 如需詳細資訊，請參閱[資料列層級安全性](https://msdn.microsoft.com/library/dn765131)。

## <a name="protect-data-in-transit"></a>保護傳輸中的資料
保護傳輸中的資料應該是您的資料保護策略中不可或缺的部分。 因為資料會從許多位置來回移動，hello 一般建議您一律使用 SSL/TLS 通訊協定 tooexchange 資料分散在不同的位置。 在某些情況下，您可能想 tooisolate hello 整個通訊通道，您的內部部署與雲端之間使用虛擬私人網路 (VPN) 的基礎結構。

對於在內部部署基礎結構與 Azure 之間移動的資料，您應該考慮適當的防護措施，例如 HTTPS 或 VPN。

針對需要從多個工作站位在內部 tooAzure toosecure 存取的組織，使用[Azure 站台對站 VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create)。

需要 toosecure 的組織從位於個別的工作站存取內部或外部部署 tooAzure，請考慮使用[點對站 VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create)。

較大的資料集可以透過專用的高速 WAN 連結 (例如 [ExpressRoute](https://azure.microsoft.com/services/expressroute/)) 移動。 如果您選擇 toouse ExpressRoute，您也可以加密 hello 資料在 hello 應用程式層級使用[SSL/TLS](https://support.microsoft.com/kb/257591)或為了提高保護其他通訊協定。

如果透過 hello Azure 網站互動與 Azure 儲存體，所有交易將會透過 HTTPS 都發生。 [儲存體 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)透過 HTTPS 也可以與使用的 toointeract [Azure 儲存體](https://azure.microsoft.com/services/storage/)和[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。

失敗 tooprotect 資料在傳輸過程中的組織就更容易受到如[攔截攻擊](https://technet.microsoft.com/library/gg195821.aspx)，[竊聽](https://technet.microsoft.com/library/gg195641.aspx)和工作階段攔截。 Hello 第一個步驟中獲得存取 tooconfidential 資料時，可以是這些攻擊。

深入了解 Azure VPN 選項，藉由讀取 hello 文章 toolearn[規劃和設計 VPN 閘道](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-plan-design)。

## <a name="enable-database-auditing"></a>啟用資料庫稽核
稽核 SQL Server Database Engine hello 或個別資料庫的執行個體牽涉到追蹤和記錄 hello 資料庫引擎發生的事件。 SQL Server 稽核可讓您建立伺服器稽核，其中可能包含伺服器等級事件的伺服器稽核規格，以及資料庫等級事件的資料庫稽核規格。 可以稽核的事件寫入 toohello 事件記錄檔或 tooaudit 檔案。

根據管制或安裝的標準需求而定，會有數個 SQL Server 的稽核等級。 SQL Server Audit 提供 hello 工具和程序，您必須擁有 tooenable、 市集和稽核檢視各種伺服器和資料庫物件。

[Azure SQL Database 稽核](https://docs.microsoft.com/azure/sql-database/sql-database-auditing)追蹤資料庫事件並將事件寫入 Azure 儲存體帳戶中 tooan 稽核記錄檔。

稽核可協助您保持法規遵循、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。

稽核可讓和有助於遵循 toocompliance 標準但並不保證相容性。

深入了解資料庫稽核 toolearn 和如何 tooenable，請閱讀 hello 文章[啟用 Azure 資訊安全中心中的 SQL 伺服器上的稽核和威脅偵測](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers)。

## <a name="enable-database-threat-detection"></a>啟用資料庫威脅偵測
SQL 威脅偵測可讓您 toodetect，以及藉由提供異常活動的安全性警示發生時，回應 toopotential 威脅。 一旦有可疑活動、潛在弱點、SQL 插入式攻擊和異常資料庫存取模式發生時，您將會收到警示。 SQL 威脅偵測警示提供可疑活動的詳細資訊和建議動作如何 tooinvestigate 和降低 hello 威脅。

例如，SQL 資料隱碼是 hello 一般 Web 應用程式安全性問題 hello 網際網路，使用的 tooattack 資料導向應用程式上的其中一個。 攻擊者利用的應用程式的弱點可能會 tooinject 惡意的 SQL 陳述式到應用程式項目欄位中，違反或修改 hello 資料庫中的資料。

有關如何 toolearn 威脅偵測功能為您的資料庫，在 Azure 入口網站，請參閱 hello tooset [SQL Database 威脅偵測](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection)。

此外，SQL 威脅偵測將自有的警示與 [Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)整合。 我們邀請您 tootry 它 60 天的免費。

深入了解 Database 威脅偵測 toolearn 和如何 tooenable，請閱讀 hello 文章[啟用 Azure 資訊安全中心中的 SQL 伺服器上的稽核和威脅偵測](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers)。

## <a name="conclusion"></a>結論
Azure 資料庫是強固的資料庫平台，具有完整的安全性功能，能符合許多組織及法務相容性需求。 您可以協助控制 tooyour hello 實體存取的資料，及使用各種不同的選項，提供在 hello 檔案-資料行，或使用透明資料加密、 資料格層級加密或資料列層級安全性的資料列層級的資料安全性來保護資料。 永遠加密也可讓您操作對加密資料，簡化的應用程式更新的 hello 程序。 接著，存取 tooauditing 活動會提供您的需要可讓您存取資料的方式和時機的 tooknow hello 資訊的 SQL 資料庫記錄。

## <a name="next-steps"></a>後續步驟
- toolearn 進一步了解防火牆規則，請參閱[防火牆規則](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)。
- toolearn 有關使用者和登入，請參閱[管理登入](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)。
- 如需教學課程，請參閱[保護 Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial)。
