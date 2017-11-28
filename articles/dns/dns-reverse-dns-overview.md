---
title: "在 Azure 中的反向 DNS 的 aaaOverview |Microsoft 文件"
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
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a><span data-ttu-id="aec42-103">Azure 反向 DNS 和支援概觀</span><span class="sxs-lookup"><span data-stu-id="aec42-103">Overview of reverse DNS and support in Azure</span></span>

<span data-ttu-id="aec42-104">本文提供如何反向 DNS 的運作方式，以及 hello 概觀反向 DNS 案例，Azure 支援。</span><span class="sxs-lookup"><span data-stu-id="aec42-104">This article gives an overview of how reverse DNS works, and hello reverse DNS scenarios supported in Azure.</span></span>

## <a name="what-is-reverse-dns"></a><span data-ttu-id="aec42-105">什麼是反向 DNS？</span><span class="sxs-lookup"><span data-stu-id="aec42-105">What is reverse DNS?</span></span>

<span data-ttu-id="aec42-106">傳統的 DNS 記錄啟用從 DNS 名稱 （例如，'www.contoso.com') tooan 的 IP 位址 （例如 64.4.6.100) 對應。</span><span class="sxs-lookup"><span data-stu-id="aec42-106">Conventional DNS records enable a mapping from a DNS name (such as 'www.contoso.com') tooan IP address (such as 64.4.6.100).</span></span>  <span data-ttu-id="aec42-107">反向 DNS 可讓 hello 轉譯的 IP 位址 (64.4.6.100) 後 tooa 名稱 ('www.contoso.com')。</span><span class="sxs-lookup"><span data-stu-id="aec42-107">Reverse DNS enables hello translation of an IP address (64.4.6.100) back tooa name ('www.contoso.com').</span></span>

<span data-ttu-id="aec42-108">反向 DNS 記錄使用於多種情況。</span><span class="sxs-lookup"><span data-stu-id="aec42-108">Reverse DNS records are used in a variety of situations.</span></span> <span data-ttu-id="aec42-109">例如，反向 DNS 記錄都廣泛利用驗證的電子郵件訊息的寄件者 hello 抵抗電子垃圾郵件。</span><span class="sxs-lookup"><span data-stu-id="aec42-109">For example, reverse DNS records are widely used in combating e-mail spam by verifying hello sender of an e-mail message.</span></span>  <span data-ttu-id="aec42-110">hello 接收的郵件伺服器擷取 hello hello 傳送伺服器的 IP 位址，反向 DNS 記錄，並確認是否裝載的授權的 toosend hello 傳來的電子郵件原始網域。</span><span class="sxs-lookup"><span data-stu-id="aec42-110">hello receiving mail server retrieves hello reverse DNS record of hello sending server's IP address, and verifies if that host is authorized toosend e-mail from hello originating domain.</span></span> 

## <a name="how-reverse-dns-works"></a><span data-ttu-id="aec42-111">反向 DNS 的運作方式</span><span class="sxs-lookup"><span data-stu-id="aec42-111">How reverse DNS works</span></span>

<span data-ttu-id="aec42-112">反向 DNS 記錄託管於特殊的 DNS 區域，稱為 'ARPA' 區域。</span><span class="sxs-lookup"><span data-stu-id="aec42-112">Reverse DNS records are hosted in special DNS zones, known as 'ARPA' zones.</span></span>  <span data-ttu-id="aec42-113">這些區域都會以平行方式，與裝載 'contoso.com'，像是 hello 一般階層構成個別 DNS 階層。</span><span class="sxs-lookup"><span data-stu-id="aec42-113">These zones form a separate DNS hierarchy in parallel with hello normal hierarchy hosting domains such as 'contoso.com'.</span></span>

<span data-ttu-id="aec42-114">例如，hello 'www.contoso.com' 的 DNS 記錄被實作 hello 名稱在 hello 區域 'contoso.com'，' www' 搭配使用的 DNS 'A' 記錄。</span><span class="sxs-lookup"><span data-stu-id="aec42-114">For example, hello DNS record 'www.contoso.com' is implemented using a DNS 'A' record with hello name 'www' in hello zone 'contoso.com'.</span></span>  <span data-ttu-id="aec42-115">此 A 記錄點 toohello 對應的 IP 位址，在此情況下 64.4.6.100。</span><span class="sxs-lookup"><span data-stu-id="aec42-115">This A record points toohello corresponding IP address, in this case 64.4.6.100.</span></span>  <span data-ttu-id="aec42-116">hello 反向對應實作分別使用 'PTR' 記錄，名為 '100' hello 區域 '6.4.64.in-addr.arpa' （IP 位址會反轉 ARPA 區域中附註）。此 PTR 記錄，如果它已正確地設定指向 toohello 名稱 'www.contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="aec42-116">hello reverse lookup is implemented separately, using a 'PTR' record named '100' in hello zone '6.4.64.in-addr.arpa' (note that IP addresses are reversed in ARPA zones.)  This PTR record, if it has been configured correctly, points toohello name 'www.contoso.com'.</span></span>

