---
title: "aaaUse IoT 閘道 tooconnect 裝置 tooAzure IoT 中樞 |Microsoft 文件"
description: "了解 toouse 為 IoT 閘道 tooconnect TI SensorTag Intel NUC 和傳送感應器資料 tooAzure IoT 中樞 hello 中的雲端。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 閘道連接裝置 toocloud"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="8e396-104">使用 IoT 閘道 tooconnect 事項 toohello 雲端 SensorTag tooAzure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8e396-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="8e396-105">開始本教學課程之前，請確定您已完成[將 Intel NUC 設定為 IoT 閘道器](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)。</span><span class="sxs-lookup"><span data-stu-id="8e396-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="8e396-106">在[設定為 IoT 閘道 Intel NUC](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)，您設定 hello Intel NUC 裝置與 IoT 閘道。</span><span class="sxs-lookup"><span data-stu-id="8e396-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8e396-107">學習目標</span><span class="sxs-lookup"><span data-stu-id="8e396-107">What you will learn</span></span>

<span data-ttu-id="8e396-108">您了解如何 toouse IoT 閘道 tooconnect 德州儀器 SensorTag (CC2650STK) tooAzure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8e396-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="8e396-109">hello IoT 閘道傳送溫度和溼度從收集的資料 hello SensorTag tooAzure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8e396-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8e396-110">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="8e396-110">What you will do</span></span>

- <span data-ttu-id="8e396-111">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8e396-111">Create an IoT hub.</span></span>
- <span data-ttu-id="8e396-112">在 hello SensorTag hello IoT 中樞註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="8e396-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="8e396-113">啟用 hello hello IoT 閘道與 hello SensorTag 之間的連線。</span><span class="sxs-lookup"><span data-stu-id="8e396-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="8e396-114">執行 b 範例應用程式 toosend SensorTag 資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8e396-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8e396-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="8e396-115">What you need</span></span>

