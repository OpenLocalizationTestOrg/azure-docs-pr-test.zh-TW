---
title: "教學課程：Azure Active Directory 與 Litmos 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Litmos 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a>教學課程：Azure Active Directory 與 Litmos 整合

在此教學課程中，您學會如何 toointegrate Litmos 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Litmos 可以提供下列優點 hello:

- 您可以控制存取 tooLitmos Azure AD 中。
- 您可以啟用您的使用者 tooautomatically get 登入 tooLitmos （單一登入） 具有其 Azure AD 帳戶。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Litmos 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Litmos 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Litmos
2. 設定並測試 Azure AD 單一登入

## <a name="adding-litmos-from-hello-gallery"></a>從 hello 圖庫加入 Litmos
tooconfigure hello 整合 Litmos 到 Azure AD，您需要 tooadd Litmos hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Litmos 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**Litmos**，選取**Litmos**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![Litmos hello [結果] 清單中](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Litmos 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Litmos 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Litmos 中相關的使用者之間的連結關聯性需要 toobe 建立。

Litmos 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及 Litmos 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Litmos](#create-a-litmos-test-user)**  -toohave 許 Simon Litmos 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Litmos 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Litmos，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Litmos**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. 在 hello **Litmos 網域和 Url**區段中，執行下列步驟的 hello:

    ![Litmos 網域及 URL 單一登入資訊](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    a. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.litmos.com/account/Login`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.litmos.com/integration/samllogin`

    > [!NOTE] 
    > 這些都不是真正的值。 這些值以 hello 實際識別項和回覆 URL 更新，稍後在教學課程中或連絡說明[Litmos 支援小組](https://www.litmos.com/contact-us/)tooget 這些值。

4. 在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. Hello 組態的一部分，您需要 toocustomize hello **SAML 權杖屬性**Litmos 應用程式。

    ![屬性區段](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | 屬性名稱   | 屬性值 |   
    | ---------------  | ----------------|
    | 名字 |user.givenname |
    | 姓氏  |user.surname |
    | 電子郵件 |user.mail |

    a. 按一下**加入屬性**tooopen hello**加入屬性**對話方塊。

    ![新增屬性](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![新增屬性對話方塊](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    b. 在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。

    c. 從 hello**值**清單，顯示該資料列的型別 hello 屬性值。
    
    d. 按一下 [確定] 。     

6. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. 在不同的瀏覽器視窗中，以系統管理員身分登入 tooyour Litmos 公司網站。

8. 在 hello hello 左側導覽列中按一下**帳戶**。
   
    ![應用程式端的帳戶區段][22] 

9. 按一下 hello**整合** 索引標籤。
   
    ![整合索引標籤][23] 

10. 在 hello**整合**索引標籤上，向下捲動太**第 3 個合作對象整合**，然後按一下 **SAML 2.0**  索引標籤。
   
    ![SAML 2.0 區段][24] 

11. 複製下的 hello 值**litmos 是 hello SAML 端點：**並將它貼到 hello**回覆 URL**  文字方塊中 hello **Litmos 網域和 Url** Azure 入口網站中的區段。 
   
    ![SAML 端點][26] 

12. 在您**Litmos**應用程式中，執行下列步驟的 hello:
    
     ![Litmos 應用程式][25] 
     
     a. 按一下 [啟用 SAML] 。
    
     b. 在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **SAML X.509 憑證**文字方塊。
     
     c. 按一下 [儲存變更] 。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. 在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![hello [使用者] 對話方塊](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    a. 在 hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。

    d. 按一下 [建立] 。
  
### <a name="create-a-litmos-test-user"></a>建立 Litmos 測試使用者

hello 本節目標在於 toocreate Litmos 中呼叫許 Simon 的使用者。  
hello Litmos 應用程式支援恰好在時間佈建。 這表示，使用者帳戶會自動建立必要期間嘗試 tooaccess hello 應用程式使用存取面板 hello。

**toocreate 呼叫許 Simon Litmos，在使用者執行下列步驟的 hello:**

1. 在不同的瀏覽器視窗中，以系統管理員身分登入 tooyour Litmos 公司網站。

2. 在 hello hello 左側導覽列中按一下**帳戶**。
   
    ![應用程式端的帳戶區段][22] 

3. 按一下 hello**整合** 索引標籤。
   
    ![整合索引標籤][23] 

4. 在 hello**整合**索引標籤上，向下捲動太**第 3 個合作對象整合**，然後按一下 **SAML 2.0**  索引標籤。
   
    ![SAML 2.0][24] 
    
5. 選取 [自動產生使用者]
   
    ![自動產生使用者][27] 

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooLitmos 啟用許 Simon toouse Azure 單一登入。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooLitmos，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Litmos**。

    ![hello 應用程式清單中的 hello Litmos 連結](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。  

當您按一下的 hello Litmos 磚 hello 存取面板中時，您應該取得自動登入 tooyour Litmos 應用程式。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

