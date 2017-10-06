---
title: "教學課程：Azure Active Directory 與 Salesforce 沙箱整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Salesforce 沙箱之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>教學課程：Azure Active Directory 與 Salesforce 沙箱整合

在此教學課程中，您學會如何 toointegrate 與 Azure Active Directory (Azure AD) 的 Salesforce 沙箱。

整合 Azure AD 與 Salesforce 沙箱可以提供下列優點 hello:

- 您可以控制存取 tooSalesforce 沙箱的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooSalesforce （單一登入） 的沙箱與他們的 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure Azure AD 與 Salesforce 沙箱的整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 啟用 Salesforce Sandbox 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Salesforce 沙箱
2. 設定並測試 Azure AD 單一登入

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a>從 hello 圖庫加入 Salesforce 沙箱
tooconfigure hello 整合 Salesforce 沙箱到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Salesforce 沙箱。

**tooadd Salesforce 沙箱 hello 圖庫中，從執行下列步驟的 hello:**

1. 在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. 按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**Salesforce 沙箱**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. 在 [hello [結果] 窗格中，選取 [ **Salesforce 沙箱**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Salesforce Sandbox 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 [Salesforce 沙箱是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 Salesforce 沙箱中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Salesforce 沙箱中。

tooconfigure 和測試 Azure AD 單一登入與 Salesforce 沙箱，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Salesforce 沙箱測試使用者](#creating-a-salesforce-sandbox-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Salesforce 沙箱中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Salesforce 沙箱應用程式中。

**tooconfigure Azure AD 單一登入與 Salesforce 沙箱，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello **Salesforce 沙箱**應用程式整合頁面上，按一下 [**單一登入**。

    ![設定單一登入][4]

2. 在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. 在 [hello **Salesforce 沙箱網域和 Url**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     在 [hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > 這個值不是真正的 hello。 更新此值與 hello 實際登入 URL。請連絡[Salesforce 沙箱用戶端支援小組](https://help.salesforce.com/support)tooget 此值。


4. 如果您已經在您目錄中，設定單一登入另一個 Salesforce 沙箱的執行個體，則您也必須設定 hello**識別碼**toohave hello 相同的值為 hello**登入 URL**。 
    
    >[!Note]
    >hello**識別碼**欄位可以找到藉由檢查 hello**顯示進階設定**hello 上的核取方塊**設定應用程式 URL** hello 對話方塊頁面 


5. 在 [hello **SAML 簽章憑證**區段中，按一下**憑證**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. 在 [hello **Salesforce 沙箱設定**區段中，按一下**設定 Salesforce 沙箱**tooopen**設定登入**視窗。 複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. 在您的瀏覽器中開啟新索引標籤，並登入 tooyour Salesforce 沙箱管理員帳戶。

9. 在 [hello 最上層顯示 hello 功能表上，按一下**安裝**。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. Hello hello 左側瀏覽窗格中按一下**安全性控制**，然後按一下 [**單一登入設定**。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. Hello 單一登入設定] 區段中，執行下列步驟的 hello:![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     a.  選取 [已啟用 SAML] 。 

     b.這是另一個 C# 主控台應用程式。  按一下 [新增] 。

12. 在 hello SAML 單一登入設定] 區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    a.In hello 名稱文字方塊中，型別 hello hello 組態名稱 (例如： *SPSSOWAAD\_測試*)。 

    b. 貼上**SMAL 實體識別碼**值傳入 hello**簽發者**文字方塊。

    c. 在 [hello**實體識別碼**文字方塊中，輸入**https://test.salesforce.com**便 hello 第一個您要加入 tooyour 目錄的 Salesforce 沙箱執行個體。 如果您已新增執行個體的 Salesforce 沙箱則 hello**實體識別碼**hello 中的型別**登入 URL**，應該採用下列格式：`http://company.my.salesforce.com`  
 
    d. 按一下**瀏覽**tooupload hello 下載憑證。  

    e. 做為**SAML 識別類型**，選取**判斷提示包含從 hello 使用者物件的同盟識別碼 hello**。
 
    f. 做為**SAML 識別位置**，選取**hello 的 hello Subject 陳述式的 NameIdentifier 元素中的識別是**。

    g. 貼上**單一登入服務 URL**到 hello**身分識別提供者登入 URL**文字方塊。 

    h. SFDC 不支援 SAML 登出。  因應措施是，貼上 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello 到**身分識別提供者登出 URL**文字方塊。

    i. 在 [服務提供者起始的要求繫結]，選取 [HTTP POST]。 

    j. 按一下 [儲存] 。

### <a name="enable-your-domain"></a>啟用網域
本節假設您已經建立了一個網域。  如需詳細資訊，請參閱[定義您的網域名稱](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)。

**tooenable 您的網域，執行下列步驟的 hello:**

1. 在 [hello 左側瀏覽窗格中，按一下 [**定義域管理**，然後按一下 [**我的網域。**
   
     ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >請確定您的網域已正確設定。 

2. 在 hello**登入頁面設定**區段中，按一下**編輯**，然後當**驗證服務**，選取 hello 名稱從先前的 hello hello SAML 單一登入設定區段，然後按一下 [最後**儲存**。
   
   ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

當您設定網域之後，您的使用者應該使用 hello 網域 URL toologin toohello Salesforce 沙箱。  

hello URL 的 tooget hello 值，按一下您已建立 hello 前一節中的 hello SSO 設定檔。    

> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. 使用者 toodisplay hello 清單太移**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. 在 [hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>建立 Salesforce Sandbox 測試使用者

本節會在 Salesforce Sandbox 中建立名為 Britta Simon 的使用者。 Salesforce Sandbox 支援預設啟用的 Just-In-Time 佈建。
在這一節沒有您需要進行的動作項目。 如果使用者不存在於 Salesforce 沙箱，當您嘗試 tooaccess Salesforce 沙箱時，會建立一個新。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooSalesforce 沙箱。

![指派使用者][200] 

**tooassign 許 Simon tooSalesforce 沙箱，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**Salesforce 沙箱**。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

如果您想 tootest SSO 設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定使用者佈建](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

