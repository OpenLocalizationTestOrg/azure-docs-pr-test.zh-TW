---
title: "aaaProtecting DNS 區域與記錄 |Microsoft 文件"
description: "如何 tooprotect DNS 區域與記錄設定 Microsoft Azure DNS。"
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
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="5946f-103">Tooprotect DNS 區域的方式，以及記錄</span><span class="sxs-lookup"><span data-stu-id="5946f-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="5946f-104">DNS 區域和記錄是重要的資源。</span><span class="sxs-lookup"><span data-stu-id="5946f-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="5946f-105">刪除 DNS 區域或甚至只是單一的 DNS 記錄，可能會導致整個服務中斷。</span><span class="sxs-lookup"><span data-stu-id="5946f-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="5946f-106">因此，保護重要的 DNS 區域和記錄以防未經授權或意外變更相當重要。</span><span class="sxs-lookup"><span data-stu-id="5946f-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="5946f-107">本文說明如何 Azure DNS 可讓您 tooprotect 您的 DNS 區域和對這類變更的記錄。</span><span class="sxs-lookup"><span data-stu-id="5946f-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="5946f-108">我們會套用 Azure Resource Manager 提供的兩個強大的安全性功能︰[角色型存取控制](../active-directory/role-based-access-control-what-is.md)和[資源鎖定](../azure-resource-manager/resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="5946f-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="5946f-109">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="5946f-109">Role-based access control</span></span>

