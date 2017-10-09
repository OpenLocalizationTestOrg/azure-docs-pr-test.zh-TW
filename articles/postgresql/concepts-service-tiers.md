---
title: "aaa\"Azure PostgreSQL 資料庫中的定價層\""
description: "適用於 PostgreSQL 的 Azure 資料庫中的定價層"
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: article
ms.date: 05/31/2017
ms.openlocfilehash: f10389dd2ad1ff04e83b02786a407c10140a007b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>適用於 PostgreSQL 的 Azure 資料庫選項和效能：了解每個定價層中可用的項目
當您建立 Azure Database PostgreSQL 伺服器時，您決定選擇三個主要 tooconfigure hello 資源配置給該伺服器。 這些選項會影響 hello 效能和延展性的 hello 伺服器。
- 定價層 
- 計算單位
- 儲存體 (GB)

每個定價層會有多種效能層級 （計算的單位） toochoose，根據您的工作負載的需求。 較高的效能層級提供額外資源，為您伺服器設計的 toodeliver 較高的輸送量。 您可以變更在幾乎任何應用程式停機時間的定價層中的 hello 伺服器的效能層級。

> [!IMPORTANT]
> 雖然 hello 服務處於公開預覽狀態，並不保證的服務等級協定 (SLA)。

在適用於 PostgreSQL 的 Azure 資料庫內，您可以擁有一個或多個資料庫。 您可以選擇單一資料庫，每個伺服器 tooutilize toocreate 所有 hello 資源，或建立多個資料庫 tooshare hello 資源。 

## <a name="choose-a-pricing-tier"></a>選擇定價層
在預覽版中，適用於 PostgreSQL 的 Azure 資料庫提供兩個定價層︰基本和標準。 進階層目前尚無法使用，但即將推出。 

hello 下表提供 hello 定價層適用於不同的應用程式工作負載的最佳的範例。

| 定價層  | 目標工作負載 |
| :----------- | :----------------|
| 基本 | 最適合需要可調整計算和儲存體而不需 IOPS 保證的小型工作負載。 範例包括用於開發或測試的伺服器，或者不常使用的小規模應用程式。 |
| 標準 | hello go-toooption 雲端需要 IOPS 的應用程式保證其高輸送量。 範例包括 Web 或分析應用程式。 |
| 進階 | 最適合需要為交易和 IO 提供低延遲的工作負載。 提供許多並行使用者 hello 最佳支援。 適用於 toodatabases 支援關鍵任務應用程式。<br />無法在預覽中使用 hello Premium 定價層。 |

toodecide 上的定價層所決定，如果您的工作負載需要 IOPS 保證初次啟動。 如果需要，請使用標準定價層。

| **定價層功能** | **基本** | **標準** |
| :------------------------ | :-------- | :----------- |
| 計算單位數目上限 | 100 | 800 | 
| 總儲存體上限 | 1 TB | 1 TB | 
| 儲存體 IOPS 保證 | N/A | 是 | 
| 儲存體 IOPS 上限 | N/A | 3,000 | 
| 資料庫備份的保留期限 | 7 天 | 35 天 | 

在 hello 預覽時間範圍內，一旦建立 hello 伺服器時，無法變更定價層。 在未來的 hello，它將會是可能 tooupgrade 或降級伺服器，一個定價層 tooanother 層。

