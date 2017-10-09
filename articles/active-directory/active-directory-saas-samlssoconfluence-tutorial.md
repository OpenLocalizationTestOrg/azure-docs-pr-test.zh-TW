---
title: "教學課程：Azure Active Directory 與 SAML SSO for Confluence by resolution GmbH 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與解析 GmbH 機器人學的 SAML SSO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a>教學課程：Azure Active Directory 與 SAML SSO for Confluence by resolution GmbH 整合

在此教學課程中，您學會如何解析與 Azure Active Directory (Azure AD) GmbH toointegrate 機器人學的 SAML SSO。

解析 GmbH 與 Azure AD 整合的機器人學 SAML SSO 可以提供下列優點 hello:

- 您可以控制存取 tooSAML 機器人學的 SSO 解析 GmbH Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooSAML 機器人學的 SSO 的解析度 GmbH （單一登入），其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 解析 GmbH 機器人學的 SAML sso 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- SAML SSO for Confluence by resolution GmbH 單一登入已啟用的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 解析 GmbH 加入機器人學的 SAML SSO，從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a>解析 GmbH 加入機器人學的 SAML SSO，從 hello 組件庫

tooconfigure hello 整合機器人學的 SAML SSO 解析 GmbH 到 Azure AD，您需要 tooadd SAML SSO 機器人學解析 GmbH hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**解析從 hello 圖庫 GmbH tooadd 機器人學的 SAML SSO 執行 hello 下列步驟：**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**解析 GmbH 機器人學的 SAML SSO**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. 在 hello 結果 窗格中，選取 **解析 GmbH 機器人學的 SAML SSO**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAML SSO for Confluence by resolution GmbH 設定及測試 Azure AD 單一登入。

針對單一登入 toowork，Azure AD 需要 tooknow 機器人學的 SAML sso GmbH 是 tooa 使用者在 Azure AD 中解析何種 hello 對等項目的使用者。 換句話說，Azure AD 使用者與 hello 相關的使用者機器人學的 SAML SSO 中解析之間的連結關聯性 GmbH 需要 toobe 建立。

解析 GmbH 機器人學的 SAML SSO 中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入與 SAML SSO 機器人學解析 GmbH，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立機器人學解析 GmbH 測試使用者的 SAML SSO](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave 解析是連結的 toohello Azure AD 使用者表示法的 GmbH 許 Simon 機器人學的 SAML SSO 中的對應。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並解析 GmbH 應用程式設定單一登入的機器人學您 SAML SSO 中。

**tooconfigure Azure AD 單一登入使用機器人學的 SAML SSO 解析 GmbH，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello**解析 GmbH 機器人學的 SAML SSO**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. 在 hello**機器人學解析 GmbH 網域和 Url 的 SAML SSO**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    a. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/samlsso`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/samlsso`

4. 按一下 [顯示進階 URL 設定]。 如果您想 tooconfigure hello 應用程式中的**SP**初始模式：

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。 請連絡[機器人學解析 GmbH 用戶端的 SAML SSO 支援小組](https://www.resolution.de/go/support)tooget 這些值。 

5. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. 在不同的網頁瀏覽器視窗中，登入 tooyour**機器人學解析 GmbH 管理員入口網站的 SAML SSO**身為系統管理員。

8. 將滑鼠停留在齒輪，然後按一下 hello**附加元件**。
    
    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. 您已重新導向的 tooAdministrator 存取頁面。 輸入 hello 密碼，然後按一下**確認** 按鈕。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. 在 [ATLASSIAN MARKETPLACE] 索引標籤上，按一下 [尋找新的附加元件]。 

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. 搜尋**SAML 單一登入 (SSO) 針對機器人學**按一下**安裝**按鈕 tooinstall hello 新 SAML 外掛程式。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. hello 外掛程式安裝將會啟動。 按一下 [關閉] 。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. 按一下 [管理] 。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. 按一下**設定**tooconfigure hello 新的外掛程式。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. 您也可以在 [使用者與安全性] 索引標籤底下找到這個新的外掛程式。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. 在**設定 SAML 單一登入外掛程式**頁面上，按一下**新增其他身分識別提供者**按鈕 tooconfigure hello 設定身分識別提供者。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. 在這個頁面上執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    a. 新增**名稱**的 hello 身分識別提供者 （例如 Azure AD）。
    
    b. 新增**描述**的 hello 身分識別提供者 （例如 Azure AD）。

    c. 按一下**XML**和選取 hello**中繼資料**您從 Azure 入口網站下載的檔案。

    d. 按一下 [載入] 按鈕。

    e. 它會讀取 hello IdP 中繼資料，並於其中填入 hello hello 螢幕擷取畫面中反白顯示的欄位。   
18. 按一下**儲存設定**按鈕 toosave hello 設定。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a>建立 SAML SSO for Confluence by resolution GmbH 測試使用者

tooenable Azure AD 使用者 toolog 中解析 GmbH tooSAML 機器人學的 SSO，它們必須佈建到機器人學的 SAML SSO 解析 GmbH。  
在 SAML SSO for Confluence by resolution GmbH 中，佈建是手動工作。

**tooprovision 使用者帳戶，執行下列步驟的 hello:**

1. 登入 tooyour SAML SSO 機器人學解析 GmbH 公司網站的系統管理員身分。

2. 將滑鼠停留在齒輪，然後按一下 hello**使用者管理**。

    ![新增員工](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. 在 使用者 區段底下，按一下 新增使用者 索引標籤。在 hello **加入使用者**對話方塊頁面上，執行下列步驟的 hello:

    ![新增員工](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    a. 在 hello **Username**文字方塊中，使用者像許 Simon 的型別 hello 電子郵件。

    b. 在 hello**全名**文字方塊中，類型許 Simon 類似使用者的 hello 完整名稱。

    c. 在 hello**電子郵件**文字方塊中，輸入 hello 電子郵件地址的使用者喜歡Brittasimon@contoso.com。

    d. 在 [hello**密碼**許 Simon 的型別 hello 密碼] 文字方塊中。

    e. 按一下**確認密碼**重新輸入 hello 密碼。
    
    f. 按一下 [新增] 按鈕。    

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooSAML 解析 GmbH 機器人學的 SSO。

![指派使用者][200] 

**tooassign 許 Simon tooSAML 機器人學的 SSO 解析 GmbH，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**解析 GmbH 機器人學的 SAML SSO**。

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello 機器人學的 SAML SSO 所解析 GmbH 磚 hello 存取面板中時，您應該取得機器人學自動登入 tooyour SAML SSO 解析 GmbH 應用程式。
如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

