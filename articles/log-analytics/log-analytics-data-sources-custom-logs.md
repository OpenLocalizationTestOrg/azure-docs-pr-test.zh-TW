---
title: "aaaCollect 自訂登入 OMS 記錄分析 |Microsoft 文件"
description: "Log Analytics 可從 Windows 和 Linux 電腦上的文字檔收集事件。  這篇文章描述如何 toodefine 新的自訂記錄檔和詳細資料的 hello 記錄它們建立 hello OMS 儲存機制中。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a>Log Analytics 中的自訂記錄檔
記錄分析中的 hello 自訂記錄檔資料來源可讓您從 Windows 和 Linux 電腦上的文字檔 toocollect 事件。 許多應用程式記錄資訊 tootext 檔，而不是標準的記錄服務，例如 Windows 事件記錄檔或 Syslog。  一旦收集完成，您可以剖析使用 hello tooindividual 欄位中的 hello 記錄檔中的每一筆記錄[自訂欄位](log-analytics-custom-fields.md)記錄分析的功能。

![自訂記錄檔收集](media/log-analytics-data-sources-custom-logs/overview.png)

hello 收集的記錄檔 toobe 必須符合下列準則的 hello。

- hello 記錄必須有每行的單一項目，或使用時間戳記相符 hello 下列其中一種格式在 hello 開頭的每個項目。

    YYYY-MM-DD HH:MM:SS <br>M/D/YYYY HH:MM:SS AM/PM <br>Mon DD,YYYY HH:MM:SS

- hello 記錄檔不允許循環的更新會以新的項目覆寫 hello 檔案。
- hello 記錄檔必須使用 ASCII 或 utf-8 編碼。  不支援其他格式，例如 UTF-16。

>[!NOTE]
>如果 hello 記錄檔中有重複的項目，將會收集記錄分析它們。  不過，hello 搜尋結果會不一致，hello 篩選結果會顯示數個事件比 hello 結果計數。  它將會驗證 hello 記錄 toodetermine 如果 hello 建立應用程式，它會造成這種行為，並盡可能建立 hello 自訂記錄檔集合定義之前解決。  
>
  
## <a name="defining-a-custom-log"></a>定義自訂記錄檔
使用下列程序 toodefine 自訂記錄檔的 hello。  如需逐步解說的範例，以新增自訂的記錄檔的這篇文章捲動 toohello 結束。

### <a name="step-1-open-hello-custom-log-wizard"></a>步驟 1. 開啟 hello 自訂記錄檔精靈
hello 自訂記錄檔精靈 hello OMS 入口網站中執行，並可讓您新的自訂記錄檔 toocollect toodefine。

1. 在 hello OMS 入口網站中，移過**設定**。
2. 按一下 [資料]，然後按一下 [自訂記錄檔]。
3. 根據預設，所有的組態變更會自動推入 tooall 代理程式。  Linux 代理程式，請傳送 toohello Fluentd 資料收集器的組態檔案。  如果您想 toomodify 手動在每個 Linux 代理程式上的這個檔案，然後取消核取方塊 hello*套用下列組態 toomy Linux 電腦*。
4. 按一下**新增 +** tooopen hello 自訂記錄檔精靈。

### <a name="step-2-upload-and-parse-a-sample-log"></a>步驟 2. 上傳和剖析範例記錄檔
您開始上傳 hello 自訂記錄檔的範例。  hello 精靈將會剖析，並顯示您 toovalidate 此檔案中的 hello 項目。  記錄分析將使用您指定 tooidentify 每一筆記錄的 hello 分隔符號。

**新的一行**為 hello 預設分隔符號，用於有單一項目，每行的記錄檔。  如果 hello 一行開頭的日期和時間，其中一種 hello 可用的格式，則您可以指定**時間戳記**支援跨越一行以上的項目分隔符號。

如果使用時間戳記分隔符號，則會與 hello 日期/時間為 hello 記錄檔中的項目指定填入 hello TimeGenerated 屬性儲存在 OMS 中的每一筆記錄。  如果使用新行的分隔符號，然後 TimeGenerated 會填入日期和時間，記錄分析會收集 hello 項目。

> [!NOTE]
> 記錄分析目前會將 hello 日期/時間從使用為 UTC 時間戳記分隔符號的記錄檔收集。  很快就會變更的 toouse hello 時區 hello 代理程式上。
>
>

