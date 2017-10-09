---
title: "使用 Azure CDN aaaAnalyze 使用量統計資料的進階 HTTP 報表 |Microsoft 文件"
description: "了解如何 toocreate 進階 HTTP Microsoft Azure CDN 中的報表。 這些報告提供有關 CDN 活動的詳細資訊。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ef90adc1-580e-4955-8ff1-bde3f3cafc5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3184ec00d089613e25c62762f93043cb4ba68394
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-usage-statistics-with-azure-cdn-advanced-http-reports"></a>使用 Azure CDN 進階 HTTP 報告分析使用量統計資料
## <a name="overview"></a>概觀
本文件說明 Microsoft Azure CDN 中的進階 HTTP 報告。 這些報告提供有關 CDN 活動的詳細資訊。

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="accessing-advanced-http-reports"></a>存取進階 HTTP 報告
1. 從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-advanced-http-reports/cdn-manage-btn.png)
   
    hello CDN 管理入口網站隨即開啟。
2. 暫留在 hello**分析** 索引標籤，然後暫留在 hello**進階 HTTP 報表**彈出式視窗。  按一下 [HTTP 大型平台] 。
   
    ![CDN 管理入口網站 - 進階報告功能表](./media/cdn-advanced-http-reports/cdn-advanced-reports.png)
   
    報告選項隨即顯示。

## <a name="geography-reports-map-based"></a>地理位置報告 (以地圖為基礎)
有五個利用對應 tooindicate hello 區域內容所要求的報表。 這些報告包括世界地圖、美國地圖、加拿大地圖、歐洲地圖和亞太地區地圖。

每個地圖為基礎的報表會根據地理實體 （亦即，國家 （地區）、 狀態和省） 根據 toohello 叫用來自該區域的百分比。 此外，對應是提供 toohelp 視覺化您的內容所要求的 hello 位置。 它是無法 toodo，因此依每個區域的色彩編碼根據 toohello 數量視需要發生在該區域中。 淺色陰影區域表示對您的內容有較低的需求，而較暗區域則表示對您的內容有較高的需求。

正下方 hello 對應提供每個區域的詳細的流量和頻寬資訊。 這可讓您 tooview hello 總數叫用、 叫用的 hello 百分比、 hello 總數量 （以 gb 為單位），傳送的資料和 hello 百分比的資料傳輸的每個區域。 檢視每個這些度量的描述。 最後，當您將滑鼠停留在區域 （也就是國家 （地區）、 狀態或 province），hello hello 區域中發生的叫用的 hello 百分比將顯示名稱和是為工具提示。

下面提供每一種以地圖為基礎的地理位置報告的簡短描述。

| 報告名稱 | 說明 |
| --- | --- |
| 世界地圖 |此報表可讓您針對 CDN 內容 tooview hello 全球需求。 每個國家/地區為 hello world 對應 tooindicate hello 百分比的上叫用來自該區域的色彩標示。 |
| 美國地圖 |此報告可讓您 tooview hello 需求適用於您的 CDN 內容在 hello 美國。 每個狀態是來自該地區的叫用的這個對應 tooindicate hello 百分比以色彩標示。 |
| 加拿大地圖 |此報表可讓您在加拿大 CDN 內容 tooview hello 需求。 每個 province 是來自該地區的叫用的這個對應 tooindicate hello 百分比以色彩標示。 |
| 歐洲地圖 |此報表可讓您在歐洲 CDN 內容 tooview hello 需求。 每個國家 （地區） 是來自該地區的叫用的這個對應 tooindicate hello 百分比以色彩標示。 |
| 亞太地區地圖 |此報告可讓位於亞洲 CDN 內容 tooview hello 需求。 每個國家 （地區） 是來自該地區的叫用的這個對應 tooindicate hello 百分比以色彩標示。 |

