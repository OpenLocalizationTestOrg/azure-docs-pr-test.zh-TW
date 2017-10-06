---
title: "連接覆盆子 Pi （節點） tooAzure IoT-第 3 課： 執行範例 |Microsoft 文件"
description: "部署和執行範例應用程式 tooRaspberry Pi 3 傳送訊息 tooyour IoT 中樞和閃爍 hello LED。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "閃爍 led 雲端 pi, 來自雲端的 led 閃爍"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>執行範例應用程式 toosend 裝置到雲端訊息
## <a name="what-you-will-do"></a>將執行的作業
本文將告訴您 toodeploy 及執行範例應用程式覆盆子 Pi 3 傳送訊息 tooyour IoT 中樞。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標
您將學習如何 toouse hello 的 gulp 工具 toodeploy 和 pi 執行 hello 範例 Node.js 應用程式。

## <a name="what-you-need"></a>您需要什麼
* 在開始這項工作之前，您必須已順利完成[建立 Azure 的函式應用程式與儲存體帳戶 tooprocess 和市集 IoT 中樞訊息](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)。

## <a name="get-your-iot-hub-and-device-connection-strings"></a>取得 IoT 中樞與裝置連接字串
hello 裝置連接字串會使用 Pi tooconnect tooyour IoT 中樞。 hello IoT 中樞連接字串是使用的 tooconnect toohello 身分識別登錄在 IoT 中樞 toomanage hello 裝置允許 tooconnect tooyour IoT 中樞。 

* 列出資源群組中的所有您 IoT 中樞執行下列 Azure CLI 命令的 hello:

```bash
az iot hub list -g iot-sample --query [].name
```

使用`iot-sample`做為 hello 值`{resource group name}`如果您沒有變更 hello 值。

* 藉由執行下列 Azure CLI 命令的 hello 收到 hello IoT 中樞連接字串：

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`這是您指定當您建立 IoT 中樞，並註冊 Pi hello 名稱。

* 藉由執行下列命令的 hello 收到 hello 裝置連接字串：

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

使用`myraspberrypi`做為 hello 值`{device id}`如果您沒有變更 hello 值。

## <a name="configure-hello-device-connection"></a>設定 hello 裝置連線
1. 藉由執行下列命令的 hello 初始化 hello 設定檔：
   
   ```bash
   npm install
   gulp init
   ```
2. 開啟 hello 裝置組態檔`config-raspberrypi.json`在 Visual Studio 程式碼執行下列命令的 hello:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. 請遵循取代 hello hello`config-raspberrypi.json`檔案：
   
   * 取代**[裝置的主機名稱或 IP 位址]** hello 裝置 IP 位址或主機名稱與您向`device-discovery-cli`或與您的裝置設定時，會繼承 hello 值。
   * 取代**[IoT 裝置連接字串]**以 hello`device connection string`您取得的。
   * 取代**[IoT 中樞連接字串]**以 hello`iot hub connection string`您取得的。

更新 hello`config-raspberrypi.json`檔案，所以您可以部署 hello 範例應用程式，從您的電腦。

## <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
部署和執行 pi 的 hello 範例應用程式，執行下列命令的 hello:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>確認 hello 範例應用程式可正常運作
您應該會看到 hello LED 所連接的 tooPi 閃爍每隔兩秒鐘。 每次 hello LED 閃爍，hello 範例應用程式傳送訊息 tooyour IoT 中樞，並確認該 hello 訊息已成功傳送 tooyour IoT 中樞。 此外，收到 hello IoT 中樞的每個訊息會列印 hello 主控台視窗中。 hello 範例應用程式會自動終止後傳送 20 則訊息。

![具有所傳送和接收之訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a>摘要
您已部署並執行 hello 新閃爍範例應用程式上 Pi toosend 裝置到雲端訊息 tooyour IoT 中樞。 現在，當它們被寫入 toohello 儲存體帳戶，您可以監視您的訊息。

## <a name="next-steps"></a>後續步驟
[讀取保留在 Azure 儲存體中的訊息](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

