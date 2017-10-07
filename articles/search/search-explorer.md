---
title: "aaa\"查詢索引 （入口網站的 Azure 搜尋） |Microsoft 文件 」"
description: "發出 hello Azure 入口網站的搜尋總管 中搜尋查詢。"
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>查詢 Azure 搜尋索引使用 hello Azure 入口網站中的搜尋總管
> [!div class="op_single_selector"]
> * [概觀](search-query-overview.md)
> * [入口網站](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

本文將告訴您如何 tooquery Azure 搜尋索引使用**搜尋總管**hello Azure 入口網站中。 在您的服務，您可以使用搜尋總管 toosubmit 簡單或完整 Lucene 查詢字串 tooany 現有的索引。

## <a name="open-hello-service-dashboard"></a>開啟 hello 服務儀表板
1. 按一下**所有資源**hello 跳躍列上的 hello 左方的 hello [Azure 入口網站](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)。
2. 選取您的 Azure 搜尋服務。

## <a name="select-an-index"></a>選取索引

您想要從 hello toosearch 選取 hello 索引**索引**磚。

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>開啟搜尋總管

按一下 hello 搜尋總管磚 tooslide 開啟 hello 搜尋列上的和 [結果] 窗格。

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>開始搜尋

當使用 hello 搜尋總管，您可以指定[查詢參數](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)tooformulate hello 查詢。

1. 在 [查詢字串] 中輸入查詢，然後按 [搜尋]。 

   hello 查詢字串會自動剖析成 hello 適當要求 URL toosubmit hello Azure 搜尋 REST API 針對 HTTP 要求。   
   
   您可以使用任何有效簡單或完整 Lucene 查詢語法 toocreate hello 的要求。 hello`*`字元是不依特定順序傳回所有文件的對等 tooan 空白或未指定搜尋。

2. 在**結果**，查詢結果會出現在未經處理的 JSON，以傳回相同 toohello 裝載時以程式設計方式發出要求的 HTTP 回應主體。

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>後續步驟

hello 下列資源提供其他的查詢語法資訊和範例。

 + [簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Lucene 查詢語法](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Lucene 查詢語法範例](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [OData 篩選條件運算式語法](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 