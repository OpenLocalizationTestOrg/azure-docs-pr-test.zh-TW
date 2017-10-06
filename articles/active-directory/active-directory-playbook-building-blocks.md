---
title: "aaaAzure 證明概念腳本建置組塊的 Active Directory |Microsoft 文件"
description: "探索並快速實作身分識別和存取管理案例"
services: active-directory
keywords: "azure active directory, 腳本, 概念證明, PoC"
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Azure Active Directory 概念證明腳本：構成要素

## <a name="catalog-of-roles"></a>角色目錄

| 角色 | 說明 | 概念證明 (PoC) 責任 |
| --- | --- | --- |
| **身分識別架構 / 開發小組** | 這個小組通常是 hello 一個設計 hello 方案、 實作原型，磁碟機的核准，且最後互相 toooperations | 可提供 hello 環境並且 hello 的評估 hello 不同情況下，從 hello 管理的角度 |
| **內部部署身分識別作業小組** | 管理 hello 不同的身分識別來源內部部署： Active Directory 樹系、 LDAP 目錄、 HR 系統和同盟身分識別提供者。 | 提供存取 tooon 內部部署資源所需的 hello PoC 案例。<br/>應該儘量不要牽涉到他們|
| **應用程式技術擁有者** | Hello 不同的雲端應用程式和服務，將會與 Azure AD 整合技術擁有者 | 提供有關 SaaS 應用程式 (可能是用於測試的執行個體) 的詳細資料 |
| **Azure AD 全域管理員** | 管理 hello Azure AD 組態 | 提供的認證 tooconfigure hello 同步處理服務。 通常在 PoC hello 相同小組的識別架構但區分 hello 作業階段|
| **資料庫小組** | Hello 資料庫基礎結構的擁有者 | 提供存取 tooSQL 環境 （ADFS 或 Azure AD Connect） 的特定案例的準備工作。<br/>應該儘量不要牽涉到他們 |
| **網路小組** | Hello 網路基礎結構的擁有者 | 提供必要存取權 hello 網路層級 hello 同步處理伺服器 tooproperly 存取 hello 資料來源及雲端服務 （防火牆規則、 開啟的連接埠、 IPSec 規則等等）。 |
| **安全性小組** | 定義 hello 安全性策略、 分析安全性報告從各種來源，並會遵循的結果。 | 提供目標安全性評估案例 |

## <a name="common-prerequisites-for-all-building-blocks"></a>所有構成要素的一般必要條件

以下是 Azure AD Premium 之任何 POC 都需要的一些必要條件。

