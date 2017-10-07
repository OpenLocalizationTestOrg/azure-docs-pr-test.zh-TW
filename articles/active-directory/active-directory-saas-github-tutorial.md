---
title: "教學課程：Azure Active Directory 與 GitHub 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 GitHub 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>教學課程：Azure Active Directory 與 GitHub 整合

在此教學課程中，您學會如何 toointegrate GitHub 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 GitHub 可以提供下列優點 hello:

- 您可以控制存取 tooGitHub Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooGitHub （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 GitHub 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 GitHub 單一登入的訂用帳戶


> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。


在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。


## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 GitHub
2. 設定並測試 Azure AD 單一登入


## <a name="adding-github-from-hello-gallery"></a>從 hello 圖庫加入 GitHub
tooconfigure hello 整合 GitHub 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd GitHub。

**tooadd GitHub hello 圖庫中，從執行下列步驟的 hello:**

1. 在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**GitHub.com**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. 在 [hello [結果] 窗格中，選取 [ **GitHub**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 GitHub 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 對應項目在 GitHub 中的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 GitHub 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** GitHub 中。

tooconfigure 及測試 Azure AD 單一登入與 GitHub，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 GitHub 測試使用者](#creating-a-GitHub-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 GitHub 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入 GitHub 應用程式中。

**tooconfigure Azure AD 單一登入與 GitHub，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站上 hello **GitHub**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. 在 [hello **GitHub 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    a. 在 [hello**登入 URL**文字方塊中，做為型別 hello 值：`https://github.com/orgs/<entity-id>/sso`

    b. 在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > 請注意這些不是 hello 實際值。 您有 tooupdate hello 實際登入 URL 和識別碼具有這些值。 這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。 移 tooGitHub 管理 > 一節 tooretrieve 這些值。 

4. 在 [hello**使用者屬性**區段中，選取**使用者識別碼**user.mail 為。

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. 在 [hello **SAML 簽章憑證**區段中，按一下**建立新憑證**。

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. 在 [hello**建立新的憑證**] 對話方塊中，按一下 hello 日曆圖示，然後選取**到期日**。 然後按一下 [儲存] 按鈕。

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. 在 hello **SAML 簽章憑證**區段中，選取**啟用新的憑證**按一下**儲存**] 按鈕。

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. Hello 快顯視窗上**變換憑證**視窗中，按一下 [**確定**。

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. 在 [hello **GitHub 組態**區段中，按一下**設定 GitHub** tooopen**設定登入**視窗。

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. 在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 GitHub 組織網站。

12. 瀏覽過**設定**按一下**安全性**

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. 檢查 hello**啟用 SAML 驗證**] 方塊中，顯示 hello 單一登入設定欄位。 然後，使用 Azure AD 組態 hello 單一登入 URL 值 tooupdate hello 單一登入的 URL。

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. 設定下列欄位的 hello:

    a. **登入 URL**： 輸入**SAML 單一登入服務 URL**從 hello**設定 GitHub**上 Azure AD 區段

    b. **簽發者**： 輸入**SAML 實體識別碼**從 hello**設定 GitHub**上 Azure AD 區段

    c. **公開憑證**： 開啟 hello 從 Azure AD 中包括 「 開始憑證 」 和 「 結束憑證 」 為 「 記事本 」 並複製 hello 內容下載憑證

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. 按一下**測試 SAML 設定**tooconfirm 所沒有的驗證失敗或 SSO 期間發生的錯誤。

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. 按一下 [儲存] 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。 


### <a name="creating-a-github-test-user"></a>建立 GitHub 測試使用者

在訂單 tooenable Azure AD 使用者 toolog 到 GitHub，您必須是佈建到 GitHub。  
在 GitHub 的 hello 案例中，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟 hello:**

1. 登入 tooyour GitHub 公司網站的系統管理員身分。

2. 按一下 [人員] 。

    ![人員](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "人員")

3. 按一下 [邀請成員]。

    ![邀請使用者](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "邀請使用者")

4. 在 [hello**邀請成員**對話方塊頁面上，執行下列步驟的 hello:

    a. 在 [hello**電子郵件**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。

    ![邀請人員](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "邀請人員")
    
    b. 按一下 [傳送邀請]。

    ![邀請人員](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "邀請人員")

    > [!NOTE]
    > hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。


### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooGitHub 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooGitHub，執行下列步驟的 hello:**

1. 在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**GitHub.com**。

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    


### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello GitHub 磚 hello 存取面板中的時，您應該取得已登入的 tooyour GitHub 應用程式。 您將會以登入組織帳戶但需要 toolog 使用您個人的帳戶。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
