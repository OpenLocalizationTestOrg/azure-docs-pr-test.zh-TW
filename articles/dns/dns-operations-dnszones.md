---
title: "管理 Azure DNS 中的 DNS 區域 - PowerShell | Microsoft Docs"
description: "您可以使用 Azure Powershell 管理 DNS 區域。 本文說明如何在 Azure DNS 上更新、刪除及建立 DNS 區域"
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
ms.openlocfilehash: 92f1da660d875c76d5d826669d6c1d12018c3d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="a2d2b-104">如何管理使用 PowerShell 的 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2d2b-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="a2d2b-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="a2d2b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2d2b-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="a2d2b-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a2d2b-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="a2d2b-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a2d2b-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="a2d2b-109">本文說明如何使用 Azure PowerShell 管理 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-109">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="a2d2b-110">您也可以使用跨平台 [Azure CLI](dns-operations-dnszones-cli.md) 或 Azure 入口網站來管理 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="a2d2b-111">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-111">Create a DNS zone</span></span>

<span data-ttu-id="a2d2b-112">使用 `New-AzureRmDnsZone` Cmdlet 建立 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-112">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="a2d2b-113">下列範例會在稱為 *MyResourceGroup* 的資源群組中建立稱為 *contoso.com* 的 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="a2d2b-113">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="a2d2b-114">下列範例示範如何使用 *project = demo* 和 *env = test* 這兩個 [Azure Resource Manager 標籤](dns-zones-records.md#tags)，建立 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="a2d2b-114">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="a2d2b-115">取得 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-115">Get a DNS zone</span></span>

<span data-ttu-id="a2d2b-116">若要擷取 DNS 區域，請使用 `Get-AzureRmDnsZone` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-116">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="a2d2b-117">此作業會傳回對應至 Azure DNS 中現有區域的 DNS 區域物件。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-117">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="a2d2b-118">這個物件包含區域的相關資料 (例如記錄集的數目)，但不包含記錄集本身 (請參閱 `Get-AzureRmDnsRecordSet`)。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-118">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="a2d2b-119">列出 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-119">List DNS zones</span></span>

<span data-ttu-id="a2d2b-120">您可以從 `Get-AzureRmDnsZone` 中省略區域名稱，以列舉資源群組中的所有區域：</span><span class="sxs-lookup"><span data-stu-id="a2d2b-120">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="a2d2b-121">此作業會傳回一系列的區域物件。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="a2d2b-122">您可以從 `Get-AzureRmDnsZone` 中省略區域名稱和資源群組名稱，以列舉 Azure 訂用帳戶中的所有區域。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-122">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="a2d2b-123">更新 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-123">Update a DNS zone</span></span>

<span data-ttu-id="a2d2b-124">您可以使用 `Set-AzureRmDnsZone`變更 DNS 區域資源。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-124">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="a2d2b-125">這個 Cmdlet 不會更新區域內的任何 DNS 記錄集 (請參閱[如何管理 DNS 記錄](dns-operations-recordsets.md))。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-125">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="a2d2b-126">它只用來更新區域資源本身的屬性。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-126">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="a2d2b-127">這些可寫入區域屬性目前僅限於[區域資源的Azure Resource Manager「標籤」](dns-zones-records.md#tags)。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-127">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="a2d2b-128">請使用下列兩種方法之一來更新 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="a2d2b-128">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="a2d2b-129">使用區域名稱和資源群組來指定區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-129">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="a2d2b-130">這種方法會以指定的值取代現有的區域標籤。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-130">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="a2d2b-131">使用 $zone 物件來指定區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-131">Specify the zone using a $zone object</span></span>

<span data-ttu-id="a2d2b-132">此方法會擷取現有的區域物件、修改標籤，然後認可變更。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-132">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="a2d2b-133">如此一來，就可以保留現有的標籤。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="a2d2b-134">使用 `Set-AzureRmDnsZone` 搭配 $zone 物件時，會使用 [Etag 檢查](dns-zones-records.md#etags)，以確保不會覆寫並行變更。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="a2d2b-135">您可以使用選擇性的 `-Overwrite` 參數來停用這些檢查。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-135">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="a2d2b-136">刪除 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-136">Delete a DNS Zone</span></span>

