---
title: "aaaIoT DevKit toocloud 連接 IoT DevKit AZ3166 tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 toosetup 並在本教學課程中連接它 IoT DevKit AZ3166 tooAzure IoT 中樞 toosend 資料 toohello Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="84dba-103">連接 IoT DevKit AZ3166 tooAzure hello 雲端中的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="84dba-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="84dba-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/)可以是使用的 toodevelop 和原型的物聯網 (IoT) 解決方案，並運用 Microsoft Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="84dba-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="84dba-105">其包含具有豐富週邊設備與感應器的 Arduino 相容面板、開放原始碼面板封裝，以及不斷擴展的[專案目錄](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/)。</span><span class="sxs-lookup"><span data-stu-id="84dba-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="84dba-106">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="84dba-106">What you do</span></span>
<span data-ttu-id="84dba-107">連接[DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT 中樞您建立時，收集 hello 氣溫和溼度資料從感應器和傳送嗨資料 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="84dba-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="84dba-108">還沒有 DevKit 嗎？</span><span class="sxs-lookup"><span data-stu-id="84dba-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="84dba-109">在[這裡](https://aka.ms/iot-devkit-purchase)取得新的 DevKit。</span><span class="sxs-lookup"><span data-stu-id="84dba-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="84dba-110">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="84dba-110">What you learn</span></span>

* <span data-ttu-id="84dba-111">如何 tooconnect IoT DevKit tooWireless 存取點，並準備您的開發環境。</span><span class="sxs-lookup"><span data-stu-id="84dba-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="84dba-112">如何 toocreate IoT 中樞和 MXChip IoT DevKit 如註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="84dba-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="84dba-113">如何執行範例應用程式上 MXChip IoT DevKit toocollect 感應器資料。</span><span class="sxs-lookup"><span data-stu-id="84dba-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="84dba-114">如何 toosend hello 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="84dba-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="84dba-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="84dba-115">What you need</span></span>

* <span data-ttu-id="84dba-116">使用 Micro USB 纜線的 MXChip IoT DevKit 面板。</span><span class="sxs-lookup"><span data-stu-id="84dba-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="84dba-117">立即取得</span><span class="sxs-lookup"><span data-stu-id="84dba-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="84dba-118">執行 Windows 10 或 macOS 10.10+ 的電腦</span><span class="sxs-lookup"><span data-stu-id="84dba-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="84dba-119">作用中的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84dba-119">An active Azure subscription</span></span>
  * <span data-ttu-id="84dba-120">啟動 [30 天免費試用 Microsoft Azure 帳戶](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="84dba-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="84dba-121">準備硬體</span><span class="sxs-lookup"><span data-stu-id="84dba-121">Prepare your hardware</span></span>

<span data-ttu-id="84dba-122">連結 hello 硬體 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="84dba-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="84dba-123">您需要的硬體</span><span class="sxs-lookup"><span data-stu-id="84dba-123">Hardware you need</span></span>

* <span data-ttu-id="84dba-124">DevKit 面板</span><span class="sxs-lookup"><span data-stu-id="84dba-124">DevKit board</span></span>
* <span data-ttu-id="84dba-125">Micro USB 纜線</span><span class="sxs-lookup"><span data-stu-id="84dba-125">Micro USB cable</span></span>

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="84dba-127">DevKit tooyour 電腦連線</span><span class="sxs-lookup"><span data-stu-id="84dba-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="84dba-128">連接 USB 結束 tooyour PC</span><span class="sxs-lookup"><span data-stu-id="84dba-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="84dba-129">連接微 USB 結束 toohello DevKit</span><span class="sxs-lookup"><span data-stu-id="84dba-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="84dba-130">hello 綠色 LED 下一步 toopower 確認連接</span><span class="sxs-lookup"><span data-stu-id="84dba-130">hello green LED next toopower confirms connection</span></span>

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="84dba-132">設定 WiFi</span><span class="sxs-lookup"><span data-stu-id="84dba-132">Configure WiFi</span></span>

<span data-ttu-id="84dba-133">IoT 專案依賴網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="84dba-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="84dba-134">使用下列指示 tooconfigure hello DevKit tooconnect tooWiFi hello。</span><span class="sxs-lookup"><span data-stu-id="84dba-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="84dba-135">進入 AP 模式</span><span class="sxs-lookup"><span data-stu-id="84dba-135">Enter AP Mode</span></span>

<span data-ttu-id="84dba-136">按住按鈕 B，然後推送釋放 hello 重設 按鈕，然後按一下 發行 按鈕 b。您 DevKit 會進入 AP 模式 WiFi 的設定。</span><span class="sxs-lookup"><span data-stu-id="84dba-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="84dba-137">囉 」 畫面會顯示服務的 hello DevKit 設定 Identifier(SSID) hello 與 hello 設定入口網站的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="84dba-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="84dba-139">連接 tooDevKit AP</span><span class="sxs-lookup"><span data-stu-id="84dba-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="84dba-140">現在，使用另一個 WiFi 啟用裝置 （PC 或行動電話） tooconnect toohello DevKit SSID （hello 上方螢幕擷取畫面中反白顯示），將 hello 密碼保持空白。</span><span class="sxs-lookup"><span data-stu-id="84dba-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="84dba-142">為 DevKit 設定 WiFi</span><span class="sxs-lookup"><span data-stu-id="84dba-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="84dba-143">選取您想，hello DevKit tooconnect hello WiFi 網路開啟 hello PC 或行動電話瀏覽器中的 hello DevKit 螢幕上顯示的 IP 位址，然後輸入 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="84dba-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="84dba-144">按一下**連接**toocomplete:</span><span class="sxs-lookup"><span data-stu-id="84dba-144">Click **Connect** toocomplete:</span></span>

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="84dba-146">Hello 連接成功後，hello DevKit 會在幾秒鐘的時間重新開機。</span><span class="sxs-lookup"><span data-stu-id="84dba-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="84dba-147">如果成功，您會看到囉 」 畫面上的 hello WiFi 名稱和 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="84dba-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="84dba-149">顯示 hello 相片中的 hello IP 位址可能不符合實際 hello IP 指派和 hello DevKit 螢幕上顯示。</span><span class="sxs-lookup"><span data-stu-id="84dba-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="84dba-150">這是正常現象 WiFi 使用 DHCP toodynamically 指派 Ip。</span><span class="sxs-lookup"><span data-stu-id="84dba-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="84dba-151">WiFi 設定之後，您的認證會保留該連接的 hello 裝置上，即使已拔除。</span><span class="sxs-lookup"><span data-stu-id="84dba-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="84dba-152">例如，如果您在家中設定 WiFi hello DevKit，然後 hello DevKit toohello office，您必須 tooreconfigure AP 模式 (開始步驟**輸入 AP 模式**) tooconnect hello DevKit tooyour office WiFi。</span><span class="sxs-lookup"><span data-stu-id="84dba-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="84dba-153">開始使用 DevKit</span><span class="sxs-lookup"><span data-stu-id="84dba-153">Start using DevKit</span></span>

<span data-ttu-id="84dba-154">hello DevKit 上執行的預設應用程式會檢查 hello 韌體 hello 最新版本，並顯示您的某些感應器診斷資料。</span><span class="sxs-lookup"><span data-stu-id="84dba-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="84dba-155">升級 toohello 最新的韌體</span><span class="sxs-lookup"><span data-stu-id="84dba-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="84dba-156">系統將提示同時 hello 目前和最新的韌體版本，如果沒有升級所需的 hello 螢幕上。</span><span class="sxs-lookup"><span data-stu-id="84dba-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="84dba-157">請遵循[升級韌體](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/)引導 tooupgrade 它。</span><span class="sxs-lookup"><span data-stu-id="84dba-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="84dba-159">這是一次性的一旦您啟動 hello DevKit 上進行開發上, 傳您的應用程式，您將有 hello 最新的韌體，隨附於您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="84dba-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="84dba-160">測試各種感應器</span><span class="sxs-lookup"><span data-stu-id="84dba-160">Test various sensors</span></span>

<span data-ttu-id="84dba-161">按下按鈕 B tootest 感應器、 繼續按下並釋放 hello B 按鈕 toocycle 透過每個感應器。</span><span class="sxs-lookup"><span data-stu-id="84dba-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="84dba-163">準備開發環境</span><span class="sxs-lookup"><span data-stu-id="84dba-163">Prepare development environment</span></span>

<span data-ttu-id="84dba-164">現在時間 tooset hello 開發環境： 工具和您 toobuild 令人驚豔的 IoT 應用程式的封裝。</span><span class="sxs-lookup"><span data-stu-id="84dba-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="84dba-165">您可以選擇 Windows 或 macOS 根據 tooyour 作業系統的版本。</span><span class="sxs-lookup"><span data-stu-id="84dba-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="84dba-166">Windows</span><span class="sxs-lookup"><span data-stu-id="84dba-166">Windows</span></span>

<span data-ttu-id="84dba-167">我們鼓勵您 toouse hello 安裝封裝 tooprepare hello 開發環境。</span><span class="sxs-lookup"><span data-stu-id="84dba-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="84dba-168">如果您遇到任何問題，您可以依照 hello[手動步驟](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/)tooget 完成工作。</span><span class="sxs-lookup"><span data-stu-id="84dba-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="84dba-169">下載最新的封裝</span><span class="sxs-lookup"><span data-stu-id="84dba-169">Download latest package</span></span>

<span data-ttu-id="84dba-170">hello`.zip`您下載的檔案包含所有必要工具和所需的 DevKit 開發的封裝。</span><span class="sxs-lookup"><span data-stu-id="84dba-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="84dba-171">下載</span><span class="sxs-lookup"><span data-stu-id="84dba-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="84dba-172">hello`.zip`檔案包含 hello 下列工具和封裝。</span><span class="sxs-lookup"><span data-stu-id="84dba-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="84dba-173">如果您已經有安裝某些元件時，會偵測到 hello 指令碼，並略過它們。</span><span class="sxs-lookup"><span data-stu-id="84dba-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="84dba-174">Node.js 和 Yarn: hello 安裝指令碼和自動化的工作的執行階段</span><span class="sxs-lookup"><span data-stu-id="84dba-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="84dba-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -跨平台命令列管理 Azure 資源，hello MSI 經驗包含相依的 Python 和 pip。</span><span class="sxs-lookup"><span data-stu-id="84dba-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="84dba-176">[Visual Studio Code](https://code.visualstudio.com/)：DevKit 開發的輕量型程式碼編輯器</span><span class="sxs-lookup"><span data-stu-id="84dba-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="84dba-177">[適用於 Arduino 的 Visual Studio Code 擴充功能](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino)：使用 VS Code 啟用 Arduino 開發</span><span class="sxs-lookup"><span data-stu-id="84dba-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="84dba-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello 副檔名 Arduino 依賴這項工具</span><span class="sxs-lookup"><span data-stu-id="84dba-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="84dba-179">DevKit 面板封裝： 工具鏈結、 程式庫和 hello DevKit 的專案</span><span class="sxs-lookup"><span data-stu-id="84dba-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="84dba-180">ST-Link 公用程式：基本公用程式與驅動程式</span><span class="sxs-lookup"><span data-stu-id="84dba-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="84dba-181">執行安裝指令碼</span><span class="sxs-lookup"><span data-stu-id="84dba-181">Run installation script</span></span>

<span data-ttu-id="84dba-182">在 Windows 檔案總管 中，找出 hello`.zip`並將它解壓縮，尋找`install.cmd`，以滑鼠右鍵按一下並選取**以系統管理員身分執行** toostart。</span><span class="sxs-lookup"><span data-stu-id="84dba-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="84dba-184">在安裝期間，您會看到每個工具或封裝的 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="84dba-184">During installation, you will see hello progress of each tool or package.</span></span>

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="84dba-186">確認 tooinstall 驅動程式</span><span class="sxs-lookup"><span data-stu-id="84dba-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="84dba-187">hello VS Code Arduino 擴充功能會依賴 hello Arduino IDE。</span><span class="sxs-lookup"><span data-stu-id="84dba-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="84dba-188">如果這是 hello 第一次安裝 hello Arduino IDE 時，您將會提示的 tooinstall 相關驅動程式：</span><span class="sxs-lookup"><span data-stu-id="84dba-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="84dba-190">會花費大約 10 分鐘 toofinish 安裝，視您的網際網路速度而定。</span><span class="sxs-lookup"><span data-stu-id="84dba-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="84dba-191">Hello 安裝完成之後，您應該在桌面上會看到 Visual Studio 程式碼和 Arduino IDE 快速鍵。</span><span class="sxs-lookup"><span data-stu-id="84dba-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="84dba-192">有時在您啟動 VS Code 時，系統會出現錯誤提示，指出找不到 Arduino IDE 或相關面板封裝。</span><span class="sxs-lookup"><span data-stu-id="84dba-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="84dba-193">關閉與程式碼，它一次啟動 IDE Arduino toosolve 和 VS 程式碼應該尋找 Arduino IDE 路徑正確。</span><span class="sxs-lookup"><span data-stu-id="84dba-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="84dba-194">macOS (預覽)</span><span class="sxs-lookup"><span data-stu-id="84dba-194">macOS (Preview)</span></span>

<span data-ttu-id="84dba-195">您可以依照這些步驟 tooprepare 開發環境上 macOS。</span><span class="sxs-lookup"><span data-stu-id="84dba-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="84dba-196">安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="84dba-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="84dba-197">請遵循 hello[官方指南](https://docs.microsoft.com//cli/azure/install-azure-cli)tooinstall Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="84dba-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="84dba-198">使用 `curl` 命令安裝 Azure CLI 2.0：</span><span class="sxs-lookup"><span data-stu-id="84dba-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="84dba-199">然後重新啟動您的命令殼層，變更 tootake 效果：</span><span class="sxs-lookup"><span data-stu-id="84dba-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="84dba-200">安裝 Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="84dba-200">Install Arduino IDE</span></span>

<span data-ttu-id="84dba-201">Visual Studio 程式碼 Arduino 延伸 hello 依賴 hello Arduino IDE。</span><span class="sxs-lookup"><span data-stu-id="84dba-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="84dba-202">下載並安裝 hello [macOS Arduino IDE](https://www.arduino.cc/en/Main/Software)。</span><span class="sxs-lookup"><span data-stu-id="84dba-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="84dba-203">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="84dba-203">Install Visual Studio Code</span></span>

<span data-ttu-id="84dba-204">下載並安裝[適用於 macOS 的 Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="84dba-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="84dba-205">這會是 hello 建置 DevKit IoT 應用程式的主要開發工具。</span><span class="sxs-lookup"><span data-stu-id="84dba-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="84dba-206">下載最新的封裝</span><span class="sxs-lookup"><span data-stu-id="84dba-206">Download latest package</span></span>

1. <span data-ttu-id="84dba-207">安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="84dba-207">Install Node.js.</span></span> <span data-ttu-id="84dba-208">您可以使用熱門 macOS 封裝管理員[Homebrew](https://brew.sh/)或[預先建立的安裝程式](https://nodejs.org/en/download/)tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="84dba-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="84dba-209">下載 `.zip` 檔案，其包含使用 VS Code 開發 DevKit 所需之工作指令碼。</span><span class="sxs-lookup"><span data-stu-id="84dba-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="84dba-210">下載</span><span class="sxs-lookup"><span data-stu-id="84dba-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="84dba-211">找出 hello`.zip`並將它解壓縮。</span><span class="sxs-lookup"><span data-stu-id="84dba-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="84dba-212">然後啟動**終端機**應用程式，並執行下列命令 tooconfigure 的 hello:</span><span class="sxs-lookup"><span data-stu-id="84dba-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="84dba-213">移動已解壓縮的資料夾 tooyour macOS 使用者資料夾：</span><span class="sxs-lookup"><span data-stu-id="84dba-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="84dba-214">安裝 `npm` 封裝：</span><span class="sxs-lookup"><span data-stu-id="84dba-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="84dba-215">安裝適用於 Arduino 的 Visual Studio Code 擴充功能</span><span class="sxs-lookup"><span data-stu-id="84dba-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="84dba-216">Visual Studio 程式碼可讓您 tooinstall Marketplace 擴充功能直接在 hello 工具中，只要按一下 hello hello 功能表左的窗格中的擴充功能圖示，然後搜尋`Arduino`tooinstall:</span><span class="sxs-lookup"><span data-stu-id="84dba-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="84dba-218">安裝 DevKit 面板封裝</span><span class="sxs-lookup"><span data-stu-id="84dba-218">Install DevKit board package</span></span>

<span data-ttu-id="84dba-219">您必須使用 Visual Studio 程式碼中的 hello 面板管理員 tooadd hello DevKit 面板。</span><span class="sxs-lookup"><span data-stu-id="84dba-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="84dba-220">使用`Cmd+Shift+P`tooinvoke 命令調色盤，然後輸入**Arduino**然後尋找並選取**Arduino： 面板管理員**。</span><span class="sxs-lookup"><span data-stu-id="84dba-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="84dba-221">按一下**'其他 Url'**在 hello 右下方。</span><span class="sxs-lookup"><span data-stu-id="84dba-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="84dba-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="84dba-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="84dba-223">在 hello`settings.json`檔案中，於 hello 下方加入線條`USER SETTINGS`窗格並儲存。</span><span class="sxs-lookup"><span data-stu-id="84dba-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="84dba-225">現在 hello 面板管理員中搜尋 'az3166'，安裝 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="84dba-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="84dba-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="84dba-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="84dba-227">現在您有所有必要工具的 hello macOS 為安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="84dba-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="84dba-228">開啟專案資料夾</span><span class="sxs-lookup"><span data-stu-id="84dba-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="84dba-229">啟動 VS Code</span><span class="sxs-lookup"><span data-stu-id="84dba-229">Launch VS Code</span></span>

<span data-ttu-id="84dba-230">請確定 DevKit 未連線。</span><span class="sxs-lookup"><span data-stu-id="84dba-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="84dba-231">第一次啟動 VS Code 和 hello DevKit tooyour 電腦連線。</span><span class="sxs-lookup"><span data-stu-id="84dba-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="84dba-232">VS Code 會自動尋找它，並快顯簡介頁面：</span><span class="sxs-lookup"><span data-stu-id="84dba-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="84dba-234">有時候在您啟動 VS Code 時，系統會出現錯誤提示，指明找不到 Arduino IDE 或相關面板封裝。</span><span class="sxs-lookup"><span data-stu-id="84dba-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="84dba-235">關閉 VS 程式碼，它一次重新啟動 Arduino IDE toosolve 和 VS 程式碼應該尋找 Arduino IDE 路徑正確。</span><span class="sxs-lookup"><span data-stu-id="84dba-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="84dba-236">開啟 Arduino 範例資料夾</span><span class="sxs-lookup"><span data-stu-id="84dba-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="84dba-237">切換太**'Arduino 範例'**索引標籤上，瀏覽過`Examples for MXCHIP AZ3166 > AzureIoT`，然後按一下  `GetStarted`。</span><span class="sxs-lookup"><span data-stu-id="84dba-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="84dba-239">如果您遇到 tooclose hello 窗格中，tooreload 它使用`Ctrl+Shift+P`(macOS: `Cmd+Shift+P`) tooinvoke 命令調色盤，然後輸入**Arduino** toofind 選取**Arduino： 範例**。</span><span class="sxs-lookup"><span data-stu-id="84dba-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="84dba-240">佈建 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="84dba-240">Provision Azure services</span></span>

<span data-ttu-id="84dba-241">在 hello 方案視窗中，執行您的工作`Ctrl+P`(macOS: `Cmd+P`) 輸入 'task 雲端佈建':</span><span class="sxs-lookup"><span data-stu-id="84dba-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="84dba-242">在 hello VS Code 終端機，互動式的命令列將引導您完成佈建 hello 所需的 Azure 服務：</span><span class="sxs-lookup"><span data-stu-id="84dba-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="84dba-244">組建並上傳 Arduino 草圖</span><span class="sxs-lookup"><span data-stu-id="84dba-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="84dba-245">安裝必要的程式庫</span><span class="sxs-lookup"><span data-stu-id="84dba-245">Install required library</span></span>

1. <span data-ttu-id="84dba-246">按`F1`或`Ctrl+Shift+P`(macOS: `Cmd+Shift+P`) tooinvoke 命令調色盤，然後輸入**Arduino**然後尋找並選取**Arduino： 程式庫管理員**。</span><span class="sxs-lookup"><span data-stu-id="84dba-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="84dba-247">搜尋 `ArduinoJson` 程式庫，然後按一下 [安裝]</span><span class="sxs-lookup"><span data-stu-id="84dba-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="84dba-248">建置並上傳 hello 裝置程式碼</span><span class="sxs-lookup"><span data-stu-id="84dba-248">Build and upload hello device code</span></span>

<span data-ttu-id="84dba-249">使用`Ctrl+P`(macOS: `Cmd+P`) toorun ' 工作的裝置上傳 '。</span><span class="sxs-lookup"><span data-stu-id="84dba-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="84dba-250">終端機 hello 會提示您 tooenter 組態模式。</span><span class="sxs-lookup"><span data-stu-id="84dba-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="84dba-251">toodo，按住按鈕，然後推播和發行 hello 重設 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84dba-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="84dba-252">囉 」 畫面會顯示 「 設定 」。</span><span class="sxs-lookup"><span data-stu-id="84dba-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="84dba-253">這是擷取自 '任務雲端佈建' 步驟 tooset hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="84dba-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="84dba-254">然後就會開始驗證和上傳 hello Arduino 草圖：</span><span class="sxs-lookup"><span data-stu-id="84dba-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="84dba-256">hello DevKit 會重新啟動並開始執行 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="84dba-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="84dba-257">測試 hello 專案</span><span class="sxs-lookup"><span data-stu-id="84dba-257">Test hello project</span></span>

<span data-ttu-id="84dba-258">在 VS 程式碼中，按一下 hello 電源插頭圖示 hello 狀態列 tooopen hello 序列的監視器上。</span><span class="sxs-lookup"><span data-stu-id="84dba-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="84dba-259">hello 範例應用程式時您會看到下列結果 hello 順利執行：</span><span class="sxs-lookup"><span data-stu-id="84dba-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="84dba-260">hello 序列的監視器顯示 hello 以下 hello 螢幕擷取畫面中的 hello 內容相同的資訊。</span><span class="sxs-lookup"><span data-stu-id="84dba-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="84dba-261">hello MXChip IoT DevKit 上的 LED 閃爍不停。</span><span class="sxs-lookup"><span data-stu-id="84dba-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![VS Code 的最終輸出](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="84dba-263">問題與意見反應</span><span class="sxs-lookup"><span data-stu-id="84dba-263">Problems and feedback</span></span>

<span data-ttu-id="84dba-264">您可以找到[常見問題集](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/)如果遇到問題，或是聯繫 toous hello 通道下方。</span><span class="sxs-lookup"><span data-stu-id="84dba-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84dba-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="84dba-265">Next steps</span></span>

<span data-ttu-id="84dba-266">已成功連接 MXChip IoT DevKit tooyour IoT 中樞，並傳送的嗨擷取感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="84dba-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="84dba-267">使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="84dba-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="84dba-268">透過 iothub-explorer 管理雲端裝置傳訊</span><span class="sxs-lookup"><span data-stu-id="84dba-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="84dba-269">儲存 IoT 中樞訊息 tooAzure 資料存放區</span><span class="sxs-lookup"><span data-stu-id="84dba-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="84dba-270">使用 Power BI toovisualize 即時感應器資料從 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="84dba-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="84dba-271">使用 Azure Web Apps toovisualize 即時感應器資料從 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="84dba-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="84dba-272">Azure Machine Learning 中使用 IoT 中樞的 hello 感應器資料的氣象預報預測</span><span class="sxs-lookup"><span data-stu-id="84dba-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="84dba-273">透過 iothub-explorer進行裝置管理</span><span class="sxs-lookup"><span data-stu-id="84dba-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="84dba-274">搭配 Logic Apps 進行遠端監視和通知</span><span class="sxs-lookup"><span data-stu-id="84dba-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)