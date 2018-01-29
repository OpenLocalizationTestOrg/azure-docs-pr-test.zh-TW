---
title: "如何將現有的 Azure 訂用帳戶新增至您的 Azure AD 目錄 | Microsoft Docs"
description: "如何將現有的訂用帳戶新增至您的 Azure AD 目錄"
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/12/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: e063e6a46b6b99c4bbe749347e6887a930adb882
ms.sourcegitcommit: 0e1c4b925c778de4924c4985504a1791b8330c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/06/2018
---
# <a name="how-to-associate-or-add-an-azure-subscription-to-azure-active-directory"></a>如何將 Azure 訂用帳戶關聯或新增至 Azure Active Directory

本文涵蓋有關 Azure 訂用帳戶與 Azure Active Directory (Azure AD) 之間關係，以及如何將現有訂用帳戶新增至 Azure AD 目錄的資訊。 Azure 訂用帳戶具有 Azure AD 目錄的信任關係，這表示它信任此目錄來驗證使用者、服務和裝置。 多個訂用帳戶可以信任相同的目錄，但是每個訂用帳戶只能信任一個目錄。 

訂用帳戶與目錄之間存在的信任關係不同於訂用帳戶與 Azure 中其他資源 (網站、資料庫等) 之間的關係。 如果訂用帳戶已過期，也會停止存取與訂用帳戶相關聯的其他資源。 但 Azure AD 目錄會保留在 Azure 中，而且您可以將不同的訂用帳戶與該目錄產生關聯，以及使用新的訂用帳戶管理此目錄。

所有使用者都有會對他們進行驗證的單一主目錄，但是他它們也可以是其他目錄中的來賓。 在 Azure AD 中，您可以看到您的使用者帳戶為其成員或來賓的目錄。

## <a name="before-you-begin"></a>開始之前

* 您必須使用具有訂用帳戶之 RBAC 擁有者存取權的帳戶登入。
* 您用於登入的帳戶必須同時存在於與訂用帳戶相關聯的目前目錄中和您想要將訂用帳戶新增至的目錄中。 若要深入了解如何取得其他目錄的存取權，請參閱 [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者](active-directory-b2b-admin-add-users.md)

## <a name="to-associate-an-existing-subscription-to-your-azure-ad-directory"></a>將現有的訂用帳戶關聯至您的 Azure AD 目錄

1. 在 [Azure 入口網站的 [訂用帳戶] 頁面](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)登入並選取訂用帳戶。
2. 按一下 [變更目錄]。

    ![顯示變更目錄按鈕的螢幕擷取畫面](./media/active-directory-how-subscriptions-associated-directory/edit-directory-button.PNG)
3. 檢閱警告。 所有具備指派存取權的[角色型存取控制 (RBAC)](role-based-access-control-configure.md) 使用者以及所有訂用帳戶管理員都會在訂用帳戶目錄變更時喪失存取權。
4. 選取目錄。

    ![顯示變更目錄 UI 的螢幕擷取畫面](./media/active-directory-how-subscriptions-associated-directory/edit-directory-ui.PNG)
5. 按一下 [變更]。
6. 成功！ 使用目錄切換器來移至新的目錄。 最多可能需要 10 分鐘的時間才能正確顯示所有項目。

    ![顯示變更目錄成功通知的螢幕擷取畫面](./media/active-directory-how-subscriptions-associated-directory/edit-directory-success.PNG)

    ![顯示切換器的螢幕擷取畫面](./media/active-directory-how-subscriptions-associated-directory/directory-switcher.PNG)


變更訂用帳戶目錄是一項服務層級作業。 它並不會影響訂用帳戶帳單擁有權，而帳戶管理員仍然可以透過[帳戶中心](https://account.azure.com/subscriptions)變更服務管理員。 如果您想要刪除原始目錄，您必須將訂用帳戶的帳單擁有權轉移給新的帳戶管理員。若要深入了解如何移轉帳單擁有權，請參閱[將 Azure 訂用帳戶的擁有權轉移轉至另一個帳戶](../billing/billing-subscription-transfer.md)。 

## <a name="next-steps"></a>後續步驟

* 若要深入了解如何免費建立新的 Azure AD 目錄，請參閱[如何取得 Azure Active Directory 租用戶](develop/active-directory-howto-tenant.md)
* 若要深入了解如何移轉 Azure 訂用帳戶的帳單擁有權，請參閱[將 Azure 訂用帳戶的擁有權轉移轉至另一個帳戶](../billing/billing-subscription-transfer.md)
* 若要深入了解如何在 Microsoft Azure 中控制資源存取，請參閱 [了解 Azure 中的資源存取](active-directory-understanding-resource-access.md)
* 如需有關如何在 Azure AD 中指派角色的詳細資訊，請參閱 [在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
