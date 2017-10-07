---
title: "角色型存取控制 (RBAC) 使用 Azure PowerShell aaaManage |Microsoft 文件"
description: "如何 toomanage RBAC 與 Azure PowerShell，包括列出角色、 指派角色，以及刪除角色指派。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a>使用 Azure PowerShell 管理角色型存取控制
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

您可以在 hello Azure 入口網站和 Azure 資源管理 API toomanage 存取 tooyour 訂用帳戶在細微的層級中使用角色型存取控制 (RBAC)。 利用此功能，您可以藉由指定在特定範圍的某些角色 toothem 授與存取 Active Directory 使用者、 群組或服務主體。

您可以使用 PowerShell toomanage RBAC 之前，您需要下列必要條件 hello:

* Azure PowerShell 0.8.8 或更新版本。 tooinstall hello 最新版本並關聯它與您 Azure 訂用帳戶，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
* Azure Resource Manager Cmdlet。 安裝 hello [Azure 資源管理員 cmdlet](/powershell/azure/overview)在 PowerShell 中。

## <a name="list-roles"></a>列出角色
### <a name="list-all-available-roles"></a>列出所有可用的角色
toolist RBAC 角色可供指派和 tooinspect hello 作業 toowhich 他們授與存取權，會使用`Get-AzureRmRoleDefinition`。

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>列出角色的動作
toolist hello 動作特定的角色，會使用`Get-AzureRmRoleDefinition <role name>`。

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - 特定角色的 Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>查看誰具有存取權
toolist RBAC 存取指派，使用`Get-AzureRmRoleAssignment`。

### <a name="list-role-assignments-at-a-specific-scope"></a>列出特定範圍的角色指派
您可以看到所有 hello 存取指派指定的訂用帳戶、 資源群組或資源。 比方說，toosee hello 所有都 hello 作用中的指派為資源群組，請使用`Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`。

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 資源群組的 Get-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>清單的角色指派 tooa 使用者
使用者和指派給 toohello toowhich hello 使用者所屬的群組的 hello 角色指定所有的 hello 角色指派 tooa toolist 使用`Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`。

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 使用者的 Get-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>列出傳統服務管理員和共同管理員角色指派
toolist 存取指派 hello 傳統訂用帳戶管理員和 coadministrators，使用：

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>授與存取權
### <a name="search-for-object-ids"></a>搜尋物件識別碼
tooassign 角色，您需要 tooidentify hello 物件 （使用者、 群組或應用程式） 和 hello 範圍。

如果您不知道 hello 訂用帳戶 ID，您可以找到它在 hello**訂閱**hello Azure 入口網站上的刀鋒視窗。 如何 tooquery hello 訂用帳戶 id，請參閱的 toolearn [Get-azuresubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) MSDN 上。

使用 Azure AD 群組，tooget hello 物件識別碼：

    Get-AzureRmADGroup -SearchString <group name in quotes>

tooget hello 物件識別碼的 Azure AD 服務主體或應用程式，使用：

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>指派在 hello 訂用帳戶範圍的角色 tooan 應用程式
toogrant hello 訂用帳戶範圍，使用的存取 tooan 應用程式：

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>指派給角色 tooa 使用者在 hello 資源群組領域
toogrant 存取 tooa 使用者在 hello 資源群組範圍，使用：

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>指定角色 tooa 群組在 hello 資源範圍
toogrant 存取 tooa 群組在 hello 資源範圍，使用：

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>移除存取
使用者、 群組和應用程式，使用 tooremove 存取：

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>建立自訂角色
toocreate 自訂安全性角色，使用 hello```New-AzureRmRoleDefinition```命令。 有兩種方法來建構使用 PSRoleDefinitionObject 或 JSON 範本的 hello 角色。 

