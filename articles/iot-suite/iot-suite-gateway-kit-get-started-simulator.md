---
title: "使用 Intel NUC 將閘道連線到 Azure IoT 套件 | Microsoft Docs"
description: "使用 Microsoft IoT Commercial Gateway Kit 和預先設定的遠端監視解決方案。 使用 Azure IoT Edge 閘道來連線到遠端監視解決方案、將模擬的遙測資料傳送到雲端，並回應解決方案儀表板所叫用的方法。"
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
ms.openlocfilehash: 9ed57d3c23e2adbd42c054f33c8ed46e3d6c9792
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="38971-104">將 Azure IoT Edge 閘道連線到預先設定的遠端監視解決方案，並傳送模擬的遙測資料</span><span class="sxs-lookup"><span data-stu-id="38971-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="38971-105">本教學課程說明如何使用 Azure IoT Edge 來模擬溫度和溼度資料，以傳送至預先設定的遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="38971-105">This tutorial shows you how to use Azure IoT Edge to simulate temperature and humidity data to send to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="38971-106">教學課程會使用：</span><span class="sxs-lookup"><span data-stu-id="38971-106">The tutorial uses:</span></span>

- <span data-ttu-id="38971-107">Azure IoT Edge，以實作範例閘道。</span><span class="sxs-lookup"><span data-stu-id="38971-107">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="38971-108">IoT 套件遠端監視預先設定解決方案作為以雲端為基礎的後端。</span><span class="sxs-lookup"><span data-stu-id="38971-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="38971-109">概觀</span><span class="sxs-lookup"><span data-stu-id="38971-109">Overview</span></span>

<span data-ttu-id="38971-110">在本教學課程中，您會完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="38971-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="38971-111">將遠端監視預先設定解決方案的執行個體部署至您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="38971-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="38971-112">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="38971-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="38971-113">設定 Intel NUC 閘道裝置，以便與您的電腦和遠端監視解決方案進行通訊。</span><span class="sxs-lookup"><span data-stu-id="38971-113">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="38971-114">將 IoT Edge 閘道設定為傳送模擬的遙測資料，供您在解決方案儀表板上檢視。</span><span class="sxs-lookup"><span data-stu-id="38971-114">Configure the IoT Edge gateway to send simulated telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="38971-115">遠端監視解決方案會佈建一組 Azure 訂用帳戶中的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="38971-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="38971-116">部署會反映實際的企業架構。</span><span class="sxs-lookup"><span data-stu-id="38971-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="38971-117">若要避免不必要的 Azure 耗用量費用，當您使用完 azureiotsuite.com 中預先設定解決方案的執行個體時，請將它刪除。</span><span class="sxs-lookup"><span data-stu-id="38971-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="38971-118">如果您還需要預先設定的解決方案，可以輕鬆地將它重新建立。</span><span class="sxs-lookup"><span data-stu-id="38971-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="38971-119">如需將遠端監視解決方案執行時的耗用量降低的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案以供示範][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="38971-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="38971-120">重複上述步驟來新增第二個裝置，並讓此裝置使用 **device02** 之類的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="38971-120">Repeat the previous steps to add a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="38971-121">此範例會將閘道中兩個模擬裝置的資料傳送到遠端監控解決方案。</span><span class="sxs-lookup"><span data-stu-id="38971-121">The sample sends data from two simulated devices in the gateway to the remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="38971-122">建置自訂的 IoT Edge 模組</span><span class="sxs-lookup"><span data-stu-id="38971-122">Build the custom IoT Edge module</span></span>

