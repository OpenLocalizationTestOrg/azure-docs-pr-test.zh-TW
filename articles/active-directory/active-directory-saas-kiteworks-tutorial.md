---
title: "教學課程：將 Azure Active Directory 與 Kiteworks 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Kiteworks 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a>教學課程：將 Azure Active Directory 與 Kiteworks 整合

在此教學課程中，您學會如何 toointegrate Kiteworks 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Kiteworks 可以提供下列優點 hello:

- 您可以控制存取 tooKiteworks Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooKiteworks （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Kiteworks 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Kiteworks 單一登入功能的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Kiteworks
2. 設定並測試 Azure AD 單一登入

## <a name="adding-kiteworks-from-hello-gallery"></a>從 hello 圖庫加入 Kiteworks
tooconfigure hello 整合 Kiteworks 到 Azure AD，您需要 tooadd Kiteworks hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Kiteworks 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Kiteworks**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. 在 hello 結果 窗格中，選取  **Kiteworks**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kiteworks 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Kiteworks 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Kiteworks 中相關的使用者之間的連結關聯性需要 toobe 建立。

Kiteworks 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Kiteworks 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Kiteworks](#creating-a-kiteworks-test-user)**  -toohave 許 Simon Kiteworks 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Kiteworks 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Kiteworks，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Kiteworks**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. 在 hello **Kiteworks 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.kiteworks.com`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[Kiteworks 用戶端支援小組](http://accellion.com/support)tooget 這些值。 
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. 在 hello **Kiteworks 組態**區段中，按一下**設定 Kiteworks** tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. 登入 tooyour Kiteworks 公司網站的系統管理員身分。

8. 在 hello hello 上方的工具列中按一下**設定**。
   
    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. 在 hello**驗證和授權**區段中，按一下**SSO 安裝**。 
   
    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. 在 hello SSO 安裝程式 頁面上，執行下列步驟的 hello:
   
    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    a. 選取 [透過 SSO 驗證]。

    b. 選取 [起始 AuthnRequest]。

    c. 在 hello **IDP 實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。 

    d. 在 hello**單一登入服務 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。

    e. 在 hello**單一登出服務 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。

    f. 開啟 [記事本]，複製 hello 內容，您所下載的憑證，然後將它貼到 hello **RSA 公開金鑰憑證**文字方塊。
 
    g. 按一下 [儲存] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-kiteworks-test-user"></a>建立 Kiteworks 測試使用者

hello 本節目標在於 toocreate Kiteworks 中呼叫許 Simon 的使用者。

Kiteworks 支援預設啟用的 Just-in-Time 佈建。 在這一節沒有您需要進行的動作項目。 如果尚未存在期間嘗試 tooaccess Kitewors，建立新的使用者。

>[!NOTE]
>若要手動 toocreate 使用者，您需要 toocontact hello [Kiteworks 支援小組](http://accellion.com/support)。
 

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooKiteworks 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooKiteworks，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Kiteworks**。

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。  

當您按一下的 hello Kiteworks 磚 hello 存取面板中時，您應該取得自動登入 tooyour Kiteworks 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

