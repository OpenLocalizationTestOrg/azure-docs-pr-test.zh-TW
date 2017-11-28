---
title: "Azure DNS 疑難排解指南 | Microsoft Docs"
description: "如何對使用 Azure DNS 的常見問題進行疑難排解"
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
ms.openlocfilehash: 1d9bb681a864bdc3e5a2f9c9a531d9566b16ada4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="59411-103">Azure DNS 疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="59411-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="59411-104">此頁面提供 Azure DNS 常見問題的疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="59411-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="59411-105">如果這些步驟未能解決問題，您也可以在 [MSDN 上的社群支援論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork)搜尋或張貼您的問題。</span><span class="sxs-lookup"><span data-stu-id="59411-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="59411-106">或者，開啟 Azure 支援要求。</span><span class="sxs-lookup"><span data-stu-id="59411-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="59411-107">我無法建立 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="59411-107">I can't create a DNS zone</span></span>

<span data-ttu-id="59411-108">若要解決常見的問題，請嘗試下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59411-108">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="59411-109">檢閱 Azure DNS 稽核記錄檔以判斷失敗原因。</span><span class="sxs-lookup"><span data-stu-id="59411-109">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="59411-110">每個 DNS 區域名稱都必須是其資源群組中唯一的。</span><span class="sxs-lookup"><span data-stu-id="59411-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="59411-111">也就是說，兩個名稱相同的 DNS 區域無法共用一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="59411-111">That is, two DNS zones with the same name cannot share a resource group.</span></span> <span data-ttu-id="59411-112">請嘗試使用不同的區域名稱，或不同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="59411-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="59411-113">您會看到「您已達到或超過訂用帳戶 {subscription id} 中的區域數目上限。」的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="59411-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="59411-114">請使用其他 Azure 訂用帳戶、刪除相同的區域或聯絡 Azure 支援中心以提高您的訂用帳戶限制。</span><span class="sxs-lookup"><span data-stu-id="59411-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span></span>
4.  <span data-ttu-id="59411-115">您會看到「區域 '{zone name}' 無法使用。」的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="59411-115">You may see an error "The zone '{zone name}' is not available."</span></span> <span data-ttu-id="59411-116">此錯誤表示 Azure DNS 無法為此 DNS 區域配置名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="59411-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span></span> <span data-ttu-id="59411-117">請嘗試使用不同的區域名稱。</span><span class="sxs-lookup"><span data-stu-id="59411-117">Try using a different zone name.</span></span> <span data-ttu-id="59411-118">或者，如果您是網域名稱擁有者，請連絡 Azure 支援中心，他們可以為您配置名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="59411-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="59411-119">**建議的文件**</span><span class="sxs-lookup"><span data-stu-id="59411-119">**Recommended documents**</span></span>

