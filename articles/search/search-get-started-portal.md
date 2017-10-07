---
標題： aaa 」 教學課程： hello 入口網站中建立第一個的 Azure 搜尋索引 |Microsoft 文件"描述： hello Azure 入口網站，在使用預先定義的範例資料 toogenerate 索引。 探索全文檢索搜尋、篩選器、面向、模糊搜尋、地理搜尋功能等等。
服務： 搜尋 documentationcenter: '作者： HeidiSteen 管理員： jhubbard 編輯器:' 標記： azure 入口網站

ms.assetid: 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service： 搜尋 ms.devlang: na ms.workload： 搜尋 ms.topic： 英雄文章 ms.tgt_pltfrm: na ms.date: 06/26/2017 ms.author: heidist

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a>教學課程： Hello 入口網站中建立第一個的 Azure 搜尋索引

在 hello Azure 入口網站，開始使用預先定義的範例資料集 tooquickly 產生使用 hello 索引**匯入資料**精靈。 使用**搜尋總管**探索全文檢索搜尋、篩選器、面向、模糊搜尋和地理搜尋功能。  

此無程式碼的簡介，讓您從預先定義的資料著手，以便立即撰寫有趣的查詢。 雖然入口網站工具無法取代程式碼，但很適合用於下列工作︰

+ 產品量產時間最短的實際操作學習
+ 在 [匯入資料] 中撰寫程式碼前，先設定索引的原型
+ 在 [搜尋總管] 中測試查詢和剖析器語法
+ 檢視現有的索引已發行的 tooyour 服務並尋找其屬性

**估計時間︰**大約 15 分鐘，但如果還需要註冊帳戶或服務，則時間較長。 

或者，使用專業[Azure 搜尋.NET 中的程式碼為基礎的簡介 tooprogramming](search-howto-dotnet-sdk.md)。

## <a name="prerequisites"></a>必要條件

本教學課程會採用 [Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)和 [Azure 搜尋服務](search-create-service-portal.md)。 

