---
title: "教學課程：Azure Active Directory 與 ServiceNow 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ServiceNow 和 ServiceNow Express 之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>教學課程：Azure Active Directory 與 ServiceNow 整合
在此教學課程中，您學會如何 toointegrate ServiceNow 和 ServiceNow Express with Azure Active Directory (Azure AD)。

與 Azure AD 整合 ServiceNow 和 ServiceNow Express 可以提供下列優點 hello:

* 您可以控制存取 tooServiceNow Azure AD 和 ServiceNow Express
* 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooServiceNow 和 ServiceNow 快速 （單一登入）
* 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
tooconfigure Azure AD 與 ServiceNow 和 ServiceNow Express 整合，您需要下列項目 hello:

* Azure AD 訂用帳戶
* 若為 ServiceNow，ServiceNow 的執行個體或租用戶 (Calgary 版本或更新版本)
* 若為 ServiceNow Express，ServiceNow Express 的執行個體 (Helsinki 版本或更新版本)
* hello ServiceNow 租用戶必須擁有 hello[多個提供者單一登入外掛程式](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0)啟用。 [提交服務要求](https://hi.service-now.com)即可達到此目的。 

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。
> 
> 

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

* 除非必要，否則您不應使用生產環境，。
* 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 ServiceNow
2. 為 ServiceNow 或 ServiceNow Express 設定和測試 Azure AD 單一登入

## <a name="adding-servicenow-from-hello-gallery"></a>從 hello 圖庫加入 ServiceNow
tooconfigure hello 整合 ServiceNow 或 ServiceNow Express 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd ServiceNow。 

**tooadd ServiceNow hello 圖庫中，從執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。 
   
    ![Active Directory][1]
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式][2]
4. 按一下**新增**hello hello 頁底端。
   
    ![應用程式][3]
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![應用程式][4]
6. 在 [hello] 搜尋方塊中，輸入**ServiceNow**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. 在 hello 結果窗格中，選取  **ServiceNow**，然後按一下**完成**tooadd hello 應用程式。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試透過 ServiceNow 或 ServiceNow Express 使用 Azure AD 單一登入功能。

單一登入 toowork，Azure AD 需要 tooknow ServiceNow 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與 ServiceNow 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。
此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** ServiceNow 中。 tooconfigure 及 Azure AD 單一登入與 ServiceNow 的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入 servicenow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable 使用者 toouse 這項功能。
2. **[設定 Azure AD 單一登入 ServiceNow 快速](#configuring-azure-ad-single-sign-on-for-servicenow-express)** -tooenable 使用者 toouse 這項功能。
3. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
4. **[建立測試使用者 ServiceNow](#creating-a-servicenow-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 ServiceNow 中對應項目。
5. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
6. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

> [!NOTE]
> 如果您想要 tooconfigure ServiceNow 略過步驟 2。 同樣地，如果您想要 tooconfigure ServiceNow Express 略過步驟 1。
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>為 ServiceNow 設定 Azure AD 單一登入
1. Hello Azure AD 傳統入口網站中，在 hello **ServiceNow**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊.
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749323.png "設定單一登入")

2. 在 hello**如何想您使用者 toosign tooServiceNow 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749324.png "設定單一登入")

3. 在 hello**設定應用程式設定**頁面上，執行下列步驟的 hello:
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "設定應用程式 URL")
   
    a. 在 hello **ServiceNow 登入 URL**文字方塊中，輸入您使用者 toosign 上 tooyour ServiceNow 的應用程式遵循 hello 模式所使用的 URL: `https://<instance-name>.service-now.com`。
   
    b. 在 hello**識別碼**文字方塊中，輸入您使用者 toosign 上 tooyour ServiceNow 的應用程式遵循 hello 模式所使用的 URL: `https://<instance-name>.service-now.com`。
   
    c. 按一下 [下一步] 

