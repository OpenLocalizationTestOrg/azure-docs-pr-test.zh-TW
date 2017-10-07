---
title: "教學課程：Azure Active Directory 與 Front 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與前端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a>教學課程：Azure Active Directory 與 Front 整合

在此教學課程中，您學會如何 toointegrate 與 Azure Active Directory (Azure AD) 的前面。

與 Azure AD 整合前端可以提供下列優點 hello:

- 您可以控制存取 tooFront Azure AD 中。
- 您可以啟用您的使用者 tooautomatically get 登入 tooFront （單一登入） 具有其 Azure AD 帳戶。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

前端 tooconfigure Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Front 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 正在將前端從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-front-from-hello-gallery"></a>正在將前端從 hello 組件庫
tooconfigure hello 整合前端到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 前面。

**tooadd 前端 hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**前端**，選取**前端**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![Hello [結果] 清單中的最上層](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Front 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 對應的使用者在前面是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與前面 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

在最前面，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入前的，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立最上層測試使用者](#create-a-front-test-user)** -toohave 對應項目許 Simon 前面所連結的 toohello Azure AD 使用者表示法。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並在最上層應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入前，以執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello**前端**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. 在 hello**前端網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    a. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.frontapp.com`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.frontapp.com/sso/saml/callback`

4. 請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.frontapp.com`
     
    > [!NOTE] 
    > 這些都不是真正的值。 這些值與 hello 實際識別項、 回覆 URL 和登入 URL 稍後在教學課程中或連絡所說明的更新[前端用戶端支援小組](mailto:support@frontapp.com)tooget 這些值。 

5. 在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. 在 hello**前端組態**區段中，按一下**設定前端**tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. 以系統管理員身分登入 tooyour 最上層租用戶。

9. 跳過**設定 （齒輪圖示在 hello 左提要欄位中的 hello 底部） > 喜好設定**。
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. 按一下 [單一登入]  連結。
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. 選取**SAML** hello 下拉式清單中**單一登入**。
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. 在 hello**進入點**文字方塊放 hello 值**單一登入服務 URL**從 Azure AD 應用程式組態精靈。
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. 開啟您下載**Certificate(Base64)** [記事本]，複製 hello 到剪貼簿，它的內容中，然後將它貼入 toohello **Signing certificate**文字方塊。
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. 在 hello**服務提供者設定**區段中，執行下列步驟的 hello:

    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    a. 複製 hello 值**實體識別碼**並將它貼到 hello**識別碼** 文字方塊中的**前端網域和 Url** Azure 入口網站中的區段。

    b. 複製 hello 值**ACS URL**並將它貼到 hello**登入 URL**  文字方塊中的**前端網域和 Url** Azure 入口網站中的區段。
    
15. 按一下 [儲存]  按鈕。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. 在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![hello [使用者] 對話方塊](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    a. 在 hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。

    d. 按一下 [建立] 。
 
### <a name="create-a-front-test-user"></a>建立 Front 測試使用者

在本節中，您會於 Front 建立名為 Britta Simon 的使用者。 使用[前端用戶端支援小組](mailto:support@frontapp.com)hello 前端平台中新增 hello 使用者。 您必須先建立和啟動使用者，然後才能使用單一登入。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooFront 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooFront，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**前端**。

    ![hello 應用程式清單中的 hello 前方連結](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您使用 Azure AD SSOconfiguration hello 存取面板。

當您按一下 hello 前面的圖格 hello 存取面板中時，您應該取得自動登入 tooyour 前端應用程式。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

