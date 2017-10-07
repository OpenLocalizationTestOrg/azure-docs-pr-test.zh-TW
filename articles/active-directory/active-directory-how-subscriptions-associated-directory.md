---
title: "aaaHow Azure 訂用帳戶相關聯 Azure Active Directory |Microsoft 文件"
description: "登入 tooMicrosoft Azure 和相關的問題，例如 hello Azure 訂用帳戶與 Azure Active Directory 之間的關聯性。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Azure 訂用帳戶如何與 Azure Active Directory 產生關聯
本文涵蓋 hello Azure 訂用帳戶與 Azure Active Directory (Azure AD) 之間的關聯性的相關資訊及如何 tooadd 現有的訂用帳戶 tooyour Azure AD 目錄。

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>您的 Azure 訂閱關聯性 tooAzure AD
您的 Azure 訂用帳戶已與 Azure AD，表示其信任 hello directory tooauthenticate 使用者、 服務和裝置的信任關係。 多個訂閱可以信任 hello 相同的目錄，但每個訂閱只能信任一個目錄。 

hello 之間的信任關係的訂用帳戶的目錄是不同於它與其他資源 （網站、 資料庫等等） 的 Azure 中的 hello 關係。 如果訂閱已過期，存取 toohello hello 訂用帳戶相關聯的其他資源也會停止。 Azure AD 目錄會保留在 Azure 中，但您可以將不同的訂用帳戶與該目錄產生關聯，並管理 hello 目錄使用 hello 新訂用帳戶。

![訂用帳戶如何與圖表產生關聯](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

所有使用者都有會對他們進行驗證的單一主目錄，但是他它們也可以是其他目錄中的來賓。 在 Azure AD 中，您可以看到其中您的使用者帳戶是成員或來賓 hello 目錄。

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD 和雲端服務訂用帳戶
Azure AD 提供 hello 核心目錄和身分識別管理功能的支援大部分的 Microsoft 雲端服務，包括：

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

當您註冊的任何這些 Microsoft 雲端服務，您會收到 hello 免費的 Azure AD 服務。 如果您想 tooadd 其他 Azure 訂用帳戶 tooan Azure AD 目錄，您必須登入 Microsoft 帳戶。 如果您登入 tooAzure 的工作或學校帳戶，您無法加入 tooan 現有 Azure 訂用帳戶的目錄，因為您工作或學校帳戶，無法直接由 Azure 進行驗證。 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>tooadd 現有的訂用帳戶 tooyour Azure AD 目錄
您必須使用這兩個 hello 目前的目錄中的 hello 與相關聯的訂用帳戶已存在的帳戶，登入，而且希望在 hello 目錄 tooadd 它。 

1. 登入 toohello [Azure 帳戶中心](https://account.windowsazure.com/Home/Index)想 tootransfer 是 hello hello 訂用帳戶的帳戶管理員的擁有權的帳戶。
2. 請確定您想 toobe hello 訂用帳戶擁有者為目標的 hello 目錄中的 hello 使用者。
3. 按一下 [移轉訂用帳戶]。
4. 指定 hello 收件者。 hello 收件者自動取得含有接受連結的電子郵件。
5. hello 收件者按一下 hello 連結，並遵循 hello 指示，包括輸入其付款資訊。 Hello 收件者成功時，會傳送 hello 訂用帳戶。 
6. hello hello 訂用帳戶的預設目錄變更 toohello 目錄中的 hello 使用者是。


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>建議 toomanage 的訂閱和目錄
hello Azure 訂用帳戶的系統管理角色來管理資源繫結 toohello Azure 訂用帳戶。 本節說明 hello Azure 訂用帳戶系統管理員與 Azure AD 目錄管理員之間的差異。 系統管理角色和其他建議使用這些訂用帳戶均涵蓋於 toomanage[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles.md)。

根據預設，您獲指派 hello 服務系統管理員角色，當您註冊。 如果其他人需要 toosign 中的並使用 hello 存取服務相同的訂用帳戶，您可以將它們新增為共同管理員。 

Azure AD 有一組不同的系統管理角色 toomanage hello 目錄和身分識別相關功能。 例如，hello 目錄全域管理員可以新增使用者和群組 toohello 目錄，或需要多重要素驗證的使用者。 建立目錄的使用者指派 toohello 全域管理員角色，他們可以指派管理角色 tooother 使用者。 其他服務 (例如 Office 365 和 Microsoft Intune) 也會使用 Azure AD 系統管理角色。 

Azure 訂用帳戶管理員和 Azure AD 目錄管理員是兩個不同的角色。 
* Azure 訂用帳戶系統管理員可以管理 Azure 中的資源，而且可以在 hello Azure 入口網站中使用 Azure AD，（因為 hello Azure 入口網站本身是一項 Azure 資源）。 
* 目錄管理員可以管理屬性只能在 hello Azure AD 目錄中。

使用者可以同時擔任這兩個角色，但並非必要。 無法將目錄全域管理員指派為 Azure 訂用帳戶的服務管理員或共同管理員 (反之亦然)。 不是 hello 訂用帳戶的系統管理員，hello 使用者可以登入 toohello Azure 入口網站，但無法管理該訂用帳戶在 hello 入口網站中的 hello 目錄。 不過，這位使用者可以管理使用 Azure AD PowerShell 或 Office 365 系統管理中心 hello 之類的其他工具的目錄。

## <a name="next-steps"></a>後續步驟
* toolearn 深入了解如何 toochange 管理員 Azure 訂用帳戶，請參閱[的 Azure 訂用帳戶 tooanother 帳戶的擁有權轉移](../billing/billing-subscription-transfer.md)
* toolearn 深入了解如何控制資源存取 Microsoft Azure 中，請參閱[了解 Azure 中的資源存取](active-directory-understanding-resource-access.md)
* 如需有關如何 tooassign 角色在 Azure AD 中，請參閱[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
