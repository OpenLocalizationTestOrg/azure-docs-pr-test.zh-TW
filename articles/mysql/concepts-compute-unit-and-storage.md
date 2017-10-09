---
title: "說明適用於 MySQL 的 Azure 資料庫中的計算單位 | Microsoft Docs"
description: "用於 MySQL 的 azure DB： 本文件說明計算單位，與您的工作負載達到時，會發生什麼情況的 hello 概念 hello 最大的計算單位。"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 751b4fff2760e55565e2bc80d49db17a57397779
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-mysql"></a>說明適用於 MySQL 的 Azure 資料庫中的計算單位
本文說明的計算單位 hello 概念和工作負載達到 hello 計算的最大單位時，會發生什麼事。

## <a name="what-are-compute-units"></a>什麼是計算單位？
計算的單位包括量值的 CPU 處理輸送量保證 toobe 可用 tooa 單一 Azure 資料庫的 MySQL 伺服器。 計算單位是 CPU 和記憶體資源的混合量值。 一般來說，50 個計算的單位等同於 toohalf 的核心。 100 為計算單位等同於 tooone 核心。 2000 計算單位等同於 tootwenty 核心的保證的處理輸送量 tooyour 可用伺服器。

hello 每個計算的單位的記憶體數量最適合用於 hello 基本及標準定價層。 Hello 效能層級增加加倍 hello 計算單位等同資源可用 toothat toodoubling hello 組 MySQL 將單一 Azure 資料庫。

例如，標準的 800 個計算單位所提供的 CPU 輸送量與記憶體，比標準的 100 個計算單位設定多 8 倍。 相同但是 hello 標準 100 計算單位是提供 CPU 輸送量比較 tooBasic 100 計算單位，hello 已預先設定的標準定價層中的記憶體數量為 double hello 的定價層的基本設定的記憶體的數量。 因此，標準定價層提供更好的工作負載效能且比基本定價層，以選取計算的單位相同的 hello 的交易延遲更低。

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a>如何判斷我的工作負載所需的計算單位的 hello 數目？
如果您要尋找 toomigrate 在內部部署執行現有的 MySQL 伺服器或虛擬機器上，您可以透過評估的處理輸送量多少核心您的工作負載需要判斷 hello 計算的單位數目。 

如果您現有的內部部署或虛擬機器伺服器目前使用 4 個核心 (不含計算 CPU 超執行緒)，一開始請為適用於 MySQL 伺服器的 Azure 資料庫設定 400 個計算單位。 計算單位可根據您的工作負載需求，動態地相應增加或減少，而且幾乎不會產生任何應用程式停機時間。 

在 Azure 入口網站或寫入 Azure CLI 命令-toomeasure hello 監視器 hello 度量圖表會計算單位。 相關的度量 toomonitor 為 hello 計算單位百分比和計算的單位的限制。

>[!IMPORTANT]
> 如果您發現儲存體 IOPS 不完全利用 toohello 最大值，請考慮監視 hello 運算單位使用率以及。 引發 hello 計算的單位可能會允許 IO 輸送量因而 hello 到期 toolimited CPU 或記憶體的效能瓶頸。

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>當我達到計算單位上限時會發生什麼狀況？
效能層級制定和控管 tooprovide 資源 toorun 資料庫工作負載向上 toohello hello 選取的定價層和效能層級的最大限制。 

如果您的工作負載達到 hello 最大限制是 hello 計算單位或佈建的 IOPS 限制，您可以繼續 tooutilize hello 資源在 hello 最大的允許層級，但您的查詢很有可能 toosee 增加延遲。 這些限制不會導致任何錯誤，但而是會降低 hello 工作負載，除非 hello 緩慢的問題變成嚴重的查詢逾時。 

如果您的工作負載達到 hello 最大連接數目限制，會引發明確的錯誤。 如需資源限制的詳細資訊，請參閱[適用於 MySQL 的 Azure 資料庫中的限制](concepts-limits.md)。

## <a name="next-steps"></a>後續步驟
如需定價層的詳細資訊，請參閱[適用於 MySQL 的 Azure 資料庫定價層](./concepts-service-tiers.md)。
