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
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="8a0cf-103">建立 Azure 角色型存取控制的自訂角色</span><span class="sxs-lookup"><span data-stu-id="8a0cf-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="8a0cf-104">如果 hello 內建角色都不符合您的特定存取需求，建立自訂安全性角色中所有存取控制 (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="8a0cf-105">您可以使用建立自訂角色[Azure PowerShell](role-based-access-control-manage-access-powershell.md)， [Azure 命令列介面](role-based-access-control-manage-access-azure-cli.md)(CLI)，和 hello [REST API](role-based-access-control-manage-access-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="8a0cf-106">如同內建的角色，您可以指派自訂角色 toousers、 群組和應用程式在訂用帳戶、 資源群組和資源的範圍。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="8a0cf-107">自訂角色會儲存在 Azure AD 租用戶中，而且可在訂用帳戶之間共用。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="8a0cf-108">每個租用戶可以建立註冊 too2000 自訂角色。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="8a0cf-109">hello 下列範例示範自訂安全性角色的監視，並重新啟動虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="8a0cf-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

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
## <a name="actions"></a><span data-ttu-id="8a0cf-110">動作</span><span class="sxs-lookup"><span data-stu-id="8a0cf-110">Actions</span></span>
<span data-ttu-id="8a0cf-111">hello**動作**的自訂安全性角色的屬性會指定 hello Azure 操作 toowhich hello 角色會授與的存取。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="8a0cf-112">它是識別 Azure 資源提供者的安全性實體作業的作業字串集合。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="8a0cf-113">操作字串 hello 的遵照格式`Microsoft.<ProviderName>/<ChildResourceType>/<action>`。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="8a0cf-114">作業包含萬用字元的字串 (\*) 授與存取權的比對 hello 作業字串 tooall 作業。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="8a0cf-115">例如：</span><span class="sxs-lookup"><span data-stu-id="8a0cf-115">For instance:</span></span>

* <span data-ttu-id="8a0cf-116">`*/read`授與存取 tooread 作業的所有 Azure 資源提供者的所有資源類型。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="8a0cf-117">`Microsoft.Compute/*`授與存取 tooall hello Microsoft.Compute 資源提供者中的所有資源類型的作業。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="8a0cf-118">`Microsoft.Network/*/read`授與存取 tooread hello Microsoft.Network 資源提供者中所有的資源類型，Azure 的作業。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="8a0cf-119">`Microsoft.Compute/virtualMachines/*`授與存取虛擬機器和及其子系的資源類型 tooall 作業。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="8a0cf-120">`Microsoft.Web/sites/restart/Action`授與存取 toorestart 網站。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="8a0cf-121">使用`Get-AzureRmProviderOperation`（以 PowerShell) 或`azure provider operations show`（在 Azure CLI) toolist 作業的 Azure 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="8a0cf-122">您也可以使用這些命令 tooverify 作業字串有效和 tooexpand 萬用字元操作字串。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell 螢幕擷取畫面 - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="8a0cf-124">Azure CLI 螢幕擷取畫面 - azure 提供者作業顯示 "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="8a0cf-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="8a0cf-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="8a0cf-125">NotActions</span></span>
<span data-ttu-id="8a0cf-126">使用 hello **NotActions**如果 hello 一組作業，您會希望 tooallow 更輕鬆地定義限制的作業中排除的屬性。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="8a0cf-127">hello 自訂安全性角色授與存取權的計算方式是減去 hello **NotActions**作業 hello**動作**作業。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="8a0cf-128">如果指派使用者角色中的作業中排除**NotActions**，並指派第二個角色，授與存取相同的作業，hello 使用者是的 toohello 允許 tooperform 該作業。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="8a0cf-129">**NotActions**不是拒絕規則 – 它時，只是方便 toocreate 一組允許的作業需要 toobe 排除特定的作業。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="8a0cf-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="8a0cf-130">AssignableScopes</span></span>
<span data-ttu-id="8a0cf-131">hello **AssignableScopes** hello 自訂角色屬性會指定 hello 範圍 （訂用帳戶、 資源群組或資源） 中的 hello 自訂的角色是指派的可用。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="8a0cf-132">您可以在 hello 自訂角色指派的可用只有 hello 訂閱或資源群組需要它，而不混亂的情形使用者體驗 hello 其餘 hello 訂用帳戶或資源群組。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="8a0cf-133">有效的可指派範圍範例包括：</span><span class="sxs-lookup"><span data-stu-id="8a0cf-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="8a0cf-134">"/ 訂用帳戶/c276fc76-9cd4-44c9-99a7-4fd71546436e"，"/ 訂用帳戶/e91d47c4-76f3-4271-a796-21b4ecfe3624"-讓 hello 角色可供指派兩個訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="8a0cf-135">"/ 訂用帳戶/c276fc76-9cd4-44c9-99a7-4fd71546436e"-讓 hello 角色可供指派單一訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="8a0cf-136">"/ 訂用帳戶/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/網路 」-讓 hello 分派只在 hello 網路資源群組中可用的角色。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="8a0cf-137">您至少必須使用一個訂用帳戶、資源群組或資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="8a0cf-138">自訂角色存取控制</span><span class="sxs-lookup"><span data-stu-id="8a0cf-138">Custom roles access control</span></span>
<span data-ttu-id="8a0cf-139">hello **AssignableScopes** hello 自訂角色的內容也會控制誰可以檢視、 修改和刪除 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="8a0cf-140">誰可以建立自訂角色？</span><span class="sxs-lookup"><span data-stu-id="8a0cf-140">Who can create a custom role?</span></span>
    <span data-ttu-id="8a0cf-141">訂用帳戶、資源群組和資源的擁有者 (和使用者存取管理員) 可以建立自訂角色以在這些範圍中使用。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="8a0cf-142">hello 使用者建立 hello 角色需要 toobe 無法 tooperform`Microsoft.Authorization/roleDefinition/write`作業上所有的 hello **AssignableScopes**的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="8a0cf-143">誰可以修改自訂角色？</span><span class="sxs-lookup"><span data-stu-id="8a0cf-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="8a0cf-144">訂用帳戶、資源群組和資源的擁有者 (和使用者存取管理員) 可以在這些範圍中修改自訂角色。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="8a0cf-145">使用者需要 toobe 無法 tooperform hello`Microsoft.Authorization/roleDefinition/write`作業上所有的 hello **AssignableScopes**的自訂安全性角色。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="8a0cf-146">誰可以檢視自訂角色？</span><span class="sxs-lookup"><span data-stu-id="8a0cf-146">Who can view custom roles?</span></span>
    <span data-ttu-id="8a0cf-147">Azure RBAC 中的所有內建角色允許檢視可用於指派的角色。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="8a0cf-148">使用者可以執行 hello`Microsoft.Authorization/roleDefinition/read`在範圍內的作業可以檢視 hello RBAC 角色可供在該範圍的指派。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="8a0cf-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8a0cf-149">See also</span></span>
* <span data-ttu-id="8a0cf-150">[Role Based Access Control](role-based-access-control-configure.md)： 開始使用 RBAC hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="8a0cf-151">了解 toomanage 與的存取方式：</span><span class="sxs-lookup"><span data-stu-id="8a0cf-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="8a0cf-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a0cf-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="8a0cf-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8a0cf-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="8a0cf-154">REST API</span><span class="sxs-lookup"><span data-stu-id="8a0cf-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="8a0cf-155">[內建角色](role-based-access-built-in-roles.md)： 取得標準中 RBAC 的 hello 角色的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8a0cf-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
