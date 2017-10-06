---
title: "教學課程：Azure Active Directory 與 Google Apps 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Google 應用程式之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>教學課程：Azure Active Directory 與 Google Apps 整合

在此教學課程中，您學會如何 toointegrate Google 應用程式與 Azure Active Directory (Azure AD)。

整合 Azure AD 與 Google Apps 可以提供下列優點 hello:

- 您可以控制存取 tooGoogle 應用程式的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooGoogle （單一登入） 的應用程式使用其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 與 Azure AD SaaS 應用程式整合的詳細資訊，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Google Apps 的整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Google Apps 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="video-tutorial"></a>影片教學課程
如何 tooEnable 單一登入 tooGoogle 在 2 分鐘內的應用程式：

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>常見問題集
1. **問：Chromebook 及其他 Chrome 裝置是否與 Azure AD 單一登入相容？**
   
    答: [是]，使用者將無法使用其 Azure AD 認證其 Chromebook 裝置到 toosign。 若要了解為何使用者可能收到兩次提供認證的提示，請參閱此 [Google Apps 支援文章](https://support.google.com/chrome/a/answer/6060880) 。

2. **問： 如果我啟用單一登入，將使用者要能夠 toouse 到任何 Google 產品，例如 Google 教室、 GMail、 google 雲端硬碟、 YouTube，等其 Azure AD 認證 toosign 嗎？**
   
    答: [是]，取決於[的 Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583)您選擇 tooenable 或為您的組織停用。

3. **問：我是否可以只為一部分 Google Apps 使用者啟用單一登入？**
   
    答： 否，立即開啟在 [單一登入需要所有您 Google Apps 使用者 tooauthenticate 使用他們的 Azure AD 認證。 Google Apps 不支援多重身分識別提供者，因為您的 Google Apps 環境的 hello 身分識別提供者可以是 Azure AD 或 Google-但不是能同時執行 hello 相同的時間。

4. **問： 如果使用者透過 Windows 登入，會自動驗證 tooGoogle 應用程式而不取得提示輸入密碼嗎？**
   
    答：有兩個選項可允許這樣的情況。 第一個是，使用者可以透過 [Azure Active Directory Join](active-directory-azureadjoin-overview.md)登入 Windows 10 裝置。 或者，使用者無法登入加入網域的 tooan 內部單一登入 tooAzure AD 透過已啟用的 Active Directory 的 Windows 裝置[Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md)部署。 這兩個選項需要您遵循教學課程 tooenable 單一登入 Azure AD 之間的 hello tooperform hello 步驟和 Google Apps。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Google Apps
2. 設定並測試 Azure AD 單一登入

## <a name="adding-google-apps-from-hello-gallery"></a>從 hello 圖庫加入 Google Apps
tooconfigure hello 整合 Google 應用程式到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Google Apps。

**tooadd Google Apps hello 圖庫中，從執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Google Apps**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. 在 [hello [結果] 窗格中，選取 [ **Google Apps**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Google Apps 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Google Apps 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Google Apps 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Google Apps 中。

tooconfigure 及 Azure AD 單一登入與 Google Apps 的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Google Apps 的測試使用者](#creating-a-google-apps-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Google Apps 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Google Apps 的應用程式中。

**tooconfigure Azure AD 單一登入與 Google Apps，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Google Apps**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. 在 [hello **Google Apps 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > 這不是真實的值。 更新 hello 值與 hello 實際登入 URL。 請連絡 hello [Google 支援小組](https://www.google.com/contact/)。
 
4. 在 [hello **SAML 簽章憑證**區段中，按一下**憑證**，然後儲存您的電腦上的 [hello 憑證。

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. 在 [hello **Google 應用程式組態**區段中，按一下**設定 Google Apps** tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 單一登入服務 URL 和變更密碼 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. 在您的瀏覽器中開啟新索引標籤，並登入 hello [Google 應用程式系統管理員主控台](http://admin.google.com/)使用您的系統管理員帳戶。

8. 按一下 [安全性] 。 如果您沒有看到 hello 連結，它可能會隱藏在 hello**其他控制項**功能表底部 hello 囉 」 畫面。
   
    ![按一下 [安全性]。][10]

9. 在 [hello**安全性**頁面上，按一下**設定單一登入 (SSO)。**
   
    ![按一下 [SSO]。][11]

10. 執行下列組態變更的 hello:
   
    ![設定 SSO][12]
   
    a. 選取 [使用第三方識別提供者來設定 SSO]。

    b. 在**登入頁面 URL** Google Apps] 欄位中，貼上的 hello 值**單一登入服務 URL**，從 Azure 入口網站複製的。

    c. 在 [hello**登出頁面 URL** Google Apps] 欄位中，貼上的 hello 值**登出 URL**，從 Azure 入口網站複製的。 

    d. 在 [hello**變更密碼 URL** Google Apps] 欄位中，貼上的 hello 值**變更密碼 URL**，從 Azure 入口網站複製的。 

    e. 在 Google Apps，hello**驗證憑證**，hello 將憑證上傳您從 Azure 入口網站下載。

    f. 按一下 [儲存變更] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-google-apps-test-user"></a>建立 Google Apps 測試使用者

hello 本節目標在於 toocreate 呼叫許 Simon Google 應用程式軟體中的使用者。 Google Apps 支援預設啟用的自動佈建。 在這一節沒有您需要進行的動作。 如果使用者不存在於 Google 應用程式軟體，當您嘗試 tooaccess Google 應用程式軟體時，會建立一個新。

>[!NOTE] 
>若要手動 toocreate 使用者，請連絡 hello [Google 支援小組](https://www.google.com/contact/)。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用 Azure 單一登入許 Simon toouse tooGoogle 應用程式授與存取權。

![指派使用者][200] 

**tooassign 許 Simon tooGoogle 應用程式，請執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Google Apps**。

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在此區段中，您的單一登入設定，開啟 hello 存取面板 tootest [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md)，然後登入 hello 測試帳戶，然後按一下**Google Apps**磚 hello 存取面板中。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定使用者佈建](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png