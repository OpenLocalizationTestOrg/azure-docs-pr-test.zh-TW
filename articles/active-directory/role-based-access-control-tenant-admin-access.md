---
title: "租用戶管理員提高存取權限 - Azure AD | Microsoft Docs"
description: "本主題說明角色型存取控制 (RBAC) 的內建角色。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: bf64a92b359a6f68d84fa5ee17eda64ed6371990
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="79549-103">使用角色型存取控制以租用戶系統管理員提高存取權限</span><span class="sxs-lookup"><span data-stu-id="79549-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="79549-104">角色型存取控制可協助租用戶系統管理員取得存取權限暫時提升，以便他們可以比平常授與更高的權限。</span><span class="sxs-lookup"><span data-stu-id="79549-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="79549-105">租用戶管理員可以視需要將自己提升至使用者存取系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="79549-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="79549-106">該角色提供租用戶系統管理員權限，可在 "/" 的範圍內授與自己或其他角色。</span><span class="sxs-lookup"><span data-stu-id="79549-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="79549-107">這項功能很重要，因為它可讓租用戶管理員查看組織中的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="79549-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="79549-108">它也可讓自動化應用程式 (如發票開立與稽核) 存取所有的訂用帳戶，並針對帳單或資產管理提供組織狀態的精確檢視。</span><span class="sxs-lookup"><span data-stu-id="79549-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization for billing or asset management.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="79549-109">如何使用 elevateAccess 提供租用戶存取</span><span class="sxs-lookup"><span data-stu-id="79549-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="79549-110">基本程序適用於下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="79549-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="79549-111">使用 REST，呼叫 elevateAccess，這會授與您在 "/" 的範圍的使用者存取系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="79549-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="79549-112">建立[角色指派](/rest/api/authorization/roleassignments)以在任何範圍的指派任何角色。</span><span class="sxs-lookup"><span data-stu-id="79549-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="79549-113">下列範例顯示在 "/" 的範圍指派讀取者角色的屬性︰</span><span class="sxs-lookup"><span data-stu-id="79549-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. <span data-ttu-id="79549-114">在使用者存取的系統管理員時，您也可以在 "/" 的範圍刪除角色指派。</span><span class="sxs-lookup"><span data-stu-id="79549-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="79549-115">撤銷您的使用者存取系統管理員權限，直到再次需要這些權限。</span><span class="sxs-lookup"><span data-stu-id="79549-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="79549-116">如何復原 elevateAccess 動作</span><span class="sxs-lookup"><span data-stu-id="79549-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="79549-117">當您呼叫 elevateAccess 時，您建立自己的角色指派，因此您需要刪除作業才能撤銷這些權限。</span><span class="sxs-lookup"><span data-stu-id="79549-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="79549-118">呼叫 [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get)，其中 roleName = 使用者存取系統管理員，以判斷使用者存取系統管理員角色的 GUID 名稱。</span><span class="sxs-lookup"><span data-stu-id="79549-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="79549-119">回應應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="79549-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    <span data-ttu-id="79549-120">從 name 參數儲存 GUID，在此案例中為 **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**。</span><span class="sxs-lookup"><span data-stu-id="79549-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="79549-121">呼叫 [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get)，其中 principalId = 您自己的 ObjectId。</span><span class="sxs-lookup"><span data-stu-id="79549-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="79549-122">這樣會列出您租用戶中的所有指派。</span><span class="sxs-lookup"><span data-stu-id="79549-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="79549-123">尋找範圍是 "/" 的位置，且 RoleDefinitionId 以您在步驟 1 中所找到的角色名稱 GUID 結尾。</span><span class="sxs-lookup"><span data-stu-id="79549-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="79549-124">角色指派看起來應該像這樣︰</span><span class="sxs-lookup"><span data-stu-id="79549-124">The role assignment should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    <span data-ttu-id="79549-125">同樣地，從 name 參數儲存 GUID，在此案例中為 **e7dd75bc-06f6-4e71-9014-ee96a929d099**。</span><span class="sxs-lookup"><span data-stu-id="79549-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="79549-126">最後，呼叫 [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById)，其中 roleAssignmentId = 您在步驟 2 中找到的名稱 GUID。</span><span class="sxs-lookup"><span data-stu-id="79549-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79549-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="79549-127">Next steps</span></span>

- <span data-ttu-id="79549-128">深入了解[使用 REST 管理角色型存取控制](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="79549-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="79549-129">在 Azure 入口網站中[管理存取權指派](role-based-access-control-manage-assignments.md)</span><span class="sxs-lookup"><span data-stu-id="79549-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
