---
title: "與其他的 Azure AD aaaRole 型存取控制 |Microsoft 文件"
description: "使用 hello REST API 管理角色型存取控制"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>管理角色型存取控制以 hello REST API
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

角色型存取控制 (RBAC) 在 hello Azure 入口網站和 Azure 資源管理員 API，可協助您管理存取 tooyour 訂用帳戶和細微的層級的資源。 利用此功能，您可以藉由指定在特定範圍的某些角色 toothem 授與存取 Active Directory 使用者、 群組或服務主體。

## <a name="list-all-role-assignments"></a>列出所有角色指派
列出所有的 hello 角色指派，在指定的 hello 範圍及 subscopes。

toolist 角色指派，您必須能夠存取太`Microsoft.Authorization/roleAssignments/read`hello 範圍的作業。 所有的 hello 內建的角色會授與存取 toothis 作業。 如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

### <a name="request"></a>要求
使用 hello**取得**方法具有下列 URI 的 hello:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

內 hello URI，請遵循替代 toocustomize hello 您的要求：

1. 取代*{範圍}*與 hello 想 toolist hello 角色指派的範圍。 hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：

   * 訂用帳戶：/subscriptions/{subscription-id}  
   * 資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 將 *{api-version}* 取代為 2015-07-01。
3. 取代*{filter}* hello 條件，您會希望 tooapply toofilter hello 角色指派清單：

   * 清單只 hello 的角色指派指定範圍內，不包括在 subscopes hello 角色指派：`atScope()`    
   * 僅列出特定使用者、群組或應用程式的角色指派： `principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * 僅列出特定使用者的角色指派，包括從群組繼承的角色指派 | `assignedTo('{objectId of user}')`

### <a name="response"></a>Response
狀態碼：200

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a>取得角色指派的相關資訊
取得 hello 角色指派的識別項所指定的單一角色指派的相關資訊。

tooget 資訊有關角色指派，您必須能夠存取太`Microsoft.Authorization/roleAssignments/read`作業。 所有的 hello 內建的角色會授與存取 toothis 作業。 如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

### <a name="request"></a>要求
使用 hello**取得**方法具有下列 URI 的 hello:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

內 hello URI，請遵循替代 toocustomize hello 您的要求：

1. 取代*{範圍}*與 hello 想 toolist hello 角色指派的範圍。 hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：

   * 訂用帳戶：/subscriptions/{subscription-id}  
   * 資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 取代*{角色-指派-識別碼}* hello hello 角色指派的 GUID 識別碼。
3. 將 *{api-version}* 取代為 2015-07-01。

### <a name="response"></a>Response
狀態碼：200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a>建立角色指派
建立角色指派在 hello hello 指定主體授與的 hello 指定的角色，請指定範圍。

toocreate 角色指派，您必須能夠存取太`Microsoft.Authorization/roleAssignments/write`作業。 Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。 如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

### <a name="request"></a>要求
使用 hello**放**方法具有下列 URI 的 hello:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

內 hello URI，請遵循替代 toocustomize hello 您的要求：

1. 取代*{範圍}*與 hello 範圍，此時您希望 toocreate hello 角色指派。 當您在父範圍中建立角色指派時，所有的子領域會繼承 hello 相同的角色指派。 hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：

   * 訂用帳戶：/subscriptions/{subscription-id}  
   * 資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1   
   * 資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 取代*{角色-指派-識別碼}*以新的 GUID，而成為 hello hello 新角色指派的 GUID 識別碼。
3. 將 *{api-version}* 取代為 2015-07-01。

Hello 要求主體中，提供 hello 遵循格式中的 hello 值：

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| 元素名稱 | 必要 | 類型 | 說明 |
| --- | --- | --- | --- |
| roleDefinitionId |是 |String |hello hello 角色識別碼。 hello hello 識別項的格式如下：`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| principalId |是 |String |hello Azure AD 主體 （使用者、 群組或服務主體） 的 objectId toowhich hello 角色指派。 |

### <a name="response"></a>Response
狀態碼：201

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a>刪除角色指派
刪除角色指派 hello 在指定範圍。

toodelete 角色指派，您必須擁有存取 toohello`Microsoft.Authorization/roleAssignments/delete`作業。 Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。 如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

### <a name="request"></a>要求
使用 hello**刪除**方法具有下列 URI 的 hello:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

內 hello URI，請遵循替代 toocustomize hello 您的要求：

1. 取代*{範圍}*與 hello 範圍，此時您希望 toocreate hello 角色指派。 hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：

   * 訂用帳戶：/subscriptions/{subscription-id}  
   * 資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 取代*{角色-指派-識別碼}* hello 角色指派 id 的 GUID。
3. 將 *{api-version}* 取代為 2015-07-01。

### <a name="response"></a>Response
狀態碼：200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a>列出所有角色
列出所有 hello 角色可供使用時指定的 hello 的指派範圍。

toolist 角色必須具有存取太`Microsoft.Authorization/roleDefinitions/read`hello 範圍的作業。 所有的 hello 內建的角色會授與存取 toothis 作業。 如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

### <a name="request"></a>要求
使用 hello**取得**方法具有下列 URI 的 hello:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

內 hello URI，請遵循替代 toocustomize hello 您的要求：

1. 取代*{範圍}*與 hello 想 toolist hello 角色的範圍。 hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：

   * 訂用帳戶：/subscriptions/{subscription-id}  
   * 資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 將 *{api-version}* 取代為 2015-07-01。
