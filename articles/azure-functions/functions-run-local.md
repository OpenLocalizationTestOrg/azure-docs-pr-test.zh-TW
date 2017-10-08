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
# <a name="code-and-test-azure-functions-locally"></a>撰寫 Azure 函式並在本機進行測試

Hello 時[Azure 入口網站]提供完整設定的工具來開發和測試 Azure 功能，許多開發人員偏好的本機開發體驗。 Azure 的函式可讓您輕鬆 toouse 您最愛的程式碼編輯器和本機開發工具 toodevelop 和測試您在本機電腦上的函式。 您的函式可以透過 Azure 中的事件觸發，您也可以在本機電腦上對 C# 和 JavaScript 函式進行偵錯。 

如果您是 Visual Studio C# 開發人員，Azure Functions 也能[與 Visual Studio 2017 整合](functions-develop-vs.md)。

## <a name="install-hello-azure-functions-core-tools"></a>安裝 hello Azure 函式的核心工具

Azure 功能的核心工具是 hello Azure 函式執行階段，您可以在本機的 Windows 電腦上執行本機版。 它不是模擬器。 它具有 hello 相同的執行階段函式，在 Azure 中的次方。

hello [Azure 函式的核心工具]提供為 npm 封裝。 您必須先[安裝 NodeJS](https://docs.npmjs.com/getting-started/installing-node) \(英文\)，它將會包含 npm。  

>[!NOTE]
>此時，hello Azure 函式的核心工具封裝只可以安裝於 Windows 電腦。 這項限制是因為暫時性的限制 tooa hello 函式主應用程式中。

[Azure 函式的核心工具]加入下列的命令別名的 hello:
* **func**
* **azfun**
* **azurefunctions**

這些別名的所有可用而不是`func`本主題中的 hello 範例所示。

## <a name="create-a-local-functions-project"></a>建立本機的 Functions 專案

在本機執行，函式專案時有 hello 檔案 host.json 和 local.settings.json 目錄。 此目錄是 hello 函式應用程式在 Azure 中的對等項目。 toolearn 深入了解 hello Azure 函式的資料夾結構，請參閱 hello [Azure 函式的開發人員指南](functions-reference.md#folder-structure)。

在命令提示字元執行下列命令的 hello:

```
func init MyFunctionProj
```

hello 輸出看起來像下列範例中的 hello:

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

從建立 Git 儲存機制、 使用 hello 選項 tooopt `--no-source-control [-n]`。

<a name="local-settings"></a>

## <a name="local-settings-file"></a>本機設定檔

hello 檔案 local.settings.json 儲存應用程式設定、 連接字串，與 Azure 功能的核心工具的設定。 它有下列結構的 hello:

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
| 設定      | 說明                            |
| ------------ | -------------------------------------- |
| **IsEncrypted** | 當設定太**true**，使用本機電腦金鑰加密的所有值。 需搭配 `func settings` 命令使用。 預設值為 **false**。 |
| **值** | 於本機執行時使用的應用程式設定集合。 新增應用程式設定 toothis 物件。  |
| **AzureWebJobsStorage** | 設定 hello 連接字串 toohello hello Azure 函式執行階段會在內部使用的 Azure 儲存體帳戶。 hello 儲存體帳戶支援函式的觸發程序。 所有函式都必須設定此儲存體帳戶連接字串 (由 HTTP 觸發的函式除外)。  |
| **AzureWebJobsDashboard** | 設定 hello 連線字串 toohello Azure 儲存體帳戶所使用的 toostore hello 函式記錄檔。 這個選擇性的值可讓您在 hello 入口網站中存取 hello 記錄檔。|
| **Host** | 在本機執行時，此區段中的設定自訂 hello 函式主控件程序。 | 
| **LocalHttpPort** | 設定 hello 執行 hello 本機函式主機時所使用的預設通訊埠 (`func host start`和`func run`)。 hello`--port`命令列選項的優先順序高於此值。 |
| **CORS** | 定義允許的 hello origins[跨原始資源共用 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)。 來源是以不含空格的逗號分隔清單提供。 hello 萬用字元值 (**\***) 支援，允許從任何來源的要求。 |
| **ConnectionStrings** | 包含函式的 hello 資料庫連接字串。 此物件中的連接字串會新增 toohello 環境的 hello 提供者類型**System.Data.SqlClient**。  | 

大部分的觸發程序和繫結有**連接**toohello 名稱的環境變數或應用程式設定對應的屬性。 針對每個連線屬性，都必須在 local.settings.json 檔案中定義應用程式設定。 

這些設定也可以在您的程式碼中讀取為環境變數。 在 C# 中，請使用 [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) \(機器翻譯\) 或 [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx) \(機器翻譯\)。 在 JavaScript 中，使用 `process.env`。 設定指定為系統環境變數優先於 hello local.settings.json 檔案中的值。 

在本機執行時，函式工具才會使用 hello local.settings.json 檔案中的設定。 根據預設，這些設定不會移轉自動發行的 tooAzure hello 專案時。 使用 hello`--publish-local-settings`切換[當您發行](#publish)toomake 確定這些設定會在 Azure 中加入 toohello 函式應用程式。

當沒有有效的儲存體連接字串設定為**AzureWebJobsStorage**，會顯示下列錯誤訊息的 hello:  

>在 local.settings.json 中遺失 AzureWebJobsStorage 的值。 這對 HTTP 以外的所有觸發程序是必要的。 您可以執行 'func azure functionary fetch-app-settings <functionAppName>' 或在 local.settings.json 中指定連接字串。
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>進行應用程式設定

tooset 連接字串的值，您可以執行 hello 下列其中一種：
* 輸入連接字串 hello [Azure 儲存體總管](http://storageexplorer.com/)。
* 使用其中一種 hello 下列命令：

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    這兩個命令都需要您 toofirst 登入 tooAzure。

## <a name="create-a-function"></a>建立函式

執行下列命令的 hello toocreate 函式：

```
func new
``` 
`func new`支援下列選用的引數的 hello:

| 引數     | 說明                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | 程式語言，例如 C#、 F # 或 JavaScript hello 範本。 |
| **`--template -t`** | hello 範本名稱。 |
| **`--name -n`** | hello 函式名稱。 |

例如，toocreate JavaScript HTTP 觸發程序，執行：

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

toocreate 佇列觸發的函式，執行：

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>在本機執行函式

toorun 函式的專案中，執行 hello 函式的主機。 hello 主機啟用為 hello 專案中的所有函式的觸發程序：

```
func host start
```

`func host start`支援下列選項的 hello:

| 選項     | 說明                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | hello 本機連接埠 toolisten 上。 預設值：7071。 |
| **`--debug <type>`** | hello 選項`VSCode`和`VS`。 |
| **`--cors`** | 以逗號分隔的 CORS 來源清單，不含空格。 |
| **`--nodeDebugPort -n`** | hello 節點偵錯工具 toouse hello 連接埠。 預設值：Launch.json 中的值或 5858。 |
| **`--debugLevel -d`** | hello (off、 verbose、 資訊、 警告或錯誤） 的主控台追蹤層級。 預設：info。|
| **`--timeout -t`** | hello 逾時的 hello 函式主機 t o 開始，以秒為單位。 預設值：20 秒。|
| **`--useHttps`** | 繫結 toohttps://localhost: {port} 而不是 toohttp://localhost: {port}。 根據預設，此選項會在您的電腦上建立受信任的憑證。|
| **`--pause-on-error`** | 對其他輸入結束 hello 程序之前暫停。 當您從整合式開發環境 (IDE) 啟動 Azure Functions Core Tools 時很有用。|

Hello 函式主機啟動時，它會輸出 hello 的 HTTP URL 觸發函式：

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>在 VS Code 或 Visual Studio 中進行偵錯

tooattach 偵錯工具中，傳遞 hello`--debug`引數。 toodebug JavaScript 函式，使用 Visual Studio 程式碼。 對於 C# 函式，請使用 Visual Studio。

toodebug C# 函式，會使用`--debug vs`。 您也可以使用 [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) \(英文\)。 

toolaunch hello 主機及設定 JavaScript 偵錯，執行：

```
func host start --debug vscode
```

然後在 Visual Studio 程式碼，在 hello**偵錯**檢視中，選取**附加 tooAzure 函式**。 您可以附加中斷點、檢查變數及逐步執行程式碼。

![使用 Visual Studio Code 進行 JavaScript 偵錯](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>將測試資料 tooa 函式

您可以也使用叫用函式直接`func run <FunctionName>`並提供 hello 函式的輸入的資料。 此命令會使用 hello 函式類似 toorunning**測試**hello Azure 入口網站中的索引標籤。 這個命令會啟動 hello 整個函式主控件。

`func run`支援下列選項的 hello:

| 選項     | 說明                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | 內嵌內容。 |
| **`--debug -d`** | 附加偵錯工具 toohello 主控件程序之前執行 hello 函式。|
| **`--timeout -t`** | （以秒為單位） 的時間 toowait 直到 hello 本機函式主機已就緒。|
| **`--file -f`** | 做為內容檔案名稱 toouse hello。|
| **`--no-interactive`** | 不會提示輸入。 適用於自動化情節。|

例如，toocall HTTP 觸發的函式和傳遞內容主體，執行下列命令的 hello:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>發行 tooAzure

toopublish 函式專案 tooa 函式應用程式在 Azure 中，使用 hello`publish`命令：

```
func azure functionapp publish <FunctionAppName>
```

您可以使用下列選項的 hello:

| 選項     | 說明                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  在第 tooAzure local.settings.json hello 設定已經存在時顯示提示 toooverwrite 發行設定。|
| **`--overwrite-settings -y`** | 必須與 `-i` 搭配使用。 使用本機值在 Azure 中覆寫 AppSettings (如果不同)。 預設值為提示。|

hello`publish`命令會將上傳的 hello 函式專案目錄中的 hello 內容。 如果您刪除本機檔案，hello`publish`命令不會刪除它們從 Azure。 您可以刪除在 Azure 中的檔案使用 hello [Kudu 工具](functions-how-to-use-azure-function-app-settings.md#kudu)在 hello [Azure 入口網站]。

## <a name="next-steps"></a>後續步驟

Azure Functions Core Tools 是[開放原始碼且裝載於 GitHub 上](https://github.com/azure/azure-functions-cli)。  
toofile bug 或功能要求[開啟 GitHub 問題](https://github.com/azure/azure-functions-cli/issues)。 

<!-- LINKS -->

[Azure 函式的核心工具]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure 入口網站]: https://portal.azure.com 