<span data-ttu-id="aec42-117">當組織被指派 IP 位址區塊時，因此也會擷取 hello 右 toomanage hello 對應 ARPA 區域。</span><span class="sxs-lookup"><span data-stu-id="aec42-117">When an organization is assigned an IP address block, they also acquire hello right toomanage hello corresponding ARPA zone.</span></span> <span data-ttu-id="aec42-118">hello 對應 toohello IP 位址區塊是供 Azure 所裝載和管理 microsoft ARPA 區域。</span><span class="sxs-lookup"><span data-stu-id="aec42-118">hello ARPA zones corresponding toohello IP address blocks used by Azure are hosted and managed by Microsoft.</span></span> <span data-ttu-id="aec42-119">您的 ISP 可能會裝載您自己的 IP 位址的 hello ARPA 區域，或可能會允許您選擇，例如 Azure DNS 的 DNS 服務中的 hello ARPA 區域 tooyou 主機。</span><span class="sxs-lookup"><span data-stu-id="aec42-119">Your ISP may host hello ARPA zone for your own IP addresses for you, or may allow tooyou host hello ARPA zone in a DNS service of your choice, such as Azure DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="aec42-120">正向 DNS 對應與反向 DNS 對應會在個別的平行 DNS 階層中實作。</span><span class="sxs-lookup"><span data-stu-id="aec42-120">Forward DNS lookups and reverse DNS lookups are implemented in separate, parallel DNS hierarchies.</span></span> <span data-ttu-id="aec42-121">hello 'www.contoso.com' 的反向對應是**不**裝載在 hello 區域 'contoso.com'，而是裝載於 hello 對應 IP 位址區塊的 hello ARPA 區域。</span><span class="sxs-lookup"><span data-stu-id="aec42-121">hello reverse lookup for 'www.contoso.com' is **not** hosted in hello zone 'contoso.com', rather it is hosted in hello ARPA zone for hello corresponding IP address block.</span></span> <span data-ttu-id="aec42-122">IPv4 和 IPv6 位址區塊使用不同的區域。</span><span class="sxs-lookup"><span data-stu-id="aec42-122">Separate zones are used for IPv4 and IPv6 address blocks.</span></span>

### <a name="ipv4"></a><span data-ttu-id="aec42-123">IPv4</span><span class="sxs-lookup"><span data-stu-id="aec42-123">IPv4</span></span>

<span data-ttu-id="aec42-124">IPv4 反向對應區域的 hello 名稱應為下列格式的 hello: `<IPv4 network prefix in reverse order>.in-addr.arpa`。</span><span class="sxs-lookup"><span data-stu-id="aec42-124">hello name of an IPv4 reverse lookup zone should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span>

<span data-ttu-id="aec42-125">例如，在建立反向對應區域 toohost 記錄與 Ip hello 192.0.2.0/24 前置詞中的主機時，hello 區域名稱來建立隔離的 hello 位址 (192.0.2) 然後反轉 hello 順序 (2.0.192) 並加入 hello hello 網路首碼後置詞`.in-addr.arpa`。</span><span class="sxs-lookup"><span data-stu-id="aec42-125">For example, when creating a reverse zone toohost records for hosts with IPs that are in hello 192.0.2.0/24 prefix, hello zone name would be created by isolating hello network prefix of hello address (192.0.2) and then reversing hello order (2.0.192) and adding hello suffix `.in-addr.arpa`.</span></span>