## <a name="get-actions-for-a-resource-provider"></a>取得資源提供者的動作
當您要從頭建立自訂角色時，就很重要的 tooknow 所有 hello 可能從 hello 資源提供者的作業。
使用 hello```Get-AzureRMProviderOperation```命令 tooget 這項資訊。
例如，如果您想 toocheck 所有 hello 可用操作的虛擬機器會都使用此命令：

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>使用 PSRoleDefinitionObject 建立角色
當您使用 PowerShell toocreate 自訂安全性角色時，您可以從頭開始，或使用其中一種 hello[內建角色](role-based-access-built-in-roles.md)做為起點。 本節中的 hello 範例開頭為內建的角色，然後使用所需權限進行自訂。 編輯 hello 屬性 tooadd hello*動作*， *notActions*，或*範圍*您要的然後將 hello 變更儲存為新的角色。

hello 下列範例會啟動以 hello*虛擬機器參與者*角色，並使用該 toocreate 自訂安全性角色會稱為*虛擬機器運算子*。 hello 新角色會授與存取 tooall 讀取作業的*Microsoft.Compute*， *Microsoft.Storage*，和*Microsoft.Network*資源提供者及授與存取權toostart，重新啟動，而監視虛擬機器。 hello 自訂角色可以使用兩個訂用帳戶中。

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a>使用 JSON 範本建立角色
JSON 範本可以作為 hello 自訂角色的 hello 來源定義。 hello 下列範例會建立自訂安全性角色可讓讀取權限 toostorage 和計算資源、 存取 toosupport，並將該角色 tootwo 訂用帳戶。 建立新的檔案`C:\CustomRoles\customrole1.json`以下列範例中的 hello。 hello Id 應該設定太`null`初始角色建立為新的識別碼時自動產生。 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
tooadd hello 角色 toohello 訂用帳戶，執行下列 PowerShell 命令的 hello:
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>修改自訂角色
類似 toocreating 自訂安全性角色，您可以修改現有的自訂角色使用 hello PSRoleDefinitionObject 或 JSON 範本。

### <a name="modify-role-with-psroledefinitionobject"></a>使用 PSRoleDefinitionObject 修改角色
toomodify 自訂安全性角色，首先，使用 hello`Get-AzureRmRoleDefinition`命令 tooretrieve hello 角色定義。 第二，變更所需的 hello toohello 角色定義。 最後，使用 hello`Set-AzureRmRoleDefinition`命令 toosave hello 修改角色定義。

hello 下列範例會將 hello`Microsoft.Insights/diagnosticSettings/*`作業 toohello*虛擬機器運算子*自訂角色。

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

hello 下列範例會將 Azure 訂用帳戶 toohello 可指派的範圍的 hello*虛擬機器運算子*自訂角色。

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>使用 JSON 範本修改角色
使用 hello 先前的 JSON 範本，可以輕鬆地修改現有的自訂角色 tooadd 或移除動作。 更新 hello JSON 範本，並加入 hello 網路讀取的動作 hello 下列範例所示。 hello 範本中所列的 hello 定義不是累積套用的 tooan 現有的定義，這表示該 hello 角色出現完全依照您在 hello 範本中指定。 您也需要識別碼為 hello 角色 hello tooupdate hello 識別碼 欄位。 如果您不確定此值為何，您可以使用 hello `Get-AzureRmRoleDefinition` cmdlet tooget 這項資訊。

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

tooupdate hello 現有的角色，執行下列 PowerShell 命令的 hello:
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>刪除自訂角色
toodelete 自訂安全性角色，使用 hello`Remove-AzureRmRoleDefinition`命令。

hello 下列範例會移除 hello*虛擬機器運算子*自訂角色。

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>列出自訂角色
所提供的範圍，指派 toolist hello 角色使用 hello`Get-AzureRmRoleDefinition`命令。

下列範例中的 hello 列出可供指派 hello 選取訂用帳戶中的所有角色。

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

在下列範例的 hello，hello*虛擬機器運算子*hello 中的自訂角色沒有*Production4*訂用帳戶因為該訂用帳戶不在 hello **AssignableScopes**的 hello 角色。

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>另請參閱
* [搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

