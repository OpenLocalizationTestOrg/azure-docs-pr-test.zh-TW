---
title: "管理 Azure DNS 中的 DNS 區域 - Azure CLI 2.0 | Microsoft Docs"
description: "您可以使用 Azure CLI 2.0 管理 DNS 區域。 本文說明如何在 Azure DNS 上更新、刪除及建立 DNS 區域。"
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
ms.openlocfilehash: 1414baf9e51d648cc3a46c4f8635040b4d276910
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="f03e7-104">如何使用 Azure CLI 2.0 管理 Azure DNS 中的 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="f03e7-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f03e7-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="f03e7-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="f03e7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f03e7-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="f03e7-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f03e7-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="f03e7-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f03e7-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="f03e7-109">本指南說明如何使用適用於 Windows、Mac 和 Linux 的跨平台 Azure CLI 來管理 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="f03e7-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="f03e7-110">您也可以使用 [Azure PowerShell](dns-operations-dnszones.md) 或 Azure 入口網站來管理 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="f03e7-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f03e7-111">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="f03e7-111">CLI versions to complete the task</span></span>

<span data-ttu-id="f03e7-112">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="f03e7-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="f03e7-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - 適用於傳統和資源管理部署模型的 CLI。</span><span class="sxs-lookup"><span data-stu-id="f03e7-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="f03e7-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - 適用於資源管理部署模型的新一代 CLI。</span><span class="sxs-lookup"><span data-stu-id="f03e7-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="f03e7-115">簡介</span><span class="sxs-lookup"><span data-stu-id="f03e7-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="f03e7-116">設定適用於 Azure DNS 的 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f03e7-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="f03e7-117">開始之前</span><span class="sxs-lookup"><span data-stu-id="f03e7-117">Before you begin</span></span>

<span data-ttu-id="f03e7-118">在開始設定之前，請確認您具備下列項目。</span><span class="sxs-lookup"><span data-stu-id="f03e7-118">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="f03e7-119">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f03e7-119">An Azure subscription.</span></span> <span data-ttu-id="f03e7-120">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="f03e7-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="f03e7-121">安裝最新版的 Azure CLI 2.0，該 CLI 適用於 Windows、Linux 或 MAC。</span><span class="sxs-lookup"><span data-stu-id="f03e7-121">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="f03e7-122">您可以在[安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2) 中取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f03e7-122">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="f03e7-123">登入您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="f03e7-123">Sign in to your Azure account</span></span>

<span data-ttu-id="f03e7-124">開啟主控台視窗，並驗證您的認證。</span><span class="sxs-lookup"><span data-stu-id="f03e7-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="f03e7-125">如需詳細資訊，請參閱＜從 Azure CLI 登入 Azure＞</span><span class="sxs-lookup"><span data-stu-id="f03e7-125">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="f03e7-126">選取訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f03e7-126">Select the subscription</span></span>

<span data-ttu-id="f03e7-127">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f03e7-127">Check the subscriptions for the account.</span></span>

```
az account list
```

<span data-ttu-id="f03e7-128">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f03e7-128">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="f03e7-129">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="f03e7-129">Create a resource group</span></span>

<span data-ttu-id="f03e7-130">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="f03e7-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f03e7-131">這用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="f03e7-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="f03e7-132">然而，因為所有 DNS 資源是全球性，而非區域性，資源群組位置的選擇不會對 Azure DNS 造成影響。</span><span class="sxs-lookup"><span data-stu-id="f03e7-132">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="f03e7-133">如果您使用現有的資源群組，則可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="f03e7-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="f03e7-134">取得說明</span><span class="sxs-lookup"><span data-stu-id="f03e7-134">Getting help</span></span>

<span data-ttu-id="f03e7-135">所有與 Azure DNS 相關的 CLI 2.0 命令都會以 `az network dns` 開頭。</span><span class="sxs-lookup"><span data-stu-id="f03e7-135">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="f03e7-136">使用 `--help` 選項 (簡短形式為 `-h`) 即可取得每個命令的說明。</span><span class="sxs-lookup"><span data-stu-id="f03e7-136">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="f03e7-137">例如：</span><span class="sxs-lookup"><span data-stu-id="f03e7-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="f03e7-138">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="f03e7-138">Create a DNS zone</span></span>

<span data-ttu-id="f03e7-139">使用 `az network dns zone create` 命令建立 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="f03e7-139">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="f03e7-140">如需協助，請參閱 `az network dns zone create -h`。</span><span class="sxs-lookup"><span data-stu-id="f03e7-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="f03e7-141">下列範例會在稱為 *MyResourceGroup* 的資源群組中建立稱為 *contoso.com* 的 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="f03e7-141">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="f03e7-142">使用標籤建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="f03e7-142">To create a DNS zone with tags</span></span>

