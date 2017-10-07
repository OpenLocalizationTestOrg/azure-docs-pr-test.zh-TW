---
title: "aaaMitigations-Microsoft 威脅模型化工具-Azure |Microsoft 文件"
description: "Hello Microsoft 威脅模型化工具反白顯示可能的解決方案 toohello 最公開的安全防護功能頁面上產生潛在威脅。"
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
ms.openlocfilehash: 000c0980d976b09fc9287e582e3776efaf7e390c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-mitigations"></a>Microsoft 威脅模型化工具風險降低

hello 威脅模型化工具是 Microsoft 安全性開發週期 (SDL) hello 的核心項目。 它可讓軟體架構設計人員 tooidentify 和時，它們相當容易、 更符合成本效益 tooresolve 早期減輕潛在的安全性問題。 如此一來，它可大幅減少開發 hello 總成本。 此外，我們會與非安全性專家納入考量，方便威脅分析模型的所有開發人員藉由提供清楚的指引，建立和分析威脅模型設計 hello 工具。

請瀏覽 hello **[威脅模型化工具](./azure-security-threat-modeling-tool.md)** tooget 立即開始使用 ！

## <a name="mitigation-categories"></a>風險降低類別

hello 威脅模型化工具防護功能的分類，根據 toohello Web 應用程式安全性架構，其中包含下列 hello:

| 類別 | 說明 |
| -------- | ----------- |
| **[稽核和記錄](./azure-security-threat-modeling-tool-auditing-and-logging.md)** | 誰在何時做了什麼？ 稽核和記錄，請參閱 toohow 您的應用程式記錄安全性相關事件 |
| **[驗證](./azure-security-threat-modeling-tool-authentication.md)** | 你是誰？ 驗證是一個實體證明 hello 的另一個實體，通常是透過使用者名稱和密碼等認證的身分識別的 hello 程序 |
| **[授權](./azure-security-threat-modeling-tool-authorization.md)** | 您該怎麼辦？ 授權是應用程式針對資源和作業提供存取控制的方式 |
| **[通訊安全性](./azure-security-threat-modeling-tool-communication-security.md)** | 您在與誰對話？ 通訊安全性可確保所有通訊是在最安全的情況下進行的 |
| **[設定管理](./azure-security-threat-modeling-tool-configuration-management.md)** | 應用程式的執行身分為何？ 其所連線到的資料庫為何？ 應用程式的管理方式為何？ 如何保護這些設定？ 設定管理是指 toohow 應用程式處理這些操作的問題 |
| **[密碼編譯](./azure-security-threat-modeling-tool-cryptography.md)** | 如何保護機密資料 (機密性)？ 如何防止資料或程式庫遭到竄改 (完整性)？ 如何為必須是密碼編譯增強式的隨機值提供種子？ 密碼編譯是指 toohow 機密性和完整性，會強制執行您的應用程式 |
| **[例外狀況管理](./azure-security-threat-modeling-tool-exception-management.md)** | 當應用程式中的方法呼叫失敗時，應用程式會如何處理？ 您要顯示多少資料？ 是否傳回易懂的錯誤資訊 tooend 使用者？ 您是否有傳送重要的例外狀況資訊後 toohello 呼叫者？ 應用程式會正常地失敗嗎？ |
| **[輸入驗證](./azure-security-threat-modeling-tool-input-validation.md)** | 如何知道您的應用程式收到的 hello 輸入是有效且安全的？ 輸入的驗證是指的 toohow 您的應用程式篩選、 消除或拒絕其他處理之前的輸入。 請考慮透過進入點限制輸入並透過退出點編碼輸出。 您是否信任來源的資料，例如來自資料庫和檔案共用？ |
| **[敏感資料](./azure-security-threat-modeling-tool-sensitive-data.md)** | 應用程式如何處理敏感性資料？ 機密資料是指的 toohow 應用程式處理必須受到保護，在記憶體中，透過 hello 網路，或在持續性存放區中的任何資料 |
| **[工作階段管理](./azure-security-threat-modeling-tool-session-management.md)** | 應用程式如何處理和保護使用者工作階段？ 工作階段是指 tooa 系列相關的使用者與您的 Web 應用程式之間的互動 |

這可協助您識別︰

* 在哪裡？ hello 最常犯
* 在哪裡？ hello 最可採取動作的增強功能

如此一來，您會使用這些類別 toofocus，並設定您的安全性工作的優先權，如果您知道 hello 最普遍的安全性問題發生的 hello 輸入的驗證、 驗證和授權類別，您可以從那裡開始。 如需詳細資訊，請造訪**[這個專利連結](https://www.google.com/patents/US7818788)**

## <a name="next-steps"></a>後續步驟

請瀏覽**[威脅模型化工具威脅](./azure-security-threat-modeling-tool-threats.md)** toolearn 深入了解 hello 類別 hello 工具使用 toogenerate 可能的設計威脅的威脅。
