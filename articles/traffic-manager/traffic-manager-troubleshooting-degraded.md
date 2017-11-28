---
title: "aaaTroubleshooting 降級狀態有關 Azure Traffic Manager"
description: "如何 tootroubleshoot Traffic Manager 設定檔時，它會顯示為降級狀態。"
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
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="79455-103">疑難排解 Azure 流量管理員上的已降級狀態</span><span class="sxs-lookup"><span data-stu-id="79455-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="79455-104">本文說明如何 tootroubleshoot Azure Traffic Manager 設定檔顯示降級的狀態。</span><span class="sxs-lookup"><span data-stu-id="79455-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="79455-105">此案例中，請考慮您已設定指向 toosome.cloudapp.net 裝載服務的流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="79455-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="79455-106">如果顯示 hello 健全狀況您 Traffic Manager**降級**狀態，然後 hello 的一個或多個端點的狀態可能是**降級**:</span><span class="sxs-lookup"><span data-stu-id="79455-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![降級端點狀態](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="79455-108">如果顯示 hello 健全狀況您 Traffic Manager**非作用中**狀態，則這兩個結束點可能**已停用**:</span><span class="sxs-lookup"><span data-stu-id="79455-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![非使用中流量管理員狀態](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="79455-110">了解流量管理員探查</span><span class="sxs-lookup"><span data-stu-id="79455-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="79455-111">Traffic Manager 會考慮線上 hello 探查收到 HTTP 200 回應時，才將 hello 探查路徑從端點 toobe。</span><span class="sxs-lookup"><span data-stu-id="79455-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="79455-112">其他任何非 200 的回應都是失敗。</span><span class="sxs-lookup"><span data-stu-id="79455-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="79455-113">30 倍重新導向會失敗，即使 hello 重新導向 URL 傳回 200。</span><span class="sxs-lookup"><span data-stu-id="79455-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="79455-114">若為 HTTP 探查，會忽略憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="79455-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="79455-115">hello 探查路徑 hello 實際內容並不重要，只要傳回 200。</span><span class="sxs-lookup"><span data-stu-id="79455-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="79455-116">探查 URL toosome 靜態內容 like"/ favicon.ico 」 是常用的技巧。</span><span class="sxs-lookup"><span data-stu-id="79455-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="79455-117">動態內容，例如 hello ASP 頁面不一定會傳回 200，即使 hello 應用程式狀況良好。</span><span class="sxs-lookup"><span data-stu-id="79455-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="79455-118">最佳作法是為 tooset hello 探查路徑 toosomething 具有足夠 hello 站台的邏輯 toodetermine 是向上或向下。</span><span class="sxs-lookup"><span data-stu-id="79455-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="79455-119">在 hello 上述範例中，藉由設定 hello 路徑 too"/favicon.ico"，您只測試該 w3wp.exe 正在回應。</span><span class="sxs-lookup"><span data-stu-id="79455-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="79455-120">此探查可能不會指出您的 Web 應用程式狀況良好。</span><span class="sxs-lookup"><span data-stu-id="79455-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="79455-121">較佳的選擇看起來應該 tooset 路徑 tooa 這類 「 / Probe.aspx 」 具有邏輯 toodetermine hello 健全狀況的 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="79455-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="79455-122">例如，您可以使用效能計數器 tooCPU 使用率或量值 hello 的失敗要求的數目。</span><span class="sxs-lookup"><span data-stu-id="79455-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="79455-123">或是，您無法嘗試 tooaccess 資料庫資源或工作階段狀態 toomake 確定 hello web 應用程式可以正常運作。</span><span class="sxs-lookup"><span data-stu-id="79455-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="79455-124">如果設定檔中的所有端點會都降級，然後 Traffic Manager 會將所有的端點視為狀況良好，路由流量 tooall 端點。</span><span class="sxs-lookup"><span data-stu-id="79455-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="79455-125">此行為可確保，hello 探查機制的問題不會導致在完成中斷您的服務。</span><span class="sxs-lookup"><span data-stu-id="79455-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="79455-126">疑難排解</span><span class="sxs-lookup"><span data-stu-id="79455-126">Troubleshooting</span></span>

<span data-ttu-id="79455-127">tootroubleshoot 探查失敗，您需要從 hello 探查 URL 會顯示 hello HTTP 狀態碼傳回的工具。</span><span class="sxs-lookup"><span data-stu-id="79455-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="79455-128">有許多可用工具，顯示 hello 未經處理的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="79455-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="79455-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="79455-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="79455-130">curl</span><span class="sxs-lookup"><span data-stu-id="79455-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="79455-131">wget</span><span class="sxs-lookup"><span data-stu-id="79455-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="79455-132">此外，您可以使用 hello hello F12 偵錯工具在 Internet Explorer tooview hello HTTP 回應中的 [網路] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="79455-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="79455-133">此範例中我們想要從我們的探查 URL toosee hello 回應： http://watestsdp2008r2.cloudapp.net:80/探查。</span><span class="sxs-lookup"><span data-stu-id="79455-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="79455-134">下列 PowerShell 範例 hello 說明 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="79455-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="79455-135">範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="79455-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="79455-136">請注意，我們收到重新導向回應。</span><span class="sxs-lookup"><span data-stu-id="79455-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="79455-137">如先前所述，200 以外的任何 StatusCode 都視為失敗。</span><span class="sxs-lookup"><span data-stu-id="79455-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="79455-138">流量管理員變更 hello 端點狀態 tooOffline。</span><span class="sxs-lookup"><span data-stu-id="79455-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="79455-139">tooresolve hello 問題，可傳回核取 hello 網站組態 tooensure 的 hello 適當 StatusCode hello 探查路徑中。</span><span class="sxs-lookup"><span data-stu-id="79455-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="79455-140">重新設定 hello Traffic Manager 探查 toopoint tooa 路徑傳回 200。</span><span class="sxs-lookup"><span data-stu-id="79455-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="79455-141">如果您探查使用 hello HTTPS 通訊協定，您可能需要在測試期間檢查 tooavoid SSL/TLS 錯誤 toodisable 憑證。</span><span class="sxs-lookup"><span data-stu-id="79455-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="79455-142">hello 下列 PowerShell 陳述式停用憑證驗證的 hello 目前 PowerShell 工作階段：</span><span class="sxs-lookup"><span data-stu-id="79455-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="79455-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="79455-143">Next Steps</span></span>

[<span data-ttu-id="79455-144">關於流量管理員流量路由方法</span><span class="sxs-lookup"><span data-stu-id="79455-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="79455-145">什麼是流量管理員</span><span class="sxs-lookup"><span data-stu-id="79455-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="79455-146">雲端服務</span><span class="sxs-lookup"><span data-stu-id="79455-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="79455-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="79455-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="79455-148">流量管理員的相關作業 (REST API 參考)</span><span class="sxs-lookup"><span data-stu-id="79455-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="79455-149">[Azure 流量管理員 Cmdlet][1]</span><span class="sxs-lookup"><span data-stu-id="79455-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
