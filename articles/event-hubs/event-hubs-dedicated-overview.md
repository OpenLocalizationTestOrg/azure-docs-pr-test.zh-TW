---
title: "Azure 事件中心專用容量的 aaaOverview |Microsoft 文件"
description: "Microsoft Azure 事件中樞專用容量概觀。"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 79c09975e5c0a6d4729c8f836576770abaaf322e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>事件中樞專用的概觀

*事件中心專用*容量提供單一租用戶部署的 hello 與客戶最嚴苛的需求。 完整大規模 Azure 事件中心可以輸入秒 （含） 以上的完全持久的儲存體和秒延遲遙測秒 too2 GB 過去 2 百萬個事件。 這也可讓整合式的解決方案藉由處理即時和批次上的 hello 相同的系統。 事件中心封存包含在 hello 供應項目，您可以減少 hello 複雜度，您的方案具有單一資料流支援即時和批次為基礎的管線。

hello 下表比較事件中心的 hello 可用的服務層。 hello 事件中心專用供應項目是固定的每月價格，比較 toousage 定價大部分的標準和基本的功能。 hello 專用的層提供 hello 功能 hello 標準方案，但是企業規模容量嚴苛的工作負載的客戶。 

| 功能 | 基本 | 標準 | 專用 |
| --- |:---:|:---:|:---:|
| 輸入事件 | 按百萬個事件付費 | 按百萬個事件付費 | 已包括 |
| 輸送量單位 (每秒 1 MB 輸入，每秒 2 MB 輸出) | 按小時付費 | 按小時付費 | 已包括 |
| 訊息大小 | 256 KB | 256 KB | 1 MB |
| 發行者原則 | N/A | 是 | 是 |     
| 用戶群組 | 1 - 預設值 | 20 | 20 |
| 訊息重播 | 是 | 是 | 是 |
| 最大輸送量單位 | 20 | 20 (彈性 too100)  | 1 CU≈200 |
| 代理連線 | 包含 100 個 | 包含 1,000 個 | 包含 10 萬個 |
| 其他代理連線 | N/A | 是 | 是 |
| 訊息保留期 | 含 1 天 | 含 1 天 | Too7 天最多包含 |
| 封存  (預覽版) | N/A   | 按小時付費 | 已包括 |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>事件中樞專用容量的優點

使用專用的事件中樞時，可以使用 hello 下列優點：

* 使用單一租用戶裝載，不會受到其他租用戶的干擾。
* 相較，大小會增加 too1 MB 的訊息標準 」 與 「 基本 too256 KB。
* 可重複每次效能。
* 保證您高載需要的容量 toomeet。
* 可擴充的介於 1 到 8 的容量單位 (CU) – 提供每秒 too2 百萬個輸入事件。
  * 自訂管理事件中心專用的其中每個 CU 可提供約 200 個輸送量單位 (TU) 的 hello 對等的 hello 小數位數。
* 零維護：負載平衡、作業系統更新、安全性修補程式及資料分割都由我們管理。
* 每月價格固定。

事件中心專用也會移除某些 hello 輸送量限制的 hello 標準提供項目。 在基本和標準層的輸送量單位贊成 too1000 事件每第二個或 1 MB 每秒的輸入每個 TU 和 double 該數量的輸出。 hello 專用的標尺供應項目都沒有限制的輸入和輸出事件會計算。 這些限制只受到 hello 處理 hello 購買事件中心的容量。

此服務為目標的最大遙測使用者 hello，可用 toocustomers 與 enterprise 合約。

## <a name="how-tooonboard"></a>如何 tooonboard

透過 enterprise 合約具有不同大小的自訂提供 hello 事件中心專用平台。 每個 CU 提供約 200 個輸送量單位的 hello 對等。 您可以調整您的容量向上或向下整個 hello 月份 toomeet 您的需要新增或移除自訂。 hello 專用計劃是唯一的就會發生更實用的入門訓練從 hello 事件中心產品小組 tooget hello 彈性的部署，最適合您。 

## <a name="next-steps"></a>後續步驟
請連絡您的 Microsoft 業務代表或 Microsoft 支援服務 tooget 其他詳細資料事件中心專用的容量。 您也可以瀏覽下列連結查看 hello 了有關事件中心的詳細資訊：

如需定價的詳細資訊，請造訪下列連結查看 hello:

- [事件中樞專用價格](https://azure.microsoft.com/pricing/details/event-hubs/)。 您也可以連絡您的 Microsoft 業務代表或 Microsoft 支援服務 tooget 其他詳細資料事件中心專用的容量。
- hello[事件中心常見問題集](event-hubs-faq.md)包含定價資訊，並回答一些常見問題的相關事件中心。 
