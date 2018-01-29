---
title: "教學課程： Azure Active Directory 整合與 Rollbar |Microsoft 文件"
description: "了解如何設定單一登入 Azure Active Directory 與 Rollbar 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 57537e54-9388-4272-a610-805ce45a451f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/04/2017
ms.author: jeedes
ms.openlocfilehash: bb8a81327163513ab721d2ad72da19173b59bc1f
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="tutorial-azure-active-directory-integration-with-rollbar"></a>教學課程： Azure Active Directory 整合與 Rollbar

在本教學課程中，您可以了解如何與 Azure Active Directory (Azure AD) 整合 Rollbar。

使用 Azure AD 整合 Rollbar 可以提供下列優點：

- 您可以控制可以存取 Rollbar Azure AD 中。
- 您可以啟用自動取得登入 (Single Sign-on) Rollbar 其 Azure AD 帳戶的使用者。
- 您可以在 Azure 入口網站中集中管理您的帳戶。

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 整合與 Rollbar，您需要下列項目：

- Azure AD 訂用帳戶
- Rollbar 單一登入啟用的訂閱

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二項主要的基本工作組成：

1. 從資源庫加入 Rollbar
2. 設定並測試 Azure AD 單一登入

## <a name="adding-rollbar-from-the-gallery"></a>從資源庫加入 Rollbar
若要設定 Rollbar 整合 Azure AD，您需要加入 Rollbar 從資源庫，您的受管理的 SaaS 應用程式清單。

