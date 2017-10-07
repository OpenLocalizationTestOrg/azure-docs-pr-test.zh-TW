---
title: "教學課程：Azure Active Directory 與 Bynder 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Bynder 之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>教學課程：Azure Active Directory 與 Bynder 整合
本教學課程的 hello 目標是 tooshow 您如何 toointegrate Bynder 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Bynder 可以提供下列優點 hello:

* 您可以控制存取 tooBynder Azure AD 中
* 您可以啟用您的使用者 tooautomatically get tooBynder 已登入的單一登入 (SSO) 與他們的 Azure AD 帳戶
* 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
tooconfigure Bynder 與 Azure AD 整合，您需要下列項目 hello:

* Azure AD 訂用帳戶
* 已啟用 Bynder 單一登入 (SSO) 的訂用帳戶

>[!NOTE]
>本教學課程中的步驟 tootest hello，不建議使用實際執行環境。 
> 

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

* 除非必要，否則您不應使用生產環境，。
* 如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
本教學課程的 hello 目標是 tooenable 您 tootest Microsoft Azure AD 的 SSO 在測試環境中。

本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Bynder
2. 設定並測試 Microsoft Azure AD SSO

## <a name="add-bynder-from-hello-gallery"></a>從 hello 圖庫新增 Bynder
tooconfigure hello 整合 Bynder 到 Azure AD，您需要 tooadd Bynder hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Bynder 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。 
   
    ![Active Directory][1]
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式][2]
4. 按一下**新增**hello hello 頁底端。
   
    ![應用程式][3]
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![應用程式][4]
6. 在 [hello] 搜尋方塊中，輸入**Bynder**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. 在 hello 結果 窗格中，選取  **Bynder**，然後按一下**完成**tooadd hello 應用程式。
   
    ![選取在 hello 圖庫中的 hello 應用程式](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>設定並測試 Microsoft Azure AD SSO
hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Microsoft Azure AD SSO 與 Bynder 根據稱為 「 許 Simon"的測試使用者。

SSO toowork Azure AD 需要 tooknow Bynder tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。 換句話說，Azure AD 使用者與 hello Bynder 中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Bynder 中。

tooconfigure 及測試 Bynder 與 Microsoft Azure AD 的 SSO，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Microsoft Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -Microsoft Azure AD 單一登入與許 Simon tootest。
3. **[建立測試使用者 Bynder](#creating-a-bynder-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Bynder 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Microsoft Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-microsoft-azure-ad-sso"></a>設定 Microsoft Azure AD SSO
在本節中，您將 hello 傳統入口網站中啟用 Microsoft Azure AD 的 SSO 和 Bynder 應用程式中設定單一登入。

**tooconfigure Bynder，與 Microsoft Azure AD 的 SSO 執行 hello 下列步驟：**

1. Hello 傳統入口網站中，在 hello **Bynder**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
    ![設定單一登入][6] 
2. 在 hello**如何想您使用者 toosign tooBynder 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. 在 [hello**設定應用程式設定**對話方塊頁面上，如果您想 tooconfigure hello 應用程式中的**IDP 初始化模式**，執行下列步驟的 hello，然後按一下**下一步]**:
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. 按一下 [下一步] 。
4. 如果您想 tooconfigure hello 應用程式中的**SP 初始模式**上 hello**設定應用程式設定**對話方塊頁面上，然後按一下 [hello **[顯示進階設定 （選擇性）]**]，然後輸入 hello**登入 URL**按一下**下一步**。

    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.getbynder.com/login/`
  2. 按一下 [下一步] 。
  
   >[!NOTE]
   >在此教學課程中的 hello 登入 URL 的 hello 值為只 placeholfer。 tooget hello 實際的環境，請連絡 Bynder。
   >

5. 在 hello **Bynder 在設定單一登入**頁面上，執行下列步驟的 hello，按一下 **下一步**:
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. 按一下**下載中繼資料**，然後儲存您的電腦上的 hello 檔案。
  2. 按一下 [下一步] 。
6. tooget SSO 設定應用程式，請連絡您 Bynder 的支援團隊。 附加 hello 下載的中繼資料檔案，並分享 Bynder 小組 tooset 向上 SSO 邊。
7. Hello 傳統入口網站中選取 hello 單一登入組態確認，然後**下一步**。
   
    ![Azure AD 單一登入][10]
8. 在 hello**單一登入確認**頁面上，按一下**完成**。  
   
    ![Azure AD 單一登入][11]

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節 hello 目標是 toocreate 測試使用者呼叫許 Simon hello 傳統入口網站中。

![建立 Azure AD 使用者][20]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. 在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. 針對 [使用者類型]，選取 [您組織中的新使用者]。
  2. 在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。
  3. 按一下 [下一步] 。
6. 在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. 在 hello**名字**文字方塊中，輸入**許**。  
  2. 在 hello**姓氏**文字方塊中，輸入， **Simon**。 
  3. 在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。
  4. 在 hello**角色**清單中，選取**使用者**。
  5. 按一下 [下一步] 。
7. 在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. 在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. 請記下 hello hello 值**新密碼**。
   2. 按一下頁面底部的 [新增] 。   

### <a name="create-a-bynder-test-user"></a>建立 Bynder 測試使用者
hello 本節目標在於 toocreate Bynder 中呼叫許 Simon 的使用者。 Bynder 支援預設啟用的 Just-In-Time 佈建。

在這一節沒有您需要進行的動作項目。 如果尚未存在，將會嘗試 tooaccess Bynder 期間建立新使用者。

>[!NOTE]
>若要手動 toocreate 使用者，您會需要 toocontact hello Bynder 支援小組。 
> 

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者
本節 hello 目標是授與他們存取 tooBynder tooenabling 許 Simon toouse Azure SSO。

   ![指派使用者][200]

**tooassign 許 Simon tooBynder，執行下列步驟的 hello:**

1. Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。
   
    ![指派使用者][201]
2. 在 [hello] 應用程式清單中，選取**Bynder**。
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。
   
    ![指派使用者][203]
4. 在 hello 使用者清單中選取**許 Simon**。
5. 在 hello hello 底部的工具列中按一下**指派**。
   
    ![指派使用者][205]

### <a name="test-single-sign-on"></a>測試單一登入
hello 本節目標在於 tootest 您 Microsoft Azure AD 的 SSO 組態使用 hello 存取面板。

當您按一下 hello Bynder 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Bynder 應用程式。

## <a name="additional-resources"></a>其他資源
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
