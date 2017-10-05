---
title: "Azure 反向 DNS 概觀 | Microsoft Docs"
description: "了解反向 DNS 如何運作以及如何在 Azure 中使用"
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
ms.openlocfilehash: 70a1ad070e812951fca3d2b19da12c67f0725dd0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a><span data-ttu-id="92fc8-103">Azure 反向 DNS 和支援概觀</span><span class="sxs-lookup"><span data-stu-id="92fc8-103">Overview of reverse DNS and support in Azure</span></span>

<span data-ttu-id="92fc8-104">本文提供反向 DNS 運作方式以及 Azure 支援之反向 DNS 案例的概觀。</span><span class="sxs-lookup"><span data-stu-id="92fc8-104">This article gives an overview of how reverse DNS works, and the reverse DNS scenarios supported in Azure.</span></span>

## <a name="what-is-reverse-dns"></a><span data-ttu-id="92fc8-105">什麼是反向 DNS？</span><span class="sxs-lookup"><span data-stu-id="92fc8-105">What is reverse DNS?</span></span>

<span data-ttu-id="92fc8-106">傳統 DNS 記錄可啟用從 DNS 名稱至 (例如 'www.contoso.com') IP 位址 (例如 64.4.6.100) 的對應。</span><span class="sxs-lookup"><span data-stu-id="92fc8-106">Conventional DNS records enable a mapping from a DNS name (such as 'www.contoso.com') to an IP address (such as 64.4.6.100).</span></span>  <span data-ttu-id="92fc8-107">反向 DNS 則可將 IP 位址 (64.4.6.100) 轉譯回名稱 ('www.contoso.com')。</span><span class="sxs-lookup"><span data-stu-id="92fc8-107">Reverse DNS enables the translation of an IP address (64.4.6.100) back to a name ('www.contoso.com').</span></span>

<span data-ttu-id="92fc8-108">反向 DNS 記錄使用於多種情況。</span><span class="sxs-lookup"><span data-stu-id="92fc8-108">Reverse DNS records are used in a variety of situations.</span></span> <span data-ttu-id="92fc8-109">例如，透過驗證電子郵件訊息的寄件者，反向 DNS 記錄廣泛用於對抗垃圾電子郵件。</span><span class="sxs-lookup"><span data-stu-id="92fc8-109">For example, reverse DNS records are widely used in combating e-mail spam by verifying the sender of an e-mail message.</span></span>  <span data-ttu-id="92fc8-110">接收端郵件伺服器會擷取傳送端伺服器 IP 位址的反向 DNS 記錄，並確認該主機是否獲授權從原始網域傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="92fc8-110">The receiving mail server retrieves the reverse DNS record of the sending server's IP address, and verifies if that host is authorized to send e-mail from the originating domain.</span></span> 

## <a name="how-reverse-dns-works"></a><span data-ttu-id="92fc8-111">反向 DNS 的運作方式</span><span class="sxs-lookup"><span data-stu-id="92fc8-111">How reverse DNS works</span></span>

<span data-ttu-id="92fc8-112">反向 DNS 記錄託管於特殊的 DNS 區域，稱為 'ARPA' 區域。</span><span class="sxs-lookup"><span data-stu-id="92fc8-112">Reverse DNS records are hosted in special DNS zones, known as 'ARPA' zones.</span></span>  <span data-ttu-id="92fc8-113">這些區域會與一般階層託管網域 (例如 'contoso.com') 同時形成個別的 DNS 階層。</span><span class="sxs-lookup"><span data-stu-id="92fc8-113">These zones form a separate DNS hierarchy in parallel with the normal hierarchy hosting domains such as 'contoso.com'.</span></span>

<span data-ttu-id="92fc8-114">例如，DNS 記錄 'www.contoso.com' 是使用 DNS 'A' 記錄名稱 'www' 在區域 'contoso.com' 中實作的。</span><span class="sxs-lookup"><span data-stu-id="92fc8-114">For example, the DNS record 'www.contoso.com' is implemented using a DNS 'A' record with the name 'www' in the zone 'contoso.com'.</span></span>  <span data-ttu-id="92fc8-115">此 A 記錄會指向對應的 IP 位址，在此情況下為 64.4.6.100。</span><span class="sxs-lookup"><span data-stu-id="92fc8-115">This A record points to the corresponding IP address, in this case 64.4.6.100.</span></span>  <span data-ttu-id="92fc8-116">反向對應會在區域 '6.4.64.in-addr.arpa' 中使用名為 '100' 的 'PTR' 記錄分別實作 (請注意，IP 位址會在 ARPA 區域中反轉)。此 PTR 記錄 (如果它已正確設定) 會指向名稱 'www.contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="92fc8-116">The reverse lookup is implemented separately, using a 'PTR' record named '100' in the zone '6.4.64.in-addr.arpa' (note that IP addresses are reversed in ARPA zones.)  This PTR record, if it has been configured correctly, points to the name 'www.contoso.com'.</span></span>

