---
title: "DNS 區域和記錄概觀 - Azure DNS | Microsoft Docs"
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
ms.openlocfilehash: 5818986c939c464a364c52ab31225e15130ab30e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-dns-zones-and-records"></a><span data-ttu-id="ff133-103">DNS 區域和記錄的概觀</span><span class="sxs-lookup"><span data-stu-id="ff133-103">Overview of DNS zones and records</span></span>

<span data-ttu-id="ff133-104">此頁面說明的重要概念，包括網域、DNS 區域、DNS 記錄和記錄集，以及在 Azure DNS 中所受到的支援。</span><span class="sxs-lookup"><span data-stu-id="ff133-104">This page explains the key concepts of domains, DNS zones, and DNS records and record sets, and how they are supported in Azure DNS.</span></span>

## <a name="domain-names"></a><span data-ttu-id="ff133-105">網域名稱</span><span class="sxs-lookup"><span data-stu-id="ff133-105">Domain names</span></span>

<span data-ttu-id="ff133-106">網域名稱系統是網域階層。</span><span class="sxs-lookup"><span data-stu-id="ff133-106">The Domain Name System is a hierarchy of domains.</span></span> <span data-ttu-id="ff133-107">階層從「根」網域開始，其名稱只是 '**.**'。</span><span class="sxs-lookup"><span data-stu-id="ff133-107">The hierarchy starts from the 'root' domain, whose name is simply '**.**'.</span></span>  <span data-ttu-id="ff133-108">下面接著最上層網域，例如 'com'、'net'、'org'、'uk' 或 'jp'。</span><span class="sxs-lookup"><span data-stu-id="ff133-108">Below this come top-level domains, such as 'com', 'net', 'org', 'uk' or 'jp'.</span></span>  <span data-ttu-id="ff133-109">再往下是第二層網域，例如 'org.uk' 或 'co.jp'。</span><span class="sxs-lookup"><span data-stu-id="ff133-109">Below these are second-level domains, such as 'org.uk' or 'co.jp'.</span></span> <span data-ttu-id="ff133-110">DNS 階層中的網域散佈在全球，裝載在世界各地的 DNS 名稱伺服器上。</span><span class="sxs-lookup"><span data-stu-id="ff133-110">The domains in the DNS hierarchy are globally distributed, hosted by DNS name servers around the world.</span></span>

<span data-ttu-id="ff133-111">網域名稱註冊機構是種組織，可讓您購買網域名稱，例如 'contoso.com'。</span><span class="sxs-lookup"><span data-stu-id="ff133-111">A domain name registrar is an organization that allows you to purchase a domain name, such as 'contoso.com'.</span></span>  <span data-ttu-id="ff133-112">購買網域名稱可讓您控制該名稱底下的 DNS 階層，例如將網域名稱 'www.contoso.com' 導向貴公司的網站。</span><span class="sxs-lookup"><span data-stu-id="ff133-112">Purchasing a domain name gives you the right to control the DNS hierarchy under that name, for example allowing you to direct the name 'www.contoso.com' to your company web site.</span></span> <span data-ttu-id="ff133-113">可以讓該註冊機構代表您，將網域裝載在其自有的名稱伺服器上；或允許您指定替代的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff133-113">The registrar may host the domain in its own name servers on your behalf, or allow you to specify alternative name servers.</span></span>

<span data-ttu-id="ff133-114">Azure DNS 提供散佈全球、高可用性的名稱伺服器基礎結構，可用來裝載您的網域。</span><span class="sxs-lookup"><span data-stu-id="ff133-114">Azure DNS provides a globally distributed, high-availability name server infrastructure, which you can use to host your domain.</span></span> <span data-ttu-id="ff133-115">只要將您的網域裝載於 Azure DNS 中，就可以像管理其他 Azure 服務一樣，使用相同的認證、API、工具、計費方式和支援來管理 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ff133-115">By hosting your domains in Azure DNS, you can manage your DNS records with the same credentials, APIs, tools, billing, and support as your other Azure services.</span></span>

