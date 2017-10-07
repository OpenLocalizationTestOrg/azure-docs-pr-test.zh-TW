---
title: "aaaWhat 是與 Azure Active Directory 的應用程式存取和單一登入？ | Microsoft Docs"
description: "使用 Azure Active Directory tooenable 單一登入 tooall hello SaaS 和 web 應用程式所需的商務。"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 75d1a3fd-b3c5-4495-a5c8-c4c24145ff00
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curyand
ms.openlocfilehash: 429522cbd570ab27359c4630c5a6d7b25b692ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-access-and-single-sign-on-with-azure-active-directory"></a>什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？
單一登入意指要能 tooaccess 所有 hello 應用程式和 toodo 商務需要的登入一次只能使用單一使用者帳戶的資源。 一旦登入，您可以存取所有您需要不必要的 tooauthenticate hello 應用程式 （例如輸入密碼） 第二次。

許多組織依賴軟體即服務 (SaaS) 應用程式，例如 Office 365、Box 和 Salesforce 來提升使用者生產力。 在過去，IT 人員需要 tooindividually 建立和更新每個 SaaS 應用程式中的使用者帳戶和使用者有 tooremember 每個 SaaS 應用程式密碼。

Azure Active Directory 延伸內部部署 Active Directory 至 hello 雲端啟用使用者 toouse 其主要組織帳戶 toonot 只有登入 tootheir 加入網域的裝置和公司資源，但也是全部 hello web 和 SaaS 應用程式需要其工作。

因此不只使用者沒有 toomanage 多重集的使用者名稱和密碼，可自動佈建或取消佈建存取其應用程式根據其組織的群組成員，以及其狀態為員工。 Azure Active Directory 引進了安全性和存取管理控制項，讓您 toocentrally 管理使用者存取所有 SaaS 應用程式。

Azure AD 可輕鬆整合 toomany 今天的熱門的 SaaS 應用程式。它提供身分識別和存取管理，及直接管理，可讓使用者 toosingle 登入 tooapplications 或探索並啟動它們從入口網站，例如 Office 365 或 hello Azure AD 存取面板。

hello hello 整合架構包含下列四個主要建置組塊的 hello:

* 單一登入可讓使用者 tooaccess 根據其組織帳戶，在 Azure AD 中其 SaaS 應用程式。 單一登入可讓使用者 tooauthenticate tooan 應用程式使用單一組織帳戶。
* 使用者佈建可讓使用者根據在 Windows Server Active Directory 和/或 Azure AD 中所做的變更，佈建和解除佈建到目標 SaaS。 佈建的帳戶可讓使用者獲得授權的 toobe toouse 應用程式，它們透過單一登入已驗證之後。
* Hello Azure 管理入口網站中的集中式應用程式存取管理 可讓單點 SaaS 應用程式存取和使用 hello 能力 toodelegate 應用程式存取決策制定和核准 tooanyone hello 組織中的管理，
* 統一報告和監視 Azure AD 中的使用者活動

## <a name="how-does-single-sign-on-with-azure-active-directory-work"></a>單一登入如何搭配 Azure Active Directory 運作？
當使用者 「 登入 」 tooan 應用程式時，它們通過驗證程序當他們是他們的身分它們的必要的 tooprove。 沒有單一登入，這通常是藉由輸入的密碼儲存在 hello 應用程式，以及 hello 使用者是否為必要的 tooknow 這個密碼。

Azure AD 支援三個不同的方式 toosign tooapplications 中：

* **同盟單一登入**可讓應用程式 tooredirect tooAzure AD 進行使用者驗證，而不是它自己的密碼提示。 這被支援應用程式支援 SAML 2.0 中，WS-同盟或 OpenID Connect，例如通訊協定，且 hello 豐富模式的單一登入。
* **密碼單一登入** 可以使用網頁瀏覽器延伸或行動應用程式，安全儲存應用程式的密碼以及重新執行。 這可利用 hello 現有登入程序提供的 hello 應用程式，但可讓系統管理員 toomanage hello 密碼並不需要 hello 使用者 tooknow hello 密碼。
* **現有單一登入**任何現有單一登入已設定為從 hello 應用程式，但可讓這些應用程式連結 toobe toohello Office 365 或 Azure AD 存取面板入口網站，而且也可讓啟用 Azure AD tooleverage其他 hello 應用程式會啟動時那里 Azure AD 中的報告。

