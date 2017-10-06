---
title: "aaaCreate 第一個的 Azure IoT 閘道模組 |Microsoft 文件"
description: "建立模組，並將它加入 tooa 範例應用程式 toocustomize 模組行為。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>第 5 課：建立您的第一個 Azure IoT 閘道器模組
Azure IoT 邊緣可讓您撰寫的 Java、.NET 或 Node.js 的 toobuild 模組，本教學課程中引導您 hello 步驟建置 c 模組

## <a name="what-you-will-do"></a>將執行的作業

- 編譯並執行 Intel NUC 上 hello hello_world 範例應用程式。
- 建立模組，並在 Intel NUC 上編譯。
- 新增 hello 新模組 toohello hello_world 範例應用程式，然後執行 Intel NUC hello 範例。 hello 新的模組會列印出"hello_world 」 訊息時間戳記。

## <a name="what-you-will-learn"></a>學習目標

- 如何 toocompile 和 Intel NUC 上執行範例應用程式。
- 如何 toocreate 模組。
- 如何 tooadd 模組 tooa 範例應用程式。

## <a name="what-you-need"></a>您需要什麼

已安裝在主機電腦上的 Azure IoT Edge。

## <a name="folder-structure"></a>資料夾結構

您在第 1 課複製 hello 範例程式碼的第 5 課 hello 子資料夾，在沒有`module`資料夾和`sample`資料夾。

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- hello`module/my_module`資料夾包含 hello 來源的程式碼和指令碼 toobuild hello 模組。
- hello`sample`資料夾包含 hello 來源的程式碼和指令碼 toobuild hello 範例應用程式。

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>編譯及執行 Intel NUC 上 hello hello_world 範例應用程式

hello`hello_world`範例會建立閘道，根據 hello`hello_world.json`指定 hello 兩個預先定義的模組 hello 應用程式相關聯的檔案。 hello 閘道記錄檔的"hello world"訊息 tooa 檔案每隔 5 秒。 在本節中編譯並執行 hello`hello_world`應用程式使用其預設模組。

toocompile 和執行 hello`hello_world`應用程式中，您的主機電腦上執行下列步驟：

1. 藉由執行下列命令的 hello 初始化 hello 設定檔：

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. 更新 hello 閘道器組態檔以 hello Intel NUC MAC 位址。 略過此步驟，如果您已經完成 hello 課程太[設定及執行範例應用程式 b][config_ble]。

   1. 執行下列命令的 hello 開啟 hello 閘道器組態檔：

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. 更新 hello 閘道的 MAC 位址時您[設定為 IoT 閘道 Intel NUC][setup_nuc]，然後儲存 hello 檔案。

1. 藉由執行下列命令的 hello 編譯 hello 範例原始程式碼：

   ```bash
   gulp compile
   ```

   hello 命令會傳送 hello 範例來源的程式碼 tooIntel NUC 並執行`build.sh`toocompile 它。

1. 執行 hello `hello_world` Intel NUC 的應用程式，執行下列命令的 hello:

   ```bash
   gulp run
   ```

   hello 命令執行`../Tools/run-hello-world.js`中指定`config.json`toostart 上 Intel NUC hello 範例應用程式。

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>建立新的模組，並在 Intel NUC 上編譯

hello 執行下列步驟會逐步引導您建立新的模組和 Intel NUC 上進行編譯。 hello 模組會列印出時間戳記在收到這些訊息。 本節中，您將建立您的第一個自訂閘道器模組。

任何 Azure IoT 邊緣模組必須實作下列介面的 hello:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

您可以選擇性地實作下列介面的 hello:

   ```C
   pfModule_Start Module_Start
   ```

hello 下列圖表顯示 hello 重要狀態路徑的模組。 hello 正方形矩形代表狀態之間移動 hello 模組時，實作 tooperform 作業的方法。 hello 橢圓形是 hello 模組可以處於重大狀態。

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

現在讓我們來建立 hello 範本為基礎的模組：

1. 執行下列命令的 hello 開啟 hello 範本資料夾：

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`做為範本，可促進 hello 建立模組。 hello 範本宣告 hello 介面。 您只需要 toodo 是 tooadd 邏輯 toohello`MyModule_Receive`函式。
   - `build.sh`是 hello 組建指令碼 toocompile hello 模組 Intel NUC 上。
1. 開啟 hello`src/my_module.c`檔案，並包含兩個標頭檔：

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. 新增下列程式碼 toohello hello`MyModule_Receive`函式：

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. 更新 hello`config.json`檔案 toospecify hello `workspace` Intel NUC 上您主機電腦和 hello 部署路徑的資料夾。 在編譯時，hello 中 hello 檔案`workspace`資料夾將會傳送的 toohello 部署路徑。

   1. 開啟 hello`config.json`檔案執行下列命令的 hello:

      ```bash
      code config.json
      ```

   1. 更新`config.json`以 hello 下列組態：

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. 藉由執行下列命令的 hello 編譯 hello 模組：

   ```bash
   gulp compile
   ```

   hello 命令會傳送 hello 來源的程式碼 tooIntel NUC 並執行`build.sh`toocompile hello 模組。

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>加入 hello 模組 toohello hello_world 範例應用程式，並在 Intel NUC 執行 hello 應用程式

tooperform 這項工作，請遵循下列步驟：

1. Intel NUC 上列出所有 hello 可用模組二進位檔 （.so 檔案），藉由執行下列命令的 hello:

   ```bash
   gulp modules --list
   ```

   hello 二進位路徑`my_module`您編譯應該會列出如下：

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   如果您變更中的 hello 預設登入使用者名稱`config-gateway.json`，hello 二進位路徑的開頭將`home/<your username>`而不是`root`。

1. 新增`my_module`toohello`hello_world`範例應用程式：

   1. 開啟 hello`hello_world.json`檔案執行下列命令的 hello:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. 新增下列程式碼 toohello hello `modules` > 一節：

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      hello 值`module.path`應該`/root/gateway_sample/module/my_module/build/libmy_module.so`。 hello 程式碼會宣告`my_module`hello 閘道，以及 hello hello 模組二進位檔中指定的位置與相關聯的 toobe `module.path`。
   1. 新增下列程式碼 toohello hello `links` > 一節：

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      此程式碼會指定傳送訊息時，則從 hello`hello_world`模組太`my_module`。

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. 執行 hello`hello_world`範例應用程式，執行下列命令的 hello:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   hello`--config`參數會強制 hello`run-hello-world.js`使用 hello 來編寫 toorun`hello_world.json`檔案。

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

恭喜！ 您現在可以看到這個新模組 hello 行為，只會列印"hello world"訊息時間戳記、 hello 原始"hello_world 」 模組從不同的結果。

## <a name="next-steps"></a>後續步驟

您已建立新的模組，在閘道上 toohello hello_world 範例，並取得 hello 範例與 hello 新模組的應用程式 toorun 加入。 如果您想深入了解 Azure IoT 閘道模組 toolearn，您可以找到更多的模組範例這裡： [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules)。

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
