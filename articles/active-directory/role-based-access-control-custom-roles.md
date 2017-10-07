---
title: "aaaCreate Azure rbac 進行的自訂角色 |Microsoft 文件"
description: "深入了解如何 toodefine 自訂角色所有存取控制與您 Azure 訂用帳戶中的更精確識別管理。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>建立 Azure 角色型存取控制的自訂角色
如果 hello 內建角色都不符合您的特定存取需求，建立自訂安全性角色中所有存取控制 (RBAC)。 您可以使用建立自訂角色[Azure PowerShell](role-based-access-control-manage-access-powershell.md)， [Azure 命令列介面](role-based-access-control-manage-access-azure-cli.md)(CLI)，和 hello [REST API](role-based-access-control-manage-access-rest.md)。 如同內建的角色，您可以指派自訂角色 toousers、 群組和應用程式在訂用帳戶、 資源群組和資源的範圍。 自訂角色會儲存在 Azure AD 租用戶中，而且可在訂用帳戶之間共用。

每個租用戶可以建立註冊 too2000 自訂角色。 

hello 下列範例示範自訂安全性角色的監視，並重新啟動虛擬機器：

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a>動作
hello**動作**的自訂安全性角色的屬性會指定 hello Azure 操作 toowhich hello 角色會授與的存取。 它是識別 Azure 資源提供者的安全性實體作業的作業字串集合。 操作字串 hello 的遵照格式`Microsoft.<ProviderName>/<ChildResourceType>/<action>`。 作業包含萬用字元的字串 (\*) 授與存取權的比對 hello 作業字串 tooall 作業。 例如：

* `*/read`授與存取 tooread 作業的所有 Azure 資源提供者的所有資源類型。
* `Microsoft.Compute/*`授與存取 tooall hello Microsoft.Compute 資源提供者中的所有資源類型的作業。
* `Microsoft.Network/*/read`授與存取 tooread hello Microsoft.Network 資源提供者中所有的資源類型，Azure 的作業。
* `Microsoft.Compute/virtualMachines/*`授與存取虛擬機器和及其子系的資源類型 tooall 作業。
* `Microsoft.Web/sites/restart/Action`授與存取 toorestart 網站。

使用`Get-AzureRmProviderOperation`（以 PowerShell) 或`azure provider operations show`（在 Azure CLI) toolist 作業的 Azure 資源提供者。 您也可以使用這些命令 tooverify 作業字串有效和 tooexpand 萬用字元操作字串。

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell 螢幕擷取畫面 - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Azure CLI 螢幕擷取畫面 - azure 提供者作業顯示 "Microsoft.Compute/virtualMachines/\*/action" ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
使用 hello **NotActions**如果 hello 一組作業，您會希望 tooallow 更輕鬆地定義限制的作業中排除的屬性。 hello 自訂安全性角色授與存取權的計算方式是減去 hello **NotActions**作業 hello**動作**作業。

> [!NOTE]
> 如果指派使用者角色中的作業中排除**NotActions**，並指派第二個角色，授與存取相同的作業，hello 使用者是的 toohello 允許 tooperform 該作業。 **NotActions**不是拒絕規則 – 它時，只是方便 toocreate 一組允許的作業需要 toobe 排除特定的作業。
>
>

## <a name="assignablescopes"></a>AssignableScopes
hello **AssignableScopes** hello 自訂角色屬性會指定 hello 範圍 （訂用帳戶、 資源群組或資源） 中的 hello 自訂的角色是指派的可用。 您可以在 hello 自訂角色指派的可用只有 hello 訂閱或資源群組需要它，而不混亂的情形使用者體驗 hello 其餘 hello 訂用帳戶或資源群組。

有效的可指派範圍範例包括：

* "/ 訂用帳戶/c276fc76-9cd4-44c9-99a7-4fd71546436e"，"/ 訂用帳戶/e91d47c4-76f3-4271-a796-21b4ecfe3624"-讓 hello 角色可供指派兩個訂用帳戶中。
* "/ 訂用帳戶/c276fc76-9cd4-44c9-99a7-4fd71546436e"-讓 hello 角色可供指派單一訂用帳戶中。
* "/ 訂用帳戶/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/網路 」-讓 hello 分派只在 hello 網路資源群組中可用的角色。

> [!NOTE]
> 您至少必須使用一個訂用帳戶、資源群組或資源識別碼。
>
>

## <a name="custom-roles-access-control"></a>自訂角色存取控制
hello **AssignableScopes** hello 自訂角色的內容也會控制誰可以檢視、 修改和刪除 hello 角色。

* 誰可以建立自訂角色？
    訂用帳戶、資源群組和資源的擁有者 (和使用者存取管理員) 可以建立自訂角色以在這些範圍中使用。
    hello 使用者建立 hello 角色需要 toobe 無法 tooperform`Microsoft.Authorization/roleDefinition/write`作業上所有的 hello **AssignableScopes**的 hello 角色。
* 誰可以修改自訂角色？
    訂用帳戶、資源群組和資源的擁有者 (和使用者存取管理員) 可以在這些範圍中修改自訂角色。 使用者需要 toobe 無法 tooperform hello`Microsoft.Authorization/roleDefinition/write`作業上所有的 hello **AssignableScopes**的自訂安全性角色。
* 誰可以檢視自訂角色？
    Azure RBAC 中的所有內建角色允許檢視可用於指派的角色。 使用者可以執行 hello`Microsoft.Authorization/roleDefinition/read`在範圍內的作業可以檢視 hello RBAC 角色可供在該範圍的指派。

## <a name="see-also"></a>另請參閱
* [Role Based Access Control](role-based-access-control-configure.md)： 開始使用 RBAC hello Azure 入口網站中。
* 了解 toomanage 與的存取方式：
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
  * [REST API](role-based-access-control-manage-access-rest.md)
* [內建角色](role-based-access-built-in-roles.md)： 取得標準中 RBAC 的 hello 角色的相關詳細資料。
