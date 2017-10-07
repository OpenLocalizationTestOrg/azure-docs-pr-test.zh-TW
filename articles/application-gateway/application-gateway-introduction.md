---
title: "aaaIntroduction tooAzure 應用程式閘道 |Microsoft 文件"
description: "此頁面提供概觀 hello 第 7 層負載平衡的應用程式閘道服務包括閘道大小、 HTTP 負載平衡時，cookie 架構工作階段親和性，以及 SSL 卸載。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: b37a2473-4f0e-496b-95e7-c0594e96f83e
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c40c9dba64ab03d9f6f81b3cb8f26c6562ac26c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-gateway"></a>應用程式閘道的概觀

Microsoft Azure 應用程式閘道是專用的虛擬設備，它會以服務形式提供應用程式傳遞控制器 (ADC)。 它會為您的應用程式提供各種第 7 層負載平衡功能。 它可讓客戶 toooptimize web 伺服陣列產能卸載 CPU 密集 SSL 終止 toohello 應用程式閘道。 它也提供其他層 7 路由功能，包括循環配置資源發佈的連入流量，cookie 為基礎的工作階段親和性，路徑為基礎的路由 URL，和 hello 能力 toohost 單一應用程式閘道背後的多個網站。 Web 應用程式的防火牆 (WAF) 也會提供 hello 應用程式閘道 WAF SKU 的一部分。 它提供保護 tooweb 應用程式，從一般 web 弱點和破解。 應用程式閘道可以設定為面向網際網路的閘道、內部專用閘道或兩者混合。 

![案例](./media/application-gateway-introduction/scenario.png)

## <a name="features"></a>特性

應用程式閘道目前提供下列功能的 hello:


* **[Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)** -從網頁型的常見攻擊，例如 SQL 資料隱碼、 跨網站指令碼的攻擊和工作階段倘若 hello web 應用程式中的防火牆 (WAF) Azure 應用程式閘道可保護的 web 應用程式。
* **HTTP 負載平衡** - 應用程式閘道提供循環配置資源負載平衡。 負載平衡會在第 7 層進行，而且只會用於 HTTP(S) 流量。
* **Cookie 架構工作階段親和性**-hello cookie 架構工作階段親和性功能十分有用，當您想 tookeep hello 上的使用者工作階段時相同的後端。 使用閘道管理 cookie，hello 應用程式閘道會從使用者工作階段 toohello 無法 toodirect 後續流量相同後端處理。 這項功能，請務必在工作階段狀態儲存在本機 hello 後端伺服器的使用者工作階段的情況下。
* **[安全通訊端層 (SSL) 卸載](application-gateway-ssl-arm.md)** -這項功能會採用 hello 最密切相關的工作，解密關閉您的 web 伺服器的 HTTPS 流量。 所終止 hello hello 應用程式閘道和轉送 hello 要求 toohello 伺服器未加密的 SSL 連線，是由解密 unburdened hello web 伺服器。  應用程式閘道重新加密 hello 回應，再將它傳送後 toohello 用戶端。 此功能十分有用 hello 後端所在位置的案例中的 hello 相同保護虛擬網路 hello Azure 中的應用程式閘道。
* **[結束 tooEnd SSL](application-gateway-backend-ssl.md)**  -應用程式閘道支援結束 tooend 加密的流量。 應用程式閘道會終止在 hello 應用程式閘道的 hello SSL 連線。 hello 閘道會接著套用 hello 路由規則 toohello 流量重新加密 hello 封包，並將轉送 hello 封包 toohello 適當的後端基礎 hello 路由定義的規則。 Hello web 伺服器的任何回應 hello 會經歷相同的處理序後 toohello 終端使用者。
* **[URL 為基礎的內容路由傳送](application-gateway-url-route-overview.md)** -這項功能提供了 hello 功能 toouse 不同的後端伺服器不同的流量。 可以路由的 tooa 不同後端 hello web 伺服器上的資料夾或 CDN 的流量。 此功能可讓不處理特定內容的後端得以減少不必要的負載。
* **[多站台路由](application-gateway-multi-site-overview.md)** -tooconsolidate too20 網站上的單一應用程式閘道註冊可讓應用程式閘道。
* **[Websocket 支援](application-gateway-websocket.md)** -應用程式閘道的另一項絕佳功能是提供 Websocket hello 原生支援。
* **[健全狀況監視](application-gateway-probe-overview.md)** -應用程式閘道提供預設健全狀況監視的後端資源和自訂探查 toomonitor 更具體的案例。
* **[SSL 政策和加密](application-gateway-ssl-policy-overview.md)** ： 這項功能提供的 hello 能力 toolimit hello SSL 通訊協定版本和 hello 這類編碼器 hello 的處理的順序與支援的套件。
* **[要求重新導向](application-gateway-redirect-overview.md)** -這項功能提供 hello 功能 tooredirect HTTP 要求 tooan HTTPS 接聽程式。
* **[多租用戶後端支援](application-gateway-web-app-overview.md)** - 應用程式閘道支援將多租用戶後端服務 (例如 App Web Apps 和 API 閘道) 設定為後端集區成員。 
* **[進階診斷](application-gateway-diagnostics.md)** - 應用程式閘道提供完整的診斷和存取記錄檔。 防火牆記錄檔可供已啟用 WAF 的應用程式閘道資源使用。

## <a name="benefits"></a>優點

應用程式閘道對於下列項目很實用：