|<span data-ttu-id="aec42-126">子網路類別</span><span class="sxs-lookup"><span data-stu-id="aec42-126">Subnet class</span></span>|<span data-ttu-id="aec42-127">網路首碼</span><span class="sxs-lookup"><span data-stu-id="aec42-127">Network prefix</span></span>  |<span data-ttu-id="aec42-128">反轉的網路首碼</span><span class="sxs-lookup"><span data-stu-id="aec42-128">Reversed network prefix</span></span>  |<span data-ttu-id="aec42-129">標準後置詞</span><span class="sxs-lookup"><span data-stu-id="aec42-129">Standard suffix</span></span>  |<span data-ttu-id="aec42-130">反向區域名稱</span><span class="sxs-lookup"><span data-stu-id="aec42-130">Reverse zone name</span></span> |
|-------|----------------|------------|-----------------|---------------------------|
|<span data-ttu-id="aec42-131">類別 A</span><span class="sxs-lookup"><span data-stu-id="aec42-131">Class A</span></span>|<span data-ttu-id="aec42-132">203.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="aec42-132">203.0.0.0/8</span></span>     | <span data-ttu-id="aec42-133">203</span><span class="sxs-lookup"><span data-stu-id="aec42-133">203</span></span>        | <span data-ttu-id="aec42-134">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="aec42-134">.in-addr.arpa</span></span>   | `203.in-addr.arpa`        |
|<span data-ttu-id="aec42-135">類別 B</span><span class="sxs-lookup"><span data-stu-id="aec42-135">Class B</span></span>|<span data-ttu-id="aec42-136">198.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="aec42-136">198.51.0.0/16</span></span>   | <span data-ttu-id="aec42-137">51.198</span><span class="sxs-lookup"><span data-stu-id="aec42-137">51.198</span></span>     | <span data-ttu-id="aec42-138">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="aec42-138">.in-addr.arpa</span></span>   | `51.198.in-addr.arpa`     |
|<span data-ttu-id="aec42-139">類別 C</span><span class="sxs-lookup"><span data-stu-id="aec42-139">Class C</span></span>|<span data-ttu-id="aec42-140">192.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="aec42-140">192.0.2.0/24</span></span>    | <span data-ttu-id="aec42-141">2.0.192</span><span class="sxs-lookup"><span data-stu-id="aec42-141">2.0.192</span></span>    | <span data-ttu-id="aec42-142">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="aec42-142">.in-addr.arpa</span></span>   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a><span data-ttu-id="aec42-143">無類別 IPv4 委派</span><span class="sxs-lookup"><span data-stu-id="aec42-143">Classless IPv4 delegation</span></span>

<span data-ttu-id="aec42-144">在某些情況下，配置 tooan 組織 hello IP 範圍小於類別 C （/ 24） 範圍。</span><span class="sxs-lookup"><span data-stu-id="aec42-144">In some cases, hello IP range allocated tooan organization is smaller than a Class C (/24) range.</span></span> <span data-ttu-id="aec42-145">在此情況下，hello IP 範圍不是落在區域界限內 hello`.in-addr.arpa`區域階層，因此無法做為子區域委派。</span><span class="sxs-lookup"><span data-stu-id="aec42-145">In this case, hello IP range does not fall on a zone boundary within hello `.in-addr.arpa` zone hierarchy, and hence cannot be delegated as a child zone.</span></span>

<span data-ttu-id="aec42-146">相反地，使用不同的機制是 tootransfer 控制項的個別的反向對應 (PTR) 記錄 tooa 專用 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="aec42-146">Instead, a different mechanism is used tootransfer control of individual reverse lookup (PTR) records tooa dedicated DNS zone.</span></span> <span data-ttu-id="aec42-147">這項機制會委派子區域的每個 IP 範圍，然後對應 hello 的每個 IP 位址範圍個別 toothat 子區域使用 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="aec42-147">This mechanism delegates a child zone for each IP range, then maps each IP address in hello range individually toothat child zone using CNAME records.</span></span>

