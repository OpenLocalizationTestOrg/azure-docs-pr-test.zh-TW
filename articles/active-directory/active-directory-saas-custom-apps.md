---
title: "應用程式的 Azure AD 的 SSO aaaConfigure |Microsoft 文件"
description: "了解如何 tooself 服務連接的應用程式 tooAzure Active Directory 使用 SAML 和密碼登入"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>設定單一登入 tooapplications 不在 hello Azure Active Directory 應用程式庫
這篇文章是關於此功能可讓系統管理員 tooconfigure 單一登入 tooapplications hello Azure Active Directory 應用程式庫中沒有*無須撰寫程式碼*。 此功能已在 2015 年 11 月 18 日的技術預覽中發行，並且包含在 [Azure Active Directory Premium](active-directory-editions.md)中。 如果您改為需要開發人員指引 toointegrate 自訂應用程式與 Azure AD 透過程式碼，請參閱[Azure AD 的驗證案例](active-directory-authentication-scenarios.md)。

hello Azure Active Directory 應用程式庫提供的清單，稱為 toosupport 的單一登入與 Azure Active Directory，一種形式的應用程式中所述[本文](active-directory-appssoaccess-whatis.md)。 一旦 （做為 IT 專家或系統整合者組織中） 找到 hello 應用程式想 tooconnect，您可以開始在 Azure 管理入口網站 tooenable 單一登入的 hello 呈現的後續 hello 逐步指示。

具有 [Azure Active Directory Premium](active-directory-editions.md) 授權的客戶也會取得以下額外功能：

