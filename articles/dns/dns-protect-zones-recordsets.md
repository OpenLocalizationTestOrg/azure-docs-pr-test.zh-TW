---
title: "保護 DNS 區域和記錄 | Microsoft Docs"
description: "如何在 Microsoft Azure DNS 中保護 DNS 區域和記錄集。"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 0b7040d6273b3a6b85cd55850d596807226b87fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="ba8b3-103">如何保護 DNS 區域和記錄</span><span class="sxs-lookup"><span data-stu-id="ba8b3-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="ba8b3-104">DNS 區域和記錄是重要的資源。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="ba8b3-105">刪除 DNS 區域或甚至只是單一的 DNS 記錄，可能會導致整個服務中斷。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="ba8b3-106">因此，保護重要的 DNS 區域和記錄以防未經授權或意外變更相當重要。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="ba8b3-107">這篇文章說明 Azure DNS 如何讓您保護您的 DNS 區域和記錄免於這類變更。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="ba8b3-108">我們會套用 Azure Resource Manager 提供的兩個強大的安全性功能︰[角色型存取控制](../active-directory/role-based-access-control-what-is.md)和[資源鎖定](../azure-resource-manager/resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="ba8b3-109">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="ba8b3-109">Role-based access control</span></span>

<span data-ttu-id="ba8b3-110">Azure 角色型存取控制 (RBAC) 可以對 Azure 使用者、群組和資源進行更細緻的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="ba8b3-111">使用 RBAC，您可以準確地授與使用者執行其作業所需的存取權。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="ba8b3-112">如需有關 RBAC 如何協助您管理存取權的詳細資訊，請參閱[什麼是角色型存取控制](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="ba8b3-113">「DNS 區域參與者」角色</span><span class="sxs-lookup"><span data-stu-id="ba8b3-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="ba8b3-114">「DNS 區域參與者」角色是內建角色，由 Azure 提供用於管理 DNS 資源。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="ba8b3-115">將「DNS 區域參與者」權限指派給使用者或群組，可讓該群組管理 DNS 資源，但是無法管理任何其他類型的資源。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="ba8b3-116">例如，假設資源群組 'myzones' 包含 Contoso Corporation 的五個區域。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="ba8b3-117">將該資源群組的「DNS 區域參與者」權限授與 DNS 系統管理員，可讓他們具有這些 DNS 區域的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="ba8b3-118">它也可避免授與不必要的權限，例如 DNS 系統管理員無法建立或停止虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="ba8b3-119">指派 RBAC 權限的最簡單方式是[透過 Azure 入口網站](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="ba8b3-120">開啟資源群組的 [存取控制 (IAM)] 刀鋒視窗，按一下 [新增]、選取 [DNS 區域參與者] 角色，然後選取必要的使用者或群組以授與權限。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![透過 Azure 入口網站的資源群組層級 RBAC](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="ba8b3-122">權限也可以[使用 Azure PowerShell 授與](../active-directory/role-based-access-control-manage-access-powershell.md)：</span><span class="sxs-lookup"><span data-stu-id="ba8b3-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="ba8b3-123">對等的命令也可以[透過 Azure CLI 使用](../active-directory/role-based-access-control-manage-access-azure-cli.md)：</span><span class="sxs-lookup"><span data-stu-id="ba8b3-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="ba8b3-124">區域層級 RBAC</span><span class="sxs-lookup"><span data-stu-id="ba8b3-124">Zone level RBAC</span></span>

<span data-ttu-id="ba8b3-125">Azure RBAC 規則可以套用至訂用帳戶、資源群組或個別資源。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="ba8b3-126">在 Azure DNS 的情況下，該資源可以是個別 DNS 區域或甚至是個別記錄集。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="ba8b3-127">例如，假設資源群組 'myzones' 包含區域 'contoso.com' 和子區域 'customers.contoso.com'，其中 CNAME 記錄是針對每個客戶帳戶建立的。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="ba8b3-128">用來管理這些 CNAME 記錄的帳戶應該獲得指派權限以僅在 'customers.contoso.com' 區域中建立記錄，它不應該有其他區域的存取權。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="ba8b3-129">區域層級 RBAC 權限可以透過 Azure 入口網站授與。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="ba8b3-130">開啟區域的 [存取控制 (IAM)] 刀鋒視窗，按一下 [新增]、選取 [DNS 區域參與者] 角色，然後選取必要的使用者或群組以授與權限。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![透過 Azure 入口網站的 DNS 區域層級 RBAC](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="ba8b3-132">權限也可以[使用 Azure PowerShell 授與](../active-directory/role-based-access-control-manage-access-powershell.md)：</span><span class="sxs-lookup"><span data-stu-id="ba8b3-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="ba8b3-133">對等的命令也可以[透過 Azure CLI 使用](../active-directory/role-based-access-control-manage-access-azure-cli.md)：</span><span class="sxs-lookup"><span data-stu-id="ba8b3-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="ba8b3-134">記錄集層級 RBAC</span><span class="sxs-lookup"><span data-stu-id="ba8b3-134">Record set level RBAC</span></span>

<span data-ttu-id="ba8b3-135">我們可以繼續下一步。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-135">We can go one step further.</span></span> <span data-ttu-id="ba8b3-136">請考慮 Contoso Corporation 的郵件系統管理員，他需要存取位於 'contoso.com' 區域頂點的 MX 和 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="ba8b3-137">她不需要存取任何其他 MX 或 TXT 記錄，或任何其他類型的任何記錄。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="ba8b3-138">Azure DNS 可讓您在記錄集層級指派權限，準確地給予郵件系統管理員需要存取的記錄。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="ba8b3-139">郵件系統管理員準確地獲得她需要的控制權，且無法進行任何其他變更。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="ba8b3-140">記錄集層級 RBAC 權限可透過 Azure 入口網站，使用記錄集刀鋒視窗中的 [使用者] 按鈕來設定︰</span><span class="sxs-lookup"><span data-stu-id="ba8b3-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![透過 Azure 入口網站的記錄集層級 RBAC](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="ba8b3-142">記錄集層級 RBAC 權限也可以[使用 Azure PowerShell 授與](../active-directory/role-based-access-control-manage-access-powershell.md)：</span><span class="sxs-lookup"><span data-stu-id="ba8b3-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="ba8b3-143">對等的命令也可以[透過 Azure CLI 使用](../active-directory/role-based-access-control-manage-access-azure-cli.md)：</span><span class="sxs-lookup"><span data-stu-id="ba8b3-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="ba8b3-144">自訂角色</span><span class="sxs-lookup"><span data-stu-id="ba8b3-144">Custom roles</span></span>

<span data-ttu-id="ba8b3-145">內建「DNS 區域參與者」角色可以有 DNS 資源的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="ba8b3-146">此外，也可以建置自己的客戶 Azure 角色，以提供更細微的控制。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="ba8b3-147">請再考量一次區域 'customers.contoso.com' 中的 CNAME 記錄是針對每個 Contoso Corporation 客戶帳戶建立的範例。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="ba8b3-148">用來管理這些 CNAME 的帳戶應該授與只管理 CNAME 記錄的權限。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="ba8b3-149">如此便無法修改其他類型的記錄 (例如變更 MX 記錄)，或執行區域層級作業，例如區域刪除。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="ba8b3-150">下列範例示範只管理 CNAME 記錄的自訂角色定義︰</span><span class="sxs-lookup"><span data-stu-id="ba8b3-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

<span data-ttu-id="ba8b3-151">Actions 屬性會定義下列 DNS 特定權限︰</span><span class="sxs-lookup"><span data-stu-id="ba8b3-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="ba8b3-152">`Microsoft.Network/dnsZones/CNAME/*` 授與 CNAME 記錄的完整控制權</span><span class="sxs-lookup"><span data-stu-id="ba8b3-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="ba8b3-153">`Microsoft.Network/dnsZones/read` 授與權限以讀取 DNS 區域，但無法修改它們，讓您查看在其中建立 CNAME 的區域。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="ba8b3-154">剩餘的動作會從 [DNS 區域參與者內建角色](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor)複製。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="ba8b3-155">使用自訂 RBAC 角色，以避免刪除記錄集，同時仍然允許更新它們不是有效的控制。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="ba8b3-156">它會防止記錄集被刪除，但它不會防止它們被修改。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="ba8b3-157">允許的修改包括從記錄集新增和移除記錄，包括移除所有記錄以保持「空白」記錄集。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="ba8b3-158">這與從 DNS 解析觀點來刪除記錄集有相同的效果。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="ba8b3-159">目前無法透過 Azure 入口網站定義自訂角色定義。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="ba8b3-160">可以使用 Azure PowerShell 建立根據此角色定義的自訂角色︰</span><span class="sxs-lookup"><span data-stu-id="ba8b3-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="ba8b3-161">也可以透過 Azure CLI 建立︰</span><span class="sxs-lookup"><span data-stu-id="ba8b3-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="ba8b3-162">然後可以使用與內建角色相同的方式指派角色，如本文稍早所述。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="ba8b3-163">如需有關如何建立、管理及指派自訂角色的詳細資訊，請參閱[在 Azure RBAC 中自訂角色](../active-directory/role-based-access-control-custom-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="ba8b3-164">資源鎖定</span><span class="sxs-lookup"><span data-stu-id="ba8b3-164">Resource locks</span></span>

<span data-ttu-id="ba8b3-165">除了 RBAC，Azure Resource Manager 支援另一種安全性控制項，也就是「鎖定」資源的能力。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="ba8b3-166">其中 RBAC 規則可讓您控制特定使用者和群組的動作，資源鎖定會套用至資源，而且對於所有使用者和角色都有效。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="ba8b3-167">如需詳細資訊，請參閱 [使用 Azure 資源管理員來鎖定資源](../azure-resource-manager/resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="ba8b3-168">有兩種類型的資源鎖定︰**DoNotDelete** 和 **ReadOnly**。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="ba8b3-169">這些可以套用至 DNS 區域，或個別的記錄集。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="ba8b3-170">下列章節說明幾個常見的案例，以及如何使用資源鎖定進行支援。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="ba8b3-171">保護免於所有變更</span><span class="sxs-lookup"><span data-stu-id="ba8b3-171">Protecting against all changes</span></span>

<span data-ttu-id="ba8b3-172">若要避免任何變更，將 ReadOnly 鎖定套用至區域。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="ba8b3-173">這樣可以防止建立新的記錄集，現有記錄集也能免於遭到修改或刪除。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="ba8b3-174">可以透過 Azure 入口網站來建立區域層級資源鎖定。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="ba8b3-175">從 DNS 區域刀鋒視窗中，按一下 [鎖定]，然後按一下 [新增]：</span><span class="sxs-lookup"><span data-stu-id="ba8b3-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![透過 Azure 入口網站的區域層級資源鎖定](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="ba8b3-177">也可以透過 Azure PowerShell 來建立區域層級資源鎖定：</span><span class="sxs-lookup"><span data-stu-id="ba8b3-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="ba8b3-178">設定 Azure 資源鎖定目前無法透過 Azure CLI 獲得支援。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="ba8b3-179">保護個別記錄</span><span class="sxs-lookup"><span data-stu-id="ba8b3-179">Protecting individual records</span></span>

<span data-ttu-id="ba8b3-180">若要防止現有 DNS 記錄集遭到修改，請將 ReadOnly 鎖定套用至記錄集。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8b3-181">將 DoNotDelete 鎖定套用至記錄集不是有效的控制。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="ba8b3-182">它會防止記錄集被刪除，但它不會防止它被修改。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="ba8b3-183">允許的修改包括從記錄集新增和移除記錄，包括移除所有記錄以保持「空白」記錄集。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="ba8b3-184">這與從 DNS 解析觀點來刪除記錄集有相同的效果。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="ba8b3-185">記錄集層級資源鎖定目前只能使用 Azure PowerShell 進行設定。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="ba8b3-186">在 Azure 入口網站或 Azure CLI 不支援。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="ba8b3-187">防止區域刪除</span><span class="sxs-lookup"><span data-stu-id="ba8b3-187">Protecting against zone deletion</span></span>

<span data-ttu-id="ba8b3-188">在 Azure DNS 中刪除區域時，也會一併刪除區域中的所有記錄集。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="ba8b3-189">此作業無法復原。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-189">This operation cannot be undone.</span></span>  <span data-ttu-id="ba8b3-190">不小心刪除重要區域，可能會對業務造成嚴重影響。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="ba8b3-191">因此，防止意外區域刪除非常重要。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="ba8b3-192">將 DoNotDelete 鎖定套用至區域可防止區域刪除。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="ba8b3-193">不過，因為鎖定會由子資源繼承，也會防止區域中任何記錄集遭到刪除，這可能不是想要的結果。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="ba8b3-194">此外，如以上所述，因為記錄仍然可以從現有的記錄集移除，所以它是無效的。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="ba8b3-195">另外，請考慮將 DoNotDelete 鎖定套用至區域中的記錄集，例如 SOA 記錄集。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="ba8b3-196">因為在未刪除記錄集的情況下無法刪除區域，這樣可以防止區域刪除，同時讓區域內的記錄集可以自由地被修改。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="ba8b3-197">如果嘗試刪除區域，Azure Resource Manager 會偵測到這樣也會刪除 SOA 記錄集，並且封鎖呼叫，因為 SOA 已被鎖定。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="ba8b3-198">不會刪除任何記錄集。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-198">No record sets are deleted.</span></span>

<span data-ttu-id="ba8b3-199">下列 PowerShell 命令會針對指定區域的 SOA 記錄建立 DoNotDelete 鎖定︰</span><span class="sxs-lookup"><span data-stu-id="ba8b3-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="ba8b3-200">防止意外區域刪除的另一個方法是使用自訂的角色來確保用來管理您的區域的操作員和服務帳戶不具備區域刪除權限。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="ba8b3-201">真的需要刪除區域時，您可以強制執行兩個步驟刪除，先授與區域刪除權限 (在區域範圍，以防止刪除錯誤的區域)，然後其次刪除區域。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="ba8b3-202">這個第二個方法的優點是適用於這些帳戶存取的所有區域，而不需記得建立任何鎖定。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="ba8b3-203">它的缺點則是具有區域刪除權限的任何帳戶，例如訂用帳戶擁有者仍可能不小心刪除重要區域。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="ba8b3-204">可以同時使用這兩種方法 - 資源鎖定和自訂角色，做為 DNS 區域保護的深度防禦方法。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba8b3-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba8b3-205">Next steps</span></span>

* <span data-ttu-id="ba8b3-206">如需使用 RBAC 的詳細資訊，請參閱[開始使用 Azure 入口網站中的存取管理](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="ba8b3-207">如需使用資源鎖定的詳細資訊，請參閱[使用 Azure Resource Manager 鎖定資源](../azure-resource-manager/resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="ba8b3-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

