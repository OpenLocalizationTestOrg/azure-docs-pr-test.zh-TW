---
title: "aaaAzure 身分識別和存取安全性最佳作法 |Microsoft 文件"
description: "本文提供使用內建 Azure 功能的一些身分識別管理和存取控制最佳作法。"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: af07dfda84758b9124641078ac8f696f725f2bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a>Azure 身分識別管理和存取控制安全性最佳作法
許多人認為身分識別 toobe hello 新界限層安全性，高於從 hello 傳統的網路中心觀點來看該角色。 這項演進的安全性注意事項和投資 hello 主要 pivot 來自 hello 事實網路界線變得越來越 porous 以及周邊防禦不可與它們一次先前 toohello 爆炸的有效[BYOD](http://aka.ms/byodcg)裝置和雲端應用程式。

本文將討論 Azure 身分識別管理和存取控制安全性最佳作法的集合。 這些最佳作法從我們的經驗與[Azure AD](../active-directory/active-directory-whatis.md)和 hello 經驗的客戶自己。

針對每個最佳作法，我們會說明︰

* 哪些 hello 最佳作法是
* 為什麼要 tooenable 該最佳作法
* 如果您無法 tooenable hello 最佳作法，可能 hello 結果
* 可能的替代方式 toohello 最佳作法
* 如何了解 tooenable hello 最佳作法

此 Azure 身分識別管理和存取控制的安全性最佳做法文章根據共識意見，Azure 平台功能以及功能集，存在於 hello 撰寫本文時的時間。 隨時間變更的意見和技術，且這篇文章會定期 tooreflect 上更新這些變更。

本文討論的 Azure 身分識別管理和存取控制安全性最佳作法包括：

* 集中管理您的身分識別
* 啟用單一登入 (SSO)
* 部署密碼管理
* 對使用者強制執行 Multi-Factor Authentication (MFA)
* 使用角色型存取控制 (RBAC)
* 使用資源管理員來控制資源的建立位置
* 指南的 SaaS 應用程式開發人員 tooleverage 身分識別功能
* 主動監視可疑的活動

## <a name="centralize-your-identity-management"></a>集中管理您的身分識別
保護您的身分識別的一個重要步驟是 tooensure 它可以從一個有關此帳戶建立所在的單一位置管理帳戶。 同時 hello 大部分 hello 企業 IT 組織將其主要帳戶目錄內部、 混合式雲端部署位於 hello 上升而且很重要，您了解如何 toointegrate 內部部署和雲端目錄並提供toohello 使用者順暢的體驗。

tooaccomplish 這[混合式身分識別](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md)案例我們建議兩個選項：

* 使用 Azure AD Connect 同步處理內部部署目錄與雲端目錄。
* 使用 [Active Directory Federation Services](https://msdn.microsoft.com/library/bb897402.aspx) (AD FS) 建立內部部署身分識別與雲端目錄的同盟

組織無法使用其雲端身分識別其在內部部署身分識別將會遇到的 toointegrate 增加系統管理額外負荷中管理帳戶，進而增加 hello 發生的錯誤和安全性缺口的可能性。

如需有關 Azure AD 同步處理的詳細資訊，請參閱 hello 文章[整合內部部署身分識別與 Azure Active Directory](../active-directory/active-directory-aadconnect.md)。

## <a name="enable-single-sign-on-sso"></a>啟用單一登入 (SSO)
當您有多個目錄 toomanage 時，這會變成不僅可針對系統管理問題 IT，但也會有多個密碼 tooremember 的使用者。 使用[SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)將提供您的使用者使用 hello 相同 toosign 中設定的認證，並存取需要無論在此資源是位在內部或 hello 雲端中的 hello 資源 hello 能力。

使用 SSO tooenable 使用者 tooaccess 其[SaaS 應用程式](../active-directory/active-directory-appssoaccess-whatis.md)根據 Azure AD 中的組織帳戶。 這不只適用於 Microsoft SaaS 應用程式，也適用於其他應用程式，例如 [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) 和 [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md)。 您的應用程式可以設定的 toouse Azure AD 為[SAML 型身分識別](../active-directory/fundamentals-identity.md)提供者。 做為安全性控制項，Azure AD 不會發出可讓它們 toosign 放入 hello 應用程式除非被授予使用 Azure AD 存取權杖。 您可以直接授與存取權，或透過其所屬的群組授與。

> [!NOTE]
> hello 決策 toouse SSO 會影響您如何整合在內部部署目錄與雲端目錄。 如果您想 SSO，您將需要 toouse 同盟，因為目錄同步作業只會提供給[相同的登入體驗](../active-directory/active-directory-aadconnect.md)。
>
>

不會強制進行 SSO 的使用者和應用程式的組織會多公開的 tooscenarios 其中使用者會有多個密碼，可直接增加 hello 可能性重複使用密碼，或使用弱式密碼的使用者。

您可以進一步了解 Azure AD 的 SSO 閱讀 hello 文章[AD FS 管理和使用 Azure AD Connect 自訂](../active-directory/active-directory-aadconnect-federation-management.md)。

## <a name="deploy-password-management"></a>部署密碼管理
在案例中，您有多個租用戶或您想讓 tooenable 使用者太[重設其密碼](../active-directory/active-directory-passwords-update-your-own-password.md)，很重要，您會使用適當的安全性原則 tooprevent 濫用。 在 Azure 中，您可以利用 hello 自助式密碼重設功能，並自訂 hello 安全性選項 toomeet 您的業務需求。

它是特別重要 tooobtain 來自這些使用者的意見反應，而且當他們嘗試 tooperform 執行這些步驟，了解從他們的使用經驗。 根據這些體驗，詳細說明的計劃 toomitigate 潛在問題的較大的群組的 hello 部署期間可能發生的。 也建議您改用 hello[密碼重設註冊活動報表](../active-directory/active-directory-passwords-get-insights.md)toomonitor hello 使用者註冊。

組織想 tooavoid 密碼變更的支援電話，但啟用使用者 tooreset 自己的密碼會更容易受到 tooa 較高呼叫磁碟區 toohello 服務台 toopassword 問題原因。 有多個租用戶的組織，務必您實作此類型的功能，並啟用使用者 tooperform 密碼重設 hello 安全性原則中所建立的安全性界限內。

您可以進一步了解密碼重設讀取 hello 文章[部署密碼管理並訓練使用者 toouse 它](../active-directory/active-directory-passwords-best-practices.md)。

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a>對使用者強制執行 Multi-Factor Authentication (MFA)
對於組織，需要 toobe 符合業界標準，例如[PCI DSS 3.2 版](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32)，multi-factor authentication 是必須已驗證使用者的功能。 超出要與業界標準相容，強制執行 MFA tooauthenticate 使用者也可以協助組織 toomitigate 認證遭竊攻擊類型，例如[傳遞的雜湊 (PtH)](http://aka.ms/PtHPaper)。

藉由為使用者啟用 Azure MFA，您會加入第二層安全性 toouser 登入和交易。 在此情況下，交易可能會存取位於檔案伺服器或 SharePoint Online 中的文件。 Azure MFA 也可協助 IT tooreduce hello 可能性遭入侵的認證將會有存取 tooorganization 資料。

例如： 您對您的使用者強制執行 Azure MFA 和驗證為 toouse 通話或簡訊設定。 如果 hello 使用者的認證遭到入侵，hello 攻擊者將不會是能 tooaccess 任何資源，因為他不會存取 toouser 電話。 不要在新增額外識別身分保護層級的組織會更容易受到認證遭竊攻擊，這可能會導致 toodata 洩露。

一種替代方法，適用於想 tookeep hello 整個驗證控制組織單位是 toouse [Azure Multi-factor Authentication Server](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)，也稱為 MFA 內部部署。 使用此方法，您將無法 tooenforce 多重要素驗證，同時保留 hello MFA server 內部部署。

如需 Azure MFA 的詳細資訊，請閱讀 hello 文章[開始使用 Azure Multi-factor Authentication hello 定域機組中](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。

## <a name="use-role-based-access-control-rbac"></a>使用角色型存取控制 (RBAC)
限制存取根據 hello[需要 tooknow](https://en.wikipedia.org/wiki/Need_to_know)和[最小權限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)安全性原則是命令式 tooenforce 安全性原則所需的資料存取的組織。 Azure 角色型存取控制 (RBAC) 可以使用的 tooassign 權限 toousers、 群組和應用程式在特定範圍內。 訂用帳戶、 資源群組或單一資源，可以是 hello 範圍的角色指派。

您可以利用[內建的 RBAC](../active-directory/role-based-access-built-in-roles.md) Azure tooassign 權限 toousers 中的角色。 請考慮使用*儲存體帳戶參與者*需要 toomanage 儲存體帳戶的雲端操作員和*傳統儲存體帳戶參與者*角色 toomanage 傳統儲存體帳戶。 對於需要 toomanage Vm 和儲存體帳戶的雲端操作員，請考慮將它們新增到太*虛擬機器參與者*角色。

不會強制進行資料存取控制功能，例如 RBAC 利用的組織可能會提供必要 tootheir 使用者以外的權限。 這可能會導致 toodata 洩露允許使用者存取類型的資料 （例如，高商業影響），它們不應該在 hello 第一個位置中有 toocertain 型別。

您可以進一步了解 Azure rbac 進行讀取 hello 文章[所有存取控制](../active-directory/role-based-access-control-configure.md)。

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a>使用資源管理員來控制資源的建立位置
雲端操作員 tooperform 工作時防止中斷的慣例所需 toomanage 貴組織的資源，是非常重要。 想 toocontrol hello 位置，您可以建立資源的組織應該硬式編碼這些位置。

tooachieve，組織可以建立安全性原則所定義，描述 hello 動作或被明確拒絕的資源。 您指定這些原則定義，在 hello 預期的範圍，例如 hello 訂用帳戶、 資源群組或個別的資源。

> [!NOTE]
> 這不是 hello 相同為 RBAC，實際上它會運用 RBAC tooauthenticate hello 使用者具有權限 toocreate 這些資源。
>
>

運用[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toocreate 自訂原則也其中 hello 組織想 tooallow 作業只當 hello 適當的成本中心的情況下會產生關聯，否則它們將會拒絕 hello 要求。

不會控制如何建立資源的組織都可能會濫用 hello 服務藉由建立更多的資源比所需的更容易受到 toousers。 強化 hello 資源建立程序是重要的步驟 toosecure 多租用戶案例。

您可以進一步了解與 Azure 資源管理員建立原則，藉由讀取 hello 文章[使用原則 toomanage 資源和控制存取](../azure-resource-manager/resource-manager-policy.md)。

## <a name="guide-developers-tooleverage-identity-capabilities-for-saas-apps"></a>指南的 SaaS 應用程式開發人員 tooleverage 身分識別功能
當使用者存取可與內部部署或雲端目錄整合的 [SaaS 應用程式時](https://azure.microsoft.com/marketplace/active-directory/all/)，使用者身分識別會運用在許多案例中。 首先和最重要，我們建議開發人員使用安全的方法 toodevelop 這些應用程式，例如[Microsoft 安全性開發週期 (SDL)](https://www.microsoft.com/sdl/default.aspx)。 Azure AD 提供身分識別做為服務，支援業界標準通訊協定 (例如 [OAuth 2.0](http://oauth.net/2/) 和 [OpenID Connect](http://openid.net/connect/))，以及適用於不同平台的開放原始碼程式庫，來簡化開發人員的驗證工作。

請確定 tooregister 驗證 tooAzure AD 會將委派的任何應用程式，這是強制性的程序。 這背後的 hello 原因是因為 Azure AD 登入 (SSO) 處理或交換權杖時，需要 toocoordinate hello 通訊與 hello 應用程式。 hello 的 hello Azure AD 所簽發的權杖的存留時間過期時，就會過期 hello 使用者工作階段。 一定要評估您的應用程式是否應該使用此時間，或者可以縮短此時間。 減少 hello 存留期可做為將會強制使用者 toosign 出一段時間為基礎的安全性措施。

不會強制進行身分識別控制項 tooaccess 應用程式並不會在 toosecurely 如何應用程式整合其身分識別管理系統引導其開發人員的組織可能會更容易受到 toocredential 竊取類型的攻擊，例如[弱式開啟 Web 應用程式安全性專案 (OWASP) 前 10 個中所述的驗證和工作階段管理](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)。

您可以閱讀 [Azure AD 的驗證案例](../active-directory/active-directory-authentication-scenarios.md)，進一步了解 SaaS 應用程式的驗證案例。

## <a name="actively-monitor-for-suspicious-activities"></a>主動監視可疑的活動
根據太[Verizon 2016 資料缺口報表](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/)、 認證入侵仍處於 hello 上升並成為其中一個 hello 利潤最高的企業網路罪犯的。 基於這個理由，是重要 toohave 作用中的身分識別監視系統可以快速偵測可疑行為活動和觸發程序進一步調查的警示。 Azure AD 有兩項主要功能可協助組織監視其身分識別：Azure AD Premium [異常報告](../active-directory/active-directory-view-access-usage-reports.md)與 [Azure AD 身分識別保護](../active-directory/active-directory-identityprotection.md)功能。

請確定 toouse hello 異常報告 tooidentify 嘗試 toosign 中的[不被追蹤](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md)，[暴力](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md)攻擊特定帳戶，從多個位置中的嘗試 toosign 登入從[受感染裝置](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md)和可疑的 IP 位址。 請記住，這些都是報告。 換句話說，您必須處理和程序中的放置的 IT 系統管理員 」 toorun 這些報表 hello 每日或依需求 （通常是在事件回應案例中）。

相較之下，Azure AD identity protection 是作用中的監視系統和它將會加上旗標 hello 它自己的儀表板上目前的風險。 除此之外，您也會透過電子郵件收到每日摘要通知。 我們建議您調整 hello 風險層級根據 tooyour 商務需求。 hello 風險事件的風險層級是 hello hello 風險事件嚴重性指示 （高、 中或低）。 hello 風險層級可協助識別身分保護使用者設定優先權 hello tooreduce hello 風險 tootheir 組織必須採取的動作。

未主動監視其身分識別系統的組織有洩漏使用者認證的風險。 可疑的活動所採取的不知情的情況下將使用這些認證，組織就看不能 toomitigate 這種類型的威脅。
您可以閱讀 [Azure Active Directory 身分識別保護](../active-directory/active-directory-identityprotection.md)，進一步了解 Azure 身分識別保護。
