## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="e6bc7-101">準備您的 Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="e6bc7-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="e6bc7-102">安裝 Raspbian</span><span class="sxs-lookup"><span data-stu-id="e6bc7-102">Install Raspbian</span></span>

<span data-ttu-id="e6bc7-103">如果這是 hello 用覆盆子 Pi 的第一次，您會需要 tooinstall hello Raspbian 使用作業系統 NOOBS hello 套件中包含的 hello SD 卡上。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="e6bc7-104">hello[覆盆子 Pi 軟體指南][ lnk-install-raspbian]描述如何 tooinstall 覆盆子 Pi 上的作業系統。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="e6bc7-105">本教學課程假設您已安裝 hello Raspbian 作業系統覆盆子 pi。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="e6bc7-106">包含在 hello hello sd 記憶卡[覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件][ lnk-starter-kits]已經有 NOOBS 安裝。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="e6bc7-107">您可以開機 hello 覆盆子 Pi 從這張介面卡，並選擇 tooinstall hello Raspbian OS。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="e6bc7-108">設定 hello 硬體</span><span class="sxs-lookup"><span data-stu-id="e6bc7-108">Set up hello hardware</span></span>

<span data-ttu-id="e6bc7-109">本教學課程使用包含在 hello hello BME280 感應器[覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件][ lnk-starter-kits] toogenerate 遙測資料。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="e6bc7-110">它會使用 LED tooindicate hello 覆盆子 Pi 處理從 hello 方案儀表板的方法引動過程時。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="e6bc7-111">hello hello bread 面板上的元件如下：</span><span class="sxs-lookup"><span data-stu-id="e6bc7-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="e6bc7-112">紅色 LED</span><span class="sxs-lookup"><span data-stu-id="e6bc7-112">Red LED</span></span>
- <span data-ttu-id="e6bc7-113">220-Ohm 電阻器 (紅色、紅色、棕色)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="e6bc7-114">BME280 感應器</span><span class="sxs-lookup"><span data-stu-id="e6bc7-114">BME280 sensor</span></span>

<span data-ttu-id="e6bc7-115">hello 下列圖表顯示如何 tooconnect 硬體：</span><span class="sxs-lookup"><span data-stu-id="e6bc7-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Raspberry Pi 的硬體設定][img-connection-diagram]

<span data-ttu-id="e6bc7-117">hello 下表摘要說明從 hello 覆盆子 Pi toohello 元件上 hello breadboard hello 連線：</span><span class="sxs-lookup"><span data-stu-id="e6bc7-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="e6bc7-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="e6bc7-118">Raspberry Pi</span></span>            | <span data-ttu-id="e6bc7-119">試驗電路板</span><span class="sxs-lookup"><span data-stu-id="e6bc7-119">Breadboard</span></span>             |<span data-ttu-id="e6bc7-120">色彩</span><span class="sxs-lookup"><span data-stu-id="e6bc7-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="e6bc7-121">GND (針腳 14)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-121">GND (Pin 14)</span></span>            | <span data-ttu-id="e6bc7-122">LED -ve 針腳 (18A)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="e6bc7-123">紫色</span><span class="sxs-lookup"><span data-stu-id="e6bc7-123">Purple</span></span>          |
| <span data-ttu-id="e6bc7-124">GPCLK0 (針腳 7)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="e6bc7-125">電阻器 (25A)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-125">Resistor (25A)</span></span>         | <span data-ttu-id="e6bc7-126">橙色</span><span class="sxs-lookup"><span data-stu-id="e6bc7-126">Orange</span></span>          |
| <span data-ttu-id="e6bc7-127">SPI_CE0 (針腳 24)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="e6bc7-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-128">CS (39A)</span></span>               | <span data-ttu-id="e6bc7-129">藍色</span><span class="sxs-lookup"><span data-stu-id="e6bc7-129">Blue</span></span>          |
| <span data-ttu-id="e6bc7-130">SPI_SCLK (針腳 23)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="e6bc7-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-131">SCK (36A)</span></span>              | <span data-ttu-id="e6bc7-132">黃色</span><span class="sxs-lookup"><span data-stu-id="e6bc7-132">Yellow</span></span>        |
| <span data-ttu-id="e6bc7-133">SPI_MISO (針腳 21)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="e6bc7-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-134">SDO (37A)</span></span>              | <span data-ttu-id="e6bc7-135">白色</span><span class="sxs-lookup"><span data-stu-id="e6bc7-135">White</span></span>         |
| <span data-ttu-id="e6bc7-136">SPI_MOSI (針腳 19)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="e6bc7-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-137">SDI (38A)</span></span>              | <span data-ttu-id="e6bc7-138">綠色</span><span class="sxs-lookup"><span data-stu-id="e6bc7-138">Green</span></span>         |
| <span data-ttu-id="e6bc7-139">GND (針腳 6)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-139">GND (Pin 6)</span></span>             | <span data-ttu-id="e6bc7-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-140">GND (35A)</span></span>              | <span data-ttu-id="e6bc7-141">黑色</span><span class="sxs-lookup"><span data-stu-id="e6bc7-141">Black</span></span>         |
| <span data-ttu-id="e6bc7-142">3.3 V (針腳 1)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="e6bc7-143">3Vo (34A)</span><span class="sxs-lookup"><span data-stu-id="e6bc7-143">3Vo (34A)</span></span>              | <span data-ttu-id="e6bc7-144">紅色</span><span class="sxs-lookup"><span data-stu-id="e6bc7-144">Red</span></span>           |

