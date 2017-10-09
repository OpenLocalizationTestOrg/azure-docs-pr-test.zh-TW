---
title: "aaaHow tooadd IoT 中樞事件來源 tooyour Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "本教學課程涵蓋的 tooadd 事件來源也就是如何連接 tooan IoT 中樞 tooyour 時間數列 Insights 環境"
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
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a>如何 tooadd IoT 中樞事件來源

本教學課程涵蓋如何 toouse 會 hello Azure 入口網站 tooadd 從 IoT 中樞 tooyour 時間數列 Insights 環境中讀取事件來源。

## <a name="prerequisites"></a>必要條件

您已建立 IoT 中樞，並在撰寫事件 tooit。 如需有關 IoT 中樞的詳細資訊，請參閱 <https://azure.microsoft.com/services/iot-hub/>

> [取用者群組]每個時間序列 Insights 事件來源必須 toohave 未與任何其他取用者共用其自己專用的取用者群組。 如果多個讀取器會使用來自事件 hello 相同取用者群組，所有的讀取器都可能 toosee 失敗。 如需詳細資訊，請參閱 hello [IoT 中樞開發人員指南](../iot-hub/iot-hub-devguide.md)。

## <a name="choose-an-import-option"></a>選擇匯入選項

您可以手動輸入 hello 事件來源的 hello 設定路徑，或選取 hello IoT 中樞已可用 tooyou 從 IoT 中樞。
在 hello**匯入選項**選取器選擇其中一個 hello 下列選項：

* 手動提供 IoT 中樞設定
* 從可用的訂用帳戶使用 IoT 中樞

### <a name="select-an-available-iot-hub"></a>選取可用的 IoT 中樞

hello 下表說明包含其描述的 hello 新的事件來源 索引標籤中的每個選項做為事件來源中選取可用的 IoT 中樞時：

| 屬性名稱 | 說明 |
| --- | --- |
| 事件來源名稱 | hello 事件來源名稱。 此名稱在 Time Series Insights 中必須是唯一的。
| 來源 | 選擇**IoT 中樞**toocreate IoT 中樞事件來源。
| 訂用帳戶識別碼 | 選取在其中建立此 IoT 中心 hello 訂用帳戶。
| IoT 中樞名稱 | 選取 hello hello IoT 中樞名稱。
| IoT 中樞原則名稱 | 選取 hello 共用存取原則，可以在 hello IoT 中樞設定 索引標籤找到。每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。 hello 共用存取原則的事件來源*必須*有**服務連線**權限。
| IoT 中樞取用者群組 | hello hello IoT 中樞取用者群組 tooread 事件。 它強烈建議 toouse 事件來源的專用的取用者群組。

### <a name="provide-iot-hub-settings-manually"></a>手動提供 IoT 中樞設定

hello 下列資料表說明 hello 其描述與新的事件來源 索引標籤中的每個屬性輸入的設定時以手動方式：

| 屬性名稱 | 說明 |
| --- | --- |
| 事件來源名稱 | hello 事件來源名稱。 此名稱在 Time Series Insights 中必須是唯一的。
| 來源 | 選擇**IoT 中樞**toocreate IoT 中樞事件來源。
| 訂用帳戶識別碼 | 此 IoT 中樞建立所在的 hello 訂用帳戶。
| 資源群組 | 此 IoT 中樞建立所在的 hello 訂用帳戶。
| IoT 中樞名稱 | hello IoT 中樞名稱。 當您建立 IoT 中樞時，您也會指定特定名稱
| IoT 中樞原則名稱 | hello 共用存取原則，可以建立 hello IoT 中樞設定 索引標籤。每一個共用存取原則都會有名稱、權限 (由您設定) 和存取金鑰。 hello 共用存取原則的事件來源*必須*有**服務連線**權限。
| IoT 中樞原則金鑰 | 使用 tooauthenticate 存取 toohello 服務匯流排命名空間的 hello 共用存取金鑰。 輸入 hello 主要或次要金鑰這裡。
| IoT 中樞取用者群組 | hello hello IoT 中樞取用者群組 tooread 事件。 它強烈建議 toouse 事件來源的專用的取用者群組。

## <a name="next-steps"></a>後續步驟

1. 新增資料存取原則 tooyour 環境[定義資料存取原則](time-series-insights-data-access.md)
1. 存取您的環境中 hello[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)