一旦使用者已驗證的應用程式，也需要在 hello 會告訴 hello 應用程式的應用程式佈建帳戶記錄 toohave 其中那里權限和存取層級位於 hello 應用程式。 hello 佈建這個帳戶記錄可能會發生自動執行，或它之前，可能發生手動由系統管理員 hello 使用者提供單一登入存取。

 以下是有關這些單一登入模式和佈建的詳細資訊。

### <a name="federated-single-sign-on"></a>同盟單一登入
同盟單一登入可讓您的組織 toobe 經由 Azure AD 中的 hello 使用者帳戶資訊，使用 Azure AD 自動登入 tooa 協力廠商 SaaS 應用程式中的登入可讓 hello 使用者。

在此案例中，當您已經登入 Azure AD 中，而且您想 tooaccess 資源所控制的第三方 SaaS 應用程式中，同盟作業免除重新驗證使用者 toobe hello 需求。

Azure AD 可支援同盟單一登入支援 hello SAML 2.0 WS-同盟、 應用程式或 OpenID connect 通訊協定。

亦請參閱： [管理同盟單一登入的憑證](active-directory-sso-certs.md)

### <a name="password-based-single-sign-on"></a>密碼單一登入
設定密碼單一登入，可讓您的組織 toobe 經由 hello 協力廠商 SaaS 應用程式中的 hello 使用者帳戶資訊，使用 Azure AD 自動登入 tooa 協力廠商 SaaS 應用程式中的 hello 使用者。 當您啟用此功能時，Azure AD 會收集並安全地儲存 hello 使用者帳戶資訊和 hello 相關的密碼。

Azure AD 可以對具有 HTML 登入頁面的任何雲端應用程式支援密碼單一登入。 使用自訂瀏覽器外掛程式，AAD hello 使用者的登入透過安全地擷取應用程式 hello 使用者名稱和密碼等認證 hello hello 目錄中的程序會自動執行，這些認證輸入 hello 應用程式的登入頁面代表 hello 使用者執行。 有兩個使用案例：

1. **系統管理員管理認證**– 系統管理員可以建立及管理應用程式認證和指定這些認證 toousers 或需要存取 toohello 應用程式的使用者群組。 在這些情況下，hello 終端使用者不需要 tooknow hello 認證，但是依然可以利用單一登入存取 toohello 應用程式，只要按一下它，其存取權面板中，或透過提供的連結。 這種方法可以讓 hello 認證的 hello 系統管理員，以及方便的生命週期管理的使用者，讓它們不需要 tooremember 或管理應用程式專用密碼。 hello 認證是在處理序; 中的 hello 自動化註冊時模糊化 hello 終端使用者從不過，它們是技術上找到 hello 使用者利用 web 偵錯工具，以及使用者和系統管理員應遵循相同的安全性原則，如同 hello 認證的 hello 都會提供直接由 hello 使用者。 當提供的帳戶存取權是由許多使用者共用時，例如社交媒體或文件共用應用程式，系統管理員提供的認證會很有用。
2. **使用者管理認證**– 系統管理員可以指派應用程式 tooend 使用者或群組，並允許 hello 結束使用者 tooenter 他們自己的認證時直接存取 hello 應用程式的 hello 其存取權面板中的第一次。 這會建立方便起見，不需要 toocontinually 使用者輸入 hello 應用程式專用密碼每次存取 hello 應用程式。 此使用案例也可用來當作逐步執行的棋子 tooadministrative 管理 hello 認證，讓 hello 系統管理員可以設定 hello 應用程式的新認證在未來的日期而不需要變更 hello 位使用者的 hello 應用程式存取經驗。

在這兩種情況下，認證會儲存在 hello 目錄中，以加密狀態，而且只會透過 HTTPS 傳遞 hello 自動登入程序期間。 使用密碼單一登入，Azure AD 就能對無法支援同盟通訊協定的應用程式提供方便的身分識別存取管理解決方案。

