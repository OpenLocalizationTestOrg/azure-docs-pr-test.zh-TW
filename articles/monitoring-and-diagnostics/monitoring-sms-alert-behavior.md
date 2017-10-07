---
title: "動作群組在 aaaSMS 警示行為 |Microsoft 文件"
description: "SMS 訊息格式和回應 tooSMS 訊息 toounsubscribe，重新訂閱或要求協助。"
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
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>動作群組中的 SMS 警示行為
## <a name="overview"></a>概觀 ##
動作群組可讓您 tooconfigure 接收器的清單。 定義活動記錄檔的警示; 時，可以再運用這些群組確保特定的動作群組在 hello 活動記錄在警示觸發時收到通知。 Hello 警示機制支援的其中一個是 SMS;hello 警示支援雙向通訊。 使用者可以回應 tooan 警示：

- **取消訂閱警示：**使用者可取消訂閱所有動作群組或單一動作群組的 SMS 警示。  
- **重新訂閱 tooalerts:**使用者可以重新訂閱 tooall SMS 警示的所有動作群組或設為單數動作群組。  
- **要求協助：**使用者可以要求在 hello SMS 的詳細資訊。 將其重新導向的 toothis 發行項

本文件涵蓋的 hello SMS 警示 hello 行為和 hello 回應動作 hello 使用者可以根據進行 hello hello 使用者地區設定：

## <a name="usacanada-sms-behavior"></a>美國/加拿大 SMS 行為
### <a name="receiving-an-sms-alert"></a>接收 SMS 警示
設定成動作群組一部分的 SMS 收件者，將會在警示啟動時收到 SMS。 hello SMS 對於將執行 hello 下列資訊：
* 此警示已傳送至 hello 動作群組的簡短名稱
- Hello 警示的標題

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>取消訂閱一個動作群組的 SMS 警示
使用者可以取消訂閱 SMS 一個動作群組的警示所回應 toohello shortcode 20873 與 hello 關鍵字: 「 停用&lt;動作群組的簡短名稱&gt;"。

例如 使用者希望 toounsubscribe 從與 hello shortname"Azure"，動作群組的警示就會傳送 SMS toohello shortcode 20873，指出 「 停用 Azure 」

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>取消訂閱所有動作群組的 SMS 警示
使用者可以取消訂閱的所有動作群組的所有 SMS 警示由回應 toohello shortcode 20873 與任何的 hello 下列關鍵字：
* STOP

例如 使用者希望 toounsubscribe 從所有的動作群組的所有 SMS 警示就會傳送 SMS toohello shortcode 20873，指出 「 停止 」

>[!NOTE]
>如果使用者已取消訂用 SMS 發出警示通知，但接著會加入新的動作群組 tooa;這些接收 SMS 警示，該新的動作群組，但仍未訂閱的所有先前的動作群組。
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>有一個動作群組的 resubscribing tooSMS 警示
使用者可以重新 tooSMS 一個動作群組的警示訂閱的回應 toohello shortcode 20873 與 hello 關鍵字: 「 啟用&lt;動作群組的簡短名稱&gt;"。

例如 希望 tooresubscribe tooalerts hello shortname"Azure"，動作群組的使用者就會傳送 SMS toohello shortcode 20873，指出 「 啟用 Azure 」

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>所有的動作群組的 resubscribing tooSMS 警示
使用者可以重新 tooall SMS 警示適用於所有的動作群組的訂閱所回應 toohello shortcode 20873 與任何的 hello 下列關鍵字：

* START

例如 使用者希望 toounsubscribe 從所有的動作群組的所有 SMS 警示就會傳送 SMS toohello shortcode 20873，指出 「 啟動 」

### <a name="requesting-help-via-sms"></a>透過 SMS 要求說明
使用者可以要求 hello SMS 的詳細資訊均已接收回應 toohello shortcode 20873 與任何 hello 下列關鍵字：
* HELP

Toohello 搭配連結 toothis 發行項的使用者會傳送回應。

## <a name="next-steps"></a>後續步驟
取得[活動記錄檔警示概觀](monitoring-overview-alerts.md)並了解如何 tooget 警示  
深入了解 [SMS 速率限制](monitoring-alerts-rate-limiting.md)  
深入了解[動作群組](monitoring-action-groups.md)
