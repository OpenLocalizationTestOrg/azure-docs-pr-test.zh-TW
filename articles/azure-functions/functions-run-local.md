---
title: "開發 Azure 函數並在本機執行 | Microsoft Docs"
description: "在於 Azure Functions 上執行 Azure 函式之前，先了解如何撰寫 Azure 函式並在本機電腦上進行測試。"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: bbe03973dbd7c70463caa6d1a45efae2ec722c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="358b8-103">撰寫 Azure 函式並在本機進行測試</span><span class="sxs-lookup"><span data-stu-id="358b8-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="358b8-104">雖然「Azure 入口網站」[]有提供開發及測試 Azure Functions 的完整工具集，有許多開發人員仍偏好本機開發體驗。</span><span class="sxs-lookup"><span data-stu-id="358b8-104">While the [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="358b8-105">Azure Functions 可讓您輕鬆使用最喜愛的程式碼編輯器及本機開發工具，在本機電腦上開發並測試您的函式。</span><span class="sxs-lookup"><span data-stu-id="358b8-105">Azure Functions makes it easy to use your favorite code editor and local development tools to develop and test your functions on your local computer.</span></span> <span data-ttu-id="358b8-106">您的函式可以透過 Azure 中的事件觸發，您也可以在本機電腦上對 C# 和 JavaScript 函式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="358b8-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="358b8-107">如果您是 Visual Studio C# 開發人員，Azure Functions 也能[與 Visual Studio 2017 整合](functions-develop-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="358b8-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-the-azure-functions-core-tools"></a><span data-ttu-id="358b8-108">安裝 Azure Functions Core Tools</span><span class="sxs-lookup"><span data-stu-id="358b8-108">Install the Azure Functions Core Tools</span></span>

<span data-ttu-id="358b8-109">Azure Functions Core Tools 是 Azure Functions 執行階段的本機版本，可讓您在本機 Windows 電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="358b8-109">Azure Functions Core Tools is a local version of the Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="358b8-110">它不是模擬器。</span><span class="sxs-lookup"><span data-stu-id="358b8-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="358b8-111">它與在 Azure 中提供 Functions 的執行階段是相同的執行階段。</span><span class="sxs-lookup"><span data-stu-id="358b8-111">It's the same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="358b8-112">[Azure Functions Core Tools] 是以 npm 套件的形式提供。</span><span class="sxs-lookup"><span data-stu-id="358b8-112">The [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="358b8-113">您必須先[安裝 NodeJS](https://docs.npmjs.com/getting-started/installing-node) \(英文\)，它將會包含 npm。</span><span class="sxs-lookup"><span data-stu-id="358b8-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="358b8-114">目前 Azure Functions Core Tools 套件只能安裝在 Windows 電腦上。</span><span class="sxs-lookup"><span data-stu-id="358b8-114">At this time, the Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="358b8-115">此限制是因為 Functions 主機的暫時性限制所造成。</span><span class="sxs-lookup"><span data-stu-id="358b8-115">This restriction is due to a temporary limitation in the Functions host.</span></span>

<span data-ttu-id="358b8-116">[Azure Functions Core Tools]新增了下列命令別名：</span><span class="sxs-lookup"><span data-stu-id="358b8-116">[Azure Functions Core Tools] adds the following command aliases:</span></span>
* <span data-ttu-id="358b8-117">**func**</span><span class="sxs-lookup"><span data-stu-id="358b8-117">**func**</span></span>
* <span data-ttu-id="358b8-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="358b8-118">**azfun**</span></span>
* <span data-ttu-id="358b8-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="358b8-119">**azurefunctions**</span></span>

<span data-ttu-id="358b8-120">這些別名都可以用來取代本主題範例中所顯示的 `func`。</span><span class="sxs-lookup"><span data-stu-id="358b8-120">All of these alias can be used instead of `func` shown in the examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="358b8-121">建立本機的 Functions 專案</span><span class="sxs-lookup"><span data-stu-id="358b8-121">Create a local Functions project</span></span>