| 必要條件 | 資源 |
| --- | --- |
| 已定義有效 Azure 訂用帳戶的 Azure AD 租用戶 | [Tooget Azure Active Directory 的租用戶](active-directory-howto-tenant.md)<br/>**注意：**如果您已經有 Azure AD Premium 授權的環境，您可以藉由瀏覽 toohttps://aka.ms/accessaad 取得零 cap 訂用帳戶 <br/>深入了解：https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ and https://technet.microsoft.com/library/dn832618.aspx |
| 已定義並確認的網域 | [新增自訂網域名稱 tooAzure Active Directory](active-directory-domains-add-azure-portal.md)<br/>**注意：**某些工作負載，例如 Power BI 無法佈建 azure AD 租用戶下 hello 涵蓋。 toocheck 如果有指定的網域是相關聯的 tooa 租用戶中，瀏覽 toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration。 如果您取得成功的回應，則 hello 網域已指派 tooa 租用戶，並可能會需要。 如果是這種情況，請連絡 Microsoft 以獲得進一步的指導。 深入了解在 hello 接管選項：[何謂 azure 的自助註冊？](active-directory-self-service-signup.md) |
| 已啟用 Azure AD Premium 或 EMS 試用版 | [Azure Active Directory Premium 可免費使用一個月](https://azure.microsoft.com/trial/get-started-active-directory/) |
| 您已指派 Azure AD Premium 或 EMS 授權 tooPoC 使用者 | [在 Azure Active Directory 中進行自身和使用者的授權](active-directory-licensing-get-started-azure-portal.md) |
| Azure AD 全域管理員認證 | [在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles-azure-portal.md) |
| 選擇性但強烈建議使用：作為後援的平行實驗室環境 | [Azure AD Connect 的必要條件](./connect/active-directory-aadconnect-prerequisites.md) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>目錄同步作業 - 密碼雜湊同步處理 (PHS) - 全新安裝

近似時間 tooComplete： 小於 1,000 PoC 使用者一小時

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 伺服器 tooRun Azure AD Connect | [Azure AD Connect 的必要條件](./connect/active-directory-aadconnect-prerequisites.md) |
| 目標中 hello 的 POC 使用者相同的網域和安全性群組和 OU 的一部分 | [自訂 Azure AD Connect 安裝](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Azure AD 連接所需的功能會識別 POC hello | [將 Active Directory 與 Azure Active Directory 連接 - 設定同步處理功能](./connect/active-directory-aadconnect.md#configure-sync-features) |
| 您有內部部署和雲端環境所需的認證  | [Azure AD Connect：帳戶與權限](./connect/active-directory-aadconnect-accounts-permissions.md) |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 下載 Azure AD Connect hello 最新版本 | [下載 Microsoft Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594) |
| 安裝 Azure AD Connect 與 hello 簡單的路徑： Express <br/>1.篩選 toohello 目標 OU toominimize hello 同步處理週期時間<br/>2.Hello 內部群組中選擇目標集的使用者。<br/>3.部署所需的 hello 其他 POC 佈景主題的 hello 功能 | [Azure AD Connect：自訂安裝：網域和 OU 篩選](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect：自訂安裝：群組型篩選](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect：整合內部部署身分識別與 Azure Active Directory：設定同步處理功能](./connect/active-directory-aadconnect.md#configure-sync-features) |
| 開啟 hello Azure AD Connect UI，並查看執行中的 hello 設定檔已完成 （匯入、 同步處理，與匯出） | [Azure AD Connect 同步處理：排程器](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| 開啟 hello [Azure AD 管理入口網站](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/)、 移 toohello"All Users"刀鋒視窗中，新增 「 授權來源 」 資料行顯示 hello 使用者，請參閱適當地標示為來自 Windows Server AD 」 | [Azure AD 管理入口網站](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>考量

1. 查看 hello 安全性考量，密碼雜湊同步的[這裡](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)。  如果試驗生產使用者的密碼雜湊同步處理針對不是一個選項，請考慮下列替代方案的 hello:
   * Hello 實際執行網域中建立測試使用者。 確定您不會同步處理任何其他帳戶
   * 移動 tooan 使用者接受度測試環境
2.  如果您想 toopursue 同盟，值得 toounderstand hello 成本超過 hello POC 的內部部署身分識別提供者相關聯的同盟的解決方案和量值會針對 hello 優勢在於，您要尋找：
    * 因此您需要高可用性的 toodesign 是 hello 關鍵路徑中
    * 這是您需要 toocapacity 計劃在內部部署服務
    * 它是在內部部署服務，您需要 toomonitor/維護/patch

深入了解：[了解 Office 365 身分識別和 Azure Active Directory - 同盟身分識別](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>商標

近似時間 tooComplete: 15 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 資產 （映像、 標誌、 等等）。最佳的視覺效果中，請確定 hello 資產有 hello 建議的大小。 | [新增公司品牌 tooyour 登入頁面 hello Azure Active Directory 中](active-directory-branding-custom-signon-azure-portal.md) |
| 選擇性： 如果 hello 環境具有 ADFS 伺服器，存取 toohello 伺服器 toocustomize 網頁佈景主題 | [AD FS 使用者登入自訂](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| 用戶端電腦 tooperform 使用者登入體驗 |  |
| 選擇性： 行動裝置 toovalidate 體驗 |  |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 移 tooAzure AD 管理入口網站 | [Azure AD 管理入口網站 - 公司商標](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| 上傳 hello 資產 hello 登入頁面 （英雄標誌、 小標誌、 標籤、 等等）。 （選擇性） 如果您有 AD FS 時，對齊 hello 相同資產 ADFS 登入頁面 | [新增公司品牌 tooyour 登入和存取面板頁面： 可自訂的元素](active-directory-add-company-branding.md) |
| 等待幾分鐘的時間，hello 變更 toofully 生效 |  |
| 登入以 hello POC 使用者認證 toohttps://myapps.microsoft.com |  |
| 確認在瀏覽器中的 hello 外觀與風格 | [新增公司品牌 tooyour 登入和存取面板頁面](active-directory-add-company-branding.md) |
| （選擇性） 確認在其他裝置中的 hello 外觀與風格 |  |

### <a name="considerations"></a>考量

如果 hello 舊的外觀及操作保持 hello 自訂後再排清 hello 瀏覽器用戶端快取，然後重試 hello 作業。

## <a name="group-based-licensing"></a>群組型授權

近似時間 tooComplete: 10 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 所有 POC 使用者都是安全性群組 (不論是雲端還是內部部署) 的成員 | [在 Azure Active Directory 中建立群組和新增使用者](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 在 Azure AD 管理入口網站中移 toolicenses 刀鋒視窗 | [Azure AD 管理入口網站：授權](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| 指派 POC 使用者 hello 授權 toohello 安全性群組。 | [Azure Active Directory 中使用者的授權 tooa 群組指派](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>考量

發生任何問題，請移過[案例、 限制和已知的問題與使用 Azure Active Directory 中的群組 toomanage 授權](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>SaaS 同盟 SSO 組態

近似時間 tooComplete: 60 分鐘的時間

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 測試環境的 hello SaaS 應用程式。 在本指南中，我們將使用 ServiceNow 作為範例。<br/>我們強烈建議 toouse 上瀏覽現有的資料品質和對應的測試執行個體 toominimize 摩擦。 | 移 toohttps://developer.servicenow.com/app.do# ！ / 首頁 toostart hello 讓測試執行個體的處理程序 |
| 系統管理員存取 toohello ServiceNow 管理主控台 | [教學課程：Azure Active Directory 與 ServiceNow 整合](active-directory-saas-servicenow-tutorial.md) |
| 目標集的使用者 tooassign hello 應用程式。 建議包含 hello PoC 使用者的安全性群組。 <br/>如果正在建立 hello 群組並不可行的然後指派 hello 使用者 hello PoC toodirectly toohello 應用程式 | [指派的使用者或群組 tooan 企業應用程式在 Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 共用 Microsoft 文件中的 hello 教學課程 tooall 執行者  | [教學課程：Azure Active Directory 與 ServiceNow 整合](active-directory-saas-servicenow-tutorial.md) |
| 設定工作會議，並遵循 hello 教學課程步驟，與每個動作項目。 | [教學課程：Azure Active Directory 與 ServiceNow 整合](active-directory-saas-servicenow-tutorial.md) |
| 指派 hello 必要條件中所識別的 hello 應用程式 toohello 群組。 如果 hello POC hello 範圍內，有條件式存取，您可以再次瀏覽的更新版本，並將 MFA 和類似。 <br/>請注意這會開始運作 hello 佈建程序 （若已設定） |  [指派的使用者或群組 tooan 企業應用程式在 Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) <br/>[在 Azure Active Directory 中建立群組和新增使用者](active-directory-groups-create-azure-portal.md) |
| 使用 Azure AD 管理入口網站 tooadd ServiceNow 的應用程式庫中| [Azure AD 管理入口網站：企業應用程式](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[Azure Active Directory 中企業應用程式管理的新功能](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| 在 ServiceNow 應用程式的 [單一登入] 刀鋒視窗中，啟用 [SAML 登入] |  |
| 在 [單一登入 URL] 和 [識別碼] 欄位中填入您的 ServiceNow URL<br/>Hello] 核取方塊太 「 讓新的憑證使用中 」<br/>並 [儲存] 設定 |  |
| 開啟 」 設定 ServiceNow"刀鋒視窗上 hello 底部 hello 面板 tooview 自訂指示 tooconfigure ServiceNow |  |
| 請依照下列指示 tooconfigure ServiceNow |  |
| 在 ServiceNow 應用程式的 [佈建] 刀鋒視窗中，啟用 [自動] 佈建 | [管理企業中的應用程式 hello 新版 Azure 入口網站佈建使用者帳戶](active-directory-enterprise-apps-manage-provisioning.md) |
| 等候幾分鐘讓佈建完成。  在 [hello 同時，就可以檢查佈建報表的 hello |  |
| 有權存取的測試使用者身分登入 toohttps://myapps.microsoft.com/ | [Hello 存取面板是什麼？](active-directory-saas-access-panel-introduction.md) |
| 按一下剛建立的 hello 應用程式的 hello 磚。 確認存取 |  |
| （選擇性） 您可以檢查 hello 應用程式使用情況報告。 請注意一些延遲，因此您需要 toowait hello 報表中的某些時間 toosee hello 流量。 | [Hello Azure Active Directory 入口網站中的登入活動報表： 受管理的應用程式的使用量](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory 報告保留原則](active-directory-reporting-retention.md) |

### <a name="considerations"></a>考量

1. 上述[教學課程](active-directory-saas-servicenow-tutorial.md)參考 tooold Azure AD 管理體驗。 但 PoC 是根據[快速入門](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away)體驗。
2. 如果不存在於 hello 圖庫 hello 目標應用程式，您可以使用 「 攜帶您自己的應用程式 」。 深入了解：[Azure Active Directory 中企業應用程式管理的新功能：從一個位置新增自訂應用程式](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>SaaS 密碼 SSO 組態

近似時間 tooComplete: 15 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| SaaS 應用程式的測試環境。 其中一個「密碼 SSO」範例就是 HipChat 和 Twitter。 任何其他應用程式，您需要 hello hello 頁面的 html 登入表單的正確的 URL。 | [Microsoft Azure Marketplace 上的 Twitter](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Microsoft Azure Marketplace 上的 HipChat](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| 測試 hello 應用程式的帳戶。 | [註冊 Twitter](https://twitter.com/signup?lang=en)<br/>[免費註冊：HipChat](https://www.hipchat.com/sign_up) |
| 目標集的使用者 tooassign hello 應用程式。 建議使用安全性群組包含 hello 使用者。 | [指派的使用者或群組 tooan 企業應用程式在 Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| 本機系統管理員存取 tooa 電腦 toodeploy hello Internet Explorer、 Chrome 或 Firefox 存取面板延伸模組 | [適用於 IE 的存取面板擴充功能](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[適用於 Chrome 的存取面板擴充功能](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[適用於 Firefox 的存取面板擴充功能](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 安裝 hello 瀏覽器延伸模組 | [適用於 IE 的存取面板擴充功能](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[適用於 Chrome 的存取面板擴充功能](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[適用於 Firefox 的存取面板擴充功能](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| 從資源庫設定應用程式 | [什麼是 Azure Active Directory 中的企業應用程式管理的新功能： hello 全新和改善的應用程式庫](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| 設定密碼 SSO | [單一登入企業應用程式在 hello 新版 Azure 入口網站中管理： 密碼為基礎的登入](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Hello hello 必要條件中所識別的應用程式 toohello 群組指派 | [指派的使用者或群組 tooan 企業應用程式在 Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| 有權存取的測試使用者身分登入 toohttps://myapps.microsoft.com/ |  |
| 按一下剛建立的 hello 應用程式的 hello 磚。 | [Hello 存取面板是什麼？: 不會佈建身分識別的密碼型 SSO](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| 提供 hello 應用程式認證 | [Hello 存取面板是什麼？: 不會佈建身分識別的密碼型 SSO](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| 關閉 hello 瀏覽器和重複 hello 登入。 這次 hello 使用者應該會看到無縫存取方式 toohello 應用程式。 |  |
| （選擇性） 您可以檢查 hello 應用程式使用情況報告。 請注意一些延遲，因此您需要 toowait hello 報表中的某些時間 toosee hello 流量。 | [Hello Azure Active Directory 入口網站中的登入活動報表： 受管理的應用程式的使用量](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory 報告保留原則](active-directory-reporting-retention.md) |

### <a name="considerations"></a>考量

如果不存在於 hello 圖庫 hello 目標應用程式，您可以使用 「 攜帶您自己的應用程式 」。 深入了解：[Azure Active Directory 中企業應用程式管理的新功能：從一個位置新增自訂應用程式](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 請注意下列需求的 hello:
   * 應用程式應該要有已知的登入 URL
   * hello 登入頁面應包含具有多個文字欄位 hello 瀏覽器延伸模組可以自動填入 HTML 表單。 在最小的 hello，它應該包含使用者名稱和密碼。

## <a name="saas-shared-accounts-configuration"></a>SaaS 共用帳戶組態

近似時間 tooComplete: 30 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| hello 的目標應用程式清單和 hello 事先的確切登入 URL。 您可以使用 Twitter 作為範例。 | [Microsoft Azure Marketplace 上的 Twitter](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[註冊 Twitter](https://twitter.com/signup?lang=en) |
| 此 SaaS 應用程式的共用認證。 | [使用 Azure AD 來共用帳戶](active-directory-sharing-accounts.md)<br/>[Azure AD 的 Facebook、Twitter 及 LinkedIn 自動密碼變換現已提供預覽版！ - Enterprise Mobility and Security 部落格] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| 在至少兩個小組成員將會存取認證 hello 相同的帳戶。 他們必須是安全性群組的成員。 | [指派的使用者或群組 tooan 企業應用程式在 Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| 本機系統管理員存取 tooa 電腦 toodeploy hello Internet Explorer、 Chrome 或 Firefox 存取面板延伸模組 | [適用於 IE 的存取面板擴充功能](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[適用於 Chrome 的存取面板擴充功能](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[適用於 Firefox 的存取面板擴充功能](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 安裝 hello 瀏覽器延伸模組 | [適用於 IE 的存取面板擴充功能](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[適用於 Chrome 的存取面板擴充功能](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[適用於 Firefox 的存取面板擴充功能](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| 從資源庫設定應用程式 | [什麼是 Azure Active Directory 中的企業應用程式管理的新功能： hello 全新和改善的應用程式庫](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| 設定密碼 SSO | [單一登入企業應用程式在 hello 新版 Azure 入口網站中管理： 密碼為基礎的登入](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Hello hello 必要條件指派這些認證時所識別的應用程式 toohello 群組指派 | [指派的使用者或群組 tooan 企業應用程式在 Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| 身分登入不同的使用者，存取應用程式，為 hello**共用相同帳戶。**  |  |
| （選擇性） 您可以檢查 hello 應用程式使用情況報告。 請注意一些延遲，因此您需要 toowait hello 報表中的某些時間 toosee hello 流量。 | [Hello Azure Active Directory 入口網站中的登入活動報表： 受管理的應用程式的使用量](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory 報告保留原則](active-directory-reporting-retention.md) |


### <a name="considerations"></a>考量

如果不存在於 hello 圖庫 hello 目標應用程式，您可以使用 「 攜帶您自己的應用程式 」。 深入了解：[Azure Active Directory 中企業應用程式管理的新功能：從一個位置新增自訂應用程式](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 請注意下列需求的 hello:
   * 應用程式應該要有已知的登入 URL
   * hello 登入頁面應包含具有多個文字欄位 hello 瀏覽器延伸模組可以自動填入 HTML 表單。 在最小的 hello，它應該包含使用者名稱和密碼。

## <a name="app-proxy-configuration"></a>應用程式 Proxy 組態

近似時間 tooComplete: 20 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| Microsoft Azure AD 基本或進階訂用帳戶，以及您是全域管理員的 Azure AD 目錄 | [Azure Active Directory 版本](active-directory-editions.md) |
| Web 應用程式裝載內部希望 tooconfigure 遠端存取 |  |
| 執行 Windows Server 2012 R2 或 Windows 8.1 或更高版本的伺服器，您可以安裝 hello 應用程式 Proxy 連接器 | [了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md) |
| 如果 hello 路徑中有防火牆，請確認它已開啟，因此該連接器可以進行 HTTPS (TCP) 的 hello 要求 toohello 應用程式 Proxy | [在 [hello Azure 入口網站中啟用應用程式 Proxy： 應用程式 Proxy 的必要條件](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| 如果您的組織使用 proxy 伺服器 tooconnect toohello 網際網路，看看 hello 部落格文章工作與現有的內部 proxy 伺服器需要詳細說明如何 tooconfigure 它們 | [使用現有的內部部署 Proxy 伺服器](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| Hello 伺服器上安裝連接器 | [在 [hello Azure 入口網站中啟用應用程式 Proxy： 安裝和註冊 hello 連接器](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| 發行為應用程式 Proxy 應用程式的 Azure AD 中的 hello 內部應用程式 | [使用 Azure AD 應用程式 Proxy 發佈應用程式](application-proxy-publish-azure-portal.md) |
| 指派測試使用者 | [使用 Azure AD 應用程式 Proxy 發佈應用程式 - 新增測試使用者](application-proxy-publish-azure-portal.md#add-a-test-user) |
| (選擇性) 為您的使用者設定單一登入體驗 | [使用 Azure AD 應用程式 Proxy 提供單一登入](application-proxy-sso-azure-portal.md) |
| 測試應用程式登入為 tooMyApps 入口網站指派的使用者 | https://myapps.microsoft.com |

### <a name="considerations"></a>考量

1. 雖然我們建議您公司網路中放置 hello 連接器，一些情況下您會看到放置在 hello 定域機組中更佳的效能。 深入了解：[使用 Azure Active Directory 應用程式 Proxy 時的網路拓撲考量](application-proxy-network-topology-considerations.md)
2. 如需進一步的安全性詳細資料，以及這如何僅透過維護輸出連線來提供特別安全的遠端存取解決方案，請參閱：[使用 Azure AD 應用程式 Proxy 從遠端存取應用程式的安全性考量](application-proxy-security-considerations.md)

## <a name="generic-ldap-connector-configuration"></a>一般 LDAP 連接器組態

近似時間 tooComplete: 60 分鐘的時間

> [!IMPORTANT]
> 這是一種需要對 FIM/MIM 有某種程度熟悉的進階組態。 如果在生產環境中使用，建議您瀏覽[頂級支援](https://support.microsoft.com/premier)以查看此組態的相關問題。

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 已安裝及設定 Azure AD Connect | 構成要素：[目錄同步作業 - 密碼雜湊同步處理](#directory-synchronization--password-hash-sync-phs--new-installation) |
| 符合需求的 ADLDS 執行個體 | [泛型的 LDAP 連接器技術參照： hello 泛型 LDAP 連接器概觀](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| 使用者所使用之工作負載及與這些工作負載關聯之屬性的清單 | [Azure AD Connect 同步： 同步處理 tooAzure Active Directory 的屬性](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 新增一般 LDAP 連接器 | [一般 LDAP 連接器技術參考：建立新的連接器](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| 為已建立的連接器建立執行設定檔 (完整匯入、差異匯入、完整同步處理、差異同步處理、匯出) | [建立管理代理程式執行設定檔 (英文)](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)<br/> [使用連接器與 hello Azure AD Connect 同步處理服務管理員](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| 執行完整匯入設定檔，並確認連接器空間中有物件 | [搜尋連接器空間物件](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)<br/>[使用連接器與 Azure AD Connect 同步處理服務管理員 hello： 搜尋連接器空間](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| 建立同步處理規則，讓 Metaverse 中的物件具有必要的工作負載屬性 | [Azure AD Connect 同步： 變更 hello 預設組態的最佳做法： 變更 tooSynchronization 規則](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Azure AD Connect 同步處理：了解宣告式佈建](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Azure AD Connect 同步處理：了解宣告式佈建運算式](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| 啟動完整的同步處理週期 | [Azure AD Connect 同步： 排程器： 啟動 hello 排程器](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| 發生問題時進行疑難排解 | [疑難排解為 not synchronizing tooAzure AD 物件](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| 確認，LDAP 的使用者可以登入，而且存取 hello 應用程式 | https://myapps.microsoft.com |

### <a name="considerations"></a>考量

> [!IMPORTANT]
> 這是一種需要對 FIM/MIM 有某種程度熟悉的進階組態。 如果在生產環境中使用，建議您瀏覽[頂級支援](https://support.microsoft.com/premier)以查看此組態的相關問題。

## <a name="groups---delegated-ownership"></a>群組 - 委派的擁有權

近似時間 tooComplete: 10 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 已設定 SaaS 應用程式 (同盟 SSO 或密碼 SSO) | 構成要素：[SaaS 同盟 SSO 組態](#saas-federated-sso-configuration) |
| 識別雲端群組指派存取 toohello 應用程式中 #1 | 構成要素：[SaaS 同盟 SSO 組態](#saas-federated-sso-configuration) <br/>[在 Azure Active Directory 中建立群組和新增使用者](active-directory-groups-create-azure-portal.md) |
| Hello 群組擁有者的認證可以使用 | [使用 Azure Active Directory 群組管理存取 tooresources](active-directory-manage-groups.md) |
| 經 hello 資訊工作者存取 hello 應用程式的認證 | [Hello 存取面板是什麼？](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 找出 hello 群組已被授與存取 toohello 應用程式，並設定 hello 擁有者指定的群組| [管理 Azure Active Directory 中群組的 hello 設定](active-directory-groups-settings-azure-portal.md) |
| Hello 群組擁有者身分登入，請參閱 < 群組存取面板] 索引標籤中的 hello 群組成員資格 | [Azure Active Directory 群組管理頁面](https://account.activedirectory.windowsazure.com/r/#/groups) |
| 新增您想要 tootest hello 資訊工作者 |  |
| Hello 資訊工作者身分登入，確認 hello 磚可供使用 | [Hello 存取面板是什麼？](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>考量

如果 hello 應用程式佈建已啟用，您可能需要 toowait 幾分鐘的時間才能存取 hello 資訊工作者 hello 應用程式佈建 toocomplete hello。

## <a name="saas-and-identity-lifecycle"></a>SaaS 和身分識別生命週期

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 已設定 SaaS 應用程式 (同盟 SSO 或密碼 SSO) | 構成要素：[SaaS 同盟 SSO 組態](#saas-federated-sso-configuration) |
| 識別雲端群組指派存取 toohello 應用程式中 #1 | 構成要素：[SaaS 同盟 SSO 組態](#saas-federated-sso-configuration) <br/>[在 Azure Active Directory 中建立群組和新增使用者](active-directory-groups-create-azure-portal.md) |
| 經 hello 資訊工作者存取 hello 應用程式的認證 | [Hello 存取面板是什麼？](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 移除太指派 hello hello 群組 hello 應用程式使用者| [管理 Azure Active Directory 租用戶中使用者的群組成員資格](active-directory-groups-members-azure-portal.md) |
| 等候幾分鐘來執行取消佈建 | [Azure AD 中的自動化 SaaS 應用程式使用者佈建：自動化佈建如何運作？](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| 在上的另一個瀏覽器工作階段中，為 「 hello 資訊工作者 toomy 應用程式入口網站登入，確認該磚遺漏 | http://myapps.microsoft.com |


### <a name="considerations"></a>考量

推斷 hello PoC 案例 tooleavers 及/或請假案例。 如果 hello 使用者取得停用了在內部部署 AD 或移除，再也沒有方式 toolog toohello SaaS 應用程式中。

## <a name="self-service-access-tooapplication-management"></a>自助服務存取 tooApplication 管理

近似時間 tooComplete: 10 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 識別 POC 的使用者，會要求存取 toohello 應用程式，做為 hello 安全性群組的一部分 | 構成要素：[SaaS 同盟 SSO 組態](#saas-federated-sso-configuration) |
| 已部署「目標應用程式」 | 構成要素：[SaaS 同盟 SSO 組態](#saas-federated-sso-configuration) |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 移 tooEnterprise Azure AD 管理入口網站中的應用程式] 刀鋒視窗 | [Azure AD 管理入口網站：企業應用程式](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| 根據自助必要條件設定應用程式 | [Azure Active Directory 中企業應用程式管理的新功能：設定自助式應用程式存取](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| 為 「 hello 資訊工作者 toomy 應用程式入口網站登入 | http://myapps.microsoft.com |
| 請注意 [+ 新增應用程式] op hello] 頁面上的按鈕。 它使用 tooget access toohello 應用程式 |  |

### <a name="considerations"></a>考量

選擇的 hello 應用程式可能有佈建需求，因此將立即 toohello 應用程式可能會導致發生一些錯誤。 如果選擇的 hello 應用程式支援使用 azure ad 佈建，而且它已設定，您可以將此機會 tooshow hello 整個資料流工作結束 tooend。 請參閱 hello 的建置組塊[SaaS 同盟 SSO 組態](#saas-federated-sso-configuration)進一步建議

## <a name="self-service-password-reset"></a>自助式密碼重設

近似時間 tooComplete: 15 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 在您的租用戶中啟用自助式密碼管理。 | [IT 系統管理員的 Azure Active Directory 密碼重設](active-directory-passwords.md) |
| 啟用密碼回寫 toomanage 密碼從內部部署。 請注意，這需要特定的 Azure AD Connect 版本 | [密碼回寫先決條件](active-directory-passwords-writeback.md) |
| 找出 hello PoC 使用者將會使用這項功能，並確定它們安全性群組的成員。 hello 使用者必須為非系統管理員 toofully showcase hello 功能 | [自訂： Azure AD 密碼管理： 限制存取 toopassword 重設](active-directory-passwords-writeback.md) |


### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 瀏覽 tooAzure AD 管理入口網站： 密碼重設 | [Azure AD 管理入口網站：密碼重設](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| 判斷 hello 密碼重設原則。 基於 POC，您可以使用電話及問與答。建議 tooenable 註冊 toobe 需要登入 tooaccess 面板上 |  |
| 以資訊工作者身分登出和登入 |  |
| 提供 hello 自助式密碼重設資料，例如設定每個步驟 2 | http://aka.ms/ssprsetup |
| 關閉 hello 瀏覽器 |  |
| 開始為您在步驟 4 中使用的 hello 資訊工作者 hello 登入程序 |  |
| 重設 hello 密碼 | [更新自己的密碼：重設密碼](active-directory-passwords-update-your-own-password.md) |
| 再試一次登入您的新密碼 tooAzure AD 以及 tooon 內部部署資源 |  |

### <a name="considerations"></a>考量

1. 如果 toocause 人事將會升級 hello Azure AD Connect，然後考慮使用針對雲端帳戶，或讓它示範針對個別的環境
2. hello 系統管理員有不同的原則，並使用 hello 系統管理員帳戶 tooreset hello 密碼可能 taint hello PoC 造成混淆。 請確定您使用一般使用者帳戶 tootest hello 重設作業


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>使用通話進行 Azure Multi-Factor Authentication

近似時間 tooComplete: 10 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 識別將使用 MFA 的 POC 使用者  |  |
| 可供 MFA 挑戰使用的收訊良好手機  | [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 瀏覽過 Azure AD 管理入口網站中的 < 使用者和群組 > 刀鋒視窗 | [Azure AD 管理入口網站：使用者和群組](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| 關閉 [所有使用者] 刀鋒視窗 |  |
| 在 [hello 頂端，選擇 [多因素驗證] 按鈕列 | Azure MFA 入口網站的直接 URL：https://aka.ms/mfaportal |
| Hello 「 使用者 」 設定中選取 hello PoC 使用者並啟用它們的 MFA | [Azure Multi-Factor Authentication 中的使用者狀態](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Hello PoC 使用者，以及逐步 hello 證明程序的登入  |  |

### <a name="considerations"></a>考量

1. hello PoC 中明確地將使用者的 MFA 設定上的所有登入此建置組塊的步驟。 此外，還有「條件式存取」和 Identity Protection 之類的其他工具，可在更具目標性的案例中進行 MFA。 這會是項目 tooconsider 從 POC tooproduction 移動時。
2. 此建置區塊中的 hello PoC 步驟明確使用電話做 hello expedience 的 MFA 方法。 當您從 POC tooproduction 轉換，我們建議使用應用程式，例如 hello [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md)做為您第二個因素，可能的話。
深入了解：[DRAFT NIST 特殊出版品 800-63B (英文)](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>SaaS 應用程式的 MFA 條件式存取

近似時間 tooComplete: 10 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 識別 PoC 使用者 tootarget hello 原則。 這些使用者應該在安全性群組 tooscope hello 條件式存取原則 | [SaaS 同盟 SSO 組態](#saas-federated-sso-configuration) |
| 已設定 SaaS 應用程式 |  |
| PoC 使用者已指派 toohello 應用程式 |  |
| 認證 toohello POC 使用者可用 |  |
| 已為 MFA 註冊 POC 使用者。 使用收訊良好的手機 | http://aka.ms/ssprsetup |
| Hello 內部網路中的裝置。 Hello 內部位址範圍中設定的 IP 位址 | 尋找您的 IP 位址：https://www.bing.com/search?q=what%27s+my+ip |
| Hello （可以是電話使用 hello 貨運公司的行動網路） 的外部網路中的裝置 |  |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 移 tooAzure AD 管理入口網站： 條件式存取] 刀鋒視窗 | [Azure AD 管理入口網站：條件式存取](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| 建立「條件式存取」原則：<br/>- 以 [使用者和群組] 底下的「PoC 使用者」為目標<br/>- 以 [雲端應用程式] 底下的「PoC 應用程式」為目標<br/>- 以所有位置為目標，但 [條件] -> [位置] 底下的受信任位置除外 **注意：**受信任的 IP 是在 [MFA 入口網站](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx)中設定<br/>- 在 [授權] 底下要求多重要素驗證 | [開始使用 Azure Active Directory 中的條件式存取：原則設定步驟](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| 從公司網路內部存取應用程式 | [開始使用 Azure Active Directory 中的條件式存取： 測試 hello 原則](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| 從公用網路存取應用程式 | [開始使用 Azure Active Directory 中的條件式存取： 測試 hello 原則](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>考量

如果您使用同盟時，您可以使用 hello 在內部部署身分識別提供者 (IdP) toocommunicate hello 內部/外部宣告與公司網路狀態。 您可以使用這項技術，而不需要 toomanage hello 可以複雜 tooassess 和大型組織中管理之 IP 位址清單。 在安裝程式，您需要 hello 漫遊的 「 網路 」 案例 （例如咖啡廳的位置記錄 hello 內部網路，以及時已登入參數的使用者） 的帳戶，並請確定您了解 hello 影響。 深入了解：[使用 Azure Multi-Factor Authentication 與 AD FS 保護雲端資源：同盟使用者的可信任 IP](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>Privileged Identity Management (PIM)

近似時間 tooComplete: 15 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 識別要納入 hello pim POC hello 全域管理員 | [開始使用 Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) |
| 識別將會變成 hello 安全性系統管理員的 hello 全域管理員 | [開始使用 Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)<br/> [Azure Active Directory PIM 中不同的系統管理角色](active-directory-privileged-identity-management-roles.md) |
| 選擇性： 確認是否 hello 全域系統管理員有電子郵件存取 tooexercise PIM 中的電子郵件通知 | [什麼是 Azure AD Privileged Identity Management？: hello 角色啟用設定](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 登入 toohttps://portal.azure.com 做為全域管理員 (版本 GA) 並啟動程序的 hello PIM 刀鋒視窗。 hello 全域系統管理員執行此步驟會植入 hello 安全性系統管理員身分。  讓我們將此執行者稱為 GA1 | [使用 Azure AD Privileged Identity Management 中的 hello 安全性精靈](active-directory-privileged-identity-management-security-wizard.md) |
| 找出 hello 全域系統管理員，並將其從永久 tooeligible 移。 這應該是從 hello 為了清楚起見使用在步驟 1 中的另一個管理。 讓我們將此執行者稱為 GA2 | [Azure 的 AD Privileged Identity Management： 如何 tooadd 或移除使用者角色](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[什麼是 Azure AD Privileged Identity Management？: hello 角色啟用設定](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| 現在，GA2 toohttps://portal.azure.com 身分登入，然後再試一次變更 「 使用者設定 」。 請注意，部分選項是呈現灰色。 | |
| Hello 和新的索引標籤中相同的工作階段如步驟 3 中，瀏覽現在 toohttps://portal.azure.com 並加入 hello PIM 刀鋒視窗 toohello 儀表板。 | [如何 tooactivate 或停用角色在 Azure AD Privileged Identity Management： 新增 hello Privileged Identity Management 的應用程式](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| 要求啟用 toohello 全域管理員角色 | [如何 tooactivate 或停用角色在 Azure AD Privileged Identity Management： 啟用角色](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| 請注意，如果 GA2 從未註冊 MFA，將必須註冊 Azure MFA |  |
| 返回 toohello 步驟 3 中的 [原始] 索引標籤，然後按一下 hello hello 瀏覽器中的重新整理] 按鈕。 請注意，您現在有存取 toochange [使用者設定] | |
| （選擇性） 如果您的全域系統管理員啟用電子郵件，您可以檢查 GA1 和 GA2 的收件匣並查看 hello hello 角色啟動的通知 |  |
| 8 檢查 hello 稽核歷程記錄，並觀察 hello 報表 tooconfirm hello 權限提高 GA2 所示。 | [什麼是 Azure AD Privileged Identity Management？：檢閱角色活動](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>考量

此功能是 Azure AD Premium P2 和/或 EMS E5 的一部分

## <a name="discovering-risk-events"></a>探索風險事件

近似時間 tooComplete: 20 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 已下載並安裝 Tor 瀏覽器的裝置 | [下載 Tor 瀏覽器](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| 存取 tooPOC 使用者 toodo hello 登入 | [Azure Active Directory Identity Protection 腳本](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 開啟 Tor 瀏覽器 | [下載 Tor 瀏覽器](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| 登入 toohttps://myapps.microsoft.com 以 hello POC 使用者帳戶 | [Azure Active Directory Identity Protection 腳本：模擬風險事件](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| 等候 5-7 分鐘 |  |
| 全域管理員 toohttps://portal.azure.com 身分登入，然後開啟刀鋒視窗中的識別身分保護 hello | https://aka.ms/aadipgetstarted |
| 開啟 hello 風險事件刀鋒伺服器。 您應該會在 [從匿名 IP 位址登入] 底下看到一個項目  | [Azure Active Directory Identity Protection 腳本：模擬風險事件](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>考量

此功能是 Azure AD Premium P2 和/或 EMS E5 的一部分

## <a name="deploying-sign-in-risk-policies"></a>部署登入風險原則

近似時間 tooComplete: 10 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 已下載並安裝 Tor 瀏覽器的裝置 | [下載 Tor 瀏覽器](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| 在測試 POC 使用者 toodo hello 記錄的存取權 |  |
| 已向 MFA 註冊 POC 使用者。 請確定 toouse 好接收電話 | 構成要素：[使用通話進行 Azure Multi-Factor Authentication](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 全域管理員 toohttps://portal.azure.com 身分登入，然後開啟 hello Identity Protection] 刀鋒視窗 | https://aka.ms/aadipgetstarted |
| 依下列方式啟用登入風險原則：<br/>- 指派至：POC 使用者<br/>- 條件：中度或更高的登入風險 (從匿名位置登入是視為中度風險層級)<br/>- 控制項：需要 MFA | [Azure Active Directory Identity Protection 腳本：登入風險](active-directory-identityprotection-playbook.md#sign-in-risk) |
| 開啟 Tor 瀏覽器 | [下載 Tor 瀏覽器](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| 登入 toohttps://myapps.microsoft.com 以 hello PoC 使用者帳戶 |  |
| 請注意 hello MFA 挑戰 | [使用 Azure AD Identity Protection 時的登入體驗：有風險的登入復原](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>考量

此功能是 Azure AD Premium P2 和/或 EMS E5 的一部分。 toolearn 風險事件有關的詳細資訊請造訪： [Azure Active Directory 風險事件](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>設定憑證式驗證

近似時間 toocomplete: 20 分鐘

### <a name="pre-requisites"></a>必要條件

| 必要條件 | 資源 |
| --- | --- |
| 具有從「企業 PKI」佈建之使用者憑證的裝置 (Windows、iOS 或 Android) | [部署使用者憑證](https://msdn.microsoft.com/library/cc770857.aspx) |
| 與 ADFS 同盟的 Azure AD 網域 | [Azure AD Connect 和同盟](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Active Directory 憑證服務概觀](https://technet.microsoft.com/library/hh831740.aspx)|
| 針對 iOS 裝置，安裝 Microsoft Authenticator 應用程式 | [開始使用 hello Microsoft 驗證器應用程式](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>步驟

| 步驟 | 資源 |
| --- | --- |
| 在 ADFS 上啟用「憑證驗證」 | [設定驗證原則： tooconfigure 主要驗證 Windows Server 2012 R2 中，全域](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| 選擇性：在 Azure AD 中為 Exchange Active Sync 用戶端啟用「憑證驗證」 | [開始在 Azure Active Directory 中使用憑證式驗證](active-directory-certificate-based-authentication-get-started.md) |
| 瀏覽 tooAccess 面板，並使用使用者憑證進行驗證 | https://myapps.microsoft.com |

### <a name="considerations"></a>考量

關於此部署的警告，請瀏覽的 toolearn: [ADFS： 向 Azure AD 的憑證驗證 （& s) Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> 使用者憑證的持有應該受到保護。 可透過管理裝置或使用 PIN (在使用智慧卡的情況下) 的方式來保護。



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