<span data-ttu-id="e6bc7-145">您需要 toocomplete hello 硬體安裝程式：</span><span class="sxs-lookup"><span data-stu-id="e6bc7-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="e6bc7-146">連接 hello 套件中包含您覆盆子 Pi toohello 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="e6bc7-147">您覆盆子 Pi tooyour 的網路連線使用包含在您的套件中的 hello 乙太網路纜線。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="e6bc7-148">或者，您可以為 Raspberry Pi 設定[無線連線能力][lnk-pi-wireless]。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="e6bc7-149">您現在已完成覆盆子 Pi 的 hello 硬體安裝。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="e6bc7-150">登入及存取 hello 終端機</span><span class="sxs-lookup"><span data-stu-id="e6bc7-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="e6bc7-151">您有兩個選項 tooaccess 終端機環境覆盆子 Pi 上：</span><span class="sxs-lookup"><span data-stu-id="e6bc7-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="e6bc7-152">如果您有鍵盤，監視連線的 tooyour 覆盆子 Pi，您可以使用 hello Raspbian GUI tooaccess 終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="e6bc7-153">從您桌面的電腦使用 SSH 您覆盆子 pi hello 命令列存取。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="e6bc7-154">在 hello GUI 中的終端機視窗</span><span class="sxs-lookup"><span data-stu-id="e6bc7-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="e6bc7-155">Raspbian hello 預設認證是使用者名稱**pi**和密碼**覆盆子**。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="e6bc7-156">您可以在 hello 工作列 hello GUI 中，啟動 hello**終端機**使用 hello 圖示看起來像監視器公用程式。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="e6bc7-157">使用 SSH 登入</span><span class="sxs-lookup"><span data-stu-id="e6bc7-157">Sign in with SSH</span></span>

<span data-ttu-id="e6bc7-158">您可以使用 SSH 的命令列存取 tooyour 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="e6bc7-159">hello 文章[SSH (Secure Shell)] [ lnk-pi-ssh]描述如何 tooconfigure SSH 您覆盆子 pi，以及如何從 tooconnect [Windows] [ lnk-ssh-windows]或[Linux 和 Mac OS][lnk-ssh-linux]。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="e6bc7-160">以使用者名稱 **pi** 和密碼 **raspberry** 登入。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="e6bc7-161">選擇性︰共用 Raspberry Pi 上的資料夾</span><span class="sxs-lookup"><span data-stu-id="e6bc7-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="e6bc7-162">或者，您可能想覆盆子 pi tooshare 資料夾與您的桌面環境。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="e6bc7-163">共用資料夾可讓您 toouse 慣用桌面的文字編輯器 (例如[Visual Studio Code](https://code.visualstudio.com/)或[適文字](http://www.sublimetext.com/)) tooedit 檔案，而不是使用您覆盆子 pi`nano`或`vi`.</span><span class="sxs-lookup"><span data-stu-id="e6bc7-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="e6bc7-164">隨 Windows 資料夾 tooshare Samba 上設定伺服器 hello 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="e6bc7-165">或者，使用內建的 hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) SFTP 用戶端在桌面上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="e6bc7-166">啟用 SPI</span><span class="sxs-lookup"><span data-stu-id="e6bc7-166">Enable SPI</span></span>

<span data-ttu-id="e6bc7-167">您可以執行 hello 範例應用程式之前，您必須啟用 hello 序列周邊介面 (SPI) 匯流排上 hello 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="e6bc7-168">hello SPI 匯流排上，與 hello BME280 感應器裝置通訊 hello 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="e6bc7-169">使用下列命令 tooedit hello 設定檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6bc7-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="e6bc7-170">找出 hello 一行：</span><span class="sxs-lookup"><span data-stu-id="e6bc7-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="e6bc7-171">toouncomment hello 列，delete hello `#` hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="e6bc7-172">儲存您的變更 (**Ctrl-O**， **Enter**) 和結束 hello 編輯器 (**Ctrl X**)。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="e6bc7-173">tooenable SPI，重新啟動 hello 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="e6bc7-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="e6bc7-174">重新啟動中斷連線的 hello 終端機，您需要 toosign 中再次 hello 覆盆子 Pi 重新啟動時：</span><span class="sxs-lookup"><span data-stu-id="e6bc7-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/