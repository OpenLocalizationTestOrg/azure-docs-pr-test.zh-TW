---
title: "教學課程：Azure Active Directory 與 Tableau Server 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Tableau 伺服器之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a>教學課程：Azure Active Directory 與 Tableau Server 整合

在此教學課程中，您學會如何 toointegrate Tableau 伺服器與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Tableau 伺服器可以提供下列優點 hello:

- 您可以控制存取 tooTableau 伺服器的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooTableau （單一登入） 的伺服器使用其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Tableau 伺服器與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Tableau Server 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 新增 Tableau 伺服器從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-tableau-server-from-hello-gallery"></a>新增 Tableau 伺服器從 hello 組件庫
tooconfigure hello 整合 Tableau 伺服器到 Azure AD，您需要 tooadd Tableau 伺服器 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Tableau 伺服器 hello 圖庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Tableau 伺服器**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. 在 [hello [結果] 窗格中，選取 [ **Tableau 伺服器**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Tableau Server 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Tableau Server 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Tableau 伺服器中的相關的使用者之間的連結關聯性需要 toobe 建立。

Tableau Server 中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Tableau 伺服器與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Tableau 伺服器測試使用者](#creating-a-tableau-server-test-user)** -toohave 許 Simon Tableau 伺服器是連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Tableau 伺服器應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Tableau 伺服器，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Tableau 伺服器**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. 在 [hello **Tableau 伺服器網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    a. 在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://azure.<domain name>.link`
    
    b. 在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://azure.<domain name>.link`

    c. 在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://azure.<domain name>.link/wg/saml/SSO/index.html`
     
    > [!NOTE] 
    > hello 上述值不是實際值。 更新版本中，您可以更新 hello 值有 hello 實際的 URL 和從 hello Tableau 伺服器組態] 頁面上的識別項。 

4. Tableau 伺服器應用程式預期 hello SAML 判斷提示，以特定格式。 設定下列宣告為此應用程式的 hello。 您可以從 hello 管理這些屬性的 hello 值**使用者屬性 」**應用程式整合頁面上的一節。 hello 下列螢幕擷取畫面顯示 hello 的範例相同。
    
    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. 在 hello**使用者屬性**區段 hello**單一登入**] 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:
    
    | 屬性名稱 | 屬性值 |
    | ---------------| --------------- |    
    | username | *user.displayname* |

    a. 按一下**加入屬性**tooopen hello**加入屬性**對話方塊。

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    b. 在 [hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。
    
    c. 從 hello**值**清單，顯示該資料列的型別 hello 屬性值。
    
    d. 按一下 [確定]。


6. 在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS>
8. tooget SSO 設定應用程式，您需要 toosign 上 tooyour Tableau Server 租用戶系統管理員身分。
   
   a. 在 [hello Tableau 伺服器組態中，按一下 [hello **SAML** ] 索引標籤。
  
    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   b. 選取的 hello 核取方塊**使用 SAML 進行單一登入**。
   
   c. Tableau 伺服器傳回的 URL: hello Tableau Server 使用者將用來存取，例如 http://tableau_server 的 URL。 不建議使用 http://localhost。 不支援使用包含結尾斜線的 URL (例如，http://tableau_server/)。 複製**Tableau 伺服器傳回的 URL**並將它貼 tooAzure AD**登入 URL** ] 文字方塊中的**Tableau 伺服器網域和 Url** > 一節。
   
   d. SAML 實體識別碼： hello 實體識別碼可唯一識別您 Tableau 伺服器安裝 toohello IdP。 您可以輸入 Tableau 伺服器 URL 一次，如果需要，但是它並沒有 toobe Tableau 伺服器 URL。 複製**SAML 實體識別碼**並將它貼 tooAzure AD**識別碼**] 文字方塊中的**Tableau 伺服器網域和 Url** > 一節。
     
   e. 按一下 hello**匯出中繼資料檔案**在 hello 文字編輯器應用程式中開啟它。 找出判斷提示取用者服務 URL，Http Post 和索引 0 與複製 hello URL。 現在將它貼入 tooAzure AD**回覆 URL** ] 文字方塊中的**Tableau 伺服器網域和 Url** > 一節。
   
   f. 尋找您從 Azure 入口網站下載的同盟中繼資料檔案，然後將它上傳在 hello **SAML Idp 中繼資料檔案**。
   
   g. 按一下 hello**確定**hello Tableau 伺服器組態] 頁面中的按鈕。
   
    >[!NOTE] 
    >客戶有 tooupload 任何憑證 hello Tableau Server SAML SSO 設定中，它將會遭到忽略 hello SSO 資料流程中。
    >如果您需要協助 Tableau 伺服器上設定 SAML 則 toothis 發行項，請參閱[設定 SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm)。
    >
<CE>

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-tableau-server-test-user"></a>建立 Tableau Server 測試使用者

hello 本節目標在於 toocreate 呼叫許 Simon Tableau Server 中的使用者。 您需要 tooprovision hello Tableau 伺服器中的所有 hello 使用者。 

Hello 使用者的該使用者名稱應符合您已在 hello Azure AD 的自訂屬性中的 hello 值**username**。 以正確對應 hello 整合應該會運作的 hello[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)。

>[!NOTE]
>若要手動 toocreate 使用者，您會需要 toocontact hello Tableau 伺服器系統管理員，您組織中。
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

本節中，您可以授與存取 tooTableau 伺服器啟用了許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooTableau 伺服器上，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Tableau 伺服器**。

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Tableau 伺服器] 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Tableau 伺服器應用程式。
如需存取面板的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

