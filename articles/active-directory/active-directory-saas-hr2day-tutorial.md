---
title: "教學課程：Azure Active Directory 與 HR2day by Merces 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與由 Merces HR2day 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>教學課程：Azure Active Directory 與 HR2day by Merces 整合

在此教學課程中，您學會如何 toointegrate HR2day 由 Merces 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合所 Merces HR2day 可以提供下列優點 hello:

- 您可以控制存取 tooHR2day Merces 由 Azure AD 中。
- 您可以啟用 tooautomatically 取得登入 tooHR2day Merces 其 Azure AD 帳戶與您的使用者。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如需 SaaS 應用程式與 Azure AD 整合的詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure HR2day Merces 所使用的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶。
- 已啟用 HR2day by Merces 單一登入的訂用帳戶。

> [!NOTE]
> 我們不建議使用實際執行環境 tootest hello 本教學課程中的步驟。

tootest hello 步驟在本教學課程，請遵循下列建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD，可取得 [Azure AD 一個月免費試用版](https://azure.microsoft.com/pricing/free-trial/)。  

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 此處概述的 hello 案例包含兩個主要建置組塊：

1. 新增由 Merces HR2day 從 hello 組件庫。
2. 設定並測試 Azure AD 單一登入。

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>從 hello 圖庫新增由 Merces HR2day
tooconfigure hello 整合由 Merces HR2day 到 Azure AD 中，加入所 Merces HR2day hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd HR2day Merces hello 圖庫中，從所採取下列步驟的 hello:**

1. 在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，選取 hello **Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 跳過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新的應用程式中，選取 hello**新的應用程式**hello 頂端 hello 對話方塊上的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**由 Merces HR2day**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. 在 hello 結果 窗格中，選取**由 Merces HR2day**，然後選取 hello**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 HR2day by Merces 搭配運作的 Azure AD 單一登入。

Azure AD 單一登入 toowork，需要 tooknow 負責 hello 對等項目的使用者中由 Merces HR2day tooa 使用者在 Azure AD 中。 換句話說，您需要 tooestablish Azure AD 使用者與 hello 由 Merces HR2day 中相關的使用者之間的連結。

在由 Merces HR2day，將指派 hello**使用者名稱**在 Azure AD 中太**Username** tooestablish hello 關聯性。

tooconfigure 及測試 HR2day Merces 由 Azure AD 單一登入，您必須遵循的建置組塊 toocomplete hello:

1. [設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)： 啟用使用者 toouse 這項功能。
2. [建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)：使用 Britta Simon 測試 Azure AD 單一登入。
3. [建立由 Merces 測試使用者 HR2day](#creating-an-hr2day-by-merces-test-user)： 在由是連結的 toohello Azure AD 使用者表示法的 Merces HR2day 建立許 Simon 對應項目。
4. [指派給 Azure AD hello 測試使用者](#assigning-the-azure-ad-test-user)： 啟用許 Simon toouse Azure AD 單一登入。
5. [測試單一登入](#testing-single-sign-on)： 驗證是否 hello 設定可正常運作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入在您 HR2day Merces 應用程式。

**tooconfigure Azure AD 單一登入與 HR2day 由 Merces，採取下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello**由 Merces HR2day**應用程式整合頁面上，選取**單一登入**。

    ![設定單一登入][4]

2. tooenable 單一登入，在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**。
 
    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. 在 hello **Merces 網域和 Url HR2day**區段中，採取下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. 在 hello**登入 URL**方塊中，輸入 URL，使用下列模式的 hello: `https://<tenantname>.force.com/<instancename>`。

    b. 在 hello**識別碼**方塊中，輸入 URL，使用下列模式的 hello: `https://hr2day.force.com/<companyname>`。

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與 hello 實際登入 URL 和識別碼。 連絡 hello [Merces 用戶端支援小組 HR2day](mailto:servicedesk@merces.nl) tooget 這些值。 
 


4. 在 hello **SAML 簽章憑證**區段中，選取**Certificate(Base64)**，然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. 本章節描述如何 tooenable 使用者 tooauthenticate tooHR2day 由 Merces 與 Azure AD 的帳戶。 他們這麼做，使用 hello SAML 通訊協定為基礎的同盟。

    您 HR2day Merces 應用程式所預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML 權杖。 hello 下列螢幕擷取畫面顯示此動作的範例。 

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    您可以設定 hello SAML 判斷提示之前，您必須連絡 hello [Merces 用戶端支援小組 HR2day](mailto:servicedesk@merces.nl)並要求您的租用戶 hello hello 唯一識別碼屬性值。 您需要此值 toocomplete hello 中的步驟 hello 下一節。 

6. 在 hello**單一登入**對話方塊中的，在 hello**使用者屬性**區段中，設定 hello SAML 權杖屬性 hello 下列影像所示。 接著採取下列步驟的 hello。
    
      | 屬性名稱    |   屬性值 |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | join([mail],"102938475Z","@" |
    
      a. tooopen hello**加入屬性**對話方塊中，選取**加入屬性**。

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. 在 hello**名稱**方塊中，輸入**ATTR_LOGINCLAIM**。

    c. 從 hello**值**清單中，選取**join （)**。

    d. 從 hello **String1**清單中，選取**user.mail**。

    e. 如**String2**，輸入 hello HR2day 小組所提供的唯一識別碼。

    f. 在 hello**分隔符號**方塊中，輸入 **@** 。
    
    g. 選取 [確定]。

7. 選取 hello**儲存** 按鈕。

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. 在 hello **HR2day Merces 組態**區段中，選取**設定 HR2day Merces 所**tooopen hello**設定登入**視窗。 複製 hello**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL**從 hello**快速參考**> 一節。

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. 您的應用程式，請連絡 hello tooconfigure SSO [Merces 用戶端支援小組 HR2day](mailTo:servicedesk@merces.nl)。 附加 hello 下載**Certificate(Base64)**檔案 tooyour 電子郵件。 也提供 hello**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL** ，讓它們可以設定為 SSO 整合。

    > [!NOTE]
    >提到 toohello Merces 小組的這項整合需要 hello 與 hello 模式設定的實體識別碼 toobe **https://hr2day.force.com/INSTANCENAME**。

    > [!TIP]
    >您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  將此應用程式從 hello 後**Active Directory** > **企業應用程式**區段中，選取 hello**單一登入** 索引標籤。然後存取 hello 內嵌文件，透過 hello**組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能的 hello [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 在 Azure AD 中的測試使用者採取下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，選取 hello **Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後選取**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**對話方塊中，選取**新增**hello 最上層顯示 hello 對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊中，接受 hello 下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**] 方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**，然後記下 hello 密碼。

    d. 選取 [ **建立**]。
 
### <a name="create-an-hr2day-by-merces-test-user"></a>建立 HR2day by Merces 測試使用者

hello 本節目標在於 toocreate HR2day 中呼叫 Merces 許 Simon 的使用者。 在 hello HR2day 帳戶 tooadd hello 使用者處理 hello [Merces 用戶端支援小組 HR2day](mailto:servicedesk@merces.nl)。 

> [!NOTE]
> 若要手動 toocreate 使用者，請連絡 hello [Merces 用戶端支援小組 HR2day](mailto:servicedesk@merces.nl)。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與由 Merces 她存取 tooHR2day 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooHR2day 由 Merces，採取下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視、 移 toohello 目錄檢視，並前往太**企業應用程式**。 接著，選取 [所有應用程式]。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**由 Merces HR2day**。

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. 在左側 hello hello 功能表中選取**使用者和群組**。

    ![指派使用者][202] 

4. 選取 hello**新增** 按鈕。 然後，在 hello**將作業加入**對話方塊中，選取**使用者和群組**。

    ![指派使用者][203]

5. 在 hello**使用者和群組**對話方塊中的，在 hello**使用者**清單中，選取**許 Simon**。

6. 按一下 hello**選取** 按鈕。

7. 在 hello**將作業加入**對話方塊中，選取**指派**。
    
### <a name="test-single-sign-on"></a>測試單一登入

hello 本節的目標是 tootest 您 Azure AD 單一登入的組態使用 hello 存取面板。  

當您選取 hello HR2day 由 Merces 磚 hello 存取面板中時，您會自動取得登入 tooyour HR2day Merces 應用程式。

## <a name="additional-resources"></a>其他資源

* [教學課程有關清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