<span data-ttu-id="92fc8-117">當組織獲指派 IP 位址區塊時，也會取得管理對應的 ARPA 區域的權限。</span><span class="sxs-lookup"><span data-stu-id="92fc8-117">When an organization is assigned an IP address block, they also acquire the right to manage the corresponding ARPA zone.</span></span> <span data-ttu-id="92fc8-118">對應至 Azure 所使用 IP 位址區塊的 ARPA 區域會由 Microsoft 託管並管理。</span><span class="sxs-lookup"><span data-stu-id="92fc8-118">The ARPA zones corresponding to the IP address blocks used by Azure are hosted and managed by Microsoft.</span></span> <span data-ttu-id="92fc8-119">您的 ISP 可能會為您託管您自己 IP 位址的 ARPA 區域，或可能讓您在所選的 DNS 服務 (例如，Azure DNS) 中託管 ARPA 區域。</span><span class="sxs-lookup"><span data-stu-id="92fc8-119">Your ISP may host the ARPA zone for your own IP addresses for you, or may allow to you host the ARPA zone in a DNS service of your choice, such as Azure DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="92fc8-120">正向 DNS 對應與反向 DNS 對應會在個別的平行 DNS 階層中實作。</span><span class="sxs-lookup"><span data-stu-id="92fc8-120">Forward DNS lookups and reverse DNS lookups are implemented in separate, parallel DNS hierarchies.</span></span> <span data-ttu-id="92fc8-121">'www.contoso.com' 的反向對應**不是**在區域 'contoso.com' 中託管，而是在對應的 IP 位址區塊的 ARPA 區域中託管。</span><span class="sxs-lookup"><span data-stu-id="92fc8-121">The reverse lookup for 'www.contoso.com' is **not** hosted in the zone 'contoso.com', rather it is hosted in the ARPA zone for the corresponding IP address block.</span></span> <span data-ttu-id="92fc8-122">IPv4 和 IPv6 位址區塊使用不同的區域。</span><span class="sxs-lookup"><span data-stu-id="92fc8-122">Separate zones are used for IPv4 and IPv6 address blocks.</span></span>

### <a name="ipv4"></a><span data-ttu-id="92fc8-123">IPv4</span><span class="sxs-lookup"><span data-stu-id="92fc8-123">IPv4</span></span>

<span data-ttu-id="92fc8-124">IPv4 反向對應區域的名稱格式應該如下：`<IPv4 network prefix in reverse order>.in-addr.arpa`。</span><span class="sxs-lookup"><span data-stu-id="92fc8-124">The name of an IPv4 reverse lookup zone should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span>

<span data-ttu-id="92fc8-125">例如，在建立反向區域託管 IP 前置詞為 192.0.2.0/24 的主機記錄時，會先取出位址的網路首碼 (192.0.2)，然後反轉順序 (2.0.192) 並加上尾碼 `.in-addr.arpa`，以這種方式建立區域名稱。</span><span class="sxs-lookup"><span data-stu-id="92fc8-125">For example, when creating a reverse zone to host records for hosts with IPs that are in the 192.0.2.0/24 prefix, the zone name would be created by isolating the network prefix of the address (192.0.2) and then reversing the order (2.0.192) and adding the suffix `.in-addr.arpa`.</span></span>

