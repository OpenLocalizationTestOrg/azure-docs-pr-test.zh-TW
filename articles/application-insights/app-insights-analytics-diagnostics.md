---
title: "在 Azure Application Insights 中的 web 應用程式效能變更 aaaSmart 診斷 |Microsoft 文件"
description: "自動診斷您 Web 應用程式之效能遙測資料中的突然增加或段差情況。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a>診斷您應用程式遙測資料中的突發變更

*這項功能處於預覽狀態。*

只要按一下，即可診斷您 Web 應用程式的效能或使用情況上的突發變更！ 每當您建立在時間圖表時，會出現 hello 智慧的診斷功能[分析](app-insights-analytics.md)中[Application Insights](app-insights-overview.md)。 無論與您的結果，例如高峰或 dip，hello 趨勢的不尋常變更智慧診斷會識別維度和相關聯的值可能會詳述 hello 變更的模式。 這可協助您快速診斷 hello 問題。 

在此範例中，智慧診斷已識別的 hello 變更相關聯的屬性值的模式，並反白顯示 hello 與不該模式的結果差異：

![範例分析診斷結果](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a>診斷資料變更

1.  在 [分析] 中執行查詢，並將它轉譯成時間圖表。 
2.  按一下任何醒目提示的尖峰點 (如果有的話)。
 
    ![尖峰點](./media/app-insights-analytics-diagnostics/peak.png)

    診斷需要幾秒鐘 toodiscover 模式。

3. hello 診斷結果索引標籤會顯示說明您的資料不一致的模式。

    ![結果](./media/app-insights-analytics-diagnostics/result.png)
 
    hello 文字會顯示 hello 維度值出現 toocorrelate 與 hello shift 鍵。 在此範例中，它是與特定的要求和特定的瀏覽器版本關聯。

    另請注意 hello 兩個元件的 hello 圖，其中 hello 篩選 true 和 false。 hello false 元件會顯示未變更的趨勢。 換句話說，沒有任何變更在 hello 遙測結果中，如果我們排除 hello 的診斷所識別的維度有問題的組合。 相反地，該組合中的 hello 結果並調查 hello 反白顯示區域內顯示重大的變更。 這會顯示診斷發現說明 hello 變更屬性的組合。

4.  如果 hello 模式很複雜，您需要比 toohover**全部顯示**toosee hello 維度。

    ![全部顯示](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  萬一診斷尋找有關 hello '沒有結果' 頁面將會呈現任何顯著的模式 toonotify。 此時，您可以變更您的查詢。 例如，您可以縮小 hello 時間範圍和分類收納中分析查詢，進一步的分析和具有較好的結果。

特定的頁面上，您的網站發生問題，在特定瀏覽器上 hello 知識為利器，現在可以移至直線 toohello 問題頁面，並調查最近的變更。

## <a name="try-hello-demo"></a>請嘗試 hello 示範

[按一下這裡 toosee 示範](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H)針對取樣資料。

## <a name="how-it-works"></a>運作方式

智慧診斷會使用進階不受監督的機器學習演算法根據 hello [DiffPatterns](app-insights-analytics-reference.md)作業。 看起來的候選模式，可能會詳述 hello 資料變更。 它會分析的每個候選位置 hello 度量 hello 影響，並顯示 hello 模式最佳相互關聯與 hello 變更。

## <a name="no-diagnostic-points"></a>沒有任何診斷點？

當符合下列準則的 hello 時，只適用於智慧診斷：

 * 已開啟 [智慧型診斷] 設定。 尋找在分析中的 hello 設定圖示下。
 * hello 智慧診斷 選項中分析設定為已選取。 
 * 時間軸： hello hello 圖表的 x 軸的類型必須是`datetime`。
 * 折線圖或區域圖：診斷只有在這些類型的圖表才能運作。 使用`| render timechart`或`| render areachart`結尾 hello 您的查詢，或從 hello 下拉式清單選取器選取線條或區域圖。
 * 不一致： Hello 資料中必須有重大的不一致。
 * 足夠的點 tooanalyze。
 * 不超過一個彙總 hello 查詢中的子句。
 * 包含名稱定義 hello 之前沒有專案子句摘要子句。

 
 ## <a name="related-articles"></a>相關文章

 * [Analytics 教學課程](app-insights-analytics-tour.md)
 * [智慧偵測](app-insights-proactive-diagnostics.md)自動警示 tooperformance 問題。
