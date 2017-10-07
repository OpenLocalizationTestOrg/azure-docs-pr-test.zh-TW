---
title: "教學課程：Azure Active Directory 與 Zscaler ZSCloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Zscaler ZSCloud 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a>教學課程：Azure Active Directory 與 Zscaler ZSCloud 整合

在此教學課程中，您學會如何 toointegrate Zscaler ZSCloud 與 Azure Active Directory (Azure AD)。

Zscaler ZSCloud 整合與 Azure AD 可以提供下列優點 hello:

- 您可以控制存取 tooZscaler ZSCloud 的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooZscaler ZSCloud （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Zscaler ZSCloud 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Zscaler ZSCloud 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Zscaler ZSCloud
2. 設定並測試 Azure AD 單一登入

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a>從 hello 圖庫加入 Zscaler ZSCloud
tooconfigure hello 整合 Zscaler ZSCloud 的 Azure AD，您需要 tooadd Zscaler ZSCloud hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Zscaler ZSCloud 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Zscaler ZSCloud**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. 在 hello 結果 窗格中，選取  **Zscaler ZSCloud**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Zscaler ZSCloud 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Zscaler ZSCloud 中是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Zscaler ZSCloud 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Zscaler ZSCloud 中。

tooconfigure 及測試 Azure AD 單一登入 Zscaler ZSCloud，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[設定 proxy 設定](#configuring-proxy-settings)** -tooconfigure hello 在 Internet Explorer proxy 設定
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Zscaler ZSCloud 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Zscaler ZSCloud 應用程式中。

**tooconfigure Azure AD 單一登入 Zscaler ZSCloud 中，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Zscaler ZSCloud**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. 在 hello **Zscaler ZSCloud 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     在 hello**登入 URL**文字方塊中，您的使用者 」 toosign 上 ZScaler ZSCloud 應用程式 tooyour 所使用的型別 hello URL。
    
    > [!NOTE] 
    > 具有這個值與 hello tooupdate 實際的登入 URL。 請連絡[Zscaler ZSCloud 用戶端支援小組](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint)tooget 此值。 
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. 在 hello **Zscaler ZSCloud 設定**區段中，按一下**設定 Zscaler ZSCloud** tooopen**設定登入**視窗。 複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. 在不同的網頁瀏覽器視窗中，以登入 tooyour ZScaler ZSCloud 公司網站的系統管理員。

8. 在 hello 最上層顯示 hello 功能表上，按一下**管理**。
   
    ![管理](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "管理")

9. 在 [管理系統管理員和角色] 下按一下 [管理使用者和驗證]。   
            
    ![管理使用者和驗證](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "管理使用者和驗證")

10. 在 hello**選擇驗證選項，為您的組織**區段中，執行下列步驟的 hello:   
                
    ![驗證](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "驗證")
   
    a. 選取 [使用 SAML 單一登入進行驗證] 。

    b.這是另一個 C# 主控台應用程式。 按一下 [設定 SAML 單一登入參數] 。

11. 在 hello**設定 SAML 單一登入參數**對話方塊頁面上，執行下列步驟，hello，然後按一下**完成**

    ![單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "單一登入")
    
    a. 貼上 hello **SAML 單一登入服務 URL**值傳入 hello **hello SAML 入口網站 toowhich 使用者的 URL 會傳送驗證**文字方塊。
    
    b. 在 hello**屬性包含登入名稱**文字方塊中，輸入**NameID**。
    
    c. tooupload 下載的憑證，按一下  **Zscaler pem**。
    
    d. 選取 [啟用 SAML 自動佈建] 。

12. 在 hello**設定使用者驗證**對話方塊頁面上，執行下列步驟的 hello:

    ![管理](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "管理")
    
    a. 按一下 [儲存] 。

    b.這是另一個 C# 主控台應用程式。 按一下 [立即啟用] 。

## <a name="configuring-proxy-settings"></a>進行 Proxy 設定
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>在 Internet Explorer tooconfigure hello proxy 設定

1. 啟動 **Internet Explorer**。

2. 選取**網際網路選項**從 hello**工具**功能表開啟 hello**網際網路選項**對話方塊。   
    
     ![網際網路選項](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "網際網路選項")

3. 按一下 hello**連線** 索引標籤。   
  
     ![連線](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "連線")

4. 按一下**LAN 設定**tooopen hello **LAN 設定**對話方塊。

5. 在 hello Proxy 伺服器區段中，執行下列步驟的 hello:   
   
    ![Proxy 伺服器](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy 伺服器")

    a. 選取 [在您的區域網路使用 Proxy 伺服器]。

    b. 在 [hello 位址] 文字方塊中輸入**gateway.zscalerone.ne**。

    c. 在 [hello 連接埠] 文字方塊中，輸入**80**。

    d. 選取 [近端網址不使用 Proxy 伺服器] 。

    e. 按一下**確定**tooclose hello**區域網路 (LAN) 設定**對話方塊。

6. 按一下**確定**tooclose hello**網際網路選項**對話方塊。

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。

### <a name="creating-a-zscaler-zscloud-test-user"></a>建立 Zscaler ZSCloud 測試使用者

tooenable Azure AD 使用者 toolog 中 tooZScaler ZSCloud，它們必須已佈建的 tooZScaler ZSCloud。  
在 ZScaler ZSCloud 的 hello 案例中，佈建須手動進行。

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure 使用者佈建，執行下列步驟的 hello:

1. 登入 tooyour **Zscaler**租用戶。

2. 按一下 [系統管理] 。   
   
    ![管理](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "管理")

3. 按一下 [使用者管理] 。   
        
     ![新增](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "新增")

4. 在 hello**使用者**索引標籤上，按一下 **新增**。
      
    ![新增](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "新增")

5. 在 hello 新增使用者 區段中，執行下列步驟的 hello:
        
    ![新增使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "新增使用者")
   
    a. 型別 hello **UserID**，**使用者顯示名稱**，**密碼**，**確認密碼**，然後選取**群組**和 hello**部門**想 tooprovision 之有效 AAD 帳戶。

    b. 按一下 [儲存] 。

> [!NOTE]
> 您可以使用任何其他 ZScaler ZSCloud 使用者帳戶建立工具或 Api 提供 ZScaler ZSCloud tooprovision AAD 使用者帳戶。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與存取 tooZscaler ZSCloud 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooZscaler ZSCloud 中，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Zscaler ZSCloud**。

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。

當您按一下的 hello Zscaler ZSCloud 磚 hello 存取面板中時，您應該取得自動登入 tooyour Zscaler ZSCloud 應用程式。

如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