* 需要要求的應用程式從 hello 相同的使用者/用戶端工作階段 tooreach hello 相同後端的虛擬機器。 這些應用程式的範例包括購物車應用程式和網頁郵件伺服器。
* 移除 Web 伺服器陣列的 SSL 終止負荷。
* 應用程式，例如內容傳遞網路，這需要的 hello 長時間執行相同的 TCP 連線 toobe 路由或負載平衡的 toodifferent 後端伺服器上的多個 HTTP 要求。
* 支援 Websocket 流量的應用程式
* 保護 Web 應用程式不致遭受常見的 Web 型攻擊，例如 SQL 插入式攻擊、跨網站指令碼攻擊和工作階段攔截。
* 以不同路由準則 (例如 url 路徑或網域標頭) 為基礎的邏輯流量分配。

應用程式閘道完全由 Azure 管理、可調整且可用性極高。 它提供一組豐富的診斷和記錄功能，很好管理。 當您建立應用程式閘道時，將會有一個端點 (公用 VIP 或內部 ILB IP) 形成關聯，並用於輸入網路流量。 此 VIP 或 ILB IP 係由 Azure 負載平衡器在 hello 傳輸層級 (TCP/UDP) 處理，並具備正在背景工作執行個體的負載平衡的 toohello 應用程式閘道的所有連入網路流量。 hello 應用程式閘道，然後路由 hello HTTP/HTTPS 流量是否為虛擬機器，根據其設定雲端服務，內部或外部 IP 位址。

應用程式閘道的負載平衡作為 Azure 受管理的服務，以允許 hello hello Azure 軟體負載平衡器後方的第 7 層負載平衡器佈建。 流量管理員可以使用的 toocomplete hello 案例中，下列映像，其中 Traffic Manager 提供重新導向和可用性的流量 toomultiple 應用程式閘道資源在不同的區域，而應用程式閘道所提供的 hello 中所見跨區域第 7 層負載平衡。 此案例的範例，請參閱在：[使用負載平衡中 hello Azure 雲端服務](../traffic-manager/traffic-manager-load-balancing-azure.md)

![流量管理員和應用程式閘道案例](./media/application-gateway-introduction/tm-lb-ag-scenario.png)

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="gateway-sizes-and-instances"></a>閘道大小和執行個體

應用程式閘道目前提供三種大小：**小型**、**中型**和**大型**。 小型執行個體大小是針對開發和測試案例。

您可以建立每個訂閱，too50 應用程式閘道上，且每個應用程式閘道可以 too10 執行個體每一個。 每個應用程式閘道可以包含 20 個 http 接聽程式。 如需應用程式閘道限制的完整清單，請瀏覽[應用程式閘道服務限制](../azure-subscription-service-limits.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#application-gateway-limits)。

hello 下表顯示啟用 SSL 卸載，每個應用程式閘道執行個體的平均效能輸送量：

| 後端頁面回應 | 小型 | 中型 | 大型 |
| --- | --- | --- | --- |
| 6K |7.5 Mbps |13 Mbps |50 Mbps |
| 100K |35 Mbps |100 Mbps |200 Mbps |

> [!NOTE]
> 這些值是應用程式閘道輸送量的近似值。 hello 實際輸送量取決於各種不同的環境詳細資料，例如平均頁面大小後, 端執行個體和處理時間 tooserve 頁面的位置。 如需實際效能數字，您需自行執行測試。 這些值僅供容量規劃指引使用。

## <a name="health-monitoring"></a>健康狀況監視

Azure 應用程式閘道會自動監視透過基本或自訂的健全狀況探查的 hello hello 後端執行個體的健全狀況。 藉由使用健全狀況探查，它可確保只有狀況良好的主機回應 tootraffic。 如需詳細資訊，請參閱 [應用程式閘道健全狀況監視概觀](application-gateway-probe-overview.md)。

## <a name="configuring-and-managing"></a>設定和管理

對於其端點，應用程式閘道可以有公用 IP、私人 IP 或兩者 (若已設定)。 應用程式閘道會設定於自己的子網路中的虛擬網路內。 建立或使用應用程式閘道的 hello 子網路不能包含任何其他類型的資源，hello 唯一資源 hello 子網路中允許的其他應用程式閘道。 您的後端資源，hello 後端伺服器可以包含在不同的子網路中 hello toosecure hello 應用程式閘道相同的虛擬網路。 Hello 後端應用程式不需要此子網路。 只要 hello 應用程式閘道可以到達 hello ip 位址，應用程式閘道會是能 tooprovide ADC hello 後端伺服器的功能。 

您可以藉由使用 REST API、PowerShell Cmdlet、Azure CLI 或 [Azure 入口網站](https://portal.azure.com/)來建立和管理應用程式閘道。 如需應用程式閘道上的其他問題請造訪[應用程式閘道常見問題集](application-gateway-faq.md)tooview 的常見清單常見問題集。

## <a name="pricing"></a>價格

價格是以每小時的閘道器執行個體費用和資料處理費用為基礎。 每小時定價 hello WAF SKU 的閘道是不同於標準 SKU 費用。 您可在[應用程式閘道價格詳細資料](https://azure.microsoft.com/pricing/details/application-gateway/)找到此價格資訊。 資料處理費用保持 hello 相同。

## <a name="faq"></a>常見問題集

如需應用程式閘道的常見問題集，請參閱[應用程式閘道常見問題集](application-gateway-faq.md)。

## <a name="next-steps"></a>後續步驟

了解應用程式閘道之後, 您就能[建立應用程式閘道](application-gateway-create-gateway-portal.md)或您可以[建立 SSL 卸載應用程式閘道](application-gateway-ssl-arm.md)tooload 平衡 HTTPS 連線。

toolearn 如何 toocreate 應用程式閘道使用的 URL 為基礎內容的路由，跳過[建立應用程式閘道使用的 URL 為基礎的路由](application-gateway-create-url-route-arm-ps.md)如需詳細資訊。

有關某些 toolearn hello 其他網路功能的 Azure 功能的金鑰，請參閱[Azure 網路](../networking/networking-overview.md)。
