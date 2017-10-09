---
title: "SQL 資料倉儲中的 aaaConcurrency 和工作負載管理 |Microsoft 文件"
description: "了解 Azure SQL 資料倉儲中的並行存取和工作負載管理以開發解決方案。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>SQL 資料倉儲中的並行存取和工作負載管理
Microsoft Azure SQL 資料倉儲大規模 toodeliver 可預測的效能可協助您控制並行層級和資源配置，例如記憶體和 CPU 優先順序。 本文介紹 toohello 概念的並行存取，以及工作負載的管理，說明已實作這兩種功能，以及如何控制這些資料倉儲中。 支援多使用者環境的預定的 toohelp SQL 資料倉儲工作負載管理。 它並不適用於多租用戶工作負載。

## <a name="concurrency-limits"></a>並行存取限制
SQL 資料倉儲可讓向上 too1，024 並行連線。 這 1,024 個連線全都可以並行提交查詢。 不過，SQL 資料倉儲 toooptimize 輸送量可能排入佇列，每個查詢所接收的最小記憶體授與某些查詢 tooensure。 佇列會在查詢執行時發生。 佇列的查詢時可以提高的並行到達限制，SQL 資料倉儲總輸送量，方法是確保作用中的查詢取得存取 toocritically 所需的記憶體資源。  

並行存取限制受到兩個概念所控制：「並行查詢」和「並行存取插槽」。 針對查詢 tooexecute，它必須在 hello 查詢並行限制和 hello 並行位置配置內執行。

