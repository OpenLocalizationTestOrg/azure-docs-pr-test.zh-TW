---
title: "aaaAzure RemoteApp-測試您的網路頻寬使用量的一些常見案例 |Microsoft 文件"
description: "了解常見的使用量案例，可協助您找出適用於 Azure RemoteApp 的網路頻寬需求。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 06417c75-0c63-4ecf-b9d1-66a7af6b7b91
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 22c1dbb61d956d58d01eb4e11363266168e337e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp - 利用一些常見案例測試您的網路頻寬使用量
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

如我們所述[評估 Azure RemoteApp 的網路頻寬使用量](remoteapp-bandwidth.md)，hello 出 hello 產生的 Azure RemoteApp tooyour 網路的影響是 toorun 的最佳方式 toofigure 某些使用方式的測試。 執行這些測試設定時間週期和量值 hello 頻寬所需的每個案例。 如果您擁有 hello 功能，您也可以測量 hello 網路封包遺失與網路抖動 toounderstand hello 網路模式，將特定的環境中建立。

當評估 hello 頻寬使用量，請記住不同公司內的不同使用者之間的使用方式。 例如，文字讀者和作家所耗用的頻寬會比使用視訊的使用者還少。 為獲得最佳結果，研究您自己的使用者需求，建立下列案例中，最能代表貴公司中的 hello 使用者 hello 的混合。 請記住太[檢閱 hello 因素會影響頻寬使用量和使用者體驗](remoteapp-bandwidthexperience.md)-幫助您識別 hello 理想的測試。

了解 hello 測試的第一次讀取挑選您的混合，然後再執行它們。 您可以使用 hello 表 toohelp 追蹤效能。

> [!NOTE]
> 如果您無法執行您自己的網路測試，或您沒有 hello 時間 toodo 因此，請參閱我們[基本的網路頻寬估計值/建議](remoteapp-bandwidthguidelines.md)。 不過，您的級距可能有所不同，因此，如果您「可以」  執行自己的測試，就應該這樣做。
> 
> 

## <a name="hello-usage-tests"></a>hello 使用測試
這其中每一個測試的執行時間各有不同，並且會測試各種耗用網路頻寬的功能/特性。 請記住 toochoose hello 最符合您公司的個別使用者的測試混合。

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>高階主管/複雜的 PowerPoint - 執行 900-1000秒
使用者可以在全螢幕模式中使用 Microsoft Office PowerPoint，呈現 45-50 張高畫質的投影片。 hello 投影片應該包含影像、 轉換 （含動畫），以及貴公司的典型使用色彩漸層的背景。 hello 使用者應該在每張投影片上花費至少 20 秒。

當投影片轉換 toohello hello 簡報中的下一個投影片，本案例會建立暴增的流量。

### <a name="simple-powerpoint---run-for-620-seconds"></a>簡單的 PowerPoint - 執行 ~620 秒
使用者可以在全螢幕模式中使用 Microsoft Office PowerPoint，來呈現約含 30 張投影片的簡單 PowerPoint 檔案。 hello 投影片是文字比更耗費在 hello 主管/複雜 PowerPoint 案例中，而且具有更簡單的背景和映像 （黑色圖表）。 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer - 執行 ~250 秒
使用者會使用 Internet Explorer 瀏覽 hello web。 hello 使用者瀏覽和捲動文字、 自然的映像，以及某些圖的混合。 hello hello 本機磁碟機的 hello 與遠端桌面工作階段主機 （RD 工作階段主機） 伺服器上儲存的網頁。MHT 檔案。 hello 使用者捲動 Page Up、 Page Down，向上和向下鍵，使用不同的間隔，捲軸每個金鑰/類型：

    - 向下鍵 - 每 500 毫秒 250 次點擊
    - Page Up 鍵 - 每 1000 毫秒 36 次點擊
    - 向下鍵 - 每 100 毫秒 75 次點擊
    - Page Down 鍵 - 每 500 毫秒 20 次點擊
    - 向上鍵 - 每 300 毫秒 120 次點擊

### <a name="pdf-document---simple---run-for-610-seconds"></a>PDF 文件 - 簡單 - 執行 ~610 秒
使用者會使用 Adobe Acrobat Reader，以各種不同方式來讀取和搜尋 PDF 文件。 hello 文件應該包含資料表、 簡單的圖形和多個文字字型。 hello 文件為 35 40 頁的長度。 hello 使用者捲動至兩個不同的費率向後和轉送，四個不同的縮放大小 (符合 toopage，調整 toowidth，100%，而將另一個選擇)。 縮放的 hello 可確保 hello 文字 （字型） 呈現不同的大小。 捲動已關閉 hello Page Up、 Page Down，向上和向下鍵，使用不同的每個捲軸的間隔。

### <a name="pdf-document---mixed---run-for-320-seconds"></a>PDF 文件 - 混合 - 執行 ~320 秒
使用者會使用 Adobe Acrobat Reader，以各種不同方式來讀取和搜尋 PDF 文件。 hello 文件所組成 （包括相片） 的高品質影像、 資料表、 簡單的圖形和多個文字字型。 hello 使用者捲動至兩個不同的費率向後和轉送，四個不同的縮放大小 (符合 toopage，調整 toowidth，100%，而將另一個選擇)。 縮放的 hello 可確保 hello 文字 （字型） 呈現不同的大小。 捲動已關閉 hello Page Up、 Page Down，向上和向下鍵，使用不同的每個捲軸的間隔。

