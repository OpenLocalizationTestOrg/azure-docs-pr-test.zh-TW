---
title: "aaaDevelop 和執行的 Azure 函式在本機 |Microsoft 文件"
description: "了解如何 toocode 和測試 Azure 函式在本機電腦上執行 Azure 函式之前。"
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
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="4ae42-103">撰寫 Azure 函式並在本機進行測試</span><span class="sxs-lookup"><span data-stu-id="4ae42-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="4ae42-104">Hello 時[Azure 入口網站]提供完整設定的工具來開發和測試 Azure 功能，許多開發人員偏好的本機開發體驗。</span><span class="sxs-lookup"><span data-stu-id="4ae42-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="4ae42-105">Azure 的函式可讓您輕鬆 toouse 您最愛的程式碼編輯器和本機開發工具 toodevelop 和測試您在本機電腦上的函式。</span><span class="sxs-lookup"><span data-stu-id="4ae42-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="4ae42-106">您的函式可以透過 Azure 中的事件觸發，您也可以在本機電腦上對 C# 和 JavaScript 函式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="4ae42-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="4ae42-107">如果您是 Visual Studio C# 開發人員，Azure Functions 也能[與 Visual Studio 2017 整合](functions-develop-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="4ae42-108">安裝 hello Azure 函式的核心工具</span><span class="sxs-lookup"><span data-stu-id="4ae42-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="4ae42-109">Azure 功能的核心工具是 hello Azure 函式執行階段，您可以在本機的 Windows 電腦上執行本機版。</span><span class="sxs-lookup"><span data-stu-id="4ae42-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="4ae42-110">它不是模擬器。</span><span class="sxs-lookup"><span data-stu-id="4ae42-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="4ae42-111">它具有 hello 相同的執行階段函式，在 Azure 中的次方。</span><span class="sxs-lookup"><span data-stu-id="4ae42-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="4ae42-112">hello [Azure 函式的核心工具]提供為 npm 封裝。</span><span class="sxs-lookup"><span data-stu-id="4ae42-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="4ae42-113">您必須先[安裝 NodeJS](https://docs.npmjs.com/getting-started/installing-node) \(英文\)，它將會包含 npm。</span><span class="sxs-lookup"><span data-stu-id="4ae42-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="4ae42-114">此時，hello Azure 函式的核心工具封裝只可以安裝於 Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="4ae42-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="4ae42-115">這項限制是因為暫時性的限制 tooa hello 函式主應用程式中。</span><span class="sxs-lookup"><span data-stu-id="4ae42-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="4ae42-116">[Azure 函式的核心工具]加入下列的命令別名的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="4ae42-117">**func**</span><span class="sxs-lookup"><span data-stu-id="4ae42-117">**func**</span></span>
* <span data-ttu-id="4ae42-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="4ae42-118">**azfun**</span></span>
* <span data-ttu-id="4ae42-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="4ae42-119">**azurefunctions**</span></span>

<span data-ttu-id="4ae42-120">這些別名的所有可用而不是`func`本主題中的 hello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="4ae42-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="4ae42-121">建立本機的 Functions 專案</span><span class="sxs-lookup"><span data-stu-id="4ae42-121">Create a local Functions project</span></span>

