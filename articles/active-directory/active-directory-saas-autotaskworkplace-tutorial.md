---
title: "教學課程：Azure Active Directory 與 Autotask Workplace 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間 Autotask 工作地點。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a>教學課程：Azure Active Directory 與 Autotask Workplace

在此教學課程中，您學會如何 toointegrate Autotask 與 Azure Active Directory (Azure AD) 的工作場所。

與 Azure AD 整合 Autotask 工作地點可以提供下列優點 hello:

- 您可以控制存取 tooAutotask 工作地點的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooAutotask （單一登入） 的工作地點使用其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Autotask 工作場所的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Autotask Workplace 單一登入功能的訂用帳戶
- 您必須是工作地點的系統管理員或進階系統管理員。
- Hello Azure AD 中，您必須擁有系統管理員帳戶。
- 會利用這項功能的 hello 使用者必須具有內工作地點和 hello Azure AD 的帳戶，而且兩個電子郵件地址必須相符。

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. Autotask 工作地點加入從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-autotask-workplace-from-hello-gallery"></a>Autotask 工作地點加入從 hello 組件庫
tooconfigure hello 整合 Autotask 工作區到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Autotask 工作地點。

**tooadd Autotask 工作場所 hello 圖庫中，從執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory] 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**Autotask 工作場所**，選取**Autotask 工作場所**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。

    ![Autotask 工作場所中 hello 結果清單](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Autotask Workplace 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Autotask 工作地點中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Autotask 工作地點中的相關的使用者之間的連結關聯性需要 toobe 建立。

Autotask 工作地點中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 和測試 Azure AD 單一登入的 Autotask 工作地點網路，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Autotask 工作地點的測試使用者](#create-an-autotask-workplace-test-user)** -toohave 許 Simon Autotask 工作地點所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Autotask 工作場所應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入的 Autotask 工作地點網路，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Autotask 工作場所**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入連結][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. 如果您想 tooconfigure hello 應用程式中的**IDP**起始模式中，執行下列步驟在 hello hello **Autotask 工作場所網域和 Url** > 一節：

    ![IDP 的 Autotask Workplace 網域和 URL 單一登入資訊](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    a. 在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`

    b. 在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`

4. 如果您想 tooconfigure hello 應用程式中的**SP**初始的模式中，核取**顯示進階的 URL 設定**並執行下列步驟的 hello:

    ![SP 的 Autotask Workplace 網域和 URL 單一登入資訊](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.awp.autotask.net/loginsso`
     
    > [!NOTE] 
    > 這些都不是真正的值。 更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。 請連絡[Autotask 工作地點的用戶端支援小組](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)tooget 這些值。 

5. 在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. 在不同的網頁瀏覽器視窗中，tooWorkplace 線上使用登入 hello 系統管理員認證。

    >[!Note]
    >當設定 hello IdP，子網域必須 toobe 指定。 tooconfirm hello 正確子網域，登入 tooWorkplace 線上。 登入之後，請注意 toohello 子網域 hello URL 中。
    >hello 子網域屬於 hello hello"https://"和".awp.autotask.net/ 」 之間，而且應該是我們、 eu、 ca 或 au 登錄。

8. 跳過**組態** > **單一登入**並執行下列步驟的 hello:

    ![Autotask 單一登入組態](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    a. 選取 hello **XML 中繼資料檔**選項，然後再上傳 hello**中繼資料 XML**從 Azure 入口網站下載。

    b. 按一下 [啟用 SSO]。
    
    ![Autotask 單一登入核准組態](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    c. 選取 hello**我確認這項資訊是否正確，以及我信任此 IdP**核取方塊。

    d. 按一下 [核准]。
     
>[!Note]
>如果您需要設定 Autotask 工作地點的協助，請參閱[本頁](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)tooget 協助您工作場所帳戶。

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. 在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![hello [使用者] 對話方塊](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    a. 在 [hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。

    d. 按一下 [建立] 。

### <a name="create-an-autotask-workplace-test-user"></a>建立 Autotask Workplace 測試使用者

在本節中，您會在 Autotask 中建立名為 Britta Simon 的使用者。 請使用[Autotask 工作場所支援小組](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)tooadd hello hello Autotask 工作場所平台的使用者。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooAutotask 工作地點。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooAutotask 工作地點，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Autotask 工作場所**。

    ![hello Autotask 工作場所 hello 應用程式清單中的連結](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下的 hello Autotask 工作場所磚 hello 存取面板中時，您應該取得自動登入 tooyour Autotask 工作場所應用程式。
如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

