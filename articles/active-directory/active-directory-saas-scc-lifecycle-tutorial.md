---
title: "教學課程：Azure Active Directory 與 SCC LifeCycle 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse SCC LifeCycle 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>教學課程：Azure Active Directory 與 SCC LifeCycle 整合
本教學課程的 hello 目標是 Azure 與 SCC LifeCycle tooshow hello 整合。  

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* 已啟用 SCC LifeCycle 單一登入 (SSO) 的訂用帳戶

完成本教學課程之後, hello 您已指派的 tooSCC 生命週期將會無法 toosingle 登入 hello 應用程式位於您 SCC LifeCycle 公司網站 （服務提供者起始登入），Azure AD 使用者，或使用 hello[簡介存取面板 toohello](active-directory-saas-access-panel-introduction.md)。

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

1. 啟用 SCC LifeCycle 的 hello 應用程式整合
2. 設定單一登入 (SSO)
3. 設定使用者佈建
4. 指派使用者

![案例](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "案例")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>啟用 SCC LifeCycle 的 hello 應用程式整合
本節 hello 目標是 toooutline 如何 SCC LifeCycle tooenable hello 應用程式整合。

**SCC LifeCycle tooenable hello 應用程式整合執行 hello 下列步驟：**

1. 在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
    ![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "應用程式")
4. 按一下**新增**hello hello 頁底端。
   
    ![新增應用程式](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "新增應用程式")
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![從資源庫新增應用程式](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在 hello**搜尋方塊**，型別**SCC LifeCycle**。
   
    ![應用程式資源庫](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "應用程式資源庫")
7. 在 hello 結果窗格中，選取  **SCC LifeCycle**，然後按一下**完成**tooadd hello 應用程式。
   
    ![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")
   
## <a name="configure-single-sign-on"></a>設定單一登入

hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooSCC 透過同盟，使用 Azure AD 的帳戶生命週期如何 hello SAML 通訊協定為基礎。

**tooconfigure 單一登入，請執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **SCC LifeCycle**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello * * 設定單一登入 * * 對話方塊。
   
    ![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "設定單一登入")
2. Hello 上**如何想您 tooSCC 生命週期上的使用者 toosign**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
    ![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "設定單一登入")
3. 在 hello**設定應用程式 URL**  頁面的 hello**登入 URL**文字方塊中，型別 hello URL 上使用的使用者 toosign tooyour SCC LifeCycle 的應用程式使用下列模式的 hello"*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*"，然後按一下**下一步**。
   
    ![設定應用程式 URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "設定應用程式 URL")
4. 在 hello **SCC LifeCycle 在設定單一登入**頁面上，按一下**下載中繼資料**，然後儲存在本機電腦上的中繼資料檔案。
   
   ![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "設定單一登入")
5. 轉寄該中繼資料檔案 tooSCC LifeCycle 支援小組。
   
   >[!NOTE]
   >單一登入具有 toobe hello SCC LifeCycle 支援小組啟用。
   > 
   > 

6. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。
   
    ![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "設定單一登入")
   
## <a name="configure-user-provisioning"></a>設定使用者佈建

在訂單 tooenable Azure AD 使用者 toolog 入 SCC LifeCycle，它們必須佈建到 SCC LifeCycle。 沒有您 tooconfigure 使用者佈建 tooSCC 生命週期的動作項目。

當入 SCC LifeCycle 指派的使用者嘗試 toolog 時，SCC LifeCycle 帳戶會在必要時自動建立。

>[!NOTE]
>您可以使用任何其他 SCC LifeCycle 使用者帳戶建立工具或 Api 提供 SCC LifeCycle tooprovision AAD 使用者帳戶。
> 
> 

## <a name="assign-users"></a>指派使用者
tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

**tooassign 使用者 tooSCC 生命週期，執行下列步驟的 hello:**

1. 在 hello Azure 傳統入口網站，建立測試帳戶。
2. 在 hello * * SCC LifeCycle * * 應用程式整合頁面上，按一下 **指派使用者**。
   
    ![指派使用者](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "指派使用者")
3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
    ![是](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "是")

如果您想 tootest SSO 設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