4. toohave Azure AD 自動設定 ServiceNow SAML 型驗證中，輸入 ServiceNow 執行個體名稱、 管理員使用者名稱，以及系統管理員密碼 hello**自動設定單一登入**按一下*設定*。 請注意提供該 hello 管理員使用者名稱必須具有 hello **security_admin**此 toowork ServiceNow 中指派的角色。 否則，toomanually 設定 ServiceNow toouse Azure AD 做為 SAML 身分識別提供者，請按一下**手動設定進行單一登入的 hello 應用程式**，然後按一下 **下一步**和完整的 hello下列步驟。
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "設定應用程式 URL")

5. 在 hello**在 ServiceNow 設定單一登入**頁面上，按一下**下載憑證**，儲存在本機電腦上的 hello 憑證檔案。
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749325.png "設定單一登入")

6. 登入 tooyour ServiceNow 的應用程式系統管理員身分。

7. 啟動 hello*整合的多個提供者單一登入安裝程式*依照外掛程式 hello 接下來的步驟：
   
    a. Hello hello 左側瀏覽窗格中移過**系統定義**區段，然後按一下**外掛程式**。
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "啟動外掛程式")
   
    b. 搜尋*整合 - 多個提供者單一登入安裝程式*。
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "啟動外掛程式")
   
    c. 選取 hello 外掛程式。 按一下滑鼠右鍵並選取 [啟動/升級]。
   
    d. 按一下 hello **Activate**  按鈕。

8. Hello hello 左側瀏覽窗格中按一下**屬性**。  
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "設定應用程式 URL")

9. 在 [hello**多個提供者 SSO 屬性**] 對話方塊中，執行下列步驟的 hello:
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "設定應用程式 URL")
   
    a. 針對 [啟用多個提供者 SSO]，選取 [是]。
   
    b. 做為**啟用偵錯記錄收到 hello 多個提供者 SSO 整合**，選取**是**。
   
    c. 在**hello 欄位 hello 使用者資料表，其中...**文字方塊中，輸入**user_name**。
   
    d. 按一下 [儲存] 。

10. Hello hello 左側瀏覽窗格中按一下**x509 憑證**。
    
     ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "設定單一登入")

11. 在 hello **X.509 憑證** 對話方塊中，按一下 **新增**。
    
     ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "設定單一登入")

12. 在 [hello **X.509 憑證**] 對話方塊中，執行下列步驟的 hello:
    
     ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "設定單一登入")
    
     a. 按一下 [新增] 。
    
     b. 在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： **TestSAML2.0**)。
    
     c. 選取 [使用中] 。
    
     d. 針對 [格式]，選取 [PEM]。
    
     e. 針對 [類型]，選取 [信任存放區憑證]。
    
     f. 開啟 [記事本]，複製到剪貼簿，其內容的 hello 的 Base64 編碼的憑證，然後將它貼入 toohello **PEM 憑證**文字方塊。
    
     g. 按一下 [更新] 。

13. Hello hello 左側瀏覽窗格中按一下**身分識別提供者**。
    
     ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "設定單一登入")

14. 在 hello**身分識別提供者** 對話方塊中，按一下 **新增**:
    
     ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "設定單一登入")

15. 在 hello**身分識別提供者** 對話方塊中，按一下  **SAML2 Update1？**:
    
     ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "設定單一登入")

