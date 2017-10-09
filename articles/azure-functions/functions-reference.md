---
title: "開發 Azure 函式 aaaGuidance |Microsoft 文件"
description: "了解 hello Azure 函式概念和技術，您需要在 Azure 中，所有的程式語言和繫結之間的 toodevelop 函式。"
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "開發指南, azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Azure Functions 開發人員指南
在 Azure 功能中，特定的功能會共用一些核心技術概念和元件，不論語言 hello 或您使用的繫結。 您跳至了解給定的語言或繫結的詳細資料特定 tooa，先確定 tooread 透過適用於這些 tooall 本概觀。

本文章假設，您已閱讀 hello [Azure 函式概觀](functions-overview.md)並十分熟悉[WebJobs SDK 的概念，例如觸發程序，繫結和 hello JobHost 執行階段](../app-service-web/websites-dotnet-webjobs-sdk.md)。 Azure 的函式根據 hello WebJobs SDK。 

## <a name="function-code"></a>函式程式碼
A*函式*是 hello Azure 函式中的主要概念。 您選擇的語言撰寫的函式的程式碼並儲存 hello 程式碼和組態檔中的 hello 相同的資料夾。 hello 組態會命名為`function.json`，其中包含 JSON 組態資料。 支援各種不同的語言，和每個都有稍微不同的體驗最佳化 toowork 最適合該語言。 

hello function.json 檔案定義 hello 函式繫結和其他組態設定。 hello runtime 使用這個檔案 toodetermine hello 事件 toomonitor 和如何 toopass 資料到傳回的資料，從函式執行。 hello 以下為範例 function.json 檔案。

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

設定 hello`disabled`屬性太`true`tooprevent hello 函式不會執行。

hello`bindings`屬性可讓您設定觸發程序和繫結。 每個繫結共用一些常見的設定和某些設定，這是特定 tooa 特定類型的繫結。 每一個繫結需要 hello 下列設定：

| 屬性 | 值/類型 | 註解 |
| --- | --- | --- |
| `type` |string |繫結類型。 例如， `queueTrigger`。 |
| `direction` |'in'、'out' |指出 hello 繫結是否接收到 hello 函式的資料或傳送的資料，從 hello 函式。 |
| `name` |字串 |用於 hello hello 名稱繫結 hello 函式中的資料。 C# 中，這是引數名稱;javascript，它的索引鍵/值清單中的 hello 索引鍵。 |

## <a name="function-app"></a>函式應用程式
函式應用程式是由一或多個由 Azure App Service 一起管理的個別函式所組成。 所有函式應用程式共用中的 hello 函式 hello 相同定價計劃、 連續部署和執行階段版本。 函式的所有共用 hello 以多個語言可以撰寫相同函式應用程式。 請將函式應用程式，為方法 tooorganize 來共同管理您的函式。 

## <a name="runtime-script-host-and-web-host"></a>執行階段 (指令碼主機和 Web 主機)
hello 執行階段或指令碼主機是 hello 基礎 WebJobs SDK host 接聽事件，會收集並傳送資料，及最終會執行您的程式碼。 

toofacilitate HTTP 觸發程序，也是設計的 toosit 前面 hello 指令碼裝載在實際執行案例中的 web 主機。 有兩部主機，可幫助 tooisolate hello script host hello 前端流量由 hello web 主機所管理。

## <a name="folder-structure"></a>資料夾結構
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

當設定 Azure App Service 中的函式 tooa 函式應用程式部署的專案，您可以將此資料夾結構與站台碼。 您可以使用現有工具 (如持續整合和部署) 或自訂部署指令碼來執行部署時間封裝安裝或程式碼 Transpilation。

> [!NOTE]
> 請確定 toodeploy 您`host.json`檔案和函式資料夾直接 toohello`wwwroot`資料夾。 不包含 hello`wwwroot`中您的部署資料夾。 否則，您會得到 `wwwroot\wwwroot` 資料夾。 
> 
> 

## <a id="fileupdate"></a>Tooupdate 應用程式檔案的運作方式
hello Azure 入口網站內建的 hello 函式編輯器可讓您更新 hello *function.json*檔案和 hello 函式的程式碼檔案。 tooupload 或其他更新檔，例如*package.json*或*project.json*或相依性，您有 toouse 其他部署方法。