密碼 SSO 依賴瀏覽器延伸模組 toosecurely 擷取 hello 應用程式和使用者特定資訊從 Azure AD，並將它套用 toohello 服務。 Azure AD 支援的大多數協力廠商 SaaS 應用程式都支援這項功能。

針對密碼型 SSO，hello 終端使用者的瀏覽器可以是：

* Internet Explorer 8、9、10、11 -- Windows 7 或更新版本 (另請參閱 [IE 擴充功能部署指南](active-directory-saas-ie-group-policy.md))
* Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上
* Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上

**注意：** hello 密碼型 SSO 延伸模組將可供 Windows 10 中的 edge 瀏覽器延伸模組會變成支援 Edge 的說明時。

### <a name="existing-single-sign-on"></a>現有單一登入
在設定單一登入應用程式時，hello Azure 管理入口網站提供的 現有單一登入 」 的第三個選項。 此選項只會允許 hello 管理員 toocreate 連結 tooan 應用程式，並將它放 hello 選使用者的存取面板上。

例如，如果應用程式設定使用 Active Directory Federation Services 2.0 tooauthenticate 使用者時，系統管理員可以使用 hello 現有單一登入 」 選項 toocreate 連結 tooit hello 存取面板上。 當使用者存取 hello 連結時，它們會使用 Active Directory Federation Services 2.0，或任何現有的單一登入解決方案 hello 應用程式提供驗證。

### <a name="user-provisioning"></a>使用者佈建
對於選取的應用程式，Azure AD 會啟用自動的使用者佈建和解除佈建第三方 SaaS 應用程式中 hello 使用 Windows Server Active Directory 或 Azure AD 識別身分資訊的 Azure 管理入口網站中的帳戶。 當使用者在 Azure AD 中獲得其中一個應用程式中指定的權限時，可以是自動建立 （佈建帳戶） hello 目標 SaaS 應用程式中。

當使用者刪除或其資訊變更在 Azure AD 中時，這些變更也會反映在 hello SaaS 應用程式。 這表示，設定自動化身分識別生命週期管理可讓系統管理員 toocontrol，並提供自動化佈建和解除佈建從 SaaS 應用程式。 在 Azure AD 中，使用者佈建已啟用此自動化身分識別週期管理。

詳細資訊，請參閱 toolearn[自動化使用者佈建和取消佈建 tooSaaS 應用程式](active-directory-saas-app-provisioning.md)

## <a name="get-started-with-hello-azure-ad-application-gallery"></a>開始使用 hello Azure AD 應用程式庫
準備好 tooget 啟動嗎？toodeploy 單一登入 Azure AD 之間和 SaaS 應用程式，您的組織使用，請遵循這些指導方針。

