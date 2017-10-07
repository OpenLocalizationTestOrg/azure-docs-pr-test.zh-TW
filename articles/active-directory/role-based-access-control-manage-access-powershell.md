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
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="bea3e-103">使用 Azure PowerShell 管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="bea3e-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bea3e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bea3e-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="bea3e-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bea3e-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="bea3e-106">REST API</span><span class="sxs-lookup"><span data-stu-id="bea3e-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="bea3e-107">您可以在 hello Azure 入口網站和 Azure 資源管理 API toomanage 存取 tooyour 訂用帳戶在細微的層級中使用角色型存取控制 (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="bea3e-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Management API toomanage access tooyour subscription at a fine-grained level.</span></span> <span data-ttu-id="bea3e-108">利用此功能，您可以藉由指定在特定範圍的某些角色 toothem 授與存取 Active Directory 使用者、 群組或服務主體。</span><span class="sxs-lookup"><span data-stu-id="bea3e-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="bea3e-109">您可以使用 PowerShell toomanage RBAC 之前，您需要下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="bea3e-109">Before you can use PowerShell toomanage RBAC, you need hello following prerequisites:</span></span>

* <span data-ttu-id="bea3e-110">Azure PowerShell 0.8.8 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="bea3e-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="bea3e-111">tooinstall hello 最新版本並關聯它與您 Azure 訂用帳戶，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="bea3e-111">tooinstall hello latest version and associate it with your Azure subscription, see [how tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="bea3e-112">Azure Resource Manager Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bea3e-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="bea3e-113">安裝 hello [Azure 資源管理員 cmdlet](/powershell/azure/overview)在 PowerShell 中。</span><span class="sxs-lookup"><span data-stu-id="bea3e-113">Install hello [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="bea3e-114">列出角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="bea3e-115">列出所有可用的角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-115">List all available roles</span></span>
<span data-ttu-id="bea3e-116">toolist RBAC 角色可供指派和 tooinspect hello 作業 toowhich 他們授與存取權，會使用`Get-AzureRmRoleDefinition`。</span><span class="sxs-lookup"><span data-stu-id="bea3e-116">toolist RBAC roles that are available for assignment and tooinspect hello operations toowhich they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="bea3e-118">列出角色的動作</span><span class="sxs-lookup"><span data-stu-id="bea3e-118">List actions of a role</span></span>
<span data-ttu-id="bea3e-119">toolist hello 動作特定的角色，會使用`Get-AzureRmRoleDefinition <role name>`。</span><span class="sxs-lookup"><span data-stu-id="bea3e-119">toolist hello actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - 特定角色的 Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="bea3e-121">查看誰具有存取權</span><span class="sxs-lookup"><span data-stu-id="bea3e-121">See who has access</span></span>
<span data-ttu-id="bea3e-122">toolist RBAC 存取指派，使用`Get-AzureRmRoleAssignment`。</span><span class="sxs-lookup"><span data-stu-id="bea3e-122">toolist RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="bea3e-123">列出特定範圍的角色指派</span><span class="sxs-lookup"><span data-stu-id="bea3e-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="bea3e-124">您可以看到所有 hello 存取指派指定的訂用帳戶、 資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="bea3e-124">You can see all hello access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="bea3e-125">比方說，toosee hello 所有都 hello 作用中的指派為資源群組，請使用`Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`。</span><span class="sxs-lookup"><span data-stu-id="bea3e-125">For example, toosee hello all hello active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 資源群組的 Get-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a><span data-ttu-id="bea3e-127">清單的角色指派 tooa 使用者</span><span class="sxs-lookup"><span data-stu-id="bea3e-127">List roles assigned tooa user</span></span>
<span data-ttu-id="bea3e-128">使用者和指派給 toohello toowhich hello 使用者所屬的群組的 hello 角色指定所有的 hello 角色指派 tooa toolist 使用`Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`。</span><span class="sxs-lookup"><span data-stu-id="bea3e-128">toolist all hello roles that are assigned tooa specified user and hello roles that are assigned toohello groups toowhich hello user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 使用者的 Get-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="bea3e-130">列出傳統服務管理員和共同管理員角色指派</span><span class="sxs-lookup"><span data-stu-id="bea3e-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="bea3e-131">toolist 存取指派 hello 傳統訂用帳戶管理員和 coadministrators，使用：</span><span class="sxs-lookup"><span data-stu-id="bea3e-131">toolist access assignments for hello classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="bea3e-132">授與存取權</span><span class="sxs-lookup"><span data-stu-id="bea3e-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="bea3e-133">搜尋物件識別碼</span><span class="sxs-lookup"><span data-stu-id="bea3e-133">Search for object IDs</span></span>
<span data-ttu-id="bea3e-134">tooassign 角色，您需要 tooidentify hello 物件 （使用者、 群組或應用程式） 和 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="bea3e-134">tooassign a role, you need tooidentify both hello object (user, group, or application) and hello scope.</span></span>