* 任何支援 SAML 2.0 身分識別提供者的應用程式皆可進行自助式整合 (SP 起始或 IdP 起始)
* Web 應用程式可在使用 [密碼型 SSO](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* 進行使用者佈建使用 hello SCIM 通訊協定的應用程式的自助服務連線 ([此處所述](active-directory-scim-provisioning.md))
* 能力 tooadd 連結 tooany 應用程式在 hello [Office 365 應用程式啟動器](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/)或 hello [Azure AD 存取面板](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

這可包括 SaaS 應用程式使用，但尚未經過初始 toohello Azure AD 應用程式庫，不僅 tooservers 您控制，在 hello 雲端或內部部署組織的第三方 web 應用程式。

這些功能 (也稱為「應用程式整合範本」 )，為支援 SAML、SCIM 或表單型驗證的應用程式提供標準型連接點，包括有彈性的選項和與廣泛應用程式相容性的設定。 

## <a name="adding-an-unlisted-application"></a>新增未列出的應用程式
tooconnect 應用程式使用的應用程式整合範本中，請登入 hello Azure 管理入口網站使用您的 Azure Active Directory 系統管理員帳戶，並瀏覽 toohello **Active Directory > [目錄] > 應用程式**區段中，選取**新增**，然後**從 hello 組件庫新增應用程式**。 

![][1]

在 hello 應用程式庫，您可以加入未列出應用程式使用 hello**自訂**類別 hello 左側，或藉由選取 hello**新增未列出的應用程式**hello 搜尋中所顯示的連結結果，如果您想要的應用程式找不到。 輸入您的應用程式的名稱之後, 您可以設定 hello 單一登入選項和行為。 

**快速提示**： 最佳作法是使用 hello 搜尋函式 toocheck toosee 如果 hello 應用程式庫中的 hello 應用程式已經存在。 如果找到 hello 應用程式，其描述會在提及 「 單一登入 」，然後 hello 應用程式已經支援同盟單一登入。 

![][2]

這種方式來新增應用程式提供非常相似的經驗 toohello 適用於預先整合的應用程式的其中一個。 選取 toostart**設定單一登入**。 hello 下一個畫面會顯示 hello 下列三個選項的設定單一登入，hello 下列各節所述。

![][3]

## <a name="azure-ad-single-sign-on"></a>Azure AD 單一登入
選取此選項 tooconfigure SAML 型 hello 應用程式驗證。 這需要 hello 應用程式支援 SAML 2.0 中，以及您應該收集資訊如何 toouse hello SAML 功能 hello 應用程式，然後再繼續。 選取之後**下一步**，您將會提示的 tooenter 三個不同的 Url 對應 toohello hello 應用程式的 SAML 端點。 

![][4]

它們是：

* **登入 URL (SP 起始只)** – 其中 hello 使用者進入 toosign 中 toothis 應用程式。 如果 hello 應用程式設定 tooperform 服務提供者起始單一登入，然後當使用者巡覽 toothis URL、 hello 服務提供者會執行 hello 必要的重新導向 tooAzure AD tooauthenticate 和中的 hello 使用者登入。 如果已填入此欄位，Azure AD 會使用 Office 365 和 Azure AD 存取面板 hello 這個 URL toolaunch hello 應用程式。 如果這個欄位是 ommited，則 Azure AD 將會改為執行身分識別提供者-初始的登入 hello 應用程式啟動時從 Office 365、 Azure AD 存取面板 hello 或 hello Azure AD 單一登入 URL (copiable 從 hello 儀表板 索引標籤)。
* **簽發者 URL** -hello 簽發者 URL 應專門用於識別 hello 應用程式所設定的單一登入。 這是 Azure AD 會將回復 tooapplication 傳送 hello 與 hello 值**觀眾**hello SAML 權杖中和 hello 應用程式的參數是預期的 toovalidate 它。 這個值也會顯示為 hello**實體識別碼**hello 應用程式所提供的任何 SAML 中繼資料中。 請檢查 hello 應用程式的 SAML 文件內容的詳細資料是實體識別碼或適用對象值。 以下是如何 hello 觀眾 URL 會出現在 hello SAML 權杖傳回的 toohello 應用程式的範例：

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **回覆 URL** -hello 回覆 URL 是 hello 應用程式預期 tooreceive hello SAML 權杖中的位置。 這也是參考的 tooas hello**判斷提示取用者服務 (ACS) URL**。 查看 hello 應用程式的 SAML 權杖的回覆 URL 或 ACS URL 是什麼的詳細資訊的 SAML 文件。
  這些輸入之後，請按一下**下一步**tooproceed toohello 下一個畫面。 此畫面會提供哪些需求 toobe 上設定 hello 應用程式端 tooenable 它 tooaccept 來自 Azure AD SAML 權杖的相關資訊。 

![][5]

哪些值需要將 hello 應用程式而有所不同，因此請查看 hello 應用程式的 SAML 文件，如需詳細資訊。 hello**登入**和**登出**服務 URL 解析 toohello 相同的端點，為您的 Azure AD 執行個體中的 hello SAML 要求處理端點。 會顯示為 hello SAML 權杖的發出的 toohello 應用程式內的 hello 「 簽發者 」 的 hello 值為 hello 簽發者 URL。 

設定您的應用程式之後，按一下**下一步**按鈕，然後再 hello**完成**tooclose hello 對話方塊。 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>指派使用者和群組 tooyour SAML 應用程式
一旦您的應用程式已設定的 toouse Azure AD 做為 SAML 型身分識別提供者，它是就緒 tootest。 做為安全性控制項，Azure AD 不會發出可讓它們 toosign 放入 hello 應用程式除非被授予使用 Azure AD 存取權杖。 使用者可以直接獲得存取權，或透過其所屬的群組取得。 

tooassign 的使用者或群組 tooyour 應用程式，按一下 hello**指派使用者** 按鈕。 選取 hello 使用者或群組，您想 tooassign，，然後選取 [hello**指派**] 按鈕。 

![][6]

將使用者指派可讓 Azure AD tooissue hello 使用者，以及造成此應用程式 tooappear 磚 hello 使用者的存取權面板中的語彙基元。 如果 hello 使用者正在使用 Office 365，則應用程式磚也會出現在 hello Office 365 應用程式啟動程式。 

您可以上傳使用 hello hello 應用程式磚標誌**上傳標誌**按鈕 hello**設定**hello 應用程式 索引標籤。 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>自訂 hello hello SAML 權杖中發出的宣告
使用者驗證 toohello 應用程式時，Azure AD 就會唯一識別它們的 hello 使用者的相關中發出 SAML 權杖 toohello 應用程式，其中包含資訊 （或宣告）。 根據預設，這包括 hello 使用者的使用者名稱、 電子郵件地址、 名字和姓氏。 

您可以檢視或編輯 hello hello SAML 權杖 toohello 應用程式中傳送嗨宣告**屬性** 索引標籤。 

![][7]

有兩個可能的原因為何，您可能需要在 hello SAML 權杖中發出的 tooedit hello 宣告： 撰寫 •hello 應用程式 toorequire 不同組的宣告的 Uri 或宣告值 •Your 應用程式部署需要 hello 的方式NameIdentifier 宣告 toobe 以外的項目 hello 使用者名稱 （也稱為使用者主體名稱） 儲存在 Azure Active Directory。 

如需如何 tooadd] 與 [編輯宣告這些案例的資訊，請參閱這[上宣告的自訂文件：](active-directory-saml-claims-customization.md)。 

### <a name="testing-hello-saml-application"></a>測試 hello SAML 應用程式
一旦 hello SAML Url 和憑證已在 Azure AD 和 hello 應用程式中，使用者或群組已指派給 toohello 應用程式在 Azure 中，並 hello 宣告已檢閱並編輯如有必要，然後 hello 使用者是準備 toosign 到 hello應用程式。 

tootest，只需登入 hello https://myapps.microsoft.com toohello 應用程式中，指派給您的使用者帳戶在 Azure AD 存取面板，然後按一下關閉 hello 單一登入程序的 hello 應用程式 tookick hello 磚。 或者，您可以瀏覽直接 hello 應用程式和登入從該處 toohello 登入 URL。 

偵錯秘訣，請參閱此[有關的文章 toodebug SAML 型單一登入 tooapplications](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>密碼單一登入
選取此選項 tooconfigure[密碼型單一登入](active-directory-appssoaccess-whatis.md)web 應用程式具有 HTML 登入頁面。 密碼型 SSO，也會參照的 tooas vaulting 的密碼，可讓您 toomanage 使用者存取和密碼 tooweb 應用程式不支援識別同盟。 它也很有用的案例中的數個使用者需要 tooshare 單一帳戶，例如 tooyour 公司的社交媒體應用程式的帳戶。 

選取之後**下一步**，系統會提示的 tooenter hello hello 應用程式的網頁型登入頁面 URL。 請注意，這必須包括 hello 使用者名稱和密碼輸入的欄位的 hello 頁面。 輸入一次，Azure AD 會啟動處理序 tooparse hello 登入頁面使用者名稱輸入和密碼輸入。 如果 hello 程序不成功，然後它引導您完成安裝的瀏覽器延伸模組 （需要 Internet Explorer、 Chrome 或 Firefox） 可讓您 toomanually 擷取 hello 欄位的一個替代程序。

一旦擷取 hello 登入頁面，可能會指派使用者和群組，而且認證原則可以設定就像一般[密碼 SSO 應用程式](active-directory-appssoaccess-whatis.md)。

注意： 您可以上傳使用 hello hello 應用程式磚標誌**上傳標誌**按鈕 hello**設定**hello 應用程式 索引標籤。 

## <a name="existing-single-sign-on"></a>現有單一登入
選取此選項 tooadd 連結 tooan 應用程式 tooyour 組織的 Azure AD 存取面板或 Office 365 入口網站。 您可以使用這個 tooadd 連結 toocustom web 應用程式目前使用 Azure Active Directory Federation Services （或其他同盟服務），而不是 Azure AD 進行驗證。 或者，您可以加入深層連結 toospecific SharePoint 網頁或其他網頁，您只想 tooappear 使用者的存取面板上。 

選取之後**下一步**，您將無法以 hello 應用程式 toolink 提示的 tooenter hello URL。 完成後，使用者和群組可能會指派 toohello 應用程式，這會造成 hello 應用程式 tooappear hello [Office 365 應用程式啟動器](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/)或 hello [Azure AD 存取面板](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)這些使用者。

注意： 您可以上傳使用 hello hello 應用程式磚標誌**上傳標誌**按鈕 hello**設定**hello 應用程式 索引標籤。

## <a name="related-articles"></a>相關文章
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)
* [如何 tooCustomize 中發出的宣告 hello SAML 權杖 Pre-Integrated 應用程式](active-directory-saml-claims-customization.md)
* [SAML 型單一登入疑難排解](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
