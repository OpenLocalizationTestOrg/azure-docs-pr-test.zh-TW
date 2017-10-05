---
title: "使用 Intel NUC 將閘道連線到 Azure IoT 套件 | Microsoft Docs"
description: "使用 Microsoft IoT Commercial Gateway Kit 和預先設定的遠端監視解決方案。 使用 Azure IoT Edge 閘道，讓 SensorTag 裝置連線到遠端監視解決方案、將遙測傳送到雲端，並回應解決方案儀表板所叫用的方法。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: bda16be1094276fcecef1e708f9d7db307d94a89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="66abb-104">將 Azure IoT Edge 閘道連線到預先設定的遠端監視解決方案，並從 SensorTag 傳送遙測</span><span class="sxs-lookup"><span data-stu-id="66abb-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="66abb-105">本教學課程說明如何使用 Azure IoT Edge 將 SensorTag 裝置中的溫度和溼度資料傳送至預先設定的遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="66abb-105">This tutorial shows you how to use Azure IoT Edge to send temperature and humidity data from SensorTag device to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="66abb-106">SensorTag 會使用藍牙來連線到 Intel NUC 閘道。</span><span class="sxs-lookup"><span data-stu-id="66abb-106">The SensorTag connects to the Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="66abb-107">教學課程會使用：</span><span class="sxs-lookup"><span data-stu-id="66abb-107">The tutorial uses:</span></span>

- <span data-ttu-id="66abb-108">Azure IoT Edge，以實作範例閘道。</span><span class="sxs-lookup"><span data-stu-id="66abb-108">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="66abb-109">IoT 套件遠端監視預先設定解決方案作為以雲端為基礎的後端。</span><span class="sxs-lookup"><span data-stu-id="66abb-109">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="66abb-110">概觀</span><span class="sxs-lookup"><span data-stu-id="66abb-110">Overview</span></span>

