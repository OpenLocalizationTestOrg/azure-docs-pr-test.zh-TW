---
title: "記錄分析 aaaCustom 欄位 |Microsoft 文件"
description: "記錄分析 hello 自訂欄位功能可讓您 toocreate 您自己從 OMS 資料會加入 toohello 屬性收集記錄的可搜尋的欄位。  本文描述 hello 程序 toocreate 自訂欄位，並提供範例事件的詳細逐步解說。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a>Log Analytics 中的自訂欄位
hello**自訂欄位**功能記錄分析可讓您 tooextend hello OMS 儲存機制中的現有記錄中加入您自己可搜尋的欄位。  自訂欄位會自動填入擷取自 hello 中其他屬性的資料相同的記錄。

![自訂欄位概觀](media/log-analytics-custom-fields/overview.png)

例如，下列的 hello 範例筆都有有用的資料埋藏在 hello 事件描述。  擷取這項資料並將其分成不同屬性，將可讓您對資料進行排序和篩選等動作。

![記錄檔搜尋按鈕](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> 在 hello 預覽，您可以是有限的 too100 工作區中的自訂欄位。  這項功能正式上市時，此限制數量將會擴大。
> 
> 

## <a name="creating-a-custom-field"></a>建立自訂欄位
當您建立自訂欄位時，記錄分析必須了解哪些資料 toouse toopopulate 其值。  它會使用一種技術來自 Microsoft 研究項被稱為 FlashExtract tooquickly 識別此資料。  不需要您 tooprovide 明確指示，記錄分析學習 hello 資料，您會想 tooextract 從您提供的範例。

hello 下列各節提供 hello 程序建立自訂欄位。  這篇文章底部 hello 是範例擷取的逐步解說。

> [!NOTE]
> hello 自訂欄位會擴展為 hello 符合指定準則會新增 toohello OMS 資料存放區，使它只會出現在記錄收集 hello 自訂欄位建立之後的記錄。  hello 自訂欄位將不會加入 toorecords 時就已 hello 資料存放區中建立。
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a>步驟 1 – 識別記錄將會擁有 hello 自訂欄位
hello 第一個步驟為 tooidentify hello 記錄會得到 hello 自訂欄位。  您開始使用[標準的記錄搜尋](log-analytics-log-searches.md)，然後選取記錄 tooact 為記錄分析將從中學習的 hello 模型。  當您指定將 tooextract 資料至自訂欄位時，hello**欄位擷取精靈** 會開啟您驗證並精簡 hello 準則。

1. 跳過**記錄搜尋**並用[查詢 tooretrieve hello 記錄](log-analytics-log-searches.md)，將會擁有 hello 自訂欄位。
2. 選取記錄分析將使用做為模型 tooact 解壓縮資料 toopopulate hello 自訂欄位的記錄。  您會識別 hello 資料，您想要從這筆記錄，tooextract 記錄分析將使用此資訊 toodetermine hello 邏輯 toopopulate hello 自訂欄位的所有類似的記錄。
3. 按一下 [hello] 按鈕 toohello hello 記錄和選取任何文字屬性左邊**從擷取欄位**。
4. hello**欄位擷取精靈] 會開啟**，而且您所選取的 hello 記錄會顯示在 [hello**主要範例**資料行。  hello 自訂欄位將會定義以針對選取的 hello 屬性中的相同值的 hello 這些記錄。  
5. 如果您想要 hello 選取項目時不完全，選取其他欄位 toonarrow hello 條件。  順序 toochange 會 hello hello 準則的欄位值，您必須取消，並選取不同的記錄符合您想要的 hello 準則。

### <a name="step-2---perform-initial-extract"></a>步驟 2 - 執行初始擷取。
一旦您已經識別 hello 記錄將會擁有 hello 自訂欄位，您會識別您想要 tooextract 的 hello 資料。  記錄分析將使用此資訊 tooidentify 類似的模式中類似的記錄。  在此之後的 hello 步驟將會無法 toovalidate hello 的結果，並提供其分析中的記錄分析 toouse 的進一步詳細資料。

1. 反白顯示您想 toopopulate hello 自訂欄位的 hello 範例記錄中的 hello 文字。  您接著會有對話方塊方塊 tooprovide hello 欄位和 tooperform hello 初始擷取的名稱。  hello 字元 **\_CF**會自動附加。
2. 按一下**擷取**tooperform 收集記錄的分析。  
3. hello**摘要**和**搜尋結果**區段會顯示 hello hello 擷取結果，讓您檢查其正確性。  **摘要**顯示 hello 用準則 tooidentify 記錄及計數針對每個已識別的 hello 資料值。  **搜尋結果**提供詳細的 hello 的準則相符的記錄清單。

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a>步驟 3 – 確認 hello 擷取的精確度，並建立自訂欄位
一旦您已經執行 hello 初始擷取，記錄分析會顯示其結果，根據已收集的資料。  如果 hello 結果看起來正確然後您就可以建立 hello 自訂欄位而無須進行進一步的動作。  如果沒有，您可以精簡 hello 結果以便讓記錄分析改善其邏輯。

1. 如果 hello 初始擷取中的任何值不正確，然後按一下 hello**編輯**圖示下一步 tooan 不正確的記錄，然後選取**修改此反白顯示**順序 toomodify hello 選取範圍中。
2. hello 項目會複製的 toohello**其他範例**hello 下方區段**主要範例**。  您可以調整 hello 反白顯示以下 toohelp 記錄分析了解其應該做的 hello 選擇。
3. 按一下**擷取**toouse 所有 hello 現有這個新資訊 tooevaluate 記錄。  hello 結果可能會修改以外 hello 其中是您剛才修改根據這個新資訊的記錄。
4. 繼續 tooadd 更正，直到 hello 中的所有記錄都擷取正確識別 hello 資料 toopopulate hello 新自訂欄位。
5. 按一下**儲存擷取**當您滿意 hello 結果。  hello 自訂欄位現在已經在定義中，但它還不會加入 tooany 記錄。
6. 等候新記錄符合 hello 指定準則 toobe 收集，然後再重新執行 hello 記錄搜尋。 新的記錄都應該有 hello 自訂欄位。
7. 使用 hello 像任何其他記錄的內容的自訂欄位。  可用 tooaggregate 與群組資料並甚至使用 tooproduce 全新深入見解。

## <a name="viewing-custom-fields"></a>檢視自訂欄位
您可以檢視 hello 從管理群組中的所有自訂欄位的清單**設定**hello OMS 儀表板的磚。  依序選取 [資料] 和 [自訂欄位]，可取得工作區中所有自訂欄位的清單。  

![自訂欄位](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a>移除自訂欄位
有兩種方式 tooremove 自訂欄位。  hello 第一個是 hello**移除**檢視 hello 完整清單，如上面所述，當每個欄位的選項。  hello 其他方法是的 tooretrieve 記錄並按一下 hello 按鈕 toohello 方 hello 欄位。  hello 功能表會有選項 tooremove hello 自訂欄位。

## <a name="sample-walkthrough"></a>範例逐步解說
hello 下一節逐步解說建立自訂欄位的完整範例。  這個範例會擷取在 Windows 事件指出變更狀態的服務中的 hello 服務名稱。  這會依賴由服務控制管理員建立 hello Windows 電腦上的系統記錄檔中的事件。  如果您想 toofollow 此範例中，您必須是[收集 hello 系統記錄檔的資訊事件](log-analytics-data-sources-windows-events.md)。

我們輸入下列查詢 tooreturn hello 所有事件從服務控制管理員事件識別碼為 7036 的 hello 事件，指出啟動或停止服務。

![查詢](media/log-analytics-custom-fields/query.png)

然後，我們選取任何事件識別碼為 7036 的記錄。

![來源記錄](media/log-analytics-custom-fields/source-record.png)

我們希望 hello 服務名稱會出現在 hello **RenderedDescription**屬性及選取 hello 按鈕的下一步 toothis 屬性。

![擷取欄位](media/log-analytics-custom-fields/extract-fields.png)

hello**欄位擷取精靈**會開啟，而且 hello **EventLog**和**EventID** hello 中已選取欄位**主要範例**資料行。  這表示該 hello 自訂欄位將會針對識別碼為 7036 的事件 hello 系統記錄檔事件定義。  所以我們不需要 tooselect 任何其他欄位就足夠了。

![主要範例](media/log-analytics-custom-fields/main-example.png)

我們反白顯示 hello hello 中的 hello 服務名稱**RenderedDescription**屬性並使用**服務**tooidentify hello 服務名稱。  hello 自訂欄位將會被稱為**Service_CF**。

![欄位標題](media/log-analytics-custom-fields/field-title.png)

我們會看到某些記錄但不是其他正確識別該 hello 服務名稱。   hello**搜尋結果**顯示 hello hello 名稱的該部分**WMI 效能配接器**未被選取。  hello**摘要**顯示四個記錄與**DPRMA**服務錯誤的包含了額外字組，且兩筆記錄識別**模組安裝程式**而不是**Windows 模組安裝程式**。  

![搜尋結果](media/log-analytics-custom-fields/search-results-01.png)

我們以 hello 開頭**WMI 效能配接器**記錄。  我們按一下它的編輯圖示，然後 [修改此醒目提示] 。  

![修改醒目提示](media/log-analytics-custom-fields/modify-highlight.png)

我們增加 hello 反白顯示 tooinclude hello word **WMI** ，然後重新執行 hello 擷取。  

![其他範例](media/log-analytics-custom-fields/additional-example-01.png)

我們可以看到該 hello 項目**WMI 效能配接器**已經更正，且記錄分析也利用該資訊 toocorrect hello 記錄**Windows 模組安裝程式**。  我們可以看到在 hello**摘要**雖然區段， **DPMRA**為仍然未被正確識別。

![搜尋結果](media/log-analytics-custom-fields/search-results-02.png)

我們捲動 tooa hello DPMRA 服務的記錄，並使用相同的處理序記錄的 toocorrect hello。

![其他範例](media/log-analytics-custom-fields/additional-example-02.png)

 當我們執行 hello 擷取時，我們可以看到，所有的結果現在都很精確。

![搜尋結果](media/log-analytics-custom-fields/search-results-03.png)

我們可以看到**Service_CF**建立但尚未加入 tooany 記錄。

![初始計數](media/log-analytics-custom-fields/initial-count.png)

因此 new 經過一些時間後收集事件，我們可以看到，hello **Service_CF**欄位現在正在加入 toorecords 符合我們準則。

![最終結果](media/log-analytics-custom-fields/final-results.png)

我們現在可以使用 hello 像任何其他的記錄內容的自訂欄位。  tooillustrate，我們建立由新的 hello 分組的查詢， **Service_CF**欄位 tooinspect 哪些服務為最常使用的 hello。

![以查詢分組](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a>後續步驟
* 深入了解[記錄搜尋](log-analytics-log-searches.md)toobuild 查詢準則中使用自訂欄位。
* 監視可利用自訂欄位來剖析的[自訂記錄檔](log-analytics-data-sources-custom-logs.md)。

