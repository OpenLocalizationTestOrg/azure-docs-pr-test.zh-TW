---
title: "在 Azure API 管理中使用群組管理開發人員帳戶 | Microsoft Docs"
description: "了解如何在 Azure API 管理中使用群組來管理管理開發人員帳戶。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="24850-103">如何在 Azure API 管理中建立和使用群組來管理開發人員帳戶</span><span class="sxs-lookup"><span data-stu-id="24850-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="24850-104">在 API 管理中，群組的作用是管理產品對於開發人員的可見度。</span><span class="sxs-lookup"><span data-stu-id="24850-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="24850-105">產品是先設為可讓群組看見，然後群組中的開發人員就能檢視和訂閱與群組相關聯的產品。</span><span class="sxs-lookup"><span data-stu-id="24850-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="24850-106">API 管理具有下列不可變的系統群組。</span><span class="sxs-lookup"><span data-stu-id="24850-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="24850-107">**管理員** - Azure 訂用帳戶管理員是此群組的成員。</span><span class="sxs-lookup"><span data-stu-id="24850-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="24850-108">管理員可管理 API 管理服務執行個體、建立開發人員所使用的 API、作業和產品。</span><span class="sxs-lookup"><span data-stu-id="24850-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="24850-109">**開發人員** - 已驗證開發人員入口網站使用者屬於此群組。</span><span class="sxs-lookup"><span data-stu-id="24850-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="24850-110">開發人員是使用您的 API 建置應用程式的客戶。</span><span class="sxs-lookup"><span data-stu-id="24850-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="24850-111">開發人員獲授與開發人員入口網站的存取權，並建置呼叫 API 作業的應用程式。</span><span class="sxs-lookup"><span data-stu-id="24850-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="24850-112">**來賓** - 未經驗證的開發人員入口網站使用者 (例如，造訪 API 管理執行個體之開發人員入口網站的潛在客戶) 屬於此群組。</span><span class="sxs-lookup"><span data-stu-id="24850-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="24850-113">他們可獲得特定唯讀存取權限，例如他們可檢視 API 但無法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="24850-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="24850-114">除了這些系統群組以外，管理員還可以建立自訂群組，或使用 [使用 Azure Active Directory 相關租用戶中的外部群組][leverage external groups in associated Azure Active Directory tenants]。</span><span class="sxs-lookup"><span data-stu-id="24850-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="24850-115">自訂群組和外部群組可以與系統群組一起使用，提供開發人員 API 產品的能見度及存取權。</span><span class="sxs-lookup"><span data-stu-id="24850-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="24850-116">例如，您可以為與特定夥伴組織有關的開發人員建立一個自訂群組，並只允許他們存取來自含相關 API 之產品的 API。</span><span class="sxs-lookup"><span data-stu-id="24850-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="24850-117">使用者可以是多個群組的成員。</span><span class="sxs-lookup"><span data-stu-id="24850-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="24850-118">本指南說明 API 管理執行個體的管理員如何加入新的群組，並將這些群組與產品和開發人員建立關聯。</span><span class="sxs-lookup"><span data-stu-id="24850-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="24850-119">除了在發佈者入口網站中建立和管理群組，您還可以使用 API 管理 REST API [群組](https://msdn.microsoft.com/library/azure/dn776329.aspx) 實體，建立和管理您的群組。</span><span class="sxs-lookup"><span data-stu-id="24850-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="24850-120"><a name="create-group"> </a>建立群組</span><span class="sxs-lookup"><span data-stu-id="24850-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="24850-121">若要建立新的群組，請在您「API 管理」服務的「Azure 入口網站」中按一下 [發行者入口網站]。</span><span class="sxs-lookup"><span data-stu-id="24850-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="24850-122">這會帶您前往 API 管理發行者入口網站。</span><span class="sxs-lookup"><span data-stu-id="24850-122">This takes you to the API Management publisher portal.</span></span>

![發行者入口網站][api-management-management-console]

