---
title: "使用 Azure PowerShell 管理 Azure DNS 中的 DNS 記錄 | Microsoft Docs"
description: "將網域裝載於 Azure DNS 時，在 Azure DNS 管理 DNS 記錄集和記錄。 對記錄集和記錄執行作業的所有 PowerShell 命令。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 2962e30e5d9c60b8e786e2ba79647cabfc5925cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="38e7a-104">使用 Azure PowerShell 管理 Azure DNS 中的 DNS 記錄和記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="38e7a-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="38e7a-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="38e7a-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="38e7a-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="38e7a-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="38e7a-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="38e7a-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38e7a-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="38e7a-109">本文說明如何使用 Azure PowerShell 來管理 DNS 區域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="38e7a-109">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="38e7a-110">也可以使用跨平台 [Azure CLI](dns-operations-recordsets-cli.md) 或 [Azure 入口網站](dns-operations-recordsets-portal.md)來管理 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="38e7a-110">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="38e7a-111">此文章中的範例假設您已[安裝 Azure PowerShell、登入，並建立 DNS 區域](dns-operations-dnszones.md)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-111">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="38e7a-112">簡介</span><span class="sxs-lookup"><span data-stu-id="38e7a-112">Introduction</span></span>

<span data-ttu-id="38e7a-113">在 Azure DNS 中建立 DNS 記錄前，您需要先了解 Azure DNS 如何將 DNS 記錄組織成 DNS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-113">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="38e7a-114">如需在 Azure DNS 的 DNS 記錄的詳細資訊，請參閱 [DNS 區域與記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="38e7a-115">建立新的 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="38e7a-115">Create a new DNS record</span></span>

