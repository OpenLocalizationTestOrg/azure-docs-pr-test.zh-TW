---
title: "管理 Azure DNS 中的 DNS 區域 - Azure CLI 1.0 | Microsoft Docs"
description: "您可以使用 Azure CLI 1.0 管理 DNS 區域。 本文說明如何在 Azure DNS 上更新、刪除及建立 DNS 區域。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 588c87749f049eff5b9e0729f6769c8367ba41e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="39078-104">如何使用 Azure CLI 1.0 管理 Azure DNS 中的 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="39078-104">How to manage DNS Zones in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="39078-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="39078-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="39078-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39078-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="39078-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="39078-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="39078-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="39078-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="39078-109">本指南說明如何使用適用於 Windows、Mac 和 Linux 的跨平台 Azure CLI 1.0 來管理 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="39078-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="39078-110">您也可以使用 [Azure PowerShell](dns-operations-dnszones.md) 或 Azure 入口網站來管理 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="39078-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="39078-111">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="39078-111">CLI versions to complete the task</span></span>

<span data-ttu-id="39078-112">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="39078-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="39078-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - 適用於傳統和資源管理部署模型的 CLI。</span><span class="sxs-lookup"><span data-stu-id="39078-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="39078-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - 適用於資源管理部署模型的新一代 CLI。</span><span class="sxs-lookup"><span data-stu-id="39078-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="39078-115">簡介</span><span class="sxs-lookup"><span data-stu-id="39078-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="39078-116">取得說明</span><span class="sxs-lookup"><span data-stu-id="39078-116">Getting help</span></span>

<span data-ttu-id="39078-117">所有與 Azure DNS 相關的 CLI 1.0 命令都會以 `azure network dns` 開頭。</span><span class="sxs-lookup"><span data-stu-id="39078-117">All CLI 1.0 commands relating to Azure DNS start with `azure network dns`.</span></span> <span data-ttu-id="39078-118">使用 `--help` 選項 (簡短形式為 `-h`) 即可取得每個命令的說明。</span><span class="sxs-lookup"><span data-stu-id="39078-118">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="39078-119">例如：</span><span class="sxs-lookup"><span data-stu-id="39078-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="39078-120">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="39078-120">Create a DNS zone</span></span>

<span data-ttu-id="39078-121">使用 `azure network dns zone create` 命令建立 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="39078-121">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="39078-122">如需協助，請參閱 `azure network dns zone create -h`。</span><span class="sxs-lookup"><span data-stu-id="39078-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="39078-123">下列範例會在稱為 *MyResourceGroup* 的資源群組中建立稱為 *contoso.com* 的 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="39078-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="39078-124">使用標籤建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="39078-124">To create a DNS zone with tags</span></span>

<span data-ttu-id="39078-125">下列範例示範如何使用 `--tags` 參數 (簡短形式為 `-t`)，利用 *project = demo* 和 *env = test* 這兩個 [Azure Resource Manager 標籤](dns-zones-records.md#tags)，建立 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="39078-125">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="39078-126">取得 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="39078-126">Get a DNS zone</span></span>

<span data-ttu-id="39078-127">若要擷取 DNS 區域，請使用 `azure network dns zone show`。</span><span class="sxs-lookup"><span data-stu-id="39078-127">To retrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="39078-128">如需協助，請參閱 `azure network dns zone show -h`。</span><span class="sxs-lookup"><span data-stu-id="39078-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="39078-129">下列範例會從資源群組 MyResourceGroup 傳回 DNS 區域 contoso.com 及其相關聯的資料。</span><span class="sxs-lookup"><span data-stu-id="39078-129">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="39078-130">以下是回應範例。</span><span class="sxs-lookup"><span data-stu-id="39078-130">The following example is the response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="39078-131">請注意，`azure network dns zone show` 不會傳回 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="39078-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="39078-132">若要列出 DNS 記錄，請使用 `azure network dns record-set list`。</span><span class="sxs-lookup"><span data-stu-id="39078-132">To list DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="39078-133">列出 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="39078-133">List DNS zones</span></span>

<span data-ttu-id="39078-134">若要列舉 DNS 區域，請使用 `azure network dns zone list`。</span><span class="sxs-lookup"><span data-stu-id="39078-134">To enumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="39078-135">如需協助，請參閱 `azure network dns zone list -h`。</span><span class="sxs-lookup"><span data-stu-id="39078-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="39078-136">指定資源群組只會列出資源群組內的區域︰</span><span class="sxs-lookup"><span data-stu-id="39078-136">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="39078-137">省略資源群組則會列出訂用帳戶中的所有區域︰</span><span class="sxs-lookup"><span data-stu-id="39078-137">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="39078-138">更新 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="39078-138">Update a DNS zone</span></span>

<span data-ttu-id="39078-139">您可以使用 `azure network dns zone set`變更 DNS 區域資源。</span><span class="sxs-lookup"><span data-stu-id="39078-139">Changes to a DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="39078-140">如需協助，請參閱 `azure network dns zone set -h`。</span><span class="sxs-lookup"><span data-stu-id="39078-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="39078-141">此命令不會更新區域內的任何 DNS 記錄集 (請參閱[如何管理 DNS 記錄](dns-operations-recordsets-cli-nodejs.md))。</span><span class="sxs-lookup"><span data-stu-id="39078-141">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="39078-142">它只用來更新區域資源本身的屬性。</span><span class="sxs-lookup"><span data-stu-id="39078-142">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="39078-143">這些屬性目前僅限於區域資源的 [Azure Resource Manager「標籤」](dns-zones-records.md#tags)。</span><span class="sxs-lookup"><span data-stu-id="39078-143">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="39078-144">下列範例示範如何更新 DNS 區域上的標籤。</span><span class="sxs-lookup"><span data-stu-id="39078-144">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="39078-145">現有標籤會由指定值取代。</span><span class="sxs-lookup"><span data-stu-id="39078-145">The existing tags are replaced by the value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="39078-146">刪除 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="39078-146">Delete a DNS Zone</span></span>

<span data-ttu-id="39078-147">可以使用 `azure network dns zone delete`刪除 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="39078-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="39078-148">如需協助，請參閱 `azure network dns zone delete -h`。</span><span class="sxs-lookup"><span data-stu-id="39078-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="39078-149">刪除 DNS 區域也會刪除該區域內的所有 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="39078-149">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="39078-150">此作業無法復原。</span><span class="sxs-lookup"><span data-stu-id="39078-150">This operation cannot be undone.</span></span> <span data-ttu-id="39078-151">如果 DNS 區域正在使用中，當該區域遭到刪除時，使用該區域的服務將會失敗。</span><span class="sxs-lookup"><span data-stu-id="39078-151">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="39078-152">若要防止區域意外遭到刪除，請參閱[如何保護 DNS 區域和記錄](dns-protect-zones-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="39078-152">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="39078-153">此命令會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="39078-153">This command prompts for confirmation.</span></span> <span data-ttu-id="39078-154">選擇性的 `--quiet` 參數 (簡短形式為 `-q`) 會隱藏這個提示。</span><span class="sxs-lookup"><span data-stu-id="39078-154">The optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="39078-155">下列範例示範如何從資源群組 MyResourceGroup 刪除區域 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="39078-155">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="39078-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39078-156">Next steps</span></span>

<span data-ttu-id="39078-157">了解如何在 DNS 區域中[管理記錄集和記錄](dns-getstarted-create-recordset-cli-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="39078-157">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="39078-158">了解如何[將您的網域委派給 Azure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="39078-158">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

