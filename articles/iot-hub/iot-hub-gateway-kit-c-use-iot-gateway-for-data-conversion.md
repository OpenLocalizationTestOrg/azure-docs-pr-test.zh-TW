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
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="3429d-104">搭配 Azure IoT Edge 使用 IoT 閘道進行感應器資料轉換</span><span class="sxs-lookup"><span data-stu-id="3429d-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="3429d-105">開始本教學課程之前，請確定您已完成下列課程序列中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3429d-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="3429d-106">將 Intel NUC 設定為 IoT 閘道</span><span class="sxs-lookup"><span data-stu-id="3429d-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="3429d-107">使用 IoT 閘道 tooconnect 事項 toohello 雲端 SensorTag tooAzure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3429d-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="3429d-108">Iot 閘道的其中一個用途是 tooprocess 收集資料，再將它傳送 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="3429d-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="3429d-109">Azure IoT 邊緣導入了可建立和組裝 tooform hello 資料處理工作流程的模組。</span><span class="sxs-lookup"><span data-stu-id="3429d-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="3429d-110">模組接收訊息、 執行一些動作，然後再針對其他模組 tooprocess 移動。</span><span class="sxs-lookup"><span data-stu-id="3429d-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3429d-111">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="3429d-111">What you learn</span></span>

<span data-ttu-id="3429d-112">您了解 toocreate 模組 tooconvert 從 hello SensorTag 成不同格式的訊息。</span><span class="sxs-lookup"><span data-stu-id="3429d-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3429d-113">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="3429d-113">What you do</span></span>

* <span data-ttu-id="3429d-114">建立模組 tooconvert 接收的訊息為 hello.json 格式。</span><span class="sxs-lookup"><span data-stu-id="3429d-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="3429d-115">編譯 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="3429d-115">Compile hello module.</span></span>
* <span data-ttu-id="3429d-116">加入 Azure IoT 邊緣 hello 模組 toohello b 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3429d-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="3429d-117">執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3429d-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3429d-118">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="3429d-118">What you need</span></span>

* <span data-ttu-id="3429d-119">下列教學課程完成順序中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3429d-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="3429d-120">將 Intel NUC 設定為 IoT 閘道</span><span class="sxs-lookup"><span data-stu-id="3429d-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="3429d-121">使用 IoT 閘道 tooconnect 事項 toohello 雲端 SensorTag tooAzure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3429d-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="3429d-122">在主機電腦上執行的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="3429d-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="3429d-123">Windows 上建議使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="3429d-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="3429d-124">Linux 和 macOS 已隨附 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="3429d-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="3429d-125">hello IP 位址和 hello 使用者名稱和密碼 tooaccess hello hello SSH 用戶端的閘道。</span><span class="sxs-lookup"><span data-stu-id="3429d-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="3429d-126">網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="3429d-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="3429d-127">建立模組</span><span class="sxs-lookup"><span data-stu-id="3429d-127">Create a module</span></span>

1. <span data-ttu-id="3429d-128">Hello 主機電腦上，執行 hello SSH 用戶端，並連接 toohello IoT 閘道。</span><span class="sxs-lookup"><span data-stu-id="3429d-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="3429d-129">藉由執行下列命令的 hello 複製 hello hello 轉換模組從 GitHub toohello 主目錄的 hello IoT 閘道的原始程式檔：</span><span class="sxs-lookup"><span data-stu-id="3429d-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="3429d-130">這是 hello C 程式設計語言撰寫的原生 Azure 邊緣模組。</span><span class="sxs-lookup"><span data-stu-id="3429d-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="3429d-131">hello 模組會將 hello 格式接收的訊息轉換成下列其中一個 hello:</span><span class="sxs-lookup"><span data-stu-id="3429d-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="3429d-132">編譯 hello 模組</span><span class="sxs-lookup"><span data-stu-id="3429d-132">Compile hello module</span></span>

<span data-ttu-id="3429d-133">toocompile hello 模組，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="3429d-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="3429d-134">您取得`libmy_module.so`檔案 hello 編譯完成之後。</span><span class="sxs-lookup"><span data-stu-id="3429d-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="3429d-135">記下 hello 此檔案的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="3429d-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="3429d-136">新增 hello 模組 toohello b 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="3429d-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="3429d-137">藉由執行下列命令的 hello 移 toohello 範例資料夾中：</span><span class="sxs-lookup"><span data-stu-id="3429d-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="3429d-138">執行下列命令的 hello 開啟 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="3429d-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="3429d-139">將模組插入下列程式碼 toohello hello `modules` > 一節。</span><span class="sxs-lookup"><span data-stu-id="3429d-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

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

1. <span data-ttu-id="3429d-140">取代`[Your libmy_module.so path]`hello hello libmy_module.so hello 絕對路徑的程式碼中 ' 檔案。</span><span class="sxs-lookup"><span data-stu-id="3429d-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="3429d-141">Hello 中的 hello 程式碼取代`links`以 hello 下列其中一節：</span><span class="sxs-lookup"><span data-stu-id="3429d-141">Replace hello code in hello `links` section with hello following one:</span></span>

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

1. <span data-ttu-id="3429d-142">按`ESC`，然後輸入`:wq`toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="3429d-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="3429d-143">執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="3429d-143">Run hello sample application</span></span>

1. <span data-ttu-id="3429d-144">Hello SensorTag 電源。</span><span class="sxs-lookup"><span data-stu-id="3429d-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="3429d-145">執行下列命令的 hello 設定 hello SSL_CERT_FILE 環境變數：</span><span class="sxs-lookup"><span data-stu-id="3429d-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="3429d-146">執行下列命令的 hello hello 範例應用程式執行與 hello 加入的模組：</span><span class="sxs-lookup"><span data-stu-id="3429d-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="3429d-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3429d-147">Next steps</span></span>

<span data-ttu-id="3429d-148">已成功使用 hello IoT 閘道 tooconvert hello 訊息從 SensorTag 成 hello.json 格式。</span><span class="sxs-lookup"><span data-stu-id="3429d-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
