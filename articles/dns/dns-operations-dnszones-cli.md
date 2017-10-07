---
title: "aaaManage DNS 區域中 Azure DNS-Azure CLI 2.0 |Microsoft 文件"
description: "您可以使用 Azure CLI 2.0 管理 DNS 區域。 本文將說明如何 tooupdate、 刪除及 Azure DNS 上建立 DNS 區域。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="d2cb3-104">如何使用 Azure DNS toomanage DNS 區域 hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d2cb3-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2cb3-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="d2cb3-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="d2cb3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2cb3-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="d2cb3-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d2cb3-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="d2cb3-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d2cb3-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="d2cb3-109">本指南也說明如何 toomanage 您的 DNS 區域使用 hello 跨平台 Azure CLI，這是適用於 Windows、 Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="d2cb3-110">您也可以管理您使用的 DNS 區域[Azure PowerShell](dns-operations-dnszones.md)或 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="d2cb3-111">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="d2cb3-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="d2cb3-112">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="d2cb3-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="d2cb3-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -我們 CLI hello 傳統和資源管理部署模型。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="d2cb3-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -hello 資源管理部署模型我們下一個層代 CLI。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="d2cb3-115">簡介</span><span class="sxs-lookup"><span data-stu-id="d2cb3-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="d2cb3-116">設定適用於 Azure DNS 的 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d2cb3-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="d2cb3-117">開始之前</span><span class="sxs-lookup"><span data-stu-id="d2cb3-117">Before you begin</span></span>

