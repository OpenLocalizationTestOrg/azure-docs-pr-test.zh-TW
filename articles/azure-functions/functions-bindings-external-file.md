---
title: "aaaAzure 函式的外部檔案繫結 （預覽） |Microsoft 文件"
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
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="1625b-103">Azure Functions 外部檔案繫結 (預覽)</span><span class="sxs-lookup"><span data-stu-id="1625b-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="1625b-104">本文將說明如何 toomanipulate 檔案從不同 SaaS 提供者 （例如 OneDrive、 Dropbox） 內您利用內建繫結的函式。</span><span class="sxs-lookup"><span data-stu-id="1625b-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="1625b-105">Azure Functions 支援適用於外部檔案的觸發程序、輸入和輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="1625b-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="1625b-106">這個繫結 tooSaaS 提供者，會建立應用程式開發介面的連接，或使用來自函式應用程式的資源群組的現有應用程式開發介面連線。</span><span class="sxs-lookup"><span data-stu-id="1625b-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="1625b-107">支援的檔案連線</span><span class="sxs-lookup"><span data-stu-id="1625b-107">Supported File connections</span></span>

|<span data-ttu-id="1625b-108">連接器</span><span class="sxs-lookup"><span data-stu-id="1625b-108">Connector</span></span>|<span data-ttu-id="1625b-109">觸發程序</span><span class="sxs-lookup"><span data-stu-id="1625b-109">Trigger</span></span>|<span data-ttu-id="1625b-110">輸入</span><span class="sxs-lookup"><span data-stu-id="1625b-110">Input</span></span>|<span data-ttu-id="1625b-111">輸出</span><span class="sxs-lookup"><span data-stu-id="1625b-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="1625b-112">Box</span><span class="sxs-lookup"><span data-stu-id="1625b-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="1625b-113">x</span><span class="sxs-lookup"><span data-stu-id="1625b-113">x</span></span>|<span data-ttu-id="1625b-114">x</span><span class="sxs-lookup"><span data-stu-id="1625b-114">x</span></span>|<span data-ttu-id="1625b-115">x</span><span class="sxs-lookup"><span data-stu-id="1625b-115">x</span></span>
|[<span data-ttu-id="1625b-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="1625b-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="1625b-117">x</span><span class="sxs-lookup"><span data-stu-id="1625b-117">x</span></span>|<span data-ttu-id="1625b-118">x</span><span class="sxs-lookup"><span data-stu-id="1625b-118">x</span></span>|<span data-ttu-id="1625b-119">x</span><span class="sxs-lookup"><span data-stu-id="1625b-119">x</span></span>
|[<span data-ttu-id="1625b-120">FTP</span><span class="sxs-lookup"><span data-stu-id="1625b-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="1625b-121">x</span><span class="sxs-lookup"><span data-stu-id="1625b-121">x</span></span>|<span data-ttu-id="1625b-122">x</span><span class="sxs-lookup"><span data-stu-id="1625b-122">x</span></span>|<span data-ttu-id="1625b-123">x</span><span class="sxs-lookup"><span data-stu-id="1625b-123">x</span></span>
|[<span data-ttu-id="1625b-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="1625b-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="1625b-125">x</span><span class="sxs-lookup"><span data-stu-id="1625b-125">x</span></span>|<span data-ttu-id="1625b-126">x</span><span class="sxs-lookup"><span data-stu-id="1625b-126">x</span></span>|<span data-ttu-id="1625b-127">x</span><span class="sxs-lookup"><span data-stu-id="1625b-127">x</span></span>
|[<span data-ttu-id="1625b-128">商務用 OneDrive</span><span class="sxs-lookup"><span data-stu-id="1625b-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="1625b-129">x</span><span class="sxs-lookup"><span data-stu-id="1625b-129">x</span></span>|<span data-ttu-id="1625b-130">x</span><span class="sxs-lookup"><span data-stu-id="1625b-130">x</span></span>|<span data-ttu-id="1625b-131">x</span><span class="sxs-lookup"><span data-stu-id="1625b-131">x</span></span>
|[<span data-ttu-id="1625b-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="1625b-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="1625b-133">x</span><span class="sxs-lookup"><span data-stu-id="1625b-133">x</span></span>|<span data-ttu-id="1625b-134">x</span><span class="sxs-lookup"><span data-stu-id="1625b-134">x</span></span>|<span data-ttu-id="1625b-135">x</span><span class="sxs-lookup"><span data-stu-id="1625b-135">x</span></span>
|[<span data-ttu-id="1625b-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="1625b-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="1625b-137">x</span><span class="sxs-lookup"><span data-stu-id="1625b-137">x</span></span>|<span data-ttu-id="1625b-138">x</span><span class="sxs-lookup"><span data-stu-id="1625b-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="1625b-139">外部檔案連線也可以用在 [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list) 中</span><span class="sxs-lookup"><span data-stu-id="1625b-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="1625b-140">外部檔案觸發程序繫結</span><span class="sxs-lookup"><span data-stu-id="1625b-140">External File trigger binding</span></span>

<span data-ttu-id="1625b-141">hello Azure 外部檔案觸發程序可讓您監視遠端資料夾，並執行您的函式程式碼，偵測到變更時。</span><span class="sxs-lookup"><span data-stu-id="1625b-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="1625b-142">hello 外部檔案觸發程序會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列</span><span class="sxs-lookup"><span data-stu-id="1625b-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="1625b-143">名稱模式</span><span class="sxs-lookup"><span data-stu-id="1625b-143">Name patterns</span></span>
<span data-ttu-id="1625b-144">您可以指定檔案名稱模式中 hello`path`屬性。</span><span class="sxs-lookup"><span data-stu-id="1625b-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="1625b-145">參考的 hello 資料夾必須存在於 hello SaaS 提供者。</span><span class="sxs-lookup"><span data-stu-id="1625b-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="1625b-146">範例：</span><span class="sxs-lookup"><span data-stu-id="1625b-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="1625b-147">此路徑會尋找名為*原始 File1.txt*在 hello*輸入*資料夾，然後 hello hello 值`name`函式程式碼中的變數會是`File1.txt`。</span><span class="sxs-lookup"><span data-stu-id="1625b-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="1625b-148">另一個範例：</span><span class="sxs-lookup"><span data-stu-id="1625b-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="1625b-149">此路徑也會尋找名為*原始 File1.txt*，和 hello hello 值`filename`和`fileextension`函式程式碼中的變數會是*原始 File1*和*txt*。</span><span class="sxs-lookup"><span data-stu-id="1625b-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="1625b-150">您可以限制 hello 檔案類型的檔案副檔名為 hello 使用固定的值。</span><span class="sxs-lookup"><span data-stu-id="1625b-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="1625b-151">例如：</span><span class="sxs-lookup"><span data-stu-id="1625b-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="1625b-152">在此情況下，只有*.png*檔案在 hello*範例*資料夾觸發程序 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="1625b-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="1625b-153">大括號是名稱模式中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="1625b-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="1625b-154">大括號名稱中含有 hello、 double hello 大括號 toospecify 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1625b-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="1625b-155">例如：</span><span class="sxs-lookup"><span data-stu-id="1625b-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="1625b-156">此路徑會尋找名為*{20140101}-soundfile.mp3*在 hello*映像*資料夾，然後 hello `name` hello 函式程式碼中的變數值會是*soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="1625b-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="1625b-157">處理有害的檔案</span><span class="sxs-lookup"><span data-stu-id="1625b-157">Handling poison files</span></span>
<span data-ttu-id="1625b-158">外部檔案的觸發程序函式失敗時，Azure 函式重試該函式 too5 時間 （包括 hello 第一次嘗試） 的預設值為指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="1625b-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="1625b-159">如果所有 5 次嘗試失敗，函式會將名為訊息 tooa 儲存體佇列*webjobs-apihubtrigger-有害*。</span><span class="sxs-lookup"><span data-stu-id="1625b-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="1625b-160">hello 佇列訊息的有害的檔案是包含下列屬性的 hello 的 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="1625b-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="1625b-161">FunctionId (hello 格式*&lt;函式應用程式名稱 >*。函式。*&lt;函式名稱 >*)</span><span class="sxs-lookup"><span data-stu-id="1625b-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="1625b-162">FileType</span><span class="sxs-lookup"><span data-stu-id="1625b-162">FileType</span></span>
* <span data-ttu-id="1625b-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="1625b-163">FolderName</span></span>
* <span data-ttu-id="1625b-164">FileName</span><span class="sxs-lookup"><span data-stu-id="1625b-164">FileName</span></span>
* <span data-ttu-id="1625b-165">ETag (檔案版本識別碼，例如："0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="1625b-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="1625b-166">觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="1625b-166">Trigger usage</span></span>
<span data-ttu-id="1625b-167">在 C# 函數中，您 toohello 輸入的檔案將資料繫結函式簽章中使用具名的參數，例如`<T> <name>`。</span><span class="sxs-lookup"><span data-stu-id="1625b-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="1625b-168">其中`T`是 hello 資料類型的 toodeserialize hello 資料分割，以及`paramName`是您在指定的 hello 名稱[觸發 JSON](#trigger)。</span><span class="sxs-lookup"><span data-stu-id="1625b-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="1625b-169">Node.js 函式，在您存取 hello 輸入的檔資料使用`context.bindings.<name>`。</span><span class="sxs-lookup"><span data-stu-id="1625b-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="1625b-170">hello 檔案可以還原序列化為任何下列類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="1625b-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="1625b-171">任何[物件 (機器翻譯)](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化的檔案資料。</span><span class="sxs-lookup"><span data-stu-id="1625b-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="1625b-172">如果您宣告自訂的輸入的類型 (例如`FooType`)，Azure 函式會嘗試 toodeserialize hello JSON 資料到您指定的型別。</span><span class="sxs-lookup"><span data-stu-id="1625b-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="1625b-173">字串 - 適用於文字檔案資料。</span><span class="sxs-lookup"><span data-stu-id="1625b-173">String - useful for text file data.</span></span>

<span data-ttu-id="1625b-174">在 C# 函式，您也可以繫結 tooany 的 hello 下列類型，並 hello 函式執行階段會嘗試使用該類型的 hello 檔案資料還原序列化：</span><span class="sxs-lookup"><span data-stu-id="1625b-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="1625b-175">觸發程序範例</span><span class="sxs-lookup"><span data-stu-id="1625b-175">Trigger sample</span></span>
<span data-ttu-id="1625b-176">假設您有下列 function.json hello，定義檔案外部觸發程序：</span><span class="sxs-lookup"><span data-stu-id="1625b-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="1625b-177">請參閱記錄 hello toohello 監控的資料夾加入每個檔案內容的 hello 特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="1625b-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="1625b-178">C#</span><span class="sxs-lookup"><span data-stu-id="1625b-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="1625b-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="1625b-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="1625b-180">C# 中的觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="1625b-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="1625b-181">Node.js 中的觸發程序使用方式</span><span class="sxs-lookup"><span data-stu-id="1625b-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="1625b-182">外部檔案輸入繫結</span><span class="sxs-lookup"><span data-stu-id="1625b-182">External File input binding</span></span>
<span data-ttu-id="1625b-183">hello Azure 外部的檔案輸入繫結可讓您 toouse 函式中的外部資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="1625b-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="1625b-184">hello 外部檔案輸入的 tooa 函式會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="1625b-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="1625b-185">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1625b-185">Note hello following:</span></span>

* <span data-ttu-id="1625b-186">`path`必須包含 hello 資料夾名稱和 hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1625b-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="1625b-187">例如，如果您有[佇列觸發程序](functions-bindings-storage-queue.md)在您的函式，您可以使用`"path": "samples-workitems/{queueTrigger}"`toopoint tooa 檔案在 hello`samples-workitems`資料夾名稱符合 hello hello 觸發程序的訊息中指定的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1625b-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="1625b-188">輸入使用方式</span><span class="sxs-lookup"><span data-stu-id="1625b-188">Input usage</span></span>
<span data-ttu-id="1625b-189">在 C# 函數中，您 toohello 輸入的檔案將資料繫結函式簽章中使用具名的參數，例如`<T> <name>`。</span><span class="sxs-lookup"><span data-stu-id="1625b-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="1625b-190">其中`T`是 hello 資料類型的 toodeserialize hello 資料分割，以及`paramName`是您在指定的 hello 名稱[輸入繫結](#input)。</span><span class="sxs-lookup"><span data-stu-id="1625b-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="1625b-191">Node.js 函式，在您存取 hello 輸入的檔資料使用`context.bindings.<name>`。</span><span class="sxs-lookup"><span data-stu-id="1625b-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="1625b-192">hello 檔案可以還原序列化為任何下列類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="1625b-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="1625b-193">任何[物件 (機器翻譯)](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化的檔案資料。</span><span class="sxs-lookup"><span data-stu-id="1625b-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="1625b-194">如果您宣告自訂的輸入的類型 (例如`InputType`)，Azure 函式會嘗試 toodeserialize hello JSON 資料到您指定的型別。</span><span class="sxs-lookup"><span data-stu-id="1625b-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="1625b-195">字串 - 適用於文字檔案資料。</span><span class="sxs-lookup"><span data-stu-id="1625b-195">String - useful for text file data.</span></span>

<span data-ttu-id="1625b-196">在 C# 函式，您也可以繫結 tooany 的 hello 下列類型，並 hello 函式執行階段會嘗試使用該類型的 hello 檔案資料還原序列化：</span><span class="sxs-lookup"><span data-stu-id="1625b-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="1625b-197">外部檔案輸出繫結</span><span class="sxs-lookup"><span data-stu-id="1625b-197">External File output binding</span></span>
<span data-ttu-id="1625b-198">hello Azure 外部的檔案輸出繫結可讓您在您的函式的 toowrite files tooan 外部資料夾。</span><span class="sxs-lookup"><span data-stu-id="1625b-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="1625b-199">輸出的函式使用下列 JSON 物件中 hello hello hello 外部檔案`bindings`function.json 的陣列：</span><span class="sxs-lookup"><span data-stu-id="1625b-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="1625b-200">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1625b-200">Note hello following:</span></span>

* <span data-ttu-id="1625b-201">`path`必須包含 hello 資料夾名稱和到 hello 檔案名稱 toowrite。</span><span class="sxs-lookup"><span data-stu-id="1625b-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="1625b-202">例如，如果您有[佇列觸發程序](functions-bindings-storage-queue.md)在您的函式，您可以使用`"path": "samples-workitems/{queueTrigger}"`toopoint tooa 檔案在 hello`samples-workitems`資料夾名稱符合 hello hello 觸發程序的訊息中指定的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1625b-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="1625b-203">輸出使用方式</span><span class="sxs-lookup"><span data-stu-id="1625b-203">Output usage</span></span>
<span data-ttu-id="1625b-204">在 C# 函數中，您使用繫結 toohello 輸出檔名為 hello`out`函式簽章中的參數喜歡`out <T> <name>`，其中`T`是 hello 資料類型的 tooserialize hello 資料分割，和`paramName`是 hello 名稱指定在[輸出繫結](#output)。</span><span class="sxs-lookup"><span data-stu-id="1625b-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="1625b-205">Node.js 函式，在您存取 hello 輸出檔案使用`context.bindings.<name>`。</span><span class="sxs-lookup"><span data-stu-id="1625b-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="1625b-206">您可以撰寫使用任何下列類型的 hello toohello 輸出檔：</span><span class="sxs-lookup"><span data-stu-id="1625b-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="1625b-207">任何[物件](https://msdn.microsoft.com/library/system.object.aspx) - 適用於 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="1625b-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="1625b-208">如果您宣告自訂輸出型別 (例如`out OutputType paramName`)，Azure 函式會嘗試 tooserialize 物件為 JSON。</span><span class="sxs-lookup"><span data-stu-id="1625b-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="1625b-209">如果 hello 函式結束時，hello 輸出參數為 null，hello 函式執行階段會建立檔案為 null 的物件。</span><span class="sxs-lookup"><span data-stu-id="1625b-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="1625b-210">字串 - (`out string paramName`) 適用於文字檔案資料。</span><span class="sxs-lookup"><span data-stu-id="1625b-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="1625b-211">hello 函式執行階段建立檔案，只有當 hello 函式結束時，字串參數為非 null。</span><span class="sxs-lookup"><span data-stu-id="1625b-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="1625b-212">您也可以輸出 tooany hello 下列類型的 C# 函式中：</span><span class="sxs-lookup"><span data-stu-id="1625b-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="1625b-213">輸入 + 輸出範例</span><span class="sxs-lookup"><span data-stu-id="1625b-213">Input + Output sample</span></span>
<span data-ttu-id="1625b-214">假設您有下列 function.json hello，定義[儲存體佇列觸發程序](functions-bindings-storage-queue.md)、 外部檔案輸入和輸出的外部檔案：</span><span class="sxs-lookup"><span data-stu-id="1625b-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="1625b-215">請參閱 hello 複製 hello 輸入的檔 toohello 輸出檔案的特定語言的範例。</span><span class="sxs-lookup"><span data-stu-id="1625b-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="1625b-216">C#</span><span class="sxs-lookup"><span data-stu-id="1625b-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="1625b-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="1625b-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="1625b-218">C# 中的使用方式</span><span class="sxs-lookup"><span data-stu-id="1625b-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="1625b-219">Node.js 中的使用方式</span><span class="sxs-lookup"><span data-stu-id="1625b-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="1625b-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1625b-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
