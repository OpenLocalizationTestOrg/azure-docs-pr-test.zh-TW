---
title: "教學課程：Azure Active Directory 與 Coupa 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Coupa 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>教學課程：Azure Active Directory 與 Coupa 整合
本教學課程的 hello 目標是 Azure 與 Coupa tooshow hello 整合。  
本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* 已啟用 Coupa 單一登入 (SSO) 的訂用帳戶

完成本教學課程之後, 您已指派 tooCoupa hello Azure AD 使用者將無法 toosingle 登入 hello 應用程式使用 hello[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

* 啟用 Coupa 的 hello 應用程式整合
* 設定單一登入
* 設定使用者佈建
* 指派使用者

![案例](./media/active-directory-saas-coupa-tutorial/IC791897.png "案例")

## <a name="enable-hello-application-integration-for-coupa"></a>啟用 Coupa 的 hello 應用程式整合
本節 hello 目標是 toooutline 如何 Coupa tooenable hello 應用程式整合。

**tooenable hello 應用程式整合 Coupa 中，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
   ![應用程式](./media/active-directory-saas-coupa-tutorial/IC700994.png "應用程式")
4. 按一下**新增**hello hello 頁底端。
   
   ![新增應用程式](./media/active-directory-saas-coupa-tutorial/IC749321.png "新增應用程式")
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
   ![從資源庫新增應用程式](./media/active-directory-saas-coupa-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在 hello**搜尋方塊**，型別**Coupa**。
   
   ![應用程式資源庫](./media/active-directory-saas-coupa-tutorial/IC791898.png "應用程式資源庫")
7. 在 hello 結果窗格中，選取  **Coupa**，然後按一下**完成**tooadd hello 應用程式。
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>設定單一登入

hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooCoupa 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。  

設定單一登入 coupa 需要 tooretrieve 從憑證的指紋值。 如果您不熟悉這個程序，請參閱[如何 tooretrieve 憑證的指紋值](http://youtu.be/YKQF266SAxI)。

**tooconfigure 單一登入，請執行下列步驟的 hello:**

1. 登入 tooyour Coupa 公司網站的系統管理員身分。
2. 跳過**安裝\>安全性控制**。
   
   ![安全性控制項](./media/active-directory-saas-coupa-tutorial/IC791900.png "安全性控制項")
3. toodownload hello Coupa 中繼資料檔案 tooyour，請按一下**下載並匯入 SP 中繼資料**。
   
   ![Coupa 預存程序中繼資料](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa 預存程序中繼資料")
4. 在不同的瀏覽器視窗中，登入 toohello Azure 傳統入口網站。
5. 在 hello **Coupa**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791902.png "設定單一登入")
6. 在 hello**如何想您使用者 toosign tooCoupa 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
   ![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791903.png "設定單一登入")
7. 在 hello**設定應用程式 URL**頁面上，執行下列步驟的 hello:
   
   ![設定應用程式 URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "設定應用程式 URL")   
   1. 在 hello**登入 URL**文字方塊中，您的使用者 toosign 上 tooyour Coupa 的應用程式所使用的型別 URL (例如:"*http://company.Coupa.com*")。
   2. 開啟您下載的 Coupa 中繼資料檔案，然後複製 hello **AssertionConsumerService index/URL**。
   3. 在 hello **coupa 轉送 URL**文字方塊中，貼上 hello **AssertionConsumerService index/URL**值。
   4. 按一下 [下一步] 。
8. 在 hello**在 Coupa 設定單一登入**頁面、 toodownload 中繼資料檔案，按一下**下載中繼資料**，然後儲存在本機電腦上的 hello 檔案。
   
   ![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791905.png "設定單一登入")
9. Hello Coupa 公司網站上，前往 太**安裝\>安全性控制**。
   
   ![安全性控制項](./media/active-directory-saas-coupa-tutorial/IC791900.png "安全性控制項")
10. 在 hello**使用 Coupa 認證登入**區段中，執行下列步驟的 hello:  

   ![使用 Coupa 認證登入](./media/active-directory-saas-coupa-tutorial/IC791906.png "使用 Coupa 認證登入") 
   1. 選取 [使用 SAML 登入] 。
   2. 按一下**瀏覽**tooupload 您下載的 Azure Active 中繼資料檔案。
   3. 按一下 [儲存] 。
11. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。
    
   ![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791907.png "設定單一登入")
    
## <a name="configure-user-provisioning"></a>設定使用者佈建

在訂單 tooenable Azure AD 使用者 toolog 入 Coupa，它們必須佈建到 Coupa。  

* 在 Coupa 的 hello 案例中，佈建須手動進行。

**tooconfigure 使用者佈建，執行下列步驟的 hello:**

1. 登入 tooyour **Coupa**以系統管理員身分的公司網站。
2. 在 hello 最上層顯示 hello 功能表上，按一下**安裝**，然後按一下**使用者**。
   
   ![使用者](./media/active-directory-saas-coupa-tutorial/IC791908.png "使用者")
3. 按一下 [建立] 。
   
   ![建立使用者](./media/active-directory-saas-coupa-tutorial/IC791909.png "建立使用者")
4. 在 hello**使用者建立**區段中，執行下列步驟的 hello:
   
   ![使用者詳細資料](./media/active-directory-saas-coupa-tutorial/IC791910.png "使用者詳細資料")
   
   1. 型別 hello**登入**，**名字**，**姓氏**，**單一登入識別碼**，**電子郵件**屬性您想 tooprovision 寫入 hello 的有效 Azure Active Directory 帳戶相關的文字方塊。
   2. 按一下 [建立] 。   
   >[!NOTE]
   >hello Azure Active Directory 帳戶持有者會收到含有連結 tooconfirm hello 帳戶的電子郵件之前就會生效。 
   > 

>[!NOTE]
>您可以使用任何其他 Coupa 使用者帳戶建立工具或 Api 提供 Coupa tooprovision AAD 使用者帳戶。 
> 

## <a name="assign-users"></a>指派使用者
tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

**tooassign 使用者 tooCoupa，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，建立測試帳戶。
2. 在 hello * * Coupa * * 應用程式整合頁面上，按一下 **指派使用者**。
   
   ![指派使用者](./media/active-directory-saas-coupa-tutorial/IC791911.png "指派使用者")
3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
   ![是](./media/active-directory-saas-coupa-tutorial/IC767830.png "是")

如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

