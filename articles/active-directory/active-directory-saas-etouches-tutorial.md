---
title: "教學課程：Azure Active Directory 與 etouches 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 etouches 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a>教學課程：Azure Active Directory 與 etouches 整合

在此教學課程中，您學會如何 toointegrate etouches 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 etouches 可以提供下列優點 hello:

- 您可以控制存取 tooetouches Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooetouches （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure etouches 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 etouches 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 etouches
2. 設定並測試 Azure AD 單一登入

## <a name="adding-etouches-from-hello-gallery"></a>從 hello 圖庫加入 etouches
tooconfigure hello 整合 etouches 到 Azure AD，您需要 tooadd etouches hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd etouches 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**etouches**，選取**etouches**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![etouches hello [結果] 清單中](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 etouches 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 etouches 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello etouches 中相關的使用者之間的連結關聯性需要 toobe 建立。

Etouches 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 etouches 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 etouches](#create-an-etouches-test-user)**  -toohave 是連結的 toohello Azure AD 使用者表示法的 etouches 的許 Simon 的對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 etouches 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 etouches，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **etouches**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. 在 hello **etouches 網域和 Url**區段中，執行下列步驟的 hello:

    ![etouches 網域及 URL 單一登入資訊](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.eiseverywhere.com/<instance name>`

    > [!NOTE] 
    > 這些都不是真正的值。 您可以更新 hello 值與實際的 hello 登入 URL 和識別碼，在 hello 教學課程稍後會說明。
    > 

4. etouches 應用程式預期 hello SAML 判斷提示，以特定格式。 設定下列宣告為此應用程式的 hello。 您可以從 hello 管理這些屬性的 hello 值**使用者屬性**hello 應用程式。 hello 下列螢幕擷取畫面會顯示這個範例。 

    ![使用者屬性](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. 在 hello**使用者屬性**hello 區段**單一登入** 對話方塊中，hello 映像中所示設定 SAML 權杖屬性並執行下列步驟的 hello:
    
    | 屬性名稱 | 屬性值 |
    | ------------------- | -------------------- |
    | 電子郵件 | user.mail |    
    
    a. 按一下**加入屬性**tooopen hello**加入屬性**對話方塊。

    ![新增屬性](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![[新增屬性] 對話方塊](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    b. 在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。

    c. 從 hello**值**清單，顯示該資料列的型別 hello 屬性值。
    
    d. 按一下 [確定] 。 

6. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. tooget SSO 設定應用程式執行下列步驟在 hello etouches 應用程式中的 hello: 

    ![etouches 組態](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    a. 登入太**etouches**使用 hello 系統管理員權限的應用程式。
   
    b. 移 toohello **SAML**組態。

    c. 在 [hello**一般設定**區段中，開啟下載的憑證，從 Azure 入口網站，在記事本中，複製 hello 內容，然後貼到 hello IDP 中繼資料] 文字方塊。 

    d. 按一下 hello**儲存，並保持** 按鈕。
  
    e. 按一下 hello**更新中繼資料**hello SAML 中繼資料 區段中的按鈕。 

    f. 隨即會開啟 hello 頁面，並執行 SSO。 一次 hello SSO 運作，您可以設定 hello 使用者名稱。

    g. 在 hello 使用者名稱 欄位中，選取 hello **emailaddress** hello 圖所示。 

    h. 複製 hello**預存程序的實體識別碼**值並貼到 hello**識別碼**文字方塊中，位於**etouches 網域和 Url** Azure 入口網站上的一節。

    i. 複製 hello **SSO URL / ACS**值並貼到 hello**登入 URL**文字方塊中，位於**etouches 網域和 Url** Azure 入口網站上的一節。
   
> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="create-an-etouches-test-user"></a>建立 etouches 測試使用者

在本節中，您會於 etouches 建立名為 Britta Simon 的使用者。 使用[etouches 用戶端支援小組](https://www.etouches.com/event-software/support/customer-support/)tooadd hello hello etouches 平台的使用者。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooetouches 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooetouches，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**etouches**。

    ![hello 應用程式清單中的 hello etouches 連結](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入


hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。

當您按一下的 hello etouches 磚 hello 存取面板中時，您應該取得自動登入 tooyour etouches 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

