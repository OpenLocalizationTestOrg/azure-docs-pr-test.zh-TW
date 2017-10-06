---
title: "教學課程：Azure Active Directory 與 Menlo Security 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Menlo 安全性之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a>教學課程：Azure Active Directory 與 Menlo Security 整合

在此教學課程中，您學會如何 toointegrate Menlo 安全性與 Azure Active Directory (Azure AD)。

使用 Azure AD 整合 Menlo 安全性可以提供下列優點的 hello:

- 您可以在 Azure AD 中擁有存取 tooMenlo 安全性控制
- 您可以啟用您的使用者 tooautomatically get 登入 tooMenlo （單一登入） 的安全性與他們的 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Menlo 安全性與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Menlo Security 單一登入功能的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 組件庫中加入 Menlo 安全性
2. 設定並測試 Azure AD 單一登入

## <a name="adding-menlo-security-from-hello-gallery"></a>從 hello 組件庫中加入 Menlo 安全性
tooconfigure hello Menlo 安全性整合至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Menlo 安全性。

**tooadd Menlo 安全性從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Menlo 安全性**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. 在 hello 結果 窗格中，選取  **Menlo 安全性**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Menlo Security 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Menlo 安全性是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Menlo 安全性相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Menlo 安全性。

tooconfigure 和測試 Azure AD 單一登入具有 Menlo 安全性，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Menlo 安全性](#creating-a-menlo-security-test-user)** -toohave 許 Simon Menlo 安全性連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Menlo 安全性應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入具有 Menlo 安全性，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Menlo 安全性**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. 在 hello **Menlo 安全性網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.menlosecurity.com/account/login`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`

    > [!NOTE] 
    > 這些值不是真正的 hello。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[Menlo 安全性用戶端支援小組](https://www.menlosecurity.com/menlo-contact)tooget 這些值。 
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. 在 hello **Menlo 安全性組態**區段中，按一下**設定 Menlo 安全性**tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼**，和**SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. tooconfigure 單一登入上**Menlo 安全性**，登入 toohello **Menlo 安全性**身為系統管理員的網站。

8. 在下**設定**太移**驗證**並執行下列動作：
    
    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    a. 刻度 hello 核取方塊**使用 SAML 啟用使用者驗證**。

    b. 選取**允許外部存取**太**是**。

    c. 在 [SAML 提供者] 下選取 [Azure Active Directory]。

    d. **SAML 2.0 端點**： 貼上 hello **SAML 單一登入服務 URL**您從 Azure 入口網站複製的。

    e. **服務識別元 （簽發者）** ： 貼上 hello **SAML 實體識別碼**您從 Azure 入口網站複製的。

    f. **X.509 憑證**： 開啟 hello**憑證 (Base64)**從 [記事本] 中的 hello Azure 入口網站下載，並將它貼入此方塊中。

    g. 按一下**儲存**toosave hello 設定。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-menlo-security-test-user"></a>建立 Menlo Security 測試使用者
 
在本節中，您要在 Menlo Security 中建立名為 Britta Simon 的使用者。 使用[Menlo 安全性用戶端支援小組](https://www.menlosecurity.com/menlo-contact)tooadd hello hello Menlo 安全性平台的使用者。 您必須先建立和啟動使用者，然後才能使用單一登入。 

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooMenlo 安全性。

![指派使用者][200] 

**tooassign 許 Simon tooMenlo 安全性，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Menlo 安全性**。

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會測試您的 Azure AD 單一登入設定。

開啟瀏覽器視窗中 「 InPrivate"或"Incognito 」 模式 tootrigger 新的驗證。  在 Internet Explorer 中，使用 Ctrl+Shift+P。  在 Chrome 中，使用 Ctrl+Shift+N。  在 hello 私用瀏覽視窗中，瀏覽 tooa 受保護的資源並執行 Azure AD 登入。  成功登入，系統會採用的 toohello 要求站台隔離工作階段中。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

