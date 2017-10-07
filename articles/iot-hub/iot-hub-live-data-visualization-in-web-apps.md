---
title: "從您的 Azure IoT 中樞 – Web 應用程式的感應器資料 aaaReal 時間資料視覺效果 |Microsoft 文件"
description: "使用 Microsoft Azure App Service toovisualize 氣溫和溼度資料會從 hello 感應器收集並傳送 tooyour Iot 中樞 hello Web 應用程式功能。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "即時資料視覺效果, 即時資料視覺效果, 感應器資料視覺效果"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a>使用 hello Azure App Service Web 應用程式功能時，視覺化您的 Azure IoT 中樞的即時感應器資料

![端對端圖表](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>您學到什麼

在此教學課程中，您學會 toovisualize 即時感應器資料 IoT 中樞接收執行 web 應用程式裝載 web 應用程式上的方式。 如果您想在 IoT 中樞的 tootry toovisualize hello 資料使用 Power BI，請參閱[使用 Power BI toovisualize 即時感應器資料從 Azure IoT 中樞](iot-hub-live-data-visualization-in-power-bi.md)。

## <a name="what-you-do"></a>您要做什麼

- 在 [hello Azure 入口網站中建立 web 應用程式。
- 新增取用者群組，讓您的 IoT 中樞準備好進行資料存取。
- 設定 hello web 應用程式 tooread 感應器資料從 IoT 中樞。
- 上傳 web 應用程式 toobe hello web 應用程式所裝載。
- 開啟 hello web 應用程式 toosee 即時氣溫和溼度資料從 IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

- [將裝置設定](iot-hub-raspberry-pi-kit-node-get-started.md)，其中涵蓋了 hello 下列需求：
  - 作用中的 Azure 訂用帳戶
  - 您訂用帳戶之下的 IoT 中樞
  - 用戶端應用程式所傳送訊息 tooyour Iot 中樞
- [下載 Git](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a>建立 Web 應用程式

1. 在 [hello [Azure 入口網站](https://ms.portal.azure.com/)，按一下 [**新增** > **Web + 行動** > **Web 應用程式**。
2. 輸入唯一的作業名稱，確認 hello 訂用帳戶，指定資源群組和位置，選取**Pin toodashboard**，然後按一下 [**建立**。

   我們建議您選取 hello 與資源群組的相同位置。 這樣可協助處理速度並減少 hello 的資料傳輸成本。

   ![建立 Web 應用程式](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a>設定從 IoT 中樞 hello web 應用程式 tooread 資料

1. 開啟您剛才佈建的 hello web 應用程式。
2. 按一下**應用程式設定**，然後在**應用程式設定**，加入下列索引鍵/值組的 hello:

   | Key                                   | 值                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | Azure.IoT.IoTHub.ConnectionString     | 取自 iothub-explorer                                |
   | Azure.IoT.IoTHub.ConsumerGroup        | hello 您加入 tooyour IoT 中樞的 hello 取用者群組名稱  |

   ![加入具有索引鍵/值組的設定 tooyour web 應用程式](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. 按一下**應用程式設定**下**一般設定**，切換 hello **Web 通訊端**選項，然後再按一下**儲存**。

   ![切換 hello Web 通訊端選項](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a>上傳 hello web 應用程式所裝載的 web 應用程式 toobe

在 GitHub 上，我們已啟用 Web 應用程式 (web application)，以顯示 IoT 中樞的即時感應器資料。 您只需要 toodo 是與 Git 儲存機制設定 hello web 應用程式 toowork，請下載 hello web 應用程式從 GitHub，並再將它上傳的 hello web 應用程式 toohost tooAzure。

1. 在 [hello web 應用程式中，按一下 [**部署選項** > **選擇來源** > **本機 Git 儲存機制**，然後按一下 [**確定**.

   ![設定 web 應用程式部署 toouse hello 本機 Git 儲存機制](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. 按一下**部署認證**，在 Azure 中建立的使用者名稱和密碼 toouse tooconnect toohello Git 儲存機制，然後按一下**儲存**。

3. 按一下**概觀**，並記下的 hello 值**Git 複製 url**。

   ![取得 hello Git 複製 URL 的 web 應用程式](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. 開啟本機電腦上的命令或終端機視窗。

5. 從 GitHub 下載 hello web 應用程式，並將它上傳的 hello web 應用程式 toohost tooAzure。 toodo，執行下列命令的 hello:

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > \<Git 複製 URL\>是 hello hello hello 上找到的 Git 儲存機制 URL**概觀**hello web 應用程式頁面。

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a>開啟 hello web 應用程式 toosee 即時氣溫和溼度資料從 IoT 中樞

在 [hello**概觀**頁面的 web 應用程式，按一下 [hello URL tooopen hello web 應用程式。

![取得 web 應用程式的 hello URL](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

您應該看到 hello 即時溫度和溼度資料從 IoT 中樞。

![顯示即時溫度和溼度的 Web 應用程式 (web app) 頁面](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> 確定 hello 範例應用程式正在執行您的裝置上。 如果沒有，就會空白圖表，您可以參考下的 toohello 教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)。

## <a name="next-steps"></a>後續步驟
您已成功從 IoT 中樞使用 web 應用程式 toovisualize 即時感應器資料。

從 Azure IoT 中樞的替代方式 toovisualize 資料，請參閱[使用 Power BI toovisualize 即時感應器資料，或從 IoT 中樞](iot-hub-live-data-visualization-in-power-bi.md)。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