- <span data-ttu-id="8e396-116">在[將 Intel NUC 設定為 IoT 閘道器](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)教學課程中，您已將 Intel NUC 設定為 IoT 閘道器。</span><span class="sxs-lookup"><span data-stu-id="8e396-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="8e396-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e396-117">An active Azure subscription.</span></span> <span data-ttu-id="8e396-118">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="8e396-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="8e396-119">在主機電腦上執行的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="8e396-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="8e396-120">Windows 上建議使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="8e396-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="8e396-121">Linux 和 macOS 已隨附 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="8e396-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="8e396-122">hello IP 位址和 hello 使用者名稱和密碼 tooaccess hello hello SSH 用戶端的閘道。</span><span class="sxs-lookup"><span data-stu-id="8e396-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="8e396-123">網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="8e396-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="8e396-124">您將在這裡為 SensorTag 註冊這個新裝置</span><span class="sxs-lookup"><span data-stu-id="8e396-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="8e396-125">啟用 hello hello IoT 閘道與 hello SensorTag 之間的連線</span><span class="sxs-lookup"><span data-stu-id="8e396-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="8e396-126">在本節中，您可以執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e396-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="8e396-127">取得藍芽連線 hello SensorTag hello MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="8e396-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="8e396-128">起始從 hello IoT 閘道 toohello SensorTag 藍芽連線。</span><span class="sxs-lookup"><span data-stu-id="8e396-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="8e396-129">取得藍芽連線 hello SensorTag hello MAC 位址</span><span class="sxs-lookup"><span data-stu-id="8e396-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="8e396-130">Hello 主機電腦上，執行 hello SSH 用戶端，並連接 toohello IoT 閘道。</span><span class="sxs-lookup"><span data-stu-id="8e396-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="8e396-131">解除封鎖藍芽，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e396-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="8e396-132">Hello IoT 閘道上啟動 hello 藍芽服務，並輸入 藍芽殼層 tooconfigure 藍芽執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="8e396-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="8e396-133">藉由執行 hello 藍芽控制站上的電源 hello 下列在 hello 藍芽介面的命令：</span><span class="sxs-lookup"><span data-stu-id="8e396-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![hello 與 bluetoothctl hello IoT 閘道上的藍芽控制站上的電源](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="8e396-135">啟動掃描附近的藍芽裝置執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e396-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![使用 bluetoothctl 掃描附近的藍牙裝置](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="8e396-137">按 hello 配對 hello SensorTag 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8e396-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="8e396-138">hello 綠色 LED 上 hello SensorTag 閃爍。</span><span class="sxs-lookup"><span data-stu-id="8e396-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="8e396-139">在 hello 藍芽介面，您應該會看到的 hello SensorTag 找到。</span><span class="sxs-lookup"><span data-stu-id="8e396-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="8e396-140">記下 hello hello SensorTag MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="8e396-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="8e396-141">在此範例中，是 hello MAC 位址的 hello SensorTag `24:71:89:C0:7F:82`。</span><span class="sxs-lookup"><span data-stu-id="8e396-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="8e396-142">執行下列命令的 hello 關閉 hello 掃描：</span><span class="sxs-lookup"><span data-stu-id="8e396-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![使用 bluetoothctl 停止掃描附近的藍牙裝置](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="8e396-144">起始從 hello IoT 閘道 toohello SensorTag 藍芽連線</span><span class="sxs-lookup"><span data-stu-id="8e396-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="8e396-145">執行下列命令的 hello 連線 toohello SensorTag:</span><span class="sxs-lookup"><span data-stu-id="8e396-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![連接 bluetoothctl toohello SensorTag](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="8e396-147">Hello SensorTag 從中斷連線並執行下列命令的 hello 結束 hello 藍芽介面：</span><span class="sxs-lookup"><span data-stu-id="8e396-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![中斷與 bluetoothctl hello SensorTag](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="8e396-149">您已成功啟用 hello hello SensorTag 與 hello IoT 閘道之間的連線。</span><span class="sxs-lookup"><span data-stu-id="8e396-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="8e396-150">執行 b 範例應用程式 toosend SensorTag 資料 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8e396-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="8e396-151">hello 藍芽低能源 (B) 的範例應用程式會提供 Azure IoT 邊緣。</span><span class="sxs-lookup"><span data-stu-id="8e396-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="8e396-152">hello 範例應用程式會收集從 b 連接，並傳送嗨資料 tooyou IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8e396-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="8e396-153">您需要 toorun hello 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="8e396-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="8e396-154">Hello 範例應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="8e396-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="8e396-155">Hello IoT 閘道上執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="8e396-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="8e396-156">Hello 範例應用程式設定</span><span class="sxs-lookup"><span data-stu-id="8e396-156">Configure hello sample application</span></span>

1. <span data-ttu-id="8e396-157">藉由執行下列命令的 hello 移 toohello hello 範例應用程式的資料夾：</span><span class="sxs-lookup"><span data-stu-id="8e396-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="8e396-158">執行下列命令的 hello 開啟 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="8e396-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="8e396-159">在 hello 設定檔中，填入 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="8e396-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="8e396-160">**IoTHubName**: hello IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="8e396-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="8e396-161">**IoTHubSuffix**： 取得 IoTHubSuffix 從 hello 主索引鍵的 hello 裝置連接字串，您記下下。</span><span class="sxs-lookup"><span data-stu-id="8e396-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="8e396-162">請確定您取得 hello 裝置連接字串 hello 主索引鍵，且不 hello IoT 中樞連接字串的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8e396-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="8e396-163">hello 主索引鍵的 hello 裝置連接字串的格式的 hello `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`。</span><span class="sxs-lookup"><span data-stu-id="8e396-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="8e396-164">**傳輸**: hello 預設值是`amqp`。</span><span class="sxs-lookup"><span data-stu-id="8e396-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="8e396-165">這個值會顯示 hello 通訊協定 transpotation 期間。</span><span class="sxs-lookup"><span data-stu-id="8e396-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="8e396-166">這可以是 `http`、`amqp` 或 `mqtt`。</span><span class="sxs-lookup"><span data-stu-id="8e396-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="8e396-167">**macAddress**: hello hello SensorTag 您記下的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="8e396-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="8e396-168">**deviceID**： 您建立 IoT 中樞中的 hello 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="8e396-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="8e396-169">**deviceKey**: hello 裝置連接字串 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8e396-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![完整的 hello 的 hello b 範例應用程式的組態檔](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="8e396-171">按`ESC`和型別`:wq`toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="8e396-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="8e396-172">執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="8e396-172">Run hello sample application</span></span>

1. <span data-ttu-id="8e396-173">請確定 hello SensorTag 電源已開啟。</span><span class="sxs-lookup"><span data-stu-id="8e396-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="8e396-174">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e396-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="8e396-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e396-175">Next steps</span></span>

[<span data-ttu-id="8e396-176">搭配 Azure IoT Edge 使用 IoT 閘道進行感應器資料轉換</span><span class="sxs-lookup"><span data-stu-id="8e396-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
