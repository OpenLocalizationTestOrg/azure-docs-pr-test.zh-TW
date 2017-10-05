---
title: "使用 Azure CLI 2.0 管理 Azure DNS 中的 DNS 記錄 | Microsoft Docs"
description: "將網域裝載於 Azure DNS 時，在 Azure DNS 管理 DNS 記錄集和記錄。 對記錄集和記錄執行作業的所有 CLI 2.0 命令。"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9543759d7ba88c7c5068021cebbeec6b8d63633e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="7fe19-104">使用 Azure CLI 2.0 管理 Azure DNS 中的 DNS 記錄和記錄集</span><span class="sxs-lookup"><span data-stu-id="7fe19-104">Manage DNS records and recordsets in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7fe19-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7fe19-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="7fe19-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7fe19-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="7fe19-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7fe19-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="7fe19-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fe19-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="7fe19-109">本文適用於 Windows、Mac 和 Linux，將會說明如何使用跨平台 Azure 命令列介面 (CLI) 2.0 管理 DNS 區域的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="7fe19-110">您也可以使用 [Azure PowerShell](dns-operations-recordsets.md) 或 [Azure 入口網站](dns-operations-recordsets-portal.md)來管理 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="7fe19-111">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="7fe19-111">CLI versions to complete the task</span></span>

