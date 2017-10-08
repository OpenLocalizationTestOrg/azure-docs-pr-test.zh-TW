---
title: "在 Azure CDN aaaAnalyze 邊緣節點的效能 |Microsoft 文件"
description: "在 Microsoft Azure CDN 中分析邊緣節點效能。 邊緣效能分析提供 hello CDN 細微資訊流量和頻寬使用量。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 8cc596a7-3e01-4f76-af7b-a05a1421517e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 35361d1c5e27fc6b8536c29e33c2ed217ee4d17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-edge-node-performance-in-microsoft-azure-cdn"></a>在 Microsoft Azure CDN 中分析邊緣節點效能
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>概觀
邊緣效能分析提供 hello CDN 細微資訊流量和頻寬使用量。 這項資訊接著可以使用的 toogenerate 趨勢統計資料，可讓您 toogain 深入了解您的資產如何在快取和傳遞 tooyour 用戶端。 接著，這可讓您 tooform 的策略，在什麼發出您的內容和 toodetermine toooptimize hello 傳遞方式應該是處理 toobetter 運用 hello CDN。 如此一來，不僅將會無法 tooimprove 資料傳遞的效能，但您也會是能 tooreduce CDN 成本。

> [!NOTE]
> 所有報告都採用 UTC/GMT 標記法來指定日期/時間。
> 
> 

## <a name="reports-and-log-collection"></a>報告和記錄收集
Hello 邊緣效能分析模組必須收集 CDN 活動資料之前它會產生報表。 一天其內容涵蓋 hello 前一天期間發生的 hello 活動之後，就會發生此集合的程序。 這表示報表的統計資料在 hello 階段處理，並不一定代表 hello 一天的統計資料的範例包含 hello 組完整的 hello 資料目前的日期。 這些報告的 hello 主要功能是 tooassess 效能。 它們不應該用於計費用途或確切的數值統計資料。

> [!NOTE]
> hello 未經處理的資料，從中產生邊緣效能分析報表可至少 90 天。
> 
> 

## <a name="dashboard"></a>儀表板
hello 邊緣效能分析儀表板會追蹤目前和歷史 CDN 流量透過圖表和統計資料。 使用此儀表板 toodetect 最近和長期趨勢 CDN 流量 hello 效能，為您的帳戶。

此儀表板由下列元件組成：

* 互動式圖表，可讓關鍵計量與趨勢的 hello 視覺效果。
* 時間表，可看出關鍵度量和趨勢的長期模式。
* 關鍵度量和統計資訊，依整體效能、使用量和效率來測量，指出 CDN 網路如何改善網站流量。

### <a name="accessing-hello-edge-performance-dashboard"></a>存取 hello 邊緣績效儀表板
1. 從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    hello CDN 管理入口網站隨即開啟。
2. 暫留在 hello**分析** 索引標籤，然後暫留在 hello**邊緣效能分析**彈出式視窗。  按一下 [儀表板] 。
   
    hello 邊緣節點分析儀表板會顯示。

### <a name="chart"></a>圖表
hello 儀表板包含追蹤 hello 透過其下方出現的 hello 時間軸中選取時間週期的度量圖表。  圖表向上 toohello CDN 活動的最後一個兩年的時間軸會顯示 hello 圖表的正下方。

#### <a name="using-hello-chart"></a>使用 hello 圖
* 根據預設，會繪製 hello hello 過去 30 天內的快取效率速率。
* 此圖表是根據每天整理的資料產生。
* 停留 hello 折線圖上的日期，會指出在該日期 hello 標準日期和 hello 值。
* 按一下 反白顯示週末 tootoggle 的淺灰色分隔號代表週末 hello 圖表到覆疊。 這種覆疊有助於識別週末的流量模式。
* 按一下檢視一年以前 tootoggle 覆疊的 hello 前一年的活動透過 hello 相同期間到 hello 圖表。 這種比較可讓您深入了解長期的 CDN 使用模式。 hello hello 圖表右上角包含一個圖例來表示每個折線圖的 hello 色彩代碼。

