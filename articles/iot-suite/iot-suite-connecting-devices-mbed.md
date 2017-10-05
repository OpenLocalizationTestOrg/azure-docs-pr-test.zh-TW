---
title: "在 mbed 上使用 C 連接裝置 | Microsoft Docs"
description: "描述如何在 mbed 上使用已寫入 C 的應用程式，將裝置連接至 Azure IoT Suite 預先設定遠端監視方案。"
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
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="877f0-103">將裝置連接至遠端監視預先設定方案 (mbed)</span><span class="sxs-lookup"><span data-stu-id="877f0-103">Connect your device to the remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="877f0-104">案例概觀</span><span class="sxs-lookup"><span data-stu-id="877f0-104">Scenario overview</span></span>
<span data-ttu-id="877f0-105">在此案例中，您會建立一個裝置，此裝置會將下列遙測資料傳送給遠端監視[預先設定解決方案][lnk-what-are-preconfig-solutions]：</span><span class="sxs-lookup"><span data-stu-id="877f0-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="877f0-106">外部溫度</span><span class="sxs-lookup"><span data-stu-id="877f0-106">External temperature</span></span>
* <span data-ttu-id="877f0-107">內部溫度</span><span class="sxs-lookup"><span data-stu-id="877f0-107">Internal temperature</span></span>
* <span data-ttu-id="877f0-108">溼度</span><span class="sxs-lookup"><span data-stu-id="877f0-108">Humidity</span></span>

<span data-ttu-id="877f0-109">為了簡化起見，在裝置上的程式碼會產生範例值，但我們鼓勵您將實際的感應器連接到您的裝置並傳送實際的遙測資料來擴充此範例。</span><span class="sxs-lookup"><span data-stu-id="877f0-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="877f0-110">此裝置同時也能夠回應從解決方案儀表板叫用的方法，以及回應解決方案儀表板中設定的所需屬性值。</span><span class="sxs-lookup"><span data-stu-id="877f0-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="877f0-111">若要完成此教學課程，您需要一個有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="877f0-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="877f0-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="877f0-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="877f0-113">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="877f0-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="877f0-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="877f0-114">Before you start</span></span>
<span data-ttu-id="877f0-115">在您為裝置撰寫任何程式碼之前，您必須先佈建遠端監視預先設定解決方案，並在該解決方案中佈建新的自訂裝置。</span><span class="sxs-lookup"><span data-stu-id="877f0-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="877f0-116">佈建遠端監視預先設定解決方案</span><span class="sxs-lookup"><span data-stu-id="877f0-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="877f0-117">您在本教學課程中建立的裝置會將資料傳送給[遠端監視][lnk-remote-monitoring]預先設定解決方案的執行個體。</span><span class="sxs-lookup"><span data-stu-id="877f0-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="877f0-118">如果您尚未在您的 Azure 帳戶中佈建遠端監視預先設定解決方案，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="877f0-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="877f0-119">在 <https://www.azureiotsuite.com/> 頁面上，按一下 [**+**] 以建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="877f0-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="877f0-120">按一下 [遠端監視] 面板上的 [選取]，以建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="877f0-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="877f0-121">在 [建立遠端監視解決方案] 頁面上，輸入 您選擇的 [解決方案名稱]，選取您要部署的 [區域]，並選取想要使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="877f0-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="877f0-122">按一下 [建立解決方案] 。</span><span class="sxs-lookup"><span data-stu-id="877f0-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="877f0-123">等候佈建程序完成。</span><span class="sxs-lookup"><span data-stu-id="877f0-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="877f0-124">預先設定的解決方案使用可計費的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="877f0-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="877f0-125">當您使用完預先設定的解決方案之後，請務必將它從您的訂用帳戶中移除，以避免任何不必要的費用。</span><span class="sxs-lookup"><span data-stu-id="877f0-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="877f0-126">您可以從訂用帳戶中完全移除預先設定的解決方案，請至 <https://www.azureiotsuite.com/> 頁面進行此操作。</span><span class="sxs-lookup"><span data-stu-id="877f0-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="877f0-127">當遠端監視解決方案的佈建程序完成之後，請按一下 [啟動]  ，以在瀏覽器中開啟解決方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="877f0-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![解決方案儀表板][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="877f0-129">在遠端監視方案中佈建您的裝置</span><span class="sxs-lookup"><span data-stu-id="877f0-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="877f0-130">如果您已經在解決方案中佈建裝置，則可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="877f0-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="877f0-131">建立用戶端應用程式時，您需要知道裝置認證。</span><span class="sxs-lookup"><span data-stu-id="877f0-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="877f0-132">對於連線到預先設定解決方案的裝置，該裝置必須使用有效的認證向 IoT 中樞識別自己。</span><span class="sxs-lookup"><span data-stu-id="877f0-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="877f0-133">您會從解決方案儀表板收到裝置認證。</span><span class="sxs-lookup"><span data-stu-id="877f0-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="877f0-134">稍後在本教學課程中，您會將您的裝置認證包含在您的用戶端應用程式中。</span><span class="sxs-lookup"><span data-stu-id="877f0-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="877f0-135">若要在您的遠端監視解決方案中新增裝置，請在解決方案儀表板中完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="877f0-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="877f0-136">在儀表板左下角，按一下 [新增裝置] 。</span><span class="sxs-lookup"><span data-stu-id="877f0-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![新增裝置][1]
2. <span data-ttu-id="877f0-138">在 [自訂裝置] 面板中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="877f0-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![新增自訂裝置][2]
3. <span data-ttu-id="877f0-140">選擇 [讓我定義自己的裝置識別碼]。</span><span class="sxs-lookup"><span data-stu-id="877f0-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="877f0-141">輸入裝置識別碼 (例如 **mydevice**)，按一下 [檢查 ID] 以確認沒有其他裝置使用該名稱，然後按一下 [建立] 來佈建裝置。</span><span class="sxs-lookup"><span data-stu-id="877f0-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![新增裝置識別碼][3]
4. <span data-ttu-id="877f0-143">記下裝置認證 (裝置識別碼、IoT 中樞主機名稱及裝置金鑰)。</span><span class="sxs-lookup"><span data-stu-id="877f0-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="877f0-144">用戶端應用程式需要這些值，才能連接到遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="877f0-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="877f0-145">然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="877f0-145">Then click **Done**.</span></span>
   
    ![檢視裝置認證][4]
