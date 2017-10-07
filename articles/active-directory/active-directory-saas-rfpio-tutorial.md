---
title: "教學課程：Azure Active Directory 與 RFPIO 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 RFPIO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>教學課程：Azure Active Directory 與 RFPIO 整合

在此教學課程中，您學會如何 toointegrate RFPIO 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 RFPIO 可以提供下列優點 hello:

- 您可以控制誰能夠存取 tooRFPIO Azure AD 中。
- 您可以啟用您的使用者 tooautomatically get 登入 tooRFPIO （單一登入） 具有其 Azure AD 帳戶。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure RFPIO 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶。
- 已啟用 RFPIO 單一登入的訂用帳戶。

> [!NOTE]
> 我們不建議您在本教學課程使用實際執行環境 tootest hello 步驟。

tootest hello 步驟在本教學課程，請遵循下列建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 此教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 加入 RFPIO 從 hello 組件庫。
2. 設定並測試 Azure AD 單一登入。

## <a name="add-rfpio-from-hello-gallery"></a>從 hello 圖庫新增 RFPIO
tooconfigure hello 整合 RFPIO 到 Azure AD，您需要 tooadd RFPIO hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO 從 hello 組件庫

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，在 hello 左側的導覽窗格中，選取 hello **Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 選取 [企業應用程式]，然後選取 [所有應用程式]。

    ![應用程式][2]
    
3. tooadd 新的應用程式中，選取 hello**新的應用程式**上 hello 對話方塊頂端的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**RFPIO**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. 在 hello 結果 窗格中，選取  **RFPIO**，然後選取 hello**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 RFPIO 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow RFPIO 中的對等項目的使用者與 Azure AD 中的使用者之間是什麼 hello 關聯性。 換句話說，Azure AD 使用者與 hello RFPIO 中相關的使用者之間的連結關聯性需要 toobe 建立。

RFPIO 中, 指派的 hello 值**使用者名**做為 hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 RFPIO 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)**-tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#creating-an-azure-ad-test-user)**-許 Simon 與 Azure AD 單一登入 tootest。
3. **[建立測試使用者 RFPIO](#creating-a-rfpio-test-user)**  -toohave 許 Simon RFPIO 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assigning-the-azure-ad-test-user)**-tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 如果 hello 設定可正常運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 RFPIO 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 RFPIO，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **RFPIO**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. 在 hello **RFPIO 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    a. 在 hello**識別碼**文字方塊中，型別 hello URL:`https://www.rfpio.com`

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b.這是另一個 C# 主控台應用程式。 按一下 [顯示進階 URL 設定]。

    c. 在 hello**轉送狀態**文字方塊中輸入的字串值。 請連絡[RFPIO 支援小組](https://www.rfpio.com/contact/)tooget 此值。 

4. 按一下 [顯示進階 URL 設定]。 如果您想 tooconfigure hello 應用程式中的**SP**初始模式：   

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    在 hello**登入 URL**文字方塊中，型別 hello URL:`https://www.app.rfpio.com`

5. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. 在不同的網頁瀏覽器視窗中，登入 toohello **RFPIO**身為系統管理員的網站。

8. 按一下 hello 底部左上的角的下拉式清單。

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. 按一下 hello**組織設定**。 

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. 按一下 hello**功能和整合**。

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. 在 hello **SAML SSO 設定**按一下**編輯**。

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. 在本節中執行下列動作：

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    a. 複製的 hello hello 內容**下載中繼資料 XML**並將它貼到 hello**身分識別組態**欄位。

    > [!NOTE]
    >toocopy hello 內容的下載**中繼資料 XML**使用**記事本 + +**或適當**XML 編輯器**。 

    b. 按一下 [驗證] 。

    c. 按一下之後**驗證**、 翻轉**SAML(Enabled)** tooon。

    d. 按一下 [提交] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="create-a-rfpio-test-user"></a>建立 RFPIO 測試使用者

tooenable Azure AD 使用者 toolog 中 tooRFPIO，它們必須佈建到 RFPIO。  
中的 RFPIO hello 案例中，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟的 hello:**

1. 登入 tooyour RFPIO 公司網站的系統管理員身分。

2. 按一下 hello 底部左上的角的下拉式清單。

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. 按一下 hello**組織設定**。 

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. 按一下 [小組成員]。

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. 按一下 [新增成員]。

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. 在 hello**加入新成員**> 一節。 執行下列動作：

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app8.png)

    a. Enter**電子郵件地址**在 hello**輸入每行一個電子郵件**欄位。

    b. 請根據您的需求選取 [角色]。

    c. 按一下[新增成員]。
        
    > [!NOTE]
    > hello Azure Active Directory 帳戶持有者會收到一封電子郵件，並且遵循連結 tooconfirm 他們的帳戶之前就會生效。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooRFPIO 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooRFPIO，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**RFPIO**。

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您 Azure AD 單一登入組態使用測試 hello 存取面板。

當您按一下的 hello RFPIO 磚 hello 存取面板中時，您應該取得自動登入 tooyour RFPIO 應用程式。
如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [教學課程有關清單 toointegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