函式應用程式已內建應用程式服務，因此所有 hello[部署選項可用 toostandard web 應用程式](../app-service-web/web-sites-deploy.md)還有適用於函式應用程式。 以下是一些您可以使用 tooupload 或更新函式應用程式檔案的方法。 

#### <a name="toouse-app-service-editor"></a>toouse 應用程式服務編輯器
1. 在 hello Azure 函式入口網站中，按一下 **函式應用程式設定**。
2. 在 hello**進階設定**區段中，按一下**移 tooApp 服務設定**。
3. 在 [應用程式功能表導覽] 中的 [開發工具] 底下，按一下 [App Service 編輯器]。
4. 按一下 [執行] 。
   
   應用程式服務編輯器載入後，您會看到 hello *host.json*下的檔案和函式資料夾*wwwroot*。 
5. 開啟檔案 tooedit 它們，或從拖放您開發機器 tooupload 檔案。

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>toouse hello 函式應用程式的 SCM (Kudu) 端點
1. 瀏覽至 `https://<function_app_name>.scm.azurewebsites.net`。
2. 按一下 [偵錯主控台] > [CMD]。
3. 瀏覽過`D:\home\site\wwwroot\`tooupdate *host.json*或`D:\home\site\wwwroot\<function_name>`tooupdate 函式的檔案。
4. 拖放檔案，您想成 hello tooupload 適當 hello 檔案方格中的資料夾。 您將可以卸除檔案的 hello 檔案方格中有兩個區域。 如*.zip*檔案，與 hello 標籤會出現一個方塊 」 將拖曳到此處 tooupload 與解壓縮。 」 針對其他檔案類型，卸除 hello 檔案方格中，但 hello 」 解壓縮"方塊外。

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>toouse 連續部署
請遵循 hello 主題中的 hello 指示[Azure 函式的連續部署](functions-continuous-deployment.md)。

## <a name="parallel-execution"></a>平行執行
多個觸發事件發生時速度快過單一執行緒的函式執行階段可以處理它們，hello 執行階段可能會叫用數次以平行方式的 hello 函式。  如果函式的應用程式使用 hello[裝載計劃的耗用量](functions-scale.md#how-the-consumption-plan-works)，hello 函式應用程式無法自動向外擴充。  Hello 函式應用程式，每個執行個體是否 hello 應用程式上執行 hello 裝載計劃或一般的耗用量[應用程式服務裝載計劃](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)，可能會處理透過多個執行緒並行函式引動過程。  hello 並行函式引動過程中每個函式應用程式執行個體的數目上限依據觸發程序正由其他函式 hello 函式應用程式中的 hello 資源以及 hello 類型而異。

## <a name="functions-runtime-versioning"></a>Functions 執行階段版本設定

您可以設定的 hello 函式執行階段使用 hello hello 版本`FUNCTIONS_EXTENSION_VERSION`應用程式設定。 例如，hello 值"~ 1"表示函式應用程式會使用 1，因為它的主要版本。 函式應用程式的發行是升級的 tooeach 新次要版本。 您可以在 hello 檢視 hello 函式應用程式的確切版本**設定**hello Azure 入口網站中的索引標籤。

## <a name="repositories"></a>儲存機制
hello Azure 函式的程式碼是開放原始碼，並儲存在 GitHub 儲存機制：

* [Azure Functions 執行階段](https://github.com/Azure/azure-webjobs-sdk-script/)
* [Azure Functions 入口網站](https://github.com/projectkudu/AzureFunctionsPortal)
* [Azure Functions 範本](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/)
* [Azure WebJobs SDK 延伸模組](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>繫結
以下是所有已支援繫結的表格。

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>報告問題
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列資源的 hello:

* [Azure Functions 的最佳作法](functions-best-practices.md)
* [Azure Functions C# 開發人員參考](functions-reference-csharp.md)
* [Azure Functions F# 開發人員參考](functions-reference-fsharp.md)
* [Azure Functions NodeJS 開發人員參考](functions-reference-node.md)
* [Azure Functions 觸發程序和繫結](functions-triggers-bindings.md)
* [Azure 的函式： hello 旅程](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/)hello Azure 應用程式服務團隊部落格上。 Azure Functions 的開發歷史。

