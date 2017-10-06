---
title: "教學課程：Azure Active Directory 與 Yonyx Interactive Guides 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間 Yonyx 互動式輔助線。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 24e30d243143651b8d32535c76dc300931ae5746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a>教學課程：Azure Active Directory 與 Yonyx Interactive Guides 整合

在此教學課程中，您學會如何與 Azure Active Directory (Azure AD) 的 toointegrate Yonyx Interactive 引導。

與 Azure AD 整合 Yonyx 互動式指南可以提供下列優點 hello:

- 您可以控制存取 tooYonyx 互動式輔助線的 Azure AD 中
- 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooYonyx 互動式指南 （單一登入）
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Yonyx 互動式輔助線與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Yonyx Interactive Guides 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Yonyx 互動式輔助線
2. 設定並測試 Azure AD 單一登入

## <a name="adding-yonyx-interactive-guides-from-hello-gallery"></a>從 hello 圖庫加入 Yonyx 互動式輔助線
tooconfigure hello 整合 Yonyx 互動式指南到 Azure AD，您需要 tooadd Yonyx 互動式指南 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Yonyx 互動式指南從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory] 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**Yonyx 互動式指南**，選取**Yonyx 互動式指南**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![Yonyx hello [結果] 清單中的互動式輔助線](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Yonyx Interactive Guides 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Yonyx 互動式指南中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Yonyx 互動式指南中的相關的使用者之間的連結關聯性需要 toobe 建立。

在 Yonyx 互動式輔助線，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入與 Yonyx 互動式指南，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Yonyx 互動式指南](#create-a-yonyx-interactive-guides-test-user)** -toohave 許 Simon Yonyx 互動式指南是連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Yonyx 互動式指南應用程式中設定單一登入。

**Azure AD 單一登入的 tooconfigure Yonyx 互動式指南，以執行 hello 下列步驟：**

1. 在 Azure 入口網站上 hello hello **Yonyx 互動式指南**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入連結][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. 在 [hello **Yonyx 互動式指南網域和 Url**區段中，執行下列步驟的 hello:

    ![Yonyx Interactive Guides 網域和 URL 單一登入資訊](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    a. 在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.yonyx.com/y/conversation/?id=<guid number>`

    b. 在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.yonyx.com`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[Yonyx 互動式輔助線用戶端支援小組](mailto:support@yonyx.com)tooget 這些值。 
 
4. 在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. 在 [hello **Yonyx 互動式輔助線設定**區段中，按一下**設定 Yonyx 互動式指南**tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![Yonyx Interactive Guides 設定](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. tooconfigure 單一登入上**Yonyx 互動式指南**端，您需要下載 toosend hello **Certificate(Base64)**，**登出 URL**， **SAML單一登入服務 URL** **SAML 實體識別碼**太[Yonyx 互動式輔助線的支援團隊](mailto:support@yonyx.com)。 設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

  ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a>建立 Yonyx Interactive Guides 測試使用者

hello 本節目標在於 toocreate 呼叫許 Simon Yonyx 互動式指南中的使用者。 Yonyx Interactive Guides 支援預設啟用的 Just-In-Time 佈建。

在這一節沒有您需要進行的動作項目。 如果尚未存在期間嘗試 tooaccess Yonyx 互動式指南，建立新的使用者。

>[!NOTE]
>若要手動 toocreate 使用者，您需要 toocontact hello Yonyx 互動式指南支援透過小組< mailto:support@yonyx.com >。 

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooYonyx 互動式輔助線。

![指派 hello 使用者角色][200]

**tooassign 許 Simon tooYonyx 互動式指南，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Yonyx 互動式指南**。

    ![hello 應用程式清單中的 hello Yonyx 互動式輔助線連結](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下的 hello Yonyx 互動式指南磚 hello 存取面板中時，您應該取得自動登入 tooyour Yonyx 互動式指南應用程式。

如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

