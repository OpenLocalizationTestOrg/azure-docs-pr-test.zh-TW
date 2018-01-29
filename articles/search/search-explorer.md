---
title: "查詢索引 (入口網站 - Azure 搜尋服務) | Microsoft Docs"
description: "在 Azure 入口網站的搜尋總管中發出搜尋查詢。"
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
ms.openlocfilehash: dd68d8ed073bf7b8666ddef35a2f1f84df690b4b
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-the-azure-portal"></a>在 Azure 入口網站中使用搜尋總管查詢 Azure 搜尋服務索引
> [!div class="op_single_selector"]
> * [概觀](search-query-overview.md)
> * [入口網站](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

本文說明如何在 Azure 入口網站中使用**搜尋總管**查詢 Azure 搜尋服務索引。 您可以使用搜尋總管，在您的服務中對於任何現有的索引送出簡單或完整的 Lucene 查詢字串。

## <a name="open-the-service-dashboard"></a>開啟服務儀表板
1. 按一下 [Azure 入口網站](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)左側導向列中的 [所有資源]。
2. 選取您的 Azure 搜尋服務。

## <a name="select-an-index"></a>選取索引

選取您想要從 [索引] 圖格搜尋的索引。

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>開啟搜尋總管

按一下 [搜尋總管] 圖格以滑動開啟搜尋列和結果窗格。

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>開始搜尋

使用 [搜尋總管] 時可以指定任何 [查詢參數](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)以編寫查詢。

1. 在 [查詢字串] 中輸入查詢，然後按 [搜尋]。 

   查詢字串會自動剖析為適當的要求 URL，以便對 Azure 搜尋服務 REST API 提交 HTTP 要求。   
   
   您可以使用任何有效的簡單或完整 Lucene 查詢語法來建立要求。 `*` 字元就相當於不依特定順序傳回所有文件的空白或未指定搜尋。

2. 在 [結果] 中，查詢結果會以未經處理的 JSON 呈現，與在以程式設計方式發出要求時，傳回 HTTP 回應主體的承載相同。

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>後續步驟

下列資源提供其他的查詢語法資訊和範例。

 + [簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Lucene 查詢語法](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Lucene 查詢語法範例](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [OData 篩選條件運算式語法](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 