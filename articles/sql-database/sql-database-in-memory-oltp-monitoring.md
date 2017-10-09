---
title: "aaaMonitor XTP 記憶體中儲存體 |Microsoft 文件"
description: "估計和監視 XTP 記憶體內儲存體使用量、容量；解決容量錯誤 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>監視記憶體內部 OLTP 儲存體
使用 [記憶體內部 OLTP](sql-database-in-memory.md)時，記憶體最佳化資料表中的資料和資料表變數位於記憶體內部 OLTP 儲存體中。 每個 Premium 服務層有記憶體中 OLTP 儲存體大小上限，而其記錄在 hello [SQL Database 服務層文章](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)。 一旦超過此限制，插入和更新作業可能會開始出錯 (錯誤碼 41823)。 此時，您將會需要 tooeither 刪除 tooreclaim 記憶體資料，或升級資料庫的 hello 效能層。

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>判斷資料是否可容納 hello 記憶體中儲存體端點
判斷 hello 儲存體端點： 請參閱 hello [SQL Database 服務層的發行項](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)的 hello hello 不同 Premium 服務層的儲存體大寫字。

預估記憶體需求的記憶體最佳化資料表運作的 hello 相同未在 Azure SQL Database for SQL Server 的方式一樣。 花幾分鐘的時間 tooreview 該主題[MSDN](https://msdn.microsoft.com/library/dn282389.aspx)。

請注意，hello 資料表和資料表變數的資料列，以及索引，會計入 hello 最大使用者資料的大小。 另外，ALTER TABLE 需要足夠的空間 toocreate hello 整個資料表和索引的新版本。

## <a name="monitoring-and-alerting"></a>監視和警示
您可以監視記憶體中儲存體使用的 hello 百分比[效能層的儲存體端點](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)hello Azure 中[入口網站](https://portal.azure.com/): 

* 在 hello 資料庫刀鋒視窗中，找出 hello 資源使用率方塊並按一下編輯。
* 然後選取 hello 度量`In-Memory OLTP Storage percentage`。
* tooadd 警示，hello 資源使用率方塊 tooopen hello 計量刀鋒視窗中，按一下，然後按一下 新增警示。

或使用下列查詢 tooshow hello 記憶體中儲存體使用率的 hello:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>更正記憶體不足情況 - 錯誤 41823
記憶體不足導致插入、更新和建立作業失敗，並出現錯誤訊息 41823。

錯誤訊息 41823 表示 hello 記憶體最佳化資料表和資料表變數已經超過最大值 hello。

tooresolve 這個錯誤，可能是：

* 刪除資料中的 hello 記憶體最佳化資料表，可能會卸載 hello 資料 tootraditional、 以磁碟為基礎的資料表。或者，
* 升級 hello 服務層 tooone 具有足夠記憶體中的儲存體 hello 資料中，您需要 tookeep 記憶體最佳化資料表中的。

## <a name="next-steps"></a>後續步驟
如需監視指引，請參閱[使用動態管理檢視監視 Azure SQL Database](sql-database-monitoring-with-dmvs.md)。
