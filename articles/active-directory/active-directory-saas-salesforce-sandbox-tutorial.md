---
title: "教學課程：Azure Active Directory 與 Salesforce 沙箱整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Salesforce 沙箱的單一登入、 自動化佈建，以及更多 ！。"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>教學課程：Azure Active Directory 與 Salesforce 沙箱整合

本教學課程的 hello 目標是 Azure 與 Salesforce 沙箱 tooshow hello 整合。  

>[!TIP]
>如需意見反應，請參閱 hello [Azure 支援頁面](http://go.microsoft.com/fwlink/?LinkId=521878)。 
> 

沙箱提供您將能夠 toocreate hello 的組織在不同的環境，針對各種用途，例如開發、 多個複本，測試和定型集，而不需要犧牲 hello 資料並在您的 Salesforce 生產環境中的應用程式組織。  

如需詳細資訊，請參閱 [沙箱概觀](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* 在 Salesforce.com 中的沙箱

如果您還沒有有效的沙箱在 Salesforce.com 中，您會需要 toocontact Salesforce。

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

1. 啟用 Salesforce 沙箱的 hello 應用程式整合
2. 設定單一登入 (SSO)
3. 啟用您的網域
4. 設定使用者佈建
5. 指派使用者

![案例](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "案例")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>啟用 Salesforce 沙箱的 hello 應用程式整合
本節 hello 目標是 toooutline 如何 Salesforce 沙箱 tooenable hello 應用程式整合。

**tooenable hello 應用程式整合 Salesforce 沙箱，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
   ![應用程式](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "應用程式")
4. tooopen hello**應用程式庫**，按一下 **加入應用程式**，然後按一下**新增應用程式的 我的組織 toouse**。
   
   ![您該怎麼想 toodo？](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "您該怎麼想 toodo？")
5. 在 hello**搜尋方塊**，型別**Salesforce 沙箱**。
   
   ![應用程式資源庫](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "應用程式資源庫")
6. 在 hello 結果窗格中，選取  **Salesforce 沙箱**，然後按一下**完成**tooadd hello 應用程式。
   
   ![Salesforce 沙箱](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce 沙箱")
   
## <a name="configur-single-sign-on-sso"></a>設定單一登入 (SSO)

hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooSalesforce 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。

**tooconfigure 單一登入，請執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **Salesforce 沙箱**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "設定單一登入")
2. 在 hello**如何想您使用者 toosign tooSalesforce 沙箱上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
   ![Salesforce 沙箱](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce 沙箱")
3. Hello 上**設定應用程式 URL**  頁面的 hello**登入 URL**文字方塊中，輸入您的 URL 使用下列模式的 hello `http://company.my.salesforce.com`，然後按一下**下一步**。
   
   ![設定應用程式 URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "設定應用程式 URL")
4. 如果您已經在您目錄中，設定單一登入另一個 Salesforce 沙箱的執行個體，則您也必須設定 hello**識別碼**toohave hello 相同的值為 hello**登入 URL**。 
 * hello**識別碼**欄位可以找到藉由檢查 hello**顯示進階設定**hello 上的核取方塊**設定應用程式 URL** hello 對話方塊頁面。
5. 在 hello**於 Salesforce 沙箱設定單一登入**頁面上，按一下**下載憑證**，然後儲存您的電腦上的 hello 憑證檔案。
   
   ![設定單一登入](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "設定單一登入")
6. 在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Salesforce 沙箱。
7. 在 hello 最上層顯示 hello 功能表上，按一下**安裝**。
   
   ![設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "設定")
8. Hello hello 左側瀏覽窗格中按一下**安全性控制**，然後按一下**單一登入設定**。
   
   ![單一登入設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "單一登入設定")
9. 在 hello 單一登入設定 區段中，執行下列步驟的 hello:
   
   ![單一登入設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "單一登入設定")  
 1.  選取 [已啟用 SAML] 。 
 2.  按一下 [新增] 。
10. 在 hello SAML 單一登入設定 區段中，執行下列步驟的 hello:
    
    ![SAML 單一登入設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML 單一登入設定")  
 1. 在 [hello 名稱] 文字方塊中，輸入 hello hello 組態名稱 (例如： *SPSSOWAAD\_測試*)。 
 2. 在 Azure 傳統入口網站，在 hello hello**於 Salesforce 沙箱設定單一登入**對話方塊頁面上，複製 hello**簽發者 URL**值並貼到 hello**簽發者**文字方塊。
 3. 在 hello**實體識別碼**文字方塊中，輸入**https://test.salesforce.com**如果這是您要加入 tooyour 目錄 hello 第一個 Salesforce 沙箱執行個體。 如果您已新增執行個體的 Salesforce 沙箱則 hello**實體識別碼**hello 中的型別**登入 URL**，應該採用下列格式：`http://company.my.salesforce.com`   
 4. 按一下**瀏覽**tooupload hello 下載憑證。  
 5. 做為**SAML 識別類型**，選取**判斷提示包含從 hello 使用者物件的同盟識別碼 hello**。 
 6. 做為**SAML 識別位置**，選取**hello 的 hello Subject 陳述式的 NameIdentifier 元素中的識別是**。
 7. 在 Azure 傳統入口網站，在 hello hello**於 Salesforce 沙箱設定單一登入**對話方塊頁面上，複製 hello**遠端登入 URL**值並貼到 hello**身分識別提供者登入 URL**文字方塊。 
 8. SFDC 不支援 SAML 登出。  因應措施是，貼上 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello 到**身分識別提供者登出 URL**文字方塊。
 9. 在 [服務提供者起始的要求繫結]，選取 [HTTP POST]。 
 10. 按一下 [儲存] 。
11. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。
    
    ![設定單一登入](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "設定單一登入")

## <a name="enable-your-domain"></a>啟用網域
本節假設您已經建立了一個網域。  如需詳細資訊，請參閱 [定義您的網域名稱](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)。

**tooenable 您的網域，執行下列步驟的 hello:**

1. 在 hello 左側瀏覽窗格中，按一下 **定義域管理**，然後按一下**我的網域。**
   
   ![我的網域](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "我的網域")
   
   >[!NOTE]
   >請確定您的網域已正確設定。 
   > 
2. 在 hello**登入頁面設定**區段中，按一下**編輯**，然後當**驗證服務**，選取 hello 名稱從先前的 hello hello SAML 單一登入設定區段，然後按一下 最後**儲存**。
   
   ![我的網域](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "我的網域")

當您設定網域之後，您的使用者應該使用 hello 網域 URL toologin toohello Salesforce 沙箱。  

hello URL 的 tooget hello 值，按一下您已建立 hello 前一節中的 hello SSO 設定檔。

## <a name="configure-user-provisioning"></a>設定使用者佈建
hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooSalesforce 沙箱。

**tooconfigure 使用者佈建，執行下列步驟的 hello:**

1. 在 hello Salesforce 入口網站，在 hello 上方導覽列中，選取名稱 tooexpand 使用者功能表：
   
   ![我的設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "我的設定")
2. 從使用者功能表中，選取**我的設定**tooopen 您**我的設定**頁面。
3. 在 hello 左窗格中，按一下 **個人**tooexpand hello 個人的區段，然後按一下**重設我的安全性 Token**:
   
   ![我的設定](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "我的設定")
4. 在 hello**重設我的安全性 Token**頁面上，按一下**重設安全性 Token** toorequest 包含 Salesforce.com 安全性 token 的電子郵件。
   
   ![新的權杖](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "新的權杖")
5. 檢查您的電子郵件收件匣，尋找來自 Salesforce.com 且主旨為「**salesforce.com.com 安全性確認**」的電子郵件。
6. 檢閱此電子郵件和複製 hello 安全性 token 值。
7. 在 Azure 傳統入口網站，在 hello hello **salesforce 沙箱**應用程式整合頁面上，按一下 **設定使用者佈建**tooopen hello**設定使用者佈建**對話方塊。
   
   ![設定使用者佈建](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "設定使用者佈建")
8. 在 hello**輸入您 Salesforce 沙箱認證 tooenable 自動使用者佈建**頁面上，提供下列組態設定的 hello:
   
   ![Salesforce 沙箱](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce 沙箱")   
 1. 在 hello **Salesforce 沙箱管理使用者名稱**文字方塊中，輸入的 Salesforce 帳戶名稱已 hello**系統管理員**在 Salesforce.com 被指派的設定檔。
 2. 在 hello **Salesforce 沙箱管理員密碼**文字方塊中，此帳戶類型 hello 密碼。
 3. 在 hello**使用者安全性 Token**文字方塊中，貼上 hello 安全性 token 值。
 4. 按一下**驗證**tooverify 您的設定。
 5. 按一下 hello**下一步**按鈕 tooopen hello**確認**頁面。
9. 在 hello**確認**頁面上，按一下**完成**toosave 您的設定。
   
## <a name="assigning-users"></a>指派使用者

tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

**tooassign 使用者 tooSalesforce 沙箱，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，建立測試帳戶。
2. 在 hello * * Salesforce 沙箱 * * 應用程式整合頁面上，按一下 **指派使用者**。
   
   ![指派使用者](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "指派使用者")
3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
   ![是](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "是")

您現在應該等候 10 分鐘並驗證 hello 帳戶已同步處理的 tooSalesforce 沙箱。

如果您想 tootest SSO 設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](https://msdn.microsoft.com/library/dn308586)。

