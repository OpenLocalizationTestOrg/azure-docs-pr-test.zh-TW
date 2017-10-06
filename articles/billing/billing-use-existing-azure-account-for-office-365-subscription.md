---
title: "註冊 Office 365 與 Azure 帳戶的 aaaSign |Microsoft 文件"
description: "深入了解如何使用 Azure 帳戶 toocreate Office 365 訂用帳戶"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: d19e1c1edff0b9658b639e796a72bbf4e87b9c3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a>使用 Azure 帳戶註冊 Office 365 訂用帳戶
如果您是 Azure 訂閱者時，您可以使用您的 Azure 帳戶 toosign 註冊 Office 365 訂閱。 如果您屬於具有 Azure 訂用帳戶的組織，您可以為現有 Azure Active Directory (Azure AD) 中的使用者建立 Office 365 訂用帳戶。 註冊 tooOffice 365 使用 Azure Active Directory 租用戶中具有全域管理員或帳單的系統管理員權限的帳戶。 如需詳細資訊，請參閱[在 Azure AD 中檢查我的帳戶權限](#RoleInAzureAD)和[在 Azure Active Directory 中指派系統管理員角色](../active-directory/active-directory-assign-admin-roles.md)。

如果您已經有 Office 365 帳戶和 Azure 訂用帳戶，您可以[將 Office 365 租用戶 tooan Azure 訂用帳戶產生關聯](billing-add-office-365-tenant-to-azure-subscription.md)。

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a>使用 Azure 帳戶取得 Office 365 訂用帳戶

1. 移 toohello [Office 365 產品頁面](https://products.office.com/business)，選取計劃。
2. 按一下**登入**hello hello 頁面右上角。

    ![Office 365 試用頁面的螢幕擷取畫面](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. 使用 Azure 帳戶認證進行登入。 如果您要為您的組織建立訂用帳戶，使用 Azure 帳戶，您的 Azure Active Directory 租用戶中的 hello 全域管理員或計費管理員目錄角色的成員。

    ![Office 365 登入的螢幕擷取畫面](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. 按一下 [立即試用] 。

    ![確認您的 Office 365 訂單的螢幕擷取畫面。](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. 在 hello 順序回條] 頁面上，按一下 [**繼續**。

    ![收到 hello Office 365 訂單的螢幕擷取畫面](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

這樣就準備好了。 如果您為組織建立 hello Office 365 訂用帳戶，請使用下列 Azure AD 使用者現在會在 Office 365 中的步驟 toocheck hello。

1. 開啟 hello Office 365 系統管理中心。
2. 展開 使用者，然後按一下作用中使用者。

    ![Hello Office 365 admin center 使用者的螢幕擷取畫面](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

Hello Office 365 訂用帳戶註冊之後，會加入 toohello 相同 Azure 訂用帳戶所屬的 Azure Active Directory 執行個體。 如需詳細資訊，請參閱[深入了解 Azure 和 Office 365 訂用帳戶](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs)和[Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](../active-directory/active-directory-how-subscriptions-associated-directory.md)。

## <a id="RoleInAzureAD"></a>在 Azure AD 中檢查我的帳戶權限
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下 [更多服務]，然後搜尋 [Active Directory]。

    ![螢幕擷取畫面的 Active Directory 的 hello Azure 入口網站](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. 按一下 [使用者和群組] > [所有使用者]。
4. 選取 hello 使用者名稱。 

    ![顯示 hello Azure Active Directory 使用者的螢幕擷取畫面](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. 按一下 [目錄角色]。
  
    ![顯示 hello Azure 入口網站的目錄角色的螢幕擷取畫面](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  hello 角色**全域管理員**或**有限的系統管理員** > **計費管理員**是必要的 toocreate Office 365 訂閱的使用者在現有的 Azure Active Directory。

    ![顯示 Azure 入口網站目錄角色帳務管理員的螢幕擷取畫面](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。 
