---
title: "Azure 搜尋 hello 入口網站中的 aaaImport 資料 |Microsoft 文件"
description: "使用 Azure Vm 上的 hello Azure 入口網站 toocrawl NoSQL Azure Cosmos DB Blob 儲存體、 資料表儲存體、 SQL Database 和 SQL Server 的 Azure 資料中的 hello Azure 搜尋匯入資料精靈。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 00b0e59594560c0cdaea748df196518e9fba3834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-tooazure-search-using-hello-portal"></a>匯入資料 tooAzure 搜尋使用 hello 入口網站
hello Azure 入口網站提供**匯入資料**hello Azure 搜尋索引將資料載入儀表板上的精靈。 

  ![Hello 命令列上的匯入資料][1]

就內部而言，hello 精靈會設定並叫用*索引子*，自動化 hello 編製索引處理序的幾個步驟： 

* 在 hello tooan 外部資料來源連接相同的 Azure 訂用帳戶
* 產生 hello 來源資料的結構為基礎的可修改的索引結構描述
* JSON 文件載入使用從 hello 資料來源擷取資料列集的索引

您可以使用 Azure Cosmos DB 中的範例資料試試看這個工作流程。 請瀏覽[hello Azure 入口網站中開始使用 Azure 搜尋](search-get-started-portal.md)如需相關指示。

> [!NOTE]
> 您可以啟動 hello**匯入資料**hello Azure Cosmos DB 儀表板 toosimplify 編製索引的該資料來源中的精靈。 在左瀏覽到 太**集合** > **加入 Azure 搜尋**tooget 啟動。

## <a name="data-sources-supported-by-hello-import-data-wizard"></a>Hello 匯入資料精靈 」 所支援的資料來源
hello 匯入資料精靈 支援下列資料來源的 hello: 

* Azure SQL Database
* Azure VM 上的 SQL Server 關聯式資料
* Azure Cosmos DB
* Azure Blob 儲存體
* Azure 資料表儲存體

必須輸入扁平化資料集。 您可以只從單一資料表、資料庫檢視或對等的資料結構匯入。 執行 hello 精靈之前，您應該建立這個資料結構。

## <a name="connect-tooyour-data"></a>Tooyour 資料連接
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)和開啟 hello 服務儀表板。 您可以按一下**更多服務**hello 跳躍列 toosearch 現有的 「 搜尋服務"hello 目前訂用帳戶中。 
2. 按一下**匯入資料**hello 命令列 tooslide 開啟 hello 匯入資料 刀鋒視窗上。  
3. 按一下**tooyour 資料連接**toospecify 索引子所使用的資料來源定義。 對於內部訂閱資料來源，通常可以偵測並讀取連接資訊，整體的設定需求降到最低 hello 精靈。

|  |  |
| --- | --- |
| **現有的資料來源** |如果您的搜尋服務中已經定義索引子，您可以針對另一次匯入選取現有的資料來源定義。 |
| **Azure SQL Database** |Hello 頁面上，或是透過 ADO.NET 連接字串可以指定服務名稱，具有讀取權限，資料庫使用者的認證和資料庫名稱。 選擇 hello 連接字串選項 tooview 或自訂屬性。 <br/><br/>必須在 hello 頁面上指定 hello 資料表或檢視，能夠 hello 資料列集。 Hello 連線成功，提供下拉式清單，讓您可以選取範圍之後，就會出現此選項。 |
| **在 Azure VM 上的 SQL Server** |指定完整服務名稱、使用者識別碼與密碼以及資料庫作為連接字串。 toouse 此資料來源，您先前必須已安裝憑證加密 hello 連線的 hello 本機存放區中。 如需指示，請參閱[SQL VM 連接 tooAzure 搜尋](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md)。 <br/><br/>必須在 hello 頁面上指定 hello 資料表或檢視，能夠 hello 資料列集。 Hello 連線成功，提供下拉式清單，讓您可以選取範圍之後，就會出現此選項。 |
| **Azure Cosmos DB** |需求包括 hello 帳戶、 資料庫和集合。 Hello 集合中的所有文件將會包含在 hello 索引。 您可以定義查詢 tooflatten 或篩選 hello 資料列集，或 toodetect 變更文件，後續的資料重新整理作業。 |
| **Azure Blob 儲存體** |需求包括 hello 儲存體帳戶和容器。 （選擇性） 如果 blob 名稱會遵循虛擬的命名慣例，進行群組，您可以指定 hello 名稱 hello 虛擬目錄部分為容器底下的資料夾。 如需詳細資訊，請參閱[為 Blob 儲存體編製索引](search-howto-indexing-azure-blob-storage.md)。 |
| **Azure 資料表儲存體** |需求包括 hello 儲存體帳戶和資料表名稱。 您可以選擇性地指定查詢 tooretrieve hello 資料表子集。 如需詳細資訊，請參閱[為表格儲存體編製索引](search-howto-indexing-azure-tables.md)。 |

