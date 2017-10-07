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
# <a name="how-tooprotect-dns-zones-and-records"></a>Tooprotect DNS 區域的方式，以及記錄

DNS 區域和記錄是重要的資源。 刪除 DNS 區域或甚至只是單一的 DNS 記錄，可能會導致整個服務中斷。  因此，保護重要的 DNS 區域和記錄以防未經授權或意外變更相當重要。

本文說明如何 Azure DNS 可讓您 tooprotect 您的 DNS 區域和對這類變更的記錄。  我們會套用 Azure Resource Manager 提供的兩個強大的安全性功能︰[角色型存取控制](../active-directory/role-based-access-control-what-is.md)和[資源鎖定](../azure-resource-manager/resource-group-lock-resources.md)。

## <a name="role-based-access-control"></a>角色型存取控制

Azure 角色型存取控制 (RBAC) 可以對 Azure 使用者、群組和資源進行更細緻的存取權管理。 使用 RBAC，您可以授與明確地說 hello 少量的存取權，使用者需要 tooperform 他們的工作。 如需有關 RBAC 如何協助您管理存取權的詳細資訊，請參閱[什麼是角色型存取控制](../active-directory/role-based-access-control-what-is.md)。

### <a name="hello-dns-zone-contributor-role"></a>hello 'DNS 區域參與者' 角色

hello 'DNS 區域參與者' 角色是由 Azure 提供用於管理 DNS 資源的內建角色。  DNS 區域的參與者權限 tooa 使用者或群組指派可讓該群組 toomanage DNS 資源，但沒有任何其他類型的資源。

例如，假設 hello 資源群組 'myzones' Contoso Corporation 包含五個區域。 授與 hello DNS 系統管理員 DNS 區域參與者 ' 的權限 toothat 資源群組，可讓這些 DNS 區域的完整控制權。 它也可避免授與不必要的權限，例如 hello DNS 系統管理員無法建立或停止虛擬機器。

hello 最簡單方式 tooassign RBAC 權限是[hello Azure 入口網站透過](../active-directory/role-based-access-control-configure.md)。  開啟 hello [存取控制 (IAM)] 刀鋒視窗中的 hello 資源群組，然後按一下 [加入]，然後選取 hello 'DNS 區域參與者' 角色和所需的 hello 選取使用者或群組 toogrant 權限。

![資源群組層級 RBAC 透過 hello Azure 入口網站](./media/dns-protect-zones-recordsets/rbac1.png)

權限也可以[使用 Azure PowerShell 授與](../active-directory/role-based-access-control-manage-access-powershell.md)：

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