3. 取代*{filter}* hello 條件，您希望角色 tooapply toofilter hello 清單：

   * 清單角色在 hello 分派可用的指定範圍和其子範圍的任何：`atScopeAndBelow()`
   * 使用確切的顯示名稱來搜尋角色： `roleName%20eq%20'{role-display-name}'`。 使用 hello URL 編碼形式的 hello 角色 hello 確切的顯示名稱。 例如， `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>Response
狀態碼：200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a>取得角色的相關資訊
取得 hello 角色定義識別項所指定的單一角色的相關資訊。 tooget 使用它的顯示名稱的單一角色的相關的資訊，請參閱[列出所有角色](role-based-access-control-manage-access-rest.md#list-all-roles)。

tooget 有關角色的資訊，您必須能夠存取太`Microsoft.Authorization/roleDefinitions/read`作業。 所有的 hello 內建的角色會授與存取 toothis 作業。 如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

### <a name="request"></a>要求
使用 hello**取得**方法具有下列 URI 的 hello:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

內 hello URI，請遵循替代 toocustomize hello 您的要求：

1. 取代*{範圍}*與 hello 想 toolist hello 角色指派的範圍。 hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：

   * 訂用帳戶：/subscriptions/{subscription-id}  
   * 資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 取代*{角色-定義-識別碼}* hello 角色定義的 hello GUID 識別碼。
3. 將 *{api-version}* 取代為 2015-07-01。

### <a name="response"></a>Response
狀態碼：200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a>建立自訂角色
建立自訂角色。

toocreate 自訂安全性角色，您必須能夠存取太`Microsoft.Authorization/roleDefinitions/write`作業上所有的 hello `AssignableScopes`。 Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。 如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

### <a name="request"></a>要求
使用 hello**放**方法具有下列 URI 的 hello:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

內 hello URI，請遵循替代 toocustomize hello 您的要求：

1. 取代*{範圍}* hello 與第一個*AssignableScope*的 hello 自訂角色。 hello 遵循範例顯示如何 toospecify hello 不同層級的範圍。

   * 訂用帳戶：/subscriptions/{subscription-id}  
   * 資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 取代*{角色-定義-識別碼}*以新的 GUID，而成為新的自訂角色 hello hello GUID 識別碼。
3. 將 *{api-version}* 取代為 2015-07-01。

Hello 要求主體中，提供 hello 遵循格式中的 hello 值：

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| 元素名稱 | 必要 | 類型 | 說明 |
| --- | --- | --- | --- |
| 名稱 |是 |String |Hello 自訂角色的 GUID 識別碼。 |
| properties.roleName |是 |String |Hello 自訂角色的顯示名稱。 大小上限為 128 個字元。 |
| properties.description |否 |String |Hello 自訂角色的描述。 大小上限為 1024 個字元。 |
| properties.type |是 |String |設定得 「 CustomRole。 」 |
| properties.permissions.actions |yes |String[] |字串 hello 自訂角色所授與的指定 hello 作業的動作陣列。 |
| properties.permissions.notActions |否 |String[] |指定 hello 作業 tooexclude hello 自訂角色所授與的 hello 作業的動作字串的陣列。 |
| properties.assignableScopes |是 |String[] |陣列的範圍中的 hello 可以使用自訂角色。 |

### <a name="response"></a>Response
狀態碼：201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a>更新自訂角色
修改自訂角色。

toomodify 自訂安全性角色，您必須能夠存取太`Microsoft.Authorization/roleDefinitions/write`作業上所有的 hello `AssignableScopes`。 Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。 如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

### <a name="request"></a>要求
使用 hello**放**方法具有下列 URI 的 hello:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

內 hello URI，請遵循替代 toocustomize hello 您的要求：

1. 取代*{範圍}* hello 與第一個*AssignableScope*的 hello 自訂角色。 hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：

   * 訂用帳戶：/subscriptions/{subscription-id}  
   * 資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 取代*{角色-定義-識別碼}* hello 自訂角色的 hello GUID 識別碼。
3. 將 *{api-version}* 取代為 2015-07-01。

Hello 要求主體中，提供 hello 遵循格式中的 hello 值：

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| 元素名稱 | 必要 | 類型 | 說明 |
| --- | --- | --- | --- |
| 名稱 |是 |String |Hello 自訂角色的 GUID 識別碼。 |
| properties.roleName |是 |String |Hello 更新自訂角色的顯示名稱。 |
| properties.description |否 |String |Hello 的描述更新自訂角色。 |
| properties.type |是 |String |設定得 「 CustomRole。 」 |
| properties.permissions.actions |yes |String[] |指定 hello 作業 toowhich hello 的動作字串的陣列會更新自訂角色授與的存取。 |
| properties.permissions.notActions |否 |String[] |從 hello 作業的 hello 更新自訂角色授與的指定 hello 作業 tooexclude 之字串的動作陣列。 |
| properties.assignableScopes |是 |String[] |陣列的範圍中的 hello 更新自訂角色可用。 |

### <a name="response"></a>Response
狀態碼：201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a>刪除自訂角色
刪除自訂角色。

toodelete 自訂安全性角色，您必須能夠存取太`Microsoft.Authorization/roleDefinitions/delete`作業上所有的 hello `AssignableScopes`。 Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。 如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。

### <a name="request"></a>要求
使用 hello**刪除**方法具有下列 URI 的 hello:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

內 hello URI，請遵循替代 toocustomize hello 您的要求：

1. 取代*{範圍}*與 hello 想 toodelete hello 角色定義的範圍。 hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：

   * 訂用帳戶：/subscriptions/{subscription-id}  
   * 資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * 資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. 取代*{角色-定義-識別碼}* hello GUID 角色定義識別碼為 hello 自訂角色。
3. 將 *{api-version}* 取代為 2015-07-01。

### <a name="response"></a>Response
狀態碼：200

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a>後續步驟

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
