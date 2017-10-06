---
title: "aaaAzure Active Directory 常見問題集 |Microsoft 文件"
description: "Azure Active Directory 常見問題集解答疑問 tooaccess Azure 和 Azure Active Directory、 密碼管理和應用程式的存取。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a>Azure Active Directory 常見問題集
Azure Active Directory (Azure AD) 是全方位的身分識別即服務 (IDaaS) 解決方案，其涉及範圍橫跨身分識別、存取管理和安全性的所有層面。

如需詳細資訊，請參閱[什麼是 Azure Active Directory？](active-directory-whatis.md)。


## <a name="access-azure-and-azure-active-directory"></a>存取 Azure 和 Azure Active Directory
**問： 我為什麼收到 「 找到的任何訂用帳戶 」 當我嘗試 tooaccess Azure AD 中 hello Azure 傳統入口網站？**

**答：** tooaccess hello Azure 傳統入口網站，每位使用者必須具備 Azure 訂用帳戶的權限。 如果您有 Office 365 或 Azure AD 的付費的訂閱，請移至太[http://aka.ms/accessAAD](http://aka.ms/accessAAD)一次性的啟用步驟。 否則，您將需要可用 tooactivate [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)或付費的訂閱。

如需詳細資訊，請參閱：

* [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](active-directory-how-subscriptions-associated-directory.md)
* [管理 Office 365 訂用帳戶在 Azure 中的 hello 目錄](active-directory-manage-o365-subscription.md)

- - -
**問： 什麼是 Azure AD 中的 hello 關聯 Office 365 和 Azure？**

**答：** Azure AD 為您提供常見的身分識別和存取功能 tooall web 服務。 不論您使用 Office 365、 Microsoft Azure，Intune，或其他人，您是已經在使用 Azure AD toohelp 開啟登入及存取管理所有這些服務。

設定 toouse web 服務的所有使用者會都定義為一或多個 Azure AD 執行個體中的使用者帳戶。 您可以為這些帳戶設定免費的 Azure AD 功能，如雲端應用程式存取。

Azure AD 付費服務 (例如 Enterprise Mobility + Security) 可透過全方位的企業級管理和安全性解決方案來彌補其他 Web 服務 (例如 Office 365 和 Microsoft Azure) 的不足。
- - -
**問： 為什麼登入 Azure 入口網站 toohello 但不是 hello Azure 傳統入口網站？**

**答：** hello Azure 入口網站不需要有效的訂用帳戶，且 hello 傳統入口網站需要有效的訂用帳戶。  如果您沒有訂用帳戶，您無法登入 toohello 傳統入口網站。
- - -
**問： hello 訂用帳戶管理員與目錄管理員之間的差異為何？**

**答：**根據預設，您獲指派 hello 訂用帳戶管理員角色時登入 azure。 訂用帳戶管理員可以使用 Microsoft 帳戶或是工作或學校帳戶，從 hello Azure 訂用帳戶的 hello 目錄相關聯。  這個角色是授權的 toomanage hello Azure 入口網站中的服務。

如果其他人在 toosign 以及存取服務所使用 hello 相同訂用帳戶，您可以將它們加入為共同管理員。 這個角色有 hello 相同身 hello 服務系統管理員存取權限，但無法變更 hello 關聯的訂用帳戶 tooAzure 目錄。  如需有關訂用帳戶系統管理員 」 的詳細資訊，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](../billing-add-change-azure-subscription-administrator.md)和[如何 Azure 訂用帳戶相關聯 Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)。


Azure AD 有一組不同的系統管理員角色 toomanage hello 目錄和身分識別相關功能。  這些系統管理員 」 將會在 hello Azure 入口網站存取 toovarious 功能或 hello Azure 傳統入口網站。 hello 系統管理員角色會決定其功能，例如建立或編輯使用者、 指派系統管理角色 tooothers、 重設使用者密碼、 管理使用者授權或管理的網域。  如需有關 Azure AD 目錄管理員及其角色的詳細資訊，請參閱[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles.md)。

此外﹐Azure AD 付費服務 (例如 Enterprise Mobility + Security) 可透過全方位的企業級管理和安全性解決方案來彌補其他 Web 服務 (例如 Office 365 和 Microsoft Azure) 的不足。

- - -
**問︰是否有報告可顯示 Azure AD 使用者授權何時即將過期？**

**答：**否。  目前無法使用此功能。

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>開始使用混合式 Azure AD


