---
title: "適用於 C 的 Azure IoT 裝置 SDK | Microsoft Docs"
description: "開始使用適用於 C 的 Azure IoT 裝置 SDK，以及了解如何建立與 IoT 中樞通訊的裝置應用程式。"
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
ms.openlocfilehash: 459b630f28fe48064f4ba280974f3fdbdb82f0a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="01a3f-103">適用於 C 的 Azure IoT 裝置 SDK</span><span class="sxs-lookup"><span data-stu-id="01a3f-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="01a3f-104">**Azure IoT 裝置 SDK** 是一組程式庫，其設計目的是要簡化從 **Azure IoT 中樞**服務傳送訊息和接收訊息的程序。</span><span class="sxs-lookup"><span data-stu-id="01a3f-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="01a3f-105">有各種不同的 SDK，每個 SDK 都以特定的平台為目標，而本文將說明的是「Azure IoT 裝置 SDK (適用於 C)」 。</span><span class="sxs-lookup"><span data-stu-id="01a3f-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="01a3f-106">Azure IoT 裝置 SDK (適用於 C) 是以 ANSI C (C99) 撰寫，以獲得最大可攜性。</span><span class="sxs-lookup"><span data-stu-id="01a3f-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="01a3f-107">此功能讓程式庫很適合在多個平台和裝置上運作，尤其是在以將磁碟和記憶體使用量降至最低做為優先考量的情況下。</span><span class="sxs-lookup"><span data-stu-id="01a3f-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="01a3f-108">有許多平台已進行過 SDK 測試 (如需詳細資料，請參閱 [Azure IoT 認證裝置目錄](https://catalog.azureiotsuite.com/))。</span><span class="sxs-lookup"><span data-stu-id="01a3f-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="01a3f-109">雖然本文包含在 Windows 平台上執行之範例程式碼的逐步解說，但本文所述的程式碼在各種支援的平台上都完全相同。</span><span class="sxs-lookup"><span data-stu-id="01a3f-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="01a3f-110">本文介紹 Azure IoT 裝置 SDK (適用於 C) 的架構。文中會示範如何初始化裝置程式庫，將資料傳送到 IoT 中樞，以及從 IoT 中樞接收訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="01a3f-111">本文中的資訊應足以讓您開始使用 SDK，但也提供了可取得程式庫其他相關資訊的指標。</span><span class="sxs-lookup"><span data-stu-id="01a3f-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="01a3f-112">SDK 架構</span><span class="sxs-lookup"><span data-stu-id="01a3f-112">SDK architecture</span></span>

