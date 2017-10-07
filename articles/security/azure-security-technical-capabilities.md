---
title: "aaaAzure 安全技術功能 |Microsoft 文件"
description: "深入了解雲端運算服務，其中包含寬的選取範圍的計算執行個體 （& s） 可以自動 toomeet hello 需求的應用程式或企業上下調整的服務。"
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
ms.date: 05/26/2017
ms.author: TomSh
ms.openlocfilehash: a0ef17883be54dab4cb6b597204f3197dc05c28c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-technical-capabilities"></a>Azure 安全性技術功能

了解 tooassist 目前和預期 Azure 客戶，並利用 hello 各種安全性相關功能中提供和周圍 hello Azure 平台，Microsoft 開發了一系列的技術白皮書、 安全性概觀、 最佳作法，並檢查清單。 hello 廣度及深度方面的主題範圍，並定期更新。 這份文件摘要 hello 抽象下一節中為該系列的一部分。 如果您需要關於此 Azure 安全性系列的進一步資訊，您可以在 (URL) 找到。

## <a name="azure-platform"></a>Azure 平台

[Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/) 是一個由基礎結構和應用程式服務所組成的雲端平台，內含整合式資料服務與進階分析以及開發人員工具和服務，並裝載在 Microsoft 的公用雲端資料中心內。 客戶使用 Azure 的許多不同容量與案例中的，從基本運算、 網路及存放裝置，toomobile 和 web 應用程式服務，例如物聯網 toofull 雲端案例和可開放原始碼技術搭配使用，並為混合式部署雲端部署或託管客戶的資料中心內。 Azure 提供雲端技術的建置組塊 toohelp 公司節省成本、 快速、 創新和主動管理系統。 當您建置，或移轉 IT 資產 tooa 雲端提供者時，您依賴在該組織的能力 tooprotect 應用程式和 hello 服務與 hello 控制項提供您以雲端為基礎的資產的 toomanage hello 安全性資料。

Microsoft Azure 是複雜性的 hello 唯一雲端運算的提供者可提供安全且一致的應用程式平台和基礎結構做為-服務的小組 toowork 內其不同的雲端熟練度和層級專案，使用整合式資料服務和分析，只要存在，跨 Microsoft 和非 Microsoft 平台，可發現資料中的智慧開啟 架構和工具，提供整合雲端與內部部署以及部署 Azure 雲端服務內的選擇在內部部署資料中心。 Hello Microsoft 信任雲端的一部分，客戶依賴 Azure 的領先業界安全性、 可靠性、 相容性、 隱私權和 hello vast 網路的人員、 合作夥伴和處理序 toosupport 組織 hello 雲端中。

透過 Microsoft Azure，您可以：

- 可加速 hello 雲端與創新。

- 利用深入見解來支援商業決策和應用程式。

- 免費建置及隨處部署。

- 保護其業務。

## <a name="scope"></a>Scope

