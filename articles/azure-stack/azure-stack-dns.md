---
title: "在 Azure 堆疊 aaaDNS |Microsoft 文件"
description: "Azure Stack 中的 DNS"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/27/2017
ms.author: victorh
ms.openlocfilehash: 8620178833ac29e9653cce332b7c5d89bbdea0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dns-in-azure-stack"></a><span data-ttu-id="cce71-103">Azure Stack 中的 DNS</span><span class="sxs-lookup"><span data-stu-id="cce71-103">DNS in Azure Stack</span></span>
<span data-ttu-id="cce71-104">Azure 堆疊包含 hello 下列 DNS 的功能：</span><span class="sxs-lookup"><span data-stu-id="cce71-104">Azure Stack includes hello following DNS features:</span></span>
* <span data-ttu-id="cce71-105">支援 DNS 主機名稱解析</span><span class="sxs-lookup"><span data-stu-id="cce71-105">Support for DNS hostname resolution</span></span>
* <span data-ttu-id="cce71-106">使用 API 建立和管理 DNS 區域和記錄</span><span class="sxs-lookup"><span data-stu-id="cce71-106">Create and manage DNS zones and records using API</span></span>

## <a name="support-for-dns-hostname-resolution"></a><span data-ttu-id="cce71-107">支援 DNS 主機名稱解析</span><span class="sxs-lookup"><span data-stu-id="cce71-107">Support for DNS hostname resolution</span></span>
<span data-ttu-id="cce71-108">您可以指定建立對應的公用 IP 資源的 DNS 網域名稱標籤*domainnamelabel.location*。 cloudapp.azurestack.external toohello 公用 IP 位址在 hello Azure 堆疊中的受管理 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cce71-108">You can specify a DNS domain name label for a public IP resource, which creates a mapping for *domainnamelabel.location*.cloudapp.azurestack.external toohello public IP address in hello Azure Stack managed DNS servers.</span></span>  

<span data-ttu-id="cce71-109">例如，如果您建立的公用 IP 資源**contoso** hello 本機 Azure 堆疊位置中的網域名稱標籤，為 hello 完整的網域名稱 (FQDN) **contoso.local.cloudapp.azurestack.external** toohello 公用 IP 位址 hello 資源的解析。</span><span class="sxs-lookup"><span data-stu-id="cce71-109">For example, if you create a public IP resource with **contoso** as a domain name label in hello Local Azure Stack location, hello fully qualified domain name (FQDN) **contoso.local.cloudapp.azurestack.external** resolves toohello public IP address of hello resource.</span></span> <span data-ttu-id="cce71-110">您可以使用這個 FQDN toocreate 自訂網域指向 Azure 堆疊中 toohello 公用 IP 位址的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="cce71-110">You can use this FQDN toocreate a custom domain CNAME record that points toohello public IP address in Azure Stack.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cce71-111">每個所建立的網域名稱標籤，皆必須具有唯一的 Azure Stack 位置。</span><span class="sxs-lookup"><span data-stu-id="cce71-111">Each domain name label created must be unique within its Azure Stack location.</span></span>

<span data-ttu-id="cce71-112">如果您建立 hello 公用 IP 位址使用 hello 入口網站時，它看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="cce71-112">If you create hello public IP address using hello portal, it looks like this:</span></span>

![建立公用 IP 位址](media/azure-stack-whats-new-dns/image01.png)

<span data-ttu-id="cce71-114">此設定很有用，如果您想 tooassociate 公用 IP 位址與負載平衡的資源。</span><span class="sxs-lookup"><span data-stu-id="cce71-114">This configuration is useful if you want tooassociate a public IP address with a load-balanced resource.</span></span> <span data-ttu-id="cce71-115">例如，您將可能有負載平衡器處理來自 Web 應用程式的要求。</span><span class="sxs-lookup"><span data-stu-id="cce71-115">For example, you might have a load balancer processing requests from a web application.</span></span> <span data-ttu-id="cce71-116">後方 hello 負載平衡器是一或多個虛擬機器的網站。</span><span class="sxs-lookup"><span data-stu-id="cce71-116">Behind hello load balancer is a web site located  on one or more virtual machines.</span></span> <span data-ttu-id="cce71-117">現在您可以存取 hello 負載平衡的網站的 DNS 名稱，而非 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="cce71-117">Now you can access hello load-balanced web site by a DNS name, rather than by an IP address.</span></span>

