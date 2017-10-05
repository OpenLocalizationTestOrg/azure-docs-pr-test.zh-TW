---
title: "在 Azure DNS 中託管反向 DNS 對應區域 | Microsoft Docs"
description: "了解如何使用 Azure DNS 為您的 IP 範圍託管反向 DNS 對應區域"
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
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="21383-103">在 Azure DNS 中託管反向 DNS 對應區域</span><span class="sxs-lookup"><span data-stu-id="21383-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="21383-104">本文說明如何在 Azure DNS 中為指派的 IP 範圍託管反向 DNS 對應區域。</span><span class="sxs-lookup"><span data-stu-id="21383-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="21383-105">由反向對應區域代表的 IP 範圍必須指派給您的組織，通常由您的 ISP 指派。</span><span class="sxs-lookup"><span data-stu-id="21383-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="21383-106">若要為指派給 Azure 服務之 Azure 擁有的 IP 位址設定反向 DNS，請參閱[為配置給 Azure 服務的 IP 位址設定反向對應](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="21383-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="21383-107">在閱讀本文之前，您應該先熟悉這篇 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="21383-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="21383-108">本文會逐步引導您使用 Azure 入口網站、Azure PowerShell、Azure CLI 1.0 或 Azure CLI 2.0，建立第一個反向對應 DNS 區域和記錄。</span><span class="sxs-lookup"><span data-stu-id="21383-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="21383-109">建立反向對應 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="21383-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="21383-110">登入 [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="21383-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="21383-111">在 [中樞] 功能表上，按一下 [新增] > [網路] > 然後按一下 [DNS 區域] 開啟 [建立 DNS 區域] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="21383-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![DNS 區域](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="21383-113">在 [建立 DNS 區域] 刀鋒視窗中，命名 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="21383-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="21383-114">區域名稱針對 IPv4 和 IPv6 前置詞的製作方式不同。</span><span class="sxs-lookup"><span data-stu-id="21383-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="21383-115">請遵循 [IPv4](#ipv4) 或 [IPv6](#ipv6) 的指示來命名區域。</span><span class="sxs-lookup"><span data-stu-id="21383-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="21383-116">完成後按一下 [建立] 以建立區域。</span><span class="sxs-lookup"><span data-stu-id="21383-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="21383-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="21383-117">IPv4</span></span>

<span data-ttu-id="21383-118">IPv4 反向對應區域的名稱是以其所代表的 IP 範圍為根據。</span><span class="sxs-lookup"><span data-stu-id="21383-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="21383-119">格式應如下：`<IPv4 network prefix in reverse order>.in-addr.arpa`。</span><span class="sxs-lookup"><span data-stu-id="21383-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="21383-120">如需範例，請參閱 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md#ipv4)。</span><span class="sxs-lookup"><span data-stu-id="21383-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="21383-121">在 Azure DNS 中建立無類別反向 DNS 對應區域時，區域名稱中必須使用連字號 (`-`) 而不是正斜線 ('/')。</span><span class="sxs-lookup"><span data-stu-id="21383-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="21383-122">例如，IP 範圍 192.0.2.128/26 必須使用 `128-26.2.0.192.in-addr.arpa` 作為區域名稱，而不是 `128/26.2.0.192.in-addr.arpa`。</span><span class="sxs-lookup"><span data-stu-id="21383-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="21383-123">這是因為，雖然 DNS 標準兩者都支援，但 Azure DNS 不支援包含正斜線 (`/`) 字元的 DNS 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="21383-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="21383-124">下例示範如何透過 Azure 入口網站，在 Azure DNS 中建立名為 `2.0.192.in-addr.arpa` 的「類別 C」反向 DNS 區域：</span><span class="sxs-lookup"><span data-stu-id="21383-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![建立 DNS 區域](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="21383-126">「資源群組位置」定義資源群組的位置，對 DNS 區域沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="21383-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="21383-127">DNS 區域一定是「全域」位置，並不會顯示出來。</span><span class="sxs-lookup"><span data-stu-id="21383-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="21383-128">下列範例示範如何使用 Azure PowerShell 和 Azure CLI 完成這項工作：</span><span class="sxs-lookup"><span data-stu-id="21383-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="21383-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21383-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="21383-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="21383-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="21383-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="21383-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="21383-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="21383-132">IPv6</span></span>

