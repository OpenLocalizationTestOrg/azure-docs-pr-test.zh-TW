---
title: "aaaGet 開始使用 Azure IoT 邊緣 (Windows) |Microsoft 文件"
description: "如何 toobuild Azure IoT 邊緣閘道在 Windows 電腦，並了解 Azure IoT 邊緣的索引鍵概念，例如模組和 JSON 組態檔。"
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5dd13cbfc02eeb55d9f2dbffca5021f2624acf14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a>在 Windows 上探索 Azure IoT Edge 架構

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>如何 toorun hello 範例

hello **build.cmd**指令碼會產生其輸出中 hello**建置**hello 的本機複本中的資料夾**iot 邊緣**儲存機制。 此輸出會包含 hello 這個範例中使用兩個 IoT 邊緣模組。

hello 組建指令碼位置**logger.dll**在 hello**建置\\模組\\記錄器\\偵錯**資料夾和**hello\_world.dll**在 hello**建置\\模組\\hello_world\\偵錯**資料夾。 使用這些路徑 hello**模組路徑**值 hello 下列 JSON 設定檔中所示。

hello hello\_世界\_範例程序需要 hello 路徑 tooa JSON 組態檔做為命令列引數。 hello 下列的範例 JSON 檔案中提供 hello SDK 儲存機制**範例\\hello\_世界\\src\\hello\_世界\_win.json**。 此設定檔運作，除非您修改 hello 模組建置指令碼 tooplace hello IoT 邊緣或範例在非預設位置中的可執行檔。

> [!NOTE]
> hello 模組路徑的相對 toohello 目錄，其中 hello hello\_世界\_sample.exe 所在。 hello 範例 JSON 組態檔的預設值 toowriting '.log.txt' 目前的工作目錄中。

```json
{
  "modules": [
    {
      "name": "logger",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
        }
      },
      "args": { "filename": "log.txt" }
    },
    {
      "name": "hello_world",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
        }
      },
      "args": null
      }
  ],
  "links": [
    {
      "source": "hello_world",
      "sink": "logger"
    }
  ]
}
```

1. 瀏覽 toohello**建置**資料夾中的 hello 本機副本的 hello 根**iot 邊緣**儲存機制。

1. 執行下列命令的 hello:

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
