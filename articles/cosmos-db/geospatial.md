---
title: "使用 Azure Cosmos DB 中的地理空間資料 | Microsoft Docs"
description: "了解如何使用 Azure Cosmos DB 和 DocumentDB API 建立與查詢空間物件，以及為其編製索引。"
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
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="c4cde-103">使用 Azure Cosmos DB 中的地理空間和 GeoJSON 位置資料</span><span class="sxs-lookup"><span data-stu-id="c4cde-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="c4cde-104">本文將介紹 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 中的地理空間功能。</span><span class="sxs-lookup"><span data-stu-id="c4cde-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="c4cde-105">閱讀本文後，您將能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="c4cde-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="c4cde-106">如何在 Azure Cosmos DB 中儲存空間資料？</span><span class="sxs-lookup"><span data-stu-id="c4cde-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="c4cde-107">如何以 SQL 和 LINQ 查詢 Azure Cosmos DB 中的地理空間資料？</span><span class="sxs-lookup"><span data-stu-id="c4cde-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="c4cde-108">如何在 Azure Cosmos DB 中啟用或停用空間編製索引？</span><span class="sxs-lookup"><span data-stu-id="c4cde-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="c4cde-109">本文示範如何透過 DocumentDB API 使用空間資料。</span><span class="sxs-lookup"><span data-stu-id="c4cde-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="c4cde-110">請參閱此 [GitHub 專案](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs)中的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="c4cde-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="c4cde-111">空間資料簡介</span><span class="sxs-lookup"><span data-stu-id="c4cde-111">Introduction to spatial data</span></span>
<span data-ttu-id="c4cde-112">空間資料可描述空間中物件的位置和形狀。</span><span class="sxs-lookup"><span data-stu-id="c4cde-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="c4cde-113">在大部分的應用程式中，這些會對應至地球上的物件，也就是地理空間資料。</span><span class="sxs-lookup"><span data-stu-id="c4cde-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="c4cde-114">空間資料可以用來代表人、感興趣的地方、城市邊界或湖泊。</span><span class="sxs-lookup"><span data-stu-id="c4cde-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="c4cde-115">常見使用案例通常涉及鄰近性查詢，例如「尋找我目前位置附近的所有咖啡廳」。</span><span class="sxs-lookup"><span data-stu-id="c4cde-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="c4cde-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="c4cde-116">GeoJSON</span></span>
<span data-ttu-id="c4cde-117">Azure Cosmos DB 支援對使用 [GeoJSON 規格 (英文)](https://tools.ietf.org/html/rfc7946) 表示的地理空間點資料執行編製索引和查詢。</span><span class="sxs-lookup"><span data-stu-id="c4cde-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="c4cde-118">GeoJSON 資料結構一律為有效的 JSON 物件，因此可透過 Azure Cosmos DB 來儲存及查詢，無須使用任何特殊的工具或程式庫。</span><span class="sxs-lookup"><span data-stu-id="c4cde-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="c4cde-119">Azure Cosmos DB SDK 提供協助程式類別和方法，以便更容易使用空間資料。</span><span class="sxs-lookup"><span data-stu-id="c4cde-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="c4cde-120">點、LineString 和多邊形</span><span class="sxs-lookup"><span data-stu-id="c4cde-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="c4cde-121">**點** 代表空間中的單一位置。</span><span class="sxs-lookup"><span data-stu-id="c4cde-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="c4cde-122">在地理空間資料中，某個點所代表的確切位置可能是雜貨店的街道地址、電話亭、汽車或城市。</span><span class="sxs-lookup"><span data-stu-id="c4cde-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="c4cde-123">點會使用其座標組或經緯度，以 GeoJSON (和 Azure Cosmos DB) 來表示。</span><span class="sxs-lookup"><span data-stu-id="c4cde-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="c4cde-124">以下是點的 JSON 範例。</span><span class="sxs-lookup"><span data-stu-id="c4cde-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="c4cde-125">**Azure Cosmos DB 中的點**</span><span class="sxs-lookup"><span data-stu-id="c4cde-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="c4cde-126">GeoJSON 規格會先指定經度，然後再指定緯度。</span><span class="sxs-lookup"><span data-stu-id="c4cde-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="c4cde-127">如同其他的地圖應用程式，經度和緯度為角度，並以度為表示單位。</span><span class="sxs-lookup"><span data-stu-id="c4cde-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="c4cde-128">經度值是從本初子午線測量，並介於 -180 和 180.0 度之間；緯度值是從赤道測量，並介於 -90.0 和 90.0 度之間。</span><span class="sxs-lookup"><span data-stu-id="c4cde-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="c4cde-129">Azure Cosmos DB 會依照 WGS-84 參考系統所表示的方式來解譯座標。</span><span class="sxs-lookup"><span data-stu-id="c4cde-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="c4cde-130">請參閱下方詳細的座標參考系統資料。</span><span class="sxs-lookup"><span data-stu-id="c4cde-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="c4cde-131">如這個包含位置資料的使用者設定檔範例所示，這可內嵌於 Azure Cosmos DB 文件中：</span><span class="sxs-lookup"><span data-stu-id="c4cde-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="c4cde-132">**儲存在 Azure Cosmos DB 中含有位置的使用設定檔**</span><span class="sxs-lookup"><span data-stu-id="c4cde-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="c4cde-133">除了點之外，GeoJSON 也支援 Linestring 和多邊形。</span><span class="sxs-lookup"><span data-stu-id="c4cde-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="c4cde-134">**Linestring** 表示空間中一連串的點 (兩個以上)，以及連接這些點的線段。</span><span class="sxs-lookup"><span data-stu-id="c4cde-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="c4cde-135">在地理空間資料中，LineStrings 通常用來代表高速公路或河流。</span><span class="sxs-lookup"><span data-stu-id="c4cde-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="c4cde-136">**多邊形**是由連接的點組成邊界，並形成封閉的 LineString。</span><span class="sxs-lookup"><span data-stu-id="c4cde-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="c4cde-137">多邊形常用來代表自然構成物，例如湖泊，或代表政治管轄權，例如城市和州省。</span><span class="sxs-lookup"><span data-stu-id="c4cde-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="c4cde-138">以下是 Azure Cosmos DB 中多邊形的範例。</span><span class="sxs-lookup"><span data-stu-id="c4cde-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="c4cde-139">**GeoJSON 中的多邊形**</span><span class="sxs-lookup"><span data-stu-id="c4cde-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="c4cde-140">GeoJSON 規格需要此資料才能形成有效的多邊形；若要建立一個封閉的形狀，最後一個座標組應該與第一個座標組相同。</span><span class="sxs-lookup"><span data-stu-id="c4cde-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="c4cde-141">多邊形內的點必須以逆時針順序指定。</span><span class="sxs-lookup"><span data-stu-id="c4cde-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="c4cde-142">以順時針順序指定的多邊形，代表區域內的反轉。</span><span class="sxs-lookup"><span data-stu-id="c4cde-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="c4cde-143">除了點、LineString 和多邊形之外，GeoJSON 也會指定如何將多個地理空間位置的表示加以分組，以及如何將任意屬性與地理位置產生關聯成為 **特徵**的表示。</span><span class="sxs-lookup"><span data-stu-id="c4cde-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="c4cde-144">由於這些物件都是有效的 JSON，因此均可在 Azure Cosmos DB 中儲存及處理。</span><span class="sxs-lookup"><span data-stu-id="c4cde-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="c4cde-145">不過，Azure Cosmos DB 僅支援自動編製點的索引。</span><span class="sxs-lookup"><span data-stu-id="c4cde-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="c4cde-146">座標參考系統</span><span class="sxs-lookup"><span data-stu-id="c4cde-146">Coordinate reference systems</span></span>
<span data-ttu-id="c4cde-147">由於地球的形狀並不規則，地理空間資料的座標可以許多座標參考系統 (CRS) 來表示，而這些系統各有自己的參考框架和測量單位。</span><span class="sxs-lookup"><span data-stu-id="c4cde-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="c4cde-148">例如「英國國家格網參考系統」對英國而言是非常精確的參考系統，但對其他地區則不是。</span><span class="sxs-lookup"><span data-stu-id="c4cde-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="c4cde-149">現今最常使用的 CRS 是「全球大地座標系統」[WGS-84](http://earth-info.nga.mil/GandG/wgs84/)。</span><span class="sxs-lookup"><span data-stu-id="c4cde-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="c4cde-150">GPS 裝置和許多地圖服務，包括 Google 地圖與 Bing Maps API 均是使用 WGS-84。</span><span class="sxs-lookup"><span data-stu-id="c4cde-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="c4cde-151">Azure Cosmos DB 僅支援對使用 WGS-84 CRS 的地理空間資料執行編製索引和查詢。</span><span class="sxs-lookup"><span data-stu-id="c4cde-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="c4cde-152">建立具有空間資料的文件</span><span class="sxs-lookup"><span data-stu-id="c4cde-152">Creating documents with spatial data</span></span>
<span data-ttu-id="c4cde-153">當您建立包含 GeoJSON 值的文件時，值會根據集合的索引編製原則，自動以空間索引進行索引編製。</span><span class="sxs-lookup"><span data-stu-id="c4cde-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="c4cde-154">如果您是以動態類型的語言 (如 Python 或 Node.js) 使用 Azure Cosmos DB SDK，則必須建立有效的 GeoJSON。</span><span class="sxs-lookup"><span data-stu-id="c4cde-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="c4cde-155">**以 Node.js 建立具有地理空間資料的文件**</span><span class="sxs-lookup"><span data-stu-id="c4cde-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="c4cde-156">如果您使用 DocumentDB API，則可在 `Microsoft.Azure.Documents.Spatial` 命名空間中使用 `Point` 及 `Polygon` 類別，藉此將位置資訊內嵌在應用程式物件中。</span><span class="sxs-lookup"><span data-stu-id="c4cde-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="c4cde-157">這些類別可協助將空間資料序列化和還原序列化簡化成 GeoJSON。</span><span class="sxs-lookup"><span data-stu-id="c4cde-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="c4cde-158">**以 .NET 建立具有地理空間資料的文件**</span><span class="sxs-lookup"><span data-stu-id="c4cde-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="c4cde-159">如果您沒有經緯度資訊，但有實體地址或位置名稱，如城市或國家/地區，您可以使用像是 Bing Maps REST 服務之類的地理編碼服務，來查閱實際的座標。</span><span class="sxs-lookup"><span data-stu-id="c4cde-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="c4cde-160">在 [這裡](https://msdn.microsoft.com/library/ff701713.aspx)深入了解 Bing Maps 地理編碼。</span><span class="sxs-lookup"><span data-stu-id="c4cde-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="c4cde-161">查詢空間類型</span><span class="sxs-lookup"><span data-stu-id="c4cde-161">Querying spatial types</span></span>
<span data-ttu-id="c4cde-162">既然我們已經探討過如何插入地理空間資料，現在就來看看如何透過 SQL 和 LINQ 使用 Azure Cosmos DB 查詢此資料。</span><span class="sxs-lookup"><span data-stu-id="c4cde-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="c4cde-163">空間 SQL 內建函數</span><span class="sxs-lookup"><span data-stu-id="c4cde-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="c4cde-164">Azure Cosmos DB 支援下列開放地理空間協會 (OGC) 內建的地理空間查詢函式。</span><span class="sxs-lookup"><span data-stu-id="c4cde-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="c4cde-165">如需更多完整的 SQL 語言內建函式，請參閱[查詢 Azure Cosmos DB](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="c4cde-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="c4cde-166"><strong>用法</strong></span><span class="sxs-lookup"><span data-stu-id="c4cde-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="c4cde-167"><strong>說明</strong></span><span class="sxs-lookup"><span data-stu-id="c4cde-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c4cde-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="c4cde-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="c4cde-169">傳回兩個 GeoJSON Point、Polygon 或 LineString 運算式之間的距離。</span><span class="sxs-lookup"><span data-stu-id="c4cde-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c4cde-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="c4cde-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="c4cde-171">傳回布林運算式，指出第一個 GeoJSON 物件 (Point、Polygon 或 LineString) 是否位在第二個 GeoJSON 物件 (Point、Polygon 或 LineString) 內。</span><span class="sxs-lookup"><span data-stu-id="c4cde-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c4cde-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="c4cde-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="c4cde-173">傳回布林運算式，指出兩個指定的 GeoJSON 物件 (Point、Polygon 或 LineString) 是否相交。</span><span class="sxs-lookup"><span data-stu-id="c4cde-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c4cde-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="c4cde-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="c4cde-175">傳回布林值，指出指定的 GeoJSON Point、Polygon 或 LineString 運算式是否有效。</span><span class="sxs-lookup"><span data-stu-id="c4cde-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="c4cde-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="c4cde-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="c4cde-177">如果指定的 GeoJSON Point、Polygon 或 LineString 運算式有效，就傳回包含布林值的 JSON 值；但如果是無效的，就會額外加上做為字串值的原因。</span><span class="sxs-lookup"><span data-stu-id="c4cde-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="c4cde-178">空間函數可以用來對空間資料執行鄰近性查詢。</span><span class="sxs-lookup"><span data-stu-id="c4cde-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="c4cde-179">例如，以下查詢使用 ST_DISTANCE 內建函數傳回所有家族文件，且這些文件在 30 公里指定位置內。</span><span class="sxs-lookup"><span data-stu-id="c4cde-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="c4cde-180">**查詢**</span><span class="sxs-lookup"><span data-stu-id="c4cde-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="c4cde-181">**結果**</span><span class="sxs-lookup"><span data-stu-id="c4cde-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="c4cde-182">如果您將空間索引編製包含在索引編製原則中，則「距離查詢」將會透過索引獲得有效利用。</span><span class="sxs-lookup"><span data-stu-id="c4cde-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="c4cde-183">如需空間索引編製的詳細資料，請參閱下面的章節。</span><span class="sxs-lookup"><span data-stu-id="c4cde-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="c4cde-184">如果您沒有指定路徑的空間索引，仍然可以透過指定 `x-ms-documentdb-query-enable-scan` 要求標頭 (且值設定為 "true") 執行空間查詢。</span><span class="sxs-lookup"><span data-stu-id="c4cde-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="c4cde-185">在.NET 中，可以傳遞選用的 **FeedOptions** 引數至查詢 (且 [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) 設定為 true)，藉此執行此作業。</span><span class="sxs-lookup"><span data-stu-id="c4cde-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="c4cde-186">ST_WITHIN 可用來檢查點是否在多邊形內。</span><span class="sxs-lookup"><span data-stu-id="c4cde-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="c4cde-187">多邊形常用來表示邊界，例如郵遞區號、州省邊界或自然構成物。</span><span class="sxs-lookup"><span data-stu-id="c4cde-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="c4cde-188">此外，如果您將空間索引編製包含在索引編製原則中，則「距離內」查詢將會透過索引獲得有效利用。</span><span class="sxs-lookup"><span data-stu-id="c4cde-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="c4cde-189">ST_WITHIN 中的多邊形引數只可以包含單一環狀，也就是 Polygon 本身不能有漏洞。</span><span class="sxs-lookup"><span data-stu-id="c4cde-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="c4cde-190">**查詢**</span><span class="sxs-lookup"><span data-stu-id="c4cde-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="c4cde-191">**結果**</span><span class="sxs-lookup"><span data-stu-id="c4cde-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="c4cde-192">與 Azure Cosmos DB 查詢中不相符類型的運作方式類似，如果任一引數中指定的位置值格式不正確或無效，則會評估為**未定義**，且會在查詢結果中略過已評估的文件。</span><span class="sxs-lookup"><span data-stu-id="c4cde-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="c4cde-193">如果您的查詢沒有傳回任何結果，請執行 ST_ISVALIDDETAILED 來偵錯，了解空間類型無效的原因。</span><span class="sxs-lookup"><span data-stu-id="c4cde-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="c4cde-194">Azure Cosmos DB 也支援反向查詢，亦即您可以在 Azure Cosmos DB 中編製多邊形或線的索引，然後查詢包含指定點的區域。</span><span class="sxs-lookup"><span data-stu-id="c4cde-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="c4cde-195">這是物流業中常用的模式，例如，可用來識別卡車何時進入或離開指定的區域。</span><span class="sxs-lookup"><span data-stu-id="c4cde-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="c4cde-196">**查詢**</span><span class="sxs-lookup"><span data-stu-id="c4cde-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="c4cde-197">**結果**</span><span class="sxs-lookup"><span data-stu-id="c4cde-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="c4cde-198">ST_ISVALID 和 ST_ISVALIDDETAILED 可用來檢查空間物件是否有效。</span><span class="sxs-lookup"><span data-stu-id="c4cde-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="c4cde-199">例如，下列查詢以超出範圍的緯度值 (-132.8)，檢查點的有效性。</span><span class="sxs-lookup"><span data-stu-id="c4cde-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="c4cde-200">ST_ISVALID 只會傳回布林值，而 ST_ISVALIDDETAILED 會傳回布林和字串，字串中包含被視為無效的原因。</span><span class="sxs-lookup"><span data-stu-id="c4cde-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="c4cde-201">** 查詢 **</span><span class="sxs-lookup"><span data-stu-id="c4cde-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="c4cde-202">**結果**</span><span class="sxs-lookup"><span data-stu-id="c4cde-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="c4cde-203">這些函數也可以用來驗證多邊形。</span><span class="sxs-lookup"><span data-stu-id="c4cde-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="c4cde-204">例如，這裡我們使用 ST_ISVALIDDETAILED 驗證未封閉的多邊形。</span><span class="sxs-lookup"><span data-stu-id="c4cde-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="c4cde-205">**查詢**</span><span class="sxs-lookup"><span data-stu-id="c4cde-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="c4cde-206">**結果**</span><span class="sxs-lookup"><span data-stu-id="c4cde-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="c4cde-207">.NET SDK 中的 LINQ 查詢</span><span class="sxs-lookup"><span data-stu-id="c4cde-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="c4cde-208">DocumentDB.NET SDK 也是虛設常式方法 `Distance()` 和 `Within()` 的提供者，供您在 LINQ 運算式中使用。</span><span class="sxs-lookup"><span data-stu-id="c4cde-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="c4cde-209">DocumentDB LINQ 提供者會將這些方法呼叫，轉譯為同等的 SQL 內建函數呼叫 (分別為 ST_DISTANCE 和 ST_WITHIN)。</span><span class="sxs-lookup"><span data-stu-id="c4cde-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="c4cde-210">以下是 LINQ 查詢的範例，該查詢會使用 LINQ 在 Azure Cosmos DB 集合中找出所有文件，而這些文件的「位置」值會在指定點的 30 公里半徑內。</span><span class="sxs-lookup"><span data-stu-id="c4cde-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="c4cde-211">**距離的 LINQ 查詢**</span><span class="sxs-lookup"><span data-stu-id="c4cde-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="c4cde-212">同樣地，以下是尋找所有文件的查詢，這些文件的「位置」均在指定的方塊/多邊形內。</span><span class="sxs-lookup"><span data-stu-id="c4cde-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="c4cde-213">**範圍內的 LINQ 查詢**</span><span class="sxs-lookup"><span data-stu-id="c4cde-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="c4cde-214">既然我們已經探討過如何使用 LINQ 和 SQL 查詢文件，現在來看一下如何針對空間編製索引設定 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="c4cde-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="c4cde-215">編製索引</span><span class="sxs-lookup"><span data-stu-id="c4cde-215">Indexing</span></span>
<span data-ttu-id="c4cde-216">如我們在[使用 Azure Cosmos DB 進行無從驗證結構描述的編製索引 (英文)](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) 文件中所述，我們設計的 Azure Cosmos DB 資料庫引擎真正是無從驗證結構描述的，並提供一流的 JSON 支援。</span><span class="sxs-lookup"><span data-stu-id="c4cde-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="c4cde-217">Azure Cosmos DB 的寫入最佳化資料庫引擎原生就能了解以 GeoJSON 標準表示的空間資料 (點、多邊形及線)。</span><span class="sxs-lookup"><span data-stu-id="c4cde-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="c4cde-218">簡單來說，大地座標的幾何會投影在 2D 平面上，然後使用 **quadtree**以漸進方式分成格子。</span><span class="sxs-lookup"><span data-stu-id="c4cde-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="c4cde-219">這些格子會根據 **希伯特空間填滿曲線**(Hilbert space filling curve) 內的格子位置對應至 1D，並保留點的位置。</span><span class="sxs-lookup"><span data-stu-id="c4cde-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="c4cde-220">此外，在為位置資料編製索引之後，會經過稱為**鑲嵌式**的處理程序，也就是會將位置上相交的所有格子識別為索引鍵並儲存在 Azure Cosmos DB 索引中。</span><span class="sxs-lookup"><span data-stu-id="c4cde-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="c4cde-221">在查詢時，點和多邊形之類的引數也會經過鑲嵌，以擷取相關的格子 ID 範圍，然後用來從索引擷取資料。</span><span class="sxs-lookup"><span data-stu-id="c4cde-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="c4cde-222">如果指定的索引編製原則包含 /* (所有路徑) 的空間索引，則表示集合中可找到的所有點均已編製索引，能進行有效率的空間查詢 (ST_WITHIN 和 ST_DISTANCE)。</span><span class="sxs-lookup"><span data-stu-id="c4cde-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="c4cde-223">空間索引沒有整數位數值，且一律使用預設的整數位數值。</span><span class="sxs-lookup"><span data-stu-id="c4cde-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="c4cde-224">Azure Cosmos DB 支援自動編製 Point、Polygon 及 LineString 的索引</span><span class="sxs-lookup"><span data-stu-id="c4cde-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="c4cde-225">以下 JSON 片段顯示已啟用空間索引的索引編製原則，也就是為文件中可找到的所有 GeoJSON 點編製索引，以用於空間查詢。</span><span class="sxs-lookup"><span data-stu-id="c4cde-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="c4cde-226">如果您要使用 Azure 入口網站修改索引編製原則，可以為索引編製原則指定以下 JSON，藉此啟用集合的空間索引編製。</span><span class="sxs-lookup"><span data-stu-id="c4cde-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="c4cde-227">**已針對點和多邊形啟用空間的集合索引編製原則 JSON**</span><span class="sxs-lookup"><span data-stu-id="c4cde-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="c4cde-228">以下是 .NET 的程式碼片段示範，供您了解如何建立集合，同時針對所有包含點的路徑啟用空間索引編製。</span><span class="sxs-lookup"><span data-stu-id="c4cde-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="c4cde-229">**建立含空間索引編制的集合**</span><span class="sxs-lookup"><span data-stu-id="c4cde-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="c4cde-230">而以下說明如何修改現有的集合，以利用儲存在文件內任何一個點上的空間索引編制。</span><span class="sxs-lookup"><span data-stu-id="c4cde-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="c4cde-231">**修改含空間索引編制的現有集合**</span><span class="sxs-lookup"><span data-stu-id="c4cde-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="c4cde-232">如果文件中的 GeoJSON 位置值格式不正確或無效，就不會為其編製索引以用於空間查詢。</span><span class="sxs-lookup"><span data-stu-id="c4cde-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="c4cde-233">您可以使用 ST_ISVALID 和 ST_ISVALIDDETAILED 驗證位置值。</span><span class="sxs-lookup"><span data-stu-id="c4cde-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="c4cde-234">如果您的集合定義包含分割索引鍵，不會報告索引轉換進度。</span><span class="sxs-lookup"><span data-stu-id="c4cde-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c4cde-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4cde-235">Next steps</span></span>
<span data-ttu-id="c4cde-236">既然您已經學會如何開始使用 Azure Cosmos DB 中的地理空間支援，您可以：</span><span class="sxs-lookup"><span data-stu-id="c4cde-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="c4cde-237">使用 [GitHub 上的地理空間 .NET 程式碼範例](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)來開始轉寫程式碼</span><span class="sxs-lookup"><span data-stu-id="c4cde-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="c4cde-238">在 [Azure Cosmos DB 查詢園地 (英文)](http://www.documentdb.com/sql/demo#geospatial) 中瞭解地理空間查詢</span><span class="sxs-lookup"><span data-stu-id="c4cde-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="c4cde-239">深入了解 [Azure Cosmos DB 查詢](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="c4cde-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="c4cde-240">深入了解 [Azure Cosmos DB 編製索引原則](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="c4cde-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