16. Hello SAML2 Update1 屬性 對話方塊中，執行下列步驟的 hello:
    
     ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "設定單一登入")

    a. 在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： **SAML 2.0**)。

    b. 在 hello**使用者欄位**文字方塊中，輸入**電子郵件**或**user_name**，取決於哪一個欄位使用 toouniquely 識別您的 ServiceNow 部署中的使用者。 

    > [!NOTE] 
    > 您可以設定 Azure AD tooemit 任一 hello Azure AD 使用者識別碼 （使用者主體名稱），或為所要 toohello hello hello SAML 權杖中的唯一識別碼 hello 電子郵件地址**ServiceNow > 屬性 > 單一登入**區段hello Azure 傳統入口網站和對應所需的 hello 欄位 toohello **nameidentifier**屬性。 hello 選屬性儲存在 Azure AD （例如使用者主體名稱） 中的 hello 值必須符合 hello 值儲存在 ServiceNow 中的 hello 輸入欄位 （例如使用者名稱）

    c. 在傳統入口網站 hello Azure AD，複製 hello**身分識別提供者識別碼**值並貼到 hello**身分識別提供者 URL**文字方塊。

    d. 在傳統入口網站 hello Azure AD，複製 hello**驗證要求 URL**值並貼到 hello**身分識別提供者的 AuthnRequest**文字方塊。

    e. 在傳統入口網站 hello Azure AD，複製 hello**單一登出服務 URL**值並貼到 hello**身分識別提供者 SingleLogoutRequest**文字方塊。

    f. 在 hello **ServiceNow 首頁**文字方塊中，您的 ServiceNow 執行個體首頁的型別 hello URL。

    > [!NOTE] 
    > hello ServiceNow 執行個體首頁是串連您**ServieNow 租用戶 URL**和**/navpage.do** (例如：`https://fabrikam.service-now.com/navpage.do`)。

    g. 在 hello**實體識別碼 / 簽發者**文字方塊中，您的 ServiceNow 租用戶的型別 hello URL。

    h. 在 hello**觀眾 URL**文字方塊中，您的 ServiceNow 租用戶的型別 hello URL。 

    i. 在 hello**通訊協定繫結 hello IDP 的 SingleLogoutRequest**文字方塊中，輸入**urn: oasis： 名稱： tc: SAML:2.0:bindings:HTTP-重新導向**。

    j. 在 hello NameID 原則文字方塊中，輸入**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-格式： 未指定**。

    k. 取消選取 [建立 AuthnContextClass]。

    l. 在 hello **AuthnContextClassRef 方法**，型別`http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`。 只有您是僅限雲端組織時才需要此值。 如果您使用內部部署 ADFS 或 MFA 進行驗證，則不應該設定這個值。 

    m. 在 [時鐘誤差] 文字方塊中，輸入 **60**。

    n. 針對**單一登入指令碼**，選取 **MultiSSO_SAML2_Update1**。

    o. 做為**x509 憑證**，選取您已建立 hello 上一個步驟中的 hello 憑證。

    p. 按一下 [提交] 。 

1. 在傳統入口網站 hello Azure AD，選取 hello 單一登入組態確認，然後**下一步**。 
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "設定單一登入")

2. 在 hello**單一登入確認**頁面上，按一下**完成**。
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "設定單一登入")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>為 ServiceNow Express 設定 Azure AD 單一登入
1. Hello Azure AD 傳統入口網站中，在 hello **ServiceNow**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊.
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749323.png "設定單一登入")

2. 在 hello**如何想您使用者 toosign tooServiceNow 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749324.png "設定單一登入")

3. 在 hello**設定應用程式設定**頁面上，執行下列步驟的 hello:
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "設定應用程式 URL")
   
    a. 在 hello **ServiceNow 登入 URL**文字方塊中，輸入您使用者 toosign 上 tooyour ServiceNow 的應用程式遵循 hello 模式所使用的 URL: `https://<instance-name>.service-now.com`。
   
    b. 在 hello**簽發者 URL**文字方塊中，輸入您使用者 toosign 上 tooyour ServiceNow 的應用程式遵循 hello 模式所使用的 URL `https://<instance-name>.service-now.com`。
   
    c. 按一下 [下一步] 

4. 按一下**手動設定 hello 應用程式的單一登入**，然後按一下 **下一步**和 hello 完成下列步驟。
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "設定應用程式 URL")

5. 在 hello**在 ServiceNow 設定單一登入**頁面上，按一下**下載憑證**，儲存在本機電腦上的 hello 憑證檔案，然後按一下**下一步**。
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749325.png "設定單一登入")

6. 登入 tooyour ServiceNow Express 應用程式，以系統管理員。

7. Hello hello 左側瀏覽窗格中按一下**單一登入**。  
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "設定應用程式 URL")

8. 在 [hello**單一登入**] 對話方塊中，按一下向右鍵和設定 hello 下列屬性的 hello 上限 hello 組態圖示：
   
    ![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "設定應用程式 URL")
   
    a. 切換**啟用多個提供者 SSO** toohello 權限。
   
    b. 切換**啟用偵錯記錄多個提供者 SSO 整合 hello** toohello 權限。
   
    c. 在**hello 欄位 hello 使用者資料表，其中...**文字方塊中，輸入**user_name**。
