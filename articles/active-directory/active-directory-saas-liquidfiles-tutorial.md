---
title: "教學課程：Azure Active Directory 與 LiquidFiles 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 LiquidFiles 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 67eb888090f81e0ceb791ed45d564b98fe1eb6d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a>教學課程：Azure Active Directory 與 LiquidFiles 整合

在此教學課程中，您學會如何 toointegrate LiquidFiles 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 LiquidFiles 可以提供下列優點 hello:

- 您可以控制存取 tooLiquidFiles Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooLiquidFiles （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure LiquidFiles 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 LiquidFiles 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 LiquidFiles
2. 設定並測試 Azure AD 單一登入

## <a name="adding-liquidfiles-from-hello-gallery"></a>從 hello 圖庫加入 LiquidFiles
tooconfigure hello 整合 LiquidFiles 到 Azure AD，您需要 tooadd LiquidFiles hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd LiquidFiles 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**LiquidFiles**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. 在 hello 結果 窗格中，選取  **LiquidFiles**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 LiquidFiles 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 LiquidFiles 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello LiquidFiles 中相關的使用者之間的連結關聯性需要 toobe 建立。

LiquidFiles 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 LiquidFiles 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 LiquidFiles](#creating-a-liquidfiles-test-user)**  -toohave 許 Simon LiquidFiles 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 LiquidFiles 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 LiquidFiles，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **LiquidFiles**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. 在 hello **LiquidFiles 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<YOUR_SERVER_URL>/saml/init`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<YOUR_SERVER_URL>`

    c. b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<YOUR_SERVER_URL>/saml/consume`

    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與 hello 實際的登入 URL，識別項和回覆 URL。 請連絡[LiquidFiles 用戶端支援小組](https://www.liquidfiles.com/support.html)tooget 這些值。 
 
4. 在 hello **SAML 簽章憑證**區段，複製 hello**指紋**憑證值。

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. 在 hello **LiquidFiles 組態**區段中，按一下**設定 LiquidFiles** tooopen**設定登入**視窗。 複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. 以系統管理員身分登入 tooyour LiquidFiles 公司網站。

8. 按一下**單一登入**在 hello **Admin > 組態**hello 功能表。

9. 在 hello**單一登入組態**頁面上，執行下列步驟的 hello

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    a. 在 [單一登入方法] 中，選取 [SAML 2]。

    b. 在 hello **IDP 登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。

    c. 在 hello **IDP 登出 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。

    d. 在 hello **IDP 憑證指紋**文字方塊中，貼上 hello**指紋**您從 Azure 入口網站複製的值...

    e. 在 hello 名稱識別碼格式的文字方塊中，輸入 hello 值**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-: emailAddress**。

    f. 在 hello 驗證內容文字方塊中，輸入 hello 值**urn: oasis： 名稱： tc: SAML:2.0:ac:classes:PasswordProtectedTransport**。

    g. 按一下 [儲存] 。  

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-liquidfiles-test-user"></a>建立 LiquidFiles 測試使用者

hello 本節目標在於 toocreate LiquidFiles 中呼叫許 Simon 的使用者。 使用您 LiquidFiles 伺服器系統管理員 tooget 自行新增的使用者身分登入 tooyour LiquidFiles 應用程式之前。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooLiquidFiles 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooLiquidFiles，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**LiquidFiles**。

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。

當您按一下的 hello LiquidFiles 磚 hello 存取面板中時，您應該取得自動登入 tooyour LiquidFiles 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