**問︰當我新增為共同作業人員時如何離開租用戶？**

**答：**當您加入為共同作業者 tooanother 組織的租用戶時，您可以使用 hello 「 租用戶切換器 」 中 hello 上方右 tooswitch 租用戶之間。  目前沒有任何方式 tooleave hello 邀請組織，Microsoft 努力提供這項功能。  這項功能可用之前，您可以詢問 hello 邀請組織 tooremove 您從其租用戶。
- - -
**問： 如何連線我在內部部署目錄 tooAzure AD？**

**答：**您可以使用 Azure AD Connect 連接您在內部部署目錄 tooAzure AD。

如需詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

- - -
**問︰如何設定內部部署目錄與雲端應用程式之間的 SSO？**

**答：**您只需要單一登入 (SSO) 在內部部署目錄與 Azure AD 之間的 tooset。 只要您透過 Azure AD 存取雲端應用程式，則 hello 服務自動磁碟機 toocorrectly 向其內部部署認證您的使用者。

透過同盟解決方案 (例如 Active Directory Federation Services (AD FS)) 或藉由設定密碼雜湊同步處理，就能輕鬆實現從內部部署實作 SSO。您可以使用 hello Azure AD Connect 設定精靈，輕鬆部署這兩個選項。

如需詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

- - -
**問︰Azure AD 是否可為組織中的使用者提供自助入口網站？**