#### <a name="updating-hello-chart"></a>更新 hello 圖表
* 時間範圍： 執行 hello 下列其中一種：
  * 選取 hello 時間軸中的 hello 所需的區域。 hello 圖表將會更新對應 toohello 選取時段的資料。
  * 按兩下 hello 圖表 toodisplay 向上 tooa 最多兩年的所有可用的歷程記錄資料。
* 計量： 按一下 hello 圖表顯示圖示，下一步需要 toohello 度量。 hello 圖表與 hello 時間軸會與 hello 對應的標準資料重新整理。

### <a name="key-metrics-and-statistics"></a>關鍵度量和統計資料
#### <a name="efficiency-metrics"></a>效能度量
hello 這些度量的目的是 toosee 是否可以改善快取效率。 hello 衍生自快取效率的主要優點為：

* 這可能會導致 hello 來源伺服器上的降低的負載：
  * 更好的 Web 伺服器效能。
  * 降低營運成本。
* 改善資料傳遞加速，因為系統將會直接從 hello CDN 來處理更多的要求。

| 欄位 | 說明 |
| --- | --- |
| 快取效率 |表示已從快取服務的 hello 百分比傳輸的資料。 這個度量會測量時 hello 的快取版本要求直接從 hello CDN （邊緣伺服器） toorequesters （例如網頁瀏覽器） 所提供的內容 |
| 命中率 |表示已從快取服務的要求 hello 百分比。 這個度量會測量時 hello 的快取版本要求內容已提供直接從 hello CDN （邊緣伺服器） toorequesters （例如網頁瀏覽器）。 |
| 遠端位元組 % - 無快取組態 |表示已從來源伺服器 toohello CDN （邊緣伺服器），不會快取結果 hello 略過快取功能 （HTTP 規則引擎） 服務的流量的 hello 百分比。 |
| 遠端位元組 % - 過期的快取 |過時的內容重新驗證的結果指出 hello 百分比的從來源伺服器 toohello CDN （邊緣伺服器） 所提供的流量。 |

#### <a name="usage-metrics"></a>用量度量
這些度量的 hello 目的是 tooprovide 深入了解下列成本剪下量值的 hello:

* 透過 hello CDN 的營運成本降至最低。
* 透過快取效率和壓縮減少 CDN 支出。

> [!NOTE]
> 流量磁碟區的數字代表用於計算比例和百分比，以及大量的客戶只可能會顯示 hello 總流量的一部分的流量。
> 
> 

| 欄位 | 說明 |
| --- | --- |
| 平均輸出位元組 |指出 hello 平均每個要求 hello CDN （邊緣伺服器） toohello 要求者 （例如網頁瀏覽器） 從服務傳送的位元組數目。 |
| 無快取組態位元組速率 |表示 hello 百分比的 hello CDN （邊緣伺服器） toohello 要求者 （例如網頁瀏覽器） 不會快取到期 toohello 略過快取功能，從提供的流量。 |
| 壓縮的位元組速率 |表示 hello 之百分比傳送嗨 CDN （邊緣伺服器） toorequesters （例如網頁瀏覽器） 的流量以壓縮格式。 |
| 輸出位元組 |指出 hello 資料量，以位元組為單位，傳遞從 hello CDN （邊緣伺服器） toohello 要求者 （例如網頁瀏覽器）。 |
| 輸入位元組 |指出資料，以位元組為單位，從要求者 （例如網頁瀏覽器） toohello CDN （邊緣伺服器） 傳送的 hello 數量。 |
| 遠端位元組 |指出資料，以位元組為單位，從 CDN 和客戶原始伺服器 toohello CDN （邊緣伺服器） 傳送的 hello 數量。 |

#### <a name="performance-metrics"></a>效能度量
這些度量的 hello 用途是 tootrack 為流量的整體 CDN 效能。

