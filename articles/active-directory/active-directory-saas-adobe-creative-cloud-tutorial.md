---
title: "教學課程：Azure Active Directory 與 Adobe Creative Cloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Adobe 創意雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>教學課程：Azure Active Directory 與 Adobe Creative Cloud 整合

在此教學課程中，您學會如何 toointegrate Adobe c 雲端與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Adobe 創意雲端可以提供下列優點 hello:

- 您可以控制存取 tooAdobe 創意雲端的 Azure AD 中
- 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooAdobe 創意雲端 （單一登入）
- 您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 Adobe 創意雲端的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Adobe Creative Cloud 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Adobe 創意雲端
2. 設定並測試 Azure AD 單一登入

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>從 hello 圖庫加入 Adobe 創意雲端
tooconfigure hello 整合 Adobe 創意雲端的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Adobe 創意雲端。

**tooadd Adobe 創意雲端 hello 圖庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Adobe 創意雲端**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. 在 [hello [結果] 窗格中，選取 [ **Adobe 創意雲端**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Adobe Creative Cloud 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Adobe 創意雲端中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Adobe 創意雲端中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Adobe 創意雲端中。

tooconfigure 和測試 Azure AD 單一登入與 Adobe 創意雲端，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Adobe 創意雲端](#creating-an-adobe-creative-cloud-test-user)** -toohave 許 Simon Adobe 創意雲端是連結的 toohello Azure AD 的她的表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入 Adobe 創意雲端應用程式中。

**以 Adobe 創意雲端，Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**

1. 在 hello Azure 管理入口網站上 hello **Adobe 創意雲端**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. 在 [hello **Adobe 創意雲端網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. 在 [hello**識別碼**文字方塊中，做為型別 hello 值：`https://www.okta.com/saml2/service-provider/<token>`

    b. 在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > 請注意這些不是 hello 實際值。 您有 tooupdate hello 實際的識別項和回覆 url 的這些值。 這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。 若要手動 toocreate 使用者，您會需要 toocontact hello Adobe 創意雲端支援小組。

4. 在 [hello **Adobe 創意雲端網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **SP**初始模式：

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. 按一下 hello**顯示進階的 URL 設定**選項

    b. 在 [hello**登入 URL**文字方塊中，做為型別 hello 值：`https://adobe.com`

5. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. 在 [hello **Adobe 創意雲端組態**區段中，按一下**設定 Adobe 創意雲端**tooopen**設定登入**視窗。 請將複製 hello **SAML 實體識別碼**和**SAML SSO 服務 URL**從快速參考 > 一節。

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Adobe 創意雲端租用戶。

8.  跳過**識別**在 hello 左側的導覽窗格中，按一下您的網域。 然後執行下列步驟 hello**單一登入需要設定**> 一節。

    ![設定](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "設定")

9. 按一下**瀏覽**tooupload hello 下載憑證從 Azure AD 太**IDP 憑證**。

10. 在 [hello **IDP 簽發者**文字方塊中，將 hello 值放**SAML 實體識別碼**您複製從**設定登入**Azure 入口網站中的區段。

11. 在 [hello **IDP 登入 URL**文字方塊中，將 hello 值放**SAML SSO 服務 URL**您複製從**設定登入**Azure 入口網站中的區段。

12. 選取 [HTTP - 重新導向] 作為 **IDP 繫結**。

13. 選取 [電子郵件地址] 作為**使用者登入設定**。
 
14. 按一下 [儲存]  按鈕。

15. hello 儀表板現在會呈現 hello XML **「 下載中繼資料 」**檔案。 它包含 Adobe 的 EntityDescriptor URL 和 AssertionConsumerService URL。 請開啟 hello 檔案，並在 hello Azure AD 應用程式中設定它們。

    ![在應用程式端設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![在應用程式端設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. 使用 hello EntityDescriptor 值 Adobe 提供您輸入**識別碼**上 hello**設定應用程式設定**對話方塊。

    b. 使用 hello AssertionConsumerService 值 Adobe 提供您輸入**回覆 URL**上 hello**設定應用程式設定**對話方塊。
 
### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>建立 Adobe Creative Cloud 測試使用者

在訂單 tooenable Azure AD 使用者 toolog 到 Adobe 創意雲端，您必須是佈建到 Adobe 創意雲端。  
在 Adobe 創意雲端的 hello 情況下，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟 hello:**

1. 登入 tooyour Adobe 創意雲端公司站台系統管理員身分。

2. 按一下 [人員] 。

    ![人員](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "人員")

3. 按一下 [邀請使用者] 。

    ![邀請使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "邀請使用者")

4. 在 [hello**邀請人員**對話方塊頁面上，執行下列步驟的 hello:

    ![邀請人員](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "邀請人員")

    a. 在 [hello**電子郵件**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。
    
    b. 按一下 [邀請] 。

    > [!NOTE]
    > hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooAdobe 創意雲端啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooAdobe 創意雲端中，執行下列步驟的 hello:**

1. 在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Adobe 創意雲端**。

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello Adobe 創意雲端磚 hello 存取面板中的時，您應該取得自動登入 tooyour Adobe 創意雲端應用程式。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png