5. <span data-ttu-id="877f0-147">從解決方案儀表板的裝置清單中選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="877f0-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="877f0-148">然後，在 [裝置詳細資料] 面板中，按一下 [啟用裝置]。</span><span class="sxs-lookup"><span data-stu-id="877f0-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="877f0-149">裝置的狀態現在會是 [正在執行]。</span><span class="sxs-lookup"><span data-stu-id="877f0-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="877f0-150">遠端監視解決方案現在已可從您的裝置接收遙測資料，並在該裝置上叫用方法。</span><span class="sxs-lookup"><span data-stu-id="877f0-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a><span data-ttu-id="877f0-151">建置並執行 C 範例方案</span><span class="sxs-lookup"><span data-stu-id="877f0-151">Build and run the C sample solution</span></span>

<span data-ttu-id="877f0-152">下列指示描述將[啟用 mbed 的 Freescale FRDM-K64F][lnk-mbed-home] 裝置連接至遠端監視解決方案的步驟。</span><span class="sxs-lookup"><span data-stu-id="877f0-152">The following instructions describe the steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device to the remote monitoring solution.</span></span>

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a><span data-ttu-id="877f0-153">將 mbed 裝置連接到網路和桌上型電腦</span><span class="sxs-lookup"><span data-stu-id="877f0-153">Connect the mbed device to your network and desktop machine</span></span>

1. <span data-ttu-id="877f0-154">使用乙太網路纜線將 mbed 裝置連接到您的網路。</span><span class="sxs-lookup"><span data-stu-id="877f0-154">Connect the mbed device to your network using an Ethernet cable.</span></span> <span data-ttu-id="877f0-155">這是必要的步驟，因為範例應用程式需要透過網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="877f0-155">This step is necessary because the sample application requires internet access.</span></span>

1. <span data-ttu-id="877f0-156">請參閱 [mbed 使用者入門][lnk-mbed-getstarted]來將您的 mbed 裝置連接至桌上型電腦。</span><span class="sxs-lookup"><span data-stu-id="877f0-156">See [Getting Started with mbed][lnk-mbed-getstarted] to connect your mbed device to your desktop PC.</span></span>

1. <span data-ttu-id="877f0-157">如果桌上型電腦執行的是 Windows，請參閱 [PC 組態][lnk-mbed-pcconnect]以設定對您 mbed 裝置的序列埠存取。</span><span class="sxs-lookup"><span data-stu-id="877f0-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] to configure serial port access to your mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-the-sample-code"></a><span data-ttu-id="877f0-158">建立 mbed 專案並匯入範例程式碼</span><span class="sxs-lookup"><span data-stu-id="877f0-158">Create an mbed project and import the sample code</span></span>

