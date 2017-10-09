---
title: "教學課程：Azure Active Directory 與 ScaleX Enterprise 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ScaleX 企業之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a>教學課程：Azure Active Directory 與 ScaleX Enterprise 整合

在此教學課程中，您學會如何 toointegrate ScaleX 企業與 Azure Active Directory (Azure AD)。

使用 Azure AD 整合 ScaleX Enterprise 可以提供下列優點的 hello:

- 您可以控制存取 tooScaleX Enterprise 的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooScaleX （單一登入） 的企業使用其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。 什麼是搭配 [Azure Active Directory](active-directory-appssoaccess-whatis.md) 的應用程式存取和單一登入？

## <a name="prerequisites"></a>必要條件

tooconfigure ScaleX 企業與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 ScaleX Enterprise 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 ScaleX Enterprise
2. 設定並測試 Azure AD 單一登入

## <a name="adding-scalex-enterprise-from-hello-gallery"></a>從 hello 圖庫加入 ScaleX Enterprise
tooconfigure hello 整合 ScaleX 企業 tooAzure AD 中的，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd ScaleX 企業。

**tooadd ScaleX 企業 hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**ScaleX 企業**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. 在 hello 結果 窗格中，選取  **ScaleX 企業**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 ScaleX Enterprise 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow ScaleX 企業中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello ScaleX 企業中的相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** ScaleX 企業中。

tooconfigure 及 ScaleX 企業與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 ScaleX 企業](#creating-a-scalex-enterprise-test-user)** -toohave 許 Simon ScaleX Enterprise 是連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 ScaleX 企業應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入使用 ScaleX Enterprise，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **ScaleX 企業**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. 在 hello **ScaleX 企業網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    a. 在 hello**識別碼**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://platform.rescale.com/saml2/<company id>/`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://platform.rescale.com/saml2/<company id>/acs/`

4. 請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    在 hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://platform.rescale.com/saml2/<company id>/sso/`
     
    > [!NOTE] 
    > 這些不是 hello 實際值。 更新這些值以 hello 實際的識別項 」、 「 回覆 URL 或 「 登入 URL。 請連絡[ScaleX 企業用戶端支援小組](http://info.rescale.com/contact_sales)tooget 這些值。 

5. ScaleX 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 toomodify 自訂屬性對應 tooyour SAML token 屬性設定。 按一下**檢視和編輯所有其他使用者屬性**核取方塊 tooopen hello 自訂屬性的設定。

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    a. 以滑鼠右鍵按一下 hello 屬性**名稱**並按一下 [刪除]。

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    b. 按一下**emailaddress**屬性 tooopen hello 編輯屬性 視窗。 變更其值從**user.mail**太**user.userprincipalname**按一下 [確定]。

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. 在 hello **ScaleX 企業設定**區段中，按一下**設定 ScaleX 企業**tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼**和**SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. tooconfigure 單一登入上**ScaleX 企業**側邊，以系統管理員身分登入 toohello ScaleX Enterprise 公司網站。

9. 右按一下上方的 hello hello 功能表，然後選取**Contoso 管理**。

    > [!NOTE] 
    > Contoso 只是一個範例。 這應該是您實際的公司名稱。 

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. 選取**整合**hello 最上層功能表，然後選取從**單一登入**。

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. 完成 hello 表單，如下所示：

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    a. 選取 [建立可驗證 SSO 的任何使用者]。

    b. **服務提供者 saml**: hello 值貼上***urn: oasis： 名稱： tc: SAML:2.0:nameid-格式： 持續性***

    c. **ACS 的回應中的身分識別提供者電子郵件欄位名稱**: hello 值貼上`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    d. **身分識別提供者 EntityDescriptor 實體識別碼：**貼上 hello **SAML 實體識別碼**從 hello Azure 入口網站複製的值。

    e. **身分識別提供者 SingleSignOnService URL:**貼上 hello **SAML 單一登入服務 URL**從 hello Azure 入口網站。

    f. **身分識別提供者公開 X509 憑證：**從 記事本 和 貼上此方塊中的 hello 內容中的 hello Azure 下載開啟 hello X509 憑證。 請確認有無分行符號 hello hello 憑證內容的中間。
    
    g. 請檢查下列核取方塊的 hello:**已啟用、 加密 NameID 和符號 AuthnRequests。**

    h. 按一下**更新 SSO 設定**toosave hello 設定。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-scalex-enterprise-test-user"></a>建立 ScaleX Enterprise 測試使用者

tooenable Azure AD 使用者 toolog 中 tooScaleX 企業，必須將他們佈建 tooScaleX 企業中。 在 ScaleX 企業的 hello 案例中，佈建是自動的工作而不需要任何手動步驟。 將在 hello ScaleX 端上自動佈建任何使用者都可以成功驗證的登入認證。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與使用者存取 tooScaleX 企業啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooScaleX 企業中，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**ScaleX 企業**。

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。

### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

按一下的 hello ScaleX 企業磚 hello 存取面板中就會自動登入 tooyour ScaleX 企業應用程式。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](https://msdn.microsoft.com/library/dn308586)。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

