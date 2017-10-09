---
title: "教學課程：Azure Active Directory 與 Perception United States (非 UltiPro) 整合 |Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與感覺 United States (非 UltiPro) 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>教學課程：Azure Active Directory 與 Perception United States (非 UltiPro) 整合

在此教學課程中，您學會如何 toointegrate 感覺 United States (非 UltiPro) 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合感覺 United States (非 UltiPro) 可以提供下列優點 hello:

- 您可以控制存取 tooPerception 美國 (非 UltiPro) 的 Azure AD 中。
- 您可以啟用您的使用者 tooautomatically get 登入 tooPerception 美國 (非-UltiPro) （單一登入） 具有其 Azure AD 帳戶。
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 整合與感覺 United States (非 UltiPro)，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Perception United States (非 UltiPro) 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入感覺 United States (非 UltiPro)
2. 設定並測試 Azure AD 單一登入

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a>從 hello 圖庫加入感覺 United States (非 UltiPro)
tooconfigure hello 整合的感覺 United States (非 UltiPro) 至 Azure AD，您會需要 tooadd 感覺 United States (非 UltiPro) 從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單。

**tooadd 感覺 United States (非 UltiPro) 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![hello 新應用程式按鈕][3]

4. 在 hello 搜尋方塊中，輸入**感覺 United States (非 UltiPro)**，選取**感覺 United States (非 UltiPro)**然後按一下 從結果面板**新增**按鈕 tooaddhello 應用程式。

    ![Hello 結果清單中的感覺 United States (非 UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入

在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Perception United States (非 UltiPro) 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中感覺 United States (非 UltiPro) 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 相關的使用者的感覺 United States (非 UltiPro) 之間的連結關聯性需要 toobe 建立。

在感覺 United States (非 UltiPro)，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 和測試 Azure AD 單一登入與感覺 United States (非 UltiPro)，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立感覺 United States (非 UltiPro) 測試使用者](#create-a-perception-united-states-non-ultipro-test-user)** -toohave 許 Simon 中感覺 United States (非 UltiPro) 表示法連結的 toohello Azure AD 使用者的對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並感覺 United States (非 UltiPro) 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與感覺 United States (非-UltiPro)，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello**感覺 United States (非 UltiPro)**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入連結][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![單一登入對話方塊](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. 在 hello**感覺 United States (非 UltiPro) 網域和 Url**區段中，執行下列步驟的 hello:

    ![Perception United States (非 UltiPro) 網域與 URL 單一登入資訊](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. 在 hello**識別碼**文字方塊中，型別 hello URL:`https://perception.kanjoya.com/sp`

    b. 在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > hello 值不是真正的。 您將會更新 hello 實際回覆 URL，在 hello 教學課程稍後會說明 hello 值。
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. 在 hello**感覺 United States (非 UltiPro) 組態**區段中，按一下**設定感覺 United States (非 UltiPro)** tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼**從 hello**快速參考 > 一節。**

    a. hello**感覺 United States (非 UltiPro)**應用程式需要 hello **SAML 實體識別碼**值，您已複製，toobe uri 編碼。 tooget hello 編碼的 uri 值，使用 hello 以下連結：**http://www.url-encode-decode.com/**。

    b. 取得 hello uri 之後編碼的值將其與 hello**回覆 URL**如所述的以下層

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. 貼上 hello hello 中的值之上**回覆 URL**  文字方塊中的**感覺 United States (非 UltiPro) 網域和 Url** > 一節。

    ![Perception United States (非 UltiPro) 設定](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. 在另一個瀏覽器視窗中，系統管理員身分登入 tooyour 感覺 United States (非 UltiPro) 公司網站。

8. 在 hello 主要工具列上，按一下 **帳戶設定**。

    ![Perception United States (非 UltiPro) 使用者](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. 在 hello**帳戶設定**頁面上，執行下列步驟的 hello:

    ![Perception United States (非 UltiPro) 使用者](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. 在 hello**公司名稱**文字方塊中，型別 hello 名稱 hello**公司**。
    
    b. 在 hello**帳戶名稱**文字方塊中，型別 hello 名稱 hello**帳戶**。

    c. 在**預設回覆 tooEmail**文字方塊中，有效的型別 hello**電子郵件**。

    d. 為 [SSO 識別提供者] 選取 [SAML 2.0]。

10. 在 hello **SSO 組態**頁面上，執行下列步驟的 hello:

    ![Perception United States (非 UltiPro) SSOConfig](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. 為 [SAML NameID 類型] 選取 [電子郵件]。

    b. 在 hello **SSO 組態名稱**文字方塊中，型別名稱 hello 您**組態**。
    
    c. 在**身分識別提供者名稱**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。 

    d. 在**SAML 網域文字方塊**，輸入 hello 網域，像是 **@contoso.com** 。

    e. 按一下**再次上傳**tooupload hello**中繼資料 XML**檔案。

    f. 按一下 [更新] 。


> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

   ![建立 Azure AD 測試使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。

    ![hello [新增] 按鈕](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. 在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:

    ![hello [使用者] 對話方塊](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. 在 hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。

    d. 按一下 [建立] 。
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>建立 Perception United States (非 UltiPro) 測試使用者

在本節中，您會於 Perception United States (非 UltiPro) 建立名為 Britta Simon 的使用者。 使用[感覺 United States (非 UltiPro) 支援小組](http://www.ultimatesoftware.com/Contact/ContactUs)tooadd hello hello 感覺 United States (非 UltiPro) 平台的使用者。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooPerception 美國 (非 UltiPro)。

![指派 hello 使用者角色][200] 

**tooassign 許 Simon tooPerception 美國 (非-UltiPro)，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**感覺 United States (非 UltiPro)**。

    ![hello 應用程式清單中的 hello 感覺 United States (非 UltiPro) 連結](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202]

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![hello 將作業加入窗格][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello 感覺 United States (非 UltiPro) 磚 hello 存取面板中的時，您應該取得自動登入 tooyour 感覺 United States (非 UltiPro) 應用程式。
如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