> <span data-ttu-id="24850-124">如果您尚未建立 API 管理服務執行個體，請參閱[開始使用 Azure API 管理][Get started with Azure API Management]教學課程中的[建立 API 管理服務執行個體][Create an API Management service instance]。</span><span class="sxs-lookup"><span data-stu-id="24850-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="24850-125">從左邊的 [API 管理] 功能表中按一下 [群組]，然後按一下 [新增群組]。</span><span class="sxs-lookup"><span data-stu-id="24850-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Add new group][api-management-add-group]

<span data-ttu-id="24850-127">輸入群組的唯一名稱和選用的描述，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="24850-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Add new group][api-management-add-group-window]

<span data-ttu-id="24850-129">新群組會顯示在 [群組] 索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="24850-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="24850-130">若要編輯群組的 [名稱] 或 [說明]，請在清單中按一下群組名稱。</span><span class="sxs-lookup"><span data-stu-id="24850-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="24850-131">若要刪除群組，請按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="24850-131">To delete the group, click **Delete**.</span></span>

![Group added][api-management-new-group]

<span data-ttu-id="24850-133">現在已建立群組，它可以與產品和開發人員建立關聯。</span><span class="sxs-lookup"><span data-stu-id="24850-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="24850-134"><a name="associate-group-product"> </a>將群組與產品建立關聯</span><span class="sxs-lookup"><span data-stu-id="24850-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="24850-135">若要將群組與產品建立關聯，請從左邊的 [API 管理] 功能表中按一下 [產品]，然後按一下所需產品的名稱。</span><span class="sxs-lookup"><span data-stu-id="24850-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Set visibility][api-management-add-group-to-product]

<span data-ttu-id="24850-137">選取 [可見度]  索引標籤來加入和移除群組，以及檢視產品的目前群組。</span><span class="sxs-lookup"><span data-stu-id="24850-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="24850-138">若要加入或移除群組，請核取或取消核取所需群組的核取方塊，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="24850-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Set visibility][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="24850-140">若要加入 Azure Active Directory 群組，請參閱 [如何在 Azure API 管理中使用 Azure Active Directory 授權開發人員帳戶](api-management-howto-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="24850-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="24850-141">若要從產品的 [可見度] 索引標籤中設定群組，請按一下 [管理群組]。</span><span class="sxs-lookup"><span data-stu-id="24850-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="24850-142">當產品與群組建立關聯之後，該群組中的開發人員就可以檢視和訂閱產品。</span><span class="sxs-lookup"><span data-stu-id="24850-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="24850-143"><a name="associate-group-developer"> </a>將群組與開發人員建立關聯</span><span class="sxs-lookup"><span data-stu-id="24850-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="24850-144">若要將群組與開發人員建立關聯，請從左邊的 [API 管理] 功能表中，按一下 [使用者]，然後核取要與群組建立關聯之開發人員旁邊的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="24850-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Add developer to group][api-management-add-group-to-developer]

<span data-ttu-id="24850-146">核取想要的開發人員之後，在 [加入群組]  下拉式清單中按一下所需的群組。</span><span class="sxs-lookup"><span data-stu-id="24850-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="24850-147">使用 [Remove from Group]  下拉式清單，可從群組中移除開發人員。</span><span class="sxs-lookup"><span data-stu-id="24850-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![開發人員][api-management-add-group-to-developer-saved]

<span data-ttu-id="24850-149">在開發人員與群組之間加入關聯之後，您可以在 [ **使用者** ] 索引標籤中檢視此關聯。</span><span class="sxs-lookup"><span data-stu-id="24850-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="24850-150"><a name="next-steps"> </a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="24850-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="24850-151">當開發人員加入至群組之後，他們就可以檢視和訂閱與該群組相關聯的產品。</span><span class="sxs-lookup"><span data-stu-id="24850-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="24850-152">如需詳細資訊，請參閱 [如何在 Azure API 管理中建立和發佈產品][How create and publish a product in Azure API Management]。</span><span class="sxs-lookup"><span data-stu-id="24850-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="24850-153">除了在發佈者入口網站中建立和管理群組，您還可以使用 API 管理 REST API [群組](https://msdn.microsoft.com/library/azure/dn776329.aspx) 實體，建立和管理您的群組。</span><span class="sxs-lookup"><span data-stu-id="24850-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
