---
title: "aaaManage DNS 記錄，使用 Azure DNS hello Azure CLI 2.0 |Microsoft 文件"
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
ms.openlocfilehash: 9d6f8e74ebad55ccd2381fd84a830d2c7bbb1f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="6c3f2-104">管理 DNS 記錄和使用 Azure CLI 2.0 hello Azure DNS 中的資料錄集</span><span class="sxs-lookup"><span data-stu-id="6c3f2-104">Manage DNS records and recordsets in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c3f2-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6c3f2-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="6c3f2-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6c3f2-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="6c3f2-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6c3f2-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="6c3f2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c3f2-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="6c3f2-109">本文章將示範如何使用您的 DNS 區域的 toomanage DNS 記錄 hello 跨平台的 Azure 命令列介面 (CLI) 2.0 中，這是適用於 Windows、 Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="6c3f2-110">您也可以管理您使用的 DNS 記錄[Azure PowerShell](dns-operations-recordsets.md)或 hello [Azure 入口網站](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6c3f2-111">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="6c3f2-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="6c3f2-112">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="6c3f2-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="6c3f2-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -我們 CLI hello 傳統和資源管理部署模型。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="6c3f2-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -hello 資源管理部署模型我們下一個層代 CLI。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="6c3f2-115">本文章中的 hello 範例假設您已經有[安裝 hello Azure CLI 2.0 中，登入，並建立 DNS 區域](dns-operations-dnszones-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-115">hello examples in this article assume you have already [installed hello Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="6c3f2-116">簡介</span><span class="sxs-lookup"><span data-stu-id="6c3f2-116">Introduction</span></span>

<span data-ttu-id="6c3f2-117">Azure DNS 中建立 DNS 記錄之前, 您必須先 toounderstand Azure DNS 到 DNS 資料錄集所組織的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="6c3f2-118">如需在 Azure DNS 的 DNS 記錄的詳細資訊，請參閱 [DNS 區域與記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="6c3f2-119">建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-119">Create a DNS record</span></span>

<span data-ttu-id="6c3f2-120">toocreate DNS 記錄，使用 hello`az network dns record-set <record-type> set-record`命令 (其中`<record-type>`是 hello 記錄類型，也就是</span><span class="sxs-lookup"><span data-stu-id="6c3f2-120">toocreate a DNS record, use hello `az network dns record-set <record-type> set-record` command (where `<record-type>` is hello type of record, i.e</span></span> <span data-ttu-id="6c3f2-121">a、srv、txt 等等。)如需協助，請參閱 `az network dns record-set --help`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="6c3f2-122">當建立記錄，您需要 toospecify hello 資源群組名稱、 區域名稱，記錄集名稱、 hello 記錄類型和正在建立 hello 記錄 hello 詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="6c3f2-123">hello 指定的記錄集名稱必須是*相對*名稱，這表示它必須排除 hello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="6c3f2-124">如果 hello 記錄集不存在，此命令建立它。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="6c3f2-125">如果 hello 記錄集已經存在，則此命令會新增 hello 記錄您指定 toohello 現有資料錄集。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-125">If hello record set already exists, this command adds hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="6c3f2-126">如果建立新的記錄集，則會使用預設存留時間 (TTL) 3600。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="6c3f2-127">如需有關如何 toouse 不同 TTLs，請參閱指示[建立 DNS 記錄集](#create-a-dns-record-set)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="6c3f2-128">hello 下列範例會建立稱為 「 A 記錄*www* hello 區域*contoso.com* hello 資源群組中*MyResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="6c3f2-129">hello IP 位址記錄是的 hello *1.2.3.4*。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="6c3f2-130">在 hello 區域的 hello 區域的 apex 設定 toocreate 記錄 (在此情況下，"contoso.com")，使用 hello 記錄名稱"@"，包括 hello 引號：</span><span class="sxs-lookup"><span data-stu-id="6c3f2-130">toocreate a record set in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="6c3f2-131">建立 DNS 記錄集</span><span class="sxs-lookup"><span data-stu-id="6c3f2-131">Create a DNS record set</span></span>

<span data-ttu-id="6c3f2-132">Hello DNS 記錄的現有資料錄集，請加入的 tooan 在上述範例 hello，或是建立 hello 記錄集*隱含*。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="6c3f2-133">您也可以建立 hello 記錄集*明確*加入記錄 tooit 之前。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="6c3f2-134">Azure DNS 支援 'empty' 的資料錄集，可做為預留位置 tooreserve DNS 名稱建立 DNS 記錄之前。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="6c3f2-135">空的資料錄集會顯示在 hello Azure DNS 控制平面，但不是會出現在 hello Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="6c3f2-136">資料錄集建立使用 hello`az network dns record-set <record-type> create`命令。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-136">Record sets are created using hello `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="6c3f2-137">如需協助，請參閱 `az network dns record-set <record-type> create --help`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="6c3f2-138">建立明確設定的 hello 記錄可讓您 toospecify 記錄集屬性，例如 hello[存留時間 (TTL)](dns-zones-records.md#time-to-live)和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="6c3f2-139">[設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="6c3f2-140">hello 下列範例會建立空的資料錄集的類型為 'A' 以 60 秒的 TTL，使用 hello`--ttl`參數 (簡短形式`-l`):</span><span class="sxs-lookup"><span data-stu-id="6c3f2-140">hello following example creates an empty record set of type 'A' with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="6c3f2-141">hello 下列範例會建立之記錄集的兩個中繼資料的項目，"dept = finance"和"環境 = 實際執行 」，利用 hello`--metadata`參數：</span><span class="sxs-lookup"><span data-stu-id="6c3f2-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="6c3f2-142">建立好空白記錄集之後，可依[建立 DNS 記錄](#create-a-dns-record)所述使用 `azure network dns record-set <record-type> set-record` 新增記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="6c3f2-143">建立其他類型的記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-143">Create records of other types</span></span>

<span data-ttu-id="6c3f2-144">有看到詳細 toocreate 'A' 記錄的方式，下列範例會顯示 toocreate 記錄的其他記錄類型如何支援 Azure dns hello。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="6c3f2-145">hello 參數使用 toospecify hello 記錄資料的 hello 記錄 hello 類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="6c3f2-146">例如，型別"A"的記錄，您指定 hello IPv4 位址搭配 hello 參數`--ipv4-address <IPv4 address>`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="6c3f2-147">hello 參數，可以使用列出每個記錄類型為`az network dns record-set <record-type> set-record --help`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-147">hello parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="6c3f2-148">在各案例中，我們會示範如何 toocreate 單一記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="6c3f2-149">hello 記錄加入的 toohello 現有資料錄集，或隱含建立的記錄組。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="6c3f2-150">如需明確建立記錄集和定義記錄集參數的詳細資訊，請參閱[建立 DNS 記錄集](#create-a-dns-record-set)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="6c3f2-151">我們不會提供範例 toocreate SOA 記錄集，因為 SOAs 會建立和刪除與每個 DNS 區域和無法建立或刪除個別。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="6c3f2-152">不過， [SOA 可以修改，在稍後的範例所示的 hello](#to-modify-an-SOA-record)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="6c3f2-153">建立 AAAA 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="6c3f2-154">建立 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="6c3f2-155">hello DNS 標準不允許在 hello 區域的區域的 apex CNAME 記錄 (`--Name "@"`)，也請勿允許包含多個記錄的資料錄集。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="6c3f2-156">如需詳細資訊，請參閱 [CNAME 記錄](dns-zones-records.md#cname-records)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="6c3f2-157">建立 MX 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-157">Create an MX record</span></span>

<span data-ttu-id="6c3f2-158">在此範例中，我們使用 hello 記錄集名稱"@"toocreate hello 在 hello 區域的 apex MX 記錄 (在此情況下，"contoso.com")。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="6c3f2-159">建立 NS 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="6c3f2-160">建立 PTR 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-160">Create a PTR record</span></span>

<span data-ttu-id="6c3f2-161">在此情況下，' 我-arpa-zone.com' 代表 hello ARPA 區域代表您的 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="6c3f2-162">在此區域中設定每個 PTR 記錄對應 tooan 此 IP 範圍內的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="6c3f2-163">hello 記錄名稱 '10' 是 hello hello IP 位址，由這個記錄此 IP 範圍內的最後一個八位元。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="6c3f2-164">建立 SRV 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-164">Create an SRV record</span></span>

<span data-ttu-id="6c3f2-165">建立時[SRV 記錄集](dns-zones-records.md#srv-records)，指定 hello *\_服務*和*\_通訊協定*hello 中記錄集名稱。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="6c3f2-166">沒有任何需要 tooinclude"@"hello 記錄集中名稱建立一筆 SRV 記錄於 hello 區域的 apex 設定。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="6c3f2-167">建立 TXT 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-167">Create a TXT record</span></span>

<span data-ttu-id="6c3f2-168">hello 下列範例顯示如何 toocreate TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="6c3f2-169">如需支援 TXT 記錄中的 hello 最大字串長度的詳細資訊，請參閱[TXT 記錄](dns-zones-records.md#txt-records)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="6c3f2-170">取得記錄集</span><span class="sxs-lookup"><span data-stu-id="6c3f2-170">Get a record set</span></span>

<span data-ttu-id="6c3f2-171">使用現有的資料錄集，tooretrieve `az network dns record-set <record-type> show`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-171">tooretrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="6c3f2-172">如需協助，請參閱 `az network dns record-set <record-type> show --help`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="6c3f2-173">Hello 記錄建立的記錄或資料錄集時，設定指定的名稱必須是*相對*名稱，這表示它必須排除 hello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="6c3f2-174">您也需要 toospecify hello 記錄類型，包含 hello 記錄 hello 區域設定，並 hello 含有 hello 區域的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="6c3f2-175">hello 下列範例會擷取 hello 記錄*www*從區域類型的*contoso.com*資源群組中*MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6c3f2-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="6c3f2-176">列出記錄集</span><span class="sxs-lookup"><span data-stu-id="6c3f2-176">List record sets</span></span>

<span data-ttu-id="6c3f2-177">您可以使用 hello 列出 DNS 區域中的所有記錄`az network dns record-set list`命令。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-177">You can list all records in a DNS zone by using hello `az network dns record-set list` command.</span></span> <span data-ttu-id="6c3f2-178">如需協助，請參閱 `az network dns record-set list --help`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="6c3f2-179">這個範例會傳回所有資料錄集，在 hello 區域*contoso.com*，資源群組中*MyResourceGroup*，不論名稱或記錄類型：</span><span class="sxs-lookup"><span data-stu-id="6c3f2-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="6c3f2-180">這個範例會傳回所有符合 hello 指定記錄類型 （在此情況下，'A' 記錄） 的資料錄集：</span><span class="sxs-lookup"><span data-stu-id="6c3f2-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="6c3f2-181">新增記錄 tooan，現有的資料錄集</span><span class="sxs-lookup"><span data-stu-id="6c3f2-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="6c3f2-182">您可以使用`az network dns record-set <record-type> set-record`同時 toocreate 新記錄中的記錄設定，或 tooadd 記錄 tooan 現有的記錄設定。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-182">You can use `az network dns record-set <record-type> set-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="6c3f2-183">如需詳細資訊，請參閱上面的[建立 DNS 記錄](#create-a-dns-record)和[建立其他類型的記錄](#create-records-of-other-types)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="6c3f2-184">從現有的記錄集移除記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="6c3f2-185">tooremove DNS 記錄，從現有的資料錄集，使用`az network dns record-set <record-type> remove-record`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-185">tooremove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="6c3f2-186">如需協助，請參閱 `az network dns record-set <record-type> remove-record -h`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="6c3f2-187">此命令會刪除記錄集內的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="6c3f2-188">如果刪除 hello 記錄組中的最後一筆記錄，就會將本身設 hello 記錄也會刪除。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-188">If hello last record in a record set is deleted, hello record set itself is also deleted.</span></span> <span data-ttu-id="6c3f2-189">相反地，使用 tookeep hello 空的資料錄集的 hello`--keep-empty-record-set`選項。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-189">tookeep hello empty record set instead, use hello `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="6c3f2-190">您需要 toospecify hello 記錄 toobe 刪除和 hello 區域應予以刪除，從使用 hello 相同參數做為建立記錄使用時`az network dns record-set <record-type> set-record`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-190">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="6c3f2-191">這些參數在上面的[建立 DNS 記錄](#create-a-dns-record)和[建立其他類型的記錄](#create-records-of-other-types)中有所說明。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="6c3f2-192">下列範例刪除 hello hello 的記錄中包含值 '1.2.3.4' hello 記錄從名為*www* hello 區域*contoso.com*，hello 資源群組中*MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="6c3f2-192">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="6c3f2-193">修改現有記錄集</span><span class="sxs-lookup"><span data-stu-id="6c3f2-193">Modify an existing record set</span></span>

<span data-ttu-id="6c3f2-194">每個記錄集都包含[存留時間 (TTL)](dns-zones-records.md#time-to-live)、[中繼資料](dns-zones-records.md#tags-and-metadata)和 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="6c3f2-195">hello 下列各節說明如何 toomodify 每個這些屬性。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-195">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="6c3f2-196">toomodify A、 AAAA、 MX、 NS、 PTR、 SRV、 或 TXT 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-196">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="6c3f2-197">toomodify 現有類型 A、 AAAA、 MX、 NS、 PTR、 SRV、 或 TXT 記錄，您應該先新增新的記錄，然後刪除 hello 現有記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-197">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="6c3f2-198">如需有關的詳細指示 toodelete 和新增記錄，請參閱 hello 的本文稍早章節。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-198">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="6c3f2-199">下列範例中的 hello 顯示 toomodify 'A' 記錄，從 IP 位址 1.2.3.4 tooIP 定址 5.6.7.8 的方式：</span><span class="sxs-lookup"><span data-stu-id="6c3f2-199">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="6c3f2-200">您無法加入、 移除或修改 hello 自動建立在 hello 區域的 apex 設定的 NS 記錄中的 hello 記錄 (`--Name "@"`，包括引號)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-200">You cannot add, remove, or modify hello records in hello automatically created NS record set at hello zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="6c3f2-201">此資料錄集時，允許 hello 只變更為 toomodify hello 記錄集 TTL 和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-201">For this record set, hello only changes permitted are toomodify hello record set TTL and metadata.</span></span>

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="6c3f2-202">toomodify CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-202">toomodify a CNAME record</span></span>

<span data-ttu-id="6c3f2-203">不同於大多數的其他記錄類型，CNAME 記錄集只能包含單一記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="6c3f2-204">因此，您無法加入新的記錄並移除 hello 現有記錄中的，與其他記錄類型來取代 hello 目前值。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-204">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="6c3f2-205">相反地，使用 toomodify CNAME 記錄， `az network dns record-set cname set-record`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-205">Instead, toomodify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="6c3f2-206">如需說明，請參閱 `az network dns record-set cname set-record --help`</span><span class="sxs-lookup"><span data-stu-id="6c3f2-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="6c3f2-207">hello 範例會修改 hello CNAME 記錄集*www* hello 區域*contoso.com*，資源群組中*MyResourceGroup*，toopoint 太 'www.fabrikam.net' 而不是其現有的值：</span><span class="sxs-lookup"><span data-stu-id="6c3f2-207">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="6c3f2-208">toomodify SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-208">toomodify an SOA record</span></span>

<span data-ttu-id="6c3f2-209">不同於大多數的其他記錄類型，CNAME 記錄集只能包含單一記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="6c3f2-210">因此，您無法加入新的記錄並移除 hello 現有記錄中的，與其他記錄類型來取代 hello 目前值。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-210">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="6c3f2-211">相反地，使用 toomodify hello SOA 記錄`az network dns record-set soa update`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-211">Instead, toomodify hello SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="6c3f2-212">如需協助，請參閱 `az network dns record-set soa update --help`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="6c3f2-213">hello 下列範例示範如何 tooset hello 'email' 屬性的 hello SOA 記錄 hello 區域*contoso.com* hello 資源群組中*MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6c3f2-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="6c3f2-214">在 hello 區域的 apex toomodify NS 記錄</span><span class="sxs-lookup"><span data-stu-id="6c3f2-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="6c3f2-215">在 hello 區域的 apex 設定 hello NS 記錄會自動建立與每個 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="6c3f2-216">它包含 hello hello Azure DNS 名稱伺服器指派的 toohello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="6c3f2-217">您可以加入其他的名稱伺服器 toothis NS 記錄集，toosupport 共同裝載網域使用一個以上的 DNS 提供者。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="6c3f2-218">您也可以修改 hello TTL 和此記錄集的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="6c3f2-219">不過，您無法移除或修改 hello 預先填入的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="6c3f2-220">請注意這適用於僅 toohello NS 記錄集在 hello 區域的 apex。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="6c3f2-221">如果沒有限制，您可以修改其他 NS 記錄集在您的區域 （做為使用的 toodelegate 子區域）。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="6c3f2-222">hello 下列範例顯示如何 tooadd 其他的名稱伺服器 toohello NS 記錄設定在 hello 區域的 apex:</span><span class="sxs-lookup"><span data-stu-id="6c3f2-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="6c3f2-223">toomodify hello TTL 為現有的記錄設定</span><span class="sxs-lookup"><span data-stu-id="6c3f2-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="6c3f2-224">toomodify hello TTL 現有記錄的設定，請使用`azure network dns record-set <record-type> update`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-224">toomodify hello TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="6c3f2-225">如需協助，請參閱 `azure network dns record-set <record-type> update --help`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="6c3f2-226">hello 下列範例顯示如何 toomodify 記錄集 TTL，在此情況下 too60 秒：</span><span class="sxs-lookup"><span data-stu-id="6c3f2-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="6c3f2-227">toomodify hello 中繼資料的現有資料錄集</span><span class="sxs-lookup"><span data-stu-id="6c3f2-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="6c3f2-228">[設定中繼資料記錄](dns-zones-records.md#tags-and-metadata)可以是使用的 tooassociate 特定應用程式資料使用每個資料錄集時，做為索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="6c3f2-229">toomodify hello 中繼資料的現有記錄的設定，請使用`az network dns record-set <record-type> update`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-229">toomodify hello metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="6c3f2-230">如需協助，請參閱 `az network dns record-set <record-type> update --help`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="6c3f2-231">hello 下列範例示範如何 toomodify 記錄設定兩個中繼資料的項目，「 部門 = finance"和"環境 = 生產 」。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="6c3f2-232">請注意，任何現有的中繼資料是*取代*所指定的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="6c3f2-233">刪除記錄集</span><span class="sxs-lookup"><span data-stu-id="6c3f2-233">Delete a record set</span></span>

<span data-ttu-id="6c3f2-234">使用 hello 也可以刪除資料錄集`az network dns record-set <record-type> delete`命令。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-234">Record sets can be deleted by using hello `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="6c3f2-235">如需協助，請參閱 `azure network dns record-set <record-type> delete --help`。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="6c3f2-236">刪除資料錄集時，也會刪除 hello 資料錄集內的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="6c3f2-237">您無法刪除 hello SOA 和 NS 記錄集在 hello 區域的 apex (`--name "@"`)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-237">You cannot delete hello SOA and NS record sets at hello zone apex (`--name "@"`).</span></span>  <span data-ttu-id="6c3f2-238">當 hello 區域建立，而且已刪除 hello 區域時自動刪除，這些會自動建立。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="6c3f2-239">hello 下列範例會刪除名為 hello 記錄*www*從 hello 區域類型的*contoso.com*資源群組中*MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6c3f2-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="6c3f2-240">您已提示的 tooconfirm hello 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="6c3f2-241">此提示，toosuppress 使用 hello`--yes`切換。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-241">toosuppress this prompt, use hello `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c3f2-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c3f2-242">Next steps</span></span>

<span data-ttu-id="6c3f2-243">深入了解[ Azure DNS 中的區域和記錄](dns-zones-records.md)。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="6c3f2-244">了解如何太[保護您的區域和記錄](dns-protect-zones-recordsets.md)時使用 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="6c3f2-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