1. 按一下**瀏覽**並瀏覽 tooa 範例檔案。  請注意，在某些瀏覽器中，這個按鈕可能標示為 [選擇檔案]  。
2. 按一下 [下一步] 。
3. hello 自訂記錄精靈會將上傳 hello 檔案和清單 hello 記錄，它會識別。
4. 變更是使用的 tooidentify 新記錄的 hello 分隔符號和可識別最適合您的記錄檔中的 hello 記錄選取 hello 分隔符號。
5. 按一下 [下一步] 。

### <a name="step-3-add-log-collection-paths"></a>步驟 3. 新增記錄檔收集路徑
它可以在其中尋找 hello 自訂記錄檔的 hello 代理程式上，您必須定義一個或多個路徑。  您可以提供特定路徑和名稱為 hello 記錄檔，或您可以使用萬用字元 hello 名稱指定的路徑。  這可支援每天會建立一個新檔案的應用程式或在一個檔案到達特定大小時提供支援。  您也可以為單一記錄檔提供多個路徑。

例如，應用程式可能會建立記錄檔每一天 hello 如同 log20100316.txt hello 名稱中包含的日期。 這類記錄檔的模式可能是*記錄\*.txt*會套用 tooany 遵循 hello 應用程式的記錄檔的命名配置。

hello 下表提供有效的模式範例 toospecify 不同記錄檔。

| 說明 | 路徑 |
|:--- |:--- |
| Windows 代理程式上的 *C:\Logs* 中，副檔名為 .txt 的所有檔案 |C:\Logs\\\*.txt |
| Windows 代理程式上的 *C:\Logs* 中，名稱開頭為 log 且副檔名為 .txt 的所有檔案 |C:\Logs\log\*.txt |
| Windows 代理程式上的 */var/log/audit* 中副檔名為 .txt 的所有檔案 |/var/log/audit/*.txt |
| Linux 代理程式上的 */var/log/audit* 中，名稱開頭為 log 且副檔名為 .txt 的所有檔案 |/var/log/audit/log\*.txt |

1. 選取您要加入其中的路徑格式的 Windows 或 Linux toospecify。
2. 輸入 hello 路徑中，按一下 [hello  **+**  ] 按鈕。
3. 任何其他路徑重複 hello 程序。

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a>步驟 4. 提供的名稱和描述 hello 記錄檔
hello 您指定的名稱將用於 hello 記錄類型 （如上所述）。  它最後一定會與 _CL toodistinguish 它做為自訂的記錄檔。

1. 輸入 hello 記錄檔的名稱。  hello  **\_CL**會自動被賦予後置詞。
2. 新增選擇性的 [描述] 。
3. 按一下**下一步**toosave hello 自訂記錄檔定義。

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a>步驟 5。 驗證所要收集 hello 自訂記錄檔
它可能會佔用 tooan 小時從新的自訂記錄檔 tooappear 記錄分析中的 hello 初始資料。  它會開始收集項目從 hello 記錄檔路徑中找到 hello 從 hello 點指定該您定義的 hello 自訂記錄檔。  它將不會保留您上傳 hello 自訂記錄檔建立期間的 hello 項目，但它會收集 hello 找到的記錄檔中的現有項目。

一旦記錄分析會開始收集從 hello 自訂記錄檔，其記錄將會提供記錄搜尋。  使用您提供給 hello hello 做的自訂記錄檔的 hello 名稱**類型**在查詢中。

> [!NOTE]
> 如果遺漏從 hello 搜尋 hello RawData 屬性，您可能需要 tooclose，並重新開啟您的瀏覽器。
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a>步驟 6. 剖析 hello 自訂記錄項目
hello 整個記錄檔項目會儲存在單一屬性呼叫**RawData**。  您最有可能會想 tooseparate hello 不同資訊片段中每個項目插入儲存在 hello 記錄中的個別屬性。  您使用 hello[自訂欄位](log-analytics-custom-fields.md)記錄分析的功能。

這裡不會提供詳細的步驟，以剖析 hello 自訂記錄項目。  請參閱 toohello[自訂欄位](log-analytics-custom-fields.md)這項資訊的文件。

## <a name="disabling-a-custom-log"></a>停用自訂記錄檔
自訂記錄檔定義一旦建立就無法移除，但您可以移除其所有集合路徑來停用它。

1. 在 hello OMS 入口網站中，移過**設定**。
2. 按一下 [資料]，然後按一下 [自訂記錄檔]。
3. 按一下**詳細資料**下一步 toohello 自訂記錄檔定義 toodisable。
4. 移除每個 hello 自訂記錄檔定義的 hello 集合路徑。