<span data-ttu-id="ff133-116">Azure DNS 目前不支援購買網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ff133-116">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="ff133-117">若想要購買網域名稱，必須洽詢第三方網域名稱註冊機構。</span><span class="sxs-lookup"><span data-stu-id="ff133-117">If you want to purchase a domain name, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="ff133-118">註冊機構通常會收取些微年費。</span><span class="sxs-lookup"><span data-stu-id="ff133-118">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="ff133-119">然後便可以在 Azure DNS 裝載這些網域來管理 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ff133-119">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="ff133-120">如需詳細資訊，請參閱 [將網域委派給 Azure DNS](dns-domain-delegation.md) 。</span><span class="sxs-lookup"><span data-stu-id="ff133-120">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="dns-zones"></a><span data-ttu-id="ff133-121">DNS 區域</span><span class="sxs-lookup"><span data-stu-id="ff133-121">DNS zones</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a><span data-ttu-id="ff133-122">DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="ff133-122">DNS records</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a><span data-ttu-id="ff133-123">存留時間</span><span class="sxs-lookup"><span data-stu-id="ff133-123">Time-to-live</span></span>

<span data-ttu-id="ff133-124">存留時間，或 TTL，指定每一筆記錄由用戶端快取多久，之後才會重新查詢。</span><span class="sxs-lookup"><span data-stu-id="ff133-124">The time to live, or TTL, specifies how long each record is cached by clients before being re-queried.</span></span> <span data-ttu-id="ff133-125">在上述範例中，TTL 是 3600 秒 (1 小時)。</span><span class="sxs-lookup"><span data-stu-id="ff133-125">In the above example, the TTL is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="ff133-126">在 Azure DNS 中，TTL 是針對記錄集而指定，而非針對每一筆記錄，因此相同的值，會套用到該記錄集內的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="ff133-126">In Azure DNS, the TTL is specified for the record set, not for each record, so the same value is used for all records within that record set.</span></span>  <span data-ttu-id="ff133-127">您可以指定介於 1 到 2,147,483,647 秒之間的任何 TTL 值。</span><span class="sxs-lookup"><span data-stu-id="ff133-127">You can specify any TTL value between 1 and 2,147,483,647 seconds.</span></span>

### <a name="wildcard-records"></a><span data-ttu-id="ff133-128">萬用字元記錄</span><span class="sxs-lookup"><span data-stu-id="ff133-128">Wildcard records</span></span>