## <a name="customize-target-index"></a>自訂目標索引
初步索引通常會集中 hello 推斷。 加入、 編輯或刪除欄位 toocomplete hello 結構描述。 此外，設定屬性在 hello 欄位層級 toodetermine 其後續搜尋行為。

1. 在**自訂目標索引**，指定 hello 名稱和**金鑰**使用的 toouniquely 識別每個文件。 hello 索引鍵必須是字串。 如果欄位值包含空格或連字號確定 tooset 中的進階選項**匯入資料**toosuppress hello 這些字元之驗證檢查。
2. 檢閱並修改 hello 剩餘的欄位。 通常會為您填入欄位名稱和類型。 建立 hello 索引之前，您可以變更 hello 資料型別。 之後若要變更，就需要重建。
3. 設定每個欄位的索引屬性：
   
   * 可擷取搜尋結果中傳回 hello 欄位。
   * 可篩選可讓 hello 欄位 toobe 在篩選運算式中參考。
   * 可排序可讓 hello 欄位 toobe 用於排序。
   * 可進行 facet 處理可讓多面向導覽的 hello 欄位。
   * Searchable 能夠進行全文檢索搜尋。
4. 按一下 hello**分析器**索引標籤上，如果您想 toospecify hello 欄位層級語言分析器。 此時只能指定語言分析器。 使用自訂分析器或非語言分析器 (如關鍵字、模式等等) 需要有程式碼。
   
   * 按一下**Searchable** toodesignate 全文檢索搜尋 hello 欄位，並啟用 hello 分析器下拉式清單。
   * 選擇您想要的 hello 分析器。 如需詳細資訊，請參閱[以多種語言建立文件的索引](search-language-support.md)。
5. 按一下 hello**建議工具**tooenable 預先輸入的查詢建議選取的欄位。

## <a name="import-your-data"></a>匯入資料
1. 在**匯入資料**，提供 hello 索引子的名稱。 前文提過該 hello 產品 hello 匯入資料精靈是索引子。 稍後，如果您想 tooview 或編輯它，您需要選取它從 hello 入口網站，而不是透過重新執行 hello 精靈。 
2. 指定 hello 排程，根據 hello 地區時區 hello 服務佈建。
3. 設定進階的選項 toospecify 臨界值是否索引可以繼續在文件卸除。 此外，您可以指定是否**金鑰**toocontain 空格或斜線允許欄位。  
4. 按一下**確定**toocreate hello 索引和 hello 資料匯入。

您可以監視 hello 入口網站中的索引。 載入文件時，您已定義的 hello 索引將會增加 hello 文件計數。 有時花幾分鐘，讓 hello 入口網站頁面 toopick 向上 hello 最新的更新。

hello 索引，便準備好 tooquery 所有 hello 文件會載入。

## <a name="query-an-index-using-search-explorer"></a>使用搜尋總管查詢索引

hello 入口網站包含**搜尋總管**，讓您可以查詢的索引，而不需要 toowrite 任何程式碼。 您可以將 [搜尋總管](search-explorer.md) 使用於任何索引。

hello 搜尋經驗為基礎預設設定，例如 hello[簡單的語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)和預設的 [受 searchMode 查詢參數 (https://docs.microsoft.com/rest/api/searchservice/search-documents)。 

結果會傳回在 JSON 中，詳細資訊的格式，以便您可以檢查 hello 整份文件。

## <a name="edit-an-existing-indexer"></a>編輯現有的索引子
如前所述，hello 匯入資料精靈 」 建立**索引子**，您可以修改為在 hello 入口網站中的獨立建構。

在 hello 服務儀表板按兩下 hello 索引子磚 tooslide 訂用帳戶建立的所有索引子的清單。 按兩下其中一個 hello 索引子 toorun、 編輯或刪除它。 您可以取代現有的另一個 hello 索引、 變更 hello 資料來源，以及編製索引期間設定錯誤臨界值的選項。

## <a name="edit-an-existing-index"></a>編輯現有索引
同時也建立 hello 精靈**索引**。 在 Azure 搜尋中，結構更新 tooan 索引將需要重建該索引。 重建將需要刪除 hello 索引，重新建立 hello 索引使用修訂過的結構描述中有 hello 您想要的變更，並重新載入資料。 結構化更新包含變更資料類型和重新命名或刪除欄位。

不需要重建的編輯作業包含新增欄位、變更評分設定檔、變更建議，或變更語言分析器。 如需詳細資訊，請參閱 [更新索引](https://msdn.microsoft.com/library/azure/dn800964.aspx) 。


## <a name="next-steps"></a>後續步驟
檢閱這些連結 toolearn 更多關於索引子：

* [為 Azure SQL Database 編製索引](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB 編製索引](search-howto-index-documentdb.md)
* [為 Blob 儲存體編製索引](search-howto-indexing-azure-blob-storage.md)
* [為表格儲存體編製索引](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png

