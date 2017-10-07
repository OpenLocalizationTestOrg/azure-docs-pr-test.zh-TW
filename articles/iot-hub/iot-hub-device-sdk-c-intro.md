---
title: "C 的 aaaThe Azure IoT 裝置 SDK |Microsoft 文件"
description: "開始使用 hello Azure IoT 裝置 SDK for C，並了解如何 toocreate 裝置應用程式的通訊與 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="7b1df-103">適用於 C 的 Azure IoT 裝置 SDK</span><span class="sxs-lookup"><span data-stu-id="7b1df-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="7b1df-104">hello **Azure IoT 裝置 SDK**是一組程式庫設計 toosimplify hello 的 hello 從傳送訊息 tooand 接收訊息的處理程序**Azure IoT 中樞**服務。</span><span class="sxs-lookup"><span data-stu-id="7b1df-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="7b1df-105">有不同的變化的 hello SDK，每個目標為特定的平台，但此文章說明 hello **C 的 Azure IoT 裝置 SDK**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="7b1df-106">C 的 hello Azure IoT 裝置 SDK 採用 ANSI C (C99) toomaximize 可攜性。</span><span class="sxs-lookup"><span data-stu-id="7b1df-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="7b1df-107">這個功能可以讓 hello 文件庫適合的 toooperate 上多個平台和裝置，特別是在最小化磁碟和記憶體耗用量是優先順序。</span><span class="sxs-lookup"><span data-stu-id="7b1df-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="7b1df-108">有各種平台的 hello SDK 已經過測試，(請參閱 hello [IoT 裝置類別目錄的 Azure 認證](https://catalog.azureiotsuite.com/)如需詳細資訊)。</span><span class="sxs-lookup"><span data-stu-id="7b1df-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="7b1df-109">雖然這篇文章包含 hello Windows 平台上執行的範例程式碼的逐步解說，本文中所述的 hello 程式碼支援的平台的 hello 範圍是一樣。</span><span class="sxs-lookup"><span data-stu-id="7b1df-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="7b1df-110">本文介紹 hello Azure IoT 裝置 SDK 的 toohello 結構 c。它會示範如何 tooinitialize hello 裝置程式庫，傳送資料 tooIoT 中樞，並從其中接收訊息。</span><span class="sxs-lookup"><span data-stu-id="7b1df-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="7b1df-111">本文章中的 hello 資訊應該使用 hello SDK，啟動足夠 tooget，但還提供指標 tooadditional 有關 hello 文件庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="7b1df-112">SDK 架構</span><span class="sxs-lookup"><span data-stu-id="7b1df-112">SDK architecture</span></span>

