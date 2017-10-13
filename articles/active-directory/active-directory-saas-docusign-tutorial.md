---
title: "教學課程：Azure Active Directory 與 DocuSign 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 DocuSign 之間的單一登入。"
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
ms.openlocfilehash: 29c99fdf39d366df90abc070f7b836320935035c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a>教學課程：Azure Active Directory 與 DocuSign 整合

在本教學課程中，您會了解如何整合 DocuSign 與 Azure Active Directory (Azure AD)。

DocuSign 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 DocuSign 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 DocuSign (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 DocuSign 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 DocuSign 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 DocuSign
2. 設定並測試 Azure AD 單一登入

## <a name="adding-docusign-from-the-gallery"></a>從資源庫新增 DocuSign
若要設定將 DocuSign 整合到 Azure AD 中，您需要從資源庫將 DocuSign 新增到受管理的 SaaS 應用程式清單。

**若要從資源庫新增 DocuSign，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **DocuSign**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. 在結果窗格中，選取 [DocuSign]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 DocuSign 設定及測試 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 DocuSign 與 Azure AD 中互相對應的使用者。 換句話說，必須建立 Azure AD 使用者和 DocuSign 中相關使用者之間的連結關聯性。

建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 DocuSign 中 **Username** 的值。

若要設定及測試與 DocuSign 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 DocuSign 測試使用者](#creating-a-docusign-test-user)** - 在 DocuSign 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 DocuSign 應用程式中設定單一登入。

**若要使用 DocuSign 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [DocuSign] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. 在 [SAML 簽署憑證] 區段上，按一下 [\憑證 (Base 64)\]，然後將憑證檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. 在 Azure 入口網站的 [DocuSign 設定] 區段中，按一下 [設定 DocuSign] 可開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。
    
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **DocuSign 系統管理入口網站**。

6. 在左側導覽功能表中按一下 [網域] 。
   
    ![設定單一登入][51]

7. 在右窗格中，按一下 [宣告網域] 。
   
    ![設定單一登入][52]

8. 在 [宣告網域] 對話方塊，於 [網域名稱] 文字方塊內輸入您的公司網域，然後按一下 [宣告]。 確定您已驗證網域，而且狀態為作用中。
   
    ![設定單一登入][53]

9. 在左側的功能表中，按一下 [識別提供者]   
   
    ![設定單一登入][54]
10. 在右窗格中，按一下 [新增識別提供者] 。 
   
    ![設定單一登入][55]

11. 在 [識別提供者設定]  頁面上執行下列步驟：
   
    ![設定單一登入][56]

    a. 在 [名稱] 文字方塊中，輸入組態的唯一名稱。 請勿使用空格。

    b.這是另一個 C# 主控台應用程式。 將 **SAML 實體識別碼**貼到 [識別提供者簽發者] 文字方塊。

    c. 將 [SAML 單一登入服務 URL] 貼到 [識別提供者登入 URL] 文字方塊。

    d. 將 [登出 URL] 貼到 [識別提供者登出 URL] 文字方塊。

    e. 選取 [登入驗證要求]。

    f. 選取 [POST] 做為 [驗證要求傳送方式]。

    g. 選取 [GET] 作為 [登出要求傳送方式]。

12. 在 [自訂屬性對應] 區段中，選擇您想要與 Azure AD 宣告對應的欄位。 在此範例中，**emailaddress** 宣告的對應值是 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。 這是 Azure AD 針對電子郵件宣告所提供的預設宣告名稱。 
   
    > [!NOTE]
    > 請使用適當的 **使用者識別碼**，將使用者從 Azure AD 對應到 DocuSign 使用者對應。 選取適當的欄位，並根據組織的設定輸入適當的值。
          
    ![設定單一登入][57]

13. 在 [識別提供者憑證] 區段中按一下 [新增憑證]，然後上傳您已從 Azure AD 入口網站下載的憑證。   
   
    ![設定單一登入][58]

14. 按一下 [儲存] 。

15. 在 [識別提供者] 區段中，按一下 [動作]，然後按一下 [端點]。   
   
    ![設定單一登入][59]
 
16. 在 **DocuSign 系統管理入口網站**的 [檢視 SAML 2.0 端點] 區段中，執行下列步驟：
   
    ![設定單一登入][60]
   
    a. 複製**服務提供者簽發者 URL**，然後貼入 Azure 入口網站的 **DocuSign 網域與 URL** 區段上的 [識別碼] 文字方塊，請遵循下列模式：`https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`。
   
    b.這是另一個 C# 主控台應用程式。 複製**服務提供者登入 URL**，然後貼入 Azure 入口網站的 [DocuSign 網域與 URL] 區段上的 [登入 URL] 文字方塊，遵循下列模式：`https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`。

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    c.  按一下 [關閉]。
    
17. 在 Azure 入口網站上，按一下 [儲存]。
    
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. 在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-docusign-test-user"></a>建立 DocuSign 測試使用者

應用程式支援**及時 (Just In Time) 使用者佈建**，而在驗證之後，則會在應用程式中自動建立使用者。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 DocuSign 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派給 DocuSign，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [DocuSign]。

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在存取面板中按一下 [DocuSign] 磚時，應該會自動登入您的 DocuSign 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
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

