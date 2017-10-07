---
title: "教學課程：Azure Active Directory 與 SuccessFactors 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse SuccessFactors 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>教學課程：Azure Active Directory 與 SuccessFactors 整合
本教學課程的 hello 目標是 tooshow 您如何 toointegrate SuccessFactors 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 SuccessFactors 可以提供下列優點 hello:

* 您可以控制存取 tooSuccessFactors Azure AD 中
* 您可以啟用您的使用者 tooautomatically get 登入 tooSuccessFactors （單一登入） 具有其 Azure AD 帳戶
* 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
tooconfigure 與 SuccessFactors 的 Azure AD 整合，您需要下列項目 hello:

* 有效的 Azure 訂閱
* SuccessFactors 中的租用戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。
> 
> 

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

* 除非必要，否則您不應使用生產環境，。
* 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 單一登入的測試環境中。

本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 SuccessFactors
2. 設定並測試 Azure AD 單一登入

## <a name="adding-successfactors-from-hello-gallery"></a>從 hello 圖庫加入 SuccessFactors
tooconfigure hello 整合 SuccessFactors 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SuccessFactors。

**tooadd SuccessFactors hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站上 hello 左邊的導覽面板中，按一下  **Active Directory**。
   
    ![設定單一登入][1]
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![設定單一登入][2]
4. 按一下**新增**hello hello 頁底端。
   
    ![應用程式][3]
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![設定單一登入][4]
6. 在 hello**搜尋方塊**，型別**SuccessFactors**。
   
    ![設定單一登入][5]