<span data-ttu-id="7fe19-112">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="7fe19-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="7fe19-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - 適用於傳統和資源管理部署模型的 CLI。</span><span class="sxs-lookup"><span data-stu-id="7fe19-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="7fe19-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - 適用於資源管理部署模型的新一代 CLI。</span><span class="sxs-lookup"><span data-stu-id="7fe19-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="7fe19-115">此文章中的範例假設您已[安裝 Azure CLI 2.0、登入，並建立 DNS 區域](dns-operations-dnszones-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-115">The examples in this article assume you have already [installed the Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="7fe19-116">簡介</span><span class="sxs-lookup"><span data-stu-id="7fe19-116">Introduction</span></span>

<span data-ttu-id="7fe19-117">在 Azure DNS 中建立 DNS 記錄前，您需要先了解 Azure DNS 如何將 DNS 記錄組織成 DNS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="7fe19-118">如需在 Azure DNS 的 DNS 記錄的詳細資訊，請參閱 [DNS 區域與記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="7fe19-119">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-119">Create a DNS record</span></span>

<span data-ttu-id="7fe19-120">若要建立 DNS 記錄，請使用 `az network dns record-set <record-type> set-record` 命令 (其中 `<record-type>` 是記錄的類型，亦即</span><span class="sxs-lookup"><span data-stu-id="7fe19-120">To create a DNS record, use the `az network dns record-set <record-type> set-record` command (where `<record-type>` is the type of record, i.e</span></span> <span data-ttu-id="7fe19-121">a、srv、txt 等等。)如需協助，請參閱 `az network dns record-set --help`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="7fe19-122">建立記錄時，您必須指定資源群組名稱、區域名稱、記錄集名稱、記錄類型，以及所建立記錄的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7fe19-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="7fe19-123">提供的記錄集名稱必須是「相對」名稱，表示它不能包含區域名稱。</span><span class="sxs-lookup"><span data-stu-id="7fe19-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="7fe19-124">如果記錄集不存在，此命令會為您建立。</span><span class="sxs-lookup"><span data-stu-id="7fe19-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="7fe19-125">如果記錄集已經存在，此命令會將您指定的記錄新增至現有的記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-125">If the record set already exists, this command adds the record you specify to the existing record set.</span></span>

<span data-ttu-id="7fe19-126">如果建立新的記錄集，則會使用預設存留時間 (TTL) 3600。</span><span class="sxs-lookup"><span data-stu-id="7fe19-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="7fe19-127">如需如何使用不同 TTL 的指示，請參閱[建立 DNS 記錄集](#create-a-dns-record-set)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="7fe19-128">下列範例會在 MyResourceGroup 資源群組的 contoso.com 區域中建立稱為 www 的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="7fe19-129">A 記錄的 IP 位址是 1.2.3.4。</span><span class="sxs-lookup"><span data-stu-id="7fe19-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="7fe19-130">若要在區域頂點 (在此案例中為 "contoso.com") 建立記錄集，請使用記錄名稱 "@" (包括引號)：</span><span class="sxs-lookup"><span data-stu-id="7fe19-130">To create a record set in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="7fe19-131">建立 DNS 記錄集</span><span class="sxs-lookup"><span data-stu-id="7fe19-131">Create a DNS record set</span></span>

<span data-ttu-id="7fe19-132">在上述範例中，DNS 記錄不是新增至現有記錄集，就是記錄集是以*隱含方式*建立。</span><span class="sxs-lookup"><span data-stu-id="7fe19-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="7fe19-133">您也可以先*明確地*建立記錄集，再於其中新增記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="7fe19-134">Azure DNS 支援「空白」記錄集，其可做為預留位置，以在建立 DNS 記錄之前保留 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="7fe19-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="7fe19-135">空白記錄集可在 Azure DNS 控制面板中看到，但不會出現在 Azure DNS 名稱伺服器上。</span><span class="sxs-lookup"><span data-stu-id="7fe19-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="7fe19-136">請使用 `az network dns record-set <record-type> create` 命令建立記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-136">Record sets are created using the `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="7fe19-137">如需協助，請參閱 `az network dns record-set <record-type> create --help`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="7fe19-138">明確地建立記錄集可讓您指定記錄集屬性，例如[存留時間 (TTL)](dns-zones-records.md#time-to-live) 和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7fe19-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="7fe19-139">[記錄集中繼資料](dns-zones-records.md#tags-and-metadata)可用來將應用程式特定資料與每一個資料集產生關聯 (以索引鍵值組的形式)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="7fe19-140">下列範例使用 `--ttl` 參數 (簡短形式 `-l`)，建立類型「A」且 60 秒 TTL 的空白記錄集：</span><span class="sxs-lookup"><span data-stu-id="7fe19-140">The following example creates an empty record set of type 'A' with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="7fe19-141">下列範例使用 `--metadata` 參數建立具有兩個中繼資料項目 ("dept=finance" 和 "environment=production") 的記錄集：</span><span class="sxs-lookup"><span data-stu-id="7fe19-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="7fe19-142">建立好空白記錄集之後，可依[建立 DNS 記錄](#create-a-dns-record)所述使用 `azure network dns record-set <record-type> set-record` 新增記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="7fe19-143">建立其他類型的記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-143">Create records of other types</span></span>

<span data-ttu-id="7fe19-144">參閱如何建立 'A' 記錄的詳細資訊後，下列範例會示範如何建立 Azure DNS 所支援其他記錄類型的記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="7fe19-145">用來指定記錄資料的參數，根據記錄的類型而所有不同。</span><span class="sxs-lookup"><span data-stu-id="7fe19-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="7fe19-146">例如，對於類型 "A" 的記錄，您可使用參數 `--ipv4-address <IPv4 address>` 指定 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="7fe19-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="7fe19-147">每個記錄類型的參數可以使用 `az network dns record-set <record-type> set-record --help` 列出。</span><span class="sxs-lookup"><span data-stu-id="7fe19-147">The parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="7fe19-148">在每個案例中，我們會說明如何建立單一記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="7fe19-149">記錄會新增至現有記錄集，或者會以隱含方式建立記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="7fe19-150">如需明確建立記錄集和定義記錄集參數的詳細資訊，請參閱[建立 DNS 記錄集](#create-a-dns-record-set)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="7fe19-151">我們沒有提供 SOA 記錄集的建立範例，因為已與每一個 DNS 區域完成 SOA 建立與刪除，且無法個別建立或刪除 SOA。</span><span class="sxs-lookup"><span data-stu-id="7fe19-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="7fe19-152">然而，[可以對 SOA 進行修改，如稍後範例所示](#to-modify-an-SOA-record)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="7fe19-153">建立 AAAA 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="7fe19-154">建立 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="7fe19-155">DNS 標準在區域頂點不允許 CNAME 記錄 (`--Name "@"`)，也不允許包含一個記錄以上的記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-155">The DNS standards do not permit CNAME records at the apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="7fe19-156">如需詳細資訊，請參閱 [CNAME 記錄](dns-zones-records.md#cname-records)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="7fe19-157">建立 MX 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-157">Create an MX record</span></span>

<span data-ttu-id="7fe19-158">此範例會使用記錄集名稱 "@"，在區域頂點 (在此案例中，"contoso.com") 建立 MX 記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="7fe19-159">建立 NS 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="7fe19-160">建立 PTR 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-160">Create a PTR record</span></span>

<span data-ttu-id="7fe19-161">在此情況下，'my-arpa-zone.com' 代表表示您 IP 範圍的 ARPA 區域。</span><span class="sxs-lookup"><span data-stu-id="7fe19-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="7fe19-162">此區域中的每個 PTR 記錄集都與此 IP 範圍內的一個 IP 位址相對應。</span><span class="sxs-lookup"><span data-stu-id="7fe19-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="7fe19-163">記錄名稱 '10' 是此記錄所代表的這個 IP 範圍內 IP 位址的最後一個八位元。</span><span class="sxs-lookup"><span data-stu-id="7fe19-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="7fe19-164">建立 SRV 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-164">Create an SRV record</span></span>

<span data-ttu-id="7fe19-165">建立 [SRV 記錄集](dns-zones-records.md#srv-records)時，指定記錄集名稱中的 *\_服務* 和 *\_通訊協定*。</span><span class="sxs-lookup"><span data-stu-id="7fe19-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="7fe19-166">在區域頂點建立一筆 SRV 記錄集時，不需要在記錄集名稱中包含 "@"。</span><span class="sxs-lookup"><span data-stu-id="7fe19-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="7fe19-167">建立 TXT 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-167">Create a TXT record</span></span>

<span data-ttu-id="7fe19-168">下列範例示範如何建立 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="7fe19-169">如需 TXT 記錄中，所支援字串長度上限的相關資訊，請參閱 [TXT 記錄](dns-zones-records.md#txt-records)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="7fe19-170">取得記錄集</span><span class="sxs-lookup"><span data-stu-id="7fe19-170">Get a record set</span></span>

<span data-ttu-id="7fe19-171">若要擷取現有的記錄集，使用 `az network dns record-set <record-type> show`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-171">To retrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="7fe19-172">如需協助，請參閱 `az network dns record-set <record-type> show --help`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="7fe19-173">和建立記錄或記錄集時相同，提供的記錄集名稱必須是「相對」名稱，表示它不能包含區域名稱。</span><span class="sxs-lookup"><span data-stu-id="7fe19-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="7fe19-174">您也必須指定記錄類型、包含記錄集的區域，以及包含區域的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7fe19-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="7fe19-175">下列範例會從 MyResourceGroup 資源群組的 contoso.com 區域中，擷取類型為 A 的 www 記錄：</span><span class="sxs-lookup"><span data-stu-id="7fe19-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="7fe19-176">列出記錄集</span><span class="sxs-lookup"><span data-stu-id="7fe19-176">List record sets</span></span>

<span data-ttu-id="7fe19-177">您可以使用 `az network dns record-set list` 命令來列出 DNS 區域中的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-177">You can list all records in a DNS zone by using the `az network dns record-set list` command.</span></span> <span data-ttu-id="7fe19-178">如需協助，請參閱 `az network dns record-set list --help`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="7fe19-179">這個範例會傳回資源群組 MyResourceGroup 之區域 contoso.com 中的所有記錄集，不論其名稱或記錄類型為何︰</span><span class="sxs-lookup"><span data-stu-id="7fe19-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="7fe19-180">此範例會傳回符合指定記錄類型 (此案例中為 'A' 記錄) 的所有記錄集：</span><span class="sxs-lookup"><span data-stu-id="7fe19-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="7fe19-181">將記錄新增至現有的記錄集</span><span class="sxs-lookup"><span data-stu-id="7fe19-181">Add a record to an existing record set</span></span>

<span data-ttu-id="7fe19-182">您可以使用 `az network dns record-set <record-type> set-record` 在新的記錄集內建立記錄，或用它將記錄新增至現有記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-182">You can use `az network dns record-set <record-type> set-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="7fe19-183">如需詳細資訊，請參閱上面的[建立 DNS 記錄](#create-a-dns-record)和[建立其他類型的記錄](#create-records-of-other-types)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="7fe19-184">從現有的記錄集移除記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="7fe19-185">若要從現有記錄集內移除 DNS 記錄，請使用 `az network dns record-set <record-type> remove-record`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-185">To remove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="7fe19-186">如需協助，請參閱 `az network dns record-set <record-type> remove-record -h`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="7fe19-187">此命令會刪除記錄集內的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="7fe19-188">如果記錄集內的最後一個記錄遭到刪除，記錄集本身也會遭到刪除。</span><span class="sxs-lookup"><span data-stu-id="7fe19-188">If the last record in a record set is deleted, the record set itself is also deleted.</span></span> <span data-ttu-id="7fe19-189">若要改為保留空白記錄集，請使用 `--keep-empty-record-set` 選項。</span><span class="sxs-lookup"><span data-stu-id="7fe19-189">To keep the empty record set instead, use the `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="7fe19-190">您必須使用和使用 `az network dns record-set <record-type> set-record` 建立記錄時相同的參數，指定要刪除的記錄和應從哪個區域中刪除。</span><span class="sxs-lookup"><span data-stu-id="7fe19-190">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="7fe19-191">這些參數在上面的[建立 DNS 記錄](#create-a-dns-record)和[建立其他類型的記錄](#create-records-of-other-types)中有所說明。</span><span class="sxs-lookup"><span data-stu-id="7fe19-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="7fe19-192">下列範例會在 MyResourceGroup 資源群組的 contoso.com 區域中，刪除名為 www 之記錄集內值為 '1.2.3.4' 的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-192">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="7fe19-193">修改現有記錄集</span><span class="sxs-lookup"><span data-stu-id="7fe19-193">Modify an existing record set</span></span>

<span data-ttu-id="7fe19-194">每個記錄集都包含[存留時間 (TTL)](dns-zones-records.md#time-to-live)、[中繼資料](dns-zones-records.md#tags-and-metadata)和 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="7fe19-195">下列各節說明如何修改每個屬性。</span><span class="sxs-lookup"><span data-stu-id="7fe19-195">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="7fe19-196">修改 A、AAAA、MX、NS、PTR、SRV 或 TXT 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-196">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="7fe19-197">若要修改類型為 A、AAAA、MX、NS、PTR、SRV 或 TXT 的現有記錄，您應該先新增記錄，再刪除現有記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-197">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="7fe19-198">如需如何刪除和新增記錄的詳細指示，請參閱本文稍早的章節。</span><span class="sxs-lookup"><span data-stu-id="7fe19-198">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="7fe19-199">下列範例說明如何修改 'A' 記錄，從 IP 位址 1.2.3.4 到 IP 位址 5.6.7.8：</span><span class="sxs-lookup"><span data-stu-id="7fe19-199">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="7fe19-200">您無法在區域頂點 (`--Name "@"` (包含引號)) 在自動建立的 NS 記錄集中新增、移除或修改記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-200">You cannot add, remove, or modify the records in the automatically created NS record set at the zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="7fe19-201">針對此記錄集，修改記錄集 TTL 與中繼資料是唯一允許的變更。</span><span class="sxs-lookup"><span data-stu-id="7fe19-201">For this record set, the only changes permitted are to modify the record set TTL and metadata.</span></span>

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="7fe19-202">修改 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-202">To modify a CNAME record</span></span>

<span data-ttu-id="7fe19-203">不同於大多數的其他記錄類型，CNAME 記錄集只能包含單一記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="7fe19-204">因此就其他記錄類型而言，您無法透過新增新記錄與移除現有記錄，來取代目前的值。</span><span class="sxs-lookup"><span data-stu-id="7fe19-204">Therefore, you cannot replace the current value by adding a new record and removing the existing record, as for other record types.</span></span>

<span data-ttu-id="7fe19-205">相反地，若要修改 CNAME 記錄，請使用 `az network dns record-set cname set-record`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-205">Instead, to modify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="7fe19-206">如需說明，請參閱 `az network dns record-set cname set-record --help`</span><span class="sxs-lookup"><span data-stu-id="7fe19-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="7fe19-207">此範例會修改 MyResourceGroup 資源群組之 contoso.com 區域中的 CNAME 記錄集 www，使其指向 'www.fabrikam.net' 而非其現有值︰</span><span class="sxs-lookup"><span data-stu-id="7fe19-207">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="7fe19-208">修改 SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-208">To modify an SOA record</span></span>

<span data-ttu-id="7fe19-209">不同於大多數的其他記錄類型，CNAME 記錄集只能包含單一記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="7fe19-210">因此就其他記錄類型而言，您無法透過新增新記錄與移除現有記錄，來取代目前的值。</span><span class="sxs-lookup"><span data-stu-id="7fe19-210">Therefore, you cannot replace the current value by adding a new record and removing the existing record, as for other record types.</span></span>

<span data-ttu-id="7fe19-211">相反地，若要修改 SOA 記錄，請使用 `az network dns record-set soa update`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-211">Instead, to modify the SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="7fe19-212">如需協助，請參閱 `az network dns record-set soa update --help`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="7fe19-213">下列範例說明如何設定資源群組 MyResourceGroup 之區域 contoso.com 的 SOA 記錄 'email' 屬性：</span><span class="sxs-lookup"><span data-stu-id="7fe19-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="7fe19-214">在區域頂點修改 NS 記錄</span><span class="sxs-lookup"><span data-stu-id="7fe19-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="7fe19-215">系統會自動使用每個 DNS 區域在區域頂點建立 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="7fe19-216">此記錄集包含指派給區域的 Azure DNS 名稱伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="7fe19-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="7fe19-217">您可以將其他名稱伺服器新增至此 NS 記錄集，以支援使用多個 DNS 提供者的共同裝載網域。</span><span class="sxs-lookup"><span data-stu-id="7fe19-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="7fe19-218">您也可以修改此記錄集的 TTL 和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7fe19-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="7fe19-219">不過，您無法移除或修改預先填入的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="7fe19-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="7fe19-220">請注意，這只適用於區域頂點的 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="7fe19-221">區域中的其他 NS 記錄集 (如用於委派子區域) 可以修改，沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="7fe19-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="7fe19-222">下列範例顯示如何將其他的名稱伺服器新增至在區域頂點的 NS 記錄集：</span><span class="sxs-lookup"><span data-stu-id="7fe19-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="7fe19-223">修改現有記錄集的 TTL</span><span class="sxs-lookup"><span data-stu-id="7fe19-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="7fe19-224">若要修改現有記錄集的 TTL，請使用 `azure network dns record-set <record-type> update`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-224">To modify the TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="7fe19-225">如需協助，請參閱 `azure network dns record-set <record-type> update --help`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="7fe19-226">下列範例說明如何修改記錄集 TTL，在此案例中是修改為 60 秒︰</span><span class="sxs-lookup"><span data-stu-id="7fe19-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="7fe19-227">修改現有記錄集的中繼資料</span><span class="sxs-lookup"><span data-stu-id="7fe19-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="7fe19-228">[記錄集中繼資料](dns-zones-records.md#tags-and-metadata)可用來將應用程式特定資料與每一個資料集產生關聯 (以索引鍵值組的形式)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="7fe19-229">若要修改現有記錄集的中繼資料，請使用 `az network dns record-set <record-type> update`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-229">To modify the metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="7fe19-230">如需協助，請參閱 `az network dns record-set <record-type> update --help`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="7fe19-231">下列範例示範如何修改具有兩個中繼資料項目 ("dept=finance" 與 "environment=production") 的記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="7fe19-232">請注意，任何現有的中繼資料都會由給定值所「取代」。</span><span class="sxs-lookup"><span data-stu-id="7fe19-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="7fe19-233">刪除記錄集</span><span class="sxs-lookup"><span data-stu-id="7fe19-233">Delete a record set</span></span>

<span data-ttu-id="7fe19-234">您可以使用 `az network dns record-set <record-type> delete` 命令來刪除記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-234">Record sets can be deleted by using the `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="7fe19-235">如需協助，請參閱 `azure network dns record-set <record-type> delete --help`。</span><span class="sxs-lookup"><span data-stu-id="7fe19-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="7fe19-236">刪除記錄集時，也會刪除記錄集內的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="7fe19-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="7fe19-237">您無法在區域頂點 (`--name "@"`) 刪除 SOA 和 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="7fe19-237">You cannot delete the SOA and NS record sets at the zone apex (`--name "@"`).</span></span>  <span data-ttu-id="7fe19-238">這些項目在區域建立時即會自動建立，且當區域刪除時則會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="7fe19-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="7fe19-239">下列範例會從 MyResourceGroup 資源群組的 contoso.com 區域中，刪除類型為 A 的 www 記錄集：</span><span class="sxs-lookup"><span data-stu-id="7fe19-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="7fe19-240">系統會提示您確認刪除作業。</span><span class="sxs-lookup"><span data-stu-id="7fe19-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="7fe19-241">若要抑制此提示，請使用 `--yes` 參數。</span><span class="sxs-lookup"><span data-stu-id="7fe19-241">To suppress this prompt, use the `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fe19-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7fe19-242">Next steps</span></span>

<span data-ttu-id="7fe19-243">深入了解[ Azure DNS 中的區域和記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="7fe19-244">了解使用 Azure DNS 時，如何[保護區域和記錄](dns-protect-zones-recordsets.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe19-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