<span data-ttu-id="59411-120">[DNS 區域和記錄](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="59411-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="59411-121">
[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="59411-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="59411-122">我無法建立 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="59411-122">I can't create a DNS record</span></span>

<span data-ttu-id="59411-123">若要解決常見的問題，請嘗試下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59411-123">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="59411-124">檢閱 Azure DNS 稽核記錄檔以判斷失敗原因。</span><span class="sxs-lookup"><span data-stu-id="59411-124">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="59411-125">記錄集是否已經存在？</span><span class="sxs-lookup"><span data-stu-id="59411-125">Does the record set exist already?</span></span>  <span data-ttu-id="59411-126">Azure DNS 是使用記錄*集*管理記錄，記錄集是名稱與類型相同之記錄的集合。</span><span class="sxs-lookup"><span data-stu-id="59411-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span></span> <span data-ttu-id="59411-127">如果已經有名稱與類型相同的記錄存在，此時若要新增其他此類型記錄，您應該編輯現有的記錄集。</span><span class="sxs-lookup"><span data-stu-id="59411-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span></span>
3.  <span data-ttu-id="59411-128">您是否正嘗試在 DNS 區域頂點 (區域的 [根]) 建立記錄？</span><span class="sxs-lookup"><span data-stu-id="59411-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span></span> <span data-ttu-id="59411-129">如果是，DNS 慣例是使用 ‘@’ 字元做為記錄名稱。</span><span class="sxs-lookup"><span data-stu-id="59411-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span></span> <span data-ttu-id="59411-130">也請注意，DNS 標準不允許在區域頂點使用 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="59411-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span></span>
4.  <span data-ttu-id="59411-131">您有 CNAME 衝突嗎？</span><span class="sxs-lookup"><span data-stu-id="59411-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="59411-132">DNS 標準不允許 CNAME 記錄的名稱和任何其他類型記錄的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="59411-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span></span> <span data-ttu-id="59411-133">如果您有現有的 CNAME，建立不同類型但名稱相同的記錄將會失敗。</span><span class="sxs-lookup"><span data-stu-id="59411-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span></span>  <span data-ttu-id="59411-134">同樣地，如果名稱和不同類型的現有記錄相同，建立 CNAME 將會失敗。</span><span class="sxs-lookup"><span data-stu-id="59411-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span></span> <span data-ttu-id="59411-135">請透過移除其他記錄或選擇不同的記錄名稱來排除衝突。</span><span class="sxs-lookup"><span data-stu-id="59411-135">Remove the conflict by removing the other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="59411-136">您已達到 DNS 區域中允許的記錄集數目限制嗎？</span><span class="sxs-lookup"><span data-stu-id="59411-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span></span> <span data-ttu-id="59411-137">Azure 入口網站中，區域的 [內容] 底下會顯示目前的記錄集數目和記錄集數目上限。</span><span class="sxs-lookup"><span data-stu-id="59411-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span></span> <span data-ttu-id="59411-138">如果您已經達到此限制，請刪除部分記錄集或連絡 Azure 支援中心以提高您在此區域的記錄集上限，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="59411-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="59411-139">**建議的文件**</span><span class="sxs-lookup"><span data-stu-id="59411-139">**Recommended documents**</span></span>

<span data-ttu-id="59411-140">[DNS 區域和記錄](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="59411-140">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="59411-141">
[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="59411-141">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="59411-142">我無法解析我的 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="59411-142">I can't resolve my DNS record</span></span>

<span data-ttu-id="59411-143">DNS 名稱解析是多步驟程序，可能會因為許多原因而失敗。</span><span class="sxs-lookup"><span data-stu-id="59411-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="59411-144">下面的步驟將可協助您調查 Azure DNS 中裝載之區域中 DNS 記錄的 DNS 解析為何會失敗。</span><span class="sxs-lookup"><span data-stu-id="59411-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="59411-145">確認已經在 Azure DNS 中正確設定 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="59411-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="59411-146">在 Azure 入口網站中檢閱 DNS 記錄、檢查區域名稱、記錄名稱及記錄類型是否正確。</span><span class="sxs-lookup"><span data-stu-id="59411-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="59411-147">確認 DNS 記錄已在 Azure DNS 名稱伺服器上正確解析。</span><span class="sxs-lookup"><span data-stu-id="59411-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span></span>
    - <span data-ttu-id="59411-148">如果您從本機電腦執行 DNS 查詢，您可能會看到沒有反映名稱伺服器目前狀態的快取結果。</span><span class="sxs-lookup"><span data-stu-id="59411-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span></span>  <span data-ttu-id="59411-149">而且，公司網路通常是使用會防止 DNS 查詢被導向到特定名稱伺服器的 DNS Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="59411-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span></span>  <span data-ttu-id="59411-150">為避免發生這些問題，請使用網路型名稱解析服務，例如 [digwebinterface](http://digwebinterface.com)。</span><span class="sxs-lookup"><span data-stu-id="59411-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="59411-151">請務必為您的 DNS 區域指定正確的名稱伺服器，如 Azure 入口網站中所顯示的。</span><span class="sxs-lookup"><span data-stu-id="59411-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span></span>
    - <span data-ttu-id="59411-152">檢查 DNS 名稱是否正確 (您將必須指定包括區域名稱在內的完整名稱) 和記錄類型是否正確</span><span class="sxs-lookup"><span data-stu-id="59411-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span></span>
3.  <span data-ttu-id="59411-153">確認 DNS 網域名稱已經正確[委派給 Azure DNS 名稱伺服器](dns-domain-delegation.md)。</span><span class="sxs-lookup"><span data-stu-id="59411-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="59411-154">有[許多第三方網站可提供 DNS 委派驗證](https://www.bing.com/search?q=dns+check+tool)。</span><span class="sxs-lookup"><span data-stu-id="59411-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="59411-155">這是一個*區域*委派測試，所以您應該只輸入 DNS 區域名稱，而不是完整的記錄名稱。</span><span class="sxs-lookup"><span data-stu-id="59411-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span></span>
4.  <span data-ttu-id="59411-156">完成上述步驟之後，現在應該可以正確解析您的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="59411-156">Having completed the above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="59411-157">若要確認，您可以再使用一次 [digwebinterface](http://digwebinterface.com)，這一次使用預設名稱伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="59411-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="59411-158">**建議的文件**</span><span class="sxs-lookup"><span data-stu-id="59411-158">**Recommended documents**</span></span>

[<span data-ttu-id="59411-159">將網域委派給 Azure DNS</span><span class="sxs-lookup"><span data-stu-id="59411-159">Delegate a domain to Azure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="59411-160">如何指定 SRV 記錄的 [服務] 和 [通訊協定]？</span><span class="sxs-lookup"><span data-stu-id="59411-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="59411-161">Azure DNS 是以記錄集的方式管理 DNS 記錄—記錄集是名稱與類型相同之記錄的集合。</span><span class="sxs-lookup"><span data-stu-id="59411-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span></span> <span data-ttu-id="59411-162">對於 SRV 記錄集，需要在記錄集名稱中指定 [服務] 和 [通訊協定]。</span><span class="sxs-lookup"><span data-stu-id="59411-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span></span> <span data-ttu-id="59411-163">系統已經為記錄集內每筆記錄個別指定其他 SRV 參數 ([優先順序]、[權數]、[連接埠] 及 [目標])。</span><span class="sxs-lookup"><span data-stu-id="59411-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span></span>

<span data-ttu-id="59411-164">例如，SRV 記錄名稱 (服務名稱 'sip'，通訊協定 'tcp')：</span><span class="sxs-lookup"><span data-stu-id="59411-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="59411-165">\_sip.\_tcp (在區域頂點建立記錄集)</span><span class="sxs-lookup"><span data-stu-id="59411-165">\_sip.\_tcp (creates a record set at the zone apex)</span></span>
- <span data-ttu-id="59411-166">\_sip.\_tcp.sipservice (建立名為 'sipservice' 的記錄集)</span><span class="sxs-lookup"><span data-stu-id="59411-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="59411-167">**建議的文件**</span><span class="sxs-lookup"><span data-stu-id="59411-167">**Recommended documents**</span></span>

<span data-ttu-id="59411-168">[DNS 區域和記錄](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="59411-168">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="59411-169">
[使用 Azure 入口網站建立 DNS 記錄集和記錄](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="59411-169">
[Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="59411-170">
[SRV 記錄類型 (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="59411-170">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="59411-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59411-171">Next steps</span></span>

* <span data-ttu-id="59411-172">了解 [DNS 區域和記錄](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="59411-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="59411-173">若要開始使用 Azure DNS，請學習如何[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)和[建立 DNS 記錄](dns-getstarted-create-recordset-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="59411-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="59411-174">若要移轉現有的 DNS 區域，請學習如何[匯入和匯出 DNS 區域檔案](dns-import-export.md)。</span><span class="sxs-lookup"><span data-stu-id="59411-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>

