---
title: "aaaAzure CDN 的概觀 |Microsoft 文件"
description: "了解 Azure 內容傳遞網路 (CDN) 是何種 hello 和如何 toouse 它 toodeliver 高頻寬內容的快取 blob 和靜態內容。"
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Hello Azure 內容傳遞網路 (CDN) 的概觀
> [!NOTE]
> 本文件說明 Azure 內容傳遞網路 (CDN) 是何種 hello、 它的運作方式及 hello 功能的每個 Azure CDN 產品。  如果您想 tooskip 這項資訊和如何移直線 tooa 教學課程 toocreate CDN 端點，請參閱[使用 Azure CDN](cdn-create-new-endpoint.md)。  如果您想 toosee 目前 CDN 節點位置的清單，請參閱[Azure CDN POP 位置](cdn-pop-locations.md)。
> 
> 

hello Azure 內容傳遞網路 (CDN) 會快取靜態的 web 內容在策略性放置的位置傳遞內容 toousers tooprovide 最大輸送量。  hello CDN 提供開發人員一套傳遞高頻寬內容的快取 hello 世界各地的 hello 實體節點內容的全球解決方案。 

使用 hello CDN toocache 網站資產的 hello 優點包括：

* 更好的效能和使用者經驗對於使用者，尤其是當使用多個往返所在位置的應用程式需要 tooload 內容。
* 大型的縮放比例 toobetter 處理瞬間大量負載，例如在 hello 開頭的產品上市。
* 藉由散發使用者要求並處理來自邊緣伺服器內容、 較少的流量會傳送 toohello 原點。

## <a name="how-it-works"></a>運作方式
![CDN 概觀](./media/cdn-overview/cdn-overview.png)

1. 使用者 (Alice) 使用具有特殊網域名稱的 URL (例如 `<endpointname>.azureedge.net`) 要求檔案 (也稱為資產)。  DNS 會路由傳送嗨要求 toohello 最佳執行點顯示 (POP) 位置。  這通常是 hello 地理位置最靠近 toohello 使用者快顯程式。
2. 如果在 hello POP hello 邊緣伺服器快取中沒有 hello 檔案，hello 邊緣 hello 的原始伺服器要求 hello 檔案。  hello 來源可以是 Azure Web 應用程式、 Azure 雲端服務、 Azure 儲存體帳戶或任何可公開存取的網頁伺服器。
3. hello 原點傳回 hello 檔案 toohello edge server，包括選用描述 hello 檔案-存留時間 (TTL) 的 HTTP 標頭。
4. hello 邊緣伺服器 hello 檔案會快取，並傳回 hello 檔案 toohello 原始要求者 (Alice)。  hello TTL 到期之前 hello 檔案則維持在 hello edge server 快取。  如果 hello 原點沒有指定的 TTL hello 預設的 TTL 為 7 天。
5. 其他使用者可能要求 hello 相同的檔案使用該相同的 URL，並也可能會導向的 toothat 相同的快顯程式。
6. 如果未過期 hello TTL hello 檔案 hello 邊緣伺服器會從 hello 快取傳回 hello 檔。  這會產生更快、更靈敏回應的使用者經驗。

## <a name="azure-cdn-features"></a>Azure CDN 功能
共有三種 Azure CDN 產品︰**來自 Akamai 的 Azure CDN 標準**、**來自 Verizon 的 Azure CDN 標準**和**來自 Verizon 的 Azure CDN 進階**。  hello 下表列出與每個可用的 hello 功能。

|  | 標準 Akamai | 標準 Verizon | 進階 Verizon |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __效能功能和最佳化__ |
| [動態網站加速](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[動態網站加速 - 調整映像壓縮](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[動態網站加速 - 物件預先擷取](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [影片串流最佳化](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [大型檔案最佳化](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [全域伺服器負載平衡 (GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [快速清除](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [資產預先載入](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| [查詢字串快取](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| IPv4/IPv6 雙重堆疊 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [HTTP/2 支援](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __安全性__ |
| CDN 端點的 HTTPS 支援 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [自訂網域 HTTPS](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [自訂網域名稱支援](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [地理位置篩選](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [權杖驗證](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [DDOS 保護](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __分析和報告__ |
| [核心分析](cdn-analyze-usage-patterns.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [進階 HTTP 報告](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [即時統計資料](cdn-real-time-stats.md) | | |**&#x2713;** |
| [即時警示](cdn-real-time-alerts.md) | | |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __容易使用__ |
| 很容易與[儲存體](cdn-create-a-storage-account-with-cdn.md)、[雲端服務](cdn-cloud-service-with-cdn.md)、[Web Apps](../app-service-web/app-service-web-tutorial-content-delivery-network.md) 和[媒體服務](../media-services/media-services-portal-manage-streaming-endpoints.md)等 Azure 服務整合 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| 透過 [REST API](https://msdn.microsoft.com/library/mt634456.aspx)、[.NET](cdn-app-dev-net.md)、[Node.js](cdn-app-dev-node.md) 或 [PowerShell](cdn-manage-powershell.md) 管理。 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [可自訂的、規則式內容傳遞引擎](cdn-rules-engine.md) | | |**&#x2713;** |
| 快取/標頭設定 (使用 [規則引擎](cdn-rules-engine.md)) | | |**&#x2713;** |
| URL 重新導向/重寫 (使用 [規則引擎](cdn-rules-engine.md)) | | |**&#x2713;** |
| 行動裝置規則 (使用 [規則引擎](cdn-rules-engine.md)) | | |**&#x2713;** |

\* Verizon 支援透過一般 Web 傳遞直接傳遞大型檔案和媒體。


> [!TIP]
> 有一項功能，您想要在 Azure CDN toosee 嗎？  [請不吝提供意見](https://feedback.azure.com/forums/169397-cdn)！ 
> 
> 

## <a name="next-steps"></a>後續步驟
tooget 入門 CDN，請參閱[使用 Azure CDN](cdn-create-new-endpoint.md)。

如果您已經是 CDN 客戶，您現在可以管理您的 CDN 端點，透過 hello [Microsoft Azure 入口網站](https://portal.azure.com)或[PowerShell](cdn-manage-powershell.md)。

toosee hello CDN 中的動作，請簽出 hello[我們建置 2016年工作階段的視訊](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/)。

深入了解如何 tooautomate Azure CDN 與[.NET](cdn-app-dev-net.md)或[Node.js](cdn-app-dev-node.md)。

如需價格資訊，請參閱 [CDN 價格](https://azure.microsoft.com/pricing/details/cdn/)。

