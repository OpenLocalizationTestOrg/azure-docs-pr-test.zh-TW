---
title: "教學課程：Azure Active Directory 與 Small Improvements 整合| Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間些許進步。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a>教學課程：Azure Active Directory 與 Small Improvements 整合

在此教學課程中，您學會如何 toointegrate 些許進步與 Azure Active Directory (Azure AD)。

與 Azure AD 整合些許進步可以提供下列優點 hello:

- 您可以控制存取 tooSmall 增強功能的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooSmall （單一登入） 的增強功能與他們的 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 小型的增強功能的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Small Improvements 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入小型的增強功能
2. 設定並測試 Azure AD 單一登入

## <a name="adding-small-improvements-from-hello-gallery"></a>從 hello 圖庫加入小型的增強功能
tooconfigure hello 整合些許進步到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 些許進步。

**tooadd 些許進步 hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**些許進步**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. 在 hello 結果 窗格中，選取 **些許進步**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Small Improvements 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 對應項目小提升的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 些許進步中相關的使用者之間的連結關聯性需要 toobe 建立。

在小型的增強功能，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 和測試 Azure AD 單一登入小的增強功能，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立小型的增強功能的測試使用者](#creating-a-small-improvements-test-user)** -toohave 許 Simon 小改進項目是連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並些許進步應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入小的增強功能，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello**些許進步**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. 在 hello**小型改進網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.small-improvements.com`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.small-improvements.com`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[小改善用戶端支援小組](mailto:support@small-improvements.com)tooget 這些值。 
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. 在 hello**小改進組態**區段中，按一下**設定些許進步**tooopen**設定登入**視窗。 複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. 在另一個瀏覽器視窗中，系統管理員身分登入 tooyour 些許進步公司網站。

8. 從 hello 主要儀表板] 頁面上，按一下 [**管理**hello 左邊的按鈕。
   
    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. 按一下 hello **SAML SSO**按鈕**整合**> 一節。
   
    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. 在 hello SSO 安裝程式 頁面上，執行下列步驟的 hello:
   
    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    a. 在 hello **HTTP 端點**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。

    b. 開啟 [記事本]，複製 hello 內容，您所下載的憑證，然後將它貼到 hello **x509 憑證**文字方塊。 

    c. 如果您想 toohave SSO 與登入表單驗證 選項可供使用者，然後檢查 hello**太啟用透過登入/密碼存取**選項。  

    d. 輸入 hello 適當的值 tooName hello SSO 登入按鈕在 hello **SAML 提示**文字方塊。  

    e. 按一下 [儲存] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-small-improvements-test-user"></a>建立 Small Improvements 的測試使用者

tooenable Azure AD 使用者 toolog 中 tooSmall 增強功能，它們必須佈建到些許進步。 中的些許進步 hello 案例中，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟的 hello:**

1. 以系統管理員身分登入 tooyour 些許進步公司網站。

2. Hello 首頁上，繼續保持 hello toohello 功能表中，按一下**管理**。

3. 按一下 hello**使用者目錄**從使用者管理 區段中的按鈕。 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. 按一下 [新增使用者]。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. 在 [hello**新增使用者**] 對話方塊中，執行下列步驟的 hello: 

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    a. 輸入 hello**名字**類似使用者的**許**。

    b. 輸入 hello**姓氏**類似使用者的**Simon**。

    c. 輸入 hello**電子郵件**類似使用者的 **brittasimon@contoso.com** 。 

    d. 您也可以選擇 tooenter hello 個人訊息在 hello**傳送通知電子郵件**方塊。 如果您不想 toosend hello 通知，然後取消核取此核取方塊。

    e. 按一下 [建立使用者] 。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

本節中，在您啟用 Azure 單一登入許 Simon toouse tooSmall 改進授與存取權。

![指派使用者][200] 

**tooassign 許 Simon tooSmall 增強功能，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**些許進步**。

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。  

當您按一下的 hello 些許進步磚 hello 存取面板中時，您應該取得自動登入 tooyour 些許進步應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

