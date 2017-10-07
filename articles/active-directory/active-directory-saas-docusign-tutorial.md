---
title: "教學課程：Azure Active Directory 與 DocuSign 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 DocuSign 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>教學課程：Azure Active Directory 與 DocuSign 整合

在此教學課程中，您學會如何 toointegrate DocuSign 與 Azure Active Directory (Azure AD)。

整合 Azure AD 與 DocuSign 可以提供下列優點 hello:

- 您可以控制存取 tooDocuSign Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooDocuSign （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 DocuSign 的整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 DocuSign 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 DocuSign
2. 設定並測試 Azure AD 單一登入

## <a name="adding-docusign-from-hello-gallery"></a>從 hello 圖庫加入 DocuSign
tooconfigure hello 整合 DocuSign 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd DocuSign。

**tooadd DocuSign hello 圖庫中，從執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**DocuSign**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. 在 [hello [結果] 窗格中，選取 [ **DocuSign**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 DocuSign 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 docusign 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 docusign 的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** docusign。

tooconfigure 及 Azure AD 單一登入與 DocuSign 的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 DocuSign](#creating-a-docusign-test-user) ** -toohave 許 Simon docusign 連結的 toohello Azure AD 使用者表示法的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 DocuSign 的應用程式中。

**tooconfigure Azure AD 單一登入與 DocuSign，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **DocuSign**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. 在 [hello **SAML 簽章憑證**區段中，按一下**憑證 (base-64)**然後儲存憑證檔案儲存在您的電腦。

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. 在 hello **DocuSign 組態**> 一節的 Azure 入口網站中，按一下**設定 DocuSign** tooopen 設定登入視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**
    
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. 在不同的網頁瀏覽器視窗中，登入 tooyour **DocuSign 管理員入口網站**身為系統管理員。

6. 在 [hello hello 左側的導覽功能表上，按一下 [**網域**。
   
    ![設定單一登入][51]

7. 在 [hello 右窗格中，按一下 [**宣告網域**。
   
    ![設定單一登入][52]

8. 在 [hello**宣告網域**對話方塊中的，在 [hello**網域名稱**文字方塊中，輸入您公司的網域，然後再按一下**宣告**。 請確定您確認 hello 網域，而且 hello 狀態為使用中。
   
    ![設定單一登入][53]

9. 在 [hello 左側功能表中，按一下 [**身分識別提供者**  
   
    ![設定單一登入][54]
10. Hello 右窗格中，按一下 [**新增身分識別提供者**。 
   
    ![設定單一登入][55]

11. 在 [hello**身分識別提供者設定**頁面上，執行下列步驟的 hello:
   
    ![設定單一登入][56]

    a. 在 [hello**名稱**文字方塊中，輸入您的組態的唯一名稱。 請勿使用空格。

    b. 貼上**SAML 實體識別碼**到 hello**身分識別提供者簽發者**文字方塊。

    c. 貼上**SAML 單一登入服務 URL**到 hello**身分識別提供者登入 URL**文字方塊。

    d. 貼上**登出 URL**到 hello**身分識別提供者登出 URL**文字方塊。

    e. 選取 [登入驗證要求]。

    f. 選取 [POST] 做為 [驗證要求傳送方式]。

    g. 選取 [GET] 作為 [登出要求傳送方式]。

12. 在 [hello**自訂屬性對應**區段中，選擇 hello 欄位想 toomap 與 Azure AD 的宣告。 在此範例中，hello **emailaddress** hello 值是對應宣告**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。 它是從 Azure AD 電子郵件宣告 hello 預設宣告的名稱。 
   
    > [!NOTE]
    > 使用適當的 hello**使用者識別碼**toomap hello 使用者從 Azure AD tooDocuSign 使用者對應。 選取 hello 適當欄位，然後輸入 hello 取決於您的組織設定適當的值。
          
    ![設定單一登入][57]

13. 在 [hello**身分識別提供者憑證**區段中，按一下**加入憑證**，然後再上傳您從 Azure AD 入口網站下載的 hello 憑證。   
   
    ![設定單一登入][58]

14. 按一下 [儲存] 。

15. 在 [hello**身分識別提供者**區段中，按一下**動作**，然後按一下 [**端點**。   
   
    ![設定單一登入][59]
 
16. 在 [hello**檢視 SAML 2.0 端點**區段**DocuSign 管理員入口網站**，執行下列步驟的 hello:
   
    ![設定單一登入][60]
   
    a. 複製 hello**服務提供者簽發者 URL**，然後貼入 hello**識別碼**上的文字方塊**DocuSign 網域和 Url** hello Azure 入口網站的下列 hello 區段模式： `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`。
   
    b. 複製 hello**服務提供者登入 URL**，然後貼入 hello**登入 URL**上的文字方塊**DocuSign 網域和 Url** hello Azure 入口網站的下列 hello 區段模式： `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`。

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  按一下 [關閉]。
    
17. 在 [hello Azure 入口網站，按一下 [**儲存**。
    
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. 在 [hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-docusign-test-user"></a>建立 DocuSign 測試使用者

應用程式支援**即時使用者佈建恰好**和之後自動建立 hello 應用程式中驗證使用者。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooDocuSign 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooDocuSign，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**DocuSign**。

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello DocuSign 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 DocuSign 的應用程式。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定使用者佈建](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

