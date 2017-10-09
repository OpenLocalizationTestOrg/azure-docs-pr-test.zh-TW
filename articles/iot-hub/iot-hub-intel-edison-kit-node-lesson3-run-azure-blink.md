---
title: "連接 （節點） 的 Intel Edison tooAzure IoT-第 3 課： 將訊息傳送 |Microsoft 文件"
description: "部署和執行範例應用程式 tooIntel Edison 傳送訊息 tooyour IoT 中樞和閃爍 hello LED。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 雲端服務，arduino 傳送資料 toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>執行範例應用程式 toosend 裝置到雲端訊息
## <a name="what-you-will-do"></a>將執行的作業
本文將告訴您 toodeploy 及執行範例應用程式上傳送的 Intel Edison 訊息 tooyour IoT 中樞。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

## <a name="what-you-will-learn"></a>學習目標
您將學習如何 toouse hello 的 gulp 工具 toodeploy 並 Edison 上執行 hello 範例 C 應用程式。

## <a name="what-you-need"></a>您需要什麼
* 在開始這項工作之前，您必須已順利完成[建立 Azure 的函式應用程式與儲存體帳戶 tooprocess 和市集 IoT 中樞訊息][process-and-store-iot-hub-messages]。

## <a name="get-your-iot-hub-and-device-connection-strings"></a>取得 IoT 中樞與裝置連接字串
hello 裝置連接字串是使用的 tooconnect Edison tooyour IoT 中樞。 hello IoT 中樞連接字串是使用的 tooconnect 您 IoT 中樞 toohello 裝置身分識別代表 Edison hello IoT 中樞。

* 列出資源群組中的所有您 IoT 中樞執行下列 Azure CLI 命令的 hello:

```bash
az iot hub list -g iot-sample --query [].name
```

使用`iot-sample`做為 hello 值`{resource group name}`如果您沒有變更 hello 值。

* 藉由執行下列 Azure CLI 命令的 hello 收到 hello IoT 中樞連接字串：

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`這是您指定當您建立 IoT 中樞，並註冊 Edison hello 名稱。

* 藉由執行下列命令的 hello 收到 hello 裝置連接字串：

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

使用`myinteledison`做為 hello 值`{device id}`如果您沒有變更 hello 值。

## <a name="configure-hello-device-connection"></a>設定 hello 裝置連線
1. 藉由執行下列命令的 hello 初始化 hello 設定檔：

   ```bash
   npm install
   gulp init
   ```

2. 開啟 hello 裝置組態檔`config-edison.json`在 Visual Studio 程式碼執行下列命令的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. 請遵循取代 hello hello`config-edison.json`檔案：

   * 取代**[裝置的主機名稱或 IP 位址]** hello 裝置的 IP 位址設定您的裝置時關閉標記。
   * 取代**[IoT 裝置連接字串]**以 hello`device connection string`您取得的。
   * 取代**[IoT 中樞連接字串]**以 hello`iot hub connection string`您取得的。

   > [!NOTE]
   > 您在本文中不需要 `azure_storage_connection_string`。 請讓它保持原狀。

## <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
部署和執行下列命令的 hello Edison 執行 hello 範例應用程式：

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>確認 hello 範例應用程式可正常運作
您應該會看到 hello LED 所連接的 tooEdison 閃爍每隔兩秒鐘。 每次 hello LED 閃爍，hello 範例應用程式傳送訊息 tooyour IoT 中樞，並確認該 hello 訊息已成功傳送 tooyour IoT 中樞。 此外，收到 hello IoT 中樞的每個訊息會列印 hello 主控台視窗中。 hello 範例應用程式會自動終止後傳送 20 則訊息。

![具有所傳送和接收之訊息的範例應用程式][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>摘要
您已部署，而且執行 Edison toosend 裝置到雲端訊息 tooyour IoT 中樞 hello 新閃爍範例應用程式。 您現在監視您的郵件將它們寫入 toohello 儲存體帳戶。

## <a name="next-steps"></a>後續步驟
[讀取保存在 Azure 儲存體中的訊息][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md