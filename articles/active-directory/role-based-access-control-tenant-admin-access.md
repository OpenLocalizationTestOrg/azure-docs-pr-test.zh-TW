---
title: "aaaTenant 系統管理員提高權限的 Azure AD 存取權 |Microsoft 文件"
description: "本主題描述 hello 內建的角色型存取控制 (RBAC) 的角色。"
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
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="d3987-103">使用角色型存取控制以租用戶系統管理員提高存取權限</span><span class="sxs-lookup"><span data-stu-id="d3987-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="d3987-104">角色型存取控制可協助租用戶系統管理員取得存取權限暫時提升，以便他們可以比平常授與更高的權限。</span><span class="sxs-lookup"><span data-stu-id="d3987-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="d3987-105">租用戶系統管理員可以將自己提高 toohello 使用者存取系統管理員角色在需要時。</span><span class="sxs-lookup"><span data-stu-id="d3987-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="d3987-106">該角色可讓 hello 自己或其他租用戶系統管理員權限 toogrant hello 上的角色"/"的範圍。</span><span class="sxs-lookup"><span data-stu-id="d3987-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="d3987-107">這項功能非常重要的因為它可讓 hello 租用戶系統管理員 toosee 所有 hello 組織中的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d3987-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="d3987-108">它也可自動化應用程式 （例如開發票和稽核） tooaccess hello 的所有訂閱，而且提供 hello 狀態 hello 帳單或資產管理組織的精確檢視。</span><span class="sxs-lookup"><span data-stu-id="d3987-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="d3987-109">Toouse elevateAccess toogive 租用戶的存取方式</span><span class="sxs-lookup"><span data-stu-id="d3987-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="d3987-110">hello 基本程序運作方式與 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d3987-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="d3987-111">使用 REST 呼叫*elevateAccess*，哪些授與您 hello 使用者存取系統管理員角色，在"/"的範圍。</span><span class="sxs-lookup"><span data-stu-id="d3987-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="d3987-112">建立[角色指派](/rest/api/authorization/roleassignments)tooassign 在任何範圍的任何角色。</span><span class="sxs-lookup"><span data-stu-id="d3987-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="d3987-113">下列範例中的 hello 顯示 hello 屬性指派 hello 讀取者角色，在"/"的範圍：</span><span class="sxs-lookup"><span data-stu-id="d3987-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="d3987-114">在使用者存取的系統管理員時，您也可以在 "/" 的範圍刪除角色指派。</span><span class="sxs-lookup"><span data-stu-id="d3987-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="d3987-115">撤銷您的使用者存取系統管理員權限，直到再次需要這些權限。</span><span class="sxs-lookup"><span data-stu-id="d3987-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="d3987-116">如何 tooundo hello elevateAccess 動作</span><span class="sxs-lookup"><span data-stu-id="d3987-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="d3987-117">當您呼叫*elevateAccess*為自己建立角色指派，因此 toorevoke 那些權限您需要 toodelete hello 分派。</span><span class="sxs-lookup"><span data-stu-id="d3987-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="d3987-118">呼叫[GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get)其中 roleName = 使用者存取系統管理員 toodetermine hello 名稱 hello 使用者存取系統管理員角色的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d3987-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="d3987-119">hello 回應看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="d3987-119">hello response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
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

    <span data-ttu-id="d3987-120">儲存從 hello hello GUID*名稱*參數，在此情況下**18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**。</span><span class="sxs-lookup"><span data-stu-id="d3987-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="d3987-121">呼叫 [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get)，其中 principalId = 您自己的 ObjectId。</span><span class="sxs-lookup"><span data-stu-id="d3987-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="d3987-122">這樣就會列出所有您指派 hello 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="d3987-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="d3987-123">尋找一個 hello hello 範圍所在"/"，並與 hello 角色 hello RoleDefinitionId 結束命名您在步驟 1 中所找到的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d3987-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="d3987-124">hello 角色指派看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="d3987-124">hello role assignment should look like this:</span></span>

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

    <span data-ttu-id="d3987-125">同樣地，從 hello 儲存 hello GUID*名稱*參數，在此情況下**e7dd75bc-06f6-4e71-9014-ee96a929d099**。</span><span class="sxs-lookup"><span data-stu-id="d3987-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="d3987-126">最後，呼叫[刪除 roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById)其中 roleAssignmentId = hello 名稱您在步驟 2 中找到的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d3987-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3987-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3987-127">Next steps</span></span>

- <span data-ttu-id="d3987-128">深入了解[使用 REST 管理角色型存取控制](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="d3987-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="d3987-129">[管理存取權指派](role-based-access-control-manage-assignments.md)hello Azure 入口網站中</span><span class="sxs-lookup"><span data-stu-id="d3987-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
