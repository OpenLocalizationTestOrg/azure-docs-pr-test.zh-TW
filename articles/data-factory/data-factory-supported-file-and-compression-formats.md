---
title: "Azure Data Factory 中的 aaaFile 和壓縮格式 |Microsoft 文件"
description: "深入了解支援的 Azure Data Factory 的 hello 檔案格式。"
keywords: "blob 資料, azure blob 複製"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="c5d89-104">了解 Azure Data Factory 所支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="c5d89-105">*本主題適用於下列連接器的 toohello: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md)， [Azure Blob](data-factory-azure-blob-connector.md)， [Azure Data Lake Store](data-factory-azure-datalake-connector.md)，[檔案系統](data-factory-onprem-file-system-connector.md)， [FTP](data-factory-ftp-connector.md)， [HDFS](data-factory-hdfs-connector.md)， [HTTP](data-factory-http-connector.md)，和[SFTP](data-factory-sftp-connector.md)。*</span><span class="sxs-lookup"><span data-stu-id="c5d89-105">*This topic applies toohello following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="c5d89-106">Azure Data Factory 支援下列檔案格式類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="c5d89-106">Azure Data Factory supports hello following file format types:</span></span>

* [<span data-ttu-id="c5d89-107">文字格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="c5d89-108">JSON 格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="c5d89-109">Avro 格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="c5d89-110">ORC 格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="c5d89-111">Parquet 格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="c5d89-112">文字格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-112">Text format</span></span>
<span data-ttu-id="c5d89-113">如果您想要從文字檔 tooread 或撰寫 tooa 文字檔案，設定 hello`type`屬性在 hello `format` hello 資料集部分太**TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-113">If you want tooread from a text file or write tooa text file, set hello `type` property in hello `format` section of hello dataset too**TextFormat**.</span></span> <span data-ttu-id="c5d89-114">您也可以指定下列 hello**選擇性**屬性在 hello `format` > 一節。</span><span class="sxs-lookup"><span data-stu-id="c5d89-114">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="c5d89-115">請參閱[TextFormat 範例](#textformat-example)> 一節有關 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="c5d89-115">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="c5d89-116">屬性</span><span class="sxs-lookup"><span data-stu-id="c5d89-116">Property</span></span> | <span data-ttu-id="c5d89-117">說明</span><span class="sxs-lookup"><span data-stu-id="c5d89-117">Description</span></span> | <span data-ttu-id="c5d89-118">允許的值</span><span class="sxs-lookup"><span data-stu-id="c5d89-118">Allowed values</span></span> | <span data-ttu-id="c5d89-119">必要</span><span class="sxs-lookup"><span data-stu-id="c5d89-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c5d89-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c5d89-120">columnDelimiter</span></span> |<span data-ttu-id="c5d89-121">hello 字元會在檔案中，使用 tooseparate 資料行。</span><span class="sxs-lookup"><span data-stu-id="c5d89-121">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="c5d89-122">您可以考慮的 toouse 罕見的不可列印字元可能不可能存在於資料中。</span><span class="sxs-lookup"><span data-stu-id="c5d89-122">You can consider toouse a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="c5d89-123">例如，指定 "\u0001"，這代表「標題開頭」(SOH)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="c5d89-124">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="c5d89-124">Only one character is allowed.</span></span> <span data-ttu-id="c5d89-125">hello**預設**值是**逗號 （'，'）**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-125">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="c5d89-126">toouse Unicode 字元，請參閱太[Unicode 字元](https://en.wikipedia.org/wiki/List_of_Unicode_characters)tooget hello 為其對應的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c5d89-126">toouse a Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="c5d89-127">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-127">No</span></span> |
| <span data-ttu-id="c5d89-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="c5d89-128">rowDelimiter</span></span> |<span data-ttu-id="c5d89-129">hello 字元用於 tooseparate 資料列檔案中。</span><span class="sxs-lookup"><span data-stu-id="c5d89-129">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="c5d89-130">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="c5d89-130">Only one character is allowed.</span></span> <span data-ttu-id="c5d89-131">hello**預設**值可以是任何 hello 讀取下列值： **["\r\n"、"\r"、"\n"]**和**"\r\n"**寫入。</span><span class="sxs-lookup"><span data-stu-id="c5d89-131">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="c5d89-132">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-132">No</span></span> |
| <span data-ttu-id="c5d89-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="c5d89-133">escapeChar</span></span> |<span data-ttu-id="c5d89-134">hello 特殊字元都使用資料行分隔符號 tooescape hello 內容的輸入檔中。</span><span class="sxs-lookup"><span data-stu-id="c5d89-134">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="c5d89-135">您無法同時為資料表指定 escapeChar 和 quoteChar。</span><span class="sxs-lookup"><span data-stu-id="c5d89-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="c5d89-136">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="c5d89-136">Only one character is allowed.</span></span> <span data-ttu-id="c5d89-137">沒有預設值。</span><span class="sxs-lookup"><span data-stu-id="c5d89-137">No default value.</span></span> <br/><br/><span data-ttu-id="c5d89-138">範例： 如果您以逗號 （'，'） hello 資料行分隔符號，但您想要以 hello 文字 toohave hello 逗號字元 (範例:"Hello，world")，您可以定義為 hello 逸出字元 '$'，並使用字串"Hello$，world hello 來源中。</span><span class="sxs-lookup"><span data-stu-id="c5d89-138">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="c5d89-139">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-139">No</span></span> |
| <span data-ttu-id="c5d89-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="c5d89-140">quoteChar</span></span> |<span data-ttu-id="c5d89-141">hello 字元使用 tooquote 字串值。</span><span class="sxs-lookup"><span data-stu-id="c5d89-141">hello character used tooquote a string value.</span></span> <span data-ttu-id="c5d89-142">hello hello 引號字元內的資料行和資料列分隔符號會視為 hello 字串值的一部分。</span><span class="sxs-lookup"><span data-stu-id="c5d89-142">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="c5d89-143">這個屬性是適用於 tooboth 輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="c5d89-143">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="c5d89-144">您無法同時為資料表指定 escapeChar 和 quoteChar。</span><span class="sxs-lookup"><span data-stu-id="c5d89-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="c5d89-145">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="c5d89-145">Only one character is allowed.</span></span> <span data-ttu-id="c5d89-146">沒有預設值。</span><span class="sxs-lookup"><span data-stu-id="c5d89-146">No default value.</span></span> <br/><br/><span data-ttu-id="c5d89-147">比方說，如果您以逗號 （'，'） hello 資料行分隔符號，但您想要以 hello 文字 toohave 逗號字元 (範例： < Hello，world >)，您可以定義"（雙引號） hello 引號字元，並使用 hello 字串"Hello，world"hello 來源中。</span><span class="sxs-lookup"><span data-stu-id="c5d89-147">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="c5d89-148">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-148">No</span></span> |
| <span data-ttu-id="c5d89-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="c5d89-149">nullValue</span></span> |<span data-ttu-id="c5d89-150">Toorepresent null 值使用一或多個字元。</span><span class="sxs-lookup"><span data-stu-id="c5d89-150">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="c5d89-151">一或多個字元。</span><span class="sxs-lookup"><span data-stu-id="c5d89-151">One or more characters.</span></span> <span data-ttu-id="c5d89-152">hello**預設**有效值**"\N"和"NULL"**在讀取和**"\N"**寫入。</span><span class="sxs-lookup"><span data-stu-id="c5d89-152">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="c5d89-153">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-153">No</span></span> |
| <span data-ttu-id="c5d89-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="c5d89-154">encodingName</span></span> |<span data-ttu-id="c5d89-155">指定 hello 編碼名稱。</span><span class="sxs-lookup"><span data-stu-id="c5d89-155">Specify hello encoding name.</span></span> |<span data-ttu-id="c5d89-156">有效的編碼名稱。</span><span class="sxs-lookup"><span data-stu-id="c5d89-156">A valid encoding name.</span></span> <span data-ttu-id="c5d89-157">請參閱 [Encoding.EncodingName 屬性](https://msdn.microsoft.com/library/system.text.encoding.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="c5d89-158">例如：windows-1250 或 shift_jis。</span><span class="sxs-lookup"><span data-stu-id="c5d89-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="c5d89-159">hello**預設**值是**utf-8**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-159">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="c5d89-160">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-160">No</span></span> |
| <span data-ttu-id="c5d89-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="c5d89-161">firstRowAsHeader</span></span> |<span data-ttu-id="c5d89-162">指定是否 tooconsider hello 做為標頭的第一個資料列。</span><span class="sxs-lookup"><span data-stu-id="c5d89-162">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="c5d89-163">對於輸入資料集，Data Factory 會讀取第一個資料列做為標頭。</span><span class="sxs-lookup"><span data-stu-id="c5d89-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="c5d89-164">對於輸出資料集，Data Factory 會寫入第一個資料列做為標頭。</span><span class="sxs-lookup"><span data-stu-id="c5d89-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="c5d89-165">相關範例案例請參閱[使用 `firstRowAsHeader` 和 `skipLineCount` 的案例](#scenarios-for-using-firstrowasheader-and-skiplinecount)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="c5d89-166">True</span><span class="sxs-lookup"><span data-stu-id="c5d89-166">True</span></span><br/><span data-ttu-id="c5d89-167"><b>False (預設值)</b></span><span class="sxs-lookup"><span data-stu-id="c5d89-167"><b>False (default)</b></span></span> |<span data-ttu-id="c5d89-168">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-168">No</span></span> |
| <span data-ttu-id="c5d89-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="c5d89-169">skipLineCount</span></span> |<span data-ttu-id="c5d89-170">從輸入檔讀取資料時，表示 hello tooskip 資料列數目。</span><span class="sxs-lookup"><span data-stu-id="c5d89-170">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="c5d89-171">如果未指定 skipLineCount 和 firstRowAsHeader，hello 線條會略過第一次，並 hello 標頭資訊從 hello 輸入檔讀取。</span><span class="sxs-lookup"><span data-stu-id="c5d89-171">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="c5d89-172">相關範例案例請參閱[使用 `firstRowAsHeader` 和 `skipLineCount` 的案例](#scenarios-for-using-firstrowasheader-and-skiplinecount)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="c5d89-173">Integer</span><span class="sxs-lookup"><span data-stu-id="c5d89-173">Integer</span></span> |<span data-ttu-id="c5d89-174">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-174">No</span></span> |
| <span data-ttu-id="c5d89-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="c5d89-175">treatEmptyAsNull</span></span> |<span data-ttu-id="c5d89-176">指定是否 tootreat null 或空字串，以 null 值時從輸入檔讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c5d89-176">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="c5d89-177">**True (預設值)**</span><span class="sxs-lookup"><span data-stu-id="c5d89-177">**True (default)**</span></span><br/><span data-ttu-id="c5d89-178">False</span><span class="sxs-lookup"><span data-stu-id="c5d89-178">False</span></span> |<span data-ttu-id="c5d89-179">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="c5d89-180">TextFormat 範例</span><span class="sxs-lookup"><span data-stu-id="c5d89-180">TextFormat example</span></span>
<span data-ttu-id="c5d89-181">下列 JSON 定義資料集的 hello，在某些 hello 選擇性屬性指定。</span><span class="sxs-lookup"><span data-stu-id="c5d89-181">In hello following JSON definition for a dataset, some of hello optional properties are specified.</span></span>

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

<span data-ttu-id="c5d89-182">toouse`escapeChar`而不是`quoteChar`，取代與 hello 一行`quoteChar`以下列的 escapeChar hello:</span><span class="sxs-lookup"><span data-stu-id="c5d89-182">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="c5d89-183">使用 firstRowAsHeader 和 skipLineCount 的案例</span><span class="sxs-lookup"><span data-stu-id="c5d89-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="c5d89-184">您要從非檔案來源 tooa 文字檔案複製，並希望 tooadd 包含 hello 結構描述中繼資料標頭的資料行 (例如： SQL 結構描述)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-184">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="c5d89-185">指定`firstRowAsHeader`hello 輸出資料集，在此案例中為 true。</span><span class="sxs-lookup"><span data-stu-id="c5d89-185">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="c5d89-186">您要從文字檔，其中包含的標頭列 tooa 非檔案接收複製，而且想要線條的 toodrop。</span><span class="sxs-lookup"><span data-stu-id="c5d89-186">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="c5d89-187">指定`firstRowAsHeader`hello 輸入資料集，則為 true。</span><span class="sxs-lookup"><span data-stu-id="c5d89-187">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="c5d89-188">您要複製的文字檔案，並想 tooskip hello 開頭沒有包含任何資料或標頭資訊的幾行。</span><span class="sxs-lookup"><span data-stu-id="c5d89-188">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="c5d89-189">指定`skipLineCount`tooindicate hello 數行 toobe 略過。</span><span class="sxs-lookup"><span data-stu-id="c5d89-189">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="c5d89-190">如果 hello 檔案的其餘部分 hello 包含標頭行，您也可以指定`firstRowAsHeader`。</span><span class="sxs-lookup"><span data-stu-id="c5d89-190">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="c5d89-191">如果兩個`skipLineCount`和`firstRowAsHeader`和指定的會先略過 hello 行 hello 標頭資訊然後讀取 hello 輸入檔</span><span class="sxs-lookup"><span data-stu-id="c5d89-191">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

## <a name="json-format"></a><span data-ttu-id="c5d89-192">JSON 格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-192">JSON format</span></span>
<span data-ttu-id="c5d89-193">太**匯入/匯出 JSON 檔案儲存為-至 / 從 Azure Cosmos DB**，hello，請參閱[匯入/匯出 JSON 文件](data-factory-azure-documentdb-connector.md#importexport-json-documents)一節中[將資料移至 azure 或從 Azure Cosmos DB](data-factory-azure-documentdb-connector.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="c5d89-193">too**import/export a JSON file as-is into/from Azure Cosmos DB**, hello see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="c5d89-194">如果您想 tooparse hello JSON 檔案，或將 JSON 格式寫入 hello 資料，設定 hello`type`屬性在 hello`format`太區段**JsonFormat**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-194">If you want tooparse hello JSON files or write hello data in JSON format, set hello `type` property in hello `format` section too**JsonFormat**.</span></span> <span data-ttu-id="c5d89-195">您也可以指定下列 hello**選擇性**屬性在 hello `format` > 一節。</span><span class="sxs-lookup"><span data-stu-id="c5d89-195">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="c5d89-196">請參閱[JsonFormat 範例](#jsonformat-example)> 一節有關 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="c5d89-196">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="c5d89-197">屬性</span><span class="sxs-lookup"><span data-stu-id="c5d89-197">Property</span></span> | <span data-ttu-id="c5d89-198">說明</span><span class="sxs-lookup"><span data-stu-id="c5d89-198">Description</span></span> | <span data-ttu-id="c5d89-199">必要</span><span class="sxs-lookup"><span data-stu-id="c5d89-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5d89-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="c5d89-200">filePattern</span></span> |<span data-ttu-id="c5d89-201">表示 hello 模式，每個 JSON 檔案中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="c5d89-201">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="c5d89-202">允許的值為︰**setOfObjects** 和 **arrayOfObjects**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="c5d89-203">hello**預設**值是**setOfObjects**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-203">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="c5d89-204">關於這些模式的詳細資訊，請參閱 [JSON 檔案模式](#json-file-patterns)一節。</span><span class="sxs-lookup"><span data-stu-id="c5d89-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="c5d89-205">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-205">No</span></span> |
| <span data-ttu-id="c5d89-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="c5d89-206">jsonNodeReference</span></span> | <span data-ttu-id="c5d89-207">如果您想 tooiterate 從陣列中的 hello 物件擷取資料欄位與 hello 相同模式中，指定該陣列的 hello JSON 路徑。</span><span class="sxs-lookup"><span data-stu-id="c5d89-207">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="c5d89-208">從 JSON 檔案複製資料時，才支援這個屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="c5d89-209">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-209">No</span></span> |
| <span data-ttu-id="c5d89-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="c5d89-210">jsonPathDefinition</span></span> | <span data-ttu-id="c5d89-211">自訂資料行名稱 （開始使用小寫） 指定每個資料行對應的 hello JSON 路徑運算式。</span><span class="sxs-lookup"><span data-stu-id="c5d89-211">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="c5d89-212">從 JSON 檔案複製資料時，才支援這個屬性，您可以從物件或陣列中擷取資料。</span><span class="sxs-lookup"><span data-stu-id="c5d89-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="c5d89-213">在根物件的欄位，啟動以根 $;針對所選擇的 hello 陣列內的欄位`jsonNodeReference`屬性，開始從 hello 陣列項目。</span><span class="sxs-lookup"><span data-stu-id="c5d89-213">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="c5d89-214">請參閱[JsonFormat 範例](#jsonformat-example)> 一節有關 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="c5d89-214">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="c5d89-215">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-215">No</span></span> |
| <span data-ttu-id="c5d89-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="c5d89-216">encodingName</span></span> |<span data-ttu-id="c5d89-217">指定 hello 編碼名稱。</span><span class="sxs-lookup"><span data-stu-id="c5d89-217">Specify hello encoding name.</span></span> <span data-ttu-id="c5d89-218">Hello 有效編碼名稱清單，請參閱： [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx)屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-218">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="c5d89-219">例如：windows-1250 或 shift_jis。</span><span class="sxs-lookup"><span data-stu-id="c5d89-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="c5d89-220">hello**預設**值是： **utf-8**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-220">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="c5d89-221">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-221">No</span></span> |
| <span data-ttu-id="c5d89-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="c5d89-222">nestingSeparator</span></span> |<span data-ttu-id="c5d89-223">為使用的 tooseparate 巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="c5d89-223">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="c5d89-224">hello 預設值是 '。 '（點）。</span><span class="sxs-lookup"><span data-stu-id="c5d89-224">hello default value is '.' (dot).</span></span> |<span data-ttu-id="c5d89-225">否</span><span class="sxs-lookup"><span data-stu-id="c5d89-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="c5d89-226">JSON 檔案模式</span><span class="sxs-lookup"><span data-stu-id="c5d89-226">JSON file patterns</span></span>

<span data-ttu-id="c5d89-227">複製活動可以剖析 hello 下列 JSON 檔案的模式：</span><span class="sxs-lookup"><span data-stu-id="c5d89-227">Copy activity can parse hello following patterns of JSON files:</span></span>

- <span data-ttu-id="c5d89-228">**類型 I：setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="c5d89-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="c5d89-229">每個檔案都會包含單一物件，或以行分隔/串連的多個物件。</span><span class="sxs-lookup"><span data-stu-id="c5d89-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="c5d89-230">在輸出資料集中選擇此選項時，複製活動會產生單一 JSON 檔案，每行一個物件 (以行分隔)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="c5d89-231">**單一物件 JSON 範例**</span><span class="sxs-lookup"><span data-stu-id="c5d89-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="c5d89-232">**以行分隔的 JSON 範例**</span><span class="sxs-lookup"><span data-stu-id="c5d89-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="c5d89-233">**串連的 JSON 範例**</span><span class="sxs-lookup"><span data-stu-id="c5d89-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="c5d89-234">**類型 II：arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="c5d89-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="c5d89-235">每個檔案都會包含物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="c5d89-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="c5d89-236">JsonFormat 範例</span><span class="sxs-lookup"><span data-stu-id="c5d89-236">JsonFormat example</span></span>

<span data-ttu-id="c5d89-237">**案例 1︰從 JSON 檔案複製資料**</span><span class="sxs-lookup"><span data-stu-id="c5d89-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="c5d89-238">請參閱 hello JSON 檔案中複製資料時，下列兩個樣本。</span><span class="sxs-lookup"><span data-stu-id="c5d89-238">See hello following two samples when copying data from JSON files.</span></span> <span data-ttu-id="c5d89-239">hello 泛型點 toonote:</span><span class="sxs-lookup"><span data-stu-id="c5d89-239">hello generic points toonote:</span></span>

<span data-ttu-id="c5d89-240">**範例 1︰從物件和陣列擷取資料**</span><span class="sxs-lookup"><span data-stu-id="c5d89-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="c5d89-241">在此範例中，您可以預期 toosingle 表格式結果中的記錄會對應一個根 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="c5d89-241">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="c5d89-242">如果您有在 JSON 檔案以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="c5d89-242">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="c5d89-243">而且您想的 toocopy 到 Azure SQL 中的資料表 hello 下列格式，從物件和陣列中擷取資料：</span><span class="sxs-lookup"><span data-stu-id="c5d89-243">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="c5d89-244">id</span><span class="sxs-lookup"><span data-stu-id="c5d89-244">id</span></span> | <span data-ttu-id="c5d89-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="c5d89-245">deviceType</span></span> | <span data-ttu-id="c5d89-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="c5d89-246">targetResourceType</span></span> | <span data-ttu-id="c5d89-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="c5d89-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="c5d89-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="c5d89-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c5d89-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="c5d89-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="c5d89-250">PC</span><span class="sxs-lookup"><span data-stu-id="c5d89-250">PC</span></span> | <span data-ttu-id="c5d89-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="c5d89-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="c5d89-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="c5d89-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="c5d89-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="c5d89-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="c5d89-254">hello 與輸入資料集**JsonFormat**類型的定義如下: （與 hello 相關部分的部分定義）。</span><span class="sxs-lookup"><span data-stu-id="c5d89-254">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="c5d89-255">具體而言：</span><span class="sxs-lookup"><span data-stu-id="c5d89-255">More specifically:</span></span>

- <span data-ttu-id="c5d89-256">`structure`區段會定義自訂的 hello 資料行名稱和 hello 對應的資料類型轉換 tootabular 資料時。</span><span class="sxs-lookup"><span data-stu-id="c5d89-256">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="c5d89-257">這個區段是**選擇性**除非需要 toodo 資料行對應。</span><span class="sxs-lookup"><span data-stu-id="c5d89-257">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="c5d89-258">請參閱[來源資料集資料行 toodestination 資料集資料行對應](data-factory-map-columns.md)> 一節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c5d89-258">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="c5d89-259">`jsonPathDefinition`指定每個資料行會指出其中 tooextract hello 資料 hello JSON 路徑。</span><span class="sxs-lookup"><span data-stu-id="c5d89-259">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="c5d89-260">從陣列 toocopy 資料，您可以使用**陣列 [x].property** tooextract 的 hello hello x 次物件，或您從給定屬性的值可以使用**陣列 [*].property** toofindhello 任何物件，其中包含這類屬性的值。</span><span class="sxs-lookup"><span data-stu-id="c5d89-260">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="c5d89-261">**範例 2： 跨套用多個具有相同模式陣列中的 hello 物件**</span><span class="sxs-lookup"><span data-stu-id="c5d89-261">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="c5d89-262">在此範例中，您可以預期 tootransform 一個根 JSON 物件表格式結果中的多個記錄。</span><span class="sxs-lookup"><span data-stu-id="c5d89-262">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="c5d89-263">如果您有在 JSON 檔案以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="c5d89-263">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="c5d89-264">您想的 toocopy 到 Azure SQL 中的資料表 hello 下列格式的扁平化 hello hello 陣列內的資料及交叉聯結使用 hello 常見的根目錄資訊和：</span><span class="sxs-lookup"><span data-stu-id="c5d89-264">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="c5d89-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="c5d89-265">ordernumber</span></span> | <span data-ttu-id="c5d89-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="c5d89-266">orderdate</span></span> | <span data-ttu-id="c5d89-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="c5d89-267">order_pd</span></span> | <span data-ttu-id="c5d89-268">order_price</span><span class="sxs-lookup"><span data-stu-id="c5d89-268">order_price</span></span> | <span data-ttu-id="c5d89-269">city</span><span class="sxs-lookup"><span data-stu-id="c5d89-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c5d89-270">01</span><span class="sxs-lookup"><span data-stu-id="c5d89-270">01</span></span> | <span data-ttu-id="c5d89-271">20170122</span><span class="sxs-lookup"><span data-stu-id="c5d89-271">20170122</span></span> | <span data-ttu-id="c5d89-272">P1</span><span class="sxs-lookup"><span data-stu-id="c5d89-272">P1</span></span> | <span data-ttu-id="c5d89-273">23</span><span class="sxs-lookup"><span data-stu-id="c5d89-273">23</span></span> | <span data-ttu-id="c5d89-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="c5d89-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="c5d89-275">01</span><span class="sxs-lookup"><span data-stu-id="c5d89-275">01</span></span> | <span data-ttu-id="c5d89-276">20170122</span><span class="sxs-lookup"><span data-stu-id="c5d89-276">20170122</span></span> | <span data-ttu-id="c5d89-277">P2</span><span class="sxs-lookup"><span data-stu-id="c5d89-277">P2</span></span> | <span data-ttu-id="c5d89-278">13</span><span class="sxs-lookup"><span data-stu-id="c5d89-278">13</span></span> | <span data-ttu-id="c5d89-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="c5d89-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="c5d89-280">01</span><span class="sxs-lookup"><span data-stu-id="c5d89-280">01</span></span> | <span data-ttu-id="c5d89-281">20170122</span><span class="sxs-lookup"><span data-stu-id="c5d89-281">20170122</span></span> | <span data-ttu-id="c5d89-282">P3</span><span class="sxs-lookup"><span data-stu-id="c5d89-282">P3</span></span> | <span data-ttu-id="c5d89-283">231</span><span class="sxs-lookup"><span data-stu-id="c5d89-283">231</span></span> | <span data-ttu-id="c5d89-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="c5d89-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="c5d89-285">hello 與輸入資料集**JsonFormat**類型的定義如下: （與 hello 相關部分的部分定義）。</span><span class="sxs-lookup"><span data-stu-id="c5d89-285">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="c5d89-286">具體而言：</span><span class="sxs-lookup"><span data-stu-id="c5d89-286">More specifically:</span></span>

- <span data-ttu-id="c5d89-287">`structure`區段會定義自訂的 hello 資料行名稱和 hello 對應的資料類型轉換 tootabular 資料時。</span><span class="sxs-lookup"><span data-stu-id="c5d89-287">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="c5d89-288">這個區段是**選擇性**除非需要 toodo 資料行對應。</span><span class="sxs-lookup"><span data-stu-id="c5d89-288">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="c5d89-289">請參閱[來源資料集資料行 toodestination 資料集資料行對應](data-factory-map-columns.md)> 一節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c5d89-289">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="c5d89-290">`jsonNodeReference`表示以相同模式下的 hello hello 物件的 tooiterate 和擷取資料**陣列**訂單產品線。</span><span class="sxs-lookup"><span data-stu-id="c5d89-290">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="c5d89-291">`jsonPathDefinition`指定每個資料行會指出其中 tooextract hello 資料 hello JSON 路徑。</span><span class="sxs-lookup"><span data-stu-id="c5d89-291">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="c5d89-292">在此範例中，""、"orderdate"和"city"正在根物件具有開頭為"$"。，"order_pd"和"order_price 」 定義衍生自不含"$"。 hello 陣列項目路徑時的 JSON 路徑。</span><span class="sxs-lookup"><span data-stu-id="c5d89-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="c5d89-293">**請注意下列點 hello:**</span><span class="sxs-lookup"><span data-stu-id="c5d89-293">**Note hello following points:**</span></span>

* <span data-ttu-id="c5d89-294">如果 hello`structure`和`jsonPathDefinition`中未定義 hello Data Factory 的資料集，hello 複製活動會偵測 hello 從 hello 第一個物件的結構描述，以及將扁平化 hello 整個物件。</span><span class="sxs-lookup"><span data-stu-id="c5d89-294">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="c5d89-295">Hello JSON 輸入中有一個陣列，如果預設 hello 複製活動 hello 整個陣列將值轉換成字串。</span><span class="sxs-lookup"><span data-stu-id="c5d89-295">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="c5d89-296">您可以選擇使用 tooextract 資料`jsonNodeReference`及/或`jsonPathDefinition`，或未指定在略過它`jsonPathDefinition`。</span><span class="sxs-lookup"><span data-stu-id="c5d89-296">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="c5d89-297">如果有重複名稱在 hello 相同層級，hello 複製活動會挑選 hello 最後一個。</span><span class="sxs-lookup"><span data-stu-id="c5d89-297">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="c5d89-298">屬性名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="c5d89-298">Property names are case-sensitive.</span></span> <span data-ttu-id="c5d89-299">名稱相同但大小寫不同的兩個屬性會被視為兩個不同的屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="c5d89-300">**案例 2： 寫入資料 tooJSON 檔案**</span><span class="sxs-lookup"><span data-stu-id="c5d89-300">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="c5d89-301">如果您有遵循 SQL 資料庫資料表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="c5d89-301">If you have hello following table in SQL Database:</span></span>

| <span data-ttu-id="c5d89-302">id</span><span class="sxs-lookup"><span data-stu-id="c5d89-302">id</span></span> | <span data-ttu-id="c5d89-303">order_date</span><span class="sxs-lookup"><span data-stu-id="c5d89-303">order_date</span></span> | <span data-ttu-id="c5d89-304">order_price</span><span class="sxs-lookup"><span data-stu-id="c5d89-304">order_price</span></span> | <span data-ttu-id="c5d89-305">order_by</span><span class="sxs-lookup"><span data-stu-id="c5d89-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c5d89-306">1</span><span class="sxs-lookup"><span data-stu-id="c5d89-306">1</span></span> | <span data-ttu-id="c5d89-307">20170119</span><span class="sxs-lookup"><span data-stu-id="c5d89-307">20170119</span></span> | <span data-ttu-id="c5d89-308">2000</span><span class="sxs-lookup"><span data-stu-id="c5d89-308">2000</span></span> | <span data-ttu-id="c5d89-309">David</span><span class="sxs-lookup"><span data-stu-id="c5d89-309">David</span></span> |
| <span data-ttu-id="c5d89-310">2</span><span class="sxs-lookup"><span data-stu-id="c5d89-310">2</span></span> | <span data-ttu-id="c5d89-311">20170120</span><span class="sxs-lookup"><span data-stu-id="c5d89-311">20170120</span></span> | <span data-ttu-id="c5d89-312">3500</span><span class="sxs-lookup"><span data-stu-id="c5d89-312">3500</span></span> | <span data-ttu-id="c5d89-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="c5d89-313">Patrick</span></span> |
| <span data-ttu-id="c5d89-314">3</span><span class="sxs-lookup"><span data-stu-id="c5d89-314">3</span></span> | <span data-ttu-id="c5d89-315">20170121</span><span class="sxs-lookup"><span data-stu-id="c5d89-315">20170121</span></span> | <span data-ttu-id="c5d89-316">4000</span><span class="sxs-lookup"><span data-stu-id="c5d89-316">4000</span></span> | <span data-ttu-id="c5d89-317">Jason</span><span class="sxs-lookup"><span data-stu-id="c5d89-317">Jason</span></span> |

<span data-ttu-id="c5d89-318">與每個記錄，您預期 toowrite tooa JSON 物件中的 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="c5d89-318">and for each record, you expect toowrite tooa JSON object in hello following format:</span></span>
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

<span data-ttu-id="c5d89-319">hello 輸出資料集與**JsonFormat**類型的定義如下: （與 hello 相關部分的部分定義）。</span><span class="sxs-lookup"><span data-stu-id="c5d89-319">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="c5d89-320">更具體來說，`structure`區段會定義目的地檔案中的 hello 自訂屬性名稱`nestingSeparator`(預設值是"。") 會使用的 tooidentify hello 巢狀層級從 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="c5d89-320">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") are used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="c5d89-321">這個區段是**選擇性**除非您想要比較的來源資料行名稱，toochange hello 屬性名稱，或是巢狀化某些 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-321">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="c5d89-322">AVRO 格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-322">AVRO format</span></span>
<span data-ttu-id="c5d89-323">如果您想 tooparse hello Avro 檔案，或寫入 Avro 格式中的 hello 資料，設定 hello `format` `type`屬性太**AvroFormat**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-323">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="c5d89-324">您不需要 toospecify hello typeProperties 區段中的 hello 格式 > 一節中的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-324">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="c5d89-325">範例：</span><span class="sxs-lookup"><span data-stu-id="c5d89-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="c5d89-326">toouse Avro 格式的 Hive 資料表中，您可以使用參照太[Apache Hive 教學課程](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-326">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="c5d89-327">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="c5d89-327">Note hello following points:</span></span>  

* <span data-ttu-id="c5d89-328">不支援[複雜資料類型](http://avro.apache.org/docs/current/spec.html#schema_complex) (記錄、列舉、陣列、對應、等位和固定)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="c5d89-329">ORC 格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-329">ORC format</span></span>
<span data-ttu-id="c5d89-330">如果您想 tooparse hello ORC 檔案，或寫入 ORC 格式中的 hello 資料，設定 hello `format` `type`屬性太**OrcFormat**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-330">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="c5d89-331">您不需要 toospecify hello typeProperties 區段中的 hello 格式 > 一節中的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-331">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="c5d89-332">範例：</span><span class="sxs-lookup"><span data-stu-id="c5d89-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="c5d89-333">如果您不複製 ORC 檔案**為-是**在內部部署和雲端之間資料存放區，您需要在閘道機器上的 tooinstall hello JRE 8 (Java Runtime Environment)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="c5d89-334">64 位元閘道需要 64 位元 JRE，而 32 位元閘道需要 32 位元 JRE。</span><span class="sxs-lookup"><span data-stu-id="c5d89-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="c5d89-335">您可以從 [這裡](http://go.microsoft.com/fwlink/?LinkId=808605)找到這兩個版本。</span><span class="sxs-lookup"><span data-stu-id="c5d89-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="c5d89-336">請選擇適當的一個 hello。</span><span class="sxs-lookup"><span data-stu-id="c5d89-336">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="c5d89-337">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="c5d89-337">Note hello following points:</span></span>

* <span data-ttu-id="c5d89-338">不支援複雜資料類型 (STRUCT、MAP、LIST、UNION)</span><span class="sxs-lookup"><span data-stu-id="c5d89-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="c5d89-339">ORC 檔案有 3 種 [壓縮相關選項](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/)︰NONE、ZLIB、SNAPPY。</span><span class="sxs-lookup"><span data-stu-id="c5d89-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="c5d89-340">Data Factory 支援以這些壓縮格式的任一項從 ORC 檔案讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c5d89-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="c5d89-341">它會使用 hello 壓縮轉碼器是 hello 中繼資料 tooread hello 資料中。</span><span class="sxs-lookup"><span data-stu-id="c5d89-341">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="c5d89-342">不過，在撰寫 tooan ORC 檔案時，Data Factory 選擇 ZLIB，ORC hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="c5d89-342">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="c5d89-343">目前沒有任何選項 toooverride 這種行為。</span><span class="sxs-lookup"><span data-stu-id="c5d89-343">Currently, there is no option toooverride this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="c5d89-344">Parquet 格式</span><span class="sxs-lookup"><span data-stu-id="c5d89-344">Parquet format</span></span>
<span data-ttu-id="c5d89-345">如果您想 tooparse hello Parquet 檔案，或寫入 Parquet 格式中的 hello 資料，設定 hello `format` `type`屬性太**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-345">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="c5d89-346">您不需要 toospecify hello typeProperties 區段中的 hello 格式 > 一節中的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-346">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="c5d89-347">範例：</span><span class="sxs-lookup"><span data-stu-id="c5d89-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="c5d89-348">如果您不複製 Parquet 檔案**為-是**在內部部署和雲端之間資料存放區，您需要在閘道機器上的 tooinstall hello JRE 8 (Java Runtime Environment)。</span><span class="sxs-lookup"><span data-stu-id="c5d89-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="c5d89-349">64 位元閘道需要 64 位元 JRE，而 32 位元閘道需要 32 位元 JRE。</span><span class="sxs-lookup"><span data-stu-id="c5d89-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="c5d89-350">您可以從 [這裡](http://go.microsoft.com/fwlink/?LinkId=808605)找到這兩個版本。</span><span class="sxs-lookup"><span data-stu-id="c5d89-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="c5d89-351">請選擇適當的一個 hello。</span><span class="sxs-lookup"><span data-stu-id="c5d89-351">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="c5d89-352">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="c5d89-352">Note hello following points:</span></span>

* <span data-ttu-id="c5d89-353">不支援複雜資料類型 (MAP、LIST)</span><span class="sxs-lookup"><span data-stu-id="c5d89-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="c5d89-354">Parquet 檔案具有下列相關的壓縮選項的 hello: NONE、 SNAPPY、 GZIP、 和 LZO。</span><span class="sxs-lookup"><span data-stu-id="c5d89-354">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="c5d89-355">Data Factory 支援以這些壓縮格式的任一項從 ORC 檔案讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c5d89-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="c5d89-356">它使用 hello 中繼資料 tooread hello 資料中的 hello 壓縮轉碼器。</span><span class="sxs-lookup"><span data-stu-id="c5d89-356">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="c5d89-357">不過，在撰寫 tooa Parquet 檔案時，Data Factory 選擇 SNAPPY，hello Parquet 格式的預設值。</span><span class="sxs-lookup"><span data-stu-id="c5d89-357">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="c5d89-358">目前沒有任何選項 toooverride 這種行為。</span><span class="sxs-lookup"><span data-stu-id="c5d89-358">Currently, there is no option toooverride this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="c5d89-359">壓縮支援</span><span class="sxs-lookup"><span data-stu-id="c5d89-359">Compression support</span></span>
<span data-ttu-id="c5d89-360">處理大型資料集可能會導致 I/O 和網路瓶頸。</span><span class="sxs-lookup"><span data-stu-id="c5d89-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="c5d89-361">因此，壓縮的資料存放區中可以加速資料傳輸 hello 網路上和節省磁碟空間，不僅也使效能大幅改善在處理大型資料。</span><span class="sxs-lookup"><span data-stu-id="c5d89-361">Therefore, compressed data in stores can not only speed up data transfer across hello network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="c5d89-362">目前，Azure Blob 或內部部署檔案系統等以檔案為基礎的資料存放區支援壓縮。</span><span class="sxs-lookup"><span data-stu-id="c5d89-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="c5d89-363">資料集，使用 hello toospecify 壓縮**壓縮**屬性集中 hello JSON 如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="c5d89-363">toospecify compression for a dataset, use hello **compression** property in hello dataset JSON as in hello following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="c5d89-364">假設 hello 範例資料集當做 hello 的複製活動的輸出，hello 複製活動壓縮 hello GZIP 轉碼器所使用的最佳比例輸出資料，並再寫入名為 pagecounts.csv.gz hello Azure Blob 儲存體中的檔案中的 hello 壓縮資料。</span><span class="sxs-lookup"><span data-stu-id="c5d89-364">Suppose hello sample dataset is used as hello output of a copy activity, hello copy activity compresses hello output data with GZIP codec using optimal ratio and then write hello compressed data into a file named pagecounts.csv.gz in hello Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="c5d89-365">Hello 中的資料不支援的壓縮設定**AvroFormat**， **OrcFormat**，或**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-365">Compression settings are not supported for data in hello **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="c5d89-366">當讀取這些格式的檔案，Data Factory 會偵測並使用 hello 中繼資料中的 hello 壓縮轉碼器。</span><span class="sxs-lookup"><span data-stu-id="c5d89-366">When reading files in these formats, Data Factory detects and uses hello compression codec in hello metadata.</span></span> <span data-ttu-id="c5d89-367">這些格式撰寫 toofiles，Data Factory 就可以選擇該格式的 hello 預設壓縮轉碼器。</span><span class="sxs-lookup"><span data-stu-id="c5d89-367">When writing toofiles in these formats, Data Factory chooses hello default compression codec for that format.</span></span> <span data-ttu-id="c5d89-368">例如，ZLIB for OrcFormat 和 SNAPPY for ParquetFormat。</span><span class="sxs-lookup"><span data-stu-id="c5d89-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="c5d89-369">hello**壓縮**區段有兩個屬性：</span><span class="sxs-lookup"><span data-stu-id="c5d89-369">hello **compression** section has two properties:</span></span>  

* <span data-ttu-id="c5d89-370">**類型：** hello 壓縮轉碼器，它可以是**GZIP**， **Deflate**， **BZIP2**，或**ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-370">**Type:** hello compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="c5d89-371">**層級：** hello 壓縮率，它可以是**最佳**或**最快**。</span><span class="sxs-lookup"><span data-stu-id="c5d89-371">**Level:** hello compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="c5d89-372">**最快：** hello 壓縮作業應該完成儘快，即使未以最佳方式壓縮 hello 產生的檔案。</span><span class="sxs-lookup"><span data-stu-id="c5d89-372">**Fastest:** hello compression operation should complete as quickly as possible, even if hello resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="c5d89-373">**最佳**: hello 壓縮作業應以最佳方式壓縮，即使 hello 作業需要花費較長的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="c5d89-373">**Optimal**: hello compression operation should be optimally compressed, even if hello operation takes a longer time toocomplete.</span></span>

    <span data-ttu-id="c5d89-374">如需詳細資訊，請參閱 [壓縮層級](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) 主題。</span><span class="sxs-lookup"><span data-stu-id="c5d89-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="c5d89-375">當您指定`compression`屬性中輸入的資料集 JSON hello 管線可以讀取壓縮的資料來源 hello; 和 hello 複製活動在 hello 屬性指定的輸出資料集 JSON 中時，可以寫入壓縮的資料 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="c5d89-375">When you specify `compression` property in an input dataset JSON, hello pipeline can read compressed data from hello source; and when you specify hello property in an output dataset JSON, hello copy activity can write compressed data toohello destination.</span></span> <span data-ttu-id="c5d89-376">以下是一些範例案例：</span><span class="sxs-lookup"><span data-stu-id="c5d89-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="c5d89-377">GZIP 壓縮資料從 Azure blob、 解壓縮，讀寫結果資料 tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="c5d89-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data tooan Azure SQL database.</span></span> <span data-ttu-id="c5d89-378">定義 hello 輸入的 Azure Blob 資料集以 hello `compression` `type` GZIP JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-378">You define hello input Azure Blob dataset with hello `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="c5d89-379">讀取純文字檔案從內部部署檔案系統中的資料、 壓縮會利用 GZip 格式和寫入 hello 壓縮資料 tooan Azure blob。</span><span class="sxs-lookup"><span data-stu-id="c5d89-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write hello compressed data tooan Azure blob.</span></span> <span data-ttu-id="c5d89-380">定義輸出 Azure Blob 資料集以 hello `compression` `type` GZip JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-380">You define an output Azure Blob dataset with hello `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="c5d89-381">從 FTP 伺服器讀取.zip 檔案解壓縮它 tooget hello 檔案內，並登陸那些檔案至 Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="c5d89-381">Read .zip file from FTP server, decompress it tooget hello files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="c5d89-382">定義輸入的 FTP 資料集以 hello `compression` `type` ZipDeflate JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="c5d89-382">You define an input FTP dataset with hello `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="c5d89-383">GZIP 壓縮的資料從 Azure blob、 將它解壓縮、 BZIP2，進行壓縮讀寫結果資料 tooan Azure blob。</span><span class="sxs-lookup"><span data-stu-id="c5d89-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data tooan Azure blob.</span></span> <span data-ttu-id="c5d89-384">定義 hello 輸入的 Azure Blob 資料集`compression``type`設定 tooGZIP 和 hello 與輸出資料集`compression``type`在此情況下設定 tooBZIP2。</span><span class="sxs-lookup"><span data-stu-id="c5d89-384">You define hello input Azure Blob dataset with `compression` `type` set tooGZIP and hello output dataset with `compression` `type` set tooBZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="c5d89-385">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5d89-385">Next steps</span></span>
<span data-ttu-id="c5d89-386">請參閱下列文章中的 Azure Data Factory 支援的檔案為基礎的資料存放區的 hello:</span><span class="sxs-lookup"><span data-stu-id="c5d89-386">See hello following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="c5d89-387">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="c5d89-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="c5d89-388">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c5d89-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="c5d89-389">FTP</span><span class="sxs-lookup"><span data-stu-id="c5d89-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="c5d89-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="c5d89-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="c5d89-391">檔案系統</span><span class="sxs-lookup"><span data-stu-id="c5d89-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="c5d89-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="c5d89-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
