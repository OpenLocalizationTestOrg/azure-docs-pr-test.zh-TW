---
title: "搭配 Azure IoT Edge 使用實體裝置 | Microsoft Docs"
description: "如何使用 Texas Instruments SensorTag 裝置，透過 Raspberry Pi 3 上執行的 IoT Edge 閘道將資料傳送至 IoT 中樞。 閘道是使用 Azure IoT Edge 所建置的。"
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
ms.openlocfilehash: 02962a91c739a53dfcf947bcc736e5c293b9384f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-to-forward-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="86c1e-104">在 Raspberry Pi 上使用 Azure IoT Edge 將裝置到雲端訊息轉送到 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="86c1e-104">Use Azure IoT Edge on a Raspberry Pi to forward device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="86c1e-105">本逐步解說的[藍牙低功耗範例][lnk-ble-samplecode]示範如何使用 [Azure IoT Edge][lnk-sdk] 以便：</span><span class="sxs-lookup"><span data-stu-id="86c1e-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="86c1e-106">從實體裝置將裝置對雲端遙測轉送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="86c1e-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span></span>
* <span data-ttu-id="86c1e-107">將命令從 IoT 中樞路由傳送至實體裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-107">Route commands from IoT Hub to a physical device.</span></span>

<span data-ttu-id="86c1e-108">本逐步解說涵蓋下列項目：</span><span class="sxs-lookup"><span data-stu-id="86c1e-108">This walkthrough covers:</span></span>

* <span data-ttu-id="86c1e-109">**架構**：有關藍牙低功耗範例的重要架構資訊。</span><span class="sxs-lookup"><span data-stu-id="86c1e-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span></span>
* <span data-ttu-id="86c1e-110">**建置和執行**︰建置和執行範例所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="86c1e-110">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="86c1e-111">架構</span><span class="sxs-lookup"><span data-stu-id="86c1e-111">Architecture</span></span>

<span data-ttu-id="86c1e-112">本逐步解說會示範如何在執行 Raspbian Linux 的 Raspberry Pi 3 上建置和執行 IoT Edge 閘道。</span><span class="sxs-lookup"><span data-stu-id="86c1e-112">The walkthrough shows you how to build and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="86c1e-113">閘道是使用 IoT Edge 所建置的。</span><span class="sxs-lookup"><span data-stu-id="86c1e-113">The gateway is built using IoT Edge.</span></span> <span data-ttu-id="86c1e-114">這個範例會使用 Texas Instruments SensorTag 藍牙低功耗 (BLE) 裝置來收集溫度資料。</span><span class="sxs-lookup"><span data-stu-id="86c1e-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span></span>

<span data-ttu-id="86c1e-115">當您執行 IoT Edge 閘道時，它會執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-115">When you run the IoT Edge gateway it:</span></span>

* <span data-ttu-id="86c1e-116">使用藍牙低功耗 (BLE) 通訊協定連接到 SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="86c1e-117">使用 HTTP 通訊協定來連接到「IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="86c1e-117">Connects to IoT Hub using the HTTP protocol.</span></span>
* <span data-ttu-id="86c1e-118">將遙測從 SensorTag 裝置轉送到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="86c1e-118">Forwards telemetry from the SensorTag device to IoT Hub.</span></span>
* <span data-ttu-id="86c1e-119">將命令從 IoT 中樞路由傳送到 SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-119">Routes commands from IoT Hub to the SensorTag device.</span></span>

<span data-ttu-id="86c1e-120">閘道包含下列 IoT Edge 模組︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-120">The gateway contains the following IoT Edge modules:</span></span>

