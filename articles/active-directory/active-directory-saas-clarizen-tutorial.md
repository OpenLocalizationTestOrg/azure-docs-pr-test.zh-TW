---
title: "教學課程：Azure Active Directory 與 Clarizen 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Clarizen 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>教學課程：Azure Active Directory 與 Clarizen 整合

在此教學課程中，您學會如何 toointegrate Azure Active Directory (Azure AD)，與 Clarizen。 此整合提供下列您 hello 下列優點：

- 您可以控制，在 Azure AD 中擁有存取 tooClarizen。
- 您可以啟用自動登入 （單一登入） 的 tooClarizen 其 Azure AD 帳戶與您使用者 toobe。
- 您可以管理您的帳戶，在單一中央位置，hello Azure 入口網站。

本教學課程中的 hello 案例包含兩個主要工作：

1. 從 hello 圖庫新增 Clarizen。
2. 設定和測試 Azure AD 單一登入。

若您想了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合的更多詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
tooconfigure 與 Clarizen 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用單一登入的 Clarizen 訂用帳戶

tootest hello 步驟在本教學課程，請遵循下列建議：

- 在測試環境中測試 Azure AD 單一登入。 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 測試環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="add-clarizen-from-hello-gallery"></a>從 hello 圖庫新增 Clarizen
tooconfigure hello 整合 Clarizen 的 Azure AD 中，從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單加入 Clarizen。

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左的窗格中按一下 hello **Azure Active Directory**圖示。

    ![Azure Active Directory 圖示][1]

2. 按一下 [企業應用程式]。 然後按一下 [所有應用程式]。

    ![按一下 [企業應用程式] 和 [所有應用程式]][2]

3. 按一下 hello**新增**在 hello hello 對話方塊頂端的按鈕。

    ![hello [新增] 按鈕][3]

