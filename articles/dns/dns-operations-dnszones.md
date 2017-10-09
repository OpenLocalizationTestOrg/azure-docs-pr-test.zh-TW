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
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="4e534-104">如何使用 PowerShell toomanage DNS 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e534-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="4e534-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="4e534-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e534-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="4e534-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4e534-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="4e534-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4e534-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="4e534-109">本文章將示範如何 toomanage 您的 DNS 區域使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4e534-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="4e534-110">您也可以管理您的 DNS 區域使用 hello 跨平台[Azure CLI](dns-operations-dnszones-cli.md)或 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4e534-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="4e534-111">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-111">Create a DNS zone</span></span>

<span data-ttu-id="4e534-112">DNS 區域由使用 hello `New-AzureRmDnsZone` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4e534-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="4e534-113">hello 下列範例會建立 DNS 區域呼叫*contoso.com*呼叫 hello 資源群組中*MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="4e534-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="4e534-114">hello 下列範例示範如何 toocreate DNS 區域具有兩個[Azure 資源管理員標記](dns-zones-records.md#tags)，*專案 = 示範*和*env = test*:</span><span class="sxs-lookup"><span data-stu-id="4e534-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="4e534-115">取得 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-115">Get a DNS zone</span></span>

<span data-ttu-id="4e534-116">tooretrieve DNS 區域，使用 hello `Get-AzureRmDnsZone` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4e534-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="4e534-117">此操作會傳回 DNS 區域物件對應 tooan 現有的區域中 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="4e534-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="4e534-118">hello 物件包含有關 hello 區域 （例如 hello 數字的資料錄集），資料，但不是包含本身的 hello 資料錄集 (請參閱`Get-AzureRmDnsRecordSet`)。</span><span class="sxs-lookup"><span data-stu-id="4e534-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="4e534-119">列出 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-119">List DNS zones</span></span>

<span data-ttu-id="4e534-120">藉由略過從 hello 區域名稱`Get-AzureRmDnsZone`，您可以列舉資源群組中的所有區域。</span><span class="sxs-lookup"><span data-stu-id="4e534-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="4e534-121">此作業會傳回一系列的區域物件。</span><span class="sxs-lookup"><span data-stu-id="4e534-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="4e534-122">藉由略過 hello 區域名稱和 hello 資源群組名稱，從`Get-AzureRmDnsZone`，您可以列舉 hello Azure 訂用帳戶中的所有區域。</span><span class="sxs-lookup"><span data-stu-id="4e534-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="4e534-123">更新 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-123">Update a DNS zone</span></span>

<span data-ttu-id="4e534-124">變更 DNS 區域資源可使用 tooa `Set-AzureRmDnsZone`。</span><span class="sxs-lookup"><span data-stu-id="4e534-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="4e534-125">此 cmdlet 不會更新 hello 區域內 hello DNS 資料錄集 (請參閱[如何 tooManage DNS 記錄](dns-operations-recordsets.md))。</span><span class="sxs-lookup"><span data-stu-id="4e534-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="4e534-126">它只有已使用 hello 區域資源本身的 tooupdate 的屬性。</span><span class="sxs-lookup"><span data-stu-id="4e534-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="4e534-127">hello 可寫入的區域屬性會限制目前 toohello [Azure 資源管理員 '標記' hello 區域資源](dns-zones-records.md#tags)。</span><span class="sxs-lookup"><span data-stu-id="4e534-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="4e534-128">使用下列兩種方式 tooupdate hello 的其中一個 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="4e534-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="4e534-129">指定使用 hello 區域名稱和資源群組的 hello 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="4e534-130">這種方法，取代指定 hello 值 hello 現有區域的標籤。</span><span class="sxs-lookup"><span data-stu-id="4e534-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="4e534-131">指定使用 $zone 物件 hello 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="4e534-132">這個方法會擷取 hello 現有區域物件、 修改 hello 標記，並認可 hello 的變更，然後。</span><span class="sxs-lookup"><span data-stu-id="4e534-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="4e534-133">如此一來，就可以保留現有的標籤。</span><span class="sxs-lookup"><span data-stu-id="4e534-133">In this way, existing tags can be preserved.</span></span>

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

