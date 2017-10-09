---
title: "aaaAzure DNS 疑難排解指南 |Microsoft 文件"
description: "Tootroubleshoot 常見方式，與 Azure DNS 問題"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="46afb-103">Azure DNS 疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="46afb-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="46afb-104">此頁面提供 Azure DNS 常見問題的疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="46afb-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="46afb-105">如果這些步驟未能解決問題，您也可以在 [MSDN 上的社群支援論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork)搜尋或張貼您的問題。</span><span class="sxs-lookup"><span data-stu-id="46afb-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="46afb-106">或者，開啟 Azure 支援要求。</span><span class="sxs-lookup"><span data-stu-id="46afb-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="46afb-107">我無法建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="46afb-107">I can't create a DNS zone</span></span>

<span data-ttu-id="46afb-108">tooresolve 常見的問題，再試一次一或多個步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="46afb-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="46afb-109">檢閱 hello Azure DNS 稽核記錄 toodetermine hello 失敗原因。</span><span class="sxs-lookup"><span data-stu-id="46afb-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="46afb-110">每個 DNS 區域名稱都必須是其資源群組中唯一的。</span><span class="sxs-lookup"><span data-stu-id="46afb-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="46afb-111">也就是兩個 DNS 區域與 hello 相同名稱不能共用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="46afb-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="46afb-112">請嘗試使用不同的區域名稱，或不同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="46afb-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="46afb-113">您可能會看到錯誤 「 您已達到或超過 hello 的訂用帳戶 {訂閱 id} 中的區域數目上限。 」</span><span class="sxs-lookup"><span data-stu-id="46afb-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="46afb-114">使用不同的 Azure 訂用帳戶、 刪除某些區域中，或連絡 Azure 支援 tooraise 訂用帳戶限制。</span><span class="sxs-lookup"><span data-stu-id="46afb-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="46afb-115">您可能會看到錯誤 「 hello 區域 '{區域 name}' 不可以使用。 」</span><span class="sxs-lookup"><span data-stu-id="46afb-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="46afb-116">此錯誤表示 Azure DNS 已無法 tooallocate 名稱伺服器的 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="46afb-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="46afb-117">請嘗試使用不同的區域名稱。</span><span class="sxs-lookup"><span data-stu-id="46afb-117">Try using a different zone name.</span></span> <span data-ttu-id="46afb-118">或者，如果您 hello 網域名稱擁有者，請連絡 Azure 支援人員可以配置名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="46afb-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="46afb-119">**建議的文件**</span><span class="sxs-lookup"><span data-stu-id="46afb-119">**Recommended documents**</span></span>

