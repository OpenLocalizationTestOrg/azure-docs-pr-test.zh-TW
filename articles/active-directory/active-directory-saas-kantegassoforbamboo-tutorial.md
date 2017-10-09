---
title: "教學課程：Azure Active Directory 與 Kantega SSO for Bamboo 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Bamboo 的 Kantega SSO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a>教學課程：Azure Active Directory 與 Kantega SSO for Bamboo 整合

在此教學課程中，您學會如何 toointegrate Bamboo 與 Azure Active Directory (Azure AD) 的 Kantega SSO。

與 Azure AD 整合 Bamboo 的 Kantega SSO 可以提供下列優點 hello:

- 您可以控制存取 tooKantega Bamboo 的 SSO 的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooKantega Bamboo （單一登入） 的 SSO 與他們的 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 Bamboo 的 Kantega SSO 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Kantega SSO for Bamboo 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Bamboo 的 Kantega SSO
2. 設定並測試 Azure AD 單一登入

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a>從 hello 圖庫加入 Bamboo 的 Kantega SSO
tooconfigure hello 整合 Bamboo 的 Kantega SSO 至 Azure AD，您需要 tooadd Kantega SSO Bamboo hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd hello 庫、 Bamboo 的 Kantega SSO 執行 hello 下列步驟：**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Bamboo 的 Kantega SSO**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. 在 hello 結果 窗格中，選取  **Bamboo 的 Kantega SSO**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kantega SSO for Bamboo 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Bamboo 的 Kantega SSO 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Bamboo 的 Kantega SSO 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

Bamboo 的 Kantega SSO 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入使用 Kantega SSO Bamboo，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Bamboo 測試使用者 Kantega SSO](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Bamboo 的 Kantega SSO 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的 Kantega SSO Bamboo 應用程式中。

**Azure AD 單一登入的 tooconfigure 竹 的 Kantega sso 執行 hello 下列步驟：**

1. 在 Azure 入口網站上 hello hello **Bamboo 的 Kantega SSO**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. 在**IDP**起始模式，在 hello **Bamboo 網域和 Url Kantega SSO**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    a. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. 在**SP**初始的模式中，核取**顯示進階的 URL 設定**並執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`
     
    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。 Bamboo 外掛程式將說明這一點在 hello 教學課程後面的 hello 組態期間，會收到這些值。

5. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. 在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Bamboo 內部部署伺服器上。

8. 將滑鼠停留在齒輪，然後按一下 hello**附加元件**。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. 在附加元件索引標籤區段下，按一下 [尋找新的附加元件]。 搜尋**Bamboo SAML & Kerberos 的 Kantega SSO**按一下**安裝**按鈕 tooinstall hello 新 SAML 外掛程式。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. hello 外掛程式安裝將會啟動。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. 一旦 hello 安裝已完成。 按一下 [關閉] 。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. 按一下 [管理] 。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. 按一下**設定**tooconfigure hello 新的外掛程式。  

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. 在 hello **SAML** > 一節。 選取**Azure Active Directory (Azure AD)**從 hello**新增身分識別提供者**下拉式清單。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. 選取 [基本] 作為訂用帳戶層級。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. 在 hello**應用程式屬性**區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    a. 複製 hello**應用程式識別碼 URI**值，並使用它作為**識別碼、 回覆 URL 和登入 URL**上 hello **Bamboo 網域和 Url Kantega SSO** Azure 入口網站中的區段。

    b. 按一下 [下一步] 。

17. 在 hello**中繼資料匯入**區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    a. 選取 [我的電腦上的中繼資料檔案]，上傳您從 Azure 入口網站下載的中繼資料檔案。

    b.這是另一個 C# 主控台應用程式。 按一下 [下一步] 。

18. 在 hello**名稱和 SSO 位置**區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    a. Hello 身分識別提供者的名稱新增在**身分識別提供者名稱**文字方塊中 （例如 Azure AD）。

    b. 按一下 [下一步] 。

19. 請確認 hello 簽章憑證，然後按一下**下一步**。    

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. 在 hello **Bamboo 使用者帳戶**區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    a. 選取**Bamboo 的內部目錄中建立使用者，視**，然後輸入 hello 適當 hello 群組的使用者名稱 (可以是多個否。 群組，以逗號分隔)。

    b.這是另一個 C# 主控台應用程式。 按一下 [下一步] 。

21. 按一下 [完成] 。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. 在 hello**已知的 Azure AD 網域**區段中，執行下列步驟：   

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    a. 選取**已知網域**hello 的 hello 頁面的左面板中。

    b. 輸入網域名稱在 hello**已知網域**文字方塊。

    c. 按一下 [儲存] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a>建立 Kantega SSO for Bamboo 測試使用者

tooenable Azure AD 使用者 toolog 中 tooBamboo，它們必須佈建到 Bamboo。 在 Kantega SSO for Bamboo 中，佈建是手動工作。

**tooprovision 使用者帳戶，執行下列步驟的 hello:**

1. 系統管理員身分登入 tooyour Bamboo 內部部署伺服器上。

2. 將滑鼠停留在齒輪，然後按一下 hello**使用者管理**。

    ![新增員工](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. 按一下 [使用者] 。 在 hello**新增使用者**區段中，執行下列步驟：

    ![新增員工](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    a. 在 hello **Username**文字方塊中，型別 hello 電子郵件的使用者要Brittasimon@contoso.com。
    
    b. 在 hello**密碼**文字方塊中，輸入 hello 密碼的使用者。

    c. 在 hello**確認密碼**文字方塊中，重新輸入 hello 密碼的使用者。
    
    d. 在 hello**全名**文字方塊中，例如許 Simon 的 hello 使用者類型完整名稱。
    
    e. 在 hello**電子郵件**文字方塊中，輸入 hello 電子郵件地址的使用者喜歡Brittasimon@contoso.com。
    
    f. 按一下 [儲存] 。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooKantega Bamboo 的 SSO。

![指派使用者][200] 

**tooassign 許 Simon tooKantega 竹 的 SSO 執行 hello 下列步驟：**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Bamboo 的 Kantega SSO**。

    ![設定單一登入](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Kantega SSO Bamboo 磚 hello 存取面板中時，您應該取得自動登入 tooyour Kantega SSO Bamboo 應用程式。
如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

