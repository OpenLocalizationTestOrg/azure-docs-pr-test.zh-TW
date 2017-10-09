---
title: "aaaGet 開始使用 Azure IoT 邊緣 (Linux) |Microsoft 文件"
description: "如何在 Linux 上的閘道 toobuild 電腦，並了解 Azure IoT 邊緣的索引鍵概念，例如模組和 JSON 組態檔。"
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a>在 Linux 上探索 Azure IoT Edge 架構

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>如何 toorun hello 範例

hello **build.sh**指令碼會產生其輸出中 hello**建置**hello 的本機複本中的資料夾**iot 邊緣**儲存機制。 此輸出會包含 hello 這個範例中使用兩個 IoT 邊緣模組。

hello 組建指令碼位置**liblogger.so**在 hello**組建/模組/記錄器/**資料夾和**libhello\_world.so**在 hello**建置 /模組/hello_world/**資料夾。 使用這些路徑 hello**模組路徑**值 hello 下列範例 JSON 設定檔中所示。

hello hello\_世界\_範例程序需要 hello 路徑 tooa JSON 組態檔的命令列引數。 hello 下列的範例 JSON 檔案中提供 hello SDK 儲存機制**範例/hello\_世界/src/hello\_世界\_lin.json**。 此設定檔運作，除非您修改 hello 模組建置指令碼 tooplace hello IoT 邊緣或範例在非預設位置中的可執行檔。

> [!NOTE]
> hello 模組路徑的相對 toohello 目前工作目錄從哪裡 hello hello\_世界\_範例可執行檔就會啟動、 不 hello hello 可執行檔所在的目錄。 hello 範例 JSON 組態檔的預設值 toowriting '.log.txt' 目前的工作目錄中。

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. 瀏覽 toohello**建置**資料夾中的 hello 本機副本的 hello 根**iot 邊緣**儲存機制。

1. 執行下列命令的 hello:

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

