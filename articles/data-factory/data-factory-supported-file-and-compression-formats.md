---
title: "Azure Data Factory 中的檔案和壓縮格式 | Microsoft Docs"
description: "了解 Azure Data Factory 所支援的檔案格式。"
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
ms.openlocfilehash: f4746e0dd249e417b8077a9bc733d2886daafdf2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="09bd0-104">了解 Azure Data Factory 所支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="09bd0-105">*此主題適用於下列連接器：[Amazon S3](data-factory-amazon-simple-storage-service-connector.md)、[Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md)、[檔案系統](data-factory-onprem-file-system-connector.md)、[FTP](data-factory-ftp-connector.md)、[HDFS](data-factory-hdfs-connector.md)、[HTTP](data-factory-http-connector.md) 與 [SFTP](data-factory-sftp-connector.md)。*</span><span class="sxs-lookup"><span data-stu-id="09bd0-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="09bd0-106">Azure Data Factory 支援下列檔案格式類型：</span><span class="sxs-lookup"><span data-stu-id="09bd0-106">Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="09bd0-107">文字格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="09bd0-108">JSON 格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="09bd0-109">Avro 格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="09bd0-110">ORC 格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="09bd0-111">Parquet 格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="09bd0-112">文字格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-112">Text format</span></span>
<span data-ttu-id="09bd0-113">如果您想要從文字檔讀取或寫入至文字檔，請將資料集之 `format` 區段中的 `type` 屬性設定成 **TextFormat**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="09bd0-114">您也可以在 `format` 區段中指定下列**選擇性**屬性。</span><span class="sxs-lookup"><span data-stu-id="09bd0-114">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="09bd0-115">關於如何設定，請參閱 [TextFormat 範例](#textformat-example)一節。</span><span class="sxs-lookup"><span data-stu-id="09bd0-115">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="09bd0-116">屬性</span><span class="sxs-lookup"><span data-stu-id="09bd0-116">Property</span></span> | <span data-ttu-id="09bd0-117">說明</span><span class="sxs-lookup"><span data-stu-id="09bd0-117">Description</span></span> | <span data-ttu-id="09bd0-118">允許的值</span><span class="sxs-lookup"><span data-stu-id="09bd0-118">Allowed values</span></span> | <span data-ttu-id="09bd0-119">必要</span><span class="sxs-lookup"><span data-stu-id="09bd0-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="09bd0-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="09bd0-120">columnDelimiter</span></span> |<span data-ttu-id="09bd0-121">用來分隔檔案中的資料行的字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-121">The character used to separate columns in a file.</span></span> <span data-ttu-id="09bd0-122">您可以考慮使用資料中不太可能存在的罕見不可列印字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="09bd0-123">例如，指定 "\u0001"，這代表「標題開頭」(SOH)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="09bd0-124">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-124">Only one character is allowed.</span></span> <span data-ttu-id="09bd0-125">**預設值**是**逗號 (',')**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-125">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="09bd0-126">若要使用 Unicode 字元，請參考 [Unicode 字元 (英文)](https://en.wikipedia.org/wiki/List_of_Unicode_characters) 以取得其對應的代碼。</span><span class="sxs-lookup"><span data-stu-id="09bd0-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="09bd0-127">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-127">No</span></span> |
| <span data-ttu-id="09bd0-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="09bd0-128">rowDelimiter</span></span> |<span data-ttu-id="09bd0-129">用來分隔檔案中的資料列的字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-129">The character used to separate rows in a file.</span></span> |<span data-ttu-id="09bd0-130">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-130">Only one character is allowed.</span></span> <span data-ttu-id="09bd0-131">**預設值**是下列任一個值：**["\r\n", "\r", "\n"]** (讀取時) 與 **"\r\n"** (寫入時)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="09bd0-132">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-132">No</span></span> |
| <span data-ttu-id="09bd0-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="09bd0-133">escapeChar</span></span> |<span data-ttu-id="09bd0-134">用來逸出輸入檔內容中的資料行分隔符號的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-134">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="09bd0-135">您無法同時為資料表指定 escapeChar 和 quoteChar。</span><span class="sxs-lookup"><span data-stu-id="09bd0-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="09bd0-136">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-136">Only one character is allowed.</span></span> <span data-ttu-id="09bd0-137">沒有預設值。</span><span class="sxs-lookup"><span data-stu-id="09bd0-137">No default value.</span></span> <br/><br/><span data-ttu-id="09bd0-138">例如，如果您以逗號 (',') 做為資料行分隔符號，但您想要在文字中使用逗號字元 (例如："Hello, world")，您可以定義 ‘$’ 做為逸出字元，並在來源中使用字串 "Hello$, world"。</span><span class="sxs-lookup"><span data-stu-id="09bd0-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="09bd0-139">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-139">No</span></span> |
| <span data-ttu-id="09bd0-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="09bd0-140">quoteChar</span></span> |<span data-ttu-id="09bd0-141">用來引用字串值的字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-141">The character used to quote a string value.</span></span> <span data-ttu-id="09bd0-142">引號字元內的資料行和資料列分隔符號會被視為字串值的一部分。</span><span class="sxs-lookup"><span data-stu-id="09bd0-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="09bd0-143">這個屬性同時適用於輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="09bd0-143">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="09bd0-144">您無法同時為資料表指定 escapeChar 和 quoteChar。</span><span class="sxs-lookup"><span data-stu-id="09bd0-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="09bd0-145">只允許一個字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-145">Only one character is allowed.</span></span> <span data-ttu-id="09bd0-146">沒有預設值。</span><span class="sxs-lookup"><span data-stu-id="09bd0-146">No default value.</span></span> <br/><br/><span data-ttu-id="09bd0-147">例如，如果您以逗號 (',') 做為資料行分隔符號，但您想要在文字中使用逗號字元 (例如：<Hello, world>)，您可以定義 " (雙引號) 做為引用字元，並在來源中使用字串 "Hello, world"。</span><span class="sxs-lookup"><span data-stu-id="09bd0-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="09bd0-148">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-148">No</span></span> |
| <span data-ttu-id="09bd0-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="09bd0-149">nullValue</span></span> |<span data-ttu-id="09bd0-150">用來代表 null 值的一個或多個字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-150">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="09bd0-151">一或多個字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-151">One or more characters.</span></span> <span data-ttu-id="09bd0-152">**預設值**為 **"\N" 和 "NULL"** (讀取時) 及 **"\N"** (寫入時)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="09bd0-153">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-153">No</span></span> |
| <span data-ttu-id="09bd0-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="09bd0-154">encodingName</span></span> |<span data-ttu-id="09bd0-155">指定編碼名稱。</span><span class="sxs-lookup"><span data-stu-id="09bd0-155">Specify the encoding name.</span></span> |<span data-ttu-id="09bd0-156">有效的編碼名稱。</span><span class="sxs-lookup"><span data-stu-id="09bd0-156">A valid encoding name.</span></span> <span data-ttu-id="09bd0-157">請參閱 [Encoding.EncodingName 屬性](https://msdn.microsoft.com/library/system.text.encoding.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="09bd0-158">例如：windows-1250 或 shift_jis。</span><span class="sxs-lookup"><span data-stu-id="09bd0-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="09bd0-159">**預設值**為 **UTF-8**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-159">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="09bd0-160">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-160">No</span></span> |
| <span data-ttu-id="09bd0-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="09bd0-161">firstRowAsHeader</span></span> |<span data-ttu-id="09bd0-162">指定是否將第一個資料列視為標頭。</span><span class="sxs-lookup"><span data-stu-id="09bd0-162">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="09bd0-163">對於輸入資料集，Data Factory 會讀取第一個資料列做為標頭。</span><span class="sxs-lookup"><span data-stu-id="09bd0-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="09bd0-164">對於輸出資料集，Data Factory 會寫入第一個資料列做為標頭。</span><span class="sxs-lookup"><span data-stu-id="09bd0-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="09bd0-165">相關範例案例請參閱[使用 `firstRowAsHeader` 和 `skipLineCount` 的案例](#scenarios-for-using-firstrowasheader-and-skiplinecount)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="09bd0-166">True</span><span class="sxs-lookup"><span data-stu-id="09bd0-166">True</span></span><br/><span data-ttu-id="09bd0-167"><b>False (預設值)</b></span><span class="sxs-lookup"><span data-stu-id="09bd0-167"><b>False (default)</b></span></span> |<span data-ttu-id="09bd0-168">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-168">No</span></span> |
| <span data-ttu-id="09bd0-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="09bd0-169">skipLineCount</span></span> |<span data-ttu-id="09bd0-170">表示從輸入檔讀取資料時要略過的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="09bd0-170">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="09bd0-171">如果指定 skipLineCount 和 firstRowAsHeader，則會先略過程式碼行，再從輸入檔讀取標頭資訊。</span><span class="sxs-lookup"><span data-stu-id="09bd0-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="09bd0-172">相關範例案例請參閱[使用 `firstRowAsHeader` 和 `skipLineCount` 的案例](#scenarios-for-using-firstrowasheader-and-skiplinecount)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="09bd0-173">Integer</span><span class="sxs-lookup"><span data-stu-id="09bd0-173">Integer</span></span> |<span data-ttu-id="09bd0-174">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-174">No</span></span> |
| <span data-ttu-id="09bd0-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="09bd0-175">treatEmptyAsNull</span></span> |<span data-ttu-id="09bd0-176">指定從輸入檔讀取資料時，是否將 null 或空字串視為 null 值。</span><span class="sxs-lookup"><span data-stu-id="09bd0-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="09bd0-177">**True (預設值)**</span><span class="sxs-lookup"><span data-stu-id="09bd0-177">**True (default)**</span></span><br/><span data-ttu-id="09bd0-178">False</span><span class="sxs-lookup"><span data-stu-id="09bd0-178">False</span></span> |<span data-ttu-id="09bd0-179">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="09bd0-180">TextFormat 範例</span><span class="sxs-lookup"><span data-stu-id="09bd0-180">TextFormat example</span></span>
<span data-ttu-id="09bd0-181">在以下的資料集 JSON 定義中，已指定一些選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="09bd0-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

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

<span data-ttu-id="09bd0-182">若要使用 `escapeChar` 而不是`quoteChar`，請使用下列 escapeChar 取代含有 `quoteChar` 的那一行：</span><span class="sxs-lookup"><span data-stu-id="09bd0-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="09bd0-183">使用 firstRowAsHeader 和 skipLineCount 的案例</span><span class="sxs-lookup"><span data-stu-id="09bd0-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="09bd0-184">您正從非檔案來源複製到文字檔，並想要加入標頭行，其中包含結構描述中繼資料 (例如︰SQL 結構描述)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="09bd0-185">在此案例的輸出資料集，將 `firstRowAsHeader` 指定為 true。</span><span class="sxs-lookup"><span data-stu-id="09bd0-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="09bd0-186">您正從包含標頭行的文字檔複製到非檔案接收器，並想要刪除那一行。</span><span class="sxs-lookup"><span data-stu-id="09bd0-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="09bd0-187">在輸入資料集，將 `firstRowAsHeader` 指定為 true。</span><span class="sxs-lookup"><span data-stu-id="09bd0-187">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="09bd0-188">您正從文字檔複製，並想略過不包含資料或標頭資訊的開頭幾行。</span><span class="sxs-lookup"><span data-stu-id="09bd0-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="09bd0-189">指定 `skipLineCount` 以表示要略過的行數。</span><span class="sxs-lookup"><span data-stu-id="09bd0-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="09bd0-190">如果檔案其餘部分包含標頭行，您也可以指定 `firstRowAsHeader`。</span><span class="sxs-lookup"><span data-stu-id="09bd0-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="09bd0-191">如果 `skipLineCount` 和 `firstRowAsHeader` 都指定，則會先略過那幾行，再從輸入檔讀取標頭資訊</span><span class="sxs-lookup"><span data-stu-id="09bd0-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="09bd0-192">JSON 格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-192">JSON format</span></span>
<span data-ttu-id="09bd0-193">若要**將 JSON 檔案原封不動匯入到 Azure Cosmos DB 或從中匯出**，請參閱[將資料移進/移出 Azure Cosmos DB](data-factory-azure-documentdb-connector.md) 一文中的[匯入/匯出 JSON 文件](data-factory-azure-documentdb-connector.md#importexport-json-documents)一節。</span><span class="sxs-lookup"><span data-stu-id="09bd0-193">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="09bd0-194">如果您想要剖析 JSON 檔案，或以 JSON 格式寫入資料，請將 `format` 區段中的 `type` 屬性設定成 **JsonFormat**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="09bd0-195">您也可以在 `format` 區段中指定下列**選擇性**屬性。</span><span class="sxs-lookup"><span data-stu-id="09bd0-195">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="09bd0-196">關於如何設定，請參閱 [JsonFormat 範例](#jsonformat-example)一節。</span><span class="sxs-lookup"><span data-stu-id="09bd0-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="09bd0-197">屬性</span><span class="sxs-lookup"><span data-stu-id="09bd0-197">Property</span></span> | <span data-ttu-id="09bd0-198">說明</span><span class="sxs-lookup"><span data-stu-id="09bd0-198">Description</span></span> | <span data-ttu-id="09bd0-199">必要</span><span class="sxs-lookup"><span data-stu-id="09bd0-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09bd0-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="09bd0-200">filePattern</span></span> |<span data-ttu-id="09bd0-201">表示每個 JSON 檔案中儲存的資料模式。</span><span class="sxs-lookup"><span data-stu-id="09bd0-201">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="09bd0-202">允許的值為︰**setOfObjects** 和 **arrayOfObjects**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="09bd0-203">**預設值**為 **setOfObjects**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-203">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="09bd0-204">關於這些模式的詳細資訊，請參閱 [JSON 檔案模式](#json-file-patterns)一節。</span><span class="sxs-lookup"><span data-stu-id="09bd0-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="09bd0-205">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-205">No</span></span> |
| <span data-ttu-id="09bd0-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="09bd0-206">jsonNodeReference</span></span> | <span data-ttu-id="09bd0-207">如果您想要逐一查看陣列欄位內相同模式的物件並擷取資料，請指定該陣列的 JSON 路徑。</span><span class="sxs-lookup"><span data-stu-id="09bd0-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="09bd0-208">從 JSON 檔案複製資料時，才支援這個屬性。</span><span class="sxs-lookup"><span data-stu-id="09bd0-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="09bd0-209">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-209">No</span></span> |
| <span data-ttu-id="09bd0-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="09bd0-210">jsonPathDefinition</span></span> | <span data-ttu-id="09bd0-211">指定 JSON 路徑運算式，以自訂資料行名稱來對應每個資料行 (開頭為小寫)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="09bd0-212">從 JSON 檔案複製資料時，才支援這個屬性，您可以從物件或陣列中擷取資料。</span><span class="sxs-lookup"><span data-stu-id="09bd0-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="09bd0-213">如果是根物件下的欄位，請從根 $ 開始，如果是 `jsonNodeReference` 屬性所選陣列內的欄位，請從陣列元素開始。</span><span class="sxs-lookup"><span data-stu-id="09bd0-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="09bd0-214">關於如何設定，請參閱 [JsonFormat 範例](#jsonformat-example)一節。</span><span class="sxs-lookup"><span data-stu-id="09bd0-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="09bd0-215">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-215">No</span></span> |
| <span data-ttu-id="09bd0-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="09bd0-216">encodingName</span></span> |<span data-ttu-id="09bd0-217">指定編碼名稱。</span><span class="sxs-lookup"><span data-stu-id="09bd0-217">Specify the encoding name.</span></span> <span data-ttu-id="09bd0-218">如需有效編碼名稱的清單，請參閱： [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) 屬性。</span><span class="sxs-lookup"><span data-stu-id="09bd0-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="09bd0-219">例如：windows-1250 或 shift_jis。</span><span class="sxs-lookup"><span data-stu-id="09bd0-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="09bd0-220">**預設值**為 **UTF-8**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-220">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="09bd0-221">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-221">No</span></span> |
| <span data-ttu-id="09bd0-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="09bd0-222">nestingSeparator</span></span> |<span data-ttu-id="09bd0-223">用來分隔巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="09bd0-223">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="09bd0-224">預設值為 '.' (點)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-224">The default value is '.' (dot).</span></span> |<span data-ttu-id="09bd0-225">否</span><span class="sxs-lookup"><span data-stu-id="09bd0-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="09bd0-226">JSON 檔案模式</span><span class="sxs-lookup"><span data-stu-id="09bd0-226">JSON file patterns</span></span>

<span data-ttu-id="09bd0-227">複製活動可以剖析下列 JSON 檔案模式︰</span><span class="sxs-lookup"><span data-stu-id="09bd0-227">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="09bd0-228">**類型 I：setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="09bd0-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="09bd0-229">每個檔案都會包含單一物件，或以行分隔/串連的多個物件。</span><span class="sxs-lookup"><span data-stu-id="09bd0-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="09bd0-230">在輸出資料集中選擇此選項時，複製活動會產生單一 JSON 檔案，每行一個物件 (以行分隔)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="09bd0-231">**單一物件 JSON 範例**</span><span class="sxs-lookup"><span data-stu-id="09bd0-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="09bd0-232">**以行分隔的 JSON 範例**</span><span class="sxs-lookup"><span data-stu-id="09bd0-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="09bd0-233">**串連的 JSON 範例**</span><span class="sxs-lookup"><span data-stu-id="09bd0-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="09bd0-234">**類型 II：arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="09bd0-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="09bd0-235">每個檔案都會包含物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="09bd0-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="09bd0-236">JsonFormat 範例</span><span class="sxs-lookup"><span data-stu-id="09bd0-236">JsonFormat example</span></span>

<span data-ttu-id="09bd0-237">**案例 1︰從 JSON 檔案複製資料**</span><span class="sxs-lookup"><span data-stu-id="09bd0-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="09bd0-238">從 JSON 檔案複製資料時，請參閱以下兩個範例。</span><span class="sxs-lookup"><span data-stu-id="09bd0-238">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="09bd0-239">一般注意事項：</span><span class="sxs-lookup"><span data-stu-id="09bd0-239">The generic points to note:</span></span>

<span data-ttu-id="09bd0-240">**範例 1︰從物件和陣列擷取資料**</span><span class="sxs-lookup"><span data-stu-id="09bd0-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="09bd0-241">在此範例中，預計會有一個根 JSON 物件對應至表格式結果中的單一記錄。</span><span class="sxs-lookup"><span data-stu-id="09bd0-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="09bd0-242">如果您的 JSON 檔案含有下列內容：</span><span class="sxs-lookup"><span data-stu-id="09bd0-242">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="09bd0-243">而且想要使用下列格式，將它複製到 Azure SQL 資料表，請同時從物件和陣列擷取資料︰</span><span class="sxs-lookup"><span data-stu-id="09bd0-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="09bd0-244">id</span><span class="sxs-lookup"><span data-stu-id="09bd0-244">id</span></span> | <span data-ttu-id="09bd0-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="09bd0-245">deviceType</span></span> | <span data-ttu-id="09bd0-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="09bd0-246">targetResourceType</span></span> | <span data-ttu-id="09bd0-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="09bd0-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="09bd0-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="09bd0-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="09bd0-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="09bd0-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="09bd0-250">PC</span><span class="sxs-lookup"><span data-stu-id="09bd0-250">PC</span></span> | <span data-ttu-id="09bd0-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="09bd0-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="09bd0-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="09bd0-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="09bd0-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="09bd0-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="09bd0-254">**JsonFormat** 類型的輸入資料集定義如下：(僅含相關元素的局部定義)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="09bd0-255">具體而言：</span><span class="sxs-lookup"><span data-stu-id="09bd0-255">More specifically:</span></span>

- <span data-ttu-id="09bd0-256">`structure` 區段定義自訂資料行名稱，以及轉換成表格式資料時對應的資料類型。</span><span class="sxs-lookup"><span data-stu-id="09bd0-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="09bd0-257">除非您需要對應資料行，否則這個區段是**選擇性**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-257">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="09bd0-258">如需詳細資訊，請參閱[將來源資料集資料行對應至目的地資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-258">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="09bd0-259">`jsonPathDefinition` 指定每個資料行的 JSON 路徑，以指出從哪裡擷取資料。</span><span class="sxs-lookup"><span data-stu-id="09bd0-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="09bd0-260">若要從陣列複製資料，您可以使用 **array[x].property** 從第 x 個物件擷取指定屬性的值，也可以使用 **array[*].property** 從包含這類屬性的物件中尋找此值。</span><span class="sxs-lookup"><span data-stu-id="09bd0-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="09bd0-261">**範例 2︰交叉套用陣列中具有相同模式的多個物件**</span><span class="sxs-lookup"><span data-stu-id="09bd0-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="09bd0-262">在此範例中，預計會將一個根 JSON 物件轉換成表格式結果中的多筆記錄。</span><span class="sxs-lookup"><span data-stu-id="09bd0-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="09bd0-263">如果您的 JSON 檔案含有下列內容：</span><span class="sxs-lookup"><span data-stu-id="09bd0-263">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="09bd0-264">您想要簡維陣列內的資料，將內容複製到下列格式的 Azure SQL 資料表，並與一般根資訊交叉聯結︰</span><span class="sxs-lookup"><span data-stu-id="09bd0-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="09bd0-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="09bd0-265">ordernumber</span></span> | <span data-ttu-id="09bd0-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="09bd0-266">orderdate</span></span> | <span data-ttu-id="09bd0-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="09bd0-267">order_pd</span></span> | <span data-ttu-id="09bd0-268">order_price</span><span class="sxs-lookup"><span data-stu-id="09bd0-268">order_price</span></span> | <span data-ttu-id="09bd0-269">city</span><span class="sxs-lookup"><span data-stu-id="09bd0-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="09bd0-270">01</span><span class="sxs-lookup"><span data-stu-id="09bd0-270">01</span></span> | <span data-ttu-id="09bd0-271">20170122</span><span class="sxs-lookup"><span data-stu-id="09bd0-271">20170122</span></span> | <span data-ttu-id="09bd0-272">P1</span><span class="sxs-lookup"><span data-stu-id="09bd0-272">P1</span></span> | <span data-ttu-id="09bd0-273">23</span><span class="sxs-lookup"><span data-stu-id="09bd0-273">23</span></span> | <span data-ttu-id="09bd0-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="09bd0-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="09bd0-275">01</span><span class="sxs-lookup"><span data-stu-id="09bd0-275">01</span></span> | <span data-ttu-id="09bd0-276">20170122</span><span class="sxs-lookup"><span data-stu-id="09bd0-276">20170122</span></span> | <span data-ttu-id="09bd0-277">P2</span><span class="sxs-lookup"><span data-stu-id="09bd0-277">P2</span></span> | <span data-ttu-id="09bd0-278">13</span><span class="sxs-lookup"><span data-stu-id="09bd0-278">13</span></span> | <span data-ttu-id="09bd0-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="09bd0-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="09bd0-280">01</span><span class="sxs-lookup"><span data-stu-id="09bd0-280">01</span></span> | <span data-ttu-id="09bd0-281">20170122</span><span class="sxs-lookup"><span data-stu-id="09bd0-281">20170122</span></span> | <span data-ttu-id="09bd0-282">P3</span><span class="sxs-lookup"><span data-stu-id="09bd0-282">P3</span></span> | <span data-ttu-id="09bd0-283">231</span><span class="sxs-lookup"><span data-stu-id="09bd0-283">231</span></span> | <span data-ttu-id="09bd0-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="09bd0-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="09bd0-285">**JsonFormat** 類型的輸入資料集定義如下：(僅含相關元素的局部定義)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="09bd0-286">具體而言：</span><span class="sxs-lookup"><span data-stu-id="09bd0-286">More specifically:</span></span>

- <span data-ttu-id="09bd0-287">`structure` 區段定義自訂資料行名稱，以及轉換成表格式資料時對應的資料類型。</span><span class="sxs-lookup"><span data-stu-id="09bd0-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="09bd0-288">除非您需要對應資料行，否則這個區段是**選擇性**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-288">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="09bd0-289">如需詳細資訊，請參閱[將來源資料集資料行對應至目的地資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-289">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="09bd0-290">`jsonNodeReference` 表示逐一查看**陣列** orderlines 下相同模式的物件並擷取資料。</span><span class="sxs-lookup"><span data-stu-id="09bd0-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="09bd0-291">`jsonPathDefinition` 指定每個資料行的 JSON 路徑，以指出從哪裡擷取資料。</span><span class="sxs-lookup"><span data-stu-id="09bd0-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="09bd0-292">在此範例中，"ordernumber"、"orderdate" 和 "city" 位於根物件下，JSON 路徑開頭為 "$."，而 "order_pd" 和 "order_price" 以衍生自陣列元素的路徑定義，不含 "$."。</span><span class="sxs-lookup"><span data-stu-id="09bd0-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="09bd0-293">**請注意下列幾點**：</span><span class="sxs-lookup"><span data-stu-id="09bd0-293">**Note the following points:**</span></span>

* <span data-ttu-id="09bd0-294">如果 Data Factory 資料集中未定義 `structure`和 `jsonPathDefinition`，複製活動會偵測第一個物件的結構描述，並簡維整個物件。</span><span class="sxs-lookup"><span data-stu-id="09bd0-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="09bd0-295">如果 JSON 輸入具有陣列，依預設，複製活動會將整個陣列值轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="09bd0-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="09bd0-296">您可以選擇使用 `jsonNodeReference` 及/或 `jsonPathDefinition` 從其中擷取資料，或不要在 `jsonPathDefinition` 中指定以略過它。</span><span class="sxs-lookup"><span data-stu-id="09bd0-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="09bd0-297">如果相同層級中有重複的名稱，複製活動會挑選最後一個。</span><span class="sxs-lookup"><span data-stu-id="09bd0-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="09bd0-298">屬性名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="09bd0-298">Property names are case-sensitive.</span></span> <span data-ttu-id="09bd0-299">名稱相同但大小寫不同的兩個屬性會被視為兩個不同的屬性。</span><span class="sxs-lookup"><span data-stu-id="09bd0-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="09bd0-300">**案例 2︰將資料寫入 JSON 檔案**</span><span class="sxs-lookup"><span data-stu-id="09bd0-300">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="09bd0-301">如果您在 SQL Database 中有下列資料表︰</span><span class="sxs-lookup"><span data-stu-id="09bd0-301">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="09bd0-302">id</span><span class="sxs-lookup"><span data-stu-id="09bd0-302">id</span></span> | <span data-ttu-id="09bd0-303">order_date</span><span class="sxs-lookup"><span data-stu-id="09bd0-303">order_date</span></span> | <span data-ttu-id="09bd0-304">order_price</span><span class="sxs-lookup"><span data-stu-id="09bd0-304">order_price</span></span> | <span data-ttu-id="09bd0-305">order_by</span><span class="sxs-lookup"><span data-stu-id="09bd0-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="09bd0-306">1</span><span class="sxs-lookup"><span data-stu-id="09bd0-306">1</span></span> | <span data-ttu-id="09bd0-307">20170119</span><span class="sxs-lookup"><span data-stu-id="09bd0-307">20170119</span></span> | <span data-ttu-id="09bd0-308">2000</span><span class="sxs-lookup"><span data-stu-id="09bd0-308">2000</span></span> | <span data-ttu-id="09bd0-309">David</span><span class="sxs-lookup"><span data-stu-id="09bd0-309">David</span></span> |
| <span data-ttu-id="09bd0-310">2</span><span class="sxs-lookup"><span data-stu-id="09bd0-310">2</span></span> | <span data-ttu-id="09bd0-311">20170120</span><span class="sxs-lookup"><span data-stu-id="09bd0-311">20170120</span></span> | <span data-ttu-id="09bd0-312">3500</span><span class="sxs-lookup"><span data-stu-id="09bd0-312">3500</span></span> | <span data-ttu-id="09bd0-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="09bd0-313">Patrick</span></span> |
| <span data-ttu-id="09bd0-314">3</span><span class="sxs-lookup"><span data-stu-id="09bd0-314">3</span></span> | <span data-ttu-id="09bd0-315">20170121</span><span class="sxs-lookup"><span data-stu-id="09bd0-315">20170121</span></span> | <span data-ttu-id="09bd0-316">4000</span><span class="sxs-lookup"><span data-stu-id="09bd0-316">4000</span></span> | <span data-ttu-id="09bd0-317">Jason</span><span class="sxs-lookup"><span data-stu-id="09bd0-317">Jason</span></span> |

<span data-ttu-id="09bd0-318">而針對每一筆記錄，您預期以下列格式寫入 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="09bd0-318">and for each record, you expect to write to a JSON object in the following format:</span></span>
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

<span data-ttu-id="09bd0-319">**JsonFormat** 類型的輸出資料集定義如下：(僅含相關元素的局部定義)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="09bd0-320">更具體來說，`structure` 區段會定義目的檔案中的自訂屬性名稱，`nestingSeparator` (預設值是 ".") 則用來識別名稱中的巢狀層。</span><span class="sxs-lookup"><span data-stu-id="09bd0-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="09bd0-321">除非您想要變更屬性名稱與來源資料行名稱之間的對照，或巢狀化某些屬性，否則這個區段是**選擇性**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="09bd0-322">AVRO 格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-322">AVRO format</span></span>
<span data-ttu-id="09bd0-323">如果您想要剖析 Avro 檔案，或以 Avro 格式寫入資料，請將 `format``type` 屬性設定為 **AvroFormat**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="09bd0-324">您不需要在 typeProperties 區段內的 Format 區段中指定任何屬性。</span><span class="sxs-lookup"><span data-stu-id="09bd0-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="09bd0-325">範例：</span><span class="sxs-lookup"><span data-stu-id="09bd0-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="09bd0-326">若要在 Hive 資料表中使用 Avro 格式，您可以參考 [Apache Hive 的教學課程](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="09bd0-327">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="09bd0-327">Note the following points:</span></span>  

* <span data-ttu-id="09bd0-328">不支援[複雜資料類型](http://avro.apache.org/docs/current/spec.html#schema_complex) (記錄、列舉、陣列、對應、等位和固定)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="09bd0-329">ORC 格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-329">ORC format</span></span>
<span data-ttu-id="09bd0-330">如果您想要剖析 ORC 檔案，或以 ORC 格式寫入資料，請將 `format``type` 屬性設定為 **OrcFormat**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="09bd0-331">您不需要在 typeProperties 區段內的 Format 區段中指定任何屬性。</span><span class="sxs-lookup"><span data-stu-id="09bd0-331">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="09bd0-332">範例：</span><span class="sxs-lookup"><span data-stu-id="09bd0-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="09bd0-333">如果您不會在內部部署與雲端資料存放區之間複製 ORC 檔案 **as-is** ，您需要在閘道機器上安裝 JRE 8 (Java 執行階段環境)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="09bd0-334">64 位元閘道需要 64 位元 JRE，而 32 位元閘道需要 32 位元 JRE。</span><span class="sxs-lookup"><span data-stu-id="09bd0-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="09bd0-335">您可以從 [這裡](http://go.microsoft.com/fwlink/?LinkId=808605)找到這兩個版本。</span><span class="sxs-lookup"><span data-stu-id="09bd0-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="09bd0-336">請選擇適當的版本。</span><span class="sxs-lookup"><span data-stu-id="09bd0-336">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="09bd0-337">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="09bd0-337">Note the following points:</span></span>

* <span data-ttu-id="09bd0-338">不支援複雜資料類型 (STRUCT、MAP、LIST、UNION)</span><span class="sxs-lookup"><span data-stu-id="09bd0-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="09bd0-339">ORC 檔案有 3 種 [壓縮相關選項](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/)︰NONE、ZLIB、SNAPPY。</span><span class="sxs-lookup"><span data-stu-id="09bd0-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="09bd0-340">Data Factory 支援以這些壓縮格式的任一項從 ORC 檔案讀取資料。</span><span class="sxs-lookup"><span data-stu-id="09bd0-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="09bd0-341">它會使用中繼資料裡的壓縮轉碼器來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="09bd0-341">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="09bd0-342">不過，寫入 ORC 檔案時，Data Factory 會選擇 ZLIB，這是 ORC 的預設值。</span><span class="sxs-lookup"><span data-stu-id="09bd0-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="09bd0-343">目前沒有任何選項可覆寫這個行為。</span><span class="sxs-lookup"><span data-stu-id="09bd0-343">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="09bd0-344">Parquet 格式</span><span class="sxs-lookup"><span data-stu-id="09bd0-344">Parquet format</span></span>
<span data-ttu-id="09bd0-345">如果您想要剖析 Parquet 檔案，或以 Parquet 格式寫入資料，請將 `format``type` 屬性設定為 **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="09bd0-346">您不需要在 typeProperties 區段內的 Format 區段中指定任何屬性。</span><span class="sxs-lookup"><span data-stu-id="09bd0-346">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="09bd0-347">範例：</span><span class="sxs-lookup"><span data-stu-id="09bd0-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="09bd0-348">如果您不是在內部部署與雲端資料存放區之間 **以原狀直接** 複製 Parquet 檔案，您需要在閘道機器上安裝 JRE 8 (Java 執行階段環境)。</span><span class="sxs-lookup"><span data-stu-id="09bd0-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="09bd0-349">64 位元閘道需要 64 位元 JRE，而 32 位元閘道需要 32 位元 JRE。</span><span class="sxs-lookup"><span data-stu-id="09bd0-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="09bd0-350">您可以從 [這裡](http://go.microsoft.com/fwlink/?LinkId=808605)找到這兩個版本。</span><span class="sxs-lookup"><span data-stu-id="09bd0-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="09bd0-351">請選擇適當的版本。</span><span class="sxs-lookup"><span data-stu-id="09bd0-351">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="09bd0-352">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="09bd0-352">Note the following points:</span></span>

* <span data-ttu-id="09bd0-353">不支援複雜資料類型 (MAP、LIST)</span><span class="sxs-lookup"><span data-stu-id="09bd0-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="09bd0-354">Parquet 檔案已有下列壓縮相關選項：NONE、SNAPPY、GZIP 和 LZO。</span><span class="sxs-lookup"><span data-stu-id="09bd0-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="09bd0-355">Data Factory 支援以這些壓縮格式的任一項從 ORC 檔案讀取資料。</span><span class="sxs-lookup"><span data-stu-id="09bd0-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="09bd0-356">它會使用中繼資料裡的壓縮轉碼器來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="09bd0-356">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="09bd0-357">不過，寫入 Parquet 檔案時，Data Factory 會選擇 SNAPPY，這是 Parquet 格式的預設值。</span><span class="sxs-lookup"><span data-stu-id="09bd0-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="09bd0-358">目前沒有任何選項可覆寫這個行為。</span><span class="sxs-lookup"><span data-stu-id="09bd0-358">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="09bd0-359">壓縮支援</span><span class="sxs-lookup"><span data-stu-id="09bd0-359">Compression support</span></span>
<span data-ttu-id="09bd0-360">處理大型資料集可能會導致 I/O 和網路瓶頸。</span><span class="sxs-lookup"><span data-stu-id="09bd0-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="09bd0-361">因此，存放區中的壓縮資料不但可以跨網路加速資料傳輸和節省磁碟空間，也能在處理巨量資料時帶來顯著的效能提升。</span><span class="sxs-lookup"><span data-stu-id="09bd0-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="09bd0-362">目前，Azure Blob 或內部部署檔案系統等以檔案為基礎的資料存放區支援壓縮。</span><span class="sxs-lookup"><span data-stu-id="09bd0-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="09bd0-363">若要指定資料集的壓縮，請使用資料集 JSON 中的 **壓縮** 屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="09bd0-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

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

<span data-ttu-id="09bd0-364">假設範例資料集是用來作為複製活動的輸出，則複製活動會使用 GZIP 轉碼器以最佳比率壓縮輸出資料，然後將壓縮的資料寫入到「Azure Blob 儲存體」中名為 pagecounts.csv.gz 的檔案。</span><span class="sxs-lookup"><span data-stu-id="09bd0-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="09bd0-365">不支援 **AvroFormat**、**OrcFormat** 或 **ParquetFormat** 的資料壓縮設定。</span><span class="sxs-lookup"><span data-stu-id="09bd0-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="09bd0-366">讀取這些格式的檔案時，Data Factory 會偵測並使用中繼資料中的壓縮轉碼器。</span><span class="sxs-lookup"><span data-stu-id="09bd0-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="09bd0-367">寫入這些格式的檔案時，Data Factory 會選擇該格式的預設壓縮轉碼器。</span><span class="sxs-lookup"><span data-stu-id="09bd0-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="09bd0-368">例如，ZLIB for OrcFormat 和 SNAPPY for ParquetFormat。</span><span class="sxs-lookup"><span data-stu-id="09bd0-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="09bd0-369">[壓縮]  區段有兩個屬性：</span><span class="sxs-lookup"><span data-stu-id="09bd0-369">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="09bd0-370">**類型：**壓縮轉碼器，可以是 **GZIP**、**Deflate**、**BZIP2** 或 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="09bd0-371">**層級：**壓縮比，它可以是**最佳**或**最快**。</span><span class="sxs-lookup"><span data-stu-id="09bd0-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="09bd0-372">**最快：** 即使未以最佳方式壓縮所產生的檔案，壓縮作業也應儘速完成。</span><span class="sxs-lookup"><span data-stu-id="09bd0-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="09bd0-373">**最佳**：即使作業耗費較長的時間才能完成，壓縮作業也應以最佳方式壓縮。</span><span class="sxs-lookup"><span data-stu-id="09bd0-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="09bd0-374">如需詳細資訊，請參閱 [壓縮層級](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) 主題。</span><span class="sxs-lookup"><span data-stu-id="09bd0-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="09bd0-375">當您在輸入資料集 JSON 中指定 `compression` 屬性時，管線可以從來源讀取壓縮的資料，當您在輸出資料集 JSON 中指定屬性，複製活動可以將壓縮的資料寫入到目的地。</span><span class="sxs-lookup"><span data-stu-id="09bd0-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="09bd0-376">以下是一些範例案例：</span><span class="sxs-lookup"><span data-stu-id="09bd0-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="09bd0-377">從 Azure blob 讀取 GZIP 壓縮資料，將其解壓縮，並將結果資料寫入到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="09bd0-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="09bd0-378">您可以利用設為 GZIP 的 `compression` `type` JSON 屬性，定義輸入 Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="09bd0-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="09bd0-379">從來自內部部署檔案系統之純文字檔案讀取資料、使用 GZip 格式加以壓縮並將壓縮的資料寫入到 Azure blob。</span><span class="sxs-lookup"><span data-stu-id="09bd0-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="09bd0-380">您可以利用設為 GZip 的 `compression` `type` JSON 屬性，定義輸出 Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="09bd0-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="09bd0-381">從 FTP 伺服器讀取.zip 檔、將它解壓縮以取得其中的檔案，並將這些檔案放入 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="09bd0-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="09bd0-382">您可以利用設為 ZipDeflate 的 `compression` `type` JSON 屬性，定義輸入 FTP 資料集。</span><span class="sxs-lookup"><span data-stu-id="09bd0-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="09bd0-383">從 Azure blob 讀取 GZIP 壓縮資料，將其解壓縮、使用 BZIP2 將其壓縮，並將結果資料寫入到 Azure blob。</span><span class="sxs-lookup"><span data-stu-id="09bd0-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="09bd0-384">您會在此情況下利用設為 GZIP 的 `compression` `type` 定義輸入 Azure Blob 資料集，並利用設為 BZIP2 的 `compression` `type` 定義輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="09bd0-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="09bd0-385">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09bd0-385">Next steps</span></span>
<span data-ttu-id="09bd0-386">如需 Azure Data Factory 所支援的檔案型資料存放區，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="09bd0-386">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="09bd0-387">Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="09bd0-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="09bd0-388">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="09bd0-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="09bd0-389">FTP</span><span class="sxs-lookup"><span data-stu-id="09bd0-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="09bd0-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="09bd0-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="09bd0-391">檔案系統</span><span class="sxs-lookup"><span data-stu-id="09bd0-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="09bd0-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="09bd0-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