<span data-ttu-id="4ae42-122">在本機執行，函式專案時有 hello 檔案 host.json 和 local.settings.json 目錄。</span><span class="sxs-lookup"><span data-stu-id="4ae42-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="4ae42-123">此目錄是 hello 函式應用程式在 Azure 中的對等項目。</span><span class="sxs-lookup"><span data-stu-id="4ae42-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="4ae42-124">toolearn 深入了解 hello Azure 函式的資料夾結構，請參閱 hello [Azure 函式的開發人員指南](functions-reference.md#folder-structure)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="4ae42-125">在命令提示字元執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="4ae42-126">hello 輸出看起來像下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="4ae42-127">從建立 Git 儲存機制、 使用 hello 選項 tooopt `--no-source-control [-n]`。</span><span class="sxs-lookup"><span data-stu-id="4ae42-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="4ae42-128">本機設定檔</span><span class="sxs-lookup"><span data-stu-id="4ae42-128">Local settings file</span></span>

<span data-ttu-id="4ae42-129">hello 檔案 local.settings.json 儲存應用程式設定、 連接字串，與 Azure 功能的核心工具的設定。</span><span class="sxs-lookup"><span data-stu-id="4ae42-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="4ae42-130">它有下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-130">It has hello following structure:</span></span>

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
| <span data-ttu-id="4ae42-131">設定</span><span class="sxs-lookup"><span data-stu-id="4ae42-131">Setting</span></span>      | <span data-ttu-id="4ae42-132">說明</span><span class="sxs-lookup"><span data-stu-id="4ae42-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="4ae42-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="4ae42-133">**IsEncrypted**</span></span> | <span data-ttu-id="4ae42-134">當設定太**true**，使用本機電腦金鑰加密的所有值。</span><span class="sxs-lookup"><span data-stu-id="4ae42-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="4ae42-135">需搭配 `func settings` 命令使用。</span><span class="sxs-lookup"><span data-stu-id="4ae42-135">Used with `func settings` commands.</span></span> <span data-ttu-id="4ae42-136">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="4ae42-136">Default value is **false**.</span></span> |
| <span data-ttu-id="4ae42-137">**值**</span><span class="sxs-lookup"><span data-stu-id="4ae42-137">**Values**</span></span> | <span data-ttu-id="4ae42-138">於本機執行時使用的應用程式設定集合。</span><span class="sxs-lookup"><span data-stu-id="4ae42-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="4ae42-139">新增應用程式設定 toothis 物件。</span><span class="sxs-lookup"><span data-stu-id="4ae42-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="4ae42-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="4ae42-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="4ae42-141">設定 hello 連接字串 toohello hello Azure 函式執行階段會在內部使用的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ae42-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="4ae42-142">hello 儲存體帳戶支援函式的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="4ae42-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="4ae42-143">所有函式都必須設定此儲存體帳戶連接字串 (由 HTTP 觸發的函式除外)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="4ae42-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="4ae42-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="4ae42-145">設定 hello 連線字串 toohello Azure 儲存體帳戶所使用的 toostore hello 函式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4ae42-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="4ae42-146">這個選擇性的值可讓您在 hello 入口網站中存取 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4ae42-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="4ae42-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="4ae42-147">**Host**</span></span> | <span data-ttu-id="4ae42-148">在本機執行時，此區段中的設定自訂 hello 函式主控件程序。</span><span class="sxs-lookup"><span data-stu-id="4ae42-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="4ae42-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="4ae42-149">**LocalHttpPort**</span></span> | <span data-ttu-id="4ae42-150">設定 hello 執行 hello 本機函式主機時所使用的預設通訊埠 (`func host start`和`func run`)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="4ae42-151">hello`--port`命令列選項的優先順序高於此值。</span><span class="sxs-lookup"><span data-stu-id="4ae42-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="4ae42-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="4ae42-152">**CORS**</span></span> | <span data-ttu-id="4ae42-153">定義允許的 hello origins[跨原始資源共用 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="4ae42-154">來源是以不含空格的逗號分隔清單提供。</span><span class="sxs-lookup"><span data-stu-id="4ae42-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="4ae42-155">hello 萬用字元值 (**\***) 支援，允許從任何來源的要求。</span><span class="sxs-lookup"><span data-stu-id="4ae42-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="4ae42-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="4ae42-156">**ConnectionStrings**</span></span> | <span data-ttu-id="4ae42-157">包含函式的 hello 資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="4ae42-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="4ae42-158">此物件中的連接字串會新增 toohello 環境的 hello 提供者類型**System.Data.SqlClient**。</span><span class="sxs-lookup"><span data-stu-id="4ae42-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="4ae42-159">大部分的觸發程序和繫結有**連接**toohello 名稱的環境變數或應用程式設定對應的屬性。</span><span class="sxs-lookup"><span data-stu-id="4ae42-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="4ae42-160">針對每個連線屬性，都必須在 local.settings.json 檔案中定義應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="4ae42-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="4ae42-161">這些設定也可以在您的程式碼中讀取為環境變數。</span><span class="sxs-lookup"><span data-stu-id="4ae42-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="4ae42-162">在 C# 中，請使用 [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) \(機器翻譯\) 或 [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx) \(機器翻譯\)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="4ae42-163">在 JavaScript 中，使用 `process.env`。</span><span class="sxs-lookup"><span data-stu-id="4ae42-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="4ae42-164">設定指定為系統環境變數優先於 hello local.settings.json 檔案中的值。</span><span class="sxs-lookup"><span data-stu-id="4ae42-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="4ae42-165">在本機執行時，函式工具才會使用 hello local.settings.json 檔案中的設定。</span><span class="sxs-lookup"><span data-stu-id="4ae42-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="4ae42-166">根據預設，這些設定不會移轉自動發行的 tooAzure hello 專案時。</span><span class="sxs-lookup"><span data-stu-id="4ae42-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="4ae42-167">使用 hello`--publish-local-settings`切換[當您發行](#publish)toomake 確定這些設定會在 Azure 中加入 toohello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ae42-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="4ae42-168">當沒有有效的儲存體連接字串設定為**AzureWebJobsStorage**，會顯示下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="4ae42-169">在 local.settings.json 中遺失 AzureWebJobsStorage 的值。</span><span class="sxs-lookup"><span data-stu-id="4ae42-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="4ae42-170">這對 HTTP 以外的所有觸發程序是必要的。</span><span class="sxs-lookup"><span data-stu-id="4ae42-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="4ae42-171">您可以執行 'func azure functionary fetch-app-settings <functionAppName>' 或在 local.settings.json 中指定連接字串。</span><span class="sxs-lookup"><span data-stu-id="4ae42-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="4ae42-172">進行應用程式設定</span><span class="sxs-lookup"><span data-stu-id="4ae42-172">Configure app settings</span></span>

<span data-ttu-id="4ae42-173">tooset 連接字串的值，您可以執行 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="4ae42-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="4ae42-174">輸入連接字串 hello [Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="4ae42-175">使用其中一種 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="4ae42-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="4ae42-176">這兩個命令都需要您 toofirst 登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="4ae42-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="4ae42-177">建立函式</span><span class="sxs-lookup"><span data-stu-id="4ae42-177">Create a function</span></span>

<span data-ttu-id="4ae42-178">執行下列命令的 hello toocreate 函式：</span><span class="sxs-lookup"><span data-stu-id="4ae42-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="4ae42-179">`func new`支援下列選用的引數的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="4ae42-180">引數</span><span class="sxs-lookup"><span data-stu-id="4ae42-180">Argument</span></span>     | <span data-ttu-id="4ae42-181">說明</span><span class="sxs-lookup"><span data-stu-id="4ae42-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="4ae42-182">程式語言，例如 C#、 F # 或 JavaScript hello 範本。</span><span class="sxs-lookup"><span data-stu-id="4ae42-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="4ae42-183">hello 範本名稱。</span><span class="sxs-lookup"><span data-stu-id="4ae42-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="4ae42-184">hello 函式名稱。</span><span class="sxs-lookup"><span data-stu-id="4ae42-184">hello function name.</span></span> |

<span data-ttu-id="4ae42-185">例如，toocreate JavaScript HTTP 觸發程序，執行：</span><span class="sxs-lookup"><span data-stu-id="4ae42-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="4ae42-186">toocreate 佇列觸發的函式，執行：</span><span class="sxs-lookup"><span data-stu-id="4ae42-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="4ae42-187">在本機執行函式</span><span class="sxs-lookup"><span data-stu-id="4ae42-187">Run functions locally</span></span>

<span data-ttu-id="4ae42-188">toorun 函式的專案中，執行 hello 函式的主機。</span><span class="sxs-lookup"><span data-stu-id="4ae42-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="4ae42-189">hello 主機啟用為 hello 專案中的所有函式的觸發程序：</span><span class="sxs-lookup"><span data-stu-id="4ae42-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="4ae42-190">`func host start`支援下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="4ae42-191">選項</span><span class="sxs-lookup"><span data-stu-id="4ae42-191">Option</span></span>     | <span data-ttu-id="4ae42-192">說明</span><span class="sxs-lookup"><span data-stu-id="4ae42-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="4ae42-193">hello 本機連接埠 toolisten 上。</span><span class="sxs-lookup"><span data-stu-id="4ae42-193">hello local port toolisten on.</span></span> <span data-ttu-id="4ae42-194">預設值：7071。</span><span class="sxs-lookup"><span data-stu-id="4ae42-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="4ae42-195">hello 選項`VSCode`和`VS`。</span><span class="sxs-lookup"><span data-stu-id="4ae42-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="4ae42-196">以逗號分隔的 CORS 來源清單，不含空格。</span><span class="sxs-lookup"><span data-stu-id="4ae42-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="4ae42-197">hello 節點偵錯工具 toouse hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="4ae42-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="4ae42-198">預設值：Launch.json 中的值或 5858。</span><span class="sxs-lookup"><span data-stu-id="4ae42-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="4ae42-199">hello (off、 verbose、 資訊、 警告或錯誤） 的主控台追蹤層級。</span><span class="sxs-lookup"><span data-stu-id="4ae42-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="4ae42-200">預設：info。</span><span class="sxs-lookup"><span data-stu-id="4ae42-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="4ae42-201">hello 逾時的 hello 函式主機 t o 開始，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="4ae42-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="4ae42-202">預設值：20 秒。</span><span class="sxs-lookup"><span data-stu-id="4ae42-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="4ae42-203">繫結 toohttps://localhost: {port} 而不是 toohttp://localhost: {port}。</span><span class="sxs-lookup"><span data-stu-id="4ae42-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="4ae42-204">根據預設，此選項會在您的電腦上建立受信任的憑證。</span><span class="sxs-lookup"><span data-stu-id="4ae42-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="4ae42-205">對其他輸入結束 hello 程序之前暫停。</span><span class="sxs-lookup"><span data-stu-id="4ae42-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="4ae42-206">當您從整合式開發環境 (IDE) 啟動 Azure Functions Core Tools 時很有用。</span><span class="sxs-lookup"><span data-stu-id="4ae42-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="4ae42-207">Hello 函式主機啟動時，它會輸出 hello 的 HTTP URL 觸發函式：</span><span class="sxs-lookup"><span data-stu-id="4ae42-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="4ae42-208">在 VS Code 或 Visual Studio 中進行偵錯</span><span class="sxs-lookup"><span data-stu-id="4ae42-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="4ae42-209">tooattach 偵錯工具中，傳遞 hello`--debug`引數。</span><span class="sxs-lookup"><span data-stu-id="4ae42-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="4ae42-210">toodebug JavaScript 函式，使用 Visual Studio 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4ae42-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="4ae42-211">對於 C# 函式，請使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4ae42-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="4ae42-212">toodebug C# 函式，會使用`--debug vs`。</span><span class="sxs-lookup"><span data-stu-id="4ae42-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="4ae42-213">您也可以使用 [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="4ae42-214">toolaunch hello 主機及設定 JavaScript 偵錯，執行：</span><span class="sxs-lookup"><span data-stu-id="4ae42-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="4ae42-215">然後在 Visual Studio 程式碼，在 hello**偵錯**檢視中，選取**附加 tooAzure 函式**。</span><span class="sxs-lookup"><span data-stu-id="4ae42-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="4ae42-216">您可以附加中斷點、檢查變數及逐步執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="4ae42-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![使用 Visual Studio Code 進行 JavaScript 偵錯](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="4ae42-218">將測試資料 tooa 函式</span><span class="sxs-lookup"><span data-stu-id="4ae42-218">Passing test data tooa function</span></span>

<span data-ttu-id="4ae42-219">您可以也使用叫用函式直接`func run <FunctionName>`並提供 hello 函式的輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="4ae42-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="4ae42-220">此命令會使用 hello 函式類似 toorunning**測試**hello Azure 入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4ae42-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="4ae42-221">這個命令會啟動 hello 整個函式主控件。</span><span class="sxs-lookup"><span data-stu-id="4ae42-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="4ae42-222">`func run`支援下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="4ae42-223">選項</span><span class="sxs-lookup"><span data-stu-id="4ae42-223">Option</span></span>     | <span data-ttu-id="4ae42-224">說明</span><span class="sxs-lookup"><span data-stu-id="4ae42-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="4ae42-225">內嵌內容。</span><span class="sxs-lookup"><span data-stu-id="4ae42-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="4ae42-226">附加偵錯工具 toohello 主控件程序之前執行 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="4ae42-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="4ae42-227">（以秒為單位） 的時間 toowait 直到 hello 本機函式主機已就緒。</span><span class="sxs-lookup"><span data-stu-id="4ae42-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="4ae42-228">做為內容檔案名稱 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="4ae42-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="4ae42-229">不會提示輸入。</span><span class="sxs-lookup"><span data-stu-id="4ae42-229">Does not prompt for input.</span></span> <span data-ttu-id="4ae42-230">適用於自動化情節。</span><span class="sxs-lookup"><span data-stu-id="4ae42-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="4ae42-231">例如，toocall HTTP 觸發的函式和傳遞內容主體，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="4ae42-232"><a name="publish"></a>發行 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4ae42-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="4ae42-233">toopublish 函式專案 tooa 函式應用程式在 Azure 中，使用 hello`publish`命令：</span><span class="sxs-lookup"><span data-stu-id="4ae42-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="4ae42-234">您可以使用下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ae42-234">You can use hello following options:</span></span>

| <span data-ttu-id="4ae42-235">選項</span><span class="sxs-lookup"><span data-stu-id="4ae42-235">Option</span></span>     | <span data-ttu-id="4ae42-236">說明</span><span class="sxs-lookup"><span data-stu-id="4ae42-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="4ae42-237">在第 tooAzure local.settings.json hello 設定已經存在時顯示提示 toooverwrite 發行設定。</span><span class="sxs-lookup"><span data-stu-id="4ae42-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="4ae42-238">必須與 `-i` 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="4ae42-238">Must be used with `-i`.</span></span> <span data-ttu-id="4ae42-239">使用本機值在 Azure 中覆寫 AppSettings (如果不同)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="4ae42-240">預設值為提示。</span><span class="sxs-lookup"><span data-stu-id="4ae42-240">Default is prompt.</span></span>|

<span data-ttu-id="4ae42-241">hello`publish`命令會將上傳的 hello 函式專案目錄中的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="4ae42-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="4ae42-242">如果您刪除本機檔案，hello`publish`命令不會刪除它們從 Azure。</span><span class="sxs-lookup"><span data-stu-id="4ae42-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="4ae42-243">您可以刪除在 Azure 中的檔案使用 hello [Kudu 工具](functions-how-to-use-azure-function-app-settings.md#kudu)在 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="4ae42-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ae42-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ae42-244">Next steps</span></span>

<span data-ttu-id="4ae42-245">Azure Functions Core Tools 是[開放原始碼且裝載於 GitHub 上](https://github.com/azure/azure-functions-cli)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="4ae42-246">toofile bug 或功能要求[開啟 GitHub 問題](https://github.com/azure/azure-functions-cli/issues)。</span><span class="sxs-lookup"><span data-stu-id="4ae42-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Azure 函式的核心工具]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure 入口網站]: https://portal.azure.com 
