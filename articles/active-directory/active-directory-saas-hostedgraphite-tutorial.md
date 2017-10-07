---
title: "教學課程：Azure Active Directory 與 Hosted Graphite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與裝載 Graphite 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a>教學課程：Azure Active Directory 與 Hosted Graphite 整合

在此教學課程中，您學會如何 toointegrate Hosted Graphite 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合裝載 Graphite 可以提供下列優點 hello:

- 您可以控制存取 tooHosted Graphite Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooHosted Graphite （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與裝載 Graphite 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Hosted Graphite 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 加入裝載 Graphite 從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-hosted-graphite-from-hello-gallery"></a>加入裝載 Graphite 從 hello 組件庫
tooconfigure hello 整合裝載 Graphite 到 Azure AD，您需要 tooadd Hosted Graphite hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Hosted Graphite 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**裝載 Graphite**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. 在 hello 結果 窗格中，選取 **裝載 Graphite**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Hosted Graphite 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中裝載 Graphite 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 裝載 Graphite 中相關的使用者之間的連結關聯性需要 toobe 建立。

在裝載 Graphite，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及裝載 Graphite 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立裝載 Graphite 測試使用者](#creating-a-hosted-graphite-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示裝載 Graphite 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入裝載 Graphite 應用程式中。

**tooconfigure Azure AD 單一登入裝載 Graphite，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello**裝載 Graphite**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. 在 hello**裝載 Graphite 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP 初始化模式**，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    a. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.hostedgraphite.com/metadata/<user id>`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.hostedgraphite.com/complete/saml/<user id>`

4. 在 hello**裝載 Graphite 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**SP 初始模式**，執行下列步驟的 hello:
   
    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    a. 按一下 hello**顯示進階的 URL 設定**選項

    b. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.hostedgraphite.com/login/saml/<user id>/`   

    > [!NOTE] 
    > 請注意這些不是 hello 實際值。 這些值以 hello 有 tooupdate 實際的識別項、 回覆 URL 和登入 URL。 tooget 這些值，您可以移 tooAccess]-> [SAML 設定在您的應用程式端或連絡人[裝載 Graphite 支援小組](mailto:help@hostedgraphite.com)。
    >
 
5. 在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. 在 hello**裝載 Graphite 組態**區段中，按一下**設定裝載 Graphite** tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. 以系統管理員身分登入 tooyour 裝載 Graphite 租用戶。

9. 移 toohello **SAML 設定 頁面**hello 提要欄位中 (**存取 SAML 設定->** )。
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. 確認這些 Url 符合您的設定對 hello**裝載 Graphite 網域和 Url** hello Azure 入口網站的區段。
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. 在**實體或簽發者 ID**和**SSO 登入 URL**等文字方塊中，貼上的 hello 值**SAML 實體識別碼**和**SAML 單一登入服務 URL**您已複製從 Azure 入口網站。 
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. 選取 [唯讀] 做為 [預設使用者角色]。
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. 從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **X.509 憑證**文字方塊。
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. 按一下 [儲存]  按鈕。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-hosted-graphite-test-user"></a>建立 Hosted Graphite 測試使用者

hello 本節目標在於 toocreate 中裝載 Graphite 呼叫許 Simon 的使用者。 Hosted Graphite 支援預設啟用的 Just-In-Time 佈建。

在這一節沒有您需要進行的動作項目。 如果尚未存在，將會嘗試 tooaccess Hosted Graphite 期間建立新使用者。

>[!NOTE]
>若要手動 toocreate 使用者，您需要透過 toocontact hello 裝載 Graphite 支援小組< mailto:help@hostedgraphite.com >。 

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooHosted Graphite 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooHosted Graphite，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**裝載 Graphite**。

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。

當您按一下 hello 裝載 Graphite 磚 hello 存取面板中的時，您應該取得自動登入 tooyour 裝載 Graphite 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