### <a name="flash-video-playback---run-for-180-seconds"></a>Flash 視訊播放 - 執行 ~180 秒
使用者檢視內嵌於網頁中以 Adobe Flash 編碼的視訊。 hello web 網頁會儲存在 hello 本機硬碟 hello RD 工作階段主機伺服器。 hello 視訊便會播放 Internet Explorer 中所內嵌的 player 外掛程式。

此案例會模擬使用者檢視包含多媒體的豐富內容網頁。 大部分的 hello 資料應該透過 VOBR bo。

### <a name="word-remote-typing---run-for-1800-seconds"></a>Word 遠端輸入 - 執行 ~1800 秒
使用者透過 RDP 工作階段輸入文件。 按鍵輸入會傳送 hello hello RDP 工作階段 tooa 文件在 Microsoft Word 中的用戶端從 hello 遠端工作階段中執行。 hello 輸入速率是一個字元的每個 250 毫秒 （總計 7050 字元）。 

這是一個知識工作者的 hello 最常見情況。 這種情況下測試使用者輸入的新式工作處理器 hello 回應的性。 這個案例是使用頻寬的機密 tooeven 小變更。

## <a name="tracking-hello-test-results"></a>追蹤 hello 測試結果
您可以使用下列資料表 tooevaluate hello 案例，您的環境中的 hello。 下面提供的 hello 資料只供說明-可能大幅不同於您的觀察。 

為了簡單起見，我們假設所有案例都會使用 hello 相同 1920 x 1080 像素為單位的螢幕解析度進行都測試及抖動 hello 120 ms + 標記約 1%中的以下 200 毫秒，網路延遲 （延遲） 與網路上的 TCP 傳輸。

關於 hello 資料表：

* **平均經驗**包含使用者生產力不會大幅影響，但不是排除偶爾的視訊或音訊問題的 hello 的網路頻寬。 hello 系統所能 toorecover 快速利用 hello 動態邏輯。 hello 網路頻寬估計值嘗試 tooguarantee hello 品質的 hello 使用者經驗。
  * **值得注意的問題 （中斷點）**包含使用者可能會注意到重大的問題，在其經驗中，而其生產力可測量的時間週期內受影響的 hello 的網路頻寬。 此時 hello RDP 演算法會致力並無法保證 hello 使用者品質使用經驗，因為沒有足夠的網路頻寬。
  * **建議**包含建議的較佳或絕佳體驗的 hello 網路頻寬。 它是通常一個步驟中 hello 對應的 hello 值高於**平均經驗**資料行。
  * **注意事項** 包括觀察值和註解。

| 測試 | 平均體驗 | 值得注意的問題 (中斷點) | 建議的網路頻寬 | 注意事項 |
| --- | --- | --- | --- | --- |
| 高階主管/複雜的 PPT |10 MB/秒 |1 MB/秒 |> 10 MB/秒，通常使用 100 MB/秒  |在 1 MB/秒內遺失許多動畫 |
| 簡單的 PPT |5 MB/秒 |256 KB/秒 |10 MB/秒 |在 256 KB/s hello 投影片載入，發生明顯的延遲 |
| Internet Explorer |10 MB/秒 |1 MB/秒 |> 10 MB/秒，通常使用 100 MB/秒  |在 1 MB/秒內，Web 視訊是模糊且不穩定的，快速捲動會發生問題 |
| 簡單的 PDF |1 MB/秒 |256 KB/秒 |5 MB/秒 |在 256 KB/s 它需要一些時間 tooload hello 頁面 |
| 混合的 PDF |1 MB/秒 |256 KB/秒 |5 MB/秒 |在 256 KB/s hello 頁面佔用大量的時間 tooload |
| Flash 視訊播放 |10 MB/秒 |1 MB/秒 |> 10 MB/秒，通常使用 100 MB/秒  |1 MB/s hello 視訊是有顆粒狀而捨棄某些畫面格 |
| Word 遠端輸入 |256 KB/秒 |128 KB/秒 |1 MB/秒 |在 256 KB/s 使用者可能會注意到 hello 按鍵動作之間的時間 |

tooevaluate hello 網路頻寬，每位使用者建立的上述案例 hello 混合和 hello 的所需的網路頻寬相對應的比例。 挑選 hello 您案例所需的最高數字。 由於使用者幾乎永遠不會使用單獨的 hello 系統時，考慮某些保留使用的使用者可同時在 hello 相同的網路。

## <a name="learn-more"></a>詳細資訊
* [Estimate Azure RemoteApp network bandwidth usage (評估 Azure RemoteApp 網路頻寬使用量)](remoteapp-bandwidth.md)
* [Azure RemoteApp - how do network bandwidth and quality of experience work together? (Azure RemoteApp - 如何兼顧網路頻寬和體驗品質？)](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp network bandwidth - general guidelines (if you can't test your own) (Azure RemoteApp 網路頻寬 - 一般指引 (如果您無法自行測試))](remoteapp-bandwidthguidelines.md)