<span data-ttu-id="ff133-129">Azure DNS 支援 [萬用字元記錄](https://en.wikipedia.org/wiki/Wildcard_DNS_record)。</span><span class="sxs-lookup"><span data-stu-id="ff133-129">Azure DNS supports [wildcard records](https://en.wikipedia.org/wiki/Wildcard_DNS_record).</span></span> <span data-ttu-id="ff133-130">萬用字元記錄會傳回具有相符名稱的任何查詢 (除非在非萬用字元記錄集內，還有更接近的相符項目)。</span><span class="sxs-lookup"><span data-stu-id="ff133-130">Wildcard records are returned in response to any query with a matching name (unless there is a closer match from a non-wildcard record set).</span></span> <span data-ttu-id="ff133-131">Azure DNS 支援 NS 和 SOA 以外的所有記錄類型的萬用字元記錄集。</span><span class="sxs-lookup"><span data-stu-id="ff133-131">Azure DNS supports wildcard record sets for all record types except NS and SOA.</span></span>

<span data-ttu-id="ff133-132">若要建立萬用字元記錄集，請使用記錄集名稱 '\*'。</span><span class="sxs-lookup"><span data-stu-id="ff133-132">To create a wildcard record set, use the record set name '\*'.</span></span> <span data-ttu-id="ff133-133">或者，也可以使用最左邊標籤是 '\*' 的名稱，例如 '\*.foo'。</span><span class="sxs-lookup"><span data-stu-id="ff133-133">Alternatively, you can also use a name with '\*' as its left-most label, for example, '\*.foo'.</span></span>

### <a name="cname-records"></a><span data-ttu-id="ff133-134">CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="ff133-134">CNAME records</span></span>

<span data-ttu-id="ff133-135">CNAME 記錄集不能與其他具有相同名稱的記錄集共存。</span><span class="sxs-lookup"><span data-stu-id="ff133-135">CNAME record sets cannot coexist with other record sets with the same name.</span></span> <span data-ttu-id="ff133-136">例如，您無法同時建立具有相對名稱 'www' 的 CNAME 記錄集和具有相對名稱 'www' 的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="ff133-136">For example, you cannot create a CNAME record set with the relative name 'www' and an A record with the relative name 'www' at the same time.</span></span>

<span data-ttu-id="ff133-137">因為區域頂點 (名稱 = '@') 一定會包含建立區域時所建立的 NS 和 SOA 記錄集，您無法在區域頂點建立 CNAME 記錄集。</span><span class="sxs-lookup"><span data-stu-id="ff133-137">Because the zone apex (name = '@') always contains the NS and SOA record sets that were created when the zone was created, you can't create a CNAME record set at the zone apex.</span></span>

<span data-ttu-id="ff133-138">這些條件約束源自於 DNS 標準，而不是 Azure DNS 的限制。</span><span class="sxs-lookup"><span data-stu-id="ff133-138">These constraints arise from the DNS standards and are not limitations of Azure DNS.</span></span>

### <a name="ns-records"></a><span data-ttu-id="ff133-139">NS 記錄</span><span class="sxs-lookup"><span data-stu-id="ff133-139">NS records</span></span>

<span data-ttu-id="ff133-140">區域頂點 (名稱 '@') 的 NS 記錄集會在每個 DNS 區域自動建立，並在刪除該區域時自動將其刪除 (無法個別刪除)。</span><span class="sxs-lookup"><span data-stu-id="ff133-140">The NS record set at the zone apex (name '@') is created automatically with each DNS zone, and is deleted automatically when the zone is deleted (it cannot be deleted separately).</span></span>

<span data-ttu-id="ff133-141">此記錄集包含指派給區域的 Azure DNS 名稱伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="ff133-141">This record set contains the names of the Azure DNS name servers assigned to the zone.</span></span> <span data-ttu-id="ff133-142">您可以將其他名稱伺服器新增至此 NS 記錄集，以支援使用多個 DNS 提供者的共同裝載網域。</span><span class="sxs-lookup"><span data-stu-id="ff133-142">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="ff133-143">您也可以修改此記錄集的 TTL 和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ff133-143">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="ff133-144">不過，您無法移除或修改預先填入的 Azure DNS 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff133-144">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span> 

<span data-ttu-id="ff133-145">請注意，這只適用於區域頂點的 NS 記錄集。</span><span class="sxs-lookup"><span data-stu-id="ff133-145">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="ff133-146">區域中的其他 NS 記錄集 (如用於委派子區域) 可以建立、修改和刪除，沒有條件約束。</span><span class="sxs-lookup"><span data-stu-id="ff133-146">Other NS record sets in your zone (as used to delegate child zones) can be created, modified and deleted without constraint.</span></span>

### <a name="soa-records"></a><span data-ttu-id="ff133-147">SOA 記錄</span><span class="sxs-lookup"><span data-stu-id="ff133-147">SOA records</span></span>

<span data-ttu-id="ff133-148">在每個區域頂點 (名稱 = '@') 會自動建立 SOA 記錄集，並在刪除該區域時自動將其刪除。</span><span class="sxs-lookup"><span data-stu-id="ff133-148">A SOA record set is created automatically at the apex of each zone (name = '@'), and is deleted automatically when the zone is deleted.</span></span>  <span data-ttu-id="ff133-149">無法個別建立或刪除 SOA 記錄。</span><span class="sxs-lookup"><span data-stu-id="ff133-149">SOA records cannot be created or deleted separately.</span></span>

<span data-ttu-id="ff133-150">可以修改 SOA 記錄除了 'Host' 屬性以外的所有屬性，因為依照預先設定，該屬性會參考 Azure DNS 所提供的主要名稱伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="ff133-150">You can modify all properties of the SOA record except for the 'host' property, which is pre-configured to refer to the primary name server name provided by Azure DNS.</span></span>

### <a name="spf-records"></a><span data-ttu-id="ff133-151">SPF 記錄</span><span class="sxs-lookup"><span data-stu-id="ff133-151">SPF records</span></span>

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a><span data-ttu-id="ff133-152">SRV 記錄</span><span class="sxs-lookup"><span data-stu-id="ff133-152">SRV records</span></span>

<span data-ttu-id="ff133-153">各種服務都會使用 [SRV 記錄](https://en.wikipedia.org/wiki/SRV_record)來指定伺服器位置。</span><span class="sxs-lookup"><span data-stu-id="ff133-153">[SRV records](https://en.wikipedia.org/wiki/SRV_record) are used by various services to specify server locations.</span></span> <span data-ttu-id="ff133-154">在 Azure DNS 中指定 SRV 記錄時︰</span><span class="sxs-lookup"><span data-stu-id="ff133-154">When specifying an SRV record in Azure DNS:</span></span>

* <span data-ttu-id="ff133-155">必須在記錄集名稱中包括 [服務] 和 [通訊協定]，並在其前方加上底線。</span><span class="sxs-lookup"><span data-stu-id="ff133-155">The *service* and *protocol* must be specified as part of the record set name, prefixed with underscores.</span></span>  <span data-ttu-id="ff133-156">例如，'\_sip.\_tcp.name'。</span><span class="sxs-lookup"><span data-stu-id="ff133-156">For example, '\_sip.\_tcp.name'.</span></span>  <span data-ttu-id="ff133-157">在區域頂點的記錄，則不需要在記錄名稱中指定 '@'，只要使用服務與通訊協定即可，例如 '\_sip.\_tcp'。</span><span class="sxs-lookup"><span data-stu-id="ff133-157">For a record at the zone apex, there is no need to specify '@' in the record name, simply use the service and protocol, for example '\_sip.\_tcp'.</span></span>
* <span data-ttu-id="ff133-158">系統已將 [優先順序]、[權數]、[連接埠] 和 [目標]，指定為記錄集內每筆記錄的參數。</span><span class="sxs-lookup"><span data-stu-id="ff133-158">The *priority*, *weight*, *port*, and *target* are specified as parameters of each record in the record set.</span></span>

### <a name="txt-records"></a><span data-ttu-id="ff133-159">TXT 記錄</span><span class="sxs-lookup"><span data-stu-id="ff133-159">TXT records</span></span>

<span data-ttu-id="ff133-160">TXT 記錄是用來將網域名稱對應到任意文字字串。</span><span class="sxs-lookup"><span data-stu-id="ff133-160">TXT records are used to map domain names to arbitrary text strings.</span></span> <span data-ttu-id="ff133-161">用於多個應用程式，特別是與電子郵件設定相關的應用程式，例如[寄件者原則架構 (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework)和 [DomainKeys Identified Mail (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail)。</span><span class="sxs-lookup"><span data-stu-id="ff133-161">They are used in multiple applications, in particular related to email configuration, such as the [Sender Policy Framework (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) and [DomainKeys Identified Mail (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).</span></span>

<span data-ttu-id="ff133-162">DNS 標準允許單一 TXT 記錄包含多個字串，每個長度最多可達 254 個字元。</span><span class="sxs-lookup"><span data-stu-id="ff133-162">The DNS standards permit a single TXT record to contain multiple strings, each of which may be up to 254 characters in length.</span></span> <span data-ttu-id="ff133-163">使用多個字串時，用戶端會將這些字串連接並視為單一字串。</span><span class="sxs-lookup"><span data-stu-id="ff133-163">Where multiple strings are used, they are concatenated by clients and treated as a single string.</span></span>

<span data-ttu-id="ff133-164">在呼叫 Azure DNS REST API 時，您必須分別指定每個 TXT 字串。</span><span class="sxs-lookup"><span data-stu-id="ff133-164">When calling the Azure DNS REST API, you need to specify each TXT string separately.</span></span>  <span data-ttu-id="ff133-165">當使用 Azure 入口網站、PowerShell 或 CLI 介面時，您應該為每筆記錄指定單一字串，如有需要，字串將自動分段成 254 個字元的區段。</span><span class="sxs-lookup"><span data-stu-id="ff133-165">When using the Azure portal, PowerShell or CLI interfaces you should specify a single string per record, which is automatically divided into 254-character segments if necessary.</span></span>

<span data-ttu-id="ff133-166">DNS 記錄中的多個字串，不應與 TXT 記錄集中的多個 TXT 記錄相混淆。</span><span class="sxs-lookup"><span data-stu-id="ff133-166">The multiple strings in a DNS record should not be confused with the multiple TXT records in a TXT record set.</span></span>  <span data-ttu-id="ff133-167">TXT 記錄集可以包含多個記錄，「每一個」記錄可以包含多個字串。</span><span class="sxs-lookup"><span data-stu-id="ff133-167">A TXT record set can contain multiple records, *each of which* can contain multiple strings.</span></span>  <span data-ttu-id="ff133-168">Azure DNS 支援每個 TXT 記錄集中的 字串總長度上限為 1024 個字元 (所有記錄的總和)。</span><span class="sxs-lookup"><span data-stu-id="ff133-168">Azure DNS supports a total string length of up to 1024 characters in each TXT record set (across all records combined).</span></span>

## <a name="tags-and-metadata"></a><span data-ttu-id="ff133-169">標記和中繼資料</span><span class="sxs-lookup"><span data-stu-id="ff133-169">Tags and metadata</span></span>

### <a name="tags"></a><span data-ttu-id="ff133-170">標記</span><span class="sxs-lookup"><span data-stu-id="ff133-170">Tags</span></span>

<span data-ttu-id="ff133-171">標記是名稱-值組的清單，由 Azure Resource Manager 用來標示資源。</span><span class="sxs-lookup"><span data-stu-id="ff133-171">Tags are a list of name-value pairs and are used by Azure Resource Manager to label resources.</span></span>  <span data-ttu-id="ff133-172">Azure Resource Manager 會使用標記來啟用 Azure 帳單篩選過的檢視，也可讓您設定標記需要的原則。</span><span class="sxs-lookup"><span data-stu-id="ff133-172">Azure Resource Manager uses tags to enable filtered views of your Azure bill, and also enables you to set a policy on which tags are required.</span></span> <span data-ttu-id="ff133-173">如需標記的詳細資訊，請參閱 [使用標記來組織您的 Azure 資源](../azure-resource-manager/resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="ff133-173">For more information about tags, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>

<span data-ttu-id="ff133-174">Azure DNS 支援在 DNS 區域資源上，使用 Azure Resource Manager 標記。</span><span class="sxs-lookup"><span data-stu-id="ff133-174">Azure DNS supports using Azure Resource Manager tags on DNS zone resources.</span></span>  <span data-ttu-id="ff133-175">不支援在 DNS 記錄集上使用標記，不過，支援在 DNS 記錄集上使用「中繼資料」作為替代，如下所述。</span><span class="sxs-lookup"><span data-stu-id="ff133-175">It does not support tags on DNS record sets, although as an alternative 'metadata' is supported on DNS record sets as explained below.</span></span>

### <a name="metadata"></a><span data-ttu-id="ff133-176">中繼資料</span><span class="sxs-lookup"><span data-stu-id="ff133-176">Metadata</span></span>

<span data-ttu-id="ff133-177">Azure DNS 支援使用 '中繼資料' 來替代記錄集標記，用以標註記錄集。</span><span class="sxs-lookup"><span data-stu-id="ff133-177">As an alternative to record set tags, Azure DNS supports annotating record sets using 'metadata'.</span></span>  <span data-ttu-id="ff133-178">類似於標記，中繼資料可讓您建立名稱-值組與每個記錄集之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="ff133-178">Similar to tags, metadata enables you to associate name-value pairs with each record set.</span></span>  <span data-ttu-id="ff133-179">這非常有用，例如，可用以記錄每個記錄集的目的。</span><span class="sxs-lookup"><span data-stu-id="ff133-179">This can be useful, for example to record the purpose of each record set.</span></span>  <span data-ttu-id="ff133-180">與標記不同的是，中繼資料無法用來提供 Azure 帳單篩選過的檢視，也無法在 Azure Resource Manager 原則中指定。</span><span class="sxs-lookup"><span data-stu-id="ff133-180">Unlike tags, metadata cannot be used to provide a filtered view of your Azure bill and cannot be specified in an Azure Resource Manager policy.</span></span>

## <a name="etags"></a><span data-ttu-id="ff133-181">Etag</span><span class="sxs-lookup"><span data-stu-id="ff133-181">Etags</span></span>

<span data-ttu-id="ff133-182">假設有兩個人或兩個處理序同時嘗試修改 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ff133-182">Suppose two people or two processes try to modify a DNS record at the same time.</span></span> <span data-ttu-id="ff133-183">何者獲勝？</span><span class="sxs-lookup"><span data-stu-id="ff133-183">Which one wins?</span></span> <span data-ttu-id="ff133-184">獲勝者知道他已覆寫另一人所做的變更嗎？</span><span class="sxs-lookup"><span data-stu-id="ff133-184">And does the winner know that they've overwritten changes created by someone else?</span></span>

<span data-ttu-id="ff133-185">Azure DNS 使用 Etag 以安全地處理相同資源的並行變更。</span><span class="sxs-lookup"><span data-stu-id="ff133-185">Azure DNS uses Etags to handle concurrent changes to the same resource safely.</span></span> <span data-ttu-id="ff133-186">Etag 和 [Azure Resource Manager「標籤」](#tags)分開。</span><span class="sxs-lookup"><span data-stu-id="ff133-186">Etags are separate from [Azure Resource Manager 'Tags'](#tags).</span></span> <span data-ttu-id="ff133-187">每個 DNS 資源 (區域或記錄集) 都有一個相關聯的 Etag。</span><span class="sxs-lookup"><span data-stu-id="ff133-187">Each DNS resource (zone or record set) has an Etag associated with it.</span></span> <span data-ttu-id="ff133-188">每當擷取資源時，也會擷取其 Etag。</span><span class="sxs-lookup"><span data-stu-id="ff133-188">Whenever a resource is retrieved, its Etag is also retrieved.</span></span> <span data-ttu-id="ff133-189">更新資源時，您可以選擇傳回 Etag，讓 Azure DNS 可以確認伺服器上的 Etag 相符。</span><span class="sxs-lookup"><span data-stu-id="ff133-189">When updating a resource, you can choose to pass back the Etag so Azure DNS can verify that the Etag on the server matches.</span></span> <span data-ttu-id="ff133-190">因為每次更新資源都會重新產生 Etag，Etag 不符就表示發生並行變更。</span><span class="sxs-lookup"><span data-stu-id="ff133-190">Since each update to a resource results in the Etag being regenerated, an Etag mismatch indicates a concurrent change has occurred.</span></span> <span data-ttu-id="ff133-191">建立新的資源時也可以使用 Etag，以確保該資源尚不存在。</span><span class="sxs-lookup"><span data-stu-id="ff133-191">Etags can also be used when creating a new resource to ensure that the resource does not already exist.</span></span>

<span data-ttu-id="ff133-192">根據預設，Azure DNS PowerShell 會使用 Etag 來禁止對區域和記錄集進行並行變更。</span><span class="sxs-lookup"><span data-stu-id="ff133-192">By default, Azure DNS PowerShell uses Etags to block concurrent changes to zones and record sets.</span></span> <span data-ttu-id="ff133-193">選擇性的 *-Overwrite* 參數可以用來停用 Etag 檢查，在此情況下，會覆寫任何已發生的並行變更。</span><span class="sxs-lookup"><span data-stu-id="ff133-193">The optional *-Overwrite* switch can be used to suppress Etag checks, in which case any concurrent changes that have occurred are overwritten.</span></span>

<span data-ttu-id="ff133-194">在 Azure DNS REST API 層級上是使用 HTTP 標頭指定 Etag。</span><span class="sxs-lookup"><span data-stu-id="ff133-194">At the level of the Azure DNS REST API, Etags are specified using HTTP headers.</span></span>  <span data-ttu-id="ff133-195">下表提供它們的行為：</span><span class="sxs-lookup"><span data-stu-id="ff133-195">Their behavior is given in the following table:</span></span>

| <span data-ttu-id="ff133-196">頁首</span><span class="sxs-lookup"><span data-stu-id="ff133-196">Header</span></span> | <span data-ttu-id="ff133-197">行為</span><span class="sxs-lookup"><span data-stu-id="ff133-197">Behavior</span></span> |
| --- | --- |
| <span data-ttu-id="ff133-198">None</span><span class="sxs-lookup"><span data-stu-id="ff133-198">None</span></span> |<span data-ttu-id="ff133-199">PUT 一定成功 (沒有 Etag 檢查)</span><span class="sxs-lookup"><span data-stu-id="ff133-199">PUT always succeeds (no Etag checks)</span></span> |
| <span data-ttu-id="ff133-200">If-match <etag></span><span class="sxs-lookup"><span data-stu-id="ff133-200">If-match <etag></span></span> |<span data-ttu-id="ff133-201">唯有當資源存在且 Etag 符合時，PUT 才會成功</span><span class="sxs-lookup"><span data-stu-id="ff133-201">PUT only succeeds if resource exists and Etag matches</span></span> |
| <span data-ttu-id="ff133-202">If-match *</span><span class="sxs-lookup"><span data-stu-id="ff133-202">If-match *</span></span> |<span data-ttu-id="ff133-203">唯有當資源存在時，PUT 才會成功</span><span class="sxs-lookup"><span data-stu-id="ff133-203">PUT only succeeds if resource exists</span></span> |
| <span data-ttu-id="ff133-204">If-none-match *</span><span class="sxs-lookup"><span data-stu-id="ff133-204">If-none-match *</span></span> |<span data-ttu-id="ff133-205">唯有當資源不存在時，PUT 才會成功</span><span class="sxs-lookup"><span data-stu-id="ff133-205">PUT only succeeds if resource does not exist</span></span> |


## <a name="limits"></a><span data-ttu-id="ff133-206">限制</span><span class="sxs-lookup"><span data-stu-id="ff133-206">Limits</span></span>

<span data-ttu-id="ff133-207">使用 Azure DNS 時，會適用下列的預設限制︰</span><span class="sxs-lookup"><span data-stu-id="ff133-207">The following default limits apply when using Azure DNS:</span></span>

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a><span data-ttu-id="ff133-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff133-208">Next steps</span></span>

* <span data-ttu-id="ff133-209">若要開始使用 Azure DNS，請學習如何[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)和[建立 DNS 記錄](dns-getstarted-create-recordset-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ff133-209">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="ff133-210">若要移轉現有的 DNS 區域，請學習如何[匯入和匯出 DNS 區域檔案](dns-import-export.md)。</span><span class="sxs-lookup"><span data-stu-id="ff133-210">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>
