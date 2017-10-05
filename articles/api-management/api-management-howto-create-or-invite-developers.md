---
title: "如何在 Azure API 管理中管理使用者帳戶 | Microsoft Docs"
description: "了解如何在 Azure API 管理中建立或邀請使用者"
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
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="ee63d-103">如何在 Azure API 管理中管理使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="ee63d-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="ee63d-104">在 API 管理中，開發人員是指您使用 API 管理所公開之 API 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ee63d-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="ee63d-105">本指南示範如何建立並邀請開發人員使用您以 API 管理執行個體提供給他們的 API 和產品。</span><span class="sxs-lookup"><span data-stu-id="ee63d-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="ee63d-106">如需以程式設計方式管理使用者帳戶的相關資訊，請參閱 [API 管理 REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) 參考中的[使用者實體](https://msdn.microsoft.com/library/azure/dn776330.aspx)文件。</span><span class="sxs-lookup"><span data-stu-id="ee63d-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="ee63d-107"><a name="create-developer"> </a>建立新的開發人員</span><span class="sxs-lookup"><span data-stu-id="ee63d-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="ee63d-108">若要建立新的開發人員，請在您「API 管理」服務的「Azure 入口網站」中按一下 [發行者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="ee63d-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="ee63d-109">這會帶您前往 API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="ee63d-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="ee63d-110">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="ee63d-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![發行者入口網站][api-management-management-console]

<span data-ttu-id="ee63d-112">從左邊的 [API 管理] 功能表中按一下 [使用者]，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="ee63d-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Create developer][api-management-create-developer]

<span data-ttu-id="ee63d-114">輸入新開發人員的 [電子郵件]、[密碼] 和 [名稱]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ee63d-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Create developer][api-management-add-new-user]

<span data-ttu-id="ee63d-116">依預設，新建立的開發人員帳戶為 [作用中]，且與 [開發人員] 群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="ee63d-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![New developer][api-management-new-developer]

<span data-ttu-id="ee63d-118">處於「作用中」  狀態的開發人員帳戶可用來存取擁有訂用帳戶的所有 API。</span><span class="sxs-lookup"><span data-stu-id="ee63d-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="ee63d-119">若要將新建立的開發人員與其他群組建立關聯，請參閱 [如何將群組與開發人員建立關聯][How to associate groups with developers]。</span><span class="sxs-lookup"><span data-stu-id="ee63d-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="ee63d-120"><a name="invite-developer"> </a>邀請開發人員</span><span class="sxs-lookup"><span data-stu-id="ee63d-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="ee63d-121">若要邀請開發人員，請從左邊的 [API 管理] 功能表中按一下 [使用者]，然後按一下 [邀請使用者]。</span><span class="sxs-lookup"><span data-stu-id="ee63d-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Invite developer][api-management-invite-developer]

<span data-ttu-id="ee63d-123">輸入開發人員的名稱和電子郵件地址，然後按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="ee63d-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Invite developer][api-management-invite-developer-window]

<span data-ttu-id="ee63d-125">這時會顯示確認訊息，但剛獲邀的開發人員在尚未接受邀請之前，都不會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="ee63d-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Invite confirmation][api-management-invite-developer-confirmation]

<span data-ttu-id="ee63d-127">邀請開發人員時，有一封電子郵件會傳送給開發人員。</span><span class="sxs-lookup"><span data-stu-id="ee63d-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="ee63d-128">此電子郵件是以範本產生，可自訂。</span><span class="sxs-lookup"><span data-stu-id="ee63d-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="ee63d-129">如需詳細資訊，請參閱 [設定電子郵件範本][Configure email templates]。</span><span class="sxs-lookup"><span data-stu-id="ee63d-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="ee63d-130">接受邀請時，帳戶就會變成作用中。</span><span class="sxs-lookup"><span data-stu-id="ee63d-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="ee63d-131"><a name="block-developer"> </a> 停用或重新啟用開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="ee63d-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="ee63d-132">依預設，新建立或邀請的開發人員帳戶為「作用中」 。</span><span class="sxs-lookup"><span data-stu-id="ee63d-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="ee63d-133">若要停用開發人員帳戶，請按一下 [封鎖] 。</span><span class="sxs-lookup"><span data-stu-id="ee63d-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="ee63d-134">若要重新啟用已封鎖的開發人員帳戶，請按一下 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="ee63d-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="ee63d-135">已封鎖的開發人員帳戶無法存取開發人員入口網站或呼叫任何 API。</span><span class="sxs-lookup"><span data-stu-id="ee63d-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="ee63d-136">若要刪除使用者帳戶，請按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="ee63d-136">To delete a user account, click **Delete**.</span></span>

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="ee63d-138">重設使用者密碼</span><span class="sxs-lookup"><span data-stu-id="ee63d-138">Reset a user password</span></span>
<span data-ttu-id="ee63d-139">若要重設使用者帳戶的密碼，請按一下帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="ee63d-139">To reset the password for a user account, click the name of the account.</span></span>

![重設密碼][api-management-view-developer]

<span data-ttu-id="ee63d-141">按一下 [重設密碼]  連結可傳送連結給使用者，以便重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="ee63d-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![重設密碼][api-management-reset-password]

<span data-ttu-id="ee63d-143">若要以程式設計方式使用使用者帳戶，請參閱 [API 管理 REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) 參考中的[使用者實體](https://msdn.microsoft.com/library/azure/dn776330.aspx)文件。</span><span class="sxs-lookup"><span data-stu-id="ee63d-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="ee63d-144">若要將使用者帳戶密碼重設為特定值，您可以使用 [更新使用者](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) 作業並指定所要的密碼。</span><span class="sxs-lookup"><span data-stu-id="ee63d-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="ee63d-145">擱置驗證</span><span class="sxs-lookup"><span data-stu-id="ee63d-145">Pending verification</span></span>
![擱置驗證][api-management-pending-verification]

## <span data-ttu-id="ee63d-147"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee63d-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="ee63d-148">建立開發人員帳戶之後，您可以將它與角色建立關聯，並讓它訂閱產品和 API。</span><span class="sxs-lookup"><span data-stu-id="ee63d-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="ee63d-149">如需詳細資訊，請參閱[如何建立和使用群組][How to create and use groups]。</span><span class="sxs-lookup"><span data-stu-id="ee63d-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

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
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
