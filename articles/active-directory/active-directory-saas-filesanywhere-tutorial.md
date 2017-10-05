---
title: "教學課程：Azure Active Directory 與 FilesAnywhere 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 FilesAnywhere 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 4153056bd21006061c6ad8ff9cf3c17de9248628
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a>教學課程：Azure Active Directory 與 FilesAnywhere 整合

在本教學課程中，您會了解如何整合 FilesAnywhere 與 Azure Active Directory (Azure AD)。

FilesAnywhere 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 FilesAnywhere 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 FilesAnywhere (單一登入)
- 您可以在 Azure 管理入口網站中集中管理您的帳戶

若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 FilesAnywhere 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 啟用 FilesAnywhere 單一登入的訂用帳戶


> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。


若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。


## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 FilesAnywhere
2. 設定並測試 Azure AD 單一登入


## <a name="adding-filesanywhere-from-the-gallery"></a>從資源庫新增 FilesAnywhere
若要設定 FilesAnywhere 與 Azure AD 整合，您需要從資源庫將 FilesAnywhere 新增到受管理的 SaaS 應用程式清單中。

**若要從資源庫新增 FilesAnywhere，請執行下列步驟：**

1. 在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 按一下對話方塊頂端的 [新增] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **FilesAnywhere**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. 在結果窗格中，選取 [FilesAnywhere]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FilesAnywhere 設定及測試 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 FilesAnywhere 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者和 FilesAnywhere 中的相關使用者之間建立連結關聯性。

建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 FilesAnywhere 中 **Username** 的值。

若要設定並測試與 FilesAnywhere 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 FilesAnywhere 測試使用者](#creating-a-filesanywhere-test-user)** - 在 FilesAnywhere 中，建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。
3. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
4. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 FilesAnywhere 中設定單一登入。

**若要設定與 FilesAnywhere 搭配運作的 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 管理入口網站的 [FilesAnywhere] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. 如果您想要以 **IDP 起始模式**設定應用程式，請在 [FilesAnywhere 網域和 URL] 區段上執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    a. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.filesanywhere.com/saml20.aspx?c=215`
> [!NOTE]
> 請注意，**clientid** 的值 **215** 只是範例。 您必須以實際的 clientid 值加以取代。

4. 在 [FilesAnywhere 網域和 URL] 區段中，如果您想要在 [SP 起始模式] 中設定應用程式，請執行下列步驟：
    
    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    a. 按一下 [顯示進階 URL 設定] 選項

    b. 在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://<sub domain>.filesanywhere.com/`

    > [!NOTE] 
    > 請注意這些不是真正的值。 您必須使用實際的「登入 URL」及「回覆 URL」來更新這些值。 請連絡 [FilesAnywhere 支援小組](mailto:support@FilesAnywhere.com) 以取得這些值。 

5. FilesAnywhere Software 應用程式會預期要有特定格式的 SAML 判斷提示。 請設定此應用程式的下列宣告。 您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。 以下螢幕擷取畫面顯示上述的範例。
    
    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    當使用者註冊 FilesAnywhere 時，他們會取得來自 [FilesAnywhere 小組](mailto:support@FilesAnywhere.com)的 **clientid** 屬性值。 您必須使用 FilesAnywhere 提供的唯一值，新增 [用戶端 ID] 屬性。 上述的所有屬性都是必要屬性。
    > [!NOTE] 
    > 請注意，**clientid** 的值 **2331**只是範例。 您必須提供實際值。


6. 在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：
    
    | 屬性名稱 | 屬性值 |
    | ---------------| --------------- |    
    | clientid | *"uniquevalue"* |

    a. 按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    b. 在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。
    
    c. 在 [值] 清單中，選取該列所顯示的值。
    
    d. 按一下 [確定]。

7. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. 在 [FilesAnywhere 組態] 區段上，按一下 [設定 FilesAnywhere] 以開啟 [設定登入] 視窗。

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. 若要在 FilesAnywhere 結尾為您的應用程式完成 SSO 組態，請連絡 [FilesAnywhere 支援小組](mailto:support@FilesAnywhere.com)，並且提供已下載的 SAML 權杖簽署憑證和單一登入 (SSO) URL。

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. 移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. 在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。 



### <a name="creating-a-filesanywhere-test-user"></a>建立 FilesAnywhere 測試使用者

應用程式僅在使用者佈建時支援，驗證之後，會在應用程式中自動建立使用者。 


### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 FilesAnywhere 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派到 FilesAnywhere，請執行下列步驟：**

1. 在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [FilesAnywhere] 。

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    


### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在存取面板中按一下 [FilesAnywhere] 圖格時，應該會自動登入您的 FilesAnywhere 應用程式。


## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
