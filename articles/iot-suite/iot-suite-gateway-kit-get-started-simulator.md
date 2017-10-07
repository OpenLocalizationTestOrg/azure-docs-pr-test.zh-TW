---
title: "aaaConnect 閘道 tooAzure IoT 套件使用 Intel NUC |Microsoft 文件"
description: "使用 hello Microsoft IoT 商業閘道套件和 hello 遠端監視預先設定的解決方案。 使用 hello Azure IoT 邊緣閘道 tooconnect toohello 遠端監視解決方案，傳送模擬的遙測 toohello 雲端，並回應 toomethods 叫用從 hello 方案儀表板。"
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
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="1b9ae-104">連接您 Azure IoT 邊緣閘道 toohello 遠端監視預先設定的解決方案並傳送模擬的遙測</span><span class="sxs-lookup"><span data-stu-id="1b9ae-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="1b9ae-105">本教學課程會示範如何在 toouse Azure IoT 邊緣 toosimulate 溫度和溼度資料 toosend toohello 遠端監視預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="1b9ae-106">hello 教學課程使用：</span><span class="sxs-lookup"><span data-stu-id="1b9ae-106">hello tutorial uses:</span></span>

- <span data-ttu-id="1b9ae-107">Azure IoT 邊緣 tooimplement 閘道範例。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="1b9ae-108">hello IoT 套件遠端監視預先設定的解決方案做為 hello 以雲端為基礎的後端。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="1b9ae-109">概觀</span><span class="sxs-lookup"><span data-stu-id="1b9ae-109">Overview</span></span>

<span data-ttu-id="1b9ae-110">在本教學課程中，您完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b9ae-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="1b9ae-111">部署 hello 遠端監視預先設定的解決方案 tooyour Azure 訂用帳戶的執行個體。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="1b9ae-112">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="1b9ae-113">設定電腦與 hello 遠端監視解決方案程式 Intel NUC 閘道裝置 toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="1b9ae-114">設定的 hello IoT 邊緣閘道 toosend 模擬 hello 方案儀表板，您可以檢視的遙測。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="1b9ae-115">hello 遠端監視解決方案會佈建一組您 Azure 訂用帳戶中的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="1b9ae-116">hello 部署會反映實際的企業架構。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="1b9ae-117">當您完成與其 tooavoid 不必要的 Azure 使用費用，會刪除 hello 預先設定的解決方案，在 azureiotsuite.com 您執行個體。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="1b9ae-118">如果您需要再次 hello 預先設定的方案，您可以輕鬆地重新建立。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="1b9ae-119">減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="1b9ae-120">第二台裝置，例如使用裝置識別碼重複上一個步驟 tooadd hello **device02**。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="1b9ae-121">hello 範例會將資料從兩個模擬裝置傳送 hello 閘道 toohello 遠端監視解決方案中。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="1b9ae-122">建置自訂 IoT 邊緣模組 hello</span><span class="sxs-lookup"><span data-stu-id="1b9ae-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="1b9ae-123">您現在可以建置 hello 自訂 IoT 邊緣模組，可讓 hello 閘道 toosend 訊息 toohello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="1b9ae-124">如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="1b9ae-125">從使用下列命令的 hello GitHub 下載 hello 自訂 IoT 邊緣模組 hello 原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="1b9ae-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="1b9ae-126">建置 hello 使用下列命令的 hello 自訂 IoT 邊緣模組：</span><span class="sxs-lookup"><span data-stu-id="1b9ae-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="1b9ae-127">hello 組建指令碼會置於 hello 組建資料夾中的 hello libsimulator.so 自訂 IoT 邊緣模組。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="1b9ae-128">設定及執行 hello IoT 邊緣閘道</span><span class="sxs-lookup"><span data-stu-id="1b9ae-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="1b9ae-129">您現在可以設定 hello IoT 邊緣閘道 toosend 模擬的遙測 tooyour 遠端監視儀表板。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="1b9ae-130">如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="1b9ae-131">在此教學課程中，您可以使用 hello 標準`vi`hello Intel NUC 上的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="1b9ae-132">如果您不使用`vi`之前，您應該先完成簡介教學課程中，例如[Unix hello vi 編輯器教學課程][ lnk-vi-tutorial] toofamiliarize 自己與這個編輯器。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="1b9ae-133">或者，您可以安裝 hello 更加易懂易記[nano](https://www.nano-editor.org/)編輯器使用 hello 命令`smart install nano -y`。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="1b9ae-134">開啟 hello 範例組態檔中 hello **vi**編輯器使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b9ae-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="1b9ae-135">找出下列行 hello hello iot 中樞模組的組態中的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b9ae-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="1b9ae-136">取代值以 hello IoT 中樞資訊您建立並儲存在 hello 開始本教學課程的 hello 預留位置。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="1b9ae-137">IoTHubName hello 值看起來像**yourrmsolution37e08**，IoTSuffix hello 值通常是**azure devices.net**。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="1b9ae-138">找出下列行 hello hello 對應模組的組態中的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b9ae-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="1b9ae-139">取代 hello **deviceID**和**deviceKey**預留位置取代 hello 識別碼與您先前建立 hello 遠端監視解決方案中的 hello 兩個裝置的金鑰。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="1b9ae-140">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-140">Save your changes.</span></span>

<span data-ttu-id="1b9ae-141">您現在可以執行的 hello IoT 邊緣閘道使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="1b9ae-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="1b9ae-142">hello 閘道上 hello Intel NUC 開始，並傳送遙測模擬的 toohello 遠端監視解決方案：</span><span class="sxs-lookup"><span data-stu-id="1b9ae-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![IoT Edge 閘道會產生模擬的遙測資料][img-simulated telemetry]

<span data-ttu-id="1b9ae-144">按**CTRL-C** tooexit hello 程式在任何時間。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="1b9ae-145">檢視 hello 遙測</span><span class="sxs-lookup"><span data-stu-id="1b9ae-145">View hello telemetry</span></span>

<span data-ttu-id="1b9ae-146">hello IoT 邊緣閘道現在正在模擬的遙測 toohello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="1b9ae-147">您可以檢視 hello 遙測 hello 方案儀表板上。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="1b9ae-148">瀏覽 toohello 方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="1b9ae-149">選取您設定在 hello hello 閘道中的 hello 兩個裝置的其中一個**裝置 tooView**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="1b9ae-150">從 hello 閘道裝置 hello 遙測會顯示 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![顯示從 hello 模擬的閘道裝置遙測][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="1b9ae-152">如果您離開 hello 遠端監視您的 Azure 帳戶中執行的解決方案，您所要支付 hello 次執行。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="1b9ae-153">減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="1b9ae-154">使用完畢時，請從您的 Azure 帳戶刪除 hello 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b9ae-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b9ae-155">Next steps</span></span>

<span data-ttu-id="1b9ae-156">請瀏覽 hello [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)取得更多範例和 Azure IoT 文件。</span><span class="sxs-lookup"><span data-stu-id="1b9ae-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started