## <a name="geography-reports-bar-charts"></a>地理位置報告 (橫條圖)
有兩個額外報表，以提供統計資訊根據 toogeography，也就是前城市和頂端國家 （地區）。 這些報表排名城市與國家 （地區），分別根據 toohello 的點擊次數源自於這些地區。 在產生這種類型的報表，時橫條圖會指出 hello 前 10 個城市或在特定平台上的要求內容的國家/地區。 此橫條圖可讓您 tooquickly 評估 hello 區域產生 hello 最高為您的內容要求數。

hello 左手邊 hello 圖形 （y 軸） 表示多少命中項目的發生 hello 指定區域。 正下方 hello 圖形 （x 軸），您會發現 hello 前 10 個區域的每個的標籤。

### <a name="using-hello-bar-charts"></a>使用 hello 橫條圖
* 如果您將滑鼠停留在列，工具提示的方式將顯示 hello 名稱和 hello 的總點擊次數 hello 區域中發生的。
* hello hello 頂端城市報表的工具提示會識別由其名稱、 縣/市和國家/地區縮寫縣 （市）。
* 如果無法判斷 hello 縣 （市） 或要求來源的地區 （亦即，縣/市），它會表示他們是未知。 如果 hello 國家/地區 （也就是??） 是未知，則兩個問號，隨即出現。
* 報表可能包含度量"Europe"或 hello [亞太地區/地區]。 這些項目並非 tooprovide 那些區域中的所有 IP 位址上的統計資訊。 相反地，而只適用於 toorequests 源自分布在歐洲或亞太地區/而不是 tooa 特定縣市或國家/地區的 IP 位址。

已使用的 toogenerate hello 橫條圖的 hello 資料可以檢視其下。 您將找到 hello 的總點擊次數，叫用，hello 數量 （以 gb 為單位），傳送資料的 hello 百分比和 hello 百分比的資料傳輸進行 hello 頂端 250 區域。 檢視每個這些度量的描述。

下面提供這兩種報告的簡短描述。

| 報告名稱 | 說明 |
| --- | --- |
| 前幾名城市 |此報表會根據根據 toohello 的點擊次數來自該地區的城市。 |
| 前幾名國家/地區 |此報表會根據國家/地區，根據 toohello 的點擊次數源自該區域。 |

## <a name="daily-summary"></a>每日摘要
hello 每日摘要報表可讓您 tooview hello 總數叫用數和特定平台透過傳送每日的資料。 這項資訊可用 tooquickly 分辨 CDN 的活動模式。 比方說，此報告可協助您偵測出哪幾天發生的流量高於或低於預期。

時產生這種類型的報表，橫條圖會提供特定平台需求有經驗的 toohello 少量的視覺指示每天透過 hello hello 報表所涵蓋時段。 它會藉由顯示列 hello 報表中的每一天來這樣做。 例如，選取時間週期的 hello 呼叫"過去一週 將會產生七個橫條的橫條圖。 每個橫條會指出 hello 的總點擊次數發生在那一天。

hello hello 圖形 （y 軸） 的左側指出多少命中項目的發生在 hello 指定日期。 正下方 hello 圖形 （x 軸），您會發現標籤 hello 日期 (格式： YYYY MM DD) hello 報告中包含的每一天。

> [!TIP]
> 如果您將滑鼠停留在列，hello 的總點擊次數發生在該日期會顯示為工具提示。
> 
> 

已使用的 toogenerate hello 橫條圖的 hello 資料可以檢視其下。 那里您會發現 hello 的總點擊次數與 hello 數量 （以 gb 為單位） 傳送資料所涵蓋的 hello 報表每一天。

## <a name="by-hour"></a>依小時
hello 依小時報告可讓您 tooview hello 總數叫用數和特定平台透過傳送每小時的資料。 這項資訊可用 tooquickly 分辨 CDN 的活動模式。 例如，此報表可協助您偵測 hello hello 一天的時間週期，獲得更高或低於預期的流量。

在產生這種類型的報表，時橫條圖會提供每小時透過 hello hello 報表所涵蓋時段的發生的特定平台需求的 toohello 少量的視覺指示。 它會藉由顯示列 hello 報表所涵蓋的每小時來這樣做。 例如，選取 24 小時期間將會產生 24 個橫條的橫條圖。 每個橫條會指出 hello 的總點擊次數在該小時內發生。

