---
title: "教學課程：Azure Active Directory 與 Qualtrics 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Qualtrics 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>教學課程：Azure Active Directory 與 Qualtrics 整合
本教學課程的 hello 目標是 Azure 與 Qualtrics tooshow hello 整合。  

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* 已啟用 Qualtrics 單一登入 (SSO) 的訂用帳戶

完成本教學課程之後, 您已指派 tooQualtrics hello Azure AD 使用者將能夠 toosingle 登入位於您 Qualtrics 公司網站 （服務提供者起始登入），或使用 hello 的 hello 應用程式[簡介 toohello存取面板](active-directory-saas-access-panel-introduction.md)。

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

1. 啟用 Qualtrics 的 hello 應用程式整合
2. 設定單一登入 (SSO)
3. 設定使用者佈建
4. 指派使用者

![案例](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "案例")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>啟用 Qualtrics 的 hello 應用程式整合
本節 hello 目標是 toooutline 如何 Qualtrics tooenable hello 應用程式整合。

**tooenable hello 應用程式整合，qualtrics，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
   ![應用程式](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "應用程式")
4. 按一下**新增**hello hello 頁底端。
   
   ![新增應用程式](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "新增應用程式")
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
   ![從資源庫新增應用程式](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在 hello**搜尋方塊**，型別**Qualtrics**。
   
   ![應用程式資源庫](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "應用程式資源庫")
7. 在 hello 結果窗格中，選取  **Qualtrics**，然後按一下**完成**tooadd hello 應用程式。
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>設定單一登入

hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooQualtrics 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。

**tooconfigure 單一登入，請執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **Qualtrics**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "設定單一登入")
2. 在 hello**如何想您使用者 toosign tooQualtrics 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
   ![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "設定單一登入")
3. 在 hello**設定應用程式 URL**  頁面的 hello **Qualtrics 登入 URL**文字方塊中，輸入您的 URL (例如:"*https://ssotest2ut1.qualtrics.com*")，然後按一下 **下一步**。
   
   ![設定應用程式 URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "設定應用程式 URL")
4. 在 hello**在 Qualtrics 設定單一登入**頁面上，按一下**下載中繼資料**，然後儲存您的電腦上的 hello 中繼資料檔案。
   
   ![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "設定單一登入")
5. 傳送嗨中繼資料檔案 toohello Qualtrics 支援小組。
   
   >[!NOTE]
   >hello SSO 組態必須 toobe hello Qualtrics 支援小組所執行。 只要 hello 組態完成之後，您會收到通知。
   > 
   > 
6. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "設定單一登入")
   
## <a name="configure-user-provisioning"></a>設定使用者佈建

不沒有您 tooconfigure 使用者佈建 tooQualtrics 任何動作項目。 當指派的使用者嘗試 toolog 入 Qualtrics 使用 hello 存取面板時，Qualtrics 會檢查 hello 使用者是否存在。  

如果尚無可用的使用者帳戶，Qualtrics 就會自動予以建立。

## <a name="assign-users"></a>指派使用者
tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

**tooassign 使用者 tooQualtrics，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，建立測試帳戶。
2. 在 hello **Qualtrics**應用程式整合頁面上，按一下 **指派使用者**。
   
   ![指派使用者](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "指派使用者")
3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
   ![是](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "是")

如果您想 tootest SSO 設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

