---
title: "教學課程：Azure Active Directory 與 SuccessFactors 整合 | Microsoft Docs"
description: "了解如何設定單一登入 Azure Active Directory 與 SuccessFactors 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: jeedes
ms.openlocfilehash: b9545599b4ac02927c38931777a3cee623a4e940
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>教學課程：Azure Active Directory 與 SuccessFactors 整合

在本教學課程中，您可以了解如何與 Azure Active Directory (Azure AD) 整合 SuccessFactors。

SuccessFactors 與 Azure AD 整合提供下列優點：

- 您可以控制可以存取 SuccessFactors 的 Azure AD 中。
- 您可以讓您自動取得登入 SuccessFactors （單一登入） 具有其 Azure AD 帳戶的使用者。
- 您可以在 Azure 入口網站中集中管理您的帳戶。

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 SuccessFactors 的整合，您需要下列項目：

- Azure AD 訂用帳戶
- SuccessFactors 單一登入啟用訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二項主要的基本工作組成：

1. 從資源庫新增 SuccessFactors
2. 設定並測試 Azure AD 單一登入

## <a name="adding-successfactors-from-the-gallery"></a>從資源庫新增 SuccessFactors
若要設定 SuccessFactors 與 Azure AD 的整合，您需要從資源庫將 SuccessFactors 新增到受控 SaaS 應用程式清單。

