---
title: "利用 PowerShell 開始使用 Azure DNS | Microsoft Docs"
description: "了解如何在 Azure DNS 中建立 DNS 區域和記錄。 這份逐步指南將引導您使用 PowerShell 建立和管理第一個 DNS 區域和記錄。"
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
ms.openlocfilehash: 48f7ba325f61b4a91c0208b4c99058da801bee19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="dfaa9-104">利用 PowerShell 開始使用 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="dfaa9-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfaa9-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dfaa9-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="dfaa9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfaa9-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="dfaa9-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dfaa9-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="dfaa9-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dfaa9-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="dfaa9-109">本文將逐步引導您使用 Azure PowerShell 建立第一個 DNS 區域和記錄。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-109">This article walks you through the steps to create your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="dfaa9-110">您也可以使用 Azure 入口網站或跨平台 Azure CLI 執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-110">You can also perform these steps using the Azure portal or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="dfaa9-111">DNS 區域用來裝載特定網域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="dfaa9-112">若要開始將網域裝載到 Azure DNS 中，您必須建立該網域名稱的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="dfaa9-113">接著在此 DNS 區域內，建立網域的每筆 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="dfaa9-114">最後，若要將 DNS 區域發佈至網際網路，您需要設定網域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="dfaa9-115">以下說明上述各步驟。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-115">Each of these steps is described below.</span></span>

<span data-ttu-id="dfaa9-116">這些指示假設您已經安裝並登入 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-116">These instructions assume you have already installed and signed in to Azure PowerShell.</span></span> <span data-ttu-id="dfaa9-117">如需說明，請參閱[如何使用 PowerShell 管理 DNS 區域](dns-operations-dnszones.md)。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-117">For help, see [How to manage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="dfaa9-118">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="dfaa9-118">Create the resource group</span></span>

<span data-ttu-id="dfaa9-119">建立 DNS 區域之前，會建立資源群組以包含 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="dfaa9-120">以下顯示命令。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-120">The following shows the command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="dfaa9-121">建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="dfaa9-121">Create a DNS zone</span></span>

<span data-ttu-id="dfaa9-122">使用 `New-AzureRmDnsZone` Cmdlet 建立 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-122">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="dfaa9-123">下列範例會在稱為 MyResourceGroup 的資源群組中建立稱為 contoso.com 的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="dfaa9-124">使用範例來建立 DNS 區域，並將值替換為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-124">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="dfaa9-125">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="dfaa9-125">Create a DNS record</span></span>

<span data-ttu-id="dfaa9-126">您可以使用 `New-AzureRmDnsRecordSet` Cmdlet 來建立記錄集。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-126">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="dfaa9-127">下列範例會在資源群組 "MyResourceGroup" 中的 DNS 區域 "contoso.com" 中，建立具有相對名稱 "www" 的記錄。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-127">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="dfaa9-128">記錄集的完整名稱是 "www.contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-128">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="dfaa9-129">記錄類型為 'A'，IP 位址是 "1.2.3.4"，TTL 為 3600 秒。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-129">The record type is "A", with IP address "1.2.3.4", and the TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="dfaa9-130">關於其他記錄類型、具有多個記錄的記錄集和修改現有的記錄，請參閱[使用 Azure PowerShell 管理 DNS 記錄和記錄集](dns-operations-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-130">For other record types, for record sets with more than one record, and to modify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="dfaa9-131">檢視記錄</span><span class="sxs-lookup"><span data-stu-id="dfaa9-131">View records</span></span>

<span data-ttu-id="dfaa9-132">若要列出區域中的 DNS 記錄，請使用︰</span><span class="sxs-lookup"><span data-stu-id="dfaa9-132">To list the DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="dfaa9-133">更新名稱伺服器</span><span class="sxs-lookup"><span data-stu-id="dfaa9-133">Update name servers</span></span>

<span data-ttu-id="dfaa9-134">當您滿意 DNS 區域且已正確設定記錄之後，您必須設定網域名稱來使用 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="dfaa9-135">這可讓網際網路上的其他使用者找到您的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-135">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="dfaa9-136">`Get-AzureRmDnsZone` Cmdlet 可顯示您的區域的名稱伺服器：</span><span class="sxs-lookup"><span data-stu-id="dfaa9-136">The name servers for your zone are given by the `Get-AzureRmDnsZone` cmdlet:</span></span>

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

<span data-ttu-id="dfaa9-137">這些名稱伺服器應該向網域名稱註冊機構 (您購買網域名稱的來源) 設定。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-137">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="dfaa9-138">您的註冊機構會提供選項來設定網域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-138">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="dfaa9-139">如需詳細資訊，請參閱[將網域委派給 Azure DNS](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-139">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="dfaa9-140">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="dfaa9-140">Delete all resources</span></span>

<span data-ttu-id="dfaa9-141">若要刪除這篇文章中建立的所有資源，請採取下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="dfaa9-141">To delete all resources created in this article, take the following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="dfaa9-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfaa9-142">Next steps</span></span>

<span data-ttu-id="dfaa9-143">若要深入了解 Azure DNS，請參閱 [Azure DNS 概觀](dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-143">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="dfaa9-144">若要深入了解在 Azure DNS 中管理 DNS 區域，請參閱[使用 PowerShell 在 Azure DNS 中管理 DNS 區域](dns-operations-dnszones.md)。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-144">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="dfaa9-145">若要深入了解在 Azure DNS 中管理 DNS 記錄，請參閱[使用 PowerShell 在 Azure DNS 中管理 DNS 記錄和記錄集](dns-operations-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="dfaa9-145">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

