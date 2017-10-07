---
title: "教學課程：Azure Active Directory 與 Replicon 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Replicon 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>教學課程：Azure Active Directory 與 Replicon 整合
本教學課程的 hello 目標是 Azure 與 Replicon tooshow hello 整合。 本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* Replicon 租用戶

完成本教學課程之後, 您已指派 tooReplicon hello Azure AD 使用者將能夠 toosingle 登入位於您 Replicon 公司網站 （服務提供者起始登入），或使用 hello 的 hello 應用程式[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

1. 啟用 Replicon 的 hello 應用程式整合
2. 設定單一登入 (SSO)
3. 設定使用者佈建
4. 指派使用者

![案例](./media/active-directory-saas-replicon-tutorial/IC777798.png "案例")

## <a name="enable-hello-application-integration-for-replicon"></a>啟用 Replicon 的 hello 應用程式整合
本節 hello 目標是 toooutline 如何 Replicon tooenable hello 應用程式整合。

**tooenable hello 應用程式整合 Replicon 中，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
    ![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式](./media/active-directory-saas-replicon-tutorial/IC700994.png "應用程式")
4. 按一下**新增**hello hello 頁底端。
   
    ![新增應用程式](./media/active-directory-saas-replicon-tutorial/IC749321.png "新增應用程式")
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![從資源庫新增應用程式](./media/active-directory-saas-replicon-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在 hello**搜尋方塊**，型別**Replicon**。
   
    ![應用程式資源庫](./media/active-directory-saas-replicon-tutorial/IC777799.png "應用程式資源庫")
7. 在 hello 結果窗格中，選取  **Replicon**，然後按一下**完成**tooadd hello 應用程式。
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>設定單一登入

hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooReplicon 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。

**tooconfigure 單一登入，請執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **Replicon**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
    ![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC777801.png "設定單一登入")
2. 在 hello**如何想您使用者 toosign tooReplicon 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
    ![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC777802.png "設定單一登入")
3. 在 hello**設定應用程式 URL**頁面上，執行下列步驟的 hello:
   
    ![設定應用程式 URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "設定應用程式 URL")
  1. 在 hello **Replicon 登入 URL**文字方塊中，輸入 Replicon 租用戶 URL (例如： *https://na2.replicon.com/company/saml2/sp-sso/post*)。
  2. 在 hello **Replicon 回覆 URL**文字方塊中，輸入 Replicon **AssertionConsumerService** URL (例如： *https://global.replicon.com/ ！saml2/公司/sso/post/*)。  
      
     >[!NOTE]
     >您可以從 hello Replicon 中繼資料取得 hello URL: **https://global.replicon.com/ ！ /saml2/\<YourCompanyKey\>**。
     > 
     > 
 
  3. 按一下 [下一步] 。

4. 在 hello**在 Replicon 設定單一登入**頁面、 toodownload 中繼資料，按一下**下載中繼資料**，然後儲存您的電腦上的 hello 中繼資料。
   
    ![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC777804.png "設定單一登入")
5. 在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Replicon 公司網站。

6. tooconfigure SAML 2.0 執行 hello 下列步驟：
   
    ![啟用 SAML 驗證](./media/active-directory-saas-replicon-tutorial/IC777805.png "啟用 SAML 驗證")
  
  1. toodisplay hello **EnableSAML Authentication2**  對話方塊中，新增下列 tooyour URL，公司金鑰 hello: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * hello 下列範例示範 hello hello 完整的 URL 結構描述：  
   **https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. 按一下 hello  **+**  tooexpand hello **v20Configuration** > 一節。
   3. 按一下 hello  **+**  tooexpand hello **metaDataConfiguration** > 一節。
   4. 按一下**選擇檔案**，tooselect 您的身分識別提供者中繼資料 XML 檔案，然後按一下**送出**。

7. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。
   
    ![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC778418.png "設定單一登入")
   
## <a name="configure-user-provisioning"></a>設定使用者佈建

在訂單 tooenable Azure AD 使用者 toolog 入 Replicon，它們必須佈建到 Replicon。  

在 Replicon 的 hello 案例中，佈建須手動進行。

**tooconfigure 使用者佈建，執行下列步驟的 hello:**

1. 在 Web 瀏覽器視窗中，以系統管理員身分登入您的 Replicon 公司網站。
2. 跳過**管理\>使用者**。
   
    ![使用者](./media/active-directory-saas-replicon-tutorial/IC777806.png "使用者")
3. 按一下 [新增使用者] 。
   
    ![新增使用者](./media/active-directory-saas-replicon-tutorial/IC777807.png "新增使用者")
4. 在 hello**使用者設定檔**區段中，執行下列步驟的 hello:
   
    ![使用者設定檔](./media/active-directory-saas-replicon-tutorial/IC777808.png "使用者設定檔")
   
  1. 在 hello**登入名稱**文字方塊中，型別 hello Azure AD 電子郵件地址的 hello Azure AD 使用者要 tooprovision。
  2. 針對 [驗證類型] 選取 [SSO]。
  3. 在 hello**部門**文字方塊中，輸入 hello 使用者的部門。
  4. 針對 [員工類型] 選取 [系統管理員]。
  5. 按一下 [儲存使用者設定檔] 。

>[!NOTE]
>您可以使用任何其他 Replicon 使用者帳戶建立工具或 Api 提供 Replicon tooprovision AAD 使用者帳戶。
> 
> 

## <a name="assign-users"></a>指派使用者
tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

**tooassign 使用者 tooReplicon，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，建立測試帳戶。

2. 在 hello **Replicon**應用程式整合頁面上，按一下 **指派使用者**。
   
    ![指派使用者](./media/active-directory-saas-replicon-tutorial/IC777809.png "指派使用者")

3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
    ![是](./media/active-directory-saas-replicon-tutorial/IC767830.png "是")

如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

