---
title: "開始使用 Azure IoT Edge (Linux) | Microsoft Docs"
description: "如何在 Linux 機器上建置閘道，並了解 Azure IoT Edge 中的重要概念，例如模組和 JSON 組態檔。"
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
ms.openlocfilehash: b02d79fcd9cd2a2ef0041aac4e85528263c8d58a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="7a681-103">在 Linux 上探索 Azure IoT Edge 架構</span><span class="sxs-lookup"><span data-stu-id="7a681-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="7a681-104">如何執行範例</span><span class="sxs-lookup"><span data-stu-id="7a681-104">How to run the sample</span></span>

<span data-ttu-id="7a681-105">**build.sh** 指令碼會在 **iot-edge** 存放庫本機複本的 **build** 資料夾中產生其輸出。</span><span class="sxs-lookup"><span data-stu-id="7a681-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="7a681-106">這輸出包含在此範例中使用的兩個 IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="7a681-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="7a681-107">build 指令碼會將 **liblogger.so** 放在 **build/modules/logger/** 資料夾中，並將 **libhello\_world.so** 放在 **build/modules/hello_world/** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7a681-107">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="7a681-108">使用這些路徑作為**模組路徑**值 (如下列範例 JSON 設定檔所示)。</span><span class="sxs-lookup"><span data-stu-id="7a681-108">Use these paths for the **module path** values as shown in the following example JSON settings file.</span></span>

<span data-ttu-id="7a681-109">hello\_world\_sample 程序會採用 JSON 組態檔的路徑做為命令列引數。</span><span class="sxs-lookup"><span data-stu-id="7a681-109">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span></span> <span data-ttu-id="7a681-110">下列範例 JSON 檔案提供於 SDK 儲存裝置中 (位於 **samples/hello\_world/src/hello\_world\_lin.json**)。</span><span class="sxs-lookup"><span data-stu-id="7a681-110">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="7a681-111">除非您修改 build 指令碼以將 IoT Edge 模組或範例可執行檔放置在非預設位置，否則此組態檔將保有原始功能。</span><span class="sxs-lookup"><span data-stu-id="7a681-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="7a681-112">模組路徑是 hello\_world\_sample 可執行檔啟動之目前工作目錄的相對路徑，不是可執行檔所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="7a681-112">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span></span> <span data-ttu-id="7a681-113">範例 JSON 組態檔的預設值為在目前的工作目錄中寫入 'log.txt'。</span><span class="sxs-lookup"><span data-stu-id="7a681-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="7a681-114">瀏覽至 **iot-edge** 存放庫的本機複本根中的 **build** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7a681-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="7a681-115">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="7a681-115">Run the following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

