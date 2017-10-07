---
title: "教學課程：Azure Active Directory 與 Velpic SAML 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Velpic SAML 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a>教學課程：Azure Active Directory 與 Velpic SAML 整合

在此教學課程中，您學會如何 toointegrate Velpic SAML 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Velpic SAML 可以提供下列優點 hello:

- 您可以控制存取 tooVelpic SAML 的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooVelpic SAML （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Velpic SAML 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Velpic SAML 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Velpic SAML
2. 設定並測試 Azure AD 單一登入

## <a name="adding-velpic-saml-from-hello-gallery"></a>從 hello 圖庫加入 Velpic SAML
tooconfigure hello 整合 Velpic SAML 到 Azure AD，您需要 tooadd Velpic SAML hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Velpic SAML 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Velpic SAML**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. 在 hello 結果 窗格中，選取  **Velpic SAML**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Velpic SAML 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Velpic saml 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Velpic saml 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Velpic saml。

tooconfigure 及 Velpic SAML 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave 許 Simon Velpic saml 連結的 toohello Azure AD 表示她的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 Velpic SAML 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Velpic SAML，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站上 hello **Velpic SAML**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. 輸入 hello 詳細資料中 hello **Velpic SAML 網域和 Url**區段-

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    a. 在 hello**登入 URL**文字方塊中，做為型別 hello 值：`https://<sub-domain>.velpicsaml.net`

    b. 在 hello**識別碼**文字方塊中，貼上 hello **'的單一登入 URL'**值`https://auth.velpic.com/saml/v2/<entity-id>/login`
    
    > [!NOTE]
    > 請注意，將由 hello Velpic SAML 小組提供 hello 登入 URL 識別項的值可設定 hello SSO 外掛程式 Velpic SAML 端時。 您需要 toocopy 來自 Velpic SAML 應用程式頁面上的值並貼至此處。

4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. 在 hello Velpic SAML 組態] 區段中，按一下 [設定 Velpic SAML tooopen 設定登入視窗。 複製 hello 快速參考 > 一節中的 hello SAML 實體識別碼。

7. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Velpic SAML 公司網站。

8. 按一下**管理**索引標籤上，並移過**整合**區段需要 tooclick**外掛程式**登入按鈕 toocreate 新外掛程式。

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. 按一下 hello **'加入外掛程式'**  按鈕。
    
    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. 按一下 hello **SAML**磚 hello 新增外掛程式網頁中。
    
    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. 輸入新 SAML 外掛程式 hello hello 名稱，然後按一下 hello **'Add'**  按鈕。

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. 輸入 hello 詳細資料，如下所示：

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    a. 在 hello**名稱**文字方塊中，型別 hello SAML 外掛程式名稱。

    b. 在 hello**簽發者 URL**文字方塊中，貼上 hello **SAML 實體識別碼**您所複製的 hello**設定登入**hello Azure 入口網站視窗。

    c. 在 hello**提供者中繼資料組態**上載 hello 中繼資料 XML 檔案，您從 Azure 入口網站下載檔案。

    d. 您也可以選擇 tooenable SAML 即時佈建藉由啟用 hello **'自動建立新的使用者'**核取方塊。 如果使用者不存在於 Velpic，而且沒有啟用這個旗標，從 Azure 的 hello 登入將會失敗。 如果 hello 旗標已啟用的 hello 使用者會自動佈建到 Velpic 在 hello 登入時間。 

    e. 複製 hello**單一登入 URL**從 hello 文字方塊中，然後貼上在 hello Azure 入口網站。
    
    f. 按一下 [儲存] 。

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-velpic-saml-test-user"></a>建立 Velpic SAML 測試使用者

此步驟為通常不需要 hello 應用程式支援即時使用者佈建。 如果未啟用 hello 自動使用者佈建然後建立手動使用者即可，如下所述。

以系統管理員身分登入您的 Velpic SAML 公司網站，然後執行下列步驟：
    
1. 按一下 管理 索引標籤上並移 tooUsers 區段中，然後按一下新按鈕 tooadd 使用者。

    ![新增使用者](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. 在 hello **「 建立新的使用者 」**對話方塊頁面上，執行下列步驟的 hello。

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    a. 在 hello**名字**文字方塊中，類型許 Simon 的 hello 名字。

    b. 在 hello**姓氏**文字方塊中，類型許 Simon 的 hello 最後一個名稱。

    c. 在 hello**使用者名**文字方塊中，輸入 hello 的使用者名稱，Simon 許。

    d. 在 [hello**電子郵件**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。

    e. 其餘的 hello 資訊是選擇性的您可以填入必要的。
    
    f. 按一下 [儲存] 。  

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooVelpic SAML 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooVelpic SAML，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Velpic SAML**。

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

1. 當您按一下的 hello Velpic SAML 磚 hello 存取面板中時，您應該取得 Velpic SAML 應用程式的登入頁面。 您應該會看見 hello **'登入 Azure AD'** hello 登入頁面上的按鈕。

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. 按一下 hello **'登入 Azure AD'**按鈕 toolog tooVelpic 使用 Azure AD 帳戶中的。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

