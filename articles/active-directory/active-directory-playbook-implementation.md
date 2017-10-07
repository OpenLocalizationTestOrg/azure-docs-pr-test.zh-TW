---
title: "Active Directory PoC 腳本實作 aaaAzure |Microsoft 文件"
description: "探索並快速實作身分識別和存取管理案例"
services: active-directory
keywords: "azure active directory, 腳本, 概念證明, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Azure Active Directory 概念證明腳本：實作

## <a name="foundation---syncing-ad-tooazure-ad"></a>Foundation-同步處理 AD tooAzure AD 

混合式身分識別是大多數 hello 企業客戶已經有內部部署目錄的 hello 基礎。 hello 現在的目標是 toointentionally 為花更多時間這裡做為可能 tooshow hello 值 hello 實際的身分識別和存取案例。 

| 案例 | 建置組塊| 
| --- | --- |  
| [延伸您內部部署身分識別 toohello 雲端](#extending-your-on-premises-identity-to-the-cloud) | [目錄同步作業 - 密碼雜湊同步處理](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**注意**︰如果您已經有 DirSync/ADSync 或舊版的 Azure AD Connect，則這是選擇性步驟。 本指南中的某些案例可能需要較新版本的 Azure AD Connect。  <br/>[商標](active-directory-playbook-building-blocks.md#branding) | 
| [使用群組指派 Azure AD 授權](#assigning-azure-ad-licenses-using-groups) | [群組型授權](active-directory-playbook-building-blocks.md#group-based-licensing) |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>延伸您內部部署身分識別 toohello 雲端 

1. Bob 是在 Contoso hello Active Directory 系統管理員。 他為一組使用者的服務取得 hello 需求 tooenable 身分識別。 執行 Azure AD Connect 精靈之後 hello hello 目標使用者身分使用 hello 雲端中。 
2. Tooaccess hello Azure Active Directory 存取面板，並確認她可以進行驗證，Bob 就會詢問 Susie hello 的目標使用者的其中一個。 Susie 看到了加上商標的登入頁面，以及一個可供啟用未來之應用程式存取權的空白存取面板。

### <a name="assigning-azure-ad-licenses-using-groups"></a>使用群組指派 Azure AD 授權 

1. Bob 為 hello Azure AD 全域管理員，且想一部分的 Azure AD 的 hello 初始首展的 tooallocate Azure AD 授權 tooa 特定一組使用者。
2. Bob 建立 hello 群組試驗使用者。 
3. Bob 指派 hello 授權 toohello 群組
4. Susie hello 資訊工作者，其中是她的工作函式的一部分加入 toohello 安全性群組
5. 一段時間後 Susie 有存取 toohello Azure AD premium 授權。 這將在稍後啟用多個 hello POC 案例。

## <a name="theme---lots-of-apps-one-identity"></a>佈景主題 - 許多應用程式、一個身分識別

| 案例 | 建置組塊| 
| --- | --- |  
| [整合 SaaS 應用程式 - 同盟 SSO](#integrate-saas-applications---federated-sso) | [SaaS 同盟 SSO 組態](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[群組 - 委派的擁有權](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [整合 SaaS 應用程式 - 密碼 SSO](#integrate-saas-applications---password-sso) | [SaaS 密碼 SSO 組態](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [SSO 和身分識別生命週期事件](#sso-and-identity-lifecycle-events) | [SaaS 和身分識別生命週期](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle) |
| [安全存取 tooShared 帳戶](#secure-access-to-shared-accounts) | [SaaS 共用的帳戶設定](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration) |
| [安全遠端存取 tooOn 內部部署應用程式](#secure-remote-access-to-on-premises-applications) | [應用程式 Proxy 組態](active-directory-playbook-building-blocks.md#app-proxy-configuration) |
| [同步處理 LDAP 識別 tooAzure AD](#synchronize-ldap-identities-to-azure-ad) |  [一般 LDAP 連接器組態](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### <a name="integrate-saas-applications---federated-sso"></a>整合 SaaS 應用程式 - 同盟 SSO 

1. Bob 是 hello Azure AD 全域管理員，並收到來自 hello 行銷部門 tooenable 存取 tootheir ServiceNow 執行個體的要求。 Bob 尋找 Azure AD 文件中的 hello 逐步教學課程，並遵循它，並委派 hello 使用者 toohello 應用程式 tooKevin，行銷團隊 hello 開頭的指派。 
2. Kevin 登入為 ServiceNow 權利 hello 擁有者，並指派 Susie toohello 應用程式。 Kevin 同時注意到 ServiceNow 已自動建立 Susie 的設定檔
3. Susie 是資訊工作者 hello 行銷部門中。 她記錄 tooazure AD 和尋找所有 SaaS 應用程式，她會都指派 tooin myapps 入口網站中。 從該處，她會順暢地取得存取 tooServiceNow。
4. hello 行銷部門想 tooaudit 存取過 ServiceNow。 Bob 下載活動報告，並透過電子郵件向 Kevin 分享該報告。  

### <a name="sso-and-identity-lifecycle-events"></a>SSO 和身分識別生命週期事件

1. Susie 採用請假，並由公司原則 hello 內部部署 AD 帳戶已暫時停用。 Susie 現在無法登入 tooAzure AD，因此無法存取 ServiceNow。 
2. Susie 可從行銷 tooSales 橫向移動。 Kevin 把她在 ServiceNow 的存取權移除。 Susie 登入 hello azure ad myapps 並她不會再看見 hello ServiceNow 磚。 10 分鐘過後，Kevin 確認 Susie 的帳戶早已從 ServiceNow 管理主控台停用。

### <a name="integrate-saas-applications---password-sso"></a>整合 SaaS 應用程式 - 密碼 SSO

1. Bob 設定存取 tooAtlassian HipChat。 HipChat 有密碼 SSO 整合和授與存取 tooSusie
2. Susie 登入 toohello myapps 入口網站，並會看到 Azure AD IE 瀏覽器延伸模組，她下載連結 toodownload hello
3. 在按一下後，系統提示她輸入 HipChat 使用者名稱和密碼認證。 這是一次性作業，而且它完成後，她必須存取 tooHipChat
4. 幾天之後，Susie 再次開啟 myapps 入口網站並按一下 HipChat。 這一次，她在存取時沒有遇到任何問題
5. Kevin，hello HipChat 應用程式擁有者想 tooaudit 存取過 hello 應用程式。 Bob 下載稽核報告，並透過電子郵件向 Kevin 分享該報告。 

### <a name="secure-access-tooshared-accounts"></a>安全存取 tooShared 帳戶 

1. Bob 是 hello 銷售團隊成員的工作的 toosecure hello 共用 Twitter 控制代碼。 他將 Twitter 新增為 SSO 應用程式，並將其指派 toohello 安全性群組的 hello 銷售團隊。 他所提供 hello 認證 toohello 共用帳戶，他 hello 系統中，提供它。 
2. 共用的 Twitter 認證已不再受信任，因為 toomultiple 不知情的人。 Bob 可以讓 hello Twitter 密碼自動變換。
3. Susie，hello 銷售團隊的成員登入 toohello myapps 入口網站，並看到連結 toodownload hello Azure AD IE 瀏覽器延伸模組。 她因此安裝了該擴充功能。
4. 她按一下後 get 直接存取 tooTwitter。 她不知道 hello 密碼。
5. Arnold 也是 hello 銷售團隊的一部分。 他有相同的經驗 Susie 為在步驟 3-4 hello
6. hello 銷售部門想 tooaudit 存取過 Twitter。 Bob 下載活動報告，並透過電子郵件向 Kevin 分享該報告。 

### <a name="secure-remote-access-tooon-premises-applications"></a>安全遠端存取 tooOn 內部部署應用程式

1. Bob，hello Azure AD 全域管理員，具有 tooenable 員工 tooaccess 幾個實用的內部資源，例如 hello 費用的應用程式，從遠端工作時收到許多要求。 他會遵循 hello[應用程式 Proxy 的文件](active-directory-application-proxy-enable.md)tooinstall 連接器並發佈做為應用程式 Proxy 應用程式的費用。 
2. Bob 與 Susie hello 員工需要遠端存取的其中一個共用 hello 外部費用應用程式 URL。 她存取 hello 連結，而且之後對 AAD 進行驗證，她在無法 tooaccess hello 費用應用程式繼續 toobe 生產力遠端時。 
3. 然後 Bob 會繼續 toopublish 其他內部部署應用程式使用 hello 相同處理程序，並提供存取 toousers，視需要。 他將新增的條件存取及多因素驗證 hello 更為敏感他所發行的應用程式、 tooensure 額外的安全性。

### <a name="synchronize-ldap-identities-tooazure-ad"></a>同步處理 LDAP 識別 tooAzure AD

1. Bob 所任職公司的身分識別基礎結構很複雜。 大部分的 hello 使用者會被保留內部 Windows Server Active Directory 網域服務 (ADDS)。 其中有些人則由 Active Directory 輕量型目錄服務 (ADLDS) 內的 HR 系統進行管理。
2. Bob 被負責與啟用 （也這些中未出現 ADDS） 的所有使用者存取 tooSaaS 應用程式。
3. Bob 在 Azure AD Connect 設定 ADLDS 泛型 LDAP 連接器 toopull 資料。
4. Bob 建立同步處理規則，因此 LDAP 使用者填入 Metaverse 和 tooAzure AD
5. 身為 LDAP 使用者的 Susie 使用已同步處理的身分識別來存取其 SaaS 應用程式



> [!IMPORTANT] 
> 這是一種需要對 FIM/MIM 有某種程度熟悉的進階組態。 如果在生產環境中使用，建議您瀏覽[頂級支援](https://support.microsoft.com/premier)以查看此組態的相關問題。



## <a name="theme---increase-your-security"></a>佈景主題 - 增加您的安全性 

| 案例 | 建置組塊| 
| --- | --- |  
| [安全的系統管理員帳戶存取權](#secure-administrator-account-access) | [使用電話進行 Azure MFA](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [安全的應用程式存取](#secure-access-to-applications) | [SaaS 應用程式的條件式存取](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [啟用即時系統管理](#enable-just-in-time-jit-administration) | [Privileged Identity Management](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [根據風險保護身分識別](#protect-identities-based-on-risk) | [探索風險事件](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[部署登入風險原則](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [使用憑證式驗證無需密碼進行驗證](#authenticate-without-passwords-using-certificate-based-authentication) | [設定憑證式驗證](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>安全的系統管理員帳戶存取權

1. Bob 是 hello Azure AD 全域管理員。 他發現 Stuart hello 服務的共同管理員身分。 
2. Bob 設定 tooalways 需要 MFA tooimprove hello 安全性狀態的 Stuart 的帳戶
3. Stuart 中記錄 toohello Azure 入口網站與他必須 tooregister 通知其電話號碼 toocontinue hello 登入
4. 現在會使用多因素驗證時，會受到保護從 Stuart 後續登入，他現在取得通話 tooverify 他的身分識別。

### <a name="secure-access-tooapplications"></a>安全存取 tooapplications

1. Kevin 位於 ServiceNow 的 hello 業務擁有者。 hello 公司存取外部 hello 公司網路時，現在想使用 MFA 那些使用者 toologin。
2. Bob，我們的 Azure AD 全域管理員，將條件式存取原則 toohello ServiceNow 的應用程式 tooenable MFA 進行外部存取
3. Susie，我們的資訊工作者，登入我的應用程式入口網站，並按一下 hello ServiceNow 磚。 她現在正在接受 MFA 的查問。

### <a name="enable-just-in-time-jit-administration"></a>啟用即時 (JIT) 系統管理

1. Bob 和 Stuart 是 Azure AD 全域管理員。 他們想 tooenable JIT 存取 toohello 管理角色和也 hello 使用方式的 hello tookeep 記錄權限角色。
2. Bob hello Azure AD 租用戶中可 PIM 以及 hello 安全性系統管理員。 他從永久 tooeligible 變更自己和 Stuart 的全域管理員角色成員資格。
3. Bob 和 Stuart 現在需要執行任何操作變更 tooAzure AD 之前啟動 hello Azure 入口網站透過其角色組態。 

### <a name="protect-identities-based-on-risk"></a>根據風險保護身分識別 

1. Susie 是一位資訊工作者，她嘗試從 Tor 瀏覽器登入。 
2. Bob 檢查 hello Azure AD identity protection 儀表板，並可看見 Susie 的登入，從匿名 IP 位址。 hello 安全性團隊希望 toochallenge 這類存取使用者的 MFA
3. Bob 可以讓 Azure AD Identity Protection 原則 toochallenge MFA 中型或更高的風險事件
4. 時間流逝，Susie 再次從 Tor 瀏覽器登入。 此時，她將會看到 hello MFA 挑戰

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>使用憑證式驗證無需密碼進行驗證

1. Bob 是金融機構的全域管理員，該機構禁止使用密碼作為其應用程式的驗證因素。
2. Bob 在 ADFS 與 Azure AD 上啟用並強制執行憑證驗證
3. Susie 存取應用程式時提示 tooauthenticate 使用憑證

## <a name="theme---scale-with-self-service"></a>佈景主題 - 使用自助式縮放比例

| 案例 | 建置組塊| 
| --- | --- |  
| [自助式密碼重設](#self-service-password-reset) | [自助式密碼重設](active-directory-playbook-building-blocks.md#self-service-password-reset) |
| [自助服務存取 tooApplications](#self-service-access-to-applications) | [自助服務存取 tooApplications](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>自助式密碼重設 

1. Bob 是 hello Azure AD 全域管理員，可讓自助服務密碼管理 tooa 使用者子集，包括 Susie。 
2. Susie 記錄中 toomyapps 入口網站，並查看訊息 tooregister 她的安全性資訊未來密碼重設事件。
3. 時間快轉幾天，Susie 忘記其密碼，因此她透過 Azure AD 入口網站重設密碼

### <a name="self-service-access-tooapplications"></a>自助服務存取 tooApplications 

1. Kevin 位於 ServiceNow 的 hello 業務擁有者。 他想要使用者太 「 註冊 」 它依需求，而不是將它們全部加入
2. Bob，我們的 Azure AD 全域管理員，修改 hello ServiceNow 的應用程式 tooenable 自助服務要求
3. Susie，我們的資訊工作者，登入我的應用程式入口網站並按一下 hello"新增更多應用程式 按鈕，並查看做為其中一個建議的應用程式的 hello 的 ServiceNow。 然後她會瀏覽後 toomy 應用程式入口網站，並查看 hello ServiceNow 的應用程式。

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]