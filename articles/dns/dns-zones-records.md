---
title: "aaaDNS 區域，以及記錄概觀-Azure DNS |Microsoft 文件"
description: "將 DNS 區域和記錄，裝載於 Microsoft Azure DNS 中的支援概觀。"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a><span data-ttu-id="a028b-103">DNS 區域和記錄的概觀</span><span class="sxs-lookup"><span data-stu-id="a028b-103">Overview of DNS zones and records</span></span>

<span data-ttu-id="a028b-104">此頁面說明 hello 的網域、 DNS 區域和 DNS 記錄和資料錄集，及它們如何支援 Azure DNS 中的重要概念。</span><span class="sxs-lookup"><span data-stu-id="a028b-104">This page explains hello key concepts of domains, DNS zones, and DNS records and record sets, and how they are supported in Azure DNS.</span></span>

## <a name="domain-names"></a><span data-ttu-id="a028b-105">網域名稱</span><span class="sxs-lookup"><span data-stu-id="a028b-105">Domain names</span></span>

<span data-ttu-id="a028b-106">hello 網域名稱系統是網域的階層。</span><span class="sxs-lookup"><span data-stu-id="a028b-106">hello Domain Name System is a hierarchy of domains.</span></span> <span data-ttu-id="a028b-107">hello 階層是從 hello 'root' 網域，其名稱只是開始 '**。**'。</span><span class="sxs-lookup"><span data-stu-id="a028b-107">hello hierarchy starts from hello 'root' domain, whose name is simply '**.**'.</span></span>  <span data-ttu-id="a028b-108">下面接著最上層網域，例如 'com'、'net'、'org'、'uk' 或 'jp'。</span><span class="sxs-lookup"><span data-stu-id="a028b-108">Below this come top-level domains, such as 'com', 'net', 'org', 'uk' or 'jp'.</span></span>  <span data-ttu-id="a028b-109">再往下是第二層網域，例如 'org.uk' 或 'co.jp'。</span><span class="sxs-lookup"><span data-stu-id="a028b-109">Below these are second-level domains, such as 'org.uk' or 'co.jp'.</span></span> <span data-ttu-id="a028b-110">全域發佈 hello DNS 階層中的 hello 網域，hello 世界各地的 DNS 名稱伺服器所裝載。</span><span class="sxs-lookup"><span data-stu-id="a028b-110">hello domains in hello DNS hierarchy are globally distributed, hosted by DNS name servers around hello world.</span></span>

<span data-ttu-id="a028b-111">網域名稱註冊機構是 toopurchase 網域名稱，例如 'contoso.com' 可讓您的組織。</span><span class="sxs-lookup"><span data-stu-id="a028b-111">A domain name registrar is an organization that allows you toopurchase a domain name, such as 'contoso.com'.</span></span>  <span data-ttu-id="a028b-112">購買網域名稱提供 hello 右 toocontrol hello DNS 階層該名稱，例如允許 toodirect hello 名稱 'www.contoso.com' tooyour 公司網站。</span><span class="sxs-lookup"><span data-stu-id="a028b-112">Purchasing a domain name gives you hello right toocontrol hello DNS hierarchy under that name, for example allowing you toodirect hello name 'www.contoso.com' tooyour company web site.</span></span> <span data-ttu-id="a028b-113">hello 註冊機構可能裝載在代表您自己名稱伺服器 hello 網域，或者允許您 toospecify 替代名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="a028b-113">hello registrar may host hello domain in its own name servers on your behalf, or allow you toospecify alternative name servers.</span></span>

<span data-ttu-id="a028b-114">Azure DNS 提供全域散發、 高可用性的名稱伺服器基礎結構，您可以使用 toohost 您的網域。</span><span class="sxs-lookup"><span data-stu-id="a028b-114">Azure DNS provides a globally distributed, high-availability name server infrastructure, which you can use toohost your domain.</span></span> <span data-ttu-id="a028b-115">裝載 Azure DNS 中的網域，您可以管理您的 DNS 記錄，以 hello 相同的認證、 Api、 工具、 帳單和支援與其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="a028b-115">By hosting your domains in Azure DNS, you can manage your DNS records with hello same credentials, APIs, tools, billing, and support as your other Azure services.</span></span>