<span data-ttu-id="d2cb3-118">確認您擁有 hello 開始您的組態之前，下列項目。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="d2cb3-119">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-119">An Azure subscription.</span></span> <span data-ttu-id="d2cb3-120">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="d2cb3-121">安裝 hello hello Azure CLI 2.0，可供 Windows、 Linux 或 MAC 最新版本</span><span class="sxs-lookup"><span data-stu-id="d2cb3-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="d2cb3-122">詳細的資訊將會位於[安裝 hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="d2cb3-123">Azure 帳戶登入 tooyour</span><span class="sxs-lookup"><span data-stu-id="d2cb3-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="d2cb3-124">開啟主控台視窗，並驗證您的認證。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="d2cb3-125">如需詳細資訊，請參閱記錄檔中的 hello Azure CLI tooAzure</span><span class="sxs-lookup"><span data-stu-id="d2cb3-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="d2cb3-126">選取 hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d2cb3-126">Select hello subscription</span></span>

<span data-ttu-id="d2cb3-127">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="d2cb3-128">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="d2cb3-129">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="d2cb3-129">Create a resource group</span></span>

<span data-ttu-id="d2cb3-130">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d2cb3-131">這當做 hello 預設位置，該資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="d2cb3-132">不過，因為所有的 DNS 資源全域，不是地區，hello 所選擇的資源群組位置沒有任何影響 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="d2cb3-133">如果您使用現有的資源群組，則可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="d2cb3-134">取得說明</span><span class="sxs-lookup"><span data-stu-id="d2cb3-134">Getting help</span></span>

<span data-ttu-id="d2cb3-135">所有相關 tooAzure DNS 的 CLI 2.0 命令開頭`az network dns`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="d2cb3-136">說明適用於每個命令使用 hello`--help`選項 (簡短形式`-h`)。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="d2cb3-137">例如：</span><span class="sxs-lookup"><span data-stu-id="d2cb3-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="d2cb3-138">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="d2cb3-138">Create a DNS zone</span></span>

<span data-ttu-id="d2cb3-139">DNS 區域建立使用 hello`az network dns zone create`命令。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="d2cb3-140">如需協助，請參閱 `az network dns zone create -h`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="d2cb3-141">hello 下列範例會建立 DNS 區域呼叫*contoso.com*呼叫 hello 資源群組中*MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d2cb3-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="d2cb3-142">toocreate DNS 區域與標籤</span><span class="sxs-lookup"><span data-stu-id="d2cb3-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="d2cb3-143">hello 下列範例示範如何 toocreate DNS 區域具有兩個[Azure 資源管理員標記](dns-zones-records.md#tags)，*專案 = 示範*和*env = test*，使用 hello `--tags`參數 (簡短形式`-t`):</span><span class="sxs-lookup"><span data-stu-id="d2cb3-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="d2cb3-144">取得 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="d2cb3-144">Get a DNS zone</span></span>

<span data-ttu-id="d2cb3-145">tooretrieve DNS 區域，使用`az network dns zone show`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="d2cb3-146">如需協助，請參閱 `az network dns zone show --help`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="d2cb3-147">hello 下列範例會傳回 hello DNS 區域*contoso.com*及其相關聯的資料，從資源群組*MyResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="d2cb3-148">下列範例中的 hello 是 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-148">hello following example is hello response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="d2cb3-149">請注意，`az network dns zone show` 不會傳回 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="d2cb3-150">toolist DNS 記錄，使用`az network dns record-set list`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="d2cb3-151">列出 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="d2cb3-151">List DNS zones</span></span>

<span data-ttu-id="d2cb3-152">tooenumerate DNS 區域，使用`az network dns zone list`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="d2cb3-153">如需協助，請參閱 `az network dns zone list --help`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="d2cb3-154">指定 hello 資源群組會列出這些區域 hello 的資源群組中：</span><span class="sxs-lookup"><span data-stu-id="d2cb3-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="d2cb3-155">省略 hello 資源群組列出 hello 訂用帳戶中的所有區域：</span><span class="sxs-lookup"><span data-stu-id="d2cb3-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="d2cb3-156">更新 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="d2cb3-156">Update a DNS zone</span></span>

<span data-ttu-id="d2cb3-157">DNS 區域資源可以使用進行的變更 tooa `az network dns zone update`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="d2cb3-158">如需協助，請參閱 `az network dns zone update --help`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="d2cb3-159">此命令不會更新 hello 區域內 hello DNS 資料錄集 (請參閱[如何 tooManage DNS 記錄](dns-operations-recordsets-cli.md))。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="d2cb3-160">它是只使用的 tooupdate 屬性 hello 區域資源本身。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="d2cb3-161">這些屬性是目前限制的 toohello [Azure 資源管理員 '標記'](dns-zones-records.md#tags) hello 區域資源。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="d2cb3-162">hello 下列範例顯示如何 tooupdate hello 標記上的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="d2cb3-163">所指定的 hello 值取代 hello 現有的標記。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="d2cb3-164">刪除 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="d2cb3-164">Delete a DNS zone</span></span>

<span data-ttu-id="d2cb3-165">可以使用 `az network dns zone delete`刪除 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="d2cb3-166">如需協助，請參閱 `az network dns zone delete --help`。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="d2cb3-167">刪除 DNS 區域時，也會刪除 hello 區域內的所有 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="d2cb3-168">此作業無法復原。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-168">This operation cannot be undone.</span></span> <span data-ttu-id="d2cb3-169">如果正在使用中的 hello DNS 區域，使用 hello 區域的服務將無法刪除 hello 區域時。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="d2cb3-170">tooprotect 區域意外刪除，請參閱[tooprotect DNS 區域的方式，以及記錄](dns-protect-zones-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="d2cb3-171">此命令會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-171">This command prompts for confirmation.</span></span> <span data-ttu-id="d2cb3-172">選擇性的 hello`--yes`參數會抑制此提示。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="d2cb3-173">hello 下列範例示範如何 toodelete hello 區域*contoso.com*從資源群組*MyResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="d2cb3-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2cb3-174">Next steps</span></span>

<span data-ttu-id="d2cb3-175">了解如何太[管理資料錄集 」 和 「 記錄](dns-getstarted-create-recordset-cli.md)DNS 區域中。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="d2cb3-176">了解如何太[委派您網域 tooAzure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="d2cb3-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

