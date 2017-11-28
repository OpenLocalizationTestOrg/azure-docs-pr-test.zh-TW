---
title: "aaaGet 開始使用 Azure DNS 使用 Azure CLI 2.0 |Microsoft 文件"
description: "深入了解如何 toocreate DNS 區域與在 Azure DNS 記錄。 這是逐步指南 toocreate 和管理您的第一個 DNS 區域和使用 Azure CLI 2.0 hello 記錄。"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="4c15c-104">利用 Azure CLI 2.0 開始使用 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="4c15c-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c15c-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4c15c-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="4c15c-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c15c-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="4c15c-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4c15c-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="4c15c-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4c15c-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="4c15c-109">本文將引導您完成 hello 步驟 toocreate 第一次的 DNS 區域，並使用記錄 hello 跨平台 Azure CLI 2.0 中，這是適用於 Windows、 Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="4c15c-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="4c15c-110">您也可以執行這些步驟使用 hello Azure 入口網站或 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4c15c-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="4c15c-111">DNS 區域是使用的 toohost hello 針對特定網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="4c15c-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="4c15c-112">toostart 裝載您的網域在 Azure DNS 中，您需要該網域名稱 toocreate DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="4c15c-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="4c15c-113">接著在此 DNS 區域內，建立網域的每筆 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="4c15c-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="4c15c-114">最後，toopublish 您的 DNS 區域 toohello 網際網路，您需要 tooconfigure hello 名稱伺服器 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="4c15c-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="4c15c-115">以下說明上述各步驟。</span><span class="sxs-lookup"><span data-stu-id="4c15c-115">Each of these steps is described below.</span></span>

<span data-ttu-id="4c15c-116">這些指示假設您已經安裝並登入 tooAzure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="4c15c-116">These instructions assume you have already installed and signed in tooAzure CLI 2.0.</span></span> <span data-ttu-id="4c15c-117">如需說明，請參閱[toomanage DNS 區域使用 Azure CLI 2.0](dns-operations-dnszones-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="4c15c-117">For help, see [How toomanage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="4c15c-118">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="4c15c-118">Create hello resource group</span></span>

<span data-ttu-id="4c15c-119">建立 hello DNS 區域之前, 建立 toocontain hello DNS 區域資源群組。</span><span class="sxs-lookup"><span data-stu-id="4c15c-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="4c15c-120">hello 下列範例示範 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="4c15c-120">hello following shows hello command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="4c15c-121">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="4c15c-121">Create a DNS zone</span></span>

<span data-ttu-id="4c15c-122">DNS 區域建立使用 hello`az network dns zone create`命令。</span><span class="sxs-lookup"><span data-stu-id="4c15c-122">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="4c15c-123">此命令，toosee 說明輸入`az network dns zone create -h`。</span><span class="sxs-lookup"><span data-stu-id="4c15c-123">toosee help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="4c15c-124">hello 下列範例會建立 DNS 區域呼叫*contoso.com* hello 資源群組中*MyResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="4c15c-124">hello following example creates a DNS zone called *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="4c15c-125">使用 hello 範例 toocreate DNS 區域時，取代為您自己的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="4c15c-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="4c15c-126">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="4c15c-126">Create a DNS record</span></span>

<span data-ttu-id="4c15c-127">toocreate DNS 記錄，使用 hello`az network dns record-set [record type] add-record`命令。</span><span class="sxs-lookup"><span data-stu-id="4c15c-127">toocreate a DNS record, use hello `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="4c15c-128">如需說明，例如 A 記錄，請參閱 `azure network dns record-set A add-record -h`。</span><span class="sxs-lookup"><span data-stu-id="4c15c-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="4c15c-129">hello 下列範例會建立一筆記錄 hello 相對名稱"www"hello"contoso.com"，"MyResourceGroup"的資源群組中的 DNS 區域中。</span><span class="sxs-lookup"><span data-stu-id="4c15c-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="4c15c-130">hello hello 資料錄集的完整名稱是"www.contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="4c15c-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="4c15c-131">hello 記錄類型是"A"，使用"1.2.3.4"的 IP 位址，則會使用預設的 TTL 為 3600 秒 （1 小時）。</span><span class="sxs-lookup"><span data-stu-id="4c15c-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="4c15c-132">對於其他記錄類型，如記錄設定具有一個以上的記錄，替代的 TTL 值和 toomodify 現有的記錄，請參閱[管理 DNS 記錄，並使用資料錄集 hello Azure CLI 2.0](dns-operations-recordsets-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="4c15c-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="4c15c-133">檢視記錄</span><span class="sxs-lookup"><span data-stu-id="4c15c-133">View records</span></span>

<span data-ttu-id="4c15c-134">toolist hello DNS 記錄，在您的區域，使用：</span><span class="sxs-lookup"><span data-stu-id="4c15c-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="4c15c-135">更新名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="4c15c-135">Update name servers</span></span>

<span data-ttu-id="4c15c-136">您可以在該程式的 DNS 區域與記錄已設定正確，您需要 tooconfigure 滿足您的網域名稱 toouse hello Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="4c15c-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="4c15c-137">這可讓其他使用者 hello 網際網路 toofind DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="4c15c-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="4c15c-138">hello 名稱伺服器，您的區域會提供 hello`az network dns zone show`命令。</span><span class="sxs-lookup"><span data-stu-id="4c15c-138">hello name servers for your zone are given by hello `az network dns zone show` command.</span></span> <span data-ttu-id="4c15c-139">toosee hello 名稱伺服器名稱，會使用 JSON 輸出，hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="4c15c-139">toosee hello name server names, use JSON output, as shown in hello following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="4c15c-140">這些名稱伺服器應該設有 hello 網域名稱註冊機構 （您購買 hello 網域名稱）。</span><span class="sxs-lookup"><span data-stu-id="4c15c-140">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="4c15c-141">您的註冊機構會提供 hello 選項 tooset hello hello 網域名稱伺服器註冊。</span><span class="sxs-lookup"><span data-stu-id="4c15c-141">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="4c15c-142">如需詳細資訊，請參閱[委派您網域 tooAzure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="4c15c-142">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="4c15c-143">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="4c15c-143">Delete all resources</span></span>
 
<span data-ttu-id="4c15c-144">toodelete 本文採用 hello 下列步驟中建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="4c15c-144">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4c15c-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c15c-145">Next steps</span></span>

<span data-ttu-id="4c15c-146">toolearn 進一步了解 Azure DNS，請參閱[Azure DNS 概觀](dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4c15c-146">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="4c15c-147">進一步了解管理 Azure DNS 的 DNS 區域 toolearn 看到[管理 DNS 區域中使用 Azure CLI 2.0 Azure DNS](dns-operations-dnszones-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="4c15c-147">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="4c15c-148">進一步了解管理 Azure DNS 的 DNS 記錄 toolearn 看到[管理 DNS 記錄和記錄設定中使用 Azure CLI 2.0 Azure DNS](dns-operations-recordsets-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="4c15c-148">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