<span data-ttu-id="38971-123">您現在可以建置自訂的 IoT Edge 模組，以讓閘道傳送訊息給遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="38971-123">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="38971-124">如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。</span><span class="sxs-lookup"><span data-stu-id="38971-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="38971-125">使用下列命令，從 GitHub 下載自訂 IoT Edge 模組的原始程式碼︰</span><span class="sxs-lookup"><span data-stu-id="38971-125">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="38971-126">使用下列命令來建置自訂的 IoT Edge 模組︰</span><span class="sxs-lookup"><span data-stu-id="38971-126">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="38971-127">建置指令碼會將 libsimulator.so 自訂 IoT Edge 模組放置在建置資料夾中。</span><span class="sxs-lookup"><span data-stu-id="38971-127">The build script places the libsimulator.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="38971-128">設定和執行 IoT Edge 閘道</span><span class="sxs-lookup"><span data-stu-id="38971-128">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="38971-129">您現在可以將 IoT Edge 閘道設定為將模擬的遙測資料傳送到遠端監視儀表板。</span><span class="sxs-lookup"><span data-stu-id="38971-129">You can now configure the IoT Edge gateway to send simulated telemetry to your remote monitoring dashboard.</span></span> <span data-ttu-id="38971-130">如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。</span><span class="sxs-lookup"><span data-stu-id="38971-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="38971-131">在本教學課程中，您可以使用 Intel NUC 上的標準 `vi` 文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="38971-131">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="38971-132">如果您之前未使用過 `vi`，請先完成入門教學課程 (例如 [Unix - The vi Editor Tutorial][lnk-vi-tutorial] ) 以熟悉這個編輯器。</span><span class="sxs-lookup"><span data-stu-id="38971-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="38971-133">或者，您可以使用 `smart install nano -y` 命令，來安裝更方便使用的 [nano](https://www.nano-editor.org/) 編輯器。</span><span class="sxs-lookup"><span data-stu-id="38971-133">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="38971-134">使用下列命令，將 **vi** 編輯器中的範例組態檔開啟︰</span><span class="sxs-lookup"><span data-stu-id="38971-134">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="38971-135">在 IoTHub 模組的組態中找出下列幾行︰</span><span class="sxs-lookup"><span data-stu-id="38971-135">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="38971-136">將預留位置值取代為本教學課程開頭所建立及儲存的 IoT 中樞資訊。</span><span class="sxs-lookup"><span data-stu-id="38971-136">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="38971-137">IoTHubName 的值會像 **yourrmsolution37e08**，IoTSuffix 的值則通常是 **azure-devices.net**。</span><span class="sxs-lookup"><span data-stu-id="38971-137">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="38971-138">在對應模組的組態中找出下列幾行︰</span><span class="sxs-lookup"><span data-stu-id="38971-138">Locate the following lines in the configuration for the mapping module:</span></span>

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

<span data-ttu-id="38971-139">將 **deviceID** 和 **deviceKey** 預留位置取代為您先前在遠端監視解決方案中所建立之兩個裝置的識別碼和金鑰。</span><span class="sxs-lookup"><span data-stu-id="38971-139">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="38971-140">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="38971-140">Save your changes.</span></span>

<span data-ttu-id="38971-141">您現在可以使用下列命令來執行 IoT Edge 閘道︰</span><span class="sxs-lookup"><span data-stu-id="38971-141">You can now run the IoT Edge gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="38971-142">此閘道會在 Intel NUC 上啟動，並將模擬的遙測資料傳送到遠端監視解決方案︰</span><span class="sxs-lookup"><span data-stu-id="38971-142">The gateway starts on the Intel NUC and sends simulated telemetry to the remote monitoring solution:</span></span>

![IoT Edge 閘道會產生模擬的遙測資料][img-simulated telemetry]

<span data-ttu-id="38971-144">按下 **CTRL-C** 可隨時結束程式。</span><span class="sxs-lookup"><span data-stu-id="38971-144">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="38971-145">檢視遙測資料</span><span class="sxs-lookup"><span data-stu-id="38971-145">View the telemetry</span></span>

<span data-ttu-id="38971-146">IoT Edge 閘道現在會將磨你的遙測資料傳送至遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="38971-146">The IoT Edge gateway is now sending simulated telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="38971-147">您可以在解決方案儀表板上檢視遙測資料。</span><span class="sxs-lookup"><span data-stu-id="38971-147">You can view the telemetry on the solution dashboard.</span></span>

- <span data-ttu-id="38971-148">瀏覽至解決方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="38971-148">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="38971-149">在 [要檢視的裝置] 下拉式清單中，選取您在閘道中所設定之兩個裝置的其中一個。</span><span class="sxs-lookup"><span data-stu-id="38971-149">Select one of the two devices you configured in the gateway in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="38971-150">來自閘道裝置的遙測資料會顯示在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="38971-150">The telemetry from the gateway devices displays on the dashboard.</span></span>

![顯示模擬閘道裝置中的遙測資料][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="38971-152">如果讓遠端監視解決方案繼續在您的 Azure 帳戶中執行，您需支付其執行期間的費用。</span><span class="sxs-lookup"><span data-stu-id="38971-152">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="38971-153">如需將遠端監視解決方案執行時的耗用量降低的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案以供示範][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="38971-153">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="38971-154">使用完畢時，從您的 Azure 帳戶將預先設定的解決方案刪除。</span><span class="sxs-lookup"><span data-stu-id="38971-154">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38971-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38971-155">Next steps</span></span>

<span data-ttu-id="38971-156">請瀏覽 [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)，取得更多 Azure IoT 的相關範例和文件。</span><span class="sxs-lookup"><span data-stu-id="38971-156">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started