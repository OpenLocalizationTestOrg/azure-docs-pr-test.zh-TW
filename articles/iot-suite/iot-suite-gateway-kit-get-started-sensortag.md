---
title: "aaaConnect 閘道 tooAzure IoT 套件使用 Intel NUC |Microsoft 文件"
description: "使用 hello Microsoft IoT 商業閘道套件和 hello 遠端監視預先設定的解決方案。 使用 hello Azure IoT 邊緣閘道 tooenable SensorTag 裝置 tooconnect toohello 遠端監視解決方案，傳送遙測 toohello 雲端，並回應 toomethods hello 方案儀表板從叫用。"
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
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="7cd3f-104">連接您 Azure IoT 邊緣閘道 toohello 遠端監視預先設定的解決方案，並從 SensorTag 傳送遙測</span><span class="sxs-lookup"><span data-stu-id="7cd3f-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="7cd3f-105">本教學課程會示範如何 toouse Azure IoT 邊緣 toosend 氣溫和溼度與監視的資料 SensorTag 裝置 toohello 遠端預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="7cd3f-106">hello SensorTag 連接使用藍芽 toohello Intel NUC 閘道。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="7cd3f-107">hello 教學課程使用：</span><span class="sxs-lookup"><span data-stu-id="7cd3f-107">hello tutorial uses:</span></span>

- <span data-ttu-id="7cd3f-108">Azure IoT 邊緣 tooimplement 閘道範例。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="7cd3f-109">hello IoT 套件遠端監視預先設定的解決方案做為 hello 以雲端為基礎的後端。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="7cd3f-110">概觀</span><span class="sxs-lookup"><span data-stu-id="7cd3f-110">Overview</span></span>