**若要從資源庫新增 SuccessFactors，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Azure Active Directory 按鈕][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![企業應用程式刀鋒視窗][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![新增應用程式按鈕][3]

4. 在 搜尋 方塊中，輸入**SuccessFactors**，選取**SuccessFactors**然後按一下 從結果面板**新增**按鈕以加入應用程式。

    ![在 [結果] 清單中的 SuccessFactors](./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您可以設定及測試 Azure AD 單一登入 SuccessFactors 根據稱為 「 許 Simon"的測試使用者。

單一登入工作，如 Azure AD 需要知道 SuccessFactors 中對等項目的使用者是使用者在 Azure AD 中。 換句話說，必須在 Azure AD 使用者和 SuccessFactors 中的相關使用者之間建立連結關聯性。

在 SuccessFactors 中，將指派的值**使用者名稱**做為值的 Azure AD 中**Username**建立的連結關聯性。

若要設定及測試對 SuccessFactors 的 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立測試使用者 SuccessFactors](#create-a-successfactors-test-user)**  -若要連結至使用者的 Azure AD 表示的 SuccessFactors 中有許 Simon 對應項目。
4. **[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 Azure 入口網站中，並設定單一登入 SuccessFactors 應用程式中。

**若要使用 SuccessFactors 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站上**SuccessFactors**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_samlbase.png)

3. 在**SuccessFactors 網域和 Url**區段中，執行下列步驟：

    ![SuccessFactors 網域和 Url 的單一登入資訊](./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰
    | |
    |--|
    | `https://<companyname>.successfactors.com/<companyname>`|
    | `https://<companyname>.sapsf.com/<companyname>`|
    | `https://<companyname>.successfactors.eu/<companyname>`|
    | `https://<companyname>.sapsf.eu`|

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：
    | |
    |--|
    | `https://www.successfactors.com/<companyname>`|
    | `https://www.successfactors.com`|
    | `https://<companyname>.successfactors.eu`|
    | `https://www.successfactors.eu/<companyname>`|
    | `https://<companyname>.sapsf.com`|
    | `https://hcm4preview.sapsf.com/<companyname>`|
    | `https://<companyname>.sapsf.eu`|
    | `https://www.successfactors.cn`|
    | `https://www.successfactors.cn/<companyname>`|

    c. 在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：
    | |
    |--|
    | `https://<companyname>.successfactors.com/<companyname>`|
    | `https://<companyname>.successfactors.com`|
    | `https://<companyname>.sapsf.com/<companyname>`|
    | `https://<companyname>.sapsf.com`|
    | `https://<companyname>.successfactors.eu/<companyname>`|
    | `https://<companyname>.successfactors.eu`|
    | `https://<companyname>.sapsf.eu`|
    | `https://<companyname>.sapsf.eu/<companyname>`|
    | `https://<companyname>.sapsf.cn`|
    | `https://<companyname>.sapsf.cn/<companyname>`|
         
    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。 請連絡[SuccessFactors 用戶端支援小組](https://www.successfactors.com/en_us/support.html)取得這些值。 

4. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![憑證下載連結](./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-successfactors-tutorial/tutorial_general_400.png)
    
6. 在**SuccessFactors 設定**區段中，按一下**設定 SuccessFactors**開啟**設定登入**視窗。 從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。

    ![設定單一登入](./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_configure.png) 

7. 在不同的網頁瀏覽器視窗中，登入您**SuccessFactors 管理入口**身為系統管理員。
    
8. 造訪 [應用程式安全性] 和原生 [單一登入功能]。 

9. 在 [重設權杖] 中放入任何值，然後按一下 [儲存權杖] 以啟用 SAML SSO。
   
    ![在應用程式端設定單一登入][11]

    > [!NOTE] 
    > 使用此值會作為 on/off 開關。 如果儲存了任何值，SAML SSO 為 ON。 如果儲存了空白值，SAML SSO 為 OFF。

10. 原生下列螢幕擷取畫面，並執行下列動作：
   
    ![在應用程式端設定單一登入][12]
   
    a. 選取 [SAML v2 SSO] 選項按鈕
   
    b. 設定**SAML 判斷提示的合作對象名稱**（例如，SAML 簽發者 + 公司名稱）。
   
    c. 在**簽發者 URL**文字方塊中，貼上**SAML 實體識別碼**您從 Azure 入口網站複製的值。
   
    d. 選取 [回應 (客戶產生的/IdP/AP)] 做為 [需要必要簽章]。
   
    e. 選取 [啟用] 做為 [啟用 SAML 旗標]。
   
    f. 選取 [否] 做為 [登入要求簽章 (SF 產生的/SP/RP)]。
   
    g. 選取 [瀏覽器/後置設定檔] 做為 [SAML 設定檔]。
   
    h. 選取 [否] 做為 [強制執行憑證有效期間]。
   
    i. 從 Azure 入口網站下載的憑證檔案的內容複製並貼到**SAML 驗證憑證**文字方塊。

    > [!NOTE] 
    > 憑證內容必須有開始憑證和結束憑證標籤。

11. 瀏覽至 [SAML V2]，然後執行下列步驟：
   
    ![在應用程式端設定單一登入][13]
   
    a. 選取 [是] 做為 [支援 SP 起始的全域登出]。
   
    b. 在**全域登出服務 URL （LogoutRequest 目的地）**文字方塊中，貼上**登出 URL**已複製的值形成 Azure 入口網站。
   
    c. 選取 [否] 做為 [要求 SP 必須加密所有 NameID 元素]。
   
    d. 選取 [未指定] 做為 [NameID 格式]。
   
    e. 選取 [是] 做為 [啟用 SP 起始的登入 (AuthnRequest)]。
   
    f. 在**做全公司的簽發者傳送要求**文字方塊中，貼上**SAML 單一登入服務 URL**您從 Azure 入口網站複製的值。

12. 執行這些步驟，如果您想要讓登入使用者名稱不區分大小寫。
   
    ![設定單一登入][29]
    
    a. 造訪 [公司設定] \(靠近底部)。
   
    b. 選取 [啟用不區分大小寫使用者名稱] 附近的核取方塊。
   
    c. 按一下 [儲存]。
   
    > [!NOTE] 
    > 如果您嘗試啟用此功能時，系統會檢查它會建立重複的 SAML 登入名稱。 例如，如果客戶有 User1 和 user1 的使用者名稱。 取消區分大小寫功能將會讓這些名稱重複。 系統提供的錯誤訊息，並不會啟用此功能。 客戶必須變更其中一個使用者名稱，讓它的拼字不同。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。

    ![Azure Active Directory 按鈕](./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png)

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png)

3. 若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。

    ![[新增] 按鈕](./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png)

4. 在 [使用者] 對話方塊中，執行下列步驟：

    ![[使用者] 對話方塊](./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png)

    a. 在 [名稱] 方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。

    c. 選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。

    d. 按一下頁面底部的 [新增] 。
 
### <a name="create-a-successfactors-test-user"></a>建立 SuccessFactors 測試使用者

若要讓 Azure AD 使用者能夠登入 SuccessFactors，它們必須佈建到 SuccessFactors。  
SuccessFactors 需以手動方式佈建。

若要在 SuccessFactors 建立使用者，您需要連絡 [SuccessFactors 支援小組](https://www.successfactors.com/en_us/support.html)。

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，以啟用要使用 Azure 單一登入授與存取權給 SuccessFactors 許 Simon。

![指派使用者角色][200] 

**若要將 Britta Simon 指派到 SuccessFactors，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [SuccessFactors] 。

    ![應用程式清單中的 [SuccessFactors] 連結](./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_app.png)  

3. 在左側功能表中，按一下 [使用者和群組]。

    ![[使用者和群組] 連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![[新增指派] 窗格][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在存取面板中按一下 [SuccessFactors] 圖格時，應該會自動登入您的 SuccessFactors 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png

[100]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_203.png

