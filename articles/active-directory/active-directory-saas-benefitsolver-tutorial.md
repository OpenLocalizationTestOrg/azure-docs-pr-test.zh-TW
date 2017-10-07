---
title: "教學課程：Azure Active Directory 與 Benefitsolver 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Benefitsolver 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>教學課程：Azure Active Directory 與 Benefitsolver 整合
本教學課程的 hello 目標是 Azure 與 Benefitsolver tooshow hello 整合。  

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

* 有效的 Azure 訂閱
* 已啟用 Benefitsolver 單一登入 (SSO) 的訂用帳戶

完成本教學課程之後, 您已指派 tooBenefitsolver hello Azure AD 使用者將無法 toosingle 登入 hello 應用程式使用 hello[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

本教學課程所述的 hello 案例包含下列建置組塊的 hello:

1. 啟用 Benefitsolver hello 應用程式整合
2. 設定單一登入 (SSO)
3. 設定使用者佈建
4. 指派使用者

![案例](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "案例")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>啟用 Benefitsolver hello 應用程式整合
本節 hello 目標是 toooutline 如何 Benefitsolver tooenable hello 應用程式整合。

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>tooenable hello 應用程式整合 Benefitsolver，執行下列步驟的 hello:
1. 在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
   ![應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "應用程式")
4. 按一下**新增**hello hello 頁底端。
   
   ![新增應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "新增應用程式")
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
   ![從資源庫新增應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在 hello**搜尋方塊**，型別**Benefitsolver**。
   
   ![應用程式資源庫](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "應用程式資源庫")
7. 在 hello 結果窗格中，選取  **Benefitsolver**，然後按一下**完成**tooadd hello 應用程式。
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>設定單一登入

hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooBenefitsolver 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。  

Benefitsolver 應用程式需要特定格式，這需要您 tooadd 自訂屬性對應 tooyour hello SAML 判斷提示**saml 權杖屬性**組態。 

hello 下列螢幕擷取畫面會顯示這個範例。

![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "屬性")

**tooconfigure 單一登入，請執行下列步驟的 hello:**

1. 在 Azure 傳統入口網站，在 hello hello **Benefitsolver**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "設定單一登入")
2. 在 hello**如何想您使用者 toosign tooBenefitsolver 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。
   
   ![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "設定單一登入")
3. 在 hello**設定應用程式設定**頁面上，執行下列步驟的 hello:
   
   ![設定應用程式設定](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "進行應用程式設定")
   
   1. 在 hello**登入 URL**文字方塊中，輸入**http://azure.benefitsolver.com**。
   2. 在 hello**回覆 URL**文字方塊中，輸入**https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**。  
   3. 按一下 [下一步] 。
4. 在 hello **Benefitsolver 在設定單一登入**頁面、 toodownload 中繼資料，按一下**下載中繼資料**，然後儲存在本機電腦上的 hello 中繼資料檔案。
   
   ![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "設定單一登入")
5. 傳送嗨下載中繼資料檔案 tooyour Benefitsolver 支援小組。
   
   >[!NOTE]
   >您 Benefitsolver 的支援團隊已 toodo hello 實際 SSO 組態。 當您的訂用帳戶啟用 SSO 之後，您會收到通知。
   >

6. 在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "設定單一登入")
7. 在 hello 最上層顯示 hello 功能表上，按一下**屬性**tooopen hello **SAML 權杖屬性**對話方塊。
   
   ![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "屬性")
8. tooadd hello 必要屬性對應，執行下列步驟的 hello:
   
   ![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "屬性")
   
   | 屬性名稱 | 屬性值 |
   | --- | --- |
   | ClientID |您需要 tooget 這個值向 Benefitsolver 支援小組。 |
   | ClientKey |您需要 tooget 這個值向 Benefitsolver 支援小組。 |
   | LogoutURL |您需要 tooget 這個值向 Benefitsolver 支援小組。 |
   | EmployeeID |您需要 tooget 這個值向 Benefitsolver 支援小組。 |
   
   1. 上述的 hello 資料表中每個資料列，按一下 **新增使用者屬性**。
   2. 在 hello**屬性名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。
   3. 在 hello**屬性值**文字方塊中，顯示該資料列選取 hello 屬性值。
   4. 按一下頁面底部的 [新增] 。
9. 按一下 [套用變更] 。

## <a name="configure-user-provisioning"></a>設定使用者佈建
在訂單 tooenable Azure AD 使用者 toolog Benefitsolver 成，它們必須佈建到 Benefitsolver。  

在的 Benefitsolver hello 案例中，員工資料是透過從 HRIS 系統 （通常每晚都會更新） 人口普查檔填入應用程式中。  

>[!NOTE]
>您可以使用任何其他 Benefitsolver 使用者帳戶建立工具或 Api 提供 Benefitsolver tooprovision AAD 使用者帳戶。 
> 

## <a name="assigning-users"></a>指派使用者
tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooassign 使用者 tooBenefitsolver，執行下列步驟的 hello:
1. 在 hello Azure 傳統入口網站，建立測試帳戶。
2. 在 hello * * Benefitsolver * * 應用程式整合頁面上，按一下 **指派使用者**。
   
   ![指派使用者](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "指派使用者")
3. 選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。
   
   ![是](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "是")

如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。 如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

