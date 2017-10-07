---
title: "SMS、 電子郵件，及 webhook 限制 aaaRate |Microsoft 文件"
description: "了解 Azure 將可能 SMS、 電子郵件或 webhook 通知動作群組的 hello 數目的限制。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a>SMS 訊息、電子郵件和 Webhook 文章的速率限制
速率限制是 tooa 特定電話號碼或電子郵件地址傳送太多的通知時所發生的擱置的通知。 速率限制可確保警示為可管理且可採取動作。

hello 規則 SMS 和電子郵件的 hello 相同。 hello 速率上限臨界值是：

 - **SMS**：1 小時 10 個訊息。
 - **電子郵件**：1 小時 100 個訊息。

## <a name="rate-limit-rules"></a>速率限制規則
- 特定的電話號碼或電子郵件是有限收到比 hello 臨界值所允許的多個訊息時的速率。
- 電話號碼或電子郵件可以是跨許多訂用帳戶動作群組的一部分。 速率限制適用於所有訂用帳戶。 它會套用一旦達到 hello 閾值時，即使從多個訂閱傳送訊息。  
- 電話號碼或電子郵件時速率限制的其他通知會傳送 toocommunicate hello 速率限制。 hello 狀態時 hello 速率限制的通知將會到期。

## <a name="rate-limit-of-webhooks"></a>Webhook 的速率限制 ##
沒有對 Webhook 的既有速率限制。

## <a name="next-steps"></a>後續步驟 ##
* 進一步了解 [SMS 警示行為](monitoring-sms-alert-behavior.md)。
* 取得[活動記錄檔警示概觀](monitoring-overview-alerts.md)，並了解如何 tooreceive 警示。  
* 了解如何太[設定警示，每當張貼服務健康情況通知](monitoring-activity-log-alerts-on-service-notifications.md)。