<span data-ttu-id="877f0-159">依照下列步驟將一些範例程式碼新增至 mbed 專案。</span><span class="sxs-lookup"><span data-stu-id="877f0-159">Follow these steps to add some sample code to an mbed project.</span></span> <span data-ttu-id="877f0-160">匯入遠端監視入門專案，然後將專案變更為使用 MQTT 通訊協定 (而非 AMQP 通訊協定)。</span><span class="sxs-lookup"><span data-stu-id="877f0-160">You import the remote monitoring starter project and then change the project to use the MQTT protocol instead of the AMQP protocol.</span></span> <span data-ttu-id="877f0-161">目前，您必須使用 MQTT 通訊協定，才能使用 IoT 中樞的裝置管理功能。</span><span class="sxs-lookup"><span data-stu-id="877f0-161">Currently, you need to use the MQTT protocol to use the device management features of IoT Hub.</span></span>

1. <span data-ttu-id="877f0-162">在您的 Web 瀏覽器中，移至 mbed.org [開發人員網站](https://developer.mbed.org/)。</span><span class="sxs-lookup"><span data-stu-id="877f0-162">In your web browser, go to the mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="877f0-163">如果您還沒有註冊，您會看到建立帳戶的選項 (它是免費的)。</span><span class="sxs-lookup"><span data-stu-id="877f0-163">If you haven't signed up, you see an option to create an account (it's free).</span></span> <span data-ttu-id="877f0-164">否則，請使用您的帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="877f0-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="877f0-165">然後按一下頁面右上角的 [編譯器]  。</span><span class="sxs-lookup"><span data-stu-id="877f0-165">Then click **Compiler** in the upper right-hand corner of the page.</span></span> <span data-ttu-id="877f0-166">這項動作會將您帶往 [工作區] 介面。</span><span class="sxs-lookup"><span data-stu-id="877f0-166">This action brings you to the *Workspace* interface.</span></span>

1. <span data-ttu-id="877f0-167">請確定您使用的硬體平台出現在視窗的右上角，或按一下右手邊的圖示來選取您的硬體平台。</span><span class="sxs-lookup"><span data-stu-id="877f0-167">Make sure the hardware platform you're using appears in the upper right-hand corner of the window, or click the icon in the right-hand corner to select your hardware platform.</span></span>

1. <span data-ttu-id="877f0-168">在主功能表上按一下 [匯入]  。</span><span class="sxs-lookup"><span data-stu-id="877f0-168">Click **Import** on the main menu.</span></span> <span data-ttu-id="877f0-169">然後按一下 [按一下這裡從 URL 匯入]。</span><span class="sxs-lookup"><span data-stu-id="877f0-169">Then click **Click here to import from URL**.</span></span>
   
    ![開始匯入至 mbed 工作區][6]

1. <span data-ttu-id="877f0-171">在快顯視窗中，輸入範例程式碼 https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ 連結，然後按一下 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="877f0-171">In the pop-up window, enter the link for the sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![將程式碼範例匯入至 mbed 工作區][7]

1. <span data-ttu-id="877f0-173">您可以看到匯入此專案的 mbed 編譯器視窗也匯入各種程式庫。</span><span class="sxs-lookup"><span data-stu-id="877f0-173">You can see in the mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="877f0-174">有些是由 Azure IoT 小組提供和維護 ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/)、[iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/)、[iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/)、[azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/))，其他則是可以在 mbed 程式庫目錄中取得的協力廠商程式庫。</span><span class="sxs-lookup"><span data-stu-id="877f0-174">Some are provided and maintained by the Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in the mbed libraries catalog.</span></span>
   
    ![檢視 mbed 專案][8]

1. <span data-ttu-id="877f0-176">在 [程式工作區] 中，以滑鼠右鍵按一下 **iothub\_amqp\_transport** 程式庫，按一下 [刪除]，然後按一下 [確定] 進行確認。</span><span class="sxs-lookup"><span data-stu-id="877f0-176">In the **Program Workspace**, right-click the **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="877f0-177">在 [程式工作區] 中，以滑鼠右鍵按一下 **azure\_amqp\_c** 程式庫，按一下 [刪除]，然後按一下 [確定] 進行確認。</span><span class="sxs-lookup"><span data-stu-id="877f0-177">In the **Program Workspace**, right-click the **azure\_amqp\_c** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="877f0-178">以滑鼠右鍵按一下 [程式工作區] 中的 **remote_monitoring** 專案，選取 [匯入程式庫]，然後選取 [從 URL]。</span><span class="sxs-lookup"><span data-stu-id="877f0-178">Right-click the **remote_monitoring** project in the **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![開始將程式庫匯入至 mbed 工作區][6]

1. <span data-ttu-id="877f0-180">在快顯視窗中，輸入 MQTT 傳輸程式庫 https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ 連結，然後按一下 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="877f0-180">In the pop-up window, enter the link for the MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![將程式庫匯入至 mbed 工作區][12]