<span data-ttu-id="7b1df-113">您可以找到 hello [ **C 的 Azure IoT 裝置 SDK** ](https://github.com/Azure/azure-iot-sdk-c) GitHub 儲存機制和檢視詳細資料的 hello API 在 hello [C 應用程式開發介面參考](https://azure.github.io/azure-iot-sdk-c/index.html)。</span><span class="sxs-lookup"><span data-stu-id="7b1df-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="7b1df-114">hello hello 程式庫的最新版本可以在 hello**主要**hello 儲存機制分支：</span><span class="sxs-lookup"><span data-stu-id="7b1df-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="7b1df-115">hello hello SDK 的核心實作處於 hello **iot 中樞\_用戶端**hello 最低 API 層 hello SDK 中的 hello 實作所在的資料夾： hello **IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="7b1df-116">hello **IoTHubClient**程式庫包含應用程式開發介面實作未經處理的訊息，用於傳送訊息 tooIoT 中樞和接收訊息，或從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7b1df-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="7b1df-117">使用此程式庫時，您要負責實作訊息序列化，但與 IoT 中樞通訊的其他細節則是由系統為您處理。</span><span class="sxs-lookup"><span data-stu-id="7b1df-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="7b1df-118">hello**序列化程式**資料夾包含 helper 函式和範例，示範如何 tooserialize 資料之前使用 [tooAzure IoT 中樞傳送 hello 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="7b1df-119">hello 使用 hello 序列化程式不是強制性，並提供為了方便起見。</span><span class="sxs-lookup"><span data-stu-id="7b1df-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="7b1df-120">toouse hello**序列化程式**程式庫，您定義指定 hello 資料 toosend tooIoT 中樞和 hello 訊息預期 tooreceive 從它的模型。</span><span class="sxs-lookup"><span data-stu-id="7b1df-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="7b1df-121">一旦定義 hello 模型之後，hello SDK 提供可讓您的 API 介面 tooeasily 工作與裝置到雲端與雲端到裝置訊息，而不需擔心 hello 序列化詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7b1df-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="7b1df-122">hello 程式庫實作使用 MQTT 和 AMQP 通訊協定傳輸的其他開放原始碼程式庫而定。</span><span class="sxs-lookup"><span data-stu-id="7b1df-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="7b1df-123">hello **IoTHubClient**取決於其他開放原始碼程式庫的程式庫：</span><span class="sxs-lookup"><span data-stu-id="7b1df-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="7b1df-124">hello [Azure C 共用公用程式](https://github.com/Azure/azure-c-shared-utility)程式庫，提供跨數個 Azure 相關 C Sdk 所需的基本工作，例如字串、 清單管理和 IO） 通用的功能。</span><span class="sxs-lookup"><span data-stu-id="7b1df-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="7b1df-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c)程式庫，也就是針對資源限制裝置最佳化的 AMQP 的用戶端實作。</span><span class="sxs-lookup"><span data-stu-id="7b1df-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="7b1df-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c)程式庫，這是一般用途的程式庫實作 hello MQTT 通訊協定，並最佳化資源限制裝置。</span><span class="sxs-lookup"><span data-stu-id="7b1df-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="7b1df-127">使用這些程式庫是更容易 toounderstand 藉由查看範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="7b1df-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="7b1df-128">hello 下列各節將引導您完成數個 hello SDK 中隨附的 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="7b1df-129">本逐步解說應可提供更佳覺得 hello 的 hello SDK 和 Api 運作簡介 toohow hello 架構圖層的各種功能。</span><span class="sxs-lookup"><span data-stu-id="7b1df-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="7b1df-130">在執行之前 hello 範例</span><span class="sxs-lookup"><span data-stu-id="7b1df-130">Before you run hello samples</span></span>

<span data-ttu-id="7b1df-131">您可以在 hello Azure IoT 裝置 SDK 執行 hello 範例 c 之前，您必須[建立 hello IoT 中心服務的執行個體](iot-hub-create-through-portal.md)您 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7b1df-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="7b1df-132">然後完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b1df-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="7b1df-133">準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="7b1df-133">Prepare your development environment</span></span>
* <span data-ttu-id="7b1df-134">取得裝置認證。</span><span class="sxs-lookup"><span data-stu-id="7b1df-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="7b1df-135">準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="7b1df-135">Prepare your development environment</span></span>

<span data-ttu-id="7b1df-136">封裝可供通用平台 （例如 NuGet 適用於 Windows 或 apt_get Debian 和 Ubuntu） 和 hello 範例會使用這些封裝時使用。</span><span class="sxs-lookup"><span data-stu-id="7b1df-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="7b1df-137">在某些情況下，您需要 toocompile hello SDK，或者針對您的裝置。</span><span class="sxs-lookup"><span data-stu-id="7b1df-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="7b1df-138">如果您需要 toocompile hello SDK，請參閱[準備開發環境](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md)hello GitHub 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="7b1df-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="7b1df-139">tooobtain hello 應用程式程式碼範例的 hello SDK 從 GitHub 下載。</span><span class="sxs-lookup"><span data-stu-id="7b1df-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="7b1df-140">收到 hello hello 來源副本**主要**分支 hello [GitHub 儲存機制](https://github.com/Azure/azure-iot-sdk-c)。</span><span class="sxs-lookup"><span data-stu-id="7b1df-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="7b1df-141">取得 hello 裝置認證</span><span class="sxs-lookup"><span data-stu-id="7b1df-141">Obtain hello device credentials</span></span>

<span data-ttu-id="7b1df-142">有 hello 範例原始碼之後下, 一件事 toodo hello 是 tooget 一組裝置認證。</span><span class="sxs-lookup"><span data-stu-id="7b1df-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="7b1df-143">如裝置 toobe 無法 tooaccess IoT 中樞，您必須先新增 hello 裝置 toohello IoT 中樞身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="7b1df-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="7b1df-144">當您新增裝置時，您會取得一組裝置認證所需的 hello 裝置 toobe 無法 tooconnect toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7b1df-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="7b1df-145">hello hello 下節中討論的範例應用程式預期這些認證中的 hello 表單**裝置連接字串**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="7b1df-146">有數個開放原始碼工具 toohelp 管理您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7b1df-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="7b1df-147">稱為[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)的 Windows 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="7b1df-148">稱為 [iothub-explorer](https://github.com/azure/iothub-explorer) 的跨平台 node.js CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="7b1df-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="7b1df-149">本教學課程使用圖形化的 hello*裝置總管*工具。</span><span class="sxs-lookup"><span data-stu-id="7b1df-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="7b1df-150">您也可以使用 hello *iot 中樞總管*工具，如果您偏好 toouse CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="7b1df-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="7b1df-151">hello 裝置總管] 工具會使用 hello Azure IoT 服務程式庫 tooperform 各種函式在 IoT 中樞內，包括新增裝置。</span><span class="sxs-lookup"><span data-stu-id="7b1df-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="7b1df-152">如果您使用 hello 裝置總管工具 tooadd 裝置時，您會取得連接字串為您的裝置。</span><span class="sxs-lookup"><span data-stu-id="7b1df-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="7b1df-153">您需要此連接字串 toorun hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="7b1df-154">如果您不熟悉 hello 裝置總管工具，hello 遵循程序描述如何 toouse 它 tooadd 裝置，並取得裝置的連接字串。</span><span class="sxs-lookup"><span data-stu-id="7b1df-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="7b1df-155">tooinstall hello 裝置總管工具，請參閱[toouse 如何 IoT 中樞裝置 hello 裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)。</span><span class="sxs-lookup"><span data-stu-id="7b1df-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="7b1df-156">當您執行 hello 程式時，您會看到此介面：</span><span class="sxs-lookup"><span data-stu-id="7b1df-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="7b1df-157">輸入您**IoT 中樞連接字串**hello 中第一次欄位，然後按一下**更新**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="7b1df-158">此步驟中設定 hello 工具，讓它可以與 IoT 中樞通訊。</span><span class="sxs-lookup"><span data-stu-id="7b1df-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="7b1df-159">Hello IoT 中樞連接字串設定時，按一下 hello**管理**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="7b1df-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="7b1df-160">此索引標籤可讓您管理 hello 在 IoT 中樞註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="7b1df-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="7b1df-161">建立裝置即可 hello**建立**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b1df-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="7b1df-162">將會顯示一個已預先填入一組金鑰 (主要和次要) 的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7b1df-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="7b1df-163">輸入 [裝置識別碼]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="7b1df-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="7b1df-164">建立 hello 裝置時，hello 裝置會列出所有的 hello 註冊裝置，包括您剛剛建立的 hello 與更新。</span><span class="sxs-lookup"><span data-stu-id="7b1df-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="7b1df-165">如果您在新裝置上按一下滑鼠右鍵，您會看到此功能表︰</span><span class="sxs-lookup"><span data-stu-id="7b1df-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="7b1df-166">如果您選擇**複製所選裝置的連線字串**，hello 裝置連接字串是複製的 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="7b1df-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="7b1df-167">Hello 裝置連接字串的副本。</span><span class="sxs-lookup"><span data-stu-id="7b1df-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="7b1df-168">您需要執行 hello hello 下列各節中所述的範例應用程式時。</span><span class="sxs-lookup"><span data-stu-id="7b1df-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="7b1df-169">當您完成上述 hello 步驟後時，您準備好 toostart 執行一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="7b1df-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="7b1df-170">這兩個範例有常數的頂端 hello hello 主要原始程式檔，可讓您 tooenter 連接字串。</span><span class="sxs-lookup"><span data-stu-id="7b1df-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="7b1df-171">例如，hello hello 從對應的行**iot 中樞\_用戶端\_範例\_mqtt**應用程式會出現，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7b1df-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="7b1df-172">使用 hello IoTHubClient 程式庫</span><span class="sxs-lookup"><span data-stu-id="7b1df-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="7b1df-173">Hello 內**iot 中樞\_用戶端**資料夾中 hello [azure iot-sdk c](https://github.com/azure/azure-iot-sdk-c)儲存機制上，有**範例**資料夾包含應用程式呼叫**iot 中樞\_用戶端\_範例\_mqtt**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="7b1df-174">hello Windows 版的 hello **iot 中樞\_用戶端\_範例\_mqtt**應用程式包含下列 Visual Studio 方案的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b1df-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="7b1df-175">如果您開啟這個專案在 Visual Studio 2017，接受 hello 提示 tooretarget hello 專案 toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="7b1df-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="7b1df-176">此解決方案內含單一專案：</span><span class="sxs-lookup"><span data-stu-id="7b1df-176">This solution contains a single project.</span></span> <span data-ttu-id="7b1df-177">此解決方案中安裝了四個 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="7b1df-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="7b1df-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="7b1df-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="7b1df-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="7b1df-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="7b1df-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="7b1df-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="7b1df-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="7b1df-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="7b1df-182">您一律需要 hello **Microsoft.Azure.C.SharedUtility**封裝時您正在使用 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="7b1df-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="7b1df-183">這個範例使用 hello MQTT 通訊協定，因此您必須包含 hello **Microsoft.Azure.umqtt**和**Microsoft.Azure.IoTHub.MqttTransport** （有相同的封裝 AMQP 和 HTTP 的封裝).</span><span class="sxs-lookup"><span data-stu-id="7b1df-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="7b1df-184">由於 hello 範例使用 hello **IoTHubClient**程式庫，您也必須包括 hello **Microsoft.Azure.IoTHub.IoTHubClient**方案中的封裝。</span><span class="sxs-lookup"><span data-stu-id="7b1df-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="7b1df-185">您可以在 hello 找到 hello 範例應用程式的 hello 實作**iot 中樞\_用戶端\_範例\_mqtt.c**原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="7b1df-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="7b1df-186">hello 下列步驟會使用此範例應用程式 toowalk 您透過必要條件 toouse hello **IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="7b1df-187">初始化 hello 程式庫</span><span class="sxs-lookup"><span data-stu-id="7b1df-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="7b1df-188">您開始使用 hello 程式庫之前，您可能需要 tooperform 某些平台專屬的初始化。</span><span class="sxs-lookup"><span data-stu-id="7b1df-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="7b1df-189">例如，如果您計劃 Linux toouse AMQP 必須初始化 hello OpenSSL 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="7b1df-190">hello 範例 hello [GitHub 儲存機制](https://github.com/Azure/azure-iot-sdk-c)呼叫 hello 公用程式函式**平台\_init**當 hello 用戶端開始，並呼叫 hello**平台\_deinit**結束之前的函式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="7b1df-191">這些函式會宣告 hello platform.h 標頭檔中。</span><span class="sxs-lookup"><span data-stu-id="7b1df-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="7b1df-192">檢查 hello 定義這些函式的目標平台在 hello[儲存機制](https://github.com/Azure/azure-iot-sdk-c)toodetermine 是否需要 tooinclude 任何平台專屬的初始化程式碼中您的用戶端。</span><span class="sxs-lookup"><span data-stu-id="7b1df-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="7b1df-193">toostart hello 文件庫中，使用第一次配置 IoT 中樞用戶端控制代碼：</span><span class="sxs-lookup"><span data-stu-id="7b1df-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="7b1df-194">您傳遞您取得 hello 裝置總管工具 toothis 函式的 hello 裝置連接字串的複本。</span><span class="sxs-lookup"><span data-stu-id="7b1df-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="7b1df-195">您也指定 hello 通訊的通訊協定 toouse。</span><span class="sxs-lookup"><span data-stu-id="7b1df-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="7b1df-196">這個範例使用 MQTT，但 AMQP 與 HTTP 也是選項。</span><span class="sxs-lookup"><span data-stu-id="7b1df-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="7b1df-197">當您具有有效**iot 中樞\_用戶端\_處理**，您可以啟動呼叫 hello Api toosend 及接收訊息 tooand 從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7b1df-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="7b1df-198">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="7b1df-198">Send messages</span></span>

<span data-ttu-id="7b1df-199">hello 範例應用程式會設定迴圈 toosend 訊息 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7b1df-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="7b1df-200">下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b1df-200">hello following snippet:</span></span>

- <span data-ttu-id="7b1df-201">建立訊息。</span><span class="sxs-lookup"><span data-stu-id="7b1df-201">Creates a message.</span></span>
- <span data-ttu-id="7b1df-202">新增屬性 toohello 訊息。</span><span class="sxs-lookup"><span data-stu-id="7b1df-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="7b1df-203">傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="7b1df-203">Sends a message.</span></span>

<span data-ttu-id="7b1df-204">首先，建立一則訊息：</span><span class="sxs-lookup"><span data-stu-id="7b1df-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="7b1df-205">每次傳送訊息時，您會指定傳送嗨資料時，會叫用參考 tooa 回呼函式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="7b1df-206">在此範例中，稱為 hello 回呼函式**SendConfirmationCallback**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="7b1df-207">下列程式碼片段的 hello 顯示這個回呼函式：</span><span class="sxs-lookup"><span data-stu-id="7b1df-207">hello following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="7b1df-208">請注意 hello 呼叫 toohello **IoTHubMessage\_終結**函式，當您完成 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="7b1df-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="7b1df-209">此函式會釋出 hello 建立 hello 訊息時配置的資源。</span><span class="sxs-lookup"><span data-stu-id="7b1df-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="7b1df-210">接收訊息</span><span class="sxs-lookup"><span data-stu-id="7b1df-210">Receive messages</span></span>

<span data-ttu-id="7b1df-211">接收訊息是非同步作業。</span><span class="sxs-lookup"><span data-stu-id="7b1df-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="7b1df-212">首先，註冊 hello 回呼 tooinvoke hello 裝置收到訊息時：</span><span class="sxs-lookup"><span data-stu-id="7b1df-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="7b1df-213">您想要的 void 指標 toowhatever hello 最後一個參數。</span><span class="sxs-lookup"><span data-stu-id="7b1df-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="7b1df-214">在 hello 範例中，它會是指標 tooan 整數，但它可能是指標 tooa 更複雜的資料結構。</span><span class="sxs-lookup"><span data-stu-id="7b1df-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="7b1df-215">此參數可讓 hello 回呼函式 toooperate 共用狀態與 hello 呼叫者，此函式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="7b1df-216">Hello 裝置收到訊息時，hello 註冊的回呼函式會叫用。</span><span class="sxs-lookup"><span data-stu-id="7b1df-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="7b1df-217">此回呼函式會擷取︰</span><span class="sxs-lookup"><span data-stu-id="7b1df-217">This callback function retrieves:</span></span>

* <span data-ttu-id="7b1df-218">hello 訊息識別碼，從 hello 訊息的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b1df-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="7b1df-219">hello 訊息內容。</span><span class="sxs-lookup"><span data-stu-id="7b1df-219">hello message content.</span></span>
* <span data-ttu-id="7b1df-220">Hello 訊息的任何自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="7b1df-220">Any custom properties from hello message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="7b1df-221">使用 hello **IoTHubMessage\_GetByteArray**函式 tooretrieve hello 訊息，在此範例中為字串。</span><span class="sxs-lookup"><span data-stu-id="7b1df-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="7b1df-222">取消初始化 hello 程式庫</span><span class="sxs-lookup"><span data-stu-id="7b1df-222">Uninitialize hello library</span></span>

<span data-ttu-id="7b1df-223">當您完成時傳送事件，並接收訊息，您可以解除初始化 hello IoT 程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="7b1df-224">toodo 因此，發出下列函式呼叫的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b1df-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="7b1df-225">此呼叫釋出先前 hello 所配置的 hello 資源**IoTHubClient\_CreateFromConnectionString**函式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="7b1df-226">如您所見，它是簡單 toosend 和接收郵件 hello **IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="7b1df-227">hello 程式庫會處理與 IoT 中樞，包括哪些通訊協定 toouse 通訊的 hello 詳細資料 （hello hello 開發人員的觀點而言，這是簡單的組態選項）。</span><span class="sxs-lookup"><span data-stu-id="7b1df-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="7b1df-228">hello **IoTHubClient**程式庫也提供精確的控制如何 tooserialize hello 資料您的裝置傳送 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7b1df-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="7b1df-229">在某些情況下此層級的控制是一項優點，但在其他實作詳細資料，您不想 toobe 關心。</span><span class="sxs-lookup"><span data-stu-id="7b1df-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="7b1df-230">在 hello 情形下，您可以考慮使用 hello**序列化程式**程式庫 hello 下一節中所述。</span><span class="sxs-lookup"><span data-stu-id="7b1df-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="7b1df-231">使用 hello 序列化程式庫</span><span class="sxs-lookup"><span data-stu-id="7b1df-231">Use hello serializer library</span></span>

<span data-ttu-id="7b1df-232">在概念上 hello**序列化程式**文件庫總結 hello **IoTHubClient** hello SDK 中的程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="7b1df-233">它會使用 hello **IoTHubClient** hello 基礎 IoT 中樞，但它與通訊的文件庫加入 hello 訊息序列化處理負擔移除 hello 開發人員的模型化功能。</span><span class="sxs-lookup"><span data-stu-id="7b1df-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="7b1df-234">此程式庫的運作方式最好是由範例示範。</span><span class="sxs-lookup"><span data-stu-id="7b1df-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="7b1df-235">內部 hello**序列化程式**資料夾中 hello [azure iot-sdk c 儲存機制](https://github.com/Azure/azure-iot-sdk-c)，是**範例**資料夾包含應用程式呼叫**simplesample\_mqtt**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="7b1df-236">此範例的 hello Windows 版本包含下列 Visual Studio 方案的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b1df-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="7b1df-237">如果您開啟這個專案在 Visual Studio 2017，接受 hello 提示 tooretarget hello 專案 toohello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="7b1df-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="7b1df-238">如同 hello 先前範例中，這其中一個包含數個 NuGet 封裝：</span><span class="sxs-lookup"><span data-stu-id="7b1df-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="7b1df-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="7b1df-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="7b1df-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="7b1df-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="7b1df-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="7b1df-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="7b1df-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="7b1df-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="7b1df-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="7b1df-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="7b1df-244">您已看過大部分的這些套件在 hello 前一個範例中，但**Microsoft.Azure.IoTHub.Serializer**新。</span><span class="sxs-lookup"><span data-stu-id="7b1df-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="7b1df-245">此套件時，需要您使用 hello**序列化程式**程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="7b1df-246">您可以在 hello 找到 hello 範例應用程式的 hello 實作**simplesample\_mqtt.c**檔案。</span><span class="sxs-lookup"><span data-stu-id="7b1df-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="7b1df-247">hello 下列各節會逐步引導您 hello 的這個範例的關鍵部分。</span><span class="sxs-lookup"><span data-stu-id="7b1df-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="7b1df-248">初始化 hello 程式庫</span><span class="sxs-lookup"><span data-stu-id="7b1df-248">Initialize hello library</span></span>

<span data-ttu-id="7b1df-249">使用 hello toostart**序列化程式**程式庫，呼叫 hello 初始化應用程式開發介面：</span><span class="sxs-lookup"><span data-stu-id="7b1df-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="7b1df-250">hello 呼叫 toohello**序列化程式\_init**函式是一次性的呼叫，並初始化 hello 基礎程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="7b1df-251">然後，您可以呼叫 hello **IoTHubClient\_LL\_CreateFromConnectionString**函式，是 hello 相同的 API，例如 hello **IoTHubClient**範例。</span><span class="sxs-lookup"><span data-stu-id="7b1df-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="7b1df-252">此呼叫會設定您裝置的連接字串 (這個呼叫也是您在其中選擇 hello 通訊協定想 toouse)。</span><span class="sxs-lookup"><span data-stu-id="7b1df-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="7b1df-253">此範例會使用 MQTT 當做 hello 傳輸，但無法使用 AMQP 或 HTTP。</span><span class="sxs-lookup"><span data-stu-id="7b1df-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="7b1df-254">最後，呼叫 hello**建立\_模型\_執行個體**函式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="7b1df-255">**WeatherStation**是 hello hello 模型命名空間和**ContosoAnemometer** hello hello 模型名稱。</span><span class="sxs-lookup"><span data-stu-id="7b1df-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="7b1df-256">一旦建立 hello 模型執行個體之後，您可以使用它，toostart 傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="7b1df-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="7b1df-257">不過，它是重要 toounderstand 是哪一種模型。</span><span class="sxs-lookup"><span data-stu-id="7b1df-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="7b1df-258">定義 hello 模型</span><span class="sxs-lookup"><span data-stu-id="7b1df-258">Define hello model</span></span>

<span data-ttu-id="7b1df-259">中的 hello**序列化程式**程式庫會定義您的裝置可以傳送 tooIoT 中樞和 hello 訊息，稱為 hello 訊息*動作*中模組化語言，它可以接收的 hello。</span><span class="sxs-lookup"><span data-stu-id="7b1df-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="7b1df-260">定義模型使用一組 C 巨集，例如 hello **simplesample\_mqtt**範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="7b1df-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="7b1df-261">hello**開始\_命名空間**和**結束\_命名空間**巨集這兩個需要 hello 模型做為引數的 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="7b1df-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="7b1df-262">預期這些巨集之間的任何項目是 hello 定義您的模型或模型，與 hello hello 模型使用的資料結構。</span><span class="sxs-lookup"><span data-stu-id="7b1df-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="7b1df-263">在此範例中，有一個名為 **ContosoAnemometer**的模型。</span><span class="sxs-lookup"><span data-stu-id="7b1df-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="7b1df-264">此模型會定義您的裝置可以傳送 tooIoT 中樞的資料之兩個部分： **DeviceId**和**WindSpeed**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="7b1df-265">它也定義您裝置可接收的三個動作 (訊息)：**TurnFanOn**、**TurnFanOff** 及 **SetAirResistance**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="7b1df-266">每個資料元素都有類型，而每個動作都有名稱 (以及一組選擇性的參數)。</span><span class="sxs-lookup"><span data-stu-id="7b1df-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="7b1df-267">hello 資料和 hello 模型中定義的動作定義的 API 介面，您可以使用 toosend 訊息 tooIoT 中樞，並回應傳送 toomessages toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="7b1df-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="7b1df-268">透過範例最能了解如何使用此模型。</span><span class="sxs-lookup"><span data-stu-id="7b1df-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="7b1df-269">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="7b1df-269">Send messages</span></span>

<span data-ttu-id="7b1df-270">hello 模型會定義您可以傳送 tooIoT 中樞的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7b1df-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="7b1df-271">在此範例中，這表示一個 hello 使用 hello 定義的兩個資料項目**WITH_DATA**巨集。</span><span class="sxs-lookup"><span data-stu-id="7b1df-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="7b1df-272">有幾個步驟需要的 toosend **DeviceId**和**WindSpeed**值 tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7b1df-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="7b1df-273">hello 第一個是您想要 toosend tooset hello 資料：</span><span class="sxs-lookup"><span data-stu-id="7b1df-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="7b1df-274">hello 先前定義的模型可讓您 tooset hello 值所設定的成員**結構**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="7b1df-275">接下來，序列化想 toosend hello 訊息：</span><span class="sxs-lookup"><span data-stu-id="7b1df-275">Next, serialize hello message you want toosend:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="7b1df-276">此程式碼序列化 hello 裝置到雲端 tooa 緩衝區 (所參考**目的地**)。</span><span class="sxs-lookup"><span data-stu-id="7b1df-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="7b1df-277">hello 程式碼接著會叫用的 hello **sendMessage** toosend hello 訊息 tooIoT 中樞函式：</span><span class="sxs-lookup"><span data-stu-id="7b1df-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="7b1df-278">hello 第二個 toolast 參數**IoTHubClient\_LL\_SendEventAsync**是參考 tooa 回呼函式會成功地傳送 hello 資料時所呼叫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="7b1df-279">以下是 hello 範例 hello 回呼函式：</span><span class="sxs-lookup"><span data-stu-id="7b1df-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="7b1df-280">hello 第二個參數是指標 toouser 內容。相同的指標傳遞太 hello**IoTHubClient\_LL\_SendEventAsync**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="7b1df-281">在此情況下，hello 內容是簡單的計數器，但它可以是您想要的任何項目。</span><span class="sxs-lookup"><span data-stu-id="7b1df-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="7b1df-282">這就是沒有 toosending 裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="7b1df-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="7b1df-283">hello 只保留 toocover 是如何 tooreceive 訊息。</span><span class="sxs-lookup"><span data-stu-id="7b1df-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="7b1df-284">接收訊息</span><span class="sxs-lookup"><span data-stu-id="7b1df-284">Receive messages</span></span>

<span data-ttu-id="7b1df-285">接收訊息的運作方式類似 toohello 訊息在中運作的方式 hello **IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="7b1df-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="7b1df-286">首先，您需登錄訊息回呼函式：</span><span class="sxs-lookup"><span data-stu-id="7b1df-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="7b1df-287">然後，您可以撰寫 hello 時收到訊息時叫用的回呼函式：</span><span class="sxs-lookup"><span data-stu-id="7b1df-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="7b1df-288">此程式碼是未定案--它具有 hello 相同的任何方案。</span><span class="sxs-lookup"><span data-stu-id="7b1df-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="7b1df-289">此函式收到 hello 訊息，並負責路由傳送透過 hello 呼叫 toohello 適當的函式太**EXECUTE\_命令**。</span><span class="sxs-lookup"><span data-stu-id="7b1df-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="7b1df-290">hello 函式，呼叫此時取決於您的模型中的 hello 動作 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="7b1df-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="7b1df-291">當您在模型中定義的動作時，您需要 tooimplement 裝置收到 hello 對應的訊息時所呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="7b1df-292">例如，如果您的模型定義這項動作：</span><span class="sxs-lookup"><span data-stu-id="7b1df-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="7b1df-293">使用此簽章定義函式：</span><span class="sxs-lookup"><span data-stu-id="7b1df-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="7b1df-294">請注意如何 hello hello 函式名稱比對 hello hello 模型中的 hello 動作名稱和 hello 的 hello 函式的參數符合指定的 hello 動作的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="7b1df-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="7b1df-295">hello 第一個參數永遠是必要項，並包含您的模型的指標 toohello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7b1df-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="7b1df-296">Hello 裝置接收符合此簽章的訊息，稱為 hello 對應函式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="7b1df-297">因此，除了具有 tooinclude hello 未定案程式碼從**IoTHubMessage**，接收訊息只是定義為模型中定義的每個動作的簡單函式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="7b1df-298">取消初始化 hello 程式庫</span><span class="sxs-lookup"><span data-stu-id="7b1df-298">Uninitialize hello library</span></span>

<span data-ttu-id="7b1df-299">當您完成將資料傳送和接收訊息，您可以解除初始化 hello IoT 程式庫：</span><span class="sxs-lookup"><span data-stu-id="7b1df-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="7b1df-300">所有這些三個函式符合先前所述 hello 三個初始設定函式。</span><span class="sxs-lookup"><span data-stu-id="7b1df-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="7b1df-301">呼叫這些 API 可確保您釋放先前配置的資源。</span><span class="sxs-lookup"><span data-stu-id="7b1df-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b1df-302">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b1df-302">Next Steps</span></span>

<span data-ttu-id="7b1df-303">本文涵蓋使用 hello 文件庫中 hello hello 基本概念**C 的 Azure IoT 裝置 SDK**。它提供您足夠的資訊 toounderstand hello SDK、 其結構，以及如何 tooget 入門使用 hello Windows 範例中包含的內容。</span><span class="sxs-lookup"><span data-stu-id="7b1df-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="7b1df-304">hello 下一個發行項的說明繼續 hello SDK hello 描述[更多關於 hello IoTHubClient 程式庫](iot-hub-device-sdk-c-iothubclient.md)。</span><span class="sxs-lookup"><span data-stu-id="7b1df-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="7b1df-305">toolearn 進一步了解開發的 IoT 中樞，請參閱 hello [Azure IoT Sdk][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="7b1df-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="7b1df-306">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="7b1df-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="7b1df-307">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="7b1df-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