安全性功能和功能支援 Microsoft Azure 的核心元件，也就有關，本白皮書的 hello 連絡窗口[Microsoft Azure 儲存體](https://docs.microsoft.com/azure/storage/storage-introduction)， [Microsoft Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)，[Microsoft Azure 虛擬機器模型](https://docs.microsoft.com/azure/virtual-machines/  )，和 hello 工具和管理所有它的基礎結構。 這份技術白皮書著重在 Microsoft Azure 技術功能可用 tooyou 為客戶 toofulfil hello 安全性與隱私權的資料保護其角色。

hello 重要性的了解此模型中共同的責任是不可或缺的移動 toohello 雲端的客戶。 雲端提供者會提供相當多的優點，來提供安全性與相容性用途，但這些優點不會 absolve hello 客戶與保護他們的使用者、 應用程式和服務供應項目。

對於 IaaS 解決方案 hello 客戶負責或共用負責保護和管理 hello 作業系統、 網路設定、 應用程式、 識別、 用戶端，以及資料。  建置在 IaaS 部署中的 PaaS 解決方案，hello 客戶仍然負責或共用負責保護和管理應用程式、 識別、 用戶端，以及資料。 如需 SaaS 解決方案，Nonetheless，hello 客戶會繼續 toobe 負責。 它們必須確保資料的分類正確，且它們共用責任 toomanage 使用者與端點的裝置。

這份文件不提供任何 hello 詳細涵蓋範圍相關的 Microsoft Azure 平台元件，例如 Azure Web Sites、 Azure Active Directory、 HDInsight、 Media Services 和其他服務層在 hello 核心元件。 雖然我們只提供最低程度的一般資訊，但我們認為讀者應該已熟悉各項 Azure 基本概念 (如 Microsoft 所提供的其他參考資料所述以及本白皮書所提供之連結中所包含的概念)。


## <a name="available-security-technical-capabilities-toofulfil-user-customer-responsibility---big-picture"></a>可用的安全性技術功能 toofulfil 使用者 （客戶） 責任大的圖片

Microsoft Azure 提供服務，可協助客戶符合 hello 安全性、 隱私權和相容性需求。 hello 下列可協助說明各種可以使用適用於 Azure 服務使用者 toobuild 安全且相容的應用程式基礎結構會根據業界標準的圖片。

![可用的安全性技術功能 - 概略圖](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig1.png)

## <a name="manage-and-control-identity-and-user-access-protect"></a>管理和控制身分識別與使用者存取 (保護)

Azure 可協助您保護商務及個人資訊由啟用您 toomanage 使用者身分識別與認證及控制存取。

### <a name="azure-active-directory"></a>Azure Active Directory

Microsoft 身分識別和存取管理解決方案說明 IT 保護存取 tooapplications 及資源 hello 公司資料中心跨和進入 hello 雲端啟用驗證，例如多因素驗證和條件的額外層級存取原則。 透過進階的安全性報告、稽核和警示來監視可疑活動，有助於減緩潛在的安全性問題。 [Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-editions)提供雲端 (SaaS) 應用程式和執行在內部部署存取 tooweb 應用程式的單一登入 toothousands。

安全性優點的 Azure Active Directory (AD) 包括 hello 能力：

- 為您的混合式企業中的每位使用者建立和管理單一身分識別，讓使用者、群組和裝置保持同步。

- 提供單一登入存取 tooyour 應用程式包括數千個預先整合的 SaaS 應用程式。

- 藉由同時對內部部署和雲端應用程式強制以規則為基礎的 Multi-Factor Authentication，啟用應用程式存取安全性。

- 佈建的安全遠端存取 tooon 內部部署 web 應用程式可以透過 Azure AD Application Proxy。

[Azure Active Directory 入口網站](http://aad.portal.azure.com/)可作為 Azure 入口網站的一部分。 這個儀表板，您可以取得您組織的 hello 狀態的概觀，並輕鬆地深入了解管理 hello 目錄、 使用者或應用程式的存取。

![Azure Active Directory](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig2.png)

Azure 的身分識別管理核心功能如下︰

- 單一登入

- Multi-Factor Authentication

- 安全性監視、警示以及機器學習服務型報告

- 消費者身分識別與存取管理

- 裝置註冊

- Privileged Identity Management

- 身分識別保護

#### <a name="single-sign-on"></a>單一登入

[單一登入 (SSO)](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)意指要能 tooaccess 所有 hello 應用程式和 toodo 商務需要的登入一次只能使用單一使用者帳戶的資源。 一旦登入，您可以存取所有您需要不必要的 tooauthenticate hello 應用程式 （例如，輸入密碼） 第二次。

許多組織依賴軟體即服務 (SaaS) 應用程式，例如 Office 365、Box 和 Salesforce 來提升使用者生產力。 在過去，IT 人員需要 tooindividually 建立和更新每個 SaaS 應用程式中的使用者帳戶和使用者有 tooremember 每個 SaaS 應用程式密碼。

[Azure AD 延伸內部部署 Active Directory 至 hello 雲端](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)，啟用使用者 toouse 其組織的主要帳戶 toonot 唯一登 tootheir 加入網域的裝置和公司資源，但也所有 hello web 和 SaaS 應用程式需要其工作。

不僅使用者沒有 toomanage 多重集的使用者名稱和密碼，可以自動佈建或取消佈建根據組織群組和其狀態為員工應用程式存取權。 [Azure AD 導入了安全性和存取管理控制項](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps)可讓您 toocentrally 管理所有 SaaS 應用程式的使用者存取權。

#### <a name="multi-factor-authentication"></a>Multi-Factor Authentication

[Azure multi-factor authentication (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication)是一種方法的驗證需要 hello 使用一個以上的驗證方法，並將重要的第二層的安全性 toouser 登入和交易。 [MFA 有助於保護](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-how-it-works)存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。 它可以透過一些驗證選項 (例如電話、文字訊息，或行動應用程式通知或驗證代碼，以及第三方 OAuth 權杖) 來提供強大的驗證功能。

#### <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>安全性監視、警示以及機器學習服務型報告

安全性監視和警示以及機器學習式報告，會識別不一致的存取模式，可以協助您保護企業安全。 您可以使用 Azure Active Directory 的存取和使用方式報表 toogain 掌握 hello 完整性與安全性貴組織的目錄。 利用此資訊，目錄管理員更能夠判斷可能發生安全性風險的地方，讓他們做充裕的計畫 toomitigate 這些風險。

在 hello Azure 傳統入口網站或透過[Azure Active directory 入口網站](http://aad.portal.azure.com/)，[報表](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide)以下列方式 hello 分類：

- 異常報表-包含登入事件，我們發現 toobe 異常。 我們的目標是 toomake 您注意這類活動，並讓您 toobe 無法 toodecide 關於事件是否可疑。

- 整合式應用程式報告 – 可供深入了解雲端應用程式在組織中的使用方式。 Azure Active Directory 提供與數千個雲端應用程式的整合。

- 錯誤報表 – 指出佈建帳戶 tooexternal 應用程式時可能發生的錯誤。

- 使用者特定報告 – 顯示特定使用者的裝置/登入活動資料。

- 活動記錄-包含 hello 內所有稽核事件的記錄，過去 24 小時、 過去 7 天或過去 30 天內，以及群組活動變更、 和密碼重設和註冊活動。

#### <a name="consumer-identity-and-access-management"></a>消費者身分識別與存取管理

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)是縮放 toohundreds 數百萬個身分識別的高可用性、 全域的身分識別管理服務消費者導向應用程式。 此服務可跨行動及 Web 平台進行整合。 取用者可以登入 tooall 您的應用程式，透過可自訂的方式藉由使用其現有的社交帳戶或建立新的認證。

在過去，應用程式開發人員想太 hello[註冊和登入取用者](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview)至其應用程式會撰寫自己的程式碼。 它們會使用內部部署資料庫或系統 toostore 的使用者名稱和密碼。 Azure Active Directory B2C 提供組織更好的方式 toointegrate 取用者身分識別管理到 hello 協助應用程式的安全、 標準為基礎的平台，並將大量的可延伸的原則。

當您使用 Azure Active Directory B2C 時，您的取用者可以使用現有的社交帳戶 (Facebook、Google、Amazon、LinkedIn) 註冊應用程式，或是建立新的認證 (電子郵件地址與密碼，或使用者名稱與密碼)。

裝置註冊

[Azure AD 裝置註冊](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview)是 hello 基礎裝置型[條件式存取](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview)案例。 裝置註冊時，Azure Active Directory 裝置註冊提供 hello 裝置時，才能使用的 tooauthenticate hello 裝置 hello 使用者登入的身分。 hello 驗證裝置 hello 裝置 hello 屬性接著可以使用的 tooenforce hello 雲端和內部部署中裝載的應用程式的條件式存取原則。

當結合[行動裝置管理 (MDM)](https://www.microsoft.com/itshowcase/Article/Content/588/Mobile-device-management-at-Microsoft) hello 裝置有關的其他資訊更新的解決方案，例如 Intune、 Azure Active Directory 中的 hello 裝置屬性。 這可讓您 toocreate 條件式存取規則，以強制從裝置 toomeet 存取您的安全性與相容性的標準。

#### <a name="privileged-identity-management"></a>Privileged Identity Management

[Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure)可讓您管理、 控制和監視您的特殊權限身分識別及 Azure AD 中的 Office 365 或 Microsoft Intune 等以及其他 Microsoft online services 存取 tooresources。

有時候使用者需要在 Azure 或 Office 365 資源或其他 SaaS 應用程式中的特殊權限作業 toocarry。 這通常表示的組織有 toogive 它們的永久特殊權限存取 Azure AD 中。 這會提高雲端資源的安全性風險，因為組織無法滴水不漏地監視這些使用者利用其管理員權限的所作所為。 此外，如果擁有特殊權限存取權的使用者帳戶遭到入侵，這個缺口可能會影響其整體的雲端安全性。 Azure AD Privileged Identity Management 可協助 tooresolve 這項風險。

Azure AD Privileged Identity Management 可讓您：

- 查看哪些使用者是 Azure AD 管理員

- 視需要啟用，"just-in-time"系統管理存取權 tooMicrosoft 線上服務，如 Office 365 和 Intune

- 取得有關系統管理員存取記錄與系統管理員指派變更的報告

- 取得警示存取 tooa 特殊權限角色

#### <a name="identity-protection"></a>身分識別保護

[Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) 是一項安全性服務，可供整合檢視會影響組織身分識別的風險事件和潛在弱點。 Identity Protection 使用現有 Azure Active Directory 的異常偵測功能 (可透過 Azure AD 的異常活動報告取得)，並引進可即時偵測異常的新風險事件類型。

## <a name="secured-resource-access-in-azure"></a>Azure 中受保護的資源存取

在 Azure 中從計費觀點著手的存取控制。 hello 擁有者的 Azure 帳戶，供造訪 hello [Azure 帳戶中心](https://account.windowsazure.com/subscriptions)，為 hello 帳戶系統管理員 (AA)。 訂用帳戶是帳單的容器，但也可做為安全性界限： 每個訂閱都有一個服務系統管理員 (SA)，可以加入、 移除和修改該訂用帳戶中的 Azure 資源使用 hello [Azure 傳統入口網站](https://manage.windowsazure.com/). 新的訂閱 hello 預設 SA 為 hello AA、 但是 hello AA 可以變更 hello Azure 帳戶中心中的 hello SA。

![Azure 中受保護的資源存取](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig3.png)

訂用帳戶也會與目錄產生關聯。 hello 目錄定義一組使用者。 這些可以是從 hello 工作或學校中建立 hello 目錄的使用者，或它們可以是外部使用者 （也就是 Microsoft 帳戶）。 訂用帳戶都可以存取已獲指派為服務系統管理員 (SA) 或共同管理員 (CA); 這些目錄使用者子集hello 只例外狀況是，由於傳統原因，Microsoft 帳戶 (先前稱為 Windows Live ID) 可以指派為 SA 或 CA 不需要出現在 hello 目錄中。

安全性導向公司應該專注於讓員工 hello 所需的確切權限。 太多權限可以公開帳戶 tooattackers。 權限太少則會讓員工無法有效率地完成工作。 [Azure 角色型存取控制 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) 可以為 Azure 提供更細緻的存取管理來協助解決這個問題。

![受保護的資源存取 ](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig4.png)

使用 RBAC 時，您可以隔離您的小組內的責任，並授與存取 toousers 只 hello 量他們需要 tooperform 他們的工作。 您可以不授與每個人 Azure 訂用帳戶或資源中無限制的權限，而是只允許執行特定的動作。 例如，使用 RBAC toolet 一位員工管理訂用帳戶中的虛擬機器，而另一個可以管理 SQL 資料庫內 hello 相同訂用帳戶。

![Azure 中受保護的資源存取 (RBAC)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig5.png)

## <a name="azure-data-security-and-encryption-protect"></a>Azure 資料安全性和加密 (保護)

其中一個 hello 雲端中的 hello 金鑰 toodata 保護佔用 hello 可能是您的資料，以及哪些控制項為適用於該狀態的可能狀態。 Azure 資料安全性和加密的最佳作法 hello 建議是周圍 hello 下列資料的狀態。

- 待用︰這包括實體媒體 (磁碟或光碟) 上以靜態方式存在的所有資訊儲存物件、容器和類型。

- 傳輸中： 當資料之間傳送元件、 位置或程式，例如透過 hello 網路跨服務匯流排 （從內部部署 toocloud，反之亦然，包括例如 ExpressRoute 的混合式連線），或輸入/輸出時處理程序，它會被視為在影片。

### <a name="encryption--rest"></a>待用加密

tooachieve 加密在靜止每個 hello 下列：

支援至少一個 hello 建議下列資料表 tooencrypt 資料 hello 中詳述的加密模式。

| 加密模型 |  |  |  |
| ----------------  | ----------------- | ----------------- | --------------- |
| 伺服器加密 | 伺服器加密 | 伺服器加密 | 用戶端加密
| 使用服務管理的金鑰的伺服器端加密 | 在 Azure Key Vault 中使用客戶管理的金鑰的伺服器端加密 | 使用內部部署客戶管理的金鑰的伺服器端加密 |
| • Azure 資源提供者執行 hello 加密和解密作業 <br> • Microsoft 管理 hello 金鑰 <br>• 完整的雲端功能 | • Azure 資源提供者執行 hello 加密和解密作業<br>• 客戶控制透過 Azure 金鑰保存庫金鑰<br>• 完整的雲端功能 | • Azure 資源提供者執行 hello 加密和解密作業 <br>• 客戶會控制金鑰由內部部署 <br> • 完整的雲端功能| • Azure 服務無法查看解密的資料 <br>• 客戶將金鑰保留在內部部署環境 (或其他安全的存放區中)。 索引鍵不是使用 tooAzure 服務 <br>• 縮減的雲端功能|

### <a name="enabling-encryption-at-rest"></a>啟用待用加密

**找出資料的所有存放位置**

加密在靜止 hello 目標是 tooencrypt 的所有資料。 這樣會減少 hello 可能性遺失重要資料或所有持續性的位置。列舉應用程式所儲存的所有資料。 

> [!Note] 
> 不只是 「 應用程式資料 」 或 「 PII' 但 tooapplication 包括與相關的任何資料的帳戶 （訂用帳戶的對應，合約資訊 PII） 的中繼資料。

請考慮什麼儲存您要使用 toostore 資料。 例如：

- 外部儲存體 (例如，SQL Azure、Document DB、HDInsights、Data Lake 等)

- 暫存儲存體 (任何包含租用戶資料的本機快取)

- 記憶體中快取 （可以置入 hello 分頁檔。）

### <a name="leverage-hello-existing-encryption-at-rest-support-in-azure"></a>利用 hello 現有加密 Azure 中的 rest 支援

對於每個您所使用的存放區，利用 hello 現有 Rest 支援加密。

- Azure 儲存體：請參閱[待用資料的 Azure 儲存體服務加密](https://docs.microsoft.com/azure/storage/storage-service-encryption)。

- SQL Azure：請參閱[透明資料加密 (TDE)、SQL Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx)

- VM 與本機磁碟儲存體 ([Azure 磁碟加密](https://docs.microsoft.com/azure/security/azure-security-disk-encryption))

對於支援使用 Azure 磁碟加密的 VM 和本機磁碟儲存體：

IaaS

與 IaaS Vm （Windows 或 Linux） 的服務應使用[Azure 磁碟加密](https://microsoft.sharepoint.com/teams/AzureSecurityCompliance/Security/SitePages/Azure%20Disk%20Encryption.aspx)tooencrypt 包含客戶資料的磁碟區。

PaaS v2

執行的服務在 PaaS v2 使用 Service Fabric 可以使用 Azure 磁碟加密的虛擬機器擴展集 [VMSS] tooencrypt 其 PaaS v2 Vm。

PaaS v1

PaaS v1 目前不支援 Azure 磁碟加密。 因此，您必須使用應用程式層級加密 tooencrypt 保存的待用資料。  這包括 (但不限於) 應用程式資料、暫存檔案、記錄和損毀傾印。

大部分的服務應嘗試 tooleverage hello 加密儲存體資源提供者。 某些服務有 toodo 明確加密，比方說，任何保存金鑰內容 (憑證、 root / 主索引鍵) 必須儲存在金鑰保存庫。

如果您使用客戶管理的金鑰支援服務端加密需要 toobe 方式 hello 客戶 tooget hello 金鑰 toous。 hello 支援和建議的方式 toodo 藉由整合與 Azure 金鑰保存庫 (AKV)。 在此情況下，客戶就能在 Azure Key Vault 中新增及管理其金鑰。 客戶可以了解如何 toouse AKV 透過[開始使用金鑰保存庫](http://go.microsoft.com/fwlink/?linkid=521402)。

toointegrate 使用 Azure 金鑰保存庫，您將從 AKV 需要解密時，加入程式碼 toorequest 索引鍵。

- 請參閱[逐步解說 – Azure 金鑰保存庫](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)有關的資訊與 AKV toointegrate。

如果您支援由客戶管理金鑰，您需要 tooprovide UX hello 客戶 toospecify 哪些金鑰保存庫 （或金鑰保存庫 URI） toouse。

因為加密在靜止涉及 hello 主機、 基礎結構和租用戶的資料加密，hello 遺失的 hello 索引鍵，到期 toosystem 失敗或惡意活動可能表示所有 hello 加密資料都都會遺失。 因此，是重要您加密在其餘方案具有劇本彈性 toosystem 失敗和惡意活動的完整的災害復原。

實作加密在靜止的服務通常是仍會受到 toohello 加密金鑰，或所遺留的資料加密狀態 hello 主機磁碟機 （例如，在 hello 分頁檔的 hello 主機作業系統。）因此，服務必須確定其服務的 hello 主機磁碟區加密。 toofacilitate 這個計算小組已啟用的主應用程式加密，它會使用 hello 部署[Bitlocker](https://technet.microsoft.com/library/dn306081.aspx) NKP 和擴充功能 toohello DCM 服務與代理程式 tooencrypt hello 主機磁碟區。

大部分服務會實作在標準 Azure VM 上。 這類服務應該會在計算團隊將其啟用時自動獲得[主機加密](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)。 在計算團隊管理的叢集中執行的服務，皆已在 Windows Server 2016 推出時自動啟用主機加密。

### <a name="encryption-in-transit"></a>傳輸中加密

保護傳輸中的資料應該是您的資料保護策略中不可或缺的部分。 從許多位置來回移動資料，因為 hello 一般建議您一律使用 SSL/TLS 通訊協定 tooexchange 資料分散在不同的位置。 在某些情況下，您可能想 tooisolate hello 整個通訊通道，您的內部部署與雲端之間使用虛擬私人網路 (VPN) 的基礎結構。

對於在內部部署基礎結構與 Azure 之間移動的資料，您應該考慮適當的防護措施，例如 HTTPS 或 VPN。

針對需要從多個工作站位在內部 tooAzure toosecure 存取的組織，使用[Azure 站台對站 VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create)。

對於組織，需要從一個工作站 toosecure 存取位於內部部署 tooAzure，使用[點對站 VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create)。

較大的資料集可以透過專用的高速 WAN 連結 (例如 [ExpressRoute](https://azure.microsoft.com/services/expressroute/)) 移動。 如果您選擇 toouse ExpressRoute，您也可以加密 hello 資料在 hello 應用程式層級使用[SSL/TLS](https://support.microsoft.com/kb/257591)或為了提高保護其他通訊協定。

如果透過 hello Azure 網站互動與 Azure 儲存體，所有交易將會透過 HTTPS 都發生。 [儲存體 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)透過 HTTPS 也可以與使用的 toointeract [Azure 儲存體](https://azure.microsoft.com/services/storage/)和[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。

失敗 tooprotect 資料在傳輸過程中的組織就更容易受到如[攔截攻擊](https://technet.microsoft.com/library/gg195821.aspx)，[竊聽](https://technet.microsoft.com/library/gg195641.aspx)，和工作階段攔截。 Hello 第一個步驟中獲得存取 tooconfidential 資料時，可以是這些攻擊。

您可以進一步了解 Azure VPN 選項藉由讀取 hello 文章[規劃和設計 VPN 閘道](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)。

### <a name="enforce-file-level-data-encryption"></a>強制執行檔案層級資料加密

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx)使用加密、 身分識別及授權原則 toohelp 保護您的檔案和電子郵件。 Azure RMS 可跨多個裝置運作 — 手機、平板電腦和 PC。保護您的組織內部和外部 這項功能可能是保護的因為 Azure RMS，增加一層，即使在離開組織範圍也不如影隨形 hello 資料。

當您使用 Azure RMS tooprotect 檔案時，您正在使用業界標準密碼編譯的完整支援[FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html)。 當您利用 Azure RMS 的資料保護時，即使它是不受 hello 控制複製的 toostorage 擁有 hello 檔案便可持續受到保護 hello 的 hello 保證 IT，例如雲端儲存體服務。 hello 相同發生時透過電子郵件共用的檔案、 hello 檔案受到保護做為附件 tooan 電子郵件訊息，指示如何 tooopen hello 受保護的附件。
規劃 Azure RMS 採用時 hello 下列建議：

- 安裝 hello [RMS 共用應用程式](https://technet.microsoft.com/library/dn339006.aspx)。 此應用程式會藉由安裝 Office 增益集來與 Office 應用程式整合，讓使用者可以輕鬆地直接保護檔案。

- 設定應用程式和服務 toosupport Azure RMS

- 建立可反映您的業務需求的[自訂範本](https://technet.microsoft.com/library/dn642472.aspx)。 例如︰最高秘密資料的範本應套用於所有最高機密相關的電子郵件。

弱式上的組織[資料分類](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf)，檔案保護可能更容易受到 toodata 外洩。 沒有適當的檔案保護組織不會是能 tooobtain 商業見解、 監督濫用情形，並防止惡意存取 toofiles。

> [!Note]
> 您可以進一步了解 Azure RMS 閱讀 hello 文章[開始使用 Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx)。

## <a name="secure-your-application-protect"></a>保護應用程式 (保護)
Azure 負責保護 hello 基礎結構和您的應用程式執行的平台時，它是您的責任 toosecure 您的應用程式本身。 換句話說，您需要 toodevelop，部署及安全的方式來管理您的應用程式程式碼和內容。 若未這麼做，您的應用程式程式碼或內容仍然可以很容易遭受 toothreats。

### <a name="web-application-firewall-waf"></a>Web 應用程式防火牆 (WAF)
[Web 應用程式防火牆 (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) 是一項[應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)功能，可提供 Web 應用程式的集中式保護，免於遭遇常見的攻擊和弱點。

Web 應用程式防火牆會根據規則從 hello [OWASP 核心規則集](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)3.0 或 2.2.9。 Web 應用程式已逐漸成為利用常見已知弱點的惡意攻擊目標。 通用的這些攻擊 SQL 插入式攻擊，跨網站指令碼處理攻擊 tooname 幾個。 防止這類攻擊中應用程式程式碼極具挑戰，可能需要嚴格的維護、 修補和監視 hello 應用程式拓撲的多個層級。 集中式的 web 應用程式防火牆有助於讓安全性管理簡單許多，並提供更好的保證 tooapplication 系統管理員針對威脅或入侵。 WAF 方案也可以回應 tooa 更快的安全性威脅的修補與保護每個個別的 web 應用程式的中央位置的已知的弱點。 現有的應用程式閘道可以輕鬆地是轉換的 tooa web 應用程式啟用防火牆應用程式閘道。

Hello 的 web 應用程式防火牆防止常見 web 弱點部分包括：

- SQL 插入式攻擊保護

- 跨網站指令碼保護

- 常見 Web 攻擊保護，例如命令插入式攻擊、HTTP 要求走私、HTTP 回應分割和遠端檔案包含攻擊

- 防範 HTTP 通訊協定違規

- 防範 HTTP 通訊協定異常行為，例如遺漏主機使用者代理程式和接受標頭

- 防範 Bot、編目程式和掃描器

- 偵測一般應用程式錯誤組態 (也就是 Apache、IIS 等)

> [!Note]
> 如需更詳細的規則清單和其保護，請參閱 hello 下列[核心規則集](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview#core-rule-sets):

Azure 也提供數個簡單好用功能 toohelp 保護您的應用程式的輸入和輸出流量。 Azure 也可協助客戶來保護其應用程式程式碼提供外部提供功能 tooscan web 應用程式的弱點。

- [使用各種驗證和授權方法保護 Web 應用程式](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)

    - [為應用程式設定 Azure Active Directory 驗證](https://azure.microsoft.com/blog/azure-websites-authentication-authorization/)


- [啟用傳輸層安全性 (TLS/SSL)-HTTPS 保護流量 tooyour 應用程式](https://docs.microsoft.com/azure/app-service-web/web-sites-configure-ssl-certificate)

    - [強制所有傳入流量透過 HTTPS 連線](http://microsoftazurewebsitescheatsheet.info/)

  - [啟用 Strict Transport Security (HSTS)](http://microsoftazurewebsitescheatsheet.info/#enable-http-strict-transport-security-hsts)


- [依用戶端的 IP 位址限制存取 tooyour 應用程式](http://microsoftazurewebsitescheatsheet.info/#filtering-traffic-by-ip)

- [限制用戶端的行為： 要求的頻率和並行存取 tooyour 應用程式](http://microsoftazurewebsitescheatsheet.info/#dynamic-ip-restrictions)

- [使用 Tinfoil 安全性掃描來掃描 Web 應用程式程式碼的弱點](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)

- [設定 TLS 相互驗證 toorequire 用戶端憑證 tooconnect tooyour web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth)

- [設定用戶端憑證，使用從您的應用程式 toosecurely 連線 tooexternal 資源](https://azure.microsoft.com/blog/using-certificates-in-azure-websites-applications/)

- [移除伺服器標準標頭 tooavoid 工具指紋識別您的應用程式](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)

- [使用點對站 VPN 保護應用程式與私人網路中資源的連線](https://docs.microsoft.com/azure/app-service-web/web-sites-integrate-with-vnet)

- [使用混合式連接保護應用程式與私人網路中資源的連線](https://docs.microsoft.com/azure/app-service-web/web-sites-hybrid-connection-get-started)

Azure 應用程式服務會使用 hello 相同 Azure 雲端服務和虛擬機器所使用的反惡意程式碼方案。 進一步了解這 toolearn 參考 tooour[反惡意程式碼文件](https://docs.microsoft.com/azure/security/azure-security-antimalware)。

## <a name="secure-your-network-protect"></a>保護網路 (保護)
Microsoft Azure 包括強固的網路基礎結構 toosupport 應用程式和服務連線需求。 在 Azure 中，位於內部部署之間的資源之間的網路連線可與 Azure 託管資源和 tooand 從 hello 網際網路和 Azure。

hello [Azure 網路基礎結構](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines)可讓您 toosecurely 連接的 Azure 資源 tooeach 與其他[虛擬網路 (Vnet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)。 VNet 是網路的您自己 hello 雲端中的表示法。 VNet 是隔離的邏輯 hello Azure 雲端專用的網路 tooyour 訂用帳戶。 您可以連接的 Vnet tooyour 在內部部署網路。

![保護網路 (保護)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig6.png)

如果您需要基本網路層級的存取控制 （根據 IP 位址和 hello TCP 或 UDP 通訊協定），則您可以使用[網路安全性群組](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)。 網路安全性群組 (NSG) 是基本可設定狀態篩選封包的防火牆，它可讓您 toocontrol 存取權限[5-tuple](https://www.techopedia.com/definition/28190/5-tuple)。

Azure 網路支援您的 Azure 虛擬網路上的網路流量 hello 能力 toocustomize hello 路由行為。 做法是在 Azure 中設定 [使用者定義的路由](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) 。

[強制通道](https://www.petri.com/azure-forced-tunneling)的機制，您可以使用您的服務不 tooensure 允許 tooinitiate 連接 toodevices hello 網際網路上。

Azure 支援專用 WAN 連結連線 tooyour 在內部部署網路和 Azure 虛擬網路與[ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)。 hello Azure 與您的站台之間的連結使用專用的連接，不會通過 hello 公用網際網路。 如果多個資料中心中執行 Azure 應用程式，您可以使用[Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute 以聰明的方式跨 hello 應用程式的執行個體的使用者要求。 您也可以路由傳送流量 tooservices 不在 Azure 中執行時可從 hello 網際網路存取。

## <a name="virtual-machine-security-protect"></a>虛擬機器安全性 (保護)

您可利用 [Azure 虛擬機器](https://docs.microsoft.com/azure/virtual-machines/)以敏捷的方式部署範圍廣泛的許多運算解決方案。 利用 Microsoft Windows、Linux、Microsoft SQL Server、Oracle、IBM、SAP 與 Azure BizTalk 服務的支援，就可以在近乎所有的作業系統上，使用任何語言部署所有工作負載。

有了 Azure，您可以使用[反惡意程式碼軟體](https://docs.microsoft.com/azure/security/azure-security-antimalware)安全性廠商，例如 Microsoft、 Symantec、 趨勢科技及 Kaspersky tooprotect 從您的虛擬機器從惡意檔案、 廣告軟體和其他威脅。

適用於 Azure 雲端服務和虛擬機器的 Microsoft Antimalware 是即時保護功能，有助於識別和移除病毒、間諜軟體和其他惡意軟體。 Microsoft 反惡意程式碼提供已知惡意或垃圾軟體嘗試 tooinstall 本身，或在您的 Azure 系統上執行時可設定的警示。

[Azure 備份](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)是可調式解決方案，可以不需成本地保護您的應用程式資料，以及將操作成本降到最低。 應用程式錯誤可能導致資料損毀，而人為錯誤可能會將 Bug 導入應用程式中。 使用 Azure 備份，您執行 Windows 與 Linux 的虛擬機器會受到保護。

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) 有助於協調工作負載和應用程式的複寫、容錯移轉及復原，因此能夠在主要位置發生故障時，透過次要位置提供工作負載和應用程式。

## <a name="ensure-compliance-cloud-services-due-diligence-checklist-protect"></a>確保合規性：雲端服務審查評鑑檢查表 (保護)

Microsoft 開發[hello 雲端服務到期勤加注意檢查清單](https://aka.ms/cloudchecklist.download)toohelp 組織執行到期勤加注意，當它們考慮移動 toohello 雲端。 它提供任何大小和類型的組織結構 — 私人企業及公用磁區組織，包括在所有層級和非營利組織版政府 — tooidentify 他們自己的效能、 服務、 資料管理和控管的目標和需求。 這可讓它們 toocompare hello 供應項目不同的雲端服務提供者，最終形成 hello 基礎雲端服務合約。

hello 檢查清單提供將對齊的新國際標準雲端服務合約，ISO/IEC 19086 子句的架構。 這項標準提供了統一的考量組織 toohelp 做出有關雲端採用，以及建立共同點，比較雲端服務供應項目。

hello 檢查清單會提升徹底檢查結果的移動 toohello 雲端，可為選擇的雲端服務提供者提供結構化的指引和一致、 可重複的方法。

採用雲端不再只是技術方面的決策。 檢查清單需求觸控組織的每個層面上，因為它們可 tooconvene 所有索引鍵內部-決策者 — hello CIO 和首席資訊安全長，以及法律風險管理、 採購，以及相容性的專業人員。 這會增加 hello 決策程序和聲音推理，藉此減少無法預見的障礙 tooadoption hello 可能性地面決策 hello 效率。

此外，hello 檢查清單：

- 公開決策者 hello 雲端採用程序的 hello 開頭的索引鍵的討論主題。

- 支援完整的商務討論法規和 hello 組織自己的目標隱私權、 個人識別資訊 (PII)，與資料安全性。

- 協助組織找出可能會影響雲端專案的任何潛在問題。

- 提供一組一致的問題，以 hello 相同的詞彙、 定義、 度量和交付項目，每個提供者，toosimplify hello 程序的比較不同雲端服務提供者的供應項目。

## <a name="azure-infrastructure-and-application-security-validation-detect"></a>Azure 基礎結構和應用程式安全性驗證 (偵測)

[Azure 操作安全性](https://docs.microsoft.com/azure/security/azure-operational-security)參考 toohello 服務、 控制項和功能可用 toousers 保護其資料、 應用程式，以及其他 Microsoft Azure 中的資產。

![安全性驗證 (偵測)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig7.png)

Azure 操作安全性是建置在結合 hello 知識透過唯一 tooMicrosoft，包括 Microsoft 安全性開發週期 (SDL)，Microsoft 回應資訊安全中心 hello hello 各種功能的架構程式及深層 hello 顧慮威脅大環境的認知。

### <a name="microsoft-operations-management-suiteoms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)為 hello hello 混合式雲端 IT 管理解決方案。 單獨使用，或將現有 System Center 部署，OMS，可讓您 tooextend hello 大的彈性和以雲端為基礎的管理基礎結構的控制項。

![Microsoft Operations Management Suite (OMS)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig8.png)

透過 OMS，您就能以低於競爭解決方案的成本來管理任何雲端中的任何執行個體，包括內部部署、Azure、AWS、Windows Server、Linux、VMware 和 OpenStack。 OMS 提供新的方法 toomanaging 建置為 hello 雲端優先世界中，您是 hello 最快速、 最具成本效益的方式 toomeet 新商務面臨的挑戰和配合新的工作負載，應用程式和雲端環境的企業。

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) 藉由將受控資源中的資料收集到中央儲存機制，以提供 OMS 監視服務。 這項資料可能包括事件、 效能資料或透過 hello API 提供的自訂資料。 一旦收集完成，就有一個 hello 資料適用於警示和分析，並匯出。

![Log Analytics](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig9.png)

這個方法可讓您從各種來源 tooconsolidate 資料，因此您可以結合資料從您的 Azure 服務與現有內部部署環境。 它會從 hello，讓所有動作都都會使用 tooall 種類的資料，該資料上採取的動作也會明確分隔 hello hello 資料集合。

### <a name="azure-security-center"></a>Azure 資訊安全中心

[Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)幫助您防止、 偵測，並以進一步掌握回應 toothreats 及控制 hello 您的 Azure 資源的安全性。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

資訊安全中心會分析您的 Azure 資源 tooidentify 潛在的安全性漏洞 hello 安全性狀態。 建議清單會引導您完成設定所需的控制項的 hello 程序。

範例包括：

- 佈建反惡意程式碼 toohelp 識別及移除惡意軟體

- 設定網路安全性群組與規則 toocontrol 流量 tooVMs

- Web 應用程式防火牆 toohelp 防禦攻擊目標 web 應用程式的佈建

- 部署遺漏的系統更新

- 定址 OS 組態不符合 hello 建議基準

資訊安全中心會自動收集、 分析，並將記錄資料從 Azure 資源、 hello 網路和反惡意程式碼的程式和防火牆等協力廠商解決方案相整合。 偵測到威脅時，會建立安全性警示。 偵測範例包括：

- 已受到危害的 VM 與已知的惡意 IP 位址進行通訊

- 使用 Windows 錯誤報告偵測到進階的惡意程式碼

- 針對 VM 的暴力密碼破解攻擊

- 來自整合式反惡意程式碼程式和防火牆的安全性警示

### <a name="azure-monitor"></a>Azure 監視器

[Azure 監視](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)指標 tooinformation 提供特定類型的資源。 它提供視覺效果、 查詢、 路由、 警示、 自動調整規模及自動化 hello Azure 基礎結構 （活動記錄檔） 從資料和每個個別的 Azure 資源 （診斷記錄檔）。

雲端應用程式相當複雜，且具有許多移動組件。 監視提供您的應用程式保持啟動的資料 tooensure 和狀況良好的狀態中執行。 它也可協助您 toostave 關閉潛在的問題或過去的疑難排解。

![Azure 監視](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig10.png)此外，您可以使用監視資料 toogain 深入了解有關應用程式。 該知識可以幫助您 tooimprove 應用程式效能或可維護性，或自動化需要手動介入的動作。

在偵測網路漏洞，並確認您的 IT 安全性和法規治理模型的合規性時，稽核您的網路安全性非常重要。 安全性群組 檢視中，您可以擷取 hello 設定網路安全性群組與安全性規則，以及 hello 有效的安全性規則。 Hello 要套用的規則清單中，您可以決定開啟 hello 通訊埠與 ss 網路的弱點可能會。

### <a name="network-watcher"></a>網路監看員

[網路監看員](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher)是地區和服務，可讓您 toomonitor 診斷在網路層級中，並從 Azure 的情況。 網路診斷和使用網路監看員的視覺化工具，可協助您了解、 診斷，以及取得 Azure insights tooyour 網路。 這項服務包括封包擷取、下一個躍點、IP 流量驗證、安全性群組檢視、NSG 流量記錄。 案例層級監視提供結束 tooend 檢視中對比 tooindividual 網路資源監視的網路資源。

### <a name="storage-analytics"></a>儲存體分析

[儲存體分析](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)可以儲存有關要求 tooa 儲存體服務的彙總的交易統計資料和容量資料的度量。 在這兩個 hello 應用程式開發介面作業層級，以及在 hello 儲存體服務層級報告交易和容量會報告在 hello 儲存體服務層級。 度量資料可使用的 tooanalyze 儲存體服務使用量，要求的 hello 儲存體服務，與使用服務的應用程式的 tooimprove hello 效能診斷問題。

### <a name="application-insights"></a>Application insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) 是多個平台上的 Web 開發人員所適用的可延伸應用程式效能管理 (APM) 服務。 它使用 toomonitor 即時 web 應用程式。 它將會自動偵測效能異常。 它包括強大的分析工具 toohelp 您診斷問題和 toounderstand 哪些使用者處理您的應用程式。 其設計目的是 toohelp 持續改善效能和可用性。 這也適用於應用程式上各種不同的平台包括.NET、 Node.js 和 J2EE，裝載在內部部署或 hello 雲端中。 它與您的 devOps 程序整合，並已連線點 tooa 各種開發工具。

它可監視︰

- **要求率、回應時間和失敗率** - 找出哪些頁面在每天哪些時段最受歡迎，以及使用者位於何處。 查看哪些頁面的表現最好。 如果您的回應時間和失敗率隨著要求增加而提高，您或許有資源配置問題。

- **相依比率、回應時間和失敗率** - 找出外部服務是否會使您降低效能。

- **例外狀況**-分析 hello 彙總統計資料，或選擇特定執行個體和下鑽研至 hello 堆疊追蹤和相關的要求。 伺服器和瀏覽器例外狀況都會報告。

- **頁面檢視和載入效能** - 由使用者的瀏覽器報告。

- 來自網頁的 **AJAX 呼叫** - 比率、回應時間和失敗率。

- **使用者和工作階段計數**。

- Windows 或 Linux 伺服器電腦中的**效能計數器**，例如 CPU、記憶體和網路使用量。

- 來自 Docker 或 Azure 的**主機診斷**。

- 來自您應用程式的**診斷追蹤記錄檔** - 讓您使追蹤事件與要求相互關聯。

- **自訂事件和度量**自行撰寫 hello 用戶端或伺服器程式碼、 tootrack 商務事件，例如銷售的項目或贏得遊戲中。
許多元件 – 也許虛擬機器、 儲存體帳戶和虛擬網路或 web 應用程式、 資料庫、 資料庫伺服器和第 3 個合作對象服務 hello 基礎結構，您的應用程式通常由所組成。 您看不到這些元件作為個別的實體，而是看到它們作為單一實體相關且彼此相依的組件。 您想 toodeploy、 管理和監視這些群組。 [Azure 資源管理員](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)可讓您與您的解決方案，為群組中的 hello 資源 toowork。

您可以部署、 更新或刪除您的解決方案是單一的協調作業，在 hello 的所有資源。 您會使用部署的範本，且該範本可以用於不同的環境，例如測試、預備和生產環境。 資源管理員提供安全性、 稽核和標記功能 toohelp 部署後管理您的資源。

**使用資源管理員的 hello 優點**

Resource Manager 會提供數個優點：

- 您可以部署、 管理及監視您的方案 hello 的所有資源群組，而非個別處理這些資源。

- 重複，您可以部署整個 hello 開發生命週期方案，並確保一致的狀態以部署您的資源。

- 您可以透過宣告式範本而非指令碼來管理基礎結構。

- 您可以定義 hello 資源，因此它們部署在 hello 正確的順序之間的相依性。

- 因為角色型存取控制 (RBAC) 原生整合至 hello 管理平台，您可以套用存取控制 tooall 服務資源群組中。

- 您可以將標籤套用 tooresources toologically 組織您的訂用帳戶中的所有 hello 資源。

- 您可以藉由檢視群組的資源成本釐清您組織的計費共用 hello 相同的標記。

> [!Note]
> 資源管理員提供新的方式 toodeploy 和管理您的方案。 如果您使用 hello 舊版部署模型而且想 toolearn 有關 hello 變更，請參閱[了解資源管理員部署和傳統部署](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model)。

## <a name="next-steps"></a>後續步驟

閱讀一些有深度的安全性主題，以深入了解安全性：

- [稽核和記錄](https://www.microsoft.com/en-us/trustcenter/security/auditingandlogging)

- [網路犯罪](https://www.microsoft.com/en-us/trustcenter/security/cybercrime)

- [設計與作業安全性 (英文)](https://www.microsoft.com/en-us/trustcenter/security/designopsecurity)

- [加密](https://www.microsoft.com/en-us/trustcenter/security/encryption)

- [身分識別和存取管理](https://www.microsoft.com/en-us/trustcenter/security/identity)

- [網路安全性](https://www.microsoft.com/en-us/trustcenter/security/networksecurity)

- [威脅管理](https://www.microsoft.com/en-us/trustcenter/security/threatmanagement)