<span data-ttu-id="aec42-148">例如，假設組織已授與 hello IP 範圍 192.0.2.128/26 isp。</span><span class="sxs-lookup"><span data-stu-id="aec42-148">For example, suppose an organization is granted hello IP range 192.0.2.128/26 by its ISP.</span></span> <span data-ttu-id="aec42-149">這代表 64 個 IP 位址，從 192.0.2.128 too192.0.2.191。</span><span class="sxs-lookup"><span data-stu-id="aec42-149">This represents 64 IP addresses, from 192.0.2.128 too192.0.2.191.</span></span> <span data-ttu-id="aec42-150">此範圍的反向 DNS 實作如下：</span><span class="sxs-lookup"><span data-stu-id="aec42-150">Reverse DNS for this range is implemented as follows:</span></span>
- <span data-ttu-id="aec42-151">hello 組織會建立稱為 128 26.2.0.192.in-in-addr.arpa 反向對應區域。</span><span class="sxs-lookup"><span data-stu-id="aec42-151">hello organization creates a reverse lookup zone called 128-26.2.0.192.in-addr.arpa.</span></span> <span data-ttu-id="aec42-152">hello 前置詞 ' 128-26' 代表 hello 內的網路區段指派 toohello 組織 hello 類別 C （/ 24） 範圍。</span><span class="sxs-lookup"><span data-stu-id="aec42-152">hello prefix '128-26' represents hello network segment assigned toohello organization within hello Class C (/24) range.</span></span>
- <span data-ttu-id="aec42-153">hello ISP hello 類別 C 上層區域從建立 NS 記錄 tooset 向上 hello hello 上方區域的 DNS 委派。</span><span class="sxs-lookup"><span data-stu-id="aec42-153">hello ISP creates NS records tooset up hello DNS delegation for hello above zone from hello Class C parent zone.</span></span> <span data-ttu-id="aec42-154">它也會建立 CNAME 記錄在 hello 父 (類別 C) 反向對應區域中，對應 hello IP 範圍 toohello 新區域建立 hello 組織中的每個 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="aec42-154">It also creates CNAME records in hello parent (Class C) reverse lookup zone, mapping each IP address in hello IP range toohello new zone created by hello organization:</span></span>

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
- <span data-ttu-id="aec42-155">然後 hello 組織管理其子區域中的 hello 個別 PTR 記錄。</span><span class="sxs-lookup"><span data-stu-id="aec42-155">hello organization then manages hello individual PTR records within their child zone.</span></span>

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
<span data-ttu-id="aec42-156">Hello PTR 記錄的 IP 位址 '192.0.2.129' 查詢的反向查閱名為 '129.2.0.192.in-addr.arpa'。</span><span class="sxs-lookup"><span data-stu-id="aec42-156">A reverse lookup for hello IP address '192.0.2.129' queries for a PTR record named '129.2.0.192.in-addr.arpa'.</span></span> <span data-ttu-id="aec42-157">此查詢會透過 hello CNAME hello 父區域 toohello PTR 記錄中 hello 子區域解析。</span><span class="sxs-lookup"><span data-stu-id="aec42-157">This query resolves via hello CNAME in hello parent zone toohello PTR record in hello child zone.</span></span>

### <a name="ipv6"></a><span data-ttu-id="aec42-158">IPv6</span><span class="sxs-lookup"><span data-stu-id="aec42-158">IPv6</span></span>

