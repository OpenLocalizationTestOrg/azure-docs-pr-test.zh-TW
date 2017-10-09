---
title: "教學課程：Azure Active Directory 與 PagerDuty 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 PagerDuty 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a>教學課程：Azure Active Directory 與 PagerDuty 整合

在此教學課程中，您學會如何 toointegrate PagerDuty 與 Azure Active Directory (Azure AD)。

整合 Azure AD 與 PagerDuty 可以提供下列優點 hello:

- 您可以控制存取 tooPagerDuty Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooPagerDuty （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 PagerDuty 的整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 PagerDuty 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 PagerDuty
2. 設定並測試 Azure AD 單一登入

## <a name="adding-pagerduty-from-hello-gallery"></a>從 hello 圖庫加入 PagerDuty
tooconfigure hello 整合 PagerDuty 的 Azure AD，您需要 tooadd PagerDuty hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd PagerDuty 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**PagerDuty**，選取**PagerDuty**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 PagerDuty 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 PagerDuty 中是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 PagerDuty 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

在 PagerDuty 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 和測試 Azure AD 單一登入與 PagerDuty，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 PagerDuty 測試使用者](#create-a-pagerduty-test-user)** -toohave 許 Simon PagerDuty 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 PagerDuty 的應用程式中。

**tooconfigure Azure AD 單一登入與 PagerDuty，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **PagerDuty**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. 在 hello **PagerDuty 網域和 Url**區段中，執行下列步驟的 hello:

    ![PagerDuty 網域及 URL 單一登入資訊](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.pagerduty.com`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.pagerduty.com`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[PagerDuty 用戶端支援小組](https://www.pagerduty.com/support/)tooget 這些值。 

4. 在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. 在 hello **PagerDuty 組態**區段中，按一下**設定 PagerDuty** tooopen**設定登入**視窗。 複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![PagerDuty 設定](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. 在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Pagerduty 公司網站。

8. 在 hello 最上層顯示 hello 功能表上，按一下**帳戶設定**。
   
    ![帳戶設定](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "帳戶設定")

9. 按一下 [單一登入] 。
   
    ![單一登入](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "單一登入")

10. 在 hello**啟用單一登入 (SSO)**頁面上，執行下列步驟的 hello:
   
    ![啟用單一登入](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "啟用單一登入")
   
    a. 開啟您從 [記事本]，複製到剪貼簿，其內容的 hello Azure 入口網站下載的 base-64 編碼的憑證，然後將它貼入 toohello **X.509 憑證**文字方塊
  
    b. 在 hello**登入 URL**文字方塊中，貼上**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。
  
    c. 在 hello**登出 URL**文字方塊中，貼上**登出 URL**您從 Azure 入口網站複製的。
 
    d. 選取 [開啟單一登入] 。
 
    e. 按一下 [儲存變更] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="create-a-pagerduty-test-user"></a>建立 PagerDuty 測試使用者

tooenable Azure AD 使用者 toolog 中 tooPagerDuty，它們必須佈建到 PagerDuty。  
在 PagerDuty 的 hello 案例中，佈建須手動進行。

>[!NOTE]
>您可以使用任何其他 Pagerduty 使用者帳戶建立工具或 Api 提供 Pagerduty tooprovision Azure Active Directory 使用者帳戶。

**tooprovision 使用者帳戶，執行下列步驟的 hello:**

1. 登入 tooyour **Pagerduty**租用戶。

2. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。

3. 按一下 [加入使用者] 。
   
    ![新增使用者](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "新增使用者")

4.  在 [hello**邀請團隊**] 對話方塊中，執行下列步驟的 hello:
   
    ![邀請團隊成員](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "邀請團隊成員")

    a. 型別 hello **First 與 Last Name**類似使用者的**許 Simon**。 
   
    b. 輸入使用者的**電子郵件**地址，如 **brittasimon@contoso.com**。
   
    c. 按一下 新增，然後按一下傳送邀請。
   
    >[!NOTE]
    >所有新增的使用者會收到邀請 toocreate PagerDuty 帳戶。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooPagerDuty 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200]

**tooassign 許 Simon tooPagerDuty，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**PagerDuty**。

    ![hello 應用程式清單中的 hello PagerDuty 連結](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello PagerDuty 磚 hello 存取 Panelyou 中的應該會收到自動登入 tooyour PagerDuty 的應用程式。

如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