<span data-ttu-id="f03e7-143">下列範例示範如何使用 `--tags` 參數 (簡短形式為 `-t`)，利用 *project = demo* 和 *env = test* 這兩個 [Azure Resource Manager 標籤](dns-zones-records.md#tags)，建立 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="f03e7-143">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="f03e7-144">取得 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="f03e7-144">Get a DNS zone</span></span>

<span data-ttu-id="f03e7-145">若要擷取 DNS 區域，請使用 `az network dns zone show`。</span><span class="sxs-lookup"><span data-stu-id="f03e7-145">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="f03e7-146">如需協助，請參閱 `az network dns zone show --help`。</span><span class="sxs-lookup"><span data-stu-id="f03e7-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="f03e7-147">下列範例會從資源群組 MyResourceGroup 傳回 DNS 區域 contoso.com 及其相關聯的資料。</span><span class="sxs-lookup"><span data-stu-id="f03e7-147">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="f03e7-148">以下是回應範例。</span><span class="sxs-lookup"><span data-stu-id="f03e7-148">The following example is the response.</span></span>

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

<span data-ttu-id="f03e7-149">請注意，`az network dns zone show` 不會傳回 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="f03e7-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="f03e7-150">若要列出 DNS 記錄，請使用 `az network dns record-set list`。</span><span class="sxs-lookup"><span data-stu-id="f03e7-150">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="f03e7-151">列出 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="f03e7-151">List DNS zones</span></span>

<span data-ttu-id="f03e7-152">若要列舉 DNS 區域，請使用 `az network dns zone list`。</span><span class="sxs-lookup"><span data-stu-id="f03e7-152">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="f03e7-153">如需協助，請參閱 `az network dns zone list --help`。</span><span class="sxs-lookup"><span data-stu-id="f03e7-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="f03e7-154">指定資源群組只會列出資源群組內的區域︰</span><span class="sxs-lookup"><span data-stu-id="f03e7-154">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="f03e7-155">省略資源群組則會列出訂用帳戶中的所有區域︰</span><span class="sxs-lookup"><span data-stu-id="f03e7-155">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="f03e7-156">更新 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="f03e7-156">Update a DNS zone</span></span>

<span data-ttu-id="f03e7-157">您可以使用 `az network dns zone update`變更 DNS 區域資源。</span><span class="sxs-lookup"><span data-stu-id="f03e7-157">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="f03e7-158">如需協助，請參閱 `az network dns zone update --help`。</span><span class="sxs-lookup"><span data-stu-id="f03e7-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="f03e7-159">此命令不會更新區域內的任何 DNS 記錄集 (請參閱[如何管理 DNS 記錄](dns-operations-recordsets-cli.md))。</span><span class="sxs-lookup"><span data-stu-id="f03e7-159">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="f03e7-160">它只用來更新區域資源本身的屬性。</span><span class="sxs-lookup"><span data-stu-id="f03e7-160">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="f03e7-161">這些屬性目前僅限於區域資源的 [Azure Resource Manager「標籤」](dns-zones-records.md#tags)。</span><span class="sxs-lookup"><span data-stu-id="f03e7-161">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="f03e7-162">下列範例示範如何更新 DNS 區域上的標籤。</span><span class="sxs-lookup"><span data-stu-id="f03e7-162">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="f03e7-163">現有標籤會由指定值取代。</span><span class="sxs-lookup"><span data-stu-id="f03e7-163">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="f03e7-164">刪除 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="f03e7-164">Delete a DNS zone</span></span>

<span data-ttu-id="f03e7-165">可以使用 `az network dns zone delete`刪除 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="f03e7-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="f03e7-166">如需協助，請參閱 `az network dns zone delete --help`。</span><span class="sxs-lookup"><span data-stu-id="f03e7-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="f03e7-167">刪除 DNS 區域也會刪除該區域內的所有 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="f03e7-167">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="f03e7-168">此作業無法復原。</span><span class="sxs-lookup"><span data-stu-id="f03e7-168">This operation cannot be undone.</span></span> <span data-ttu-id="f03e7-169">如果 DNS 區域正在使用中，當該區域遭到刪除時，使用該區域的服務將會失敗。</span><span class="sxs-lookup"><span data-stu-id="f03e7-169">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="f03e7-170">若要防止區域意外遭到刪除，請參閱[如何保護 DNS 區域和記錄](dns-protect-zones-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="f03e7-170">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="f03e7-171">此命令會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="f03e7-171">This command prompts for confirmation.</span></span> <span data-ttu-id="f03e7-172">選擇性的 `--yes` 參數會隱藏這個提示。</span><span class="sxs-lookup"><span data-stu-id="f03e7-172">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="f03e7-173">下列範例示範如何從資源群組 MyResourceGroup 刪除區域 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="f03e7-173">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="f03e7-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f03e7-174">Next steps</span></span>

<span data-ttu-id="f03e7-175">了解如何在 DNS 區域中[管理記錄集和記錄](dns-getstarted-create-recordset-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="f03e7-175">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="f03e7-176">了解如何[將您的網域委派給 Azure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="f03e7-176">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

