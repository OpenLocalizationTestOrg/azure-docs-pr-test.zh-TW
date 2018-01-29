---
title: "教學課程：Azure Active Directory 與 Tableau Online 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Tableau Online 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 47ae9dbde509726065da7eaee2c7aec491389f45
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>教學課程：Azure Active Directory 與 Tableau Online 整合

在本教學課程中，您將了解如何整合 Tableau Online 與 Azure Active Directory (Azure AD)。

Tableau Online 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Tableau Online 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Tableau Online (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Tableau Online 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Tableau Online 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二項主要的基本工作組成：

1. 從資源庫新增 Tableau Online
2. 設定並測試 Azure AD 單一登入

## <a name="adding-tableau-online-from-the-gallery"></a>從資源庫新增 Tableau Online
若要設定 Tableau Online 與 Azure AD 整合，您需要從資源庫將 Tableau Online 加入到受控 SaaS 應用程式清單中。

**如要從資源庫新增 Tableau Online，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![[應用程式]][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![[應用程式]][3]

4. 在搜尋方塊中，輸入 **Tableau Online**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. 在結果窗格中，選取 [Tableau Online]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Tableau Online 搭配運作的 Azure AD 單一登入。

若要讓單一登入能夠運作，Azure AD 必須知道 Tableau Online 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者和 Tableau Online 中的相關使用者之間建立連結關聯性。

在 Tableau Online 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。

若要使用 Tableau Online 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Tableau Online 測試使用者](#creating-a-tableau-online-test-user)** - 使 Tableau Online 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Tableau Online 應用程式中設定單一登入。

**若要設定透過 Tableau Online 使用 Azure AD 單一登入功能，請執行下列步驟：**

1. 在 Azure 入口網站的 [Tableau Online] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. 在 [Tableau Online 網域及 URL] 區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    a. 在 [登入 URL] 文字方塊中，輸入 URL：`https://sso.online.tableau.com`

    b. 在 [識別碼] 文字方塊中，輸入 URL：`https://sso.online.tableau.com/public/sp/<instancename>`

4. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. 在不同的瀏覽器視窗中，登入您的 Tableau Online 應用程式。 依序前往 [設定] 和 [驗證]。
   
    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. 若要在 [驗證類型] 區段下啟用 SAML，請 勾選 [使用 SAML 的單一登入] 核取方塊。
   
    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. 向下捲動到 [將中繼資料檔匯入到 Tableau Online]  區段。  按一下 [瀏覽]，然後匯入您從 Azure AD 下載的中繼資料檔案。 然後，按一下 [套用] 。
   
   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. 在 [比對判斷提示] 區段中，針對 [電子郵件地址]、[名字] 和 [姓氏] 插入對應的識別提供者判斷提示名稱。 若要從 Azure AD 取得這項資訊︰ 
  
    a. 在 Azure 入口網站中，移至 [Tableau Online] 應用程式整合頁面。
    
    b. 在屬性區段中，選取 [檢視及編輯所有其他使用者屬性] 核取方塊。 
    
   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    c. 使用下列步驟複製 givenname、email 和 surname 屬性的命名空間值：

   ![Azure AD 單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    d. 按一下 [user.givenname] 值 
    
    e. 從 [命名空間] 文字方塊複製該值。

   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    f. 若要複製 email 和 surname 的命名空間值，請遵循上述步驟。

    g. 切換至 Tableau Online 應用程式，然後將 [Tableau Online 屬性] 區段設定如下：
     * 電子郵件︰**mail** 或 **userprincipalname**
     * 名字︰ **givenname**
     * 姓氏︰ **surname**
   
   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下頁面底部的 [新增] 。
 
### <a name="creating-a-tableau-online-test-user"></a>建立 Tableau Online 測試使用者

在本節中，您要在 Tableau Online 中建立名為 Britta Simon 的使用者。

1. 在 [Tableau Online] 中，依序按一下 [設定] 和 [驗證] 區段。 向下捲動至 [選取使用者]  區段。 依序按一下 [新增使用者] 和 [輸入電子郵件地址]。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. 選取 [新增單一登入 (SSO) 驗證的使用者] 。 在 [輸入電子郵件地址] 文字方塊中，新增 britta.simon@contoso.com
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. 按一下頁面底部的 [新增] 。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Tableau Online 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**如要將 Britta Simon 指派給 Tableau Online，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Tableau Online] 。

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。

當您在存取面板中按一下 [Tableau Online ] 圖格時，應該會自動登入您的 Tableau Online 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

