---
title: "教學課程：Azure Active Directory 與 Salesforce 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Salesforce 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>教學課程：Azure Active Directory 與 Salesforce 整合

在此教學課程中，您學會如何 toointegrate Salesforce 與 Azure Active Directory (Azure AD)。

Azure AD 與 Salesforce 整合為您提供下列優點 hello:

- 您可以控制存取 tooSalesforce Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooSalesforce （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Salesforce 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Salesforce 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Salesforce
2. 設定並測試 Azure AD 單一登入

## <a name="adding-salesforce-from-hello-gallery"></a>從 hello 圖庫加入 Salesforce
tooconfigure hello 整合 Salesforce 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Salesforce。

**tooadd Salesforce hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Salesforce**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. 在 hello 結果 窗格中，選取  **Salesforce**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Salesforce 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 對應項目在 Salesforce 中的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與在 Salesforce 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**在 Salesforce 中。

tooconfigure 及 Azure AD 單一登入與 Salesforce 的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Salesforce 測試使用者](#creating-a-salesforce-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Salesforce 中的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Salesforce 應用程式中。

**tooconfigure Azure AD 單一登入與 Salesforce，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Salesforce**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. 在 hello **Salesforce 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    在 hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值： 
   * 企業帳戶： `https://<subdomain>.my.salesforce.com`
   * 開發人員帳戶： `https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE] 
    > 這些值不是真正的 hello。 更新這些值與 hello 實際登入 URL。 請連絡[Salesforce 用戶端支援小組](https://help.salesforce.com/support)tooget 這些值。 
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. 在 hello **Salesforce 組態**區段中，按一下**設定 Salesforce** tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。** 

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS>
7.  在您的瀏覽器中開啟新索引標籤，並登入 tooyour Salesforce 系統管理員帳戶。

8.  在 hello**管理員**瀏覽窗格中，按一下**安全性控制**tooexpand hello 相關區段。 然後按一下 [單一登入設定]。

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  在 [hello**單一登入設定**頁面上，按一下 hello**編輯**] 按鈕。
    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)

      > [!NOTE]
      > 如果您的 Salesforce 帳戶無法 tooenable 單一登入設定，您可能需要 toocontact [Salesforce 用戶端支援小組](https://help.salesforce.com/support)。 

10. 選取 啟用 SAML，然後按一下儲存。

      ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. SAML 單一登入設定，按一下 tooconfigure**新增**。

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. 在 hello **SAML 單一登入設定編輯**頁面上，進行下列設定的 hello:

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    a. Hello**名稱**欄位中，輸入易記的名稱，此組態中。 提供值**名稱**自動填入 hello **API 名稱**文字方塊。

    b. 貼上**SMAL 實體識別碼**值傳入 hello**簽發者**在 Salesforce 中的欄位。

    c. 在 [hello**實體識別碼] 文字方塊**，輸入您的 Salesforce 網域名稱使用下列模式的 hello:
      
      * 企業帳戶： `https://<subdomain>.my.salesforce.com`
      * 開發人員帳戶： `https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. 按一下**瀏覽**或**選擇檔案**tooopen hello**選擇檔案 tooUpload**  對話方塊中，選取您的 Salesforce 憑證，然後按一下**開啟**tooupload hello 憑證。

    e. 對於 [SAML 身分識別類型]，請選取 [判斷提示包含使用者的 salesforce.com 使用者名稱]。

    f. 如**SAML 識別位置**，選取**識別是 hello 的 hello Subject 陳述式的 NameIdentifier 元素中**

    g. 貼上**單一登入服務 URL**到 hello**身分識別提供者登入 URL**在 Salesforce 中的欄位。
    
    h. 對於 [服務提供者起始的要求繫結]，請選取 [HTTP 重新導向]。
    
    i. 最後，按一下 **儲存**tooapply SAML 單一登入設定。

13. 在 Salesforce 中的 hello 左瀏覽窗格，按一下 **定義域管理**tooexpand hello 相關的區段，然後按一下**我的網域**。

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. 捲動 toohello**驗證組態**區段，然後按一下 [hello**編輯**] 按鈕。

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. 在 hello**驗證服務**區段中，選取 SAML SSO 組態的 hello 易記名稱，然後按一下**儲存**。

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > 如果選取一個以上的驗證服務，則使用者會喜歡哪一種驗證服務的提示的 tooselect toosign 中與在起始單一登入 tooyour Salesforce 環境。 如果您不要 toohappen，則您應該**核取所有其他驗證服務**。
<CE>    
> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. Hello 左瀏覽窗格中 hello **Azure 入口網站**，按一下  **Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-salesforce-test-user"></a>建立 Salesforce 測試使用者

本節會在 Salesforce 中建立名為 Britta Simon 的使用者。 Salesforce 支援預設啟用的 Just-In-Time 佈建。
在這一節沒有您需要進行的動作項目。 如果使用者不在 Salesforce 中，當您嘗試 tooaccess Salesforce 時，會建立一個新。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooSalesforce 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooSalesforce，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Salesforce**。

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

您的單一登入設定，開啟 hello 存取面板的 tootest [https://myapps.microsoft.com](https://myapps.microsoft.com/)，然後登入 hello 測試帳戶，然後按一下**Salesforce**。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定使用者佈建](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