## <a name="create-and-manage-dns-zones-and-records-using-api"></a><span data-ttu-id="cce71-118">使用 API 建立和管理 DNS 區域和記錄</span><span class="sxs-lookup"><span data-stu-id="cce71-118">Create and manage DNS zones and records using API</span></span>
<span data-ttu-id="cce71-119">您可以建立和管理 DNS 區域和 Azure Stack 中的記錄。</span><span class="sxs-lookup"><span data-stu-id="cce71-119">You can create and manage DNS zones and records in Azure Stack.</span></span>  

<span data-ttu-id="cce71-120">Azure Stack 提供就像 Azure 的 DNS 服務，使用與 Azure DNS API 一致的 API。</span><span class="sxs-lookup"><span data-stu-id="cce71-120">Azure Stack provides a DNS service like Azure’s, using APIs that are consistent with Azure’s DNS APIs.</span></span>  <span data-ttu-id="cce71-121">裝載 Azure 堆疊 DNS 中的網域，您可以管理您的 DNS 記錄，以 hello 相同的認證、 Api、 工具、 帳單和支援與其他 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="cce71-121">By hosting your domains in Azure Stack DNS, you can manage your DNS records with hello same credentials, APIs, tools, billing, and support as your other Azure services.</span></span> 

<span data-ttu-id="cce71-122">明顯原因是更簡潔比 Azure 的 hello Azure 堆疊 DNS 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="cce71-122">For obvious reasons, hello Azure Stack DNS infrastructure is more compact than Azure's.</span></span> <span data-ttu-id="cce71-123">因此，hello 範圍、 小數位數和效能取決於 hello Azure 堆疊部署和部署的 hello 環境的 hello 小數位數。</span><span class="sxs-lookup"><span data-stu-id="cce71-123">Thus, hello scope, scale, and performance depend on hello scale of hello Azure Stack deployment and hello environment where it is deployed.</span></span>  <span data-ttu-id="cce71-124">因此，之類的效能、 可用性、 全域發佈和高可用性 (HA) 可能會與部署 toodeployment 有所不同。</span><span class="sxs-lookup"><span data-stu-id="cce71-124">So, things like performance, availability, global distribution, and High-Availability (HA) can vary from deployment toodeployment.</span></span>

## <a name="comparison-with-azure-dns"></a><span data-ttu-id="cce71-125">與 Azure DNS 比較</span><span class="sxs-lookup"><span data-stu-id="cce71-125">Comparison with Azure DNS</span></span>
<span data-ttu-id="cce71-126">Azure 堆疊中的 DNS 是類似 tooDNS 在 Azure 中，有兩種主要的例外：</span><span class="sxs-lookup"><span data-stu-id="cce71-126">DNS in Azure Stack is similar tooDNS in Azure, with two major exceptions:</span></span>
* <span data-ttu-id="cce71-127">**不支援 AAAA 記錄**</span><span class="sxs-lookup"><span data-stu-id="cce71-127">**It does not support AAAA records**</span></span>

    <span data-ttu-id="cce71-128">Azure Stack「不」支援 AAAA 記錄，因為 Azure Stack 並不支援 IPv6 位址。</span><span class="sxs-lookup"><span data-stu-id="cce71-128">Azure Stack does NOT support AAAA records because Azure Stack does not support IPv6 addresses.</span></span>  <span data-ttu-id="cce71-129">這是 Azure 和 Azure Stack DNS 之間的主要差異。</span><span class="sxs-lookup"><span data-stu-id="cce71-129">This is a key difference between DNS in Azure and Azure Stack.</span></span>
