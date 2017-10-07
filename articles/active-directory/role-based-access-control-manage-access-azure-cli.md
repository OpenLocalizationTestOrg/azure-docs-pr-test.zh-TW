---
title: "角色型存取控制 (RBAC) 與 Azure CLI aaaManage |Microsoft 文件"
description: "了解如何 toomanage 角色型存取控制 (RBAC) 以 hello Azure 命令列介面清單角色和角色的動作和指派 toohello 訂用帳戶和應用程式範圍的角色。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a>管理角色型存取控制以 hello Azure 命令列介面
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)


您可以使用角色型存取控制 (RBAC) hello Azure 入口網站和 Azure 資源管理員 API toomanage 存取 tooyour 訂用帳戶和細微的層級的資源。 利用此功能，您可以藉由指定在特定範圍的某些角色 toothem 授與存取 Active Directory 使用者、 群組或服務主體。

您可以使用 hello Azure 命令列介面 (CLI) toomanage RBAC 之前，您必須擁有下列必要條件 hello:

* Azure CLI 0.8.8 版或更新版本。 tooinstall hello 最新版本並關聯它與您 Azure 訂用帳戶，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。
* Azure CLI 中的 Azure Resource Manager。 跳過[hello 資源管理員的使用 hello Azure CLI](../xplat-cli-azure-resource-manager.md)如需詳細資訊。

## <a name="list-roles"></a>列出角色
### <a name="list-all-available-roles"></a>列出所有可用的角色
toolist 所有可用的角色，使用：

        azure role list

hello 下列範例顯示 hello 清單*所有可用的角色*。

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![RBAC Azure 命令列 - azure 角色清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a>列出角色的動作
toolist hello 動作的角色，使用：

    azure role show "<role name>"

hello 下列範例顯示 hello 動作的 hello*參與者*和*虛擬機器參與者*角色。

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![RBAC Azure 命令列 - azure 角色顯示 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a>列出存取權
### <a name="list-role-assignments-effective-on-a-resource-group"></a>列出資源群組上有效的角色指派
存在於資源群組中，使用 toolist hello 角色指派：

    azure role assignment list --resource-group <resource group name>

hello 下列範例顯示 hello 角色指派中 hello *pharma-銷售額-projecforcast*群組。

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure 命令列 - 依群組顯示的 azure 角色指派清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a>列出使用者的角色指派
toolist hello 角色指派特定的使用者，以及指派給 tooa 使用者群組的 hello 分派使用：

    azure role assignment list --signInName <user email>

您也可以看到繼承自群組，藉由修改 hello 命令的角色指派：

    azure role assignment list --expandPrincipalGroups --signInName <user email>

hello 下列範例顯示 hello 角色指派授與 toohello  *sameert@aaddemo.com* 使用者。 這包括直接 toohello 使用者指派的角色和角色繼承自群組。

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure 命令列 - 依使用者顯示的 azure 角色指派清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a>授與存取權
toogrant 存取您識別您想 tooassign hello 角色之後，使用：

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a>指派角色 toogroup hello 訂用帳戶範圍
tooassign 角色 tooa 群組在 hello 訂用帳戶範圍，使用：

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

hello 下列範例會將指派 hello*讀取器*角色太*Christine Koch 小組*在 hello*訂用帳戶*範圍。

![RBAC Azure 命令列 - 群組所建立的 azure 角色指派 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>指派在 hello 訂用帳戶範圍的角色 tooan 應用程式
tooassign hello 訂用帳戶範圍，使用角色 tooan 應用程式：

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

hello 下列範例會授與 hello*參與者*角色 tooan *Azure AD* hello 上的應用程式選取訂用帳戶。

 ![RBAC Azure 命令列 - 應用程式所建立的 azure 角色指派](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>指派給角色 tooa 使用者在 hello 資源群組領域
tooassign 角色 tooa 使用者在 hello 資源群組範圍，使用：

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

hello 下列範例會授與 hello*虛擬機器參與者*角色太*samert@aaddemo.com* 使用者在 hello *Pharma-銷售額-ProjectForcast*資源群組範圍。

![RBAC Azure 命令列 - 使用者所建立的 azure 角色指派 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>指定角色 tooa 群組在 hello 資源範圍
tooassign 角色 tooa 群組在 hello 資源範圍，使用：

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

hello 下列範例會授與 hello*虛擬機器參與者*角色 tooan *Azure AD*群組*子網路*。

![RBAC Azure 命令列 - 群組所建立的 azure 角色指派 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a>移除存取
tooremove 角色指派，請使用：

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

hello 下列範例會移除 hello*虛擬機器參與者*角色指派從 hello  *sammert@aaddemo.com*  hello 上的使用者*Pharma-銷售額-ProjectForcast*資源群組。
hello 範例會從 hello 訂用帳戶上的群組，然後移除 hello 角色指派。

![RBAC Azure 命令列 - azure 角色指派刪除 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a>建立自訂角色
toocreate 自訂安全性角色，使用：

    azure role create --inputfile <file path>

hello 下列範例會建立自訂安全性角色呼叫*虛擬機器運算子*。 此自訂角色會授與存取 tooall 讀取作業的*Microsoft.Compute*， *Microsoft.Storage*，和*Microsoft.Network*資源提供者及授與存取權toostart，重新啟動，而監視虛擬機器。 這個自訂角色可用於兩個訂用帳戶中。 這個範例使用 JSON 檔案做為輸入。

![JSON - 自訂角色定義 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure 命令列 - azure 角色建立 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a>修改自訂角色
toomodify 自訂安全性角色，第一次使用 hello`azure role show`命令 tooretrieve 角色定義。 第二，請 hello 所要的變更 toohello 角色定義檔。 最後，使用`azure role set`toosave hello 修改角色定義。

    azure role set --inputfile <file path>

hello 下列範例會將 hello *Microsoft.Insights/diagnosticSettings/*作業 toohello**動作**，和 Azure 訂用帳戶 toohello **AssignableScopes**hello 虛擬機器操作員自訂角色。

![JSON - 修改自訂角色定義 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![RBAC Azure 命令列 - azure 角色設定 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a>刪除自訂角色
toodelete 自訂安全性角色，第一次使用 hello`azure role show`命令 toodetermine hello**識別碼**的 hello 角色。 然後，使用 hello`azure role delete`命令 toodelete hello 角色，藉由指定 hello**識別碼**。

hello 下列範例會移除 hello*虛擬機器運算子*自訂角色。

![RBAC Azure 命令列 - azure 角色刪除 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a>列出自訂角色
所提供的範圍，指派 toolist hello 角色使用 hello`azure role list`命令。

hello，下列命令會列出可供指派 hello 選取訂用帳戶中的所有角色。

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![RBAC Azure 命令列 - azure 角色清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

在下列範例的 hello，hello*虛擬機器運算子*hello 中的自訂角色沒有*Production4*訂用帳戶因為該訂用帳戶不在 hello **AssignableScopes**的 hello 角色。

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![RBAC Azure 命令列 - 自訂角色的 azure 角色清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a>後續步驟
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

