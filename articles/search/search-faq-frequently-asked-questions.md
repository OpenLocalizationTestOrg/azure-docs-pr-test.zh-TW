---
title: "常見問題 (集 FAQ) Azure 搜尋的相關 aaaFrequently |Microsoft 文件"
description: "取得解答 toocommon 疑問 Microsoft Azure 搜尋服務"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Azure 搜尋服務 - 常見問題集 (FAQ)
 
 尋找答案 toocommonly 常見問題解答概念、 程式碼和案例相關 tooAzure 搜尋。

## <a name="platform"></a>平台

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>Azure 搜尋服務與 DBMS 的全文檢索搜尋有何不同？

Azure 搜尋服務支援多個資料來源、[許多語言的語言分析](https://docs.microsoft.com/rest/api/searchservice/language-support)、[關注與不尋常資料輸入的自訂分析](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search)、透過[評分設定檔](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)搜尋排名控制項，以及自動提示、搜尋結果醒目提示和多面向導覽等使用者體驗功能。 它也包含其他功能，例如同義字和豐富的查詢語法，但這些功能通常並無不同之處。

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>Hello Elasticsearch Azure 搜尋之間的差異為何？

比較搜尋技術時，客戶經常詢問 Azure 搜尋服務與 Elasticsearch 相較下的詳細資料。 客戶選擇 Azure 搜尋 Elasticsearch 透過他們的搜尋應用程式專案通常這樣做，因為我們所做的索引鍵的工作更容易，或者必須 hello 與其他 Microsoft 技術的內建整合：

+ Azure 搜尋服務是受到完整管理的雲端服務，當佈建足夠的備援時 (2 個用於讀取存取的複本及 3 個用於讀寫的複本)，會達到服務等級協定 (SLA) 的 99.9%。
+ Microsoft 的[自然語言處理器](https://docs.microsoft.com/rest/api/searchservice/language-support)提供先進的語言分析。  
+ [Azure 搜尋服務索引子](search-indexer-overview.md)可以搜耙各種不同的 Azure 資料來源來建立初始和累加索引。
+ 如果您需要快速回應 toofluctuations 查詢或索引的磁碟區中，您可以使用[滑桿控制項](search-manage.md#scale-up-or-down)hello Azure 入口網站，或執行中[PowerShell 指令碼](search-manage-powershell.md)，直接略過分區管理。  
+ [計分和微調功能](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)提供 hello 就來影響搜尋超過單獨哪些 hello 搜尋引擎可提供次序的分數。 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>我可以暫停 Azure 搜尋服務並停止計費嗎？

您無法暫停 hello 服務。 建立 hello 服務時您專供配置運算和儲存體資源。 它可能 toorelease 並不會回復這些資源隨。 

## <a name="indexing-operations"></a>索引作業

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>可備份及還原 (或下載及移動) 索引或索引快照集嗎？

雖然您可以用[取得索引定義](https://docs.microsoft.com/rest/api/searchservice/get-index)隨時中，沒有任何索引擷取，快照集或下載的備份還原功能*填入*hello 雲端 tooa 本機系統 中執行的索引或移動 tooanother Azure 搜尋服務。 

索引是建立和填入您所撰寫，並只會在 Azure 搜尋 hello 雲端中執行程式碼。 通常，客戶希望 toomove 索引 tooanother 服務藉由編輯其程式碼 toouse 新端點，執行這項操作，，然後重新執行編製索引。 如果您想 hello 能力 tootake 快照集或備份索引時，轉換投票[User Voice](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index)。

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>我可以索引從 SQL 資料庫複本 (適用於太[Azure SQL Database 的索引子](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 當建立索引從頭做為資料來源有 hello 使用主要或次要複本的任何限制。 不過，重新整理 （根據變更的記錄） 的累加式更新的索引需要 hello 主要複本。 這項需求是來自 SQL Database，以保證只對主要複本進行變更追蹤。 如果您嘗試使用針對索引重新整理工作負載的次要複本，並讓您享有所有 hello 資料不保證。

## <a name="search-operations"></a>搜尋作業

### <a name="can-i-search-across-multiple-indexes"></a>我可以搜尋多個索引嗎？

不可以，不支援此作業。 搜尋永遠是已設定領域的 tooa 單一索引。

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>我可以依使用者身分識別來限制搜尋主體存取嗎？

Azure 搜尋服務並沒有針對每個使用者資料存取的角色型安全性模型。 驗證，則可能是完整的權限或唯讀 hello 服務層級。 有些客戶實作了以[`$filter`搜尋參數](https://docs.microsoft.com/rest/api/searchservice/search-documents)為基礎的解決方案，但它是最佳的因應措施。 如果您想要這項功能，請在 [User Voice](https://feedback.azure.com/forums/263029-azure-search/category/86074-security) 上投下一票。

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>為什麼有零符合在我知道 toobe 有效項目上？

hello 最常見的情況不了解每種查詢類型支援不同的搜尋行為和語言分析的層級。 全文檢索搜尋，也就是 hello 主要工作負載，包括中斷 tooroot 表單關閉條款的語言分析階段。 由於 hello 語彙基元化的詞彙會比對變數數目越大，這方面的查詢剖析的投射更廣泛的網路可能的符合項目。

如果您叫用[其他查詢類型](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (萬用字元搜尋、模糊搜尋、鄰近搜尋、建議等等)，則不會進行語言分析。 詞彙會加入做為 toohello 查詢樹狀結構-是。 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>為何 hello 搜尋排名常數或等於 1.0 的每個叫用的分數？

根據預設，搜尋結果，就會獲得根據上 hello[統計屬性比對名詞](search-lucene-query-architecture.md#stage-4-scoring)，和 ordered 高 toolow hello 結果集中。 不過，某些查詢類型 （萬用字元、 前置詞、 regex） 一律參與常數分數 toohello 整體文件的分數。 這是設計的行為。 Azure 搜尋會常數評分 tooallow 透過查詢擴充 toobe 包含在 hello 結果，而不會影響 hello 排名找到的相符項目。 

例如，假設在萬用字元搜尋中輸入 "tour*" 會產生 “tours”、“tourettes” 和 “tourmaline” 的相符項目。 提供這些結果的 hello 性質，所以 tooreasonably 推斷哪些詞彙會比其他更有價值。 基於這個理由，當評分導致萬用字元、前置詞和 Regex 的查詢類型時，我們會忽略字詞頻率。 根據部分輸入的搜尋結果會提供常數評分 tooavoid 偏差朝向可能未預期的相符項目。

## <a name="design-patterns"></a>設計模式

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>Hello 實作當地語系化的搜尋的最佳方法為何？

大部分的客戶會選擇在集合上專用的欄位時 toosupporting 不同地區 （語言），在 hello 相同的索引。 地區設定特定欄位可讓可能 tooassign 適當分析器。 例如，指派包含法文字串 hello Microsoft 法文分析器 tooa 欄位。 它也可以簡化篩選。 如果您知道查詢起始為 fr-fr 頁面上，您可能會限制搜尋結果 toothis 欄位。 或者，建立[計分設定檔](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)toogive hello 欄位較多的相對權重。

## <a name="next-steps"></a>後續步驟

您的問題是否與缺少特性或功能相關？ 要求上 hello hello 功能[User Voice 網站](https://feedback.azure.com/forums/263029-azure-search)。

## <a name="see-also"></a>另請參閱

 [StackOverflow：Azure 搜尋服務](https://stackoverflow.com/questions/tagged/azure-search)   
 [全文檢索搜尋如何在 Azure 搜尋服務中運作](search-lucene-query-architecture.md)  
 [何謂 Azure 搜尋服務？](search-what-is-azure-search.md)

 