* <span data-ttu-id="cce71-130">**不是多租用戶**</span><span class="sxs-lookup"><span data-stu-id="cce71-130">**It is not multi-tenant**</span></span>

    <span data-ttu-id="cce71-131">不同於 Azure hello Azure 堆疊中的 DNS 服務不是多租用戶。</span><span class="sxs-lookup"><span data-stu-id="cce71-131">Unlike Azure, hello DNS Service in Azure Stack is not multi-tenant.</span></span> <span data-ttu-id="cce71-132">讓每個租用戶無法建立 hello 相同 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="cce71-132">So each tenant cannot create hello same DNS zone.</span></span> <span data-ttu-id="cce71-133">只有 hello 嘗試 toocreate hello 區域的第一個訂閱成功，及後續的要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="cce71-133">Only hello first subscription that attempts toocreate hello zone succeeds, and subsequent requests fail.</span></span>  <span data-ttu-id="cce71-134">這是已知問題，也是 Azure 和 Azure Stack DNS 之間的主要差異。</span><span class="sxs-lookup"><span data-stu-id="cce71-134">It is a known issue, and a key difference between Azure and Azure Stack DNS.</span></span> <span data-ttu-id="cce71-135">此問題將在未來版本中解決。</span><span class="sxs-lookup"><span data-stu-id="cce71-135">This issue will be resolved in a future release.</span></span>

<span data-ttu-id="cce71-136">此外，Azure Stack DNS 如何實作標記、中繼資料、Etag 和限制皆有細微差異。</span><span class="sxs-lookup"><span data-stu-id="cce71-136">In addition, there are some minor differences in how Azure Stack DNS implements Tags, Metadata, Etags, and Limits.</span></span>

<span data-ttu-id="cce71-137">hello 下列資訊適用於特別 tooAzure 堆疊 DNS 並稍有不同 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="cce71-137">hello following information applies specifically tooAzure Stack DNS and varies slightly from Azure DNS.</span></span> <span data-ttu-id="cce71-138">toolearn 進一步了解 Azure DNS，請參閱[DNS 區域，以及記錄](../dns/dns-zones-records.md)hello Microsoft Azure 文件站台。</span><span class="sxs-lookup"><span data-stu-id="cce71-138">toolearn more about Azure DNS, see [DNS zones and records](../dns/dns-zones-records.md) at hello Microsoft Azure documentation site.</span></span>

### <a name="tags-metadata-and-etags"></a><span data-ttu-id="cce71-139">標記、中繼資料和 Etag</span><span class="sxs-lookup"><span data-stu-id="cce71-139">Tags, metadata, and Etags</span></span>

<span data-ttu-id="cce71-140">**標記**</span><span class="sxs-lookup"><span data-stu-id="cce71-140">**Tags**</span></span>

<span data-ttu-id="cce71-141">Azure Stack DNS 支援在 DNS 區域資源上，使用 Azure Resource Manager 標記。</span><span class="sxs-lookup"><span data-stu-id="cce71-141">Azure Stack DNS supports using Azure Resource Manager tags on DNS zone resources.</span></span> <span data-ttu-id="cce71-142">不支援在 DNS 記錄集上使用標記，不過，支援在 DNS 記錄集上使用「中繼資料」作為替代，接下來會詳述。</span><span class="sxs-lookup"><span data-stu-id="cce71-142">It does not support tags on DNS record sets, although as an alternative 'metadata' is supported on DNS record sets as explained next.</span></span>

<span data-ttu-id="cce71-143">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="cce71-143">**Metadata**</span></span>

<span data-ttu-id="cce71-144">做為替代的 toorecord 集標記，Azure 堆疊 DNS 支援註釋使用 'metadata' 的資料錄集。</span><span class="sxs-lookup"><span data-stu-id="cce71-144">As an alternative toorecord set tags, Azure Stack DNS supports annotating record sets using 'metadata'.</span></span> <span data-ttu-id="cce71-145">類似 tootags，中繼資料可讓您 tooassociate 名稱 / 值組，而且每個資料錄集。</span><span class="sxs-lookup"><span data-stu-id="cce71-145">Similar tootags, metadata enables you tooassociate name-value pairs with each record set.</span></span> <span data-ttu-id="cce71-146">比方說，這可以是很有用的 toorecord hello 目的每個資料錄集。</span><span class="sxs-lookup"><span data-stu-id="cce71-146">For example, this can be useful toorecord hello purpose of each record set.</span></span> <span data-ttu-id="cce71-147">與標記不同中繼資料無法使用的 tooprovide Azure 帳單的篩選的檢視，而不指定 Azure Resource Manager 原則中。</span><span class="sxs-lookup"><span data-stu-id="cce71-147">Unlike tags, metadata cannot be used tooprovide a filtered view of your Azure bill and cannot be specified in an Azure Resource Manager policy.</span></span>

