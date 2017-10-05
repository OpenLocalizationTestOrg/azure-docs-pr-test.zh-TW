---
title: "建立 Azure RBAC 的自訂角色 | Microsoft Docs"
description: "了解如何使用 Azure 角色型存取控制來定義自訂角色，以在您的 Azure 訂用帳戶中進行更精確的身分識別管理。"
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
ms.openlocfilehash: 8e72f2c8095d13c4b6df3c6576bd58806a3c0f2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="0a5a4-103">建立 Azure 角色型存取控制的自訂角色</span><span class="sxs-lookup"><span data-stu-id="0a5a4-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="0a5a4-104">如果內建角色都不符合您的特定存取需求，請在 Azure 角色型存取控制 (RBAC) 中建立自訂角色。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of the built-in roles meet your specific access needs.</span></span> <span data-ttu-id="0a5a4-105">使用 [Azure PowerShell](role-based-access-control-manage-access-powershell.md)、[Azure 命令列介面](role-based-access-control-manage-access-azure-cli.md) (CLI) 和 [REST API](role-based-access-control-manage-access-rest.md)，可以建立自訂角色。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and the [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="0a5a4-106">就像內建角色一樣，您可以將自訂角色指派給訂用帳戶、資源群組和資源範圍的使用者、群組和應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-106">Just like built-in roles, you can assign custom roles to users, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="0a5a4-107">自訂角色會儲存在 Azure AD 租用戶中，而且可在訂用帳戶之間共用。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="0a5a4-108">每個租用戶可以建立最多 2000 個自訂角色。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-108">Each tenant can create up to 2000 custom roles.</span></span> 

<span data-ttu-id="0a5a4-109">以下範例示範可監視和重新啟動虛擬機器的自訂角色：</span><span class="sxs-lookup"><span data-stu-id="0a5a4-109">The following example shows a custom role for monitoring and restarting virtual machines:</span></span>

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
## <a name="actions"></a><span data-ttu-id="0a5a4-110">動作</span><span class="sxs-lookup"><span data-stu-id="0a5a4-110">Actions</span></span>
<span data-ttu-id="0a5a4-111">自訂角色的 **Actions** 屬性會指定角色授與存取權的 Azure 作業。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-111">The **Actions** property of a custom role specifies the Azure operations to which the role grants access.</span></span> <span data-ttu-id="0a5a4-112">它是識別 Azure 資源提供者的安全性實體作業的作業字串集合。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="0a5a4-113">作業字串遵循 `Microsoft.<ProviderName>/<ChildResourceType>/<action>` 的格式。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-113">Operation strings follow the format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="0a5a4-114">包含萬用字元 (\*) 的作業字串會授與符合作業字串的所有作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-114">Operation strings that contain wildcards (\*) grant access to all operations that match the operation string.</span></span> <span data-ttu-id="0a5a4-115">例如：</span><span class="sxs-lookup"><span data-stu-id="0a5a4-115">For instance:</span></span>

* <span data-ttu-id="0a5a4-116">`*/read` 授與所有 Azure 資源提供者的所有資源類型的讀取作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-116">`*/read` grants access to read operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="0a5a4-117">`Microsoft.Compute/*` 可授與對 Microsoft.Compute 資源提供者中所有資源類型之所有作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-117">`Microsoft.Compute/*` grants access to all operations for all resource types in the Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="0a5a4-118">`Microsoft.Network/*/read` 授與 Azure 的 Microsoft.Network 資源提供者的所有資源類型的讀取作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-118">`Microsoft.Network/*/read` grants access to read operations for all resource types in the Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="0a5a4-119">`Microsoft.Compute/virtualMachines/*` 授與虛擬機器和其子系資源類型的所有作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-119">`Microsoft.Compute/virtualMachines/*` grants access to all operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="0a5a4-120">`Microsoft.Web/sites/restart/Action` 授與重新啟動網站的存取權。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-120">`Microsoft.Web/sites/restart/Action` grants access to restart websites.</span></span>