* 並行的查詢是執行在 hello 相同的 hello 查詢時間。 SQL 資料倉儲支援 too32 hello 較大的 DWU 大小上的並行查詢。
* 並行存取插槽是根據 DWU 所配置。 每 100 個 DWU 提供 4 個並行存取插槽。 例如，DW100 會配置 4 個並行存取插槽，而 DW1000 會配置 40 個。 每個查詢取用一或多個並行 [插槽]，相依於 hello[資源類別](#resource-classes)的 hello 查詢。 Hello smallrc 資源類別中執行的查詢取用一個並行存取的位置。 較高資源類別中執行的查詢會使用更多的並行存取插槽。

hello 以下表格說明 hello 限制的並行查詢和在 hello 並行插槽各種 DWU 大小。

### <a name="concurrency-limits"></a>並行存取限制
| DWU | 並行查詢上限 | 配置的並行存取插槽 |
|:--- |:---:|:---:|
| DW100 |4 |4 |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 |20 |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

當符合以上其中一個臨界值時，新的查詢將以先進先出順序排入佇列和執行。  完成查詢與 hello 查詢和插槽數目低於 hello 限制時，會發行排入佇列的查詢。 

> [!NOTE]  
> *選取*以獨佔方式在執行的查詢動態管理檢視 (Dmv)，或目錄檢視都未受到任何 hello 並行存取限制。 您可以監視 hello 系統，無論 hello 在其上執行的查詢數目。
> 
> 

## <a name="resource-classes"></a>資源類別
資源類別可協助您控制記憶體配置和給定 tooa 查詢的 CPU 循環。 您可以指派兩種類型的資料庫角色的 hello 表單中的資源類別 tooa 使用者。 兩種類型的資源類別，如下所示為 hello:
1. 動態資源類別 (**smallrc，mediumrc，largerc，xlargerc**) 配置的記憶體，根據 hello 以變數目前的 DWU。 這表示當您向上擴充 tooa 較大的 DWU，查詢會自動取得更多記憶體。 
2. 靜態資源類別 (**staticrc10，staticrc20，staticrc30，staticrc40，staticrc50，staticrc60，staticrc70，staticrc80**) 配置 hello 相同數量的記憶體，不論 hello 目前的 DWU (前提是 hello DWU 本身有足夠的記憶體）。 這表示在較大的 DWU 中，您將可以在每個資源類別中同時執行更多查詢。

採用 **smallrc** 和 **staticrc10** 的使用者會獲得較小量的記憶體，且可利用較高的並行存取能力。 相反地，使用者指派太**xlargerc**或**staticrc80**有大量的記憶體，並因此更少的查詢可以同時執行。

根據預設，每個使用者都 hello 小型資源類別的成員**smallrc**。 hello 程序`sp_addrolemember`是使用 tooincrease hello 資源類別，和`sp_droprolemember`是使用 toodecrease hello 資源類別。 例如，此命令將會增加 hello 資源類別的 loaduser 太**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>不採用資源類別的查詢

有幾種查詢類別不會因較大的記憶體配置而受益。 hello 系統會忽略其資源類別配置，並一律改為在 hello 小型資源類別中執行這些查詢。 如果在 hello 小型資源類別中永遠執行這些查詢，可以執行並行位置有不足的壓力，而且它們不會使用比所需的多個位置。 如需詳細資訊，請參閱 [資源類別例外狀況](#query-exceptions-to-concurrency-limits) 。

## <a name="details-on-resource-class-assignment"></a>資源類別指派的詳細資料


資源類別的其他詳細資料︰

* *更改角色*需要的權限的使用者 toochange hello 資源類別。
* 雖然您可以新增使用者 tooone 或多個 hello 較高的資源類別，動態資源類別的優先順序高於靜態資源類別。 也就是說，如果使用者被指派 tooboth **mediumrc**（動態） 和**staticrc80**（靜態） **mediumrc**是 hello 資源類別，才會被接受。
 * 當使用者獲指派 toomore 比特定的資源類別類型 （多個動態資源類別或多個靜態資源類別） 中的一項資源類別時，被採用 hello 最高的資源類別。 也就是如果 tooboth mediumrc 與 largerc，則指派給使用者，被適用於高資源類別 hello (largerc)。 如果使用者獲指派 tooboth **staticrc20**和**statirc80**， **staticrc80**會接受。
* 無法變更 hello 系統管理使用者的 hello 資源類別。

如需詳細範例，請參閱 [變更使用者資源類別的範例](#changing-user-resource-class-example)。

## <a name="memory-allocation"></a>記憶體配置
有優缺點 tooincreasing 使用者的資源類別。 增加使用者的資源類別，提供其查詢存取 toomore 記憶體，這可能表示查詢執行的速度。  不過，較高的資源類別也會減少 hello 可以執行的並行查詢數目。 這是 hello 配置大量記憶體 tooa 單一查詢，或允許其他查詢，也需要記憶體配置，同時 toorun 之間的取捨。 一位使用者指定高配置記憶體的查詢，如果其他使用者將不會存取 toothat 相同記憶體 toorun 查詢。

下表中的 hello 對應 hello 記憶體配置 tooeach 發佈 DWU 和資源的類別。

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>每個散發套件的動態資源類別 (MB) 記憶體配置
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1,600 |
| DW500 |100 |400 |800 |1,600 |
| DW600 |100 |400 |800 |1,600 |
| DW1000 |100 |800 |1,600 |3,200 |
| DW1200 |100 |800 |1,600 |3,200 |
| DW1500 |100 |800 |1,600 |3,200 |
| DW2000 |100 |1,600 |3,200 |6,400 |
| DW3000 |100 |1,600 |3,200 |6,400 |
| DW6000 |100 |3,200 |6,400 |12,800 |

下表中的 hello 對應 hello 記憶體配置 tooeach 發佈 DWU 和靜態資源類別。 請注意 hello 較高的資源類別具有其記憶體減少 toohonor hello 全域 DWU 限制。

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>每個散發套件的靜態資源類別 (MB) 記憶體配置
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW500 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW600 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW1000 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1200 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1500 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW2000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW3000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW6000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |12,800 |

從上述資料表的 hello，您可以看到在 hello DW2000 上執行的查詢**xlargerc**資源類別必須存取 too6，400 MB 的記憶體內的每個 hello 60 分散式資料庫。  SQL 資料倉儲中有 60 個散發套件。 因此，toocalculate hello 總記憶體配置指定的資源類別中的查詢時，值以上的 hello 應該乘以 60。

### <a name="memory-allocations-system-wide-gb"></a>全系統記憶體配置 (GB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

從這個資料表的全系統記憶體配置中，您可以看到上 DW2000 hello xlargerc 資源類別中執行查詢配置 375 gb 的記憶體總計 (6,400 MB * 60 分佈 / 1024 tooconvert tooGB) 上的 SQL 資料倉儲的 hello 全部內容。

hello 相同計算套用 toostatic 資源類別。
 
## <a name="concurrency-slot-consumption"></a>並行存取插槽耗用量  
SQL 資料倉儲會授與更多的記憶體 tooqueries 較高的資源類別中執行。 記憶體是固定的資源。  因此，hello 更多的記憶體配置每個查詢，可以在執行較少的並行查詢的 hello。 hello 表 reiterates 所有 hello hello 並行的 DWU 可用的插槽與每個資源類別所耗用的 hello 插槽數目會顯示在單一檢視中的上一個概念。  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>動態資源類別並行存取插槽的配置和耗用量  
| DWU | 並行查詢上限 | 配置的並行存取插槽 | Smallrc 所使用的插槽 | Mediumrc 所使用的插槽 | Largerc 所使用的插槽 | Xlargerc 所使用的插槽 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |1 |2 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |
| DW400 |16 |16 |1 |4 |8 |16 |
| DW500 |20 |20 |1 |4 |8 |16 |
| DW600 |24 |24 |1 |4 |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>靜態資源類別並行存取插槽的配置和耗用量  
| DWU | 並行查詢上限 | 配置的並行存取插槽 |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |2 |4 |4 |4 |4 |4 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4 |8 |16 |16 |16 |16 |
| DW500 | 20| 20| 1| 2| 4| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4| 8| 16| 32| 32| 32|
| DW2000 | 32| 80| 1| 2| 4| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4| 8| 16| 32| 64| 128|

從上述表格中，您會看到以 DW1000 身分執行的 SQL 資料倉儲，配置最多 32 個並行查詢，以及總數 40 個的並行存取插槽。 如果所有的使用者都以 smallrc 執行，將允許 32 個並行查詢，因為每個查詢會取用 1 個並行存取插槽。 如果執行 mediumrc DW1000 上的所有使用者、 每個查詢則會配置 800 MB 散發 47 GB 的記憶體總計配置每個查詢，每並行就是限制的 too5 使用者 (40 並行插槽 / 每位使用者 mediumrc 插槽 8)。

## <a name="selecting-proper-resource-class"></a>選取適當的資源類別  
最好的作法是 toopermanently 指派使用者 tooa 資源類別，而不是變更其資源類別。 例如，載入 tooclustered 資料行存放區資料表建立高品質索引配置更多的記憶體時。 tooensure 負載存取 toohigher 記憶體、 建立使用者，特別是用於載入資料和永久指派此使用者 tooa 高資源類別。
有幾個最佳作法 toofollow 這裡。 如上所述，SQL DW 支援兩種資源類別類型：靜態資源類別和動態資源類別。
### <a name="loading-best-practices"></a>載入的最佳做法
1.  如果 hello 期望載入一般資料量，靜態資源類別是不錯的選擇。 更新版本中，當向上 tooget 更多計算能力、 hello 資料倉儲將無法 toorun 更多的並行查詢-現成的因為 hello 負載使用者不會耗用更多記憶體。
2.  如果 hello 期望在某些情況下更大的負載，動態資源類別是不錯的選擇。 更新版本中，當向上 tooget 更多計算能力，hello 負載使用者會收到更多的記憶體--現成的因此允許 hello 負載 tooperform 更快。

hello 所需的記憶體 tooprocess 載入有效率地取決於 hello 性質 hello 資料表載入和處理資料的 hello 數量。 比方說，CCI 資料表將資料載入要求一些記憶體 toolet CCI 資料列群組達到牽動。 如需詳細資訊，請參閱 hello 資料行存放區索引資料載入指引。

最佳做法，我們建議您 toouse 至少 200 MB 的記憶體載入。

### <a name="querying-best-practices"></a>查詢的最佳做法
查詢會因其複雜性而有不同的需求。 增加每個查詢的記憶體，或增加 hello 並行是這兩個有效的方式 tooaugment 根據 hello 查詢需求的整體輸送量。
1.  如果 hello 期望規則、 複雜的查詢 (例如，toogenerate 每日及每週的報表)，但是不需要 tootake 並行優點，動態資源類別是不錯的選擇。 如果 hello 系統有多個資料 tooprocess，向上擴充 hello 資料倉儲將會因此自動提供更多記憶體 toohello 使用者執行 hello 查詢。
2.  如果 hello 期望變數或 diurnal 並行模式 (例如透過 web UI 廣泛存取如果會查詢 hello 資料庫)，靜態資源類別是不錯的選擇。 稍後，當 toodata 倉儲向上擴充，hello hello 靜態資源類別相關聯的使用者會自動是無法 toorun 更多的並行查詢。

它相依於許多因素，例如 hello 少量資料的查詢，hello hello 資料表結構描述，以及各種聯結、 選取項目，與群組述詞的性質為非簡單式，根據您的查詢 hello 需求選取適當的記憶體授與。 一般的觀點而言，配置更多記憶體可讓查詢 toocomplete 較快，但是會減少 hello 整體的並行存取。 如果您不在意並行存取能力，則可以放心地超額配置記憶體。 您可能需要 toofine 微調輸送量，嘗試的資源類別的各種類別。

您可以使用 hello 下列預存程序 toofigure 出並行存取，以及記憶體授與每個資源類別，為給定 SLO 和 hello 最接近最佳資源類別的記憶體密集 CCI 非資料分割 CCI 資料表作業在指定的資源類別：

#### <a name="description"></a>Description:  
以下是 hello 用途，此預存程序：  
1. toohelp 出每個資源類別，在給定的 SLO 的並行存取，以及記憶體授與使用者數。 使用者需要 tooprovide NULL 的結構描述和 tablename 這個 hello 下面範例所示。  
2. toohelp 使用者找出 hello 最接近最佳資源類別 hello 記憶體 intensed CCI 作業 （負載，複製資料表時，會重建索引等） 指定的資源類別的非資料分割 CCI 資料表上。 hello 預存程序會使用這個資料表的結構描述 toofind 出 hello 所需的記憶體授與。

#### <a name="dependencies--restrictions"></a>相依性及限制：
- 這個預存程序不是設計的 toocalculate cci 分割資料表的記憶體需求。    
- 這個預存程序不接受的 CTAS/INSERT SELECT hello SELECT 部分的記憶體需求納入考量，並假設它 toobe 簡單的選取。
- 這個預存程序會使用暫存資料表，因此這可用 hello 工作階段中建立此預存程序所在。    
- 這個預存程序取決於 hello 目前供應項目 （例如硬體組態、 DMS 組態），如果變更了，然後此預存程序就無法正確運作。  
- 此預存程序仰賴目前提供的並行存取限制，如果限制有任何變更，此預存程序就無法正確運作。  
- 此預存程序仰賴現有的資源類別供應項目，如果其中有任何變更，此預存程序就無法正確運作。  

>  [!NOTE]  
>  如果您在使用所提供的參數來執行預存程序後沒有取得輸出，則可能有兩種情況。 <br />1.DW 參數包含無效的 SLO 值 <br />2.沒有符合 CCI 作業的資源類別 (若已提供資料表名稱)。 <br />例如，在 DW100，最高可用的記憶體授與為 400 MB 和寬型資料表結構描述是否足以 toocross hello 需求為 400 MB。
      
#### <a name="usage-example"></a>使用範例：
語法：  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:請提供 NULL 參數 tooextract hello hello 資料倉儲資料庫從目前的 DWU，或提供任何支援的 DWU hello 'DW100' 形式
2. @SCHEMA_NAME:提供 hello 資料表的結構描述名稱
3. @TABLE_NAME:提供 hello 感興趣的資料表名稱

執行此預存程序的範例：  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

無法建立 Table1 hello 上述範例中使用，如下所示：  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>以下是 hello 預存程序定義：
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>查詢的重要性
SQL 資料倉儲使用工作負載群組來實作資源類別。 有八個 hello 跨各種 DWU 大小控制 hello 行為 hello 資源類別的工作負載群組的總計。 對於任何 DWU，SQL 資料倉儲會使用僅有四個 hello 八個工作負載群組。 這使得意義，因為每個工作負載群組指派的四個資源類別 tooone: smallrc mediumrc，largerc，或 xlargerc。 hello 的了解 hello 工作負載群組重要性是其中部分工作負載群組會設定 toohigher*重要性*。 重要性可用於 CPU 排程。 以高重要性執行的查詢會取得比中度重要性的查詢高三倍的 CPU 週期。 因此，並行存取插槽對應也會判斷 CPU 優先順序。 當查詢取用 16 個以上的插槽時，就會以高重要性執行。

hello 下表顯示每個工作負載群組的 hello 重要性對應。

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>工作負載群組對應 tooconcurrency 位置和重要性
| 工作負載群組 | 並行存取插槽對應 | MB / 散發套件 | 重要性對應 |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |中型 |
| SloDWGroupC01 |2 |200 |中型 |
| SloDWGroupC02 |4 |400 |中型 |
| SloDWGroupC03 |8 |800 |中型 |
| SloDWGroupC04 |16 |1,600 |高 |
| SloDWGroupC05 |32 |3,200 |高 |
| SloDWGroupC06 |64 |6,400 |高 |
| SloDWGroupC07 |128 |12,800 |高 |

從 hello**配置和耗用量的並行插槽**圖表中，您可以看到，DW500 1、 4、 8 或 16 的並行存取位置 smallrc、 mediumrc、 largerc，和 xlargerc，分別使用。 您可以在 hello 上述圖表 toofind hello 重要性，針對每個資源類別中查詢這些值。

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>資源類別 tooimportance 的 DW500 對應
| 資源類別 | 工作負載群組 | 已使用的並行存取插槽 | MB / 散發套件 | 重要性 |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |中型 |
| mediumrc |SloDWGroupC02 |4 |400 |中型 |
| largerc |SloDWGroupC03 |8 |800 |中型 |
| xlargerc |SloDWGroupC04 |16 |1,600 |高 |
| staticrc10 |SloDWGroupC00 |1 |100 |中型 |
| staticrc20 |SloDWGroupC01 |2 |200 |中型 |
| staticrc30 |SloDWGroupC02 |4 |400 |中型 |
| staticrc40 |SloDWGroupC03 |8 |800 |中型 |
| staticrc50 |SloDWGroupC03 |16 |1,600 |高 |
| staticrc60 |SloDWGroupC03 |16 |1,600 |高 |
| staticrc70 |SloDWGroupC03 |16 |1,600 |高 |
| staticrc80 |SloDWGroupC03 |16 |1,600 |高 |

您可以使用 hello 疑難排解時，下列 DMV 查詢 toolook 在 hello 檢視方塊的 hello 資源管理員，或 tooanalyze hello 工作負載群組的作用中和歷史使用量詳細的記憶體資源配置中的 hello 差異。

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>採用並行存取限制的查詢
大多數查詢都受到資源類別控管。 這些查詢都必須容納在 hello 並行查詢和並行位置臨界值內。 使用者無法選擇 tooexclude 查詢從 hello 並行存取模型中的插槽。

tooreiterate，hello 下列陳述式，採用資源類別：

* INSERT-SELECT
* UPDATE
* 刪除
* SELECT (當查詢使用者資料表時)
* ALTER INDEX REBUILD
* ALTER INDEX REORGANIZE
* ALTER TABLE REBUILD
* CREATE INDEX
* CREATE CLUSTERED COLUMNSTORE INDEX
* CREATE TABLE AS SELECT (CTAS)
* 載入資料
* Hello 資料移動服務 (DMS) 所進行的資料移動作業

## <a name="query-exceptions-tooconcurrency-limits"></a>查詢例外狀況 tooconcurrency 限制
某些查詢不接受 hello 資源指派給類別 toowhich hello 使用者。 當 hello 特定命令所需的記憶體資源不足，通常是因為 hello 命令是中繼資料的作業時，對這些例外狀況 toohello 並行存取限制。 這些例外狀況 hello 目標是 tooavoid 較大的記憶體配置將永遠不需要的查詢。 在這些情況下，不論 hello 實際資源類別一律會使用小型資源類別 (smallrc) hello 預設指派 toohello 使用者。 例如， `CREATE LOGIN` 一律會在 smallrc 中執行。 hello 所需資源 toofulfill 這項作業都是很低，因此不會有意義 tooinclude hello 查詢 hello 並行存取模型中的插槽中。  這些查詢也不會受到 hello 32 使用者並行存取限制，無限的數量的這些查詢可以執行 toohello 工作階段限制為 1,024 工作階段設定。

hello 下列陳述式不接受資源類別：

* CREATE 或 DROP TABLE
* ALTER TABLE ...SWITCH、SPLIT 或 MERGE PARTITION
* ALTER INDEX DISABLE
* DROP INDEX
* CREATE、UPDATE 或 DROP STATISTICS
* TRUNCATE TABLE
* ALTER AUTHORIZATION
* CREATE LOGIN
* CREATE、ALTER 或 DROP USER
* CREATE、ALTER 或 DROP PROCEDURE
* CREATE 或 DROP VIEW
* INSERT VALUES
* 從系統檢視和 DMV 來 SELECT
* EXPLAIN
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a> 變更使用者資源類別的範例
1. **建立登入：**開啟連接 tooyour**主要**上 hello 裝載您的 SQL 資料倉儲資料庫的 SQL server 資料庫並執行下列命令的 hello。
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > Azure SQL 資料倉儲使用者 hello master 資料庫中是個不錯的主意 toocreate 使用者。 在 master 中建立使用者，可讓使用者 toologin 使用 SSMS 等工具，而不指定資料庫名稱。  它也可讓它們 toouse hello 物件總管 中 tooview SQL server 的所有資料庫。  如需有關建立和管理使用者的詳細資料，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。
   > 
   > 
2. **建立 SQL 資料倉儲的使用者：**開啟連接 toohello **SQL 資料倉儲**資料庫並執行下列命令的 hello。
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **授與權限：**下列範例授與 hello`CONTROL`上 hello **SQL 資料倉儲**資料庫。 `CONTROL`在 hello 資料庫層級是 hello db_owner SQL Server 中的對等。
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **增加資源類別：**使用 hello 下列查詢會 tooadd 使用者 tooa 較高的工作負載管理角色。
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **減少資源類別：**使用 hello 下列查詢會 tooremove 工作負載管理角色的使用者。
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > 不可能 tooremove smallrc 的使用者。
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>已排入佇列的查詢偵測和其他 DMV
您可以使用 hello`sys.dm_pdw_exec_requests`並行佇列中等待的 DMV tooidentify 查詢。 正在等待並行存取插槽的查詢狀態為 **暫停**。

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

工作負載管理角色可以使用 `sys.database_principals`來檢視。

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

hello，下列查詢會顯示每個使用者指派給角色。

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

SQL 資料倉儲具有 hello 下列等候類型：

* **LocalQueriesConcurrencyResourceType**： 坐 hello 並行插槽 framework 外部的查詢。 DMV 查詢及 `SELECT @@VERSION` 這類的系統函數是本機查詢的範例。
* **UserConcurrencyResourceType**： 坐在 hello 並行處理插槽架構內的查詢。 針對使用者資料表的查詢代表會使用此資源類型的範例。
* **DmsConcurrencyResourceType**：資料移動作業所產生的等候。
* **BackupConcurrencyResourceType**：此等候指出正在備份資料庫。 hello 這個資源類型的最大值為 1。 如果已經在 hello 要求多個備份相同的時間，其他人會排入佇列的 hello。

hello `sys.dm_pdw_waits` DMV 可以是使用的 toosee 要求正在等候的資源。

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

hello `sys.dm_pdw_resource_waits` DMV 顯示只有 hello 資源等候由給定的查詢。 資源等候時間僅會測量等候所提供的資源 toobe hello 時間，因為相對於的 toosignal 等候時間，這就是 hello 時間花費 hello 基礎 SQL 伺服器 tooschedule hello 查詢到 hello CPU。

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

hello `sys.dm_pdw_wait_stats` DMV 可用來等候的歷史趨勢分析。

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>後續步驟
如需管理資料庫使用者和安全性的詳細資訊，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。 如何在較大的資源類別的詳細資訊，可改進叢集資料行存放區索引的品質，請參閱[重建索引 tooimprove 區段品質]。

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[重建索引 tooimprove 區段品質]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
