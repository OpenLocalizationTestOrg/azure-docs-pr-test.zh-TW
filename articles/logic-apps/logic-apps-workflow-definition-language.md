---
title: "Azure 邏輯應用程式-aaaWorkflow 定義語言結構描述 |Microsoft 文件"
description: "定義 Azure 邏輯應用程式根據 hello 工作流程定義結構描述的工作流程"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 26c94308-aa0d-4730-97b6-de848bffff91
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: f12440e9ca269a9236132deeb888dbde7fb734d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-definition-language-schema-for-azure-logic-apps"></a>Azure Logic Apps 的工作流程定義語言結構描述

工作流程定義包含 hello 做為應用程式邏輯的一部分執行的實際邏輯。 此定義包含一或多個觸發程序啟動 hello 邏輯應用程式，則 hello 邏輯應用程式 tootake 的一個或多個動作。  
  
## <a name="basic-workflow-definition-structure"></a>基本工作流程定義結構

以下是 hello 的工作流程定義的基本結構：  
  
```json
{
    "$schema": "<schema-of the-definition>",
    "contentVersion": "<version-number-of-definition>",
    "parameters": { <parameter-definitions-of-definition> },
    "triggers": [ { <definition-of-flow-triggers> } ],
    "actions": [ { <definition-of-flow-actions> } ],
    "outputs": { <output-of-definition> }
}
```
  