* <span data-ttu-id="86c1e-121">「BLE 模組」  ，可與 BLE 裝置接合，以接收來自裝置的溫度資料，並將命令傳送到裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span></span>
* <span data-ttu-id="86c1e-122">「BLE 雲端至裝置模組」，可將從 IoT 中樞傳送的 JSON 訊息轉譯為「BLE 模組」所用的 BLE 指示。</span><span class="sxs-lookup"><span data-stu-id="86c1e-122">A *BLE cloud to device module* that translates JSON messages sent from IoT Hub into BLE instructions for the *BLE module*.</span></span>
* <span data-ttu-id="86c1e-123">「記錄器模組」，可將所有閘道訊息記錄到本機檔案。</span><span class="sxs-lookup"><span data-stu-id="86c1e-123">A *logger module* that logs all gateway messages to a local file.</span></span>
* <span data-ttu-id="86c1e-124">「身分識別對應模組」  ，可在 BLE 裝置 MAC 位址與 Azure IoT 中樞裝置身分識別之間進行轉譯。</span><span class="sxs-lookup"><span data-stu-id="86c1e-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="86c1e-125">「IoT 中樞模組」  ，將遙測資料上傳到 IoT 中樞，並從 IoT 中樞接收裝置命令。</span><span class="sxs-lookup"><span data-stu-id="86c1e-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="86c1e-126">「BLE 印表機模組」  ，可解譯來自 BLE 裝置的遙測，並將格式化的資料列印到主控台以啟用疑難排解和偵錯。</span><span class="sxs-lookup"><span data-stu-id="86c1e-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-the-gateway"></a><span data-ttu-id="86c1e-127">資料透過閘道流動的方式</span><span class="sxs-lookup"><span data-stu-id="86c1e-127">How data flows through the gateway</span></span>

<span data-ttu-id="86c1e-128">下列區塊圖說明遙測上傳資料流程路線︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span></span>

