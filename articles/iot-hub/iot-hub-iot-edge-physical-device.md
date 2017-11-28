---
title: "Azure IoT 邊緣的實體裝置 aaaUse |Microsoft 文件"
description: "如何 toouse 德州儀器 SensorTag 裝置 toosend 資料 tooan IoT 中樞透過 IoT 邊緣閘道覆盆子 Pi 3 在裝置上執行。 使用 Azure IoT 邊緣建置 hello 閘道。"
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="2ce3f-104">使用 Azure IoT 邊緣覆盆子 Pi tooforward 裝置到雲端訊息 tooIoT 中樞</span><span class="sxs-lookup"><span data-stu-id="2ce3f-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="2ce3f-105">這個逐步解說中的 hello[藍芽低能源範例][ lnk-ble-samplecode]為您示範如何 toouse [Azure IoT 邊緣][ lnk-sdk]至：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="2ce3f-106">轉送裝置到雲端遙測 tooIoT 中樞，從實體裝置。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="2ce3f-107">將命令路由傳送從 IoT 中樞 tooa 實體裝置。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="2ce3f-108">本逐步解說涵蓋下列項目：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-108">This walkthrough covers:</span></span>

* <span data-ttu-id="2ce3f-109">**架構**: hello 藍芽低能源範例架構重要資訊。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="2ce3f-110">**建置並執行**: hello 步驟需要的 toobuild 和執行的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="2ce3f-111">架構</span><span class="sxs-lookup"><span data-stu-id="2ce3f-111">Architecture</span></span>

<span data-ttu-id="2ce3f-112">hello 逐步解說將示範如何 toobuild 和覆盆子 Pi 3 上執行的 IoT 邊緣閘道執行 Raspbian Linux。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="2ce3f-113">hello 閘道是建置使用 IoT 邊緣。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="2ce3f-114">hello 範例會使用德州儀器 SensorTag 藍芽低能源 (B) 裝置 toocollect 溫度資料。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="2ce3f-115">當您執行 hello IoT 邊緣閘道它：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="2ce3f-116">會使用 hello 藍芽低能源 (B) 通訊協定 tooa SensorTag 裝置連線。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="2ce3f-117">連接 tooIoT 集線器使用 hello HTTP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="2ce3f-118">將遙測轉送從 hello SensorTag 裝置 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="2ce3f-119">將命令路由傳送從 IoT 中樞 toohello SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="2ce3f-120">hello 閘道包含下列 IoT 邊緣模組 hello:</span><span class="sxs-lookup"><span data-stu-id="2ce3f-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="2ce3f-121">A *b 模組*從 hello 裝置和傳送指令 toohello 裝置 b 裝置 tooreceive 溫度資料的介面。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="2ce3f-122">A *b 雲端 toodevice 模組*轉譯成 hello b 指示從 IoT 中樞傳送 JSON 訊息*b 模組*。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="2ce3f-123">A*記錄器模組*記錄所有閘道訊息 tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="2ce3f-124">「身分識別對應模組」  ，可在 BLE 裝置 MAC 位址與 Azure IoT 中樞裝置身分識別之間進行轉譯。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="2ce3f-125">*IoT 中樞模組*，上傳遙測資料 tooan IoT 中樞，並從 IoT 中樞接收裝置命令。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="2ce3f-126">A *b 印表機模組*，解譯遙測從 hello b 裝置，並列印格式化的資料 toohello 主控台 tooenable 疑難排解和偵錯。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="2ce3f-127">資料如何流經 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="2ce3f-127">How data flows through hello gateway</span></span>