9. 在 hello**單一登入** 對話方塊中，按一下 **加入新的憑證**。
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "設定單一登入")
10. 在 [hello **X.509 憑證**] 對話方塊中，執行下列步驟的 hello:
    
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "設定單一登入")
    
    a. 在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： **TestSAML2.0**)。
    
    b. 選取 [使用中] 。
    
    c. 針對 [格式]，選取 [PEM]。
    
    d. 針對 [類型]，選取 [信任存放區憑證]。
    
    e. 從您下載的憑證建立 Base64 編碼的檔案。
    
    > [!NOTE]
    > 如需詳細資訊，請參閱[如何 tooconvert 二進位憑證到文字檔](http://youtu.be/PlgrzUZ-Y1o)。
    > 
    > 
    
    f. 開啟 [記事本]，複製到剪貼簿，其內容的 hello 的 Base64 編碼的憑證，然後將它貼入 toohello **PEM 憑證**文字方塊。
    
    g. 按一下 [更新] 。
11. 在 hello**單一登入** 對話方塊中，按一下 **加入新的 IdP**。
    
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "設定單一登入")
12. 在 hello**新增身分識別提供者**對話方塊下方**設定身分識別提供者**，執行下列步驟的 hello:
    
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "設定單一登入")

    a. 在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： **SAML 2.0**)。

    b. 在傳統入口網站 hello Azure AD，複製 hello**身分識別提供者識別碼**值並貼到 hello**身分識別提供者 URL**文字方塊。

    c. 在傳統入口網站 hello Azure AD，複製 hello**驗證要求 URL**值並貼到 hello**身分識別提供者的 AuthnRequest**文字方塊。

    d. 在傳統入口網站 hello Azure AD，複製 hello**單一登出服務 URL**值並貼到 hello**身分識別提供者 SingleLogoutRequest**文字方塊。

    e. 做為**身分識別提供者憑證**，選取您已建立 hello 上一個步驟中的 hello 憑證。


1. 按一下**進階設定**，然後在**其他身分識別提供者屬性**，執行下列步驟的 hello:
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "設定單一登入")
   
    a. 在 hello**通訊協定繫結 hello IDP 的 SingleLogoutRequest**文字方塊中，輸入**urn: oasis： 名稱： tc: SAML:2.0:bindings:HTTP-重新導向**。
   
    b. 在 hello **NameID 原則**文字方塊中，輸入**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-格式： 未指定**。    
   
    c. 在 hello **AuthnContextClassRef 方法**，型別**http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**。
   
    d. 取消選取 [建立 AuthnContextClass]。

2. 在下**其他服務提供者內容**，執行下列步驟的 hello:
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "設定單一登入")
   
    a. 在 hello **ServiceNow 首頁**文字方塊中，您的 ServiceNow 執行個體首頁的型別 hello URL。
   
    > [!NOTE]
    > hello ServiceNow 執行個體首頁是串連您**ServieNow 租用戶 URL**和**/navpage.do** (例如： `https://fabrikam.service-now.com/navpage.do`)。
    > 
    > 
   
    b. 在 hello**實體識別碼 / 簽發者**文字方塊中，您的 ServiceNow 租用戶的型別 hello URL。
   
    c. 在 hello**對象 URI**文字方塊中，您的 ServiceNow 租用戶的型別 hello URL。 
   
    d. 在 [時鐘誤差] 文字方塊中，輸入 **60**。
   
    e. 在 hello**使用者欄位**文字方塊中，輸入**電子郵件**或**user_name**，取決於哪一個欄位使用 toouniquely 識別您的 ServiceNow 部署中的使用者。
   
    > [!NOTE]
    > 您可以設定 Azure AD tooemit 任一 hello Azure AD 使用者識別碼 （使用者主體名稱），或為所要 toohello hello hello SAML 權杖中的唯一識別碼 hello 電子郵件地址**ServiceNow > 屬性 > 單一登入**區段hello Azure 傳統入口網站和對應所需的 hello 欄位 toohello **nameidentifier**屬性。 hello 選屬性儲存在 Azure AD （例如使用者主體名稱） 中的 hello 值必須符合 hello 值儲存在 ServiceNow 中的 hello 輸入欄位 （例如使用者名稱）
    > 
    > 
   
    f. 按一下 [儲存] 。 