<span data-ttu-id="cce71-148">**Etag**</span><span class="sxs-lookup"><span data-stu-id="cce71-148">**Etags**</span></span>

<span data-ttu-id="cce71-149">假設兩位或兩個處理序嘗試 toomodify DNS 記錄 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="cce71-149">Suppose two people or two processes try toomodify a DNS record at hello same time.</span></span> <span data-ttu-id="cce71-150">何者獲勝？</span><span class="sxs-lookup"><span data-stu-id="cce71-150">Which one wins?</span></span> <span data-ttu-id="cce71-151">和 hello 成功者知道他們已經覆寫其他人建立的變更嗎？</span><span class="sxs-lookup"><span data-stu-id="cce71-151">And does hello winner know that they've overwritten changes created by someone else?</span></span>

<span data-ttu-id="cce71-152">Azure 的堆疊 DNS 會使用 Etag toohandle 並行的變更 toohello 相同資源安全。</span><span class="sxs-lookup"><span data-stu-id="cce71-152">Azure Stack DNS uses Etags toohandle concurrent changes toohello same resource safely.</span></span> <span data-ttu-id="cce71-153">Etag 和 Azure Resource Manager「標籤」分開。</span><span class="sxs-lookup"><span data-stu-id="cce71-153">Etags are separate from Azure Resource Manager 'Tags'.</span></span> <span data-ttu-id="cce71-154">每個 DNS 資源 (區域或記錄集) 都有一個相關聯的 Etag。</span><span class="sxs-lookup"><span data-stu-id="cce71-154">Each DNS resource (zone or record set) has an Etag associated with it.</span></span> <span data-ttu-id="cce71-155">每當擷取資源時，也會擷取其 Etag。</span><span class="sxs-lookup"><span data-stu-id="cce71-155">Whenever a resource is retrieved, its Etag is also retrieved.</span></span> <span data-ttu-id="cce71-156">在更新資源，您可以選擇 toopass 回 hello Etag，讓 Azure 堆疊 DNS 可以確認該 hello Etag hello 伺服器比對。</span><span class="sxs-lookup"><span data-stu-id="cce71-156">When updating a resource, you can choose toopass back hello Etag so Azure Stack DNS can verify that hello Etag on hello server matches.</span></span> <span data-ttu-id="cce71-157">因為每個更新 tooa 資源產生 hello 正在重新產生的 Etag，Etag 不符表示已發生並行的變更。</span><span class="sxs-lookup"><span data-stu-id="cce71-157">Since each update tooa resource results in hello Etag being regenerated, an Etag mismatch indicates a concurrent change has occurred.</span></span> <span data-ttu-id="cce71-158">建立新的資源 tooensure hello 資源已經存在時，也可以使用 Etag。</span><span class="sxs-lookup"><span data-stu-id="cce71-158">Etags can also be used when creating a new resource tooensure that hello resource does not already exist.</span></span>

<span data-ttu-id="cce71-159">根據預設，Azure 堆疊 DNS PowerShell 會使用 Etag tooblock 並行的變更 toozones 資料錄集。</span><span class="sxs-lookup"><span data-stu-id="cce71-159">By default, Azure Stack DNS PowerShell uses Etags tooblock concurrent changes toozones and record sets.</span></span> <span data-ttu-id="cce71-160">選擇性的 hello *-覆寫*參數可以是使用的 toosuppress Etag 檢查，在此情況下任何並行發生的變更會覆寫。</span><span class="sxs-lookup"><span data-stu-id="cce71-160">hello optional *-Overwrite* switch can be used toosuppress Etag checks, in which case any concurrent changes that have occurred are overwritten.</span></span>