<span data-ttu-id="aec42-159">IPv6 反向對應區域的 hello 名稱應為下列形式的 hello:`<IPv6 network prefix in reverse order>.ip6.arpa`</span><span class="sxs-lookup"><span data-stu-id="aec42-159">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`</span></span>

<span data-ttu-id="aec42-160">例如：</span><span class="sxs-lookup"><span data-stu-id="aec42-160">For example,.</span></span> <span data-ttu-id="aec42-161">為與 Ip 主機位於 hello 2001:db8:1000:abdc toohost 記錄建立反向對應區域時:: / 64 的前置詞，會藉由隔離 hello 的 hello 位址的網路首碼建立 hello 區域名稱 (2001:db8:abdc::)。</span><span class="sxs-lookup"><span data-stu-id="aec42-161">When creating a reverse zone toohost records for hosts with IPs that are in hello 2001:db8:1000:abdc::/64 prefix, hello zone name would be created by isolating hello network prefix of hello address (2001:db8:abdc::).</span></span> <span data-ttu-id="aec42-162">接下來展開 hello IPv6 網路首碼 tooremove[零壓縮](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx)，如果它是使用的 tooshorten hello IPv6 位址首碼 (2001:0db8:abdc:0000::)。</span><span class="sxs-lookup"><span data-stu-id="aec42-162">Next expand hello IPv6 network prefix tooremove [zero compression](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), if it was used tooshorten hello IPv6 address prefix (2001:0db8:abdc:0000::).</span></span> <span data-ttu-id="aec42-163">反向 hello 順序，因為 hello hello 前置詞中的每個十六進位數字之間的分隔符號，請使用句號，toobuild hello 反轉網路首碼 (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) 並加入 hello 尾碼`.ip6.arpa`。</span><span class="sxs-lookup"><span data-stu-id="aec42-163">Reverse hello order, using a period as hello delimiter between each hexadecimal number in hello prefix, toobuild hello reversed network prefix (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) and add hello suffix `.ip6.arpa`.</span></span>


|<span data-ttu-id="aec42-164">網路首碼</span><span class="sxs-lookup"><span data-stu-id="aec42-164">Network prefix</span></span>  |<span data-ttu-id="aec42-165">已展開並反轉的網路首碼</span><span class="sxs-lookup"><span data-stu-id="aec42-165">Expanded and reversed network prefix</span></span> |<span data-ttu-id="aec42-166">標準後置詞</span><span class="sxs-lookup"><span data-stu-id="aec42-166">Standard suffix</span></span> |<span data-ttu-id="aec42-167">反向區域名稱</span><span class="sxs-lookup"><span data-stu-id="aec42-167">Reverse zone name</span></span>  |
|---------|---------|---------|---------|
|<span data-ttu-id="aec42-168">2001:db8:abdc::/64</span><span class="sxs-lookup"><span data-stu-id="aec42-168">2001:db8:abdc::/64</span></span>    | <span data-ttu-id="aec42-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="aec42-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="aec42-170">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="aec42-170">.ip6.arpa</span></span>        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|<span data-ttu-id="aec42-171">2001:db8:1000:9102::/64</span><span class="sxs-lookup"><span data-stu-id="aec42-171">2001:db8:1000:9102::/64</span></span>    | <span data-ttu-id="aec42-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="aec42-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="aec42-173">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="aec42-173">.ip6.arpa</span></span>        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a><span data-ttu-id="aec42-174">Azure 的反向 DNS 支援</span><span class="sxs-lookup"><span data-stu-id="aec42-174">Azure support for reverse DNS</span></span>

<span data-ttu-id="aec42-175">Azure 支援兩個不同的案例與相關 tooreverse DNS:</span><span class="sxs-lookup"><span data-stu-id="aec42-175">Azure supports two separate scenarios relating tooreverse DNS:</span></span>

<span data-ttu-id="aec42-176">**裝載 hello 反向對應區域對應 tooyour IP 位址區塊。**</span><span class="sxs-lookup"><span data-stu-id="aec42-176">**Hosting hello reverse lookup zone corresponding tooyour IP address block.**</span></span>
<span data-ttu-id="aec42-177">可以使用 azure DNS 太[裝載反向對應區域和管理 hello PTR 記錄的每個反向 DNS 查閱](dns-reverse-dns-hosting.md)、 IPv4 和 IPv6。</span><span class="sxs-lookup"><span data-stu-id="aec42-177">Azure DNS can be used too[host your reverse lookup zones and manage hello PTR records for each reverse DNS lookup](dns-reverse-dns-hosting.md), for both IPv4 and IPv6.</span></span>  <span data-ttu-id="aec42-178">hello 建立 hello (ARPA) 的反向對應區域，設定 hello 委派的程序，並設定 PTR 記錄是 hello 相同與一般的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="aec42-178">hello process of creating hello reverse lookup (ARPA) zone, setting up hello delegation, and configuring PTR records is hello same as for regular DNS zones.</span></span>  <span data-ttu-id="aec42-179">hello 只差異是，必須設定 hello 委派，透過您的 ISP，而不是 DNS 註冊機構，以及應該用於 hello PTR 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="aec42-179">hello only differences are that hello delegation must be configured via your ISP rather than your DNS registrar, and only hello PTR record type should be used.</span></span>

<span data-ttu-id="aec42-180">**設定 hello 反向 DNS 記錄 hello 分派 tooyour Azure 服務的 IP 位址。**</span><span class="sxs-lookup"><span data-stu-id="aec42-180">**Configure hello reverse DNS record for hello IP address assigned tooyour Azure service.**</span></span> <span data-ttu-id="aec42-181">Azure 可讓您太[hello IP 位址配置 tooyour Azure 服務設定 hello 反向對應](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="aec42-181">Azure enables you too[configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>  <span data-ttu-id="aec42-182">Azure 會設定此反向對應為 hello 對應 ARPA 區域中的 PTR 記錄。</span><span class="sxs-lookup"><span data-stu-id="aec42-182">This reverse lookup is configured by Azure as a PTR record in hello corresponding ARPA zone.</span></span>  <span data-ttu-id="aec42-183">由 Microsoft 主控這些 ARPA 區域中，對應 Azure 中，所使用的 tooall hello IP 範圍</span><span class="sxs-lookup"><span data-stu-id="aec42-183">These ARPA zones, corresponding tooall hello IP ranges used by Azure, are hosted by Microsoft</span></span>

## <a name="next-steps"></a><span data-ttu-id="aec42-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aec42-184">Next steps</span></span>

<span data-ttu-id="aec42-185">如需反向 DNS 的詳細資訊，請參閱維基百科的 [reverse DNS lookup](http://en.wikipedia.org/wiki/Reverse_DNS_lookup) (反向 DNS 對應)。</span><span class="sxs-lookup"><span data-stu-id="aec42-185">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="aec42-186">了解如何太[主機 hello 反向對應區域，為您的 ISP 指派的 IP 範圍，在 Azure DNS](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="aec42-186">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>
<br>
<span data-ttu-id="aec42-187">了解如何太[管理您的 Azure 服務的反向 DNS 記錄](dns-reverse-dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="aec42-187">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>

