---
title: "aaaWhat 是 Azure Active Directory 中的 hello 存取面板？ | Microsoft Docs"
description: "了解如何 hello toouse 變化存取面板網頁瀏覽器、 Android 應用程式 （iPhone 和 iPad 應用程式） tooaccess SaaS 應用程式。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>Hello 存取面板是什麼？

hello 存取面板是網頁型入口網站。 它可讓使用者使用工作或學校帳戶在 Azure Active Directory tooview 並開始以雲端為基礎的應用程式的 Azure AD 系統管理員已授與存取權。 您也可以使用自助式群組並透過 hello 存取面板應用程式管理功能。

hello 存取面板是分開 hello Azure 入口網站，並不是您 toohave Azure 訂用帳戶。

![存取面板][1]

hello 存取面板可讓您 tooedit 一些設定檔設定，包括 hello 能力：

- 變更工作或學校帳戶相關聯的 hello 密碼

- 編輯密碼重設設定

- 編輯連絡人和喜好設定相關的 toomulti 雙因素驗證 (已被必要的 toouse 的帳戶，即可以系統管理員)

- 檢視帳戶詳細資料，例如，使用者識別碼、替代電子郵件、行動電話和辦公室電話號碼以及裝置

- 檢視並啟動雲端型應用程式 hello Azure AD 管理員已授與它們存取權。 如需從 hello 使用者的觀點來看 hello 存取面板的詳細資訊，請參閱使用 hello 存取面板。 

- 自我管理群組。 更具體來說，hello 系統管理員可以建立及管理 Azure AD 中的安全性群組和要求安全性群組成員資格。 如需詳細資訊，請參閱 [Azure AD 中使用者的自助群組管理](active-directory-accessmanagement-self-service-group-management.md)與[管理群組](active-directory-manage-groups.md)。




## <a name="accessing-hello-access-panel"></a>存取 hello 存取面板

您可以瀏覽下列 URL 在 web 瀏覽器中的 hello 存取 hello 存取面板：`http://myapps.microsoft.com`

如果您有自訂品牌設定登入頁面上，您可以載入此品牌藉由附加貴組織的網域 toohello hello URL 結尾：`http://myapps.microsoft.com/<your domain>.com`

在此情況下，您可以使用已在 Azure 入口網站中設定的任何作用中或已驗證網域名稱。

![Wingtip Toys 網域名稱][2]  

您需要 toodistribute hello URL tooall 將登入的使用者會與 Azure AD 整合的 tooapplications 中。

## <a name="authentication"></a>驗證

tooreach hello 存取面板中，您必須在 Azure AD 中驗證透過公司或學校帳戶。 您可以驗證的 tooAzure 向直接 AD。 或者，如果組織已經使用 Active Directory 同盟服務 (ADFS) 或其他技術設定同盟，則可由 Windows Server Active Directory 驗證您。

如果您有 Azure 或 Office 365 的訂閱，而且您已在使用 hello Azure 入口網站或 Office 365 應用程式，您可以看到應用程式的 hello 的清單不含登入一次。 如果您無法進行驗證您是在提示的 toosign hello 使用者名稱和密碼，使用 Azure AD 中為您的帳戶。 如果您的組織已設定同盟，輸入 hello 使用者名稱便已足夠。