<span data-ttu-id="2ce3f-128">hello 遵循區塊圖將說明 hello 遙測上載資料流程管線：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![遙測上傳閘道管線](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="2ce3f-130">hello 步驟的遙測資料的項目會從 b 裝置 tooIoT 中樞如下：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="2ce3f-131">hello b 裝置會產生溫度範例，並將它傳送 hello 閘道中的藍芽 toohello b 模組。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="2ce3f-132">hello b 模組收到 hello 範例，並將其發佈 toohello broker 以及 hello 裝置 hello MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="2ce3f-133">hello 身分識別對應模組拾取此訊息，並使用到 IoT 中樞裝置身分識別的內部資料表 tootranslate hello hello 裝置的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="2ce3f-134">IoT 中樞裝置身分識別是由裝置識別碼及裝置金鑰所組成。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="2ce3f-135">hello 身分識別對應模組發佈新訊息，其中包含 hello 溫度範例資料，hello 裝置 hello 裝置識別碼及 hello 裝置機碼的 hello MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="2ce3f-136">hello IoT 中樞模組接收這個新的訊息 （hello 身分識別對應模組所產生），並將其發佈 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="2ce3f-137">hello 記錄器模組會記錄所有訊息從 hello broker tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="2ce3f-138">hello 遵循區塊圖將說明 hello 裝置命令資料流程管線：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![裝置命令閘道管線](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="2ce3f-140">hello 模組會定期輪詢的 IoT 中樞 hello IoT 中樞的新命令訊息。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="2ce3f-141">當 hello IoT 中樞模組收到新的命令訊息時，它將其發佈 toohello broker。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="2ce3f-142">hello 身分識別對應模組收到 hello 命令訊息，且使用的內部資料表 tootranslate hello IoT Hub 裝置識別碼 tooa 裝置 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="2ce3f-143">接著將發佈新訊息，其中包含 hello 訊息 hello 屬性對應中的 hello 目標裝置 hello MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="2ce3f-144">hello b 雲端到裝置單元拾取此訊息，並將它轉譯成 hello b 模組 hello 適當 b 指令。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="2ce3f-145">接著將發佈新訊息。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="2ce3f-146">hello b 單元拾取此訊息，並執行 hello I/O 指令與 hello b 裝置通訊。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="2ce3f-147">hello 記錄器模組會記錄所有訊息從 hello broker tooa 磁碟檔案。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ce3f-148">必要條件</span><span class="sxs-lookup"><span data-stu-id="2ce3f-148">Prerequisites</span></span>

<span data-ttu-id="2ce3f-149">toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="2ce3f-150">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2ce3f-151">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="2ce3f-152">需要 SSH 用戶端上您 tooremotely 存取 hello 命令列 hello 覆盆子 Pi 您桌面的電腦 tooenable。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="2ce3f-153">Windows 不包含 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="2ce3f-154">我們建議使用 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="2ce3f-155">多數 Linux 散發套件和 Mac OS 包含 hello 命令列 SSH 公用程式。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="2ce3f-156">如需詳細資訊，請參閱[使用 Linux 或 Mac OS 的 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="2ce3f-157">準備硬體</span><span class="sxs-lookup"><span data-stu-id="2ce3f-157">Prepare your hardware</span></span>

<span data-ttu-id="2ce3f-158">本教學課程假設您正在使用[德州儀器 SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html)裝置連線 tooa 覆盆子 Pi 3 執行 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="2ce3f-159">安裝 Raspbian</span><span class="sxs-lookup"><span data-stu-id="2ce3f-159">Install Raspbian</span></span>

<span data-ttu-id="2ce3f-160">您可以使用其中一個 hello 遵循選項 tooinstall Raspbian 覆盆子 Pi 3 裝置。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="2ce3f-161">tooinstall hello 最新版本的 Raspbian，使用 hello [NOOBS] [ lnk-noobs]圖形化使用者介面。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="2ce3f-162">手動[下載][ lnk-raspbian]和寫入 hello hello Raspbian 作業系統 tooan SD 卡的最新映像。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="2ce3f-163">登入及存取 hello 終端機</span><span class="sxs-lookup"><span data-stu-id="2ce3f-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="2ce3f-164">您有兩個選項 tooaccess 終端機環境覆盆子 Pi 上：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="2ce3f-165">如果您有鍵盤，監視連線的 tooyour 覆盆子 Pi，您可以使用 hello Raspbian GUI tooaccess 終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="2ce3f-166">從您桌面的電腦使用 SSH 您覆盆子 pi hello 命令列存取。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="2ce3f-167">在 hello GUI 中的終端機視窗</span><span class="sxs-lookup"><span data-stu-id="2ce3f-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="2ce3f-168">Raspbian hello 預設認證是使用者名稱**pi**和密碼**覆盆子**。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="2ce3f-169">您可以在 hello 工作列 hello GUI 中，啟動 hello**終端機**使用 hello 圖示看起來像監視器公用程式。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="2ce3f-170">使用 SSH 登入</span><span class="sxs-lookup"><span data-stu-id="2ce3f-170">Sign in with SSH</span></span>

<span data-ttu-id="2ce3f-171">您可以使用 SSH 的命令列存取 tooyour 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="2ce3f-172">hello 文章[SSH (Secure Shell)] [ lnk-pi-ssh]描述如何 tooconfigure SSH 您覆盆子 pi，以及如何從 tooconnect [Windows] [ lnk-ssh-windows]或[Linux 和 Mac OS][lnk-ssh-linux]。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="2ce3f-173">以使用者名稱 **pi** 和密碼 **raspberry** 登入。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="2ce3f-174">安裝 BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="2ce3f-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="2ce3f-175">hello b 模組討論 toohello 藍芽硬體透過 hello BlueZ 堆疊。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="2ce3f-176">正確的 hello 模組 toowork 需要 BlueZ 5.37 版本。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="2ce3f-177">這些指示請確定已安裝的 BlueZ hello 正確版本。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="2ce3f-178">停止目前藍芽精靈 hello:</span><span class="sxs-lookup"><span data-stu-id="2ce3f-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="2ce3f-179">安裝 hello BlueZ 相依項目：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="2ce3f-180">從 bluez.org 下載 hello BlueZ 原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="2ce3f-181">解壓縮 hello 原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="2ce3f-182">變更目錄 toohello 新建立的資料夾：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="2ce3f-183">設定建置 hello BlueZ 程式碼 toobe:</span><span class="sxs-lookup"><span data-stu-id="2ce3f-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="2ce3f-184">建置 BlueZ：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="2ce3f-185">完成建置後安裝 BlueZ：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="2ce3f-186">變更 systemd 服務組態，讓它所指 toohello 新藍芽精靈 hello 檔案中的藍芽`/lib/systemd/system/bluetooth.service`。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="2ce3f-187">Hello 'ExecStart' 行取代成下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ce3f-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="2ce3f-188">啟用從覆盆子 Pi 3 裝置連線 toohello SensorTag 裝置</span><span class="sxs-lookup"><span data-stu-id="2ce3f-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="2ce3f-189">您必須 tooverify 您覆盆子 Pi 3 可以連接 toohello SensorTag 裝置之前執行的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="2ce3f-190">請確定 hello`rfkill`安裝公用程式：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="2ce3f-191">解除封鎖 hello 覆盆子 Pi 3 上的藍芽並檢查 hello 版本號碼**5.37**:</span><span class="sxs-lookup"><span data-stu-id="2ce3f-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="2ce3f-192">tooenter hello 互動式藍芽殼層，啟動 hello 藍芽服務，然後執行 hello **bluetoothctl**命令：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="2ce3f-193">輸入 hello 命令**開機**toopower hello 藍芽控制器。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="2ce3f-194">hello 命令會傳回類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="2ce3f-195">在 [hello 互動式藍芽 shell] 中，輸入 hello 命令**掃描**tooscan 藍芽裝置。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="2ce3f-196">hello 命令會傳回類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="2ce3f-197">請按下 hello 小按鈕 (綠色 LED 應閃爍的 hello) hello SensorTag 裝置可探索。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="2ce3f-198">hello 覆盆子 Pi 3 應該探索 hello SensorTag 裝置：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="2ce3f-199">在此範例中，您可以看到該 hello hello SensorTag 裝置的 MAC 位址**A0:E6:F8:B5:F6:00**。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="2ce3f-200">關閉掃描輸入 hello**掃描關閉**命令：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="2ce3f-201">使用其 MAC 位址輸入 tooyour SensorTag 裝置連接**連接\<MAC 位址\>**。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="2ce3f-202">下列範例輸出的 hello 是為了清楚起見縮寫：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="2ce3f-203">您可以列出一次使用 hello hello 裝置 hello GATT 特性**屬性清單**命令。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="2ce3f-204">您現在可以中斷 hello 透過從裝置 hello**中斷**命令，並結束作業從 hello 藍芽介面使用 hello**結束**命令：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="2ce3f-205">您現在準備好 toorun hello B IoT 邊緣範例您覆盆子 Pi 3 為基礎。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="2ce3f-206">執行 hello IoT 邊緣 b 範例</span><span class="sxs-lookup"><span data-stu-id="2ce3f-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="2ce3f-207">toorun hello IoT 邊緣 b 範例中，您需要 toocomplete 三項工作：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="2ce3f-208">在您的 IoT 中樞上設定兩個範例裝置。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="2ce3f-209">在 Raspberry Pi 3 裝置上建置 IoT Edge。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="2ce3f-210">設定及執行 hello b 範例覆盆子 Pi 3 裝置。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="2ce3f-211">Hello 撰寫本文時，在 IoT 邊緣只支援 b 模組中的閘道在 Linux 上執行。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="2ce3f-212">在您的 IoT 中樞上設定兩個範例裝置</span><span class="sxs-lookup"><span data-stu-id="2ce3f-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="2ce3f-213">[建立 IoT 中樞][ lnk-create-hub]在您 Azure 訂用帳戶，您需要集線器 toocomplete hello 名稱本逐步解說。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="2ce3f-214">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="2ce3f-215">加入一個稱為**SensorTag_01** tooyour IoT 中樞並記下其識別碼和裝置的金鑰。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="2ce3f-216">您可以使用 hello[裝置檔案總管或 iot 中樞總管][ lnk-explorer-tools]工具 tooadd hello 上一個步驟和 tooretrieve 中建立它的索引鍵此裝置 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="2ce3f-217">當您設定 hello 閘道，您可以對應此裝置 toohello SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="2ce3f-218">在 Raspberry Pi 3 上建置 Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="2ce3f-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="2ce3f-219">安裝 Azure IoT Edge 的相依項目：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="2ce3f-220">使用 hello 下列命令 tooclone IoT 邊緣和所有其所 tooyour 主目錄：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="2ce3f-221">當您覆盆子 Pi 3 hello IoT 邊緣儲存機制的完整複本，您可以建置使用 hello hello 資料夾包含 hello SDK 中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="2ce3f-222">設定及執行您的覆盆子 Pi 3 hello b 範例</span><span class="sxs-lookup"><span data-stu-id="2ce3f-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="2ce3f-223">toobootstrap 以及執行的 hello 範例，您必須設定每個參與的 IoT 邊緣模組 hello 閘道中。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="2ce3f-224">這個組態是以 JSON 檔案來提供，您必須設定所有五個參與的 IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="2ce3f-225">呼叫 hello 儲存機制中沒有範例 JSON 檔案**閘道\_sample.json**您可以使用做為起點來建立您自己的組態檔的 hello。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="2ce3f-226">這個檔案位於 hello **src/ble_gateway範例/** hello IoT 邊緣儲存機制的本機副本中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="2ce3f-227">hello 下列各節說明如何 tooedit 此組態檔取得 hello b 範例，然後假設該 hello IoT 邊緣存放庫處於 hello **/home/pi/iot-edge /**上您覆盆子 Pi 3 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="2ce3f-228">如果 hello 儲存機制是在其他位置，請據以調整 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="2ce3f-229">記錄器組態</span><span class="sxs-lookup"><span data-stu-id="2ce3f-229">Logger configuration</span></span>

<span data-ttu-id="2ce3f-230">假設 hello 閘道儲存機制位於 hello **/home/pi/iot-edge /**資料夾中，設定 hello 記錄器模組，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="2ce3f-231">BLE 模組組態</span><span class="sxs-lookup"><span data-stu-id="2ce3f-231">BLE module configuration</span></span>

<span data-ttu-id="2ce3f-232">hello b 裝置 hello 範例設定假設德州儀器 SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="2ce3f-233">任何標準 b 裝置週邊 GATT 應該會運作，但您可能需要 tooupdate hello GATT 特性 Id 和資料可操作。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="2ce3f-234">加入 SensorTag 裝置 hello MAC 位址：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-234">Add hello MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="2ce3f-235">如果您不使用 SensorTag 裝置，檢閱您 b 裝置 toodetermine hello 文件，您是否需要 tooupdate hello GATT 特性 Id 和資料值。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="2ce3f-236">IoT 中樞模組</span><span class="sxs-lookup"><span data-stu-id="2ce3f-236">IoT Hub module</span></span>

<span data-ttu-id="2ce3f-237">加入 hello 的 IoT 中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="2ce3f-238">hello 尾碼值通常是**azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="2ce3f-238">hello suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="2ce3f-239">身分識別對應模組組態</span><span class="sxs-lookup"><span data-stu-id="2ce3f-239">Identity mapping module configuration</span></span>

<span data-ttu-id="2ce3f-240">新增您 SensorTag 裝置和 hello 裝置識別碼和金鑰的 hello hello MAC 位址**SensorTag_01**加入 tooyour IoT 中樞的裝置：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="2ce3f-241">BLE 印表機模組組態</span><span class="sxs-lookup"><span data-stu-id="2ce3f-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="2ce3f-242">BLEC2D 模組組態</span><span class="sxs-lookup"><span data-stu-id="2ce3f-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="2ce3f-243">路由組態</span><span class="sxs-lookup"><span data-stu-id="2ce3f-243">Routing Configuration</span></span>

<span data-ttu-id="2ce3f-244">hello 下列組態可確保 hello 下列 IoT 邊緣模組之間的路由：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="2ce3f-245">hello**記錄器**模組接收並記錄所有訊息。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="2ce3f-246">hello **SensorTag**模組傳送訊息 tooboth hello**對應**和**b 印表機**模組。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="2ce3f-247">hello**對應**模組傳送訊息 toohello **iot 中樞**模組 toobe 傳送 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="2ce3f-248">hello **iot 中樞**模組傳送的訊息傳回 toohello**對應**模組。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="2ce3f-249">hello**對應**模組傳送訊息 toohello **BLEC2D**模組。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="2ce3f-250">hello **BLEC2D**模組傳送的訊息傳回 toohello**感應器標記**模組。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="2ce3f-251">toorun hello 範例傳遞 hello 路徑 toohello JSON 組態檔做為參數 toohello **b\_閘道**二進位。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="2ce3f-252">hello 下列命令假設您正在使用 hello **gateway_sample.json**組態檔。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="2ce3f-253">執行此命令從 hello **iot 邊緣**hello 覆盆子 Pi 上的資料夾：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="2ce3f-254">您可能需要 toopress hello 小按鈕，hello SensorTag 裝置 toomake 上它成為可搜尋才執行 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="2ce3f-255">當您執行 hello 範例時，您可以使用 hello[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)或 hello [iot 中樞總管](https://github.com/Azure/iothub-explorer)工具 toomonitor hello 訊息 hello IoT 邊緣閘道會將從 hello SensorTag 裝置轉送。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="2ce3f-256">例如，使用 iot 中樞總管您就可以監視裝置到雲端訊息使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="2ce3f-257">傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="2ce3f-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="2ce3f-258">hello b 模組也支援從 IoT 中樞 toohello 裝置傳送命令。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="2ce3f-259">您可以使用 hello[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)或 hello [iot 中樞總管](https://github.com/Azure/iothub-explorer)toohello b 裝置上的工具 toosend JSON 訊息 hello b 閘道模組轉送。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="2ce3f-260">如果您使用 hello 德州儀器 SensorTag 裝置，您可以開啟 LED hello 紅色、 綠色 LED 或警報器從 IoT 中樞傳送命令。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="2ce3f-261">您從 IoT 中樞傳送命令之前，先傳送 hello 下列兩個 JSON 訊息順序。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="2ce3f-262">然後您可以傳送任何 hello 命令 tooturn hello 燈號或警報器上。</span><span class="sxs-lookup"><span data-stu-id="2ce3f-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="2ce3f-263">重設所有 Led 和 hello 警報器 （關閉）：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="2ce3f-264">將 I/O 設定為「遠端」：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="2ce3f-265">現在您可以傳送任何 hello 遵循命令 tooturn hello 號誌或警報器 hello SensorTag 裝置上：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="2ce3f-266">開啟 hello 紅色 LED:</span><span class="sxs-lookup"><span data-stu-id="2ce3f-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="2ce3f-267">開啟 hello 綠色 LED:</span><span class="sxs-lookup"><span data-stu-id="2ce3f-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="2ce3f-268">開啟 hello 警報器：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="2ce3f-269">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ce3f-269">Next Steps</span></span>

<span data-ttu-id="2ce3f-270">如果您想進一步了解的 IoT 邊緣 toogain 試驗一些程式碼範例，請瀏覽 hello 下列開發人員教學課程和資源：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="2ce3f-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="2ce3f-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="2ce3f-272">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="2ce3f-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2ce3f-273">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="2ce3f-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
