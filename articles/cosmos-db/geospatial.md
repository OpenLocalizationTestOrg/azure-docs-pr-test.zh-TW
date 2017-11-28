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
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="faad1-103">使用 Azure Cosmos DB 中的地理空間和 GeoJSON 位置資料</span><span class="sxs-lookup"><span data-stu-id="faad1-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="faad1-104">這篇文章是簡介 toohello geospatial 中的功能[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="faad1-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="faad1-105">閱讀此文章之後, 將無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="faad1-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="faad1-106">如何在 Azure Cosmos DB 中儲存空間資料？</span><span class="sxs-lookup"><span data-stu-id="faad1-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="faad1-107">如何以 SQL 和 LINQ 查詢 Azure Cosmos DB 中的地理空間資料？</span><span class="sxs-lookup"><span data-stu-id="faad1-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="faad1-108">如何在 Azure Cosmos DB 中啟用或停用空間編製索引？</span><span class="sxs-lookup"><span data-stu-id="faad1-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="faad1-109">本文示範如何使用空間資料與 toowork hello DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="faad1-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="faad1-110">請參閱此 [GitHub 專案](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs)中的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="faad1-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="faad1-111">簡介 toospatial 資料</span><span class="sxs-lookup"><span data-stu-id="faad1-111">Introduction toospatial data</span></span>
<span data-ttu-id="faad1-112">空間資料會描述 hello 位置與形狀的空間中的物件。</span><span class="sxs-lookup"><span data-stu-id="faad1-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="faad1-113">在大部分的應用程式，這些對應 tooobjects hello 地球，也就是地理空間資料上。</span><span class="sxs-lookup"><span data-stu-id="faad1-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="faad1-114">空間資料可以是個人使用的 toorepresent hello 位置、 感興趣的位置或 hello 界限的縣 （市） 或湖泊。</span><span class="sxs-lookup"><span data-stu-id="faad1-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="faad1-115">常見使用案例通常涉及鄰近性查詢，例如「尋找我目前位置附近的所有咖啡廳」。</span><span class="sxs-lookup"><span data-stu-id="faad1-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="faad1-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="faad1-116">GeoJSON</span></span>
<span data-ttu-id="faad1-117">Azure Cosmos DB 支援索引和查詢表示使用 hello geospatial 點資料[GeoJSON 規格](https://tools.ietf.org/html/rfc7946)。</span><span class="sxs-lookup"><span data-stu-id="faad1-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="faad1-118">GeoJSON 資料結構一律為有效的 JSON 物件，因此可透過 Azure Cosmos DB 來儲存及查詢，無須使用任何特殊的工具或程式庫。</span><span class="sxs-lookup"><span data-stu-id="faad1-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="faad1-119">hello Azure Cosmos DB Sdk 提供 helper 類別和方法，可讓您輕鬆 toowork 空間資料。</span><span class="sxs-lookup"><span data-stu-id="faad1-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="faad1-120">點、LineString 和多邊形</span><span class="sxs-lookup"><span data-stu-id="faad1-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="faad1-121">**點** 代表空間中的單一位置。</span><span class="sxs-lookup"><span data-stu-id="faad1-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="faad1-122">在地理空間資料點會代表 hello 確切位置，可能是雜貨店、 kiosk、 汽車或某個城市的街道地址。</span><span class="sxs-lookup"><span data-stu-id="faad1-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="faad1-123">點會使用其座標組或經緯度，以 GeoJSON (和 Azure Cosmos DB) 來表示。</span><span class="sxs-lookup"><span data-stu-id="faad1-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="faad1-124">以下是點的 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="faad1-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="faad1-125">**Azure Cosmos DB 中的點**</span><span class="sxs-lookup"><span data-stu-id="faad1-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="faad1-126">hello GeoJSON 規格指定經度第一個和緯度第二個。</span><span class="sxs-lookup"><span data-stu-id="faad1-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="faad1-127">如同其他的地圖應用程式，經度和緯度為角度，並以度為表示單位。</span><span class="sxs-lookup"><span data-stu-id="faad1-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="faad1-128">經度值會從 hello 子午線衡量，並介於-180 和 180.0 度和緯度值從 hello 赤道衡量，並介於-90.0 和 90.0 度。</span><span class="sxs-lookup"><span data-stu-id="faad1-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="faad1-129">Azure Cosmos DB 解譯座標表示每個 hello WGS 84 參考系統。</span><span class="sxs-lookup"><span data-stu-id="faad1-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="faad1-130">請參閱下方詳細的座標參考系統資料。</span><span class="sxs-lookup"><span data-stu-id="faad1-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="faad1-131">如這個包含位置資料的使用者設定檔範例所示，這可內嵌於 Azure Cosmos DB 文件中：</span><span class="sxs-lookup"><span data-stu-id="faad1-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="faad1-132">**儲存在 Azure Cosmos DB 中含有位置的使用設定檔**</span><span class="sxs-lookup"><span data-stu-id="faad1-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="faad1-133">此外 toopoints，GeoJSON 也支援 LineStrings 和多邊形。</span><span class="sxs-lookup"><span data-stu-id="faad1-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="faad1-134">**LineStrings**代表一系列的空間中的兩個或多個點且 hello 將它們連接的直線線段。</span><span class="sxs-lookup"><span data-stu-id="faad1-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="faad1-135">在地理空間資料 LineStrings 是常用的 toorepresent 高速公路或河。</span><span class="sxs-lookup"><span data-stu-id="faad1-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="faad1-136">**多邊形**是由連接的點組成邊界，並形成封閉的 LineString。</span><span class="sxs-lookup"><span data-stu-id="faad1-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="faad1-137">多邊形會像湖泊常用的 toorepresent 自然格式或政治轄區像城市與州。</span><span class="sxs-lookup"><span data-stu-id="faad1-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="faad1-138">以下是 Azure Cosmos DB 中多邊形的範例。</span><span class="sxs-lookup"><span data-stu-id="faad1-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="faad1-139">**GeoJSON 中的多邊形**</span><span class="sxs-lookup"><span data-stu-id="faad1-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="faad1-140">hello GeoJSON 規格要求有效的多邊形的 hello 所提供的最後一個座標組應可讓相同 hello 為 hello 第一次，toocreate 封閉圖形。</span><span class="sxs-lookup"><span data-stu-id="faad1-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="faad1-141">多邊形內的點必須以逆時針順序指定。</span><span class="sxs-lookup"><span data-stu-id="faad1-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="faad1-142">順時針旋轉的順序指定的多邊形代表 hello 反 hello 區域內。</span><span class="sxs-lookup"><span data-stu-id="faad1-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="faad1-143">在加法 tooPoint，LineString 和多邊形，GeoJSON 也會指定如何 hello 表示 toogroup 多個地理空間位置，以及如何 tooassociate 任意數目的屬性與地理位置**功能**。</span><span class="sxs-lookup"><span data-stu-id="faad1-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="faad1-144">由於這些物件都是有效的 JSON，因此均可在 Azure Cosmos DB 中儲存及處理。</span><span class="sxs-lookup"><span data-stu-id="faad1-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="faad1-145">不過，Azure Cosmos DB 僅支援自動編製點的索引。</span><span class="sxs-lookup"><span data-stu-id="faad1-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="faad1-146">座標參考系統</span><span class="sxs-lookup"><span data-stu-id="faad1-146">Coordinate reference systems</span></span>
<span data-ttu-id="faad1-147">Hello 地球的 hello 圖形是異常，因為地理空間資料的座標被以許多的座標參考系統 (CR)，每個都有自己的畫面格的參考和度量單位。</span><span class="sxs-lookup"><span data-stu-id="faad1-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="faad1-148">比方說，「 國家 （地區） 方格的英國"hello 是 「 參照系統是非常精確 hello 英國，但超出它。</span><span class="sxs-lookup"><span data-stu-id="faad1-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="faad1-149">hello 最受歡迎使用 CR 今天為 hello World Geodetic System [WGS 84](http://earth-info.nga.mil/GandG/wgs84/)。</span><span class="sxs-lookup"><span data-stu-id="faad1-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="faad1-150">GPS 裝置和許多地圖服務，包括 Google 地圖與 Bing Maps API 均是使用 WGS-84。</span><span class="sxs-lookup"><span data-stu-id="faad1-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="faad1-151">Azure Cosmos DB 支援索引和查詢使用 hello 只 WGS 84 CRS 地理空間資料。</span><span class="sxs-lookup"><span data-stu-id="faad1-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="faad1-152">建立具有空間資料的文件</span><span class="sxs-lookup"><span data-stu-id="faad1-152">Creating documents with spatial data</span></span>
<span data-ttu-id="faad1-153">當您建立包含 GeoJSON 值的文件時，它們會自動索引中的 hello 集合素來 toohello 編製索引原則的空間索引。</span><span class="sxs-lookup"><span data-stu-id="faad1-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="faad1-154">如果您是以動態類型的語言 (如 Python 或 Node.js) 使用 Azure Cosmos DB SDK，則必須建立有效的 GeoJSON。</span><span class="sxs-lookup"><span data-stu-id="faad1-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="faad1-155">**以 Node.js 建立具有地理空間資料的文件**</span><span class="sxs-lookup"><span data-stu-id="faad1-155">**Create Document with Geospatial data in Node.js**</span></span>

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

<span data-ttu-id="faad1-156">如果您正在使用 hello DocumentDB Api，您可以使用 hello`Point`和`Polygon`內 hello 類別`Microsoft.Azure.Documents.Spatial`應用程式物件內的命名空間 tooembed 位置資訊。</span><span class="sxs-lookup"><span data-stu-id="faad1-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="faad1-157">這些類別有助於簡化 hello 序列化和還原序列化成 GeoJSON 空間資料。</span><span class="sxs-lookup"><span data-stu-id="faad1-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="faad1-158">**以 .NET 建立具有地理空間資料的文件**</span><span class="sxs-lookup"><span data-stu-id="faad1-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="faad1-159">如果您沒有 hello 緯度和經度資訊，但有 hello 實體位址或位置的名稱，例如縣市或國家/地區，您可以使用這類 Bing 地圖服務 REST 服務的地理編碼服務查閱 hello 實際座標。</span><span class="sxs-lookup"><span data-stu-id="faad1-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="faad1-160">在 [這裡](https://msdn.microsoft.com/library/ff701713.aspx)深入了解 Bing Maps 地理編碼。</span><span class="sxs-lookup"><span data-stu-id="faad1-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="faad1-161">查詢空間類型</span><span class="sxs-lookup"><span data-stu-id="faad1-161">Querying spatial types</span></span>
<span data-ttu-id="faad1-162">既然我們已經看看如何 tooinsert 地理空間資料，讓我們看看如何 tooquery 使用 Azure Cosmos DB SQL 和 LINQ 使用此資料。</span><span class="sxs-lookup"><span data-stu-id="faad1-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="faad1-163">空間 SQL 內建函數</span><span class="sxs-lookup"><span data-stu-id="faad1-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="faad1-164">Azure Cosmos DB 支援 hello 下列開放式地理空間協會 (OGC) 的地理空間查詢內建函式。</span><span class="sxs-lookup"><span data-stu-id="faad1-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="faad1-165">如需有關 hello 整組 hello SQL 語言中的內建函式的詳細資訊，請參閱太[查詢 Azure Cosmos DB](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="faad1-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="faad1-166"><strong>用法</strong></span><span class="sxs-lookup"><span data-stu-id="faad1-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="faad1-167"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="faad1-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="faad1-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="faad1-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="faad1-169">傳回兩個 hello GeoJSON 點、 多邊形或 LineString 運算式之間的 hello 距離。</span><span class="sxs-lookup"><span data-stu-id="faad1-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="faad1-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="faad1-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="faad1-171">傳回指示 hello 第一個 GeoJSON 物件 （點、 多邊形或 LineString） 是否在 hello 第二個 GeoJSON 物件 （點、 多邊形或 LineString） 的布林運算式。</span><span class="sxs-lookup"><span data-stu-id="faad1-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="faad1-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="faad1-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="faad1-173">傳回指出是否要交叉 hello 兩個指定的 GeoJSON 物件 （點、 多邊形或 LineString） 的布林運算式。</span><span class="sxs-lookup"><span data-stu-id="faad1-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="faad1-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="faad1-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="faad1-175">傳回布林值，指出 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式是否有效。</span><span class="sxs-lookup"><span data-stu-id="faad1-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="faad1-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="faad1-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="faad1-177">傳回包含布林值，如果 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式的 JSON 值有效，而且如果無效，此外 hello 原因，表示為字串值。</span><span class="sxs-lookup"><span data-stu-id="faad1-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="faad1-178">空間函式可使用的 tooperform 鄰近查詢空間資料。</span><span class="sxs-lookup"><span data-stu-id="faad1-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="faad1-179">例如，以下是 hello 的可傳回所有的系列文件，30 公里內指定的位置使用 hello ST_DISTANCE 內建函式的查詢。</span><span class="sxs-lookup"><span data-stu-id="faad1-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="faad1-180">**查詢**</span><span class="sxs-lookup"><span data-stu-id="faad1-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="faad1-181">**結果**</span><span class="sxs-lookup"><span data-stu-id="faad1-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="faad1-182">如果您包含您的編製索引原則中空間索引，然後 「 距離查詢 」 將會服務有效率地利用 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="faad1-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="faad1-183">如需有關空間索引的詳細資訊，請參閱以下的 hello 一節。</span><span class="sxs-lookup"><span data-stu-id="faad1-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="faad1-184">如果您沒有空間索引 hello 指定路徑，您仍然可以藉由指定執行空間查詢`x-ms-documentdb-query-enable-scan`hello 值與要求標頭設定太 」 為 true 」。</span><span class="sxs-lookup"><span data-stu-id="faad1-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="faad1-185">在.NET 中，這可藉由傳遞選擇性 hello **FeedOptions**與引數 tooqueries [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery)設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="faad1-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="faad1-186">可以使用的 toocheck ST_WITHIN，如果位於多邊形的點。</span><span class="sxs-lookup"><span data-stu-id="faad1-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="faad1-187">通常多邊形是使用的 toorepresent 邊界，像是郵遞區號、 狀態界限或自然的資訊。</span><span class="sxs-lookup"><span data-stu-id="faad1-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="faad1-188">再次如果您包含您的編製索引原則中空間索引，然後 「 中 」 查詢將會服務有效率地利用 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="faad1-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="faad1-189">ST_WITHIN 中的多邊形引數可以包含單一環形，也就是 hello 多邊形必須不能包含在它們的漏洞。</span><span class="sxs-lookup"><span data-stu-id="faad1-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="faad1-190">**查詢**</span><span class="sxs-lookup"><span data-stu-id="faad1-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="faad1-191">**結果**</span><span class="sxs-lookup"><span data-stu-id="faad1-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="faad1-192">在 Azure Cosmos DB 查詢中，適用於類似 toohow 不相符的類型如果 hello 位置指定值的引數格式不正確或無效，，然後它會太評估**未定義**以及評估 hello 文件 toobe 略過從 hello查詢結果。</span><span class="sxs-lookup"><span data-stu-id="faad1-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="faad1-193">如果您的查詢會不傳回任何結果，請執行 ST_ISVALIDDETAILED toodebug hello spatail 類型無效的原因。</span><span class="sxs-lookup"><span data-stu-id="faad1-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="faad1-194">Azure Cosmos DB 也支援執行反向查詢，也就是您可以索引多邊形或線條在 Azure Cosmos DB 中，然後再查詢包含指定的點的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="faad1-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="faad1-195">此模式常用於物流 tooidentify 例如當卡車進入或離開指定的區域。</span><span class="sxs-lookup"><span data-stu-id="faad1-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="faad1-196">**查詢**</span><span class="sxs-lookup"><span data-stu-id="faad1-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="faad1-197">**結果**</span><span class="sxs-lookup"><span data-stu-id="faad1-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="faad1-198">ST_ISVALID 和 ST_ISVALIDDETAILED 可以是使用的 toocheck，如果空間物件有效。</span><span class="sxs-lookup"><span data-stu-id="faad1-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="faad1-199">比方說，下列查詢的 hello 檢查點與超出範圍的緯度值 (-132.8) hello 有效性。</span><span class="sxs-lookup"><span data-stu-id="faad1-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="faad1-200">ST_ISVALID 傳回只是布林值，並傳回 ST_ISVALIDDETAILED hello 布林值和字串，包含 hello 原因為何，它被視為無效。</span><span class="sxs-lookup"><span data-stu-id="faad1-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="faad1-201">** 查詢 **</span><span class="sxs-lookup"><span data-stu-id="faad1-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="faad1-202">**結果**</span><span class="sxs-lookup"><span data-stu-id="faad1-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="faad1-203">這些函式也可以使用的 toovalidate 多邊形。</span><span class="sxs-lookup"><span data-stu-id="faad1-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="faad1-204">例如，這裡我們使用 ST_ISVALIDDETAILED toovalidate 未關閉的多邊形。</span><span class="sxs-lookup"><span data-stu-id="faad1-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="faad1-205">**查詢**</span><span class="sxs-lookup"><span data-stu-id="faad1-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="faad1-206">**結果**</span><span class="sxs-lookup"><span data-stu-id="faad1-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="faad1-207">Hello.NET SDK 中的 LINQ 查詢</span><span class="sxs-lookup"><span data-stu-id="faad1-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="faad1-208">hello DocumentDB.NET SDK 提供者也虛設常式方法`Distance()`和`Within()`LINQ 運算式中使用。</span><span class="sxs-lookup"><span data-stu-id="faad1-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="faad1-209">hello DocumentDB LINQ 提供者會轉譯這些方法呼叫 toohello 對等 SQL 內建函式呼叫 (ST_DISTANCE 和 ST_WITHIN 分別)。</span><span class="sxs-lookup"><span data-stu-id="faad1-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="faad1-210">以下範例中的 LINQ 查詢，其 「 位置 」 值半徑為 30 的 hello 公里內指定的 hello Azure Cosmos DB 集合中尋找所有文件的點使用 LINQ。</span><span class="sxs-lookup"><span data-stu-id="faad1-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="faad1-211">**距離的 LINQ 查詢**</span><span class="sxs-lookup"><span data-stu-id="faad1-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="faad1-212">同樣地，以下是尋找其 「 位置 」 是 hello 內的所有 hello 文件會都指定方塊/多邊形的查詢。</span><span class="sxs-lookup"><span data-stu-id="faad1-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="faad1-213">**範圍內的 LINQ 查詢**</span><span class="sxs-lookup"><span data-stu-id="faad1-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="faad1-214">既然我們已經探討如何使用 LINQ 與 SQL tooquery 文件讓我們看看如何 tooconfigure Azure Cosmos DB 空間索引。</span><span class="sxs-lookup"><span data-stu-id="faad1-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="faad1-215">編製索引</span><span class="sxs-lookup"><span data-stu-id="faad1-215">Indexing</span></span>
<span data-ttu-id="faad1-216">如我們所述 hello[結構描述以 Azure Cosmos DB 索引無從驗證](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)紙張，我們設計 Azure Cosmos DB 的資料庫引擎 toobe 真正無從驗證結構描述，並提供 JSON 的第一個類別支援。</span><span class="sxs-lookup"><span data-stu-id="faad1-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="faad1-217">hello 寫入最佳化資料庫引擎的 Azure Cosmos DB 原本即了解空間資料 （點、 多邊形和線條） 代表 hello GeoJSON 標準中。</span><span class="sxs-lookup"><span data-stu-id="faad1-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="faad1-218">簡單地說，測量 2D 平面座標的投影則漸進式分成使用的儲存格 hello 幾何**quadtree**。</span><span class="sxs-lookup"><span data-stu-id="faad1-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="faad1-219">這些資料格都是根據 hello 位置 hello 資料格內的對應的 too1D**希伯特空間填滿曲線**，保留的點的位置。</span><span class="sxs-lookup"><span data-stu-id="faad1-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="faad1-220">此外時位置資料具有索引，它將經歷這道程序**鑲嵌式**，也就是 hello 的所有資料格相交的位置識別並儲存為 hello Azure Cosmos DB 索引中的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="faad1-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="faad1-221">在查詢時，引數，像是點和多邊形，還有鑲嵌的 tooextract hello 相關的資料格識別碼範圍，然後使用 tooretrieve hello 索引資料。</span><span class="sxs-lookup"><span data-stu-id="faad1-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="faad1-222">如果您指定包含空間索引的編製索引原則 / * （所有路徑），然後找到 hello 集合內的所有點已編列都索引供有效率空間查詢 （ST_WITHIN 和 ST_DISTANCE）。</span><span class="sxs-lookup"><span data-stu-id="faad1-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="faad1-223">空間索引沒有整數位數值，且一律使用預設的整數位數值。</span><span class="sxs-lookup"><span data-stu-id="faad1-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="faad1-224">Azure Cosmos DB 支援自動編製 Point、Polygon 及 LineString 的索引</span><span class="sxs-lookup"><span data-stu-id="faad1-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="faad1-225">hello 下列 JSON 片段顯示編製索引的原則與啟用的空間索引，也就是索引空間查詢文件中找到任何 GeoJSON 點。</span><span class="sxs-lookup"><span data-stu-id="faad1-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="faad1-226">如果您要修改 hello 編製索引原則使用 hello Azure 入口網站，您可以指定下列 JSON 原則 tooenable 空間在集合中索引編製索引的 hello。</span><span class="sxs-lookup"><span data-stu-id="faad1-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="faad1-227">**已針對點和多邊形啟用空間的集合索引編製原則 JSON**</span><span class="sxs-lookup"><span data-stu-id="faad1-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="faad1-228">以下是程式碼片段顯示如何 toocreate 具有空間索引的集合針對開啟包含點的所有路徑的.NET 中。</span><span class="sxs-lookup"><span data-stu-id="faad1-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="faad1-229">**建立含空間索引編制的集合**</span><span class="sxs-lookup"><span data-stu-id="faad1-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="faad1-230">以下是如何修改儲存在文件內的任何點上的空間索引的現有集合 tootake 優點。</span><span class="sxs-lookup"><span data-stu-id="faad1-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="faad1-231">**修改含空間索引編制的現有集合**</span><span class="sxs-lookup"><span data-stu-id="faad1-231">**Modify an existing collection with spatial indexing**</span></span>

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
> <span data-ttu-id="faad1-232">如果 hello 位置 GeoJSON hello 文件中的值是格式不正確或不正確，然後它會取得建立索引，空間查詢。</span><span class="sxs-lookup"><span data-stu-id="faad1-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="faad1-233">您可以使用 ST_ISVALID 和 ST_ISVALIDDETAILED 驗證位置值。</span><span class="sxs-lookup"><span data-stu-id="faad1-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="faad1-234">如果您的集合定義包含分割索引鍵，不會報告索引轉換進度。</span><span class="sxs-lookup"><span data-stu-id="faad1-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="faad1-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="faad1-235">Next steps</span></span>
<span data-ttu-id="faad1-236">既然您已經學會有關如何 tooget 入門 geospatial 支援 Azure Cosmos DB 中，您可以：</span><span class="sxs-lookup"><span data-stu-id="faad1-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="faad1-237">開始撰寫程式碼以 hello [GitHub 上的地理空間.NET 程式碼範例](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="faad1-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="faad1-238">取得指針與地理空間查詢在 hello [Azure Cosmos DB 查詢遊樂場](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="faad1-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="faad1-239">深入了解 [Azure Cosmos DB 查詢](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="faad1-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="faad1-240">深入了解 [Azure Cosmos DB 編製索引原則](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="faad1-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