**答：**是，Azure AD 為您提供 hello [Azure AD 存取面板](http://myapps.microsoft.com)自助使用者和應用程式的存取。 如果您是 Office 365 客戶，您可以找到 hello 的許多相同的功能在 hello Office 365 入口網站。

如需詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

- - -
**問︰Azure AD 是否會協助我管理內部部署基礎結構？**

**答：** 是。 hello Azure AD Premium edition 提供 Azure AD Connect Health。 Azure AD Connect Health 可協助您監視及了解您的內部部署身分識別基礎結構和 hello 同步處理服務。  

如需詳細資訊，請參閱[監視您內部部署識別基礎結構和同步處理雲端中的服務 hello](active-directory-aadconnect-health.md)。  

- - -
## <a name="password-management"></a>密碼管理
**問︰是否可以使用 Azure AD 密碼回寫，但不使用密碼同步處理？（在此案例中，是它可能 toouse Azure AD 自助式密碼重設 (SSPR) 與 hello 雲端中的密碼回寫並儲存密碼嗎？）**

**答：**您不需要 toosynchronize 您 Active Directory 密碼 tooAzure AD tooenable 回寫。 在同盟環境中，Azure AD 單一登入 (SSO) 依賴 hello 在內部部署目錄 tooauthenticate hello 使用者。 這種情況下不需要在 Azure AD 中追蹤 hello 在內部部署密碼 toobe。

- - -
**問： 如何花費時間的回寫 tooActive Directory 內部部署密碼 toobe？**

**答：**密碼回寫會即時運作。

如需詳細資訊，請參閱[開始使用密碼管理](active-directory-passwords-getting-started.md)。

- - -
**問︰是否可以搭配使用密碼回寫和由系統管理員管理的密碼？**

**答：**是，如果您有密碼回寫啟用時，系統管理員所執行的 hello 密碼作業被寫回 tooyour 在內部部署環境。  

如需詳細的解答 toopassword 相關的問題，請參閱[密碼管理常見問題集](active-directory-passwords-faq.md)。
- - -
**問： 如果我不記得我現有的 Office 365/Azure AD 密碼嘗試 toochange 我的密碼時，我可以做什麼？**

**答︰**在這種情況下有幾種做法。  使用自助式密碼重設 (SSPR) (如果可用的話)。  SSPR 能否運作取決於其設定方式。  如需詳細資訊，請參閱[方式沒有 hello 密碼重設入口網站工作](active-directory-passwords-best-practices.md)。

針對 Office 365 使用者，您的系統管理員可以使用重設 hello 密碼 hello 中所述的步驟[重設使用者密碼](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US)。

Azure AD 帳戶管理員可以重設密碼，利用 hello 下列其中一種：

- [重設 hello Azure 入口網站中的帳戶](active-directory-users-reset-password-azure-portal.md)
- [重設 hello 傳統入口網站中的帳戶](active-directory-create-users-reset-password.md)
- [使用 PowerShell](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>安全性
**問︰帳戶會在特定次數的嘗試失敗之後鎖定，或者是否使用更複雜的策略？**</br>
我們會使用更複雜的策略 toolock 帳戶。  這根據 hello IP hello 要求和 hello 輸入的密碼。 hello hello 鎖定持續時間也會增加根據 hello，則攻擊的可能性。  

**問： 特定 （一般） 密碼取得拒絕以 hello 訊息 '此密碼已使用的 toomany 次'，此參考 toopasswords hello 目前的 active directory 中使用嗎？**</br>
這是指 toopasswords 全域通用，例如 「 密碼 」 的任何變數和"123456"。

**問︰來自可疑來源 (殭屍網路、Tor 端點) 的登入要求是否會在 B2C 租用戶中遭到封鎖，或者需要基本或進階版本租用戶？**</br>
我們沒有適用於所有 B2C 租用戶的閘道，可篩選要求並提供殭屍網路的一些防護功能。

## <a name="application-access"></a>應用程式存取
**問︰哪裡可以找到與 Azure AD 預先整合的應用程式及其功能的清單？**

**答：** Azure AD 擁有來自 Microsoft、應用程式服務提供者或協力廠商超過 2600 個預先整合的應用程式。 所有預先整合的應用程式皆支援單一登入 (SSO)。 SSO 可讓您使用您的組織認證 tooaccess 應用程式。 某些 hello 應用程式也支援自動佈建和解除佈建。

Hello 預先整合應用程式的完整清單，請參閱 hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/)。

- - -
**問： 如果 hello 我需要的應用程式不在 hello Azure AD 服務商場嗎？**

**答：**若您使用 Azure AD Premium，就可以新增及設定您想要的任何應用程式。 視應用程式功能和您的喜好設定而定，您可以設定 SSO 和自動化佈建。  

如需詳細資訊，請參閱：

* [設定單一登入 tooapplications 不在 hello Azure Active Directory 應用程式庫](active-directory-saas-custom-apps.md)
* [使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組](active-directory-scim-provisioning.md)

- - -
**問： 如何使用者登入 tooapplications 使用 Azure AD？**

**答：** Azure AD 使用者 tooview 提供數種方式，並存取其應用程式，例如：

* hello Azure AD 存取面板
* hello Office 365 應用程式啟動器
* 直接登入 toofederated 應用程式
* 深層連結 toofederated，密碼為基礎或現有的應用程式

如需詳細資訊，請參閱[部署 Azure AD 整合的應用程式 toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)。

- - -
**問： 什麼是 Azure AD hello 不同方式，可讓驗證和單一登入 tooapplications 嗎？**

**答：**Azure AD 針對驗證和授權支援許多標準化的通訊協定，例如 SAML 2.0、OpenID Connect、OAuth 2.0 和 WS-同盟。 Azure AD 也可針對僅支援表單型驗證的應用程式，支援密碼存放和自動化登入功能。  

如需詳細資訊，請參閱：

* [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)
* [Active Directory 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [單一登入如何搭配 Azure Active Directory 運作？](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
**問︰是否可以新增在內部部署中執行的應用程式？**

**答：** Azure AD Application Proxy 可讓您輕鬆且安全存取您選擇的 tooon 內部部署 web 應用程式。 您可以存取這些應用程式在 hello 做為服務 (SaaS) 應用程式存取您的軟體，在 Azure AD 中的方式相同。 沒有需要 VPN 或 toochange 網路基礎結構。  

如需詳細資訊，請參閱[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)。

- - -
**問︰如何對存取特定應用程式的使用者要求 Multi-Factor Authentication？**

**答：** Azure AD 條件式存取可讓您針對每個應用程式指派唯一的存取原則。 在您的原則，您可以進行多重要素驗證一律，或當使用者不屬於連接的 toohello 區域網路。  

如需詳細資訊，請參閱[tooOffice 365 和其他應用程式保護的存取連接 tooAzure Active Directory](active-directory-conditional-access.md)。

- - -
**問︰SaaS 應用程式的自動化使用者佈建是什麼？**

**答：**使用 Azure AD tooautomate hello 建立、 維護和移除許多熱門的雲端 SaaS 應用程式中的使用者識別。

如需詳細資訊，請參閱[自動化使用者佈建和解除佈建 tooSaaS 應用程式與 Azure Active Directory](active-directory-saas-app-provisioning.md)。

- - -
**問︰是否可以設定與 Azure AD 之間的安全 LDAP 連線？**

**答：**否。 Azure AD 不支援 hello LDAP 通訊協定。
