---
title: "教學課程：Azure Active Directory 與 Pingboard 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Pingboard 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>教學課程：Azure Active Directory 與 Pingboard 整合

在此教學課程中，您學會如何 toointegrate Pingboard 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Pingboard 可以提供下列優點 hello:

- 您可以控制存取 tooPingboard Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooPingboard （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Pingboard 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Pingboard 單一登入功能的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Pingboard
2. 設定並測試 Azure AD 單一登入

## <a name="adding-pingboard-from-hello-gallery"></a>從 hello 圖庫加入 Pingboard
tooconfigure hello 整合 Pingboard 到 Azure AD，您需要 tooadd Pingboard hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Pingboard 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Pingboard**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. 在 hello 結果 窗格中，選取  **Pingboard**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Pingboard 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Pingboard 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Pingboard 中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Pingboard 中。

tooconfigure 及 Pingboard 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Pingboard](#creating-a-pingboard-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Pingboard 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 Pingboard 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Pingboard，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站上 hello **Pingboard**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. 在 hello **Pingboard 網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    a. 在 hello**識別碼**文字方塊中，做為型別 hello 值：`http://<entity-id>.pingboard.com/sp`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<entity-id>.pingboard.com/auth/saml/consume`

    > [!NOTE] 
    > 請注意這些不是 hello 實際值。 您有 tooupdate hello 實際的識別項和回覆 url 的這些值。 這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。 請連絡[Pingboard 用戶端支援小組](https://support.pingboard.com/)tooget 這些值。 

4. 請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    a. 在 hello**登入 URL**文字方塊中，做為型別 hello 值：`http://<sub-domain>.pingboard.com/sign_in`
     
5. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. tooconfigure SSO Pingboard 端開啟新的瀏覽器視窗，並登入 tooyour Pingboard 帳戶。 您必須是 Pingboard admin tooset 設定單一登上。

8. 從 hello 上方的功能表選取**應用程式 > 整合**

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  在 hello**整合**頁面上，尋找 hello **"Azure Active Directory"**磚，然後按一下它。

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. 在 hello 強制回應之後按一下**「 設定 」**

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. 在 hello 遵循頁面上，您會發現 「 Azure SSO 整合會啟用。 」。 開啟 hello 下載中繼資料 XML 檔案中的內容 記事本 和 貼上 hello **IDP 中繼資料**。

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. 將驗證 hello 檔案，且現在會啟用單一登入的所有項目是否正確，

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-pingboard-test-user"></a>建立 Pingboard 測試使用者

在訂單 tooenable Azure AD 使用者 toolog Pingboard 成，它們必須佈建到 Pingboard。  
中的 Pingboard hello 案例中，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟 hello:**

1. 登入 tooyour Pingboard 公司網站的系統管理員身分。

2. 按一下 [目錄] 頁面上的 [新增員工] 按鈕。

    ![新增員工](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. 在 hello **"加入 Employee"**對話方塊頁面上，執行下列步驟的 hello。

    ![邀請人員](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    a. 在 hello**全名**文字方塊中，類型許 Simon 的 hello 完整名稱。

    b. 在 [hello**電子郵件**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。

    c. 在 hello**職稱**文字方塊中，類型許 Simon 的 hello 職稱。

    d. 在 hello**位置**下拉式清單中，選取 hello 許 Simon 位置。
    
    e. 按一下 [新增] 。   

4. 確認畫面會出現 tooconfirm hello 加入的使用者。
    
    ![確認](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooPingboard 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooPingboard，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Pingboard**。

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Pingboard 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Pingboard 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
