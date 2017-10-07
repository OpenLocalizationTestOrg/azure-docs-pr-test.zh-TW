---
title: "aaaHow 管理使用者帳戶，在 Azure API 管理 |Microsoft 文件"
description: "深入了解如何在 Azure API 管理 toocreate 或邀請使用者"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a>如何 toomanage 使用者帳戶在 Azure API 管理
在 API 管理開發人員會是 hello hello Api 公開使用 API 管理使用者。 此指南示範 toohow toocreate 和邀請開發人員 toouse hello 應用程式開發介面和可用 toothem 利用您的 API 管理執行個體的產品。 如需以程式設計方式管理使用者帳戶資訊，請參閱 hello[使用者實體](https://msdn.microsoft.com/library/azure/dn776330.aspx)文件以 hello [API 管理 REST](https://msdn.microsoft.com/library/azure/dn776326.aspx)參考。

## <a name="create-developer"> </a>建立新的開發人員
按一下 新的開發人員，toocreate**發行者入口網站**API 管理服務的 hello Azure 入口網站中。 這會帶您 toohello API 管理發行者入口網站。 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。

![發行者入口網站][api-management-management-console]

按一下**使用者**從 hello **API 管理**hello 左、，然後按一下功能表**將使用者加入**。

![Create developer][api-management-create-developer]

輸入 hello**電子郵件**，**密碼**，和**名稱**hello 新的開發人員，然後按一下**儲存**。

![Create developer][api-management-add-new-user]

根據預設，會建立新的開發人員帳戶**Active**，與 hello 與**開發人員**群組。

![New developer][api-management-new-developer]

中的開發人員帳戶**active**狀態可以是使用的 tooaccess 所有 hello Api 他們擁有的訂閱。 tooassociate hello 新建立的開發人員與其他群組，請參閱[tooassociate 與開發人員的群組方式][How tooassociate groups with developers]。

## <a name="invite-developer"> </a>邀請開發人員
tooinvite 為開發人員，按一下**使用者**從 hello **API 管理**hello 左、，然後按一下功能表**邀請使用者**。

![Invite developer][api-management-invite-developer]

輸入 hello 名稱和電子郵件地址 hello 開發人員，然後按一下 **邀請**。

![Invite developer][api-management-invite-developer-window]

會顯示確認訊息，但新邀請 hello 開發人員不會顯示在 hello 清單，直到他們接受 hello 邀請之後。 

![Invite confirmation][api-management-invite-developer-confirmation]

當開發人員會受邀時，電子郵件傳送 toohello 開發人員。 此電子郵件是以範本產生，可自訂。 如需詳細資訊，請參閱 [設定電子郵件範本][Configure email templates]。

一旦接受 hello 邀請，hello 帳戶變成作用中。

## <a name="block-developer"> </a> 停用或重新啟用開發人員帳戶
依預設，新建立或邀請的開發人員帳戶為「作用中」 。 toodeactivate 開發人員帳戶，按一下**區塊**。 tooreactivate 封鎖的開發人員帳戶，按一下**Activate**。 已封鎖的開發人員帳戶無法存取 hello 開發人員入口網站，或呼叫任何 Api。 toodelete 使用者帳戶，按一下**刪除**。

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a>重設使用者密碼
tooreset hello 使用者帳戶密碼，按一下 hello hello 帳戶名稱。

![重設密碼][api-management-view-developer]

按一下**重設密碼**toosend 連結 toohello 使用者 tooreset 他們的密碼。

![重設密碼][api-management-reset-password]

tooprogrammatically 使用使用者帳戶，請參閱 hello[使用者實體](https://msdn.microsoft.com/library/azure/dn776330.aspx)文件以 hello [API 管理 REST](https://msdn.microsoft.com/library/azure/dn776326.aspx)參考。 tooreset 使用者帳戶密碼 tooa 特定值，您可以使用 hello[更新使用者](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser)作業並指定 hello 所需的密碼。

## <a name="pending-verification"></a>擱置驗證
![擱置驗證][api-management-pending-verification]

## <a name="next-steps"> </a>後續步驟
開發人員帳戶建立之後，您可以將它與角色關聯，並訂閱 tooproducts 和 Api。 如需詳細資訊，請參閱[如何 toocreate 和使用群組][How toocreate and use groups]。

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
