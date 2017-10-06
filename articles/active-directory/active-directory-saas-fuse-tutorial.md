---
title: "教學課程：Azure Active Directory 與 Fuse 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與保險絲之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 720ed8af0b5de1e3bee5a40353ca0ee661766864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a>教學課程：Azure Active Directory 與 Fuse 整合

在此教學課程中，您學會如何 toointegrate 保險絲與 Azure Active Directory (Azure AD)。

與 Azure AD 整合保險絲可以提供下列優點 hello:

- 您可以控制存取 tooFuse Azure AD 中。
- 您可以啟用您的使用者 tooautomatically get 登入 tooFuse （單一登入） 具有其 Azure AD 帳戶。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

保險絲 tooconfigure Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Fuse 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫新增保險絲
2. 設定和測試 Azure AD 單一登入

## <a name="add-fuse-from-hello-gallery"></a>從 hello 圖庫新增保險絲
tooconfigure hello 整合保險絲到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 保險絲。

**tooadd 保險絲從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory] 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 [hello] 搜尋方塊中，輸入**保險絲**，選取**保險絲**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![保險絲 hello [結果] 清單中](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Fuse 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中保險絲是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 之間的連結關聯性相關的建立保險絲需求 toobe 中的使用者。

保險絲中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及保險絲與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者保險絲](#create-a-fuse-test-user)** -toohave 許 Simon 保險絲所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並保險絲應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與保險絲，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello**保險絲**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入連結][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. 在 [hello**保險絲網域和 Url**區段中，執行下列步驟的 hello:

    ![Fuse 網域與 URL 單一登入資訊](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant name>.fusion-universal.com/`

    > [!NOTE] 
    > 這不是真實的值。 更新此值以 hello 實際的登入 URL。 請連絡[保險絲用戶端支援小組](mailto:support@fusion-universal.com)tooget 此值。 
 
4. 在 [hello **SAML 簽章憑證**區段中，按一下**憑證 (Raw)**然後儲存 hello 憑證檔案儲存在您的電腦。

    ![hello 憑證下載連結](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. 在 [hello**保險絲組態**區段中，按一下**設定保險絲**tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![Fuse 設定](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. tooget SSO 設定應用程式，請連絡[保險絲支援小組](mailto:support@fusion-universal.com)，提供下列 hello:

    * 下載的 hello**憑證 (Raw) 檔案**
    * hello **SAML 單一登入服務 URL**
    * hello **SAML 實體識別碼**
    * hello**登出 URL**

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. 在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![hello [使用者] 對話方塊](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    a. 在 [hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。

    d. 按一下 [建立] 。
 
### <a name="create-a-fuse-test-user"></a>建立 Fuse 測試使用者

在本節中，您要在 Fuse 中建立名為 Britta Simon 的使用者。 請使用[保險絲支援小組](mailto:support@fusion-universal.com)tooadd hello hello 保險絲平台的使用者。


### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooFuse 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooFuse，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**保險絲**。

    ![hello 應用程式清單中的 hello 保險絲連結](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello 保險絲磚 hello 存取面板中的時，您應該取得自動登入 tooyour 保險絲應用程式。
如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

