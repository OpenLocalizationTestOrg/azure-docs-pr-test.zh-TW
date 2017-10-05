---
title: "將 Intel Edison (C) 連接到 Azure IoT - 第 4 課：接收訊息 | Microsoft Docs"
description: "範例應用程式會在 Edison 上執行，並監視來自 IoT 中樞的傳入訊息。 新的 Gulp 工作會從 IoT 中樞將訊息傳送到 Edison 來使 LED 閃爍。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "arduino 從 web 控制 led, arduino 透過 web 控制 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b7de7a8b53cdb1d7c2560225fce9166e555e5123
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a>執行範例應用程式以接收雲端到裝置訊息
在本文中，您將在 Intel Edison 上部署範例應用程式。 範例應用程式會監視來自 IoT 中樞的傳入訊息。 您也會在電腦上執行 Gulp 工作，以從 IoT 中樞將訊息傳送到 Edison。 當範例應用程式收到訊息時，便會使 LED 閃爍。 如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。

## <a name="what-you-will-do"></a>將執行的作業
* 將範例應用程式連接到 IoT 中樞。
* 部署並執行範例應用程式。
* 從 IoT 中樞將訊息傳送到 Edison 來使 LED 閃爍。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 如何監視來自 IoT 中樞的傳入訊息。
* 如何從 IoT 中樞將「雲端到裝置」訊息傳送到 Edison。

## <a name="what-you-need"></a>您需要什麼
* Intel Edison，進行設定以供使用。 若要了解如何設定 Edison，請參閱[設定裝置][configure-your-device]。
* 在您的 Azure 訂用帳戶中建立的 IoT 中樞。 若要了解如何建立 IoT 中樞，請參閱[建立您的 Azure IoT 中樞][create-your-azure-iot-hub]。

## <a name="connect-the-sample-application-to-your-iot-hub"></a>將範例應用程式連接到 IoT 中樞
1. 請確定您已位於存放庫資料夾 `iot-hub-c-edison-getting-started`。 執行下列命令來在 Visual Studio Code 中開啟範例應用程式︰

   ```bash
   cd Lesson4
   code .
   ```

   `app` 子資料夾中的檔案為關鍵的來源檔案，這個來源檔案包含監視來自 IoT 中樞之傳入訊息的程式碼。 `blinkLED` 函數會使 LED 閃爍。

   ![範例應用程式中的儲存機制結構][repo-structure]
2. 執行下列命令初始化組態檔：

   ```bash
   npm install
   gulp init
   ```

   如果您已在此電腦上完成[建立 Azure 函式應用程式與儲存體帳戶][create-an-azure-function-app-and-storage-account]中的步驟，則會繼承所有組態，因此您可以略過部署和執行範例應用程式之工作的步驟。 如果您是在不同電腦上完成[建立 Azure 函數應用程式與儲存體帳戶][create-an-azure-function-app-and-storage-account]中的步驟，您必須取代 `config-edison.json` 檔案中的預留位置。 `config-edison.json` 檔案位於您主資料夾的子資料夾中。

   ![config-edison.json 檔案的內容](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * 以您設定裝置時所記下的裝置 IP 位址來取代 **[device hostname or IP address]**。
   * 以透過執行 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` 命令所取得的裝置連接字串取代 **[IoT device connection string]**。
   * 以透過執行 `az iot hub show-connection-string --name {my hub name}` 命令所取得的 IoT 中樞連接字串取代 **[IoT hub connection string]**。

   > [!NOTE]
   > 也請執行 **gulp install-tools** (如果您未在第 1 課這麼做)。

## <a name="deploy-and-run-the-sample-application"></a>部署和執行範例應用程式
執行下列命令，在 Edison 上部署和執行範例應用程式：

```bash
gulp deploy && gulp run
```

gulp 命令會將範例應用程式部署到 Edison。 然後，它會在 Edison 上執行應用程式，並在主機電腦上執行個別的工作，以從 IoT 中樞將 20 個閃爍訊息傳送到 Edison。

在範例應用程式執行後，它便會開始接聽來自 IoT 中樞的訊息。 同時，gulp 工作會從 IoT 中樞將數個「閃爍」訊息傳送到 Edison。 每當 Edison 收到閃爍訊息時，範例應用程式便會呼叫 `blinkLED` 函式來使 LED 閃爍。

當 gulp 工作從 IoT 中樞將 20 個訊息傳送到 Edison 時，LED 每兩秒應該會閃爍一次。 最後將會有一個「停止」訊息，來讓應用程式停止執行。

![具有 gulp 命令和閃爍訊息的範例應用程式][gulp-command-and-blink-messages]

## <a name="summary"></a>摘要
您已成功從 IoT 中樞將訊息傳送到 Edison 來使 LED 閃爍。 下一個工作是「選讀：變更 LED 的開與關行為」。

## <a name="next-steps"></a>後續步驟
[變更 LED 的開與關行為][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md