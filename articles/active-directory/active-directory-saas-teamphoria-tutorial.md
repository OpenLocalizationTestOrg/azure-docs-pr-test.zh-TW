---
title: "教學課程：Azure Active Directory 與 Teamphoria 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Teamphoria 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>教學課程：Azure Active Directory 與 Teamphoria 整合

在此教學課程中，您學會如何 toointegrate Teamphoria 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Teamphoria 可以提供下列優點 hello:

- 您可以控制存取 tooTeamphoria Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooTeamphoria （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>必要條件

tooconfigure Teamphoria 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 一個已啟用 Teamphoria 單一登入功能的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Teamphoria
2. 設定並測試 Azure AD 單一登入

## <a name="adding-teamphoria-from-hello-gallery"></a>從 hello 圖庫加入 Teamphoria
tooconfigure hello 整合 Teamphoria 到 Azure AD，您需要 tooadd Teamphoria hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

**tooadd Teamphoria 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Teamphoria**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. 在 [hello [結果] 窗格中，選取 [ **Teamphoria**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Teamphoria 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Teamphoria 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Teamphoria 中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Teamphoria 中。

tooconfigure 及 Teamphoria 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Teamphoria](#creating-a-teamphoria-test-user) ** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Teamphoria 中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 Teamphoria 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Teamphoria，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站上 hello **Teamphoria**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. 在 [hello **Teamphoria 網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    a. 在 [hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello URL:`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > 請注意這些不是 hello 實際值。 這些值以 hello 有 tooupdate 實際的登入 URL。 請連絡[Teamphoria 用戶端支援小組](https://www.teamphoria.com/)tooget hello 登入 URL。 

4. 在 [hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)** ，然後儲存您的電腦上的 [hello 憑證。

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. 在 [hello **Teamphoria 組態**區段中，按一下**設定 Teamphoria** tooopen**設定登入**視窗。 複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. tooconfigure 單一登入上**Teamphoria**側邊，以系統管理員身分登入 tooyour Teamphoria 應用程式。

8. 跳過**系統管理設定**選項 hello 左邊工具列中，在按一下 [設定] 索引標籤的 hello hello**單一登入**tooopen hello SSO 組態視窗。

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. 按一下**新增身分識別提供者**hello 右上角 tooopen hello 在表單中加入 hello SSO 設定的選項。

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. Hello 欄位中輸入 hello 詳細資料，如所述的以下層

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    a. **顯示名稱**: hello] 管理頁面上輸入 hello 外掛程式 hello 顯示名稱。

    b. **按鈕名稱**: hello hello] 索引標籤會顯示在 hello 登入頁面上，針對透過 SSO 登入名稱。

    c. **憑證**： 開啟 hello 憑證之前下載從 hello Azure 入口網站在 「 記事本 」 中的 hello 複製 hello 內容相同，並將它這裡貼 hello 方塊中。

    d. **進入點**： 貼上 hello **SAML 單一登入服務 URL**複製舊版表單 hello Azure 入口網站。

    e. 切換 hello 選項太**ON** ，然後按一下 [**儲存**。 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-teamphoria-test-user"></a>建立 Teamphoria 測試使用者

在訂單 tooenable Azure AD 使用者 toolog Teamphoria 成，它們必須佈建到 Teamphoria。 中的 Teamphoria hello 案例中，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟 hello:**

1. 登入 tooyour Teamphoria 公司網站的系統管理員身分。

2. 按一下**管理員**設定 hello 左工具列上，並在 [hello**管理**索引標籤處按一下**使用者**tooopen hello 管理頁面的使用者。

    ![新增員工](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. 按一下 hello**手動邀請**選項。

    ![邀請人員](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. 在這個頁面上執行下列動作。 
    
    ![邀請人員](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    a. 在 [hello**電子郵件地址**文字方塊中，hello**電子郵件地址**BrittaSimon。

    b. 在 [hello**名字**文字方塊中，輸入**許**。

    c. 在 [hello**姓氏**文字方塊中，輸入**Simon**。

    d. 按一下 [邀請 1 位使用者]。 使用者需要 tooaccept hello 邀請 tooget hello 系統中建立。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooTeamphoria 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooTeamphoria，執行下列步驟的 hello:**

1. 在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Teamphoria**。

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

如果要測試您的單一登入設定，請開啟存取面板。 如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](https://msdn.microsoft.com/library/dn308586)。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