hello 圖形 （y 軸） 的 hello 左側指出多少命中項目的發生在 hello 指定小時。 正下方 hello 圖形 （x 軸），您會發現標籤表示 hello 日期/時間 (格式： YYYY MM DD hh: mm) hello 報告中包含每個小時。 回報使用 24 小時格式時間，而且它指定使用 hello UTC/GMT 的時區。

> [!TIP]
> 如果您將滑鼠停留在列，hello 的總點擊次數發生在該小時內會顯示為工具提示。
> 
> 

已使用的 toogenerate hello 橫條圖的 hello 資料可以檢視其下。 那里您會發現 hello 的總點擊次數 hello 資料和數量 （以 gb 為單位） 傳送 hello 報表所涵蓋的每個小時。

## <a name="by-file"></a>依檔案
hello 由檔案報表可讓您 tooview hello 需求和 hello 流量所造成的量 hello 在特定平台透過最要求資產。 在產生這種類型的報表，時橫條圖就會產生 hello 前 10 個最常被要求資產上一段指定時間週期的 hello。

> [!NOTE]
> 基於 hello 這份報表，邊緣 CNAME 的 Url 會是轉換的 tootheir 相等 CDN 的 Url。 這可讓精確票數的 hello 的總點擊次數與資產相關聯 hello CDN 邊緣使用的 CNAME URL toorequest 不論它。
> 
> 

hello 左手邊 hello 圖形 （y 軸） 的一段指定時間週期的 hello 表示 hello 要求每個資產的數目。 正下方 hello 圖形 （x 軸），您會發現，指出每個 hello top 10 要求資產的 hello 檔案名稱的標籤。

已使用的 toogenerate hello 橫條圖的 hello 資料可以檢視其下。 您將找到下列資訊為每個 hello 頂端 250 要求資產的 hello： 相對路徑、 叫用、 叫用的 hello 百分比、 hello 數量 （以 gb 為單位），傳送資料的 hello 總數以及 hello 百分比傳送資料。

## <a name="by-file-detail"></a>依檔案詳細資料
hello 檔案詳細資料的報表可讓您透過特定的資產在特定平台所造成的要求和 hello 流量 tooview hello 數量。 在 hello 這份報表的最上方會是 hello 檔案詳細資料的選項。 此選項會提供一份您最常要求的資產 hello 選平台上。 在順序 toogenerate 檔案詳細資料的報表，您將需要 tooselect hello 所需的資產 hello 檔案詳細資料的選項。 在那之後，橫條圖會指出每日的視需要產生一段指定時間週期的 hello 的 hello 數量。

hello 左手邊 hello 圖形 （y 軸） 的指示 hello 的總要求數資產發生在特定日期。 正下方 hello 圖形 （x 軸），您會發現標籤 hello 日期 (格式： YYYY MM DD) 回報 hello 哪些 CDN 需求的資產。

已使用的 toogenerate hello 橫條圖的 hello 資料可以檢視其下。 那里您會發現 hello 的總點擊次數與 hello 數量 （以 gb 為單位） 傳送資料所涵蓋的 hello 報表每一天。

## <a name="by-file-type"></a>依檔案類型
hello 依檔案類型的報表可讓您 tooview hello 量的需求和 hello 依檔案類型所產生的流量。 在產生這種類型的報表，時環圈圖會指出 hello 百分比 hello 前 10 個檔案類型所產生的叫用。

> [!TIP]
> 如果您將滑鼠停留在 hello 環圈圖配量，hello 網際網路媒體類型的檔案類型將會顯示為工具提示。
> 
> 

已使用的 toogenerate hello 環圈圖的 hello 資料可以檢視其下。 您將找到 hello 檔案名稱副檔名/網際網路媒體類型、 hello 的總點擊次數、 叫用的 hello 百分比、 hello 數量 （以 gb 為單位），傳送的資料和 hello hello 的每個傳輸的資料百分比排名最前面的 250 檔案類型。