7. 在 hello 結果 窗格中，選取  **SuccessFactors**，然後按一下**完成**tooadd hello 應用程式。
   
    ![設定單一登入][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD 單一登入與 SuccessFactors 根據稱為 「 許 Simon"的測試使用者。

單一登入 toowork，Azure AD 需要 tooknow 是在 SuccessFactors tooan 使用者在 Azure AD 中的 hello 對等項目的使用者。 換句話說，Azure AD 使用者與 hello SuccessFactors 中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** SuccessFactors 中。

tooconfigure 及測試 Azure AD 單一登入 SuccessFactors，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 SuccessFactors](#creating-a-successfactors-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 SuccessFactors 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入
在本節中，您可以啟用 Azure AD 單一登入 hello 傳統入口網站中，並設定單一登入 SuccessFactors 應用程式中。

**tooconfigure Azure AD 單一登入 SuccessFactors 中，執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **SuccessFactors**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
    ![設定單一登入][7]
2. 在 hello**如何想您使用者 toosign tooSuccessFactors 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
    ![設定單一登入][8]
3. 在 hello**設定應用程式 URL**頁面上，執行下列步驟，hello，然後按一下**下一步**。
   
    ![設定單一登入][9]
   
    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用其中一個 hello 下列模式： 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用其中一個 hello 下列模式： 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. 按一下 [下一步] 。 

    > [!NOTE]
    > 請注意這些不是 hello 實際值。 您有 tooupdate hello 實際的登入 URL 及回覆 URL 與這些值。 tooget 這些值，請連絡[SuccessFactors 支援團隊](https://www.successfactors.com/en_us/support.html)。

1. 在 hello**於 SuccessFactors 設定單一登入**頁面上，按一下**下載憑證**，然後儲存在本機電腦上的 hello 憑證檔案。
   
    ![設定單一登入][10]

2. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **SuccessFactors 系統管理入口網站** 。

3. 請瀏覽**應用程式安全性**和原生太**單一登入的功能**。 

4. 任何值置於 hello**重設語彙基元**按一下**語彙基元儲存**tooenable SAML SSO。
   
    ![在應用程式端設定單一登入][11]

    > [!NOTE] 
    > 這個值只做 hello 開啟/關閉參數。 如果儲存的任何值，hello SAML SSO 會是 ON。 如果為空白值會儲存 hello SAML SSO 為 OFF。

1. 原生 toobelow 螢幕擷取畫面，並執行下列動作的 hello。
   
    ![在應用程式端設定單一登入][12]
   
    a. 選取 hello **SAML v2 SSO**選項按鈕
   
    b. 設定 SAML 判斷提示的合作對象 Name(e.g.SAml issuer + company name) hello。
   
    c. 在 hello **SAML 簽發者**文字方塊放 hello 值**簽發者 URL**從 Azure AD 應用程式組態精靈。
   
    d. 選取 [回應 (客戶產生的/IdP/AP)] 做為 [需要必要簽章]。
   
    e. 選取 [啟用] 做為 [啟用 SAML 旗標]。
   
    f. 選取 [否] 做為 [登入要求簽章 (SF 產生的/SP/RP)]。
   
    g. 選取 [瀏覽器/後置設定檔] 做為 [SAML 設定檔]。
   
    h. 選取 [否] 做為 [強制執行憑證有效期間]。
   
    i. Hello hello 下載的憑證檔案的內容複製並貼到 hello **SAML 驗證憑證**文字方塊。

    > [!NOTE] 
    > hello 憑證內容必須有憑證和結束憑證標記開頭。

1. 瀏覽 tooSAML V2、，然後執行下列步驟的 hello:
   
    ![在應用程式端設定單一登入][13]
   
    a. 選取 [是] 做為 [支援 SP 起始的全域登出]。
   
    b. 在 hello**全域登出服務 URL （LogoutRequest 目的地）**文字方塊放 hello 值**遠端登出 URL**從 Azure AD 應用程式組態精靈。
   
    c. 選取 [否] 做為 [要求 SP 必須加密所有 NameID 元素]。
   
    d. 選取 [未指定] 做為 [NameID 格式]。
   
    e. 選取 [是] 做為 [啟用 SP 起始的登入 (AuthnRequest)]。
   
    f. 在 hello**做全公司的簽發者傳送要求**文字方塊放 hello 值**遠端登入 URL**從 Azure AD 應用程式組態精靈。
2. 執行這些步驟，如果您想 toomake hello 登入使用者名稱不區分大小寫。
   
    a. 請瀏覽**公司設定**(near hello 下方）。
   
    b. 選取 [啟用不區分大小寫使用者名稱] 附近的核取方塊。
   
    c. 按一下 [儲存]。
   
    ![設定單一登入][29]

    > [!NOTE] 
    > 如果您嘗試 tooenable，hello 系統會檢查如果網域控制站會建立重複的 SAML 登入名稱。 例如，如果 hello 客戶有 User1 和 user1 的使用者名稱。 取消區分大小寫功能將會讓這些名稱重複。 hello 系統提供的錯誤訊息，並將不會啟用 hello 功能。 hello 客戶將會需要 toochange hello 使用者名稱的其中一個，實際的拼法不同。 

1. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。
   
    ![應用程式][14]
2. 在 hello**單一登入確認**頁面上，按一下**完成**。
   
    ![應用程式][15]

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節 hello 目標是 toocreate 測試使用者呼叫許 Simon hello 傳統入口網站中。

![建立 Azure AD 使用者][16]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![建立 Azure AD 測試使用者][17]
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。
   
    ![建立 Azure AD 測試使用者][18]
4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。
   
    ![建立 Azure AD 測試使用者][19]
5. 在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者][20]
   
    a. 針對 [使用者類型]，選取 [您組織中的新使用者]。
   
    b. 在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。
   
    c. 按一下 [下一步] 。
6. 在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者][21]
   
    a. 在 hello**名字**文字方塊中，輸入**許**。  
   
    b. 在 hello**姓氏**文字方塊中，輸入， **Simon**。
   
    c. 在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。
   
    d. 在 hello**角色**清單中，選取**使用者**。
   
    e. 按一下 [下一步] 。
7. 在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。
   
    ![建立 Azure AD 測試使用者][22]
8. 在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者][23]
   
    a. 請記下 hello hello 值**新密碼**。
   
    b. 按一下頁面底部的 [新增] 。  

### <a name="creating-a-successfactors-test-user"></a>建立 SuccessFactors 測試使用者
在訂單 tooenable Azure AD 使用者 toolog 入 SuccessFactors，它們必須佈建到 SuccessFactors。  
在 SuccessFactors 的 hello 案例中，佈建須手動進行。

tooget SuccessFactors 中建立的使用者，您需要 toocontact hello [SuccessFactors 支援團隊](https://www.successfactors.com/en_us/support.html)。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者
本節 hello 目標是授與他們存取 tooSuccessFactors tooenabling 許 Simon toouse Azure 單一登入。

![指派使用者][24]

**tooassign 許 Simon tooSuccessFactors，執行下列步驟的 hello:**

1. Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。
   
    ![指派使用者][25]
2. 在 [hello] 應用程式清單中，選取**SuccessFactors**。
   
    ![設定單一登入][26]
3. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。
   
    ![指派使用者][27]
4. 在 hello 使用者清單中選取**許 Simon**。
5. 在 hello hello 底部的工具列中按一下**指派**。
   
    ![指派使用者][28]

### <a name="testing-single-sign-on"></a>測試單一登入
hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。

當您按一下的 hello SuccessFactors 磚 hello 存取面板中時，您應該取得自動登入 tooyour SuccessFactors 的應用程式。

## <a name="additional-resources"></a>其他資源
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
