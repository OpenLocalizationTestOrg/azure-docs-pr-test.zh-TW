---
title: "教學課程：Azure Active Directory 與 Asana 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Asana 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a>教學課程：Azure Active Directory 與 Asana 整合

在此教學課程中，您學會如何 toointegrate Asana 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Asana 可以提供下列優點 hello:

- 您可以控制存取 tooAsana Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooAsana （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Asana 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Asana 單一登入功能的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Asana
2. 設定並測試 Azure AD 單一登入

## <a name="adding-asana-from-hello-gallery"></a>從 hello 圖庫加入 Asana
tooconfigure hello 整合 Asana 到 Azure AD，您需要 tooadd Asana hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Asana 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**Asana**，選取**Asana**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Asana 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Asana 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Asana 中相關的使用者之間的連結關聯性需要 toobe 建立。

Asana 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Asana 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Asana](#create-an-asana-test-user)**  -toohave 許 Simon Asana 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Asana 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Asana，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Asana**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. 在 hello **Asana 網域和 Url**區段中，執行下列步驟的 hello:

    ![Asana 網域與 URL 單一登入資訊](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    a. 在 hello**登入 URL**文字方塊中，型別 URL:`https://app.asana.com/`

    b. 在 hello**識別碼**文字方塊中，型別值：`https://app.asana.com/`
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. 在 hello **Asana 組態**區段中，按一下**設定 Asana** tooopen**設定登入**視窗。 複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![Asana 設定](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. 在不同的瀏覽器視窗中，登入 tooyour Asana 應用程式。 tooconfigure Asana，hello hello 右上角的囉 」 畫面上的工作區名稱，即可存取 hello 工作地區設定中的 SSO。 然後，按一下 [\<您的工作區名稱\> 設定]。 
   
    ![Asana sso 設定](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. 在 hello**組織設定**視窗中，按一下 **管理**。 然後，按一下 **成員必須透過 SAML 登入**tooenable hello SSO 組態。 hello 執行 hello 下列步驟：
   
    ![設定單一登入組織設定](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     a. 在 hello**登入頁面 URL**文字方塊中，貼上 hello **SAML 單一登入服務 URL**。

     b. 從 Azure 入口網站下載的 hello 憑證上按一下滑鼠右鍵，然後開啟 hello 憑證檔案，使用 [記事本] 或您慣用的文字編輯器。 Hello 之間複製 hello 內容開始和 hello 結束憑證標題並將它貼在 hello **X.509 憑證**文字方塊。

9. 按一下 [儲存] 。 跳過[Asana 指南來設定 SSO](https://asana.com/guide/help/premium/authentication#gl-saml)如果您需要進一步協助。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![hello [新增] 按鈕](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="create-an-asana-test-user"></a>建立 Asana 測試使用者

在本節中，您要在 Asana 中建立名為 Britta Simon 的使用者。

1. 在**Asana**，go toohello**小組**hello 左面板上的一節。 按一下 hello 加上簽章 按鈕。 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. 輸入 hello 電子郵件britta.simon@contoso.com在 hello 文字方塊中，然後選取 **邀請**。

3. 按一下 [傳送邀請] 。 hello 新使用者會收到一封電子郵件到其電子郵件帳戶。 她將需要 toocreate 並驗證 hello 帳戶。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooAsana 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200]

**tooassign 許 Simon tooAsana，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Asana**。

    ![hello 應用程式清單中的 hello Asana 連結](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

本節目標 hello tootest 是您 Azure AD 單一登入。

移至 tooAsana 登入頁面。 在 hello 電子郵件地址 文字方塊中，插入 hello 電子郵件地址britta.simon@contoso.com。Hello 密碼文字方塊保留空白中，然後按**登入**。 您將會重新導向的 tooAzure AD 登入頁面。 完成您的 Azure AD 認證。 現在，您已在 Asana 上登入。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
