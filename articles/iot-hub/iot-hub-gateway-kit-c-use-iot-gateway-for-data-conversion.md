---
title: "在 IoT 閘道上使用 Azure IoT Edge 進行資料轉換 | Microsoft Docs"
description: "使用 IoT 閘道可從 Azure IoT Edge 透過自訂模組轉換感應器資料的格式。"
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
ms.openlocfilehash: d5c735a4adbc59e9526ec4fd40720c5ec136d63d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="a7e9d-104">搭配 Azure IoT Edge 使用 IoT 閘道進行感應器資料轉換</span><span class="sxs-lookup"><span data-stu-id="a7e9d-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="a7e9d-105">開始本教學課程之前，請確定您循序完成下列課程：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-105">Before you start this tutorial, make sure you’ve completed the following lessons in sequence:</span></span>
> * [<span data-ttu-id="a7e9d-106">將 Intel NUC 設定為 IoT 閘道</span><span class="sxs-lookup"><span data-stu-id="a7e9d-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="a7e9d-107">使用 IoT 閘道將裝置連接到雲端 - SensorTag 至 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="a7e9d-107">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="a7e9d-108">IoT 閘道的其中一個用途是要在傳送資料至雲端之前處理所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-108">One purpose of an Iot gateway is to process collected data before sending it to the cloud.</span></span> <span data-ttu-id="a7e9d-109">Azure IoT Edge 推出的模組可用來建立和組合以形成資料處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-109">Azure IoT Edge introduces modules which can be created and assembled to form the data processing workflow.</span></span> <span data-ttu-id="a7e9d-110">模組會接收訊息、對其執行某個動作，然後移動它，以供其他模組處理。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-110">A module receives a message, performs some action on it, and then move it on for other modules to process.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="a7e9d-111">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="a7e9d-111">What you learn</span></span>

<span data-ttu-id="a7e9d-112">您了解如何建立模組，將訊息從 SensorTag 轉換成不同格式。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-112">You learn how to create a module to convert messages from the SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="a7e9d-113">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="a7e9d-113">What you do</span></span>

* <span data-ttu-id="a7e9d-114">建立模組，將已接收的訊息轉換成 .json 格式。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-114">Create a module to convert a received message into the .json format.</span></span>
* <span data-ttu-id="a7e9d-115">編譯模組。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-115">Compile the module.</span></span>
* <span data-ttu-id="a7e9d-116">透過 Azure IoT Edge 將模組新增至 BLE 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-116">Add the module to the BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="a7e9d-117">執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-117">Run the sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a7e9d-118">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="a7e9d-118">What you need</span></span>

* <span data-ttu-id="a7e9d-119">循序完成下列教學課程：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-119">The following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="a7e9d-120">將 Intel NUC 設定為 IoT 閘道</span><span class="sxs-lookup"><span data-stu-id="a7e9d-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="a7e9d-121">使用 IoT 閘道將裝置連接到雲端 - SensorTag 至 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="a7e9d-121">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="a7e9d-122">在主機電腦上執行的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="a7e9d-123">Windows 上建議使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="a7e9d-124">Linux 和 macOS 已隨附 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="a7e9d-125">從 SSH 用戶端存取閘道所用的 IP 位址和使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-125">The IP address and the username and password to access the gateway from the SSH client.</span></span>
* <span data-ttu-id="a7e9d-126">網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="a7e9d-127">建立模組</span><span class="sxs-lookup"><span data-stu-id="a7e9d-127">Create a module</span></span>

1. <span data-ttu-id="a7e9d-128">在主機電腦上，執行 SSH 用戶端並連線至 IoT 閘道。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-128">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="a7e9d-129">執行下列命令，將轉換模組的原始程式檔從 GitHub 複製到 IoT 閘道的主目錄：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-129">Clone the source files of the conversion module from GitHub to the home directory of the IoT gateway by running the following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="a7e9d-130">這是以 C 程式設計語言撰寫的原生 Azure Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-130">This is a native Azure Edge module written in the C programming language.</span></span> <span data-ttu-id="a7e9d-131">模組會將所接收訊息的格式轉換成下列其中一個：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-131">The module converts the format of received messages into the following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-the-module"></a><span data-ttu-id="a7e9d-132">編譯模組</span><span class="sxs-lookup"><span data-stu-id="a7e9d-132">Compile the module</span></span>

<span data-ttu-id="a7e9d-133">若要編譯模組，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-133">To compile the module, run the following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change the build script runnable
chmod 777 build.sh
# remove the invalid windows character
sed -i -e "s/\r$//" build.sh
# run the build shell script
./build.sh
```

<span data-ttu-id="a7e9d-134">編譯完成之後，您會得到 `libmy_module.so` 檔案。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-134">You get a `libmy_module.so` file after the compile is completed.</span></span> <span data-ttu-id="a7e9d-135">記下此檔案的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-135">Make a note of the absolute path of this file.</span></span>

## <a name="add-the-module-to-the-ble-sample-application"></a><span data-ttu-id="a7e9d-136">將模組新增至 BLE 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="a7e9d-136">Add the module to the BLE sample application</span></span>

1. <span data-ttu-id="a7e9d-137">執行下列命令來前往範例資料夾：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-137">Go to the samples folder by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="a7e9d-138">執行下列命令來開啟組態檔：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-138">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="a7e9d-139">插入下列程式碼至 `modules` 區段來新增模組。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-139">Add a module by inserting the following code to the `modules` section.</span></span>

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

1. <span data-ttu-id="a7e9d-140">將程式碼中的 `[Your libmy_module.so path]` 取代為 libmy_module.so 檔案的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-140">Replace `[Your libmy_module.so path]` in the code with the absolute path of the libmy_module.so\` file.</span></span>
1. <span data-ttu-id="a7e9d-141">使用下列程式碼取代 `links` 區段中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-141">Replace the code in the `links` section with the following one:</span></span>

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

1. <span data-ttu-id="a7e9d-142">按下 `ESC` 然後輸入 `:wq` 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-142">Press `ESC`, and then type `:wq` to save the file.</span></span>

## <a name="run-the-sample-application"></a><span data-ttu-id="a7e9d-143">執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="a7e9d-143">Run the sample application</span></span>

1. <span data-ttu-id="a7e9d-144">開啟 SensorTag 的電源。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-144">Power on the SensorTag.</span></span>
1. <span data-ttu-id="a7e9d-145">執行下列命令來設定 SSL_CERT_FILE 環境變數：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-145">Set the SSL_CERT_FILE environment variable by running the following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="a7e9d-146">執行下列命令來使用新增的模組執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="a7e9d-146">Run the sample application with the added module by running the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="a7e9d-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7e9d-147">Next steps</span></span>

<span data-ttu-id="a7e9d-148">您已成功使用 IoT 閘道將訊息從 SensorTag 轉換為 .json 格式。</span><span class="sxs-lookup"><span data-stu-id="a7e9d-148">You’ve successfully use the IoT gateway to convert the message from SensorTag into the .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
