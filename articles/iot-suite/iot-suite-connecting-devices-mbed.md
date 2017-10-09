---
title: "一部裝置上 mbed 使用 C aaaConnect |Microsoft 文件"
description: "描述如何 tooconnect 裝置 toohello Azure IoT 套件預先設定的遠端使用撰寫 C mbed 裝置上執行的應用程式的監視解決方案。"
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="f129d-103">連接您的裝置 toohello 遠端監視預先設定的解決方案 (mbed)</span><span class="sxs-lookup"><span data-stu-id="f129d-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="f129d-104">案例概觀</span><span class="sxs-lookup"><span data-stu-id="f129d-104">Scenario overview</span></span>
<span data-ttu-id="f129d-105">在此案例中，您會建立傳送嗨遵循遙測 toohello 遠端監視的裝置[預先設定的解決方案][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="f129d-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="f129d-106">外部溫度</span><span class="sxs-lookup"><span data-stu-id="f129d-106">External temperature</span></span>
* <span data-ttu-id="f129d-107">內部溫度</span><span class="sxs-lookup"><span data-stu-id="f129d-107">Internal temperature</span></span>
* <span data-ttu-id="f129d-108">溼度</span><span class="sxs-lookup"><span data-stu-id="f129d-108">Humidity</span></span>

<span data-ttu-id="f129d-109">為了簡單起見，hello hello 裝置上的程式碼會產生範例值，但我們鼓勵您 tooextend hello 範例實際感應器 tooyour 裝置連接和傳送實際的遙測。</span><span class="sxs-lookup"><span data-stu-id="f129d-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="f129d-110">hello 裝置也是可以 toorespond toomethods hello 方案儀表板從叫用，且想要設定 hello 方案儀表板中的屬性值。</span><span class="sxs-lookup"><span data-stu-id="f129d-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="f129d-111">toocomplete 本教學課程中，您需要使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f129d-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="f129d-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f129d-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f129d-113">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="f129d-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f129d-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="f129d-114">Before you start</span></span>
<span data-ttu-id="f129d-115">在您為裝置撰寫任何程式碼之前，您必須先佈建遠端監視預先設定解決方案，並在該解決方案中佈建新的自訂裝置。</span><span class="sxs-lookup"><span data-stu-id="f129d-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="f129d-116">佈建遠端監視預先設定解決方案</span><span class="sxs-lookup"><span data-stu-id="f129d-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="f129d-117">您在本教學課程中建立的 hello 裝置傳送嗨資料 tooan 執行個體[遠端監視][ lnk-remote-monitoring]預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f129d-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="f129d-118">如果您沒有已佈建 hello 遠端監視您的 Azure 帳戶中預先設定的解決方案，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f129d-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="f129d-119">在 hello <https://www.azureiotsuite.com/>頁面上，按一下 **+**  toocreate 方案。</span><span class="sxs-lookup"><span data-stu-id="f129d-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="f129d-120">按一下**選取**上 hello**遠端監視**面板 toocreate 您的方案。</span><span class="sxs-lookup"><span data-stu-id="f129d-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="f129d-121">在 hello**建立遠端監視解決方案**頁面上，輸入**方案名稱**您選擇的選取 hello**區域**toodeploy，再選取 hello Azure訂用帳戶 toowant toouse。</span><span class="sxs-lookup"><span data-stu-id="f129d-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="f129d-122">按一下 [建立解決方案] 。</span><span class="sxs-lookup"><span data-stu-id="f129d-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="f129d-123">等待直到 hello 佈建程序完成。</span><span class="sxs-lookup"><span data-stu-id="f129d-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="f129d-124">預先設定的 hello 解決方案會使用可計費的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="f129d-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="f129d-125">請務必 tooremove hello 預先設定的方案，從您的訂用帳戶，當您在與其 tooavoid 任何不必要的費用。</span><span class="sxs-lookup"><span data-stu-id="f129d-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="f129d-126">您可以完整移除預先設定的方案從您的訂用帳戶瀏覽 hello <https://www.azureiotsuite.com/>頁面。</span><span class="sxs-lookup"><span data-stu-id="f129d-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="f129d-127">Hello 佈建 hello 遠端監視解決方案的程序完成時，請按一下**啟動**tooopen hello 方案儀表板在您的瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="f129d-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![解決方案儀表板][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="f129d-129">佈建您的裝置 hello 遠端監視解決方案中</span><span class="sxs-lookup"><span data-stu-id="f129d-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="f129d-130">如果您已經在解決方案中佈建裝置，則可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="f129d-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="f129d-131">當您建立 hello 用戶端應用程式時，您會需要 tooknow hello 裝置認證。</span><span class="sxs-lookup"><span data-stu-id="f129d-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="f129d-132">提供裝置 tooconnect toohello 預先設定的解決方案，它必須將自己識別 tooIoT 集線器使用有效的認證。</span><span class="sxs-lookup"><span data-stu-id="f129d-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="f129d-133">您可以擷取 hello 裝置認證從 hello 方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="f129d-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="f129d-134">您稍後在本教學課程中，用戶端應用程式包含 hello 裝置認證。</span><span class="sxs-lookup"><span data-stu-id="f129d-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="f129d-135">tooadd 裝置 tooyour 遠端監視解決方案，下列的完整 hello hello 方案儀表板中的步驟：</span><span class="sxs-lookup"><span data-stu-id="f129d-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="f129d-136">在 hello 左下角的 hello 儀表板，按一下 **新增裝置**。</span><span class="sxs-lookup"><span data-stu-id="f129d-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![新增裝置][1]
2. <span data-ttu-id="f129d-138">在 hello**自訂裝置** 面板中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="f129d-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![新增自訂裝置][2]
3. <span data-ttu-id="f129d-140">選擇 [讓我定義自己的裝置識別碼]。</span><span class="sxs-lookup"><span data-stu-id="f129d-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="f129d-141">輸入裝置識別碼，例如**mydevice**，按一下 **檢查識別碼**tooverify 還未在使用中，該名稱，然後按一下**建立**tooprovision hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="f129d-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![新增裝置識別碼][3]
4. <span data-ttu-id="f129d-143">請注意 hello 裝置認證 （裝置識別碼、 IoT 中樞的主機名稱、 和裝置金鑰）。</span><span class="sxs-lookup"><span data-stu-id="f129d-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="f129d-144">用戶端應用程式需要這些值 tooconnect toohello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="f129d-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="f129d-145">然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="f129d-145">Then click **Done**.</span></span>
   
    ![檢視裝置認證][4]
5. <span data-ttu-id="f129d-147">Hello hello 方案儀表板中的裝置清單中選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="f129d-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="f129d-148">然後，在 hello**裝置詳細資料**] 面板中，按一下 [**啟用裝置**。</span><span class="sxs-lookup"><span data-stu-id="f129d-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="f129d-149">您的裝置 hello 狀態現在是**執行**。</span><span class="sxs-lookup"><span data-stu-id="f129d-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="f129d-150">hello 遠端監視解決方案現在可以從您的裝置接收遙測，並叫用 hello 裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="f129d-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="f129d-151">建置並執行 hello C 範例方案</span><span class="sxs-lookup"><span data-stu-id="f129d-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="f129d-152">hello 下列指示描述連接 hello 步驟[mbed 啟用 Freescale FRDM K64F] [ lnk-mbed-home]裝置 toohello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="f129d-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="f129d-153">Hello mbed 裝置 tooyour 網路和桌面的電腦連接</span><span class="sxs-lookup"><span data-stu-id="f129d-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="f129d-154">Hello mbed 裝置 tooyour 網路使用乙太網路纜線連線。</span><span class="sxs-lookup"><span data-stu-id="f129d-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="f129d-155">這個步驟是必要的因為 hello 範例應用程式需要網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="f129d-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="f129d-156">請參閱[入門 mbed] [ lnk-mbed-getstarted] tooconnect mbed 裝置 tooyour 桌面電腦。</span><span class="sxs-lookup"><span data-stu-id="f129d-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="f129d-157">如果您桌面的電腦執行 Windows，請參閱[PC 組態][ lnk-mbed-pcconnect] tooconfigure 序列連接埠存取 tooyour mbed 裝置。</span><span class="sxs-lookup"><span data-stu-id="f129d-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="f129d-158">建立 mbed 專案並匯入 hello 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="f129d-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="f129d-159">請遵循這些步驟 tooadd 某些範例程式碼 tooan mbed 專案。</span><span class="sxs-lookup"><span data-stu-id="f129d-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="f129d-160">您匯入 hello 遠端監視入門專案，然後變更 hello 專案 toouse hello MQTT 通訊協定，而不是 hello AMQP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="f129d-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="f129d-161">目前，您需要 toouse hello MQTT 通訊協定 toouse hello 裝置管理功能的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f129d-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="f129d-162">在 網頁瀏覽器，移 toohello mbed.org[開發人員網站](https://developer.mbed.org/)。</span><span class="sxs-lookup"><span data-stu-id="f129d-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="f129d-163">如果您尚未註冊，您會看到選項 toocreate （它是免費） 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f129d-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="f129d-164">否則，請使用您的帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="f129d-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="f129d-165">然後按一下 **編譯器**hello 右上角的 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="f129d-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="f129d-166">此動作可讓您 toohello*工作區*介面。</span><span class="sxs-lookup"><span data-stu-id="f129d-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="f129d-167">請確定 hello 您所使用的硬體平台會出現在 hello 右上角的 [hello] 視窗中，或按一下 hello 圖示 hello 右下角 tooselect 在您的硬體平台。</span><span class="sxs-lookup"><span data-stu-id="f129d-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="f129d-168">按一下**匯入**hello 主功能表上。</span><span class="sxs-lookup"><span data-stu-id="f129d-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="f129d-169">然後按一下 **按這裡從 URL tooimport**。</span><span class="sxs-lookup"><span data-stu-id="f129d-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![啟動匯入 toombed 工作區][6]

1. <span data-ttu-id="f129d-171">在 hello 快顯視窗中，輸入 hello 範例程式碼 https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ hello 連結，然後按一下 **匯入**。</span><span class="sxs-lookup"><span data-stu-id="f129d-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![匯入範例程式碼 toombed 工作區][7]

1. <span data-ttu-id="f129d-173">您可以在 hello mbed 編譯器視窗中看到，匯入這個專案也會匯入的各種程式庫。</span><span class="sxs-lookup"><span data-stu-id="f129d-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="f129d-174">部分提供且由 hello Azure IoT 團隊負責維護 ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/)， [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/)， [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/)， [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/))，而其他則 hello mbed 媒體櫃類別目錄中所適用的協力廠商程式庫。</span><span class="sxs-lookup"><span data-stu-id="f129d-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![檢視 mbed 專案][8]

1. <span data-ttu-id="f129d-176">在 hello**程式工作區**，以滑鼠右鍵按一下 hello **iot 中樞\_amqp\_傳輸**程式庫，按一下**刪除**，然後按一下 **確定**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="f129d-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="f129d-177">在 hello**程式工作區**，以滑鼠右鍵按一下 hello **azure\_amqp\_c**程式庫，按一下 **刪除**，然後按一下 **確定** tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="f129d-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="f129d-178">以滑鼠右鍵按一下 hello **remote_monitoring** hello 中的專案**程式工作區**，選取**匯入程式庫**，然後選取**From URL**。</span><span class="sxs-lookup"><span data-stu-id="f129d-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![啟動程式庫匯入 toombed 工作區][6]

1. <span data-ttu-id="f129d-180">在 hello 快顯視窗中，輸入 hello MQTT 傳輸程式庫 https://developer.mbed.org/users/AzureIoTClient/code/iothub hello 連結\_mqtt\_傳輸 / 然後按一下 **匯入**。</span><span class="sxs-lookup"><span data-stu-id="f129d-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![匯入程式庫 toombed 工作區][12]

1. <span data-ttu-id="f129d-182">Hello 重複上一個步驟 tooadd hello MQTT 從程式庫 https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /。</span><span class="sxs-lookup"><span data-stu-id="f129d-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="f129d-183">您的工作區現在看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="f129d-183">Your workspace now looks like hello following:</span></span>

    ![檢視 mbed 工作區][13]

1. <span data-ttu-id="f129d-185">遠端開啟 hello\_monitoring\remote_monitoring.c 檔案和取代現有的 hello`#include`陳述式，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="f129d-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="f129d-186">刪除所有剩餘 hello 遠端中的程式碼的 hello\_monitoring\remote\_monitoring.c 檔案。</span><span class="sxs-lookup"><span data-stu-id="f129d-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="f129d-187">建置並執行 hello 範例</span><span class="sxs-lookup"><span data-stu-id="f129d-187">Build and run hello sample</span></span>

<span data-ttu-id="f129d-188">新增程式碼 tooinvoke hello**遠端\_監視\_執行**函式，然後建置並執行 hello 裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="f129d-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="f129d-189">新增**主要**函式與下列程式碼結尾 hello hello 遠端\_monitoring.c 檔案 tooinvoke hello**遠端\_監視\_執行**函式：</span><span class="sxs-lookup"><span data-stu-id="f129d-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="f129d-190">按一下**編譯**toobuild hello 程式。</span><span class="sxs-lookup"><span data-stu-id="f129d-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="f129d-191">您可以安全地忽略任何警告，，但如果 hello 建置會產生錯誤，修正後再繼續。</span><span class="sxs-lookup"><span data-stu-id="f129d-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="f129d-192">如果 hello 建置成功，hello mbed 編譯器網站會產生 hello 專案名稱的.bin 檔案，並會下載 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="f129d-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="f129d-193">複製 hello.bin 檔案 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="f129d-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="f129d-194">儲存 hello.bin 檔案 toohello 裝置會導致 hello 裝置 toorestart 並執行 hello.bin 檔案中包含的 hello 程式。</span><span class="sxs-lookup"><span data-stu-id="f129d-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="f129d-195">您可以手動重新啟動 hello 程式隨時按下上 hello mbed 裝置 hello 重設按鈕。</span><span class="sxs-lookup"><span data-stu-id="f129d-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="f129d-196">使用 SSH 用戶端應用程式，例如 PuTTY toohello 裝置連線。</span><span class="sxs-lookup"><span data-stu-id="f129d-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="f129d-197">您可以判斷您的裝置會使用透過檢查 Windows 裝置管理員中的 hello 序列連接埠。</span><span class="sxs-lookup"><span data-stu-id="f129d-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="f129d-198">在 PuTTY，按一下 hello**序列**連接類型。</span><span class="sxs-lookup"><span data-stu-id="f129d-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="f129d-199">hello 裝置通常會 9600 傳輸連接中，因此輸入 hello 9600**速度**方塊。</span><span class="sxs-lookup"><span data-stu-id="f129d-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="f129d-200">然後按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="f129d-200">Then click **Open**.</span></span>

1. <span data-ttu-id="f129d-201">hello 程式開始執行。</span><span class="sxs-lookup"><span data-stu-id="f129d-201">hello program starts executing.</span></span> <span data-ttu-id="f129d-202">如果 hello 程式沒有自動啟動您的連接時，可能會發生 tooreset hello 面板 （按 CTRL + Break 或按 hello 面板的 [重設] 按鈕）。</span><span class="sxs-lookup"><span data-stu-id="f129d-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