<span data-ttu-id="cce71-161">在 hello 的 hello Azure 堆疊 DNS REST API 層級的 Etag 會使用 HTTP 標頭所指定的。</span><span class="sxs-lookup"><span data-stu-id="cce71-161">At hello level of hello Azure Stack DNS REST API, Etags are specified using HTTP headers.</span></span> <span data-ttu-id="cce71-162">下表中的 hello 中提供它們的行為：</span><span class="sxs-lookup"><span data-stu-id="cce71-162">Their behavior is given in hello following table:</span></span>

| <span data-ttu-id="cce71-163">標頭</span><span class="sxs-lookup"><span data-stu-id="cce71-163">Header</span></span> | <span data-ttu-id="cce71-164">行為</span><span class="sxs-lookup"><span data-stu-id="cce71-164">Behavior</span></span>|
|--------|---------|
| <span data-ttu-id="cce71-165">None</span><span class="sxs-lookup"><span data-stu-id="cce71-165">None</span></span>   | <span data-ttu-id="cce71-166">PUT 一定成功 (沒有 Etag 檢查)</span><span class="sxs-lookup"><span data-stu-id="cce71-166">PUT always succeeds (no Etag checks)</span></span>|
| <span data-ttu-id="cce71-167">If-match</span><span class="sxs-lookup"><span data-stu-id="cce71-167">If-match</span></span>| <span data-ttu-id="cce71-168">唯有當資源存在且 Etag 符合時，PUT 才會成功</span><span class="sxs-lookup"><span data-stu-id="cce71-168">PUT only succeeds if resource exists and Etag matches</span></span>|
| <span data-ttu-id="cce71-169">If-match *</span><span class="sxs-lookup"><span data-stu-id="cce71-169">If-match *</span></span>| <span data-ttu-id="cce71-170">唯有當資源存在時，PUT 才會成功</span><span class="sxs-lookup"><span data-stu-id="cce71-170">PUT only succeeds if resource exists</span></span>|
| <span data-ttu-id="cce71-171">If-none-match *</span><span class="sxs-lookup"><span data-stu-id="cce71-171">If-none-match *</span></span>| <span data-ttu-id="cce71-172">唯有當資源不存在時，PUT 才會成功</span><span class="sxs-lookup"><span data-stu-id="cce71-172">PUT only succeeds if resource does not exist</span></span>|

### <a name="limits"></a><span data-ttu-id="cce71-173">限制</span><span class="sxs-lookup"><span data-stu-id="cce71-173">Limits</span></span>

<span data-ttu-id="cce71-174">使用 Azure 堆疊 DNS 時，適用下列預設限制 hello:</span><span class="sxs-lookup"><span data-stu-id="cce71-174">hello following default limits apply when using Azure Stack DNS:</span></span>

| <span data-ttu-id="cce71-175">資源</span><span class="sxs-lookup"><span data-stu-id="cce71-175">Resource</span></span>| <span data-ttu-id="cce71-176">預設限制</span><span class="sxs-lookup"><span data-stu-id="cce71-176">Default limit</span></span>|
|---------|--------------|
| <span data-ttu-id="cce71-177">每一訂用帳戶的區域</span><span class="sxs-lookup"><span data-stu-id="cce71-177">Zones per subscription</span></span>| <span data-ttu-id="cce71-178">100</span><span class="sxs-lookup"><span data-stu-id="cce71-178">100</span></span>|
| <span data-ttu-id="cce71-179">每一區域的記錄集</span><span class="sxs-lookup"><span data-stu-id="cce71-179">Record sets per zone</span></span>| <span data-ttu-id="cce71-180">5000</span><span class="sxs-lookup"><span data-stu-id="cce71-180">5000</span></span>|
| <span data-ttu-id="cce71-181">每一記錄集的記錄</span><span class="sxs-lookup"><span data-stu-id="cce71-181">Records per record set</span></span>| <span data-ttu-id="cce71-182">20</span><span class="sxs-lookup"><span data-stu-id="cce71-182">20</span></span>|

## <a name="next-steps"></a><span data-ttu-id="cce71-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cce71-183">Next steps</span></span>
[<span data-ttu-id="cce71-184">適用於 Azure Stack 的 iDNS 簡介</span><span class="sxs-lookup"><span data-stu-id="cce71-184">Introducing iDNS for Azure Stack</span></span>](azure-stack-understanding-dns.md)
