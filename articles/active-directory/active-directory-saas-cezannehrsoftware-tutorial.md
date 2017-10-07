---
title: "教學課程：Azure Active Directory 與 Cezanne HR Software 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Cezanne HR 軟體之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>教學課程：Azure Active Directory 與 Cezanne HR Software 整合

在此教學課程中，您學會如何 toointegrate Cezanne HR 軟體與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Cezanne HR 軟體可以提供下列優點 hello。 您可以：

- 在 Azure AD 中擁有存取 tooCezanne 控制 HR 軟體。
- 可讓您的使用者 tooautomatically 登入 tooCezanne HR 軟體搭配單一登入 (SSO) 與 Azure AD 帳戶。
- 管理您的帳戶，在單一中央位置： hello Azure 入口網站。

toolearn 進一步了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合，請參閱[什麼是應用程式存取及 SSO 與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 Cezanne HR software 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Cezanne HR Software SSO 的訂用帳戶

> [!NOTE]
> tootest hello 步驟在本教學課程，我們建議您不要使用實際執行環境。

tootest hello 步驟在本教學課程，請遵循下列建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD SSO。 

本教學課程所述的 hello 案例包含兩個主要建置組塊：

* 從 hello 圖庫加入 Cezanne HR 軟體
* 設定並測試 Azure AD SSO

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>從 hello 圖庫新增 Cezanne HR 軟體
tooconfigure hello 整合 Cezanne HR 軟體到 Azure AD 中，從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單加入 Cezanne HR 軟體。

tooadd Cezanne HR 軟體 hello 圖庫中，從 hello 遵循：

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，在 [hello 左的窗格中選取 hello **Azure Active Directory** ] 按鈕。 

    ![hello"Azure Active Directory"的按鈕][1]

2. 選取 [企業應用程式] > [所有應用程式]。

    ![hello [所有應用程式] 連結][2]
    
3. 新的應用程式，在 hello hello 頂端 tooadd**所有應用程式**對話方塊中，選取**新的應用程式**。

    ![hello 「 新的應用程式 」 按鈕][3]

4. 在 [hello] 搜尋方塊中，輸入**Cezanne HR 軟體**。

    ![hello 搜尋方塊](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. 在 [hello 結果清單中，選取 [ **Cezanne HR 軟體**]，然後選取 [hello**新增**按鈕 tooadd hello 應用程式。

    ![hello 結果清單](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Cezanne HR Software 搭配運作的 Azure AD SSO。

SSO toowork Azure AD 需要 tooknow hello Cezanne HR 軟體對等項目的 toohello Azure AD 使用者。 換句話說，您必須建立 Azure AD 使用者與 hello 相關的使用者之間的連結關聯性中 hello Cezanne HR 軟體。

tooestablish hello 連結關聯性，指派 hello Cezanne HR 軟體**使用者名**值為 hello Azure AD **Username**值。

tooconfigure 和測試 Azure AD SSO 使用 Cezanne HR 軟體，完成下列建置組塊的 hello。

### <a name="configure-azure-ad-sso"></a>設定 Azure AD SSO

本節中，您可以在 hello Azure 入口網站中啟用 Azure AD 的 SSO 及 Cezanne HR 軟體應用程式中設定 SSO，藉由 hello 下列：

1. 在 Azure 入口網站上 hello hello **Cezanne HR 軟體**應用程式整合頁面上，選取**單一登入**。

    ![hello 「 單一登入 」 的命令][4]

2. 在 [hello tooenable SSO，**單一登入**對話方塊中，選取 hello**模式**做為**SAML 型登入**。
 
    ![hello [模式] 方塊](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. 在下**Cezanne HR 軟體網域和 Url**，請勿遵循 hello:

    ![hello"Cezanne HR 軟體網域和 Url 」 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. 在 [hello**登入 URL**方塊中，輸入 URL，請使用下列語法已經 hello:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. 在 [hello**回覆 URL**方塊中，輸入 URL，請使用下列語法已經 hello:`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > hello 上述值不是實際。 Hello 實際的回覆 URL 與 hello 登入 URL 加以更新。 tooobtain hello 值，請連絡 hello [Cezanne HR 軟體用戶端支援小組](mailto:info@cezannehr.com)。

4. 在下**SAML 簽章憑證**，選取**憑證 (Base64)**，然後儲存您的電腦上的 hello 憑證檔案。

    ![hello 「 SAML 簽章憑證 」 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. 選取 [ **儲存**]。

    ![hello [儲存] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. 在下**Cezanne HR 軟體組態**，選取**設定 Cezanne HR 軟體**tooopen hello**設定登入**視窗。 複製 hello **SAML 實體識別碼**和**SAML 單一登入服務**URL 從 hello**快速參考**> 一節。

    ![hello"Cezanne HR 軟體組態 > 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. 在不同的網頁瀏覽器視窗中，登入 tooyour Cezanne HR software 租用戶系統管理員身分。

8. Hello 左窗格中，選取**系統安裝**。 選取 [安全性設定] > [單一登入設定]。

    ![hello 「 單一登入設定 」 連結](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. 在 [hello**允許使用者 toolog 中使用下列單一登入 (SSO) 服務的 hello**窗格中，選取 hello **SAML 2.0**核取方塊並選取 hello**進階組態**選項。

    ![單一登入服務選項](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. 選取 [新增]。

    ![hello"新增] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. 在下**SAML 2.0 身分識別提供者**，請勿遵循 hello:

    ![hello < SAML 2.0 身分識別提供者 > 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. 在 [hello**顯示名稱**方塊中，輸入您的身分識別提供者的 hello 名稱。

    b. 在 [hello**實體識別碼**方塊中，貼上 hello **SAML 實體識別碼**從 hello Azure 入口網站中複製。 

    c. 在 [hello **SAML 繫結**清單方塊中，選取**POST**。

    d. 在 [hello**安全性權杖服務端點**方塊中，貼上 hello **SAML 單一登入服務**您所複製的 hello Azure 入口網站的 URL。 
    
    e. 在 [hello**使用者 ID 的屬性名稱**方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`。
    
    f. tooupload hello 從 Azure AD 中，選取 hello 下載憑證**上傳**] 按鈕。
    
    g. 選取 [確定] 。 

12. 選取 [ **儲存**]。

    ![hello [儲存] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> 當您設定 hello 應用程式時，您可以閱讀 hello hello 中前面指示的精簡版本[Azure 入口網站](https://portal.azure.com)。 從 hello 新增 hello 應用程式之後**Active Directory** > **企業應用程式**區段中，選取 hello**單一登入**] 索引標籤。然後存取 hello 內嵌文件從 hello**組態**> 一節。 

toolearn 進一步了解 hello embedded 文件功能，請參閱[Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
在本節中，您可以建立測試使用者許 Simon hello Azure 入口網站中。

![hello 許 Simon 的測試使用者][100]

在 Azure AD 中的測試使用者 toocreate hello 遵循：

1. 在 [hello **Azure 入口網站**，在 [hello 左的窗格中選取 hello **Azure Active Directory** ] 按鈕。

    ![hello"Azure Active Directory"的按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，選取**使用者和群組** > **所有使用者**。
    
    ![hello，"All users"連結](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    hello**所有使用者**對話方塊隨即開啟。

3. tooopen hello**使用者**對話方塊中，選取**新增**。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊方塊中，執行下列 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**方塊中，輸入使用者許 Simon 的**電子郵件地址**。

    c. 選取 hello**顯示密碼**核取方塊，然後注意 hello 值所產生的 hello**密碼**方塊。

    d. 選取 [ **建立**]。
 
### <a name="create-a-cezanne-hr-software-test-user"></a>建立 Cezanne HR Software 測試使用者

tooenable Azure AD 使用者 toosign tooCezanne HR 軟體，您必須佈建到 Cezanne HR 軟體。 中的 Cezanne HR 軟體 hello 案例中，佈建須手動進行。

佈建使用者帳戶，藉由下列 hello:

1.  Tooyour Cezanne HR software 公司網站管理員身分登入。

2.  Hello 左窗格中，選取**系統安裝** > **管理使用者** > **新增使用者**。

    ![hello [加入新使用者] 連結](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "新使用者")

3.  在下**人員詳細資料**，請勿遵循 hello:

    ![hello < 人員詳細資料 > 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "新使用者")
    
    a. 將 [內部使用者] 設為 [OFF]。
    
    b. 在 [hello**名字**方塊中，型別 hello 使用者的名字，例如**許**。  
 
    c. 在 [hello**姓氏**方塊中，型別 hello 使用者的姓氏，例如**Simon**。
    
    d. 在 [hello**電子郵件**方塊中，輸入 hello 使用者的電子郵件地址，例如Brittasimon@contoso.com。

4.  在下**帳戶資訊**，請勿遵循 hello:

    ![hello 」 帳戶資訊 > 一節](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "新使用者")
    
    a. 在 [hello **Username**方塊中，輸入 hello 使用者的電子郵件地址，例如Brittasimon@contoso.com。
    
    b. 在 [hello**密碼**方塊中，輸入 hello 使用者的密碼。
    
    c. 在 [hello**安全性角色**方塊中，選取**HR Professional**。
    
    d. 選取 [確定] 。

5. 在 [hello**單一登入**索引標籤上，在 [hello **SAML 2.0 識別碼**區段中，選取**加入新**。

    ![hello"新增"按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "使用者")

6. 在 [hello**身分識別提供者**清單方塊中，選取您的身分識別提供者。 在 [hello**使用者識別碼**方塊中，輸入測試使用者許 Simon 的帳戶 hello 電子郵件地址。

    ![hello 「 身分識別提供者 」 和 「 使用者識別碼 」 方塊](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "使用者")
    
7. 選取 [ **儲存**]。

    ![hello [儲存] 按鈕](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "使用者")

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooCezanne HR 軟體啟用測試使用者許 Simon toouse Azure SSO。

![測試使用者存取][200] 

1. 在 [hello Azure 入口網站，開啟 hello 應用程式檢視並前往 toohello 目錄檢視。 選取 [企業應用程式] > [所有應用程式]。

    ![hello [所有應用程式] 連結][201] 

2. 在 [hello] 應用程式清單中，選取**Cezanne HR 軟體**。

    ![hello"應用程式] 清單](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. 在左側 hello hello 功能表中選取**使用者和群組**。

    ![指派使用者][202] 

4. 選取 [新增] 。 接著在 hello**將作業加入**對話方塊中，選取**使用者和群組**。

    ![[使用者和群組] 連結][203]

5. 在 [hello**使用者和群組**對話方塊中的，在 hello**使用者**清單中，選取**許 Simon**。

6. 在 [hello**使用者和群組**對話方塊中，選取**選取**。

7. 在 [hello**將作業加入**對話方塊中，選取**指派**。
    
### <a name="test-sso"></a>測試 SSO

本節中，在中，您可以測試您的 Azure AD 的 SSO 組態使用 hello 存取面板。

當您選取 hello Cezanne HR 軟體磚 hello 存取面板中時，您登入自動 tooyour Cezanne HR 軟體應用程式。

## <a name="next-steps"></a>後續步驟

* [如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

