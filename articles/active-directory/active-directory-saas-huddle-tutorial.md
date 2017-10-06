---
title: "教學課程：Azure Active Directory 與 Huddle 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Huddle 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a>教學課程：Azure Active Directory 與 Huddle 整合

在此教學課程中，您學會如何 toointegrate Huddle 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Huddle 可以提供下列優點的 hello:

- 您可以控制存取 tooHuddle Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooHuddle （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

與 Huddle tooconfigure Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Huddle 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述

在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Huddle
2. 設定並測試 Azure AD 單一登入

## <a name="adding-huddle-from-hello-gallery"></a>從 hello 圖庫加入 Huddle
tooconfigure hello Huddle 至 Azure AD 整合，您需要 tooadd Huddle hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Huddle 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Huddle**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. 在 [hello [結果] 窗格中，選取 [ **Huddle**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Huddle 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Huddle 中是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 之間的連結關聯性相關的建立 Huddle 需求 toobe 中的使用者。

在 Huddle 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入 Huddle，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。

2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。

3. **[建立測試使用者 Huddle](#creating-a-huddle-test-user) ** -toohave 許 Simon Huddle 所連結的 toohello Azure AD 使用者表示法中對應項目。

4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。

5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Huddle 的應用程式中。

**tooconfigure Azure AD 單一登入與 Huddle，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Huddle**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. 在 [hello **Huddle 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`http://<company name>.huddle.com`

    > [!NOTE] 
    > 這不是真實的值。 更新此值以 hello 實際的登入 URL。 請連絡[Huddle 的用戶端支援小組](https://huddle.zendesk.com)tooget 此值。 

4. 在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. 在 [hello **Huddle 設定**區段中，按一下**設定 Huddle** tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。** 

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. tooconfigure 單一登入 Huddle 端上，您需要下載 toosend hello**憑證**， **SAML 單一登入服務 URL**，和**SAML 實體識別碼**太[Huddle 的用戶端支援小組](https://huddle.zendesk.com)。 設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。  
   
    >[!NOTE]
    > 單一登入需要 toobe 由 hello Huddle 支援小組啟用。 Hello 組態完成後，您會收到通知。 
    > 

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 
   
### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-huddle-test-user"></a>建立 Huddle 測試使用者

tooenable Azure AD 使用者 toolog 中 tooHuddle，它們必須佈建到 Huddle。 在 Huddle 的 hello 案例中，佈建須手動進行。

**tooconfigure 使用者佈建，執行下列步驟的 hello:**

1. 登入 tooyour **Huddle**以系統管理員身分的公司網站。
2. 按一下 [工作區] 。
3. 按一下 [人員] \> [邀請人員]。
   
   ![人員](./media/active-directory-saas-huddle-tutorial/IC787838.png "人員")

4. 在 [hello**建立新的邀請**區段中，執行下列步驟的 hello:
   
   ![新的邀請](./media/active-directory-saas-huddle-tutorial/IC787839.png "新的邀請")
   
   a. 在 [hello**選擇小組 tooinvite 人員 toojoin**清單中，選取**小組**。

   b. 型別 hello**電子郵件地址**有效的 Azure AD 的帳戶中您要 tooprovision 太**輸入電子郵件地址的人，您想要 tooinvite**文字方塊。

   c. 按一下 [邀請] 。   
   
    >[!NOTE]
    > hello Azure AD 帳戶持有者將收到包含連結 tooconfirm hello 帳戶之前它會變成作用中的電子郵件。 
    > 

>[!NOTE]
>您可以使用任何其他 Huddle 使用者帳戶建立工具或 Api 提供 Huddle tooprovision Azure AD 使用者帳戶。 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooHuddle 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooHuddle，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Huddle**。

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Huddle 磚 hello 存取面板中的時，您應該取得自動 Huddle 的應用程式的登入頁面。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
