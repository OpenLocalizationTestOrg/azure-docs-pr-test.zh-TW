---
title: "教學課程：Azure Active Directory 與 Questetra BPM Suite 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Questetra BPM Suite 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: e2515d571aa1615f14b597ef82b1087df3827f82
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>教學課程：Azure Active Directory 與 Questetra BPM Suite 整合

在本教學課程中，您將了解如何整合 Questetra BPM Suite 與 Azure Active Directory (Azure AD)。

Questetra BPM Suite 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Questetra BPM Suite 的人員。
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Questetra BPM Suite (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Questetra BPM Suite 整合，您需要以下項目：

- Azure AD 訂用帳戶
- 已啟用 Questetra BPM Suite 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二項主要的基本工作組成：

1. 從資源庫加入 Questetra BPM Suite
2. 設定和測試 Azure AD 單一登入

## <a name="add-questetra-bpm-suite-from-the-gallery"></a>從資源庫加入 Questetra BPM Suite
若要設定 Questetra BPM Suite 與 Azure AD 整合，您需要從資源庫將 Questetra BPM Suite 加入至受控 SaaS 應用程式的清單。

**若要從資源庫新增 Questetra BPM Suite，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![[應用程式]][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![[應用程式]][3]

4. 在搜尋方塊中，輸入 **Questetra BPM Suite**，從結果面板中選取 [Questetra BPM Suite]，然後按一下 [新增] 按鈕以新增應用程式。

    ![從資源庫新增](./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Questetra BPM Suite 搭配運作的 Azure AD 單一登入。

單一登入若要運作，Azure AD 必須知道 Questetra BPM Suite 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者和 Questetra BPM Suite 中的相關使用者之間建立連結關聯性。

在 Questetra BPM Suite 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要使用 Questetra BPM Suite 設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Questetra BPM Suite 測試使用者](#create-a-questetra-bpm-suite-test-user)** - 使 Questetra BPM Suite 中對應的 Britta Simon 連結到使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Questetra BPM Suite 應用程式中設定單一登入。

**若要使用 Questetra BPM Suite 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Questetra BPM Suite] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![SAML 型登入](./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_samlbase.png)

3. 在 [Questetra BPM Suite 網域與 URL] 區段上，執行下列步驟：

    ![Questetra BPM Suite 網域與 URL 區段](./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.questetra.net/saml/SSO/alias/bpm`

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.questetra.net/`

    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的「登入 URL」及「識別碼」來更新這些值。 您可以從 **Questetra BPM Suite** [SP 資訊] 區段取得這些值，本教學課程後續將會加以說明；您也可以連絡 [Questetra BPM Suite 用戶端支援小組](https://www.questetra.com/contact/)。 
 
4. 在 [SAML 簽署憑證] 區段上，按一下 [\憑證 (Base 64)\]，然後將憑證檔案儲存在您的電腦上。

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![[儲存] 按鈕](./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_400.png)

6. 在 [Questetra BPM Suite 設定] 區段上，按一下 [設定 Questetra BPM Suite] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。

    ![Questetra BPM Suite 設定區段](./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_configure.png) 

7. 在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 **Questetra BPM Suite** 公司網站。

8. 在頂端的功能表中，按一下 [系統設定] 。 
   
    ![Azure AD 單一登入][10]

9. 若要開啟 [SingleSignOnSAML] 頁面，按一下 [SSO (SAML)]。 
   
    ![Azure AD 單一登入][11]

10. 在 **Questetra BPM Suite** 公司網站的 [SP 資訊] 區段中，執行以下步驟：

    a. 從 Azure 入口網站複製 **ACS URL**，然後再貼入 [Questetra BPM Suite 網域與 URL] 區段中的 [登入 URL] 文字方塊。
    
    b. 從 Azure 入口網站複製**實體識別碼**，然後再貼入 [Questetra BPM Suite 網域與 URL] 區段中的 [識別碼] 文字方塊。

11. 在您的 **Questetra BPM Suite** 公司網站上，執行下列步驟： 
   
    ![設定單一登入][15]
   
    a. 選取 [啟用單一登入] 。
   
    b. 在 [實體識別碼] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。
    
    c. 在 [登入頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。
    
    d. 在 [登出頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。
    
    e. 在 [NameID 格式] 文字方塊中，輸入 `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`。

    f. 在從 Azure 入口網站下載的記事本檔案中開啟您的 **Base-64** 編碼憑證，將憑證的內容複製到剪貼簿，再貼到 [驗證憑證] 文字方塊。 

    g. 按一下 [檔案] 。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-questetra-bpm-suite-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-questetra-bpm-suite-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-questetra-bpm-suite-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-questetra-bpm-suite-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b. 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下頁面底部的 [新增] 。
 
### <a name="create-a-questetra-bpm-suite-test-user"></a>建立 Questetra BPM Suite 測試使用者

本節目標是在 Halogen Software 中建立名為 Questetra BPM Suite 的使用者。

**若要在 Questetra BPM Suite 中建立名為 Britta Simon 的使用者，請執行以下步驟：**

1. 以系統管理員身分登入您的 Questetra BPM Suite 公司網站。
2. 移至 [系統設定] > [使用者清單] > [新增使用者]。 
3. 在 [新增使用者] 對話方塊上，執行下列步驟： 
   
    ![建立測試使用者][300] 
   
    a. 在 [名稱] 文字方塊中，輸入使用者 **britta.simon@contoso.com** 的**名稱**。
   
    b. 在 [電子郵件] 文字方塊中，輸入使用者 **britta.simon@contoso.com** 的**電子郵件**
   
    c. 在 [密碼] 文字方塊中，輸入使用者的**密碼**。
    
    d. 按一下 [新增使用者] 。

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Questetra BPM Suite 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派到 Questetra BPM Suite，請執行以下步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Questetra BPM Suite] 。

    ![應用程式清單中的 Questetra BPM Suite](./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在 [存取面板] 中按一下 [Questetra BPM Suite] 磚時，您應該會自動登入您的 Questetra BPM Suite 應用程式。
如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png

[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_203.png
[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 