|<span data-ttu-id="92fc8-126">子網路類別</span><span class="sxs-lookup"><span data-stu-id="92fc8-126">Subnet class</span></span>|<span data-ttu-id="92fc8-127">網路首碼</span><span class="sxs-lookup"><span data-stu-id="92fc8-127">Network prefix</span></span>  |<span data-ttu-id="92fc8-128">反轉的網路首碼</span><span class="sxs-lookup"><span data-stu-id="92fc8-128">Reversed network prefix</span></span>  |<span data-ttu-id="92fc8-129">標準後置詞</span><span class="sxs-lookup"><span data-stu-id="92fc8-129">Standard suffix</span></span>  |<span data-ttu-id="92fc8-130">反向區域名稱</span><span class="sxs-lookup"><span data-stu-id="92fc8-130">Reverse zone name</span></span> |
|-------|----------------|------------|-----------------|---------------------------|
|<span data-ttu-id="92fc8-131">類別 A</span><span class="sxs-lookup"><span data-stu-id="92fc8-131">Class A</span></span>|<span data-ttu-id="92fc8-132">203.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="92fc8-132">203.0.0.0/8</span></span>     | <span data-ttu-id="92fc8-133">203</span><span class="sxs-lookup"><span data-stu-id="92fc8-133">203</span></span>        | <span data-ttu-id="92fc8-134">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="92fc8-134">.in-addr.arpa</span></span>   | `203.in-addr.arpa`        |
|<span data-ttu-id="92fc8-135">類別 B</span><span class="sxs-lookup"><span data-stu-id="92fc8-135">Class B</span></span>|<span data-ttu-id="92fc8-136">198.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="92fc8-136">198.51.0.0/16</span></span>   | <span data-ttu-id="92fc8-137">51.198</span><span class="sxs-lookup"><span data-stu-id="92fc8-137">51.198</span></span>     | <span data-ttu-id="92fc8-138">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="92fc8-138">.in-addr.arpa</span></span>   | `51.198.in-addr.arpa`     |
|<span data-ttu-id="92fc8-139">類別 C</span><span class="sxs-lookup"><span data-stu-id="92fc8-139">Class C</span></span>|<span data-ttu-id="92fc8-140">192.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="92fc8-140">192.0.2.0/24</span></span>    | <span data-ttu-id="92fc8-141">2.0.192</span><span class="sxs-lookup"><span data-stu-id="92fc8-141">2.0.192</span></span>    | <span data-ttu-id="92fc8-142">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="92fc8-142">.in-addr.arpa</span></span>   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a><span data-ttu-id="92fc8-143">無類別 IPv4 委派</span><span class="sxs-lookup"><span data-stu-id="92fc8-143">Classless IPv4 delegation</span></span>

<span data-ttu-id="92fc8-144">在某些情況下，配置給組織的 IP 範圍會小於類別 C (/24) 範圍。</span><span class="sxs-lookup"><span data-stu-id="92fc8-144">In some cases, the IP range allocated to an organization is smaller than a Class C (/24) range.</span></span> <span data-ttu-id="92fc8-145">本例中，IP 範圍不是落在 `.in-addr.arpa` 區域階層的區域界限內，因此無法委派為子區域。</span><span class="sxs-lookup"><span data-stu-id="92fc8-145">In this case, the IP range does not fall on a zone boundary within the `.in-addr.arpa` zone hierarchy, and hence cannot be delegated as a child zone.</span></span>

<span data-ttu-id="92fc8-146">改用不同的機制將個別反向對應 (PTR) 記錄的控制權轉移到專用的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="92fc8-146">Instead, a different mechanism is used to transfer control of individual reverse lookup (PTR) records to a dedicated DNS zone.</span></span> <span data-ttu-id="92fc8-147">這項機制會為每個 IP 範圍委派子區域，然後分別將範圍中的每個 IP 位址對應至使用 CNAME 記錄的子區域。</span><span class="sxs-lookup"><span data-stu-id="92fc8-147">This mechanism delegates a child zone for each IP range, then maps each IP address in the range individually to that child zone using CNAME records.</span></span>

