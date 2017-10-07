---
title: "Azure SQL Database aaaPerformance 建議 |Microsoft 文件"
description: "hello Azure SQL Database 提供您 SQL 資料庫，可改善目前的查詢效能的建議。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 77db338a0a395aec78c9e02849ae5ba4f2d01680
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-recommendations"></a>效能建議

Azure SQL Database 會學習和會與您的應用程式，並提供您的 SQL database toomaximize hello 效能讓您自訂的建議。 同時藉由分析 SQL Database 的使用記錄來持續評估效能。 hello 建議提供資料庫唯一的工作負載模式為基礎，並協助改善其效能。

> [!NOTE]
> 建議在您的資料庫上啟用 [自動調整] 來使用建議。 如需詳細資訊，請參閱[自動調整](sql-database-automatic-tuning.md)。
>

## <a name="create-index-recommendations"></a>建立索引建議
Azure SQL Database 連續監視正在執行的 hello 查詢並找出 hello 索引無法改善 hello 效能。 一旦確信遺漏特定索引，將會建立新的 [建立索引] 建議。 Azure SQL Database 建置信賴估計效能改善 hello 索引將會把透過時間。 根據 hello 估計效能改善，建議會分類為高、 中或低。 

使用建議建立的索引永遠都會標記為 auto_created 索引。 查看 sys.indexes 檢視，可以得知哪些索引為 auto_created。 自動建立的索引不會封鎖 ALTER/RENAME 命令。 如果您嘗試 toodrop hello 資料行上建立索引的自動，hello 命令會將 $ 並 hello 自動建立索引與 hello 命令以及捨棄訊息。 一般索引會封鎖 hello ALTER/重新命名 命令會編製索引的資料行上。

一旦建立 hello 索引建議套用時，Azure SQL Database 將會比較的 hello 查詢的效能與 hello 基準效能。 如果新的索引所引進 hello 效能增強功能，建議會標示為成功並影響報告可使用。 萬一 hello 索引未帶來 hello 好處，即會自動回復。 如此一來 Azure SQL Database 可確保使用的建議將只會提升 hello 資料庫效能。

任何**建立索引**建議的撤退原則的套用 hello 建議，如果 hello 資料庫或集區 DTU 使用量 80%以上最後 20 分鐘或如果 hello 儲存體高於 90%的使用方式中不允許。 在此情況下，將會延遲 hello 建議。

## <a name="drop-index-recommendations"></a>卸除索引建議
此外 toodetecting 遺漏的索引時，Azure SQL Database 連續會分析現有的索引的 hello 效能。 如果未使用索引，Azure SQL Database 會建議卸除它。 在兩種情況下會建議使用卸除索引：
* 索引是另一個索引的複本 (編製和內含索引的資料行、分割、結構描述及篩選器相同)
* 索引長時間都未使用 (93 天)

卸除索引建議也經過實作後的 hello 驗證。 如果 hello 效能已獲得改善 hello 影響報表會提供。 偵測到效能降低時，將會還原建議。


## <a name="parameterize-queries-recommendations"></a>參數化查詢建議
**將查詢參數化**建議會有一個或更多查詢不斷重新編譯過，但得到 hello 相同的查詢執行計劃時出現。 這種狀況會強制參數化，可讓 toobe 快取，並在未來改善效能並減少資源使用狀況 hello 中重複使用的查詢計劃機會 tooapply 開啟。 

每一個查詢中一開始發行對 SQL Server 需要編譯 toobe toogenerate 執行計畫。 每個產生的計劃會新增 toohello 計畫快取，以及後續執行作業的 hello 相同的查詢可以重複使用此計劃的 hello 快取中，排除 hello 需要其他的編譯。 

傳送查詢，包含非參數化的值，應用程式可能會導致 tooa 的效能負擔，其中針對每個這類查詢使用不同參數值 hello 執行計畫會編譯一次。 在許多情況下 hello 與不同的參數值產生相同的查詢 hello 相同的執行計畫，但這些計劃仍然會個別加入 toohello 計畫快取。 重新編譯執行計畫使用的資料庫資源，增加 hello 查詢持續時間的時間和溢位 hello 計劃導致快取計劃 toobe hello 快取中收回。 SQL Server 的這個行為可以藉由設定強制參數化選項 hello 資料庫上的 hello 改變。 

toohelp 估計 hello 的這項建議的影響，您會提供與比較 hello 實際 CPU 使用量和 hello 投影 CPU 使用量 （就像已套用 hello 建議）。 此外 tooCPU 節省您查詢持續時間會減少 hello 編譯中所花費的時間。 也會有額外負荷更不在計畫快取，讓大部分的 hello 計劃快取中的 toostay 及重複使用。 您可以按一下 hello 套用此建議快速且輕鬆地**套用**命令。 

一旦您套用這項建議，它可讓您在資料庫上的分鐘內的強制參數化，並開始監視處理序可在大約 24 小時延續 hello。 在這段期間之後, 您將會是能 toosee hello 驗證報表會顯示資料庫的 CPU 使用量之前的 24 小時，而且在套用 hello 建議之後。 SQL Database Advisor 還具有會自動回復 hello 套用建議，如果已偵測到的效能低下的安全性機制。

## <a name="fix-schema-issues-recommendations"></a>修正結構描述問題建議
**請修正結構描述問題**建議時，會出現 hello SQL Database 服務通知中的結構描述相關的 SQL 錯誤發生在您的 Azure SQL Database 上的 hello 數目異常狀況。 您的資料庫在一小時內遇到多個結構描述相關的錯誤時 (無效的資料行名稱、無效的物件名稱等)，通常會出現此建議。

「 結構描述問題 」 是一種在 SQL Server 未對齊的 hello SQL 查詢的 hello 定義與 hello 資料庫結構描述的 hello 定義時，就可能發生的語法錯誤類別。 例如，其中一個 hello hello 查詢所預期的資料行可能會遺漏在 hello 目標資料表中，反之亦然。 

Azure SQL Database 服務通知中的結構描述相關的 SQL 錯誤發生在您的 Azure SQL Database 上的 hello 數目異常狀況時，就會出現 「 修正結構描述問題 」 的建議。 下列表格顯示 hello 錯誤 tooschema 相關的問題的 hello:

| SQL 錯誤碼 | 訊息 |
| --- | --- |
| 201 |程序或函數 '' 必須有參數 ''，但未提供。 |
| 207 |無效的資料行名稱 '*'。 |
| 208 |無效的物件名稱 '*'。 |
| 213 |資料行名稱或提供的數值數量與資料表定義不相符。 |
| 2812 |找不到預存程序 ' *'。 |
| 8144 |程序或函數 * 指定了太多的引數。 |

## <a name="next-steps"></a>後續步驟
監視您的建議，並繼續 tooapply 它們 toorefine 效能。 資料庫工作負載會動態地持續變更。 SQL Database advisor 會繼續 toomonitor，並提供可以改善您的資料庫效能的建議。 

* 請參閱[hello Azure 入口網站的效能建議](sql-database-advisor-portal.md)toouse 效能建議如何 hello Azure 入口網站的步驟。
* 請參閱[查詢效能深入資訊](sql-database-query-performance.md)有關 toolearn 和檢視 hello top 查詢的效能影響。

## <a name="additional-resources"></a>其他資源
* [查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [角色型存取控制](../active-directory/role-based-access-control-what-is.md)