<span data-ttu-id="38e7a-116">如果新記錄的名稱和類型與現有記錄相同，您需要[將它新增至現有的記錄集](#add-a-record-to-an-existing-record-set)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-116">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="38e7a-117">否則，如果新記錄的名稱和類型與現有記錄不同，則必須建立新的記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-117">If your new record has a different name and type to all existing records, you need to create a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="38e7a-118">在新的記錄集中建立 'A' 記錄</span><span class="sxs-lookup"><span data-stu-id="38e7a-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="38e7a-119">您可以使用 `New-AzureRmDnsRecordSet` Cmdlet 來建立記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-119">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="38e7a-120">建立記錄集時，您必須指定記錄集名稱、區域、存留時間 (TTL) 和記錄類型，與要建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="38e7a-120">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span></span>

<span data-ttu-id="38e7a-121">將記錄加入至記錄集的參數，根據記錄集的類型而所有不同。</span><span class="sxs-lookup"><span data-stu-id="38e7a-121">The parameters for adding records to a record set vary depending on the type of the record set.</span></span> <span data-ttu-id="38e7a-122">例如，使用 'A' 類型的記錄集時，您需要使用參數 `-IPv4Address` 來指定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="38e7a-122">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span></span> <span data-ttu-id="38e7a-123">若是其他記錄類型，則使用其他變數。</span><span class="sxs-lookup"><span data-stu-id="38e7a-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="38e7a-124">請參閱[其他記錄類型範例](#additional-record-type-examples)，以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="38e7a-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="38e7a-125">下列範例會在 DNS 區域 'contoso.com' 中建立具有相對名稱 'www' 的記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-125">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="38e7a-126">記錄集的完整名稱是 'www.contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="38e7a-126">The fully-qualified name of the record set is 'www.contoso.com'.</span></span> <span data-ttu-id="38e7a-127">記錄類型為 'A'，且 TTL 為 3600 秒。</span><span class="sxs-lookup"><span data-stu-id="38e7a-127">The record type is 'A', and the TTL is 3600 seconds.</span></span> <span data-ttu-id="38e7a-128">此記錄集都會包含一筆記錄，其中 IP 位址為 '1.2.3.4'。</span><span class="sxs-lookup"><span data-stu-id="38e7a-128">The record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="38e7a-129">若要在區域頂點 (在此案例中為 'contoso.com') 建立記錄集，請使用記錄集名稱 '@' (不包括引號)：</span><span class="sxs-lookup"><span data-stu-id="38e7a-129">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="38e7a-130">如果您需要建立包含多筆記錄的記錄集，請先建立本機陣列並新增記錄，然後將陣列傳遞給 `New-AzureRmDnsRecordSet`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="38e7a-130">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="38e7a-131">[記錄集中繼資料](dns-zones-records.md#tags-and-metadata)可用來將應用程式特定資料與每一個資料集產生關聯 (以索引鍵值組的形式)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="38e7a-132">下列範例示範如何建立具有兩個中繼資料項目 ('dept=finance' 與 'environment=production') 的記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-132">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="38e7a-133">Azure DNS 也支援 'empty' 記錄集，此可作為建立 DNS 記錄前保留 DNS 名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="38e7a-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="38e7a-134">空記錄集會顯示在 Azure DNS 控制面板中，但不會出現在 Azure DNS 名稱伺服器上。</span><span class="sxs-lookup"><span data-stu-id="38e7a-134">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span></span> <span data-ttu-id="38e7a-135">下列範例會建立空記錄集：</span><span class="sxs-lookup"><span data-stu-id="38e7a-135">The following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="38e7a-136">建立其他類型的記錄</span><span class="sxs-lookup"><span data-stu-id="38e7a-136">Create records of other types</span></span>

<span data-ttu-id="38e7a-137">參閱如何建立 'A' 記錄的詳細資訊後，下列範例會示範如何建立 Azure DNS 所支援其他記錄類型的記錄。</span><span class="sxs-lookup"><span data-stu-id="38e7a-137">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="38e7a-138">在每個案例中，我們會說明如何建立包含單一記錄的記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-138">In each case, we show how to create a record set containing a single record.</span></span> <span data-ttu-id="38e7a-139">可將 'A' 記錄的先前範例加以調整，即可建立含多個記錄的其他類型記錄集、具中繼資料的其他類型記錄集，或建立空的記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-139">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span></span>

<span data-ttu-id="38e7a-140">我們沒有提供 SOA 記錄集的建立範例，因為已與每一個 DNS 區域完成 SOA 建立與刪除，且無法個別建立或刪除 SOA。</span><span class="sxs-lookup"><span data-stu-id="38e7a-140">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="38e7a-141">然而，[可以對 SOA 進行修改，如稍後範例所示](#to-modify-an-SOA-record)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-141">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="38e7a-142">建立含有單一記錄的 AAAA 記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="38e7a-143">建立含有單一記錄的 CNAME 記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="38e7a-144">DNS 標準在區域頂點不允許 CNAME 記錄 (`-Name '@'`)，也不允許包含一個記錄以上的記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-144">The DNS standards do not permit CNAME records at the apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="38e7a-145">如需詳細資訊，請參閱 [CNAME 記錄](dns-zones-records.md#cname-records)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="38e7a-146">建立含有單一記錄的 MX 記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="38e7a-147">在此範例中，我們使用記錄集名稱 '@' 在區域頂點建立 MX 記錄 (在此案例中為 'contoso.com')。</span><span class="sxs-lookup"><span data-stu-id="38e7a-147">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="38e7a-148">建立含有單一記錄的 NS 記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="38e7a-149">建立含有單一記錄的 PTR 記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="38e7a-150">在此情況下，'my-arpa-zone.com' 代表表示您 IP 範圍的 ARPA 反向對應區域。</span><span class="sxs-lookup"><span data-stu-id="38e7a-150">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="38e7a-151">此區域中的每個 PTR 記錄集都與此 IP 範圍內的一個 IP 位址相對應。</span><span class="sxs-lookup"><span data-stu-id="38e7a-151">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span> <span data-ttu-id="38e7a-152">記錄名稱 '10' 是此記錄所代表的這個 IP 範圍內 IP 位址的最後一個八位元。</span><span class="sxs-lookup"><span data-stu-id="38e7a-152">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="38e7a-153">建立含有單一記錄的 SRV 記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="38e7a-154">建立 [SRV 記錄集](dns-zones-records.md#srv-records)時，指定記錄集名稱中的 *\_服務* 和 *\_通訊協定*。</span><span class="sxs-lookup"><span data-stu-id="38e7a-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="38e7a-155">在區域頂點建立一筆 SRV 記錄集時，不需要在記錄集名稱中包含 '@'。</span><span class="sxs-lookup"><span data-stu-id="38e7a-155">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="38e7a-156">建立含有單一記錄的 TXT 記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="38e7a-157">下列範例示範如何建立 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="38e7a-157">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="38e7a-158">如需 TXT 記錄中，所支援字串長度上限的相關資訊，請參閱 [TXT 記錄](dns-zones-records.md#txt-records)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-158">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="38e7a-159">取得記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-159">Get a record set</span></span>

<span data-ttu-id="38e7a-160">若要擷取現有的記錄集，使用 `Get-AzureRmDnsRecordSet`。</span><span class="sxs-lookup"><span data-stu-id="38e7a-160">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="38e7a-161">此 cmdlet 會傳回 Azure DNS 中代表記錄集的本機物件。</span><span class="sxs-lookup"><span data-stu-id="38e7a-161">This cmdlet returns a local object that represents the record set in Azure DNS.</span></span>

<span data-ttu-id="38e7a-162">如同 `New-AzureRmDnsRecordSet`，提供的記錄集名稱必須是*相對*名稱，表示它不能包含區域名稱。</span><span class="sxs-lookup"><span data-stu-id="38e7a-162">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="38e7a-163">您也必須指定記錄類型，以及包含記錄集的區域。</span><span class="sxs-lookup"><span data-stu-id="38e7a-163">You also need to specify the record type, and the zone containing the record set.</span></span>

<span data-ttu-id="38e7a-164">下列範例示範如何擷取記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-164">The following example shows how to retrieve a record set.</span></span> <span data-ttu-id="38e7a-165">在此範例中，使用 `-ZoneName` 和 `-ResourceGroupName` 參數來指定區域。</span><span class="sxs-lookup"><span data-stu-id="38e7a-165">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="38e7a-166">或者，您也可以使用 `-Zone` 參數傳遞的區域物件來指定區域。</span><span class="sxs-lookup"><span data-stu-id="38e7a-166">Alternatively, you can also specify the zone using a zone object, passed using the `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="38e7a-167">列出記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-167">List record sets</span></span>

<span data-ttu-id="38e7a-168">您也可以使用 `Get-AzureRmDnsZone`，透過省略 `-Name` 及/或 `-RecordType` 參數，在區域中列出記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-168">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="38e7a-169">下列範例會傳回區域中的所有記錄集︰</span><span class="sxs-lookup"><span data-stu-id="38e7a-169">The following example returns all record sets in the zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="38e7a-170">下列範例示範將記錄集名稱省略時，如何透過指定記錄類型來擷取指定類型的所有記錄集：</span><span class="sxs-lookup"><span data-stu-id="38e7a-170">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="38e7a-171">若要擷取所有記錄類型中，具有指定名稱的所有記錄集，您必須擷取所有記錄集，然後篩選結果︰</span><span class="sxs-lookup"><span data-stu-id="38e7a-171">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="38e7a-172">在以上所有範例中，您可以使用 `-ZoneName` 和 `-ResourceGroupName` 參數來指定區域 (如上所示)，或透過指定區域物件來指定：</span><span class="sxs-lookup"><span data-stu-id="38e7a-172">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="38e7a-173">將記錄新增至現有的記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-173">Add a record to an existing record set</span></span>

<span data-ttu-id="38e7a-174">若要將記錄新增至現有的記錄集，請遵循下列三個步驟︰</span><span class="sxs-lookup"><span data-stu-id="38e7a-174">To add a record to an existing record set, follow the following three steps:</span></span>

1. <span data-ttu-id="38e7a-175">取得現有記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-175">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="38e7a-176">將新記錄新增至本機記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-176">Add the new record to the local record set.</span></span> <span data-ttu-id="38e7a-177">這是一種離線作業。</span><span class="sxs-lookup"><span data-stu-id="38e7a-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="38e7a-178">將對變更的認可傳回給 Azure DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="38e7a-178">Commit the change back to the Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="38e7a-179">使用 `Set-AzureRmDnsRecordSet`，用指定的記錄集*取代* Azure DNS 中現有的記錄集 (與其中所包含的所有記錄)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-179">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span></span> <span data-ttu-id="38e7a-180">[Etag 檢查 ](dns-zones-records.md#etags) 是用來確保並行變更不會遭到覆寫。</span><span class="sxs-lookup"><span data-stu-id="38e7a-180">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="38e7a-181">您可以使用選擇性的 `-Overwrite` 參數來停用這些檢查。</span><span class="sxs-lookup"><span data-stu-id="38e7a-181">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="38e7a-182">作業的此序列也可以「經由管道輸送」，亦即使用管道傳遞記錄集物件，而不是以參數進行傳遞。</span><span class="sxs-lookup"><span data-stu-id="38e7a-182">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="38e7a-183">上述範例顯示如何將 'A' 記錄新增至類型 'A' 的現有記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-183">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span></span> <span data-ttu-id="38e7a-184">作業的類似序列也可用來將記錄新增至其他類型的記錄集，可透過每一個記錄類型專屬的其他變數取代 `Add-AzureRmDnsRecordConfig` 的 `-Ipv4Address` 變數。</span><span class="sxs-lookup"><span data-stu-id="38e7a-184">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span></span> <span data-ttu-id="38e7a-185">每個記錄類型的參數對 `New-AzureRmDnsRecordConfig`cmdlet 而言是相同的，如以上[其他記錄類型範例](#additional-record-type-examples)所示。</span><span class="sxs-lookup"><span data-stu-id="38e7a-185">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="38e7a-186">類型 'CNAME' 或 'SOA' 的記錄集不能包含多個記錄。</span><span class="sxs-lookup"><span data-stu-id="38e7a-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="38e7a-187">這個條件是起因於 DNS 標準。</span><span class="sxs-lookup"><span data-stu-id="38e7a-187">This constraint arises from the DNS standards.</span></span> <span data-ttu-id="38e7a-188">而非 Azure DNS 的限制。</span><span class="sxs-lookup"><span data-stu-id="38e7a-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="38e7a-189">從現有的記錄集移除記錄</span><span class="sxs-lookup"><span data-stu-id="38e7a-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="38e7a-190">從記錄集移除記錄的程序，與將記錄新增至現有記錄集的程序類似︰</span><span class="sxs-lookup"><span data-stu-id="38e7a-190">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span></span>

1. <span data-ttu-id="38e7a-191">取得現有記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-191">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="38e7a-192">從本機記錄集物件中移除記錄。</span><span class="sxs-lookup"><span data-stu-id="38e7a-192">Remove the record from the local record set object.</span></span> <span data-ttu-id="38e7a-193">這是一種離線作業。</span><span class="sxs-lookup"><span data-stu-id="38e7a-193">This is an off-line operation.</span></span> <span data-ttu-id="38e7a-194">要移除的記錄必須完全符合現有的資料錄，包括所有參數。</span><span class="sxs-lookup"><span data-stu-id="38e7a-194">The record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="38e7a-195">將對變更的認可傳回給 Azure DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="38e7a-195">Commit the change back to the Azure DNS service.</span></span> <span data-ttu-id="38e7a-196">使用選擇性 `-Overwrite` 參數來停止對並行變更的 [Etag 檢查](dns-zones-records.md#etags)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-196">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="38e7a-197">使用上述序列，將最後一筆記錄從記錄集中移除並不會刪除記錄集，而是會留下空的記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-197">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="38e7a-198">若要完全移除記錄集，請參閱[刪除記錄集](#delete-a-record-set)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-198">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="38e7a-199">與將記錄新增至記錄集的方式類似，移除記錄集的作業序列也可以管道輸送︰</span><span class="sxs-lookup"><span data-stu-id="38e7a-199">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="38e7a-200">藉由將特定類型的適當參數傳遞至 `Remove-AzureRmDnsRecordSet`，以支援不同的記錄類型。</span><span class="sxs-lookup"><span data-stu-id="38e7a-200">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="38e7a-201">每個記錄類型的參數對 `New-AzureRmDnsRecordConfig`cmdlet 而言是相同的，如以上[其他記錄類型範例](#additional-record-type-examples)所示。</span><span class="sxs-lookup"><span data-stu-id="38e7a-201">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="38e7a-202">修改現有記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-202">Modify an existing record set</span></span>

<span data-ttu-id="38e7a-203">修改現有記錄集的步驟，與從記錄集新增或移除記錄時所採取的步驟相類似：</span><span class="sxs-lookup"><span data-stu-id="38e7a-203">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="38e7a-204">使用 `Get-AzureRmDnsRecordSet`擷取現有的記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-204">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="38e7a-205">透過下列方式修改本機記錄集︰</span><span class="sxs-lookup"><span data-stu-id="38e7a-205">Modify the local record set object by:</span></span>
    * <span data-ttu-id="38e7a-206">新增或移除記錄</span><span class="sxs-lookup"><span data-stu-id="38e7a-206">Adding or removing records</span></span>
    * <span data-ttu-id="38e7a-207">變更現有記錄的參數</span><span class="sxs-lookup"><span data-stu-id="38e7a-207">Changing the parameters of existing records</span></span>
    * <span data-ttu-id="38e7a-208">變更記錄集中繼資料和存留時間 (TTL)</span><span class="sxs-lookup"><span data-stu-id="38e7a-208">Changing the record set metadata and time to live (TTL)</span></span>
3. <span data-ttu-id="38e7a-209">使用 `Set-AzureRmDnsRecordSet` Cmdlet 來認可您所做的變更。</span><span class="sxs-lookup"><span data-stu-id="38e7a-209">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="38e7a-210">這會以指定的記錄集*取代* Azure DNS 中現有的記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-210">This *replaces* the existing record set in Azure DNS with the record set specified.</span></span>

<span data-ttu-id="38e7a-211">使用 `Set-AzureRmDnsRecordSet` 時，會使用 [Etag 檢查](dns-zones-records.md#etags) 來確保不會覆寫並行變更。</span><span class="sxs-lookup"><span data-stu-id="38e7a-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="38e7a-212">您可以使用選擇性的 `-Overwrite` 參數來停用這些檢查。</span><span class="sxs-lookup"><span data-stu-id="38e7a-212">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

### <a name="to-update-a-record-in-an-existing-record-set"></a><span data-ttu-id="38e7a-213">更新現有記錄集中的記錄</span><span class="sxs-lookup"><span data-stu-id="38e7a-213">To update a record in an existing record set</span></span>

<span data-ttu-id="38e7a-214">在此範例中，我們會變更現有 'A' 記錄的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="38e7a-214">In this example, we change the IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="38e7a-215">修改 SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="38e7a-215">To modify an SOA record</span></span>

<span data-ttu-id="38e7a-216">您無法在區域頂點 (`-Name "@"` (包含引號)) 從自動建立的 SOA 記錄集中新增或移除記錄。</span><span class="sxs-lookup"><span data-stu-id="38e7a-216">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="38e7a-217">不過，您可以修改 SOA 記錄 (「主機」除外) 和記錄集 TTL 內的任何參數。</span><span class="sxs-lookup"><span data-stu-id="38e7a-217">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

<span data-ttu-id="38e7a-218">下列範例示範如何變更 SOA 記錄的 *Email* 屬性：</span><span class="sxs-lookup"><span data-stu-id="38e7a-218">The following example shows how to change the *Email* property of the SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="38e7a-219">在區域頂點修改 NS 記錄</span><span class="sxs-lookup"><span data-stu-id="38e7a-219">To modify NS records at the zone apex</span></span>

<span data-ttu-id="38e7a-220">系統會自動使用每個 DNS 區域在區域頂點建立 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-220">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="38e7a-221">此記錄集包含指派給區域的 Azure DNS 名稱伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="38e7a-221">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="38e7a-222">您可以將其他名稱伺服器新增至此 NS 記錄集，以支援使用多個 DNS 提供者的共同裝載網域。</span><span class="sxs-lookup"><span data-stu-id="38e7a-222">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="38e7a-223">您也可以修改此記錄集的 TTL 和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="38e7a-223">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="38e7a-224">不過，您無法移除或修改預先填入的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="38e7a-224">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="38e7a-225">請注意，這只適用於區域頂點的 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-225">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="38e7a-226">區域中的其他 NS 記錄集 (如用於委派子區域) 可以修改，沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="38e7a-226">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="38e7a-227">下列範例顯示如何將其他的名稱伺服器新增至在區域頂點的 NS 記錄集：</span><span class="sxs-lookup"><span data-stu-id="38e7a-227">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-record-set-metadata"></a><span data-ttu-id="38e7a-228">若要修改記錄集中繼資料</span><span class="sxs-lookup"><span data-stu-id="38e7a-228">To modify record set metadata</span></span>

<span data-ttu-id="38e7a-229">[記錄集中繼資料](dns-zones-records.md#tags-and-metadata)可用來將應用程式特定資料與每一個資料集產生關聯 (以索引鍵值組的形式)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="38e7a-230">下列範例示範如何修改現有記錄集的中繼資料︰</span><span class="sxs-lookup"><span data-stu-id="38e7a-230">The following example shows how to modify the metadata of an existing record set:</span></span>

```powershell
# Get the record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="38e7a-231">刪除記錄集</span><span class="sxs-lookup"><span data-stu-id="38e7a-231">Delete a record set</span></span>

<span data-ttu-id="38e7a-232">您可以使用 `Remove-AzureRmDnsRecordSet` Cmdlet 來刪除記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-232">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="38e7a-233">刪除記錄集時，也會刪除記錄集內的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="38e7a-233">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="38e7a-234">您無法在區域頂點 (`-Name '@'`) 刪除 SOA 和 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-234">You cannot delete the SOA and NS record sets at the zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="38e7a-235">Azure DNS 在區域建立時就自動建立了這些項目，並且會在區域刪除時自動刪除這些項目。</span><span class="sxs-lookup"><span data-stu-id="38e7a-235">Azure DNS created these automatically when the zone was created, and deletes them automatically when the zone is deleted.</span></span>

<span data-ttu-id="38e7a-236">下列範例說明如何刪除記錄集。</span><span class="sxs-lookup"><span data-stu-id="38e7a-236">The following example shows how to delete a record set.</span></span> <span data-ttu-id="38e7a-237">在此範例中，記錄集名稱、記錄集類型、區域名稱和資源群組是個別明確指定。</span><span class="sxs-lookup"><span data-stu-id="38e7a-237">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="38e7a-238">或者，可以透過名稱、類型，和使用物件指定的區域，來指定記錄集︰</span><span class="sxs-lookup"><span data-stu-id="38e7a-238">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="38e7a-239">至於第三個選項，記錄集本身即可透過記錄集物件進行指定︰</span><span class="sxs-lookup"><span data-stu-id="38e7a-239">As a third option, the record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="38e7a-240">將記錄集的刪除方式指定為使用記錄集物件時，則會使用 [Etag 檢查](dns-zones-records.md#etags)，來確保不會刪除並行變更。</span><span class="sxs-lookup"><span data-stu-id="38e7a-240">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="38e7a-241">您可以使用選擇性的 `-Overwrite` 參數來停用這些檢查。</span><span class="sxs-lookup"><span data-stu-id="38e7a-241">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="38e7a-242">記錄集物件也可以經由管道輸送，而不是當做參數傳遞：</span><span class="sxs-lookup"><span data-stu-id="38e7a-242">The record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="38e7a-243">確認提示</span><span class="sxs-lookup"><span data-stu-id="38e7a-243">Confirmation prompts</span></span>

<span data-ttu-id="38e7a-244">`New-AzureRmDnsRecordSet`、`Set-AzureRmDnsRecordSet` 和 `Remove-AzureRmDnsRecordSet` cmdlets 皆支援確認提示。</span><span class="sxs-lookup"><span data-stu-id="38e7a-244">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="38e7a-245">如果 `$ConfirmPreference`PowerShell 喜好設定變數的值為 `Medium` 或更低，則每個 cmdlet 會提示確認。</span><span class="sxs-lookup"><span data-stu-id="38e7a-245">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="38e7a-246">因為 `$ConfirmPreference` 的預設值為 `High`，使用預設 PowerShell 設定時不會出現這些提示。</span><span class="sxs-lookup"><span data-stu-id="38e7a-246">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span></span>

<span data-ttu-id="38e7a-247">您可以使用 `-Confirm` 參數覆寫目前 `$ConfirmPreference` 設定。</span><span class="sxs-lookup"><span data-stu-id="38e7a-247">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="38e7a-248">如果您指定 `-Confirm` 或 `-Confirm:$True`，此 cmdlet 在執行前會提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="38e7a-248">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="38e7a-249">如果您指定 `-Confirm:$False`，此 cmdlet 不會提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="38e7a-249">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="38e7a-250">如需 `-Confirm` 和 `$ConfirmPreference` 的詳細資訊，請參閱[有關喜好設定變數](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38e7a-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38e7a-251">Next steps</span></span>

<span data-ttu-id="38e7a-252">深入了解[ Azure DNS 中的區域和記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="38e7a-253">了解使用 Azure DNS 時，如何[保護區域和記錄](dns-protect-zones-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-253">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="38e7a-254">檢閱 [Azure DNS PowerShell 參考文件](/powershell/module/azurerm.dns)。</span><span class="sxs-lookup"><span data-stu-id="38e7a-254">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