<span data-ttu-id="92fc8-148">例如，假設 ISP 授與組織的 IP 範圍是 192.0.2.128/26。</span><span class="sxs-lookup"><span data-stu-id="92fc8-148">For example, suppose an organization is granted the IP range 192.0.2.128/26 by its ISP.</span></span> <span data-ttu-id="92fc8-149">這代表 64 個 IP 位址，從 192.0.2.128 到 192.0.2.191。</span><span class="sxs-lookup"><span data-stu-id="92fc8-149">This represents 64 IP addresses, from 192.0.2.128 to 192.0.2.191.</span></span> <span data-ttu-id="92fc8-150">此範圍的反向 DNS 實作如下：</span><span class="sxs-lookup"><span data-stu-id="92fc8-150">Reverse DNS for this range is implemented as follows:</span></span>
- <span data-ttu-id="92fc8-151">組織建立名為 128-26.2.0.192.in-addr.arpa 的反向對應區域。</span><span class="sxs-lookup"><span data-stu-id="92fc8-151">The organization creates a reverse lookup zone called 128-26.2.0.192.in-addr.arpa.</span></span> <span data-ttu-id="92fc8-152">前置詞 '128-26' 代表指派給類別 C (/24) 範圍內組織的網路區段。</span><span class="sxs-lookup"><span data-stu-id="92fc8-152">The prefix '128-26' represents the network segment assigned to the organization within the Class C (/24) range.</span></span>
- <span data-ttu-id="92fc8-153">ISP 會建立 NS 記錄，從類別 C 的上層區域設定上述區域的 DNS 委派。</span><span class="sxs-lookup"><span data-stu-id="92fc8-153">The ISP creates NS records to set up the DNS delegation for the above zone from the Class C parent zone.</span></span> <span data-ttu-id="92fc8-154">它也會在上層 (類別 C) 反向對應區域中建立 CNAME 記錄，將 IP 範圍中的每個 IP 位址對應到組織建立的新區域：</span><span class="sxs-lookup"><span data-stu-id="92fc8-154">It also creates CNAME records in the parent (Class C) reverse lookup zone, mapping each IP address in the IP range to the new zone created by the organization:</span></span>

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- <span data-ttu-id="92fc8-155">然後組織管理自己子區域內的個別 PTR 記錄。</span><span class="sxs-lookup"><span data-stu-id="92fc8-155">The organization then manages the individual PTR records within their child zone.</span></span>

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
<span data-ttu-id="92fc8-156">IP 位址 '192.0.2.129' 的反向對應會查詢名為 '129.2.0.192.in-addr.arpa' 的 PTR 記錄。</span><span class="sxs-lookup"><span data-stu-id="92fc8-156">A reverse lookup for the IP address '192.0.2.129' queries for a PTR record named '129.2.0.192.in-addr.arpa'.</span></span> <span data-ttu-id="92fc8-157">此查詢透過上層區域的 CNAME 解析成子區域的 PTR 記錄。</span><span class="sxs-lookup"><span data-stu-id="92fc8-157">This query resolves via the CNAME in the parent zone to the PTR record in the child zone.</span></span>

### <a name="ipv6"></a><span data-ttu-id="92fc8-158">IPv6</span><span class="sxs-lookup"><span data-stu-id="92fc8-158">IPv6</span></span>

<span data-ttu-id="92fc8-159">IPv6 反向對應區域的名稱格式應該如下：`<IPv6 network prefix in reverse order>.ip6.arpa`。</span><span class="sxs-lookup"><span data-stu-id="92fc8-159">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`</span></span>

<span data-ttu-id="92fc8-160">例如：</span><span class="sxs-lookup"><span data-stu-id="92fc8-160">For example,.</span></span> <span data-ttu-id="92fc8-161">在建立反向區域託管 IP 前置詞為 2001:db8:1000:abdc::/64 的主機記錄時，會隔離位址的網路首碼 (2001:db8:abdc::) 來建立區域名稱。</span><span class="sxs-lookup"><span data-stu-id="92fc8-161">When creating a reverse zone to host records for hosts with IPs that are in the 2001:db8:1000:abdc::/64 prefix, the zone name would be created by isolating the network prefix of the address (2001:db8:abdc::).</span></span> <span data-ttu-id="92fc8-162">接著展開 IPv6 網路首碼以移除[零壓縮](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx)，如果它用來縮短 IPv6 位址首碼 (2001:0db8:abdc:0000::)。</span><span class="sxs-lookup"><span data-stu-id="92fc8-162">Next expand the IPv6 network prefix to remove [zero compression](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), if it was used to shorten the IPv6 address prefix (2001:0db8:abdc:0000::).</span></span> <span data-ttu-id="92fc8-163">反轉順序，前置詞中每個十六進位數字之間使用句點為分隔符號，建置反轉的網路前置詞 (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`)，再加上尾碼 `.ip6.arpa`。</span><span class="sxs-lookup"><span data-stu-id="92fc8-163">Reverse the order, using a period as the delimiter between each hexadecimal number in the prefix, to build the reversed network prefix (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) and add the suffix `.ip6.arpa`.</span></span>