<span data-ttu-id="4e534-134">當使用`Set-AzureRmDnsZone`$zone 物件時， [Etag 檢查](dns-zones-records.md#etags)可用 tooensure 並行的變更不會覆寫。</span><span class="sxs-lookup"><span data-stu-id="4e534-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="4e534-135">您可以使用選擇性的 hello`-Overwrite`切換 toosuppress 這些檢查。</span><span class="sxs-lookup"><span data-stu-id="4e534-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="4e534-136">刪除 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-136">Delete a DNS Zone</span></span>

<span data-ttu-id="4e534-137">您可以使用 hello 刪除 DNS 區域`Remove-AzureRmDnsZone`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4e534-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="4e534-138">刪除 DNS 區域時，也會刪除 hello 區域內的所有 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="4e534-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="4e534-139">此作業無法復原。</span><span class="sxs-lookup"><span data-stu-id="4e534-139">This operation cannot be undone.</span></span> <span data-ttu-id="4e534-140">如果正在使用中的 hello DNS 區域，使用 hello 區域的服務將無法刪除 hello 區域時。</span><span class="sxs-lookup"><span data-stu-id="4e534-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="4e534-141">tooprotect 區域意外刪除，請參閱[tooprotect DNS 區域的方式，以及記錄](dns-protect-zones-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="4e534-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="4e534-142">使用下列兩種方式 toodelete hello 的其中一個 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="4e534-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="4e534-143">指定使用 hello 區域名稱和資源群組名稱的 hello 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="4e534-144">指定使用 $zone 物件 hello 區域</span><span class="sxs-lookup"><span data-stu-id="4e534-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="4e534-145">您可以指定使用刪除 hello 區域 toobe`$zone`所傳回物件`Get-AzureRmDnsZone`。</span><span class="sxs-lookup"><span data-stu-id="4e534-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="4e534-146">hello 區域物件也管線傳遞而不被傳遞做為參數：</span><span class="sxs-lookup"><span data-stu-id="4e534-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="4e534-147">如同`Set-AzureRmDnsZone`，指定區域使用 hello`$zone`物件的啟用 Etag 檢查 tooensure 並行的變更不會刪除。</span><span class="sxs-lookup"><span data-stu-id="4e534-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="4e534-148">使用 hello`-Overwrite`切換 toosuppress 這些檢查。</span><span class="sxs-lookup"><span data-stu-id="4e534-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="4e534-149">確認提示</span><span class="sxs-lookup"><span data-stu-id="4e534-149">Confirmation prompts</span></span>

<span data-ttu-id="4e534-150">hello `New-AzureRmDnsZone`， `Set-AzureRmDnsZone`，和`Remove-AzureRmDnsZone`cmdlet 都支援確認提示。</span><span class="sxs-lookup"><span data-stu-id="4e534-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="4e534-151">同時`New-AzureRmDnsZone`和`Set-AzureRmDnsZone`提示您確認如果 hello `$ConfirmPreference` PowerShell 喜好設定變數的值為`Medium`或更低。</span><span class="sxs-lookup"><span data-stu-id="4e534-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="4e534-152">由於 toohello 高可能會影響刪除 DNS 區域，hello`Remove-AzureRmDnsZone`指令程式會先提示確認如果 hello `$ConfirmPreference` PowerShell 變數有任何值以外`None`。</span><span class="sxs-lookup"><span data-stu-id="4e534-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="4e534-153">因為 hello 預設值為`$ConfirmPreference`是`High`，則只`Remove-AzureRmDnsZone`預設提示確認。</span><span class="sxs-lookup"><span data-stu-id="4e534-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="4e534-154">您可以覆寫 hello 目前`$ConfirmPreference`設定使用 hello`-Confirm`參數。</span><span class="sxs-lookup"><span data-stu-id="4e534-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="4e534-155">如果您指定`-Confirm`或`-Confirm:$True`，hello cmdlet 會提示您確認再它執行。</span><span class="sxs-lookup"><span data-stu-id="4e534-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="4e534-156">如果您指定`-Confirm:$False`，hello cmdlet 不會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="4e534-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="4e534-157">如需 `-Confirm` 和 `$ConfirmPreference` 的詳細資訊，請參閱[有關喜好設定變數](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)。</span><span class="sxs-lookup"><span data-stu-id="4e534-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e534-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e534-158">Next steps</span></span>

<span data-ttu-id="4e534-159">了解如何太[管理資料錄集 」 和 「 記錄](dns-operations-recordsets.md)DNS 區域中。</span><span class="sxs-lookup"><span data-stu-id="4e534-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="4e534-160">了解如何太[委派您網域 tooAzure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="4e534-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="4e534-161">檢閱 hello [Azure DNS PowerShell 參考文件](/powershell/module/azurerm.dns)。</span><span class="sxs-lookup"><span data-stu-id="4e534-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

