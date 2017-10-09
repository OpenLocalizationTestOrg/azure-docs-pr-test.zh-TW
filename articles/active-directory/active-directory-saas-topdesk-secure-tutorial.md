---
title: "教學課程：Azure Active Directory 與 TOPdesk - Secure 整合 | Microsoft Docs"
description: "深入了解如何 toouse TOPdesk-保護 Azure Active Directory tooenable 單一登入、 與自動化佈建更多 ！。"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>教學課程：Azure Active Directory 與 TOPdesk - Secure 整合
本教學課程的 hello 目標是 tooshow hello 整合 Azure 與 TOPdesk-Secure。  
本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* 已啟用 TOPdesk - Secure 單一登入功能的訂用帳戶

完成本教學課程、 hello Azure AD 使用者之後您已指派 tooTOPdesk-安全的會是能 toosingle 登入位於您 TOPdesk-Secure 公司網站 （服務提供者起始登入） 的 hello 應用程式或使用 hello[簡介存取面板 toohello](active-directory-saas-access-panel-introduction.md)。

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

1. 啟用 TOPdesk-Secure 的 hello 應用程式整合
2. 設定單一登入
3. 設定使用者佈建
4. 指派使用者

![案例](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "案例")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>啟用 TOPdesk-Secure 的 hello 應用程式整合
本節 hello 目標是 toooutline 如何 TOPdesk-Secure tooenable hello 應用程式整合。

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>tooenable hello 應用程式整合 TOPdesk-Secure，執行下列步驟的 hello:
1. 在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
    ![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。

3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "應用程式")

4. 按一下**新增**hello hello 頁底端。
   
    ![新增應用程式](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "新增應用程式")

5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![從資源庫新增應用程式](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "從資源庫新增應用程式")

6. 在 hello**搜尋方塊**，型別**TOPdesk-Secure**。
   
    ![應用程式資源庫](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "應用程式資源庫")