<span data-ttu-id="5946f-110">Azure 角色型存取控制 (RBAC) 可以對 Azure 使用者、群組和資源進行更細緻的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="5946f-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="5946f-111">使用 RBAC，您可以授與明確地說 hello 少量的存取權，使用者需要 tooperform 他們的工作。</span><span class="sxs-lookup"><span data-stu-id="5946f-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="5946f-112">如需有關 RBAC 如何協助您管理存取權的詳細資訊，請參閱[什麼是角色型存取控制](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="5946f-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="5946f-113">hello 'DNS 區域參與者' 角色</span><span class="sxs-lookup"><span data-stu-id="5946f-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="5946f-114">hello 'DNS 區域參與者' 角色是由 Azure 提供用於管理 DNS 資源的內建角色。</span><span class="sxs-lookup"><span data-stu-id="5946f-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="5946f-115">DNS 區域的參與者權限 tooa 使用者或群組指派可讓該群組 toomanage DNS 資源，但沒有任何其他類型的資源。</span><span class="sxs-lookup"><span data-stu-id="5946f-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="5946f-116">例如，假設 hello 資源群組 'myzones' Contoso Corporation 包含五個區域。</span><span class="sxs-lookup"><span data-stu-id="5946f-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="5946f-117">授與 hello DNS 系統管理員 DNS 區域參與者 ' 的權限 toothat 資源群組，可讓這些 DNS 區域的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="5946f-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="5946f-118">它也可避免授與不必要的權限，例如 hello DNS 系統管理員無法建立或停止虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5946f-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="5946f-119">hello 最簡單方式 tooassign RBAC 權限是[hello Azure 入口網站透過](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="5946f-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="5946f-120">開啟 hello [存取控制 (IAM)] 刀鋒視窗中的 hello 資源群組，然後按一下 [加入]，然後選取 hello 'DNS 區域參與者' 角色和所需的 hello 選取使用者或群組 toogrant 權限。</span><span class="sxs-lookup"><span data-stu-id="5946f-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![資源群組層級 RBAC 透過 hello Azure 入口網站](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="5946f-122">權限也可以[使用 Azure PowerShell 授與](../active-directory/role-based-access-control-manage-access-powershell.md)：</span><span class="sxs-lookup"><span data-stu-id="5946f-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="5946f-123">hello 等命令也是[可透過 hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="5946f-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="5946f-124">區域層級 RBAC</span><span class="sxs-lookup"><span data-stu-id="5946f-124">Zone level RBAC</span></span>

<span data-ttu-id="5946f-125">Azure RBAC 規則可以套用的 tooa 訂閱的資源群組或 tooan 個別資源。</span><span class="sxs-lookup"><span data-stu-id="5946f-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="5946f-126">在 Azure DNS 的 hello 情況下，該資源可以是個別的 DNS 區域或甚至個別資料錄集。</span><span class="sxs-lookup"><span data-stu-id="5946f-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="5946f-127">例如，假設 hello 資源群組 'myzones' 包含 hello 區域 'contoso.com' 和 subzone 'customers.contoso.com' 所在的每個客戶帳戶建立 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="5946f-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="5946f-128">hello 使用帳戶 toomanage 這些 CNAME 記錄應指派權限 toocreate 記錄只有 hello 'customers.contoso.com' 區域中的，不應該存取 toohello 其他區域。</span><span class="sxs-lookup"><span data-stu-id="5946f-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="5946f-129">區域層級 RBAC 權限可以授與透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5946f-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="5946f-130">開啟 hello hello 區域的 [存取控制 (IAM)] 刀鋒視窗，然後按一下 [加入]，然後選取 hello 'DNS 區域參與者' 角色和所需的 hello 選取使用者或群組 toogrant 權限。</span><span class="sxs-lookup"><span data-stu-id="5946f-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![透過 hello Azure 入口網站的 DNS 區域層級 RBAC](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="5946f-132">權限也可以[使用 Azure PowerShell 授與](../active-directory/role-based-access-control-manage-access-powershell.md)：</span><span class="sxs-lookup"><span data-stu-id="5946f-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="5946f-133">hello 等命令也是[可透過 hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="5946f-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="5946f-134">記錄集層級 RBAC</span><span class="sxs-lookup"><span data-stu-id="5946f-134">Record set level RBAC</span></span>

<span data-ttu-id="5946f-135">我們可以繼續下一步。</span><span class="sxs-lookup"><span data-stu-id="5946f-135">We can go one step further.</span></span> <span data-ttu-id="5946f-136">請考慮 hello 的郵件管理員 Contoso Corporation 針對需要存取 toohello MX 並在 hello 區域的 hello 'contoso.com' 區域的 apex TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="5946f-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="5946f-137">她不需要存取 tooany 其他 MX 或 TXT 記錄或任何其他型別的 tooany 記錄。</span><span class="sxs-lookup"><span data-stu-id="5946f-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="5946f-138">Azure DNS 可讓您在 hello 記錄集層級，tooprecisely hello 記錄 hello 的郵件管理員 tooassign 權限需要存取。</span><span class="sxs-lookup"><span data-stu-id="5946f-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="5946f-139">hello 郵件系統管理員將獲得精確 hello 控制她必須，而且無法 toomake 任何其他變更。</span><span class="sxs-lookup"><span data-stu-id="5946f-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="5946f-140">記錄集層級 RBAC 權限可以透過 Azure 入口網站，使用 hello 記錄集刀鋒視窗中的 hello 'Users' 按鈕 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="5946f-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![設定記錄層級 RBAC 透過 hello Azure 入口網站](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="5946f-142">記錄集層級 RBAC 權限也可以[使用 Azure PowerShell 授與](../active-directory/role-based-access-control-manage-access-powershell.md)：</span><span class="sxs-lookup"><span data-stu-id="5946f-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="5946f-143">hello 等命令也是[可透過 hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="5946f-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="5946f-144">自訂角色</span><span class="sxs-lookup"><span data-stu-id="5946f-144">Custom roles</span></span>

<span data-ttu-id="5946f-145">hello 內建的 DNS 區域參與者 ' 角色可讓 DNS 資源的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="5946f-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="5946f-146">它也是可能 toobuild 自己客戶的 Azure 角色、 tooprovide 更精細的控制。</span><span class="sxs-lookup"><span data-stu-id="5946f-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="5946f-147">請再次考量在 hello 區域 'customers.contoso.com' CNAME 記錄建立的每個 Contoso Corporation 客戶帳戶所在的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="5946f-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="5946f-148">hello 使用帳戶 toomanage 這些 Cname 應該被授與的權限 toomanage CNAME 的記錄。</span><span class="sxs-lookup"><span data-stu-id="5946f-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="5946f-149">它是則其他無法 toomodify 記錄類型 （例如變更 MX 記錄），或執行區域層級作業，例如區域刪除。</span><span class="sxs-lookup"><span data-stu-id="5946f-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="5946f-150">hello 下列範例顯示自訂角色定義，用於管理 CNAME 的記錄：</span><span class="sxs-lookup"><span data-stu-id="5946f-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="5946f-151">hello 動作屬性會定義下列 DNS 特定權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="5946f-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="5946f-152">`Microsoft.Network/dnsZones/CNAME/*` 授與 CNAME 記錄的完整控制權</span><span class="sxs-lookup"><span data-stu-id="5946f-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="5946f-153">`Microsoft.Network/dnsZones/read`授與權限 tooread DNS 區域，但 toomodify 它們，讓您 toosee hello 的區域中的 hello 正在建立 CNAME。</span><span class="sxs-lookup"><span data-stu-id="5946f-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="5946f-154">其餘的動作會從 hello 複製的 hello [DNS 區域參與者內建角色](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor)。</span><span class="sxs-lookup"><span data-stu-id="5946f-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="5946f-155">使用自訂的 RBAC 角色 tooprevent，刪除資料錄集時仍允許它們 toobe 更新不是有效的控制。</span><span class="sxs-lookup"><span data-stu-id="5946f-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="5946f-156">它會防止記錄集被刪除，但它不會防止它們被修改。</span><span class="sxs-lookup"><span data-stu-id="5946f-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="5946f-157">允許的修改包括新增和移除 hello 資料錄集，包括移除所有記錄記錄 tooleave 'empty' 的記錄組。</span><span class="sxs-lookup"><span data-stu-id="5946f-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="5946f-158">這會有相同的效果刪除 hello 記錄設定從 DNS 解析觀點來看 hello。</span><span class="sxs-lookup"><span data-stu-id="5946f-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="5946f-159">目前無法透過 Azure 入口網站 hello 定義自訂角色定義。</span><span class="sxs-lookup"><span data-stu-id="5946f-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="5946f-160">可以使用 Azure PowerShell 建立根據此角色定義的自訂角色︰</span><span class="sxs-lookup"><span data-stu-id="5946f-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="5946f-161">它也可以建立透過 hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="5946f-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="5946f-162">hello 角色可以再指派 hello 以相同方式做為內建的角色，如本文稍早所述。</span><span class="sxs-lookup"><span data-stu-id="5946f-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="5946f-163">如需有關如何 toocreate、 管理及指派自訂的角色，請參閱[Azure rbac 進行中的自訂角色](../active-directory/role-based-access-control-custom-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="5946f-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="5946f-164">資源鎖定</span><span class="sxs-lookup"><span data-stu-id="5946f-164">Resource locks</span></span>

<span data-ttu-id="5946f-165">在加法 tooRBAC Azure 資源管理員支援其他類型的安全性控制，也就是 hello 能力 too'lock' 的資源。</span><span class="sxs-lookup"><span data-stu-id="5946f-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="5946f-166">RBAC 規則可讓您 toocontrol hello 動作的特定使用者和群組，資源鎖定會套用的 toohello 資源，並跨所有使用者和角色會生效。</span><span class="sxs-lookup"><span data-stu-id="5946f-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="5946f-167">如需詳細資訊，請參閱[使用 Azure Resource Manager 來鎖定資源](../azure-resource-manager/resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="5946f-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="5946f-168">有兩種類型的資源鎖定︰**DoNotDelete** 和 **ReadOnly**。</span><span class="sxs-lookup"><span data-stu-id="5946f-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="5946f-169">套用這些 tooa DNS 區域或 tooan 個別的資料錄集。</span><span class="sxs-lookup"><span data-stu-id="5946f-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="5946f-170">hello 下列各節說明幾個常見的案例，以及如何 toosupport 它們使用資源的鎖定。</span><span class="sxs-lookup"><span data-stu-id="5946f-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="5946f-171">保護免於所有變更</span><span class="sxs-lookup"><span data-stu-id="5946f-171">Protecting against all changes</span></span>

<span data-ttu-id="5946f-172">tooprevent 任何正在進行變更，將 ReadOnly 鎖定 toohello zone 套用。</span><span class="sxs-lookup"><span data-stu-id="5946f-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="5946f-173">這樣可以防止建立新的記錄集，現有記錄集也能免於遭到修改或刪除。</span><span class="sxs-lookup"><span data-stu-id="5946f-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="5946f-174">透過 hello Azure 入口網站，就可以建立區域層級的資源鎖定。</span><span class="sxs-lookup"><span data-stu-id="5946f-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="5946f-175">從 hello DNS 區域刀鋒視窗中，按一下 '鎖定'，然後 'Add':</span><span class="sxs-lookup"><span data-stu-id="5946f-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![透過 hello Azure 入口網站的區域層級的資源鎖定](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="5946f-177">也可以透過 Azure PowerShell 來建立區域層級資源鎖定：</span><span class="sxs-lookup"><span data-stu-id="5946f-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="5946f-178">設定 Azure 資源鎖定目前不支援透過 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="5946f-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="5946f-179">保護個別記錄</span><span class="sxs-lookup"><span data-stu-id="5946f-179">Protecting individual records</span></span>

<span data-ttu-id="5946f-180">tooprevent 現有的 DNS 記錄修改，針對設定適用於唯讀鎖定 toohello 記錄集。</span><span class="sxs-lookup"><span data-stu-id="5946f-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="5946f-181">套用 DoNotDelete 鎖定 tooa 記錄集不是有效的控制。</span><span class="sxs-lookup"><span data-stu-id="5946f-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="5946f-182">它會阻止 hello 記錄集被刪除，但它無法防止其遭到修改。</span><span class="sxs-lookup"><span data-stu-id="5946f-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="5946f-183">允許的修改包括新增和移除 hello 資料錄集，包括移除所有記錄記錄 tooleave 'empty' 的記錄組。</span><span class="sxs-lookup"><span data-stu-id="5946f-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="5946f-184">這會有相同的效果刪除 hello 記錄設定從 DNS 解析觀點來看 hello。</span><span class="sxs-lookup"><span data-stu-id="5946f-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="5946f-185">記錄集層級資源鎖定目前只能使用 Azure PowerShell 進行設定。</span><span class="sxs-lookup"><span data-stu-id="5946f-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="5946f-186">它們不適用於 hello Azure 入口網站或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="5946f-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="5946f-187">防止區域刪除</span><span class="sxs-lookup"><span data-stu-id="5946f-187">Protecting against zone deletion</span></span>

<span data-ttu-id="5946f-188">Azure DNS 中刪除區域時，也會一併刪除 hello 區域中的所有資料錄集。</span><span class="sxs-lookup"><span data-stu-id="5946f-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="5946f-189">此作業無法復原。</span><span class="sxs-lookup"><span data-stu-id="5946f-189">This operation cannot be undone.</span></span>  <span data-ttu-id="5946f-190">不小心刪除重要區域具有 hello 潛在 toohave 重要商業影響。</span><span class="sxs-lookup"><span data-stu-id="5946f-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="5946f-191">因此，這是非常重要 tooprotect 意外區域刪除。</span><span class="sxs-lookup"><span data-stu-id="5946f-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="5946f-192">套用 DoNotDelete 鎖定 tooa 區域可防止 hello 區域刪除。</span><span class="sxs-lookup"><span data-stu-id="5946f-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="5946f-193">不過，因為鎖定會繼承子資源，也無法 hello 」 區域中刪除，但可能不是任何資料錄集。</span><span class="sxs-lookup"><span data-stu-id="5946f-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="5946f-194">此外，上面的 hello 附註所述，它也是沒有效率因為仍然可以從現有的記錄集 hello 移除記錄。</span><span class="sxs-lookup"><span data-stu-id="5946f-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="5946f-195">或者，請考慮在 hello 區域，例如 hello SOA 記錄集套用 DoNotDelete 鎖定 tooa 記錄設定。</span><span class="sxs-lookup"><span data-stu-id="5946f-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="5946f-196">無法刪除 hello 區域，但不會也刪除 hello 資料錄集，因為這樣可防止區域刪除，同時，仍允許自由修改 hello 區域 toobe 內的記錄集。</span><span class="sxs-lookup"><span data-stu-id="5946f-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="5946f-197">如果嘗試 toodelete hello 區域，Azure 資源管理員偵測到這也可能會刪除 hello SOA 記錄集，而且區塊 hello 呼叫，因為已鎖定的 hello SOA。</span><span class="sxs-lookup"><span data-stu-id="5946f-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="5946f-198">不會刪除任何記錄集。</span><span class="sxs-lookup"><span data-stu-id="5946f-198">No record sets are deleted.</span></span>

<span data-ttu-id="5946f-199">hello 下列 PowerShell 命令會建立針對 hello SOA 記錄指定區域的 hello DoNotDelete 鎖定：</span><span class="sxs-lookup"><span data-stu-id="5946f-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="5946f-200">Tooprevent 意外區域刪除則是使用自訂角色 tooensure hello 運算子和服務帳戶使用 toomanage 區域執行不會有區域的另一種方式刪除權限。</span><span class="sxs-lookup"><span data-stu-id="5946f-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="5946f-201">當您需要 toodelete 區域時，您可以強制執行兩個步驟刪除，第一個授與區域刪除範圍的權限 （hello 區域，刪除 hello 錯誤區域 tooprevent） 和第二個 toodelete hello 區域。</span><span class="sxs-lookup"><span data-stu-id="5946f-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="5946f-202">此第二種方法具有它所使用的所有區域，這些帳戶來存取而不需要任何鎖定 tooremember toocreate hello 優點。</span><span class="sxs-lookup"><span data-stu-id="5946f-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="5946f-203">它的任何帳戶與區域刪除權限，例如 hello 訂用帳戶擁有者，可以仍然不小心刪除重要區域的 hello 缺點。</span><span class="sxs-lookup"><span data-stu-id="5946f-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="5946f-204">它是可能 toouse hello 在這兩種方法資源鎖定和自訂角色為相同的時間，為深度防禦方法 tooDNS 區域保護。</span><span class="sxs-lookup"><span data-stu-id="5946f-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5946f-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5946f-205">Next steps</span></span>

* <span data-ttu-id="5946f-206">如需有關使用 RBAC 的詳細資訊，請參閱[開始使用 hello Azure 入口網站中存取管理](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="5946f-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="5946f-207">如需使用資源鎖定的詳細資訊，請參閱[使用 Azure Resource Manager 鎖定資源](../azure-resource-manager/resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="5946f-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

