---
title: "使用 Azure PowerShell 管理角色型存取控制 (RBAC) | Microsoft Docs"
description: "如何使用 Azure PowerShell 管理 RBAC，包括列出角色、指派角色，以及刪除角色指派。"
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
ms.openlocfilehash: d7b11df21650b5cb27f9c3dd8306f8d12664185e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="ee035-103">使用 Azure PowerShell 管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="ee035-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee035-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee035-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="ee035-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ee035-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="ee035-106">REST API</span><span class="sxs-lookup"><span data-stu-id="ee035-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="ee035-107">您可以使用 Azure 入口網站和「Azure 資源管理」API 中的「角色型存取控制」(RBAC) 來精確地管理對訂用帳戶的存取。</span><span class="sxs-lookup"><span data-stu-id="ee035-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Management API to manage access to your subscription at a fine-grained level.</span></span> <span data-ttu-id="ee035-108">透過這項功能，您可以為 Active Directory 使用者、群組或是服務主體指派特定範圍的一些角色，藉此賦予其存取權限。</span><span class="sxs-lookup"><span data-stu-id="ee035-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="ee035-109">使用 PowerShell 來管理 RBAC 之前，您需要具備下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="ee035-109">Before you can use PowerShell to manage RBAC, you need the following prerequisites:</span></span>

