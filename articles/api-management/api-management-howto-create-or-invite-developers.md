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
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="a1850-103">如何 toomanage 使用者帳戶在 Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="a1850-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="a1850-104">在 API 管理開發人員會是 hello hello Api 公開使用 API 管理使用者。</span><span class="sxs-lookup"><span data-stu-id="a1850-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="a1850-105">此指南示範 toohow toocreate 和邀請開發人員 toouse hello 應用程式開發介面和可用 toothem 利用您的 API 管理執行個體的產品。</span><span class="sxs-lookup"><span data-stu-id="a1850-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="a1850-106">如需以程式設計方式管理使用者帳戶資訊，請參閱 hello[使用者實體](https://msdn.microsoft.com/library/azure/dn776330.aspx)文件以 hello [API 管理 REST](https://msdn.microsoft.com/library/azure/dn776326.aspx)參考。</span><span class="sxs-lookup"><span data-stu-id="a1850-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="a1850-107"><a name="create-developer"> </a>建立新的開發人員</span><span class="sxs-lookup"><span data-stu-id="a1850-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="a1850-108">按一下 新的開發人員，toocreate**發行者入口網站**API 管理服務的 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a1850-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="a1850-109">這會帶您 toohello API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="a1850-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="a1850-110">如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。</span><span class="sxs-lookup"><span data-stu-id="a1850-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![發行者入口網站][api-management-management-console]

<span data-ttu-id="a1850-112">按一下**使用者**從 hello **API 管理**hello 左、，然後按一下功能表**將使用者加入**。</span><span class="sxs-lookup"><span data-stu-id="a1850-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![Create developer][api-management-create-developer]

<span data-ttu-id="a1850-114">輸入 hello**電子郵件**，**密碼**，和**名稱**hello 新的開發人員，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="a1850-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![Create developer][api-management-add-new-user]

<span data-ttu-id="a1850-116">根據預設，會建立新的開發人員帳戶**Active**，與 hello 與**開發人員**群組。</span><span class="sxs-lookup"><span data-stu-id="a1850-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![New developer][api-management-new-developer]

<span data-ttu-id="a1850-118">中的開發人員帳戶**active**狀態可以是使用的 tooaccess 所有 hello Api 他們擁有的訂閱。</span><span class="sxs-lookup"><span data-stu-id="a1850-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="a1850-119">tooassociate hello 新建立的開發人員與其他群組，請參閱[tooassociate 與開發人員的群組方式][How tooassociate groups with developers]。</span><span class="sxs-lookup"><span data-stu-id="a1850-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="a1850-120"><a name="invite-developer"> </a>邀請開發人員</span><span class="sxs-lookup"><span data-stu-id="a1850-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="a1850-121">tooinvite 為開發人員，按一下**使用者**從 hello **API 管理**hello 左、，然後按一下功能表**邀請使用者**。</span><span class="sxs-lookup"><span data-stu-id="a1850-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![Invite developer][api-management-invite-developer]

<span data-ttu-id="a1850-123">輸入 hello 名稱和電子郵件地址 hello 開發人員，然後按一下 **邀請**。</span><span class="sxs-lookup"><span data-stu-id="a1850-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![Invite developer][api-management-invite-developer-window]

<span data-ttu-id="a1850-125">會顯示確認訊息，但新邀請 hello 開發人員不會顯示在 hello 清單，直到他們接受 hello 邀請之後。</span><span class="sxs-lookup"><span data-stu-id="a1850-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![Invite confirmation][api-management-invite-developer-confirmation]

<span data-ttu-id="a1850-127">當開發人員會受邀時，電子郵件傳送 toohello 開發人員。</span><span class="sxs-lookup"><span data-stu-id="a1850-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="a1850-128">此電子郵件是以範本產生，可自訂。</span><span class="sxs-lookup"><span data-stu-id="a1850-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="a1850-129">如需詳細資訊，請參閱 [設定電子郵件範本][Configure email templates]。</span><span class="sxs-lookup"><span data-stu-id="a1850-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="a1850-130">一旦接受 hello 邀請，hello 帳戶變成作用中。</span><span class="sxs-lookup"><span data-stu-id="a1850-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="a1850-131"><a name="block-developer"> </a> 停用或重新啟用開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="a1850-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="a1850-132">依預設，新建立或邀請的開發人員帳戶為「作用中」 。</span><span class="sxs-lookup"><span data-stu-id="a1850-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="a1850-133">toodeactivate 開發人員帳戶，按一下**區塊**。</span><span class="sxs-lookup"><span data-stu-id="a1850-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="a1850-134">tooreactivate 封鎖的開發人員帳戶，按一下**Activate**。</span><span class="sxs-lookup"><span data-stu-id="a1850-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="a1850-135">已封鎖的開發人員帳戶無法存取 hello 開發人員入口網站，或呼叫任何 Api。</span><span class="sxs-lookup"><span data-stu-id="a1850-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="a1850-136">toodelete 使用者帳戶，按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="a1850-136">toodelete a user account, click **Delete**.</span></span>

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="a1850-138">重設使用者密碼</span><span class="sxs-lookup"><span data-stu-id="a1850-138">Reset a user password</span></span>
<span data-ttu-id="a1850-139">tooreset hello 使用者帳戶密碼，按一下 hello hello 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a1850-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![重設密碼][api-management-view-developer]

<span data-ttu-id="a1850-141">按一下**重設密碼**toosend 連結 toohello 使用者 tooreset 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="a1850-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![重設密碼][api-management-reset-password]

<span data-ttu-id="a1850-143">tooprogrammatically 使用使用者帳戶，請參閱 hello[使用者實體](https://msdn.microsoft.com/library/azure/dn776330.aspx)文件以 hello [API 管理 REST](https://msdn.microsoft.com/library/azure/dn776326.aspx)參考。</span><span class="sxs-lookup"><span data-stu-id="a1850-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="a1850-144">tooreset 使用者帳戶密碼 tooa 特定值，您可以使用 hello[更新使用者](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser)作業並指定 hello 所需的密碼。</span><span class="sxs-lookup"><span data-stu-id="a1850-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="a1850-145">擱置驗證</span><span class="sxs-lookup"><span data-stu-id="a1850-145">Pending verification</span></span>
![擱置驗證][api-management-pending-verification]

## <span data-ttu-id="a1850-147"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1850-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="a1850-148">開發人員帳戶建立之後，您可以將它與角色關聯，並訂閱 tooproducts 和 Api。</span><span class="sxs-lookup"><span data-stu-id="a1850-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="a1850-149">如需詳細資訊，請參閱[如何 toocreate 和使用群組][How toocreate and use groups]。</span><span class="sxs-lookup"><span data-stu-id="a1850-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

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
