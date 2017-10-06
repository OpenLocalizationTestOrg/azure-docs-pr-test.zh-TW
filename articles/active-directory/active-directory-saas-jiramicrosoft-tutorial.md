---
title: "教學課程：Azure Active Directory 與 JIRA SAML SSO by Microsoft 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和 microsoft JIRA SAML SSO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a>教學課程：Azure Active Directory 與 JIRA SAML SSO by Microsoft 整合

在此教學課程中，您學會如何 toointegrate JIRA SAML SSO 由 Microsoft Azure Active directory (Azure AD)。

與 Azure AD 整合 microsoft JIRA SAML SSO 可以提供下列優點 hello:

- 您可以控制存取 tooJIRA SAML SSO 的 Microsoft Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooJIRA SAML SSO （單一登入） 的 microsoft 使用他們的 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure JIRA SAML SSO 的 Microsoft Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- JIRA 伺服器應用程式安裝在 Windows 64 位元伺服器 （在內部部署或 hello 雲端 IaaS 基礎結構上）
- JIRA 伺服器已啟用 HTTPS
- 注意 hello 支援版本 JIRA 外掛程式 區段下方所述。
- JIRA 伺服器可連線網際網路上特別 tooAzure AD 登入頁面上進行驗證，應能 tooreceive hello 從 Azure AD 權杖
- JIRA 中已設定管理員認證
- JIRA 中已停用 WebSudo
- 測試在 hello JIRA 伺服器應用程式中建立使用者

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用 JIRA 的實際執行環境。 開發，或預備環境的 hello 應用程式，然後使用 hello 實際執行環境中的第一次測試 hello 整合。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="supported-versions-of-jira"></a>支援的 JIRA 版本 

目前支援下列 JIRA 版本：

- JIRA 核心和軟體： 6.0 too7.2.0
- JIRA 服務台： 3.0 too3.2

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 新增 microsoft JIRA SAML SSO 從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a>新增 microsoft JIRA SAML SSO 從 hello 組件庫
tooconfigure hello 整合 microsoft JIRA SAML SSO 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd microsoft JIRA SAML SSO。

**tooadd hello 庫、 microsoft JIRA SAML SSO 執行 hello 下列步驟：**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**JIRA SAML SSO microsoft**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. 在 hello 結果 窗格中，選取**microsoft JIRA SAML SSO**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 JIRA SAML SSO by Microsoft 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中由 Microsoft JIRA SAML SSO 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者和 microsoft JIRA SAML SSO 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