## <a name="by-directory"></a>依目錄
hello 由目錄報告可讓您透過從特定的目錄的內容在特定平台所造成的要求和 hello 流量 tooview hello 數量。 在產生這種類型的報表，時橫條圖會指出 hello 的總點擊次數 hello 前 10 個目錄中的內容所產生。

### <a name="using-hello-bar-chart"></a>使用 hello 橫條圖
* 將滑鼠停留在列 tooview hello 相對路徑 toohello 對應目錄。
* 依目錄計算需求時，不會計算儲存在目錄的子資料夾中的內容。 這項計算僅依賴 hello 內容儲存在 hello 實際目錄中產生的要求數目。
* 基於 hello 這份報表，邊緣 CNAME 的 Url 會是轉換的 tootheir 相等 CDN 的 Url。 這可讓所有統計資料的精確票數與資產相關聯 hello CDN 邊緣使用的 CNAME URL toorequest 不論它。

hello hello 圖形 （y 軸） 的左手邊表示 hello 的總要求數 hello 內容儲存在您前 10 個目錄中。 Hello 圖表上的每個橫條都代表目錄。 色彩編碼配置 toomatch 列上的使用 hello hello 250 完整目錄時前, 一節中列出 tooa 目錄。

已使用的 toogenerate hello 橫條圖的 hello 資料可以檢視其下。 您將找到下列每個 hello 頂端 250 目錄資訊的 hello： 相對路徑、 叫用、 叫用的 hello 百分比、 hello 數量 （以 gb 為單位），傳送資料的 hello 總數以及 hello 百分比傳送資料。

## <a name="by-browser"></a>依瀏覽器
hello 的瀏覽器報表可讓您 tooview 哪些瀏覽器所使用的 toorequest 內容。 時產生這種類型的報表時，圓形圖將會指出 hello hello 前 10 個瀏覽器所處理的要求百分比。

### <a name="using-hello-pie-chart"></a>使用 hello 圓形圖
* 瀏覽器的名稱和版本，請停留在 hello 圓形圖 tooview 配量。
* 此報表的 hello 目的，每個唯一的瀏覽器版本的組合會被視為不同的瀏覽器。
* hello 配量稱為 「 其他 」 表示 hello 由所有其他瀏覽器及版本處理要求百分比。

已使用的 toogenerate hello 圓形圖的 hello 資料可以檢視其下。 您將找到 hello 瀏覽器類型/版本號碼，hello 的總點擊次數與叫用每個 hello 最上層 250 瀏覽器的 hello 百分比。

## <a name="by-referrer"></a>依訪客來源
hello 的轉介者報表可讓您 tooview hello 頂端推薦者 」 toocontent hello 選平台上。 查閱者指出 hello 從中產生要求的主機名稱。 在產生這種類型的報表，時橫條圖會指出 hello 最上層的 10 推薦者 」 所產生的 hello 量的需求 （亦即，叫用）。

hello 左手邊 hello 圖形 （y 軸） 的指示 hello 總資產發生的每個查閱者的要求數。 Hello 圖表上的每個橫條都代表查閱者。 色彩編碼配置 toomatch 列上的使用 hello tooa 查閱者列在 hello 頂端 250 查閱者 > 一節。

已使用的 toogenerate hello 橫條圖的 hello 資料可以檢視其下。 您可以在此找到 hello URL、 hello 的總點擊次數，以及從每個 hello 最上層的 250 推薦者 」 產生的點擊 hello 百分比。

## <a name="by-download"></a>依下載
hello 用戶端下載的報表可讓您 tooanalyze 下載模式適用於您最常要求的內容。 hello hello 報表的頂端包含比較嘗試下載已完成下載 hello 前 10 個要求的資產的橫條圖。 每個橫條 （藍色） 是嘗試的下載或已完成的下載 （綠色），根據的 toowhether 它是以色彩標示。