* <span data-ttu-id="ee035-110">Azure PowerShell 0.8.8 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ee035-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="ee035-111">若要安裝最新版本，並將它與您的 Azure 訂用帳戶建立關聯，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ee035-111">To install the latest version and associate it with your Azure subscription, see [how to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ee035-112">Azure Resource Manager Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ee035-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="ee035-113">在 PowerShell 中，安裝 [Azure Resource Manager Cmdlet](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="ee035-113">Install the [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="ee035-114">列出角色</span><span class="sxs-lookup"><span data-stu-id="ee035-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="ee035-115">列出所有可用的角色</span><span class="sxs-lookup"><span data-stu-id="ee035-115">List all available roles</span></span>
<span data-ttu-id="ee035-116">若要列出可供指派的 RBAC 角色，以及若要檢查它們授與存取權的作業，請使用 `Get-AzureRmRoleDefinition`。</span><span class="sxs-lookup"><span data-stu-id="ee035-116">To list RBAC roles that are available for assignment and to inspect the operations to which they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="ee035-118">列出角色的動作</span><span class="sxs-lookup"><span data-stu-id="ee035-118">List actions of a role</span></span>
<span data-ttu-id="ee035-119">若要列出特定角色的動作，請使用 `Get-AzureRmRoleDefinition <role name>`。</span><span class="sxs-lookup"><span data-stu-id="ee035-119">To list the actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - 特定角色的 Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="ee035-121">查看誰具有存取權</span><span class="sxs-lookup"><span data-stu-id="ee035-121">See who has access</span></span>
<span data-ttu-id="ee035-122">若要列出 RBAC 存取權指派，請使用 `Get-AzureRmRoleAssignment`。</span><span class="sxs-lookup"><span data-stu-id="ee035-122">To list RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="ee035-123">列出特定範圍的角色指派</span><span class="sxs-lookup"><span data-stu-id="ee035-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="ee035-124">您可以查看指定訂用帳戶、資源群組或資源的所有存取權指派。</span><span class="sxs-lookup"><span data-stu-id="ee035-124">You can see all the access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="ee035-125">例如，若要查看某個資源群組的所有使用中指派，請使用 `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`。</span><span class="sxs-lookup"><span data-stu-id="ee035-125">For example, to see the all the active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 資源群組的 Get-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-to-a-user"></a><span data-ttu-id="ee035-127">列出指派給使用者的角色</span><span class="sxs-lookup"><span data-stu-id="ee035-127">List roles assigned to a user</span></span>
<span data-ttu-id="ee035-128">若要列出指派給指定使用者的所有角色，以及指派給該使用者所屬群組的角色，請使用 `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`。</span><span class="sxs-lookup"><span data-stu-id="ee035-128">To list all the roles that are assigned to a specified user and the roles that are assigned to the groups to which the user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 使用者的 Get-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="ee035-130">列出傳統服務管理員和共同管理員角色指派</span><span class="sxs-lookup"><span data-stu-id="ee035-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="ee035-131">若要列出傳統訂用帳戶管理員和共同管理員的存取權指派，請使用：</span><span class="sxs-lookup"><span data-stu-id="ee035-131">To list access assignments for the classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="ee035-132">授與存取權</span><span class="sxs-lookup"><span data-stu-id="ee035-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="ee035-133">搜尋物件識別碼</span><span class="sxs-lookup"><span data-stu-id="ee035-133">Search for object IDs</span></span>
<span data-ttu-id="ee035-134">若要指派角色，您必須識別物件 (使用者、群組或應用程式) 和範圍。</span><span class="sxs-lookup"><span data-stu-id="ee035-134">To assign a role, you need to identify both the object (user, group, or application) and the scope.</span></span>

<span data-ttu-id="ee035-135">如果您不知道訂用帳戶 ID，可以在 Azure 入口網站的 **[訂用帳戶]** 刀鋒視窗中找到。</span><span class="sxs-lookup"><span data-stu-id="ee035-135">If you don't know the subscription ID, you can find it in the **Subscriptions** blade on the Azure portal.</span></span> <span data-ttu-id="ee035-136">若要了解如何查詢訂用帳戶 ID，請參閱 MSDN 上的 [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) 。</span><span class="sxs-lookup"><span data-stu-id="ee035-136">To learn how to query for the subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="ee035-137">若要取得 Azure AD 群組的物件識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="ee035-137">To get the object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="ee035-138">若要取得 Azure AD 服務主體或應用程式的物件 ID，請使用：</span><span class="sxs-lookup"><span data-stu-id="ee035-138">To get the object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="ee035-139">將角色指派給訂用帳戶範圍中的應用程式</span><span class="sxs-lookup"><span data-stu-id="ee035-139">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="ee035-140">若要將存取權授與訂用帳戶範圍中的應用程式，請使用：</span><span class="sxs-lookup"><span data-stu-id="ee035-140">To grant access to an application at the subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="ee035-142">將角色指派給資源群組範圍中的使用者</span><span class="sxs-lookup"><span data-stu-id="ee035-142">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="ee035-143">若要將存取權授與資源群組範圍中的使用者，請使用：</span><span class="sxs-lookup"><span data-stu-id="ee035-143">To grant access to a user at the resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="ee035-145">將角色指派給資源範圍中的群組</span><span class="sxs-lookup"><span data-stu-id="ee035-145">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="ee035-146">若要將存取權授與資源範圍中的群組，請使用：</span><span class="sxs-lookup"><span data-stu-id="ee035-146">To grant access to a group at the resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="ee035-148">移除存取</span><span class="sxs-lookup"><span data-stu-id="ee035-148">Remove access</span></span>
<span data-ttu-id="ee035-149">若要移除使用者、群組和應用程式的存取權，請使用：</span><span class="sxs-lookup"><span data-stu-id="ee035-149">To remove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="ee035-151">建立自訂角色</span><span class="sxs-lookup"><span data-stu-id="ee035-151">Create a custom role</span></span>
<span data-ttu-id="ee035-152">若要建立自訂角色，請使用 ```New-AzureRmRoleDefinition``` 命令。</span><span class="sxs-lookup"><span data-stu-id="ee035-152">To create a custom role, use the ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="ee035-153">建構角色有兩種方法：使用 PSRoleDefinitionObject 或 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="ee035-153">There are two methods of structuring the role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="ee035-154">取得資源提供者的動作</span><span class="sxs-lookup"><span data-stu-id="ee035-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="ee035-155">當您從頭建立自訂角色時，務必知道所有可能來自資源提供者的作業。</span><span class="sxs-lookup"><span data-stu-id="ee035-155">When You are creating custom roles from scratch, it is important to know all the possible operations from the resource providers.</span></span>
<span data-ttu-id="ee035-156">使用 ```Get-AzureRMProviderOperation``` 命令來取得此資訊。</span><span class="sxs-lookup"><span data-stu-id="ee035-156">Use the ```Get-AzureRMProviderOperation``` command to get this information.</span></span>
<span data-ttu-id="ee035-157">例如，如果您想要檢查虛擬機器的所有可用作業，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="ee035-157">For example, if you want to check all the available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="ee035-158">使用 PSRoleDefinitionObject 建立角色</span><span class="sxs-lookup"><span data-stu-id="ee035-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="ee035-159">使用 PowerShell 建立自訂角色時，您可以從頭開始，或使用其中一個[內建角色](role-based-access-built-in-roles.md)當作起點。</span><span class="sxs-lookup"><span data-stu-id="ee035-159">When you use PowerShell to create a custom role, you can start from scratch or use one of the [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="ee035-160">本節中的範例是以內建角色當作起點，然後使用較高權限來自訂它。</span><span class="sxs-lookup"><span data-stu-id="ee035-160">The example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="ee035-161">請編輯屬性來新增您想要的 *Actions*、*notActions* 或 *scopes*，然後將變更儲存為新角色。</span><span class="sxs-lookup"><span data-stu-id="ee035-161">Edit the attributes to add the *Actions*, *notActions*, or *scopes* that you want, and then save the changes as a new role.</span></span>

<span data-ttu-id="ee035-162">下列範例會從「虛擬機器參與者」角色來開始，並使用它來建立稱為「虛擬機器操作者」的自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ee035-162">The following example starts with the *Virtual Machine Contributor* role and uses that to create a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="ee035-163">新角色會授與對 *Microsoft.Compute*、*Microsoft.Storage* 和 *Microsoft.Network* 資源提供者之所有讀取作業的存取權，以及授與對啟動、重新啟動和監視虛擬機器的存取權。</span><span class="sxs-lookup"><span data-stu-id="ee035-163">The new role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="ee035-164">自訂角色可用於兩個訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="ee035-164">The custom role can be used in two subscriptions.</span></span>

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

### <a name="create-role-with-json-template"></a><span data-ttu-id="ee035-166">使用 JSON 範本建立角色</span><span class="sxs-lookup"><span data-stu-id="ee035-166">Create role with JSON template</span></span>
<span data-ttu-id="ee035-167">JSON 範本可作為自訂角色的來源定義。</span><span class="sxs-lookup"><span data-stu-id="ee035-167">A JSON template can be used as the source definition for the custom role.</span></span> <span data-ttu-id="ee035-168">下列範例會建立自訂角色來允許讀取儲存體和計算資源及存取支援，然後將該角色新增至兩個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee035-168">The following example creates a custom role that allows read access to storage and compute resources, access to support, and adds that role to two subscriptions.</span></span> <span data-ttu-id="ee035-169">建立含有下列範例的新檔案 `C:\CustomRoles\customrole1.json`。</span><span class="sxs-lookup"><span data-stu-id="ee035-169">Create a new file `C:\CustomRoles\customrole1.json` with the following example.</span></span> <span data-ttu-id="ee035-170">最初建立角色時，應該將 Id 設為 `null`，因為會自動產生新的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ee035-170">The Id should be set to `null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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
<span data-ttu-id="ee035-171">若要將角色新增至訂用帳戶，請執行下列 PowerShell 命令︰</span><span class="sxs-lookup"><span data-stu-id="ee035-171">To add the role to the subscriptions, run the following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="ee035-172">修改自訂角色</span><span class="sxs-lookup"><span data-stu-id="ee035-172">Modify a custom role</span></span>
<span data-ttu-id="ee035-173">類似於建立自訂角色，您可以使用 PSRoleDefinitionObject 或 JSON 範本修改現有的自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ee035-173">Similar to creating a custom role, you can modify an existing custom role using either the PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="ee035-174">使用 PSRoleDefinitionObject 修改角色</span><span class="sxs-lookup"><span data-stu-id="ee035-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="ee035-175">若要修改自訂角色，請先使用 `Get-AzureRmRoleDefinition` 命令來擷取角色定義。</span><span class="sxs-lookup"><span data-stu-id="ee035-175">To modify a custom role, first, use the `Get-AzureRmRoleDefinition` command to retrieve the role definition.</span></span> <span data-ttu-id="ee035-176">接著，對角色定義進行想要的變更。</span><span class="sxs-lookup"><span data-stu-id="ee035-176">Second, make the desired changes to the role definition.</span></span> <span data-ttu-id="ee035-177">最後，使用 `Set-AzureRmRoleDefinition` 命令來儲存已修改的角色定義。</span><span class="sxs-lookup"><span data-stu-id="ee035-177">Finally, use the `Set-AzureRmRoleDefinition` command to save the modified role definition.</span></span>

<span data-ttu-id="ee035-178">下列範例會將 `Microsoft.Insights/diagnosticSettings/*` 作業加入到 *Virtual Machine Operator* 自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ee035-178">The following example adds the `Microsoft.Insights/diagnosticSettings/*` operation to the *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="ee035-180">下列範例會將 Azure 訂用帳戶新增到 *Virtual Machine Operator* 自訂角色的可指派範圍。</span><span class="sxs-lookup"><span data-stu-id="ee035-180">The following example adds an Azure subscription to the assignable scopes of the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="ee035-182">使用 JSON 範本修改角色</span><span class="sxs-lookup"><span data-stu-id="ee035-182">Modify role with JSON template</span></span>
<span data-ttu-id="ee035-183">您可以利用先前的 JSON 範本，輕鬆修改現有的自訂角色來新增或移除 Actions。</span><span class="sxs-lookup"><span data-stu-id="ee035-183">Using the previous JSON template, you can easily modify an existing custom role to add or remove Actions.</span></span> <span data-ttu-id="ee035-184">更新 JSON 範本，並新增網路的讀取動作，如下範例所示。</span><span class="sxs-lookup"><span data-stu-id="ee035-184">Update the JSON template and add the read action for networking as shown in the following example.</span></span> <span data-ttu-id="ee035-185">範本中所列的定義不會累積套用至現有的定義，這表示角色會完全依照您在範本中指定的樣子出現。</span><span class="sxs-lookup"><span data-stu-id="ee035-185">The definitions listed in the template are not cumulatively applied to an existing definition, meaning that the role appears exactly as you specify in the template.</span></span> <span data-ttu-id="ee035-186">您也需要以角色的識別碼來更新 Id 欄位。</span><span class="sxs-lookup"><span data-stu-id="ee035-186">You also need to update the Id field with the ID of the role.</span></span> <span data-ttu-id="ee035-187">如果不確定此值，您可以使用 `Get-AzureRmRoleDefinition` Cmdlet 來取得這項資訊。</span><span class="sxs-lookup"><span data-stu-id="ee035-187">If you aren't sure what this value is, you can use the `Get-AzureRmRoleDefinition` cmdlet to get this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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

<span data-ttu-id="ee035-188">若要更新現有的角色，請執行下列 PowerShell 命令︰</span><span class="sxs-lookup"><span data-stu-id="ee035-188">To update the existing role, run the following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="ee035-189">刪除自訂角色</span><span class="sxs-lookup"><span data-stu-id="ee035-189">Delete a custom role</span></span>
<span data-ttu-id="ee035-190">若要刪除自訂角色，請使用 `Remove-AzureRmRoleDefinition` 命令。</span><span class="sxs-lookup"><span data-stu-id="ee035-190">To delete a custom role, use the `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="ee035-191">下列範例會移除 *Virtual Machine Operator* 自訂角色</span><span class="sxs-lookup"><span data-stu-id="ee035-191">The following example removes the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="ee035-193">列出自訂角色</span><span class="sxs-lookup"><span data-stu-id="ee035-193">List custom roles</span></span>
<span data-ttu-id="ee035-194">若要列出範圍中可供指派的角色，請使用 `Get-AzureRmRoleDefinition` 命令。</span><span class="sxs-lookup"><span data-stu-id="ee035-194">To list the roles that are available for assignment at a scope, use the `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="ee035-195">下列範例會列出選取的訂用帳戶中可供指派的所有角色。</span><span class="sxs-lookup"><span data-stu-id="ee035-195">The following example lists all roles that are available for assignment in the selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="ee035-197">在下列範例中，*Virtual Machine Operator* 自訂角色無法在 *Production4* 訂用帳戶中使用，因為該訂用帳戶並沒有在角色的 **AssignableScopes** 中。</span><span class="sxs-lookup"><span data-stu-id="ee035-197">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

![RBAC PowerShell - Get-AzureRmRoleDefinition - 螢幕擷取畫面](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="ee035-199">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ee035-199">See also</span></span>
* <span data-ttu-id="ee035-200">[搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="ee035-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

