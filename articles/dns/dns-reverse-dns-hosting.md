---
title: "aaaHosting 反向 DNS 對應區域，在 Azure DNS |Microsoft 文件"
description: "了解如何 toouse Azure DNS toohost hello 反向 DNS 對應區域的 IP 範圍"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="d3b2a-103">在 Azure DNS 中託管反向 DNS 對應區域</span><span class="sxs-lookup"><span data-stu-id="d3b2a-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="d3b2a-104">本文說明如何 toohost hello 反轉您指派的 IP 範圍中 Azure DNS 的 DNS 對應區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="d3b2a-105">hello IP 範圍由 hello 反向對應區域，必須指派 tooyour 組織通常由您的 ISP。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="d3b2a-106">tooconfigure 反向 DNS Azure 擁有 IP 位址指派 tooyour Azure 服務，請參閱[hello IP 位址配置 tooyour Azure 服務設定 hello 反向對應](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="d3b2a-107">在閱讀本文之前，您應該先熟悉這篇 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="d3b2a-108">這篇文章會引導您透過 hello 步驟 toocreate 您的第一個反向對應 DNS 區域與記錄使用 hello Azure 入口網站，Azure PowerShell、 Azure CLI 1.0 或 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="d3b2a-109">建立反向對應 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="d3b2a-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="d3b2a-110">登入 toohello [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d3b2a-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="d3b2a-111">在 hello 中樞功能表中，按一下，然後按一下**新增** > **網路**>，然後按一下 **DNS 區域**tooopen hello**建立 DNS 區域**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![DNS 區域](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="d3b2a-113">在 hello**建立 DNS 區域**刀鋒視窗中，命名您的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="d3b2a-114">hello hello 區域名稱是以不同的方式製作的 IPv4 和 IPv6 首碼。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="d3b2a-115">使用任一個 hello 指示[IPV4](#ipv4)或[IPv6](#ipv6) tooname 您的區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="d3b2a-116">當完成時按一下**建立**toocreate hello 區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="d3b2a-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="d3b2a-117">IPv4</span></span>

<span data-ttu-id="d3b2a-118">IPv4 反向對應區域的 hello 名稱根據它所代表的 hello IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="d3b2a-119">應為下列格式的 hello: `<IPv4 network prefix in reverse order>.in-addr.arpa`。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="d3b2a-120">如需範例，請參閱 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md#ipv4)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="d3b2a-121">當 Azure DNS 中建立 classless inter-domain routing 反向 DNS 查閱區域，您必須使用連字號 (`-`) 而不是正斜線 （'/') 在 hello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="d3b2a-122">例如，針對 hello IP 範圍 192.0.2.128/26，您必須使用`128-26.2.0.192.in-addr.arpa`hello 區域名稱，而不是為`128/26.2.0.192.in-addr.arpa`。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="d3b2a-123">這是因為雖然兩者 hello DNS 標準的支援，DNS 區域名稱中包含 hello 正斜線 (`/`) Azure DNS 中不支援的字元。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="d3b2a-124">hello 下列範例示範如何 toocreate ' 類別 C' 反向 DNS 區域命名為`2.0.192.in-addr.arpa`Azure DNS 透過 hello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="d3b2a-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![建立 DNS 區域](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="d3b2a-126">hello '資源群組位置' 定義 hello 位置 hello 資源群組，且不會影響 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="d3b2a-127">hello DNS 區域位置一定是 'global'，而且不會顯示。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="d3b2a-128">hello 下列範例顯示如何 toocomplete 此工作使用 Azure PowerShell 和 hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="d3b2a-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d3b2a-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b2a-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d3b2a-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d3b2a-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="d3b2a-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="d3b2a-132">IPv6</span></span>

<span data-ttu-id="d3b2a-133">IPv6 反向對應區域的 hello 名稱應為下列格式的 hello: `<IPv6 network prefix in reverse order>.ip6.arpa`。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="d3b2a-134">如需範例，請參閱 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md#ipv6)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="d3b2a-135">hello 下列範例示範如何 toocreate IPv6 反向 DNS 查閱區域命名`0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa`Azure DNS 透過 hello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="d3b2a-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![建立 DNS 區域](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="d3b2a-137">hello '資源群組位置' 定義 hello 位置 hello 資源群組，且不會影響 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="d3b2a-138">hello DNS 區域位置一定是 'global'，而且不會顯示。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="d3b2a-139">hello 下列範例顯示如何 toocomplete 此工作使用 Azure PowerShell 和 hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="d3b2a-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d3b2a-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b2a-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="d3b2a-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="d3b2a-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="d3b2a-143">委派反向 DNS 對應區域</span><span class="sxs-lookup"><span data-stu-id="d3b2a-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="d3b2a-144">一旦建立 DNS 反向查閱區域，您必須確定該 hello 區域會從 hello 父區域委派。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="d3b2a-145">DNS 委派可讓 hello DNS 名稱解析程序 toofind hello 名稱伺服器裝載 DNS 反向查閱區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="d3b2a-146">這可讓這些名稱伺服器 tooanswer DNS 反向查詢 hello 中的 IP 位址的位址範圍。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="d3b2a-147">正向對應區域的委派 DNS 區域的 hello 程序所述[委派您網域 tooAzure DNS](dns-delegate-domain-azure-dns.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="d3b2a-148">反向對應區域的委派 hello 的運作方式相同。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="d3b2a-149">hello 唯一的差別是您需要以提供您的 IP 範圍，而不是網域名稱註冊機構的 ISP hello tooconfigure hello 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="d3b2a-150">建立 DNS PTR 記錄</span><span class="sxs-lookup"><span data-stu-id="d3b2a-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="d3b2a-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="d3b2a-151">IPv4</span></span>

<span data-ttu-id="d3b2a-152">hello 下列範例將引導您 hello 程序建立反向 DNS 區域中 Azure DNS PTR 記錄。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="d3b2a-153">其他的記錄類型和 toomodify 現有的記錄，請參閱[管理 DNS 記錄，並使用資料錄集 hello Azure 入口網站](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="d3b2a-154">頂端的 hello hello **DNS 區域**刀鋒視窗中，選取**+ 記錄集**tooopen hello**加入資料錄集**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![DNS 區域](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="d3b2a-156">在 hello**加入資料錄集**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="d3b2a-157">選取**PTR** hello 記錄 」**類型**」 功能表。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="d3b2a-158">hello PTR 記錄 hello 資料錄集的名稱必須 toobe hello rest hello IPv4 位址的反向順序。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="d3b2a-159">在此範例中，hello 前三個八位元都已填入 hello 區域名稱 (.2.0.192) 的一部分。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="d3b2a-160">因此，只有 hello 最後一個八位元會提供 hello 名稱 欄位中。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="d3b2a-161">例如，您可以將 IP 位址是 192.0.2.15 的資源記錄集命名為 "**15**"。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="d3b2a-162">在 hello"**網域名稱**」 欄位中，輸入 hello 資源使用 hello IP 的 hello 完整的網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="d3b2a-163">選取**確定**底部 hello hello 刀鋒視窗 toocreate hello DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![新增記錄集](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="d3b2a-165">hello 以下舉例說明幾如何 toocomplete 使用 PowerShell 和 hello AzureCLI 這項工作：</span><span class="sxs-lookup"><span data-stu-id="d3b2a-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d3b2a-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b2a-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="d3b2a-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="d3b2a-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="d3b2a-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="d3b2a-169">IPv6</span></span>

<span data-ttu-id="d3b2a-170">下列範例中的 hello 會引導您建立新的 'PTR' 記錄的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="d3b2a-171">其他的記錄類型和 toomodify 現有的記錄，請參閱[管理 DNS 記錄，並使用資料錄集 hello Azure 入口網站](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="d3b2a-172">頂端的 hello hello **DNS 區域刀鋒視窗**，選取**+ 記錄集**tooopen hello**加入資料錄集**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![DNS 區域刀鋒視窗](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="d3b2a-174">在 hello**加入資料錄集**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="d3b2a-175">選取**PTR** hello 記錄 」**類型**」 功能表。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="d3b2a-176">hello PTR 記錄 hello 資料錄集的名稱必須 toobe hello rest hello IPv6 位址的反向順序。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="d3b2a-177">它絕不能包含任何零壓縮。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-177">It must not include any zero compression.</span></span> <span data-ttu-id="d3b2a-178">在此範例中，hello 的 hello IPv6 都已填入 hello 區域名稱 (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa) 的一部分的第一個 64 位元。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="d3b2a-179">因此，hello 最後的 64 位元 hello 名稱 欄位中提供。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="d3b2a-180">hello hello IP 位址的最後一個 64 位元會輸入以相反順序中，使用句號做為每個十六進位數字之間的 hello 分隔符號。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="d3b2a-181">例如，您可以將 IP 位址是 2001:0db8:abdc:0000:f524:10bc:1af9:405e 的資源記錄集命名為 "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**"。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="d3b2a-182">在 hello"**網域名稱**」 欄位中，輸入 hello 資源使用 hello IP 的 hello 完整的網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="d3b2a-183">選取**確定**底部 hello hello 刀鋒視窗 toocreate hello DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![新增記錄集刀鋒視窗](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="d3b2a-185">hello 以下舉例說明幾如何 toocomplete 使用 PowerShell 和 hello AzureCLI 這項工作：</span><span class="sxs-lookup"><span data-stu-id="d3b2a-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d3b2a-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b2a-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="d3b2a-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="d3b2a-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="d3b2a-189">檢視記錄</span><span class="sxs-lookup"><span data-stu-id="d3b2a-189">View Records</span></span>

<span data-ttu-id="d3b2a-190">tooview hello 記錄建立時，瀏覽 tooyour hello Azure 入口網站中的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="d3b2a-191">Hello 中較低的 hello 一部分**DNS 區域**刀鋒視窗中，您可以看到 hello hello DNS 區域的記錄。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="d3b2a-192">您應該會看到 hello 預設 NS 與 SOA 記錄，也就建立在每個區域中加上您建立任何新記錄。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="d3b2a-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="d3b2a-193">IPv4</span></span>

<span data-ttu-id="d3b2a-194">[DNS 區域] 刀鋒視窗，顯示 IPv4 PTR 記錄：</span><span class="sxs-lookup"><span data-stu-id="d3b2a-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![DNS 區域刀鋒視窗](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="d3b2a-196">hello 下列範例顯示如何 tooview hello PTR 記錄使用 PowerShell 或 hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="d3b2a-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d3b2a-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b2a-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d3b2a-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d3b2a-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="d3b2a-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="d3b2a-200">IPv6</span></span>

<span data-ttu-id="d3b2a-201">[DNS 區域] 刀鋒視窗，顯示 IPv6 PTR 記錄：</span><span class="sxs-lookup"><span data-stu-id="d3b2a-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![DNS 區域刀鋒視窗](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="d3b2a-203">hello 以下是範例上 tooview hello 使用 PowerShell 和 hello AzureCLI 資料錄的方式：</span><span class="sxs-lookup"><span data-stu-id="d3b2a-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d3b2a-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b2a-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d3b2a-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d3b2a-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d3b2a-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="d3b2a-207">常見問題集</span><span class="sxs-lookup"><span data-stu-id="d3b2a-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="d3b2a-208">我可以在 Azure DNS 上，為 ISP 指派的 IP 區塊託管反向 DNS 對應區域嗎？</span><span class="sxs-lookup"><span data-stu-id="d3b2a-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="d3b2a-209">是。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-209">Yes.</span></span> <span data-ttu-id="d3b2a-210">完全支援裝載您自己的 IP 範圍，在 Azure DNS 中的 hello (ARPA) 的反向對應區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="d3b2a-211">在本文中，將會有說明，在 Azure DNS 中建立 hello 反向對應區域，然後使用您的 ISP 太[委派 hello 區域](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="d3b2a-212">接著，您可以管理 hello PTR 記錄 hello 中每個反向對應的相同方式其他記錄類型。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="d3b2a-213">託管反向 DNS 對應區域的費用如何？</span><span class="sxs-lookup"><span data-stu-id="d3b2a-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="d3b2a-214">裝載 hello 反向 DNS 對應區域的 Azure DNS 在您的 ISP 指派的 IP 區塊收費[標準 Azure DNS 費率](https://azure.microsoft.com/pricing/details/dns/)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="d3b2a-215">我可以同時在 Azure DNS 中為 IPv4 和 IPv6 位址託管反向 DNS 對應區域嗎？</span><span class="sxs-lookup"><span data-stu-id="d3b2a-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="d3b2a-216">是。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-216">Yes.</span></span> <span data-ttu-id="d3b2a-217">這篇文章說明如何 toocreate IPv4 和 IPv6 反向 DNS 查閱 Azure DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="d3b2a-218">可以匯入現有的反向 DNS 對應區域嗎？</span><span class="sxs-lookup"><span data-stu-id="d3b2a-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="d3b2a-219">是。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-219">Yes.</span></span> <span data-ttu-id="d3b2a-220">您可以使用 hello Azure CLI tooimport 現有 DNS 區域，將 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="d3b2a-221">正向對應區域和反向對應區域都適用。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="d3b2a-222">如需詳細資訊，請參閱[匯入和匯出 DNS 區域檔案使用 hello Azure CLI](dns-import-export.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3b2a-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3b2a-223">Next steps</span></span>

<span data-ttu-id="d3b2a-224">如需反向 DNS 的詳細資訊，請參閱維基百科的 [reverse DNS lookup](http://en.wikipedia.org/wiki/Reverse_DNS_lookup) (反向 DNS 對應)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="d3b2a-225">了解如何太[管理您的 Azure 服務的反向 DNS 記錄](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b2a-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