<span data-ttu-id="21383-133">IPv6 反向對應區域的名稱格式應該如下：`<IPv6 network prefix in reverse order>.ip6.arpa`。</span><span class="sxs-lookup"><span data-stu-id="21383-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="21383-134">如需範例，請參閱 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md#ipv6)。</span><span class="sxs-lookup"><span data-stu-id="21383-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="21383-135">下例示範如何透過 Azure 入口網站，在 Azure DNS 中建立名為 `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` 的 IPv6 反向 DNS 對應區域：</span><span class="sxs-lookup"><span data-stu-id="21383-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![建立 DNS 區域](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="21383-137">「資源群組位置」定義資源群組的位置，對 DNS 區域沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="21383-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="21383-138">DNS 區域一定是「全域」位置，並不會顯示出來。</span><span class="sxs-lookup"><span data-stu-id="21383-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="21383-139">下列範例示範如何使用 Azure PowerShell 和 Azure CLI 完成這項工作：</span><span class="sxs-lookup"><span data-stu-id="21383-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="21383-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21383-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="21383-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="21383-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="21383-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="21383-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="21383-143">委派反向 DNS 對應區域</span><span class="sxs-lookup"><span data-stu-id="21383-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="21383-144">建立反向 DNS 對應區域之後，您必須確定該區域是從父區域委派。</span><span class="sxs-lookup"><span data-stu-id="21383-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="21383-145">DNS 委派可讓 DNS 名稱解析程序尋找託管 DNS 反向 DNS 對應區域的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="21383-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="21383-146">這可讓這些名稱伺服器接聽您位址範圍中的 IP 位址 DNS 反向查詢。</span><span class="sxs-lookup"><span data-stu-id="21383-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="21383-147">至於正向對應區域，委派 DNS 區域的程序請參閱[將您的網域委派給 Azure DNS](dns-delegate-domain-azure-dns.md)。</span><span class="sxs-lookup"><span data-stu-id="21383-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="21383-148">反向對應區域的委派運作方式相同。</span><span class="sxs-lookup"><span data-stu-id="21383-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="21383-149">唯一的差別是您需要以提供 IP 範圍的 ISP 設定名稱伺服器，而不是您的網域名稱註冊機構。</span><span class="sxs-lookup"><span data-stu-id="21383-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="21383-150">建立 DNS PTR 記錄</span><span class="sxs-lookup"><span data-stu-id="21383-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="21383-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="21383-151">IPv4</span></span>

<span data-ttu-id="21383-152">下例會逐步解說在 Azure DNS 的反向 DNS 區域中建立 PTR 記錄的程序。</span><span class="sxs-lookup"><span data-stu-id="21383-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="21383-153">關於其他記錄類型和修改現有的記錄，請參閱[使用 Azure 入口網站管理 DNS 記錄和記錄集](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="21383-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="21383-154">在 [DNS 區域] 刀鋒視窗頂端，選取 [+ 記錄集] 以開啟 [新增記錄集] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="21383-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![DNS 區域](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="21383-156">在 [新增記錄集] 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="21383-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="21383-157">從記錄的 [類型] 功能表中選取 [PTR]。</span><span class="sxs-lookup"><span data-stu-id="21383-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="21383-158">PTR 記錄的記錄集名稱必須是反向順序的其餘 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="21383-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="21383-159">在本例中，已填入前三個八位元當作區域名稱的一部分 (.2.0.192)。</span><span class="sxs-lookup"><span data-stu-id="21383-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="21383-160">因此，[名稱] 欄位只要再填入最後一個八位元。</span><span class="sxs-lookup"><span data-stu-id="21383-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="21383-161">例如，您可以將 IP 位址是 192.0.2.15 的資源記錄集命名為 "**15**"。</span><span class="sxs-lookup"><span data-stu-id="21383-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="21383-162">在 [網域名稱] 欄位中，使用 IP 輸入資源的完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="21383-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="21383-163">選取刀鋒視窗底部的 [確定]，建立 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="21383-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![新增記錄集](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="21383-165">下列範例示範如何使用 PowerShell 和 Azure CLI 完成這項工作：</span><span class="sxs-lookup"><span data-stu-id="21383-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="21383-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21383-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="21383-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="21383-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="21383-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="21383-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="21383-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="21383-169">IPv6</span></span>

