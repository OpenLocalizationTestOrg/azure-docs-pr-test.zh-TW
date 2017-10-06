---
title: "Azure IoT 邊緣 IoT 閘道上的 aaaData 轉換 |Microsoft 文件"
description: "使用透過 Azure IoT 邊緣的自訂模組的感應器資料的 IoT 閘道 tooconvert hello 格式。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 閘道資料轉換, iot 閘道資料轉換"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>搭配 Azure IoT Edge 使用 IoT 閘道進行感應器資料轉換

> [!NOTE]
> 開始本教學課程之前，請確定您已完成下列課程序列中的 hello:
> * [將 Intel NUC 設定為 IoT 閘道](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [使用 IoT 閘道 tooconnect 事項 toohello 雲端 SensorTag tooAzure IoT 中樞](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

Iot 閘道的其中一個用途是 tooprocess 收集資料，再將它傳送 toohello 雲端。 Azure IoT 邊緣導入了可建立和組裝 tooform hello 資料處理工作流程的模組。 模組接收訊息、 執行一些動作，然後再針對其他模組 tooprocess 移動。

## <a name="what-you-learn"></a>您學到什麼

您了解 toocreate 模組 tooconvert 從 hello SensorTag 成不同格式的訊息。

## <a name="what-you-do"></a>您要做什麼

* 建立模組 tooconvert 接收的訊息為 hello.json 格式。
* 編譯 hello 模組。
* 加入 Azure IoT 邊緣 hello 模組 toohello b 範例應用程式。
* 執行 hello 範例應用程式。

## <a name="what-you-need"></a>您需要什麼

* 下列教學課程完成順序中的 hello:
  * [將 Intel NUC 設定為 IoT 閘道](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [使用 IoT 閘道 tooconnect 事項 toohello 雲端 SensorTag tooAzure IoT 中樞](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* 在主機電腦上執行的 SSH 用戶端。 Windows 上建議使用 PuTTY。 Linux 和 macOS 已隨附 SSH 用戶端。
* hello IP 位址和 hello 使用者名稱和密碼 tooaccess hello hello SSH 用戶端的閘道。
* 網際網路連線。

## <a name="create-a-module"></a>建立模組

1. Hello 主機電腦上，執行 hello SSH 用戶端，並連接 toohello IoT 閘道。
1. 藉由執行下列命令的 hello 複製 hello hello 轉換模組從 GitHub toohello 主目錄的 hello IoT 閘道的原始程式檔：

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   這是 hello C 程式設計語言撰寫的原生 Azure 邊緣模組。 hello 模組會將 hello 格式接收的訊息轉換成下列其中一個 hello:

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>編譯 hello 模組

toocompile hello 模組，執行下列命令的 hello:

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

您取得`libmy_module.so`檔案 hello 編譯完成之後。 記下 hello 此檔案的絕對路徑。

## <a name="add-hello-module-toohello-ble-sample-application"></a>新增 hello 模組 toohello b 範例應用程式

1. 藉由執行下列命令的 hello 移 toohello 範例資料夾中：

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. 執行下列命令的 hello 開啟 hello 設定檔：

   ```bash
   vi ble_gateway.json
   ```

1. 將模組插入下列程式碼 toohello hello `modules` > 一節。

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. 取代`[Your libmy_module.so path]`hello hello libmy_module.so hello 絕對路徑的程式碼中 ' 檔案。
1. Hello 中的 hello 程式碼取代`links`以 hello 下列其中一節：

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. 按`ESC`，然後輸入`:wq`toosave hello 檔案。

## <a name="run-hello-sample-application"></a>執行 hello 範例應用程式

1. Hello SensorTag 電源。
1. 執行下列命令的 hello 設定 hello SSL_CERT_FILE 環境變數：

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. 執行下列命令的 hello hello 範例應用程式執行與 hello 加入的模組：

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>後續步驟

已成功使用 hello IoT 閘道 tooconvert hello 訊息從 SensorTag 成 hello.json 格式。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