1. <span data-ttu-id="877f0-182">重複上述步驟以從 https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/ 新增 MQTT 程式庫。</span><span class="sxs-lookup"><span data-stu-id="877f0-182">Repeat the previous step to add the MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="877f0-183">您的工作區現在如下所示：</span><span class="sxs-lookup"><span data-stu-id="877f0-183">Your workspace now looks like the following:</span></span>

    ![檢視 mbed 工作區][13]

1. <span data-ttu-id="877f0-185">開啟 remote\_monitoring\remote_monitoring.c 檔案，並以下列程式碼取代現有的 `#include` 陳述字：</span><span class="sxs-lookup"><span data-stu-id="877f0-185">Open the remote\_monitoring\remote_monitoring.c file and replace the existing `#include` statements with the following code:</span></span>

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
1. <span data-ttu-id="877f0-186">刪除 remote\_monitoring\remote\_monitoring.c 檔案中的所有其餘程式碼。</span><span class="sxs-lookup"><span data-stu-id="877f0-186">Delete all the remaining code in the remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="877f0-187">建置並執行範例</span><span class="sxs-lookup"><span data-stu-id="877f0-187">Build and run the sample</span></span>

<span data-ttu-id="877f0-188">新增程式碼來叫用 **remote\_monitoring\_run** 函式，然後建置並執行裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="877f0-188">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="877f0-189">以位於 remote\_monitoring.c 檔案結尾的下列程式碼新增 **main** 函式，以叫用 **remote\_monitoring\_run** 函式︰</span><span class="sxs-lookup"><span data-stu-id="877f0-189">Add a **main** function with following code at the end of the remote\_monitoring.c file to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="877f0-190">按一下 [編譯]  來建置程式。</span><span class="sxs-lookup"><span data-stu-id="877f0-190">Click **Compile** to build the program.</span></span> <span data-ttu-id="877f0-191">您可以安全地略過任何警告，但如果建置產生錯誤，請修正錯誤後再繼續。</span><span class="sxs-lookup"><span data-stu-id="877f0-191">You can safely ignore any warnings, but if the build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="877f0-192">如果建置成功，mbed 編譯器網站會產生含有您專案名稱的 .bin 檔案，並將它下載到您的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="877f0-192">If the build is successful, the mbed compiler website generates a .bin file with the name of your project and downloads it to your local machine.</span></span> <span data-ttu-id="877f0-193">將 .bin 檔案複製到裝置。</span><span class="sxs-lookup"><span data-stu-id="877f0-193">Copy the .bin file to the device.</span></span> <span data-ttu-id="877f0-194">如果將 .bin 檔案儲存到裝置，將會導致裝置重新啟動並執行包含在 .bin 檔案中的程式。</span><span class="sxs-lookup"><span data-stu-id="877f0-194">Saving the .bin file to the device causes the device to restart and run the program contained in the .bin file.</span></span> <span data-ttu-id="877f0-195">您可以按 mbed 裝置上的 [重設] 按鈕來隨時手動重新啟動程式。</span><span class="sxs-lookup"><span data-stu-id="877f0-195">You can manually restart the program at any time by pressing the reset button on the mbed device.</span></span>

1. <span data-ttu-id="877f0-196">使用 SSH 用戶端應用程式 (例如 PuTTY) 連接至裝置。</span><span class="sxs-lookup"><span data-stu-id="877f0-196">Connect to the device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="877f0-197">您可以查看 [Windows 裝置管理員] 來確定裝置使用的序列埠。</span><span class="sxs-lookup"><span data-stu-id="877f0-197">You can determine the serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="877f0-198">在 PuTTY 中，按一下 [序列]  連接類型。</span><span class="sxs-lookup"><span data-stu-id="877f0-198">In PuTTY, click the **Serial** connection type.</span></span> <span data-ttu-id="877f0-199">裝置通常的連線傳輸速率是 9600，因此請在 [速度]  方塊中輸入 9600。</span><span class="sxs-lookup"><span data-stu-id="877f0-199">The device typically connects at 9600 baud, so enter 9600 in the **Speed** box.</span></span> <span data-ttu-id="877f0-200">然後按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="877f0-200">Then click **Open**.</span></span>

1. <span data-ttu-id="877f0-201">程式開始執行。</span><span class="sxs-lookup"><span data-stu-id="877f0-201">The program starts executing.</span></span> <span data-ttu-id="877f0-202">連接時如果程式沒有自動啟動，您可能必須重設面板 (按 CTRL + Break 或按面板的重設按鈕)。</span><span class="sxs-lookup"><span data-stu-id="877f0-202">You may have to reset the board (press CTRL+Break or press the board's reset button) if the program does not start automatically when you connect.</span></span>
   
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
