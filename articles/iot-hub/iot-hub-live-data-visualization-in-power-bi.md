---
title: "aaaReal 時間資料從 Azure IoT 中樞 – Power BI 的感應器資料視覺效果 |Microsoft 文件"
description: "使用 Power BI toovisualize 氣溫和溼度的資料會從 hello 感應器收集並傳送 tooyour Azure IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "即時資料視覺效果, 即時資料視覺效果, 感應器資料視覺效果"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a>使用 Power BI 將 Azure IoT 中樞的即時感應器資料視覺化

![端對端圖表](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>您學到什麼

您了解如何 toovisualize 即時感應器資料的 Azure IoT 中樞接收由 Power BI。 如果您想 tootry 視覺化 hello 資料在您的 IoT 中樞與 Web 應用程式，請參閱[使用 Azure Web Apps toovisualize 即時感應器資料從 Azure IoT 中樞](iot-hub-live-data-visualization-in-web-apps.md)。

## <a name="what-you-do"></a>您要做什麼

- 新增取用者群組，讓您的 IoT 中樞準備好進行資料存取。
- 建立、 設定及執行資料傳輸的資料流分析作業從您的 IoT 中樞 tooyour Power BI 帳戶。
- 建立並發行 Power BI 報表 toovisualize hello 資料。

## <a name="what-you-need"></a>您需要什麼

- 教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：
  - 有效的 Azure 訂用帳戶。
  - 位於您訂用帳戶中的 Azure IoT 中樞。
  - 用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。
- Power BI 帳戶。 ([免費試用 Power BI](https://powerbi.microsoft.com/))

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>設定、設定及執行串流分析作業

### <a name="create-a-stream-analytics-job"></a>建立串流分析工作

1. 在 hello Azure 入口網站中按一下 新增 > 物聯網 > 串流分析工作。
1. 輸入下列資訊為 hello 工作 hello。

   **工作名稱**: hello hello 作業名稱。 hello 名稱必須是全域唯一的。

   **資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。

   **位置**： 使用 hello 相同資源群組的位置。

   **Pin toodashboard**： 核取此選項，讓您輕鬆存取 tooyour IoT 中樞，從 hello 儀表板。

   ![在 Azure 中建立串流分析作業](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. 按一下 [建立] 。

### <a name="add-an-input-toohello-stream-analytics-job"></a>加入輸入的 toohello 資料流分析工作

1. 開啟 hello 資料流分析工作。
1. 在 [作業拓撲] 之下，按一下 [輸入]。
1. 在 [hello**輸入**] 窗格中，按一下**新增**，然後輸入下列資訊的 hello:

   **輸入的別名**: hello hello 輸入唯一別名。

   **來源**︰選取 [IoT 中樞]。

   **取用者群組**: hello 選取您剛才建立的取用者群組。
1. 按一下 [建立] 。

   ![在 Azure 中加入輸入的 tooa 資料流分析工作](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a>加入輸出 toohello 資料流分析工作

1. 在 [作業拓撲] 之下，按一下 [輸出]。
1. 在 [hello**輸出**] 窗格中，按一下**新增**，然後輸入下列資訊的 hello:

   **輸出別名**: hello hello 輸出的唯一別名。

   **接收器**︰選取 [Power BI]。
1. 按一下 [授權]，然後登入您的 Power BI 帳戶。
1. 授權之後，請輸入下列資訊的 hello:

   **群組工作區**︰選取您的目標群組工作區。

   **資料集名稱**︰輸入資料集名稱。

   **資料表名稱**︰輸入資料表名稱。
1. 按一下 [建立] 。

   ![在 Azure 中加入輸出 tooa 資料流分析工作](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>設定 hello hello 資料流分析作業的查詢

1. 在 [作業拓撲] 之下，按一下 [查詢]。
1. 取代`[YourInputAlias]`hello 作業的 hello 輸入別名。
1. 取代`[YourOutputAlias]`hello 的 hello 工作的輸出別名。
1. 按一下 [儲存] 。

   ![在 Azure 中加入查詢 tooa 資料流分析工作](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a>執行 hello 資料流分析工作

在 hello Stream Analytics 工作中，按一下 **啟動** > **現在** > **啟動**。 Hello 工作成功啟動 hello 作業狀態變更從**已停止**太**執行**。

![在 Azure 中執行串流分析作業](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a>建立及發行 Power BI 報表 toovisualize hello 資料

1. 確定 hello 範例應用程式正在執行您的裝置上。 如果沒有，請參閱下的 toohello 教學課程[設定您的裝置](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started)。
1. 登入 tooyour [Power BI](https://powerbi.microsoft.com/en-us/)帳戶。
1. 移 toohello 群組工作區中，當您建立 hello hello 資料流分析工作的輸出。
1. 按一下 [串流資料集]。

   您應該會看到當您建立 hello hello 資料流分析工作的輸出指定的 hello 列出資料集。
1. 在下**動作**，按一下第一個圖示 toocreate hello 報表。

   ![建立 Microsoft Power BI 報告](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. 經過一段時間建立列圖表 tooshow 即時溫度。
   1. 在 hello 報表建立頁面上，加入折線圖。
   1. 在 [hello**欄位**] 窗格中，展開您指定當您建立 hello hello 之資料流分析工作輸出的 hello 資料表。
   1. 拖曳**EventEnqueuedUtcTime**太**軸**上 hello**視覺效果**窗格。
   1. 拖曳**溫度**太**值**。

      現已建立折線圖。 hello x 軸會顯示以 hello UTC 時區日期和時間。 hello y 軸會顯示從 hello 感應器的溫度。

      ![加入折線圖的溫度 tooa Microsoft Power BI 報表](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. 經過一段時間建立另一個行圖表 tooshow 即時溼度。 toodo，遵循的 hello 上述相同步驟，並將**EventEnqueuedUtcTime** hello x 軸上和**溼度**hello y 軸上。

   ![加入折線圖的溼度 tooa Microsoft Power BI 報表](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. 按一下**儲存**toosave hello 報表。
1. 按一下**檔案** > **發行 tooweb**。
1. 按一下 建立內嵌程式碼，然後按一下發佈。

您要提供您可以與報表存取的任何人和程式碼片段 toointegrate hello 報告至您部落格或網站共用的 hello 報表連結。

![發佈 Microsoft Power BI 報告](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

Microsoft 也提供 hello [Power BI 行動應用程式](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/)檢視和與您的 Power BI 儀表板和報表互動行動裝置上。

## <a name="next-steps"></a>後續步驟

您已成功從您的 Azure IoT 中樞使用 Power BI toovisualize 即時感應器資料。
沒有從 Azure IoT 中樞的替代方式 toovisualize 資料。 請參閱[使用 Azure Web Apps toovisualize 即時感應器資料從 Azure IoT 中樞](iot-hub-live-data-visualization-in-web-apps.md)。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