<span data-ttu-id="46afb-120">[DNS 區域和記錄](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="46afb-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="46afb-121">
[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="46afb-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="46afb-122">我無法建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="46afb-122">I can't create a DNS record</span></span>

<span data-ttu-id="46afb-123">tooresolve 常見的問題，再試一次一或多個步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="46afb-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="46afb-124">檢閱 hello Azure DNS 稽核記錄 toodetermine hello 失敗原因。</span><span class="sxs-lookup"><span data-stu-id="46afb-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="46afb-125">Hello 記錄集並已經存在嗎？</span><span class="sxs-lookup"><span data-stu-id="46afb-125">Does hello record set exist already?</span></span>  <span data-ttu-id="46afb-126">Azure DNS 管理使用記錄的記錄*設定*，這是相同的名稱和 hello 相同的 hello 之記錄的 hello 集合型別。</span><span class="sxs-lookup"><span data-stu-id="46afb-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="46afb-127">如果存在具有相同名稱，且已輸入的 hello 的記錄，然後 tooadd 這類的另一個記錄，您應該編輯現有記錄的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="46afb-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="46afb-128">您嘗試 toocreate 在 hello DNS 區域 apex (hello 'root' hello 區域的) 的記錄嗎？</span><span class="sxs-lookup"><span data-stu-id="46afb-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="46afb-129">如果所以 hello DNS 慣例是 toouse hello ' @' 字元做為 hello 記錄名稱。</span><span class="sxs-lookup"><span data-stu-id="46afb-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="46afb-130">也請注意 hello DNS 標準不會在 hello 區域的 apex 在允許的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="46afb-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="46afb-131">您有 CNAME 衝突嗎？</span><span class="sxs-lookup"><span data-stu-id="46afb-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="46afb-132">hello DNS 標準不允許為任何其他類型的記錄名稱相同的 hello 的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="46afb-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="46afb-133">如果您有現有的 CNAME，以相同名稱的不同型別失敗的 hello 建立記錄。</span><span class="sxs-lookup"><span data-stu-id="46afb-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="46afb-134">同樣地，建立 CNAME 失敗如果 hello 名稱符合不同類型的現有記錄。</span><span class="sxs-lookup"><span data-stu-id="46afb-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="46afb-135">藉由移除 hello 移除 hello 衝突，其他的記錄，或選擇不同的記錄名稱。</span><span class="sxs-lookup"><span data-stu-id="46afb-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="46afb-136">您已達到允許 DNS 區域中的記錄集的 hello 數目 hello 上限嗎？hello 目前的記錄集數而且 hello 資料錄集的最大數目會顯示 hello hello '屬性' hello 區域底下的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="46afb-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="46afb-137">如果您已達到此限制，然後刪除某些資料錄集或連絡 Azure 支援 tooraise 此區域的資料錄集限制，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="46afb-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="46afb-138">**建議的文件**</span><span class="sxs-lookup"><span data-stu-id="46afb-138">**Recommended documents**</span></span>

<span data-ttu-id="46afb-139">[DNS 區域和記錄](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="46afb-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="46afb-140">
[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="46afb-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="46afb-141">我無法解析我的 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="46afb-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="46afb-142">DNS 名稱解析是多步驟程序，可能會因為許多原因而失敗。</span><span class="sxs-lookup"><span data-stu-id="46afb-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="46afb-143">hello 下列步驟協助您調查 DNS 記錄裝載於 Azure DNS 區域中的 DNS 解析失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="46afb-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="46afb-144">確認 hello DNS 記錄已正確設定 Azure DNS 中。</span><span class="sxs-lookup"><span data-stu-id="46afb-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="46afb-145">檢閱 hello hello 檢查 hello 區域名稱、 記錄名稱，以及記錄類型正確的 Azure 入口網站中的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="46afb-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="46afb-146">確認 hello DNS 記錄正確解析 hello Azure DNS 名稱伺服器上。</span><span class="sxs-lookup"><span data-stu-id="46afb-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="46afb-147">如果您從本機電腦進行 DNS 查詢，您可能會看到快取不會反映 hello hello 名稱伺服器的目前狀態的結果。</span><span class="sxs-lookup"><span data-stu-id="46afb-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="46afb-148">此外，公司網路通常會使用 DNS proxy 伺服器，這可以防止 DNS 查詢正在導向 toospecific 名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="46afb-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="46afb-149">tooavoid 這些問題，使用網頁型名稱解析服務例如[digwebinterface](http://digwebinterface.com)。</span><span class="sxs-lookup"><span data-stu-id="46afb-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="46afb-150">為確定 toospecify hello 正確的名稱伺服器，您的 DNS 區域，hello Azure 入口網站中所示。</span><span class="sxs-lookup"><span data-stu-id="46afb-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="46afb-151">請檢查 hello DNS 名稱正確 （必須 toospecify hello 完整限定名稱，包括 hello 區域名稱），以及 hello 記錄類型正確</span><span class="sxs-lookup"><span data-stu-id="46afb-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="46afb-152">確認已正確設定該 hello DNS 網域名稱[委派 toohello Azure DNS 名稱伺服器](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="46afb-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="46afb-153">有[許多第三方網站可提供 DNS 委派驗證](https://www.bing.com/search?q=dns+check+tool)。</span><span class="sxs-lookup"><span data-stu-id="46afb-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="46afb-154">這項測試很*區域*委派測試，因此您應該只輸入 hello DNS 區域名稱，而不 hello 完整記錄名稱。</span><span class="sxs-lookup"><span data-stu-id="46afb-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="46afb-155">已完成上述 hello，您的 DNS 記錄應現在正確解析。</span><span class="sxs-lookup"><span data-stu-id="46afb-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="46afb-156">tooverify，您可以再次使用[digwebinterface](http://digwebinterface.com)，這次使用 hello 預設名稱的伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="46afb-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="46afb-157">**建議的文件**</span><span class="sxs-lookup"><span data-stu-id="46afb-157">**Recommended documents**</span></span>

[<span data-ttu-id="46afb-158">委派網域 tooAzure DNS</span><span class="sxs-lookup"><span data-stu-id="46afb-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="46afb-159">如何指定 hello 'service' 和 'protocol' SRV 記錄？</span><span class="sxs-lookup"><span data-stu-id="46afb-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="46afb-160">Azure DNS 管理 DNS 記錄，做為資料錄集 — 以相同的名稱和 hello 相同的 hello hello 記錄的集合型別。</span><span class="sxs-lookup"><span data-stu-id="46afb-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="46afb-161">SRV 記錄集，hello 'service' 和 'protocol' 需要 toobe hello 記錄集名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="46afb-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="46afb-162">hello SRV 指定其他參數 （'priority'、 'weight'、 'port' 和 'target'） 會分別 hello 記錄組中的每一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="46afb-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="46afb-163">例如，SRV 記錄名稱 (服務名稱 'sip'，通訊協定 'tcp')：</span><span class="sxs-lookup"><span data-stu-id="46afb-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="46afb-164">\_sip。\_tcp （建立之記錄集在 hello 區域的 apex）</span><span class="sxs-lookup"><span data-stu-id="46afb-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="46afb-165">\_sip.\_tcp.sipservice (建立名為 'sipservice' 的記錄集)</span><span class="sxs-lookup"><span data-stu-id="46afb-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="46afb-166">**建議的文件**</span><span class="sxs-lookup"><span data-stu-id="46afb-166">**Recommended documents**</span></span>

<span data-ttu-id="46afb-167">[DNS 區域和記錄](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="46afb-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="46afb-168">
[建立 DNS 資料錄集，並使用記錄 hello Azure 入口網站](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="46afb-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="46afb-169">
[SRV 記錄類型 (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="46afb-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="46afb-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46afb-170">Next steps</span></span>

* <span data-ttu-id="46afb-171">了解 [DNS 區域和記錄](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="46afb-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="46afb-172">使用 Azure DNS，toostart 深入了解如何太[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)和[建立 DNS 記錄](dns-getstarted-create-recordset-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="46afb-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="46afb-173">toomigrate 現有的 DNS 區域，深入了解如何太[匯入和匯出 DNS 區域檔案](dns-import-export.md)。</span><span class="sxs-lookup"><span data-stu-id="46afb-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

