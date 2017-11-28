---
title: "開始使用 PowerShell 的 Azure DNS aaaGet |Microsoft 文件"
description: "深入了解如何 toocreate DNS 區域與在 Azure DNS 記錄。 這是逐步指南 toocreate 和管理您的第一個 DNS 區域，使用 PowerShell 的記錄。"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="4d88f-104">利用 PowerShell 開始使用 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="4d88f-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d88f-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4d88f-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="4d88f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d88f-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="4d88f-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4d88f-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="4d88f-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4d88f-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="4d88f-109">本文將指導您完成 hello 步驟 toocreate 您的第一個 DNS 區域和使用 Azure PowerShell 的記錄。</span><span class="sxs-lookup"><span data-stu-id="4d88f-109">This article walks you through hello steps toocreate your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="4d88f-110">您也可以使用 hello Azure 入口網站執行這些步驟，或 hello 跨平台 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="4d88f-110">You can also perform these steps using hello Azure portal or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="4d88f-111">DNS 區域是使用的 toohost hello 針對特定網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="4d88f-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="4d88f-112">toostart 裝載您的網域在 Azure DNS 中，您需要該網域名稱 toocreate DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="4d88f-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="4d88f-113">接著在此 DNS 區域內，建立網域的每筆 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="4d88f-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="4d88f-114">最後，toopublish 您的 DNS 區域 toohello 網際網路，您需要 tooconfigure hello 名稱伺服器 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="4d88f-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="4d88f-115">以下說明上述各步驟。</span><span class="sxs-lookup"><span data-stu-id="4d88f-115">Each of these steps is described below.</span></span>

<span data-ttu-id="4d88f-116">這些指示假設您已經安裝並登入 tooAzure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4d88f-116">These instructions assume you have already installed and signed in tooAzure PowerShell.</span></span> <span data-ttu-id="4d88f-117">如需說明，請參閱[toomanage DNS 區域使用 PowerShell](dns-operations-dnszones.md)。</span><span class="sxs-lookup"><span data-stu-id="4d88f-117">For help, see [How toomanage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="4d88f-118">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="4d88f-118">Create hello resource group</span></span>

<span data-ttu-id="4d88f-119">建立 hello DNS 區域之前, 建立 toocontain hello DNS 區域資源群組。</span><span class="sxs-lookup"><span data-stu-id="4d88f-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="4d88f-120">hello 下列範例示範 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="4d88f-120">hello following shows hello command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="4d88f-121">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="4d88f-121">Create a DNS zone</span></span>

<span data-ttu-id="4d88f-122">DNS 區域由使用 hello `New-AzureRmDnsZone` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4d88f-122">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="4d88f-123">hello 下列範例會建立 DNS 區域呼叫*contoso.com*呼叫 hello 資源群組中*MyResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="4d88f-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="4d88f-124">使用 hello 範例 toocreate DNS 區域時，取代為您自己的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="4d88f-124">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="4d88f-125">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="4d88f-125">Create a DNS record</span></span>

<span data-ttu-id="4d88f-126">您可以建立資料錄集使用 hello `New-AzureRmDnsRecordSet` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4d88f-126">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="4d88f-127">hello 下列範例會建立一筆記錄 hello 相對名稱"www"hello"contoso.com"，"MyResourceGroup"的資源群組中的 DNS 區域中。</span><span class="sxs-lookup"><span data-stu-id="4d88f-127">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="4d88f-128">hello hello 資料錄集的完整名稱是"www.contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="4d88f-128">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="4d88f-129">hello 記錄類型為"A"，使用 IP 位址"1.2.3.4"，而且 hello TTL 為 3600 秒。</span><span class="sxs-lookup"><span data-stu-id="4d88f-129">hello record type is "A", with IP address "1.2.3.4", and hello TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="4d88f-130">對於其他記錄類型，如記錄設定具有一個以上的記錄，以及 toomodify 現有的記錄，請參閱[管理 DNS 記錄和資料錄集，使用 Azure PowerShell](dns-operations-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="4d88f-130">For other record types, for record sets with more than one record, and toomodify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="4d88f-131">檢視記錄</span><span class="sxs-lookup"><span data-stu-id="4d88f-131">View records</span></span>

<span data-ttu-id="4d88f-132">toolist hello DNS 記錄，在您的區域，使用：</span><span class="sxs-lookup"><span data-stu-id="4d88f-132">toolist hello DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="4d88f-133">更新名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="4d88f-133">Update name servers</span></span>

<span data-ttu-id="4d88f-134">您可以在該程式的 DNS 區域與記錄已設定正確，您需要 tooconfigure 滿足您的網域名稱 toouse hello Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d88f-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="4d88f-135">這可讓其他使用者 hello 網際網路 toofind DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="4d88f-135">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="4d88f-136">hello 名稱伺服器，您的區域會提供 hello `Get-AzureRmDnsZone` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4d88f-136">hello name servers for your zone are given by hello `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="4d88f-137">這些名稱伺服器應該設有 hello 網域名稱註冊機構 （您購買 hello 網域名稱）。</span><span class="sxs-lookup"><span data-stu-id="4d88f-137">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="4d88f-138">您的註冊機構會提供 hello 選項 tooset hello hello 網域名稱伺服器註冊。</span><span class="sxs-lookup"><span data-stu-id="4d88f-138">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="4d88f-139">如需詳細資訊，請參閱[委派您網域 tooAzure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="4d88f-139">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="4d88f-140">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="4d88f-140">Delete all resources</span></span>

<span data-ttu-id="4d88f-141">toodelete 本文採用 hello 下列步驟中建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="4d88f-141">toodelete all resources created in this article, take hello following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4d88f-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d88f-142">Next steps</span></span>

<span data-ttu-id="4d88f-143">toolearn 進一步了解 Azure DNS，請參閱[Azure DNS 概觀](dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4d88f-143">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="4d88f-144">進一步了解管理 Azure DNS 的 DNS 區域 toolearn 看到[Azure DNS 使用 PowerShell 管理 DNS 區域](dns-operations-dnszones.md)。</span><span class="sxs-lookup"><span data-stu-id="4d88f-144">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="4d88f-145">進一步了解管理 Azure DNS 的 DNS 記錄 toolearn 看到[管理 DNS 記錄和記錄設定中使用 PowerShell 的 Azure DNS](dns-operations-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="4d88f-145">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