<span data-ttu-id="a028b-116">Azure DNS 目前不支援購買網域名稱。</span><span class="sxs-lookup"><span data-stu-id="a028b-116">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="a028b-117">如果您想 toopurchase 網域名稱，您會需要 toouse 第三方網域名稱註冊機構。</span><span class="sxs-lookup"><span data-stu-id="a028b-117">If you want toopurchase a domain name, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="a028b-118">hello 註冊機構通常費用小年費。</span><span class="sxs-lookup"><span data-stu-id="a028b-118">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="a028b-119">hello 網域的 DNS 記錄管理然後裝載在 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="a028b-119">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="a028b-120">請參閱[委派網域 tooAzure DNS](dns-domain-delegation.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a028b-120">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="dns-zones"></a><span data-ttu-id="a028b-121">DNS 區域</span><span class="sxs-lookup"><span data-stu-id="a028b-121">DNS zones</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a><span data-ttu-id="a028b-122">DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="a028b-122">DNS records</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a><span data-ttu-id="a028b-123">存留時間</span><span class="sxs-lookup"><span data-stu-id="a028b-123">Time-to-live</span></span>

<span data-ttu-id="a028b-124">hello 時間 toolive 或 TTL，會指定多久每一筆記錄快取的用戶端之前重新進行查詢。</span><span class="sxs-lookup"><span data-stu-id="a028b-124">hello time toolive, or TTL, specifies how long each record is cached by clients before being re-queried.</span></span> <span data-ttu-id="a028b-125">在上述範例中的 hello，hello TTL 是 3600 秒或 1 小時。</span><span class="sxs-lookup"><span data-stu-id="a028b-125">In hello above example, hello TTL is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="a028b-126">在 Azure DNS，hello TTL 指定 hello 資料錄集，不會針對每一筆記錄，因此相同的值用於該記錄中的所有記錄的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a028b-126">In Azure DNS, hello TTL is specified for hello record set, not for each record, so hello same value is used for all records within that record set.</span></span>  <span data-ttu-id="a028b-127">您可以指定介於 1 到 2,147,483,647 秒之間的任何 TTL 值。</span><span class="sxs-lookup"><span data-stu-id="a028b-127">You can specify any TTL value between 1 and 2,147,483,647 seconds.</span></span>

### <a name="wildcard-records"></a><span data-ttu-id="a028b-128">萬用字元記錄</span><span class="sxs-lookup"><span data-stu-id="a028b-128">Wildcard records</span></span>

<span data-ttu-id="a028b-129">Azure DNS 支援 [萬用字元記錄](https://en.wikipedia.org/wiki/Wildcard_DNS_record)。</span><span class="sxs-lookup"><span data-stu-id="a028b-129">Azure DNS supports [wildcard records](https://en.wikipedia.org/wiki/Wildcard_DNS_record).</span></span> <span data-ttu-id="a028b-130">萬用字元記錄都會傳回到具有相符名稱的回應 tooany 查詢 （除非接近的相符項目，從非萬用字元的資料錄集）。</span><span class="sxs-lookup"><span data-stu-id="a028b-130">Wildcard records are returned in response tooany query with a matching name (unless there is a closer match from a non-wildcard record set).</span></span> <span data-ttu-id="a028b-131">Azure DNS 支援 NS 和 SOA 以外的所有記錄類型的萬用字元記錄集。</span><span class="sxs-lookup"><span data-stu-id="a028b-131">Azure DNS supports wildcard record sets for all record types except NS and SOA.</span></span>

<span data-ttu-id="a028b-132">toocreate 萬用字元記錄設定，請使用 hello 記錄集名稱 '\*'。</span><span class="sxs-lookup"><span data-stu-id="a028b-132">toocreate a wildcard record set, use hello record set name '\*'.</span></span> <span data-ttu-id="a028b-133">或者，也可以使用最左邊標籤是 '\*' 的名稱，例如 '\*.foo'。</span><span class="sxs-lookup"><span data-stu-id="a028b-133">Alternatively, you can also use a name with '\*' as its left-most label, for example, '\*.foo'.</span></span>

### <a name="cname-records"></a><span data-ttu-id="a028b-134">CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="a028b-134">CNAME records</span></span>

<span data-ttu-id="a028b-135">CNAME 記錄集不能共存在 hello 與其他資料錄集具有相同名稱。</span><span class="sxs-lookup"><span data-stu-id="a028b-135">CNAME record sets cannot coexist with other record sets with hello same name.</span></span> <span data-ttu-id="a028b-136">例如，您無法建立 CNAME 記錄集相對名稱 'www' hello 和 A 記錄以 hello 相對名稱 'www' hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="a028b-136">For example, you cannot create a CNAME record set with hello relative name 'www' and an A record with hello relative name 'www' at hello same time.</span></span>

<span data-ttu-id="a028b-137">因為 hello 區域的 apex (名稱 = ' @') 一定會包含 hello NS 與 SOA 記錄 hello 區域建立時所建立的設定，您無法建立在 hello 區域的 apex 設定 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="a028b-137">Because hello zone apex (name = '@') always contains hello NS and SOA record sets that were created when hello zone was created, you can't create a CNAME record set at hello zone apex.</span></span>

<span data-ttu-id="a028b-138">這些條件約束會發生的 hello DNS 標準，而且不會限制的 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="a028b-138">These constraints arise from hello DNS standards and are not limitations of Azure DNS.</span></span>

### <a name="ns-records"></a><span data-ttu-id="a028b-139">NS 記錄</span><span class="sxs-lookup"><span data-stu-id="a028b-139">NS records</span></span>

<span data-ttu-id="a028b-140">在 hello 區域的 apex 設定 hello NS 記錄 (名稱 ' @') 會自動建立的每個 DNS 區域，並刪除 hello 區域時自動刪除 （無法刪除個別）。</span><span class="sxs-lookup"><span data-stu-id="a028b-140">hello NS record set at hello zone apex (name '@') is created automatically with each DNS zone, and is deleted automatically when hello zone is deleted (it cannot be deleted separately).</span></span>

<span data-ttu-id="a028b-141">此記錄集包含 hello hello Azure DNS 名稱伺服器指派的 toohello 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="a028b-141">This record set contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span> <span data-ttu-id="a028b-142">您可以加入其他的名稱伺服器 toothis NS 記錄集，toosupport 共同裝載網域使用一個以上的 DNS 提供者。</span><span class="sxs-lookup"><span data-stu-id="a028b-142">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="a028b-143">您也可以修改 hello TTL 和此記錄集的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a028b-143">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="a028b-144">不過，您無法移除或修改 hello 預先填入的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="a028b-144">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span> 

<span data-ttu-id="a028b-145">請注意這適用於僅 toohello NS 記錄集在 hello 區域的 apex。</span><span class="sxs-lookup"><span data-stu-id="a028b-145">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="a028b-146">可以建立、 修改和刪除條件約束沒有其他 NS 記錄集在您的區域 （做為使用的 toodelegate 子區域）。</span><span class="sxs-lookup"><span data-stu-id="a028b-146">Other NS record sets in your zone (as used toodelegate child zones) can be created, modified and deleted without constraint.</span></span>

### <a name="soa-records"></a><span data-ttu-id="a028b-147">SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="a028b-147">SOA records</span></span>

<span data-ttu-id="a028b-148">SOA 記錄集建立而自動建立 hello 區域的每個區域的 apex (名稱 = ' @')，並刪除 hello 區域時自動刪除。</span><span class="sxs-lookup"><span data-stu-id="a028b-148">A SOA record set is created automatically at hello apex of each zone (name = '@'), and is deleted automatically when hello zone is deleted.</span></span>  <span data-ttu-id="a028b-149">無法個別建立或刪除 SOA 記錄。</span><span class="sxs-lookup"><span data-stu-id="a028b-149">SOA records cannot be created or deleted separately.</span></span>

<span data-ttu-id="a028b-150">您可以修改 hello SOA 記錄 hello 'host' 屬性，就是預先設定的 toorefer toohello 主要名稱伺服器提供的 Azure DNS 除外的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="a028b-150">You can modify all properties of hello SOA record except for hello 'host' property, which is pre-configured toorefer toohello primary name server name provided by Azure DNS.</span></span>

### <a name="spf-records"></a><span data-ttu-id="a028b-151">SPF 記錄</span><span class="sxs-lookup"><span data-stu-id="a028b-151">SPF records</span></span>

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a><span data-ttu-id="a028b-152">SRV 記錄</span><span class="sxs-lookup"><span data-stu-id="a028b-152">SRV records</span></span>

<span data-ttu-id="a028b-153">[SRV 記錄](https://en.wikipedia.org/wiki/SRV_record)所使用的各種服務 toospecify 伺服器位置。</span><span class="sxs-lookup"><span data-stu-id="a028b-153">[SRV records](https://en.wikipedia.org/wiki/SRV_record) are used by various services toospecify server locations.</span></span> <span data-ttu-id="a028b-154">在 Azure DNS 中指定 SRV 記錄時︰</span><span class="sxs-lookup"><span data-stu-id="a028b-154">When specifying an SRV record in Azure DNS:</span></span>

* <span data-ttu-id="a028b-155">hello*服務*和*通訊協定*必須是指定為 hello 記錄集名稱的一部分，加上底線。</span><span class="sxs-lookup"><span data-stu-id="a028b-155">hello *service* and *protocol* must be specified as part of hello record set name, prefixed with underscores.</span></span>  <span data-ttu-id="a028b-156">例如，'\_sip.\_tcp.name'。</span><span class="sxs-lookup"><span data-stu-id="a028b-156">For example, '\_sip.\_tcp.name'.</span></span>  <span data-ttu-id="a028b-157">在 hello 區域的 apex 記錄，則會有任何需要 toospecify '@' 在 hello 記錄名稱，只要使用 hello 服務和通訊協定，例如'\_sip。\_tcp'。</span><span class="sxs-lookup"><span data-stu-id="a028b-157">For a record at hello zone apex, there is no need toospecify '@' in hello record name, simply use hello service and protocol, for example '\_sip.\_tcp'.</span></span>
* <span data-ttu-id="a028b-158">hello*優先順序*，*加權*，*連接埠*，和*目標*已指定為 hello 記錄組中的每一筆記錄的參數。</span><span class="sxs-lookup"><span data-stu-id="a028b-158">hello *priority*, *weight*, *port*, and *target* are specified as parameters of each record in hello record set.</span></span>

### <a name="txt-records"></a><span data-ttu-id="a028b-159">TXT 記錄</span><span class="sxs-lookup"><span data-stu-id="a028b-159">TXT records</span></span>

<span data-ttu-id="a028b-160">TXT 記錄會使用的 toomap 網域名稱 tooarbitrary 文字字串。</span><span class="sxs-lookup"><span data-stu-id="a028b-160">TXT records are used toomap domain names tooarbitrary text strings.</span></span> <span data-ttu-id="a028b-161">用於多個應用程式，特別相關的 tooemail 組態，例如 hello[寄件者原則架構 (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework)和[DomainKeys 識別郵件 (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail)。</span><span class="sxs-lookup"><span data-stu-id="a028b-161">They are used in multiple applications, in particular related tooemail configuration, such as hello [Sender Policy Framework (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) and [DomainKeys Identified Mail (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).</span></span>

<span data-ttu-id="a028b-162">hello DNS 標準允許單一的 TXT 記錄 toocontain 多個字串，其中每個可能是 up too254 字元的長度。</span><span class="sxs-lookup"><span data-stu-id="a028b-162">hello DNS standards permit a single TXT record toocontain multiple strings, each of which may be up too254 characters in length.</span></span> <span data-ttu-id="a028b-163">使用多個字串時，用戶端會將這些字串連接並視為單一字串。</span><span class="sxs-lookup"><span data-stu-id="a028b-163">Where multiple strings are used, they are concatenated by clients and treated as a single string.</span></span>

<span data-ttu-id="a028b-164">在呼叫 hello Azure DNS REST API 時，您需要 toospecify TXT 的每個字串分開。</span><span class="sxs-lookup"><span data-stu-id="a028b-164">When calling hello Azure DNS REST API, you need toospecify each TXT string separately.</span></span>  <span data-ttu-id="a028b-165">當使用 hello Azure 入口網站、 PowerShell 或 CLI 介面應該指定每筆記錄，如有必要就會自動劃分為段 254 個字元的單一字串。</span><span class="sxs-lookup"><span data-stu-id="a028b-165">When using hello Azure portal, PowerShell or CLI interfaces you should specify a single string per record, which is automatically divided into 254-character segments if necessary.</span></span>

<span data-ttu-id="a028b-166">在 DNS 記錄中的多個字串不應與混淆的 hello hello TXT 記錄組中的多個 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="a028b-166">hello multiple strings in a DNS record should not be confused with hello multiple TXT records in a TXT record set.</span></span>  <span data-ttu-id="a028b-167">TXT 記錄集可以包含多個記錄，「每一個」記錄可以包含多個字串。</span><span class="sxs-lookup"><span data-stu-id="a028b-167">A TXT record set can contain multiple records, *each of which* can contain multiple strings.</span></span>  <span data-ttu-id="a028b-168">Azure DNS 支援每個設定 （透過結合的所有記錄） 的 TXT 記錄總字串長度為 too1024 字元組成。</span><span class="sxs-lookup"><span data-stu-id="a028b-168">Azure DNS supports a total string length of up too1024 characters in each TXT record set (across all records combined).</span></span>

## <a name="tags-and-metadata"></a><span data-ttu-id="a028b-169">標記和中繼資料</span><span class="sxs-lookup"><span data-stu-id="a028b-169">Tags and metadata</span></span>

### <a name="tags"></a><span data-ttu-id="a028b-170">標記</span><span class="sxs-lookup"><span data-stu-id="a028b-170">Tags</span></span>

<span data-ttu-id="a028b-171">標記是名稱 / 值組的清單，以及所使用的 Azure Resource Manager toolabel 資源。</span><span class="sxs-lookup"><span data-stu-id="a028b-171">Tags are a list of name-value pairs and are used by Azure Resource Manager toolabel resources.</span></span>  <span data-ttu-id="a028b-172">Azure 資源管理員會使用您的 Azure 帳單標記 tooenable 篩選檢視，並讓您 tooset 哪些標籤上的原則所需。</span><span class="sxs-lookup"><span data-stu-id="a028b-172">Azure Resource Manager uses tags tooenable filtered views of your Azure bill, and also enables you tooset a policy on which tags are required.</span></span> <span data-ttu-id="a028b-173">如需標記的詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](../azure-resource-manager/resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="a028b-173">For more information about tags, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>

<span data-ttu-id="a028b-174">Azure DNS 支援在 DNS 區域資源上，使用 Azure Resource Manager 標記。</span><span class="sxs-lookup"><span data-stu-id="a028b-174">Azure DNS supports using Azure Resource Manager tags on DNS zone resources.</span></span>  <span data-ttu-id="a028b-175">不支援在 DNS 記錄集上使用標記，不過，支援在 DNS 記錄集上使用「中繼資料」作為替代，如下所述。</span><span class="sxs-lookup"><span data-stu-id="a028b-175">It does not support tags on DNS record sets, although as an alternative 'metadata' is supported on DNS record sets as explained below.</span></span>

### <a name="metadata"></a><span data-ttu-id="a028b-176">中繼資料</span><span class="sxs-lookup"><span data-stu-id="a028b-176">Metadata</span></span>

<span data-ttu-id="a028b-177">做為替代的 toorecord 集標記，Azure DNS 支援註釋使用 'metadata' 的資料錄集。</span><span class="sxs-lookup"><span data-stu-id="a028b-177">As an alternative toorecord set tags, Azure DNS supports annotating record sets using 'metadata'.</span></span>  <span data-ttu-id="a028b-178">類似 tootags，中繼資料可讓您 tooassociate 名稱 / 值組，而且每個資料錄集。</span><span class="sxs-lookup"><span data-stu-id="a028b-178">Similar tootags, metadata enables you tooassociate name-value pairs with each record set.</span></span>  <span data-ttu-id="a028b-179">這會很有用，例如 toorecord hello 目的每一筆記錄的設定。</span><span class="sxs-lookup"><span data-stu-id="a028b-179">This can be useful, for example toorecord hello purpose of each record set.</span></span>  <span data-ttu-id="a028b-180">與標記不同中繼資料無法使用的 tooprovide Azure 帳單的篩選的檢視，而不指定 Azure Resource Manager 原則中。</span><span class="sxs-lookup"><span data-stu-id="a028b-180">Unlike tags, metadata cannot be used tooprovide a filtered view of your Azure bill and cannot be specified in an Azure Resource Manager policy.</span></span>

## <a name="etags"></a><span data-ttu-id="a028b-181">Etag</span><span class="sxs-lookup"><span data-stu-id="a028b-181">Etags</span></span>

<span data-ttu-id="a028b-182">假設兩位或兩個處理序嘗試 toomodify DNS 記錄 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="a028b-182">Suppose two people or two processes try toomodify a DNS record at hello same time.</span></span> <span data-ttu-id="a028b-183">何者獲勝？</span><span class="sxs-lookup"><span data-stu-id="a028b-183">Which one wins?</span></span> <span data-ttu-id="a028b-184">和 hello 成功者知道他們已經覆寫其他人建立的變更嗎？</span><span class="sxs-lookup"><span data-stu-id="a028b-184">And does hello winner know that they've overwritten changes created by someone else?</span></span>

<span data-ttu-id="a028b-185">Azure DNS 會使用 Etag toohandle 並行的變更 toohello 相同資源安全。</span><span class="sxs-lookup"><span data-stu-id="a028b-185">Azure DNS uses Etags toohandle concurrent changes toohello same resource safely.</span></span> <span data-ttu-id="a028b-186">Etag 和 [Azure Resource Manager「標籤」](#tags)分開。</span><span class="sxs-lookup"><span data-stu-id="a028b-186">Etags are separate from [Azure Resource Manager 'Tags'](#tags).</span></span> <span data-ttu-id="a028b-187">每個 DNS 資源 (區域或記錄集) 都有一個相關聯的 Etag。</span><span class="sxs-lookup"><span data-stu-id="a028b-187">Each DNS resource (zone or record set) has an Etag associated with it.</span></span> <span data-ttu-id="a028b-188">每當擷取資源時，也會擷取其 Etag。</span><span class="sxs-lookup"><span data-stu-id="a028b-188">Whenever a resource is retrieved, its Etag is also retrieved.</span></span> <span data-ttu-id="a028b-189">在更新資源，您可以選擇 toopass 回 hello Etag，讓 Azure DNS 可以確認該 hello Etag hello 伺服器比對。</span><span class="sxs-lookup"><span data-stu-id="a028b-189">When updating a resource, you can choose toopass back hello Etag so Azure DNS can verify that hello Etag on hello server matches.</span></span> <span data-ttu-id="a028b-190">因為每個更新 tooa 資源產生 hello 正在重新產生的 Etag，Etag 不符表示已發生並行的變更。</span><span class="sxs-lookup"><span data-stu-id="a028b-190">Since each update tooa resource results in hello Etag being regenerated, an Etag mismatch indicates a concurrent change has occurred.</span></span> <span data-ttu-id="a028b-191">建立新的資源 tooensure hello 資源已經存在時，也可以使用 Etag。</span><span class="sxs-lookup"><span data-stu-id="a028b-191">Etags can also be used when creating a new resource tooensure that hello resource does not already exist.</span></span>

<span data-ttu-id="a028b-192">根據預設，Azure DNS PowerShell 會使用 Etag tooblock 並行的變更 toozones 資料錄集。</span><span class="sxs-lookup"><span data-stu-id="a028b-192">By default, Azure DNS PowerShell uses Etags tooblock concurrent changes toozones and record sets.</span></span> <span data-ttu-id="a028b-193">選擇性的 hello *-覆寫*參數可以是使用的 toosuppress Etag 檢查，在此情況下任何並行發生的變更會覆寫。</span><span class="sxs-lookup"><span data-stu-id="a028b-193">hello optional *-Overwrite* switch can be used toosuppress Etag checks, in which case any concurrent changes that have occurred are overwritten.</span></span>

<span data-ttu-id="a028b-194">在 hello 的 hello Azure DNS REST API 層級的 Etag 會使用 HTTP 標頭所指定的。</span><span class="sxs-lookup"><span data-stu-id="a028b-194">At hello level of hello Azure DNS REST API, Etags are specified using HTTP headers.</span></span>  <span data-ttu-id="a028b-195">下表中的 hello 中提供它們的行為：</span><span class="sxs-lookup"><span data-stu-id="a028b-195">Their behavior is given in hello following table:</span></span>

| <span data-ttu-id="a028b-196">標頭</span><span class="sxs-lookup"><span data-stu-id="a028b-196">Header</span></span> | <span data-ttu-id="a028b-197">行為</span><span class="sxs-lookup"><span data-stu-id="a028b-197">Behavior</span></span> |
| --- | --- |
| <span data-ttu-id="a028b-198">None</span><span class="sxs-lookup"><span data-stu-id="a028b-198">None</span></span> |<span data-ttu-id="a028b-199">PUT 一定成功 (沒有 Etag 檢查)</span><span class="sxs-lookup"><span data-stu-id="a028b-199">PUT always succeeds (no Etag checks)</span></span> |
| <span data-ttu-id="a028b-200">If-match <etag></span><span class="sxs-lookup"><span data-stu-id="a028b-200">If-match <etag></span></span> |<span data-ttu-id="a028b-201">唯有當資源存在且 Etag 符合時，PUT 才會成功</span><span class="sxs-lookup"><span data-stu-id="a028b-201">PUT only succeeds if resource exists and Etag matches</span></span> |
| <span data-ttu-id="a028b-202">If-match *</span><span class="sxs-lookup"><span data-stu-id="a028b-202">If-match *</span></span> |<span data-ttu-id="a028b-203">唯有當資源存在時，PUT 才會成功</span><span class="sxs-lookup"><span data-stu-id="a028b-203">PUT only succeeds if resource exists</span></span> |
| <span data-ttu-id="a028b-204">If-none-match *</span><span class="sxs-lookup"><span data-stu-id="a028b-204">If-none-match *</span></span> |<span data-ttu-id="a028b-205">唯有當資源不存在時，PUT 才會成功</span><span class="sxs-lookup"><span data-stu-id="a028b-205">PUT only succeeds if resource does not exist</span></span> |


## <a name="limits"></a><span data-ttu-id="a028b-206">限制</span><span class="sxs-lookup"><span data-stu-id="a028b-206">Limits</span></span>

<span data-ttu-id="a028b-207">使用 Azure DNS 時，適用下列預設限制 hello:</span><span class="sxs-lookup"><span data-stu-id="a028b-207">hello following default limits apply when using Azure DNS:</span></span>

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a><span data-ttu-id="a028b-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a028b-208">Next steps</span></span>

* <span data-ttu-id="a028b-209">使用 Azure DNS，toostart 深入了解如何太[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)和[建立 DNS 記錄](dns-getstarted-create-recordset-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a028b-209">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="a028b-210">toomigrate 現有的 DNS 區域，深入了解如何太[匯入和匯出 DNS 區域檔案](dns-import-export.md)。</span><span class="sxs-lookup"><span data-stu-id="a028b-210">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>
