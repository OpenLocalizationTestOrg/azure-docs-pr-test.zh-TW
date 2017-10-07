---
title: "教學課程：Azure Active Directory 與 TimeOffManager 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 TimeOffManager 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>教學課程：Azure Active Directory 與 TimeOffManager 整合

在此教學課程中，您學會如何 toointegrate TimeOffManager 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 TimeOffManager 可以提供下列優點 hello:

- 您可以控制存取 tooTimeOffManager Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooTimeOffManager （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 與 TimeOffManager 的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 TimeOffManager 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫新增 TimeOffManager
2. 設定和測試 Azure AD 單一登入

## <a name="add-timeoffmanager-from-hello-gallery"></a>從 hello 圖庫新增 TimeOffManager
tooconfigure hello 整合 TimeOffManager 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd TimeOffManager。

**tooadd TimeOffManager 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**TimeOffManager**，選取**TimeOffManager**從結果面板，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![從資源庫新增](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 TimeOffManager 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 TimeOffManager 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello TimeOffManager 中相關的使用者之間的連結關聯性需要 toobe 建立。

TimeOffManager 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。

tooconfigure 及測試 Azure AD 單一登入 TimeOffManager，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave 許 Simon TimeOffManager 所連結的 toohello Azure AD 使用者表示法中對應項目。
4. **[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 TimeOffManager 的應用程式中。

**tooconfigure Azure AD 單一登入 TimeOffManager，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **TimeOffManager**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![SAML 型登入](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. 在 hello **TimeOffManager 網域和 Url**區段中，執行下列 hello:

     ![[TimeOffManager 網域與 URL] 區段](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE] 
    > 這不是真實的值。 更新此值與 hello 實際的回覆 URL。 您可以取得此值從**單一登入設定 頁面**這稍後會加以說明 hello 教學課程中或連絡[TimeOffManager 支援小組](http://www.timeoffmanager.com/contact-us.aspx)。
 
4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooTimeOffManger 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。
    
    TimeOffManger 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML token 屬性設定。 hello 下列螢幕擷取畫面會顯示這個範例。

    ![saml 權杖屬性](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml 權杖屬性")
    
    | 屬性名稱 | 屬性值 |
    | --- | --- |
    | Firstname |User.givenname |
    | lastname |User.surname |
    | 電子郵件 |User.mail |
    
    a.  上述的 hello 資料表中每個資料列，按一下 **新增使用者屬性**。
    
    ![saml 權杖屬性](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml 權杖屬性")
    
    ![saml 權杖屬性](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml 權杖屬性")
    
    b.  在 hello**屬性名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。
    
    c.  在 hello**屬性值**文字方塊中，顯示該資料列選取 hello 屬性值。
    
    d.  按一下 [確定] 。
    
6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. 在 hello **TimeOffManager 組態**區段中，按一下**設定 TimeOffManager** tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![[TimeOffManager 設定] 區段](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 TimeOffManager 公司網站。

9. 跳過**帳戶\>帳戶選項\>單一登入設定**。
   
   ![單一登入設定](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "單一登入設定")
7. 在 hello**單一登入設定**區段中，執行下列步驟的 hello:
   
   ![單一登入設定](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "單一登入設定")
   
   a. 在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後貼上 hello 整個憑證**X.509 憑證**文字方塊。
   
   b. 在**Idp 簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。
   
   c. 在**IdP 端點 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。
   
   d. 在 [強制 SAML] 選取 [否]。
   
   e. 在 [自動建立使用者] 選取 [是]。
   
   f. 在**登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。
   
   g. 按一下 [儲存變更]。

11. 在**單一登入設定**頁面上，複製 hello 值**判斷提示取用者服務 URL**並將它貼在 hello**回覆 URL**底下的文字方塊**TimeOffManager網域和 Url** Azure 入口網站中的區段。 

      ![單一登入設定](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "單一登入設定")

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![[使用者和群組] --> [所有使用者]](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![[新增] 按鈕](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![使用者對話方塊頁面](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="create-a-timeoffmanager-test-user"></a>建立 TimeOffManager 測試使用者

在順序 tooenable Azure AD 使用者 toolog 入 TimeOffManager，它們必須已佈建的 tooTimeOffManager。  

TimeOffManager 支援即時使用者佈建。 沒有您適用的動作項目。  

會自動在 hello 第一個登入使用單一登入期間新增 hello 使用者。

>[!NOTE]
>您可以使用任何其他 TimeOffManager 使用者帳戶建立工具或 Api 提供 TimeOffManager tooprovision Azure AD 使用者帳戶。
> 

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 tooTimeOffManager 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooTimeOffManager，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**TimeOffManager**。

    ![應用程式清單中的 TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下 hello TimeOffManager 磚 hello 存取面板中的時，您應該取得自動登入 tooyour TimeOffManager 的應用程式。 如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