3. 在傳統入口網站 hello Azure AD，選取 hello 單一登入組態確認，然後**下一步**。 
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "設定單一登入")

4. 在 hello**單一登入確認**頁面上，按一下**完成**。
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "設定單一登入")

## <a name="configuring-user-provisioning"></a>設定使用者佈建
hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooServiceNow。

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure 使用者佈建，執行下列步驟的 hello:
1. Hello 管理 Azure 傳統入口網站中，在 hello **ServiceNow**應用程式整合頁面上，按一下 **設定使用者佈建**。 
   
    ![使用者佈建](./media/active-directory-saas-servicenow-tutorial/IC769498.png "使用者佈建")

2. 在 hello**輸入您 ServiceNow 認證 tooenable 自動使用者佈建**頁面上，提供下列組態設定的 hello:
   
     a. 在 hello **ServiceNow 執行個體名稱**文字方塊中，型別 hello ServiceNow 執行個體名稱。
   
     b. 在 hello **ServiceNow 管理使用者名稱**文字方塊中，型別 hello hello ServiceNow 管理員帳戶名稱。
   
     c. 在 hello **ServiceNow 管理員密碼**文字方塊中，此帳戶類型 hello 密碼。
   
     d. 按一下**驗證**tooverify 您的設定。
   
     e. 按一下 hello**下一步**按鈕 tooopen hello**後續步驟**頁面。
   
     f. 如果您想 tooprovision 所有使用者 toothis 應用程式，選取 「**hello 目錄 toothis 應用程式中的所有使用者帳戶自動佈都建**"。 
   
    ![後續步驟](./media/active-directory-saas-servicenow-tutorial/IC698804.png "後續步驟")
   
     g. 在 hello**後續步驟**頁面上，按一下**完成**toosave 您的設定。

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
在本節中，您可以建立測試使用者呼叫許 Simon hello 傳統入口網站中。

![建立 Azure AD 使用者][20]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. 在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. 針對 [使用者類型]，選取 [您組織中的新使用者]。
   
    b. 在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。
   
    c. 按一下 [下一步] 。

6. 在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. 在 hello**名字**文字方塊中，輸入**許**。  
   
   b. 在 hello**姓氏**文字方塊中，輸入， **Simon**。
   
   c. 在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。
   
   d. 在 hello**角色**清單中，選取**使用者**。
   
   e. 按一下 [下一步] 。

7. 在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. 在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. 請記下 hello hello 值**新密碼**。
   
    b. 按一下 [完成]。   

### <a name="creating-a-servicenow-test-user"></a>建立 ServiceNow 測試使用者
在本節中，您要在 ServiceNow 中建立名為 Britta Simon 的使用者。 在本節中，您要在 ServiceNow 中建立名為 Britta Simon 的使用者。 如果您不知道如何 tooadd 您的 ServiceNow 或 ServiceNow Express 中的使用者帳戶，請連絡 ServiceNow 技術支援小組。

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者
在本節中，您可以授與他們存取 tooServiceNow 啟用許 Simon toouse Azure 單一登入。

![指派使用者][200] 

**tooassign 許 Simon tooServiceNow，執行下列步驟的 hello:**

1. Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。
   
    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**ServiceNow**。
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。
   
    ![指派使用者][203] 

4. 在 hello 所有使用者清單中選取**許 Simon**。

5. 在 hello hello 底部的工具列中按一下**指派**。
   
    ![指派使用者][205]

### <a name="testing-single-sign-on"></a>測試單一登入
hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。

當您按一下 hello ServiceNow 磚 hello 存取面板中的時，您應該取得自動登入 tooyour ServiceNow 的應用程式。

## <a name="additional-resources"></a>其他資源
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
