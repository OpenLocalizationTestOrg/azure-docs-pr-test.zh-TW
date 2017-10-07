---
title: "教學課程：Azure Active Directory 與 Cisco Webex 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Cisco Webex 的單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>教學課程：Azure Active Directory 與 Cisco Webex 整合
本教學課程的 hello 目標是 Azure 與 Cisco Webex tooshow hello 整合。  
本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* Cisco Webex 租用戶

完成本教學課程之後, hello 您已指派的 tooCisco Webex 將會無法 toosingle 登入 hello 應用程式位於您 Cisco Webex 公司網站 （服務提供者起始登入），Azure AD 使用者，或使用 hello[簡介 toohello存取面板](active-directory-saas-access-panel-introduction.md)。

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

* 啟用 Cisco Webex 的 hello 應用程式整合
* 設定單一登入 (SSO)
* 設定使用者佈建
* 指派使用者

![案例](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "案例")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>啟用 Cisco Webex 的 hello 應用程式整合
本節 hello 目標是 toooutline 如何 Cisco Webex tooenable hello 應用程式整合。

**Cisco Webex tooenable hello 應用程式整合執行 hello 下列步驟：**

1. 在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
   ![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
   ![應用程式](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "應用程式")
4. 按一下**新增**hello hello 頁底端。
   
   ![新增應用程式](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "新增應用程式")
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
   ![從資源庫新增應用程式](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在 hello**搜尋方塊**，型別**Cisco Webex**。
   
   ![應用程式資源庫](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "應用程式資源庫")
7. 在 hello 結果窗格中，選取  **Cisco Webex**，然後按一下**完成**tooadd hello 應用程式。
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>設定單一登入

hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooCisco Webex 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。  

此程序的一部分，您就需要的 toocreate base 64 編碼的憑證。 如果您不熟悉這個程序，請參閱[如何 tooconvert 二進位憑證到文字檔案](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure 單一登入，請執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **Cisco Webex**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "設定單一登入")
2. 在 hello**方式上 tooCisco Webex 使用者 toosign 想您**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
   ![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "設定單一登入")
3. 在 hello**設定應用程式 URL**頁面上，執行下列步驟，hello，然後按一下**下一步**。
   
   ![設定應用程式 URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "設定應用程式 URL")   
   1. 在 hello**登入 URL**文字方塊中，輸入您的 Cisco Webex 租用戶 URL (例如： *http://contoso.webex.com*)。
   2. 在 hello **Cisco Webex 回覆 URL**文字方塊中，輸入您**Cisco Webex AssertionConsumerService URL** (例如： *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).
4. 在 hello**於 Cisco Webex 設定單一登入**頁面、 toodownload 憑證，請按一下**下載憑證**，然後儲存您的電腦上的 hello 憑證檔案。
   
   ![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "設定單一登入")
5. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Cisco Webex 公司網站。
6. 在 hello 最上層顯示 hello 功能表上，按一下**網站管理**。
   
   ![網站管理](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "網站管理")
7. 在 hello**管理站台**區段中，按一下**SSO 組態**。
   
   ![SSO 組態](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO 組態")
8. 在 hello 同盟 Web SSO 組態 區段中，執行下列步驟的 hello:
   
   ![同盟 SSO 組態](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "同盟 SSO 組態")  
   1. 從 hello**同盟通訊協定**清單中，選取**SAML 2.0**。
   2. 從您下載的憑證建立 **Base-64 編碼** 檔案。  
    >[!TIP]
    >如需詳細資訊，請參閱[如何 tooconvert 二進位憑證到文字檔案](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. 在 [記事本]，然後再複製 hello 它的內容中開啟您的 base-64 編碼的憑證。
   4. 按一下 [匯入 SAML 中繼資料] ，然後貼上 base-64 編碼的憑證。
   5. 在 Azure 傳統入口網站，在 hello hello**於 Cisco Webex 設定單一登入**對話方塊頁面上，複製 hello**簽發者 URL**值並貼到 hello **(IdP ID)SAML的簽發者**文字方塊。
   6. 在 Azure 傳統入口網站，在 hello hello**於 Cisco Webex 設定單一登入**對話方塊頁面上，複製 hello**遠端登入 URL**值並貼到 hello**客戶 SSO 服務登入URL**文字方塊。
   7. 從 hello **NameID 格式**清單中，選取**電子郵件地址**。
   8. 在 hello **AuthnContextClassRef**文字方塊中，輸入**urn: oasis： 名稱： tc: SAML:2.0:ac:classes:Password**。
   9. 在 Azure 傳統入口網站，在 hello hello**於 Cisco Webex 設定單一登入**對話方塊頁面上，複製 hello**遠端登出 URL**值並貼到 hello**客戶 SSO 服務登出URL**文字方塊。
   10. 按一下 [更新] 。
9. 在 Azure 傳統入口網站，在 hello hello**於 Cisco Webex 設定單一登入**對話方塊頁面上，選取 hello 單一登入組態確認，然後再按一下**完成**。
   
   ![設定單一登入](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "設定單一登入")
   
## <a name="configure-user-provisioning"></a>設定使用者佈建

在訂單 tooenable Azure AD 使用者 toolog 到 Cisco Webex，它們必須佈建到 Cisco Webex。  

* 在 Cisco Webex 的 hello 案例中，佈建須手動進行。

**tooprovision 使用者帳戶，執行下列步驟 hello:**

1. 登入 tooyour **Cisco Webex**租用戶。
2. 跳過**管理使用者\>新增使用者**。
   
   ![新增使用者](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "新增使用者")
3. 在 hello 新增使用者 區段中，執行下列步驟的 hello:
   
   ![新增使用者](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "新增使用者")   
   1. 針對 [帳戶類型]，選取 [主機]。
   2. Hello 下列文字方塊中輸入現有 Azure AD 使用者的 hello 資訊：**名字、 姓氏**，**使用者名**，**電子郵件**，**密碼**，**確認密碼**。
   3. 按一下 [新增] 。

>[!NOTE]
>您可以使用任何其他 Cisco Webex 使用者帳戶建立工具或 Api 提供 Cisco Webex tooprovision AAD 使用者帳戶。 
> 

## <a name="assign-users"></a>指派使用者
tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

**tooassign 使用者 tooCisco Webex 中，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，建立測試帳戶。
2. 在 hello **Cisco Webex**應用程式整合頁面上，按一下 **指派使用者**。
   
   ![指派使用者](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "指派使用者")
3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
   ![是](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "是")

如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

