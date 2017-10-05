---
title: "Azure Functions 外部檔案繫結 (預覽) | Microsoft Docs"
description: "使用 Azure Functions 中的外部檔案繫結"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 2082e4e9b23271be93f3e3ab43997c3243238da8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="6fb81-103">Azure Functions 外部檔案繫結 (預覽)</span><span class="sxs-lookup"><span data-stu-id="6fb81-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="6fb81-104">本文說明如何利用內建繫結，在您的函數內操作來自不同 SaaS 提供者 (例如 OneDrive, Dropbox) 的檔案。</span><span class="sxs-lookup"><span data-stu-id="6fb81-104">This article shows how to manipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="6fb81-105">Azure Functions 支援適用於外部檔案的觸發程序、輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="6fb81-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="6fb81-106">此繫結會建立與 SaaS 提供者的 API 連線，或使用函數應用程式之資源群組的現有 API 連線。</span><span class="sxs-lookup"><span data-stu-id="6fb81-106">This binding creates API connections to SaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="6fb81-107">支援的檔案連線</span><span class="sxs-lookup"><span data-stu-id="6fb81-107">Supported File connections</span></span>

|<span data-ttu-id="6fb81-108">連接器</span><span class="sxs-lookup"><span data-stu-id="6fb81-108">Connector</span></span>|<span data-ttu-id="6fb81-109">觸發程序</span><span class="sxs-lookup"><span data-stu-id="6fb81-109">Trigger</span></span>|<span data-ttu-id="6fb81-110">輸入</span><span class="sxs-lookup"><span data-stu-id="6fb81-110">Input</span></span>|<span data-ttu-id="6fb81-111">輸出</span><span class="sxs-lookup"><span data-stu-id="6fb81-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="6fb81-112">Box</span><span class="sxs-lookup"><span data-stu-id="6fb81-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="6fb81-113">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-113">x</span></span>|<span data-ttu-id="6fb81-114">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-114">x</span></span>|<span data-ttu-id="6fb81-115">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-115">x</span></span>
|[<span data-ttu-id="6fb81-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="6fb81-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="6fb81-117">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-117">x</span></span>|<span data-ttu-id="6fb81-118">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-118">x</span></span>|<span data-ttu-id="6fb81-119">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-119">x</span></span>
|[<span data-ttu-id="6fb81-120">FTP</span><span class="sxs-lookup"><span data-stu-id="6fb81-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="6fb81-121">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-121">x</span></span>|<span data-ttu-id="6fb81-122">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-122">x</span></span>|<span data-ttu-id="6fb81-123">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-123">x</span></span>
|[<span data-ttu-id="6fb81-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="6fb81-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="6fb81-125">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-125">x</span></span>|<span data-ttu-id="6fb81-126">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-126">x</span></span>|<span data-ttu-id="6fb81-127">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-127">x</span></span>
|[<span data-ttu-id="6fb81-128">商務用 OneDrive</span><span class="sxs-lookup"><span data-stu-id="6fb81-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="6fb81-129">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-129">x</span></span>|<span data-ttu-id="6fb81-130">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-130">x</span></span>|<span data-ttu-id="6fb81-131">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-131">x</span></span>
|[<span data-ttu-id="6fb81-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="6fb81-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="6fb81-133">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-133">x</span></span>|<span data-ttu-id="6fb81-134">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-134">x</span></span>|<span data-ttu-id="6fb81-135">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-135">x</span></span>
|[<span data-ttu-id="6fb81-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="6fb81-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="6fb81-137">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-137">x</span></span>|<span data-ttu-id="6fb81-138">x</span><span class="sxs-lookup"><span data-stu-id="6fb81-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="6fb81-139">外部檔案連線也可以用在 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) 中</span><span class="sxs-lookup"><span data-stu-id="6fb81-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="6fb81-140">外部檔案觸發程序繫結</span><span class="sxs-lookup"><span data-stu-id="6fb81-140">External File trigger binding</span></span>

<span data-ttu-id="6fb81-141">Azure 外部檔案觸發程序可讓您監視遠端資料夾，並且在偵測到變更時執行您的函數程式碼。</span><span class="sxs-lookup"><span data-stu-id="6fb81-141">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="6fb81-142">外部檔案觸發程序使用 function.json 之 `bindings` 陣列中的下列 JSON 物件</span><span class="sxs-lookup"><span data-stu-id="6fb81-142">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="6fb81-143">名稱模式</span><span class="sxs-lookup"><span data-stu-id="6fb81-143">Name patterns</span></span>
<span data-ttu-id="6fb81-144">您可以在 `path` 屬性中指定檔案名稱模式。</span><span class="sxs-lookup"><span data-stu-id="6fb81-144">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="6fb81-145">所參考的資料夾必須存在於 SaaS 提供者。</span><span class="sxs-lookup"><span data-stu-id="6fb81-145">The folder referenced must exist in the SaaS provider.</span></span>
<span data-ttu-id="6fb81-146">範例：</span><span class="sxs-lookup"><span data-stu-id="6fb81-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="6fb81-147">此路徑會尋找 *input* 資料夾中名稱為 *original-File1.txt* 的檔案，且函數程式碼中 `name` 變數的值會是 `File1.txt`。</span><span class="sxs-lookup"><span data-stu-id="6fb81-147">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="6fb81-148">另一個範例：</span><span class="sxs-lookup"><span data-stu-id="6fb81-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="6fb81-149">此路徑也會尋找名為 *original-File1.txt* 的檔案，且函數程式碼中的 `filename` 和 `fileextension` 變數值會是 *original-File1* 和 *txt*。</span><span class="sxs-lookup"><span data-stu-id="6fb81-149">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="6fb81-150">您可以使用固定的檔案副檔名值來限制檔案的檔案類型。</span><span class="sxs-lookup"><span data-stu-id="6fb81-150">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="6fb81-151">例如：</span><span class="sxs-lookup"><span data-stu-id="6fb81-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="6fb81-152">在此案例中，只有 *samples* 資料夾中的 *.png* 檔案會觸發函數。</span><span class="sxs-lookup"><span data-stu-id="6fb81-152">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="6fb81-153">大括號是名稱模式中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="6fb81-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="6fb81-154">如果要指定名稱中包含大括號的檔案名稱，請使用兩個大括號。</span><span class="sxs-lookup"><span data-stu-id="6fb81-154">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="6fb81-155">例如：</span><span class="sxs-lookup"><span data-stu-id="6fb81-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="6fb81-156">此路徑會在 *images* 資料夾中尋找名為 *{20140101}-soundfile.mp3* 的檔案，而函數程式碼中的 `name` 變數值會是 *soundfile.mp3*。</span><span class="sxs-lookup"><span data-stu-id="6fb81-156">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="6fb81-157">處理有害的檔案</span><span class="sxs-lookup"><span data-stu-id="6fb81-157">Handling poison files</span></span>
<span data-ttu-id="6fb81-158">當外部檔案觸發程序函數失敗時，Azure Functions 依預設會針對指定的檔案重試該函數最多 5 次 (包括第一次嘗試)。</span><span class="sxs-lookup"><span data-stu-id="6fb81-158">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="6fb81-159">如果 5 次嘗試全都失敗，函數會將訊息新增至名為 *webjobs-apihubtrigger-poison* 的儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="6fb81-159">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="6fb81-160">有害檔案的佇列訊息是包含下列屬性的 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="6fb81-160">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="6fb81-161">FunctionId (格式為 *&lt;function app name>*.Functions.*&lt;function name>*)</span><span class="sxs-lookup"><span data-stu-id="6fb81-161">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="6fb81-162">FileType</span><span class="sxs-lookup"><span data-stu-id="6fb81-162">FileType</span></span>
* <span data-ttu-id="6fb81-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="6fb81-163">FolderName</span></span>
* <span data-ttu-id="6fb81-164">FileName</span><span class="sxs-lookup"><span data-stu-id="6fb81-164">FileName</span></span>
* <span data-ttu-id="6fb81-165">ETag (檔案版本識別碼，例如："0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6fb81-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="6fb81-166">觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="6fb81-166">Trigger usage</span></span>
<span data-ttu-id="6fb81-167">在 C# 函數中，您使用函數簽章中的具名參數 (例如 `<T> <name>`) 繫結至輸入檔案資料。</span><span class="sxs-lookup"><span data-stu-id="6fb81-167">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="6fb81-168">其中 `T` 是您要用來還原序列化資料的資料類型，而 `paramName` 是您在 [觸發 JSON](#trigger) 中指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="6fb81-168">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="6fb81-169">在 Node.js 函數中，您使用 `context.bindings.<name>` 存取輸入檔案資料。</span><span class="sxs-lookup"><span data-stu-id="6fb81-169">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6fb81-170">檔案可以還原序列化為下列任何一種類型︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-170">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="6fb81-171">任何[物件 (機器翻譯)](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化的檔案資料。</span><span class="sxs-lookup"><span data-stu-id="6fb81-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="6fb81-172">如果您宣告自訂輸入類型 (例如 `FooType`)，Azure Functions 會嘗試將 JSON 資料還原序列化為您指定的類型。</span><span class="sxs-lookup"><span data-stu-id="6fb81-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="6fb81-173">字串 - 適用於文字檔案資料。</span><span class="sxs-lookup"><span data-stu-id="6fb81-173">String - useful for text file data.</span></span>

<span data-ttu-id="6fb81-174">在 C# 函數中，您也可以繫結至下列任何類型，且 Functions 執行階段會嘗試使用該類型將檔案資料還原序列化︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-174">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="6fb81-175">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="6fb81-175">Trigger sample</span></span>
<span data-ttu-id="6fb81-176">假設您有下列 function.json，且該檔案定義外部檔案觸發程序︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-176">Suppose you have the following function.json, that defines an external file trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

<span data-ttu-id="6fb81-177">請參閱會記錄每個新增到受監視資料夾之檔案內容的語言特定範例。</span><span class="sxs-lookup"><span data-stu-id="6fb81-177">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="6fb81-178">C#</span><span class="sxs-lookup"><span data-stu-id="6fb81-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="6fb81-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="6fb81-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="6fb81-180">C# 中的觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="6fb81-180">Trigger usage in C#</span></span> #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="6fb81-181">Node.js 中的觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="6fb81-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="6fb81-182">外部檔案輸入繫結</span><span class="sxs-lookup"><span data-stu-id="6fb81-182">External File input binding</span></span>
<span data-ttu-id="6fb81-183">Azure 外部檔案輸入繫結可讓您在函數中使用來自外部資料夾的檔案。</span><span class="sxs-lookup"><span data-stu-id="6fb81-183">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="6fb81-184">函數的外部檔案輸入會使用 function.json 之 `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-184">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="6fb81-185">請注意：</span><span class="sxs-lookup"><span data-stu-id="6fb81-185">Note the following:</span></span>

* <span data-ttu-id="6fb81-186">`path` 必須包含資料夾名稱和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6fb81-186">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="6fb81-187">例如，如果您的函數中有[佇列觸發程序](functions-bindings-storage-queue.md)，您可以使用 `"path": "samples-workitems/{queueTrigger}"` 以指向 `samples-workitems` 資料夾中具有與觸發程序訊息中指定之檔案名稱相符之名稱的檔案。</span><span class="sxs-lookup"><span data-stu-id="6fb81-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="6fb81-188">輸入使用方式</span><span class="sxs-lookup"><span data-stu-id="6fb81-188">Input usage</span></span>
<span data-ttu-id="6fb81-189">在 C# 函數中，您使用函數簽章中的具名參數 (例如 `<T> <name>`) 繫結至輸入檔案資料。</span><span class="sxs-lookup"><span data-stu-id="6fb81-189">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="6fb81-190">其中 `T` 是您要用來還原序列化資料的資料類型，而 `paramName` 是您在 [輸入繫結](#input) 中指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="6fb81-190">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="6fb81-191">在 Node.js 函數中，您使用 `context.bindings.<name>` 存取輸入檔案資料。</span><span class="sxs-lookup"><span data-stu-id="6fb81-191">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6fb81-192">檔案可以還原序列化為下列任何一種類型︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-192">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="6fb81-193">任何[物件 (機器翻譯)](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化的檔案資料。</span><span class="sxs-lookup"><span data-stu-id="6fb81-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="6fb81-194">如果您宣告自訂輸入類型 (例如 `InputType`)，Azure Functions 會嘗試將 JSON 資料還原序列化為您指定的類型。</span><span class="sxs-lookup"><span data-stu-id="6fb81-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="6fb81-195">字串 - 適用於文字檔案資料。</span><span class="sxs-lookup"><span data-stu-id="6fb81-195">String - useful for text file data.</span></span>

<span data-ttu-id="6fb81-196">在 C# 函數中，您也可以繫結至下列任何類型，且 Functions 執行階段會嘗試使用該類型將檔案資料還原序列化︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-196">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="6fb81-197">外部檔案輸出繫結</span><span class="sxs-lookup"><span data-stu-id="6fb81-197">External File output binding</span></span>
<span data-ttu-id="6fb81-198">Azure 外部檔案輸出繫結可讓您在函數中將檔案寫入到外部資料夾。</span><span class="sxs-lookup"><span data-stu-id="6fb81-198">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="6fb81-199">函數的外部檔案輸出會使用 function.json 之 `bindings` 陣列中的下列 JSON 物件︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-199">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="6fb81-200">請注意：</span><span class="sxs-lookup"><span data-stu-id="6fb81-200">Note the following:</span></span>

* <span data-ttu-id="6fb81-201">`path` 必須包含要寫入之資料夾名稱和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6fb81-201">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="6fb81-202">例如，如果您的函數中有[佇列觸發程序](functions-bindings-storage-queue.md)，您可以使用 `"path": "samples-workitems/{queueTrigger}"` 以指向 `samples-workitems` 資料夾中具有與觸發程序訊息中指定之檔案名稱相符之名稱的檔案。</span><span class="sxs-lookup"><span data-stu-id="6fb81-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="6fb81-203">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="6fb81-203">Output usage</span></span>
<span data-ttu-id="6fb81-204">在 C# 函數中，您使會用函數簽章中名為 `out` 的參數 (例如 `out <T> <name>`) 繫結至輸出檔案，其中 `T` 是您想要用來序列化資料的資料類型，而 `paramName` 是您在[輸出繫結](#output)中指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="6fb81-204">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="6fb81-205">在 Node.js 函數中，您會使用 `context.bindings.<name>` 存取輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="6fb81-205">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6fb81-206">您可以使用下列任何類型來寫入到輸出檔案︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-206">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="6fb81-207">任何[物件](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="6fb81-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="6fb81-208">如果您宣告自訂輸出類型 (例如 `out OutputType paramName`)，Azure Functions 會嘗試將物件序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="6fb81-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="6fb81-209">如果函數結束時輸出參數為 Null，則 Functions 執行階段會將檔案建立為 Null 物件。</span><span class="sxs-lookup"><span data-stu-id="6fb81-209">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="6fb81-210">字串 - (`out string paramName`) 適用於文字檔案資料。</span><span class="sxs-lookup"><span data-stu-id="6fb81-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="6fb81-211">當函數結束時，如果字串參數非 Null，Functions 執行階段才會建立檔案。</span><span class="sxs-lookup"><span data-stu-id="6fb81-211">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="6fb81-212">在 C# 函式中，您也可以輸出至下列任何類型︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-212">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="6fb81-213">輸入 + 輸出範例</span><span class="sxs-lookup"><span data-stu-id="6fb81-213">Input + Output sample</span></span>
<span data-ttu-id="6fb81-214">假設您有下列 function.json，且該檔案定義[儲存體佇列觸發程序](functions-bindings-storage-queue.md)、外部檔案輸入和外部檔案輸出︰</span><span class="sxs-lookup"><span data-stu-id="6fb81-214">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="6fb81-215">請參閱將輸入檔案複製到輸出檔案的語言特定範例。</span><span class="sxs-lookup"><span data-stu-id="6fb81-215">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="6fb81-216">C#</span><span class="sxs-lookup"><span data-stu-id="6fb81-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="6fb81-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="6fb81-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="6fb81-218">C# 中的使用方式</span><span class="sxs-lookup"><span data-stu-id="6fb81-218">Usage in C#</span></span> #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a><span data-ttu-id="6fb81-219">Node.js 中的使用方式</span><span class="sxs-lookup"><span data-stu-id="6fb81-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="6fb81-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6fb81-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