<span data-ttu-id="01a3f-113">您可以尋找[**適用於 C 的 Azure IoT 裝置 SDK**](https://github.com/Azure/azure-iot-sdk-c) GitHub 儲存機制，然後在 [C API 參考資料](https://azure.github.io/azure-iot-sdk-c/index.html)中檢視 API 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="01a3f-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="01a3f-114">在此儲存機制的 **master** 分支中可找到最新版的程式庫：</span><span class="sxs-lookup"><span data-stu-id="01a3f-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="01a3f-115">SDK 的核心實作位於 **iothub\_client** 資料夾中，此資料夾包含 SDK 中最低 API 層級的實作：**IoTHubClient** 程式庫。</span><span class="sxs-lookup"><span data-stu-id="01a3f-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="01a3f-116">**IoTHubClient** 程式庫包含了將訊息傳送至 IoT 中樞，以及從 IoT 中樞接收訊息之原始傳訊的 API 實作。</span><span class="sxs-lookup"><span data-stu-id="01a3f-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="01a3f-117">使用此程式庫時，您要負責實作訊息序列化，但與 IoT 中樞通訊的其他細節則是由系統為您處理。</span><span class="sxs-lookup"><span data-stu-id="01a3f-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="01a3f-118">**serializer** 資料夾包含 helper 函式和示範如何在資料傳送至 Azure IoT 中樞之前，使用用戶端程式庫將資料序列化的範例。</span><span class="sxs-lookup"><span data-stu-id="01a3f-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="01a3f-119">使用序列化程式並非必要，只是為了便利性而提供。</span><span class="sxs-lookup"><span data-stu-id="01a3f-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="01a3f-120">若要使用 **serializer** 程式庫，您需要定義一個模型，以指定要傳送至 IoT 中樞的資料以及您期望從 IoT 中樞收到的訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="01a3f-121">定義此模型後，SDK 會提供您一個 API 介面，可讓您輕鬆地處理裝置到雲端的訊息和雲端到裝置的訊息，而不需操心序列化細節。</span><span class="sxs-lookup"><span data-stu-id="01a3f-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="01a3f-122">此程式庫需倚賴其他使用 MQTT 和 AMQP 等通訊協定來實作傳輸的開放原始碼程式庫。</span><span class="sxs-lookup"><span data-stu-id="01a3f-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="01a3f-123">**IoTHubClient** 程式庫相依於其他開放原始碼程式庫：</span><span class="sxs-lookup"><span data-stu-id="01a3f-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="01a3f-124">[Azure C 共用公用程式](https://github.com/Azure/azure-c-shared-utility)程式庫，此程式庫提供數個 Azure 相關 C SDK 所需之基本工作 (例如字串、清單操作和 IO) 的常見功能。</span><span class="sxs-lookup"><span data-stu-id="01a3f-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="01a3f-125">[Azure uAMQP](https://github.com/Azure/azure-uamqp-c) 程式庫，這是針對資源條件約束裝置最佳化的 AMQP 用戶端端實作。</span><span class="sxs-lookup"><span data-stu-id="01a3f-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="01a3f-126">[Azure uMQTT](https://github.com/Azure/azure-umqtt-c) 程式庫，這是實作 MQTT 通訊協定並已針對資源條件約束裝置最佳化的一般用途程式庫。</span><span class="sxs-lookup"><span data-stu-id="01a3f-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="01a3f-127">查看程式碼範例可以較容易了解如何使用這些程式庫。</span><span class="sxs-lookup"><span data-stu-id="01a3f-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="01a3f-128">下列各節將為您逐步解說 SDK 中包含的幾個範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="01a3f-129">此逐步解說應可讓您輕鬆了解 SDK 架構層的各種功能以及 API 運作方式的簡介。</span><span class="sxs-lookup"><span data-stu-id="01a3f-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="01a3f-130">在您執行範例之前</span><span class="sxs-lookup"><span data-stu-id="01a3f-130">Before you run the samples</span></span>

<span data-ttu-id="01a3f-131">您必須先在您的 Azure 訂用帳戶上[建立一個 IoT 中樞服務執行個體](iot-hub-create-through-portal.md)，才能在適用於 C 的 Azure IoT 裝置 SDK 中執行範例。</span><span class="sxs-lookup"><span data-stu-id="01a3f-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="01a3f-132">然後完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="01a3f-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="01a3f-133">準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="01a3f-133">Prepare your development environment</span></span>
* <span data-ttu-id="01a3f-134">取得裝置認證。</span><span class="sxs-lookup"><span data-stu-id="01a3f-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="01a3f-135">準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="01a3f-135">Prepare your development environment</span></span>

<span data-ttu-id="01a3f-136">套件是針對常見平台 (例如適用於 Windows 的 NuGet 或適用於 Debian 和 Ubuntu 的 apt_get) 所提供，且範例會在這些套件可用時加以使用。</span><span class="sxs-lookup"><span data-stu-id="01a3f-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="01a3f-137">在某些情況下，您需要為您的裝置或在裝置編譯 SDK。</span><span class="sxs-lookup"><span data-stu-id="01a3f-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="01a3f-138">如果您需要編譯 SDK，請參閱 GitHub 儲存機制中的[準備您的開發環境](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md)。</span><span class="sxs-lookup"><span data-stu-id="01a3f-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="01a3f-139">若要取得應用程式的程式碼範例，請從 GitHub 下載 SDK 的複本。</span><span class="sxs-lookup"><span data-stu-id="01a3f-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="01a3f-140">從 [GitHub 儲存機制](https://github.com/Azure/azure-iot-sdk-c)的 **master** 分支取得一份原始檔複本。</span><span class="sxs-lookup"><span data-stu-id="01a3f-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="01a3f-141">取得裝置認證</span><span class="sxs-lookup"><span data-stu-id="01a3f-141">Obtain the device credentials</span></span>

<span data-ttu-id="01a3f-142">現在您已擁有原始程式碼範例，下一件事就是取得一組裝置認證。</span><span class="sxs-lookup"><span data-stu-id="01a3f-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="01a3f-143">若要讓裝置能夠存取 IoT 中樞，您必須先將該裝置新增至 IoT 中樞身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="01a3f-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="01a3f-144">當您新增裝置時，您會取得一組所需的裝置認證，以便裝置能夠連線到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="01a3f-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="01a3f-145">下一節所討論的應用程式範例預期這些認證的形式為**裝置連接字串**。</span><span class="sxs-lookup"><span data-stu-id="01a3f-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="01a3f-146">有幾個開放原始碼工具可協助您管理 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="01a3f-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="01a3f-147">稱為[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)的 Windows 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="01a3f-148">稱為 [iothub-explorer](https://github.com/azure/iothub-explorer) 的跨平台 node.js CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="01a3f-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="01a3f-149">本教學課程使用圖形化「裝置總管」工具。</span><span class="sxs-lookup"><span data-stu-id="01a3f-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="01a3f-150">如果您偏好使用 CLI 工具，您也可以使用 iothub-explorer 工具。</span><span class="sxs-lookup"><span data-stu-id="01a3f-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="01a3f-151">裝置總管工具會使用 Azure IoT 服務程式庫在 IoT 中樞上執行各種功能，包括新增裝置。</span><span class="sxs-lookup"><span data-stu-id="01a3f-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="01a3f-152">如果您使用裝置總管工具來新增裝置，您會得到裝置的連接字串。</span><span class="sxs-lookup"><span data-stu-id="01a3f-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="01a3f-153">您需要此連接字串才能執行應用程式範例。</span><span class="sxs-lookup"><span data-stu-id="01a3f-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="01a3f-154">如果您不熟悉此裝置總管工具，下列程序說明如何使用它來新增裝置和取得裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="01a3f-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="01a3f-155">若要安裝裝置總管工具，請參閱[如何對 IoT 中樞裝置使用裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)。</span><span class="sxs-lookup"><span data-stu-id="01a3f-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="01a3f-156">當您執行程式時，您會看到此介面：</span><span class="sxs-lookup"><span data-stu-id="01a3f-156">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="01a3f-157">請在第一個欄位中輸入您的 [IoT 中樞連接字串]，然後按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="01a3f-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="01a3f-158">此步驟可設定此工具，以便與 IoT 中樞通訊。</span><span class="sxs-lookup"><span data-stu-id="01a3f-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="01a3f-159">設定 IoT 中樞連接字串後，請按一下 [管理] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="01a3f-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="01a3f-160">此索引標籤可讓您管理在 IoT 中樞註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="01a3f-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="01a3f-161">按一下 [建立] 按鈕即可建立裝置。</span><span class="sxs-lookup"><span data-stu-id="01a3f-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="01a3f-162">將會顯示一個已預先填入一組金鑰 (主要和次要) 的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="01a3f-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="01a3f-163">輸入 [裝置識別碼]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="01a3f-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="01a3f-164">建立裝置後，就會以所有註冊的裝置 (包括您剛才建立的裝置) 更新 [裝置] 清單。</span><span class="sxs-lookup"><span data-stu-id="01a3f-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="01a3f-165">如果您在新裝置上按一下滑鼠右鍵，您會看到此功能表︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="01a3f-166">如果您選擇 [複製所選裝置的連接字串]，裝置連接字串就會複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="01a3f-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="01a3f-167">請保留一份裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="01a3f-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="01a3f-168">在執行後續各節中所述的範例應用程式時，您會需要它。</span><span class="sxs-lookup"><span data-stu-id="01a3f-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="01a3f-169">完成上述步驟後，您就可以開始執行一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="01a3f-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="01a3f-170">兩個範例在主要原始程式檔頂端都有一個常數，此常數可讓您輸入連接字串。</span><span class="sxs-lookup"><span data-stu-id="01a3f-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="01a3f-171">例如，來自 **iothub\_client\_sample\_mqtt** 應用程式的對應行會如以下所示。</span><span class="sxs-lookup"><span data-stu-id="01a3f-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="01a3f-172">使用 IoTHubClient 程式庫</span><span class="sxs-lookup"><span data-stu-id="01a3f-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="01a3f-173">在 [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) 儲存機制的 **iothub\_client** 資料夾中，有一個 [samples] 資料夾，當中包含名為 **iothub\_client\_sample\_mqtt** 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="01a3f-174">Windows 版本的 **iothub\_client\_sample\_mqtt** 應用程式包含下列 Visual Studio 方案：</span><span class="sxs-lookup"><span data-stu-id="01a3f-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="01a3f-175">如果您在 Visual Studio 2017 開啟這個專案，請接受提示以將專案的目標重定為最新版本。</span><span class="sxs-lookup"><span data-stu-id="01a3f-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="01a3f-176">此解決方案內含單一專案：</span><span class="sxs-lookup"><span data-stu-id="01a3f-176">This solution contains a single project.</span></span> <span data-ttu-id="01a3f-177">此解決方案中安裝了四個 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="01a3f-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="01a3f-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="01a3f-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="01a3f-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="01a3f-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="01a3f-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="01a3f-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="01a3f-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="01a3f-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="01a3f-182">使用 SDK 時，您永遠需要 **Microsoft.Azure.C.SharedUtility** 封裝。</span><span class="sxs-lookup"><span data-stu-id="01a3f-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="01a3f-183">此範例使用 MQTT 通訊協定，因此您必須納入 **Microsoft.Azure.umqtt** 和 **Microsoft.Azure.IoTHub.MqttTransport** 套件 (AMQP 和 HTTP 有對等套件)。</span><span class="sxs-lookup"><span data-stu-id="01a3f-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="01a3f-184">由於此範例使用 **IoTHubClient** 程式庫，因此您也必須在方案中納入 **Microsoft.Azure.IoTHub.IoTHubClient** 套件。</span><span class="sxs-lookup"><span data-stu-id="01a3f-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="01a3f-185">您可以在 **iothub\_client\_sample\_mqtt.c** 原始程式檔中找到範例應用程式的實作。</span><span class="sxs-lookup"><span data-stu-id="01a3f-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="01a3f-186">下列步驟使用此應用程式範例來逐步解說使用 **IoTHubClient** 程式庫時所需的項目。</span><span class="sxs-lookup"><span data-stu-id="01a3f-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="01a3f-187">初始化程式庫</span><span class="sxs-lookup"><span data-stu-id="01a3f-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="01a3f-188">開始使用程式庫之前，您可能需要執行某些平台特定的初始化。</span><span class="sxs-lookup"><span data-stu-id="01a3f-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="01a3f-189">例如，如果您打算在 Linux 上使用 AMQP，您就必須初始化 OpenSSL 程式庫。</span><span class="sxs-lookup"><span data-stu-id="01a3f-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="01a3f-190">[GitHub 儲存機制](https://github.com/Azure/azure-iot-sdk-c)中的範例會在用戶端啟動時呼叫 **platform\_init** 公用程式函式，並在結束之前呼叫 **platform\_deinit** 函式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="01a3f-191">這些函式在 platform.h 標頭檔中宣告。</span><span class="sxs-lookup"><span data-stu-id="01a3f-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="01a3f-192">請在[儲存機制](https://github.com/Azure/azure-iot-sdk-c)中為目標平台檢查這些函式的定義，以判斷是否需要在您的用戶端加入任何平台特定的初始化程式碼。</span><span class="sxs-lookup"><span data-stu-id="01a3f-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="01a3f-193">若要開始使用程式庫，請先配置 IoT 中樞用戶端控制代碼︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="01a3f-194">您要將從裝置總管工具取得的裝置連接字串複本傳遞給此函式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="01a3f-195">您也可以指定要使用的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="01a3f-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="01a3f-196">這個範例使用 MQTT，但 AMQP 與 HTTP 也是選項。</span><span class="sxs-lookup"><span data-stu-id="01a3f-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="01a3f-197">當您具有有效的 **IOTHUB\_CLIENT\_HANDLE** 時，您可以開始呼叫 API 以對 IoT 中樞傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="01a3f-198">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="01a3f-198">Send messages</span></span>

<span data-ttu-id="01a3f-199">應用程式範例會設定迴圈以將訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="01a3f-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="01a3f-200">下列程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-200">The following snippet:</span></span>

- <span data-ttu-id="01a3f-201">建立訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-201">Creates a message.</span></span>
- <span data-ttu-id="01a3f-202">將屬性新增至訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-202">Adds a property to the message.</span></span>
- <span data-ttu-id="01a3f-203">傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-203">Sends a message.</span></span>

<span data-ttu-id="01a3f-204">首先，建立一則訊息：</span><span class="sxs-lookup"><span data-stu-id="01a3f-204">First, create a message:</span></span>

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
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="01a3f-205">每次傳送訊息時，您會指定傳送資料時所叫用的回呼函式的參考。</span><span class="sxs-lookup"><span data-stu-id="01a3f-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="01a3f-206">在此範例中，回呼函式稱為 **SendConfirmationCallback**。</span><span class="sxs-lookup"><span data-stu-id="01a3f-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="01a3f-207">下列程式碼片段會顯示這個回呼函式︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-207">The following snippet shows this callback function:</span></span>

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

<span data-ttu-id="01a3f-208">請注意在您完成訊息時對 **IoTHubMessage\_Destroy** 函式進行的呼叫。</span><span class="sxs-lookup"><span data-stu-id="01a3f-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="01a3f-209">此函式會釋放在建立訊息時配置的資源。</span><span class="sxs-lookup"><span data-stu-id="01a3f-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="01a3f-210">接收訊息</span><span class="sxs-lookup"><span data-stu-id="01a3f-210">Receive messages</span></span>

<span data-ttu-id="01a3f-211">接收訊息是非同步作業。</span><span class="sxs-lookup"><span data-stu-id="01a3f-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="01a3f-212">首先，您會登錄在裝置接收訊息時所要叫用的回呼：</span><span class="sxs-lookup"><span data-stu-id="01a3f-212">First, you register the callback to invoke when the device receives a message:</span></span>

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

<span data-ttu-id="01a3f-213">最後一個參數是您所要項目的無效指標。</span><span class="sxs-lookup"><span data-stu-id="01a3f-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="01a3f-214">在範例中，這是一個整數的指標，但可能是更複雜的資料結構的指標。</span><span class="sxs-lookup"><span data-stu-id="01a3f-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="01a3f-215">此參數可讓回呼函式與此函式的呼叫者以共用狀態運作。</span><span class="sxs-lookup"><span data-stu-id="01a3f-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="01a3f-216">當裝置接收訊息時，會叫用登錄的回呼函式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="01a3f-217">此回呼函式會擷取︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-217">This callback function retrieves:</span></span>

* <span data-ttu-id="01a3f-218">訊息識別碼和訊息中的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="01a3f-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="01a3f-219">訊息內容。</span><span class="sxs-lookup"><span data-stu-id="01a3f-219">The message content.</span></span>
* <span data-ttu-id="01a3f-220">訊息中的任何自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="01a3f-220">Any custom properties from the message.</span></span>

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
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
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

<span data-ttu-id="01a3f-221">使用 **IoTHubMessage\_GetByteArray** 函式來擷取訊息 (在此範例中是一個字串)。</span><span class="sxs-lookup"><span data-stu-id="01a3f-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="01a3f-222">解除初始化程式庫</span><span class="sxs-lookup"><span data-stu-id="01a3f-222">Uninitialize the library</span></span>

<span data-ttu-id="01a3f-223">當您完成事件傳送和訊息接收時，您可以將 IoT 程式庫解除初始化。</span><span class="sxs-lookup"><span data-stu-id="01a3f-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="01a3f-224">若要這麼做，請發出下列函式呼叫：</span><span class="sxs-lookup"><span data-stu-id="01a3f-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="01a3f-225">此呼叫會釋出 **IoTHubClient\_CreateFromConnectionString** 函式先前所配置的資源。</span><span class="sxs-lookup"><span data-stu-id="01a3f-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="01a3f-226">如您所見，使用 **IoTHubClient** 程式庫可以輕鬆傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="01a3f-227">此程式庫會處理與 IoT 中樞進行的通訊細節，包括要使用哪個通訊協定 (從開發人員的觀點來看，這是一個簡單的設定選項)。</span><span class="sxs-lookup"><span data-stu-id="01a3f-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="01a3f-228">**IoTHubClient** 程式庫也可讓您精確地控制如何將裝置傳送到 IoT 中樞的資料序列化。</span><span class="sxs-lookup"><span data-stu-id="01a3f-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="01a3f-229">在某些情況下，此控制層級是一項優點，但在其他情況下，這是您不想要參與的實作細節。</span><span class="sxs-lookup"><span data-stu-id="01a3f-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="01a3f-230">如果是後者，您可以考慮使用下一節中說明的**序列化程式**程式庫。</span><span class="sxs-lookup"><span data-stu-id="01a3f-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="01a3f-231">使用序列化程式程式庫</span><span class="sxs-lookup"><span data-stu-id="01a3f-231">Use the serializer library</span></span>

<span data-ttu-id="01a3f-232">在概念上，「序列化程式」程式庫位於 SDK 中的 **IoTHubClient** 程式庫之上。</span><span class="sxs-lookup"><span data-stu-id="01a3f-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="01a3f-233">它會使用 **IoTHubClient** 程式庫與 IoT 中樞進行基礎通訊，但是會新增模型化功能，以減輕開發人員處理訊息序列化的負擔。</span><span class="sxs-lookup"><span data-stu-id="01a3f-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="01a3f-234">此程式庫的運作方式最好是由範例示範。</span><span class="sxs-lookup"><span data-stu-id="01a3f-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="01a3f-235">在 [azure-iot-sdk-c 儲存機制](https://github.com/Azure/azure-iot-sdk-c)的 [serializer] 資料夾中，有一個 [samples] 資料夾，當中包含名為 **simplesample\_mqtt** 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="01a3f-236">Windows 版本的這個範例包含下列 Visual Studio 解決方案：</span><span class="sxs-lookup"><span data-stu-id="01a3f-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="01a3f-237">如果您在 Visual Studio 2017 開啟這個專案，請接受提示以將專案的目標重定為最新版本。</span><span class="sxs-lookup"><span data-stu-id="01a3f-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="01a3f-238">如同先前的範例，此範例也包含數個 NuGet 套件：</span><span class="sxs-lookup"><span data-stu-id="01a3f-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="01a3f-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="01a3f-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="01a3f-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="01a3f-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="01a3f-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="01a3f-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="01a3f-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="01a3f-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="01a3f-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="01a3f-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="01a3f-244">您已在先前的範例中看過上述大多數的套件，但 **Microsoft.Azure.IoTHub.Serializer** 是新的。</span><span class="sxs-lookup"><span data-stu-id="01a3f-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="01a3f-245">當您使用 **serializer** 程式庫時必須使用此套件。</span><span class="sxs-lookup"><span data-stu-id="01a3f-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="01a3f-246">您可以在 **simplesample\_mqtt.c** 檔案中找到範例應用程式的實作。</span><span class="sxs-lookup"><span data-stu-id="01a3f-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="01a3f-247">下列各節將逐步解說此範例的重要部分。</span><span class="sxs-lookup"><span data-stu-id="01a3f-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="01a3f-248">初始化程式庫</span><span class="sxs-lookup"><span data-stu-id="01a3f-248">Initialize the library</span></span>

<span data-ttu-id="01a3f-249">若要開始使用 **serializer** 程式庫，請呼叫初始化 API︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

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

<span data-ttu-id="01a3f-250">對 **serializer\_init** 函式的呼叫是單次呼叫，此呼叫可將基礎程式庫初始化。</span><span class="sxs-lookup"><span data-stu-id="01a3f-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="01a3f-251">接著，您需呼叫 **IoTHubClient\_LL\_CreateFromConnectionString** 函式，這與 **IoTHubClient** 範例中的 API 相同。</span><span class="sxs-lookup"><span data-stu-id="01a3f-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="01a3f-252">此呼叫會設定您的裝置連接字串 (此呼叫也可用來選擇您要使用的通訊協定)。</span><span class="sxs-lookup"><span data-stu-id="01a3f-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="01a3f-253">此範例使用 MQTT 作為傳輸，但也可以使用 AMQP 或 HTTP。</span><span class="sxs-lookup"><span data-stu-id="01a3f-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="01a3f-254">最後，呼叫 **CREATE\_MODEL\_INSTANCE** 函式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="01a3f-255">**WeatherStation** 是模型的命名空間，而 **ContosoAnemometer** 是模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="01a3f-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="01a3f-256">建立模型執行個體後，您便可以使用它來開始傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="01a3f-257">不過，請務必了解模型是什麼。</span><span class="sxs-lookup"><span data-stu-id="01a3f-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="01a3f-258">定義模型</span><span class="sxs-lookup"><span data-stu-id="01a3f-258">Define the model</span></span>

<span data-ttu-id="01a3f-259">**serializer** 程式庫中的模型會定義您的裝置可傳送至 IoT 中樞的訊息以及其可接收的訊息 (在模組化語言中稱為*動作*)。</span><span class="sxs-lookup"><span data-stu-id="01a3f-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="01a3f-260">您可使用如 **simplesample\_mqtt** 應用程式範例中的一組 C 巨集來定義模型︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="01a3f-261">**BEGIN\_NAMESPACE** 和 **END\_NAMESPACE** 這兩個巨集都會以模型的命名空間作為引數。</span><span class="sxs-lookup"><span data-stu-id="01a3f-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="01a3f-262">介於這兩個巨集之間的項目應該就是您的一或多個模型的定義和模型所使用的資料結構。</span><span class="sxs-lookup"><span data-stu-id="01a3f-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="01a3f-263">在此範例中，有一個名為 **ContosoAnemometer**的模型。</span><span class="sxs-lookup"><span data-stu-id="01a3f-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="01a3f-264">此模型會定義您裝置可傳送到 IoT 中樞的兩個資料片段︰**DeviceId** 和 **WindSpeed**。</span><span class="sxs-lookup"><span data-stu-id="01a3f-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="01a3f-265">它也定義您裝置可接收的三個動作 (訊息)：**TurnFanOn**、**TurnFanOff** 及 **SetAirResistance**。</span><span class="sxs-lookup"><span data-stu-id="01a3f-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="01a3f-266">每個資料元素都有類型，而每個動作都有名稱 (以及一組選擇性的參數)。</span><span class="sxs-lookup"><span data-stu-id="01a3f-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="01a3f-267">模型中定義的資料和動作可定義 API 介面，此介面可供您用來將訊息傳送到 IoT 中樞，以及回應傳送至裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="01a3f-268">透過範例最能了解如何使用此模型。</span><span class="sxs-lookup"><span data-stu-id="01a3f-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="01a3f-269">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="01a3f-269">Send messages</span></span>

<span data-ttu-id="01a3f-270">此模型會定義您可以傳送到 IoT 中樞的資料。</span><span class="sxs-lookup"><span data-stu-id="01a3f-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="01a3f-271">在此範例中，這是指使用 **WITH_DATA** 巨集來定義的兩個資料項目之一。</span><span class="sxs-lookup"><span data-stu-id="01a3f-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="01a3f-272">要將 **DeviceId** 和 **WindSpeed** 值傳送至 IoT 中樞需要執行幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="01a3f-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="01a3f-273">第一個步驟是設定您要傳送的資料：</span><span class="sxs-lookup"><span data-stu-id="01a3f-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="01a3f-274">您稍早定義的模型可讓您藉由設定 **struct** 的成員來設定值。</span><span class="sxs-lookup"><span data-stu-id="01a3f-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="01a3f-275">接下來，將您需要傳送的訊息序列化︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-275">Next, serialize the message you want to send:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="01a3f-276">此程式碼會將裝置到雲端序列化至緩衝區 (由 **destination** 參考)。</span><span class="sxs-lookup"><span data-stu-id="01a3f-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="01a3f-277">此程式碼接著會叫用 **sendMessage** 函式以將訊息傳送至 IoT 中樞︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="01a3f-278">**IoTHubClient\_LL\_SendEventAsync** 的倒數第二個參數是對成功傳送資料時所呼叫之回呼函式的參考。</span><span class="sxs-lookup"><span data-stu-id="01a3f-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="01a3f-279">以下是範例中的回呼函式︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="01a3f-280">第二個參數是使用者內容的指標；即傳遞給 **IoTHubClient\_LL\_SendEventAsync** 的同一指標。</span><span class="sxs-lookup"><span data-stu-id="01a3f-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="01a3f-281">在此案例中，此內容是一個簡易計數器，但它可以是您想要的任何東西。</span><span class="sxs-lookup"><span data-stu-id="01a3f-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="01a3f-282">傳送裝置到雲端的訊息就是這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="01a3f-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="01a3f-283">最後只剩下說明如何接收訊息。</span><span class="sxs-lookup"><span data-stu-id="01a3f-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="01a3f-284">接收訊息</span><span class="sxs-lookup"><span data-stu-id="01a3f-284">Receive messages</span></span>

<span data-ttu-id="01a3f-285">接收訊息的方式類似於在 **IoTHubClient** 程式庫中使用訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="01a3f-286">首先，您需登錄訊息回呼函式：</span><span class="sxs-lookup"><span data-stu-id="01a3f-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="01a3f-287">然後，撰寫在接收訊息時所叫用的回呼函式：</span><span class="sxs-lookup"><span data-stu-id="01a3f-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="01a3f-288">此程式碼會重複使用 - 對任何解決方案而言都一樣。</span><span class="sxs-lookup"><span data-stu-id="01a3f-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="01a3f-289">此函式會接收訊息，然後透過呼叫 **EXECUTE\_COMMAND** 來負責將它路由傳送至適當的函式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="01a3f-290">此時所呼叫的函式取決於模型中的動作定義。</span><span class="sxs-lookup"><span data-stu-id="01a3f-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="01a3f-291">當您在模型中定義動作時，您必須實作在裝置接收對應的訊息時所呼叫的函式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="01a3f-292">例如，如果您的模型定義這項動作：</span><span class="sxs-lookup"><span data-stu-id="01a3f-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="01a3f-293">使用此簽章定義函式：</span><span class="sxs-lookup"><span data-stu-id="01a3f-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="01a3f-294">注意函式的名稱如何與模型中的動作名稱相符，以及函式的參數如何與為此動作指定的參數相符。</span><span class="sxs-lookup"><span data-stu-id="01a3f-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="01a3f-295">第一個參數是必要參數，含有模型執行個體的指標。</span><span class="sxs-lookup"><span data-stu-id="01a3f-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="01a3f-296">當裝置收到符合此簽章的訊息時，就會呼叫對應的函式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="01a3f-297">因此，除了必須包含 **IoTHubMessage**中重複使用的程式碼之外，接收訊息所涉及的只有為模型中定義的每個動作定義一個簡單的函式。</span><span class="sxs-lookup"><span data-stu-id="01a3f-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="01a3f-298">解除初始化程式庫</span><span class="sxs-lookup"><span data-stu-id="01a3f-298">Uninitialize the library</span></span>

<span data-ttu-id="01a3f-299">當您完成資料傳送和訊息接收時，您可以解除初始化 IoT 程式庫：</span><span class="sxs-lookup"><span data-stu-id="01a3f-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="01a3f-300">這三個函式每一個都與先前所述的三個初始化函式密切合作。</span><span class="sxs-lookup"><span data-stu-id="01a3f-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="01a3f-301">呼叫這些 API 可確保您釋放先前配置的資源。</span><span class="sxs-lookup"><span data-stu-id="01a3f-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01a3f-302">後續步驟</span><span class="sxs-lookup"><span data-stu-id="01a3f-302">Next Steps</span></span>

<span data-ttu-id="01a3f-303">本文涵蓋使用「適用於 Azure IoT 裝置 SDK」中程式庫的基本概念。這提供您足夠的資訊來了解 SDK 中包含什麼、其架構，以及如何開始使用 Windows 範例。</span><span class="sxs-lookup"><span data-stu-id="01a3f-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="01a3f-304">下一篇文章藉由說明 [IoTHubClient 程式庫的相關資訊](iot-hub-device-sdk-c-iothubclient.md)來繼續說明 SDK。</span><span class="sxs-lookup"><span data-stu-id="01a3f-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="01a3f-305">若要深入了解如何開發 IoT 中樞，請參閱 [Azure IoT SDK][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="01a3f-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="01a3f-306">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="01a3f-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="01a3f-307">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="01a3f-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