|<span data-ttu-id="92fc8-164">網路首碼</span><span class="sxs-lookup"><span data-stu-id="92fc8-164">Network prefix</span></span>  |<span data-ttu-id="92fc8-165">已展開並反轉的網路首碼</span><span class="sxs-lookup"><span data-stu-id="92fc8-165">Expanded and reversed network prefix</span></span> |<span data-ttu-id="92fc8-166">標準後置詞</span><span class="sxs-lookup"><span data-stu-id="92fc8-166">Standard suffix</span></span> |<span data-ttu-id="92fc8-167">反向區域名稱</span><span class="sxs-lookup"><span data-stu-id="92fc8-167">Reverse zone name</span></span>  |
|---------|---------|---------|---------|
|<span data-ttu-id="92fc8-168">2001:db8:abdc::/64</span><span class="sxs-lookup"><span data-stu-id="92fc8-168">2001:db8:abdc::/64</span></span>    | <span data-ttu-id="92fc8-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="92fc8-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="92fc8-170">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="92fc8-170">.ip6.arpa</span></span>        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|<span data-ttu-id="92fc8-171">2001:db8:1000:9102::/64</span><span class="sxs-lookup"><span data-stu-id="92fc8-171">2001:db8:1000:9102::/64</span></span>    | <span data-ttu-id="92fc8-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="92fc8-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="92fc8-173">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="92fc8-173">.ip6.arpa</span></span>        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a><span data-ttu-id="92fc8-174">Azure 的反向 DNS 支援</span><span class="sxs-lookup"><span data-stu-id="92fc8-174">Azure support for reverse DNS</span></span>

<span data-ttu-id="92fc8-175">Azure 支援與反向 DNS 相關的兩種不同案例：</span><span class="sxs-lookup"><span data-stu-id="92fc8-175">Azure supports two separate scenarios relating to reverse DNS:</span></span>

<span data-ttu-id="92fc8-176">**託管對應至您 IP 位址區塊的反轉對應區域。**</span><span class="sxs-lookup"><span data-stu-id="92fc8-176">**Hosting the reverse lookup zone corresponding to your IP address block.**</span></span>
<span data-ttu-id="92fc8-177">Azure DNS 可以用來[託管反轉對應區域和管理每個反向 DNS 對應的 PTR 記錄](dns-reverse-dns-hosting.md)，IPv4 及 IPv6 皆可。</span><span class="sxs-lookup"><span data-stu-id="92fc8-177">Azure DNS can be used to [host your reverse lookup zones and manage the PTR records for each reverse DNS lookup](dns-reverse-dns-hosting.md), for both IPv4 and IPv6.</span></span>  <span data-ttu-id="92fc8-178">建立反轉對應 (ARPA) 區域、設定委派，以及設定 PTR 記錄的程序與一般的 DNS 區域相同。</span><span class="sxs-lookup"><span data-stu-id="92fc8-178">The process of creating the reverse lookup (ARPA) zone, setting up the delegation, and configuring PTR records is the same as for regular DNS zones.</span></span>  <span data-ttu-id="92fc8-179">唯一的差異是必須透過您的 ISP 設定委派，而不是 DNS 註冊機構，而且僅應該使用 PTR 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="92fc8-179">The only differences are that the delegation must be configured via your ISP rather than your DNS registrar, and only the PTR record type should be used.</span></span>

<span data-ttu-id="92fc8-180">**設定指派給 Azure 服務之 IP 位址的反向 DNS 記錄**。</span><span class="sxs-lookup"><span data-stu-id="92fc8-180">**Configure the reverse DNS record for the IP address assigned to your Azure service.**</span></span> <span data-ttu-id="92fc8-181">[Azure 可讓您設定配置給 Azure 服務之 IP 位址的反向對應](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="92fc8-181">Azure enables you to [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>  <span data-ttu-id="92fc8-182">此反向對應是由 Azure 設定作為對應 ARPA 區域中的 PTR 記錄。</span><span class="sxs-lookup"><span data-stu-id="92fc8-182">This reverse lookup is configured by Azure as a PTR record in the corresponding ARPA zone.</span></span>  <span data-ttu-id="92fc8-183">對應至 Azure 所使用 IP 位址範圍的這些 ARPA 區域會由 Microsoft 託管</span><span class="sxs-lookup"><span data-stu-id="92fc8-183">These ARPA zones, corresponding to all the IP ranges used by Azure, are hosted by Microsoft</span></span>

## <a name="next-steps"></a><span data-ttu-id="92fc8-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92fc8-184">Next steps</span></span>

<span data-ttu-id="92fc8-185">如需反向 DNS 的詳細資訊，請參閱維基百科的 [reverse DNS lookup](http://en.wikipedia.org/wiki/Reverse_DNS_lookup) (反向 DNS 對應)。</span><span class="sxs-lookup"><span data-stu-id="92fc8-185">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="92fc8-186">了解如何[在 Azure DNS 中為您 ISP 指派的 IP 範圍託管反向對應區域](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="92fc8-186">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>
<br>
<span data-ttu-id="92fc8-187">了解如何[管理 Azure 服務的反向 DNS 記錄](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="92fc8-187">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>

