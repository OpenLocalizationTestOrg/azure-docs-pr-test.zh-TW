---
title: "教學課程：Azure Active Directory 與 Qualtrics 整合 | Microsoft Docs"
description: "了解如何使用 Qualtrics 搭配 Azure Active Directory 來啟用單一登入、自動佈建和更多功能！"
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
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>教學課程：Azure Active Directory 與 Qualtrics 整合
本教學課程的目的是要示範 Azure 與 Qualtrics 的整合。  

本教學課程中說明的案例假設您已經具有下列項目：

* 有效的 Azure 訂用帳戶
* 已啟用 Qualtrics 單一登入 (SSO) 的訂用帳戶

完成本教學課程之後，您指派給 Qualtrics 的 Azure AD 使用者就能夠從您的 Qualtrics 公司網站 (服務提供者起始登入)，或使用 [存取面板](active-directory-saas-access-panel-introduction.md)來單一登入應用程式。

本教學課程中說明的案例由下列建置組塊組成：

1. 啟用 Qualtrics 的應用程式整合
2. 設定單一登入 (SSO)
3. 設定使用者佈建
4. 指派使用者

![案例](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "案例")

## <a name="enabling-the-application-integration-for-qualtrics"></a>啟用 Qualtrics 的應用程式整合
本節的目的是要說明如何啟用 Qualtrics 的應用程式整合。

**若要啟用 Qualtrics 的應用程式整合，請執行下列步驟：**

1. 在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. 從 [目錄]  清單中，選取要啟用目錄整合的目錄。
3. 若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。
   
   ![應用程式](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "應用程式")
4. 按一下頁面底部的 [新增]  。
   
   ![新增應用程式](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "新增應用程式")
5. 在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。
   
   ![從資源庫新增應用程式](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在**搜尋方塊**中，輸入 **Qualtrics**。
   
   ![應用程式資源庫](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "應用程式資源庫")
7. 在結果窗格中，選取 [Qualtrics]，然後按一下 [完成] 來新增應用程式。
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>設定單一登入

本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶驗證到 Qualtrics。

**若要設定單一登入，請執行下列步驟：**

1. 在 Azure 傳統入口網站的 [Qualtrics] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "設定單一登入")
2. 在 [要如何讓使用者登入 Qualtrics] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。
   
   ![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "設定單一登入")
3. 在 [設定應用程式 URL] 頁面的 [Qualtrics 登入 URL] 文字方塊中，輸入您的 URL (例如：“ https://ssotest2ut1.qualtrics.com ")，然後按 [下一步]。
   
   ![設定應用程式 URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "設定應用程式 URL")
4. 在 [設定在 Qualtrics 單一登入] 頁面上，按一下 [下載中繼資料]，然後將中繼資料檔儲存在您的電腦上。
   
   ![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "設定單一登入")
5. 將中繼資料檔傳送至 Qualtrics 支援小組。
   
   >[!NOTE]
   >SSO 設定必須由 Qualtrics 支援小組執行。 設定完成後，您將會收到通知。
   > 
   > 
6. 在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "設定單一登入")
   
## <a name="configure-user-provisioning"></a>設定使用者佈建

沒有動作項目可讓您設定 Qualtrics 使用者佈建。 當指派的使用者透過存取面板嘗試登入 Qualtrics 時，Qualtrics 會檢查使用者是否存在。  

如果尚無可用的使用者帳戶，Qualtrics 就會自動予以建立。

## <a name="assign-users"></a>指派使用者
若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。

**若要將使用者指派給 Qualtrics，請執行下列步驟：**

1. 在 Azure 傳統入口網站中建立測試帳戶。
2. 在 [Qualtrics] 應用程式整合頁面上，按一下 [指派使用者]。
   
   ![指派使用者](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "指派使用者")
3. 選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。
   
   ![是](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "是")

如果要測試您的 SSO 設定，請開啟存取面板。 如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。

