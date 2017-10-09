---
title: "關於 Azure SQL 資料倉儲作業 aaaLearn |Microsoft 文件"
description: "SQL 資料倉儲的彈性可讓您以滑動的方式調整資料倉儲單位 (DWU)，來增加、縮減或暫停計算能力。 本文說明 hello 資料倉儲度量資訊，以及如何彼此 tooDWUs。 "
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: cadffa9c-589d-4db7-888a-1f202a753bc5
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 8be5ff6b14ab907e2b0a7eb55e0e2f4139aca8b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-workload"></a>資料倉儲工作負載
資料倉儲工作負載是指 tooall 的 hello 經過對資料倉儲的作業。 hello 資料倉儲工作負載包含 hello 倉儲將資料載入、 執行分析和報告 hello 資料倉儲、 管理 hello 資料倉儲中的資料和 hello 資料倉儲的資料匯出的 hello 整個程的序。 hello 深度和廣度的這些元件通常是 parallel hello 資料倉儲的 hello 成熟度層級。

## <a name="new-toodata-warehousing"></a>新 toodata 倉儲？
資料倉儲是從一個載入之資料的集合或更多的資料來源，而且是使用的 tooperform，例如報告和資料分析的商業智慧工作。

資料倉儲的特性在於查詢掃描較大的數字的資料列，大範圍的資料，且可能傳回 hello 基於相對較大的結果的分析和報告。 與小量交易層級的插入/更新/刪除作業相比，可載入相對大量的資料，也是資料倉儲的特點。

* Hello 資料會儲存在可最佳化使用需要大量的資料列 tooscan 或大範圍的資料的查詢方法時，資料倉儲的執行效果最好。 這種類型的掃描最適合儲存和資料列所搜尋的資料行，而不是 hello 資料時。

> [!NOTE]
> hello 記憶體中資料行存放區索引，使用資料行存放區，提供 too10x 壓縮提升和 100 倍查詢效能提升透過傳統的二進位樹狀目錄的報告和分析查詢。 我們將資料行存放區索引視為 hello 標準儲存與掃描大型資料倉儲中的資料。
> 
> 

* 資料倉儲和最佳化線上交易處理 (OLTP) 系統各有不同的需求。 hello OLTP 系統有許多插入、 更新和刪除作業。 這些作業搜尋 toospecific hello 資料表中的資料列。 資料表搜尋時 hello 資料會以逐列方式儲存具有最佳。 hello 資料可以排序和搜尋與除以迅速征服方法稱為二進位樹狀目錄或 btree 的搜尋。

## <a name="data-loading"></a>載入資料
資料載入大屬於 hello 資料倉儲工作負載。 企業通常會有忙線中的 OLTP 系統追蹤整天 hello 當客戶所產生的商務交易的變更。 定期，通常在晚上在維護期間，hello 交易移動或複製 toohello 資料倉儲。 一旦 hello 資料 hello 資料倉儲中，分析師就可以執行分析，並做出商業決策 hello 資料。

* 傳統上，hello 的程序載入稱為 ETL 的擷取、 轉換及載入。 資料通常需要 toobe 轉換，因此它是與 hello 資料倉儲中的其他資料一致。 先前，企業會使用專用的 ETL 伺服器 tooperform hello 轉換。 現在，這類快速大量平行處理與您可以在第一次，將資料載入 SQL 資料倉儲，然後再執行 hello 轉換。 此程序稱為解壓縮、 載入和轉換 (ELT)，並已成為新的標準 hello 資料倉儲工作負載。

> [!NOTE]
> 現在，使用 SQL Server 2016 就能即時在 OLTP 資料表上執行分析。 這不會不會取代資料倉儲 toostore hello 需要和分析資料，但是它提供即時的方式 tooperform 分析。
> 
> 

### <a name="reporting-and-analysis-queries"></a>報告和分析查詢
報告和分析查詢通常會根據幾個條件分成小型、中型和大型，但通常是根據時間。 大部分的資料倉儲中，還有混合快速執行與長時間執行查詢的工作負載。 在各種情況下，很重要的 toodetermine 此混合和 toodetermine 它的頻率 （每小時、 每日、 月份結束，季結束時，依此類推）。 Hello 混合式的查詢工作負載，結合的並行存取，負責人 tooproper 容量規劃的資料倉儲的重要 toounderstand 它。

* 容量規劃特別是當您需要很長的前置時間 tooadd 容量 toohello 資料倉儲時，才可以是混合式的查詢工作負載的複雜工作。 SQL 資料倉儲移除 hello 的容量規劃的急迫性，因為您可以擴大及縮減計算容量，在任何時間，而由於儲存體和計算容量獨立地調整大小。

### <a name="data-management"></a>資料管理
管理資料是很重要，特別是當您知道您可能會用完磁碟空間接近未來 hello。 資料倉儲通常會分割成有意義的範圍，會儲存為資料分割資料表中的 hello 資料。 所有 SQL Server 為基礎的產品可都讓您將移入和移出 hello 資料表的資料分割。 此資料分割切換可讓您移動較舊資料 tooless 昂貴的儲存體，將 hello 可用的最新資料保留在線上的儲存體上。

* 資料行存放區索引可支援經分割的資料表。 資料行存放區索引會使用經分割的資料表來管理和保存資料。 對於逐列儲存的資料表而言，資料分割在查詢效能方面的角色較為吃重。  
* PolyBase 在管理資料方面扮演著重要角色。 使用 PolyBase，您必須 hello 選項 tooarchive 較舊資料 tooHadoop 或 Azure blob 儲存體。  由於 hello 資料會仍在線上，這會提供更多的選項。  可能需要較長的 tooretrieve 資料從 Hadoop，但 hello 權衡取捨的擷取時間可能遠大於 hello 儲存體成本。

### <a name="exporting-data"></a>匯出資料
可用的報表和分析的其中一種方式 toomake 資料是 toosend hello 資料倉儲 tooservers 專用於執行報表和分析資料。 這些伺服器稱為資料市集。 比方說，您無法預先處理報表資料，並再將其從 hello 資料倉儲 toomany 全球伺服器 hello，toomake 客戶和分析師廣泛受到使用它。

* 產生報告，每晚您無法填入唯讀快照集的 hello 每日資料的報表伺服器。 較高的頻寬客戶提供同時降低 hello 資料倉儲上的 hello 運算資源需求。 安全性層面，從資料超市可讓您的使用者具有存取 toohello 資料倉儲的 tooreduce hello 數。
* 進行分析，您可以建立 hello 資料倉儲上的分析 cube 和 hello 資料倉儲中，針對執行分析或前置處理資料並將它匯出 toohello analysis server 進行進一步分析。

## <a name="next-steps"></a>後續步驟
既然您稍微了解 SQL 資料倉儲，了解如何 tooquickly[建立 SQL 資料倉儲][ create a SQL Data Warehouse]和[範例資料載入][load sample data]。

<!--Image references-->

<!--Article references-->
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md

<!--MSDN references-->

<!--Other web references-->