### <a name="using-hello-azure-ad-application-gallery"></a>使用 hello Azure AD 應用程式庫
hello [Azure Active Directory 應用程式庫](https://azure.microsoft.com/marketplace/active-directory/all/)提供已知 toosupport 表單的單一登入與 Azure Active Directory 的應用程式的清單。

![][1]

以下是尋找應用程式支援哪些功能的一些提示：

* Azure AD 支援自動佈建和解除佈建所有 「 精選"中的應用程式 hello [Azure Active Directory 應用程式庫](https://azure.microsoft.com/marketplace/active-directory/all/)。
* 在 [這裡](http://social.technet.microsoft.com/wiki/contents/articles/20235.azure-active-directory-application-gallery-federated-saas-apps.aspx)則可以找到特別支援使用如 SAML，WS-同盟或 OpenID Connect 通訊協定之同盟單一登入的同盟應用程式清單。

一旦您找到了您的應用程式，您可以開始 hello 應用程式庫中的後續 hello 逐步指示，並在 hello Azure 管理入口網站 tooenable 單一登入。

### <a name="application-not-in-hello-gallery"></a>不在 hello 組件庫中的應用程式嗎？
如果在 hello Azure AD 應用程式庫中找不到您的應用程式，您會有下列選項：

* **新增未列出的應用程式，您使用**-hello hello Azure 管理入口網站 tooconnect 您的組織使用未列出應用程式內的應用程式庫中使用 hello 自訂類別。 您可以加入支援 SAML 2.0 的任何應用程式做為同盟應用程式，或者加入具有 HTML 登入頁面的任何應用程式做為密碼 SSO 應用程式。 如需詳細資訊，請參閱 [加入自己的應用程式](active-directory-saas-custom-apps.md)一文。
* **新增您自己所開發的應用程式**-如果您已開發出 hello 應用程式，請遵循 hello 指導方針，在 Azure AD 開發人員文件 tooimplement 同盟單一登入的 hello 或使用佈建 hello Azure AD graph API。 如需詳細資訊，請參閱這些資源：
  
  * [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)
  * [https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore)
* **要求應用程式整合**-要求 hello 應用程式，您需要使用支援 hello [Azure AD 的意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)。

### <a name="using-hello-azure-management-portal"></a>使用 hello Azure 管理入口網站
您可以在 Azure 管理入口網站 tooconfigure hello 應用程式單一登入的 hello 使用 hello Active Directory 延伸模組。 第一個步驟中，您需要 tooselect hello hello 入口網站中的 Active Directory 區段中的目錄：

![][2]

toomanage 您協力廠商 SaaS 應用程式中，您可以切換成 hello hello 選目錄的應用程式 索引標籤。 這個檢視可讓系統管理員：

* 從 hello Azure AD 資源庫，以及您所開發的應用程式中加入新的應用程式
* 刪除整合的應用程式
* 管理已經整合 hello 應用程式

協力廠商 SaaS 應用程式的一般管理工作有：

* 啟用單一登入 Azure ad 的使用密碼 SSO，或如果適用於 hello 目標 SaaS、 同盟 sso 的話
* (選擇性) 啟用使用者佈建來佈建和解除佈建使用者 (身分識別週期管理)
* 在啟用使用者佈建應用程式，請選取 哪些使用者可以存取 toothat 應用程式

針對支援同盟單一登入的組件庫應用程式，設定您通常需要 tooprovide 額外的組態設定，例如憑證和中繼資料 toocreate hello 第三方應用程式與 Azure AD 之間的同盟的信任。 hello 設定精靈將引導您完成 hello 詳細資料，並提供讓您輕鬆存取 toohello SaaS 應用程式特定資料，和指示。

針對支援自動使用者佈建的組件庫應用程式，這需要您 toogive Azure AD 權限 toomanage 您 hello SaaS 應用程式中的帳戶。 最少，您需要的 tooprovide toohello 目標應用程式在進行驗證時，應該使用 Azure AD 認證。 其他組態設定是否需要提供 toobe 取決於 hello hello 應用程式需求。

## <a name="deploying-azure-ad-integrated-applications-toousers"></a>部署 Azure AD 整合的應用程式 toousers
Azure AD 提供 toodeploy 應用程式 tooend-使用者在組織中的幾個可自訂的方式：

* Azure AD 存取面板
* Office 365 應用程式啟動程式
* 直接登入 toofederated 應用程式
* 深層連結 toofederated，密碼為基礎或現有的應用程式

在您的組織中欄位選擇 toodeploy 方法是自行斟酌。

### <a name="azure-ad-access-panel"></a>Azure AD 存取面板
https://myapps.microsoft.com 在 hello 存取面板是網頁型的入口網站，可讓具有組織帳戶的使用者在 Azure Active Directory tooview 和啟動雲端型應用程式 toowhich 它們已被授與存取權 hello Azure AD系統管理員。 如果您的使用者[Azure Active Directory Premium](https://azure.microsoft.com/pricing/details/active-directory/)，您也可以利用透過存取面板 hello 自助式群組管理功能。

![][3]

hello 存取面板是分開 hello Azure 管理入口網站，而且不需要使用者 toohave 的 Azure 訂用帳戶或 Office 365 訂閱。

如需有關 hello Azure AD 存取面板的詳細資訊，請參閱 hello[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

### <a name="office-365-application-launcher"></a>Office 365 應用程式啟動程式
對於已部署 Office 365 的組織而言，指派 toousers 透過 Azure AD 的應用程式也會出現在 https://portal.office.com/myapps hello Office 365 入口網站。 如此便可輕鬆且方便使用者組織 toolaunch 中自己的應用程式而不需要 toouse 的第二個入口網站，並 hello 建議應用程式啟動的組織使用 Office 365 的方案。

![][4]

如需 hello Office 365 應用程式啟動程式的詳細資訊，請參閱[應用程式會出現在 hello Office 365 應用程式啟動器](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher)。

### <a name="direct-sign-on-toofederated-apps"></a>直接登入 toofederated 應用程式
最同盟的應用程式支援 SAML 2.0、 WS-同盟或 OpenID 也連接使用者 toostart hello 的應用程式的支援 hello 能力，然後再取得登入 Azure AD 透過自動重新導向或在連結 toosign 上即可。 這稱為服務提供者-初始化登入和最 hello Azure AD 應用程式庫中的同盟應用程式支援 （請參閱 hello 文件連結從 hello Azure 管理入口網站中的 hello 應用程式的單一登入設定精靈詳細資料）。

![][5]

### <a name="direct-sign-on-links-for-federated-password-based-or-existing-apps"></a>同盟、密碼或現有應用程式的直接登入連結
Azure AD 也支援直接單一登入連結 tooindividual 應用程式支援密碼單一登入、 現有單一登入，和任何形式的同盟單一登入。

這些連結是特別撰寫的 Url 傳送使用者已透過 hello Azure AD 登入特定的應用程式，而不需要 hello 使用者的程序則會從 hello Azure AD 存取面板或 Office 365 啟動它們。 這些單一登入 Url 可以找到 hello hello hello Azure 管理入口網站中，Active Directory 區段中任何預先整合應用程式的儀表板 索引標籤下，hello 以下螢幕擷取畫面所示。

![][6]

這些連結可以複製和貼上您要登入 tooprovide 連結 toohello 選取應用程式的任何地方。 可以是在電子郵件中，或是任何您已設定使用者應用程式存取權的自訂網頁型入口網站中。 以下是 Azure AD 直接單一登入 Twitter 的 URL 範例：

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Hello 存取面板類似 tooorganization 特定的 Url，您可以進一步自訂這個 URL 之後 hello myapps.microsoft.com 網域加入的其中一個 hello 作用中或已驗證網域，為您的目錄。 這可確保任何組織商標立即載入 hello 登入頁面上沒有 hello 使用者第一次需要 tooenter 他們的使用者識別碼：

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

當授權的使用者按一下其中一個特定的應用程式連結時，他們第一次看到其組織登入頁面 （假設它們沒有已登入），及在登入之後會重新導向的 tootheir 應用程式，但不先停止在 hello 存取面板。 如果 hello 使用者遺失 tooaccess hello 應用程式，例如 hello 密碼為基礎的單一登瀏覽器延伸模組的先決條件 hello 連結將會提示 hello 使用者 tooinstall hello 遺漏延伸模組。 hello 連結 URL 也會維持不變如果 hello 單一登入 hello 應用程式之設定變更。

這些連結使用 hello hello 為相同的存取控制機制存取面板和 Office 365 及 toosuccessfully 只有這些使用者或群組已獲指派 toohello hello Azure 管理入口網站中的應用程式驗證。 不過，任何未經授權的使用者會看到訊息，說明他們未獲得存取權，且都各有連結 tooload hello 存取面板 tooview 可用的應用程式，他們沒有存取權。

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [使用 Cloud App Discovery 尋找未經約束的雲端應用程式](active-directory-cloudappdiscovery-whatis.md)
* [簡介 tooManaging 存取 tooApps](active-directory-managing-access-to-apps.md)
* [比較 Azure AD 中管理外部身分識別的功能](active-directory-b2b-compare-external-identities.md)

<!--Image references-->
[1]: ./media/active-directory-appssoaccess-whatis/onlineappgallery.png
[2]: ./media/active-directory-appssoaccess-whatis/azuremgmtportal.png
[3]: ./media/active-directory-appssoaccess-whatis/accesspanel.png
[4]: ./media/active-directory-appssoaccess-whatis/officeapphub.png
[5]: ./media/active-directory-appssoaccess-whatis/workdaymobile.png
[6]: ./media/active-directory-appssoaccess-whatis/deeplink.png