<span data-ttu-id="358b8-122">在本機執行時，Functions 專案是具有 host.json 和 local.settings.json 檔案的目錄。</span><span class="sxs-lookup"><span data-stu-id="358b8-122">When running locally, a Functions project is a directory that has the files host.json and local.settings.json.</span></span> <span data-ttu-id="358b8-123">此目錄相當於 Azure 中的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="358b8-123">This directory is the equivalent of a function app in Azure.</span></span> <span data-ttu-id="358b8-124">若要深入了解 Azure Functions 的資料夾結構，請參閱 [Azure Functions 的開發人員指南](functions-reference.md#folder-structure)。</span><span class="sxs-lookup"><span data-stu-id="358b8-124">To learn more about the Azure Functions folder structure, see the [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="358b8-125">在命令提示字元中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="358b8-125">At a command prompt, run the following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="358b8-126">輸出看起來會像下列範例：</span><span class="sxs-lookup"><span data-stu-id="358b8-126">The output looks like the following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="358b8-127">若要選擇不建立 Git 存放庫，請使用 `--no-source-control [-n]` 選項。</span><span class="sxs-lookup"><span data-stu-id="358b8-127">To opt out of creating a Git repository, use the option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="358b8-128">本機設定檔</span><span class="sxs-lookup"><span data-stu-id="358b8-128">Local settings file</span></span>

<span data-ttu-id="358b8-129">local.settings.json 檔案會儲存應用程式設定、連接字串和 Azure Functions Core Tools 的設定。</span><span class="sxs-lookup"><span data-stu-id="358b8-129">The file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="358b8-130">其結構如下：</span><span class="sxs-lookup"><span data-stu-id="358b8-130">It has the following structure:</span></span>

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| <span data-ttu-id="358b8-131">設定</span><span class="sxs-lookup"><span data-stu-id="358b8-131">Setting</span></span>      | <span data-ttu-id="358b8-132">說明</span><span class="sxs-lookup"><span data-stu-id="358b8-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="358b8-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="358b8-133">**IsEncrypted**</span></span> | <span data-ttu-id="358b8-134">設定為 **true** 時，所有的值都會使用本機電腦金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="358b8-134">When set to **true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="358b8-135">需搭配 `func settings` 命令使用。</span><span class="sxs-lookup"><span data-stu-id="358b8-135">Used with `func settings` commands.</span></span> <span data-ttu-id="358b8-136">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="358b8-136">Default value is **false**.</span></span> |
| <span data-ttu-id="358b8-137">**值**</span><span class="sxs-lookup"><span data-stu-id="358b8-137">**Values**</span></span> | <span data-ttu-id="358b8-138">於本機執行時使用的應用程式設定集合。</span><span class="sxs-lookup"><span data-stu-id="358b8-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="358b8-139">請將您的應用程式設定新增至此物件。</span><span class="sxs-lookup"><span data-stu-id="358b8-139">Add your application settings to this object.</span></span>  |
| <span data-ttu-id="358b8-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="358b8-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="358b8-141">設定針對由 Azure Functions 執行階段於內部使用之 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="358b8-141">Sets the connection string to the Azure Storage account that is used internally by the Azure Functions runtime.</span></span> <span data-ttu-id="358b8-142">該儲存體帳戶支援您函式的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="358b8-142">The storage account supports your function's triggers.</span></span> <span data-ttu-id="358b8-143">所有函式都必須設定此儲存體帳戶連接字串 (由 HTTP 觸發的函式除外)。</span><span class="sxs-lookup"><span data-stu-id="358b8-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="358b8-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="358b8-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="358b8-145">設定針對用來儲存函式記錄之 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="358b8-145">Sets the connection string to the Azure Storage account that is used to store the function logs.</span></span> <span data-ttu-id="358b8-146">此選擇性值能使記錄可在入口網站中存取。</span><span class="sxs-lookup"><span data-stu-id="358b8-146">This optional value makes the logs accessible in the portal.</span></span>|
| <span data-ttu-id="358b8-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="358b8-147">**Host**</span></span> | <span data-ttu-id="358b8-148">此區段中的設定能自訂於本機執行的 Functions 主機處理序。</span><span class="sxs-lookup"><span data-stu-id="358b8-148">Settings in this section customize the Functions host process when running locally.</span></span> | 
| <span data-ttu-id="358b8-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="358b8-149">**LocalHttpPort**</span></span> | <span data-ttu-id="358b8-150">設定於執行本機 Functions 主機 (`func host start` 和 `func run`) 時所使用的預設連接埠。</span><span class="sxs-lookup"><span data-stu-id="358b8-150">Sets the default port used when running the local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="358b8-151">`--port` 命令列選項的優先順序高於此值。</span><span class="sxs-lookup"><span data-stu-id="358b8-151">The `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="358b8-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="358b8-152">**CORS**</span></span> | <span data-ttu-id="358b8-153">定義針對[跨來源資源共享 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) 所允許的來源。</span><span class="sxs-lookup"><span data-stu-id="358b8-153">Defines the origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="358b8-154">來源是以不含空格的逗號分隔清單提供。</span><span class="sxs-lookup"><span data-stu-id="358b8-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="358b8-155">支援萬用字元值 (**\***)，它能允許來自任何來源的要求。</span><span class="sxs-lookup"><span data-stu-id="358b8-155">The wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="358b8-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="358b8-156">**ConnectionStrings**</span></span> | <span data-ttu-id="358b8-157">包含函式的資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="358b8-157">Contains the database connection strings for your functions.</span></span> <span data-ttu-id="358b8-158">此物件中的連接字串會新增至具有 **System.Data.SqlClient** 提供者類型的環境。</span><span class="sxs-lookup"><span data-stu-id="358b8-158">Connection strings in this object are added to the environment with the provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="358b8-159">大部分的觸發程序和繫結都有 **Connection** 屬性，會對應至環境變數或應用程式設定的名稱。</span><span class="sxs-lookup"><span data-stu-id="358b8-159">Most triggers and bindings have a **Connection** property that maps to the name of an environment variable or app setting.</span></span> <span data-ttu-id="358b8-160">針對每個連線屬性，都必須在 local.settings.json 檔案中定義應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="358b8-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="358b8-161">這些設定也可以在您的程式碼中讀取為環境變數。</span><span class="sxs-lookup"><span data-stu-id="358b8-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="358b8-162">在 C# 中，請使用 [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) \(機器翻譯\) 或 [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx) \(機器翻譯\)。</span><span class="sxs-lookup"><span data-stu-id="358b8-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="358b8-163">在 JavaScript 中，使用 `process.env`。</span><span class="sxs-lookup"><span data-stu-id="358b8-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="358b8-164">指定為系統環境變數之設定的優先順序，將會高於 local.settings.json 檔案中的值。</span><span class="sxs-lookup"><span data-stu-id="358b8-164">Settings specified as a system environment variable take precedence over values in the local.settings.json file.</span></span> 

<span data-ttu-id="358b8-165">local.settings.json 檔案中的值，只會由於本機執行的 Functions 工具使用。</span><span class="sxs-lookup"><span data-stu-id="358b8-165">Settings in the local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="358b8-166">根據預設，在專案發佈至 Azure 時，這些設定將不會自動移轉。</span><span class="sxs-lookup"><span data-stu-id="358b8-166">By default, these settings are not migrated automatically when the project is published to Azure.</span></span> <span data-ttu-id="358b8-167">請在[發佈時](#publish)使用 `--publish-local-settings` 參數，以確保這些設定會新增至 Azure 中的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="358b8-167">Use the `--publish-local-settings` switch [when you publish](#publish) to make sure these settings are added to the function app in Azure.</span></span>

<span data-ttu-id="358b8-168">沒有針對 **AzureWebJobsStorage** 設定有效的儲存體連接字串時，系統會顯示下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="358b8-168">When no valid storage connection string is set for **AzureWebJobsStorage**, the following error message is shown:</span></span>  

><span data-ttu-id="358b8-169">在 local.settings.json 中遺失 AzureWebJobsStorage 的值。</span><span class="sxs-lookup"><span data-stu-id="358b8-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="358b8-170">這對 HTTP 以外的所有觸發程序是必要的。</span><span class="sxs-lookup"><span data-stu-id="358b8-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="358b8-171">您可以執行 'func azure functionary fetch-app-settings <functionAppName>' 或在 local.settings.json 中指定連接字串。</span><span class="sxs-lookup"><span data-stu-id="358b8-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="358b8-172">進行應用程式設定</span><span class="sxs-lookup"><span data-stu-id="358b8-172">Configure app settings</span></span>

<span data-ttu-id="358b8-173">若要設定連接字串的值，您可以執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="358b8-173">To set a value for connection strings, you can do one of the following:</span></span>
* <span data-ttu-id="358b8-174">從 [Azure 儲存體總管](http://storageexplorer.com/) \(英文\) 輸入連接字串。</span><span class="sxs-lookup"><span data-stu-id="358b8-174">Enter the connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="358b8-175">使用下列其中一個命令：</span><span class="sxs-lookup"><span data-stu-id="358b8-175">Use one of the following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="358b8-176">這兩個命令都需要先登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="358b8-176">Both commands require you to first sign-in to Azure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="358b8-177">建立函式</span><span class="sxs-lookup"><span data-stu-id="358b8-177">Create a function</span></span>

<span data-ttu-id="358b8-178">若要建立函式，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="358b8-178">To create a function, run the following command:</span></span>

```
func new
``` 
<span data-ttu-id="358b8-179">`func new` 支援下列選擇性引數︰</span><span class="sxs-lookup"><span data-stu-id="358b8-179">`func new` supports the following optional arguments:</span></span>

| <span data-ttu-id="358b8-180">引數</span><span class="sxs-lookup"><span data-stu-id="358b8-180">Argument</span></span>     | <span data-ttu-id="358b8-181">說明</span><span class="sxs-lookup"><span data-stu-id="358b8-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="358b8-182">範本程式語言，例如 C#、F# 或 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="358b8-182">The template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="358b8-183">範本名稱。</span><span class="sxs-lookup"><span data-stu-id="358b8-183">The template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="358b8-184">函式名稱。</span><span class="sxs-lookup"><span data-stu-id="358b8-184">The function name.</span></span> |

<span data-ttu-id="358b8-185">例如，若要建立 JavaScript HTTP 觸發程序，請執行：</span><span class="sxs-lookup"><span data-stu-id="358b8-185">For example, to create a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="358b8-186">若要建立佇列所觸發的函式，請執行：</span><span class="sxs-lookup"><span data-stu-id="358b8-186">To create a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="358b8-187">在本機執行函式</span><span class="sxs-lookup"><span data-stu-id="358b8-187">Run functions locally</span></span>

<span data-ttu-id="358b8-188">若要執行 Functions 專案，請執行 Functions 主機。</span><span class="sxs-lookup"><span data-stu-id="358b8-188">To run a Functions project, run the Functions host.</span></span> <span data-ttu-id="358b8-189">主機可允許專案中所有函式的觸發程序：</span><span class="sxs-lookup"><span data-stu-id="358b8-189">The host enables triggers for all functions in the project:</span></span>

```
func host start
```

<span data-ttu-id="358b8-190">`func host start` 支援下列選項：</span><span class="sxs-lookup"><span data-stu-id="358b8-190">`func host start` supports the following options:</span></span>

| <span data-ttu-id="358b8-191">選項</span><span class="sxs-lookup"><span data-stu-id="358b8-191">Option</span></span>     | <span data-ttu-id="358b8-192">說明</span><span class="sxs-lookup"><span data-stu-id="358b8-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="358b8-193">要接聽的本機連接埠。</span><span class="sxs-lookup"><span data-stu-id="358b8-193">The local port to listen on.</span></span> <span data-ttu-id="358b8-194">預設值：7071。</span><span class="sxs-lookup"><span data-stu-id="358b8-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="358b8-195">選項為 `VSCode` 和 `VS`：</span><span class="sxs-lookup"><span data-stu-id="358b8-195">The options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="358b8-196">以逗號分隔的 CORS 來源清單，不含空格。</span><span class="sxs-lookup"><span data-stu-id="358b8-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="358b8-197">要使用的節點偵錯工具連接埠。</span><span class="sxs-lookup"><span data-stu-id="358b8-197">The port for the node debugger to use.</span></span> <span data-ttu-id="358b8-198">預設值：Launch.json 中的值或 5858。</span><span class="sxs-lookup"><span data-stu-id="358b8-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="358b8-199">主控台追蹤層級 (off、verbose、info、warning 或 error)。</span><span class="sxs-lookup"><span data-stu-id="358b8-199">The console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="358b8-200">預設：info。</span><span class="sxs-lookup"><span data-stu-id="358b8-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="358b8-201">Functions 主機要啟動的逾時 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="358b8-201">The time out for the Functions host t     o start, in seconds.</span></span> <span data-ttu-id="358b8-202">預設值：20 秒。</span><span class="sxs-lookup"><span data-stu-id="358b8-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="358b8-203">繫結至 https://localhost:{port} 而不是 http://localhost:{port}。</span><span class="sxs-lookup"><span data-stu-id="358b8-203">Bind to https://localhost:{port} rather than to http://localhost:{port}.</span></span> <span data-ttu-id="358b8-204">根據預設，此選項會在您的電腦上建立受信任的憑證。</span><span class="sxs-lookup"><span data-stu-id="358b8-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="358b8-205">暫停以在結束處理程序之前取得其他輸入。</span><span class="sxs-lookup"><span data-stu-id="358b8-205">Pause for additional input before exiting the process.</span></span> <span data-ttu-id="358b8-206">當您從整合式開發環境 (IDE) 啟動 Azure Functions Core Tools 時很有用。</span><span class="sxs-lookup"><span data-stu-id="358b8-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="358b8-207">Functions 主機啟動時，它會輸出 HTTP 觸發函式的 URL：</span><span class="sxs-lookup"><span data-stu-id="358b8-207">When the Functions host starts, it outputs the URL of HTTP-triggered functions:</span></span>

```
Found the following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="358b8-208">在 VS Code 或 Visual Studio 中進行偵錯</span><span class="sxs-lookup"><span data-stu-id="358b8-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="358b8-209">若要連結偵錯工具，請傳遞 `--debug` 引數。</span><span class="sxs-lookup"><span data-stu-id="358b8-209">To attach a debugger, pass the `--debug` argument.</span></span> <span data-ttu-id="358b8-210">若要偵錯 JavaScript 函式，請使用 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="358b8-210">To debug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="358b8-211">對於 C# 函式，請使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="358b8-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="358b8-212">若要偵錯 C# 函式，請使用 `--debug vs`。</span><span class="sxs-lookup"><span data-stu-id="358b8-212">To debug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="358b8-213">您也可以使用 [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="358b8-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="358b8-214">若要啟動主機並設定 JavaScript 偵錯，請執行：</span><span class="sxs-lookup"><span data-stu-id="358b8-214">To launch the host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="358b8-215">然後，在 Visual Studio Code 的 [偵錯] 檢視中，選取 [連結至 Azure Functions]。</span><span class="sxs-lookup"><span data-stu-id="358b8-215">Then, in Visual Studio Code, in the **Debug** view, select **Attach to Azure Functions**.</span></span> <span data-ttu-id="358b8-216">您可以附加中斷點、檢查變數及逐步執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="358b8-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![使用 Visual Studio Code 進行 JavaScript 偵錯](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a><span data-ttu-id="358b8-218">將測試資料傳遞至函式</span><span class="sxs-lookup"><span data-stu-id="358b8-218">Passing test data to a function</span></span>

<span data-ttu-id="358b8-219">您也可以使用 `func run <FunctionName>` 直接叫用函式，並為函式提供輸入資料。</span><span class="sxs-lookup"><span data-stu-id="358b8-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for the function.</span></span> <span data-ttu-id="358b8-220">此命令類似於使用 Azure 入口網站中的 [測試] 索引標籤執行函式。</span><span class="sxs-lookup"><span data-stu-id="358b8-220">This command is similar to running a function using the **Test** tab in the Azure portal.</span></span> <span data-ttu-id="358b8-221">這個命令會啟動整個 Functions 主機。</span><span class="sxs-lookup"><span data-stu-id="358b8-221">This command launches the entire Functions host.</span></span>

<span data-ttu-id="358b8-222">`func run` 支援下列選項：</span><span class="sxs-lookup"><span data-stu-id="358b8-222">`func run` supports the following options:</span></span>

| <span data-ttu-id="358b8-223">選項</span><span class="sxs-lookup"><span data-stu-id="358b8-223">Option</span></span>     | <span data-ttu-id="358b8-224">說明</span><span class="sxs-lookup"><span data-stu-id="358b8-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="358b8-225">內嵌內容。</span><span class="sxs-lookup"><span data-stu-id="358b8-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="358b8-226">在執行函式之前，請先將偵錯工具附加到主機處理序。</span><span class="sxs-lookup"><span data-stu-id="358b8-226">Attach a debugger to the host process before running the function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="358b8-227">本機 Functions 主機就緒前的等候時間 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="358b8-227">Time to wait (in seconds) until the local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="358b8-228">要用來作為內容的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="358b8-228">The file name to use as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="358b8-229">不會提示輸入。</span><span class="sxs-lookup"><span data-stu-id="358b8-229">Does not prompt for input.</span></span> <span data-ttu-id="358b8-230">適用於自動化情節。</span><span class="sxs-lookup"><span data-stu-id="358b8-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="358b8-231">例如，若要呼叫 HTTP 觸發的函式並傳遞內容的內文，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="358b8-231">For example, to call an HTTP-triggered function and pass content body, run the following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="358b8-232"><a name="publish"></a>發佈至 Azure</span><span class="sxs-lookup"><span data-stu-id="358b8-232"><a name="publish"></a>Publish to Azure</span></span>

<span data-ttu-id="358b8-233">若要將 Functions 專案發佈至 Azure 中的函式應用程式，請使用 `publish` 命令：</span><span class="sxs-lookup"><span data-stu-id="358b8-233">To publish a Functions project to a function app in Azure, use the `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="358b8-234">您可以使用下列選項：</span><span class="sxs-lookup"><span data-stu-id="358b8-234">You can use the following options:</span></span>

| <span data-ttu-id="358b8-235">選項</span><span class="sxs-lookup"><span data-stu-id="358b8-235">Option</span></span>     | <span data-ttu-id="358b8-236">說明</span><span class="sxs-lookup"><span data-stu-id="358b8-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="358b8-237">將 local.settings.json 中的設定發佈至 Azure，若設定已經存在，則提示進行覆寫。</span><span class="sxs-lookup"><span data-stu-id="358b8-237">Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="358b8-238">必須與 `-i` 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="358b8-238">Must be used with `-i`.</span></span> <span data-ttu-id="358b8-239">使用本機值在 Azure 中覆寫 AppSettings (如果不同)。</span><span class="sxs-lookup"><span data-stu-id="358b8-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="358b8-240">預設值為提示。</span><span class="sxs-lookup"><span data-stu-id="358b8-240">Default is prompt.</span></span>|

<span data-ttu-id="358b8-241">`publish` 命令會將 Functions 專案目錄的內容上傳。</span><span class="sxs-lookup"><span data-stu-id="358b8-241">The `publish` command uploads the contents of the Functions project directory.</span></span> <span data-ttu-id="358b8-242">如果您在本機將檔案刪除，`publish` 命令並不會從 Azure 刪除它們。</span><span class="sxs-lookup"><span data-stu-id="358b8-242">If you delete files locally, the `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="358b8-243">您可以使用「Azure 入口網站」[]中的 [Kudu 工具](functions-how-to-use-azure-function-app-settings.md#kudu)來刪除 Azure 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="358b8-243">You can delete files in Azure by using the [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in the [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="358b8-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="358b8-244">Next steps</span></span>

<span data-ttu-id="358b8-245">Azure Functions Core Tools 是[開放原始碼且裝載於 GitHub 上](https://github.com/azure/azure-functions-cli)。</span><span class="sxs-lookup"><span data-stu-id="358b8-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="358b8-246">若要提出錯誤或功能要求，[請開啟 GitHub 問題](https://github.com/azure/azure-functions-cli/issues)。</span><span class="sxs-lookup"><span data-stu-id="358b8-246">To file a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Azure Functions Core Tools]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure 入口網站]: https://portal.azure.com 