## <a name="data-collection"></a>資料收集
Log Analytics 會從每個自訂記錄檔收集新的項目，間隔大約為每 5 分鐘。  hello 代理程式將會收集每個記錄檔中記錄其所在位置。  如果 hello 代理程式離線一段時間，然後記錄分析將收集項目從其上次離開的地方，即使那些項目在 hello agent 離線期間所建立。

hello hello 記錄項目整個內容寫入 tooa 單一屬性呼叫**RawData**。  您可以將此剖析成多個屬性，進行分析及藉由定義分別搜尋[自訂欄位](log-analytics-custom-fields.md)建立 hello 自訂記錄檔之後。

## <a name="custom-log-record-properties"></a>自訂記錄檔記錄的屬性
自訂記錄檔記錄都有您所提供和 hello hello 下表中的屬性 hello 記錄檔名稱的型別。

| 屬性 | 說明 |
|:--- |:--- |
| TimeGenerated |日期和時間 hello 記錄已分析所收集的記錄檔。  如果 hello 記錄檔會使用以時間為基礎的分隔符號這是從 hello 項目收集的 hello 時間。 |
| SourceSystem |從收集的代理程式 hello 記錄類型。 <br> OpsManager - Windows 代理程式，直接連線或由 System Center Operations Manager 管理 <br> Linux – 所有的 Linux 代理程式 |
| RawData |全文檢索的 hello 收集項目。 |
| ManagementGroupName |System Center Operations Manage agents hello 管理群組名稱。  若為其他代理程式，此為 AOI-\<工作區 ID\> |

## <a name="log-searches-with-custom-log-records"></a>使用自訂記錄檔記錄來記錄搜尋
從自訂的記錄檔的記錄會儲存在 hello OMS 儲存機制，就像任何其他資料來源的記錄。  這些使用者必須符合您提供當您定義 hello 記錄檔中，因此您可以使用 hello 類型屬性搜尋 tooretrieve 記錄收集從特定的記錄檔中的 hello 名稱的類型。

hello 下表提供的自訂記錄檔從擷取記錄的記錄搜尋不同的範例。

| 查詢 | 說明 |
|:--- |:--- |
| Type=MyApp_CL |所有事件來自名為 MyApp_CL 的自訂記錄檔。 |
| Type=MyApp_CL Severity_CF=error |來自 MyApp_CL 自訂記錄檔且在 *Severity_CF* 自訂欄位中的值為 *error* 的所有事件。 |

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。

> | 查詢 | 說明 |
|:--- |:--- |
| MyApp_CL |所有事件來自名為 MyApp_CL 的自訂記錄檔。 |
| MyApp_CL &#124; where Severity_CF=="error" |來自 MyApp_CL 自訂記錄檔且在 *Severity_CF* 自訂欄位中的值為 *error* 的所有事件。 |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>新增自訂記錄檔的範例逐步解說
hello 下一節逐步解說建立自訂的記錄檔的範例。  hello 範例記錄檔收集對每一行開頭的日期和時間，並接著以逗號分隔的程式碼、 狀態及訊息欄位的單一項目。  下面顯示了幾個範例項目。

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a>上傳和剖析範例記錄檔
我們提供一個 hello 記錄檔，可以看到 hello 將收集的事件。  在此案例中，新行字元足以做為分隔符號。  如果 hello 記錄檔中的單一項目無法透過跨越多行，則時間戳記分隔符號需要 toobe 使用。

![上傳和剖析範例記錄檔](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>新增記錄檔收集路徑
hello 記錄檔會位於*C:\MyApp\Logs*。  包含 hello 日期 hello 模式中的名稱與每一天會建立新的檔案*appYYYYMMDD.log*。  此記錄檔的完整模式為 *C:\MyApp\Logs\\\*.log*。

![記錄檔收集路徑](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a>提供的名稱和描述 hello 記錄檔
我們使用 *MyApp_CL* 這個名稱並輸入 [描述]。

![記錄檔名稱](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a>驗證所要收集 hello 自訂記錄檔
我們使用的查詢*類型 = MyApp_CL* tooreturn 所有記錄從 hello 收集的記錄。

![無自訂欄位的記錄檔查詢](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a>剖析 hello 自訂記錄項目
我們使用自訂欄位 toodefine hello *EventTime*，*程式碼*，*狀態*，和*訊息*欄位，而且我們可以看到 hello hello 差異hello 查詢所傳回的記錄。

![有自訂欄位的記錄檔查詢](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>後續步驟
* 使用[自訂欄位](log-analytics-custom-fields.md)tooparse hello hello tooindividual 欄位中的自訂記錄項目。
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。
