---
title: "教學課程：Azure Active Directory 與 Procore SSO 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Procore SSO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>教學課程：Azure Active Directory 與 Procore SSO 整合

在此教學課程中，您學會如何 toointegrate Procore SSO 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Procore SSO 可以提供下列優點 hello:

- 您可以控制存取 tooProcore SSO 的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooProcore SSO （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>必要條件

tooconfigure Procore SSO 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Procore SSO 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Procore SSO
2. 設定並測試 Azure AD 單一登入

## <a name="adding-procore-sso-from-hello-gallery"></a>從 hello 圖庫加入 Procore SSO
tooconfigure hello 整合 Procore SSO 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Procore SSO。

**tooadd Procore SSO hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Procore SSO**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. 在 hello 結果 窗格中，選取  **Procore SSO**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Procore SSO 設定及測試 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow Procore SSO 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello Procore SSO 中相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Procore SSO 中。

tooconfigure 及測試 Azure AD 單一登入與 Procore SSO，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Procore SSO](#creating-a-procore-sso-test-user)**  -toohave 許 Simon Procore SSO 是連結的 toohello Azure AD 的她的表示法中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 Procore SSO 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入使用 Procore SSO，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站上 hello **Procore SSO**應用程式整合頁面上，按一下 **單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. 在 hello **Procore SSO 網域和 Url**區段中，hello 使用者沒有 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. 在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. 在 hello **Procore SSO 組態**區段中，按一下**設定 Procore SSO** tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. tooconfigure 單一登入上**Procore SSO**端時，系統管理員身分登入 tooyour procore 公司網站。

8. 從 hello 工具箱卸除向下，按一下 [ **Admin** tooopen hello SSO 設定] 頁面。

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. 貼上的 hello 值為 hello 方塊中所述以下-

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    a. 在 hello**單一登入簽發者 URL**方塊中，貼上從 hello Azure 入口網站複製 SAML 實體識別碼 hello。

    b. 在 hello **SAML 登入目標 URL**方塊中，貼上的 hello 從 hello Azure 入口網站複製的 SAML 單一登入服務 URL。

    c. 現在開啟 hello**中繼資料 XML**上方 hello Azure 入口網站和名為 hello 標記中的複製 hello 憑證從下載**X509Certificate**。 貼上 hello 複製值到 hello**單一登入 x509 憑證**方塊。

10. 按一下 [儲存變更]。

11. 這些設定之後，您需要 toosend hello**網域名稱**(例如**contoso.com**) 透過它您登入 Procore toohello [Procore 支援小組](https://support.procore.com/)，它們將啟動該網域同盟的 SSO。

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-procore-sso-test-user"></a>建立 Procore SSO 測試使用者

請遵循以下步驟 toocreate Procore 測試使用者的 hello 邊。

1. 以系統管理員身分登入 tooyour procore 公司網站。  

2. 從 hello 工具箱卸除向下，按一下 [**目錄**tooopen hello 公司目錄] 頁面。

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. 按一下**新增人員**選項 tooopen hello 表單，並輸入下列選項-執行

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    a. 在 hello**名字**文字方塊中，類型使用者的名字，例如**許**。

    b. 在 hello**姓氏**文字方塊中，類型使用者的姓氏，例如**Simon**。

    c. 在 hello**電子郵件地址**文字方塊中，類型使用者的電子郵件地址喜歡 **BrittaSimon@contoso.com** 。

    d. 將 [權限範本] 選取為 [稍後套用權限範本]。

    e. 按一下 [建立] 。

4. 檢查並更新如 hello 新增連絡人的 hello 詳細資料。

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. 按一下**儲存和傳送 Invitiation** （需要透過郵件邀請時） 或**儲存**（直接儲存） toocomplete hello 使用者註冊。
    
    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，您可以授與他們存取 tooProcore SSO 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooProcore SSO，執行下列步驟的 hello:**

1. 在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Procore SSO**。

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

如果要測試您的單一登入設定，請開啟存取面板。 如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](https://msdn.microsoft.com/library/dn308586)。 當您按一下 hello Procore SSO 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Procore SSO 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