<span data-ttu-id="66abb-111">在本教學課程中，您會完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66abb-111">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="66abb-112">將遠端監視預先設定解決方案的執行個體部署至您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66abb-112">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="66abb-113">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="66abb-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="66abb-114">設定 Intel NUC 閘道裝置，以便與您的電腦和遠端監視解決方案進行通訊。</span><span class="sxs-lookup"><span data-stu-id="66abb-114">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="66abb-115">將 Intel NUC 閘道設定為接收 SensorTag 裝置中的遙測資料，並將資料傳送至遠端監視儀表板。</span><span class="sxs-lookup"><span data-stu-id="66abb-115">Set up your Intel NUC gateway to receive telemetry from a SensorTag device and send it to the remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="66abb-116">[Texas Instruments BLE SensorTag][lnk-sensortag]。</span><span class="sxs-lookup"><span data-stu-id="66abb-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="66abb-117">本教學課程會透過藍牙從 SensorTag 裝置擷取遙測資料。</span><span class="sxs-lookup"><span data-stu-id="66abb-117">This tutorial retrieves telemetry data over Bluetooth from the SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="66abb-118">遠端監視解決方案會佈建一組 Azure 訂用帳戶中的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="66abb-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="66abb-119">部署會反映實際的企業架構。</span><span class="sxs-lookup"><span data-stu-id="66abb-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="66abb-120">若要避免不必要的 Azure 耗用量費用，當您使用完 azureiotsuite.com 中預先設定解決方案的執行個體時，請將它刪除。</span><span class="sxs-lookup"><span data-stu-id="66abb-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="66abb-121">如果您還需要預先設定的解決方案，可以輕鬆地將它重新建立。</span><span class="sxs-lookup"><span data-stu-id="66abb-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="66abb-122">如需將遠端監視解決方案執行時的耗用量降低的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案以供示範][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="66abb-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="66abb-123">設定藍牙連線</span><span class="sxs-lookup"><span data-stu-id="66abb-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="66abb-124">設定 Intel NUC 上的藍牙功能，讓 SensorTag 裝置能夠連線並傳送遙測資料。</span><span class="sxs-lookup"><span data-stu-id="66abb-124">Configure Bluetooth on the Intel NUC to enable the SensorTag device to connect and send telemetry.</span></span>

### <a name="find-the-mac-address-of-the-sensortag"></a><span data-ttu-id="66abb-125">尋找 SensorTag 的 MAC 位址</span><span class="sxs-lookup"><span data-stu-id="66abb-125">Find the MAC address of the SensorTag</span></span>

1. <span data-ttu-id="66abb-126">在 Intel NUC 的殼層中執行下列命令，以將藍牙服務解除封鎖︰</span><span class="sxs-lookup"><span data-stu-id="66abb-126">In the shell on the Intel NUC, run the following command to unblock the Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="66abb-127">執行下列命令，以啟動 Intel NUC 上的藍牙服務，然後輸入藍牙殼層︰</span><span class="sxs-lookup"><span data-stu-id="66abb-127">Run the following commands to start the Bluetooth service on the Intel NUC and enter the Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="66abb-128">執行下列命令以開啟藍牙控制器電源︰</span><span class="sxs-lookup"><span data-stu-id="66abb-128">Run the following command to power on the Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="66abb-129">控制器開啟電源時，您會看到訊息指出**已成功開啟電源**。</span><span class="sxs-lookup"><span data-stu-id="66abb-129">When the controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="66abb-130">執行下列命令，以掃描附近的藍牙裝置︰</span><span class="sxs-lookup"><span data-stu-id="66abb-130">Run the following command to scan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="66abb-131">按下 SensorTag 上的電源按鈕，使其可供探索。</span><span class="sxs-lookup"><span data-stu-id="66abb-131">Press the power button on the SensorTag to make it discoverable.</span></span> <span data-ttu-id="66abb-132">綠色 LED 燈會閃爍。</span><span class="sxs-lookup"><span data-stu-id="66abb-132">The green LED flashes.</span></span>

1. <span data-ttu-id="66abb-133">當您看到殼層中的訊息指出控制器已發現 SensorTag 時，記下裝置的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="66abb-133">When you see a message in the shell that the controller has discovered the SensorTag, make a note of the MAC address of the device.</span></span> <span data-ttu-id="66abb-134">MAC 位址的格式類似 **A0:E6:F8:B5:F6:00**。</span><span class="sxs-lookup"><span data-stu-id="66abb-134">The MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="66abb-135">在本教學課程稍後設定閘道時，您需要這個 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="66abb-135">You need the MAC address later in the tutorial when you configure the gateway.</span></span>

1. <span data-ttu-id="66abb-136">執行下列命令來關閉藍牙掃描︰</span><span class="sxs-lookup"><span data-stu-id="66abb-136">Run the following command to turn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="66abb-137">執行下列命令，以確認您可以連線到 SensorTag 裝置︰</span><span class="sxs-lookup"><span data-stu-id="66abb-137">Run the following command to verify that you can connect to the SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="66abb-138">如果您連線成功，殼層會顯示訊息來指出**連線成功**，並列印出 SensorTag 裝置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="66abb-138">If you connect successfully, the shell shows the message **Connection successful** and prints information about the SensorTag device.</span></span> <span data-ttu-id="66abb-139">如果您無法連線，請檢查 SensorTag 的電源是否仍開啟。</span><span class="sxs-lookup"><span data-stu-id="66abb-139">If you cannot connect, check the SensorTag is still powered on.</span></span>

1. <span data-ttu-id="66abb-140">您現在可以執行下列命令，來與 SensorTag 中斷連線並結束藍牙殼層︰</span><span class="sxs-lookup"><span data-stu-id="66abb-140">You can now disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="66abb-141">建置自訂的 IoT Edge 模組</span><span class="sxs-lookup"><span data-stu-id="66abb-141">Build the custom IoT Edge module</span></span>

<span data-ttu-id="66abb-142">您現在可以建置自訂的 IoT Edge 模組，以讓閘道傳送訊息給遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="66abb-142">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="66abb-143">如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。</span><span class="sxs-lookup"><span data-stu-id="66abb-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="66abb-144">使用下列命令，從 GitHub 下載自訂 IoT Edge 模組的原始程式碼︰</span><span class="sxs-lookup"><span data-stu-id="66abb-144">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="66abb-145">使用下列命令來建置自訂的 IoT Edge 模組︰</span><span class="sxs-lookup"><span data-stu-id="66abb-145">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="66abb-146">建置指令碼會將 libsensor2remotemonitoring.so 自訂 IoT Edge 模組放置在建置資料夾中。</span><span class="sxs-lookup"><span data-stu-id="66abb-146">The build script places the libsensor2remotemonitoring.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="66abb-147">設定和執行 IoT Edge 閘道</span><span class="sxs-lookup"><span data-stu-id="66abb-147">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="66abb-148">您現在可以將 IoT Edge 閘道設定為將 SensorTag 裝置中的遙測資料傳送到遠端監視儀表板。</span><span class="sxs-lookup"><span data-stu-id="66abb-148">You can now configure the IoT Edge gateway to send telemetry from your SensorTag device to your remote monitoring dashboard.</span></span> <span data-ttu-id="66abb-149">如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。</span><span class="sxs-lookup"><span data-stu-id="66abb-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="66abb-150">在本教學課程中，您可以使用 Intel NUC 上的標準 `vi` 文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="66abb-150">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="66abb-151">如果您之前未使用過 `vi`，請先完成入門教學課程 (例如 [Unix - The vi Editor Tutorial][lnk-vi-tutorial] ) 以熟悉這個編輯器。</span><span class="sxs-lookup"><span data-stu-id="66abb-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="66abb-152">或者，您可以使用 `smart install nano -y` 命令，來安裝更方便使用的 [nano](https://www.nano-editor.org/) 編輯器。</span><span class="sxs-lookup"><span data-stu-id="66abb-152">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="66abb-153">使用下列命令，將 **vi** 編輯器中的範例組態檔開啟︰</span><span class="sxs-lookup"><span data-stu-id="66abb-153">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="66abb-154">在 IoTHub 模組的組態中找出下列幾行︰</span><span class="sxs-lookup"><span data-stu-id="66abb-154">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="66abb-155">將預留位置值取代為本教學課程開頭所建立及儲存的 IoT 中樞資訊。</span><span class="sxs-lookup"><span data-stu-id="66abb-155">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="66abb-156">IoTHubName 的值會像 **yourrmsolution37e08**，IoTSuffix 的值則通常是 **azure-devices.net**。</span><span class="sxs-lookup"><span data-stu-id="66abb-156">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="66abb-157">在對應模組的組態中找出下列幾行︰</span><span class="sxs-lookup"><span data-stu-id="66abb-157">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="66abb-158">將 **macAddress** 預留位置取代為您先前記下的 SensorTag MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="66abb-158">Replace the **macAddress** placeholder with the MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="66abb-159">將 **deviceID** 和 **deviceKey** 預留位置取代為您先前在遠端監視解決方案中所建立之兩個裝置的識別碼和金鑰。</span><span class="sxs-lookup"><span data-stu-id="66abb-159">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="66abb-160">在 SensorTag 模組的組態中找出下列幾行︰</span><span class="sxs-lookup"><span data-stu-id="66abb-160">Locate the following lines in the configuration for the SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="66abb-161">將 **device\_mac\_address** 預留位置取代為您先前記下的 SensorTag MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="66abb-161">Replace the **device\_mac\_address** placeholder  with the MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="66abb-162">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="66abb-162">Save your changes.</span></span>

<span data-ttu-id="66abb-163">您現在可以使用下列命令來執行閘道︰</span><span class="sxs-lookup"><span data-stu-id="66abb-163">You can now run the gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="66abb-164">IoT Edge 閘道會在 Intel NUC 上啟動，並將 SensorTag 中的遙測資料傳送到遠端監視解決方案︰</span><span class="sxs-lookup"><span data-stu-id="66abb-164">The IoT Edge gateway starts on the Intel NUC and sends telemetry from the SensorTag to the remote monitoring solution:</span></span>

![IoT Edge 閘道會傳送 SensorTag 中的遙測資料][img-telemetry]

<span data-ttu-id="66abb-166">按下 **CTRL-C** 可隨時結束程式。</span><span class="sxs-lookup"><span data-stu-id="66abb-166">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="66abb-167">檢視遙測資料</span><span class="sxs-lookup"><span data-stu-id="66abb-167">View the telemetry</span></span>

<span data-ttu-id="66abb-168">閘道現在會將 SensorTag 裝置中的遙測資料傳送到遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="66abb-168">The gateway is now sending telemetry from the SensorTag device to the remote monitoring solution.</span></span> <span data-ttu-id="66abb-169">您可以在解決方案儀表板上檢視遙測資料。</span><span class="sxs-lookup"><span data-stu-id="66abb-169">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="66abb-170">您也可以從解決方案儀表板，透過閘道將命令傳送到 SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="66abb-170">You can also send commands to your SensorTag device through the gateway from the solution dashboard.</span></span>

- <span data-ttu-id="66abb-171">瀏覽至解決方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="66abb-171">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="66abb-172">在 [要檢視的裝置] 下拉式清單中，選取您在閘道中所設定來代表 SensorTag 的裝置。</span><span class="sxs-lookup"><span data-stu-id="66abb-172">Select the device you configured in the gateway that represents the SensorTag in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="66abb-173">來自 SensorTag 裝置的遙測資料會顯示在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="66abb-173">The telemetry from the SensorTag device displays on the dashboard.</span></span>

![顯示 SensorTag 裝置中的遙測資料][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="66abb-175">如果讓遠端監視解決方案繼續在您的 Azure 帳戶中執行，您需支付其執行期間的費用。</span><span class="sxs-lookup"><span data-stu-id="66abb-175">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="66abb-176">如需將遠端監視解決方案執行時的耗用量降低的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案以供示範][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="66abb-176">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="66abb-177">使用完畢時，從您的 Azure 帳戶將預先設定的解決方案刪除。</span><span class="sxs-lookup"><span data-stu-id="66abb-177">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="66abb-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66abb-178">Next steps</span></span>

<span data-ttu-id="66abb-179">請瀏覽 [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)，取得更多 Azure IoT 的相關範例和文件。</span><span class="sxs-lookup"><span data-stu-id="66abb-179">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started