---
title: "教學課程：Azure Active Directory 與 Benefitsolver 整合 | Microsoft Docs"
description: "了解如何使用 Benefitsolver 搭配 Azure Active Directory 來啟用單一登入、自動化佈建和更多功能！"
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
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>教學課程：Azure Active Directory 與 Benefitsolver 整合
本教學課程的目的是要示範 Azure 與 Benefitsolver 的整合。  

本教學課程中說明的案例假設您已經具有下列項目：

* 有效的 Azure 訂閱
* 已啟用 Benefitsolver 單一登入 (SSO) 的訂用帳戶

完成本教學課程之後，您指派給 Benefitsolver 的 Azure AD 使用者就能夠單一登入應用程式或是使用 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。

本教學課程中說明的案例由下列建置組塊組成：

1. 啟用 Benefitsolver 的應用程式整合
2. 設定單一登入 (SSO)
3. 設定使用者佈建
4. 指派使用者

![案例](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "案例")

## <a name="enabling-the-application-integration-for-benefitsolver"></a>啟用 Benefitsolver 的應用程式整合
本節的目的是要說明如何啟用 Benefitsolver 的應用程式整合。

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a>若要啟用 Benefitsolver 的應用程式整合，請執行下列步驟：
1. 在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. 從 [目錄]  清單中，選取要啟用目錄整合的目錄。
3. 若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。
   
   ![應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "應用程式")
4. 按一下頁面底部的 [新增]  。
   
   ![新增應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "新增應用程式")
5. 在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。
   
   ![從資源庫新增應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "從資源庫新增應用程式")
6. 在**搜尋方塊**中，輸入 **Benefitsolver**。
   
   ![應用程式資源庫](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "應用程式資源庫")
7. 在結果窗格中，選取 [Benefitsolver]，然後按一下 [完成] 以新增應用程式。
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>設定單一登入

本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶驗證至 Benefitsolver 。  

Benefitsolver 應用程式需要特定格式的 SAML 判斷提示，因此您必須將自訂屬性對應加入 **SAML Token 屬性** 組態。 

以下螢幕擷取畫面顯示上述的範例。

![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "屬性")

**若要設定單一登入，請執行下列步驟：**

1. 在 Azure 傳統入口網站的 **Benefitsolver** 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "設定單一登入")
2. 在 [要如何讓使用者登入 Benefitsolver] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。
   
   ![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "設定單一登入")
3. 在 [設定應用程式設定]  頁面上，執行下列步驟：
   
   ![設定應用程式設定](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "進行應用程式設定")
   
   1. 在 [登入 URL] 文字方塊中，輸入：**http://azure.benefitsolver.com**。
   2. 在 [回覆 URL] 文字方塊中，輸入 **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**。  
   3. 按一下 [下一步] 。
4. 在 [設定在 Benefitsolver 單一登入] 頁面上，按一下 [下載中繼資料] 以下載您的中繼資料，然後將中繼資料檔儲存在您的本機電腦中。
   
   ![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "設定單一登入")
5. 將下載的中繼資料檔傳送給 Benefitsolver 支援小組。
   
   >[!NOTE]
   >Benefitsolver 支援小組必須執行實際的 SSO 組態。 當您的訂用帳戶啟用 SSO 之後，您會收到通知。
   >

6. 在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "設定單一登入")
7. 在頂端的功能表中，按一下 [屬性] **屬性** to open the **SAML Token 屬性** 對話方塊。
   
   ![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "屬性")
8. 若要加入必要的屬性對應，請執行下列步驟：
   
   ![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "屬性")
   
   | 屬性名稱 | 屬性值 |
   | --- | --- |
   | ClientID |您需要向 Benefitsolver 支援小組取得這個值。 |
   | ClientKey |您需要向 Benefitsolver 支援小組取得這個值。 |
   | LogoutURL |您需要向 Benefitsolver 支援小組取得這個值。 |
   | EmployeeID |您需要向 Benefitsolver 支援小組取得這個值。 |
   
   1. 針對上表中的每個資料列，按一下 [加入使用者屬性] 。
   2. 在 [屬性名稱]  文字方塊中，輸入該資料列所顯示的屬性名稱。
   3. 在 [屬性值]  文字方塊中，選取該資料列所顯示的屬性值。
   4. 按一下 [完成] 。
9. 按一下 [套用變更] 。

## <a name="configure-user-provisioning"></a>設定使用者佈建
若要讓 Azure AD 使用者可以登入 Benefitsolver，必須將他們佈建到 Benefitsolver。  

在 Benefitsolver 案例中，員工資料是透過您的 HRIS 系統的普查檔案填入應用程式中 (通常是每晚)。  

>[!NOTE]
>您可以使用任何其他的 Benefitsolver 使用者帳戶建立工具或 Benefitsolver 提供的 API 來佈建 AAD 使用者帳戶。 
> 

## <a name="assigning-users"></a>指派使用者
若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a>若要將使用者指派給 Benefitsolver，請執行下列步驟：
1. 在 Azure 傳統入口網站中建立測試帳戶。
2. 在 * * Benefitsolver * * 應用程式整合頁面上，按一下 **指派使用者**。
   
   ![指派使用者](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "指派使用者")
3. 選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。
   
   ![是](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "是")

如果要測試您的單一登入設定，請開啟存取面板。 如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。