如果您不立即想 tooprovision 服務，您可以觀看的 hello 6 分鐘示範的步驟在本教學課程中，開始三分鐘到這個[Azure Search 概觀影片](https://channel9.msdn.com/Events/Connect/2016/138)。

## <a name="find-your-service"></a>尋找您的服務
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 開啟您的 Azure 搜尋服務的 hello 服務儀表板。 如果您未釘選 hello 服務磚 tooyour 儀表板，您可以找到您的服務在這種方式： 
   
   * 在 hello Jumpbar，按一下 **更多服務**在 hello hello 左側瀏覽窗格的底部。
   * 在 [hello] 搜尋方塊中，輸入*搜尋*tooget 訂用帳戶服務的搜尋清單。 Hello 清單應會顯示您的服務。 

## <a name="check-for-space"></a>檢查空間
許多客戶開始 hello 免費服務。 這個版本是有限的 toothree 索引、 三個資料來源，以及三個索引子。 開始之前，請先確定您有空間可容納額外的項目。 本教學課程會建立各一個物件。 

> [!TIP] 
> Hello 服務儀表板上的磚會顯示多少索引、 索引子和資料來源您已經有。 hello 索引子的磚會顯示成功和失敗的指標。 按一下 hello 磚 tooview hello 索引子計數。 
>
> ![索引子和資料來源的圖格][1]
>

## <a name="create-index"></a> 建立索引和載入資料
搜尋查詢會逐一查看索引  ，其中包含用來最佳化特定搜尋行為的可搜尋資料、中繼資料及建構。

tookeep 這個入口網站為基礎的工作中，我們會使用內建的範例資料集可以使用索引子透過 hello 編目**匯入資料**精靈。 

#### <a name="step-1-start-hello-import-data-wizard"></a>步驟 1： 啟動 hello 匯入資料精靈
1. Azure 搜尋服務儀表板上，按一下 **匯入資料**hello 命令列 toostart 精靈，同時建立並填入索引中。
   
    ![匯入資料命令][2]

2. 在 hello 精靈 中，按一下 **資料來源** > **範例** > **realestate-我們為範例**。 此資料來源已預先設定名稱、類型和連線資訊。 一旦建立，就會變成可在其他匯入作業中重複使用的「現有資料來源」。

    ![選取範例資料集][9]

3. 按一下**確定**toouse 它。

#### <a name="step-2-define-hello-index"></a>步驟 2： 定義 hello 索引
建立索引通常會是手動和程式碼為基礎，但 hello 精靈可能會產生任何資料來源，它可以搜耙的索引。 至少具有一個欄位標示為 hello 文件索引鍵 toouniquely 識別每個文件，索引需要名稱和欄位集合。

欄位具有資料類型和屬性。 hello hello 頂端的核取方塊是*屬性索引*控制 hello 欄位的使用方式。 

*  表示它會出現在搜尋結果清單中。 例如當欄位僅使用於篩選運算式時，您可以清除此核取方塊，將個別欄位標記為關閉搜尋結果的限制。 
* [可篩選]、[可排序] 和 [可面向化] 判斷欄位是否可以用於篩選、排序或多面向導覽結構。 
*  表示欄位包含在全文檢索搜尋中。 字串可以搜尋。 數字欄位和布林值欄位通常會標示為不可搜尋。 

根據預設，hello 精靈會掃描為 hello 索引鍵欄位的 hello 基礎 hello 資料來源的唯一識別碼。 字串具有可擷取和可搜尋的特性。 整數具有可擷取、可篩選、可排序和可 Fact 處理的特性。

  ![產生的 realestate 索引][3]

按一下**確定**toocreate hello 索引。

#### <a name="step-3-define-hello-indexer"></a>步驟 3： 定義 hello 索引子
仍在 hello**匯入資料**精靈] 中，按一下 [**索引子** > **名稱**，然後輸入 hello 索引子的名稱。 

此物件定義可執行的程序。 您無法將它放循環的排程，但現在使用 hello 預設選項 toorun hello 索引子之後立即，當您按一下**確定**。  

  ![realestate 索引子][8]

## <a name="check-progress"></a>檢查進度
toomonitor 資料匯入，請返回 toohello 服務儀表板、 向下捲動並按兩下 hello**索引子**並排 tooopen hello 索引子清單。 您應該會看見 hello 新建立的索引子，在 [hello] 清單中，並提供狀態，指出 「 進行中 」 或成功的原因，以及 hello 編製索引的文件的數目。

   ![索引子進度訊息][4]

## <a name="query-index"></a>查詢 hello 索引
您現在可以準備 tooquery 搜尋索引。 **搜尋總管**是 hello 入口網站內建查詢工具。 它會提供搜尋方塊，以便確認搜尋結果是否如您所預期。 

> [!TIP]
> 在 hello [Azure Search 概觀影片](https://channel9.msdn.com/Events/Connect/2016/138)，hello 步驟會示範在 6m08s hello 影片。
>

1. 按一下**搜尋總管**hello 命令列上。

   ![搜尋總管命令][5]

2. 按一下**變更索引**上 hello 命令列 tooswitch 太*realestate-我們為範例*。

   ![索引和 API 命令][6]

3. 按一下**設定 API 版本**hello REST Api 可用的命令列 toosee 上。 預覽應用程式開發介面可讓您存取 toonew 功能通常尚未發行。 除非另有指示 hello 查詢下方，使用 hello 上市版 (2016年-09-01)。 

    > [!NOTE]
    > [Azure 搜尋 REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents)和 hello [.NET 程式庫](search-howto-dotnet-sdk.md#core-scenarios)完全相同，但**搜尋總管**是配備的 toohandle REST 呼叫。 它可接受兩個語法[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)和[完整 Lucene 查詢剖析器](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)，加上所有 hello 中可用的搜尋參數[搜尋文件](https://docs.microsoft.com/rest/api/searchservice/search-documents)作業。
    > 

4. 在 hello 搜尋列中，輸入以下的 hello 查詢字串，然後按一下**搜尋**。

  ![搜尋查詢範例][7]

**`search=seattle`**

+ hello`search`參數是使用的 tooinput 關鍵字搜尋的全文檢索搜尋，在此情況下，傳回在國王郡，華盛頓州的清單，其中包含*西雅圖*hello 文件中任何可搜尋的欄位。 

+ **搜尋總管**會傳回結果在 JSON 中，這是詳細資訊和固定 tooread 文件有密集的結構。 根據您的文件，您可能需要 toowrite 程式碼控制代碼搜尋結果 tooextract 重要的項目。 

+ 文件所組成標示為可擷取 hello 索引中的所有欄位。 tooview 索引屬性，在 hello 入口網站按一下*realestate-我們為範例*在 hello**索引**磚。

**`search=seattle&$count=true&$top=100`**

+ hello`&`符號就是使用的 tooappend 搜尋參數，可以依照任何順序指定。 

+  hello`$count=true`參數會傳回所有傳回的文件的 hello 總和的計數。 您可以藉由監視 `$count=true` 所報告的變更來驗證篩選查詢。 

+ hello`$top=100`傳回 hello 最高排名 hello 總計超出 100 文件。 根據預設，Azure 搜尋會傳回 hello 前 50 個最符合項目。 您可以增加或減少從傳送嗨量`$top`。

**`search=*&facet=city&$top=2`**

+ `search=*` 是空的搜尋。 空的搜尋會搜尋所有一切。 送出空的查詢太篩選器或 facet hello 完整資料集的文件的其中一個原因。 例如，您會想 hello 索引中的所有城市 faceting 導覽結構 tooconsist。

+  `facet`瀏覽傳回結構，您可以將 tooa UI 控制項。 它會傳回一些類別和一個計數。 在此情況下，類別根據 hello 數字的城市。 在 Azure 搜尋服務中沒有彙總功能，但您可以透過 `facet` 模擬彙總，其可提供各類別中的文件計數。

+ `$top=2`取回兩份文件，說明您可以使用`top`tooboth 減少或增加結果。

**`search=seattle&facet=beds`**

+ 此查詢是 beds 的面向，以 Seattle 的文字搜尋為基礎。 `"beds"`指定 facet hello 欄位會標示為可擷取、 可篩選，因此可進行 facet 處理 hello 索引和 hello 值它包含 （數字，1 到 5）、 適用於分類成群組 （3 房間，4 個房間的清單） 的清單。 

+ 只有可篩選的欄位可以面向化。 只有可擷取的欄位可以傳回 hello 結果中。

**`search=seattle&$filter=beds gt 3`**

+ hello`filter`參數會傳回符合您所提供的 hello 準則的結果。 在此情況下，房間大於 3 間。 

+ 篩選語法是 OData 建構。 如需詳細資訊，請參閱[篩選 OData 語法](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)。

**`search=granite countertops&highlight=description`**

+ 叫用的反白顯示參考 tooformatting 文字上比對 hello 關鍵字指定相符項目中找到特定的欄位。 如果您的搜尋字詞深埋在描述中，您可以加入叫用的反白顯示 toomake 它更容易 toospot。 在此情況下，hello 格式化片語`"granite countertops"`是更容易 toosee hello 描述欄位中的。

**`search=mice&highlight=description`**

+ 全文檢索搜尋會尋找具有類似語意的文字形式。 在此情況下，搜尋結果會包含"mouse"，"mice"的回應 tooa 關鍵字搜尋中的滑鼠侵擾家庭的反白顯示的文字。 不同的形式的 hello 相同字組可以出現在結果，因為語言分析。 

+ Azure 搜尋服務支援 Microsoft 和 Lucene 所提供的 56 個分析器。 使用 Azure 搜尋的 hello 預設值為 hello 標準 Lucene 分析器。 

**`search=samamish`**

+ 拼錯的字，例如 'samamish' hello Samammish 高原 hello 西雅圖地區的失敗 tooreturn 符合項目在一般搜尋。 toohandle 拼字錯誤，您可以使用模糊的搜尋，hello 下一個範例中所述。

**`search=samamish~&queryType=full`**

+ 當您指定 hello 啟用模糊搜尋`~`符號，然後使用 hello 完整查詢剖析器，它會解譯及正確剖析 hello`~`語法。 

+ 模糊的搜尋時，使用您選擇進行設定時，就會發生的 hello 完整查詢剖析器`queryType=full`。 如需啟用 hello 完整查詢剖析器查詢案例的詳細資訊，請參閱[Lucene 的查詢語法，在 Azure 搜尋](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)。

+ 當`queryType`是未指定，會使用 hello 預設簡單查詢剖析器。 hello 簡單查詢剖析器還快，但是如果您需要模糊的搜尋、 規則運算式、 鄰近搜尋或其他進階的查詢類型，您將需要 hello 完整的語法。 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ 透過 hello 支援地理空間搜尋[edm。GeographyPoint 資料型別](https://docs.microsoft.com/rest/api/searchservice/supported-data-types)上包含座標的欄位。 地理搜尋是在[篩選 OData 語法](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)中指定的一種篩選器。 

+ hello 範例查詢會篩選其中結果是少於 5 公里從指定的點 （指定為緯度和經度座標） 位置的資料的所有結果。 藉由新增`$count`，您可以查看變更 hello 距離或 hello 座標時，會傳回多少的結果。 

+ 如果搜尋應用程式有「尋找附近地點」功能或使用地圖導航功能，地理空間搜尋便很實用。 不過，並不是全文檢索搜尋。 如果您有依名稱搜尋上縣市或國家/地區的使用者需求，加入包含縣市或國家/地區中的名稱，加法 toocoordinates 欄位。

## <a name="next-steps"></a>後續步驟

+ 修改任何 hello 您剛才建立的物件。 您一次執行 hello 精靈之後，您可以返回並檢視或修改個別元件： 索引、 索引子或資料來源。 Hello 索引上不允許某些編輯，例如 hello 變更 hello 欄位資料型別，但大部分的屬性和設定是可修改。

  tooview 個別元件，按一下 hello**索引**，**索引子**，或**資料來源**磚的儀表板 toodisplay 上現有的物件清單。 toolearn 深入了解索引編輯不需要重建，請參閱[更新索引 (Azure 搜尋 REST API)](https://docs.microsoft.com/rest/api/searchservice/update-index)。

+ Hello 工具和其他資料來源的步驟，再試一次。 hello 範例資料集， `realestate-us-sample`，是從 Azure SQL Database 的 Azure 搜尋可以搜耙。 除了 Azure SQL Database，Azure 搜尋服務可以從 Azure 表格儲存體、Blob 儲存體、Azure VM 上的 SQL Server 及 Azure Cosmos DB 中的一般資料結構搜耙及推斷索引。 Hello 精靈 中，都支援所有的這些資料來源。 在程式碼中，您可以使用「索引子」輕鬆地填入索引。

+ 透過推入模型，您程式碼將推入新的位置，並變更 JSON tooyour 索引中的資料列集支援的所有其他非索引子資料來源。 如需詳細資訊，請參閱[在 Azure 搜尋服務中新增、更新或刪除文件](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents)。

若要深入了解本文提到的其他功能，請造訪下列連結︰

* [索引子概觀](search-indexer-overview.md)
* [建立的索引 （包括 hello 索引屬性的詳細的說明）](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [搜尋總管](search-explorer.md)
* [搜尋文件 (包含查詢語法範例)](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png