<span data-ttu-id="0a5a4-121">使用 `Get-AzureRmProviderOperation` (在 PowerShell 中) 或 `azure provider operations show` (在 Azure CLI 中) 來列出 Azure 資源提供者的作業。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) to list operations of Azure resource providers.</span></span> <span data-ttu-id="0a5a4-122">您也可以使用這些命令以確認作業字串有效，以及展開萬用字元作業字串。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-122">You may also use these commands to verify that an operation string is valid, and to expand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell 螢幕擷取畫面 - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="0a5a4-124">Azure CLI 螢幕擷取畫面 - azure 提供者作業顯示 "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="0a5a4-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="0a5a4-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="0a5a4-125">NotActions</span></span>
<span data-ttu-id="0a5a4-126">如果排除限制的作業可更輕鬆地定義您要允許的作業集合，請使用 **NotActions** 屬性。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-126">Use the **NotActions** property if the set of operations that you wish to allow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="0a5a4-127">自訂角色授與的存取權是藉由從 **Actions** 作業中去掉 **NotActions** 作業來計算。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-127">The access granted by a custom role is computed by subtracting the **NotActions** operations from the **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="0a5a4-128">如果為使用者指派會排除 **NotActions** 中作業的角色，並指派授與相同作業存取權的第二個角色，即會允許使用者執行該作業。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access to the same operation, the user is allowed to perform that operation.</span></span> <span data-ttu-id="0a5a4-129">**NotActions** 不是拒絕規則 – 它只是一個便利的方式，可以在需要排除特定作業時建立允許作業集。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-129">**NotActions** is not a deny rule – it is simply a convenient way to create a set of allowed operations when specific operations need to be excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="0a5a4-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="0a5a4-130">AssignableScopes</span></span>
<span data-ttu-id="0a5a4-131">自訂角色的 **AssignableScopes** 屬性會指定自訂角色可供指派的範圍 (訂用帳戶、資源群組或資源)。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-131">The **AssignableScopes** property of the custom role specifies the scopes (subscriptions, resource groups, or resources) within which the custom role is available for assignment.</span></span> <span data-ttu-id="0a5a4-132">您可以讓自訂角色僅指派給需要它的訂用帳戶或資源群組，不會干擾其餘訂用帳戶或資源群組的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-132">You can make the custom role available for assignment in only the subscriptions or resource groups that require it, and not clutter user experience for the rest of the subscriptions or resource groups.</span></span>

<span data-ttu-id="0a5a4-133">有效的可指派範圍範例包括：</span><span class="sxs-lookup"><span data-stu-id="0a5a4-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="0a5a4-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - 讓角色可用於兩個訂用帳戶中的指派。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes the role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="0a5a4-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - 讓角色可用於單一訂用帳戶中的指派。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes the role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="0a5a4-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - 讓角色僅可用於網路資源群組中的指派。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes the role available for assignment only in the Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="0a5a4-137">您至少必須使用一個訂用帳戶、資源群組或資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="0a5a4-138">自訂角色存取控制</span><span class="sxs-lookup"><span data-stu-id="0a5a4-138">Custom roles access control</span></span>
<span data-ttu-id="0a5a4-139">自訂角色的 **AssignableScopes** 屬性也會控制誰可以檢視、修改和刪除角色。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-139">The **AssignableScopes** property of the custom role also controls who can view, modify, and delete the role.</span></span>

* <span data-ttu-id="0a5a4-140">誰可以建立自訂角色？</span><span class="sxs-lookup"><span data-stu-id="0a5a4-140">Who can create a custom role?</span></span>
    <span data-ttu-id="0a5a4-141">訂用帳戶、資源群組和資源的擁有者 (和使用者存取管理員) 可以建立自訂角色以在這些範圍中使用。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="0a5a4-142">建立角色的使用者必須能夠對角色的所有 **AssignableScopes** 執行 `Microsoft.Authorization/roleDefinition/write` 作業。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-142">The user creating the role needs to be able to perform `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of the role.</span></span>
* <span data-ttu-id="0a5a4-143">誰可以修改自訂角色？</span><span class="sxs-lookup"><span data-stu-id="0a5a4-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="0a5a4-144">訂用帳戶、資源群組和資源的擁有者 (和使用者存取管理員) 可以在這些範圍中修改自訂角色。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="0a5a4-145">使用者必須能夠對自訂角色的所有 **AssignableScopes** 執行 `Microsoft.Authorization/roleDefinition/write` 作業。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-145">Users need to be able to perform the `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="0a5a4-146">誰可以檢視自訂角色？</span><span class="sxs-lookup"><span data-stu-id="0a5a4-146">Who can view custom roles?</span></span>
    <span data-ttu-id="0a5a4-147">Azure RBAC 中的所有內建角色允許檢視可用於指派的角色。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="0a5a4-148">可以在範圍中執行 `Microsoft.Authorization/roleDefinition/read` 作業的使用者，可以檢視可用於在該範圍中指派的 RBAC 角色。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-148">Users who can perform the `Microsoft.Authorization/roleDefinition/read` operation at a scope can view the RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="0a5a4-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0a5a4-149">See also</span></span>
* <span data-ttu-id="0a5a4-150">[角色型存取控制](role-based-access-control-configure.md)：開始在 Azure 入口網站中使用 RBAC。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="0a5a4-151">了解如何使用下列各項管理存取權：</span><span class="sxs-lookup"><span data-stu-id="0a5a4-151">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="0a5a4-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a5a4-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="0a5a4-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0a5a4-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="0a5a4-154">REST API</span><span class="sxs-lookup"><span data-stu-id="0a5a4-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="0a5a4-155">[內建角色](role-based-access-built-in-roles.md)︰取得有關 RBAC 中標準角色的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0a5a4-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
