---
title: "使用 IoT 閘道將裝置連線到 Azure IoT 中樞 | Microsoft Docs"
description: "了解如何使用 Intel NUC IoT 閘道連接 TI SensorTag 感應器，並將資料傳送至雲端的 Azure IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 閘道器將裝置連接至雲端"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 4fb77ed0241d15338c2574fd22828507c3e40cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-to-connect-things-to-the-cloud---sensortag-to-azure-iot-hub"></a><span data-ttu-id="f73d4-104">使用 IoT 閘道將裝置連接到雲端 - 將 SensorTag 連接到 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="f73d4-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="f73d4-105">開始本教學課程之前，請確定您已完成[將 Intel NUC 設定為 IoT 閘道器](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)。</span><span class="sxs-lookup"><span data-stu-id="f73d4-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="f73d4-106">在[將 Intel NUC 設定為 IoT 閘道器](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)中，您會將 Intel NUC 裝置設定為 IoT 閘道器。</span><span class="sxs-lookup"><span data-stu-id="f73d4-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f73d4-107">學習目標</span><span class="sxs-lookup"><span data-stu-id="f73d4-107">What you will learn</span></span>

<span data-ttu-id="f73d4-108">您將學習如何使用 IoT 閘道器，將 Texas Instruments SensorTag (CC2650STK) 連接到 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f73d4-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span></span> <span data-ttu-id="f73d4-109">IoT 閘道會將從 SensorTag 收集的溫度和溼度資料傳送到 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f73d4-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f73d4-110">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="f73d4-110">What you will do</span></span>

- <span data-ttu-id="f73d4-111">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f73d4-111">Create an IoT hub.</span></span>
- <span data-ttu-id="f73d4-112">在 SensorTag 的 IoT 中樞註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="f73d4-112">Register a device in the IoT hub for the SensorTag.</span></span>
- <span data-ttu-id="f73d4-113">啟用 IoT 閘道與 SensorTag 之間的連線。</span><span class="sxs-lookup"><span data-stu-id="f73d4-113">Enable the connection between the IoT gateway and the SensorTag.</span></span>
- <span data-ttu-id="f73d4-114">執行 BLE 應用程式，將 SensorTag 資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f73d4-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f73d4-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="f73d4-115">What you need</span></span>

- <span data-ttu-id="f73d4-116">在[將 Intel NUC 設定為 IoT 閘道器](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)教學課程中，您已將 Intel NUC 設定為 IoT 閘道器。</span><span class="sxs-lookup"><span data-stu-id="f73d4-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="f73d4-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f73d4-117">An active Azure subscription.</span></span> <span data-ttu-id="f73d4-118">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="f73d4-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="f73d4-119">在主機電腦上執行的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f73d4-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="f73d4-120">Windows 上建議使用 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="f73d4-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="f73d4-121">Linux 和 macOS 已隨附 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f73d4-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="f73d4-122">從 SSH 用戶端存取閘道所用的 IP 位址和使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f73d4-122">The IP address and the username and password to access the gateway from the SSH client.</span></span>
- <span data-ttu-id="f73d4-123">網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="f73d4-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="f73d4-124">您將在這裡為 SensorTag 註冊這個新裝置</span><span class="sxs-lookup"><span data-stu-id="f73d4-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-the-connection-between-the-iot-gateway-and-the-sensortag"></a><span data-ttu-id="f73d4-125">啟用 IoT 閘道與 SensorTag 之間的連線</span><span class="sxs-lookup"><span data-stu-id="f73d4-125">Enable the connection between the IoT gateway and the SensorTag</span></span>

<span data-ttu-id="f73d4-126">本節中，您將執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="f73d4-126">In this section, you perform the following tasks:</span></span>

- <span data-ttu-id="f73d4-127">對於藍牙連線取得 SensorTag 的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="f73d4-127">Get the MAC address of the SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="f73d4-128">初始化從 IoT 閘道器到 SensorTag 的藍牙連線。</span><span class="sxs-lookup"><span data-stu-id="f73d4-128">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span></span>

