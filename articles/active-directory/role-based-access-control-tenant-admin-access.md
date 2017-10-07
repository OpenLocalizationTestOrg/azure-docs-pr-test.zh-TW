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
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>使用角色型存取控制以租用戶系統管理員提高存取權限

角色型存取控制可協助租用戶系統管理員取得存取權限暫時提升，以便他們可以比平常授與更高的權限。 租用戶系統管理員可以將自己提高 toohello 使用者存取系統管理員角色在需要時。 該角色可讓 hello 自己或其他租用戶系統管理員權限 toogrant hello 上的角色"/"的範圍。

這項功能非常重要的因為它可讓 hello 租用戶系統管理員 toosee 所有 hello 組織中的訂用帳戶。 它也可自動化應用程式 （例如開發票和稽核） tooaccess hello 的所有訂閱，而且提供 hello 狀態 hello 帳單或資產管理組織的精確檢視。  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Toouse elevateAccess toogive 租用戶的存取方式

hello 基本程序運作方式與 hello 下列步驟：

1. 使用 REST 呼叫*elevateAccess*，哪些授與您 hello 使用者存取系統管理員角色，在"/"的範圍。

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. 建立[角色指派](/rest/api/authorization/roleassignments)tooassign 在任何範圍的任何角色。 下列範例中的 hello 顯示 hello 屬性指派 hello 讀取者角色，在"/"的範圍：

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

3. 在使用者存取的系統管理員時，您也可以在 "/" 的範圍刪除角色指派。

4. 撤銷您的使用者存取系統管理員權限，直到再次需要這些權限。


## <a name="how-tooundo-hello-elevateaccess-action"></a>如何 tooundo hello elevateAccess 動作

當您呼叫*elevateAccess*為自己建立角色指派，因此 toorevoke 那些權限您需要 toodelete hello 分派。

1.  呼叫[GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get)其中 roleName = 使用者存取系統管理員 toodetermine hello 名稱 hello 使用者存取系統管理員角色的 GUID。 hello 回應看起來應該像這樣：

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

    儲存從 hello hello GUID*名稱*參數，在此情況下**18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**。

2. 呼叫 [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get)，其中 principalId = 您自己的 ObjectId。 這樣就會列出所有您指派 hello 租用戶中。 尋找一個 hello hello 範圍所在"/"，並與 hello 角色 hello RoleDefinitionId 結束命名您在步驟 1 中所找到的 GUID。 hello 角色指派看起來應該像這樣：

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

    同樣地，從 hello 儲存 hello GUID*名稱*參數，在此情況下**e7dd75bc-06f6-4e71-9014-ee96a929d099**。

3. 最後，呼叫[刪除 roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById)其中 roleAssignmentId = hello 名稱您在步驟 2 中找到的 GUID。

## <a name="next-steps"></a>後續步驟

- 深入了解[使用 REST 管理角色型存取控制](role-based-access-control-manage-access-rest.md)

- [管理存取權指派](role-based-access-control-manage-assignments.md)hello Azure 入口網站中
