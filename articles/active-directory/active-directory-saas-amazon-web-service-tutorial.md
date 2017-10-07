---
title: "教學課程：Azure Active Directory 與 Amazon Web Services (AWS) 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Amazon Web Services (AWS) 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>教學課程：Azure Active Directory 與 Amazon Web Services (AWS) 整合

在此教學課程中，您學會如何 toointegrate Amazon Web Services (AWS) 與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Amazon Web Services (AWS) 可以提供下列優點 hello:

- 您可以控制存取 tooAmazon Web Services (AWS) 的 Azure AD 中
- 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooAmazon Web Services (AWS) （單一登入）
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 整合與 Amazon Web Services (AWS)，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Amazon Web Services (AWS) 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 新增 Amazon Web Services (AWS) 從 hello 組件庫
2. 設定並測試 Azure AD 單一登入

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>新增 Amazon Web Services (AWS) 從 hello 組件庫
tooconfigure hello 整合 Amazon Web Services (AWS) 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Amazon Web Services (AWS)。

**tooadd Amazon Web Services (AWS) 從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新增**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Amazon Web Services (AWS)**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. 在 [hello [結果] 窗格中，選取 [ **Amazon Web Services (AWS)**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Amazon Web Services (AWS) 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Amazon Web Services (AWS) 是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 hello 相關的使用者在 Amazon Web Services (AWS) 之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Amazon Web Services (AWS)。

tooconfigure 及 Amazon Web Services (AWS) 與 Azure AD 單一登入測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立測試使用者 Amazon Web Services](#creating-an-amazon-web-services-test-user) ** -toohave 許 Simon 在 Amazon Web Services (AWS) 是連結的 toohello Azure AD 的她的表示法的對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並在 Amazon Web Services (AWS) 應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入與 Amazon Web Services (AWS) 中，執行下列步驟的 hello:**

1. 在 hello Azure 網站上 hello **Amazon Web Services (AWS)**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. 在 [hello **Amazon Web Services (AWS) 網域和 Url**區段中，hello 使用者沒有 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. 在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。
    
    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. hello Amazon Web Services (AWS) 的軟體應用程式預期 hello SAML 判斷提示，以特定格式。 請設定下列宣告為此應用程式的 hello。 您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。 hello 下列螢幕擷取畫面會顯示這個範例。

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. 在 hello**使用者屬性**區段 hello**單一登入**] 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:
    
    | 屬性名稱  | 屬性值 | 命名空間 |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | user.userprincipalname | https://aws.amazon.com/SAML/Attributes |
    | 角色            | user.assignedroles |  https://aws.amazon.com/SAML/Attributes |
    
    >[!TIP]
    >您需要 tooconfigure hello 使用者佈建在 Azure AD toofetch AWS 主控台全部 hello 角色。 請參閱 hello 佈建步驟。

    a. 按一下**加入屬性**tooopen hello**加入屬性**對話方塊。

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. 在 [hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. 從 hello**值**清單，顯示該資料列的型別 hello 屬性值。 指定上方加入 hello 命名空間值。
    
    d. 按一下 [確定] 。

7. 按一下**儲存**toosave hello 設定在 Azure 上的按鈕。

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. 在不同的瀏覽器視窗中，以系統管理員身分登入 tooyour Amazon Web Services (AWS) 公司網站。

9. 按一下 [主控台首頁] 。
   
    ![設定單一登入][11]

10. 從 [安全性、身分識別與合規性] 服務按一下 [IAM]。
   
    ![設定單一登入][12]

11. 按一下 [識別提供者]，然後按一下 [建立提供者]。
   
    ![設定單一登入][13]

12. 在 [hello**設定提供者**對話方塊頁面上，執行下列步驟的 hello:
   
    ![設定單一登入][14]
 
    a. 針對 [提供者類型]，選取 [SAML]。

    b. 在 [hello**提供者名稱**文字方塊中，輸入提供者名稱 (例如： *WAAD*)。

    c. tooupload 您下載的中繼資料檔案中，按一下 [**選擇檔案**。

    d. 按一下頁面底部的 [新增] 。

13. 在 [hello**驗證提供者資訊**對話方塊頁面上，按一下 [**建立**。 
    
    ![設定單一登入][15]

14. 按一下 [角色]，然後按一下 [建立新角色]。 
    
    ![設定單一登入][16]

15. 在 [hello**設定角色名稱**] 對話方塊中，執行下列步驟的 hello: 
    
    ![設定單一登入][17] 

    a. 在 [hello**角色名稱**文字方塊中，輸入角色名稱 (例如： *TestUser*)。 

    b. 按一下頁面底部的 [新增] 。

16. 在 [hello**選取角色類型**] 對話方塊中，執行下列步驟的 hello: 
    
    ![設定單一登入][18] 

    a. 選取 [識別提供者存取的角色]。 

    b. 在 [hello**授與網頁單一登入 (WebSSO) 存取 tooSAML 提供者**區段中，按一下**選取**。

17. 在 [hello**建立信任**] 對話方塊中，執行下列步驟的 hello:  
    
    ![設定單一登入][19] 

    a. 為 SAML 提供者中，選取您先前建立的 hello SAML 提供者 (例如： *WAAD*)
  
    b. 按一下頁面底部的 [新增] 。

18. 在 [hello**確認角色信任**] 對話方塊中，按一下**下一個步驟**。
    
    ![設定單一登入][32]

19. 在 [hello**附加原則**] 對話方塊中，按一下 [**下一個步驟**。
    
    ![設定單一登入][33]

20. 在 [hello**檢閱**] 對話方塊中，執行下列步驟的 hello:
    
    ![設定單一登入][34]
 
    a. 按一下 [建立角色]。

    b. 建立所需的角色，並將它們對應 toohello 身分識別提供者。

21. 現在設定 hello 使用者佈建 toofetch AWS 全部 hello 角色

    a. 使用根帳號的 hello AWS 主控台登入

    b. 在右下角的 hello 頂端按一下您名稱，然後按一下 [hello**我的安全性認證**選項。 這會開啟一個畫面顯示警告訊息。 按一下 [hello] 按鈕**安全性認證**按鈕 toopass hello 螢幕。
        
       ![設定單一登入][36]

       ![設定單一登入][37]

    c. 在 [hello 便捷鍵區段按一下 hello**建立新的存取金鑰**] 按鈕。 這會產生存取金鑰識別碼 hello 和語彙基元的值。
    
       ![設定單一登入][38]

    d. 複製這兩個值，同時加以下載，您才不會遺失它。

    e. 在 [hello Azure 入口網站中，在 hello Amazon Web Services (AWS) 應用程式整合頁面上，按一下 [**佈建**。
        
       ![設定單一登入][35]

    f. Hello 佈建模式設定太**自動**
        
       ![設定單一登入][39]

    g. 現在在 hello **clientsecret**和**密碼語彙基元**hello 對應值，您從 AWS 主控台] 複製貼上。
    
    h. 您可以按一下 hello**測試連接**按鈕 tootest hello 連線。 一旦成功，就可以開始佈建連接器 hello。
       
       ![設定單一登入][40]

    i. 現在啟用 hello 佈建狀態太**上**。 這樣會啟動擷取 hello 角色從 hello 應用程式。

       ![設定單一登入][41]

    > [!NOTE]
    > 執行 azure AD 佈建服務每個從 AWS 某些時間 toosync hello 角色之後。 您應該會看到所有 hello 身分識別提供者都連接至 Azure AD AWS 角色，而且您可以指派 hello 應用程式 toousers 或群組時使用它們。

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. 跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. 在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-an-amazon-web-services-test-user"></a>建立 Amazon Web Services 測試使用者

在訂單 tooenable Azure AD 使用者 toolog tooAmazon Web Services (AWS) 中，它們必須佈建到 Amazon Web Services (AWS)。 在 hello 案例 Amazon Web Services (AWS) 中，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟的 hello:**

1. 登入 tooyour **Amazon Web Services (AWS)**以系統管理員身分的公司網站。

2. 按一下 hello**主控台首頁**圖示。 
   
    ![設定單一登入][11]

3. 按一下 [身分識別與存取管理]。 
   
    ![設定單一登入][28]

4. 在 [hello 儀表板，按一下 [**使用者**，然後按一下 [**建立新的使用者**。 
   
    ![設定單一登入][29]

5. Hello 建立使用者在對話方塊上，執行下列步驟的 hello: 
   
    ![設定單一登入][30]   
    
    a. 在 [hello**輸入使用者名稱**等文字方塊中，輸入 Brita Simon 的使用者名稱 (userprincipalname) 在 Azure AD 中。

    b. 按一下 [建立]。
        
### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooAmazon Web Services (AWS)。

![指派使用者][200] 

**tooassign 許 Simon tooAmazon Web Services (AWS)，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Amazon Web Services (AWS)**。

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 在**選取角色**索引標籤，選取 hello hello 使用者適當的角色。 所有這些角色會顯示 hello 角色名稱以及身分識別提供者名稱。 如此一來，您可以輕鬆地識別 AWS hello 角色。

8. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。

當您按一下的 hello Amazon Web Services (AWS) 磚 hello 存取面板中時，您應該取得自動登入 tooyour Amazon Web Services (AWS) 應用程式。 

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
