---
title: "aaaManage DNS 記錄，使用 Azure DNS hello Azure CLI 1.0 |Microsoft 文件"
description: "將網域裝載於 Azure DNS 時，在 Azure DNS 管理 DNS 記錄集和記錄。 對記錄集和記錄執行作業的所有 CLI 1.0 命令。"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="82757-104">管理 Azure DNS 使用 hello Azure CLI 1.0 中的 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-104">Manage DNS records in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="82757-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="82757-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="82757-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="82757-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="82757-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="82757-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="82757-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82757-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="82757-109">本文章將示範如何使用您的 DNS 區域的 toomanage DNS 記錄 hello 跨平台 Azure 的命令列介面 (CLI) (也就是適用於 Windows、 Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="82757-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="82757-110">您也可以管理您使用的 DNS 記錄[Azure PowerShell](dns-operations-recordsets.md)或 hello [Azure 入口網站](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="82757-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="82757-111">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="82757-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="82757-112">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="82757-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="82757-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -我們 CLI hello 傳統和資源管理部署模型。</span><span class="sxs-lookup"><span data-stu-id="82757-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="82757-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -hello 資源管理部署模型我們下一個層代 CLI。</span><span class="sxs-lookup"><span data-stu-id="82757-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="82757-115">本文章中的 hello 範例假設您已經有[安裝 hello Azure CLI 1.0，登入，並建立 DNS 區域](dns-operations-dnszones-cli-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="82757-115">hello examples in this article assume you have already [installed hello Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="82757-116">簡介</span><span class="sxs-lookup"><span data-stu-id="82757-116">Introduction</span></span>

<span data-ttu-id="82757-117">Azure DNS 中建立 DNS 記錄之前, 您必須先 toounderstand Azure DNS 到 DNS 資料錄集所組織的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="82757-118">如需在 Azure DNS 的 DNS 記錄的詳細資訊，請參閱 [DNS 區域與記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="82757-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="82757-119">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-119">Create a DNS record</span></span>

<span data-ttu-id="82757-120">toocreate DNS 記錄，使用 hello`azure network dns record-set add-record`命令。</span><span class="sxs-lookup"><span data-stu-id="82757-120">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="82757-121">如需協助，請參閱 `azure network dns record-set add-record -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="82757-122">當建立記錄，您需要 toospecify hello 資源群組名稱、 區域名稱，記錄集名稱、 hello 記錄類型和正在建立 hello 記錄 hello 詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="82757-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="82757-123">hello 指定的記錄集名稱必須是*相對*名稱，這表示它必須排除 hello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="82757-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="82757-124">如果 hello 記錄集不存在，此命令建立它。</span><span class="sxs-lookup"><span data-stu-id="82757-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="82757-125">如果 hello 記錄集已經存在，則此命令稱之為 hello 指定 toohello 現有資料錄集的記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-125">If hello record set already exists, this command adda hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="82757-126">如果建立新的記錄集，則會使用預設存留時間 (TTL) 3600。</span><span class="sxs-lookup"><span data-stu-id="82757-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="82757-127">如需有關如何 toouse 不同 TTLs，請參閱指示[建立 DNS 記錄集](#create-a-dns-record-set)。</span><span class="sxs-lookup"><span data-stu-id="82757-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="82757-128">hello 下列範例會建立稱為 「 A 記錄*www* hello 區域*contoso.com* hello 資源群組中*MyResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="82757-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="82757-129">hello IP 位址記錄是的 hello *1.2.3.4*。</span><span class="sxs-lookup"><span data-stu-id="82757-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="82757-130">toocreate hello 區域的 hello 區域的 apex 中的記錄 (在此情況下，"contoso.com")，使用 hello 記錄名稱"@"，其中包括 hello 引號：</span><span class="sxs-lookup"><span data-stu-id="82757-130">toocreate a record in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="82757-131">建立 DNS 記錄集</span><span class="sxs-lookup"><span data-stu-id="82757-131">Create a DNS record set</span></span>

<span data-ttu-id="82757-132">Hello DNS 記錄的現有資料錄集，請加入的 tooan 在上述範例 hello，或是建立 hello 記錄集*隱含*。</span><span class="sxs-lookup"><span data-stu-id="82757-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="82757-133">您也可以建立 hello 記錄集*明確*加入記錄 tooit 之前。</span><span class="sxs-lookup"><span data-stu-id="82757-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="82757-134">Azure DNS 支援 'empty' 的資料錄集，可做為預留位置 tooreserve DNS 名稱建立 DNS 記錄之前。</span><span class="sxs-lookup"><span data-stu-id="82757-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="82757-135">空的資料錄集會顯示在 hello Azure DNS 控制平面，但不是會出現在 hello Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="82757-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="82757-136">資料錄集建立使用 hello`azure network dns record-set create`命令。</span><span class="sxs-lookup"><span data-stu-id="82757-136">Record sets are created using hello `azure network dns record-set create` command.</span></span> <span data-ttu-id="82757-137">如需協助，請參閱 `azure network dns record-set create -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="82757-138">建立明確設定的 hello 記錄可讓您 toospecify 記錄集屬性，例如 hello[存留時間 (TTL)](dns-zones-records.md#time-to-live)和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="82757-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="82757-139">[設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="82757-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="82757-140">hello 下列範例會建立空的記錄設定以 60 秒的 TTL，使用 hello`--ttl`參數 (簡短形式`-l`):</span><span class="sxs-lookup"><span data-stu-id="82757-140">hello following example creates an empty record set with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="82757-141">hello 下列範例會建立之記錄集的兩個中繼資料的項目，"dept = finance"和"環境 = 實際執行 」，利用 hello`--metadata`參數 (簡短形式`-m`):</span><span class="sxs-lookup"><span data-stu-id="82757-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="82757-142">建立好空白記錄集之後，可依[建立 DNS 記錄](#create-a-dns-record)所述使用 `azure network dns record-set add-record` 新增記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="82757-143">建立其他類型的記錄</span><span class="sxs-lookup"><span data-stu-id="82757-143">Create records of other types</span></span>

<span data-ttu-id="82757-144">有看到詳細 toocreate 'A' 記錄的方式，下列範例會顯示 toocreate 記錄的其他記錄類型如何支援 Azure dns hello。</span><span class="sxs-lookup"><span data-stu-id="82757-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="82757-145">hello 參數使用 toospecify hello 記錄資料的 hello 記錄 hello 類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="82757-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="82757-146">例如，型別"A"的記錄，您指定 hello IPv4 位址搭配 hello 參數`-a <IPv4 address>`。</span><span class="sxs-lookup"><span data-stu-id="82757-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="82757-147">hello 參數，可以使用列出每個記錄類型為`azure network dns record-set add-record -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-147">hello parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="82757-148">在各案例中，我們會示範如何 toocreate 單一記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="82757-149">hello 記錄加入的 toohello 現有資料錄集，或隱含建立的記錄組。</span><span class="sxs-lookup"><span data-stu-id="82757-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="82757-150">如需明確建立記錄集和定義記錄集參數的詳細資訊，請參閱[建立 DNS 記錄集](#create-a-dns-record-set)。</span><span class="sxs-lookup"><span data-stu-id="82757-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="82757-151">我們不會提供範例 toocreate SOA 記錄集，因為 SOAs 會建立和刪除與每個 DNS 區域和無法建立或刪除個別。</span><span class="sxs-lookup"><span data-stu-id="82757-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="82757-152">不過， [SOA 可以修改，在稍後的範例所示的 hello](#to-modify-an-SOA-record)。</span><span class="sxs-lookup"><span data-stu-id="82757-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="82757-153">建立 AAAA 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="82757-154">建立 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="82757-155">hello DNS 標準不允許在 hello 區域的區域的 apex CNAME 記錄 (`-Name "@"`)，也請勿允許包含多個記錄的資料錄集。</span><span class="sxs-lookup"><span data-stu-id="82757-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="82757-156">如需詳細資訊，請參閱 [CNAME 記錄](dns-zones-records.md#cname-records)。</span><span class="sxs-lookup"><span data-stu-id="82757-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="82757-157">建立 MX 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-157">Create an MX record</span></span>

<span data-ttu-id="82757-158">在此範例中，我們使用 hello 記錄集名稱"@"toocreate hello 在 hello 區域的 apex MX 記錄 (在此情況下，"contoso.com")。</span><span class="sxs-lookup"><span data-stu-id="82757-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="82757-159">建立 NS 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="82757-160">建立 PTR 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-160">Create a PTR record</span></span>

<span data-ttu-id="82757-161">在此情況下，' 我-arpa-zone.com' 代表 hello ARPA 區域代表您的 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="82757-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="82757-162">在此區域中設定每個 PTR 記錄對應 tooan 此 IP 範圍內的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="82757-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="82757-163">hello 記錄名稱 '10' 是 hello hello IP 位址，由這個記錄此 IP 範圍內的最後一個八位元。</span><span class="sxs-lookup"><span data-stu-id="82757-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="82757-164">建立 SRV 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-164">Create an SRV record</span></span>

<span data-ttu-id="82757-165">建立時[SRV 記錄集](dns-zones-records.md#srv-records)，指定 hello *\_服務*和*\_通訊協定*hello 中記錄集名稱。</span><span class="sxs-lookup"><span data-stu-id="82757-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="82757-166">沒有任何需要 tooinclude"@"hello 記錄集中名稱建立一筆 SRV 記錄於 hello 區域的 apex 設定。</span><span class="sxs-lookup"><span data-stu-id="82757-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="82757-167">建立 TXT 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-167">Create a TXT record</span></span>

<span data-ttu-id="82757-168">hello 下列範例顯示如何 toocreate TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="82757-169">如需支援 TXT 記錄中的 hello 最大字串長度的詳細資訊，請參閱[TXT 記錄](dns-zones-records.md#txt-records)。</span><span class="sxs-lookup"><span data-stu-id="82757-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="82757-170">取得記錄集</span><span class="sxs-lookup"><span data-stu-id="82757-170">Get a record set</span></span>

<span data-ttu-id="82757-171">使用現有的資料錄集，tooretrieve `azure network dns record-set show`。</span><span class="sxs-lookup"><span data-stu-id="82757-171">tooretrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="82757-172">如需協助，請參閱 `azure network dns record-set show -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="82757-173">Hello 記錄建立的記錄或資料錄集時，設定指定的名稱必須是*相對*名稱，這表示它必須排除 hello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="82757-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="82757-174">您也需要 toospecify hello 記錄類型，包含 hello 記錄 hello 區域設定，並 hello 含有 hello 區域的資源群組。</span><span class="sxs-lookup"><span data-stu-id="82757-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="82757-175">hello 下列範例會擷取 hello 記錄*www*從區域類型的*contoso.com*資源群組中*MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="82757-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="82757-176">列出記錄集</span><span class="sxs-lookup"><span data-stu-id="82757-176">List record sets</span></span>

<span data-ttu-id="82757-177">您可以使用 hello 列出 DNS 區域中的所有記錄`azure network dns record-set list`命令。</span><span class="sxs-lookup"><span data-stu-id="82757-177">You can list all records in a DNS zone by using hello `azure network dns record-set list` command.</span></span> <span data-ttu-id="82757-178">如需協助，請參閱 `azure network dns record-set list -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="82757-179">這個範例會傳回所有資料錄集，在 hello 區域*contoso.com*，資源群組中*MyResourceGroup*，不論名稱或記錄類型：</span><span class="sxs-lookup"><span data-stu-id="82757-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="82757-180">這個範例會傳回所有符合 hello 指定記錄類型 （在此情況下，'A' 記錄） 的資料錄集：</span><span class="sxs-lookup"><span data-stu-id="82757-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="82757-181">新增記錄 tooan，現有的資料錄集</span><span class="sxs-lookup"><span data-stu-id="82757-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="82757-182">您可以使用`azure network dns record-set add-record`同時 toocreate 新記錄中的記錄設定，或 tooadd 記錄 tooan 現有的記錄設定。</span><span class="sxs-lookup"><span data-stu-id="82757-182">You can use `azure network dns record-set add-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="82757-183">如需詳細資訊，請參閱上面的[建立 DNS 記錄](#create-a-dns-record)和[建立其他類型的記錄](#create-records-of-other-types)。</span><span class="sxs-lookup"><span data-stu-id="82757-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="82757-184">從現有的記錄集移除記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="82757-185">tooremove DNS 記錄，從現有的資料錄集，使用`azure network dns record-set delete-record`。</span><span class="sxs-lookup"><span data-stu-id="82757-185">tooremove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="82757-186">如需協助，請參閱 `azure network dns record-set delete-record -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="82757-187">此命令會刪除記錄集內的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="82757-188">如果刪除資料錄集 hello 最後一筆記錄時，會將本身設 hello 記錄是**不**刪除。</span><span class="sxs-lookup"><span data-stu-id="82757-188">If hello last record in a record set is deleted, hello record set itself is **not** deleted.</span></span> <span data-ttu-id="82757-189">反而會留下空白記錄集。</span><span class="sxs-lookup"><span data-stu-id="82757-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="82757-190">toodelete hello 記錄集相反地，請參閱[刪除記錄集](#delete-a-record-set)。</span><span class="sxs-lookup"><span data-stu-id="82757-190">toodelete hello record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="82757-191">您需要 toospecify hello 記錄 toobe 刪除和 hello 區域應予以刪除，從使用 hello 相同參數做為建立記錄使用時`azure network dns record-set add-record`。</span><span class="sxs-lookup"><span data-stu-id="82757-191">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="82757-192">這些參數在上面的[建立 DNS 記錄](#create-a-dns-record)和[建立其他類型的記錄](#create-records-of-other-types)中有所說明。</span><span class="sxs-lookup"><span data-stu-id="82757-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="82757-193">此命令會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="82757-193">This command prompts for confirmation.</span></span> <span data-ttu-id="82757-194">此提示可使用，以歸併 hello`--quiet`切換 (簡短形式`-q`)。</span><span class="sxs-lookup"><span data-stu-id="82757-194">This prompt can be suppressed using hello `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="82757-195">下列範例刪除 hello hello 的記錄中包含值 '1.2.3.4' hello 記錄從名為*www* hello 區域*contoso.com*，hello 資源群組中*MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="82757-195">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="82757-196">隱藏 hello 確認提示。</span><span class="sxs-lookup"><span data-stu-id="82757-196">hello confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="82757-197">修改現有記錄集</span><span class="sxs-lookup"><span data-stu-id="82757-197">Modify an existing record set</span></span>

<span data-ttu-id="82757-198">每個記錄集都包含[存留時間 (TTL)](dns-zones-records.md#time-to-live)、[中繼資料](dns-zones-records.md#tags-and-metadata)和 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="82757-199">hello 下列各節說明如何 toomodify 每個這些屬性。</span><span class="sxs-lookup"><span data-stu-id="82757-199">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="82757-200">toomodify A、 AAAA、 MX、 NS、 PTR、 SRV、 或 TXT 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-200">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="82757-201">toomodify 現有類型 A、 AAAA、 MX、 NS、 PTR、 SRV、 或 TXT 記錄，您應該先新增新的記錄，然後刪除 hello 現有記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-201">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="82757-202">如需有關的詳細指示 toodelete 和新增記錄，請參閱 hello 的本文稍早章節。</span><span class="sxs-lookup"><span data-stu-id="82757-202">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="82757-203">下列範例中的 hello 顯示 toomodify 'A' 記錄，從 IP 位址 1.2.3.4 tooIP 定址 5.6.7.8 的方式：</span><span class="sxs-lookup"><span data-stu-id="82757-203">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="82757-204">toomodify CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-204">toomodify a CNAME record</span></span>

<span data-ttu-id="82757-205">toomodify CNAME 記錄，使用`azure network dns record-set add-record`tooadd hello 新記錄的值。</span><span class="sxs-lookup"><span data-stu-id="82757-205">toomodify a CNAME record, use `azure network dns record-set add-record` tooadd hello new record value.</span></span> <span data-ttu-id="82757-206">不同於其他記錄類型，CNAME 記錄集只能包含單一記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="82757-207">因此，hello 現有的記錄是*取代*當 hello 新記錄會加入，但不需要另外刪除 toobe。</span><span class="sxs-lookup"><span data-stu-id="82757-207">Therefore, hello existing record is *replaced* when hello new record is added, and does not need toobe deleted separately.</span></span>  <span data-ttu-id="82757-208">您將會提示的 tooaccept 這項取代。</span><span class="sxs-lookup"><span data-stu-id="82757-208">You will be prompted tooaccept this replacement.</span></span>

<span data-ttu-id="82757-209">hello 範例會修改 hello CNAME 記錄集*www* hello 區域*contoso.com*，資源群組中*MyResourceGroup*，toopoint 太 'www.fabrikam.net' 而不是其現有的值：</span><span class="sxs-lookup"><span data-stu-id="82757-209">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="82757-210">toomodify SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-210">toomodify an SOA record</span></span>

<span data-ttu-id="82757-211">使用`azure network dns record-set set-soa-record`toomodify hello SOA 給定的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="82757-211">Use `azure network dns record-set set-soa-record` toomodify hello SOA for a given DNS zone.</span></span> <span data-ttu-id="82757-212">如需協助，請參閱 `azure network dns record-set set-soa-record -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="82757-213">hello 下列範例示範如何 tooset hello 'email' 屬性的 hello SOA 記錄 hello 區域*contoso.com* hello 資源群組中*MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="82757-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="82757-214">在 hello 區域的 apex toomodify NS 記錄</span><span class="sxs-lookup"><span data-stu-id="82757-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="82757-215">在 hello 區域的 apex 設定 hello NS 記錄會自動建立與每個 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="82757-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="82757-216">它包含 hello hello Azure DNS 名稱伺服器指派的 toohello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="82757-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="82757-217">您可以加入其他的名稱伺服器 toothis NS 記錄集，toosupport 共同裝載網域使用一個以上的 DNS 提供者。</span><span class="sxs-lookup"><span data-stu-id="82757-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="82757-218">您也可以修改 hello TTL 和此記錄集的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="82757-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="82757-219">不過，您無法移除或修改 hello 預先填入的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="82757-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="82757-220">請注意這適用於僅 toohello NS 記錄集在 hello 區域的 apex。</span><span class="sxs-lookup"><span data-stu-id="82757-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="82757-221">如果沒有限制，您可以修改其他 NS 記錄集在您的區域 （做為使用的 toodelegate 子區域）。</span><span class="sxs-lookup"><span data-stu-id="82757-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="82757-222">hello 下列範例顯示如何 tooadd 其他的名稱伺服器 toohello NS 記錄設定在 hello 區域的 apex:</span><span class="sxs-lookup"><span data-stu-id="82757-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="82757-223">toomodify hello TTL 為現有的記錄設定</span><span class="sxs-lookup"><span data-stu-id="82757-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="82757-224">toomodify hello TTL 現有記錄的設定，請使用`azure network dns record-set set`。</span><span class="sxs-lookup"><span data-stu-id="82757-224">toomodify hello TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="82757-225">如需協助，請參閱 `azure network dns record-set set -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="82757-226">hello 下列範例顯示如何 toomodify 記錄集 TTL，在此情況下 too60 秒：</span><span class="sxs-lookup"><span data-stu-id="82757-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="82757-227">toomodify hello 中繼資料的現有資料錄集</span><span class="sxs-lookup"><span data-stu-id="82757-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="82757-228">[設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="82757-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="82757-229">toomodify hello 中繼資料的現有記錄的設定，請使用`azure network dns record-set set`。</span><span class="sxs-lookup"><span data-stu-id="82757-229">toomodify hello metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="82757-230">如需協助，請參閱 `azure network dns record-set set -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="82757-231">hello 下列範例示範如何 toomodify 記錄設定兩個中繼資料的項目，"dept = finance"和"環境 = 實際執行 」，利用 hello`--metadata`參數 (簡短形式`-m`)。</span><span class="sxs-lookup"><span data-stu-id="82757-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="82757-232">請注意，任何現有的中繼資料是*取代*所指定的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="82757-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="82757-233">刪除記錄集</span><span class="sxs-lookup"><span data-stu-id="82757-233">Delete a record set</span></span>

<span data-ttu-id="82757-234">使用 hello 也可以刪除資料錄集`azure network dns record-set delete`命令。</span><span class="sxs-lookup"><span data-stu-id="82757-234">Record sets can be deleted by using hello `azure network dns record-set delete` command.</span></span> <span data-ttu-id="82757-235">如需協助，請參閱 `azure network dns record-set delete -h`。</span><span class="sxs-lookup"><span data-stu-id="82757-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="82757-236">刪除資料錄集時，也會刪除 hello 資料錄集內的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="82757-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="82757-237">您無法刪除 hello SOA 和 NS 記錄集在 hello 區域的 apex (`-Name "@"`)。</span><span class="sxs-lookup"><span data-stu-id="82757-237">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="82757-238">當 hello 區域建立，而且已刪除 hello 區域時自動刪除，這些會自動建立。</span><span class="sxs-lookup"><span data-stu-id="82757-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="82757-239">hello 下列範例會刪除名為 hello 記錄*www*從 hello 區域類型的*contoso.com*資源群組中*MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="82757-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="82757-240">您已提示的 tooconfirm hello 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="82757-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="82757-241">此提示，toosuppress 使用 hello`--quiet`切換 (簡短形式`-q`)。</span><span class="sxs-lookup"><span data-stu-id="82757-241">toosuppress this prompt, use hello `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82757-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82757-242">Next steps</span></span>

<span data-ttu-id="82757-243">深入了解[ Azure DNS 中的區域和記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="82757-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="82757-244">了解如何太[保護您的區域和記錄](dns-protect-zones-recordsets.md)時使用 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="82757-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
