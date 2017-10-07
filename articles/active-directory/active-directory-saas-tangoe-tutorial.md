---
title: "教學課程：Azure Active Directory 與 Tangoe 命令高階行動裝置整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Tangoe 命令 Premium Mobile 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a>教學課程：Azure Active Directory 整合 Tangoe 命令高階行動裝置

在此教學課程中，您學會如何 toointegrate Tangoe 命令 Premium 行動裝置與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Tangoe 命令 Premium 行動可以提供下列優點 hello:

- 您可以控制存取 tooTangoe 命令 Premium 行動裝置版的 Azure AD 中
- 您可以使用其 Azure AD 帳戶啟用您使用者 tooautomatically get 登入 tooTangoe 命令 Premium 行動 （單一登入）
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Tangoe 命令 Premium 行動裝置與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Tangoe 命令高階行動裝置單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫新增 Tangoe 命令 Premium 行動裝置
2. 設定和測試 Azure AD 單一登入

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a>從 hello 圖庫新增 Tangoe 命令 Premium 行動裝置
tooconfigure hello 整合 Tangoe 命令 Premium 行動到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Tangoe 命令 Premium 行動裝置。

**tooadd Tangoe 命令 Premium Mobile 從 hello 組件庫，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 hello 搜尋方塊中，輸入**Tangoe 命令 Premium 行動**，選取**Tangoe 命令 Premium 行動**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![從資源庫新增 Tangoe 命令高階行動裝置 ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Tangoe 命令高階行動裝置設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Tangoe 命令 Premium Mobile 中是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Tangoe 命令 Premium Mobile 中相關的使用者之間的連結關聯性需要 toobe 建立。

在 Tangoe 命令 Premium 行動，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Tangoe 命令 Premium 行動裝置與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Tangoe 命令 Premium 行動](#create-a-tangoe-command-premium-mobile-test-user)** -toohave 許 Simon 中 Tangoe 命令 Premium Mobile 是連結的 toohello Azure AD 使用者表示法的對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Tangoe 命令 Premium 行動應用程式中設定單一登入。

**與 Tangoe 命令 Premium Mobile、 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**

1. 在 Azure 入口網站上 hello hello **Tangoe 命令 Premium 行動**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![SAML 型登入](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. 在 [hello **Tangoe 命令 Premium 行動網域和 Url**區段中，執行下列步驟的 hello:

    ![Tangoe 命令高階行動裝置網域與 URL](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    a. 在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`

    b. 在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://sso.tangoe.com/sp/ACS.saml2`

    > [!NOTE] 
    > 這些都不是真正的值。 Hello 實際的回覆 URL 和登入 URL 更新這些值。 請連絡[Tangoe 命令 Premium 行動用戶端支援小組](https://www.tangoe.com/contact-2/)tooget 這些值。 

4. 在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![[儲存] 按鈕](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. 在 [hello **Tangoe 命令 Premium 行動裝置組態**區段中，按一下**設定 Tangoe 命令 Premium 行動**tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![[Tangoe 命令高階行動裝置設定] 區段](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. tooget SSO 設定應用程式，請連絡您[Tangoe 命令 Premium 行動用戶端支援小組](https://www.tangoe.com/contact-2/)並提供下列 hello:

   - hello 下載的中繼資料檔案
   - hello **SAML 實體識別碼**
   - hello **SAML 單一登入服務 URL**
   - hello**登出 URL**

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![[使用者和群組] -> [所有使用者]](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![新增使用者](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![使用者對話方塊頁面](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a>建立 Tangoe 命令高階行動裝置測試使用者

在本節中，您要在 Tangoe 命令高階行動裝置中建立名為 Britta Simon 的使用者。 

Tangoe 命令 Premium 行動應用程式需要所有的 hello 使用者 toobe hello 進行單一登入前的應用程式中，佈建。 工作，所以請以 hello [Tangoe 命令 Premium 行動用戶端支援小組](https://www.tangoe.com/contact-2/)tooprovision hello 應用程式的所有這些使用者。 

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooTangoe 命令 Premium 行動裝置啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooTangoe 命令 Premium 行動裝置，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Tangoe 命令 Premium 行動**。

    ![應用程式清單中的 Tangoe 命令高階行動裝置](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。

當您按一下 hello Tangoe 命令 Premium 行動磚 hello 存取面板中的時，您應該取得自動登入 tooyour Tangoe 命令 Premium 行動應用程式。 如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

