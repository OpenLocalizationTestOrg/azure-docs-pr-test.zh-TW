---
title: "aaaSimulated 覆盆子 Pi toocloud (Node.js) 的連線覆盆子 Pi web 模擬器 tooAzure IoT 中樞 |Microsoft 文件"
description: "連接覆盆子 Pi web 模擬器 tooAzure 覆盆子 Pi toosend 資料 toohello Azure 雲端的 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "木莓澆 pi 模擬器，azure iot 木莓澆 pi 木莓澆 pi iot 中樞，木莓澆 pi 傳送資料 toocloud 木莓澆 pi toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>連接覆盆子 Pi 線上模擬器 tooAzure IoT 中樞 (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

在本教學課程中，您必須開始學習覆盆子 Pi 線上模擬器所使用的 hello 基本概念。 然後您學習如何 tooseamlessly hello Pi 模擬器 toohello 雲端使用連線[Azure IoT 中樞](iot-hub-what-is-iot-hub.md)。 

如果您有實體裝置，請瀏覽[連接覆盆子 Pi tooAzure IoT 中樞](iot-hub-raspberry-pi-kit-node-get-started.md)tooget 啟動。 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>您要做什麼

* 學習覆盆子 Pi 線上模擬器 hello 基本概念。
* 建立 IoT 中樞。
* 在 IoT 中樞對於 Pi 註冊裝置。
* Pi toosend 模擬感應器資料 tooyour IoT 中樞上執行範例應用程式。

連接模擬覆盆子 Pi tooan 的 IoT 中樞您所建立。 然後您可以執行範例應用程式與 hello 模擬器 toogenerate 感應器資料。 最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。

## <a name="what-you-learn"></a>您學到什麼

* 如何 toocreate Azure IoT 中樞，並取得新的裝置連接字串。 如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。
* 如何與覆盆子 Pi 線上模擬器 toowork。
* 如何 toosend 感應器資料 tooyour IoT 中樞。

## <a name="overview-of-raspberry-pi-web-simulator"></a>Raspberry Pi Web 模擬器概觀

按一下 [hello] 按鈕 toolaunch 覆盆子 Pi 線上模擬器。

> [!div class="button"]
[啟動 Raspberry Pi 模擬器](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

Hello web 模擬器中有三個區域。
* 組件範圍-Pi 連接 BME280 感應器和 LED 是 hello 預設循環。 hello 區域已經鎖定在預覽版本，所以目前您無法進行自訂。
* 撰寫程式碼區域-toocode 覆盆子 Pi 與線上的程式碼編輯器。 hello 預設範例應用程式從 BME280 感應器可協助 toocollect 感應器資料，並將傳送 tooyour Azure IoT 中樞。 hello 應用程式是與實際 Pi 裝置完全相容。 
* 整合式的主控台窗口-它會顯示 hello 輸出的程式碼。 在這個視窗 hello 頂端，有三個按鈕。
   * **執行**-hello 撰寫程式碼區域中執行 hello 應用程式。
   * **重設**-重設 hello 撰寫程式碼區域 toohello 預設範例應用程式。
   * **摺疊/展開**-hello 右端有是一個按鈕，針對您展開 toofold/hello 主控台視窗上。

> [!NOTE] 
現在在預覽版本中提供 hello 覆盆子 Pi web 模擬器。 我們希望 toohear 在 hello 語音[Gitter 聊天室](https://gitter.im/Microsoft/raspberry-pi-web-simulator)。 hello 原始程式碼是 public [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator)。

![Pi 線上模擬器概觀](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>在 Pi Web 模擬器上執行範例應用程式

1. 在撰寫程式碼區域，請確定您在處理 hello 預設範例應用程式。 行 15 中的 hello 預留位置取代為 hello Azure IoT 中樞裝置連接字串。
   ![取代 hello 裝置連接字串](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. 按一下**執行**或型別`npm start`toorun hello 應用程式。


您應該會看到下列 hello 輸出，它會顯示 hello 感應器資料以及 tooyour IoT 中樞傳送 hello 訊息![輸出-從覆盆子 Pi tooyour IoT 中樞傳送的感應器資料](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>後續步驟

您已執行範例應用程式 toocollect 感應器資料，並將它傳送 tooyour IoT 中樞。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