hello 等命令也是[可透過 hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>區域層級 RBAC

Azure RBAC 規則可以套用的 tooa 訂閱的資源群組或 tooan 個別資源。 在 Azure DNS 的 hello 情況下，該資源可以是個別的 DNS 區域或甚至個別資料錄集。

例如，假設 hello 資源群組 'myzones' 包含 hello 區域 'contoso.com' 和 subzone 'customers.contoso.com' 所在的每個客戶帳戶建立 CNAME 記錄。  hello 使用帳戶 toomanage 這些 CNAME 記錄應指派權限 toocreate 記錄只有 hello 'customers.contoso.com' 區域中的，不應該存取 toohello 其他區域。

區域層級 RBAC 權限可以授與透過 hello Azure 入口網站。  開啟 hello hello 區域的 [存取控制 (IAM)] 刀鋒視窗，然後按一下 [加入]，然後選取 hello 'DNS 區域參與者' 角色和所需的 hello 選取使用者或群組 toogrant 權限。

![透過 hello Azure 入口網站的 DNS 區域層級 RBAC](./media/dns-protect-zones-recordsets/rbac2.png)

權限也可以[使用 Azure PowerShell 授與](../active-directory/role-based-access-control-manage-access-powershell.md)：

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

hello 等命令也是[可透過 hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>記錄集層級 RBAC

我們可以繼續下一步。 請考慮 hello 的郵件管理員 Contoso Corporation 針對需要存取 toohello MX 並在 hello 區域的 hello 'contoso.com' 區域的 apex TXT 記錄。  她不需要存取 tooany 其他 MX 或 TXT 記錄或任何其他型別的 tooany 記錄。  Azure DNS 可讓您在 hello 記錄集層級，tooprecisely hello 記錄 hello 的郵件管理員 tooassign 權限需要存取。  hello 郵件系統管理員將獲得精確 hello 控制她必須，而且無法 toomake 任何其他變更。

記錄集層級 RBAC 權限可以透過 Azure 入口網站，使用 hello 記錄集刀鋒視窗中的 hello 'Users' 按鈕 hello 設定：

![設定記錄層級 RBAC 透過 hello Azure 入口網站](./media/dns-protect-zones-recordsets/rbac3.png)

記錄集層級 RBAC 權限也可以[使用 Azure PowerShell 授與](../active-directory/role-based-access-control-manage-access-powershell.md)：

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

hello 等命令也是[可透過 hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>自訂角色

hello 內建的 DNS 區域參與者 ' 角色可讓 DNS 資源的完整控制權。 它也是可能 toobuild 自己客戶的 Azure 角色、 tooprovide 更精細的控制。

請再次考量在 hello 區域 'customers.contoso.com' CNAME 記錄建立的每個 Contoso Corporation 客戶帳戶所在的 hello 範例。  hello 使用帳戶 toomanage 這些 Cname 應該被授與的權限 toomanage CNAME 的記錄。  它是則其他無法 toomodify 記錄類型 （例如變更 MX 記錄），或執行區域層級作業，例如區域刪除。

hello 下列範例顯示自訂角色定義，用於管理 CNAME 的記錄：

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

hello 動作屬性會定義下列 DNS 特定權限的 hello:

* `Microsoft.Network/dnsZones/CNAME/*` 授與 CNAME 記錄的完整控制權
* `Microsoft.Network/dnsZones/read`授與權限 tooread DNS 區域，但 toomodify 它們，讓您 toosee hello 的區域中的 hello 正在建立 CNAME。

其餘的動作會從 hello 複製的 hello [DNS 區域參與者內建角色](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor)。

> [!NOTE]
> 使用自訂的 RBAC 角色 tooprevent，刪除資料錄集時仍允許它們 toobe 更新不是有效的控制。 它會防止記錄集被刪除，但它不會防止它們被修改。  允許的修改包括新增和移除 hello 資料錄集，包括移除所有記錄記錄 tooleave 'empty' 的記錄組。 這會有相同的效果刪除 hello 記錄設定從 DNS 解析觀點來看 hello。

目前無法透過 Azure 入口網站 hello 定義自訂角色定義。 可以使用 Azure PowerShell 建立根據此角色定義的自訂角色︰

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

它也可以建立透過 hello Azure CLI:

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

hello 角色可以再指派 hello 以相同方式做為內建的角色，如本文稍早所述。

如需有關如何 toocreate、 管理及指派自訂的角色，請參閱[Azure rbac 進行中的自訂角色](../active-directory/role-based-access-control-custom-roles.md)。

## <a name="resource-locks"></a>資源鎖定

在加法 tooRBAC Azure 資源管理員支援其他類型的安全性控制，也就是 hello 能力 too'lock' 的資源。 RBAC 規則可讓您 toocontrol hello 動作的特定使用者和群組，資源鎖定會套用的 toohello 資源，並跨所有使用者和角色會生效。 如需詳細資訊，請參閱[使用 Azure Resource Manager 來鎖定資源](../azure-resource-manager/resource-group-lock-resources.md)。

有兩種類型的資源鎖定︰**DoNotDelete** 和 **ReadOnly**。 套用這些 tooa DNS 區域或 tooan 個別的資料錄集。  hello 下列各節說明幾個常見的案例，以及如何 toosupport 它們使用資源的鎖定。

### <a name="protecting-against-all-changes"></a>保護免於所有變更

tooprevent 任何正在進行變更，將 ReadOnly 鎖定 toohello zone 套用。  這樣可以防止建立新的記錄集，現有記錄集也能免於遭到修改或刪除。

透過 hello Azure 入口網站，就可以建立區域層級的資源鎖定。  從 hello DNS 區域刀鋒視窗中，按一下 '鎖定'，然後 'Add':

![透過 hello Azure 入口網站的區域層級的資源鎖定](./media/dns-protect-zones-recordsets/locks1.png)

也可以透過 Azure PowerShell 來建立區域層級資源鎖定：

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

設定 Azure 資源鎖定目前不支援透過 hello Azure CLI。

### <a name="protecting-individual-records"></a>保護個別記錄

tooprevent 現有的 DNS 記錄修改，針對設定適用於唯讀鎖定 toohello 記錄集。

> [!NOTE]
> 套用 DoNotDelete 鎖定 tooa 記錄集不是有效的控制。 它會阻止 hello 記錄集被刪除，但它無法防止其遭到修改。  允許的修改包括新增和移除 hello 資料錄集，包括移除所有記錄記錄 tooleave 'empty' 的記錄組。 這會有相同的效果刪除 hello 記錄設定從 DNS 解析觀點來看 hello。

記錄集層級資源鎖定目前只能使用 Azure PowerShell 進行設定。  它們不適用於 hello Azure 入口網站或 Azure CLI。

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>防止區域刪除

Azure DNS 中刪除區域時，也會一併刪除 hello 區域中的所有資料錄集。  此作業無法復原。  不小心刪除重要區域具有 hello 潛在 toohave 重要商業影響。  因此，這是非常重要 tooprotect 意外區域刪除。

套用 DoNotDelete 鎖定 tooa 區域可防止 hello 區域刪除。  不過，因為鎖定會繼承子資源，也無法 hello 」 區域中刪除，但可能不是任何資料錄集。  此外，上面的 hello 附註所述，它也是沒有效率因為仍然可以從現有的記錄集 hello 移除記錄。

或者，請考慮在 hello 區域，例如 hello SOA 記錄集套用 DoNotDelete 鎖定 tooa 記錄設定。  無法刪除 hello 區域，但不會也刪除 hello 資料錄集，因為這樣可防止區域刪除，同時，仍允許自由修改 hello 區域 toobe 內的記錄集。 如果嘗試 toodelete hello 區域，Azure 資源管理員偵測到這也可能會刪除 hello SOA 記錄集，而且區塊 hello 呼叫，因為已鎖定的 hello SOA。  不會刪除任何記錄集。

hello 下列 PowerShell 命令會建立針對 hello SOA 記錄指定區域的 hello DoNotDelete 鎖定：

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

Tooprevent 意外區域刪除則是使用自訂角色 tooensure hello 運算子和服務帳戶使用 toomanage 區域執行不會有區域的另一種方式刪除權限。 當您需要 toodelete 區域時，您可以強制執行兩個步驟刪除，第一個授與區域刪除範圍的權限 （hello 區域，刪除 hello 錯誤區域 tooprevent） 和第二個 toodelete hello 區域。

此第二種方法具有它所使用的所有區域，這些帳戶來存取而不需要任何鎖定 tooremember toocreate hello 優點。 它的任何帳戶與區域刪除權限，例如 hello 訂用帳戶擁有者，可以仍然不小心刪除重要區域的 hello 缺點。

它是可能 toouse hello 在這兩種方法資源鎖定和自訂角色為相同的時間，為深度防禦方法 tooDNS 區域保護。

## <a name="next-steps"></a>後續步驟

* 如需有關使用 RBAC 的詳細資訊，請參閱[開始使用 hello Azure 入口網站中存取管理](../active-directory/role-based-access-control-what-is.md)。
* 如需使用資源鎖定的詳細資訊，請參閱[使用 Azure Resource Manager 鎖定資源](../azure-resource-manager/resource-group-lock-resources.md)。

