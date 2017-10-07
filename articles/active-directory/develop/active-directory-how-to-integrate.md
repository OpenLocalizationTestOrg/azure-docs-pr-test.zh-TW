---
title: "與 Azure Active Directory aaaHow tooIntegrate |Microsoft 文件"
description: "指南 toobenefits 與資源與 Azure Active Directory 整合。"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 4542965ae4a7756eda9f57e9e895f8044892f20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-azure-active-directory"></a>與 Azure Active Directory 整合
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory 為組織提供企業等級的雲端應用程式身分識別管理。  Azure AD 整合可以簡化的登入程序，讓您的使用者，並協助您符合 tooIT 原則的應用程式。

## <a name="how-toointegrate"></a>如何 tooIntegrate
有幾種方式為您的應用程式 toointegrate 與 Azure AD。  充分利用適合您應用程式使用的這些案例。

### <a name="support-azure-ad-as-a-way-toosign-in-tooyour-application"></a>支援 Azure AD 作為方式 tooSign tooYour 應用程式中
**減少登入的不便，並降低支援成本。** 使用 Azure AD toosign tooyour 應用程式中，您的使用者將不會有一個更多的名稱和密碼 tooremember。  身為開發人員，您會有一個較少密碼 toostore 並保護。  沒有 toohandle 忘記的密碼重設，可能會大幅節省單獨。  Azure AD 可登入提供 hello world 熱門雲端應用程式，包括 Office 365 和 Microsoft Azure 的某些功能。  數百萬從數百萬個組織的使用者，可能是您的使用者已經登入 tooAzure AD。  深入了解[新增 Azure AD 登入支援](active-directory-authentication-scenarios.md)。

