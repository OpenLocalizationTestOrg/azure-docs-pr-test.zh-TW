---
title: "教學課程：Azure Active Directory 與 Workpath 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Workpath 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f4efa56d2c0374a977c1e46dad64b596cc9c3ea8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a>教學課程：Azure Active Directory 與 Workpath 整合

在本教學課程中，您將了解如何整合 Workpath 與 Azure Active Directory (Azure AD)。

整合 Workpath 與 Azure AD 有下列優點：

- 您可以在 Azure AD 中控制可存取 Workpath 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Workpath (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Workpath 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Workpath 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Workpath
2. 設定並測試 Azure AD 單一登入

## <a name="adding-workpath-from-the-gallery"></a>從資源庫新增 Workpath
若要設定將 Workpath 整合到 Azure AD 中，您需要從資源庫將 Workpath 新增到受管理的 SaaS 應用程式清單。

**若要從資源庫新增 Workpath，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，鍵入 **Workpath**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. 在結果窗格中，選取 [Workpath]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Workpath 設定及測試 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 Workpath 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者和 Workpath 中的相關使用者之間建立連結關聯性。

在 Workpath 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要使用 Workpath 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Workpath 測試使用者](#creating-a-workpath-test-user)** - 使 Workpath 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Workpath 應用程式中設定單一登入。

**若要使用 Workpath 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Workpath] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. 如果您想要以 **IDP** 起始模式設定應用程式，請在 [Workpath 網域和 URL] 區段上執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    a. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://api.workpath.com/v1/saml/metadata/<instancename>`

    b. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://api.workpath.com/v1/saml/assert/<instancename>`

4. 按一下 [顯示進階 URL 設定]。 如果您想要在 **SP** 起始模式中設定應用程式，請執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.workpath.com/ `

    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的「單一登入 URL」、「識別碼」及「回覆 URL」來更新這些值。 請連絡 [Workpath 支援小組](https://help.workpath.com)以取得這些值。

5. Workpath 應用程式需要特定格式的 SAML 判斷提示。 設定此應用程式的下列宣告。 您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。 以下螢幕擷取畫面顯示此設定的範例。 

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. 在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：
    
    | 屬性名稱 | 屬性值 |
    | ------------------- | -------------------- |    
    | first_name | user.givenname |
    | last_name | user.surname |
    
    a. 按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    b. 在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    c. 在 [值] 清單中，選取該列所顯示的值。

    d. [命名空間] 文字方塊保持空白。
    
    e. 按一下 [確定] 。
    

7. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. 在 [Workpath Configuration] \(Workpath 設定) 區段上，按一下 [Configure Workpath] \(設定 Workpath) 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. 若要在 **Workpath** 這一端設定單一登入，您需要將所下載的**中繼資料 XML**、**登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL** 傳送給 [Workpath 支援小組](https://help.workpath.com)。 

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-workpath-test-user"></a>建立 Workpath 測試使用者

Workpath 支援 Just-In-Time 使用者佈建。 驗證之後，會在應用程式中自動建立使用者。 


### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Workpath 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派給 Workpath，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Workpath]。

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在存取面板中按一下 [Workpath] 圖格時，應該會自動登入您的 Workpath 應用程式。
如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