由 Microsoft JIRA SAML SSO 中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 JIRA SAML SSO 的 Microsoft Azure AD 單一登入，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立由 Microsoft 測試使用者 JIRA SAML SSO](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave 許 Simon JIRA SAML SSO 由 Microsoft 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您 JIRA SAML SSO 中由 Microsoft 應用程式。

**使用 JIRA SAML SSO 的 Microsoft Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**

1. 在 Azure 入口網站上 hello hello **microsoft JIRA SAML SSO**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. 在 hello **JIRA SAML SSO 的 Microsoft 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<domain:port>/plugins/servlet/saml/auth`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<domain:port>/`

    c. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。 如果連接埠是具名 URL，則為選擇性。 Hello Jira 外掛程式，在 hello 教學課程稍後會說明設定期間，會收到這些值。
 
4. toogenerate hello**中繼資料**url，請執行下列步驟的 hello:

    a. 按一下 [應用程式註冊]。
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    b. 按一下**端點**tooopen**端點** 對話方塊。  
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    c. 按一下 hello 複製按鈕 toocopy**同盟中繼資料文件**url 並將它貼到 [記事本]。
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    d. 現在請 toohello 屬性頁的**JIRA SAML SSO microsoft**和複製 hello**應用程式識別碼**使用**複製**按鈕，並將它貼到 [記事本]。
 
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    e. 產生 hello**中繼資料 URL**使用 hello 下列模式：`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`並將此值複製 [記事本] 中，因為它正使用更新版本的 hello 外掛程式 hello 組態。

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. 請連絡[Microsoft](mailto:waadpartners@microsoft.com)以 hello 下列 hello JIRA 外掛程式的資訊。
    
    *   客戶名稱：
    *   主要網域名稱：
    *   Azure AD Premium： 是/否 （外掛程式將使用 tooall hello 客戶 Free、 Basic 和 Premium SKU）
    *   將會使用這項整合的使用者數目：
    *   JIRA 版本：
    *   註解：

7. 在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour JIRA 執行個體。

8. 將滑鼠停留在齒輪，然後按一下 hello**附加元件**。
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. 在 [附加元件] 索引標籤區段下，按一下 [管理附加元件]。

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. 手動上傳 hello 由 Microsoft 提供的外掛程式。 Hello 外掛程式安裝之後，它會出現在**使用者安裝**附加元件區段**管理附加元件**> 一節。

11. 按一下**設定**tooconfigure hello 新的外掛程式。

12. 在設定頁面上執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    a. 在**中繼資料 URL**貼上 hello**中繼資料 URL**從 Azure AD 產生，並按一下 hello**解決** 按鈕。 它會讀取 hello IdP 中繼資料 URL，並於其中填入 hello 欄位的所有資訊。

    > [!Note]
    > 預設 SAML 使用者識別碼位置是名稱識別碼。 您可以變更這個 tooan 屬性選項，然後輸入 hello 適當的屬性名稱。

    > [!TIP]
    > 確定只有一個對應 hello 應用程式，使其解析 hello 中繼資料中沒有任何錯誤的憑證。 如果有多個憑證，在解析 hello 中繼資料，系統管理員取得發生錯誤。
    
    b. 複製 hello**識別碼、 回覆 URL 和登入 URL**值並貼在**識別碼、 回覆 URL 和登入 URL**文字方塊分別以**JIRA SAML SSO 的 Microsoft 網域和 Url** Azure 入口網站上的一節。

    c. 在**登入按鈕名稱**類型 hello 名稱的按鈕，您的組織希望 hello 使用者 toosee 登入畫面上的。

    d. 在**SAML 使用者識別碼位置**選取**hello 的 hello Subject 陳述式的 NameIdentifier 元素中的使用者識別碼是**或**屬性項目中的使用者識別碼是**。  此識別碼具有 toobe hello JIRA 使用者識別碼。如果不符合 hello 使用者識別碼，系統將不會允許使用者 toolog 中。 
    
    e. 如果您選取**屬性項目中的使用者識別碼是**選項，然後在**屬性名稱**文字方塊類型 hello 屬性名稱的 hello 卻使用者識別碼。 

    f. 如果您正在使用 Azure AD 的 hello （例如 ADFS 等等） 的同盟的網域，然後按一下 上 hello**啟用主領域探索**選項，並設定 hello**網域名稱**。
    
    g. 在**網域名稱**hello 網域在此輸入名稱發生 hello ADFS 為基礎的登入。

    h. 請檢查**啟用單一登出**如果您想從 Azure AD，當使用者登出從 JIRA toolog 出。 

    i. 按一下**儲存**按鈕 toosave hello 設定。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a>建立 JIRA SAML SSO by Microsoft 測試使用者

tooenable Azure AD 使用者 toolog tooJIRA 在內部部署伺服器，您必須佈建到 JIRA SAML SSO microsoft。 對於 JIRA SAML SSO by Microsoft，佈建是手動工作。

**tooprovision 使用者帳戶，執行下列步驟的 hello:**

1. 登入 tooyour JIRA 在內部部署伺服器以系統管理員。

2. 將滑鼠停留在齒輪，然後按一下 hello**使用者管理**。

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. 您會重新導向的 tooAdministrator 存取頁面 tooenter**密碼**按一下**確認** 按鈕。

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. 在 [使用者管理] 索引標籤區段下，按一下 [建立使用者]。

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. 在 hello **「 建立新的使用者 」**對話方塊頁面上，執行下列步驟的 hello:

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    a. 在 hello**電子郵件地址**文字方塊中，輸入 hello 電子郵件地址的使用者喜歡Brittasimon@contoso.com。

    b. 在 hello**全名**文字方塊中，例如許 Simon 的 hello 使用者類型完整名稱。

    c. 在 hello **Username**文字方塊中，型別 hello 電子郵件的使用者要Brittasimon@contoso.com。

    d. 在 hello**密碼**文字方塊中，輸入 hello 密碼的使用者。

    e. 按一下 [建立使用者]。   

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooJIRA SAML SSO 由 Microsoft 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooJIRA microsoft SAML SSO 執行 hello 下列步驟：**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**JIRA SAML SSO microsoft**。

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello JIRA SAML SSO 由 Microsoft 磚 hello 存取面板中時，您應該取得自動登入 tooyour JIRA SAML SSO 的 Microsoft 應用程式。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

