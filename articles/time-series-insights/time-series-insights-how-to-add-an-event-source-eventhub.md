---
title: "aaaHow tooadd 事件中心事件來源 tooyour Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "本教學課程涵蓋如何 tooadd 事件也就是來源連接的 tooan 事件中心 tooyour 時間數列 Insights 環境"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a>如何 tooadd 事件中心事件來源

本教學課程涵蓋如何 toouse 會 hello Azure 入口網站 tooadd 從事件中心 tooyour 時間數列 Insights 環境中讀取事件來源。

## <a name="prerequisites"></a>必要條件

您已建立事件中心，並在撰寫事件 tooit。 如需有關事件中樞的詳細資訊，請參閱 <https://azure.microsoft.com/services/event-hubs/>

> [取用者群組]每個時間序列 Insights 事件來源必須 toohave 未與任何其他取用者共用其自己專用的取用者群組。 如果多個讀取器會使用來自事件 hello 相同取用者群組，所有的讀取器都可能 toosee 失敗。 請注意，每一個事件中樞另外還有 20 個用戶群組的限制。 如需詳細資訊，請參閱 hello[事件中心程式設計指南](../event-hubs/event-hubs-programming-guide.md)。

## <a name="choose-an-import-option"></a>選擇匯入選項

您可以手動輸入 hello hello 事件來源的設定或事件中心可以選取從可用 tooyou 的 hello 事件中樞。
在 hello**匯入選項**選取器選擇其中一個 hello 下列選項：

* 手動提供事件中樞設定
* 從可用的訂用帳戶使用事件中樞

### <a name="select-an-available-event-hub"></a>選取可用的事件中樞

hello 下表說明包含其描述的 hello 新的事件來源 索引標籤中的每個選項做為事件來源中選取可用的事件中樞時：

| 屬性名稱 | 說明 |
| --- | --- |
| 事件來源名稱 | hello 事件來源名稱。 此名稱在 Time Series Insights 中必須是唯一的。
| 來源 | 選擇**事件中心**toocreate 事件中心事件來源。
| 訂用帳戶識別碼 | 選取在其中建立此事件中心的 hello 訂用帳戶。
| 服務匯流排命名空間 | 選取包含 hello 事件中心的 hello 服務匯流排命名空間。
| 事件中樞名稱 | 選取 hello hello 事件中樞名稱。
| 事件中樞原則名稱 | 選取 hello 共用存取原則，可以建立 hello 事件中樞設定 索引標籤。每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。 hello 共用存取原則的事件來源*必須*有**讀取**權限。
| 事件中樞取用者群組 | hello hello 事件中樞取用者群組 tooread 事件。 它強烈建議 toouse 事件來源的專用的取用者群組。

### <a name="provide-event-hub-settings-manually"></a>手動提供事件中樞設定

hello 下列資料表說明 hello 其描述與新的事件來源 索引標籤中的每個屬性輸入的設定時以手動方式：

| 屬性名稱 | 說明 |
| --- | --- |
| 事件來源名稱 | hello 事件來源名稱。 此名稱在 Time Series Insights 中必須是唯一的。
| 來源 | 選擇**事件中心**toocreate 事件中心事件來源。
| 訂用帳戶識別碼 | 在其中建立此事件中心的 hello 訂用帳戶。
| 資源群組 | 在其中建立此事件中心的 hello 訂用帳戶。
| 服務匯流排命名空間 | 服務匯流排命名空間是一個容器，包含一組訊息實體。 建立新的事件中樞時，也會建立服務匯流排命名空間。
| 事件中樞名稱 | hello 的事件中樞的名稱。 當您建立事件中心時，您也會指定特定名稱
| 事件中樞原則名稱 | hello 共用的存取原則，可以建立 hello 事件中樞設定 索引標籤。每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。 hello 共用存取原則的事件來源*必須*有**讀取**權限。
| 事件中樞原則金鑰 | 使用 tooauthenticate 存取 toohello 服務匯流排命名空間的 hello 共用存取金鑰。 輸入 hello 主要或次要金鑰這裡。
| 事件中樞取用者群組 | hello hello 事件中樞取用者群組 tooread 事件。 它強烈建議 toouse 事件來源的專用的取用者群組。

## <a name="next-steps"></a>後續步驟

1. 新增資料存取原則 tooyour 環境[定義資料存取原則](time-series-insights-data-access.md)
1. 存取您的環境中 hello[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)
