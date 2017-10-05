---
title: "開始使用 Azure IoT Edge (Windows) | Microsoft Docs"
description: "如何在 Windows 機器上建置 Azure IoT Edge 閘道，並了解 Azure IoT Edge 中的重要概念，例如模組和 JSON 組態檔。"
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
ms.openlocfilehash: 5db39bab8e31a8e7026b34e72b4614b0f6f57772
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="31909-103">在 Windows 上探索 Azure IoT Edge 架構</span><span class="sxs-lookup"><span data-stu-id="31909-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="31909-104">如何執行範例</span><span class="sxs-lookup"><span data-stu-id="31909-104">How to run the sample</span></span>

<span data-ttu-id="31909-105">**build.cmd** 指令碼會在 **iot-edge** 存放庫本機複本的 **build** 資料夾中產生其輸出。</span><span class="sxs-lookup"><span data-stu-id="31909-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="31909-106">這輸出包含在此範例中使用的兩個 IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="31909-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="31909-107">build 指令碼會將 **logger.dll** 放在 **build\\modules\\logger\\Debug** 資料夾中，並將 **hello\_world.dll** 放在 **build\\modules\\hello_world\\Debug** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="31909-107">The build script places **logger.dll** in the **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in the **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="31909-108">使用這些路徑作為**模組路徑**值，如下列 JSON 設定檔所示。</span><span class="sxs-lookup"><span data-stu-id="31909-108">Use these paths for the **module path** values as shown in the following JSON settings file.</span></span>

<span data-ttu-id="31909-109">hello\_world\_sample 程序會採用 JSON 組態檔的路徑作為命令列引數。</span><span class="sxs-lookup"><span data-stu-id="31909-109">The hello\_world\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="31909-110">下列範例 JSON 檔案提供於 SDK 存放庫中 (位於 **samples\\hello\_world\\src\\hello\_world\_win.json**)。</span><span class="sxs-lookup"><span data-stu-id="31909-110">The following example JSON file is provided in the SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="31909-111">除非您修改 build 指令碼以將 IoT Edge 模組或範例可執行檔放置在非預設位置，否則此組態檔將保有原始功能。</span><span class="sxs-lookup"><span data-stu-id="31909-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="31909-112">模組路徑是相對於 hello\_world\_sample.exe 所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="31909-112">The module paths are relative to the directory where the hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="31909-113">範例 JSON 組態檔的預設值為在目前的工作目錄中寫入 'log.txt'。</span><span class="sxs-lookup"><span data-stu-id="31909-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="31909-114">瀏覽至 **iot-edge** 存放庫的本機複本根中的 **build** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="31909-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="31909-115">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="31909-115">Run the following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