> [!NOTE]
> 基於 hello 這份報表，邊緣 CNAME 的 Url 會是轉換的 tootheir 相等 CDN 的 Url。 這可讓所有統計資料的精確票數與資產相關聯 hello CDN 邊緣使用的 CNAME URL toorequest 不論它。
> 
> 

hello 左手邊 hello 圖形 （y 軸） 的指示 hello 每 hello top 10 要求資產的檔案名稱。 正下方 hello 圖形 （x 軸），您會發現標籤，以指出 hello 總數嘗試/已完成下載。

直接 hello 橫條圖中，以下 hello 下列資訊會列出供 hello 頂端 250 要求資產： 相對路徑 （包括檔案名稱）、 hello 的次數是下載的 toocompletion、 hello 號碼的次數，此要求，以及 hello產生完整的下載要求的百分比。

> [!TIP]
> 資產下載成功時，HTTP 用戶端 (也就是瀏覽器) 不會通知我們的 CDN。 如此一來，我們有 toocalculate 是否資產已完全下載相應 toostatus 代碼和位元組範圍要求。 hello 首先我們查看時進行這項計算 hello 要求是否導致 200 OK 狀態碼。 如果是這樣，然後我們看看的位元組範圍要求 tooensure 它們所涵蓋的 hello 整個資產。 最後，我們會比較 hello 數量 hello 要求資產 toohello 傳輸資料大小。 如果傳送嗨資料大於等於 tooor hello 檔案大小，並 hello 位元組範圍要求適用於該資產，hello 叫用將會計算為完整的下載。
> 
> 這份報表 toohello interpretive 本質，因為必須謹記在心 hello 遵循 hello 一致性與這份報告的精確度可能會改變的點。
> 
> * 當使用者代理程式的行為不同時，無法準確預測流量模式。 這可能會產生大於 100% 的下載完成結果。
> * 此報告可能無法正確表示利用 HTTP 漸進式下載的資產。 這是因為視訊中 toousers 搜尋 toodifferent 位置。
> 
> 

## <a name="by-404-errors"></a>依 404 錯誤
hello 由 404 錯誤報表可讓您產生 hello 大多數 404 找不到的狀態碼的數值內容 tooidentify hello 類型。 hello hello 報表的頂端包含 hello 404 找不到狀態碼為其傳回的前 10 個資產的橫條圖。 此橫條圖會比較 hello 的總要求數導致 「 404 找不到狀態碼這些資產的要求。 每個橫條以色彩標示。 會使用黃色列 hello 要求的 tooindicate 導致 404 找不到狀態碼。 使用紅色軸 tooindicate hello 的總要求數 hello 資產。

> [!NOTE]
> 基於 hello 這份報表，請注意下列 hello:
> 
> * 點擊代表資產的任何要求，而不考慮狀態碼。
> * 邊緣 CNAME 的 Url 會轉換的 tootheir 相同 CDN 的 Url。 這可讓所有統計資料的精確票數與資產相關聯 hello CDN 邊緣使用的 CNAME URL toorequest 不論它。
> 
> 

hello 左手邊 hello 圖形 （y 軸） 的指示 hello top 10 要求資產導致 「 404 找不到狀態碼的每個 hello 檔案名稱。 正下方 hello 圖形 （x 軸），您會發現標籤，以指出 hello 的總要求數和 hello 404 找不到的狀態程式碼所導致的要求數目。

直接 hello 橫條圖中，以下 hello 下列資訊會列出供 hello 頂端 250 要求資產： 相對路徑 （包括檔案名稱），而導致 「 404 找不到狀態碼，hello 總次數的 hello 資產的要求的 hello 數量為要求的並且 hello 404 找不到的狀態程式碼所導致的要求百分比。

## <a name="see-also"></a>另請參閱
* [Azure CDN 概觀](cdn-overview.md)
* [Microsoft Azure CDN 中的即時統計資料](cdn-real-time-stats.md)
* [覆寫使用 hello 規則引擎的預設 HTTP 行為](cdn-rules-engine.md)
* [分析邊緣效能](cdn-edge-performance.md)