## <a name="understand-hello-price"></a>了解 hello 價格
當您建立新的 Azure 資料庫的 PostgreSQL 內 hello [Azure 入口網站](https://portal.azure.com/#create/Microsoft.PostgreSQLServer)，按一下 hello**定價層**刀鋒視窗中和每月成本 hello 會顯示根據您所選取的 hello 選項。 如果您沒有 Azure 訂用帳戶，請使用 hello Azure 定價計算機 tooget 預估價格。 造訪 hello [Azure 定價計算機](https://azure.microsoft.com/pricing/calculator/)網站，然後按一下 **加入項目**，展開 hello**資料庫**分類中，選擇  **Azure 資料庫PostgreSQL** toocustomize hello 選項。

## <a name="choose-a-performance-level-compute-units"></a>選擇效能等級 (計算單位)
一旦您決定 hello PostgreSQL 伺服器的 Azure 資料庫的定價層，您就準備好 toodetermine hello 效能層級選取所需的計算單位的 hello 數目。 對於其 Web 或分析工作負載需要更高使用者並行處理的應用程式而言，200 或 400 個計算單位會是很好的起點。 

計算的單位包括量值的 CPU 處理輸送量保證 toobe 可用 tooa PostgreSQL 伺服器將單一 Azure 資料庫。 計算單位是 CPU 和記憶體資源的混合量值。  如需詳細資訊，請參閱[說明計算單位](concepts-compute-unit-and-storage.md)

### <a name="basic-pricing-tier-performance-levels"></a>基本定價層效能等級：

| **效能等級** | **50** | **100** |
| :-------------------- | :----- | :------ |
| 計算單位數目上限 | 50 | 100 |
| 內含的儲存體大小 | 50 GB | 50 GB |
| 伺服器儲存體大小上限\* | 1 TB | 1 TB |

### <a name="standard-pricing-tier-performance-levels"></a>標準定價層效能等級：

| **效能等級** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| 計算單位數目上限 | 100 | 200 | 400 | 800 |
| 內含的儲存體大小和已佈建的 IOPS | 125 GB、<br/> 375 IOPS | 125 GB、<br/> 375 IOPS | 125 GB、<br/> 375 IOPS | 125 GB、<br/> 375 IOPS |
| 伺服器儲存體大小上限\* | 1 TB | 1 TB | 1 TB | 1 TB |
| 伺服器佈建的 IOPS 上限 | 3,000 IOPS | 3,000 IOPS | 3,000 IOPS | 3,000 IOPS |
| 每個 GB 中伺服器佈建的 IOPS 上限 | 每個 GB 中固定 3 IOPS | 每個 GB 中固定 3 IOPS | 每個 GB 中固定 3 IOPS | 每個 GB 中固定 3 IOPS |

\*伺服器儲存體大小上限是指 toohello 佈建儲存體大小上限，為您的伺服器。

## <a name="storage"></a>儲存體 
hello 儲存體組態會定義 hello PostgreSQL 伺服器的儲存體容量可用 tooan Azure 資料庫的數量。 hello hello 服務所使用的儲存體包含 hello 資料庫檔案、 交易記錄檔和 hello PostgreSQL 伺服器記錄檔。 考慮 hello 大小所需的儲存體 toohost 您的資料庫和 hello 選取 hello 存放裝置設定時的效能需求 (IOPS)。

某些儲存容量與每個定價層中，記下 hello 之前為 「 包含儲存體大小 」 資料表中包含最小值 建立 hello 伺服器時，為增量來 125 GB，toohello 最大允許的存放裝置，可以加入額外的存放裝置容量。 hello 額外的存放裝置容量可以獨立 hello 計算單位組態設定。 根據選取的儲存體的 hello 數量 hello 價格變更。

每個效能層級中的 hello IOPS 組態相關 toohello 定價層和 hello 選擇的儲存體大小。 基本層不提供 IOPS 保證。 在標準定價層 hello，hello IOPS 比例 toomaximum 儲存體大小固定 3:1 比例。 375 125 GB 保證的 hello 包含儲存體佈建各有向上 too256 KB 的 IO 大小的 IOPS。 您可以選擇 too1 TB 的最大值向上額外的存放裝置、 tooguarantee 3000 佈建的 IOPS。

監視 hello 中 hello Azure 入口網站或寫入 Azure CLI 命令 toomeasure hello 耗用量的儲存體和 IOPS 的度量圖表。 相關的度量 toomonitor 是儲存空間限制、 儲存體百分比、 儲存空間使用，以及 IO 百分比。

>[!IMPORTANT]
> 在 預覽中，儲存體數量 hello 次選擇 hello hello 伺服器建立時。 尚不支援變更現有的伺服器上的 hello 儲存體大小。 

## <a name="scaling-a-server-up-or-down"></a>相應增加或減少伺服器
您一開始選擇定價層和效能層級，當您建立您的 Azure 資料庫 PostgreSQL hello。 稍後，您可以調整計算單位向上或向下，以動態方式 hello hello 範圍內相同的 hello 定價層。 在 hello Azure 入口網站、 滑動 hello 計算單位 hello 伺服器的定價層 刀鋒視窗，或其撰寫指令碼的下一個範例：[監視器和調整規模單一 PostgreSQL 伺服器使用 Azure CLI](scripts/sample-scale-server-up-or-down.md)

調整 hello 計算的單位是完成與您選擇的 hello 最大儲存體大小無關。

Hello 幕後變更 hello 資料庫效能層級在 hello 新效能層級建立 hello 原始資料庫的複本，然後將連接切換 toohello 複本。 此程序期間不會遺失任何資料。 在 hello 暫時當我們切換 toohello 複本時，會停用 toohello 資料庫的連接，所以在途中有些交易可能復原。 這個時間範圍會有不同，但平均在 4 秒下，而且超過 99% 的案例少於 30 秒。 如果有大型交易傳送 hello 目前連線的數字會停用，此視窗可能是較長。

hello hello 整個小數位數的程序的持續時間取決於 hello 大小和 hello 伺服器之前，以及之後 hello 變更定價層。 比方說，變更計算的單位內 hello 標準定價層，伺服器應該幾分鐘內完成。 hello 變更完成之前，不會套用 hello 伺服器 hello 新內容。

## <a name="next-steps"></a>後續步驟
- 如需計算單位的詳細資訊，請參閱[說明計算單位](concepts-compute-unit-and-storage.md)
- 了解如何太[監視器和調整規模單一 PostgreSQL 伺服器使用 Azure CLI](scripts/sample-scale-server-up-or-down.md)