<span data-ttu-id="bea3e-135">如果您不知道 hello 訂用帳戶 ID，您可以找到它在 hello**訂閱**hello Azure 入口網站上的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bea3e-135">If you don't know hello subscription ID, you can find it in hello **Subscriptions** blade on hello Azure portal.</span></span> <span data-ttu-id="bea3e-136">如何 tooquery hello 訂用帳戶 id，請參閱的 toolearn [Get-azuresubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="bea3e-136">toolearn how tooquery for hello subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="bea3e-137">使用 Azure AD 群組，tooget hello 物件識別碼：</span><span class="sxs-lookup"><span data-stu-id="bea3e-137">tooget hello object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="bea3e-138">tooget hello 物件識別碼的 Azure AD 服務主體或應用程式，使用：</span><span class="sxs-lookup"><span data-stu-id="bea3e-138">tooget hello object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="bea3e-139">指派在 hello 訂用帳戶範圍的角色 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="bea3e-139">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="bea3e-140">toogrant hello 訂用帳戶範圍，使用的存取 tooan 應用程式：</span><span class="sxs-lookup"><span data-stu-id="bea3e-140">toogrant access tooan application at hello subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="bea3e-142">指派給角色 tooa 使用者在 hello 資源群組領域</span><span class="sxs-lookup"><span data-stu-id="bea3e-142">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="bea3e-143">toogrant 存取 tooa 使用者在 hello 資源群組範圍，使用：</span><span class="sxs-lookup"><span data-stu-id="bea3e-143">toogrant access tooa user at hello resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="bea3e-145">指定角色 tooa 群組在 hello 資源範圍</span><span class="sxs-lookup"><span data-stu-id="bea3e-145">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="bea3e-146">toogrant 存取 tooa 群組在 hello 資源範圍，使用：</span><span class="sxs-lookup"><span data-stu-id="bea3e-146">toogrant access tooa group at hello resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="bea3e-148">移除存取</span><span class="sxs-lookup"><span data-stu-id="bea3e-148">Remove access</span></span>
<span data-ttu-id="bea3e-149">使用者、 群組和應用程式，使用 tooremove 存取：</span><span class="sxs-lookup"><span data-stu-id="bea3e-149">tooremove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="bea3e-151">建立自訂角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-151">Create a custom role</span></span>
<span data-ttu-id="bea3e-152">toocreate 自訂安全性角色，使用 hello```New-AzureRmRoleDefinition```命令。</span><span class="sxs-lookup"><span data-stu-id="bea3e-152">toocreate a custom role, use hello ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="bea3e-153">有兩種方法來建構使用 PSRoleDefinitionObject 或 JSON 範本的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="bea3e-153">There are two methods of structuring hello role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="bea3e-154">取得資源提供者的動作</span><span class="sxs-lookup"><span data-stu-id="bea3e-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="bea3e-155">當您要從頭建立自訂角色時，就很重要的 tooknow 所有 hello 可能從 hello 資源提供者的作業。</span><span class="sxs-lookup"><span data-stu-id="bea3e-155">When You are creating custom roles from scratch, it is important tooknow all hello possible operations from hello resource providers.</span></span>
<span data-ttu-id="bea3e-156">使用 hello```Get-AzureRMProviderOperation```命令 tooget 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="bea3e-156">Use hello ```Get-AzureRMProviderOperation``` command tooget this information.</span></span>
<span data-ttu-id="bea3e-157">例如，如果您想 toocheck 所有 hello 可用操作的虛擬機器會都使用此命令：</span><span class="sxs-lookup"><span data-stu-id="bea3e-157">For example, if you want toocheck all hello available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="bea3e-158">使用 PSRoleDefinitionObject 建立角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="bea3e-159">當您使用 PowerShell toocreate 自訂安全性角色時，您可以從頭開始，或使用其中一種 hello[內建角色](role-based-access-built-in-roles.md)做為起點。</span><span class="sxs-lookup"><span data-stu-id="bea3e-159">When you use PowerShell toocreate a custom role, you can start from scratch or use one of hello [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="bea3e-160">本節中的 hello 範例開頭為內建的角色，然後使用所需權限進行自訂。</span><span class="sxs-lookup"><span data-stu-id="bea3e-160">hello example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="bea3e-161">編輯 hello 屬性 tooadd hello*動作*， *notActions*，或*範圍*您要的然後將 hello 變更儲存為新的角色。</span><span class="sxs-lookup"><span data-stu-id="bea3e-161">Edit hello attributes tooadd hello *Actions*, *notActions*, or *scopes* that you want, and then save hello changes as a new role.</span></span>

<span data-ttu-id="bea3e-162">hello 下列範例會啟動以 hello*虛擬機器參與者*角色，並使用該 toocreate 自訂安全性角色會稱為*虛擬機器運算子*。</span><span class="sxs-lookup"><span data-stu-id="bea3e-162">hello following example starts with hello *Virtual Machine Contributor* role and uses that toocreate a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="bea3e-163">hello 新角色會授與存取 tooall 讀取作業的*Microsoft.Compute*， *Microsoft.Storage*，和*Microsoft.Network*資源提供者及授與存取權toostart，重新啟動，而監視虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bea3e-163">hello new role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="bea3e-164">hello 自訂角色可以使用兩個訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="bea3e-164">hello custom role can be used in two subscriptions.</span></span>

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

### <a name="create-role-with-json-template"></a><span data-ttu-id="bea3e-166">使用 JSON 範本建立角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-166">Create role with JSON template</span></span>
<span data-ttu-id="bea3e-167">JSON 範本可以作為 hello 自訂角色的 hello 來源定義。</span><span class="sxs-lookup"><span data-stu-id="bea3e-167">A JSON template can be used as hello source definition for hello custom role.</span></span> <span data-ttu-id="bea3e-168">hello 下列範例會建立自訂安全性角色可讓讀取權限 toostorage 和計算資源、 存取 toosupport，並將該角色 tootwo 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bea3e-168">hello following example creates a custom role that allows read access toostorage and compute resources, access toosupport, and adds that role tootwo subscriptions.</span></span> <span data-ttu-id="bea3e-169">建立新的檔案`C:\CustomRoles\customrole1.json`以下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="bea3e-169">Create a new file `C:\CustomRoles\customrole1.json` with hello following example.</span></span> <span data-ttu-id="bea3e-170">hello Id 應該設定太`null`初始角色建立為新的識別碼時自動產生。</span><span class="sxs-lookup"><span data-stu-id="bea3e-170">hello Id should be set too`null` on initial role creation as a new ID is generated automatically.</span></span> 

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
<span data-ttu-id="bea3e-171">tooadd hello 角色 toohello 訂用帳戶，執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="bea3e-171">tooadd hello role toohello subscriptions, run hello following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="bea3e-172">修改自訂角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-172">Modify a custom role</span></span>
<span data-ttu-id="bea3e-173">類似 toocreating 自訂安全性角色，您可以修改現有的自訂角色使用 hello PSRoleDefinitionObject 或 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="bea3e-173">Similar toocreating a custom role, you can modify an existing custom role using either hello PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="bea3e-174">使用 PSRoleDefinitionObject 修改角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="bea3e-175">toomodify 自訂安全性角色，首先，使用 hello`Get-AzureRmRoleDefinition`命令 tooretrieve hello 角色定義。</span><span class="sxs-lookup"><span data-stu-id="bea3e-175">toomodify a custom role, first, use hello `Get-AzureRmRoleDefinition` command tooretrieve hello role definition.</span></span> <span data-ttu-id="bea3e-176">第二，變更所需的 hello toohello 角色定義。</span><span class="sxs-lookup"><span data-stu-id="bea3e-176">Second, make hello desired changes toohello role definition.</span></span> <span data-ttu-id="bea3e-177">最後，使用 hello`Set-AzureRmRoleDefinition`命令 toosave hello 修改角色定義。</span><span class="sxs-lookup"><span data-stu-id="bea3e-177">Finally, use hello `Set-AzureRmRoleDefinition` command toosave hello modified role definition.</span></span>

<span data-ttu-id="bea3e-178">hello 下列範例會將 hello`Microsoft.Insights/diagnosticSettings/*`作業 toohello*虛擬機器運算子*自訂角色。</span><span class="sxs-lookup"><span data-stu-id="bea3e-178">hello following example adds hello `Microsoft.Insights/diagnosticSettings/*` operation toohello *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="bea3e-180">hello 下列範例會將 Azure 訂用帳戶 toohello 可指派的範圍的 hello*虛擬機器運算子*自訂角色。</span><span class="sxs-lookup"><span data-stu-id="bea3e-180">hello following example adds an Azure subscription toohello assignable scopes of hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="bea3e-182">使用 JSON 範本修改角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-182">Modify role with JSON template</span></span>
<span data-ttu-id="bea3e-183">使用 hello 先前的 JSON 範本，可以輕鬆地修改現有的自訂角色 tooadd 或移除動作。</span><span class="sxs-lookup"><span data-stu-id="bea3e-183">Using hello previous JSON template, you can easily modify an existing custom role tooadd or remove Actions.</span></span> <span data-ttu-id="bea3e-184">更新 hello JSON 範本，並加入 hello 網路讀取的動作 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="bea3e-184">Update hello JSON template and add hello read action for networking as shown in hello following example.</span></span> <span data-ttu-id="bea3e-185">hello 範本中所列的 hello 定義不是累積套用的 tooan 現有的定義，這表示該 hello 角色出現完全依照您在 hello 範本中指定。</span><span class="sxs-lookup"><span data-stu-id="bea3e-185">hello definitions listed in hello template are not cumulatively applied tooan existing definition, meaning that hello role appears exactly as you specify in hello template.</span></span> <span data-ttu-id="bea3e-186">您也需要識別碼為 hello 角色 hello tooupdate hello 識別碼 欄位。</span><span class="sxs-lookup"><span data-stu-id="bea3e-186">You also need tooupdate hello Id field with hello ID of hello role.</span></span> <span data-ttu-id="bea3e-187">如果您不確定此值為何，您可以使用 hello `Get-AzureRmRoleDefinition` cmdlet tooget 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="bea3e-187">If you aren't sure what this value is, you can use hello `Get-AzureRmRoleDefinition` cmdlet tooget this information.</span></span>

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

<span data-ttu-id="bea3e-188">tooupdate hello 現有的角色，執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="bea3e-188">tooupdate hello existing role, run hello following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="bea3e-189">刪除自訂角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-189">Delete a custom role</span></span>
<span data-ttu-id="bea3e-190">toodelete 自訂安全性角色，使用 hello`Remove-AzureRmRoleDefinition`命令。</span><span class="sxs-lookup"><span data-stu-id="bea3e-190">toodelete a custom role, use hello `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="bea3e-191">hello 下列範例會移除 hello*虛擬機器運算子*自訂角色。</span><span class="sxs-lookup"><span data-stu-id="bea3e-191">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="bea3e-193">列出自訂角色</span><span class="sxs-lookup"><span data-stu-id="bea3e-193">List custom roles</span></span>
<span data-ttu-id="bea3e-194">所提供的範圍，指派 toolist hello 角色使用 hello`Get-AzureRmRoleDefinition`命令。</span><span class="sxs-lookup"><span data-stu-id="bea3e-194">toolist hello roles that are available for assignment at a scope, use hello `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="bea3e-195">下列範例中的 hello 列出可供指派 hello 選取訂用帳戶中的所有角色。</span><span class="sxs-lookup"><span data-stu-id="bea3e-195">hello following example lists all roles that are available for assignment in hello selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="bea3e-197">在下列範例的 hello，hello*虛擬機器運算子*hello 中的自訂角色沒有*Production4*訂用帳戶因為該訂用帳戶不在 hello **AssignableScopes**的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="bea3e-197">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="bea3e-199">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bea3e-199">See also</span></span>
* <span data-ttu-id="bea3e-200">[搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="bea3e-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