<span data-ttu-id="a2d2b-137">您可以使用 `Remove-AzureRmDnsZone` Cmdlet 刪除 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-137">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="a2d2b-138">刪除 DNS 區域也會刪除該區域內的所有 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-138">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="a2d2b-139">此作業無法復原。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-139">This operation cannot be undone.</span></span> <span data-ttu-id="a2d2b-140">如果 DNS 區域正在使用中，當該區域遭到刪除時，使用該區域的服務將會失敗。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-140">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="a2d2b-141">若要防止區域意外遭到刪除，請參閱[如何保護 DNS 區域和記錄](dns-protect-zones-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-141">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="a2d2b-142">請使用下列兩種方法之一來刪除 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="a2d2b-142">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="a2d2b-143">使用區域名稱和資源群組名稱來指定區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-143">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="a2d2b-144">使用 $zone 物件來指定區域</span><span class="sxs-lookup"><span data-stu-id="a2d2b-144">Specify the zone using a $zone object</span></span>

<span data-ttu-id="a2d2b-145">您可以使用 `Get-AzureRmDnsZone` 所傳回的 `$zone` 物件，指定要刪除的區域。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-145">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="a2d2b-146">區域物件也可以經由管道輸送，而不是當做參數傳遞：</span><span class="sxs-lookup"><span data-stu-id="a2d2b-146">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="a2d2b-147">如同 `Set-AzureRmDnsZone` 一樣，使用 `$zone` 物件指定區域可啟用 Etag 檢查，以確保不會刪除並行的變更。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-147">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="a2d2b-148">使用 `-Overwrite` 參數來停用這些檢查。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-148">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="a2d2b-149">確認提示</span><span class="sxs-lookup"><span data-stu-id="a2d2b-149">Confirmation prompts</span></span>

<span data-ttu-id="a2d2b-150">`New-AzureRmDnsZone`、`Set-AzureRmDnsZone` 和 `Remove-AzureRmDnsZone` cmdlets 皆支援確認提示。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-150">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="a2d2b-151">如果 `$ConfirmPreference` PowerShell 喜好設定變數的值為 `Medium` 或更低，則 `New-AzureRmDnsZone` 和 `Set-AzureRmDnsZone` 兩者都會顯示確認提示。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="a2d2b-152">由於刪除 DNS 區域可能造成重大影響，所以如果 `$ConfirmPreference` PowerShell 變數的值不是 `None`，`Remove-AzureRmDnsZone` Cmdlet 就會顯示確認提示。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-152">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="a2d2b-153">由於 `$ConfirmPreference` 的預設值是 `High`，預設只有 `Remove-AzureRmDnsZone` 會顯示確認提示。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-153">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="a2d2b-154">您可以使用 `-Confirm` 參數覆寫目前 `$ConfirmPreference` 設定。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-154">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="a2d2b-155">如果您指定 `-Confirm` 或 `-Confirm:$True`，此 cmdlet 在執行前會提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-155">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="a2d2b-156">如果您指定 `-Confirm:$False`，此 cmdlet 不會提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-156">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="a2d2b-157">如需 `-Confirm` 和 `$ConfirmPreference` 的詳細資訊，請參閱[有關喜好設定變數](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2d2b-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2d2b-158">Next steps</span></span>

<span data-ttu-id="a2d2b-159">了解如何在 DNS 區域中[管理記錄集和記錄](dns-operations-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-159">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="a2d2b-160">了解如何[將您的網域委派給 Azure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-160">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="a2d2b-161">檢閱 [Azure DNS PowerShell 參考文件](/powershell/module/azurerm.dns)。</span><span class="sxs-lookup"><span data-stu-id="a2d2b-161">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

