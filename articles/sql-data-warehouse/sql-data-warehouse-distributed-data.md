---
title: "aaaHow 分散式 Azure SQL 資料倉儲中的資料運作 |Microsoft 文件"
description: "了解如何將資料分佈的大量平行處理 (MPP) 和 hello 散發在 Azure SQL 資料倉儲和平行處理資料倉儲中的資料表選項。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>大量平行處理 (MPP) 的分散式資料和分散式資料表
了解如何在 Microsoft 的大量平行處理 (MPP) 系統 Azure SQL 資料倉儲和平行資料倉儲中分散使用者資料。 設計您的資料倉儲 toouse 分散式的資料實際上會幫助您 tooachieve hello 查詢處理 hello MPP 架構的優點。 一些資料庫設計選擇可能會嚴重影響改善查詢效能。  

> [!NOTE]
> Azure SQL 資料倉儲和 Parallel Data Warehouse 使用 hello 相同大量平行處理 (MPP) 設計，但是有一些差異，因為基礎平台的 hello。 SQL 資料倉儲是一種在 Azure 上執行的平台即服務 (PaaS)。 平行資料倉儲在分析平台系統 (AP) 上執行，也就是在 Windows Server 上執行的內部部署應用裝置。
> 
> 

## <a name="what-is-distributed-data"></a>什麼是分散式資料？
在 SQL 資料倉儲和平行處理資料倉儲中，分散式的資料是指 toouser hello MPP 系統跨多個位置中儲存的資料。 每個位置做為獨立的存放裝置和其部份 hello 資料執行查詢的處理單位。 分散式的資料是基本 toorunning 平行 tooachieve 高的查詢效能的查詢。

toodistribute 資料 hello 資料倉儲將指派的使用者資料表 tooone 分散式位置的每個資料列。  您可以使用雜湊發佈方法或循環配置資源方法來散發資料表。 hello CREATE TABLE 陳述式中指定 hello 發佈方法。 

## <a name="hash-distributed-tables"></a>雜湊分散式資料表
hello 下列圖表說明如何執行完整 （非分散式資料表） 取得儲存為雜湊散發資料表。 具決定性的函式會指派每個資料列 toobelong tooone 散發。 在 hello 資料表定義中，其中一個 hello 資料行指定為 hello 散發資料行。 hello 雜湊函式會使用每個資料列 tooa 散發 hello 散發資料行 tooassign 中的 hello 值。

有 hello 散發資料行，例如區分、 資料扭曲和 hello hello 系統上執行的查詢類型的選取範圍的效能考量。

![分散式資料表](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "分散式資料表")  

* 每個資料列所屬 tooone 發佈。  
* 具決定性的雜湊演算法會指定每個資料列 tooone 散發。  
* hello 不同大小的表格所示，每個發佈的資料表資料列的 hello 數目而異。

## <a name="round-robin-distributed-tables"></a>循環配置資源分散式資料表
循環配置資源的分散式的資料表會以循序方式指派每個資料列 tooa 散發發佈 hello 資料列。 將資料快速 tooload 到循環配置資源資料表，但查詢效能可能會變慢。  通常將循環配置資源資料表需要改組 hello 列 tooenable hello 查詢 tooproduce 精確的結果，花的時間。

## <a name="distributed-storage-locations-are-called-distributions"></a>分散式儲存體位置稱為發佈
每個分散式位置稱為發佈。 查詢會以平行方式執行，每個發佈將其部分 hello 資料上執行 SQL 查詢。 SQL 資料倉儲會使用 SQL Database toorun hello 查詢。 平行處理資料倉儲會使用 SQL Server toorun hello 查詢。 這種無共用架構設計是向外延展基本 tooachieving 平行計算。

### <a name="can-i-view-hello-distributions"></a>可以檢視 hello 散發嗎？
每個散發散發識別碼，而且會顯示在系統檢視表的相關 tooSQL 資料倉儲和平行資料倉儲中。 您可以使用 hello 發佈識別碼 tootroubleshoot 查詢效能和其他問題。 如需 hello 系統檢視表的清單，請參閱 hello [MPP 系統檢視表](sql-data-warehouse-reference-tsql-statements.md)。

## <a name="difference-between-a-distribution-and-a-compute-node"></a>發佈與計算節點之間的差異
分佈是 hello 基本單位，來儲存分散式的資料及處理平行查詢。 發佈會群組為計算節點。 每個計算節點會追蹤一或多個發佈。  

* Analytics Platform System hello 硬體架構和向外延展功能的中央元件使用的計算節點。 雜湊散發資料表的 hello 圖表所示，它一定會使用每個計算節點的八個分佈。 hello 的運算節點數目，並因此 hello 的分佈數目，取決於您購買的 hello 應用裝置的運算節點的 hello 數目。 例如，如果您購買八個計算節點，您會取得 64 個發佈 (8 個計算節點 x 8 個發佈/節點)。 
* SQL 資料倉儲的發佈數目固定為 60 個，而計算節點數目則為彈性。 使用 Azure 運算和儲存體資源來實作 hello 計算節點。 相應 toohello 後端服務工作負載和 hello 運算容量 (Dwu) 您指定 hello 資料倉儲，就可以變更 hello 的運算節點數目。 當 hello 的運算節點的數目變更時，每個計算節點的 hello 數目也會變更。 

### <a name="can-i-view-hello-compute-nodes"></a>可以檢視 hello 計算節點嗎？
每個計算節點有節點識別碼，並顯示在系統檢視表的相關 tooSQL 資料倉儲和平行資料倉儲。  您可以看到 hello 計算節點的名稱開頭為 sys.pdw_nodes 系統檢視表中的 hello node_id 資料行。 如需 hello 系統檢視表的清單，請參閱 hello [MPP 系統檢視表](sql-data-warehouse-reference-tsql-statements.md)。

## <a name="Replicated"></a>複寫資料表
複寫資料表有完全 hello 資料表的副本儲存在每個計算節點。 複寫資料表中移除計算節點，然後再聯結或彙總之間的 hello 需要 tootransfer 資料。 複寫的資料表才可行小型資料表與 hello 因為每個計算節點上的額外的儲存體需要的 toostore hello 完整資料表。  

hello 下列圖表顯示複寫的資料表儲存在每個計算節點上。 對於 SQL 資料倉儲、 hello 複寫的資料表會是每個計算節點上的完整複製的 tooa 散發資料庫。 Parallel Data Warehouse hello 複寫的資料表會儲存在指派 toohello 計算節點的所有磁碟。  此磁碟策略會使用 SQL Server 檔案群組來實作。  

![複寫的資料表](media/sql-data-warehouse-distributed-data/replicated-table.png "複寫的資料表") 

## <a name="next-steps"></a>後續步驟
分散式 toouse 資料表有效，請參閱[散發 SQL 資料倉儲中的資料表](sql-data-warehouse-tables-distribute.md)  