4. 在 [hello] 搜尋方塊中，輸入**Clarizen**。

    ![Hello 搜尋方塊中輸入"Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. 在 [hello] 結果窗格中，選取 [ **Clarizen**，然後按一下 [**新增**tooadd hello 應用程式。

    ![Hello 結果窗格中，選取 Clarizen](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在下列各節的 hello，設定並測試 Azure AD 單一登入 Clarizen 根據 hello 許 Simon 的測試使用者。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Clarizen 中是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Clarizen 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。 您建立此連結關聯性 hello 將值指派為**使用者名稱**做為 hello 值的 Azure AD 中**Username** Clarizen 中。

tooconfigure 和測試 Azure AD 單一登入與 Clarizen，完成下列建置組塊的 hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)**許 Simon 與 Azure AD 單一登入 tootest。
3. **[建立測試使用者 Clarizen](#create-a-clarizen-test-user) ** toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Clarizen 中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入
啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Clarizen 的應用程式中。

1. 在 Azure 入口網站上 hello hello **Clarizen**應用程式整合頁面上，按一下 [**單一登入**。

    ![按一下 [單一登入]][4]

2. 在 [hello**單一登入**對話方塊中，如**模式**，選取**SAML 型登入**tooenable 單一登入。

    ![選取 [SAML 登入]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. 在 [hello **Clarizen 網域和 Url**區段中，執行下列步驟的 hello:

    ![識別碼和回覆 URL 方塊](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. 在 [hello**識別碼**方塊中，做為型別 hello 值： **Clarizen**

    b. 在 [hello**回覆 URL**方塊中，輸入 URL，使用下列模式的 hello: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > 這些不是 hello 實際值。 您已 toouse hello 實際識別項，而且回覆 URL。 這裡我們建議您使用 hello 唯一字串值，如 hello 識別項。 tooget hello 實際的值，請連絡 hello [Clarizen 支援小組](https://success.clarizen.com/hc/en-us/requests/new)。

4. 在 [hello **SAML 簽章憑證**區段中，按一下**建立新憑證**。

    ![按一下 [建立新的憑證]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. 在 [hello**建立新的憑證**對話方塊，按一下 hello 日曆圖示，然後選取到期日。 然後按一下 [儲存] 。

    ![選取並儲存到期日](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. 在 [hello **SAML 簽章憑證**區段中，選取**啟用新的憑證**，然後按一下**儲存**。

    ![選取使 hello 新的憑證處於作用中的 hello 核取方塊](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. 在 [hello**變換憑證**對話方塊中，按一下 [**確定**。

    ![按一下 [確定] 您想 toomake hello 憑證 active tooconfirm](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. 在 [hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![按一下 [憑證 (Base64)] toostart hello 下載](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. 在 [hello **Clarizen 組態**區段中，按一下**設定 Clarizen** tooopen hello**設定登入**視窗。

    ![按一下 [設定 Clarizen]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![[登入設定] 視窗，包括檔案和 URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Clarizen 公司網站。

11. 按一下您的使用者名稱，然後按一下 [設定]。

    ![按一下您的使用者名稱底下的 [設定]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "設定")

12. 按一下 hello**通用設定**] 索引標籤。然後下, 一步太**同盟驗證**，按一下 [**編輯**。

    ![[全域設定] 索引標籤](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "全域設定")

13. 在 [hello**同盟驗證**對話方塊方塊中，執行下列步驟的 hello:

    ![[同盟驗證] 對話方塊](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "同盟驗證")

    a. 選取 [啟用同盟驗證]。

    b. 按一下**上傳**tooupload 下載的憑證。

    c. 在 [hello**登入 URL**方塊中，輸入 hello 值**SAML 單一登入服務 URL**從 hello Azure AD 應用程式設定] 視窗。

    d. 在 [hello**登出 URL**方塊中，輸入 hello 值**登出 URL**從 hello Azure AD 應用程式設定] 視窗。

    e. 選取 [使用 POST] 。

    f. 按一下 [儲存] 。

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
在 hello Azure 入口網站，建立稱為許 Simon 的測試使用者。

![Hello Azure AD 的測試使用者名稱和電子郵件地址][100]

1. 在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory**圖示。

    ![Azure Active Directory 圖示](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. 按一下**使用者和群組**，然後按一下 [**所有使用者**toodisplay hello 使用者清單。

    ![按一下 [使用者和群組] 與 [所有使用者]](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. 在 hello hello] 對話方塊的頂端，按一下**新增**tooopen hello**使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. 在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![在 [使用者] 對話方塊中填入名稱、電子郵件地址和密碼](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. 在 [hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**] 方塊中的 hello 許 Simon 帳戶類型 hello 電子郵件地址。

    c. 選取**顯示密碼**記下的 hello 值**密碼**。

    d. 按一下 [建立] 。

### <a name="create-a-clarizen-test-user"></a>建立 Clarizen 測試使用者
tooenable Azure AD 使用者 toosign tooClarizen 中的，您必須佈建使用者帳戶。 在 Clarizen 的 hello 案例中，佈建須手動進行。

1. Tooyour Clarizen 公司網站管理員身分登入。

2. 按一下 [人員] 。

    ![按一下 [人員]](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "人員")

3. 按一下 [邀請使用者] 。

    ![[邀請使用者] 按鈕](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "邀請使用者")

4. 在 [hello**邀請人員**對話方塊方塊中，執行下列步驟的 hello:

    ![[邀請人員] 對話方塊](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "邀請人員")

    a. 在 [hello**電子郵件**] 方塊中的 hello 許 Simon 帳戶類型 hello 電子郵件地址。

    b. 按一下 [邀請] 。

    > [!NOTE]
    > hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者
藉由授與他們存取 tooClarizen 可讓許 Simon toouse Azure 單一登入。

![已指派測試使用者][200]

1. 在 [hello Azure 入口網站，開啟 hello 應用程式檢視，瀏覽 toohello 目錄檢視，按一下 [**企業應用程式**，然後按一下 [**所有應用程式**。

    ![按一下 [企業應用程式] 和 [所有應用程式]][201]

2. 在 [hello] 應用程式清單中，選取**Clarizen**。

    ![Hello 清單中選取 Clarizen](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. 在 [hello] 左窗格中，按一下 [**使用者和群組**。

    ![按一下 [使用者和群組]][202]

4. 按一下 hello**新增**] 按鈕。 然後，在 hello**將作業加入**對話方塊中，選取**使用者和群組**。

    ![hello [新增] 按鈕和 hello"新增指派] 對話方塊][203]

5. 在 [hello**使用者和群組**對話方塊中，選取**許 Simon** hello 的使用者清單中。

6. 在 [hello**使用者和群組**對話方塊方塊中，按一下 hello**選取**] 按鈕。

7. 在 [hello**將作業加入**對話方塊方塊中，按一下 hello**指派**] 按鈕。

### <a name="test-single-sign-on"></a>測試單一登入
使用存取面板 hello 測試 Azure AD 單一登入組態。

當您按一下 hello Clarizen 磚 hello 存取面板中的時，您應該會自動登入 tooyour Clarizen 的應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
