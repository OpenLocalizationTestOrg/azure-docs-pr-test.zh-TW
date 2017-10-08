---
title: "Azure Cosmos DB 中的地理空間資料與 aaaWorking |Microsoft 文件"
description: "了解如何 toocreate，索引具有 Azure Cosmos DB 空間物件，以及查詢 hello DocumentDB API。"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>使用 Azure Cosmos DB 中的地理空間和 GeoJSON 位置資料
這篇文章是簡介 toohello geospatial 中的功能[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)。 閱讀此文章之後, 將無法 tooanswer hello 下列問題：

* 如何在 Azure Cosmos DB 中儲存空間資料？
* 如何以 SQL 和 LINQ 查詢 Azure Cosmos DB 中的地理空間資料？
* 如何在 Azure Cosmos DB 中啟用或停用空間編製索引？

本文示範如何使用空間資料與 toowork hello DocumentDB API。 請參閱此 [GitHub 專案](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs)中的程式碼範例。

## <a name="introduction-toospatial-data"></a>簡介 toospatial 資料
空間資料會描述 hello 位置與形狀的空間中的物件。 在大部分的應用程式，這些對應 tooobjects hello 地球，也就是地理空間資料上。 空間資料可以是個人使用的 toorepresent hello 位置、 感興趣的位置或 hello 界限的縣 （市） 或湖泊。 常見使用案例通常涉及鄰近性查詢，例如「尋找我目前位置附近的所有咖啡廳」。 

