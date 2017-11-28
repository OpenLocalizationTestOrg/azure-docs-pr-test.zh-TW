---
title: "Azure Active Directory 中的應用程式管理的索引 aaaArticle |Microsoft Azure"
description: "了解如何 toocustomize hello 到期日您同盟的憑證，和如何 toorenew 憑證即將到期。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Azure Active Directory 中應用程式管理的文章索引
此頁面會提供撰寫 hello 有關應用程式相關的各種功能的 Azure Active Directory (Azure AD) 的每個文件的完整清單。

沒有簡單介紹 tooeach 主要功能區域中，以及根據您要尋找哪些資訊的發行項 tooread 指引。

## <a name="overview-articles"></a>概觀文章
做為優值以下的 hello 文章起點的人員只需要 Azure AD 應用程式管理功能的簡短說明。

| 文章指南 |  |
|:---:| --- |
| Azure AD 來解決簡介 toohello 應用程式管理問題 |[使用 Azure Active Directory (AD) 管理應用程式](active-directory-enable-sso-scenario.md) |
| Hello 概觀在 Azure AD 中的各種功能與相關 tooenabling 單一登入，定義誰可以存取 tooapps，和使用者啟動應用程式的方式 |[Azure Active Directory 中的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md) |
| 查看 hello 整合到您的 Azure AD 的應用程式時所需的不同步驟 |[整合 Azure Active Directory 與應用程式](active-directory-integrating-applications-getting-started.md)<br /><br />[啟用單一登入 tooSaaS 應用程式](active-directory-sso-integrate-saas-apps.md)<br /><br />[管理存取 tooApps](active-directory-managing-access-to-apps.md) |
| 如何在 Azure AD 中表示應用程式的技術說明 |[將應用程式如何及為何加入 tooAzure AD](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>疑難排解文章
本節提供快速存取 toorelevant 疑難排解指引。 可以找到每個功能區域的詳細資訊，在 hello rest 的此頁面上。

| 功能範圍 |  |
|:---:| --- |
| 同盟單一登入 |[對 SAML 型單一登入進行疑難排解](active-directory-saml-debugging.md) |
| 密碼單一登入 |[疑難排解 hello Internet explorer 的 存取面板延伸模組](active-directory-saas-ie-troubleshooting.md) |
| 應用程式 Proxy |[應用程式 Proxy 疑難排解指南](active-directory-application-proxy-troubleshoot.md) |
| 內部部署 AD 與 Azure AD 之間的單一登入 |[針對密碼同步處理進行疑難排解](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[對密碼回寫進行疑難排解](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| 動態群組成員資格 |[對動態群組成員資格進行疑難排解](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>單一登入 (SSO)
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>同盟單一登入：使用一個身分識別登入多個應用程式
單一登入可讓使用者 tooaccess 各種應用程式和服務使用只有一組認證。 您可以透過同盟這種方法啟用單一登入。 當使用者嘗試 toosign 入同盟應用程式時，他們將取得重新導向的 tootheir 組織的官方登入頁面上轉譯的 Azure Active Directory，然後會重新導向後 toohello 驗證成功後的應用程式。

| 文章指南 |  |
|:---:| --- |
| 簡介 toofederation 和其他類型的登入 |[使用 Azure AD 進行單一登入](active-directory-appssoaccess-whatis.md) |
| 透過已簡化摸單一登入設定步驟，與 Azure AD 預先整合的數千個 SaaS 應用程式 |[開始使用 hello Azure AD 應用程式庫](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[支援同盟的預先整合應用程式完整清單](http://aka.ms/aadfederatedapps)<br /><br />[如何 tooAdd 您的應用程式 toohello Azure AD App 資源庫](active-directory-app-gallery-listing.md) |
| 上如何 tooconfigure 單一登入應用程式的這類 150 個以上的應用程式教學課程[Salesforce](active-directory-saas-salesforce-tutorial.md)， [ServiceNow](active-directory-saas-servicenow-tutorial.md)， [Google Apps](active-directory-saas-google-apps-tutorial.md)， [Workday](active-directory-saas-workday-tutorial.md)，以及更多其他 |[如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md) |
| Toomanually 如何設定及自訂您的單一登入組態 |[如何 tooConfigure 同盟單一登入 tooApps 所沒有的 hello Azure Active Directory 應用程式庫](active-directory-saas-custom-apps.md)<br /><br />[如何 tooCustomize 中發出的宣告 hello SAML 權杖 Pre-Integrated 應用程式](active-directory-saml-claims-customization.md) |
| 疑難排解使用 hello SAML 通訊協定的同盟應用程式的指南 |[SAML 型單一登入疑難排解](active-directory-saml-debugging.md) |
| 如何 tooconfigure 您的應用程式憑證的到期日，以及如何 toorenew 您的憑證 |[在 Azure Active Directory 中管理同盟單一登入的憑證](active-directory-sso-certs.md) |

同盟單一登入適用於所有版本的 Azure AD 進行向上 tooten 每位使用者的應用程式。 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 支援無限多個應用程式。 如果您的組織有[Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/)或[Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)，則您可以[使用群組 tooassign 存取 toofederated 應用程式](#managing-access-to-applications)。

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>密碼型單一登入：非同盟應用程式的帳戶共用和 SSO
tooenable 單一登入 tooapplications 不支援同盟，Azure AD 提供的密碼管理功能，可安全地存放密碼 tooSaaS 應用程式及自動登入這些應用程式的使用者。 您可以輕鬆地散發新建立帳戶的認證，並與多人共用小組帳戶。 使用者不一定需要 tooknow hello 認證 toohello 帳戶獲得存取權。

| 文章指南 |  |
|:---:| --- |
| 簡介 toohow 密碼型 SSO 運作，以及簡短的技術概觀 |[使用 Azure AD 進行密碼型單一登入](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Hello 案例的摘要相關 tooaccount 共用，以及如何解決這些問題會由 Azure AD |[使用 Azure AD 共用帳戶](active-directory-sharing-accounts.md) |
| 自動定期變更 hello 特定應用程式密碼 |[自動密碼變換 (預覽)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| 部署及疑難排解指南 hello Internet Explorer 版本的 hello Azure AD 密碼管理延伸模組 |[如何 tooDeploy hello Internet explorer 使用群組原則的存取面板延伸模組](active-directory-saas-ie-group-policy.md)<br /><br />[疑難排解 hello Internet explorer 的 存取面板延伸模組](active-directory-saas-ie-troubleshooting.md) |

密碼型單一登入適用於所有版本的 Azure AD 進行向上 tooten 每位使用者的應用程式。 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 支援無限多個應用程式。 如果您的組織有[Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/)或[Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)，則您可以[使用群組 tooassign 存取 tooapplications](#managing-access-to-applications)。 自動密碼變換是一項 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 功能。

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>應用程式 Proxy： 單一登入及遠端存取 tooon 內部部署應用程式
如果您有需要 toobe 使用者和裝置 hello 網路外部存取您私人網路中的應用程式，您可以使用 Azure AD Application Proxy tooenable 安全、 遠端存取 toothose 應用程式。

| 文章指南 |  |
|:---:| --- |
| Azure AD 應用程式 Proxy 及其運作方式的概觀 |[Tooon 內部部署應用程式提供安全的遠端存取](active-directory-application-proxy-get-started.md) |
| 教學課程有關 tooconfigure 應用程式 Proxy 及如何 toopublish 第一個應用程式 |[如何 tooSet 註冊 Azure AD 應用程式 Proxy](active-directory-application-proxy-enable.md)<br /><br />[如何安裝 tooSilently hello 應用程式 Proxy 連接器](active-directory-application-proxy-silent-installation.md)<br /><br />[如何 tooPublish 應用程式使用應用程式 Proxy](active-directory-application-proxy-publish.md)<br /><br />[如何 tooUse 您自己的網域名稱](active-directory-application-proxy-custom-domains.md) |
| Tooenable 單一登入和條件式存取的應用程式的方式發佈應用程式 proxy |[使用應用程式 Proxy 進行單一登入](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[條件式存取和應用程式 Proxy](active-directory-application-proxy-conditional-access.md) |
| 指示如何針對下列案例的 hello toouse 應用程式 Proxy |[如何 tooSupport 原生用戶端應用程式](active-directory-application-proxy-native-client.md)<br /><br />[如何 tooSupport 宣告感知應用程式](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[TooSupport 應用程式如何發行對個別的網路和位置](active-directory-application-proxy-connectors.md) |
| 應用程式 Proxy 的疑難排解指南 |[應用程式 Proxy 疑難排解指南](active-directory-application-proxy-troubleshoot.md) |

應用程式 Proxy 是適用於所有版本的 Azure AD 進行向上 tooten 每位使用者的應用程式。 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 支援無限多個應用程式。 如果您的組織有[Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/)或[Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)，則您可以[使用群組 tooassign 存取 tooapplications](#managing-access-to-applications)。

您可能也會想要[Azure AD 網域服務](../active-directory-domain-services/active-directory-ds-overview.md)，可讓您 toomigrate 仍然滿足 hello 識別您在內部部署應用程式 tooAzure 需要這些應用程式。

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>在 Azure AD 與內部部署 AD 之間啟用單一登入
如果您的組織會維持在內部部署與 Azure Active Directory hello 雲端中的 Windows Server Active Directory，則您可能會想 tooenable 單一登入這兩個系統之間。 Azure AD Connect （hello 工具，將這兩個系統整合在一起） 提供多個設定單一登入選項： 建立同盟，使用 ADFS 或另一個同盟提供者，或啟用密碼同步處理。

| 文章指南 |  |
|:---:| --- |
| 在 Azure AD Connect，以及有關管理混合式環境中提供需 hello 單一登入選項的概觀 |[Azure AD Connect 中的使用者登入選項](active-directory-aadconnect-user-signin.md) |
| 同時使用內部部署 Active Directory 和 Azure Active Directory 管理環境的一般指引 |[Azure AD 混合式身分識別設計考量](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md) |
| 使用密碼同步 tooenable SSO 的指引 |[使用 Azure AD Connect 實作密碼同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[對密碼同步處理進行疑難排解](https://support.microsoft.com/en-us/kb/2855271) |
| 使用密碼回寫 tooenable SSO 的指引 |[在 Azure AD 中開始使用密碼管理](active-directory-passwords-getting-started.md)<br /><br />[疑難排解密碼回寫](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| 使用協力廠商身分識別提供者 tooenable SSO 的指引 |[將 tooEnable 相容協力廠商身分識別提供者，可以使用單一登入的清單](https://aka.ms/ssoproviders) |
| 如何 Windows 10 使用者可以享受 hello 優點的單一登入透過 Azure AD Join |[擴充雲端功能 tooWindows 10 的裝置透過 Azure Active Directory Join](active-directory-azureadjoin-overview.md) |

Azure AD Connect 適用於 [所有版本的 Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)。 「Azure AD 自助式密碼重設」適用於 [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) 和 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)。 密碼回寫 tooon 內部部署 AD 是[Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)功能。

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>條件式存取：強制高風險應用程式符合額外的安全性需求
一旦您設定單一登入 tooyour 應用程式及資源，您就可以進一步保護機密應用程式藉由強制執行每一個登入 toothat 應用程式的特定安全性需求。 比方說，您可以使用 Azure AD toodemand 所有存取 tooa 特定應用程式一律都需要多重要素驗證，無論該應用程式本來就具有支援該功能。 條件式存取的另一個常見範例是 toorequire 使用者是連接的 toohello 組織的受信任網路中的順序 tooaccess 特別機密的應用程式。

| 文章指南 |  |
|:---:| --- |
| 簡介 toohello 條件式存取功能提供跨 Azure AD，Office365，與 Intune |[使用條件式存取管理風險](active-directory-conditional-access.md) |
| Tooenable 條件式存取 hello 下列類型的資源的方式 |[SaaS 應用程式的條件式存取](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Office 365 服務的條件式存取](active-directory-conditional-access-device-policies.md)<br /><br />[內部部署應用程式的條件式存取](active-directory-conditional-access.md)<br /><br />[透過 Azure AD 應用程式 Proxy 發佈之內部部署應用程式的條件式存取](active-directory-application-proxy-conditional-access.md) |

|Tooregister 裝置與 Azure Active Directory 的排列方式 tooenable 裝置型條件式存取原則 |[的 Azure Active Directory 裝置註冊概觀](active-directory-conditional-access-device-registration-overview.md)<br /><br />[如何 tooEnable 網域加入的 Windows 裝置的自動裝置註冊](active-directory-conditional-access-automatic-device-registration.md)<br />— [適用於 Windows 8.1 裝置的步驟](active-directory-conditional-access-automatic-device-registration-setup.md)<br />— [適用於 Windows 7 裝置的步驟](active-directory-conditional-access-automatic-device-registration-setup.md) |

|Toouse hello 進行兩步驟驗證的 Microsoft 驗證器應用程式的方式 |[Microsoft 驗證器](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

「條件式存取」是一項 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 功能。

## <a name="apps--azure-ad"></a>應用程式和 Azure AD
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>Cloud App Discovery：尋找您的組織使用哪些 SaaS 應用程式
Cloud App Discovery 有助於了解 hello 組織正在使用的 SaaS 應用程式的 IT 部門。 它可以測量應用程式使用量和熱門程度，讓它可以判斷哪些應用程式將會改善效能 hello 充分利用正在受到 IT 控制和要整合 Azure AD。

| 文章指南 |  |
|:---:| --- |
| 其運作方式的一般概觀 |[使用 Cloud App Discovery 尋找未經約束的雲端應用程式](active-directory-cloudappdiscovery-whatis.md) |
| 它的運作方式與答案 tooquestions [隱私權] 深入剖析 |[安全性和隱私權考量](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| 常見問題集 |[Cloud App Discovery 的常見問題集](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| 部署 Cloud App Discovery 的教學課程 |[群組原則部署指南](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[System Center 部署指南](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[在具有自訂連接埠的 Proxy 伺服器上安裝](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| hello 變更記錄檔以取得更新 toohello Cloud App Discovery 代理程式 |[變更記錄檔](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

Cloud App Discovery 是一項 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 功能。

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>自動佈建和取消佈建 SaaS 應用程式中的使用者帳戶
自動化 hello 建立、 維護和使用者身分識別等 Dropbox、 Salesforce、 ServiceNow，以及更多的 SaaS 應用程式中移除。 比對及同步處理 Azure AD 之間的現有身分識別 SaaS 應用程式和控制存取權會自動停用帳戶，當使用者離開組織 hello。

| 文章指南 |  |
|:---:| --- |
| 深入了解其運作方式，並尋找答案 toocommon 問題 |[自動化使用者佈建和取消佈建 tooSaaS 應用程式](active-directory-saas-app-provisioning.md) |
| 設定如何在 Azure AD 與您的 SaaS 應用程式之間對應資訊 |[自訂屬性對應](active-directory-saas-customizing-attribute-mappings.md)<br><br>[撰寫屬性對應的運算式](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Tooenable 自動化佈建支援 hello SCIM 通訊協定的 tooany 應用程式的方式 |[設定自動化使用者佈建 tooany SCIM-Enabled 應用程式](active-directory-scim-provisioning.md) |
| 如何在 tooreport 及疑難排解使用者佈建 |[關於使用者自動佈建的報告](active-directory-saas-provisioning-reporting.md)<br><br>[佈建通知](active-directory-saas-account-provisioning-notifications.md)<br><br>[針對使用者佈建進行疑難排解](active-directory-application-provisioning-content-map.md) |
| 取得其屬性值為基礎的佈建的 tooan 應用程式的限制 |[範圍篩選器](active-directory-saas-scoping-filters.md) |

自動的使用者佈建適用於所有版本的 Azure AD 進行向上 tooten 每位使用者的應用程式。 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 支援無限多個應用程式。 如果您的組織有[Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/)或[Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)，則您可以[使用哪些使用者取得佈建群組 toomanage](#managing-access-to-applications)。

### <a name="building-applications-that-integrate-with-azure-ad"></a>建置與 Azure AD 整合的應用程式
如果您的組織是開發或維護的特定業務 (LoB) 應用程式，或如果您使用 Azure Active Directory 的客戶與應用程式開發人員，hello 遵循教學課程將協助您與 Azure AD 整合您的應用程式。

| 文章指南 |  |
|:---:| --- |
| 有關 IT 專業人員和應用程式開發人員整合應用程式與 Azure AD 的指南 |[hello IT 專業人員的 Azure ad 開發的應用程式的指南](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Azure Active directory 的 hello 開發人員指南](active-directory-developers-guide.md) |
| 如何 tooapplication 廠商可以在其中加入他們的應用程式 toohello Azure AD App 資源庫 |[列出在 hello Azure Active Directory 應用程式庫中的應用程式](active-directory-app-gallery-listing.md) |
| Toomanage 如何存取 toodeveloped 應用程式使用 Azure Active Directory |[如何 tooEnable 開發應用程式的使用者指派](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[指派使用者 tooyour 應用程式](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[指派群組 tooyour 應用程式](active-directory-applications-guiding-developers-assigning-groups.md) |

如果您正在開發消費者導向應用程式，您可能會想要使用[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) ，所以您不需要 toodevelop 您自己的身分識別系統 toomanage 您的使用者。 [深入了解](../active-directory-b2c/active-directory-b2c-overview.md)。

## <a name="managing-access-tooapplications"></a>管理存取 tooApplications
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>使用群組和自助 toomanage 擁有存取 toowhich 應用程式
您應該擁有存取 toowhich 資源管理 toohelp，Azure Active Directory 可讓您 tooset 指派和權限以使用群組的規模。 IT 可能選擇 tooenable 自助功能，以便在需要時，使用者可以直接要求權限。

| 文章指南 |  |
|:---:| --- |
| Azure AD 存取管理功能的概觀 |[簡介 tooManaging 存取 tooApps](active-directory-managing-access-to-apps.md)<br /><br />[Azure AD 中的存取管理運作方式](active-directory-manage-groups.md)<br /><br />[如何 tooUse 群組 tooManage 存取 tooSaaS 應用程式](active-directory-accessmanagement-group-saasapps.md) |
| 啟用應用程式和群組的自助式管理 |[自助式應用程式管理](active-directory-self-service-application-access.md)<br /><br />[自助式群組管理](active-directory-accessmanagement-self-service-group-management.md) |
| 在 Azure AD 設定群組的指示 |[如何 tooCreate 安全性群組](active-directory-accessmanagement-manage-groups.md)<br /><br />[如何 tooDesignate 群組的擁有者](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[如何 tooUse hello"All Users"群組](active-directory-accessmanagement-dedicated-groups.md) |
| 使用動態群組 tooautomatically 填入群組成員資格使用以屬性為基礎的成員資格規則 |[動態成員資格：進階規則](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[對動態群組成員資格進行疑難排解](active-directory-accessmanagement-troubleshooting.md) |

群組型應用程式存取管理適用於 [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) 和 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/)。 自助式群組管理、自助式應用程式管理以及動態群組是 [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) 功能。

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>B2B 共同作業： 啟用協力廠商存取 tooapplications
如果您的企業已經建立合作關係，與其他公司，很可能就需要 toomanage 夥伴存取 tooyour 公司應用程式。 Azure Active Directory B2B 共同作業提供簡單且安全的方式 tooshare 與協力廠商應用程式。

| 文章指南 |  |
|:---:| --- |
| 不同 Azure AD 功能的概觀，協助您管理外部使用者，例如合作夥伴、 客戶等。 |[比較 Azure AD 中管理外部身分識別的功能](active-directory-b2b-compare-external-identities.md) |
| 簡介 tooB2B 共同作業和 tooget 啟動的方式 |[與 Azure AD 的簡單安全雲端合作夥伴整合](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Azure Active Directory B2B 共同作業](active-directory-b2b-collaboration-overview.md) |
| 深入探討 Azure AD B2B 共同作業和如何 toouse 它 |[B2B 共同作業：運作方式](active-directory-b2b-how-it-works.md)<br /><br />[Azure AD B2B 共同作業目前的限制](active-directory-b2b-current-limitations.md)<br /><br />[使用 Azure AD B2B 共同作業的詳細逐步解說](active-directory-b2b-detailed-walkthrough.md) |
| 具有 Azure AD B2B 共同作業如何運作的技術詳細資料參考文章 |[適用於新增合作夥伴使用者的 CSV 檔案格式](active-directory-b2b-references-csv-file-format.md)<br /><br />[受 Azure AD B2B 共同作業影響的使用者屬性](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[合作夥伴使用者的使用者權杖格式](active-directory-b2b-references-external-user-token-format.md) |

「B2B 共同作業」目前適用於[所有版本的 Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)。

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>存取面板：存取應用程式和自助式功能的入口網站
hello Azure AD 存取面板是其中使用者可以啟動其應用程式和存取 hello 自助功能，以允許他們 toomanage 其應用程式和群組成員資格。 除了下面的 hello 清單中包含 toohello 存取面板中，存取已啟用 SSO 的應用程式的其他選項。

| 文章指南 |  |
|:---:| --- |
| Hello 不同選項可供部署單一登入應用程式 toousers 比較 |[部署 Azure AD 整合的應用程式 tooUsers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Hello 存取面板和其行動裝置的對等 MyApps 的概觀 |[簡介 tooAccess 面板和 MyApps](active-directory-saas-access-panel-introduction.md)<br />— [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| Tooaccess Azure AD 應用程式從 hello Office 365 網站的方式 |[使用 Office 365 應用程式啟動器 hello](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| 如何從 tooaccess Azure AD 應用程式 hello Intune Managed Browser 行動裝置應用程式 |[Intune Managed Browser](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| 使用深層連結 tooinitiate tooaccess Azure AD 應用程式的單一登入 |[取得直接登入連結 tooYour 應用程式](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

「存取面板」適用於 [所有版本的 Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)。

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>報告： 輕鬆地稽核存取的應用程式變更，並監視登入 tooapps
Azure Active Directory 提供數個報表和警示 toohelp 監視貴組織的存取 tooapplications。 您可以接收的異常的登入 tooyour 應用程式，警示，而且您可以追蹤何時及使用者的存取 tooan 應用程式已變更的原因。

| 文章指南 |  |
|:---:| --- |
| Hello 報告 Azure Active Directory 功能的概觀 |[開始使用 Azure AD 報告](active-directory-reporting-getting-started.md) |
| 如何 toomonitor hello 登入和使用者的應用程式使用方式 |[檢視存取和使用情況報告](active-directory-view-access-usage-reports.md) |
| 追蹤變更 toowho 可以存取特定應用程式 |[Azure Active Directory 稽核報告事件](active-directory-reporting-audit-events.md) |
| 使用這些報表 tooyour 慣用工具匯出 hello 資料 hello 報告 API |[開始使用 hello Azure AD 報告 API](active-directory-reporting-api-getting-started.md) |

哪些報表所含不同版本的 Azure Active Directory，toosee[按一下這裡](active-directory-view-access-usage-reports.md)。

## <a name="see-also"></a>另請參閱
[什麼是 Azure Active Directory？](active-directory-whatis.md)

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)

[Azure Active Directory 網域服務](https://azure.microsoft.com/services/active-directory-ds/)

[Azure Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/)
