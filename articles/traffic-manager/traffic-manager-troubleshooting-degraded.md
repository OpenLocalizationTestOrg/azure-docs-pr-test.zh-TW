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
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>疑難排解 Azure 流量管理員上的已降級狀態

本文說明如何 tootroubleshoot Azure Traffic Manager 設定檔顯示降級的狀態。 此案例中，請考慮您已設定指向 toosome.cloudapp.net 裝載服務的流量管理員設定檔。 如果顯示 hello 健全狀況您 Traffic Manager**降級**狀態，然後 hello 的一個或多個端點的狀態可能是**降級**:

![降級端點狀態](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

如果顯示 hello 健全狀況您 Traffic Manager**非作用中**狀態，則這兩個結束點可能**已停用**:

![非使用中流量管理員狀態](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>了解流量管理員探查

* Traffic Manager 會考慮線上 hello 探查收到 HTTP 200 回應時，才將 hello 探查路徑從端點 toobe。 其他任何非 200 的回應都是失敗。
* 30 倍重新導向會失敗，即使 hello 重新導向 URL 傳回 200。
* 若為 HTTP 探查，會忽略憑證錯誤。
* hello 探查路徑 hello 實際內容並不重要，只要傳回 200。 探查 URL toosome 靜態內容 like"/ favicon.ico 」 是常用的技巧。 動態內容，例如 hello ASP 頁面不一定會傳回 200，即使 hello 應用程式狀況良好。
* 最佳作法是為 tooset hello 探查路徑 toosomething 具有足夠 hello 站台的邏輯 toodetermine 是向上或向下。 在 hello 上述範例中，藉由設定 hello 路徑 too"/favicon.ico"，您只測試該 w3wp.exe 正在回應。 此探查可能不會指出您的 Web 應用程式狀況良好。 較佳的選擇看起來應該 tooset 路徑 tooa 這類 「 / Probe.aspx 」 具有邏輯 toodetermine hello 健全狀況的 hello 站台。 例如，您可以使用效能計數器 tooCPU 使用率或量值 hello 的失敗要求的數目。 或是，您無法嘗試 tooaccess 資料庫資源或工作階段狀態 toomake 確定 hello web 應用程式可以正常運作。
* 如果設定檔中的所有端點會都降級，然後 Traffic Manager 會將所有的端點視為狀況良好，路由流量 tooall 端點。 此行為可確保，hello 探查機制的問題不會導致在完成中斷您的服務。

## <a name="troubleshooting"></a>疑難排解

tootroubleshoot 探查失敗，您需要從 hello 探查 URL 會顯示 hello HTTP 狀態碼傳回的工具。 有許多可用工具，顯示 hello 未經處理的 HTTP 回應。

* [Fiddler](http://www.telerik.com/fiddler)
* [curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

此外，您可以使用 hello hello F12 偵錯工具在 Internet Explorer tooview hello HTTP 回應中的 [網路] 索引標籤。

此範例中我們想要從我們的探查 URL toosee hello 回應： http://watestsdp2008r2.cloudapp.net:80/探查。 下列 PowerShell 範例 hello 說明 hello 問題。

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

範例輸出︰

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

請注意，我們收到重新導向回應。 如先前所述，200 以外的任何 StatusCode 都視為失敗。 流量管理員變更 hello 端點狀態 tooOffline。 tooresolve hello 問題，可傳回核取 hello 網站組態 tooensure 的 hello 適當 StatusCode hello 探查路徑中。 重新設定 hello Traffic Manager 探查 toopoint tooa 路徑傳回 200。

如果您探查使用 hello HTTPS 通訊協定，您可能需要在測試期間檢查 tooavoid SSL/TLS 錯誤 toodisable 憑證。 hello 下列 PowerShell 陳述式停用憑證驗證的 hello 目前 PowerShell 工作階段：

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

## <a name="next-steps"></a>後續步驟

[關於流量管理員流量路由方法](traffic-manager-routing-methods.md)

[什麼是流量管理員](traffic-manager-overview.md)

[雲端服務](http://go.microsoft.com/fwlink/?LinkId=314074)

[Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/)

[流量管理員的相關作業 (REST API 參考)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Azure 流量管理員 Cmdlet][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
