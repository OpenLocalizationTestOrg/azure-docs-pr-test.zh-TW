## <a name="specifying-formats"></a><span data-ttu-id="01dcd-101">指定格式</span><span class="sxs-lookup"><span data-stu-id="01dcd-101">Specifying formats</span></span>
<span data-ttu-id="01dcd-102">Azure Data Factory 支援下列格式類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="01dcd-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="01dcd-103">文字格式</span><span class="sxs-lookup"><span data-stu-id="01dcd-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="01dcd-104">JSON 格式</span><span class="sxs-lookup"><span data-stu-id="01dcd-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="01dcd-105">Avro 格式</span><span class="sxs-lookup"><span data-stu-id="01dcd-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="01dcd-106">ORC 格式</span><span class="sxs-lookup"><span data-stu-id="01dcd-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="01dcd-107">Parquet 格式</span><span class="sxs-lookup"><span data-stu-id="01dcd-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="01dcd-108">指定 TextFormat</span><span class="sxs-lookup"><span data-stu-id="01dcd-108">Specifying TextFormat</span></span>
<span data-ttu-id="01dcd-109">如果您想 tooparse hello 文字檔案，或以文字格式寫入 hello 資料，設定 hello `format` `type`屬性太**TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="01dcd-110">您也可以指定下列 hello**選擇性**屬性在 hello `format` > 一節。</span><span class="sxs-lookup"><span data-stu-id="01dcd-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="01dcd-111">請參閱[TextFormat 範例](#textformat-example)> 一節有關 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="01dcd-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="01dcd-112">屬性</span><span class="sxs-lookup"><span data-stu-id="01dcd-112">Property</span></span> | <span data-ttu-id="01dcd-113">說明</span><span class="sxs-lookup"><span data-stu-id="01dcd-113">Description</span></span> | <span data-ttu-id="01dcd-114">允許的值</span><span class="sxs-lookup"><span data-stu-id="01dcd-114">Allowed values</span></span> | <span data-ttu-id="01dcd-115">必要</span><span class="sxs-lookup"><span data-stu-id="01dcd-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="01dcd-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="01dcd-116">columnDelimiter</span></span> |<span data-ttu-id="01dcd-117">hello 字元會在檔案中，使用 tooseparate 資料行。</span><span class="sxs-lookup"><span data-stu-id="01dcd-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="01dcd-118">您可以考慮 toouse 罕見的不可列印字元可能不存在您的資料： 例如指定"\u0001"表示開始的標題 (SOH)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="01dcd-119">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="01dcd-119">Only one character is allowed.</span></span> <span data-ttu-id="01dcd-120">hello**預設**值是**逗號 （'，'）**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="01dcd-121">toouse 使用 Unicode 字元，請參閱太[Unicode 字元](https://en.wikipedia.org/wiki/List_of_Unicode_characters)tooget hello 為其對應的程式碼。</span><span class="sxs-lookup"><span data-stu-id="01dcd-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="01dcd-122">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-122">No</span></span> |
| <span data-ttu-id="01dcd-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="01dcd-123">rowDelimiter</span></span> |<span data-ttu-id="01dcd-124">hello 字元用於 tooseparate 資料列檔案中。</span><span class="sxs-lookup"><span data-stu-id="01dcd-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="01dcd-125">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="01dcd-125">Only one character is allowed.</span></span> <span data-ttu-id="01dcd-126">hello**預設**值可以是任何 hello 讀取下列值： **["\r\n"、"\r"、"\n"]**和**"\r\n"**寫入。</span><span class="sxs-lookup"><span data-stu-id="01dcd-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="01dcd-127">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-127">No</span></span> |
| <span data-ttu-id="01dcd-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="01dcd-128">escapeChar</span></span> |<span data-ttu-id="01dcd-129">hello 特殊字元都使用資料行分隔符號 tooescape hello 內容的輸入檔中。</span><span class="sxs-lookup"><span data-stu-id="01dcd-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="01dcd-130">您無法同時為資料表指定 escapeChar 和 quoteChar。</span><span class="sxs-lookup"><span data-stu-id="01dcd-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="01dcd-131">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="01dcd-131">Only one character is allowed.</span></span> <span data-ttu-id="01dcd-132">沒有預設值。</span><span class="sxs-lookup"><span data-stu-id="01dcd-132">No default value.</span></span> <br/><br/><span data-ttu-id="01dcd-133">範例： 如果您以逗號 （'，'） hello 資料行分隔符號，但您想要以 hello 文字 toohave hello 逗號字元 (範例:"Hello，world")，您可以定義為 hello 逸出字元 '$'，並使用字串"Hello$，world hello 來源中。</span><span class="sxs-lookup"><span data-stu-id="01dcd-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="01dcd-134">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-134">No</span></span> |
| <span data-ttu-id="01dcd-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="01dcd-135">quoteChar</span></span> |<span data-ttu-id="01dcd-136">hello 字元使用 tooquote 字串值。</span><span class="sxs-lookup"><span data-stu-id="01dcd-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="01dcd-137">hello hello 引號字元內的資料行和資料列分隔符號會視為 hello 字串值的一部分。</span><span class="sxs-lookup"><span data-stu-id="01dcd-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="01dcd-138">這個屬性是適用於 tooboth 輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="01dcd-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="01dcd-139">您無法同時為資料表指定 escapeChar 和 quoteChar。</span><span class="sxs-lookup"><span data-stu-id="01dcd-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="01dcd-140">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="01dcd-140">Only one character is allowed.</span></span> <span data-ttu-id="01dcd-141">沒有預設值。</span><span class="sxs-lookup"><span data-stu-id="01dcd-141">No default value.</span></span> <br/><br/><span data-ttu-id="01dcd-142">比方說，如果您以逗號 （'，'） hello 資料行分隔符號，但您想要以 hello 文字 toohave 逗號字元 (範例： < Hello，world >)，您可以定義"（雙引號） hello 引號字元，並使用 hello 字串"Hello，world"hello 來源中。</span><span class="sxs-lookup"><span data-stu-id="01dcd-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="01dcd-143">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-143">No</span></span> |
| <span data-ttu-id="01dcd-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="01dcd-144">nullValue</span></span> |<span data-ttu-id="01dcd-145">Toorepresent null 值使用一或多個字元。</span><span class="sxs-lookup"><span data-stu-id="01dcd-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="01dcd-146">一或多個字元。</span><span class="sxs-lookup"><span data-stu-id="01dcd-146">One or more characters.</span></span> <span data-ttu-id="01dcd-147">hello**預設**有效值**"\N"和"NULL"**在讀取和**"\N"**寫入。</span><span class="sxs-lookup"><span data-stu-id="01dcd-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="01dcd-148">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-148">No</span></span> |
| <span data-ttu-id="01dcd-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="01dcd-149">encodingName</span></span> |<span data-ttu-id="01dcd-150">指定 hello 編碼名稱。</span><span class="sxs-lookup"><span data-stu-id="01dcd-150">Specify hello encoding name.</span></span> |<span data-ttu-id="01dcd-151">有效的編碼名稱。</span><span class="sxs-lookup"><span data-stu-id="01dcd-151">A valid encoding name.</span></span> <span data-ttu-id="01dcd-152">請參閱 [Encoding.EncodingName 屬性](https://msdn.microsoft.com/library/system.text.encoding.aspx)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="01dcd-153">例如：windows-1250 或 shift_jis。</span><span class="sxs-lookup"><span data-stu-id="01dcd-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="01dcd-154">hello**預設**值是**utf-8**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="01dcd-155">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-155">No</span></span> |
| <span data-ttu-id="01dcd-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="01dcd-156">firstRowAsHeader</span></span> |<span data-ttu-id="01dcd-157">指定是否 tooconsider hello 做為標頭的第一個資料列。</span><span class="sxs-lookup"><span data-stu-id="01dcd-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="01dcd-158">對於輸入資料集，Data Factory 會讀取第一個資料列做為標頭。</span><span class="sxs-lookup"><span data-stu-id="01dcd-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="01dcd-159">對於輸出資料集，Data Factory 會寫入第一個資料列做為標頭。</span><span class="sxs-lookup"><span data-stu-id="01dcd-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="01dcd-160">相關範例案例請參閱[使用 `firstRowAsHeader` 和 `skipLineCount` 的案例](#scenarios-for-using-firstrowasheader-and-skiplinecount)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="01dcd-161">True</span><span class="sxs-lookup"><span data-stu-id="01dcd-161">True</span></span><br/><span data-ttu-id="01dcd-162">**False (預設值)**</span><span class="sxs-lookup"><span data-stu-id="01dcd-162">**False (default)**</span></span> |<span data-ttu-id="01dcd-163">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-163">No</span></span> |
| <span data-ttu-id="01dcd-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="01dcd-164">skipLineCount</span></span> |<span data-ttu-id="01dcd-165">從輸入檔讀取資料時，表示 hello tooskip 資料列數目。</span><span class="sxs-lookup"><span data-stu-id="01dcd-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="01dcd-166">如果未指定 skipLineCount 和 firstRowAsHeader，hello 線條會略過第一次，並 hello 標頭資訊從 hello 輸入檔讀取。</span><span class="sxs-lookup"><span data-stu-id="01dcd-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="01dcd-167">相關範例案例請參閱[使用 `firstRowAsHeader` 和 `skipLineCount` 的案例](#scenarios-for-using-firstrowasheader-and-skiplinecount)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="01dcd-168">Integer</span><span class="sxs-lookup"><span data-stu-id="01dcd-168">Integer</span></span> |<span data-ttu-id="01dcd-169">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-169">No</span></span> |
| <span data-ttu-id="01dcd-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="01dcd-170">treatEmptyAsNull</span></span> |<span data-ttu-id="01dcd-171">指定是否 tootreat null 或空字串，以 null 值時從輸入檔讀取資料。</span><span class="sxs-lookup"><span data-stu-id="01dcd-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="01dcd-172">**True (預設值)**</span><span class="sxs-lookup"><span data-stu-id="01dcd-172">**True (default)**</span></span><br/><span data-ttu-id="01dcd-173">False</span><span class="sxs-lookup"><span data-stu-id="01dcd-173">False</span></span> |<span data-ttu-id="01dcd-174">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="01dcd-175">TextFormat 範例</span><span class="sxs-lookup"><span data-stu-id="01dcd-175">TextFormat example</span></span>
<span data-ttu-id="01dcd-176">hello 下列範例顯示 hello 格式內容的某些 TextFormat。</span><span class="sxs-lookup"><span data-stu-id="01dcd-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="01dcd-177">toouse`escapeChar`而不是`quoteChar`，取代與 hello 一行`quoteChar`以下列的 escapeChar hello:</span><span class="sxs-lookup"><span data-stu-id="01dcd-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="01dcd-178">使用 firstRowAsHeader 和 skipLineCount 的案例</span><span class="sxs-lookup"><span data-stu-id="01dcd-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="01dcd-179">您要從非檔案來源 tooa 文字檔案複製，並希望 tooadd 包含 hello 結構描述中繼資料標頭的資料行 (例如： SQL 結構描述)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="01dcd-180">指定`firstRowAsHeader`hello 輸出資料集，在此案例中為 true。</span><span class="sxs-lookup"><span data-stu-id="01dcd-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="01dcd-181">您要從文字檔，其中包含的標頭列 tooa 非檔案接收複製，而且想要線條的 toodrop。</span><span class="sxs-lookup"><span data-stu-id="01dcd-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="01dcd-182">指定`firstRowAsHeader`hello 輸入資料集，則為 true。</span><span class="sxs-lookup"><span data-stu-id="01dcd-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="01dcd-183">您要複製的文字檔案，並想 tooskip hello 開頭沒有包含任何資料或標頭資訊的幾行。</span><span class="sxs-lookup"><span data-stu-id="01dcd-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="01dcd-184">指定`skipLineCount`tooindicate hello 數行 toobe 略過。</span><span class="sxs-lookup"><span data-stu-id="01dcd-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="01dcd-185">如果 hello 檔案的其餘部分 hello 包含標頭行，您也可以指定`firstRowAsHeader`。</span><span class="sxs-lookup"><span data-stu-id="01dcd-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="01dcd-186">如果兩個`skipLineCount`和`firstRowAsHeader`和指定的會先略過 hello 行 hello 標頭資訊然後讀取 hello 輸入檔</span><span class="sxs-lookup"><span data-stu-id="01dcd-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="01dcd-187">指定 JsonFormat</span><span class="sxs-lookup"><span data-stu-id="01dcd-187">Specifying JsonFormat</span></span>
<span data-ttu-id="01dcd-188">太**匯入/匯出 JSON 檔案儲存為-至 / 從 Azure Cosmos DB**，請參閱[匯入/匯出 JSON 文件](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents)hello Azure Cosmos DB 連接器與詳細資料 > 一節。</span><span class="sxs-lookup"><span data-stu-id="01dcd-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="01dcd-189">如果您想 tooparse hello JSON 檔案，或將 JSON 格式寫入 hello 資料，設定 hello `format` `type`屬性太**JsonFormat**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="01dcd-190">您也可以指定下列 hello**選擇性**屬性在 hello `format` > 一節。</span><span class="sxs-lookup"><span data-stu-id="01dcd-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="01dcd-191">請參閱[JsonFormat 範例](#jsonformat-example)> 一節有關 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="01dcd-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="01dcd-192">屬性</span><span class="sxs-lookup"><span data-stu-id="01dcd-192">Property</span></span> | <span data-ttu-id="01dcd-193">說明</span><span class="sxs-lookup"><span data-stu-id="01dcd-193">Description</span></span> | <span data-ttu-id="01dcd-194">必要</span><span class="sxs-lookup"><span data-stu-id="01dcd-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="01dcd-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="01dcd-195">filePattern</span></span> |<span data-ttu-id="01dcd-196">表示 hello 模式，每個 JSON 檔案中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="01dcd-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="01dcd-197">允許的值為︰**setOfObjects** 和 **arrayOfObjects**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="01dcd-198">hello**預設**值是**setOfObjects**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="01dcd-199">關於這些模式的詳細資訊，請參閱 [JSON 檔案模式](#json-file-patterns)一節。</span><span class="sxs-lookup"><span data-stu-id="01dcd-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="01dcd-200">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-200">No</span></span> |
| <span data-ttu-id="01dcd-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="01dcd-201">jsonNodeReference</span></span> | <span data-ttu-id="01dcd-202">如果您想 tooiterate 從陣列中的 hello 物件擷取資料欄位與 hello 相同模式中，指定該陣列的 hello JSON 路徑。</span><span class="sxs-lookup"><span data-stu-id="01dcd-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="01dcd-203">從 JSON 檔案複製資料時，才支援這個屬性。</span><span class="sxs-lookup"><span data-stu-id="01dcd-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="01dcd-204">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-204">No</span></span> |
| <span data-ttu-id="01dcd-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="01dcd-205">jsonPathDefinition</span></span> | <span data-ttu-id="01dcd-206">自訂資料行名稱 （開始使用小寫） 指定每個資料行對應的 hello JSON 路徑運算式。</span><span class="sxs-lookup"><span data-stu-id="01dcd-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="01dcd-207">從 JSON 檔案複製資料時，才支援這個屬性，您可以從物件或陣列中擷取資料。</span><span class="sxs-lookup"><span data-stu-id="01dcd-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="01dcd-208">在根物件的欄位，啟動以根 $;針對所選擇的 hello 陣列內的欄位`jsonNodeReference`屬性，開始從 hello 陣列項目。</span><span class="sxs-lookup"><span data-stu-id="01dcd-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="01dcd-209">請參閱[JsonFormat 範例](#jsonformat-example)> 一節有關 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="01dcd-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="01dcd-210">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-210">No</span></span> |
| <span data-ttu-id="01dcd-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="01dcd-211">encodingName</span></span> |<span data-ttu-id="01dcd-212">指定 hello 編碼名稱。</span><span class="sxs-lookup"><span data-stu-id="01dcd-212">Specify hello encoding name.</span></span> <span data-ttu-id="01dcd-213">Hello 有效編碼名稱清單，請參閱： [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx)屬性。</span><span class="sxs-lookup"><span data-stu-id="01dcd-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="01dcd-214">例如：windows-1250 或 shift_jis。</span><span class="sxs-lookup"><span data-stu-id="01dcd-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="01dcd-215">hello**預設**值是： **utf-8**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="01dcd-216">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-216">No</span></span> |
| <span data-ttu-id="01dcd-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="01dcd-217">nestingSeparator</span></span> |<span data-ttu-id="01dcd-218">為使用的 tooseparate 巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="01dcd-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="01dcd-219">hello 預設值是 '。 '（點）。</span><span class="sxs-lookup"><span data-stu-id="01dcd-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="01dcd-220">否</span><span class="sxs-lookup"><span data-stu-id="01dcd-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="01dcd-221">JSON 檔案模式</span><span class="sxs-lookup"><span data-stu-id="01dcd-221">JSON file patterns</span></span>

<span data-ttu-id="01dcd-222">複製活動可以剖析的 JSON 檔案模式如下︰</span><span class="sxs-lookup"><span data-stu-id="01dcd-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="01dcd-223">**類型 I：setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="01dcd-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="01dcd-224">每個檔案都會包含單一物件，或以行分隔/串連的多個物件。</span><span class="sxs-lookup"><span data-stu-id="01dcd-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="01dcd-225">在輸出資料集中選擇此選項時，複製活動會產生單一 JSON 檔案，每行一個物件 (以行分隔)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="01dcd-226">**單一物件 JSON 範例**</span><span class="sxs-lookup"><span data-stu-id="01dcd-226">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="01dcd-227">**以行分隔的 JSON 範例**</span><span class="sxs-lookup"><span data-stu-id="01dcd-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="01dcd-228">**串連的 JSON 範例**</span><span class="sxs-lookup"><span data-stu-id="01dcd-228">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="01dcd-229">**類型 II：arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="01dcd-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="01dcd-230">每個檔案都會包含物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="01dcd-230">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

#### <a name="jsonformat-example"></a><span data-ttu-id="01dcd-231">JsonFormat 範例</span><span class="sxs-lookup"><span data-stu-id="01dcd-231">JsonFormat example</span></span>

<span data-ttu-id="01dcd-232">**案例 1︰從 JSON 檔案複製資料**</span><span class="sxs-lookup"><span data-stu-id="01dcd-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="01dcd-233">JSON 檔案中複製資料時，請參閱下列兩種類型的範例與 hello 泛型點 toonote:</span><span class="sxs-lookup"><span data-stu-id="01dcd-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="01dcd-234">**範例 1︰從物件和陣列擷取資料**</span><span class="sxs-lookup"><span data-stu-id="01dcd-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="01dcd-235">在此範例中，您可以預期 toosingle 表格式結果中的記錄會對應一個根 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="01dcd-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="01dcd-236">如果您有在 JSON 檔案以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="01dcd-236">If you have a JSON file with hello following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="01dcd-237">而且您想的 toocopy 到 Azure SQL 中的資料表 hello 下列格式，從物件和陣列中擷取資料：</span><span class="sxs-lookup"><span data-stu-id="01dcd-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="01dcd-238">id</span><span class="sxs-lookup"><span data-stu-id="01dcd-238">id</span></span> | <span data-ttu-id="01dcd-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="01dcd-239">deviceType</span></span> | <span data-ttu-id="01dcd-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="01dcd-240">targetResourceType</span></span> | <span data-ttu-id="01dcd-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="01dcd-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="01dcd-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="01dcd-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="01dcd-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="01dcd-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="01dcd-244">PC</span><span class="sxs-lookup"><span data-stu-id="01dcd-244">PC</span></span> | <span data-ttu-id="01dcd-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="01dcd-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="01dcd-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="01dcd-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="01dcd-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="01dcd-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="01dcd-248">hello 與輸入資料集**JsonFormat**類型的定義如下: （與 hello 相關部分的部分定義）。</span><span class="sxs-lookup"><span data-stu-id="01dcd-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="01dcd-249">具體而言：</span><span class="sxs-lookup"><span data-stu-id="01dcd-249">More specifically:</span></span>

- <span data-ttu-id="01dcd-250">`structure`區段會定義自訂的 hello 資料行名稱和 hello 對應的資料類型轉換 tootabular 資料時。</span><span class="sxs-lookup"><span data-stu-id="01dcd-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="01dcd-251">這個區段是**選擇性**除非需要 toodo 資料行對應。</span><span class="sxs-lookup"><span data-stu-id="01dcd-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="01dcd-252">如需詳細資訊，請參閱[指定矩形資料集的結構定義](#specifying-structure-definition-for-rectangular-datasets)一節。</span><span class="sxs-lookup"><span data-stu-id="01dcd-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="01dcd-253">`jsonPathDefinition`指定每個資料行會指出其中 tooextract hello 資料 hello JSON 路徑。</span><span class="sxs-lookup"><span data-stu-id="01dcd-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="01dcd-254">從陣列 toocopy 資料，您可以使用**陣列 [x].property** tooextract 的 hello hello x 次物件，或您從給定屬性的值可以使用**陣列 [*].property** toofindhello 任何物件，其中包含這類屬性的值。</span><span class="sxs-lookup"><span data-stu-id="01dcd-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="01dcd-255">**範例 2： 跨套用多個具有相同模式陣列中的 hello 物件**</span><span class="sxs-lookup"><span data-stu-id="01dcd-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="01dcd-256">在此範例中，您可以預期 tootransform 一個根 JSON 物件表格式結果中的多個記錄。</span><span class="sxs-lookup"><span data-stu-id="01dcd-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="01dcd-257">如果您有在 JSON 檔案以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="01dcd-257">If you have a JSON file with hello following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="01dcd-258">您想的 toocopy 到 Azure SQL 中的資料表 hello 下列格式的扁平化 hello hello 陣列內的資料及交叉聯結使用 hello 常見的根目錄資訊和：</span><span class="sxs-lookup"><span data-stu-id="01dcd-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="01dcd-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="01dcd-259">ordernumber</span></span> | <span data-ttu-id="01dcd-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="01dcd-260">orderdate</span></span> | <span data-ttu-id="01dcd-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="01dcd-261">order_pd</span></span> | <span data-ttu-id="01dcd-262">order_price</span><span class="sxs-lookup"><span data-stu-id="01dcd-262">order_price</span></span> | <span data-ttu-id="01dcd-263">city</span><span class="sxs-lookup"><span data-stu-id="01dcd-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="01dcd-264">01</span><span class="sxs-lookup"><span data-stu-id="01dcd-264">01</span></span> | <span data-ttu-id="01dcd-265">20170122</span><span class="sxs-lookup"><span data-stu-id="01dcd-265">20170122</span></span> | <span data-ttu-id="01dcd-266">P1</span><span class="sxs-lookup"><span data-stu-id="01dcd-266">P1</span></span> | <span data-ttu-id="01dcd-267">23</span><span class="sxs-lookup"><span data-stu-id="01dcd-267">23</span></span> | <span data-ttu-id="01dcd-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="01dcd-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="01dcd-269">01</span><span class="sxs-lookup"><span data-stu-id="01dcd-269">01</span></span> | <span data-ttu-id="01dcd-270">20170122</span><span class="sxs-lookup"><span data-stu-id="01dcd-270">20170122</span></span> | <span data-ttu-id="01dcd-271">P2</span><span class="sxs-lookup"><span data-stu-id="01dcd-271">P2</span></span> | <span data-ttu-id="01dcd-272">13</span><span class="sxs-lookup"><span data-stu-id="01dcd-272">13</span></span> | <span data-ttu-id="01dcd-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="01dcd-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="01dcd-274">01</span><span class="sxs-lookup"><span data-stu-id="01dcd-274">01</span></span> | <span data-ttu-id="01dcd-275">20170122</span><span class="sxs-lookup"><span data-stu-id="01dcd-275">20170122</span></span> | <span data-ttu-id="01dcd-276">P3</span><span class="sxs-lookup"><span data-stu-id="01dcd-276">P3</span></span> | <span data-ttu-id="01dcd-277">231</span><span class="sxs-lookup"><span data-stu-id="01dcd-277">231</span></span> | <span data-ttu-id="01dcd-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="01dcd-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="01dcd-279">hello 與輸入資料集**JsonFormat**類型的定義如下: （與 hello 相關部分的部分定義）。</span><span class="sxs-lookup"><span data-stu-id="01dcd-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="01dcd-280">具體而言：</span><span class="sxs-lookup"><span data-stu-id="01dcd-280">More specifically:</span></span>

- <span data-ttu-id="01dcd-281">`structure`區段會定義自訂的 hello 資料行名稱和 hello 對應的資料類型轉換 tootabular 資料時。</span><span class="sxs-lookup"><span data-stu-id="01dcd-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="01dcd-282">這個區段是**選擇性**除非需要 toodo 資料行對應。</span><span class="sxs-lookup"><span data-stu-id="01dcd-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="01dcd-283">如需詳細資訊，請參閱[指定矩形資料集的結構定義](#specifying-structure-definition-for-rectangular-datasets)一節。</span><span class="sxs-lookup"><span data-stu-id="01dcd-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="01dcd-284">`jsonNodeReference`表示以相同模式下的 hello hello 物件的 tooiterate 和擷取資料**陣列**訂單產品線。</span><span class="sxs-lookup"><span data-stu-id="01dcd-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="01dcd-285">`jsonPathDefinition`指定每個資料行會指出其中 tooextract hello 資料 hello JSON 路徑。</span><span class="sxs-lookup"><span data-stu-id="01dcd-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="01dcd-286">在此範例中，""、"orderdate"和"city"正在根物件具有開頭為"$"。，"order_pd"和"order_price 」 定義衍生自不含"$"。 hello 陣列項目路徑時的 JSON 路徑。</span><span class="sxs-lookup"><span data-stu-id="01dcd-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="01dcd-287">**請注意下列點 hello:**</span><span class="sxs-lookup"><span data-stu-id="01dcd-287">**Note hello following points:**</span></span>

* <span data-ttu-id="01dcd-288">如果 hello`structure`和`jsonPathDefinition`中未定義 hello Data Factory 的資料集，hello 複製活動會偵測 hello 從 hello 第一個物件的結構描述，以及將扁平化 hello 整個物件。</span><span class="sxs-lookup"><span data-stu-id="01dcd-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="01dcd-289">Hello JSON 輸入中有一個陣列，如果預設 hello 複製活動 hello 整個陣列將值轉換成字串。</span><span class="sxs-lookup"><span data-stu-id="01dcd-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="01dcd-290">您可以選擇使用 tooextract 資料`jsonNodeReference`及/或`jsonPathDefinition`，或未指定在略過它`jsonPathDefinition`。</span><span class="sxs-lookup"><span data-stu-id="01dcd-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="01dcd-291">如果有重複名稱在 hello 相同層級，hello 複製活動會挑選 hello 最後一個。</span><span class="sxs-lookup"><span data-stu-id="01dcd-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="01dcd-292">屬性名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="01dcd-292">Property names are case-sensitive.</span></span> <span data-ttu-id="01dcd-293">名稱相同但大小寫不同的兩個屬性會被視為兩個不同的屬性。</span><span class="sxs-lookup"><span data-stu-id="01dcd-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="01dcd-294">**案例 2： 寫入資料 tooJSON 檔案**</span><span class="sxs-lookup"><span data-stu-id="01dcd-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="01dcd-295">如果您在 SQL Database 中有下列資料表︰</span><span class="sxs-lookup"><span data-stu-id="01dcd-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="01dcd-296">id</span><span class="sxs-lookup"><span data-stu-id="01dcd-296">id</span></span> | <span data-ttu-id="01dcd-297">order_date</span><span class="sxs-lookup"><span data-stu-id="01dcd-297">order_date</span></span> | <span data-ttu-id="01dcd-298">order_price</span><span class="sxs-lookup"><span data-stu-id="01dcd-298">order_price</span></span> | <span data-ttu-id="01dcd-299">order_by</span><span class="sxs-lookup"><span data-stu-id="01dcd-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="01dcd-300">1</span><span class="sxs-lookup"><span data-stu-id="01dcd-300">1</span></span> | <span data-ttu-id="01dcd-301">20170119</span><span class="sxs-lookup"><span data-stu-id="01dcd-301">20170119</span></span> | <span data-ttu-id="01dcd-302">2000</span><span class="sxs-lookup"><span data-stu-id="01dcd-302">2000</span></span> | <span data-ttu-id="01dcd-303">David</span><span class="sxs-lookup"><span data-stu-id="01dcd-303">David</span></span> |
| <span data-ttu-id="01dcd-304">2</span><span class="sxs-lookup"><span data-stu-id="01dcd-304">2</span></span> | <span data-ttu-id="01dcd-305">20170120</span><span class="sxs-lookup"><span data-stu-id="01dcd-305">20170120</span></span> | <span data-ttu-id="01dcd-306">3500</span><span class="sxs-lookup"><span data-stu-id="01dcd-306">3500</span></span> | <span data-ttu-id="01dcd-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="01dcd-307">Patrick</span></span> |
| <span data-ttu-id="01dcd-308">3</span><span class="sxs-lookup"><span data-stu-id="01dcd-308">3</span></span> | <span data-ttu-id="01dcd-309">20170121</span><span class="sxs-lookup"><span data-stu-id="01dcd-309">20170121</span></span> | <span data-ttu-id="01dcd-310">4000</span><span class="sxs-lookup"><span data-stu-id="01dcd-310">4000</span></span> | <span data-ttu-id="01dcd-311">Jason</span><span class="sxs-lookup"><span data-stu-id="01dcd-311">Jason</span></span> |

<span data-ttu-id="01dcd-312">與每個記錄，您會預期 toowrite tooa JSON 物件中的格式如下：</span><span class="sxs-lookup"><span data-stu-id="01dcd-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="01dcd-313">hello 輸出資料集與**JsonFormat**類型的定義如下: （與 hello 相關部分的部分定義）。</span><span class="sxs-lookup"><span data-stu-id="01dcd-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="01dcd-314">更具體來說，`structure`區段會定義目的地檔案中的 hello 自訂屬性名稱`nestingSeparator`(預設值是"。") 將會使用的 tooidentify hello 巢狀層級從 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="01dcd-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="01dcd-315">這個區段是**選擇性**除非您想要比較的來源資料行名稱，toochange hello 屬性名稱，或是巢狀化某些 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="01dcd-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

### <a name="specifying-avroformat"></a><span data-ttu-id="01dcd-316">指定 AvroFormat</span><span class="sxs-lookup"><span data-stu-id="01dcd-316">Specifying AvroFormat</span></span>
<span data-ttu-id="01dcd-317">如果您想 tooparse hello Avro 檔案，或寫入 Avro 格式中的 hello 資料，設定 hello `format` `type`屬性太**AvroFormat**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="01dcd-318">您不需要 toospecify hello typeProperties 區段中的 hello 格式 > 一節中的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="01dcd-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="01dcd-319">範例：</span><span class="sxs-lookup"><span data-stu-id="01dcd-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="01dcd-320">toouse Avro 格式的 Hive 資料表中，您可以使用參照太[Apache Hive 教學課程](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="01dcd-321">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="01dcd-321">Note hello following points:</span></span>  

* <span data-ttu-id="01dcd-322">不支援[複雜資料類型](http://avro.apache.org/docs/current/spec.html#schema_complex) (記錄、列舉、陣列、對應、等位和固定)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="01dcd-323">指定 OrcFormat</span><span class="sxs-lookup"><span data-stu-id="01dcd-323">Specifying OrcFormat</span></span>
<span data-ttu-id="01dcd-324">如果您想 tooparse hello ORC 檔案，或寫入 ORC 格式中的 hello 資料，設定 hello `format` `type`屬性太**OrcFormat**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="01dcd-325">您不需要 toospecify hello typeProperties 區段中的 hello 格式 > 一節中的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="01dcd-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="01dcd-326">範例：</span><span class="sxs-lookup"><span data-stu-id="01dcd-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="01dcd-327">如果您不複製 ORC 檔案**為-是**在內部部署和雲端之間資料存放區，您需要在閘道機器上的 tooinstall hello JRE 8 (Java Runtime Environment)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="01dcd-328">64 位元閘道需要 64 位元 JRE，而 32 位元閘道需要 32 位元 JRE。</span><span class="sxs-lookup"><span data-stu-id="01dcd-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="01dcd-329">您可以從 [這裡](http://go.microsoft.com/fwlink/?LinkId=808605)找到這兩個版本。</span><span class="sxs-lookup"><span data-stu-id="01dcd-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="01dcd-330">請選擇適當的一個 hello。</span><span class="sxs-lookup"><span data-stu-id="01dcd-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="01dcd-331">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="01dcd-331">Note hello following points:</span></span>

* <span data-ttu-id="01dcd-332">不支援複雜資料類型 (STRUCT、MAP、LIST、UNION)</span><span class="sxs-lookup"><span data-stu-id="01dcd-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="01dcd-333">ORC 檔案有 3 種 [壓縮相關選項](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/)︰NONE、ZLIB、SNAPPY。</span><span class="sxs-lookup"><span data-stu-id="01dcd-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="01dcd-334">Data Factory 支援以這些壓縮格式的任一項從 ORC 檔案讀取資料。</span><span class="sxs-lookup"><span data-stu-id="01dcd-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="01dcd-335">它會使用 hello 壓縮轉碼器是 hello 中繼資料 tooread hello 資料中。</span><span class="sxs-lookup"><span data-stu-id="01dcd-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="01dcd-336">不過，在撰寫 tooan ORC 檔案時，Data Factory 選擇 ZLIB，ORC hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="01dcd-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="01dcd-337">目前沒有任何選項 toooverride 這種行為。</span><span class="sxs-lookup"><span data-stu-id="01dcd-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="01dcd-338">指定 ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="01dcd-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="01dcd-339">如果您想 tooparse hello Parquet 檔案，或寫入 Parquet 格式中的 hello 資料，設定 hello `format` `type`屬性太**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="01dcd-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="01dcd-340">您不需要 toospecify hello typeProperties 區段中的 hello 格式 > 一節中的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="01dcd-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="01dcd-341">範例：</span><span class="sxs-lookup"><span data-stu-id="01dcd-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="01dcd-342">如果您不複製 Parquet 檔案**為-是**在內部部署和雲端之間資料存放區，您需要在閘道機器上的 tooinstall hello JRE 8 (Java Runtime Environment)。</span><span class="sxs-lookup"><span data-stu-id="01dcd-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="01dcd-343">64 位元閘道需要 64 位元 JRE，而 32 位元閘道需要 32 位元 JRE。</span><span class="sxs-lookup"><span data-stu-id="01dcd-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="01dcd-344">您可以從 [這裡](http://go.microsoft.com/fwlink/?LinkId=808605)找到這兩個版本。</span><span class="sxs-lookup"><span data-stu-id="01dcd-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="01dcd-345">請選擇適當的一個 hello。</span><span class="sxs-lookup"><span data-stu-id="01dcd-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="01dcd-346">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="01dcd-346">Note hello following points:</span></span>

* <span data-ttu-id="01dcd-347">不支援複雜資料類型 (MAP、LIST)</span><span class="sxs-lookup"><span data-stu-id="01dcd-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="01dcd-348">Parquet 檔案具有下列相關的壓縮選項的 hello: NONE、 SNAPPY、 GZIP、 和 LZO。</span><span class="sxs-lookup"><span data-stu-id="01dcd-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="01dcd-349">Data Factory 支援以這些壓縮格式的任一項從 ORC 檔案讀取資料。</span><span class="sxs-lookup"><span data-stu-id="01dcd-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="01dcd-350">它使用 hello 中繼資料 tooread hello 資料中的 hello 壓縮轉碼器。</span><span class="sxs-lookup"><span data-stu-id="01dcd-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="01dcd-351">不過，在撰寫 tooa Parquet 檔案時，Data Factory 選擇 SNAPPY，hello Parquet 格式的預設值。</span><span class="sxs-lookup"><span data-stu-id="01dcd-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="01dcd-352">目前沒有任何選項 toooverride 這種行為。</span><span class="sxs-lookup"><span data-stu-id="01dcd-352">Currently, there is no option toooverride this behavior.</span></span>
