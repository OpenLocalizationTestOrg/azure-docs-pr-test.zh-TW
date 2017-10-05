---
title: "疑難排解 Azure 流量管理員上的已降級狀態"
description: "如何在流量管理員顯示為降級狀態時疑難排解流量管理員設定檔。"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: b1d00fb84695d2289f37647f55a7c56cf28c8c96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="52bf6-103">疑難排解 Azure 流量管理員上的已降級狀態</span><span class="sxs-lookup"><span data-stu-id="52bf6-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="52bf6-104">本文說明如何針對顯示降級狀態的 Azure 流量管理員設定檔進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="52bf6-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="52bf6-105">在此案例中，假設您已設定流量管理員設定檔來指向您的一些 cloudapp.net 託管服務。</span><span class="sxs-lookup"><span data-stu-id="52bf6-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span></span> <span data-ttu-id="52bf6-106">如果流量管理員的健康情況顯示 [降級] 狀態，則可能有一或多個端點的狀態是 [降級]：</span><span class="sxs-lookup"><span data-stu-id="52bf6-106">If the health of your Traffic Manager displays a **Degraded** status, then the status of one or more endpoints may be **Degraded**:</span></span>

![降級端點狀態](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="52bf6-108">如果流量管理員的健康情況顯示 [非使用中] 狀態，則可能有一或多個端點的狀態是 [非使用中]：</span><span class="sxs-lookup"><span data-stu-id="52bf6-108">If the health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![非使用中流量管理員狀態](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="52bf6-110">了解流量管理員探查</span><span class="sxs-lookup"><span data-stu-id="52bf6-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="52bf6-111">只有當探查收到探查路徑傳回 HTTP 200 回應時，流量管理員才會將端點視為在「線上」。</span><span class="sxs-lookup"><span data-stu-id="52bf6-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span></span> <span data-ttu-id="52bf6-112">其他任何非 200 的回應都是失敗。</span><span class="sxs-lookup"><span data-stu-id="52bf6-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="52bf6-113">即使重新導向的 URL 傳回 200，30x 重新導向也會失敗。</span><span class="sxs-lookup"><span data-stu-id="52bf6-113">A 30x redirect fails, even if the redirected URL returns a 200.</span></span>
* <span data-ttu-id="52bf6-114">若為 HTTP 探查，會忽略憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="52bf6-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="52bf6-115">只要傳回 200，探查路徑的實際內容並不重要。</span><span class="sxs-lookup"><span data-stu-id="52bf6-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="52bf6-116">探查靜態內容 (例如 "/favicon.ico") 的 URL 是常用的技巧。</span><span class="sxs-lookup"><span data-stu-id="52bf6-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="52bf6-117">即使應用程式狀況良好，動態內容 (例如 ASP 頁面) 也不一定會傳回 200。</span><span class="sxs-lookup"><span data-stu-id="52bf6-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span></span>
* <span data-ttu-id="52bf6-118">最佳做法是將探查路徑設為有足夠邏輯判斷網站是運作或關閉的項目。</span><span class="sxs-lookup"><span data-stu-id="52bf6-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span></span> <span data-ttu-id="52bf6-119">在上述範例中，您將路徑設為 "favicon.ico"，只是測試 w3wp.exe 是否有回應。</span><span class="sxs-lookup"><span data-stu-id="52bf6-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="52bf6-120">此探查可能不會指出您的 Web 應用程式狀況良好。</span><span class="sxs-lookup"><span data-stu-id="52bf6-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="52bf6-121">較好的選擇是將路徑設為 "/Probe.aspx" 之類的項目，它具有邏輯可判斷網站的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="52bf6-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span></span> <span data-ttu-id="52bf6-122">例如，您可以使用效能計數器來監視 CPU 使用率，或測量失敗的要求數。</span><span class="sxs-lookup"><span data-stu-id="52bf6-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span></span> <span data-ttu-id="52bf6-123">或者，您可以嘗試存取資料庫資源或工作階段狀態，以確定 Web 應用程式正在運作。</span><span class="sxs-lookup"><span data-stu-id="52bf6-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span></span>
* <span data-ttu-id="52bf6-124">如果設定檔中的所有端點都已降級，流量管理員會將所有端點視為狀況良好，並將流量路由傳送至所有端點。</span><span class="sxs-lookup"><span data-stu-id="52bf6-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span></span> <span data-ttu-id="52bf6-125">此行為可確保探查機制的問題不會造成您的服務完全中斷。</span><span class="sxs-lookup"><span data-stu-id="52bf6-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="52bf6-126">疑難排解</span><span class="sxs-lookup"><span data-stu-id="52bf6-126">Troubleshooting</span></span>

<span data-ttu-id="52bf6-127">若要針對探查失敗進行疑難排解，您需要工具來顯示從探查 URL 傳回的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="52bf6-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span></span> <span data-ttu-id="52bf6-128">有許多工具可顯示原始 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="52bf6-128">There are many tools available that show you the raw HTTP response.</span></span>

* [<span data-ttu-id="52bf6-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="52bf6-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="52bf6-130">curl</span><span class="sxs-lookup"><span data-stu-id="52bf6-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="52bf6-131">wget</span><span class="sxs-lookup"><span data-stu-id="52bf6-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="52bf6-132">您也可以在 Internet Explorer 中，使用 [F12 偵錯工具] 的 [網路] 索引標籤來檢視 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="52bf6-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span></span>

<span data-ttu-id="52bf6-133">在此範例中，我們想要查看來自探查 URL http://watestsdp2008r2.cloudapp.net:80/Probe 的回應。</span><span class="sxs-lookup"><span data-stu-id="52bf6-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="52bf6-134">下列 PowerShell 範例說明問題。</span><span class="sxs-lookup"><span data-stu-id="52bf6-134">The following PowerShell example illustrates the problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="52bf6-135">範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="52bf6-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="52bf6-136">請注意，我們收到重新導向回應。</span><span class="sxs-lookup"><span data-stu-id="52bf6-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="52bf6-137">如先前所述，200 以外的任何 StatusCode 都視為失敗。</span><span class="sxs-lookup"><span data-stu-id="52bf6-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="52bf6-138">流量管理員將端點狀態變更為「離線」。</span><span class="sxs-lookup"><span data-stu-id="52bf6-138">Traffic Manager changes the endpoint status to Offline.</span></span> <span data-ttu-id="52bf6-139">若要解決此問題，請檢查網站設定，確保可以從探查路徑傳回適當的 StatusCode。</span><span class="sxs-lookup"><span data-stu-id="52bf6-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span></span> <span data-ttu-id="52bf6-140">重新設定流量管理員探查，以指向傳回 200 的路徑。</span><span class="sxs-lookup"><span data-stu-id="52bf6-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span></span>

<span data-ttu-id="52bf6-141">如果您的探查使用 HTTPS 通訊協定，您可能需要停用憑證檢查，以避免在測試期間發生 SSL/TLS 錯誤。</span><span class="sxs-lookup"><span data-stu-id="52bf6-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="52bf6-142">下列 PowerShell 陳述式會停用目前 PowerShell 工作階段的憑證驗證︰</span><span class="sxs-lookup"><span data-stu-id="52bf6-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="52bf6-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52bf6-143">Next Steps</span></span>

[<span data-ttu-id="52bf6-144">關於流量管理員流量路由方法</span><span class="sxs-lookup"><span data-stu-id="52bf6-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="52bf6-145">什麼是流量管理員</span><span class="sxs-lookup"><span data-stu-id="52bf6-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="52bf6-146">雲端服務</span><span class="sxs-lookup"><span data-stu-id="52bf6-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="52bf6-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="52bf6-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="52bf6-148">流量管理員的相關作業 (REST API 參考)</span><span class="sxs-lookup"><span data-stu-id="52bf6-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="52bf6-149">[Azure 流量管理員 Cmdlet][1]</span><span class="sxs-lookup"><span data-stu-id="52bf6-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
