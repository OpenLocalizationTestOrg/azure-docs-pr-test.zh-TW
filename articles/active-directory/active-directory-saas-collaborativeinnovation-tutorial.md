---
title: "教學課程：Azure Active Directory 與 Collaborative Innovation 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與共同作業的創新之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a>教學課程：Azure Active Directory 與 Collaborative Innovation 整合

在此教學課程中，您學會如何 toointegrate 與 Azure Active Directory (Azure AD) 的共同作業創新。

整合與 Azure AD 的共同作業的創新可以提供下列優點 hello:

- 您可以控制存取 tooCollaborative 創新的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooCollaborative 創新 （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與共同作業的創新的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Collaborative Innovation 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 加入共同作業的創新從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-collaborative-innovation-from-hello-gallery"></a>加入共同作業的創新從 hello 組件庫
tooconfigure hello 整合共同作業的創新到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 共同作業的創新。

**tooadd hello 庫、 共同作業的創新執行 hello 下列步驟：**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**共同作業的創新**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. 在 [hello [結果] 窗格中，選取 [**共同作業的創新**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Collaborative Innovation 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在共同作業的創新是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 中共同作業的創新的相關的使用者之間的連結關聯性需要 toobe 建立。

在共同作業的創新，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入與共同作業的創新，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者共同作業的創新](#creating-a-collaborative-innovation-test-user)** -toohave 中共同作業是表示連結的 toohello Azure AD 使用者的創新許 Simon 對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並共同作業的創新應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與共同作業的創新，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello**共同作業的創新**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. 在 [hello**共同作業的創新網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    a. 在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.foundry.<companyname>.com/`

    b. 在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.foundry.<companyname>.com`
    
    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[共同作業的創新用戶端支援小組](https://www.unilever.com/contact/)tooget 這些值。  

4. 共同作業的創新應用程式預期 hello SAML 判斷提示，以特定格式。 請設定下列宣告為此應用程式的 hello。 您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。 hello 下列螢幕擷取畫面會顯示這個範例。
    
    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. 按一下**檢視和編輯所有其他使用者屬性**核取方塊在 hello**使用者屬性**區段 tooexpand hello 屬性。 執行下列步驟，在每個顯示 hello 屬性-hello

    | 屬性名稱 | 屬性值 |
    | ---------------| --------------- |    
    | givenname | user.givenname |
    | surname | user.surname |
    | emailaddress | user.userprincipalname |
    | 名稱 | user.userprincipalname |

    a. 按一下 hello 屬性 tooopen hello**編輯屬性**視窗。

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    b. 從 hello 刪除 hello URL 值**命名空間**。
    
    c. 按一下**確定**toosave hello 設定。

6. 在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. tooconfigure 單一登入上**共同作業的創新**端，您需要下載 toosend hello**中繼資料 XML**太[共同作業的創新技術支援小組](https://www.unilever.com/contact/)。 設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-collaborative-innovation-test-user"></a>建立 Collaborative Innovation 測試使用者

tooenable Azure AD 使用者 toolog 中 tooCollaborative 創新，它們必須佈建到共同作業的創新。  

如果此應用程式佈建為自動 hello 應用程式支援即時使用者佈建。 因此會有任何需要 tooperform 這裡所有步驟。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooCollaborative 創新。

![指派使用者][200] 

**tooassign 許 Simon tooCollaborative 創新，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**共同作業的創新**。

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello 共同作業的創新磚 hello 存取面板中時，您應該取得共同作業的創新應用程式的登入的頁面。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