7. 在 hello 結果窗格中，選取  **TOPdesk-Secure**，然後按一下**完成**tooadd hello 應用程式。
   
    ![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")

## <a name="configuring-single-sign-on"></a>設定單一登入
本節 hello 目標是 toooutline 如何 tooenable 使用者 tooauthenticate tooTOPdesk-hello SAML 通訊協定為基礎的同盟，使用 Azure AD 中與他們的帳戶安全。  
設定單一登入 topdesk-Secure 需要您 tooupload 標誌圖示檔。 tooget hello 圖示檔案，請連絡 hello TOPdesk 支援小組。

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure 單一登入，請執行下列步驟的 hello:
1. 登入 tooyour **TOPdesk-Secure**系統管理員身分的公司網站。
2. 在 hello **TOPdesk**功能表上，按一下 **設定**。
   
    ![設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "設定")

3. 按一下 [登入設定] 。
   
    ![登入設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "登入設定")

4. 展開 hello**登入設定**功能表，然後再按一下**一般**。
   
    ![一般](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "一般")

5. 在 hello**安全**hello 區段**SAML 登入**組態區段中，執行下列步驟的 hello:
   
    ![技術設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "技術設定")
   
    a. 按一下**下載**toodownload hello 公用中繼資料檔案，然後將它儲存在本機電腦上。
   
    b. 開啟 hello 中繼資料檔案，然後再找出 hello **AssertionConsumerService**節點。
    
    ![判斷提示取用者服務](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "判斷提示取用者服務")
   
    c. 複製 hello **AssertionConsumerService**值。  
      
    > [!NOTE]
    > 您將需要 hello 中 hello 值**設定應用程式 URL**稍後在本教學課程 > 一節。
    > 
    > 

6. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **Azure 傳統入口網站** 。

7. 在 hello **TOPdesk-Secure**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello * * 設定單一登入 * * 對話方塊。
   
    ![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "設定單一登入")

8. 在 hello**如何將您像使用者 toosign 上 tooTOPdesk-安全**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
    ![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "設定單一登入")

9. 在 hello**設定應用程式 URL**頁面上，執行下列步驟的 hello:
   
    ![設定應用程式 URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "設定應用程式 URL")
   
    a. 在 hello **TOPdesk-Secure 登入 URL**文字方塊中，供使用者 toosign 入 TOPdesk-安全的應用程式的型別 hello URL (例如:"*https://qssolutions.topdesk.net*")。
   
    b. 在 hello **TOPdesk-Public 回覆 URL**文字方塊中，貼上 hello **TOPdesk-Secure AssertionConsumerService URL** (例如:"*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. 按一下 [下一步] 。

10. 在 hello**於 TOPdesk-Secure 設定單一登入**頁面、 toodownload 中繼資料檔案，按一下 **下載中繼資料**，然後儲存在本機電腦上的 hello 檔案。
    
    ![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "設定單一登入")

11. toocreate 憑證檔案，執行下列步驟的 hello:
    
    ![憑證](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "憑證")
    
    a. 開啟 hello 下載的中繼資料檔案。
    b. 展開 hello **RoleDescriptor**節點具有**xsi: type**的**fed: ApplicationServiceType**。
    c. 複製 hello hello 值**X509Certificate**節點。
    d. 複製儲存 hello **X509Certificate**在檔案中的電腦上本機值。

12. 在您 TOPdesk-Secure 公司網站，請在 hello **TOPdesk**功能表上，按一下 **設定**。
    
    ![設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "設定")

13. 按一下 [登入設定] 。
    
    ![登入設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "登入設定")

14. 展開 hello**登入設定**功能表，然後再按一下**一般**。
    
    ![一般](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "一般")

15. 在 hello**公用**區段中，按一下**新增**。
    
    ![新增](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "新增")

16. 在 hello **SAML 設定助理**對話方塊頁面上，執行下列步驟的 hello:
    
    ![SAML 組態輔助程式](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML 組態輔助程式")
    
    a. 在您下載的中繼資料檔案的 tooupload**同盟中繼資料**，按一下 **瀏覽**。

    b. 在您的憑證檔案的 tooupload**憑證 (RSA)**，按一下 **瀏覽**。

    c. 所得 hello TOPdesk 支援小組，底下 tooupload hello 標誌檔**標誌圖示**，按一下 **瀏覽**。

    d. 在 hello**使用者名稱屬性**文字方塊中，輸入**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。

    e. 在 hello**顯示名稱**文字方塊中，輸入您的組態名稱。

    f. 按一下 [儲存] 。

17. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。
    
    ![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "設定單一登入")

## <a name="configuring-user-provisioning"></a>設定使用者佈建
順序 tooenable Azure AD 使用者 toolog 到 TOPdesk-在安全的它們必須佈建到 TOPdesk-Secure。  
在 TOPdesk-的案例中 hello 安全，佈建須手動進行。

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure 使用者佈建，執行下列步驟的 hello:
1. 登入 tooyour **TOPdesk-Secure**以系統管理員身分的公司網站。
2. 在 hello 最上層顯示 hello 功能表上，按一下**TOPdesk\>新增\>支援檔案\>運算子**。
   
    ![操作員](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "操作員")

3. 在 [hello **New 運算子**] 對話方塊中，執行下列步驟的 hello:
   
    ![新增操作員](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "新增操作員")
   
    a. 按一下 hello 一般索引標籤。
   
    b. 在 hello**姓氏**文字方塊中的 hello**一般**> 一節中，輸入您想要 tooprovision 之有效 Azure Active Directory 帳戶 hello 最後一個名稱。
   
    c. 選取**網站**hello hello 帳戶**位置**> 一節。
   
    d. 在 hello**登入名稱**文字方塊中的 hello **TOPdesk 登入**區段中，輸入您使用者的登入名稱。
   
    e. 按一下 [儲存] 。

> [!NOTE]
> 您可以使用任何其他 TOPdesk-Secure 使用者帳戶建立工具或 Api 提供 TOPdesk-Secure tooprovision AAD 使用者帳戶。
> 
> 

## <a name="assigning-users"></a>指派使用者
tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooassign 使用者 tooTOPdesk-Secure，請執行下列步驟的 hello:
1. 在 hello Azure 傳統入口網站，建立測試帳戶。
2. 在 hello * * TOPdesk-Secure * * 應用程式整合頁面上，按一下 **指派使用者**。
   
    ![指派使用者](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "指派使用者")

3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
    ![是](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "是")

如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