**簡化應用程式的註冊程序。**  註冊應用程式的過程中，Azure AD 會寄出使用者的基本資訊，讓您可以預先填入註冊表單，或者完全不需要用到。  使用者可以註冊您的應用程式使用社交媒體和行動應用程式中找到熟悉同意的體驗類似 toothose 透過其 Azure AD 帳戶。  任何使用者可以註冊和登入 tooan 應用程式與 Azure AD 整合而不需要 IT 人員的介入。  深入了解[註冊應用程式以進行 Azure AD 帳戶登入](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。

### <a name="browse-for-users-manage-user-provisioning-and-control-access-tooyour-application"></a>瀏覽的使用者、 管理使用者佈建，以及控制存取 tooYour 應用程式
**瀏覽 hello 目錄中的使用者。**  Hello Graph API toohelp 使用者搜尋和瀏覽使用其組織中其他人，邀請其他人時，或授與存取權，而不需 tootype 電子郵件地址。  使用者可以瀏覽使用熟悉的地址通訊錄樣式介面，包括檢視 hello hello 組織性階層的詳細資料。  深入了解 hello [Graph API](active-directory-graph-api.md)。

**重複使用您的客戶已經在管理的 Active Directory 群組與通訊群組清單。**  Azure AD 包含 hello 群組您的客戶已使用的電子郵件發佈和管理存取權。  使用 hello Graph API，重複使用這些群組，而不需要客戶 toocreate 和管理一組個別的應用程式中的群組。  群組資訊也可以傳送 tooyour 應用程式的登入語彙基元。  深入了解 hello [Graph API](active-directory-graph-api.md)。

**使用 Azure AD toocontrol 擁有存取 tooyour 應用程式。**  系統管理員和 Azure AD 中的應用程式擁有者可以指派存取 tooapplications toospecific 使用者和群組。  您可以使用 hello Graph API，來讀取這份清單和 toocontrol 佈建和解除佈建的資源，請使用它並存取應用程式中。

**使用 Azure AD 進行角色型存取控制。**  系統管理員和應用程式擁有者可以指派使用者和群組 tooroles，當您在 Azure AD 中註冊您的應用程式定義。  角色資訊會傳送 tooyour 應用程式的登入權杖，並且也可以讀取使用 hello Graph API。  深入了解 [使用 Azure AD 進行授權](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx)。

### <a name="get-access-toousers-profile-calendar-email-contacts-files-and-more"></a>取得存取 tooUser 設定檔、 行事曆、 電子郵件、 連絡人、 檔案及其他
**Azure AD 是 hello for Office 365 的授權伺服器及其他 Microsoft 商務服務。**  如果您支援 Azure AD 進行登入 tooyour 應用程式或連結您目前的使用者帳戶 tooAzure AD 使用者帳戶使用 OAuth 2.0 的支援，您可以要求讀取和寫入權限 tooa 使用者的設定檔、 行事曆、 電子郵件、 連絡人、 檔案和其他資訊。  您可以順暢地撰寫事件 toouser 行事曆，並讀取或寫入檔案 tootheir OneDrive。  深入了解[存取 hello Office 365 Api](https://msdn.microsoft.com/office/office365/howto/platform-development-overview)。

### <a name="promote-your-application-in-hello-azure-and-office-365-marketplaces"></a>升級您的應用程式在 hello Azure 和 Office 365 市場
**將升級您的組織已經使用 Azure AD 的應用程式 toohello 百萬。**  搜尋和瀏覽 Marketplace 的使用者已經使用一或多項雲端服務，讓他們成為合格的雲端服務客戶。  深入了解升級您的應用程式中[hello Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/)。

**當使用者註冊您的應用程式時，它便會出現在其 Azure AD 存取面板和 Office 365 應用程式啟動程式中。**  使用者將能夠 tooquickly 和更新版本中，輕鬆地傳回 tooyour 應用程式提升的使用者參與。  深入了解 hello [Azure AD 存取面板](../active-directory-saas-access-panel-introduction.md)。

### <a name="secure-device-to-service-and-service-to-service-communication"></a>保護裝置對服務和服務對服務通訊的安全
**使用 Azure AD 身分識別管理的服務和裝置可減少您需要 toowrite 並可讓 IT toomanage 存取 「 hello 」 程式碼。**  服務和裝置可以從 Azure AD 使用 OAuth 取得的權杖，並使用這些語彙基元 tooaccess web Api。  使用 Azure AD，您可以避免撰寫複雜的驗證程式碼。  由於 hello hello 服務和裝置身分識別儲存在 Azure AD 中，IT 可以管理金鑰和撤銷而不需 toodo 這個別應用程式中的一個位置中。

## <a name="benefits-of-integration"></a>整合的優點
與 Azure AD 整合隨附不需要您 toowrite 額外的程式碼的優點。

### <a name="integration-with-enterprise-identity-management"></a>與企業身分識別管理整合
**協助您的應用程式符合 IT 原則。**  組織整合其企業身分識別管理系統與 Azure AD 中，因此，當個人離開組織時，它們將自動存取 tooyour 應用程式，IT 需要 tootake 沒有額外的步驟。  IT 人員可以存取您的應用程式，並判斷何種存取原則所需的範例多因素驗證-減少您需要 toowrite 程式碼 toocomply 的複雜的公司原則可以管理。  Azure AD 提供詳細的稽核記錄檔的人員因此登入 tooyour 應用程式系統管理員 IT 可以追蹤使用狀況。

**Azure AD 延伸 Active Directory toohello 雲端，讓您的應用程式可以與 AD 整合。**  Hello 世界各地的許多組織 Active Directory 做為其主體的登入和身分識別管理系統，並需要其 ad 的應用程式 toowork。  與 Azure AD 整合即可將 Active Directory 和您的應用程式整合。

### <a name="advanced-security-features"></a>進階的安全性功能
**多因素驗證。**  Azure AD 提供原生多因素驗證。  IT 系統管理員可以要求多重要素驗證 tooaccess 應用程式，讓您不需要 toocode 這項支援您自己。  深入了解 [多因素驗證](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)。

**登入偵測異常。**  Azure AD 處理十億個以上次登入一天，同時使用機器學習演算法 toodetect 可疑的活動，並通知 IT 系統管理員的可能發生的問題。  藉由支援 Azure AD 登入，您的應用程式會取得這項保護的 hello 優點。 深入了解[檢視 Azure Active Directory 存取報告](../active-directory-view-access-usage-reports.md)。

**條件式存取。**  此外 toomulti 雙因素驗證，系統管理員可以要求之前使用者可以登入，必須滿足特定條件 tooyour 應用程式。  可以設定的條件中指定的群組和 hello hello 裝置用於存取狀態，包括 hello IP 位址範圍的用戶端裝置、 成員資格。  深入了解 [Azure Active Directory 條件式存取](../active-directory-conditional-access.md)。

### <a name="easy-development"></a>容易開發
**業界標準通訊協定。**  Microsoft 是認可的 toosupporting 業界標準。  Azure AD 支援 hello SAML 2.0、 OpenID Connect 1.0、 OAuth 2.0 和 WS-同盟 1.2 驗證通訊協定。  hello Graph API 是 OData 4.0 標準。  如果您的應用程式已經支援 SAML 2.0 hello 或 OpenID Connect 1.0 通訊協定的同盟登入，加入 Azure AD 支援是很直接。  深入了解 [Azure AD 支援的驗證通訊協定](active-directory-authentication-protocols.md)。

**開放原始碼程式庫。**  Microsoft 提供常用的語言與平台 toospeed 開發完全支援的開放原始碼程式庫。  hello 原始碼 Apache 2.0 下授權，也是可用 toofork 和參與回復 toohello 專案。  深入了解 [Azure AD 驗證程式庫](active-directory-authentication-libraries.md)。

### <a name="worldwide-presence-and-high-availability"></a>全球的目前狀態和高可用性
**Azure AD 中 hello 世界各地的資料中心部署和管理，且監視周圍 hello 時鐘。**  Azure AD 為 Microsoft Azure 和 Office 365 的 hello 身分識別管理系統，並部署 28 hello 世界各地的資料中心內。  保證目錄資料複寫的 toobe tooat 至少三個資料中心。  使用者存取 hello 的 Azure AD 包含其資料，最接近的複本，並自動重新路由傳送要求 tooother 資料中心偵測到問題時，請確定全域負載平衡器。

## <a name="next-steps"></a>後續步驟
[開始撰寫程式碼](active-directory-developers-guide.md#get-started)

[使用 Azure AD 登入使用者](active-directory-authentication-scenarios.md)

