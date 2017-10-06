---
title: "aaaAdd 事件來源 tooyour Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "在此教學課程中，您要連接的事件來源 tooyour 時間數列 Insights 環境"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>建立時間序列 Insights 環境使用 hello Ibiza 入口網站事件來源

Time Series Insights 事件來源衍生自事件代理程式，例如 Azure 事件中樞。 時間序列 Insights 直接連接 tooEvent 來源，而不需要使用者 toowrite 一行程式碼擷取 hello 資料流。 目前，Time Series Insights 支援 Azure 事件中樞與 Azure IoT 中樞。 在未來的 hello，將會加入更多的事件來源。

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a>步驟 tooadd 事件來源 tooyour 環境

1.  登入 toohello [Ibiza 入口網站](https://portal.azure.com)。
2.  按一下 [所有資源] 功能表中的 hello 左邊 hello hello Ibiza 入口網站。
3.  選取 Time Series Insights 環境。

  ![建立 hello 時間數列 Insights 事件來源](media/add-event-source/getstarted-create-event-source-1.png)

4.  選取 [事件來源]，按一下 [+ 新增]。

  ![建立 hello 時間數列 Insights 事件來源的詳細資料](media/add-event-source/getstarted-create-event-source-2.png)

5.  指定 hello hello 事件來源名稱。 此名稱與來自此事件來源的所有事件相關聯，並可在查詢時使用。
6.  從事件中心中的資源 hello 目前訂用帳戶的 hello 清單中選取事件中心。 否則選擇 匯入選項 」 提供事件中樞設定手動"toospecify 另一個訂用帳戶中的事件中心。 事件必須以 JSON 格式發佈。
7.  選取具有讀取權限在 hello 事件中樞的原則。
8.  指定事件中樞取用者群組。

  > [!IMPORTANT]
  > 確定任何其他服務 (例如串流分析作業或其他 Time Series Insights 環境) 均未使用此取用者群組。 如果取用者群組由其他服務，讀取作業造成負面影響此環境並 hello 其他服務。 如果您使用 「 $Default"作為 hello 取用者群組，可能導致 toopotential 重複使用其他讀取器。

9.  按一下 [建立]。

建立之後的 hello 事件來源，時間序列 Insights 將自動啟動資料流處理到您環境的資料。

## <a name="next-steps"></a>後續步驟

* [傳送事件](time-series-insights-send-events.md)toohello 事件來源
* 在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中檢視您的環境
