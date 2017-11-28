---
title: "aaaManage DNS 記錄中使用 Azure PowerShell 的 Azure DNS |Microsoft 文件"
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
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="05ec1-104">使用 Azure PowerShell 管理 Azure DNS 中的 DNS 記錄和記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="05ec1-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="05ec1-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="05ec1-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="05ec1-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="05ec1-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="05ec1-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="05ec1-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="05ec1-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="05ec1-109">本文章將示範如何 toomanage DNS 記錄您的 DNS 區域使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="05ec1-109">This article shows you how toomanage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="05ec1-110">DNS 記錄也可以使用 hello 跨平台來管理[Azure CLI](dns-operations-recordsets-cli.md)或 hello [Azure 入口網站](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-110">DNS records can also be managed by using hello cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="05ec1-111">本文章中的 hello 範例假設您已經有[安裝 Azure PowerShell，登入，並建立 DNS 區域](dns-operations-dnszones.md)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-111">hello examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="05ec1-112">簡介</span><span class="sxs-lookup"><span data-stu-id="05ec1-112">Introduction</span></span>

<span data-ttu-id="05ec1-113">Azure DNS 中建立 DNS 記錄之前, 您必須先 toounderstand Azure DNS 到 DNS 資料錄集所組織的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="05ec1-113">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="05ec1-114">如需在 Azure DNS 的 DNS 記錄的詳細資訊，請參閱 [DNS 區域與記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="05ec1-115">建立新的 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="05ec1-115">Create a new DNS record</span></span>

<span data-ttu-id="05ec1-116">如果您的新記錄 hello 相同的名稱和型別作為現有的記錄，您需要太[將它加入現有的資料錄集 toohello](#add-a-record-to-an-existing-record-set)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-116">If your new record has hello same name and type as an existing record, you need too[add it toohello existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="05ec1-117">如果您的新記錄有現有的記錄不同名稱和型別 tooall，您會需要 toocreate 新的記錄組。</span><span class="sxs-lookup"><span data-stu-id="05ec1-117">If your new record has a different name and type tooall existing records, you need toocreate a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="05ec1-118">在新的記錄集中建立 'A' 記錄</span><span class="sxs-lookup"><span data-stu-id="05ec1-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="05ec1-119">您可以建立資料錄集使用 hello `New-AzureRmDnsRecordSet` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="05ec1-119">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="05ec1-120">在建立資料錄集時，您需要 toospecify hello 記錄集名稱、 hello 區域、 建立 toolive (TTL)、 hello 記錄類型和 hello 記錄 toobe hello 時間。</span><span class="sxs-lookup"><span data-stu-id="05ec1-120">When creating a record set, you need toospecify hello record set name, hello zone, hello time toolive (TTL), hello record type, and hello records toobe created.</span></span>

<span data-ttu-id="05ec1-121">新增記錄 tooa 資料錄集的 hello 參數 hello hello 資料錄集類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="05ec1-121">hello parameters for adding records tooa record set vary depending on hello type of hello record set.</span></span> <span data-ttu-id="05ec1-122">例如，當使用類型為 'A' 的記錄集合，您需要 toospecify hello IP 位址使用 hello 參數`-IPv4Address`。</span><span class="sxs-lookup"><span data-stu-id="05ec1-122">For example, when using a record set of type 'A', you need toospecify hello IP address using hello parameter `-IPv4Address`.</span></span> <span data-ttu-id="05ec1-123">若是其他記錄類型，則使用其他變數。</span><span class="sxs-lookup"><span data-stu-id="05ec1-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="05ec1-124">請參閱[其他記錄類型範例](#additional-record-type-examples)，以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="05ec1-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="05ec1-125">hello 下列範例會建立之記錄集的 hello 相對名稱 'www' hello 'contoso.com' 的 DNS 區域中。</span><span class="sxs-lookup"><span data-stu-id="05ec1-125">hello following example creates a record set with hello relative name 'www' in hello DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="05ec1-126">hello hello 資料錄集的完整名稱是 'www.contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="05ec1-126">hello fully-qualified name of hello record set is 'www.contoso.com'.</span></span> <span data-ttu-id="05ec1-127">hello 記錄類型為 'A'、 而且 hello TTL 為 3600 秒。</span><span class="sxs-lookup"><span data-stu-id="05ec1-127">hello record type is 'A', and hello TTL is 3600 seconds.</span></span> <span data-ttu-id="05ec1-128">hello 記錄組包含單一記錄，使用 '1.2.3.4' 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="05ec1-128">hello record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="05ec1-129">toocreate 在 hello '' 區域的 apex 區域設定的一筆記錄 (在此情況下，'contoso.com')，使用 hello 記錄集名稱 ' @' （不含引號）：</span><span class="sxs-lookup"><span data-stu-id="05ec1-129">toocreate a record set at hello 'apex' of a zone (in this case, 'contoso.com'), use hello record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="05ec1-130">如果您需要的記錄集包含多個記錄的 toocreate，先建立本機陣列並新增 hello 記錄，然後傳遞 hello 陣列太`New-AzureRmDnsRecordSet`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="05ec1-130">If you need toocreate a record set containing more than one record, first create a local array and add hello records, then pass hello array too`New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="05ec1-131">[設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="05ec1-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="05ec1-132">hello 下列範例示範如何 toocreate 記錄設定兩個中繼資料項目，' dept = finance' 和 ' 環境 = 生產 '。</span><span class="sxs-lookup"><span data-stu-id="05ec1-132">hello following example shows how toocreate a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="05ec1-133">Azure DNS 也支援 'empty' 的資料錄集，可做為預留位置 tooreserve DNS 名稱建立 DNS 記錄之前。</span><span class="sxs-lookup"><span data-stu-id="05ec1-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="05ec1-134">空的資料錄集 hello Azure DNS 控制平面中, 會顯示，但會出現在 hello Azure DNS 名稱伺服器上。</span><span class="sxs-lookup"><span data-stu-id="05ec1-134">Empty record sets are visible in hello Azure DNS control plane, but do appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="05ec1-135">hello 下列範例會建立空的資料錄集：</span><span class="sxs-lookup"><span data-stu-id="05ec1-135">hello following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="05ec1-136">建立其他類型的記錄</span><span class="sxs-lookup"><span data-stu-id="05ec1-136">Create records of other types</span></span>

<span data-ttu-id="05ec1-137">有看到詳細 toocreate 'A' 記錄的方式，下列範例顯示如何 toocreate 記錄的其他記錄類型支援的 Azure DNS hello。</span><span class="sxs-lookup"><span data-stu-id="05ec1-137">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="05ec1-138">在每個案例中，我們會示範如何 toocreate 資料錄集，其中包含單一記錄。</span><span class="sxs-lookup"><span data-stu-id="05ec1-138">In each case, we show how toocreate a record set containing a single record.</span></span> <span data-ttu-id="05ec1-139">hello 'A' 記錄先前的範例可改寫的 toocreate 資料錄集包含多個資料錄，中繼資料，與其他類型的或 toocreate 空白資料錄集。</span><span class="sxs-lookup"><span data-stu-id="05ec1-139">hello earlier examples for 'A' records can be adapted toocreate record sets of other types containing multiple records, with metadata, or toocreate empty record sets.</span></span>

<span data-ttu-id="05ec1-140">我們不會提供範例 toocreate SOA 記錄集，因為 SOAs 會建立和刪除與每個 DNS 區域和無法建立或刪除個別。</span><span class="sxs-lookup"><span data-stu-id="05ec1-140">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="05ec1-141">不過， [SOA 可以修改，在稍後的範例所示的 hello](#to-modify-an-SOA-record)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-141">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="05ec1-142">建立含有單一記錄的 AAAA 記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="05ec1-143">建立含有單一記錄的 CNAME 記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="05ec1-144">hello DNS 標準不允許在 hello 區域的區域的 apex CNAME 記錄 (`-Name '@'`)，也請勿允許包含多個記錄的資料錄集。</span><span class="sxs-lookup"><span data-stu-id="05ec1-144">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="05ec1-145">如需詳細資訊，請參閱 [CNAME 記錄](dns-zones-records.md#cname-records)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="05ec1-146">建立含有單一記錄的 MX 記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="05ec1-147">在此範例中，我們使用 hello 記錄集名稱 ' @' hello 區域的 apex toocreate MX 記錄 (在此情況下，'contoso.com')。</span><span class="sxs-lookup"><span data-stu-id="05ec1-147">In this example, we use hello record set name '@' toocreate an MX record at hello zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="05ec1-148">建立含有單一記錄的 NS 記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="05ec1-149">建立含有單一記錄的 PTR 記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="05ec1-150">在此情況下，' 我-arpa-zone.com' 代表 hello ARPA 反向對應區域，表示您的 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="05ec1-150">In this case, 'my-arpa-zone.com' represents hello ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="05ec1-151">在此區域中設定每個 PTR 記錄對應 tooan 此 IP 範圍內的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="05ec1-151">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span> <span data-ttu-id="05ec1-152">hello 記錄名稱 '10' 是 hello hello IP 位址，由這個記錄此 IP 範圍內的最後一個八位元。</span><span class="sxs-lookup"><span data-stu-id="05ec1-152">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="05ec1-153">建立含有單一記錄的 SRV 記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="05ec1-154">建立時[SRV 記錄集](dns-zones-records.md#srv-records)，指定 hello *\_服務*和*\_通訊協定*hello 中記錄集名稱。</span><span class="sxs-lookup"><span data-stu-id="05ec1-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="05ec1-155">沒有任何需要 tooinclude ' @' 在 hello 記錄設定名稱建立一筆 SRV 記錄於 hello 區域的 apex 設定。</span><span class="sxs-lookup"><span data-stu-id="05ec1-155">There is no need tooinclude '@' in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="05ec1-156">建立含有單一記錄的 TXT 記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="05ec1-157">hello 下列範例顯示如何 toocreate TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="05ec1-157">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="05ec1-158">如需支援 TXT 記錄中的 hello 最大字串長度的詳細資訊，請參閱[TXT 記錄](dns-zones-records.md#txt-records)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-158">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="05ec1-159">取得記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-159">Get a record set</span></span>

<span data-ttu-id="05ec1-160">使用現有的資料錄集，tooretrieve `Get-AzureRmDnsRecordSet`。</span><span class="sxs-lookup"><span data-stu-id="05ec1-160">tooretrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="05ec1-161">此 cmdlet 會傳回代表 hello 記錄 Azure DNS 中設定的本機物件。</span><span class="sxs-lookup"><span data-stu-id="05ec1-161">This cmdlet returns a local object that represents hello record set in Azure DNS.</span></span>

<span data-ttu-id="05ec1-162">如同`New-AzureRmDnsRecordSet`，hello 記錄集名稱必須是*相對*名稱，這表示它必須排除 hello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="05ec1-162">As with `New-AzureRmDnsRecordSet`, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="05ec1-163">您也需要 toospecify hello 記錄類型，並包含 hello 資料錄集的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="05ec1-163">You also need toospecify hello record type, and hello zone containing hello record set.</span></span>

<span data-ttu-id="05ec1-164">hello 下列範例顯示如何 tooretrieve 記錄設定。</span><span class="sxs-lookup"><span data-stu-id="05ec1-164">hello following example shows how tooretrieve a record set.</span></span> <span data-ttu-id="05ec1-165">在此範例中，hello 區域使用指定 hello`-ZoneName`和`-ResourceGroupName`參數。</span><span class="sxs-lookup"><span data-stu-id="05ec1-165">In this example, hello zone is specified using hello `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="05ec1-166">或者，您也可以指定使用區域物件、 使用 hello 傳遞 hello 區域`-Zone`參數。</span><span class="sxs-lookup"><span data-stu-id="05ec1-166">Alternatively, you can also specify hello zone using a zone object, passed using hello `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="05ec1-167">列出記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-167">List record sets</span></span>

<span data-ttu-id="05ec1-168">您也可以使用`Get-AzureRmDnsZone`toolist 記錄在區域中，設定藉由略過 hello`-Name`及/或`-RecordType`參數。</span><span class="sxs-lookup"><span data-stu-id="05ec1-168">You can also use `Get-AzureRmDnsZone` toolist record sets in a zone, by omitting hello `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="05ec1-169">hello 下列範例會傳回所有資料錄集 hello 區域中：</span><span class="sxs-lookup"><span data-stu-id="05ec1-169">hello following example returns all record sets in hello zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="05ec1-170">hello 下列範例示範如何所有記錄給定類型的集合可以擷取時省略 hello 記錄集名稱指定 hello 記錄類型：</span><span class="sxs-lookup"><span data-stu-id="05ec1-170">hello following example shows how all record sets of a given type can be retrieved by specifying hello record type while omitting hello record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="05ec1-171">所有的記錄設定具有指定名稱的 tooretrieve 跨記錄類型，您需要 tooretrieve 所有資料錄集，然後篩選 hello 結果：</span><span class="sxs-lookup"><span data-stu-id="05ec1-171">tooretrieve all record sets with a given name, across record types, you need tooretrieve all record sets and then filter hello results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="05ec1-172">在上述範例的所有 hello，hello 區域可以指定使用 hello`-ZoneName`和`-ResourceGroupName`參數 （如所示），或藉由指定區域物件：</span><span class="sxs-lookup"><span data-stu-id="05ec1-172">In all hello above examples, hello zone can be specified either by using hello `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="05ec1-173">新增記錄 tooan，現有的資料錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-173">Add a record tooan existing record set</span></span>

<span data-ttu-id="05ec1-174">tooadd 記錄 tooan 現有的記錄組，請遵循下列三個步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="05ec1-174">tooadd a record tooan existing record set, follow hello following three steps:</span></span>

1. <span data-ttu-id="05ec1-175">取得 hello 現有資料錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-175">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="05ec1-176">新增 hello 新記錄 toohello 本機記錄集。</span><span class="sxs-lookup"><span data-stu-id="05ec1-176">Add hello new record toohello local record set.</span></span> <span data-ttu-id="05ec1-177">這是一種離線作業。</span><span class="sxs-lookup"><span data-stu-id="05ec1-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="05ec1-178">認可 hello 變更後 toohello Azure DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="05ec1-178">Commit hello change back toohello Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="05ec1-179">使用`Set-AzureRmDnsRecordSet`*取代*hello Azure DNS （與它所包含的所有記錄） 中設定與指定的 hello 資料錄集的現有記錄。</span><span class="sxs-lookup"><span data-stu-id="05ec1-179">Using `Set-AzureRmDnsRecordSet` *replaces* hello existing record set in Azure DNS (and all records it contains) with hello record set specified.</span></span> <span data-ttu-id="05ec1-180">[Etag 檢查](dns-zones-records.md#etags)可用 tooensure 並行的變更不會覆寫。</span><span class="sxs-lookup"><span data-stu-id="05ec1-180">[Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="05ec1-181">您可以使用選擇性的 hello`-Overwrite`切換 toosuppress 這些檢查。</span><span class="sxs-lookup"><span data-stu-id="05ec1-181">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="05ec1-182">這一系列的作業也可以是*經由管道輸出*，這表示您使用 hello 管道，而不是傳遞做為參數傳遞 hello 資料錄集物件：</span><span class="sxs-lookup"><span data-stu-id="05ec1-182">This sequence of operations can also be *piped*, meaning you pass hello record set object by using hello pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="05ec1-183">上述的 hello 範例顯示 tooadd 'A' 記錄 tooan 現有記錄的類型為 'A' 的設定方式。</span><span class="sxs-lookup"><span data-stu-id="05ec1-183">hello examples above show how tooadd an 'A' record tooan existing record set of type 'A'.</span></span> <span data-ttu-id="05ec1-184">類似的作業順序是使用的 tooadd 記錄 toorecord 組的其他類型，以取代 hello`-Ipv4Address`參數`Add-AzureRmDnsRecordConfig`與其他參數 tooeach 特定記錄類型。</span><span class="sxs-lookup"><span data-stu-id="05ec1-184">A similar sequence of operations is used tooadd records toorecord sets of other types, substituting hello `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific tooeach record type.</span></span> <span data-ttu-id="05ec1-185">hello 每個記錄類型的參數是 hello 相同 hello 與`New-AzureRmDnsRecordConfig`cmdlet，如中所示[額外的記錄類型範例](#additional-record-type-examples)上方。</span><span class="sxs-lookup"><span data-stu-id="05ec1-185">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="05ec1-186">類型 'CNAME' 或 'SOA' 的記錄集不能包含多個記錄。</span><span class="sxs-lookup"><span data-stu-id="05ec1-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="05ec1-187">這個條件約束，就會發生來自 hello DNS 標準。</span><span class="sxs-lookup"><span data-stu-id="05ec1-187">This constraint arises from hello DNS standards.</span></span> <span data-ttu-id="05ec1-188">而非 Azure DNS 的限制。</span><span class="sxs-lookup"><span data-stu-id="05ec1-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="05ec1-189">從現有的記錄集移除記錄</span><span class="sxs-lookup"><span data-stu-id="05ec1-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="05ec1-190">hello 程序 tooremove 從資料錄集的記錄會記錄 tooan 現有類似 toohello 程序 tooadd 記錄集：</span><span class="sxs-lookup"><span data-stu-id="05ec1-190">hello process tooremove a record from a record set is similar toohello process tooadd a record tooan existing record set:</span></span>

1. <span data-ttu-id="05ec1-191">取得 hello 現有資料錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-191">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="05ec1-192">移除 hello 記錄從 hello 本機的資料錄集物件。</span><span class="sxs-lookup"><span data-stu-id="05ec1-192">Remove hello record from hello local record set object.</span></span> <span data-ttu-id="05ec1-193">這是一種離線作業。</span><span class="sxs-lookup"><span data-stu-id="05ec1-193">This is an off-line operation.</span></span> <span data-ttu-id="05ec1-194">正在移除的 hello 記錄所有的參數之間必須完全符合的現有記錄。</span><span class="sxs-lookup"><span data-stu-id="05ec1-194">hello record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="05ec1-195">認可 hello 變更後 toohello Azure DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="05ec1-195">Commit hello change back toohello Azure DNS service.</span></span> <span data-ttu-id="05ec1-196">選擇性使用 hello`-Overwrite`切換 toosuppress [Etag 檢查](dns-zones-records.md#etags)並行的變更。</span><span class="sxs-lookup"><span data-stu-id="05ec1-196">Use hello optional `-Overwrite` switch toosuppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="05ec1-197">使用上述順序 tooremove hello 最後一筆記錄的記錄組從 hello 不會刪除 hello 資料錄集，而是會保留空白的資料錄集。</span><span class="sxs-lookup"><span data-stu-id="05ec1-197">Using hello above sequence tooremove hello last record from a record set does not delete hello record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="05ec1-198">tooremove 記錄設定完全，請參閱[刪除記錄集](#delete-a-record-set)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-198">tooremove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="05ec1-199">同樣地 tooadding 記錄 tooa 記錄設定，也可傳送的記錄集的作業 tooremove hello 序列：</span><span class="sxs-lookup"><span data-stu-id="05ec1-199">Similarly tooadding records tooa record set, hello sequence of operations tooremove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="05ec1-200">支援不同的記錄類型傳遞 hello 適當的特定類型的參數太`Remove-AzureRmDnsRecordSet`。</span><span class="sxs-lookup"><span data-stu-id="05ec1-200">Different record types are supported by passing hello appropriate type-specific parameters too`Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="05ec1-201">hello 每個記錄類型的參數是 hello 相同 hello 與`New-AzureRmDnsRecordConfig`cmdlet，如中所示[額外的記錄類型範例](#additional-record-type-examples)上方。</span><span class="sxs-lookup"><span data-stu-id="05ec1-201">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="05ec1-202">修改現有記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-202">Modify an existing record set</span></span>

<span data-ttu-id="05ec1-203">hello 步驟修改現有的資料錄集是從新增或移除的記錄資料錄集時所採取的類似 toohello 步驟：</span><span class="sxs-lookup"><span data-stu-id="05ec1-203">hello steps for modifying an existing record set are similar toohello steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="05ec1-204">擷取 hello 使用設定的現有記錄`Get-AzureRmDnsRecordSet`。</span><span class="sxs-lookup"><span data-stu-id="05ec1-204">Retrieve hello existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="05ec1-205">修改 hello 本機的資料錄集物件：</span><span class="sxs-lookup"><span data-stu-id="05ec1-205">Modify hello local record set object by:</span></span>
    * <span data-ttu-id="05ec1-206">新增或移除記錄</span><span class="sxs-lookup"><span data-stu-id="05ec1-206">Adding or removing records</span></span>
    * <span data-ttu-id="05ec1-207">變更現有記錄的 hello 參數</span><span class="sxs-lookup"><span data-stu-id="05ec1-207">Changing hello parameters of existing records</span></span>
    * <span data-ttu-id="05ec1-208">Hello 記錄變更中繼資料和 toolive 時間 (TTL) 設定</span><span class="sxs-lookup"><span data-stu-id="05ec1-208">Changing hello record set metadata and time toolive (TTL)</span></span>
3. <span data-ttu-id="05ec1-209">認可您的變更，使用 hello `Set-AzureRmDnsRecordSet` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="05ec1-209">Commit your changes by using hello `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="05ec1-210">這*取代*hello Azure DNS 中設定與指定的 hello 資料錄集的現有記錄。</span><span class="sxs-lookup"><span data-stu-id="05ec1-210">This *replaces* hello existing record set in Azure DNS with hello record set specified.</span></span>

<span data-ttu-id="05ec1-211">當使用`Set-AzureRmDnsRecordSet`， [Etag 檢查](dns-zones-records.md#etags)可用 tooensure 並行的變更不會覆寫。</span><span class="sxs-lookup"><span data-stu-id="05ec1-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="05ec1-212">您可以使用選擇性的 hello`-Overwrite`切換 toosuppress 這些檢查。</span><span class="sxs-lookup"><span data-stu-id="05ec1-212">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

### <a name="tooupdate-a-record-in-an-existing-record-set"></a><span data-ttu-id="05ec1-213">tooupdate 現有記錄中的記錄設定</span><span class="sxs-lookup"><span data-stu-id="05ec1-213">tooupdate a record in an existing record set</span></span>

<span data-ttu-id="05ec1-214">在此範例中，我們可以變更現有 'A' 記錄 hello IP 位址：</span><span class="sxs-lookup"><span data-stu-id="05ec1-214">In this example, we change hello IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="05ec1-215">toomodify SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="05ec1-215">toomodify an SOA record</span></span>

<span data-ttu-id="05ec1-216">您無法加入或移除 hello 自動建立在 hello 區域的 apex 設定 SOA 記錄中的記錄 (`-Name "@"`，包括引號)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-216">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="05ec1-217">不過，您可以修改任何 hello （除了 「 主機 」） 的 SOA 記錄中的 hello 參數，而且 hello 記錄設定的 TTL。</span><span class="sxs-lookup"><span data-stu-id="05ec1-217">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

<span data-ttu-id="05ec1-218">下列範例會示範如何 hello toochange hello*電子郵件*hello SOA 記錄的屬性：</span><span class="sxs-lookup"><span data-stu-id="05ec1-218">hello following example shows how toochange hello *Email* property of hello SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="05ec1-219">在 hello 區域的 apex toomodify NS 記錄</span><span class="sxs-lookup"><span data-stu-id="05ec1-219">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="05ec1-220">在 hello 區域的 apex 設定 hello NS 記錄會自動建立與每個 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="05ec1-220">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="05ec1-221">它包含 hello hello Azure DNS 名稱伺服器指派的 toohello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="05ec1-221">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="05ec1-222">您可以加入其他的名稱伺服器 toothis NS 記錄集，toosupport 共同裝載網域使用一個以上的 DNS 提供者。</span><span class="sxs-lookup"><span data-stu-id="05ec1-222">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="05ec1-223">您也可以修改 hello TTL 和此記錄集的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="05ec1-223">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="05ec1-224">不過，您無法移除或修改 hello 預先填入的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="05ec1-224">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="05ec1-225">請注意這適用於僅 toohello NS 記錄集在 hello 區域的 apex。</span><span class="sxs-lookup"><span data-stu-id="05ec1-225">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="05ec1-226">如果沒有限制，您可以修改其他 NS 記錄集在您的區域 （做為使用的 toodelegate 子區域）。</span><span class="sxs-lookup"><span data-stu-id="05ec1-226">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="05ec1-227">hello 下列範例顯示如何 tooadd 其他的名稱伺服器 toohello NS 記錄設定在 hello 區域的 apex:</span><span class="sxs-lookup"><span data-stu-id="05ec1-227">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a><span data-ttu-id="05ec1-228">toomodify 記錄集的中繼資料</span><span class="sxs-lookup"><span data-stu-id="05ec1-228">toomodify record set metadata</span></span>

<span data-ttu-id="05ec1-229">[設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="05ec1-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="05ec1-230">hello 下列範例顯示如何 toomodify hello 中繼資料的現有記錄設定：</span><span class="sxs-lookup"><span data-stu-id="05ec1-230">hello following example shows how toomodify hello metadata of an existing record set:</span></span>

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="05ec1-231">刪除記錄集</span><span class="sxs-lookup"><span data-stu-id="05ec1-231">Delete a record set</span></span>

<span data-ttu-id="05ec1-232">使用 hello 也可以刪除資料錄集`Remove-AzureRmDnsRecordSet`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="05ec1-232">Record sets can be deleted by using hello `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="05ec1-233">刪除資料錄集時，也會刪除 hello 資料錄集內的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="05ec1-233">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="05ec1-234">您無法刪除 hello SOA 和 NS 記錄集在 hello 區域的 apex (`-Name '@'`)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-234">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="05ec1-235">Azure DNS 時，建立這些自動 hello 區域建立，而且已刪除 hello 區域時自動刪除它們。</span><span class="sxs-lookup"><span data-stu-id="05ec1-235">Azure DNS created these automatically when hello zone was created, and deletes them automatically when hello zone is deleted.</span></span>

<span data-ttu-id="05ec1-236">hello 下列範例顯示如何 toodelete 記錄設定。</span><span class="sxs-lookup"><span data-stu-id="05ec1-236">hello following example shows how toodelete a record set.</span></span> <span data-ttu-id="05ec1-237">在此範例中，hello 記錄集名稱、 資料錄集類型、 區域名稱和資源群組會指定每個明確。</span><span class="sxs-lookup"><span data-stu-id="05ec1-237">In this example, hello record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="05ec1-238">或者，您可指定 hello 記錄集名稱和型別，並 hello 區域利用指定的物件：</span><span class="sxs-lookup"><span data-stu-id="05ec1-238">Alternatively, hello record set can be specified by name and type, and hello zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="05ec1-239">做為第三個選項，以 hello 記錄集本身，都可以使用資料錄集物件來指定：</span><span class="sxs-lookup"><span data-stu-id="05ec1-239">As a third option, hello record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="05ec1-240">當您指定 hello 記錄集使用資料錄集物件，刪除 toobe [Etag 檢查](dns-zones-records.md#etags)可用 tooensure 並行的變更不會刪除。</span><span class="sxs-lookup"><span data-stu-id="05ec1-240">When you specify hello record set toobe deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="05ec1-241">您可以使用選擇性的 hello`-Overwrite`切換 toosuppress 這些檢查。</span><span class="sxs-lookup"><span data-stu-id="05ec1-241">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="05ec1-242">也可以送 hello 資料錄集物件而不是傳遞做為參數：</span><span class="sxs-lookup"><span data-stu-id="05ec1-242">hello record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="05ec1-243">確認提示</span><span class="sxs-lookup"><span data-stu-id="05ec1-243">Confirmation prompts</span></span>

<span data-ttu-id="05ec1-244">hello `New-AzureRmDnsRecordSet`， `Set-AzureRmDnsRecordSet`，和`Remove-AzureRmDnsRecordSet`cmdlet 都支援確認提示。</span><span class="sxs-lookup"><span data-stu-id="05ec1-244">hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="05ec1-245">每個 cmdlet 會提示確認如果 hello `$ConfirmPreference` PowerShell 喜好設定變數的值為`Medium`或更低。</span><span class="sxs-lookup"><span data-stu-id="05ec1-245">Each cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="05ec1-246">因為 hello 預設值為`$ConfirmPreference`是`High`，這些提示系統不會提供使用 hello 預設 PowerShell 設定。</span><span class="sxs-lookup"><span data-stu-id="05ec1-246">Since hello default value for `$ConfirmPreference` is `High`, these prompts are not given when using hello default PowerShell settings.</span></span>

<span data-ttu-id="05ec1-247">您可以覆寫 hello 目前`$ConfirmPreference`設定使用 hello`-Confirm`參數。</span><span class="sxs-lookup"><span data-stu-id="05ec1-247">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="05ec1-248">如果您指定`-Confirm`或`-Confirm:$True`，hello cmdlet 會提示您確認再它執行。</span><span class="sxs-lookup"><span data-stu-id="05ec1-248">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="05ec1-249">如果您指定`-Confirm:$False`，hello cmdlet 不會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="05ec1-249">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="05ec1-250">如需 `-Confirm` 和 `$ConfirmPreference` 的詳細資訊，請參閱[有關喜好設定變數](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05ec1-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05ec1-251">Next steps</span></span>

<span data-ttu-id="05ec1-252">深入了解[ Azure DNS 中的區域和記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="05ec1-253">了解如何太[保護您的區域和記錄](dns-protect-zones-recordsets.md)時使用 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="05ec1-253">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="05ec1-254">檢閱 hello [Azure DNS PowerShell 參考文件](/powershell/module/azurerm.dns)。</span><span class="sxs-lookup"><span data-stu-id="05ec1-254">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
