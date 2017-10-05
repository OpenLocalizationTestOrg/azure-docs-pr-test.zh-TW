---
title: "利用 Azure CLI 2.0 開始使用 Azure DNS | Microsoft Docs"
description: "了解如何在 Azure DNS 中建立 DNS 區域和記錄。 這份逐步指南將引導您使用 Azure CLI 2.0 建立和管理第一個 DNS 區域和記錄。"
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
ms.openlocfilehash: 6958d61b29961f59cb22f62bec55f2d467e7e7cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="5af2f-104">利用 Azure CLI 2.0 開始使用 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="5af2f-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5af2f-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5af2f-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="5af2f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5af2f-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="5af2f-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5af2f-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="5af2f-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5af2f-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="5af2f-109">本文將逐步引導您使用跨平台 Azure CLI 2.0 (適用於 Windows、Mac 和 Linux)，建立第一個 DNS 區域和記錄。</span><span class="sxs-lookup"><span data-stu-id="5af2f-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="5af2f-110">您也可以使用 Azure 入口網站或 Azure PowerShell 執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="5af2f-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="5af2f-111">DNS 區域用來裝載特定網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="5af2f-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="5af2f-112">若要開始將網域裝載到 Azure DNS 中，您必須建立該網域名稱的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="5af2f-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="5af2f-113">接著在此 DNS 區域內，建立網域的每筆 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="5af2f-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="5af2f-114">最後，若要將 DNS 區域發佈至網際網路，您需要設定網域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="5af2f-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="5af2f-115">以下說明上述各步驟。</span><span class="sxs-lookup"><span data-stu-id="5af2f-115">Each of these steps is described below.</span></span>

<span data-ttu-id="5af2f-116">這些指示假設您已經安裝並登入 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="5af2f-116">These instructions assume you have already installed and signed in to Azure CLI 2.0.</span></span> <span data-ttu-id="5af2f-117">如需說明，請參閱[如何使用 Azure CLI 2.0 管理 DNS 區域](dns-operations-dnszones-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="5af2f-117">For help, see [How to manage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="5af2f-118">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="5af2f-118">Create the resource group</span></span>

<span data-ttu-id="5af2f-119">建立 DNS 區域之前，會建立資源群組以包含 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="5af2f-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="5af2f-120">以下顯示命令。</span><span class="sxs-lookup"><span data-stu-id="5af2f-120">The following shows the command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="5af2f-121">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="5af2f-121">Create a DNS zone</span></span>

<span data-ttu-id="5af2f-122">使用 `az network dns zone create` 命令建立 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="5af2f-122">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="5af2f-123">若要查看此命令的說明，請輸入 `az network dns zone create -h`。</span><span class="sxs-lookup"><span data-stu-id="5af2f-123">To see help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="5af2f-124">下列範例會在 MyResourceGroup 資源群組中建立稱為 contoso.com 的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="5af2f-124">The following example creates a DNS zone called *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="5af2f-125">使用範例來建立 DNS 區域，並將值替換為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="5af2f-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="5af2f-126">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="5af2f-126">Create a DNS record</span></span>

<span data-ttu-id="5af2f-127">若要建立 DNS 記錄，請使用 `az network dns record-set [record type] add-record` 命令。</span><span class="sxs-lookup"><span data-stu-id="5af2f-127">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="5af2f-128">如需說明，例如 A 記錄，請參閱 `azure network dns record-set A add-record -h`。</span><span class="sxs-lookup"><span data-stu-id="5af2f-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="5af2f-129">下列範例會在資源群組 "MyResourceGroup" 中的 DNS 區域 "contoso.com" 中，建立具有相對名稱 "www" 的記錄。</span><span class="sxs-lookup"><span data-stu-id="5af2f-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="5af2f-130">記錄集的完整名稱是 "www.contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="5af2f-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="5af2f-131">記錄類型為 "A"，IP 位址是 "1.2.3.4"，使用預設 TTL 3600 秒 (1 小時)。</span><span class="sxs-lookup"><span data-stu-id="5af2f-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="5af2f-132">關於其他記錄類型、具有多個記錄的記錄集、其他 TTL 值和修改現有的記錄，請參閱[使用 Azure CLI 2.0 管理 DNS 記錄和記錄集](dns-operations-recordsets-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="5af2f-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="5af2f-133">檢視記錄</span><span class="sxs-lookup"><span data-stu-id="5af2f-133">View records</span></span>

<span data-ttu-id="5af2f-134">若要列出區域中的 DNS 記錄，請使用︰</span><span class="sxs-lookup"><span data-stu-id="5af2f-134">To list the DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="5af2f-135">更新名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="5af2f-135">Update name servers</span></span>

<span data-ttu-id="5af2f-136">當您滿意 DNS 區域且已正確設定記錄之後，您必須設定網域名稱來使用 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="5af2f-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="5af2f-137">這可讓網際網路上的其他使用者找到您的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="5af2f-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="5af2f-138">`az network dns zone show` 命令可顯示您的區域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="5af2f-138">The name servers for your zone are given by the `az network dns zone show` command.</span></span> <span data-ttu-id="5af2f-139">若要查看名稱伺服器的名稱，請使用 JSON 輸出，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5af2f-139">To see the name server names, use JSON output, as shown in the following example.</span></span>

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

<span data-ttu-id="5af2f-140">這些名稱伺服器應該向網域名稱註冊機構 (您購買網域名稱的來源) 設定。</span><span class="sxs-lookup"><span data-stu-id="5af2f-140">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="5af2f-141">您的註冊機構會提供選項來設定網域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="5af2f-141">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="5af2f-142">如需詳細資訊，請參閱[將網域委派給 Azure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="5af2f-142">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="5af2f-143">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="5af2f-143">Delete all resources</span></span>
 
<span data-ttu-id="5af2f-144">若要刪除這篇文章中建立的所有資源，請採取下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="5af2f-144">To delete all resources created in this article, take the following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="5af2f-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5af2f-145">Next steps</span></span>

<span data-ttu-id="5af2f-146">若要深入了解 Azure DNS，請參閱 [Azure DNS 概觀](dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5af2f-146">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="5af2f-147">若要深入了解在 Azure DNS 中管理 DNS 區域，請參閱[使用 Azure CLI 2.0 在 Azure DNS 中管理 DNS 區域](dns-operations-dnszones-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="5af2f-147">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="5af2f-148">若要深入了解在 Azure DNS 中管理 DNS 記錄，請參閱[使用 Azure CLI 2.0 在 Azure DNS 中管理 DNS 記錄和記錄集](dns-operations-recordsets-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="5af2f-148">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