### <a name="geojson"></a>GeoJSON
Azure Cosmos DB 支援索引和查詢表示使用 hello geospatial 點資料[GeoJSON 規格](https://tools.ietf.org/html/rfc7946)。 GeoJSON 資料結構一律為有效的 JSON 物件，因此可透過 Azure Cosmos DB 來儲存及查詢，無須使用任何特殊的工具或程式庫。 hello Azure Cosmos DB Sdk 提供 helper 類別和方法，可讓您輕鬆 toowork 空間資料。 

### <a name="points-linestrings-and-polygons"></a>點、LineString 和多邊形
**點** 代表空間中的單一位置。 在地理空間資料點會代表 hello 確切位置，可能是雜貨店、 kiosk、 汽車或某個城市的街道地址。  點會使用其座標組或經緯度，以 GeoJSON (和 Azure Cosmos DB) 來表示。 以下是點的 JSON 範例。

**Azure Cosmos DB 中的點**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> hello GeoJSON 規格指定經度第一個和緯度第二個。 如同其他的地圖應用程式，經度和緯度為角度，並以度為表示單位。 經度值會從 hello 子午線衡量，並介於-180 和 180.0 度和緯度值從 hello 赤道衡量，並介於-90.0 和 90.0 度。 
> 
> Azure Cosmos DB 解譯座標表示每個 hello WGS 84 參考系統。 請參閱下方詳細的座標參考系統資料。
> 
> 

如這個包含位置資料的使用者設定檔範例所示，這可內嵌於 Azure Cosmos DB 文件中：

**儲存在 Azure Cosmos DB 中含有位置的使用設定檔**

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

此外 toopoints，GeoJSON 也支援 LineStrings 和多邊形。 **LineStrings**代表一系列的空間中的兩個或多個點且 hello 將它們連接的直線線段。 在地理空間資料 LineStrings 是常用的 toorepresent 高速公路或河。 **多邊形**是由連接的點組成邊界，並形成封閉的 LineString。 多邊形會像湖泊常用的 toorepresent 自然格式或政治轄區像城市與州。 以下是 Azure Cosmos DB 中多邊形的範例。 

**GeoJSON 中的多邊形**

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> hello GeoJSON 規格要求有效的多邊形的 hello 所提供的最後一個座標組應可讓相同 hello 為 hello 第一次，toocreate 封閉圖形。
> 
> 多邊形內的點必須以逆時針順序指定。 順時針旋轉的順序指定的多邊形代表 hello 反 hello 區域內。
> 
> 

在加法 tooPoint，LineString 和多邊形，GeoJSON 也會指定如何 hello 表示 toogroup 多個地理空間位置，以及如何 tooassociate 任意數目的屬性與地理位置**功能**。 由於這些物件都是有效的 JSON，因此均可在 Azure Cosmos DB 中儲存及處理。 不過，Azure Cosmos DB 僅支援自動編製點的索引。

### <a name="coordinate-reference-systems"></a>座標參考系統
Hello 地球的 hello 圖形是異常，因為地理空間資料的座標被以許多的座標參考系統 (CR)，每個都有自己的畫面格的參考和度量單位。 比方說，「 國家 （地區） 方格的英國"hello 是 「 參照系統是非常精確 hello 英國，但超出它。 

hello 最受歡迎使用 CR 今天為 hello World Geodetic System [WGS 84](http://earth-info.nga.mil/GandG/wgs84/)。 GPS 裝置和許多地圖服務，包括 Google 地圖與 Bing Maps API 均是使用 WGS-84。 Azure Cosmos DB 支援索引和查詢使用 hello 只 WGS 84 CRS 地理空間資料。 

## <a name="creating-documents-with-spatial-data"></a>建立具有空間資料的文件
當您建立包含 GeoJSON 值的文件時，它們會自動索引中的 hello 集合素來 toohello 編製索引原則的空間索引。 如果您是以動態類型的語言 (如 Python 或 Node.js) 使用 Azure Cosmos DB SDK，則必須建立有效的 GeoJSON。

**以 Node.js 建立具有地理空間資料的文件**

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

如果您正在使用 hello DocumentDB Api，您可以使用 hello`Point`和`Polygon`內 hello 類別`Microsoft.Azure.Documents.Spatial`應用程式物件內的命名空間 tooembed 位置資訊。 這些類別有助於簡化 hello 序列化和還原序列化成 GeoJSON 空間資料。

**以 .NET 建立具有地理空間資料的文件**

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

如果您沒有 hello 緯度和經度資訊，但有 hello 實體位址或位置的名稱，例如縣市或國家/地區，您可以使用這類 Bing 地圖服務 REST 服務的地理編碼服務查閱 hello 實際座標。 在 [這裡](https://msdn.microsoft.com/library/ff701713.aspx)深入了解 Bing Maps 地理編碼。

## <a name="querying-spatial-types"></a>查詢空間類型
既然我們已經看看如何 tooinsert 地理空間資料，讓我們看看如何 tooquery 使用 Azure Cosmos DB SQL 和 LINQ 使用此資料。

### <a name="spatial-sql-built-in-functions"></a>空間 SQL 內建函數
Azure Cosmos DB 支援 hello 下列開放式地理空間協會 (OGC) 的地理空間查詢內建函式。 如需有關 hello 整組 hello SQL 語言中的內建函式的詳細資訊，請參閱太[查詢 Azure Cosmos DB](documentdb-sql-query.md)。

<table>
<tr>
  <td><strong>用法</strong></td>
  <td><strong>說明</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (spatial_expr, spatial_expr)</td>
  <td>傳回兩個 hello GeoJSON 點、 多邊形或 LineString 運算式之間的 hello 距離。</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>傳回指示 hello 第一個 GeoJSON 物件 （點、 多邊形或 LineString） 是否在 hello 第二個 GeoJSON 物件 （點、 多邊形或 LineString） 的布林運算式。</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>傳回指出是否要交叉 hello 兩個指定的 GeoJSON 物件 （點、 多邊形或 LineString） 的布林運算式。</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>傳回布林值，指出 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式是否有效。</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>傳回包含布林值，如果 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式的 JSON 值有效，而且如果無效，此外 hello 原因，表示為字串值。</td>
</tr>
</table>

空間函式可使用的 tooperform 鄰近查詢空間資料。 例如，以下是 hello 的可傳回所有的系列文件，30 公里內指定的位置使用 hello ST_DISTANCE 內建函式的查詢。 

**查詢**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**結果**

    [{
      "id": "WakefieldFamily"
    }]

如果您包含您的編製索引原則中空間索引，然後 「 距離查詢 」 將會服務有效率地利用 hello 索引。 如需有關空間索引的詳細資訊，請參閱以下的 hello 一節。 如果您沒有空間索引 hello 指定路徑，您仍然可以藉由指定執行空間查詢`x-ms-documentdb-query-enable-scan`hello 值與要求標頭設定太 」 為 true 」。 在.NET 中，這可藉由傳遞選擇性 hello **FeedOptions**與引數 tooqueries [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery)設定 tootrue。 

可以使用的 toocheck ST_WITHIN，如果位於多邊形的點。 通常多邊形是使用的 toorepresent 邊界，像是郵遞區號、 狀態界限或自然的資訊。 再次如果您包含您的編製索引原則中空間索引，然後 「 中 」 查詢將會服務有效率地利用 hello 索引。 

ST_WITHIN 中的多邊形引數可以包含單一環形，也就是 hello 多邊形必須不能包含在它們的漏洞。 

**查詢**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**結果**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> 在 Azure Cosmos DB 查詢中，適用於類似 toohow 不相符的類型如果 hello 位置指定值的引數格式不正確或無效，，然後它會太評估**未定義**以及評估 hello 文件 toobe 略過從 hello查詢結果。 如果您的查詢會不傳回任何結果，請執行 ST_ISVALIDDETAILED toodebug hello spatail 類型無效的原因。     
> 
> 

Azure Cosmos DB 也支援執行反向查詢，也就是您可以索引多邊形或線條在 Azure Cosmos DB 中，然後再查詢包含指定的點的 hello 區域。 此模式常用於物流 tooidentify 例如當卡車進入或離開指定的區域。 

**查詢**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**結果**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID 和 ST_ISVALIDDETAILED 可以是使用的 toocheck，如果空間物件有效。 比方說，下列查詢的 hello 檢查點與超出範圍的緯度值 (-132.8) hello 有效性。 ST_ISVALID 傳回只是布林值，並傳回 ST_ISVALIDDETAILED hello 布林值和字串，包含 hello 原因為何，它被視為無效。

** 查詢 **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**結果**

    [{
      "$1": false
    }]

這些函式也可以使用的 toovalidate 多邊形。 例如，這裡我們使用 ST_ISVALIDDETAILED toovalidate 未關閉的多邊形。 

**查詢**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**結果**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>Hello.NET SDK 中的 LINQ 查詢
hello DocumentDB.NET SDK 提供者也虛設常式方法`Distance()`和`Within()`LINQ 運算式中使用。 hello DocumentDB LINQ 提供者會轉譯這些方法呼叫 toohello 對等 SQL 內建函式呼叫 (ST_DISTANCE 和 ST_WITHIN 分別)。 

以下範例中的 LINQ 查詢，其 「 位置 」 值半徑為 30 的 hello 公里內指定的 hello Azure Cosmos DB 集合中尋找所有文件的點使用 LINQ。

**距離的 LINQ 查詢**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

同樣地，以下是尋找其 「 位置 」 是 hello 內的所有 hello 文件會都指定方塊/多邊形的查詢。 

**範圍內的 LINQ 查詢**

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


既然我們已經探討如何使用 LINQ 與 SQL tooquery 文件讓我們看看如何 tooconfigure Azure Cosmos DB 空間索引。

## <a name="indexing"></a>編製索引
如我們所述 hello[結構描述以 Azure Cosmos DB 索引無從驗證](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)紙張，我們設計 Azure Cosmos DB 的資料庫引擎 toobe 真正無從驗證結構描述，並提供 JSON 的第一個類別支援。 hello 寫入最佳化資料庫引擎的 Azure Cosmos DB 原本即了解空間資料 （點、 多邊形和線條） 代表 hello GeoJSON 標準中。

簡單地說，測量 2D 平面座標的投影則漸進式分成使用的儲存格 hello 幾何**quadtree**。 這些資料格都是根據 hello 位置 hello 資料格內的對應的 too1D**希伯特空間填滿曲線**，保留的點的位置。 此外時位置資料具有索引，它將經歷這道程序**鑲嵌式**，也就是 hello 的所有資料格相交的位置識別並儲存為 hello Azure Cosmos DB 索引中的索引鍵。 在查詢時，引數，像是點和多邊形，還有鑲嵌的 tooextract hello 相關的資料格識別碼範圍，然後使用 tooretrieve hello 索引資料。

如果您指定包含空間索引的編製索引原則 / * （所有路徑），然後找到 hello 集合內的所有點已編列都索引供有效率空間查詢 （ST_WITHIN 和 ST_DISTANCE）。 空間索引沒有整數位數值，且一律使用預設的整數位數值。

> [!NOTE]
> Azure Cosmos DB 支援自動編製 Point、Polygon 及 LineString 的索引
> 
> 

hello 下列 JSON 片段顯示編製索引的原則與啟用的空間索引，也就是索引空間查詢文件中找到任何 GeoJSON 點。 如果您要修改 hello 編製索引原則使用 hello Azure 入口網站，您可以指定下列 JSON 原則 tooenable 空間在集合中索引編製索引的 hello。

**已針對點和多邊形啟用空間的集合索引編製原則 JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

以下是程式碼片段顯示如何 toocreate 具有空間索引的集合針對開啟包含點的所有路徑的.NET 中。 

**建立含空間索引編制的集合**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

以下是如何修改儲存在文件內的任何點上的空間索引的現有集合 tootake 優點。

**修改含空間索引編制的現有集合**

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> 如果 hello 位置 GeoJSON hello 文件中的值是格式不正確或不正確，然後它會取得建立索引，空間查詢。 您可以使用 ST_ISVALID 和 ST_ISVALIDDETAILED 驗證位置值。
> 
> 如果您的集合定義包含分割索引鍵，不會報告索引轉換進度。 
> 
> 

## <a name="next-steps"></a>後續步驟
既然您已經學會有關如何 tooget 入門 geospatial 支援 Azure Cosmos DB 中，您可以：

* 開始撰寫程式碼以 hello [GitHub 上的地理空間.NET 程式碼範例](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* 取得指針與地理空間查詢在 hello [Azure Cosmos DB 查詢遊樂場](http://www.documentdb.com/sql/demo#geospatial)
* 深入了解 [Azure Cosmos DB 查詢](documentdb-sql-query.md)
* 深入了解 [Azure Cosmos DB 編製索引原則](indexing-policies.md)