<span data-ttu-id="21383-170">下例會逐步引導您完成建立新 'PTR' 記錄的程序。</span><span class="sxs-lookup"><span data-stu-id="21383-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="21383-171">關於其他記錄類型和修改現有的記錄，請參閱[使用 Azure 入口網站管理 DNS 記錄和記錄集](dns-operations-recordsets-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="21383-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="21383-172">在 [DNS 區域] 刀鋒視窗頂端，選取 [+ 記錄集] 以開啟 [新增記錄集] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="21383-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![DNS 區域刀鋒視窗](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="21383-174">在 [新增記錄集] 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="21383-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="21383-175">從記錄的 [類型] 功能表中選取 [PTR]。</span><span class="sxs-lookup"><span data-stu-id="21383-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="21383-176">PTR 記錄的記錄集名稱必須是反向順序的其餘 IPv6 位址。</span><span class="sxs-lookup"><span data-stu-id="21383-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="21383-177">它絕不能包含任何零壓縮。</span><span class="sxs-lookup"><span data-stu-id="21383-177">It must not include any zero compression.</span></span> <span data-ttu-id="21383-178">在本例中，已填入 IPv6 的第一組 64 位元當作區域名稱的一部分 (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa)。</span><span class="sxs-lookup"><span data-stu-id="21383-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="21383-179">因此，[名稱] 欄位只要再填入最後一組 64 位元。</span><span class="sxs-lookup"><span data-stu-id="21383-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="21383-180">以反向順序輸入 IP 位址的最後一組 64 位元，每個十六進位數字之間使用句點當作分隔符號。</span><span class="sxs-lookup"><span data-stu-id="21383-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="21383-181">例如，您可以將 IP 位址是 2001:0db8:abdc:0000:f524:10bc:1af9:405e 的資源記錄集命名為 "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**"。</span><span class="sxs-lookup"><span data-stu-id="21383-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="21383-182">在 [網域名稱] 欄位中，使用 IP 輸入資源的完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="21383-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="21383-183">選取刀鋒視窗底部的 [確定]，建立 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="21383-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![新增記錄集刀鋒視窗](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="21383-185">下列範例示範如何使用 PowerShell 和 Azure CLI 完成這項工作：</span><span class="sxs-lookup"><span data-stu-id="21383-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="21383-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21383-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="21383-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="21383-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="21383-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="21383-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="21383-189">檢視記錄</span><span class="sxs-lookup"><span data-stu-id="21383-189">View Records</span></span>

<span data-ttu-id="21383-190">若要檢視您所建立的記錄，請巡覽至您在 Azure 入口網站的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="21383-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="21383-191">在 [DNS 區域] 刀鋒視窗的下半部，您可以看到 DNS 區域的記錄。</span><span class="sxs-lookup"><span data-stu-id="21383-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="21383-192">您應該會看到預設 NS 和 SOA 記錄 (在每個區域中建立)，還有您已建立的任何新記錄。</span><span class="sxs-lookup"><span data-stu-id="21383-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="21383-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="21383-193">IPv4</span></span>

<span data-ttu-id="21383-194">[DNS 區域] 刀鋒視窗，顯示 IPv4 PTR 記錄：</span><span class="sxs-lookup"><span data-stu-id="21383-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![DNS 區域刀鋒視窗](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="21383-196">下列範例示範如何使用 PowerShell 或 Azure CLI 檢視 PTR 記錄：</span><span class="sxs-lookup"><span data-stu-id="21383-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="21383-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21383-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="21383-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="21383-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="21383-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="21383-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="21383-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="21383-200">IPv6</span></span>

<span data-ttu-id="21383-201">[DNS 區域] 刀鋒視窗，顯示 IPv6 PTR 記錄：</span><span class="sxs-lookup"><span data-stu-id="21383-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![DNS 區域刀鋒視窗](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="21383-203">下列範例示範如何使用 PowerShell 和 Azure CLI 檢視記錄：</span><span class="sxs-lookup"><span data-stu-id="21383-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="21383-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21383-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="21383-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="21383-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="21383-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="21383-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="21383-207">常見問題集</span><span class="sxs-lookup"><span data-stu-id="21383-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="21383-208">我可以在 Azure DNS 上，為 ISP 指派的 IP 區塊託管反向 DNS 對應區域嗎？</span><span class="sxs-lookup"><span data-stu-id="21383-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="21383-209">是。</span><span class="sxs-lookup"><span data-stu-id="21383-209">Yes.</span></span> <span data-ttu-id="21383-210">完全支援在 Azure DNS 中為您自己的 IP 範圍託管反向對應 (ARPA) 區域。</span><span class="sxs-lookup"><span data-stu-id="21383-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="21383-211">依本文所述，在 Azure DNS 中建立反向對應區域，然後使用您的 ISP [委派區域](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="21383-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="21383-212">接著，您就可以使用與其他記錄類型相同的方式來管理每個反向對應的 PTR 記錄。</span><span class="sxs-lookup"><span data-stu-id="21383-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="21383-213">託管反向 DNS 對應區域的費用如何？</span><span class="sxs-lookup"><span data-stu-id="21383-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="21383-214">在 Azure DNS 中為 ISP 指派的 IP 區塊託管反向 DNS 對應區域，會依[標準 Azure DNS 費率](https://azure.microsoft.com/pricing/details/dns/)計價。</span><span class="sxs-lookup"><span data-stu-id="21383-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="21383-215">我可以同時在 Azure DNS 中為 IPv4 和 IPv6 位址託管反向 DNS 對應區域嗎？</span><span class="sxs-lookup"><span data-stu-id="21383-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="21383-216">是。</span><span class="sxs-lookup"><span data-stu-id="21383-216">Yes.</span></span> <span data-ttu-id="21383-217">本文說明如何在 Azure DNS 中同時建立 IPv4 和 IPv6 反向 DNS 對應區域。</span><span class="sxs-lookup"><span data-stu-id="21383-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="21383-218">可以匯入現有的反向 DNS 對應區域嗎？</span><span class="sxs-lookup"><span data-stu-id="21383-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="21383-219">是。</span><span class="sxs-lookup"><span data-stu-id="21383-219">Yes.</span></span> <span data-ttu-id="21383-220">您可以使用 Azure CLI 將現有的 DNS 區域匯入到 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="21383-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="21383-221">正向對應區域和反向對應區域都適用。</span><span class="sxs-lookup"><span data-stu-id="21383-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="21383-222">如需詳細資訊，請參閱[使用 Azure CLI 匯入及匯出 DNS 區域檔案](dns-import-export.md)。</span><span class="sxs-lookup"><span data-stu-id="21383-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="21383-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21383-223">Next steps</span></span>

<span data-ttu-id="21383-224">如需反向 DNS 的詳細資訊，請參閱維基百科的 [reverse DNS lookup](http://en.wikipedia.org/wiki/Reverse_DNS_lookup) (反向 DNS 對應)。</span><span class="sxs-lookup"><span data-stu-id="21383-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="21383-225">了解如何[管理 Azure 服務的反向 DNS 記錄](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="21383-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