| 欄位 | 說明 |
| --- | --- |
| 傳輸速率 |指出 hello 內容 hello CDN tooa 要求已傳輸的平均速率。 |
| Duration |指出 hello 的平均時間，以毫秒為單位，花費 toodeliver 資產 tooa 要求者 （例如網頁瀏覽器）。 |
| 壓縮的要求速率 |壓縮的格式表示 hello CDN （邊緣伺服器） toohello 要求者 （例如網頁瀏覽器） 會從已傳送的叫用的 hello 的百分比。 |
| 4xx 錯誤率 |表示產生 4xx 狀態碼的叫用的 hello 百分比。 |
| 5xx 錯誤率 |表示產生 5xx 狀態碼的叫用的 hello 百分比。 |
| 點擊 |指出 hello CDN 內容的要求數目。 |

#### <a name="secure-traffic-metrics"></a>安全流量度量
這些度量 hello 用途是針對 HTTPS 流量 tootrack CDN 效能。

| 欄位 | 說明 |
| --- | --- |
| 安全快取效率 |表示 hello 百分比從快取服務的 HTTPS 要求傳送的資料。 此標準會測量時 hello 的快取的版本透過 HTTPS 要求的內容已提供直接從 hello CDN （邊緣伺服器） toorequesters （例如網頁瀏覽器）。 |
| 安全傳輸速率 |表示透過 HTTPS 的 hello 內容從 hello CDN （邊緣伺服器） toorequesters （例如，網頁伺服器） 已傳輸的平均速率。 |
| 平均安全持續期間 |指出 hello 的平均時間，以毫秒為單位，花費 toodeliver 資產 tooa 要求者 （例如網頁瀏覽器） 透過 HTTPS。 |
| 安全點擊 |指出 hello CDN 內容的 HTTPS 要求的數目。 |
| 安全輸出位元組 |指出 hello 數量 HTTPS 流量，以位元組為單位，傳遞從 hello CDN （邊緣伺服器） toohello 要求者 （例如網頁瀏覽器）。 |

## <a name="reports"></a>報告
此模組中的每一份報告包含圖表和統計資料，指出各種不同度量 (例如，HTTP 狀態碼、快取狀態碼、要求 URL 等) 的頻寬和流量用量。 這項資訊可能會使用的 toodelve 深入到如何內容提供 tooyour 用戶端和 toofine 微調 CDN 行為 tooimprove 資料傳遞的效能。

### <a name="accessing-hello-edge-performance-reports"></a>存取 hello 邊緣效能報表
1. 從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    hello CDN 管理入口網站隨即開啟。
2. 暫留在 hello**分析** 索引標籤，然後暫留在 hello**邊緣效能分析**彈出式視窗。  按一下 [HTTP 大型物件] 。
   
    顯示 hello 邊緣節點分析報表畫面。