### <a name="get-the-mac-address-of-the-sensortag-for-bluetooth-connection"></a><span data-ttu-id="f73d4-129">對於藍牙連線取得 SensorTag 的 MAC 位址</span><span class="sxs-lookup"><span data-stu-id="f73d4-129">Get the MAC address of the SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="f73d4-130">在主機電腦上執行 SSH 用戶端，並連接到 IoT 閘道器。</span><span class="sxs-lookup"><span data-stu-id="f73d4-130">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="f73d4-131">執行下列命令解除封鎖藍牙︰</span><span class="sxs-lookup"><span data-stu-id="f73d4-131">Unblock Bluetooth by running the following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="f73d4-132">在 IoT 閘道上啟動藍牙服務，並執行下列命令進入藍牙介面設定藍牙︰</span><span class="sxs-lookup"><span data-stu-id="f73d4-132">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="f73d4-133">在藍牙介面執行下列命令，開啟藍牙控制器電源︰</span><span class="sxs-lookup"><span data-stu-id="f73d4-133">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![使用 bluetoothctl 在 IoT 閘道器上開啟藍牙控制器電源](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="f73d4-135">執行下列命令，開始掃描附近的藍牙裝置︰</span><span class="sxs-lookup"><span data-stu-id="f73d4-135">Start scanning for nearby Bluetooth devices by running the following command:</span></span>

   ```bash
   scan on
   ```

   ![使用 bluetoothctl 掃描附近的藍牙裝置](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="f73d4-137">按下 SensorTag 上的配對按鈕。</span><span class="sxs-lookup"><span data-stu-id="f73d4-137">Press the pairing button on the SensorTag.</span></span> <span data-ttu-id="f73d4-138">SensorTag 上的綠色 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="f73d4-138">The green LED on the SensorTag flashes.</span></span>
1. <span data-ttu-id="f73d4-139">在藍牙介面中，您應該會看見找到 SensorTag。</span><span class="sxs-lookup"><span data-stu-id="f73d4-139">At the Bluetooth shell, you should see the SensorTag is found.</span></span> <span data-ttu-id="f73d4-140">記下 SensorTag 的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="f73d4-140">Make a note of the MAC address of the SensorTag.</span></span> <span data-ttu-id="f73d4-141">在此範例中，SensorTag 的 MAC 位址是 `24:71:89:C0:7F:82`。</span><span class="sxs-lookup"><span data-stu-id="f73d4-141">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="f73d4-142">執行下列命令以關閉掃描：</span><span class="sxs-lookup"><span data-stu-id="f73d4-142">Turn off the scan by running the following command:</span></span>

   ```bash
   scan off
   ```

   ![使用 bluetoothctl 停止掃描附近的藍牙裝置](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-the-iot-gateway-to-the-sensortag"></a><span data-ttu-id="f73d4-144">初始化從 IoT 閘道器到 SensorTag 的藍牙連線</span><span class="sxs-lookup"><span data-stu-id="f73d4-144">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span></span>

1. <span data-ttu-id="f73d4-145">執行下列命令來連線至 SensorTag：</span><span class="sxs-lookup"><span data-stu-id="f73d4-145">Connect to the SensorTag by running the following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![使用 bluetoothctl 連接到 SensorTag](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="f73d4-147">執行下列命令，與 SensorTag 中斷連接並結束藍牙介面︰</span><span class="sxs-lookup"><span data-stu-id="f73d4-147">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![使用 bluetoothctl 與 SensorTag 中斷連接](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="f73d4-149">此時即已成功啟用 SensorTag 與 IoT 閘道之間的連線。</span><span class="sxs-lookup"><span data-stu-id="f73d4-149">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-to-send-sensortag-data-to-your-iot-hub"></a><span data-ttu-id="f73d4-150">執行 BLE 應用程式，將 SensorTag 資料傳送至 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="f73d4-150">Run a BLE sample application to send SensorTag data to your IoT hub</span></span>

<span data-ttu-id="f73d4-151">Bluetooth Low Energy (BLE) 範例應用程式是由 Azure IoT Edge 提供。</span><span class="sxs-lookup"><span data-stu-id="f73d4-151">The Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="f73d4-152">範例應用程式會收集 BLE 連線的資料，並將資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f73d4-152">The sample application collects data from BLE connection and send the data to you IoT hub.</span></span> <span data-ttu-id="f73d4-153">若要執行範例應用程式，需要：</span><span class="sxs-lookup"><span data-stu-id="f73d4-153">To run the sample application, you need to:</span></span>

1. <span data-ttu-id="f73d4-154">設定範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f73d4-154">Configure the sample application.</span></span>
1. <span data-ttu-id="f73d4-155">在 IoT 閘道器上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f73d4-155">Run the sample application on the IoT gateway.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="f73d4-156">設定範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f73d4-156">Configure the sample application</span></span>

1. <span data-ttu-id="f73d4-157">執行下列命令，移至範例應用程式的資料夾：</span><span class="sxs-lookup"><span data-stu-id="f73d4-157">Go to the folder of the sample application by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="f73d4-158">執行下列命令來開啟組態檔：</span><span class="sxs-lookup"><span data-stu-id="f73d4-158">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="f73d4-159">在組態檔中，輸入下列值︰</span><span class="sxs-lookup"><span data-stu-id="f73d4-159">In the configuration file, fill in the following values:</span></span>

   <span data-ttu-id="f73d4-160">**IoTHubName**：IoT 中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="f73d4-160">**IoTHubName**: The name of your IoT hub.</span></span>

   <span data-ttu-id="f73d4-161">**IoTHubSuffix**︰從您記下的裝置連接字串主索引鍵，取得 IoTHubSuffix。</span><span class="sxs-lookup"><span data-stu-id="f73d4-161">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span></span> <span data-ttu-id="f73d4-162">請確定您取得裝置連接字串的主索引鍵，而非 IoT 中樞連接字串的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f73d4-162">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span></span> <span data-ttu-id="f73d4-163">裝置連接字串的主索引鍵格式為 `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`。</span><span class="sxs-lookup"><span data-stu-id="f73d4-163">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="f73d4-164">**Transport**：預設值是 `amqp`。</span><span class="sxs-lookup"><span data-stu-id="f73d4-164">**Transport**: The default value is `amqp`.</span></span> <span data-ttu-id="f73d4-165">這個值會顯示傳輸期間的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="f73d4-165">This value shows the protocol during transpotation.</span></span> <span data-ttu-id="f73d4-166">這可以是 `http`、`amqp` 或 `mqtt`。</span><span class="sxs-lookup"><span data-stu-id="f73d4-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="f73d4-167">**macAddress**：您對於 SensorTag 記下的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="f73d4-167">**macAddress**: The MAC address of the SensorTag that you noted down.</span></span>

   <span data-ttu-id="f73d4-168">**deviceID**︰ 您建立 IoT 中樞建立的裝置本身的識別碼。</span><span class="sxs-lookup"><span data-stu-id="f73d4-168">**deviceID**: ID of the device that you created in your IoT hub.</span></span>

   <span data-ttu-id="f73d4-169">**deviceKey**：裝置連接字串的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f73d4-169">**deviceKey**: The primary key of the device connection string.</span></span>

   ![完成 BLE 範例應用程式的組態檔](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="f73d4-171">按下 `ESC` 並輸入 `:wq` 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f73d4-171">Press `ESC` and type `:wq` to save the file.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="f73d4-172">執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f73d4-172">Run the sample application</span></span>

1. <span data-ttu-id="f73d4-173">確定 SensorTag 已開啟。</span><span class="sxs-lookup"><span data-stu-id="f73d4-173">Make sure the SensorTag is powered on.</span></span>
1. <span data-ttu-id="f73d4-174">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="f73d4-174">Run the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="f73d4-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f73d4-175">Next steps</span></span>

[<span data-ttu-id="f73d4-176">搭配 Azure IoT Edge 使用 IoT 閘道進行感應器資料轉換</span><span class="sxs-lookup"><span data-stu-id="f73d4-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
