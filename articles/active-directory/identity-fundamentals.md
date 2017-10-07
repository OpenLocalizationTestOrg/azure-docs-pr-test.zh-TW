---
title: "Azure 身分識別管理 aaaFundamentals |Microsoft 文件"
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Azure 身分識別管理的基本概念
因為越來越多公司數位資源即時 hello 公司網路，在 hello 雲端，並在裝置上，外部的絕佳雲端身分識別和存取管理解決方案變得您不再需要。 以雲端為基礎的身分識別現在是最佳方式 toomaintain 控制項 hello over 和可見性，使用者如何及何時存取公司應用程式和資料。

Microsoft 有已保護的雲端式身分識別以來而現在可透過[Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-editions)，這些相同的保護系統是可用 tooyou。 使用 Azure AD，企業系統管理員可透過前所未有的更佳安全性和監管，輕易地確保使用者和系統管理員負有責任。

Azure AD Premium 是雲端式身分識別和存取管理解決方案進階的保護功能，可讓所有應用程式，請識別身分保護一個安全的身分識別 (增強 hello [Microsoft 智慧安全性 graph](https://www.microsoft.com/en-us/security/intelligence))，和權限身分識別管理。 不只是另一個監視或報告工具，來保護您的使用者識別身分即時 Azure AD Premium 即可啟用您 toocreate 風險為基礎且可調整的存取原則 tooprotect 貴組織的資料。

觀看以下短片，快速概覽 Azure AD 身分識別管理和保護功能︰
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

Microsoft 不只提供身分識別，會帶領您每個地方，但也工具 tooautomate 協助保護，以及管理您組織內 IT。 雲端運算，也無需仍要求 toomanage 控制 IT 工作，像是技術服務人員呼叫 tooreset 使用者密碼的 hello 問世，即使使用者群組管理和應用程式的要求。 複雜進一步動作，員工為現在攜帶其個人裝置 toowork 並使用方便使用的 SaaS 應用程式。 這使得掌控其橫跨公司資料中心和公用雲端平台的應用程式成為一大挑戰。

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>連接內部部署 Active Directory 與 Azure AD 和 Office 365
所做的大型投資在內部部署 Active Directory 中的組織可以透過其在內部部署目錄整合到 Azure AD 與擴充這些投資 toohello 雲端[混合式身分識別管理](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)。 這麼做可提供通用身分識別來存取各地資源，而讓您的使用者更具生產力。 使用者和組織即可使用單一登入 (SSO) tooaccess 內部部署資源和雲端服務，例如 Office 365。

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)是 hello 唯一需要完成 tooget hello 整合的工具。 Azure AD Connect 提供您的身分識別同步處理需要並取代舊版的身分識別整合工具，例如 DirSync 和 Azure AD Sync 功能 toosupport。使用 Azure AD Connect，身分識別管理和內部部署與 Azure AD 之間的同步處理是透過下列項目啟用︰

- 同步處理 - 此元件負責建立使用者、群組和其他物件。 它也會負責確保您在內部部署使用者和群組的識別資訊會比對 hello 雲端。 使用者在 Azure AD 中更新其密碼時，密碼回寫也可以是啟用的 tookeep 在內部部署目錄同步。
- AD FS 的同盟是選擇性的功能，可以使用的 tooconfigure 混合式環境中使用內部部署的 Azure AD Connect 所提供 AD FS 基礎結構。 同盟可以供組織 tooaddress 複雜的部署，如單一登入強制執行 AD 登入的原則和智慧卡或協力廠商 MFA。
- 健全狀況監視- [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)可以提供強大的監視，並提供中央位置，在 Azure 入口網站 tooview hello 此活動。

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>經由自助式和單一登入體驗提高生產力並降低技術支援成本

當有單一的使用者名稱和密碼 tooremember 和一致的經驗，從每個裝置，員工會更具生產力。 他們也儲存時，他們可以執行的時間自助服務工作，例如[忘記的密碼重設](https://docs.microsoft.com/azure/active-directory/active-directory-passwords)或要求存取 tooan 應用程式，而不需等待 hello 技術服務人員以取得協助。

Azure AD[擴充內部部署 Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)到 hello 雲端啟用使用者 toouse 其網域的裝置，公司資源和 hello web 和 SaaS 應用程式的所有主要組織帳戶它們需要 toouse tooget 完成其工作。 除了具有使用者名稱和密碼、 使用者應用程式存取權的多個集也可以自動佈建 （或取消佈建） tooremember toonot 根據其組織的群組成員資格及其實員工。 您可以控制該圖庫應用程式或您開發並透過 hello 發行您自己內部部署應用程式的存取和[Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)。

## <a name="manage-and-control-access-toocorporate-resources"></a>管理和控制存取 toocorporate 資源
Microsoft 身分識別和存取管理解決方案說明 IT 保護存取 tooapplications 及資源 hello 公司資料中心跨和進入 hello 雲端啟用驗證的額外層級，例如[多重要素驗證](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)和[條件式存取原則](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)。 透過進階的安全性報告、稽核和警示來監視可疑活動，有助於減緩潛在的安全性問題。

在 Azure AD Premium 的條件式存取原則可讓您、 hello 企業系統管理員、 hello 任何 Azure AD 連接應用程式 （hello 雲端或內部部署 web 應用程式中執行的自訂應用程式中的 SaaS 應用程式） 的能力 toocreate 以原則為基礎的存取規則。 Azure AD 評估即時，這些原則，並強制套用這些每當使用者嘗試 tooaccess 應用程式。 Azure 身分識別保護原則可讓您 tooautomatically 採取的動作如果探索到的可疑活動。 這些動作包括封鎖存取 toousers 高風險，強制執行多重要素驗證，以及重設使用者密碼，如果它看起來像認證遭洩漏。


## <a name="azure-active-directory-privileged-identity-management"></a>Azure Active Directory Privileged Identity Management

[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started)、 隨附 hello Azure Active Directory Premium P2 供應項目，可讓您 toodiscover、 限制，並監視系統管理帳戶和 Azure Active Directory 和其他其存取 tooresourcesMicrosoft online services。 它也可協助您管理 hello 確切的期間，您所需的時間視系統管理存取權。

Privileged 的 Identity Management 可強制視系統管理員權限，這樣一來，系統管理員可以要求 multi-factor 經過驗證、 暫存權限提高其權限這段時間後他們的帳戶，傳回 tooa 標準預先設定的期間使用者狀態。

## <a name="benefits-of-azure-identity"></a>Azure 身分識別的優點

透過 Azure 身分識別管理，您可以：

-   為全體企業的每位使用者建立和管理單一身分識別，讓使用者、群組和裝置與 [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) 保持同步。

-   提供單一登入存取 tooyour 應用程式包括數千個預先整合的 SaaS 應用程式或使用 hello tooon 內部 SaaS 應用程式提供安全的遠端存取[Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)。

-   藉由同時對內部部署和雲端應用程式強制以規則為基礎的 [Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)，啟用應用程式存取安全性。

-   改善使用者的產能，[自助式密碼重設](https://docs.microsoft.com/azure/active-directory/active-directory-passwords)、 群組和應用程式存取使用 hello 要求[MyApps 入口網站](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help)。

-   利用 hello[高可用性和可靠性](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications)的全球性、 企業等級、 雲端身分識別和存取管理解決方案。

## <a name="next-steps"></a>後續步驟
[深入了解 Azure 身分識別解決方案](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)