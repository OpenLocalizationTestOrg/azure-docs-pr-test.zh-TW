---
title: "aaaAzure 安全性功能，與身分識別管理可協助 |Microsoft 文件"
description: " 本文章提供協助您進行身分識別管理 hello 核心 Azure 的安全性功能的概觀。 Microsoft 身分識別和存取管理解決方案說明 IT 保護存取 tooapplications 及資源 hello 公司資料中心跨和進入 hello 雲端啟用驗證，例如多因素驗證和條件的額外層級存取原則。 "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Azure 身分識別管理安全性概觀
Microsoft 身分識別和存取管理解決方案說明 IT 保護存取 tooapplications 及資源 hello 公司資料中心跨和進入 hello 雲端啟用驗證，例如多因素驗證和條件的額外層級存取原則。 透過進階的安全性報告、稽核和警示來監視可疑活動，有助於減緩潛在的安全性問題。 [Azure Active Directory Premium](../active-directory/active-directory-editions.md)提供雲端 (SaaS) 應用程式和執行在內部部署存取 tooweb 應用程式的單一登入 toothousands。

安全性優點的 Azure Active Directory (AD) 包括 hello 能力：

* 為您的混合式企業中的每位使用者建立和管理單一身分識別，讓使用者、群組和裝置保持同步
* Tooyour 應用程式包括數千個預先整合的 SaaS 應用程式提供單一登入存取
* 藉由同時對內部部署和雲端應用程式強制以規則為基礎的 Multi-Factor Authentication，啟用應用程式存取安全性
* 佈建的安全遠端存取 tooon 內部部署 web 應用程式可以透過 Azure AD Application Proxy

這篇文章的 hello 目標是 tooprovide hello 核心 Azure 的安全性功能，協助進行身分識別管理的概觀。 我們也提供了提供給每項功能的詳細資料，因此，您可以深入的連結 tooarticles。  

hello 文件著重於 hello 下列核心 Azure 身分識別管理功能：

* 單一登入
* 反向 proxy
* Multi-Factor Authentication
* 安全性監視、警示以及機器學習服務型報告
* 消費者身分識別與存取管理
* 裝置註冊
* Privileged Identity Management
* 身分識別保護
* 混合式身分識別管理

## <a name="single-sign-on"></a>單一登入
單一登入 (SSO) 意指要能 tooaccess 所有 hello 應用程式和 toodo 商務需要的登入一次只能使用單一使用者帳戶的資源。 一旦登入，您可以存取所有您需要不必要的 tooauthenticate hello 應用程式 （例如，輸入密碼） 第二次。

許多組織依賴軟體即服務 (SaaS) 應用程式，例如 Office 365、Box 和 Salesforce 來提升使用者生產力。 在過去，IT 人員需要 tooindividually 建立和更新每個 SaaS 應用程式中的使用者帳戶和使用者有 tooremember 每個 SaaS 應用程式密碼。

Azure AD 會擴充到 hello 的雲端，在內部部署 Active Directory 環境中啟用使用者 toouse 其主要組織帳戶 toonot 只有登入 tootheir 加入網域的裝置和公司資源，但也所有 hello web 和 SaaS 應用程式需要其工作。

不僅使用者沒有 toomanage 多重集的使用者名稱和密碼，可以自動佈建或取消佈建根據組織群組和其狀態為員工應用程式存取權。 Azure AD 引進了安全性和存取管理控制項，讓您 toocentrally 管理使用者存取所有 SaaS 應用程式。

深入了解：

