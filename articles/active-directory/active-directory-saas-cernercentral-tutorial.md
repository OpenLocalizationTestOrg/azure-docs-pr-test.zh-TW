---
title: "教學課程：Azure Active Directory 與 Cerner Central 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Cerner 中央之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a>教學課程：Azure Active Directory 與 Cerner Central 整合

在此教學課程中，您學會如何 toointegrate Cerner 中央與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Cerner 中央可以提供下列優點 hello:

- 您可以控制存取 tooCerner 中央的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooCerner 中央 （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Cerner 中央與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已核准的 Cerner Central 系統帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Cerner 中央
2. 設定並測試 Azure AD 單一登入

## <a name="adding-cerner-central-from-hello-gallery"></a>從 hello 圖庫加入 Cerner 中央
tooconfigure hello 整合 Cerner 中央到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Cerner 中央。

**tooadd Cerner 中央從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**hello 對話方塊頂端的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Cerner 中央**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. 在 hello 結果 窗格中，選取  **Cerner 中央**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Cerner Central 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Cerner 集中是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Cerner 集中相關的使用者之間的連結關聯性需要 toobe 建立。

tooconfigure 及 Cerner 中央與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Cerner 中央](#creating-a-cerner-central-test-user)** -toohave 許 Simon 集中 Cerner 連結的 toohello Azure AD 表示 hello 使用者的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Cerner 管理中心應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Cerner 中央執行 hello 下列步驟：**

1. 在 Azure 入口網站上 hello hello **Cerner 中央**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. 在 hello **Cerner 中央網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    a. 在 hello**識別碼**文字方塊中，使用下列模式的 hello 類型 hello 值：
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列的 hello 模式： 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > 這些值不是真正的 hello。 以 hello 實際的識別項和回覆 URL 更新這些值。 請連絡[Cerner 中央支援小組](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations)tooget 這些值。
 
4. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. toogenerate hello**中繼資料**url，請執行下列步驟的 hello:

    a. 按一下 [應用程式註冊]。
    
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    b. 按一下**端點**tooopen**端點** 對話方塊。  
    
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    c. 按一下 hello 複製按鈕 toocopy**同盟中繼資料文件**url 並將它貼到 [記事本]。
    
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    d. 現在請 toohello 屬性頁的**Cerner 中央**和複製 hello**應用程式識別碼**使用**複製**按鈕，並將它貼到 [記事本]。
 
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    e. 產生 hello**中繼資料 URL**使用 hello 下列模式：`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`

6. tooconfigure 單一登入上**Cerner 中央**側邊，您需要 toosend hello**中繼資料 URL**太[Cerner 中央支援](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations)。 他們可以設定 hello SSO 應用程式端 toocomplete hello 整合。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。 

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-cerner-central-test-user"></a>建立 Cerner Central 測試使用者

**Cerner Central** 應用程式可允許從任何同盟身分識別提供者進行驗證。 如果使用者可以 toolog toohello 應用程式首頁中的，它們同盟，且不需要任何手動佈建。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooCerner 中央。

![指派使用者][200] 

**tooassign 許 Simon tooCerner 中央，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Cerner 中央**。

    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下的 hello Cerner 中央磚 hello 存取面板中時，您應該取得自動登入 tooyour Cerner 管理中心應用程式。 如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

