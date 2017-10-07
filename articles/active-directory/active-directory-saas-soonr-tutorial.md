---
title: "教學課程：Azure Active Directory 與 Soonr Workplace 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間 Soonr 工作地點。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>教學課程：Azure Active Directory 與 Soonr Workplace 整合

本教學課程的 hello 目標是 tooshow 您如何 toointegrate Soonr 與 Azure Active Directory (Azure AD) 的工作場所。  
與 Azure AD 整合 Soonr 工作地點可以提供下列優點 hello:

- 您可以控制存取 tooSoonr 工作地點的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooSoonr （單一登入） 的工作地點使用其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Soonr 工作場所的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Soonr Workplace 單一登入功能的訂用帳戶


> [!NOTE] 
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。


在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。


## <a name="scenario-description"></a>案例描述
本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 單一登入的測試環境中。  
本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. Soonr 工作地點加入從 hello 組件庫
2. 設定並測試 Azure AD 單一登入


## <a name="adding-soonr-workplace-from-hello-gallery"></a>Soonr 工作地點加入從 hello 組件庫
tooconfigure hello 整合 Soonr 工作區到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Soonr 工作地點。

**tooadd Soonr 工作場所 hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。 

    ![Active Directory][1]

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。

    ![應用程式][2]

4. 按一下**新增**hello hello 頁底端。

    ![應用程式][3]

5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
 
    ![應用程式][4]

6. 在 [hello] 搜尋方塊中，輸入**Soonr 工作場所**。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. 在 hello 結果窗格中，選取  **Soonr 工作場所**，然後按一下**完成**tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD 單一登入的工作場所 Soonr 根據稱為 「 許 Simon"的測試使用者。

單一登入 toowork，Azure AD 需要 tooknow Soonr 工作場所 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。 換句話說，Azure AD 使用者與 hello Soonr 工作地點中的相關的使用者之間的連結關聯性需要 toobe 建立。  

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Soonr 工作地點中。

tooconfigure 和測試 Azure AD 單一登入的 Soonr 工作地點網路，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Soonr 工作場所](#creating-a-soonr-workplace-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Soonr 工作地點中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello 傳統入口網站中，並 Soonr 工作場所應用程式中設定單一登入。


**tooconfigure Azure AD 單一登入的 Soonr 工作地點網路，執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **Soonr 工作場所**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入** 對話方塊。

    ![設定單一登入][6] 

2. 在 hello**方式上 tooSoonr 工作地點的使用者 toosign 想您**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. 在 hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:。

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello: `https://<server-name>.soonr.com/singlesignon/saml/SSO`。

    b. 按一下 [下一步] 。

    > [!NOTE] 
    > 請注意，這不是 hello 真正的價值。 您有的 tooupdate 這個值與實際的 hello 登入 URL。 請連絡 Soonr 工作場所支援小組 tooget 此值。

4. 在 hello **Soonr 工作場所設定單一登入**頁面上，按一下**下載中繼資料**然後儲存您的電腦上的 hello 檔案：

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. tooget SSO 設定應用程式，請連絡您 Soonr 工作地點的支援團隊並提供 hello 下列： 

    • hello 下載**中繼資料**檔案

    • hello**簽發者 URL**

    • hello **SAML SSO URL**

    • hello**單一登出服務 URL**

    >[!NOTE]
    >此應用程式由取代<a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask 工作場所</a>，而且可以參考<a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">這</a>教學課程使用 Azure AD 設定 hello 應用程式。
   
6. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，然後再按一下**下一步**。

    ![Azure AD 單一登入][10]

7. 在 hello**單一登入確認**頁面上，按一下**完成**。  
  
    ![Azure AD 單一登入][11]



### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。  

![建立 Azure AD 使用者][20]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. 在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. 針對 [使用者類型]，選取 [您組織中的新使用者]。

    b. 在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。

    c. 按一下 [下一步] 。

6.  在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. 在 hello**名字**文字方塊中，輸入**許**。  

    b. 在 hello**姓氏**文字方塊中，輸入， **Simon**。

    c. 在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。

    d. 在 hello**角色**清單中，選取**使用者**。

    e. 按一下 [下一步] 。

7. 在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. 在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. 請記下 hello hello 值**新密碼**。

    b. 按一下頁面底部的 [新增] 。   



### <a name="creating-a-soonr-workplace-test-user"></a>建立 Soonr Workplace 測試使用者

hello 本節目標在於 toocreate 呼叫許 Simon Soonr 工作地點中的使用者。 請使用 Soonr 工作場所支援小組 toocreate hello 平台的使用者。 您可以提高 hello 支援票證，以從 Soonr<a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">這裡</a>。


### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

本節 hello 目標是 tooenabling 許 Simon toouse Azure 單一登入授與他們存取 tooSoonr 工作地點。

![指派使用者][200] 

**tooassign 許 Simon tooSoonr 工作地點，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，tooopen hello 應用程式 檢視，在 hello 目錄檢視中，按一下 **應用程式**hello 上方功能表中。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Soonr 工作場所**。

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。

    ![指派使用者][203] 

1. 在 hello 使用者清單中選取**許 Simon**。

2. 在 hello hello 底部的工具列中按一下**指派**。

    ![指派使用者][205]



### <a name="testing-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。  
當您按一下的 hello Soonr 工作場所磚 hello 存取面板中時，您應該取得自動登入 tooyour Soonr 工作場所應用程式。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
