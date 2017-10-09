---
title: "aaaManage DNS 區域中 Azure DNS-Azure CLI 1.0 |Microsoft 文件"
description: "您可以使用 Azure CLI 1.0 管理 DNS 區域。 本文將說明如何 tooupdate、 刪除及 Azure DNS 上建立 DNS 區域。"
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
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="625c3-104">如何使用 Azure DNS toomanage DNS 區域 hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="625c3-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="625c3-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="625c3-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="625c3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="625c3-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="625c3-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="625c3-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="625c3-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="625c3-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="625c3-109">本指南也說明如何 toomanage 您的 DNS 區域使用 hello 跨平台 Azure CLI 1.0，這是適用於 Windows、 Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="625c3-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="625c3-110">您也可以管理您使用的 DNS 區域[Azure PowerShell](dns-operations-dnszones.md)或 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="625c3-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="625c3-111">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="625c3-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="625c3-112">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="625c3-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="625c3-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -我們 CLI hello 傳統和資源管理部署模型。</span><span class="sxs-lookup"><span data-stu-id="625c3-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="625c3-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -hello 資源管理部署模型我們下一個層代 CLI。</span><span class="sxs-lookup"><span data-stu-id="625c3-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="625c3-115">簡介</span><span class="sxs-lookup"><span data-stu-id="625c3-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="625c3-116">取得說明</span><span class="sxs-lookup"><span data-stu-id="625c3-116">Getting help</span></span>

<span data-ttu-id="625c3-117">所有相關 tooAzure DNS 的 CLI 1.0 命令開頭`azure network dns`。</span><span class="sxs-lookup"><span data-stu-id="625c3-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="625c3-118">說明適用於每個命令使用 hello`--help`選項 (簡短形式`-h`)。</span><span class="sxs-lookup"><span data-stu-id="625c3-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="625c3-119">例如：</span><span class="sxs-lookup"><span data-stu-id="625c3-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="625c3-120">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="625c3-120">Create a DNS zone</span></span>

<span data-ttu-id="625c3-121">DNS 區域建立使用 hello`azure network dns zone create`命令。</span><span class="sxs-lookup"><span data-stu-id="625c3-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="625c3-122">如需協助，請參閱 `azure network dns zone create -h`。</span><span class="sxs-lookup"><span data-stu-id="625c3-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="625c3-123">hello 下列範例會建立 DNS 區域呼叫*contoso.com*呼叫 hello 資源群組中*MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="625c3-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="625c3-124">toocreate DNS 區域與標籤</span><span class="sxs-lookup"><span data-stu-id="625c3-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="625c3-125">hello 下列範例示範如何 toocreate DNS 區域具有兩個[Azure 資源管理員標記](dns-zones-records.md#tags)，*專案 = 示範*和*env = test*，使用 hello `--tags`參數 (簡短形式`-t`):</span><span class="sxs-lookup"><span data-stu-id="625c3-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="625c3-126">取得 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="625c3-126">Get a DNS zone</span></span>

<span data-ttu-id="625c3-127">tooretrieve DNS 區域，使用`azure network dns zone show`。</span><span class="sxs-lookup"><span data-stu-id="625c3-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="625c3-128">如需協助，請參閱 `azure network dns zone show -h`。</span><span class="sxs-lookup"><span data-stu-id="625c3-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="625c3-129">hello 下列範例會傳回 hello DNS 區域*contoso.com*及其相關聯的資料，從資源群組*MyResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="625c3-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="625c3-130">下列範例中的 hello 是 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="625c3-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
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

<span data-ttu-id="625c3-131">請注意，`azure network dns zone show` 不會傳回 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="625c3-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="625c3-132">toolist DNS 記錄，使用`azure network dns record-set list`。</span><span class="sxs-lookup"><span data-stu-id="625c3-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="625c3-133">列出 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="625c3-133">List DNS zones</span></span>

<span data-ttu-id="625c3-134">tooenumerate DNS 區域，使用`azure network dns zone list`。</span><span class="sxs-lookup"><span data-stu-id="625c3-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="625c3-135">如需協助，請參閱 `azure network dns zone list -h`。</span><span class="sxs-lookup"><span data-stu-id="625c3-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="625c3-136">指定 hello 資源群組會列出這些區域 hello 的資源群組中：</span><span class="sxs-lookup"><span data-stu-id="625c3-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="625c3-137">省略 hello 資源群組列出 hello 訂用帳戶中的所有區域：</span><span class="sxs-lookup"><span data-stu-id="625c3-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="625c3-138">更新 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="625c3-138">Update a DNS zone</span></span>

<span data-ttu-id="625c3-139">DNS 區域資源可以使用進行的變更 tooa `azure network dns zone set`。</span><span class="sxs-lookup"><span data-stu-id="625c3-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="625c3-140">如需協助，請參閱 `azure network dns zone set -h`。</span><span class="sxs-lookup"><span data-stu-id="625c3-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="625c3-141">此命令不會更新 hello 區域內 hello DNS 資料錄集 (請參閱[如何 tooManage DNS 記錄](dns-operations-recordsets-cli-nodejs.md))。</span><span class="sxs-lookup"><span data-stu-id="625c3-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="625c3-142">它是只使用的 tooupdate 屬性 hello 區域資源本身。</span><span class="sxs-lookup"><span data-stu-id="625c3-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="625c3-143">這些屬性是目前限制的 toohello [Azure 資源管理員 '標記'](dns-zones-records.md#tags) hello 區域資源。</span><span class="sxs-lookup"><span data-stu-id="625c3-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="625c3-144">hello 下列範例顯示如何 tooupdate hello 標記上的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="625c3-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="625c3-145">所指定的 hello 值取代 hello 現有的標記。</span><span class="sxs-lookup"><span data-stu-id="625c3-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="625c3-146">刪除 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="625c3-146">Delete a DNS Zone</span></span>

<span data-ttu-id="625c3-147">可以使用 `azure network dns zone delete`刪除 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="625c3-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="625c3-148">如需協助，請參閱 `azure network dns zone delete -h`。</span><span class="sxs-lookup"><span data-stu-id="625c3-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="625c3-149">刪除 DNS 區域時，也會刪除 hello 區域內的所有 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="625c3-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="625c3-150">此作業無法復原。</span><span class="sxs-lookup"><span data-stu-id="625c3-150">This operation cannot be undone.</span></span> <span data-ttu-id="625c3-151">如果正在使用中的 hello DNS 區域，使用 hello 區域的服務將無法刪除 hello 區域時。</span><span class="sxs-lookup"><span data-stu-id="625c3-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="625c3-152">tooprotect 區域意外刪除，請參閱[tooprotect DNS 區域的方式，以及記錄](dns-protect-zones-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="625c3-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="625c3-153">此命令會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="625c3-153">This command prompts for confirmation.</span></span> <span data-ttu-id="625c3-154">選擇性的 hello`--quiet`切換 (簡短形式`-q`) 會隱藏此提示。</span><span class="sxs-lookup"><span data-stu-id="625c3-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="625c3-155">hello 下列範例示範如何 toodelete hello 區域*contoso.com*從資源群組*MyResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="625c3-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="625c3-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="625c3-156">Next steps</span></span>

<span data-ttu-id="625c3-157">了解如何太[管理資料錄集 」 和 「 記錄](dns-getstarted-create-recordset-cli-nodejs.md)DNS 區域中。</span><span class="sxs-lookup"><span data-stu-id="625c3-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="625c3-158">了解如何太[委派您網域 tooAzure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="625c3-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

