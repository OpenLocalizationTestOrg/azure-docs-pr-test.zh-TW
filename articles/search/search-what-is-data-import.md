---
title: "在 Azure 搜尋 aaaData 上載 |Microsoft 文件"
description: "了解 tooupload 資料 tooan Azure 搜尋中的索引。"
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>上傳資料 tooAzure 搜尋
> [!div class="op_single_selector"]
> * [概觀](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

有兩種方式 toopopulate 具有您資料的索引。 hello 第一個選項以手動方式將資料推送至 hello 索引使用 hello Azure 搜尋[REST API](search-import-data-rest-api.md)或[.NET SDK](search-import-data-dotnet.md)。 hello 第二個選項太[點支援的資料來源](search-indexer-overview.md)tooyour 編製索引，並讓 Azure 搜尋會自動納入 hello 資料。

## <a name="push-data-tooan-index"></a>推播資料 tooan 索引
這種方法是指傳送您資料 tooAzure 搜尋 toomake tooprogrammatically 可供搜尋它。 對於具有非常低的延遲需求 （例如，如果您需要搜尋與動態清查資料庫同步作業 toobe） 應用程式，hello 發送模型是您唯一的選項。

您可以使用 hello [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents)或[.NET SDK](search-import-data-dotnet.md) toopush 資料 tooan 索引。 正在透過 hello 入口網站將資料推送沒有工具支援。

這種方法是比 hello 提取模型更有彈性，因為個別或批次中，您可以上傳文件 （too1000 每個批次或 16 MB，總何種限制者為優先）。 hello 發送模型也可讓您 tooupload 文件 tooAzure 搜尋無論資料的位置。

了解 Azure 搜尋的 hello 資料格式是 JSON，且 hello 資料集中的所有文件必須具有對應 toofields 索引結構描述中定義的欄位。 

## <a name="pull-data-into-an-index"></a>將資料提取到索引
hello 提取模型搜耙支援的資料來源，並自動 hello 資料上傳至您的索引。 在 Azure 搜尋服務中，這項功能是透過索引子來實作，其目前可供 [Blob 儲存體](search-howto-indexing-azure-blob-storage.md)、[表格儲存體](search-howto-indexing-azure-tables.md)、[Azure Cosmos DB](http://aka.ms/documentdb-search-indexer)、[Azure SQL Database 和 Azure VM 上的 SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) 使用。 

索引子連接索引 tooa 資料來源 （通常是資料表、 檢視或對等的結構），並將對應 hello 索引中的來源欄位 tooequivalent 欄位。 在執行期間，hello 資料列集是自動轉換的 tooJSON 並載入 hello 指定的索引。 所有的索引器支援排程，好讓您可以指定 hello 資料是 toobe 重新整理的頻率。 大部分的索引子會提供變更追蹤如果 hello 資料來源支援它。 所追蹤變更和刪除 tooexisting 文件除了 toorecognizing 新文件、 索引子移除 hello 需求 tooactively 管理您的索引中的 hello 資料。 

索引子功能會公開在 hello [Azure 入口網站](search-import-data-portal.md)，hello [REST API](/rest/api/searchservice/Indexer-operations)，和 hello [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations)。 

利用 toousing hello 入口網站是，Azure 搜尋可以通常會產生預設的索引結構描述為您藉由讀取 hello hello 來源資料集的中繼資料。 處理 hello 索引之後的 hello, 允許則不需要重新索引只有結構描述編輯之前，您可以修改 hello 產生的索引。 如果您想要 toomake 影響的 hello 變更直接 hello 結構描述，您需要 toorebuild hello 索引。 

填入 hello 索引之後，您可以使用**搜尋總管**當作驗證步驟的 hello 入口網站的命令列中。

## <a name="query-an-index-using-search-explorer"></a>使用搜尋總管查詢索引

快速 tooperform hello 文件上傳的初步檢查是 toouse**搜尋總管**hello 入口網站中。 hello 總管可讓您查詢的索引，而不需要 toowrite 任何程式碼。 hello 搜尋經驗為基礎預設設定，例如 hello[簡單的語法](/rest/api/searchservice/simple-query-syntax-in-azure-search)和預設[受 searchMode 查詢參數](/rest/api/searchservice/search-documents)。 在 JSON 中會傳回結果，以便您可以檢查 hello 整份文件。

> [!TIP]
> 許多[Azure 搜尋程式碼範例](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search)包含內嵌或隨時可用資料集，提供簡單的方式 tooget 啟動。 hello 入口網站也提供範例索引子和小型不動產資料集 （名為 「 realestate-我們的範例 」） 所組成的資料來源。 當您執行 hello 預先設定的索引子上 hello 範例資料來源時，索引建立，並使用文件，然後在 搜尋總管或由您撰寫的程式碼可查詢載入。
