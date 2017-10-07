---
title: "aaaThreats-Microsoft 威脅模型化工具-Azure |Microsoft 文件"
description: "威脅 [類別目錄] 頁面上，hello Microsoft 威脅模型化工具，包含所有公開的類別產生的威脅。"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a>Microsoft 威脅模型化工具威脅

hello 威脅模型化工具是 Microsoft 安全性開發週期 (SDL) hello 的核心項目。 它可讓軟體架構設計人員 tooidentify 和時，它們相當容易、 更符合成本效益 tooresolve 早期減輕潛在的安全性問題。 如此一來，它可大幅減少開發 hello 總成本。 此外，我們會與非安全性專家納入考量，方便威脅分析模型的所有開發人員藉由提供清楚的指引，建立和分析威脅模型設計 hello 工具。

> 請瀏覽 hello **[威脅模型化工具](./azure-security-threat-modeling-tool.md)** tooget 立即開始使用 ！

hello 威脅模型化工具可協助您回答某些問題，例如 hello 下面項目：

* 攻擊者可以如何變更 hello 驗證資料？
* 什麼是 hello 影響，如果攻擊者可以讀取 hello 使用者設定檔資料？
* 如果 toohello 使用者設定檔資料庫拒絕存取會怎樣？

## <a name="stride-model"></a>STRIDE 模型

toobetter 協助您制定這幾種指標的問題，Microsoft 會使用 hello STRIDE 模型來分類不同類型的威脅，並簡化 hello 整體安全性的交談。

| 類別 | 說明 |
| -------- | ----------- |
| **詐騙** | 涉及非法存取然後使用其他使用者的驗證資訊，例如使用者名稱和密碼 |
| **竄改** | 牽涉到 hello 惡意修改資料。 範例包括未經授權的變更 toopersistent 資料，例如開啟網路，例如 hello 網際網路上的兩部電腦之間流動時加以保留在資料庫和 hello 改變的資料 |
| **否認性** | 拒絕執行動作，而不需要任何方式 tooprove 否則其他合作對象的使用者相關聯 — 例如，使用者會執行不合法的操作缺少 hello 能力 tootrace hello 禁止作業的系統。 不可否認性是指系統 toocounter 不可否認性威脅 toohello 能力。 例如，使用者購買項目可能 toosign 收到 hello 項目。 hello 廠商可以接著使用 hello 做為該 hello 使用者未收到 hello 套件的辨識項簽署回條 |
| **資訊洩漏** | 牽涉到 hello 暴露資訊 tooindividuals 洩露 toohave 存取 tooit — 比方說，使用者 tooread 它們未檔案 hello 能力授與存取權，或 hello 入侵者 tooread 傳輸中資料的兩部電腦之間的功能 |
| **阻斷服務** | 阻絕服務 (DoS) 攻擊拒絕服務 toovalid 使用者 — 例如，藉由網頁伺服器暫時無法使用或無法使用。 您必須防止某些類型的 DoS 威脅只要 tooimprove 系統可用性和可靠性 |
| **權限提高** | 無特殊權限的使用者取得授權的存取，並藉此有足夠的存取 toocompromise 或損毀 hello 整個系統。 提高權限威脅包括這些情況，攻擊者具有有效地滲入所有系統防禦，以及會成為受信任的 hello 系統本身，危險的狀況，以確實的一部分 |

## <a name="next-steps"></a>後續步驟

繼續太**[威脅模型化工具降低](./azure-security-threat-modeling-tool-mitigations.md)** toolearn hello 不同的方式可以減輕這些威脅與 Azure。
