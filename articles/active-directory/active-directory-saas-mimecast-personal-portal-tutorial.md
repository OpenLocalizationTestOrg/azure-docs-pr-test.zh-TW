---
title: "教學課程：Azure Active Directory 與 Mimecast Personal Portal 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Mimecast 個人入口網站之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a>教學課程：Azure Active Directory 與 Mimecast Personal Portal 整合

在此教學課程中，您學會如何 toointegrate Mimecast 個人入口網站與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Mimecast 個人入口網站可以提供下列優點 hello:

- 您可以控制存取 tooMimecast 個人入口網站的 Azure AD 中
- 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooMimecast 個人入口網站 （單一登入）
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 Mimecast 個人入口網站的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Mimecast Personal Portal 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Mimecast 個人入口網站
2. 設定並測試 Azure AD 單一登入

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a>從 hello 圖庫加入 Mimecast 個人入口網站
tooconfigure hello 整合 Mimecast 個人入口網站至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Mimecast 個人入口網站。

**tooadd Mimecast 個人入口網站從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Mimecast 個人入口網站**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. 在 hello 結果 窗格中，選取  **Mimecast 個人入口網站**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Mimecast Personal Portal 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Mimecast 個人入口網站中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Mimecast 個人入口網站中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

在 Mimecast 個人入口網站，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入 Mimecast 個人入口網站，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Mimecast 個人入口網站的測試使用者](#creating-a-mimecast-personal-portal-test-user)** -toohave 許 Simon Mimecast 個人入口網站，連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Mimecast 個人入口網站應用程式中。

**tooconfigure Azure AD 單一登入 Mimecast 個人入口網站，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Mimecast 個人入口網站**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. 在 hello **Mimecast 個人入口網站的網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello: 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[Mimecast 個人入口網站用戶端支援小組](https://www.mimecast.com/customer-success/technical-support/)tooget 這些值。 
 


4. 在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. 在 hello **Mimecast 個人入口網站組態**區段中，按一下**設定 Mimecast 個人入口網站**tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. 在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Mimecast Personal Portal 公司網站。

8. 跳過**服務\>應用程式**。
   
    ![應用程式](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "應用程式")

9. 按一下 [驗證設定檔] 。
   
    ![驗證設定檔](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "驗證設定檔")

10. 按一下 [新驗證設定檔] 。
   
    ![新驗證設定檔](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "新驗證設定檔")

11. 在 hello**驗證設定檔**區段中，執行下列步驟的 hello:
   
    ![驗證設定檔](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "驗證設定檔")
   
    a. 在 hello**描述**文字方塊中，輸入您的組態名稱。
   
    b. 選取 [強制執行 Mimecast Personal Portal 的 SAML 驗證] 。
   
    c. 在 [提供者] 中選取 [Azure Active Directory]。
   
    d. 在**簽發者 URL**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。
   
    e. 在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。
   
    f. 在**登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。

    g. 開啟您**base-64**編碼從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中的憑證，然後將它貼入 toohello**身分識別提供者憑證 （中繼資料）**文字方塊。

    h. 選取 [允許單一登入] 。
   
    i. 按一下 [儲存] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a>建立 Mimecast Personal Portal 測試使用者

在訂單 tooenable Azure AD 使用者 toolog 入 Mimecast 個人入口網站，他們必須佈建到 Mimecast 個人入口網站。 在 Mimecast 個人入口網站的 hello 案例中，佈建須手動進行。

您可以建立使用者之前，您會需要 tooregister 網域。

**tooconfigure 使用者佈建，執行下列步驟的 hello:**

1. 登入 tooyour **Mimecast 個人入口網站**以系統管理員身分。

2. 跳過**目錄\>內部**。
   
    ![目錄](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "目錄")

3. 按一下 [註冊新網域] 。
   
    ![註冊新網域](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "註冊新網域")

4. 在您建立好新網域之後，，按一下 [新位址] 。
   
    ![新位址](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "新位址")

5. 在 hello 新位址 對話方塊中，執行下列步驟的有效 azure 的 hello 想 tooprovision AD 帳戶：
   
    ![儲存](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "儲存")
   
    a. 在 hello**電子郵件地址**文字方塊中，輸入**電子郵件地址**的 hello 使用者 **BrittaSimon@contoso.com** 。
    
    b. 在 hello**全域名稱**文字方塊中，型別 hello **username**做為**BrittaSimon**。

    c. 在 hello**密碼**，和**確認密碼**等文字方塊中，型別 hello**密碼**hello 使用者。
   
    b. 按一下 [儲存] 。

>[!NOTE]
>您可以使用任何其他 Mimecast 個人入口網站使用者帳戶建立工具或 Api Mimecast 個人入口網站 tooprovision Azure AD 使用者帳戶所提供。 

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooMimecast 個人入口網站啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooMimecast 個人入口網站，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Mimecast 個人入口網站**。

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入
在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Mimecast 個人入口網站的並排顯示 hello 存取面板中時，您應該取得 tooyour 自動登入 Mimecast 個人入口網站應用程式。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