![遙測上傳閘道管線](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="86c1e-130">遙測的項目從 BLE 裝置流動到 IoT 中樞要採取的步驟如下：</span><span class="sxs-lookup"><span data-stu-id="86c1e-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span></span>

1. <span data-ttu-id="86c1e-131">BLE 裝置會產生溫度範例，並透過藍牙將它傳送到閘道中的 BLE 模組。</span><span class="sxs-lookup"><span data-stu-id="86c1e-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span></span>
1. <span data-ttu-id="86c1e-132">BLE 模組會接收範例，並將其發佈到訊息代理程式以及裝置的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="86c1e-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span></span>
1. <span data-ttu-id="86c1e-133">身分識別對應模組會挑選出這個訊息，並使用內部資料表來將裝置的 MAC 位址轉譯為 IoT 中樞裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="86c1e-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span></span> <span data-ttu-id="86c1e-134">IoT 中樞裝置身分識別是由裝置識別碼及裝置金鑰所組成。</span><span class="sxs-lookup"><span data-stu-id="86c1e-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="86c1e-135">識別對應模組會發佈新訊息，其中包含溫度取樣資料、裝置的 MAC 位址、裝置識別碼及裝置金鑰。</span><span class="sxs-lookup"><span data-stu-id="86c1e-135">The identity mapping module publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span></span>
1. <span data-ttu-id="86c1e-136">IoT 中樞模組會接收這個新訊息 (由身分識別對應模組所產生)，並將其發佈到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="86c1e-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span></span>
1. <span data-ttu-id="86c1e-137">記錄器模組會將所有來自訊息代理程式的所有訊息記錄到本機檔案。</span><span class="sxs-lookup"><span data-stu-id="86c1e-137">The logger module logs all messages from the broker to a local file.</span></span>

<span data-ttu-id="86c1e-138">下列區塊圖說明裝置命令資料流程路線︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-138">The following block diagram illustrates the device command data flow pipeline:</span></span>

![裝置命令閘道管線](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="86c1e-140">IoT 中樞模組會定期輪詢 IoT 中樞以取得新的命令訊息。</span><span class="sxs-lookup"><span data-stu-id="86c1e-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span></span>
1. <span data-ttu-id="86c1e-141">當 IoT 中樞模組接收到新的命令訊息時，會將其發佈到訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="86c1e-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span></span>
1. <span data-ttu-id="86c1e-142">身分識別對應模組會挑選出命令訊息，並使用內部資料表來將 IoT 中樞裝置識別碼轉譯到裝置的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="86c1e-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span></span> <span data-ttu-id="86c1e-143">接著將發佈新訊息，其中會在訊息的屬性對應中包含目標裝置的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="86c1e-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span></span>
1. <span data-ttu-id="86c1e-144">BLE 雲端至裝置模組會挑選此訊息，並將其轉譯成適當的 BLE 指示供 BLE 模組使用。</span><span class="sxs-lookup"><span data-stu-id="86c1e-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span></span> <span data-ttu-id="86c1e-145">接著將發佈新訊息。</span><span class="sxs-lookup"><span data-stu-id="86c1e-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="86c1e-146">BLE 模組會挑選出這個訊息，然後藉由與 BLE 裝置通訊來執行 I/O 指令。</span><span class="sxs-lookup"><span data-stu-id="86c1e-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span></span>
1. <span data-ttu-id="86c1e-147">記錄器模組會將所有來自訊息代理程式的所有訊息記錄到磁碟檔案。</span><span class="sxs-lookup"><span data-stu-id="86c1e-147">The logger module logs all messages from the broker to a disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86c1e-148">必要條件</span><span class="sxs-lookup"><span data-stu-id="86c1e-148">Prerequisites</span></span>

<span data-ttu-id="86c1e-149">若要完成此教學課程，您需要一個有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="86c1e-149">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="86c1e-150">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="86c1e-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="86c1e-151">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="86c1e-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="86c1e-152">您需要透過桌上型電腦上的 SSH 用戶端，才能從遠端存取 Raspberry Pi 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="86c1e-152">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="86c1e-153">Windows 不包含 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="86c1e-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="86c1e-154">我們建議使用 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="86c1e-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="86c1e-155">大部分的 Linux 散發套件和 Mac OS 都包含命令列 SSH 公用程式。</span><span class="sxs-lookup"><span data-stu-id="86c1e-155">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="86c1e-156">如需詳細資訊，請參閱[使用 Linux 或 Mac OS 的 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)。</span><span class="sxs-lookup"><span data-stu-id="86c1e-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="86c1e-157">準備硬體</span><span class="sxs-lookup"><span data-stu-id="86c1e-157">Prepare your hardware</span></span>

<span data-ttu-id="86c1e-158">本教學課程假設您正在使用 [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) 裝置連接到執行 Raspbian 的 Raspberry Pi 3。</span><span class="sxs-lookup"><span data-stu-id="86c1e-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="86c1e-159">安裝 Raspbian</span><span class="sxs-lookup"><span data-stu-id="86c1e-159">Install Raspbian</span></span>

<span data-ttu-id="86c1e-160">您可以使用下列任一選項在 Raspberry Pi 3 裝置上安裝 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="86c1e-160">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="86c1e-161">若要安裝最新版的 Raspbian，請使用 [NOOBS][lnk-noobs] 圖形化使用者介面。</span><span class="sxs-lookup"><span data-stu-id="86c1e-161">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="86c1e-162">手動[下載][lnk-raspbian]最新的 Raspbian 作業系統映像並寫入到 SD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="86c1e-162">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="86c1e-163">登入及存取終端機</span><span class="sxs-lookup"><span data-stu-id="86c1e-163">Sign in and access the terminal</span></span>

<span data-ttu-id="86c1e-164">您有兩個選項可存取 Raspberry Pi 上的終端機環境︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-164">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="86c1e-165">如果您的 Raspberry Pi 已連接鍵盤與監視器，您可以使用 Raspbian GUI 來存取終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="86c1e-165">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

* <span data-ttu-id="86c1e-166">使用 SSH 從您的桌上型電腦存取 Raspberry Pi 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="86c1e-166">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="86c1e-167">在 GUI 中使用終端機視窗</span><span class="sxs-lookup"><span data-stu-id="86c1e-167">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="86c1e-168">Raspbian 的預設認證是使用者名稱 **pi** 和密碼 **raspberry**。</span><span class="sxs-lookup"><span data-stu-id="86c1e-168">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="86c1e-169">在 GUI 的工作列中，您可以使用看似監視器的圖示來啟動 **Terminal** 公用程式。</span><span class="sxs-lookup"><span data-stu-id="86c1e-169">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="86c1e-170">使用 SSH 登入</span><span class="sxs-lookup"><span data-stu-id="86c1e-170">Sign in with SSH</span></span>

<span data-ttu-id="86c1e-171">您可以使用命令列的 SSH 存取 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="86c1e-171">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="86c1e-172">[SSH (安全殼層)][lnk-pi-ssh] 一文說明如何在 Raspberry Pi 上設定 SSH，以及如何從 [Windows][lnk-ssh-windows] 或 [Linux 和 Mac OS][lnk-ssh-linux] 連接。</span><span class="sxs-lookup"><span data-stu-id="86c1e-172">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="86c1e-173">以使用者名稱 **pi** 和密碼 **raspberry** 登入。</span><span class="sxs-lookup"><span data-stu-id="86c1e-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="86c1e-174">安裝 BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="86c1e-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="86c1e-175">BLE 模組會透過 BlueZ 堆疊與藍牙硬體通訊。</span><span class="sxs-lookup"><span data-stu-id="86c1e-175">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span></span> <span data-ttu-id="86c1e-176">您需要 5.37 版的 BlueZ 才能讓模組正常運作。</span><span class="sxs-lookup"><span data-stu-id="86c1e-176">You need version 5.37 of BlueZ for the modules to work correctly.</span></span> <span data-ttu-id="86c1e-177">下列指示可確保所安裝的 BlueZ 版本不會錯誤。</span><span class="sxs-lookup"><span data-stu-id="86c1e-177">These instructions make sure the correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="86c1e-178">停止目前的藍牙精靈：</span><span class="sxs-lookup"><span data-stu-id="86c1e-178">Stop the current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="86c1e-179">安裝 BlueZ 相依項目：</span><span class="sxs-lookup"><span data-stu-id="86c1e-179">Install the BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="86c1e-180">從 bluez.org 下載 BlueZ 原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="86c1e-180">Download the BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="86c1e-181">將原始程式碼解壓縮：</span><span class="sxs-lookup"><span data-stu-id="86c1e-181">Unzip the source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="86c1e-182">將目錄變更為新建立的資料夾：</span><span class="sxs-lookup"><span data-stu-id="86c1e-182">Change directories to the newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="86c1e-183">設定要建置的 BlueZ 程式碼：</span><span class="sxs-lookup"><span data-stu-id="86c1e-183">Configure the BlueZ code to be built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="86c1e-184">建置 BlueZ：</span><span class="sxs-lookup"><span data-stu-id="86c1e-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="86c1e-185">完成建置後安裝 BlueZ：</span><span class="sxs-lookup"><span data-stu-id="86c1e-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="86c1e-186">變更藍牙的 systemd 服務組態，讓它指向`/lib/systemd/system/bluetooth.service` 檔案中的新藍牙精靈。</span><span class="sxs-lookup"><span data-stu-id="86c1e-186">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="86c1e-187">使用下列文字來取代「ExecStart」程式碼行：</span><span class="sxs-lookup"><span data-stu-id="86c1e-187">Replace the 'ExecStart' line with the following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="86c1e-188">從 Raspberry Pi 3 裝置上啟用與 SensorTag 裝置的連線</span><span class="sxs-lookup"><span data-stu-id="86c1e-188">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="86c1e-189">執行範例之前，您需要確認 Raspberry Pi 3 可連接到 SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-189">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span></span>

1. <span data-ttu-id="86c1e-190">確定已安裝 `rfkill` 公用程式：</span><span class="sxs-lookup"><span data-stu-id="86c1e-190">Ensure the `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="86c1e-191">將 Raspberry Pi 3 上的藍牙解除封鎖，並檢查版本號碼為 **5.37**：</span><span class="sxs-lookup"><span data-stu-id="86c1e-191">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="86c1e-192">若要進入互動式藍牙殼層，請啟動藍牙服務並執行 **bluetoothctl** 命令：</span><span class="sxs-lookup"><span data-stu-id="86c1e-192">To enter the interactive bluetooth shell, start the bluetooth service and execute the **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="86c1e-193">輸入 **power on** 命令來開啟藍牙控制器電源。</span><span class="sxs-lookup"><span data-stu-id="86c1e-193">Enter the command **power on** to power up the bluetooth controller.</span></span> <span data-ttu-id="86c1e-194">命令會傳回類似下列內容的輸出：</span><span class="sxs-lookup"><span data-stu-id="86c1e-194">The command returns output similar to the following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="86c1e-195">在互動式藍牙殼層中的狀態下，輸入 **scan on** 命令以掃描藍牙裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-195">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span></span> <span data-ttu-id="86c1e-196">命令會傳回類似下列內容的輸出：</span><span class="sxs-lookup"><span data-stu-id="86c1e-196">The command returns output similar to the following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="86c1e-197">按下小按鈕 (綠色 LED 應該會閃爍)，以使 SensorTag 裝置變成可探索的。</span><span class="sxs-lookup"><span data-stu-id="86c1e-197">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span></span> <span data-ttu-id="86c1e-198">Raspberry Pi 3 應該會探索 SensorTag 裝置︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-198">The Raspberry Pi 3 should discover the SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="86c1e-199">在此範例中，您可以看到 SensorTag 裝置的 MAC 位址是 **A0:E6:F8:B5:F6:00**。</span><span class="sxs-lookup"><span data-stu-id="86c1e-199">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="86c1e-200">輸入 **scan off** 命令來關閉掃描：</span><span class="sxs-lookup"><span data-stu-id="86c1e-200">Turn off scanning by entering the **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="86c1e-201">透過輸入 **connect \<MAC 位址\>**，使用裝置的 MAC 位址來連接到 SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-201">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="86c1e-202">下列範例輸出為了清楚起見已縮減：</span><span class="sxs-lookup"><span data-stu-id="86c1e-202">The following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting to connect to A0:E6:F8:B5:F6:00
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

    > <span data-ttu-id="86c1e-203">您可以使用 **list-attributes** 命令，再次列出裝置的 GATT 特性。</span><span class="sxs-lookup"><span data-stu-id="86c1e-203">You can list the GATT characteristics of the device again using the **list-attributes** command.</span></span>

1. <span data-ttu-id="86c1e-204">您現在可以使用 **disconnect** 命令來中斷連接，然後使用 **quit** 命令來從藍牙介面結束︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-204">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span></span>

    ```sh
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="86c1e-205">您現在已經準備好在 Raspberry Pi 3 上執行 BLE IoT Edge 範例。</span><span class="sxs-lookup"><span data-stu-id="86c1e-205">You're now ready to run the BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-the-iot-edge-ble-sample"></a><span data-ttu-id="86c1e-206">執行 IoT Edge BLE 範例</span><span class="sxs-lookup"><span data-stu-id="86c1e-206">Run the IoT Edge BLE sample</span></span>

<span data-ttu-id="86c1e-207">若要執行 IoT Edge BLE 範例，您必須完成三項工作︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-207">To run the IoT Edge BLE sample, you need to complete three tasks:</span></span>

* <span data-ttu-id="86c1e-208">在您的 IoT 中樞上設定兩個範例裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="86c1e-209">在 Raspberry Pi 3 裝置上建置 IoT Edge。</span><span class="sxs-lookup"><span data-stu-id="86c1e-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="86c1e-210">在 Raspberry Pi 3 裝置上設定和執行 BLE 範例。</span><span class="sxs-lookup"><span data-stu-id="86c1e-210">Configure and run the BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="86c1e-211">在撰寫本文之際，IoT Edge 只支援 Linux 上所執行閘道中的 BLE 模組。</span><span class="sxs-lookup"><span data-stu-id="86c1e-211">At the time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="86c1e-212">在您的 IoT 中樞上設定兩個範例裝置</span><span class="sxs-lookup"><span data-stu-id="86c1e-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="86c1e-213">於 Azure 訂用帳戶中[建立 IoT 中樞][lnk-create-hub]時，您需要中樞名稱才能完成此逐步解說。</span><span class="sxs-lookup"><span data-stu-id="86c1e-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="86c1e-214">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="86c1e-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="86c1e-215">在您的 IoT 中樞新增一個名為 **SensorTag_01** 的裝置，並記下其識別碼和裝置金鑰。</span><span class="sxs-lookup"><span data-stu-id="86c1e-215">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="86c1e-216">您可以使用[裝置總管或 iothub-explorer][lnk-explorer-tools] 工具，將這個裝置新增到您在上一個步驟中建立的 IoT 中樞，並擷取其金鑰。</span><span class="sxs-lookup"><span data-stu-id="86c1e-216">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span></span> <span data-ttu-id="86c1e-217">當您設定閘道時，您會將此裝置對應到 SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-217">You map this device to the SensorTag device when you configure the gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="86c1e-218">在 Raspberry Pi 3 上建置 Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="86c1e-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="86c1e-219">安裝 Azure IoT Edge 的相依項目：</span><span class="sxs-lookup"><span data-stu-id="86c1e-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="86c1e-220">使用下列命令將 IoT Edge 及其所有子模組複製到主目錄︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-220">Use the following commands to clone IoT Edge and all its submodules to your home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="86c1e-221">當您的 Raspberry Pi 3 上擁有 IoT Edge 存放庫的完整複本時，您就可以使用下列命令，從包含該 SDK 的資料夾建置它：</span><span class="sxs-lookup"><span data-stu-id="86c1e-221">When you have a complete copy of the IoT Edge repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="86c1e-222">在 Raspberry Pi 3 上設定和執行 BLE 範例</span><span class="sxs-lookup"><span data-stu-id="86c1e-222">Configure and run the BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="86c1e-223">若要啟動並執行範例，您必須設定參與閘道的每個 IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="86c1e-223">To bootstrap and run the sample, you must configure each IoT Edge module that participates in the gateway.</span></span> <span data-ttu-id="86c1e-224">這個組態是以 JSON 檔案來提供，您必須設定所有五個參與的 IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="86c1e-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="86c1e-225">存放庫中有一個名為 **gateway\_sample.json** 的範例 JSON 檔案，您可以把它當作起點，開始建立自己的組態檔。</span><span class="sxs-lookup"><span data-stu-id="86c1e-225">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span></span> <span data-ttu-id="86c1e-226">這個檔案位於 IoT Edge 存放庫本機複本的 **samples/ble_gateway/src** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="86c1e-226">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Edge repository.</span></span>

<span data-ttu-id="86c1e-227">下列各節說明如何編輯 BLE 範例的這個組態檔，並假設 IoT Edge 存放庫位於 Raspberry Pi 3 上的 **/home/pi/iot-edge/** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="86c1e-227">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Edge repository is in the **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="86c1e-228">如果存放庫位於其他地方，請據以調整路徑。</span><span class="sxs-lookup"><span data-stu-id="86c1e-228">If the repository is elsewhere, adjust the paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="86c1e-229">記錄器組態</span><span class="sxs-lookup"><span data-stu-id="86c1e-229">Logger configuration</span></span>

<span data-ttu-id="86c1e-230">假設閘道存放庫位於 **/home/pi/iot-edge/** 資料夾中，請以如下方式設定記錄器模組：</span><span class="sxs-lookup"><span data-stu-id="86c1e-230">Assuming the gateway repository is located in the **/home/pi/iot-edge/** folder, configure the logger module as follows:</span></span>

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

#### <a name="ble-module-configuration"></a><span data-ttu-id="86c1e-231">BLE 模組組態</span><span class="sxs-lookup"><span data-stu-id="86c1e-231">BLE module configuration</span></span>

<span data-ttu-id="86c1e-232">BLE 裝置的範例組態會假設 Texas Instruments SensorTag 裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-232">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="86c1e-233">任何可作為 GATT 週邊操作的標準 BLE 裝置應該都可以運作，但您可能需要更新 GATT 特性識別碼和資料。</span><span class="sxs-lookup"><span data-stu-id="86c1e-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need to update the GATT characteristic IDs and data.</span></span> <span data-ttu-id="86c1e-234">新增 SensorTag 裝置的 MAC 位址︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-234">Add the MAC address of your SensorTag device:</span></span>

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

<span data-ttu-id="86c1e-235">如果您不是使用 SensorTag 裝置，請檢閱 BLE 裝置的文件，以判斷是否需要更新 GATT 特性識別碼和資料值。</span><span class="sxs-lookup"><span data-stu-id="86c1e-235">If you are not using a SensorTag device, review the documentation for your BLE device to determine whether you need to update the GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="86c1e-236">IoT 中樞模組</span><span class="sxs-lookup"><span data-stu-id="86c1e-236">IoT Hub module</span></span>

<span data-ttu-id="86c1e-237">新增 IoT 中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="86c1e-237">Add the name of your IoT Hub.</span></span> <span data-ttu-id="86c1e-238">尾碼值通常是 **azure-devices.net**：</span><span class="sxs-lookup"><span data-stu-id="86c1e-238">The suffix value is typically **azure-devices.net**:</span></span>

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

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="86c1e-239">身分識別對應模組組態</span><span class="sxs-lookup"><span data-stu-id="86c1e-239">Identity mapping module configuration</span></span>

<span data-ttu-id="86c1e-240">新增 SensorTag 裝置的 MAC 位址，以及您新增至 IoT 中樞之 **SensorTag_01** 裝置的裝置識別碼和金鑰：</span><span class="sxs-lookup"><span data-stu-id="86c1e-240">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span></span>

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

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="86c1e-241">BLE 印表機模組組態</span><span class="sxs-lookup"><span data-stu-id="86c1e-241">BLE Printer module configuration</span></span>

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

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="86c1e-242">BLEC2D 模組組態</span><span class="sxs-lookup"><span data-stu-id="86c1e-242">BLEC2D Module Configuration</span></span>

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

#### <a name="routing-configuration"></a><span data-ttu-id="86c1e-243">路由組態</span><span class="sxs-lookup"><span data-stu-id="86c1e-243">Routing Configuration</span></span>

<span data-ttu-id="86c1e-244">下列組態可確保 IoT Edge 模組之間的下列路由：</span><span class="sxs-lookup"><span data-stu-id="86c1e-244">The following configuration ensures the following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="86c1e-245">**Logger** 模組接收並記錄所有訊息。</span><span class="sxs-lookup"><span data-stu-id="86c1e-245">The **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="86c1e-246">**SensorTag** 模組會將訊息傳送至 **mapping** 和 **BLE Printer** 模組。</span><span class="sxs-lookup"><span data-stu-id="86c1e-246">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="86c1e-247">**mapping** 模組會將準備傳送至您的 IoT 中樞的訊息傳送給 **IoTHub** 模組。</span><span class="sxs-lookup"><span data-stu-id="86c1e-247">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span></span>
* <span data-ttu-id="86c1e-248">**IoTHub** 模組會將訊息傳回給 **mapping** 模組。</span><span class="sxs-lookup"><span data-stu-id="86c1e-248">The **IoTHub** module sends messages back to the **mapping** module.</span></span>
* <span data-ttu-id="86c1e-249">**mapping** 模組會將訊息傳送給 **BLEC2D** 模組。</span><span class="sxs-lookup"><span data-stu-id="86c1e-249">The **mapping** module sends messages to the **BLEC2D** module.</span></span>
* <span data-ttu-id="86c1e-250">**BLEC2D** 模組會將訊息傳回給 **Sensor Tag** 模組。</span><span class="sxs-lookup"><span data-stu-id="86c1e-250">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span></span>

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

<span data-ttu-id="86c1e-251">若要執行範例，請將 JSON 組態檔的路徑傳遞到 **ble\_gateway** 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="86c1e-251">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span></span> <span data-ttu-id="86c1e-252">下列命令假設您正在使用 **gateway_sample.json** 組態檔。</span><span class="sxs-lookup"><span data-stu-id="86c1e-252">The following command assumes you are using the **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="86c1e-253">在 Raspberry Pi 上從 **iot-edge** 資料夾執行此命令：</span><span class="sxs-lookup"><span data-stu-id="86c1e-253">Execute this command from the **iot-edge** folder on the Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="86c1e-254">執行範例之前，您可能需要按下 SensorTag 上的小按鈕，以使其變成可探索的項目。</span><span class="sxs-lookup"><span data-stu-id="86c1e-254">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span></span>

<span data-ttu-id="86c1e-255">當您執行範例時，可以使用 [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 或 [iothub-explorer](https://github.com/Azure/iothub-explorer) 工具，監視 IoT Edge 閘道從 SensorTag 裝置轉送的訊息。</span><span class="sxs-lookup"><span data-stu-id="86c1e-255">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the IoT Edge gateway forwards from the SensorTag device.</span></span> <span data-ttu-id="86c1e-256">例如，您可以使用 iothub-explorer，然後使用以下命令 監控裝置到雲端訊息：</span><span class="sxs-lookup"><span data-stu-id="86c1e-256">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="86c1e-257">傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="86c1e-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="86c1e-258">BLE 模組也支援從 IoT 中樞傳送命令至裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-258">The BLE module also supports sending commands from IoT Hub to the device.</span></span> <span data-ttu-id="86c1e-259">您可以使用[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)或 [iothub-explorer](https://github.com/Azure/iothub-explorer) 工具來傳送 JSON 訊息，再由 BLE 閘道模組轉送至 BLE 裝置。</span><span class="sxs-lookup"><span data-stu-id="86c1e-259">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span></span>

<span data-ttu-id="86c1e-260">如果您使用 Texas Instruments SensorTag 裝置，則可以從 IoT 中樞傳送命令以開啟紅色 LED、綠色 LED 或警報器。</span><span class="sxs-lookup"><span data-stu-id="86c1e-260">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="86c1e-261">從 IoT 中樞傳送命令之前，請先依序傳送下列兩個 JSON 訊息。</span><span class="sxs-lookup"><span data-stu-id="86c1e-261">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span></span> <span data-ttu-id="86c1e-262">然後，您可以傳送任何命令以開啟燈號或警報器。</span><span class="sxs-lookup"><span data-stu-id="86c1e-262">Then you can send any of the commands to turn on the lights or buzzer.</span></span>

1. <span data-ttu-id="86c1e-263">重設所有的 LED 與警報器 (將其關閉)：</span><span class="sxs-lookup"><span data-stu-id="86c1e-263">Reset all LEDs and the buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="86c1e-264">將 I/O 設定為「遠端」：</span><span class="sxs-lookup"><span data-stu-id="86c1e-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="86c1e-265">現在您可以在 SensorTag 裝置上傳送下列任何命令來開啟燈號或警報器：</span><span class="sxs-lookup"><span data-stu-id="86c1e-265">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span></span>

* <span data-ttu-id="86c1e-266">開啟紅色 LED：</span><span class="sxs-lookup"><span data-stu-id="86c1e-266">Turn on the red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="86c1e-267">開啟綠色 LED：</span><span class="sxs-lookup"><span data-stu-id="86c1e-267">Turn on the green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="86c1e-268">開啟警報器：</span><span class="sxs-lookup"><span data-stu-id="86c1e-268">Turn on the buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="86c1e-269">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86c1e-269">Next Steps</span></span>

<span data-ttu-id="86c1e-270">如果您想要更進一步了解 IoT Edge 並實驗一些程式碼範例，請瀏覽下列開發人員教學課程和資源：</span><span class="sxs-lookup"><span data-stu-id="86c1e-270">If you want to gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="86c1e-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="86c1e-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="86c1e-272">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="86c1e-272">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="86c1e-273">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="86c1e-273">[IoT Hub developer guide][lnk-devguide]</span></span>

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
