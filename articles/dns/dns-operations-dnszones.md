---
title: "aaaManage DNS 區域中 Azure DNS-PowerShell |Microsoft 文件"
description: "您可以使用 Azure Powershell 管理 DNS 區域。 本文說明如何刪除 tooupdate，，和 Azure DNS 上建立 DNS 區域"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a>如何使用 PowerShell toomanage DNS 區域

> [!div class="op_single_selector"]
> * [入口網站](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

本文章將示範如何 toomanage 您的 DNS 區域使用 Azure PowerShell。 您也可以管理您的 DNS 區域使用 hello 跨平台[Azure CLI](dns-operations-dnszones-cli.md)或 hello Azure 入口網站。

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>建立 DNS 區域

DNS 區域由使用 hello `New-AzureRmDnsZone` cmdlet。

hello 下列範例會建立 DNS 區域呼叫*contoso.com*呼叫 hello 資源群組中*MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

hello 下列範例示範如何 toocreate DNS 區域具有兩個[Azure 資源管理員標記](dns-zones-records.md#tags)，*專案 = 示範*和*env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>取得 DNS 區域

tooretrieve DNS 區域，使用 hello `Get-AzureRmDnsZone` cmdlet。 此操作會傳回 DNS 區域物件對應 tooan 現有的區域中 Azure DNS。 hello 物件包含有關 hello 區域 （例如 hello 數字的資料錄集），資料，但不是包含本身的 hello 資料錄集 (請參閱`Get-AzureRmDnsRecordSet`)。

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a>列出 DNS 區域

藉由略過從 hello 區域名稱`Get-AzureRmDnsZone`，您可以列舉資源群組中的所有區域。 此作業會傳回一系列的區域物件。

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

藉由略過 hello 區域名稱和 hello 資源群組名稱，從`Get-AzureRmDnsZone`，您可以列舉 hello Azure 訂用帳戶中的所有區域。

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>更新 DNS 區域

變更 DNS 區域資源可使用 tooa `Set-AzureRmDnsZone`。 此 cmdlet 不會更新 hello 區域內 hello DNS 資料錄集 (請參閱[如何 tooManage DNS 記錄](dns-operations-recordsets.md))。 它只有已使用 hello 區域資源本身的 tooupdate 的屬性。 hello 可寫入的區域屬性會限制目前 toohello [Azure 資源管理員 '標記' hello 區域資源](dns-zones-records.md#tags)。

使用下列兩種方式 tooupdate hello 的其中一個 DNS 區域：

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>指定使用 hello 區域名稱和資源群組的 hello 區域

這種方法，取代指定 hello 值 hello 現有區域的標籤。

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>指定使用 $zone 物件 hello 區域

這個方法會擷取 hello 現有區域物件、 修改 hello 標記，並認可 hello 的變更，然後。 如此一來，就可以保留現有的標籤。

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

當使用`Set-AzureRmDnsZone`$zone 物件時， [Etag 檢查](dns-zones-records.md#etags)可用 tooensure 並行的變更不會覆寫。 您可以使用選擇性的 hello`-Overwrite`切換 toosuppress 這些檢查。

## <a name="delete-a-dns-zone"></a>刪除 DNS 區域

您可以使用 hello 刪除 DNS 區域`Remove-AzureRmDnsZone`cmdlet。

> [!NOTE]
> 刪除 DNS 區域時，也會刪除 hello 區域內的所有 DNS 記錄。 此作業無法復原。 如果正在使用中的 hello DNS 區域，使用 hello 區域的服務將無法刪除 hello 區域時。
>
>tooprotect 區域意外刪除，請參閱[tooprotect DNS 區域的方式，以及記錄](dns-protect-zones-recordsets.md)。


使用下列兩種方式 toodelete hello 的其中一個 DNS 區域：

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>指定使用 hello 區域名稱和資源群組名稱的 hello 區域

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>指定使用 $zone 物件 hello 區域

您可以指定使用刪除 hello 區域 toobe`$zone`所傳回物件`Get-AzureRmDnsZone`。

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

hello 區域物件也管線傳遞而不被傳遞做為參數：

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

如同`Set-AzureRmDnsZone`，指定區域使用 hello`$zone`物件的啟用 Etag 檢查 tooensure 並行的變更不會刪除。 使用 hello`-Overwrite`切換 toosuppress 這些檢查。

## <a name="confirmation-prompts"></a>確認提示

hello `New-AzureRmDnsZone`， `Set-AzureRmDnsZone`，和`Remove-AzureRmDnsZone`cmdlet 都支援確認提示。

同時`New-AzureRmDnsZone`和`Set-AzureRmDnsZone`提示您確認如果 hello `$ConfirmPreference` PowerShell 喜好設定變數的值為`Medium`或更低。 由於 toohello 高可能會影響刪除 DNS 區域，hello`Remove-AzureRmDnsZone`指令程式會先提示確認如果 hello `$ConfirmPreference` PowerShell 變數有任何值以外`None`。

因為 hello 預設值為`$ConfirmPreference`是`High`，則只`Remove-AzureRmDnsZone`預設提示確認。

您可以覆寫 hello 目前`$ConfirmPreference`設定使用 hello`-Confirm`參數。 如果您指定`-Confirm`或`-Confirm:$True`，hello cmdlet 會提示您確認再它執行。 如果您指定`-Confirm:$False`，hello cmdlet 不會提示您確認。

如需 `-Confirm` 和 `$ConfirmPreference` 的詳細資訊，請參閱[有關喜好設定變數](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)。

## <a name="next-steps"></a>後續步驟

了解如何太[管理資料錄集 」 和 「 記錄](dns-operations-recordsets.md)DNS 區域中。
<br>
了解如何太[委派您網域 tooAzure DNS](dns-domain-delegation.md)。
<br>
檢閱 hello [Azure DNS PowerShell 參考文件](/powershell/module/azurerm.dns)。

