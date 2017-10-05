---
title: "SensorTag 裝置與 Azure IoT 閘道 - 開始使用 | Microsoft Docs"
description: "開始使用 IoT 閘道器入門套件、建立 Azure IoT 中樞，以及將 SensorTag 和閘道器連接到 IoT 中樞"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot 中樞, iot 閘道器, 開始使用物聯網, iot 工具套件"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 624bdc7877d5048da08897f868272fd8e8f3f7b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="936ed-104">開始使用 IoT 閘道器入門套件與 SensorTag</span><span class="sxs-lookup"><span data-stu-id="936ed-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="936ed-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="936ed-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="936ed-106">模擬裝置</span><span class="sxs-lookup"><span data-stu-id="936ed-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="936ed-107">在本教學課程中，您會開始了解使用 [IoT 閘道器入門套件](https://aka.ms/gateway-kit)的基本知識。</span><span class="sxs-lookup"><span data-stu-id="936ed-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="936ed-108">您會使用執行 Wind River Linux 的 Intel NUC 和 [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main)。</span><span class="sxs-lookup"><span data-stu-id="936ed-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="936ed-109">您將了解如何使用 Azure IoT 中樞讓您的裝置順暢地與雲端連線。</span><span class="sxs-lookup"><span data-stu-id="936ed-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="936ed-110">**沒有套件嗎？**按一下[這裡](https://aka.ms/gateway-kit)。</span><span class="sxs-lookup"><span data-stu-id="936ed-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="936ed-111">**沒有 SensorTag？** [從模擬裝置開始](iot-hub-gateway-kit-c-sim-get-started.md)或[購買 SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="936ed-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="936ed-112">第 1 課：設定 NUC</span><span class="sxs-lookup"><span data-stu-id="936ed-112">Lesson 1: Configure your NUC</span></span>
![第 1 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="936ed-114">在本課程中，您要將套件中的 Intel NUC (Next Unit of Computing) 設定為 Azure IoT 閘道、在 NUC 上安裝 Azure IoT Edge 套件，並執行範例應用程式以確認閘道的功能。</span><span class="sxs-lookup"><span data-stu-id="936ed-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="936ed-115">*預估完成時間：15 分鐘*</span><span class="sxs-lookup"><span data-stu-id="936ed-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="936ed-116">前往[將 Intel NUC 設定為 IoT 閘道器](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="936ed-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="936ed-117">第 2 課：建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="936ed-117">Lesson 2: Create your IoT Hub</span></span>
![第 2 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="936ed-119">在這一課，您要在主機電腦上安裝工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="936ed-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="936ed-120">然後會建立一個免費的 Azure 帳戶、佈建您的 Azure IoT 中樞，並在 IoT 中樞建立您的第一個裝置。</span><span class="sxs-lookup"><span data-stu-id="936ed-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="936ed-121">開始本課程前，請先完成第 1 課。</span><span class="sxs-lookup"><span data-stu-id="936ed-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="936ed-122">取得工具</span><span class="sxs-lookup"><span data-stu-id="936ed-122">Get the tools</span></span>
<span data-ttu-id="936ed-123">在您的主機電腦上安裝工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="936ed-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="936ed-124">*預估完成時間：20 分鐘*</span><span class="sxs-lookup"><span data-stu-id="936ed-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="936ed-125">前往[取得工具](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="936ed-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="936ed-126">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="936ed-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="936ed-127">建立資源群組、佈建第一個 Azure IoT 中樞，並使用 Azure CLI 將第一個裝置新增至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="936ed-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="936ed-128">*預估完成時間：10 分鐘*</span><span class="sxs-lookup"><span data-stu-id="936ed-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="936ed-129">前往[建立 IoT 中樞並登錄您的裝置](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="936ed-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="936ed-130">第 3 課︰接收來自 SensorTag 的訊息，並從您的 IoT 中心讀取訊息</span><span class="sxs-lookup"><span data-stu-id="936ed-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="936ed-131">在這一課，您將使用指令碼將閘道器中 BLE 範例應用程式的設定和執行自動化。</span><span class="sxs-lookup"><span data-stu-id="936ed-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="936ed-132">這類應用程式使用模組集合來彙總及轉換資料的、處理命令，或執行任意數目的相關工作。</span><span class="sxs-lookup"><span data-stu-id="936ed-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="936ed-133">模組之間透過訊息代理程式相互通訊。</span><span class="sxs-lookup"><span data-stu-id="936ed-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="936ed-134">範例應用程式有 BLE 模組和 IoT 中樞模組。</span><span class="sxs-lookup"><span data-stu-id="936ed-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="936ed-135">BLE 模組從 BLE SensorTag 接收資料。</span><span class="sxs-lookup"><span data-stu-id="936ed-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="936ed-136">IoT 中樞模組會封裝收到的資料，並透過 Azure IoT Edge 中提供的閘道架構將資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="936ed-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![第 3 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="936ed-138">設定和執行 BLE 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="936ed-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="936ed-139">設定 SensorTag 與閘道器之間的連線。</span><span class="sxs-lookup"><span data-stu-id="936ed-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="936ed-140">然後完成設定，並執行 BLE 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="936ed-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="936ed-141">*預估完成時間：15 分鐘*</span><span class="sxs-lookup"><span data-stu-id="936ed-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="936ed-142">前往[設定和執行 BLE 範例應用程式](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="936ed-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="936ed-143">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="936ed-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="936ed-144">在主機電腦上執行範例程式碼，以讀取來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="936ed-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="936ed-145">*預估完成時間：15 分鐘*</span><span class="sxs-lookup"><span data-stu-id="936ed-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="936ed-146">前往[讀取來自 IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="936ed-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="936ed-147">第 4 課︰將訊息儲存到 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="936ed-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="936ed-148">建立 Azure 函數應用程式，此應用程式會從 IoT 中樞取得傳入訊息，並將這些訊息寫入 Azure 表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="936ed-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![第 4 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="936ed-150">建立 Azure 函數應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="936ed-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="936ed-151">使用 Azure Resource Manager 範本來建立 Azure 函數應用程式及 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="936ed-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="936ed-152">*預估完成時間：10 分鐘*</span><span class="sxs-lookup"><span data-stu-id="936ed-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="936ed-153">前往[建立 Azure 函數應用程式與 Azure 儲存體帳戶](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="936ed-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="936ed-154">讀取保存在 Azure 表格儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="936ed-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="936ed-155">當閘道器到雲端訊息寫入 Azure 表格儲存體時對其進行監視。</span><span class="sxs-lookup"><span data-stu-id="936ed-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="936ed-156">*預估完成時間：5 分鐘*</span><span class="sxs-lookup"><span data-stu-id="936ed-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="936ed-157">前往[讀取保存在 Azure 表格儲存體中的訊息](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="936ed-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="936ed-158">疑難排解</span><span class="sxs-lookup"><span data-stu-id="936ed-158">Troubleshooting</span></span>
<span data-ttu-id="936ed-159">如果在課程期間遇到任何問題，您可以在[疑難排解](iot-hub-gateway-kit-c-troubleshooting.md)一文中尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="936ed-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="936ed-160">探索更多</span><span class="sxs-lookup"><span data-stu-id="936ed-160">Explore more</span></span>
<span data-ttu-id="936ed-161">若要深入了解，請瀏覽 [Intel IoT 閘道器套件開發人員區域](http://software.intel.com/iot/microsoft-azure)。</span><span class="sxs-lookup"><span data-stu-id="936ed-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>