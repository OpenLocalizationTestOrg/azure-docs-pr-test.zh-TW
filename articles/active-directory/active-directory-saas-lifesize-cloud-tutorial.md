---
title: "教學課程：Azure Active Directory 與 Lifesize Cloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Lifesize 雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a>教學課程：Azure Active Directory 與 Lifesize Cloud 整合

在此教學課程中，您學會如何 toointegrate Lifesize 雲端與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Lifesize 雲端可以提供下列優點 hello:

- 您可以控制存取 tooLifesize 雲端的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooLifesize （單一登入） 的雲端與他們的 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 Lifesize 雲端的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Lifesize Cloud 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Lifesize 雲端
2. 設定並測試 Azure AD 單一登入

## <a name="adding-lifesize-cloud-from-hello-gallery"></a>從 hello 圖庫加入 Lifesize 雲端
tooconfigure hello 整合 Lifesize 雲端的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Lifesize 雲端。

**tooadd Lifesize 雲端 hello 圖庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Lifesize 雲端**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. 在 hello 結果 窗格中，選取  **Lifesize 雲端**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Lifesize Cloud 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Lifesize 雲端中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Lifesize 雲端中的相關的使用者之間的連結關聯性需要 toobe 建立。

Lifesize 雲端中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 和測試 Azure AD 單一登入與 Lifesize 雲端，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Lifesize 雲端](#creating-a-lifesize-cloud-test-user)** -toohave 許 Simon Lifesize 雲端是連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Lifesize 雲端應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Lifesize 雲端中，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Lifesize 雲端**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. 在 hello **Lifesize 雲端網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://login.lifesizecloud.com/ls/?acs`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://login.lifesizecloud.com/<companyname>`

     
4. 請檢查**顯示進階的 URL 設定**，執行下列步驟的 hello:  
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    在 hello**轉送狀態**文字方塊中，輸入 URL，使用下列模式的 hello:`https://webapp.lifesizecloud.com/?ent=<identifier>`
   
   > [!NOTE] 
   >請注意這些不是 hello 實際值。 這些值以 hello 有 tooupdate 實際的登入 URL、 轉送狀態和識別項。 請連絡[Lifesize 雲端的用戶端支援小組](https://www.lifesize.com/support)tooget 登入 URL 和識別碼值與您可以從在 hello 教學課程稍後會說明的 SSO 組態取得轉送的狀態值。

4. 在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. 在 hello **Lifesize 雲端組態**區段中，按一下**設定 Lifesize 雲端**tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. tooget SSO 設定您的應用程式登入 hello Lifesize 雲端應用程式，以管理員權限。

8. 在右下角的 hello 頂端按一下您的名稱，然後按一下 hello**提前設定**。
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. 在 hello 提前設定現在按一下 hello **SSO 組態**連結。 它會開啟 hello SSO 組態 頁面上執行個體。
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. 現在設定 hello hello SSO 組態 UI 中的值。    
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    a. 在**身分識別提供者簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。

    b.  在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。

    c. 從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中開啟 base-64 編碼的憑證，然後將它貼入 toohello **X.509 憑證**文字方塊。
  
    d. 在 [hello SAML 屬性對應 hello 第一個名稱] 文字方塊中的輸入 hello 值做為**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**
    
    e. 在 hello SAML 屬性對應中的 hello**姓氏**文字方塊中，輸入 hello 值做為**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**
    
    f. 在 hello SAML 屬性對應中的 hello**電子郵件**文字方塊中，輸入 hello 值做為**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**

11. 您可以按一下 hello toocheck hello 組態**測試** 按鈕。
   
    >[!NOTE]
    >測試成功 toocomplete hello 設定精靈 需要在 Azure AD 中與也提供存取 toousers 或群組，讓他們可以執行 hello 測試。

12. 藉由檢查 hello 上啟用 hello SSO**啟用 SSO**  按鈕。

13. 現在按一下 hello**更新**按鈕，使所有 hello 設定會都儲存。 這會產生 hello RelayState 值。 複製 hello RelayState 值，也就產生 hello 文字方塊中，將它貼在 hello**轉送狀態**底下的文字方塊中**Lifesize 雲端網域和 Url** > 一節。 

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者

hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-lifesize-cloud-test-user"></a>建立 Lifesize Cloud 測試使用者

在本節中，您要在 Lifesize Cloud 中建立名為 Britta Simon 的使用者。 Lifesize Cloud 支援自動使用者佈建。 驗證成功後在 Azure AD，hello 使用者將會自動佈建 hello 應用程式中。 

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooLifesize 雲端啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooLifesize 雲端中，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Lifesize 雲端**。

    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下的 hello Lifesize 雲端磚 hello 存取面板中時，您應該取得 Lifesize 雲端應用程式的登入頁面。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