當您驗證時，您可以互動 hello 應用程式與 hello 目錄整合您的系統管理員。 如何 toointegrate 應用程式與 Azure AD，請參閱的 toolearn[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。

## <a name="web-browser-requirements"></a>網頁瀏覽器需求

最少 hello 存取面板需要支援 JavaScript 的瀏覽器並 CSS 啟用。 登入密碼型單一登入 (SSO) 透過 tooapplications hello 使用者 toobe，hello 存取面板延伸模組必須安裝在您的瀏覽器。 當您選取已針對密碼型 SSO 設定的應用程式時，會自動下載 hello 延伸模組。

hello 存取面板延伸模組是目前可供 Internet Explorer 8 和更新版本，Edge、 Chrome 及 Firefox 瀏覽器。

## <a name="mobile-app-support"></a>行動應用程式支援

hello Azure Active Directory 團隊發行 hello 我的應用程式的行動裝置應用程式。 當您安裝 hello 應用程式時，您可以登入 toopassword 基礎 iOS 和 Android 裝置上的 SSO 應用程式。

> [!NOTE]
> 您可以登入 tooapplications 支援同盟與 Azure AD （包括 Salesforce、 Google Apps、 Dropbox、 Box、 Concur、 Workday、 Office 365 和其他超過 70） 上幾乎任何 web 瀏覽器，在任何裝置，而不需要的外掛程式或行動應用程式。 所有其他[存取面板體驗](https://myapps.microsoft.com/)也不需要行動裝置使用我的應用程式的行動裝置應用程式 toobe hello。
>
>

### <a name="my-apps-for-android"></a>My Apps for Android

執行 Android 4.1 版和更新版本的任何 Android 裝置支援 My Apps for Android。  
它是用於 hello [Google Play 商店](https://play.google.com/store/apps/details?id=com.microsoft.myapps)。

![My Apps for Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>My Apps for iPhone 和 iPad

執行 iOS 版本 7 和更新版本的任何 iPhone 或 iPad 均支援 My Apps for iOS。  
它是用於 hello [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)。

![My Apps for iOS][4]    



## <a name="managed-browser-for-my-apps"></a>My Apps 適用的受管理瀏覽器

我的應用程式也會整合 hello Intune Managed Browser。 適用於 iOS 和 Android 裝置的 Intune Managed Browser hello 扮演一個關鍵的角色，確保行動裝置上的資料保持安全。 它可讓您安全地檢視和瀏覽可能包含公司資訊的網頁，並提供安全的網頁瀏覽經驗。  
您會發現您受管理的瀏覽器的首頁上和您的書籤，讓您更少的快速存取 toomy 應用程式按一下 tooreach 想 tooaccess 任何應用程式。

它是用於 hello [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)和[Google Play 商店](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en)。

![My Apps 適用的受管理瀏覽器][5]    





## <a name="tips-for-testing-hello-user-experience"></a>測試 hello 使用者經驗的秘訣

如果您是 Azure 系統管理員，而且使用 hello 目錄中的帳戶登入 toohello Azure 入口網站，表示您會自動為您目前的帳戶登入 toohello 存取面板。 在此情況下，您可以查看所有已指派給 tooyou 的應用程式。

**做為 tootest*不同*使用者帳戶：**

1. 按一下 hello 右上角的 hello Azure 入口網站或 hello 存取面板 中的 hello 使用者功能表，然後選取**登出**。 
2. 移 toohello[存取面板](http://myapps.microsoft.com)。
3. 在 hello 登入頁面、 型別 hello 使用者名稱和您的目錄中的 hello 帳戶密碼，您會想 tootest。


## <a name="starting-applications"></a>啟動應用程式

數種類型的應用程式可以出現在 hello 存取面板。

### <a name="office-365-applications"></a>Office 365 應用程式

如果您的組織使用 Office 365 應用程式，您的授權加以 hello Office 365 應用程式會出現在存取面板上。

當您按一下 Office 365 應用程式的應用程式磚時，您會重新導向的 toohello 應用程式和自動登入。

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>已設定同盟 SSO 的 Microsoft 及第三方應用程式

您的系統管理員可以新增 hello Active Directory 區段的 hello Azure 入口網站中應用程式與 hello SSO 模式設定太**Azure AD 單一登入**。 如果您的系統管理員已明確授與存取 toohello 應用程式，您只可以看到這些應用程式。

當您按一下其中一個應用程式磚時，您會重新導向，並自動登入 toohello 應用程式。

### <a name="password-based-sso-without-identity-provisioning"></a>不含身分識別佈建的密碼 SSO

您的系統管理員可以新增 hello Active Directory 區段的 hello Azure 入口網站中應用程式與 hello SSO 模式設定太**密碼型單一登入**。 Hello 目錄中的所有使用者都可以都看到已設定在此模式中的所有應用程式。

hello 第一次，當您按一下其中一個應用程式磚，會提示的 tooinstall hello 密碼 SSO 外掛程式，以用於 Internet Explorer 或 Chrome。 hello 安裝可能會要求您 toorestart 網頁瀏覽器。 當您傳回 toohello 存取面板，並按一下 hello 應用程式磚同樣地，系統會提示您輸入使用者名稱和密碼 hello 應用程式。 當您輸入使用者名稱和密碼時，這些認證會安全地儲存，並在 Azure AD 中連結 tooyour 帳戶。

hello 您按一下 hello 應用程式磚，您會自動登入 toohello 應用程式的下一次。  
您尚未 tooenter 認證一次，或安裝密碼 SSO 外掛程式 hello。

如果您的認證已變更 hello 目標協力廠商應用程式中，您也必須更新您的認證儲存在 Azure AD 中。 

**tooupdate 認證：**

1. 選取 hello hello 應用程式磚上的圖示。
2. 選取**更新認證**tooreenter hello 使用者名稱和密碼 hello 應用程式。


### <a name="password-based-sso-with-identity-provisioning"></a>含身分識別佈建的密碼 SSO

您的系統管理員可以新增應用程式在 hello **Active Directory** hello Azure 入口網站與 hello SSO 模式部分設定得**密碼型單一登入**，以及佈建身分識別。

hello 第一次，當您按一下其中一個應用程式的應用程式磚，會提示的 tooinstall hello**密碼 SSO 外掛程式，以用於 Internet Explorer 或 Chrome**。 hello 安裝可能會要求您 toorestart 網頁瀏覽器。  
當您傳回 toohello 存取面板，並按一下 hello 應用程式磚同樣地，您會自動登入 toohello 應用程式。

某些應用程式可能需要您 toochange 上 hello 首次登入的密碼。 如果您的認證已變更 hello 目標協力廠商應用程式中，您也必須更新儲存在 Azure AD 中的 hello 認證。 

**tooupdate 認證：**

1. 選取 hello hello 應用程式磚上的圖示。
2. 選取**更新認證**tooreenter hello 使用者名稱和密碼 hello 應用程式。


### <a name="application-with-existing-sso-solutions"></a>含現有 SSO 解決方案的應用程式

tooconfigure SSO 應用程式，hello Azure 入口網站會提供第三個選項，呼叫**現有單一登入**。 此選項可讓您的系統管理員 toocreate 連結 tooan 應用程式，並將它放在 hello 選使用者的存取面板上。

例如，如果應用程式使用 AD FS 2.0 設定的 tooauthenticate 使用者，您的系統管理員可以使用 hello**現有單一登入**選項 toocreate 連結 tooit hello 存取面板上。 當您存取 hello 連結時，您會透過 AD FS 2.0 或提供的任何現有的 SSO 解決方案 hello 應用程式進行驗證。


## <a name="next-steps"></a>後續步驟

- toosee 相關的 tooapplication 管理的所有主題的清單，請參閱 「 hello [Azure Active Directory 中的應用程式管理的文件索引](active-directory-apps-index.md)。
 
- toolearn 如何 toointegrate SaaS 應用程式至 Azure AD，請參閱 hello[如何教學課程清單 toointegrate SaaS 應用程式](active-directory-saas-tutorial-list.md)。
 
- toolearn 進一步了解使用 Azure AD 中管理應用程式，請參閱 「 hello[簡介 toosingle 登入和管理應用程式存取權與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。
 
- toolearn 進一步了解使用者佈建，請參閱[自動化使用者佈建和解除佈建 tooSaaS 應用程式](active-directory-saas-app-provisioning.md)。

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