**若要從資源庫加入 Rollbar，執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Azure Active Directory 按鈕][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![企業應用程式刀鋒視窗][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![新增應用程式按鈕][3]

4. 在 搜尋 方塊中，輸入**Rollbar**，選取**Rollbar**然後按一下 從結果面板**新增**按鈕以加入應用程式。

    ![在 [結果] 清單中的 Rollbar](./media/active-directory-saas-rollbar-tutorial/tutorial_rollbar_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，設定，並根據測試使用者稱為 「 許 Simon"Rollbar 使用測試 Azure AD 單一登入。

單一登入工作，Azure AD 需要知道對應項目中的使用者 Rollbar 是使用者在 Azure AD 中。 換句話說，必須建立 Azure AD 使用者和相關的使用者在 Rollbar 之間的連結關聯性。

Rollbar，在指定的值**使用者名**做為值的 Azure AD 中**Username**建立的連結關聯性。

若要設定和測試 Azure AD 單一登入與 Rollbar 時，您必須完成下列的建置組塊：

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立測試使用者 Rollbar](#create-a-rollbar-test-user)**  -若要在連結至使用者的 Azure AD 表示 Rollbar 許 Simon 對應項目。
4. **[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 Azure 入口網站中，並 Rollbar 應用程式中設定單一登入。

**若要設定 Azure AD 單一登入與 Rollbar，執行下列步驟：**

1. 在 Azure 入口網站上**Rollbar**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-rollbar-tutorial/tutorial_rollbar_samlbase.png)

3. 在**Rollbar 網域和 Url**區段中，如果您想要設定應用程式中的執行下列步驟**IDP**初始模式：

    ![Rollbar 網域和 Url 的單一登入資訊](./media/active-directory-saas-rollbar-tutorial/tutorial_rollbar_url.png)

    a. 在 [識別碼] 文字方塊中，輸入 URL：`https://saml.rollbar.com`

    b. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://rollbar.com/<accountname>/saml/sso/azure/`

4. 如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]，然後執行下列步驟：

    ![Rollbar 網域和 Url 的單一登入資訊](./media/active-directory-saas-rollbar-tutorial/tutorial_rollbar_url1.png)

    在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://rollbar.com/<accountname>/saml/login/azure/`
     
    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的回覆 URL 與登入 URL 更新這些值。 請連絡[Rollbar 用戶端支援小組](mailto:support@rollbar.com)取得這些值。 

5. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。

    ![憑證下載連結](./media/active-directory-saas-rollbar-tutorial/tutorial_rollbar_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-rollbar-tutorial/tutorial_general_400.png)
    
7. 在不同的網頁瀏覽器視窗中，登入您 Rollbar 公司網站的系統管理員身分。

8. 按一下**設定檔設定**右上角，然後按一下**帳戶名稱設定**。
    
    ![組態](./media/active-directory-saas-rollbar-tutorial/general.png)

9. 按一下**身分識別提供者**安全性 之下。

    ![組態](./media/active-directory-saas-rollbar-tutorial/configure1.png)

10. 在**SAML 身分識別提供者**區段中，執行下列步驟：
    
    ![組態](./media/active-directory-saas-rollbar-tutorial/configure2.png)

    a. 選取**AZURE**從**SAML 身分識別提供者**下拉式清單。

    b. 在記事本中開啟您的中繼資料檔案，將它的內容複製到剪貼簿，然後將它貼到**SAML 中繼資料**文字方塊。

    c. 按一下 [檔案] 。

11. 之後按一下儲存 按鈕，畫面會像這樣。 本節中，執行下列步驟：
    
    ![組態](./media/active-directory-saas-rollbar-tutorial/configure3.png)

    a. 選取**需要透過 SAML 身分識別提供者的登入**核取方塊。

    b. 按一下 [檔案] 。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。

    ![Azure Active Directory 按鈕](./media/active-directory-saas-rollbar-tutorial/create_aaduser_01.png)

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-rollbar-tutorial/create_aaduser_02.png)

3. 若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。

    ![[新增] 按鈕](./media/active-directory-saas-rollbar-tutorial/create_aaduser_03.png)

4. 在 [使用者] 對話方塊中，執行下列步驟：

    ![[使用者] 對話方塊](./media/active-directory-saas-rollbar-tutorial/create_aaduser_04.png)

    a. 在 [名稱] 方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。

    c. 選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。

    d. 按一下頁面底部的 [新增] 。
 
### <a name="create-a-rollbar-test-user"></a>建立 Rollbar 測試使用者

若要讓 Azure AD 使用者能夠登入 Rollbar，它們必須佈建到 Rollbar。 在 Rollbar，佈建須手動進行。

**若要佈建使用者帳戶，請執行下列步驟：**

1. 以系統管理員身分登入您 Rollbar 公司網站。

2. 按一下**設定檔設定**右上角，然後按一下**帳戶名稱設定**。

    ![User](./media/active-directory-saas-rollbar-tutorial/general.png)

3. 按一下 [使用者] 。
    
    ![新增員工](./media/active-directory-saas-rollbar-tutorial/user1.png)

4. 按一下**邀請團隊成員**。

    ![邀請人員](./media/active-directory-saas-rollbar-tutorial/user2.png)

5. 在文字方塊中，輸入類似的使用者名稱 **brittasimon@contoso.com**  ，然後按一下 **新增/邀請**。

    ![邀請人員](./media/active-directory-saas-rollbar-tutorial/user3.png)

6. 使用者會收到的邀請之後在接受, 由系統建立。

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，以啟用要使用 Azure 單一登入授與存取權 Rollbar 許 Simon。

![指派使用者角色][200] 

**若要指派 Rollbar 許 Simon，執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取**Rollbar**。

    ![應用程式清單中的 [Rollbar] 連結](./media/active-directory-saas-rollbar-tutorial/tutorial_rollbar_app.png)  

3. 在左側功能表中，按一下 [使用者和群組]。

    ![[使用者和群組] 連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![[新增指派] 窗格][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您按一下 Rollbar 磚，在存取面板時，您應該取得自動登入 Rollbar 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rollbar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rollbar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rollbar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rollbar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rollbar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rollbar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rollbar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rollbar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rollbar-tutorial/tutorial_general_203.png

