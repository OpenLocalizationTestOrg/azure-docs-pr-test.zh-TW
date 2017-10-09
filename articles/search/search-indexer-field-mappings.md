---
title: "在 Azure 搜尋索引子的 aaaField 對應"
description: "設定 Azure 搜尋索引子欄位對應 tooaccount 的欄位名稱和資料表示法中的差異"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Azure 搜尋服務索引子中的欄位對應
當使用 Azure 搜尋索引子時，您可以在其中您輸入的資料相當不符 hello 結構描述的目標索引的情況下偶爾會發現自己。 在這些情況下，您可以使用**欄位對應**tootransform hello 資料所需的圖形。

欄位對應在某些情況下很有用︰

* 您的資料來源有 `_id`欄位，但 Azure 搜尋服務不允許以底線開頭的欄位名稱。 欄位的對應可讓您太"重新命名 」 欄位。
* 您想要在 hello 的數個欄位編製索引以 hello toopopulate 相同的資料來源的資料，例如，因為您希望 tooapply 不同分析器 toothose 欄位。 欄位對應讓您「分岔」資料來源欄位。
* 您需要 tooBase64 編碼或解碼的資料。 欄位對應支援數個 **對應函式**，包括 Base64 編碼和解碼的函式。   

## <a name="setting-up-field-mappings"></a>設定欄位對應
建立新的索引子使用 hello 時，您可以加入欄位對應[建立索引子](https://msdn.microsoft.com/library/azure/dn946899.aspx)應用程式開發介面。 您可以管理使用 hello 的索引的索引子上的欄位對應[更新索引子](https://msdn.microsoft.com/library/azure/dn946892.aspx)應用程式開發介面。

欄位對應包含 3 個部分︰

1. `sourceFieldName`，表示資料來源中的欄位。 這是必要屬性。
2. 選擇性的 `targetFieldName`，表示搜尋索引中的欄位。 如果省略，hello 相同的名稱，例如使用資料來源的 hello。
3. 選擇性的 `mappingFunction`，可以使用數個預先定義的函式之一轉換您的資料。 hello 函式的完整清單位於[下方](#mappingFunctions)。

欄位對應會新增 toohello `fieldMappings` hello 索引子定義上的陣列。

例如，以下是容納欄位名稱差異的方式︰

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

索引子可以有多個欄位對應。 例如，以下是「分岔」欄位的方式︰

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Azure 搜尋會使用不區分大小寫的比較 tooresolve hello 欄位和函式名稱的欄位對應。 這是方便 （您不需要 tooget 所有正確的 hello 大小寫），但這表示您的資料來源或索引，不能只有大小寫不同的欄位。  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>欄位對應函式
目前支援的函式如下︰

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
執行*URL 安全*Base64 編碼的 hello 輸入字串。 假設 hello 輸入為 utf-8 編碼。

#### <a name="sample-use-case"></a>範例使用案例
只有 URL 安全字元可出現在 Azure 搜尋文件索引鍵 （因為客戶必須使用 hello 查閱應用程式開發介面，例如無法 tooaddress hello 文件）。 如果您的資料包含 URL unsafe 字元，而且您想 toouse 它 toopopulate 索引鍵欄位中搜尋索引中，使用此函式。   

#### <a name="example"></a>範例
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
執行的 hello 輸入字串的 Base64 解碼。 hello 輸入會假設 tooa *URL 安全*Base64 編碼字串。

#### <a name="sample-use-case"></a>範例使用案例
Blob 的自訂中繼資料值必須以 ASCII 編碼。 您可以使用 Base64 編碼 toorepresent 任意的 Unicode 字串中 blob 的自訂中繼資料。 不過，toomake 搜尋有意義，您可以使用這個函式 tooturn hello 編碼資料回 「 一般 」 字串填入搜尋索引時發生。  

#### <a name="example"></a>範例
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
分割字串欄位使用 hello 指定分隔符號和取用 hello 語彙基元在 hello hello 產生分割中的指定的位置。

例如，如果 hello 輸入是`Jane Doe`，hello`delimiter`是`" "`（空格） 和 hello`position`為 0，hello 結果為`Jane`; 如果 hello`position`為 1，hello 結果是`Doe`。 如果 hello 位置參考不存在的 tooa 語彙基元，則會傳回錯誤。

#### <a name="sample-use-case"></a>範例使用案例
資料來源包含`PersonName` 欄位中，而且您想 tooindex 成兩個不同`FirstName`和`LastName`欄位。 您可以使用這個函式 toosplit hello 輸入 hello 分隔符號使用 hello 空格字元。

#### <a name="parameters"></a>參數
* `delimiter`: 字串 toouse 做為 hello 分隔符號分割 hello 輸入的字串時。
* `position`： 在分割之後 hello 輸入字串 hello 語彙基元 toopick 整數以零為起始位置。    

#### <a name="example"></a>範例
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
轉換成字串陣列，可以使用的 toopopulate 格式化為 JSON 陣列的字串的字串`Collection(Edm.String)`hello 索引中的欄位。

例如，如果 hello 輸入字串是`["red", "white", "blue"]`，則 hello 目標欄位的型別`Collection(Edm.String)`會填入 hello 三值`red`，`white`和`blue`。 若為無法剖析為 JSON 字串陣列的輸入值，會傳回錯誤。

#### <a name="sample-use-case"></a>範例使用案例
Azure SQL database 的自然對應太的內建資料類型沒有`Collection(Edm.String)`Azure 搜尋中的欄位。 toopopulate 字串集合的欄位、 格式化為 JSON 字串陣列資料來源及使用此函式。

#### <a name="example"></a>範例
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>協助我們改進 Azure 搜尋服務
如果您有功能要求或增強功能的構想，請聯繫 toous 上我們[UserVoice 網站](https://feedback.azure.com/forums/263029-azure-search/)。