* [單一登入概觀](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](../active-directory/active-directory-appssoaccess-whatis.md)
* [整合 Azure Active Directory 單一登入與 SaaS 應用程式](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>反向 proxy
Azure AD Application Proxy 可讓您發行內部應用程式，例如[SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US)站台， [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx)，和[IIS](http://www.iis.net/)為基礎的應用程式在私人網路內部並提供您的網路之外的安全存取 toousers。 應用程式 Proxy 提供遠端存取權和單一登入 (SSO) 的許多類型的內部使用 hello 數千個 Azure AD 支援的 SaaS 應用程式的 web 應用程式。 員工可以登入 tooyour 應用程式的首頁上自己的裝置，透過這個雲端架構 proxy 進行驗證。

深入了解：

* [啟用 Azure AD 應用程式 Proxy](../active-directory/active-directory-application-proxy-enable.md)
* [使用 Azure AD 應用程式 Proxy 發佈應用程式](../active-directory/active-directory-application-proxy-publish.md)
* [使用應用程式 Proxy 進行單一登入](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [使用條件式存取](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Azure multi-factor authentication (MFA) 是驗證的程式需要 hello 使用一個以上的驗證方法，並將重要的第二層的安全性 toouser 登入和交易方法。 MFA 有助於保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。 它可以透過一些驗證選項 (例如電話、文字訊息，或行動應用程式通知或驗證代碼，以及第三方 OAuth 權杖) 來提供強大的驗證功能。

深入了解：

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure Multi-Factor Authentication 的作用](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>安全性監視、警示以及機器學習服務型報告
安全性監視和警示以及機器學習式報告，會識別不一致的存取模式，可以協助您保護企業安全。 您可以使用 Azure Active Directory 的存取和使用方式報表 toogain 掌握 hello 完整性與安全性貴組織的目錄。 利用此資訊，目錄管理員更能夠判斷可能發生安全性風險的地方，讓他們做充裕的計畫 toomitigate 這些風險。

Hello Azure 傳統入口網站，在報表的分類中 hello 下列方法：

* 異常報表-包含登入事件，我們發現 toobe 異常。 我們的目標是 toomake 您注意這類活動，並讓您 toobe 無法 toomake 判斷事件是否可疑。
* 整合式應用程式報告 – 可供深入了解雲端應用程式在組織中的使用方式。 Azure Active Directory 提供與數千個雲端應用程式的整合。
* 錯誤報表 – 指出佈建帳戶 tooexternal 應用程式時可能發生的錯誤。
* 使用者特定報告 – 顯示特定使用者的裝置/登入活動資料。
* 活動記錄-包含 hello 內所有稽核事件的記錄，過去 24 小時、 過去 7 天或過去 30 天內，以及群組活動變更、 和密碼重設和註冊活動。

深入了解：

* [檢視存取和使用情況報告](../active-directory/active-directory-view-access-usage-reports.md)
* [開始使用 Azure Active Directory 報告](../active-directory/active-directory-reporting-getting-started.md)
* [Azure Active Directory 報告指南](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>消費者身分識別與存取管理
Azure Active Directory B2C 是縮放 toohundreds 數百萬個身分識別的高可用性、 全域的身分識別管理服務消費者導向應用程式。 此服務可跨行動及 Web 平台進行整合。 取用者可以登入 tooall 您的應用程式，透過可自訂的方式藉由使用其現有的社交帳戶或建立新的認證。

在過去的 hello，應用程式開發人員想 toosign 總並在取用者的登入到應用程式會撰寫自己的程式碼。 它們會使用內部部署資料庫或系統 toostore 的使用者名稱和密碼。 Azure Active Directory B2C 提供組織更好的方式 toointegrate 取用者身分識別管理到 hello 協助應用程式的安全、 標準為基礎的平台和將大量的可延伸的原則。

當您使用 Azure Active Directory B2C 時，您的取用者可以使用現有的社交帳戶 (Facebook、Google、Amazon、LinkedIn) 註冊應用程式，或是建立新的認證 (電子郵件地址與密碼，或使用者名稱與密碼)。

深入了解：

* [什麼是 Azure Active Directory B2C？](https://azure.microsoft.com/services/active-directory-b2c/)
* [Azure Active Directory B2C 預覽：在您的應用程式中註冊與登入取用者](../active-directory-b2c/active-directory-b2c-overview.md)
* [Azure Active Directory B2C 預覽：應用程式類型](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>裝置註冊
Azure AD 裝置註冊是 hello 基礎裝置型[條件式存取](../active-directory/active-directory-conditional-access-device-registration-overview.md)案例。 裝置註冊時，Azure Active Directory 裝置註冊提供 hello 裝置時，才能使用的 tooauthenticate hello 裝置 hello 使用者登入的身分。 hello 驗證裝置 hello 裝置 hello 屬性接著可以使用的 tooenforce hello 雲端和內部部署中裝載的應用程式的條件式存取原則。

與 Intune 等行動裝置管理 (MDM) 解決方案結合時，Azure Active Directory 中的 hello 裝置屬性會更新 hello 裝置有關的其他資訊。 這可讓您 toocreate 條件式存取規則，以強制從裝置 toomeet 存取您的安全性與相容性的標準。

深入了解：

* [開始使用 Azure Active Directory 裝置註冊](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [自動向 Azure Active Directory 註冊加入網域的 Windows 裝置](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Azure Active Directory (AD) Privileged Identity Management 可讓您管理、 控制及監視您的特殊權限身分識別和存取 tooresources 在 Azure AD 中的，以及 Office 365 或 Microsoft Intune 等其他 Microsoft online services。

有時候使用者需要在 Azure 或 Office 365 資源或其他 SaaS 應用程式中的特殊權限作業 toocarry。 這通常表示的組織有 toogive 它們的永久特殊權限存取 Azure AD 中。 這會提高雲端資源的安全性風險，因為組織無法滴水不漏地監視這些使用者利用其管理員權限的所作所為。 此外，如果擁有特殊權限存取權的使用者帳戶遭到入侵，這個缺口可能會影響其整體的雲端安全性。 Azure AD Privileged Identity Management 可協助 tooresolve 這項風險。

Azure AD Privileged Identity Management 可讓您：

* 查看哪些使用者是 Azure AD 管理員
* 視需要啟用，"just-in-time"系統管理存取權 tooMicrosoft 線上服務，如 Office 365 和 Intune
* 取得有關系統管理員存取記錄與系統管理員指派變更的報告
* 取得警示存取 tooa 特殊權限角色

深入了解：

* [Azure AD 特殊權限身分識別管理](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Azure AD Privileged Identity Management 中的角色](../active-directory/active-directory-privileged-identity-management-roles.md)
* [Azure 的 AD Privileged Identity Management： 如何 tooadd 或移除使用者角色](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>身分識別保護
Azure AD Identity Protection 是一項安全性服務，可供整合檢視會影響組織身分識別的風險事件和潛在弱點。 Identity Protection 利用現有 Azure Active Directory 的異常偵測功能 (可透過 Azure AD 的異常活動報告取得)，並引進可即時偵測異常的新風險事件類型。

深入了解：

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [第 9 頻道：Azure AD 和身分識別展示：Identity Protection 預覽](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>混合式身分識別管理
Microsoft 的方法 tooidentity 跨越內部部署和 hello 雲端建立單一使用者識別進行驗證和授權 tooall 資源，不論位置為何。

深入了解：

* [混合式身分識別白皮書](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Active Directory 小組部落格](https://blogs.technet.microsoft.com/ad/)
