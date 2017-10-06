---
title: "SensorTag 裝置與 Azure IoT 閘道 - 開始使用 | Microsoft Docs"
description: "開始使用 IoT 閘道入門套件，建立您的 Azure IoT 中樞，並連接 SensorTag 和閘道 toohello IoT 中樞"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot 中樞，iot 閘道使用，以開始使用 hello 物聯網 iot 工具組"
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
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="99223-104">開始使用 IoT 閘道器入門套件與 SensorTag</span><span class="sxs-lookup"><span data-stu-id="99223-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="99223-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="99223-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="99223-106">模擬裝置</span><span class="sxs-lookup"><span data-stu-id="99223-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="99223-107">本教學課程中，在您開始學習使用的 hello 基本[IoT 閘道入門套件](https://aka.ms/gateway-kit)。</span><span class="sxs-lookup"><span data-stu-id="99223-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="99223-108">您即將使用 Intel NUC Wind 河 Linux 和 hello 執行[TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main)。</span><span class="sxs-lookup"><span data-stu-id="99223-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="99223-109">您將學習如何 tooseamleesly 連接您的裝置 toohello 雲端使用 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="99223-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="99223-110">**沒有套件嗎？**按一下[這裡](https://aka.ms/gateway-kit)。</span><span class="sxs-lookup"><span data-stu-id="99223-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="99223-111">**沒有 SensorTag？** [從模擬裝置開始](iot-hub-gateway-kit-c-sim-get-started.md)或[購買 SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="99223-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="99223-112">第 1 課：設定 NUC</span><span class="sxs-lookup"><span data-stu-id="99223-112">Lesson 1: Configure your NUC</span></span>
![第 1 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="99223-114">在這一課，您可以設定 hello 套件作為 Azure IoT 閘道 （下一個單位的運算） 的 Intel NUC、 NUC，在安裝 hello Azure IoT 邊緣套件並執行範例應用程式 tooverify hello 閘道功能。</span><span class="sxs-lookup"><span data-stu-id="99223-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="99223-115">*估計時間 toocomplete: 15 分鐘*</span><span class="sxs-lookup"><span data-stu-id="99223-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="99223-116">跳過[Intel NUC 為 IoT 閘道設定](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="99223-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="99223-117">第 2 課：建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="99223-117">Lesson 2: Create your IoT Hub</span></span>
![第 2 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="99223-119">在這一課，您在主機電腦上安裝 hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="99223-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="99223-120">然後您建立免費的 Azure 帳戶、 佈建您的 Azure IoT 中樞和 hello IoT 中樞中建立您的第一個裝置。</span><span class="sxs-lookup"><span data-stu-id="99223-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="99223-121">開始本課程前，請先完成第 1 課。</span><span class="sxs-lookup"><span data-stu-id="99223-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="99223-122">取得 hello 工具</span><span class="sxs-lookup"><span data-stu-id="99223-122">Get hello tools</span></span>
<span data-ttu-id="99223-123">主機電腦上安裝 hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="99223-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="99223-124">*估計時間 toocomplete: 20 分鐘*</span><span class="sxs-lookup"><span data-stu-id="99223-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="99223-125">跳過[取得 hello 工具](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="99223-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="99223-126">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="99223-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="99223-127">建立資源群組中，佈建第一個的 Azure IoT 中樞，並加入使用 hello Azure CLI 您第一次裝置 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="99223-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="99223-128">*估計時間 toocomplete: 10 分鐘*</span><span class="sxs-lookup"><span data-stu-id="99223-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="99223-129">跳過[建立 IoT 中樞，並註冊您的裝置](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="99223-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="99223-130">第 3 課︰接收來自 SensorTag 的訊息，並從您的 IoT 中心讀取訊息</span><span class="sxs-lookup"><span data-stu-id="99223-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="99223-131">在這一課，您將使用指令碼 tooautomate hello 組態和執行 b 範例應用程式在您的閘道。</span><span class="sxs-lookup"><span data-stu-id="99223-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="99223-132">這類應用程式使用的模組 tooaggregate 和轉換資料收集、 處理命令，或執行任意數目的相關工作。</span><span class="sxs-lookup"><span data-stu-id="99223-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="99223-133">模組之間透過訊息代理程式相互通訊。</span><span class="sxs-lookup"><span data-stu-id="99223-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="99223-134">hello 範例應用程式具有 b 模組與 IoT 中樞模組。</span><span class="sxs-lookup"><span data-stu-id="99223-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="99223-135">hello b 模組 B SensorTag 接收資料。</span><span class="sxs-lookup"><span data-stu-id="99223-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="99223-136">hello 收到 hello 資料，並將它的 Azure IoT Edge 傳送 tooyour IoT 中樞透過 hello 閘道架構提供 IoT 中樞模組封裝。</span><span class="sxs-lookup"><span data-stu-id="99223-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![第 3 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="99223-138">設定及執行 hello b 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="99223-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="99223-139">設定 hello SensorTag 和閘道之間的連線。</span><span class="sxs-lookup"><span data-stu-id="99223-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="99223-140">然後完成 hello 設定並執行 hello b 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="99223-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="99223-141">*估計時間 toocomplete: 15 分鐘*</span><span class="sxs-lookup"><span data-stu-id="99223-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="99223-142">跳過[設定和執行的 hello b 範例應用程式](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="99223-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="99223-143">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="99223-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="99223-144">執行範例程式碼在您的主機電腦 tooread 訊息從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="99223-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="99223-145">*估計時間 toocomplete: 15 分鐘*</span><span class="sxs-lookup"><span data-stu-id="99223-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="99223-146">跳過[從 IoT 中樞讀取訊息](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="99223-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="99223-147">第 4 課： 將訊息儲存 tooAzure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="99223-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="99223-148">建立從 IoT 中樞取得內送訊息，並將其寫入 tooAzure 資料表儲存體的 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="99223-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![第 4 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="99223-150">建立 Azure 函數應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="99223-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="99223-151">Azure 的函式應用程式與 Azure 儲存體帳戶，請使用 Azure Resource Manager 範本 toocreate。</span><span class="sxs-lookup"><span data-stu-id="99223-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="99223-152">*估計時間 toocomplete: 10 分鐘*</span><span class="sxs-lookup"><span data-stu-id="99223-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="99223-153">跳過[建立 Azure 的函式應用程式與 Azure 儲存體帳戶](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="99223-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="99223-154">讀取保存在 Azure 表格儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="99223-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="99223-155">當寫入 tooAzure 資料表儲存體監視 hello 閘道到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="99223-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="99223-156">*估計時間 toocomplete: 5 分鐘*</span><span class="sxs-lookup"><span data-stu-id="99223-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="99223-157">跳過[讀取訊息保存在 Azure 資料表儲存體](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="99223-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="99223-158">疑難排解</span><span class="sxs-lookup"><span data-stu-id="99223-158">Troubleshooting</span></span>
<span data-ttu-id="99223-159">如果您在 hello 課程期間有任何問題，尋找在 hello 解決方案[疑難排解](iot-hub-gateway-kit-c-troubleshooting.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="99223-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="99223-160">探索更多</span><span class="sxs-lookup"><span data-stu-id="99223-160">Explore more</span></span>
<span data-ttu-id="99223-161">請瀏覽 hello [Intel IoT 閘道套件開發人員區域](http://software.intel.com/iot/microsoft-azure)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="99223-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
