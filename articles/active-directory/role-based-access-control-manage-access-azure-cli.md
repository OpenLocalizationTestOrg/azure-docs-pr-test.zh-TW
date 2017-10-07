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
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="2e67a-103">管理角色型存取控制以 hello Azure 命令列介面</span><span class="sxs-lookup"><span data-stu-id="2e67a-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e67a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e67a-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="2e67a-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2e67a-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="2e67a-106">REST API</span><span class="sxs-lookup"><span data-stu-id="2e67a-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="2e67a-107">您可以使用角色型存取控制 (RBAC) hello Azure 入口網站和 Azure 資源管理員 API toomanage 存取 tooyour 訂用帳戶和細微的層級的資源。</span><span class="sxs-lookup"><span data-stu-id="2e67a-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="2e67a-108">利用此功能，您可以藉由指定在特定範圍的某些角色 toothem 授與存取 Active Directory 使用者、 群組或服務主體。</span><span class="sxs-lookup"><span data-stu-id="2e67a-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="2e67a-109">您可以使用 hello Azure 命令列介面 (CLI) toomanage RBAC 之前，您必須擁有下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="2e67a-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="2e67a-110">Azure CLI 0.8.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2e67a-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="2e67a-111">tooinstall hello 最新版本並關聯它與您 Azure 訂用帳戶，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="2e67a-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="2e67a-112">Azure CLI 中的 Azure Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="2e67a-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="2e67a-113">跳過[hello 資源管理員的使用 hello Azure CLI](../xplat-cli-azure-resource-manager.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2e67a-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="2e67a-114">列出角色</span><span class="sxs-lookup"><span data-stu-id="2e67a-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="2e67a-115">列出所有可用的角色</span><span class="sxs-lookup"><span data-stu-id="2e67a-115">List all available roles</span></span>
<span data-ttu-id="2e67a-116">toolist 所有可用的角色，使用：</span><span class="sxs-lookup"><span data-stu-id="2e67a-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="2e67a-117">hello 下列範例顯示 hello 清單*所有可用的角色*。</span><span class="sxs-lookup"><span data-stu-id="2e67a-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![RBAC Azure 命令列 - azure 角色清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="2e67a-119">列出角色的動作</span><span class="sxs-lookup"><span data-stu-id="2e67a-119">List actions of a role</span></span>
<span data-ttu-id="2e67a-120">toolist hello 動作的角色，使用：</span><span class="sxs-lookup"><span data-stu-id="2e67a-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="2e67a-121">hello 下列範例顯示 hello 動作的 hello*參與者*和*虛擬機器參與者*角色。</span><span class="sxs-lookup"><span data-stu-id="2e67a-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![RBAC Azure 命令列 - azure 角色顯示 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="2e67a-123">列出存取權</span><span class="sxs-lookup"><span data-stu-id="2e67a-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="2e67a-124">列出資源群組上有效的角色指派</span><span class="sxs-lookup"><span data-stu-id="2e67a-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="2e67a-125">存在於資源群組中，使用 toolist hello 角色指派：</span><span class="sxs-lookup"><span data-stu-id="2e67a-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="2e67a-126">hello 下列範例顯示 hello 角色指派中 hello *pharma-銷售額-projecforcast*群組。</span><span class="sxs-lookup"><span data-stu-id="2e67a-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure 命令列 - 依群組顯示的 azure 角色指派清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="2e67a-128">列出使用者的角色指派</span><span class="sxs-lookup"><span data-stu-id="2e67a-128">List role assignments for a user</span></span>
<span data-ttu-id="2e67a-129">toolist hello 角色指派特定的使用者，以及指派給 tooa 使用者群組的 hello 分派使用：</span><span class="sxs-lookup"><span data-stu-id="2e67a-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="2e67a-130">您也可以看到繼承自群組，藉由修改 hello 命令的角色指派：</span><span class="sxs-lookup"><span data-stu-id="2e67a-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="2e67a-131">hello 下列範例顯示 hello 角色指派授與 toohello  *sameert@aaddemo.com* 使用者。</span><span class="sxs-lookup"><span data-stu-id="2e67a-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="2e67a-132">這包括直接 toohello 使用者指派的角色和角色繼承自群組。</span><span class="sxs-lookup"><span data-stu-id="2e67a-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure 命令列 - 依使用者顯示的 azure 角色指派清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="2e67a-134">授與存取權</span><span class="sxs-lookup"><span data-stu-id="2e67a-134">Grant access</span></span>
<span data-ttu-id="2e67a-135">toogrant 存取您識別您想 tooassign hello 角色之後，使用：</span><span class="sxs-lookup"><span data-stu-id="2e67a-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="2e67a-136">指派角色 toogroup hello 訂用帳戶範圍</span><span class="sxs-lookup"><span data-stu-id="2e67a-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="2e67a-137">tooassign 角色 tooa 群組在 hello 訂用帳戶範圍，使用：</span><span class="sxs-lookup"><span data-stu-id="2e67a-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="2e67a-138">hello 下列範例會將指派 hello*讀取器*角色太*Christine Koch 小組*在 hello*訂用帳戶*範圍。</span><span class="sxs-lookup"><span data-stu-id="2e67a-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![RBAC Azure 命令列 - 群組所建立的 azure 角色指派 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="2e67a-140">指派在 hello 訂用帳戶範圍的角色 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="2e67a-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="2e67a-141">tooassign hello 訂用帳戶範圍，使用角色 tooan 應用程式：</span><span class="sxs-lookup"><span data-stu-id="2e67a-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="2e67a-142">hello 下列範例會授與 hello*參與者*角色 tooan *Azure AD* hello 上的應用程式選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e67a-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![RBAC Azure 命令列 - 應用程式所建立的 azure 角色指派](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="2e67a-144">指派給角色 tooa 使用者在 hello 資源群組領域</span><span class="sxs-lookup"><span data-stu-id="2e67a-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="2e67a-145">tooassign 角色 tooa 使用者在 hello 資源群組範圍，使用：</span><span class="sxs-lookup"><span data-stu-id="2e67a-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="2e67a-146">hello 下列範例會授與 hello*虛擬機器參與者*角色太*samert@aaddemo.com* 使用者在 hello *Pharma-銷售額-ProjectForcast*資源群組範圍。</span><span class="sxs-lookup"><span data-stu-id="2e67a-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![RBAC Azure 命令列 - 使用者所建立的 azure 角色指派 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="2e67a-148">指定角色 tooa 群組在 hello 資源範圍</span><span class="sxs-lookup"><span data-stu-id="2e67a-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="2e67a-149">tooassign 角色 tooa 群組在 hello 資源範圍，使用：</span><span class="sxs-lookup"><span data-stu-id="2e67a-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="2e67a-150">hello 下列範例會授與 hello*虛擬機器參與者*角色 tooan *Azure AD*群組*子網路*。</span><span class="sxs-lookup"><span data-stu-id="2e67a-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![RBAC Azure 命令列 - 群組所建立的 azure 角色指派 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="2e67a-152">移除存取</span><span class="sxs-lookup"><span data-stu-id="2e67a-152">Remove access</span></span>
<span data-ttu-id="2e67a-153">tooremove 角色指派，請使用：</span><span class="sxs-lookup"><span data-stu-id="2e67a-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="2e67a-154">hello 下列範例會移除 hello*虛擬機器參與者*角色指派從 hello  *sammert@aaddemo.com*  hello 上的使用者*Pharma-銷售額-ProjectForcast*資源群組。</span><span class="sxs-lookup"><span data-stu-id="2e67a-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="2e67a-155">hello 範例會從 hello 訂用帳戶上的群組，然後移除 hello 角色指派。</span><span class="sxs-lookup"><span data-stu-id="2e67a-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![RBAC Azure 命令列 - azure 角色指派刪除 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="2e67a-157">建立自訂角色</span><span class="sxs-lookup"><span data-stu-id="2e67a-157">Create a custom role</span></span>
<span data-ttu-id="2e67a-158">toocreate 自訂安全性角色，使用：</span><span class="sxs-lookup"><span data-stu-id="2e67a-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="2e67a-159">hello 下列範例會建立自訂安全性角色呼叫*虛擬機器運算子*。</span><span class="sxs-lookup"><span data-stu-id="2e67a-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="2e67a-160">此自訂角色會授與存取 tooall 讀取作業的*Microsoft.Compute*， *Microsoft.Storage*，和*Microsoft.Network*資源提供者及授與存取權toostart，重新啟動，而監視虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2e67a-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="2e67a-161">這個自訂角色可用於兩個訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="2e67a-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="2e67a-162">這個範例使用 JSON 檔案做為輸入。</span><span class="sxs-lookup"><span data-stu-id="2e67a-162">This example uses a JSON file as an input.</span></span>

![JSON - 自訂角色定義 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure 命令列 - azure 角色建立 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="2e67a-165">修改自訂角色</span><span class="sxs-lookup"><span data-stu-id="2e67a-165">Modify a custom role</span></span>
<span data-ttu-id="2e67a-166">toomodify 自訂安全性角色，第一次使用 hello`azure role show`命令 tooretrieve 角色定義。</span><span class="sxs-lookup"><span data-stu-id="2e67a-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="2e67a-167">第二，請 hello 所要的變更 toohello 角色定義檔。</span><span class="sxs-lookup"><span data-stu-id="2e67a-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="2e67a-168">最後，使用`azure role set`toosave hello 修改角色定義。</span><span class="sxs-lookup"><span data-stu-id="2e67a-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="2e67a-169">hello 下列範例會將 hello *Microsoft.Insights/diagnosticSettings/*作業 toohello**動作**，和 Azure 訂用帳戶 toohello **AssignableScopes**hello 虛擬機器操作員自訂角色。</span><span class="sxs-lookup"><span data-stu-id="2e67a-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![JSON - 修改自訂角色定義 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![RBAC Azure 命令列 - azure 角色設定 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="2e67a-172">刪除自訂角色</span><span class="sxs-lookup"><span data-stu-id="2e67a-172">Delete a custom role</span></span>
<span data-ttu-id="2e67a-173">toodelete 自訂安全性角色，第一次使用 hello`azure role show`命令 toodetermine hello**識別碼**的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="2e67a-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="2e67a-174">然後，使用 hello`azure role delete`命令 toodelete hello 角色，藉由指定 hello**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="2e67a-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="2e67a-175">hello 下列範例會移除 hello*虛擬機器運算子*自訂角色。</span><span class="sxs-lookup"><span data-stu-id="2e67a-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![RBAC Azure 命令列 - azure 角色刪除 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="2e67a-177">列出自訂角色</span><span class="sxs-lookup"><span data-stu-id="2e67a-177">List custom roles</span></span>
<span data-ttu-id="2e67a-178">所提供的範圍，指派 toolist hello 角色使用 hello`azure role list`命令。</span><span class="sxs-lookup"><span data-stu-id="2e67a-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="2e67a-179">hello，下列命令會列出可供指派 hello 選取訂用帳戶中的所有角色。</span><span class="sxs-lookup"><span data-stu-id="2e67a-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![RBAC Azure 命令列 - azure 角色清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="2e67a-181">在下列範例的 hello，hello*虛擬機器運算子*hello 中的自訂角色沒有*Production4*訂用帳戶因為該訂用帳戶不在 hello **AssignableScopes**的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="2e67a-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![RBAC Azure 命令列 - 自訂角色的 azure 角色清單 - 螢幕擷取畫面](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="2e67a-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e67a-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

