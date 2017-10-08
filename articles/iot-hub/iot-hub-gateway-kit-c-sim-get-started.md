---
title: "模擬裝置與 Azure IoT 閘道 - 開始使用 | Microsoft Docs"
description: "開始使用 IoT 閘道入門套件，建立您的 Azure IoT 中樞，並連接閘道 toohello IoT 中樞"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot 中樞，iot 閘道使用，以開始使用 hello 物聯網 iot 工具組"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="97559-104">開始使用 IoT 閘道器入門套件與模擬裝置</span><span class="sxs-lookup"><span data-stu-id="97559-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="97559-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="97559-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="97559-106">模擬裝置</span><span class="sxs-lookup"><span data-stu-id="97559-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="97559-107">本教學課程中，在您開始學習使用的 hello 基本[IoT 閘道入門套件](https://aka.ms/gateway-kit)。</span><span class="sxs-lookup"><span data-stu-id="97559-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="97559-108">您將使用執行 Wind River Linux 的 Intel NUC。</span><span class="sxs-lookup"><span data-stu-id="97559-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="97559-109">您將學習如何 tooseamleesly 連接您的裝置 toohello 雲端使用 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="97559-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="97559-110">**沒有套件嗎？**按一下[這裡](https://aka.ms/gateway-kit)。</span><span class="sxs-lookup"><span data-stu-id="97559-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="97559-111">第 1 課：設定 NUC</span><span class="sxs-lookup"><span data-stu-id="97559-111">Lesson 1: Configure your NUC</span></span>
![第 1 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="97559-113">在這一課，您可以設定 hello 套件作為 Azure IoT 閘道 （下一個單位的運算） 的 Intel NUC、 NUC，在安裝 hello Azure IoT 邊緣套件並執行範例應用程式 tooverify hello 閘道功能。</span><span class="sxs-lookup"><span data-stu-id="97559-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="97559-114">*估計時間 toocomplete: 15 分鐘*</span><span class="sxs-lookup"><span data-stu-id="97559-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="97559-115">跳過[Intel NUC 為 IoT 閘道設定](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="97559-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="97559-116">第 2 課：建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="97559-116">Lesson 2: Create your IoT Hub</span></span>
![第 2 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="97559-118">在這一課，您在主機電腦上安裝 hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="97559-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="97559-119">然後您建立免費的 Azure 帳戶、 佈建您的 Azure IoT 中樞和 hello IoT 中樞中建立您的第一個裝置。</span><span class="sxs-lookup"><span data-stu-id="97559-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="97559-120">開始本課程前，請先完成第 1 課。</span><span class="sxs-lookup"><span data-stu-id="97559-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="97559-121">取得 hello 工具</span><span class="sxs-lookup"><span data-stu-id="97559-121">Get hello tools</span></span>
<span data-ttu-id="97559-122">主機電腦上安裝 hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="97559-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="97559-123">*估計時間 toocomplete: 20 分鐘*</span><span class="sxs-lookup"><span data-stu-id="97559-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="97559-124">跳過[取得 hello 工具](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="97559-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="97559-125">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="97559-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="97559-126">建立資源群組中，佈建第一個的 Azure IoT 中樞，並加入使用 hello Azure CLI 您第一次裝置 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="97559-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="97559-127">*估計時間 toocomplete: 10 分鐘*</span><span class="sxs-lookup"><span data-stu-id="97559-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="97559-128">跳過[建立 IoT 中樞，並註冊您的裝置](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="97559-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="97559-129">第 3 課： 從 hello 模擬裝置接收訊息，並從 IoT 中樞讀取訊息</span><span class="sxs-lookup"><span data-stu-id="97559-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="97559-130">在這一課，您將使用指令碼 tooautomate hello 組態和模擬的裝置應用程式的執行在您的閘道。</span><span class="sxs-lookup"><span data-stu-id="97559-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="97559-131">hello 模擬的裝置應用程式會產生範例溫度資料，並將它傳送 tooan IoT 中樞模組。</span><span class="sxs-lookup"><span data-stu-id="97559-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="97559-132">hello 收到 hello 資料，並將它的 Azure IoT Edge 傳送 tooyour IoT 中樞透過 hello 閘道架構提供 IoT 中樞模組封裝。</span><span class="sxs-lookup"><span data-stu-id="97559-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![第 3 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="97559-134">設定並執行模擬裝置</span><span class="sxs-lookup"><span data-stu-id="97559-134">Configure and run a simulated device</span></span>
<span data-ttu-id="97559-135">準備 hello 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="97559-135">Prepare hello sample codes.</span></span> <span data-ttu-id="97559-136">然後設定及執行 hello 模擬裝置的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="97559-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="97559-137">*估計時間 toocomplete: 15 分鐘*</span><span class="sxs-lookup"><span data-stu-id="97559-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="97559-138">跳過[設定及執行模擬的裝置](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="97559-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="97559-139">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="97559-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="97559-140">在主機電腦 tooread hello 訊息上執行範例程式碼，從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="97559-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="97559-141">*估計時間 toocomplete: 15 分鐘*</span><span class="sxs-lookup"><span data-stu-id="97559-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="97559-142">跳過[從 IoT 中樞讀取訊息](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="97559-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="97559-143">第 4 課： 將訊息儲存 tooAzure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="97559-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="97559-144">建立從 IoT 中樞取得內送訊息，並將其寫入 tooAzure 資料表儲存體的 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="97559-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![第 4 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="97559-146">建立 Azure 函數應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="97559-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="97559-147">Azure 的函式應用程式與 Azure 儲存體帳戶，請使用 Azure Resource Manager 範本 toocreate。</span><span class="sxs-lookup"><span data-stu-id="97559-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="97559-148">*估計時間 toocomplete: 10 分鐘*</span><span class="sxs-lookup"><span data-stu-id="97559-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="97559-149">跳過[建立 Azure 的函式應用程式與 Azure 儲存體帳戶](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="97559-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="97559-150">讀取保存在 Azure 表格儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="97559-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="97559-151">當寫入 tooAzure 資料表儲存體監視 hello 閘道到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="97559-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="97559-152">*估計時間 toocomplete: 5 分鐘*</span><span class="sxs-lookup"><span data-stu-id="97559-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="97559-153">跳過[讀取訊息保存在 Azure 資料表儲存體](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="97559-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="97559-154">疑難排解</span><span class="sxs-lookup"><span data-stu-id="97559-154">Troubleshooting</span></span>
<span data-ttu-id="97559-155">如果您在 hello 課程期間有任何問題，尋找在 hello 解決方案[疑難排解](iot-hub-gateway-kit-c-sim-troubleshooting.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="97559-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="97559-156">探索更多</span><span class="sxs-lookup"><span data-stu-id="97559-156">Explore more</span></span>
<span data-ttu-id="97559-157">請瀏覽 hello [Intel IoT 閘道套件開發人員區域](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="97559-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
