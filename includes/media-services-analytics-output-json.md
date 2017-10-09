hello 作業產生的 JSON 輸出檔案，其中包含有關偵測到並追蹤所面臨的中繼資料。 hello 中繼資料包括指出 hello 位置的表面，以及朝識別碼數字表示 hello 追蹤個別的座標。 字體識別碼時情況下的很容易出錯 tooreset hello 人臉正面遺失或重疊在 hello 框架內，導致指派多個識別碼的某些個人。

hello 輸出 JSON 包含下列屬性的 hello:

| 元素 | 說明 |
| --- | --- |
| 版本 |這是指 toohello 版的 hello 視訊應用程式開發介面。 |
| index | （適用於僅 tooAzure 媒體 Redactor） 定義 hello hello 目前事件的框架索引。 |
| timescale |「 滴答 」 每秒的 hello 視訊。 |
| Offset |這是時間戳記的 hello 時間位移。 在版本 1.0 的影片 API 中，這永遠會是 0。 在我們於未來將支援的案例中，此值可能會變更。 |
| framerate |每秒的 hello 視訊畫面。 |
| fragments |到不同的區段，稱為片段 hello 中繼資料區塊上處理。 每個片段皆包含開始、持續時間、間隔數字及事件。 |
| start |hello 的開始時間 hello 「 刻度 」 中的第一個事件。 |
| duration |在 「 滴答 」 hello 片段 hello 長度。 |
| interval |hello 間隔在 「 滴答 」 中的 hello 片段內的每個事件項目。 |
| 活動 |每個事件包含 hello 字體偵測到與該持續時間內追蹤。 它是個包含事件之陣列的陣列。 hello 外部陣列都代表一個時間間隔。 hello 內部陣列包含 0 或更多時間中該時間點所發生的事件。 空白的括號 [] 代表沒有偵測到臉部。 |
| id |正在追蹤的 hello 字體 hello 識別碼。 如果該臉部變成無法被偵測，這個號碼可能會在無意中變更。 指定的個別應該具有相同識別碼 hello 整體視訊，整個 hello，但這不一定能應付 toolimitations hello 偵測演算法 （阻擋等等） 中 |
| x, y |hello 左上方 X 和 Y 座標 hello 面對 0.0 too1.0 中正規化的小數位數週框方塊。 <br/>-X 和 Y 座標都相對 toolandscape，因此如果您有簡介視訊 （或顛倒，iOS hello 案例），您將據此可 tootranspose hello 座標。 |
| 寬度，高度 |hello 寬度和高度 hello 面對 0.0 too1.0 中正規化的小數位數週框方塊。 |
| facesDetected |這位於 hello hello JSON 結果的結尾，並摘要說明的表面 hello 數目 hello 視訊期間偵測到該 hello 演算法。 因為 hello 識別碼可以重設不小心如果圖示會變成未偵測到 （例如朝當畫面上，尋找立即關閉），這個數字可能不一定等於 hello 字體 hello 影片數目，則為 true。 |