| 報告 | 說明 |
| --- | --- |
| 每日摘要 |可讓您每日流量趨勢 tooview 段指定的時間。 此圖形上的每個橫條都代表特定日期。 hello 軸大小的 hello 表示 hello 的總點擊次數發生在該日期。 |
| 每小時摘要 |可讓您每小時流量趨勢 tooview 段指定的時間。 此圖形上的每個橫條都代表特定日期的單一小時。 hello 軸大小的 hello 表示 hello 的總點擊次數，在該小時內發生。 |
| 通訊協定 |顯示 hello 分解 hello HTTP 和 HTTPS 通訊協定之間的流量。 環圈圖表示所發生的每一種通訊協定叫用的 hello 百分比。 |
| HTTP 方法 |可讓您的 HTTP 方法的快速意義上是的 tooget 正在使用的 toorequest 您的資料。 一般而言，hello 最常見的 HTTP 要求方法是 GET、 HEAD、 和 POST。 環圈圖表示所發生的每一種 HTTP 要求方法叫用的 hello 百分比。 |
| URL |包含圖，顯示 hello top 10 要求的 Url。 每個 URL 會顯示一個橫條。 hello 列高度的 hello 表示多少命中項目的特定 URL 已產生 hello 時間範圍所涵蓋的 hello 報表。 Hello 前 100 個的統計資料要求的 Url 會顯示此圖表的正下方。 |
| CNAME |包含圖來顯示 hello top 10 使用 CNAMEs toorequest 資產 hello 報表時間範圍。 Hello 前 100 個的統計資料要求的 Cname 會顯示此圖表的正下方。 |
| 原始來源 |包含圖，顯示 hello 前 10 個 CDN 或客戶來源伺服器的資產所要求的時間在指定期間內。 Hello 前 100 個的統計資料要求 CDN 或客戶的來源伺服器會顯示此圖表的正下方。 Hello 目錄名稱 選項中所定義的 hello 名稱來識別客戶原始伺服器。 |
| 地區 POP |顯示透過特定存在點 (POP) 路由傳送的流量。 hello 三個字母縮寫代表彈出我們 CDN 網路中。 |
| 用戶端 |包含圖，顯示 hello top 10 的用戶端要求的時間在指定期間內的資產。 基於 hello 這份報表，所有要求源自都 hello 相同 IP 位址會被視為 toobe 都 hello 從同一個用戶端。 Hello 前 100 個用戶端統計資料會顯示此圖表的正下方。 此報告有助於判斷前幾名用戶端的下載活動模式。 |
| 快取狀態 |提供的快取行為，可能會顯示方法，以便改善細目 hello 整體的使用者體驗。 Hello 最快的效能來自快取叫用，因為可以最佳化資料傳送速度降至最低的快取遺漏和過期的快取點擊率。 |
| NONE 詳細資料 |包含圖，顯示 hello top 10 的 Url 為快取內容的有效期限不已檢查的時間在指定期間內的資產。 此圖表的正下方會顯示 hello 前 100 url 中這些類型的資產的統計資料。 |
| CONFIG_NOCACHE 詳細資料 |包含一個圖形，其中顯示未快取到期 toohello 客戶的 CDN 設定資產的 hello 前 10 個 Url。 這些類型的資產是直接由 hello 原始伺服器。 此圖表的正下方會顯示 hello 前 100 url 中這些類型的資產的統計資料。 |
| UNCACHEABLE 詳細資料 |包含圖，顯示 hello 前 10 個的 Url 不會快取 toorequest 標頭資料到期的資產。 此圖表的正下方會顯示 hello 前 100 url 中這些類型的資產的統計資料。 |
| TCP_HIT 詳細資料 |包含圖，顯示 hello 前 10 個的 Url 會立即從快取服務的資產。 此圖表的正下方會顯示 hello 前 100 url 中這些類型的資產的統計資料。 |
| TCP_MISS 詳細資料 |包含圖，顯示 hello top 10 的 Url 之 TCP_MISS 快取狀態的資產。 此圖表的正下方會顯示 hello 前 100 url 中這些類型的資產的統計資料。 |
| TCP_EXPIRED_HIT 詳細資料 |包含圖，顯示 hello top 10 的 Url 已提供直接從 hello POP 的過時資產。 此圖表的正下方會顯示 hello 前 100 url 中這些類型的資產的統計資料。 |
| TCP_EXPIRED_MISS 詳細資料 |包含圖，顯示 hello 前 10 個的 Url 為新版本，都有 toobe 擷取自 hello 來源伺服器的過時資產。 此圖表的正下方會顯示 hello 前 100 url 中這些類型的資產的統計資料。 |
| TCP_CLIENT_REFRESH_MISS 詳細資料 |包含顯示 hello 前 10 個 Url，從原始伺服器因為 tooa 無快取要求從 hello 用戶端擷取資產的橫條圖。 Hello 前 100 的 Url 針對這些類型的要求統計資料會顯示此圖表的正下方。 |
| 用戶端要求類型 |指出 hello HTTP 用戶端 （例如瀏覽器） 所做的要求類型。 此報表包含為 toohow 處理的要求提供了解環圈圖。 每個要求類型的頻寬以及流量資訊會顯示 hello 圖表下方。 |
| 使用者代理程式 |包含橫條圖，顯示前 10 個使用者代理程式 toorequest hello 您透過我們的 CDN 的內容。 一般而言，使用者代理程式是網頁瀏覽器、媒體播放器或行動電話瀏覽器。 這個圖表的正下方會顯示 hello 前 100 位使用者代理程式的統計資料。 |
| 訪客來源 |包含顯示 hello top 10 推薦者 」 toocontent 透過我們的 CDN 存取橫條圖。 一般而言，查閱者是 hello URL hello 網頁或連結 tooyour 內容的資源。 Hello 圖表下面提供詳細的資訊，如 hello 頂端的 100 推薦者 」。 |
| 壓縮類型 |包含的環圈圖詳細分解所要求的資產是否由我們的邊緣伺服器壓縮。 壓縮的資產的 hello 百分比切分 hello 用的壓縮類型。 Hello 圖表下面提供詳細的資訊，針對每個壓縮類型和狀態。 |
| 檔案類型 |包含橫條圖來顯示 hello 前 10 個檔案類型已要求透過我們為您的帳戶的 CDN。 此報表的 hello 目的，檔案類型由定義 hello 資產檔案的副檔名和網際網路媒體類型 (例如.html \[text/html\]，.htm \[text/html\]，.aspx \[text/html\]等。)。 Hello 圖表下面提供詳細的資訊，如 hello 前 100 的檔案類型。 |
| 唯一的檔案 |包含繪製 hello 總數的唯一要求在特定日期的一段指定時間的資產的圖形。 |
| 權杖驗證摘要 |包含的圓形圖提供所要求的資產是否受權杖型驗證保護的快速概觀。 受保護的資產會根據其嘗試驗證 toohello 結果 hello 圖表中顯示。 |
| 權杖驗證拒絕詳細資料 |包含可讓您 tooview hello 前 10 個要求因為 tooToken 為基礎的驗證所拒絕的橫條圖。 |
| HTTP 回應碼 |分解 hello HTTP 狀態碼 (例如 200 [確定]，403 禁止，404 找不到，等)，我們的邊緣伺服器傳遞 tooyour HTTP 用戶端。 圓形圖可讓您 tooquickly 評估如何服務您的資產。 Hello 圖表下方的每個回應碼提供詳細的統計資料。 |
| 404 錯誤 |包含橫條圖，可讓您 tooview hello 前 10 個要求導致 「 404 找不到回應碼。 |
| 403 錯誤 |包含可讓您 tooview hello 前 10 個要求產生 403 禁止回應程式碼中的橫條圖。 當客戶原始伺服器或我們 POP 的邊緣伺服器拒絕要求時，就會發生「403 禁止」回應碼。 |
| 4xx 錯誤 |包含可讓您 tooview hello 前 10 個要求所產生的回應碼，在 hello 400 的範圍內的橫條圖。 這份報告中排除「403 找不到」和「404 禁止」回應碼。 通常，由於用戶端錯誤而拒絕要求時，就會發生 4xx 回應碼。 |
| 504 錯誤 |包含可讓您 tooview hello 前 10 個要求產生 504 閘道逾時回應程式碼中的橫條圖。 HTTP proxy 會嘗試 toocommunicate 與另一個伺服器時，發生逾時，就會發生的 504 閘道逾時的回應碼。 在我們 CDN 的 hello 情況下，504 閘道逾時回應碼通常會發生於邊緣伺服器時無法 tooestablish 客戶來源伺服器的通訊。 |
| 502 錯誤 |包含可讓您 tooview hello 前 10 個要求產生 502 不正確的閘道回應程式碼中的橫條圖。 當伺服器和 HTTP Proxy 之間發生 HTTP 通訊協定失敗時，就會發生「502 錯誤的閘道」回應碼。 在我們 CDN 的 hello 情況下，502 不正確的閘道回應碼通常發生客戶原始伺服器傳回無效的回應 tooan 邊緣伺服器。 無法剖析或不完整的回應就是無效。 |
| 5xx 錯誤 |包含可讓您 tooview hello 前 10 個要求所產生的回應碼，在 hello 500 範圍內的橫條圖。  這份報告中排除「502 錯誤的閘道」和「504 閘道逾時」回應碼。 |

## <a name="see-also"></a>另請參閱
* [Azure CDN 概觀](cdn-overview.md)
* [Microsoft Azure CDN 中的即時統計資料](cdn-real-time-stats.md)
* [覆寫使用 hello 規則引擎的預設 HTTP 行為](cdn-rules-engine.md)
* [進階的 HTTP 報表](cdn-advanced-http-reports.md)