<span data-ttu-id="7cd3f-111">在本教學課程中，您完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="7cd3f-112">部署 hello 遠端監視預先設定的解決方案 tooyour Azure 訂用帳戶的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="7cd3f-113">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="7cd3f-114">設定電腦與 hello 遠端監視解決方案程式 Intel NUC 閘道裝置 toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="7cd3f-115">您 Intel NUC 閘道 tooreceive 遙測設定從 SensorTag 裝置，並將它送出 toohello 遠端監視儀表板。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="7cd3f-116">[Texas Instruments BLE SensorTag][lnk-sensortag]。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="7cd3f-117">本教學課程中從 hello SensorTag 裝置透過藍牙擷取遙測資料。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="7cd3f-118">hello 遠端監視解決方案會佈建一組您 Azure 訂用帳戶中的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="7cd3f-119">hello 部署會反映實際的企業架構。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="7cd3f-120">當您完成與其 tooavoid 不必要的 Azure 使用費用，會刪除 hello 預先設定的解決方案，在 azureiotsuite.com 您執行個體。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="7cd3f-121">如果您需要再次 hello 預先設定的方案，您可以輕鬆地重新建立。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="7cd3f-122">減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="7cd3f-123">設定藍牙連線</span><span class="sxs-lookup"><span data-stu-id="7cd3f-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="7cd3f-124">設定藍芽 hello Intel NUC tooenable hello SensorTag 裝置 tooconnect 上並傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="7cd3f-125">尋找 hello SensorTag hello MAC 位址</span><span class="sxs-lookup"><span data-stu-id="7cd3f-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="7cd3f-126">在 hello 介面 hello Intel NUC 上執行下列命令 toounblock hello 藍芽服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="7cd3f-127">Hello 執行的下列命令在 hello Intel NUC toostart hello 藍芽服務，然後輸入 hello 藍芽介面：</span><span class="sxs-lookup"><span data-stu-id="7cd3f-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="7cd3f-128">執行下列命令 toopower hello 藍芽控制站上的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="7cd3f-129">Hello 控制站上時，您會看到一則訊息**上變更電源成功**。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="7cd3f-130">執行下列命令 tooscan 如附近的藍芽裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="7cd3f-131">按 hello 電源按鈕，hello SensorTag toomake 可探索它。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="7cd3f-132">hello 綠色 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="7cd3f-133">當您看到訊息，以在 hello 介面中的 hello 控制站已探索 hello SensorTag，記下 hello hello 裝置的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="7cd3f-134">hello MAC 位址看起來像**A0:E6:F8:B5:F6:00**。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="7cd3f-135">當您設定 hello 閘道，您需要在 hello 教學課程後面 hello MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="7cd3f-136">執行下列命令 tooturn 藍芽掃描功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="7cd3f-137">執行下列命令 tooverify，您可以連接 toohello SensorTag 裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="7cd3f-138">如果您已成功連接，hello 殼層顯示 hello 訊息**連線成功**並列印 hello SensorTag 裝置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="7cd3f-139">如果您無法連接，請檢查的 hello SensorTag 仍電源已開啟。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="7cd3f-140">您現在可以中斷 hello SensorTag 並執行下列命令的 hello 結束 hello 藍芽介面：</span><span class="sxs-lookup"><span data-stu-id="7cd3f-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="7cd3f-141">建置自訂 IoT 邊緣模組 hello</span><span class="sxs-lookup"><span data-stu-id="7cd3f-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="7cd3f-142">您現在可以建置 hello 自訂 IoT 邊緣模組，可讓 hello 閘道 toosend 訊息 toohello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="7cd3f-143">如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="7cd3f-144">從使用下列命令的 hello GitHub 下載 hello 自訂 IoT 邊緣模組 hello 原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="7cd3f-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="7cd3f-145">建置 hello 使用下列命令的 hello 自訂 IoT 邊緣模組：</span><span class="sxs-lookup"><span data-stu-id="7cd3f-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="7cd3f-146">hello 組建指令碼會置於 hello 組建資料夾中的 hello libsensor2remotemonitoring.so 自訂 IoT 邊緣模組。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="7cd3f-147">設定及執行 hello IoT 邊緣閘道</span><span class="sxs-lookup"><span data-stu-id="7cd3f-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="7cd3f-148">您現在可以從遠端監視儀表板您 SensorTag 裝置 tooyour 設定 hello IoT 邊緣閘道 toosend 遙測。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="7cd3f-149">如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="7cd3f-150">在此教學課程中，您可以使用 hello 標準`vi`hello Intel NUC 上的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="7cd3f-151">如果您不使用`vi`之前，您應該先完成簡介教學課程中，例如[Unix hello vi 編輯器教學課程][ lnk-vi-tutorial] toofamiliarize 自己與這個編輯器。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="7cd3f-152">或者，您可以安裝 hello 更加易懂易記[nano](https://www.nano-editor.org/)編輯器使用 hello 命令`smart install nano -y`。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="7cd3f-153">開啟 hello 範例組態檔中 hello **vi**編輯器使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="7cd3f-154">找出下列行 hello hello iot 中樞模組的組態中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="7cd3f-155">取代值以 hello IoT 中樞資訊您建立並儲存在 hello 開始本教學課程的 hello 預留位置。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="7cd3f-156">IoTHubName hello 值看起來像**yourrmsolution37e08**，IoTSuffix hello 值通常是**azure devices.net**。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="7cd3f-157">找出下列行 hello hello 對應模組的組態中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="7cd3f-158">取代 hello **macAddress**預留位置 hello 您先前記下您 SensorTag MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="7cd3f-159">取代 hello **deviceID**和**deviceKey**預留位置取代 hello 識別碼與您先前建立 hello 遠端監視解決方案中的 hello 兩個裝置的金鑰。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="7cd3f-160">找出下列行 hello hello SensorTag 模組的組態中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7cd3f-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="7cd3f-161">取代 hello**裝置\_mac\_位址**預留位置 hello 您先前記下您 SensorTag MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="7cd3f-162">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-162">Save your changes.</span></span>

<span data-ttu-id="7cd3f-163">您現在可以執行使用下列命令的 hello hello 閘道：</span><span class="sxs-lookup"><span data-stu-id="7cd3f-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="7cd3f-164">hello IoT 邊緣閘道上 hello Intel NUC 啟動，並將遙測傳送 hello SensorTag toohello 遠端監視解決方案從：</span><span class="sxs-lookup"><span data-stu-id="7cd3f-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![IoT 邊緣閘道會從 hello SensorTag 傳送遙測][img-telemetry]

<span data-ttu-id="7cd3f-166">按**CTRL-C** tooexit hello 程式在任何時間。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="7cd3f-167">檢視 hello 遙測</span><span class="sxs-lookup"><span data-stu-id="7cd3f-167">View hello telemetry</span></span>

<span data-ttu-id="7cd3f-168">hello 閘道現在正在將遙測傳送從 hello SensorTag 裝置 toohello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="7cd3f-169">您可以檢視 hello 遙測 hello 方案儀表板上。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="7cd3f-170">您也可以從 hello 方案儀表板傳送命令 tooyour SensorTag 裝置透過 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="7cd3f-171">瀏覽 toohello 方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="7cd3f-172">選取 hello 裝置中代表 hello SensorTag hello 中的 hello 閘道設定**裝置 tooView**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="7cd3f-173">從 hello SensorTag 裝置 hello 遙測會顯示 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![顯示從 hello SensorTag 裝置遙測][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="7cd3f-175">如果您離開 hello 遠端監視您的 Azure 帳戶中執行的解決方案，您所要支付 hello 次執行。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="7cd3f-176">減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="7cd3f-177">使用完畢時，請從您的 Azure 帳戶刪除 hello 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7cd3f-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7cd3f-178">Next steps</span></span>

<span data-ttu-id="7cd3f-179">請瀏覽 hello [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)取得更多範例和 Azure IoT 文件。</span><span class="sxs-lookup"><span data-stu-id="7cd3f-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started