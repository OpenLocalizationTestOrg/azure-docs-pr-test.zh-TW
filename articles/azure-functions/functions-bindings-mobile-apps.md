---
title: "aaaAzure 函式行動裝置應用程式繫結 |Microsoft 文件"
description: "了解如何在 Azure 函式 toouse Azure 行動應用程式繫結。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 事件處理, 動態運算, 無伺服器架構"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a>Azure Functions Mobile Apps 繫結
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

這篇文章說明如何 tooconfigure 和程式碼[Azure 行動應用程式](../app-service-mobile/app-service-mobile-value-prop.md)Azure 函式中的繫結。 Azure Functions 支援 Mobile Apps 的輸入和輸出繫結。

hello 行動應用程式輸入和輸出繫結可讓您[讀取和寫入 toodata 資料表](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations)行動應用程式中。

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a>Mobile Apps 輸入繫結
hello 行動應用程式的輸入繫結從行動資料表端點載入一筆記錄，並將其傳遞到您的函式。 在 C# 和 F # 函式中，任何所做的變更 toohello 記錄會傳送 hello 函式已順利結束時回復 toohello 資料表。

hello 行動應用程式輸入 tooa 函式會使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

請注意 hello 下列：

* `id`可以是靜態，或根據 hello 函式會叫用的 hello 觸發程序。 例如，如果您使用[佇列觸發程序]()那麼函式，然後`"id": "{queueTrigger}"`hello 記錄識別碼 tooretrieve 時，會使用 hello hello 佇列訊息的字串值。
* `connection`應該包含 hello 的應用程式中函式，其中包含行動應用程式的 hello URL 的應用程式設定的名稱。 hello 函式會使用此 URL tooconstruct hello 所需的 REST 作業對您的行動裝置應用程式。 您[函式應用程式中建立的應用程式設定]()包含行動裝置應用程式的 URL (如下所示`http://<appname>.azurewebsites.net`)，然後指定 hello hello 應用程式設定名稱在 hello`connection`您輸入的繫結中的屬性。 
* 您需要 toospecify`apiKey`如果您[實作 Node.js 行動裝置應用程式後端中的 API 金鑰](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key)，或[實作.NET 行動裝置應用程式後端中的 API 金鑰](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)。 toodo，您[函式應用程式中建立的應用程式設定]()包含 hello API 金鑰，然後新增 hello `apiKey` hello hello 應用程式設定名稱與您輸入繫結中的屬性。 
  
  > [!IMPORTANT]
  > 不能與您的行動裝置應用程式用戶端共用此 API 金鑰。 它應該只是分散式安全地 tooservice 端用戶端，例如 Azure 函式。 
  > 
  > [!NOTE]
  > Azure Functions 將會您的連接資訊和 API 金鑰儲存為應用程式設定，使得不會將讓它們簽入至您的原始檔控制儲存機制。 這可保護您的敏感資訊。
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a>輸入使用方式
本節說明 toouse 行動應用程式輸入的方式繫結函式程式碼中。 

Hello hello 記錄指定找到資料表和記錄識別碼，它會傳遞至名為的 hello [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm)參數 (或在 Node.js 傳遞 hello`context.bindings.<name>`物件)。 當找不到 hello 記錄時，hello 參數是`null`。 

在 C# 和 F # 函式，進行輸入 toohello 記錄 （也就是輸入參數） 的任何變更會自動傳送後 toohello 行動應用程式資料表 hello 函式已順利結束時。 在 Node.js 函數中，使用`context.bindings.<name>`tooaccess hello 輸入的記錄。 您無法在 Node.js 中修改記錄。

<a name="inputsample"></a>

## <a name="input-sample"></a>輸入範例
假設您有下列 function.json hello，來擷取行動裝置應用程式資料表的記錄識別碼 hello 佇列觸發程序的訊息為 hello:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

請參閱使用 hello hello 繫結中的輸入資料錄的 hello 特定語言的範例。 hello C# 和 F # 範例也會修改 hello 記錄`text`屬性。

* [C#](#inputcsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>C# 中的輸入範例 #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Node.js 中的輸入範例

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a>Mobile Apps 輸出繫結
使用 hello 行動應用程式輸出繫結 toowrite 新的記錄 tooa 行動應用程式資料表端點。  

hello 行動應用程式輸出的函式使用下列 JSON 物件中 hello hello `bindings` function.json 的陣列：

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

請注意 hello 下列：

* `connection`應該包含 hello 的應用程式中函式，其中包含行動應用程式的 hello URL 的應用程式設定的名稱。 hello 函式會使用此 URL tooconstruct hello 所需的 REST 作業對您的行動裝置應用程式。 您[函式應用程式中建立的應用程式設定]()包含行動裝置應用程式的 URL (如下所示`http://<appname>.azurewebsites.net`)，然後指定 hello hello 應用程式設定名稱在 hello`connection`您輸入的繫結中的屬性。 
* 您需要 toospecify`apiKey`如果您[實作 Node.js 行動裝置應用程式後端中的 API 金鑰](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key)，或[實作.NET 行動裝置應用程式後端中的 API 金鑰](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key)。 toodo，您[函式應用程式中建立的應用程式設定]()包含 hello API 金鑰，然後新增 hello `apiKey` hello hello 應用程式設定名稱與您輸入繫結中的屬性。 
  
  > [!IMPORTANT]
  > 不能與您的行動裝置應用程式用戶端共用此 API 金鑰。 它應該只是分散式安全地 tooservice 端用戶端，例如 Azure 函式。 
  > 
  > [!NOTE]
  > Azure Functions 將會您的連接資訊和 API 金鑰儲存為應用程式設定，使得不會將讓它們簽入至您的原始檔控制儲存機制。 這可保護您的敏感資訊。
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a>輸出使用方式
本節說明如何 toouse 行動應用程式輸出繫結函式程式碼中。 

在 C# 函數中，使用指名的輸出參數的型別`out object`tooaccess hello 輸出記錄。 在 Node.js 函數中，使用`context.bindings.<name>`tooaccess hello 輸出記錄。

<a name="outputsample"></a>

## <a name="output-sample"></a>輸出範例
假設您有下列 function.json，可定義佇列的觸發程序和行動應用程式輸出的 hello:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

請參閱 hello hello 行動應用程式資料表端點 hello hello 佇列訊息內容中建立一筆記錄的特定語言的範例。

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# 中的輸出範例 #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Node.js 中的輸出範例

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a>後續步驟
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