> [!NOTE]
> hello[工作流程管理 REST API](https://docs.microsoft.com/rest/api/logic/workflows)的文件有資訊 toocreate 和管理邏輯應用程式工作流程。
  
|元素名稱|必要|說明|  
|------------------|--------------|-----------------|  
|$schema|否|指定 hello 描述 hello hello 定義語言版本的 hello JSON 結構描述檔案的位置。 當您從外部參考定義時，需要這個位置。 這份文件，hello 位置為： <p>`https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#`|  
|contentVersion|否|指定 hello 定義版本。 當您部署使用 hello 定義的工作流程時，您可以使用此值 toomake 確定 hello 右定義會使用。|  
|參數|否|指定使用 tooinput 資料到 hello 定義參數。 您最多可以定義 50 個參數。|  
|觸發程序|否|指定起始 hello 工作流程的 hello 觸發程序的資訊。 您最多可以定義 10 個觸發程序。|  
|動作|否|指定 hello 流程執行時採取的動作。 您最多可以定義 250 個動作。|  
|輸出|否|指定部署的 hello 資源的相關資訊。 您最多可以定義 10 個輸出。|  
  
## <a name="parameters"></a>參數

這個區段會指定在部署階段 hello 工作流程定義中所使用的所有 hello 參數。 所有參數必須都宣告本節中，才能使用 hello 定義的其他章節。  
  
hello 下列範例顯示 hello 參數定義結構：  

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": <default-value-of-parameter>,
        "allowedValues": [ <array-of-allowed-values> ],
        "metadata" : { "key": { "name": "value"} }
    }
}
```

|元素名稱|必要|說明|  
|------------------|--------------|-----------------|  
|類型|是|**類型**：字串 <p> **宣告**：`"parameters": {"parameter1": {"type": "string"}` <p> **規格**：`"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **類型**：securestring <p> **宣告**：`"parameters": {"parameter1": {"type": "securestring"}}` <p> **規格**：`"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **類別**：int <p> **宣告**：`"parameters": {"parameter1": {"type": "int"}}` <p> **規格**：`"parameters": {"parameter1": {"value" : 5}}` <p> **類型**：bool <p> **宣告**：`"parameters": {"parameter1": {"type": "bool"}}` <p> **規格**：`"parameters": {"parameter1": { "value": true }}` <p> **類型**：陣列 <p> **宣告**：`"parameters": {"parameter1": {"type": "array"}}` <p> **規格**：`"parameters": {"parameter1": { "value": [ array-of-values ]}}` <p> **類型**：物件 <p> **宣告**：`"parameters": {"parameter1": {"type": "object"}}` <p> **規格**：`"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **類型**：secureobject <p> **宣告**：`"parameters": {"parameter1": {"type": "object"}}` <p> **規格**：`"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **注意：** hello`securestring`和`secureobject`中不會傳回型別`GET`作業。 所有密碼、金鑰和密碼都應該使用這個類型。|  
|defaultValue|否|如果在建立 hello 資源 hello 階段指定任何值，不指定 hello hello 參數的預設值。|  
|allowedValues|否|指定 hello 參數允許的值的陣列。|  
|中繼資料|否|指定 hello 參數，例如可讀取描述或是 Visual Studio 或其他工具所使用的設計階段資料的其他資訊。|  
  
此範例顯示如何使用參數，以及在 hello 本文區段中的動作：  
  
```json
"body" :
{
  "property1": "@parameters('parameter1')"
}
```

 參數也可以在輸出中使用。  
  
## <a name="triggers-and-actions"></a>觸發程序及動作  

觸發程序和動作指定 hello 呼叫可以參與工作流程執行中。 如需有關此區段的詳細資訊，請參閱[工作流程動作和觸發程序](logic-apps-workflow-actions-triggers.md)。
  
## <a name="outputs"></a>輸出  

輸出會指定可以從工作流程執行傳回的資訊。 例如，如果您有特定的狀態或值的 tootrack 每次執行時，您可以包含 hello 中的資料執行輸出。 hello 資料會出現在該回合，hello 管理 REST API 和 hello Azure 入口網站中執行的 hello 管理 UI。 您也可以傳送這些輸出 tooother 外部系統像 power Bi 建立儀表板。 輸出是*不*hello 服務 REST API 上使用 toorespond tooincoming 要求。 使用 hello toorespond tooan 連入要求`response`動作類型範例如下：
  
```json
"outputs": {  
  "key1": {  
    "value": "value1",  
    "type" : "<type-of-value>"  
  }  
} 
```

|元素名稱|必要|說明|  
|------------------|--------------|-----------------|  
|key1|是|指定 hello hello 輸出的索引鍵識別項。 取代**key1**想 toouse tooidentify hello 輸出的名稱。|  
|value|是|指定 hello hello 輸出值。|  
|類型|是|指定 hello hello 值所指定的類型。 可能的值類型為︰ <ul><li>`string`</li><li>`securestring`</li><li>`int`</li><li>`bool`</li><li>`array`</li><li>`object`</li></ul>|
  
## <a name="expressions"></a>運算式  

Hello 定義中的 JSON 值可以是常值，或者可以是使用 hello 定義時所評估的運算式。 例如：  
  
```json
"name": "value"
```

 或  
  
```json
"name": "@parameters('password') "
```

> [!NOTE]
> 某些運算式可能不存在的 hello 執行 hello 開頭的執行階段動作從中取得其值。 您可以使用**函式**toohelp 擷取其中有些值。  
  
運算式可以出現在 JSON 字串值中的任何一處，並一律產生另一個 JSON 值。 JSON 值已經決定的 toobe 運算式，hello 運算式主體的 hello 會擷取藉由移除 hello 在符號 (@)。 如果需要的常值字串開頭為 @，字串必須使用 @@ 逸出。 hello 下列範例示範如何評估運算式。  
  
|JSON 值|結果|  
|----------------|------------|  
|"parameters"|會傳回 hello 字元 'parameters'。|  
|"parameters[1]"|會傳回 hello 字元 'parameters [1]'。|  
|"@@"|傳回包含 '@' 的 1 個字元字串。|  
|" @"|傳回包含 '@' 的 2 個字元字串。|  
  
使用「字串插補」，運算式也可以出現在字串內，其中運算式會包含在 `@{ ... }` 內。 例如： <p>`"name" : "First Name: @{parameters('firstName')} Last Name: @{parameters('lastName')}"`

hello 結果一定是字串，可讓此功能類似 toohello`concat`函式。 假設您將 `myNumber` 定義為`42` 以及將 `myString` 定義為 `sampleString`：  
  
|JSON 值|結果|  
|----------------|------------|  
|"@parameters('myString')"|傳回 `sampleString` 做為字串。|  
|"@{parameters('myString')}"|傳回 `sampleString` 做為字串。|  
|"@parameters('myNumber')"|傳回 `42` 做為「編號」。|  
|"@{parameters('myNumber')}"|傳回 `42` 做為「字串」。|  
|"Answer is: @{parameters('myNumber')}"|傳回 hello 字串`Answer is: 42`。|  
|"@concat('Answer is: ', string(parameters('myNumber')))"|傳回的字串 hello`Answer is: 42`|  
|"Answer is: @@{parameters('myNumber')}"|傳回 hello 字串`Answer is: @{parameters('myNumber')}`。|  
  
## <a name="operators"></a>運算子  

運算子是您可以使用運算式或函數內的 hello 字元。 
  
|運算子|說明|  
|--------------|-----------------|  
|.|hello 點運算子可讓您 tooreference 物件的屬性|  
|?|hello 問號運算子可讓您參考的物件不會執行階段發生錯誤的 null 屬性。 例如，您可以使用這個運算式 toohandle null 輸出觸發程序： <p>`@coalesce(trigger().outputs?.body?.property1, 'my default value')`|  
|'|hello 單引號是 hello 唯一方式 toowrap 字串常值。 因為這個標點符號衝突包裝 hello 整個運算式的 hello JSON 引號，您無法使用運算式中的雙引號。|  
|[]|hello 方括號可以是使用的 tooget 具有特定索引的陣列中的值。 例如，如果您有執行的動作，會傳遞`range(0,10)`中 toohello`forEach`函式，您可以使用這個函式 tooget 出項目的陣列的：  <p>`myArray[item()]`|  
  
## <a name="functions"></a>Functions  

您也可以在運算式內呼叫函式。 hello 下表顯示可用的 hello 函式在運算式中。  
  
|運算是|評估|  
|----------------|----------------|  
|"@function('Hello')"|呼叫 hello 函式定義成員的 hello 與 hello 常值字串 Hello 做 hello 第一個參數。|  
|"@function('It's Cool!')"|呼叫 hello 與 hello 常值字串 hello 定義的 'It's Cool ！' 的函式成員 hello 第一個參數|  
|"@function().prop1"|傳回 hello hello hello prop1 屬性值`myfunction`hello 定義的成員。|  
|"@function('Hello').prop1"|呼叫 hello 函式定義成員的 hello 與 hello 常值字串 'Hello' 做為 hello 第一個參數，並傳回 hello prop1 屬性 hello 物件。|  
|"@function(parameters('Hello'))"|評估 hello Hello 參數，並傳送嗨值 toofunction|  
  
### <a name="referencing-functions"></a>參考函式  

您可以使用這些函式 tooreference 從輸出中 hello 邏輯應用程式或 hello 邏輯應用程式建立時傳入值的其他動作。 例如，您可以從一個步驟 toouse 參考 hello 資料在另一個。  
  
|函式名稱|說明|  
|-------------------|-----------------|  
|參數|傳回 hello 定義中定義的參數值。 <p>`parameters('password')` <p> **參數編號**：1 <p> **名稱**：參數 <p> **描述**︰必要。 hello hello 參數您希望其值名稱。|  
|動作|可讓運算式 tooderive 它從其他的 JSON 名稱和值組或 hello 輸出的 hello 目前的執行階段動作的值。 propertypath 顯示於 hello 下列範例中的 hello 屬性是選擇性的。 如果未指定 propertyPath，hello 參考是 toohello 整個動作物件。 此函式僅適用於動作的內部 do-until 條件。 <p>`action().outputs.body.propertyPath`|  
|動作|可讓運算式 tooderive 它從其他的 JSON 名稱和值組或 hello 輸出的 hello 執行階段動作的值。 這些運算式會明確地宣告一個動作取決於其他動作。 propertypath 顯示於 hello 下列範例中的 hello 屬性是選擇性的。 如果未指定 propertyPath，hello 參考是 toohello 整個動作物件。 您可以使用這個項目或 hello 條件的項目 toospecify 相依性，但是您不需要這兩個 toouse hello 相同的相依資源。 <p>`actions('myAction').outputs.body.propertyPath` <p> **參數編號**：1 <p> **名稱**︰動作名稱 <p> **描述**︰必要。 hello hello 動作您希望其值名稱。 <p> Hello 動作物件上的可用屬性包括： <ul><li>`name`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>請參閱 hello [Rest API](http://go.microsoft.com/fwlink/p/?LinkID=850646)如需詳細資訊，這些屬性。|
|觸發程序|可讓運算式 tooderive 它從其他的 JSON 名稱和值組或 hello hello 執行階段觸發程序輸出的值。 propertypath 顯示於 hello 下列範例中的 hello 屬性是選擇性的。 如果未指定 propertyPath，hello 參考是 toohello 整個觸發程序物件。 <p>`trigger().outputs.body.propertyPath` <p>內觸發程序的輸入使用時，hello 函式傳回 hello 先前執行的 hello 的輸出。 不過，當使用觸發程序的條件內，hello`trigger`函式會傳回 hello 輸出 hello 目前執行。 <p> Hello 觸發程序物件上的可用屬性包括： <ul><li>`name`</li><li>`scheduledTime`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>請參閱 hello [Rest API](http://go.microsoft.com/fwlink/p/?LinkID=850644)如需詳細資訊，這些屬性。|
|actionOutputs|此函式是 `actions('actionName').outputs` 的速記 <p> **參數編號**：1 <p> **名稱**︰動作名稱 <p> **描述**︰必要。 hello hello 動作您希望其值名稱。|  
|actionBody 和內文|這些函式是 `actions('actionName').outputs.body` 的速記 <p> **參數編號**：1 <p> **名稱**︰動作名稱 <p> **描述**︰必要。 hello hello 動作您希望其值名稱。|  
|triggerOutputs|此函式是 `trigger().outputs` 的速記|  
|triggerBody|此函式是 `trigger().outputs.body` 的速記|  
|item|內的重複動作使用時，此函數會傳回此反覆項目 hello 動作的 hello 陣列中的 hello 項目。 例如，如果您有動作，會針對每個項目執行訊息陣列，則可以使用此語法︰ <p>`"input1" : "@item().subject"`| 
  
### <a name="collection-functions"></a>集合函式  

這些函數會在集合上操作，並且 tooArrays、 字串和有時字典，通常會套用。  
  
|函式名稱|說明|  
|-------------------|-----------------|  
|contains|如果字典包含索引鍵、清單包含值，或字串包含子字串，則傳回 true。 例如，此函式會傳回 `true`： <p>`contains('abacaba','aca')` <p> **參數編號**：1 <p> **名稱**︰集合中 <p> **描述**︰必要。 hello 集合 toosearch 內。 <p> **參數編號**：2 <p> **名稱**︰尋找物件 <p> **描述**︰必要。 hello 內 hello 物件 toofind**集合內**。|  
|length|傳回 hello 陣列或字串中的項目數。 例如，此函式會傳回 `3`：  <p>`length('abc')` <p> **參數編號**：1 <p> **名稱**：集合 <p> **描述**︰必要。 hello tooget hello 長度的集合。|  
|empty|如果物件、陣列或字串是空的，則傳回 true。 例如，此函式會傳回 `true`： <p>`empty('')` <p> **參數編號**：1 <p> **名稱**：集合 <p> **描述**︰必要。 hello 集合 toocheck，如果是空白。|  
|交集|傳回單一陣列或物件，在陣列或物件之間具有傳入的通用元素。 例如，此函式會傳回 `[1, 2]`： <p>`intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])` <p>hello 函式的 hello 參數可以是一組物件或一組的陣列 （不兩者的混合）。 如果有兩個物件以 hello 名稱相同，hello 具有該名稱的最後一個物件會出現在 hello 最終物件。 <p> **參數編號**：1 ... *n* <p> **名稱**：集合 *n* <p> **描述**︰必要。 hello 集合 tooevaluate。 物件必須是傳入 tooappear hello 結果中的所有集合中。|  
|union|傳回單一陣列或物件陣列或物件中傳遞 toothis 函式的所有 hello 元素。 例如，此函式會傳回 `[1, 2, 3, 10, 101]`： <p>`union([1, 2, 3], [101, 2, 1, 10])` <p>hello 函式的 hello 參數可以是一組物件或一組的陣列 （不混合類別）。 如果在 hello 最終輸出中有兩個物件具有名稱相同的 hello，hello 具有該名稱的最後一個物件會出現在 hello 最終物件中。 <p> **參數編號**：1 ... *n* <p> **名稱**：集合 *n* <p> **描述**︰必要。 hello 集合 tooevaluate。 會出現在任何 hello 集合的物件也會出現在 hello 結果。|  
|first|傳回 hello hello 陣列中的第一個項目或傳入的字串。 例如，此函式會傳回 `0`： <p>`first([0,2,3])` <p> **參數編號**：1 <p> **名稱**：集合 <p> **描述**︰必要。 hello 集合 tootake hello 第一個物件。|  
|last|傳回 hello hello 陣列中的最後一個項目或傳入的字串。 例如，此函式會傳回 `3`： <p>`last('0123')` <p> **參數編號**：1 <p> **名稱**：集合 <p> **描述**︰必要。 hello 集合 tootake hello 最後一個物件。|  
|take|傳回第一次 hello**計數**傳入 hello 陣列或字串中的項目。 例如，此函式會傳回 `[1, 2]`：  <p>`take([1, 2, 3, 4], 2)` <p> **參數編號**：1 <p> **名稱**：集合 <p> **描述**︰必要。 hello 集合而使其中 tootake hello 先**計數**物件。 <p> **參數編號**：2 <p> **名稱**：計數 <p> **描述**︰必要。 hello 數目從 hello 物件 tootake**集合**。 必須是正整數。|  
|skip|傳回 hello 的索引處開始的 hello 陣列中項目**計數**。 例如，此函式會傳回 `[3, 4]`： <p>`skip([1, 2 ,3 ,4], 2)` <p> **參數編號**：1 <p> **名稱**：集合 <p> **描述**︰必要。 第一次 hello 集合 tooskip hello**計數**的物件。 <p> **參數編號**：2 <p> **名稱**：計數 <p> **描述**︰必要。 hello 數目從 hello 前端物件 tooremove**集合**。 必須是正整數。|  
|Join|傳回字串，陣列的每個項目都使用分隔符號聯結，例如這會傳回 `"1,2,3,4"`：<br /><br /> `join([1, 2, 3, 4], ',')`<br /><br /> **參數編號**：1<br /><br /> **名稱**：集合<br /><br /> **描述**︰必要。 hello 集合 toojoin 項目。<br /><br /> **參數編號**：2<br /><br /> **名稱**：分隔符號<br /><br /> **描述**︰必要。 hello 字串 toodelimit 的項目。|  
  
### <a name="string-functions"></a>字串函數

hello 下列函式僅適用於 toostrings。 您也可以在字串上使用某些集合函式。  
  
|函式名稱|說明|  
|-------------------|-----------------|  
|concat|結合任何數目的字串。 例如，如果參數 1 為 `p1`，此函式會傳回 `somevalue-p1-somevalue`： <p>`concat('somevalue-',parameters('parameter1'),'-somevalue')` <p> **參數編號**：1 ... *n* <p> **名稱**：字串 *n* <p> **描述**︰必要。 hello 字串 toocombine 成單一字串。|  
|substring|從字串傳回字元的子集。 例如，此函式會傳回 `abc`： <p>`substring('somevalue-abc-somevalue',10,3)` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 子字串不會採取哪些 hello 從 hello 字串。 <p> **參數編號**：2 <p> **名稱**：開始索引 <p> **描述**︰必要。 hello 參數 1 中的 hello 子字串開始處的索引。 <p> **參數編號**：3 <p> **名稱**：長度 <p> **描述**︰必要。 hello hello 子字串長度。|  
|取代|以指定的字串取代字串。 例如，此函式會傳回 `hello new string`： <p>`replace('hello old string', 'old', 'new')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 搜尋參數 2 和更新參數 3，當參數 1 中找不到參數 2 hello 字串。 <p> **參數編號**：2 <p> **名稱**：舊字串 <p> **描述**︰必要。 使用參數 3，當找到符合的參數 1 中的 hello 字串 tooreplace <p> **參數編號**：3 <p> **名稱**：新字串 <p> **描述**︰必要。 hello 字串也就使用的 tooreplace 參數 2 中的 hello 字串參數 1 中找到相符項目時。|  
|GUID|此函式會產生全域唯一字串 (GUID)。 例如，此函式可以產生此 GUID：`c2ecc88d-88c8-4096-912c-d6f2e2b138ce` <p>`guid()` <p> **參數編號**：1 <p> **名稱**︰格式 <p> **描述**︰選擇性。 單一格式規範表示[tooformat hello 這個 Guid 值的方式](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx)。 hello 格式參數可以是"N"、"D"、"B"、"P"X"。 如果未提供格式，則會使用 "D"。|  
|toLower|將轉換字串 toolowercase。 例如，此函式會傳回 `two by two is four`： <p>`toLower('Two by Two is Four')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 字串 tooconvert toolower 大小寫。 如果 hello 字串中的字元，並沒有對等小寫，hello 字元會包含在傳回字串 hello 保持不變。|  
|toUpper|將轉換字串 toouppercase。 例如，此函式會傳回 `TWO BY TWO IS FOUR`： <p>`toUpper('Two by Two is Four')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 字串 tooconvert tooupper 大小寫。 如果 hello 字串中的字元，並沒有對等大寫，hello 字元會包含在傳回字串 hello 保持不變。|  
|indexof|Insensitively 尋找 hello 索引內字串的大小寫的值。 例如，此函式會傳回 `7`： <p>`indexof('hello, world.', 'world')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 可能包含 hello 值的字串。 <p> **參數編號**：2 <p> **名稱**：字串 <p> **描述**︰必要。 hello 值 toosearch hello 的索引。|  
|lastindexof|Insensitively 尋找 hello 中字串 case 值的最後一個索引。 例如，此函式會傳回 `3`： <p>`lastindexof('foofoo', 'foo')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 可能包含 hello 值的字串。 <p> **參數編號**：2 <p> **名稱**：字串 <p> **描述**︰必要。 hello 值 toosearch hello 的索引。|  
|startswith|檢查如果 hello 字串的開頭值案例 insensitively。 例如，此函式會傳回 `true`： <p>`startswith('hello, world', 'hello')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 可能包含 hello 值的字串。 <p> **參數編號**：2 <p> **名稱**：字串 <p> **描述**︰必要。 hello 值 hello 字串可能的開頭。|  
|endswith|檢查如果 hello 字串的結尾值案例 insensitively。 例如，此函式會傳回 `true`： <p>`endswith('hello, world', 'world')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 可能包含 hello 值的字串。 <p> **參數編號**：2 <p> **名稱**：字串 <p> **描述**︰必要。 hello 值 hello 字串可能會以結束。|  
|split|使用分隔字元的 hello 字串分割。 例如，此函式會傳回 `["a", "b", "c"]`： <p>`split('a;b;c',';')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 分隔的字串。 <p> **參數編號**：2 <p> **名稱**：字串 <p> **描述**︰必要。 hello 分隔符號。|  
  
### <a name="logical-functions"></a>邏輯函式  

這些函式適合條件內，而是使用的 tooevaluate 任何類型的邏輯。  
  
|函式名稱|說明|  
|-------------------|-----------------|  
|equals|如果兩個值相等，則傳回 true。 例如，如果參數 1 為 someValue，此函式會傳回 `true`： <p>`equals(parameters('parameter1'), 'someValue')` <p> **參數編號**：1 <p> **名稱**：物件 1 <p> **描述**︰必要。 太 hello 物件 toocompare**物件 2**。 <p> **參數編號**：2 <p> **名稱**：物件 2 <p> **描述**︰必要。 太 hello 物件 toocompare**物件 1**。|  
|less|如果 hello 第一個引數小於 hello 第二個則傳回 true。 請注意，值類型只能是整數、浮點數或字串。 例如，此函式會傳回 `true`： <p>`less(10,100)` <p> **參數編號**：1 <p> **名稱**：物件 1 <p> **描述**︰必要。 如果它是 hello 物件 toocheck 小於**物件 2**。 <p> **參數編號**：2 <p> **名稱**：物件 2 <p> **描述**︰必要。 如果超過 hello 物件 toocheck**物件 1**。|  
|lessOrEquals|傳回 true，如果 hello 第一個引數小於或等於 toohello 第二個。 請注意，值類型只能是整數、浮點數或字串。 例如，此函式會傳回 `true`： <p>`lessOrEquals(10,10)` <p> **參數編號**：1 <p> **名稱**：物件 1 <p> **描述**︰必要。 hello toocheck 物件是否小於或等於太**物件 2**。 <p> **參數編號**：2 <p> **名稱**：物件 2 <p> **描述**︰必要。 hello toocheck 物件是否大於或等於太**物件 1**。|  
|greater|如果第二個參數大於 hello hello 第一個引數，則傳回 true。 請注意，值類型只能是整數、浮點數或字串。 例如，此函式會傳回 `false`：  <p>`greater(10,10)` <p> **參數編號**：1 <p> **名稱**：物件 1 <p> **描述**︰必要。 如果超過 hello 物件 toocheck**物件 2**。 <p> **參數編號**：2 <p> **名稱**：物件 2 <p> **描述**︰必要。 如果它是 hello 物件 toocheck 小於**物件 1**。|  
|greaterOrEquals|如果 hello 第一個引數為大於或等於 toohello 第二個則傳回 true。 請注意，值類型只能是整數、浮點數或字串。 例如，此函式會傳回 `false`： <p>`greaterOrEquals(10,100)` <p> **參數編號**：1 <p> **名稱**：物件 1 <p> **描述**︰必要。 hello toocheck 物件是否大於或等於太**物件 2**。 <p> **參數編號**：2 <p> **名稱**：物件 2 <p> **描述**︰必要。 如果是小於或等於 hello 物件 toocheck 太**物件 1**。|  
|和|如果兩個參數都為 true，則傳回 true。 兩個引數需要 toobe 布林值。 例如，此函式會傳回 `false`： <p>`and(greater(1,10),equals(0,0))` <p> **參數編號**：1 <p> **名稱**︰布林值 1 <p> **描述**︰必要。 hello 第一個引數必須是`true`。 <p> **參數編號**：2 <p> **名稱**︰布林值 2 <p> **描述**︰必要。 hello 第二個引數必須是`true`。|  
|或|如果其中一個參數為 true，則傳回 true。 兩個引數需要 toobe 布林值。 例如，此函式會傳回 `true`： <p>`or(greater(1,10),equals(0,0))` <p> **參數編號**：1 <p> **名稱**︰布林值 1 <p> **描述**︰必要。 可能的第一個引數的 hello `true`。 <p> **參數編號**：2 <p> **名稱**︰布林值 2 <p> **描述**︰必要。 hello 第二個引數可以是`true`。|  
|否|如果 hello 參數，則傳回 true `false`。 兩個引數需要 toobe 布林值。 例如，此函式會傳回 `true`： <p>`not(contains('200 Success','Fail'))` <p> **參數編號**：1 <p> **名稱**︰布林值 <p> **描述**： 如果 hello 參數，則傳回 true `false`。 兩個引數需要 toobe 布林值。 此函式會傳回 `true`：`not(contains('200 Success','Fail'))`|  
|if|傳回指定的值，根據是否 hello 運算式導致`true`或`false`。  例如，此函式會傳回 `"yes"`： <p>`if(equals(1, 1), 'yes', 'no')` <p> **參數編號**：1 <p> **名稱**︰運算式 <p> **描述**︰必要。 布林值，判斷哪些值 hello 運算式應傳回。 <p> **參數編號**：2 <p> **名稱**：True <p> **描述**︰必要。 如果 hello 運算式 hello 值 tooreturn `true`。 <p> **參數編號**：3 <p> **名稱**：False <p> **描述**︰必要。 如果 hello 運算式 hello 值 tooreturn `false`。|  
  
### <a name="conversion-functions"></a>轉換函式  

這些函式是使用的 tooconvert 之間的每個在 hello 語言中的 hello 原生類型：  
  
- 字串  
  
- integer  
  
- float  
  
- 布林值  
  
- 陣列  
  
- 字典  

-   表單  
  
|函式名稱|說明|  
|-------------------|-----------------|  
|int|將 hello 參數 tooan 整數的轉換。 例如，此函式會傳回 100 做為數字，而不是字串︰ <p>`int('100')` <p> **參數編號**：1 <p> **名稱**︰值 <p> **描述**︰必要。 hello 是轉換的 tooan 整數的值。|  
|字串|Hello 參數 tooa 字串之間轉換。 例如，此函式會傳回 `'10'`： <p>`string(10)` <p>您也可以轉換為物件 tooa 字串。 例如，如果 hello`myPar`參數是具有一個屬性的物件`abc : xyz`，則此函式會傳回`{"abc" : "xyz"}`: <p>`string(parameters('myPar'))` <p> **參數編號**：1 <p> **名稱**︰值 <p> **描述**︰必要。 hello 值都會轉換的 tooa 字串。|  
|json|轉換 hello 參數 tooa JSON 型別值，並為 hello 相反的`string()`。 例如，此函式會傳回 `[1,2,3]` 做為陣列，而不是字串︰ <p>`json('[1,2,3]')` <p>同樣地，您可以將字串 tooan 物件。 例如，此函式會傳回 `{ "abc" : "xyz" }`： <p>`json('{"abc" : "xyz"}')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 字串也就轉換的 tooa 原生型別值。 <p>hello`json()`函數支援輸入過長的 XML。 例如，hello 參數的值： <p>`<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>` <p>是轉換的 toothis JSON: <p>`{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|float|將轉換 hello 參數引數 tooa 浮點數。 例如，此函式會傳回 `10.333`： <p>`float('10.333')` <p> **參數編號**：1 <p> **名稱**︰值 <p> **描述**︰必要。 hello 值都會轉換的 tooa 浮點數。|  
|布林|將轉換 hello 參數 tooa 布林值。 例如，此函式會傳回 `false`： <p>`bool(0)` <p> **參數編號**：1 <p> **名稱**︰值 <p> **描述**︰必要。 hello 轉換的 tooa 值，則為 true。|  
|coalesce|傳回傳入的 hello 引數中的 hello 第一個非 null 物件。 **注意**︰空字串不是 null。 例如，如果未定義參數 1 和 2，此函式會傳回 `fallback`：  <p>`coalesce(parameters('parameter1'), parameters('parameter2') ,'fallback')` <p> **參數編號**：1 ... *n* <p> **名稱**：物件*n* <p> **描述**︰必要。 hello 物件 toocheck 為 null 的。|  
|base64|傳回 hello hello 輸入字串的 base64 表示法。 例如，此函式會傳回 `c29tZSBzdHJpbmc=`： <p>`base64('some string')` <p> **參數編號**：1 <p> **名稱**︰字串 1 <p> **描述**︰必要。 hello 字串 tooencode base64 表示法。|  
|base64ToBinary|傳回 base64 編碼字串的二進位表示法。 例如，此函數會傳回 hello 的二進位表示法`some string`: <p>`base64ToBinary('c29tZSBzdHJpbmc=')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello base64 編碼的字串。|  
|base64ToString|傳回 based64 編碼字串的字串表示法。 例如，此函式會傳回 `some string`： <p>`base64ToString('c29tZSBzdHJpbmc=')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello base64 編碼的字串。|  
|Binary|傳回值的二進位表示法。  例如，此函式會傳回 `some string` 的二進位表示法： <p>`binary('some string')` <p> **參數編號**：1 <p> **名稱**︰值 <p> **描述**︰必要。 是轉換的 toobinary hello 值。|  
|dataUriToBinary|傳回資料 URI 的二進位表示法。 例如，此函數會傳回 hello 的二進位表示法`some string`: <p>`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 資料 URI tooconvert toobinary 表示法。|  
|dataUriToString|傳回資料 URI 的字串表示法。 例如，此函式會傳回 `some string`： <p>`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')` <p> **參數編號**：1 <p> **名稱**：字串<p> **描述**︰必要。 hello 資料 URI tooconvert tooString 表示法。|  
|dataUri|傳回值的資料 URI。 例如，此函式會傳回此資料 URI `text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=`： <p>`dataUri('some string')` <p> **參數編號**：1<p> **名稱**︰值<p> **描述**︰必要。 hello 值 tooconvert toodata URI。|  
|decodeBase64|傳回輸入 based64 字串的字串表示法。 例如，此函式會傳回 `some string`： <p>`decodeBase64('c29tZSBzdHJpbmc=')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**：傳回輸入 based64 字串的字串表示法。|  
|encodeUriComponent|URL 逸出 hello 傳入的字串。 例如，此函式會傳回 `You+Are%3ACool%2FAwesome`： <p>`encodeUriComponent('You Are:Cool/Awesome')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 從字串 tooescape URL unsafe 字元 hello。|  
|decodeUriComponent|取消-URL 逸出 hello 傳入的字串。 例如，此函式會傳回 `You Are:Cool/Awesome`： <p>`encodeUriComponent('You+Are%3ACool%2FAwesome')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello 字串 toodecode hello URL 不安全的字元。|  
|decodeDataUri|傳回輸入資料 URI 字串的二進位表示法。 例如，此函數會傳回 hello 的二進位表示法`some string`: <p>`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')` <p> **參數編號**：1 <p> **名稱**：字串 <p> **描述**︰必要。 hello dataURI toodecode 二進位表示法。|  
|uriComponent|傳回值的 URI 編碼表示法。 例如，此函式會傳回 `You+Are%3ACool%2FAwesome`： <p>`uriComponent('You Are:Cool/Awesome')` <p> **參數編號**：1<p> **名稱**：字串 <p> **描述**︰必要。 hello 字串 toobe 編碼的 URI。|  
|uriComponentToBinary|傳回 URI 編碼字串的二進位表示法。 例如，此函式會傳回 `You Are:Cool/Awesome` 的二進位表示法： <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **參數編號**：1 <p> **名稱**：字串<p> **描述**︰必要。 hello URI 編碼的字串。|  
|uriComponentToString|傳回 URI 編碼字串的字串表示法。 例如，此函式會傳回 `You Are:Cool/Awesome`： <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **參數編號**：1<p> **名稱**：字串<p> **描述**︰必要。 hello URI 編碼的字串。|  
|xml|傳回 hello 值的 XML 表示法。 例如，此函式會傳回 `'\<name>Alan\</name>'` 所表示的 XML 內容： <p>`xml('\<name>Alan\</name>')` <p>hello`xml()`函數支援輸入過長的 JSON 物件。 例如，hello 參數`{ "abc": "xyz" }`是轉換的 tooXML 內容：`\<abc>xyz\</abc>` <p> **參數編號**：1<p> **名稱**︰值<p> **描述**︰必要。 hello 值 tooconvert tooXML。|  
|xpath|傳回符合 hello 的 hello xpath 運算式會評估為值的 xpath 運算式的 XML 節點的陣列。 <p> **範例 1** <p>假設參數的 hello 值`p1`是此 XML 的字串表示法： <p>`<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>` <p>此程式碼：`xpath(xml(parameters('p1'), '/lab/robot/name')` <p>傳回 <p>`[ <name>R1</name>, <name>R2</name> ]` <p>當此程式碼： <p>`xpath(xml(parameters('p1'), ' sum(/lab/robot/parts)')` <p>傳回 <p>`13` <p> <p> **範例 2** <p>下列 XML 內容的給定的 hello: <p>`<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>` <p>此程式碼：`@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')` <p>或此程式碼： <p>`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')` <p>傳回 <p>`<Location xmlns="http://abc.com">xyz</Location>` <p>和此程式碼：`@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')` <p>傳回 <p>``xyz`` <p> **參數編號**：1 <p> **名稱**：Xml <p> **描述**︰必要。 hello XML 哪些 tooevaluate hello XPath 運算式。 <p> **參數編號**：2 <p> **名稱**：XPath <p> **描述**︰必要。 hello XPath 運算式 tooevaluate。|  
|array|將轉換 hello 參數 tooan 陣列。 例如，此函式會傳回 `["abc"]`： <p>`array('abc')` <p> **參數編號**：1 <p> **名稱**︰值 <p> **描述**︰必要。 hello 轉換的 tooan 陣列值。|
|createArray|建立從 hello 參數的陣列。 例如，此函式會傳回 `["a", "c"]`： <p>`createArray('a', 'c')` <p> **參數編號**：1 ... *n* <p> **名稱**︰任何 *n* <p> **描述**︰必要。 hello 值 toocombine 到陣列。|
|triggerFormDataValue|傳回單一值從表單資料或表單編碼的觸發程序輸出的 hello 金鑰名稱相符。  如果有多個符合項目，則會發生錯誤。  例如，將會傳回 hello 下列`bar`:`triggerFormDataValue('foo')`<br /><br />**參數編號**：1<br /><br />**名稱**︰索引鍵名稱<br /><br />**描述**︰必要。 hello 表單資料值 tooreturn hello 索引鍵名稱。|
|triggerFormDataMultiValues|傳回值比對從表單資料或表單編碼的觸發程序輸出的 hello 索引鍵名稱的陣列。  例如，將會傳回 hello 下列`["bar"]`:`triggerFormDataValue('foo')`<br /><br />**參數編號**：1<br /><br />**名稱**︰索引鍵名稱<br /><br />**描述**︰必要。 hello 表單資料值 tooreturn hello 索引鍵名稱。|
|triggerMultipartBody|傳回 hello 多組件的輸出中的組件 hello 觸發程序的主體。<br /><br />**參數編號**：1<br /><br />**名稱**︰索引<br /><br />**描述**︰必要。 hello 一部分 tooretrieve hello 索引。|
|formDataValue|傳回單一值從表單資料或表單編碼的動作輸出 hello 金鑰名稱相符。  如果有多個符合項目，則會發生錯誤。  例如，將會傳回 hello 下列`bar`:`formDataValue('someAction', 'foo')`<br /><br />**參數編號**：1<br /><br />**名稱**︰動作名稱<br /><br />**描述**︰必要。 hello 與表單資料或表單編碼回應 hello 動作名稱。<br /><br />**參數編號**：2<br /><br />**名稱**︰索引鍵名稱<br /><br />**描述**︰必要。 hello 表單資料值 tooreturn hello 索引鍵名稱。|
|formDataMultiValues|傳回值的比對從表單資料或表單編碼的動作輸出 hello 索引鍵名稱的陣列。  例如，將會傳回 hello 下列`["bar"]`:`formDataMultiValues('someAction', 'foo')`<br /><br />**參數編號**：1<br /><br />**名稱**︰動作名稱<br /><br />**描述**︰必要。 hello 與表單資料或表單編碼回應 hello 動作名稱。<br /><br />**參數編號**：2<br /><br />**名稱**︰索引鍵名稱<br /><br />**描述**︰必要。 hello 表單資料值 tooreturn hello 索引鍵名稱。|
|multipartBody|傳回 hello 主體多組件的輸出中的組件的動作。<br /><br />**參數編號**：1<br /><br />**名稱**︰動作名稱<br /><br />**描述**︰必要。 hello hello 動作以回應多部分名稱。<br /><br />**參數編號**：2<br /><br />**名稱**︰索引<br /><br />**描述**︰必要。 hello 一部分 tooretrieve hello 索引。|

### <a name="math-functions"></a>數學函式  

這些函式可用於任一類型的數字︰**整數**和**浮點數**。  
  
|函式名稱|說明|  
|-------------------|-----------------|  
|新增|傳回的 hello 兩個數字相加 hello 結果。 例如，此函式會傳回 `20.333`： <p>`add(10,10.333)` <p> **參數編號**：1 <p> **名稱**：被加數 1 <p> **描述**︰必要。 太 hello 數字 tooadd**被加數向上進位 2**。 <p> **參數編號**：2 <p> **名稱**：被加數 2 <p> **描述**︰必要。 太 hello 數字 tooadd**被加數向上進位 1**。|  
|sub|傳回兩個數字中減去的 hello 結果。 例如，此函式會傳回 `-0.333`： <p>`sub(10,10.333)` <p> **參數編號**：1 <p> **名稱**：被減數 <p> **描述**︰必要。 hello 編號**減數**被移除了。 <p> **參數編號**：2 <p> **名稱**︰減數 <p> **描述**︰必要。 hello hello 從數字 tooremove**被減數**。|  
|mul|傳回 hello 結果將 hello 兩個數字相乘。 例如，此函式會傳回 `103.33`： <p>`mul(10,10.333)` <p> **參數編號**：1 <p> **名稱**︰被乘數 1 <p> **描述**︰必要。 hello 數字 toomultiply**被乘數 2**與。 <p> **參數編號**：2 <p> **名稱**︰被乘數 2 <p> **描述**︰必要。 hello 數字 toomultiply**被乘數 1**與。|  
|div|傳回 hello 結果除以 hello 兩個數字。 例如，此函式會傳回 `1.0333`： <p>`div(10.333,10)` <p> **參數編號**：1 <p> **名稱**︰被除數 <p> **描述**︰必要。 數字 toodivide hello 的 hello**除數**。 <p> **參數編號**：2 <p> **名稱**︰除數 <p> **描述**︰必要。 數字 toodivide hello hello**被除數**所。|  
|mod|傳回 hello 餘數除以 hello 兩個數字 （模數） 之後。 例如，此函式會傳回 `2`： <p>`mod(10,4)` <p> **參數編號**：1 <p> **名稱**︰被除數 <p> **描述**︰必要。 數字 toodivide hello 的 hello**除數**。 <p> **參數編號**：2 <p> **名稱**︰除數 <p> **描述**︰必要。 數字 toodivide hello hello**被除數**所。 Hello 相除之後不會採取 hello 其餘部分。|  
|Min|有兩個不同的模式可以呼叫此函式。 <p>這裡`min`採用陣列，而 hello 函式傳回`0`: <p>`min([0,1,2])` <p>或者，此函式可以採用值的以逗號分隔清單，也傳回 `0`： <p>`min(0,1,2)` <p> **請注意**： 所有值必須都是數字，tooonly 所以 hello 陣列 hello 參數是陣列，如果沒有具有數字。 <p> **參數編號**：1 <p> **名稱**：集合或值 <p> **描述**︰必要。 值 toofind hello 最小值或一組 hello 第一個值的其中一個陣列。 <p> **參數編號**：2 ... *n* <p> **名稱**：值 *n* <p> **描述**︰選擇性。 如果值為 hello 第一個參數，然後您可以將額外的值傳遞並 hello 所有傳遞值的最小值傳回。|  
|max|有兩個不同的模式可以呼叫此函式。 <p>這裡`max`採用陣列，而 hello 函式傳回`2`: <p>`max([0,1,2])` <p>或者，此函式可以採用值的以逗號分隔清單，也傳回 `2`： <p>`max(0,1,2)` <p> **請注意**： 所有值必須都是數字，tooonly 所以 hello 陣列 hello 參數是陣列，如果沒有具有數字。 <p> **參數編號**：1 <p> **名稱**：集合或值 <p> **描述**︰必要。 值 toofind hello 最大值或一組 hello 第一個值的其中一個陣列。 <p> **參數編號**：2 ... *n* <p> **名稱**：值 *n* <p> **描述**︰選擇性。 如果值為 hello 第一個參數，然後您可以將額外的值傳遞並 hello 所有傳遞值的最大值傳回。|  
|range|從特定數字開始產生整數的陣列。 您定義 hello 的 hello 傳回陣列的長度。 <p>例如，此函式會傳回 `[3,4,5,6]`： <p>`range(3,4)` <p> **參數編號**：1 <p> **名稱**：開始索引 <p> **描述**︰必要。 hello hello 陣列中的第一個整數。 <p> **參數編號**：2 <p> **名稱**：計數 <p> **描述**︰必要。 此值為 hello 陣列中的 hello 數目的整數。|  
|rand|產生的隨機整數 hello 內指定範圍 （含只能在第一個 end 上）。 例如，此函式可傳回 `0` 或 '1'： <p>`rand(0,2)` <p> **參數編號**：1 <p> **名稱**︰最小值 <p> **描述**︰必要。 hello 最低的整數，可傳回。 <p> **參數編號**：2 <p> **名稱**︰最大值 <p> **描述**︰必要。 此值為 hello 下一個整數之後 hello 可能傳回的最大整數。|  
  
### <a name="date-functions"></a>日期函式  
  
|函式名稱|說明|  
|-------------------|-----------------|  
|utcnow|傳回 hello 目前時間戳記，做為字串，例如： `2017-03-15T13:27:36Z`: <p>`utcnow()` <p> **參數編號**：1 <p> **名稱**︰格式 <p> **描述**︰選擇性。 任一[單一格式規範字元](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx)或[的自訂格式模式](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)，指出如何 tooformat hello 此時間戳記值。 如果未提供格式，將使用 hello ISO 8601 格式 ("o")。|  
|addseconds|將傳入的秒數 tooa 字串時間戳記的整數數字。 hello 的秒數可以是正數或負數。 根據預設，hello 結果是以 ISO 8601 字串格式 ("o")，除非格式規範中有提供。 例如：`2015-03-15T13:27:00Z`： <p>`addseconds('2015-03-15T13:27:36Z', -36)` <p> **參數編號**：1 <p> **名稱**︰時間戳記 <p> **描述**︰必要。 字串，包含 hello 時間。 <p> **參數編號**：2 <p> **名稱**︰秒 <p> **描述**︰必要。 hello 秒 tooadd 數目。 可以是負數 toosubtract 秒。 <p> **參數編號**：3 <p> **名稱**︰格式 <p> **描述**︰選擇性。 任一[單一格式規範字元](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx)或[的自訂格式模式](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)，指出如何 tooformat hello 此時間戳記值。 如果未提供格式，將使用 hello ISO 8601 格式 ("o")。|  
|addminutes|將傳入的分鐘 tooa 字串時間戳記的整數數字。 hello 的分鐘數可以是正數或負數。 根據預設，hello 結果是以 ISO 8601 字串格式 ("o")，除非格式規範中有提供。 例如：`2015-03-15T14:00:36Z`： <p>`addminutes('2015-03-15T13:27:36Z', 33)` <p> **參數編號**：1 <p> **名稱**︰時間戳記 <p> **描述**︰必要。 字串，包含 hello 時間。 <p> **參數編號**：2 <p> **名稱**︰分鐘 <p> **描述**︰必要。 hello tooadd 分鐘數。 可以是負數 toosubtract 分鐘。 <p> **參數編號**：3 <p> **名稱**︰格式 <p> **描述**︰選擇性。 任一[單一格式規範字元](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx)或[的自訂格式模式](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)，指出如何 tooformat hello 此時間戳記值。 如果未提供格式，將使用 hello ISO 8601 格式 ("o")。|  
|addhours|將傳入的小時 tooa 字串時間戳記的整數數字。 hello 數可以是正數或負數。 根據預設，hello 結果是以 ISO 8601 字串格式 ("o")，除非格式規範中有提供。 例如：`2015-03-16T01:27:36Z`： <p>`addhours('2015-03-15T13:27:36Z', 12)` <p> **參數編號**：1 <p> **名稱**︰時間戳記 <p> **描述**︰必要。 字串，包含 hello 時間。 <p> **參數編號**：2 <p> **名稱**︰小時 <p> **描述**︰必要。 hello 小時 tooadd 數目。 可以是負數 toosubtract 小時。 <p> **參數編號**：3 <p> **名稱**︰格式 <p> **描述**︰選擇性。 任一[單一格式規範字元](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx)或[的自訂格式模式](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)，指出如何 tooformat hello 此時間戳記值。 如果未提供格式，將使用 hello ISO 8601 格式 ("o")。|  
|adddays|將傳入的天 tooa 字串時間戳記的整數數字。 hello 數天內可以是正數或負數。 根據預設，hello 結果是以 ISO 8601 字串格式 ("o")，除非格式規範中有提供。 例如：`2015-02-23T13:27:36Z`： <p>`addseconds('2015-03-15T13:27:36Z', -20)` <p> **參數編號**：1 <p> **名稱**︰時間戳記 <p> **描述**︰必要。 字串，包含 hello 時間。 <p> **參數編號**：2 <p> **名稱**︰天 <p> **描述**︰必要。 hello 天 tooadd 數目。 可以是負數 toosubtract 天。 <p> **參數編號**：3 <p> **名稱**︰格式 <p> **描述**︰選擇性。 任一[單一格式規範字元](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx)或[的自訂格式模式](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)，指出如何 tooformat hello 此時間戳記值。 如果未提供格式，將使用 hello ISO 8601 格式 ("o")。|  
|formatDateTime|以日期格式傳回字串。 根據預設，hello 結果是以 ISO 8601 字串格式 ("o")，除非格式規範中有提供。 例如：`2015-02-23T13:27:36Z`： <p>`formatDateTime('2015-03-15T13:27:36Z', 'o')` <p> **參數編號**：1 <p> **名稱**︰日期 <p> **描述**︰必要。 包含 hello 日期的字串。 <p> **參數編號**：2 <p> **名稱**︰格式 <p> **描述**︰選擇性。 任一[單一格式規範字元](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx)或[的自訂格式模式](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)，指出如何 tooformat hello 此時間戳記值。 如果未提供格式，將使用 hello ISO 8601 格式 ("o")。|  
|startOfHour|傳回 hello 開頭 hello 小時 tooa 字串的時間戳記中傳遞。 例如：`2017-03-15T13:00:00Z`：<br /><br /> `startOfHour('2017-03-15T13:27:36Z')`<br /><br /> **參數編號**：1<br /><br /> **名稱**︰時間戳記<br /><br /> **描述**︰必要。 這是包含 hello 時間的字串。<br /><br />**參數編號**：2<br /><br /> **名稱**︰格式<br /><br /> **描述**︰選擇性。 任一[單一格式規範字元](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx)或[的自訂格式模式](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)，指出如何 tooformat hello 此時間戳記值。 如果未提供格式，將使用 hello ISO 8601 格式 ("o")。|  
|startOfDay|傳回 hello 開頭 hello 天 tooa 字串時間戳記中傳遞。 例如：`2017-03-15T00:00:00Z`：<br /><br /> `startOfDay('2017-03-15T13:27:36Z')`<br /><br /> **參數編號**：1<br /><br /> **名稱**︰時間戳記<br /><br /> **描述**︰必要。 這是包含 hello 時間的字串。<br /><br />**參數編號**：2<br /><br /> **名稱**︰格式<br /><br /> **描述**︰選擇性。 任一[單一格式規範字元](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx)或[的自訂格式模式](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)，指出如何 tooformat hello 此時間戳記值。 如果未提供格式，將使用 hello ISO 8601 格式 ("o")。| 
|startOfMonth|傳回 hello 開頭 hello 月份 tooa 字串時間戳記中傳遞。 例如：`2017-03-01T00:00:00Z`：<br /><br /> `startOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **參數編號**：1<br /><br /> **名稱**︰時間戳記<br /><br /> **描述**︰必要。 這是包含 hello 時間的字串。<br /><br />**參數編號**：2<br /><br /> **名稱**︰格式<br /><br /> **描述**︰選擇性。 任一[單一格式規範字元](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx)或[的自訂格式模式](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)，指出如何 tooformat hello 此時間戳記值。 如果未提供格式，將使用 hello ISO 8601 格式 ("o")。| 
|dayOfWeek|傳回 hello 字串時間戳記的星期幾元件。  星期日是 0、星期一是 1，依此類推。 例如：`3`：<br /><br /> `dayOfWeek('2017-03-15T13:27:36Z')`<br /><br /> **參數編號**：1<br /><br /> **名稱**︰時間戳記<br /><br /> **描述**︰必要。 這是包含 hello 時間的字串。| 
|dayOfMonth|傳回 hello 一天的月份元件字串時間戳記。 例如：`15`：<br /><br /> `dayOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **參數編號**：1<br /><br /> **名稱**︰時間戳記<br /><br /> **描述**︰必要。 這是包含 hello 時間的字串。| 
|dayOfYear|傳回 hello 一天的年份元件字串時間戳記。 例如：`74`：<br /><br /> `dayOfYear('2017-03-15T13:27:36Z')`<br /><br /> **參數編號**：1<br /><br /> **名稱**︰時間戳記<br /><br /> **描述**︰必要。 這是包含 hello 時間的字串。| 
|刻度|傳回 hello 刻度字串時間戳記的屬性。 例如：`1489603019`：<br /><br /> `ticks('2017-03-15T18:36:59Z')`<br /><br /> **參數編號**：1<br /><br /> **名稱**︰時間戳記<br /><br /> **描述**︰必要。 這是包含 hello 時間的字串。| 
  
### <a name="workflow-functions"></a>工作流程函式  

這些函式可協助您取得 hello 工作流程本身的執行階段資訊。  
  
|函式名稱|說明|  
|-------------------|-----------------|  
|listCallbackUrl|傳回字串 toocall tooinvoke hello 觸發程序或動作。 <p> **注意**︰此函式只能用於 **httpWebhook** 和 **apiConnectionWebhook**，不能用於**手動**、**週期**、**http**，或**apiConnection**。 <p>例如，hello`listCallbackUrl()`函式會傳回： <p>`https://prod-01.westus.logic.azure.com:443/workflows/1235...ABCD/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=xxx...xxx` |  
|工作流程|此函式讓您所有的 hello 詳細資料的 hello 工作流程本身在 hello 執行階段。 <p> Hello 工作流程物件上的可用屬性包括： <ul><li>`name`</li><li>`type`</li><li>`id`</li><li>`location`</li><li>`run`</li></ul> <p> hello 值 hello`run`屬性是具有下列屬性的物件： <ul><li>`name`</li><li>`type`</li><li>`id`</li></ul> <p>請參閱 hello [Rest API](http://go.microsoft.com/fwlink/p/?LinkID=525617)如需詳細資訊，這些屬性。<p> 例如，tooget hello 名稱 hello 目前的執行，請使用 hello`"@workflow().run.name"`運算式。 |

## <a name="next-steps"></a>後續步驟

[工作流程動作與觸發程序](logic-apps-workflow-actions-triggers.md)
