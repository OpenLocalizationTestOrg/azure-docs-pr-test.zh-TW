---
title: "將 Raspberry Pi (C) 連接到 Azure IoT - 第 3 課：執行範例 | Microsoft Docs"
description: "將範例應用程式部署至 Raspberry Pi 3 裝置，並執行該應用程式以傳送訊息至 IoT 中樞並讓 LED 閃爍。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "閃爍 led 雲端 pi, 來自雲端的 led 閃爍"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e583ba455a94f9afcc7b31e49425b518d7968919
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="8013d-104">執行範例應用程式以傳送裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="8013d-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8013d-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="8013d-105">What you will do</span></span>
<span data-ttu-id="8013d-106">本文將說明如何將範例應用程式部署至 Raspberry Pi 3，並執行該應用程式以傳送訊息至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8013d-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="8013d-107">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="8013d-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8013d-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="8013d-108">What you will learn</span></span>
<span data-ttu-id="8013d-109">您將了解如何使用 gulp 工具將範例 Node.js 應用程式部署在 Pi 上並執行。</span><span class="sxs-lookup"><span data-stu-id="8013d-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8013d-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="8013d-110">What you need</span></span>
* <span data-ttu-id="8013d-111">開始這項工作之前，您必須先成功完成[建立 Azure 函式應用程式與儲存體帳戶以處理與儲存 IoT 中樞訊息](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="8013d-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="8013d-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="8013d-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="8013d-113">Pi 使用此裝置連接字串來連接至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8013d-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="8013d-114">IoT 中樞連接字串是用來連接到 IoT 中樞中的身分識別登錄，以便管理可連接到 IoT 中樞的裝置。</span><span class="sxs-lookup"><span data-stu-id="8013d-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="8013d-115">執行下列 Azure CLI 命令，列出您的資源群組中的所有 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="8013d-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="8013d-116">如果您未變更值，請使用 `iot-sample` 作為 `{resource group name}` 的值。</span><span class="sxs-lookup"><span data-stu-id="8013d-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="8013d-117">執行下列 Azure CLI 命令取得 IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="8013d-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="8013d-118">`{my hub name}` 是您建立 IoT 中樞並登錄 Pi 時所指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="8013d-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="8013d-119">執行下列命令來取得裝置連接字串：</span><span class="sxs-lookup"><span data-stu-id="8013d-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="8013d-120">如果您未變更值，請使用 `myraspberrypi` 作為 `{device id}` 的值。</span><span class="sxs-lookup"><span data-stu-id="8013d-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="8013d-121">設定裝置連線</span><span class="sxs-lookup"><span data-stu-id="8013d-121">Configure the device connection</span></span>
1. <span data-ttu-id="8013d-122">執行下列命令初始化組態檔：</span><span class="sxs-lookup"><span data-stu-id="8013d-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="8013d-123">也請執行 **gulp install-tools** (如果您未在第 1 課這麼做)。</span><span class="sxs-lookup"><span data-stu-id="8013d-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="8013d-124">執行下列命令在 Visual Studio Code 中開啟裝置組態檔 `config-raspberrypi.json`：</span><span class="sxs-lookup"><span data-stu-id="8013d-124">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="8013d-126">在 `config-raspberrypi.json` 檔案中進行下列取代：</span><span class="sxs-lookup"><span data-stu-id="8013d-126">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="8013d-127">以您從 `device-discovery-cli` 取得的裝置 IP 位置或主機名稱，或以設定裝置時所繼承的值，來取代 **[device hostname or IP address]**。</span><span class="sxs-lookup"><span data-stu-id="8013d-127">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="8013d-128">以您取得的 `device connection string` 來取代 **[IoT device connection string]**。</span><span class="sxs-lookup"><span data-stu-id="8013d-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="8013d-129">以您取得的 `iot hub connection string` 來取代 **[IoT hub connection string]**。</span><span class="sxs-lookup"><span data-stu-id="8013d-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="8013d-130">您在本文中不需要 `azure_storage_connection_string`。</span><span class="sxs-lookup"><span data-stu-id="8013d-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="8013d-131">請讓它保持原狀。</span><span class="sxs-lookup"><span data-stu-id="8013d-131">Keep it as is.</span></span>

<span data-ttu-id="8013d-132">更新 `config-raspberrypi.json` 檔案，讓您能夠從電腦部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="8013d-132">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="8013d-133">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="8013d-133">Deploy and run the sample application</span></span>
<span data-ttu-id="8013d-134">執行下列命令，以在 Pi 上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="8013d-134">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="8013d-135">確認範例應用程式可運作</span><span class="sxs-lookup"><span data-stu-id="8013d-135">Verify that the sample application works</span></span>
<span data-ttu-id="8013d-136">您應該會看到與 Pi 連接的 LED 每兩秒閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="8013d-136">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="8013d-137">每次 LED 閃爍時，範例應用程式就會將訊息傳送至 IoT 中樞，並驗證該訊息已成功傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8013d-137">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="8013d-138">此外，IoT 中樞所收到的每則訊息都會列印在主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="8013d-138">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="8013d-139">在傳送 20 則訊息後，範例應用程式會自動終止。</span><span class="sxs-lookup"><span data-stu-id="8013d-139">The sample application terminates automatically after sending 20 messages.</span></span>

![具有所傳送和接收之訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="8013d-141">摘要</span><span class="sxs-lookup"><span data-stu-id="8013d-141">Summary</span></span>
<span data-ttu-id="8013d-142">您已在 Pi 上部署新的閃爍範例應用程式，並執行該應用程式以將裝置到雲端訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8013d-142">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="8013d-143">現在，您可以在訊息寫入儲存體帳戶時加以監視。</span><span class="sxs-lookup"><span data-stu-id="8013d-143">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8013d-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8013d-144">Next steps</span></span>
[<span data-ttu-id="8013d-145">讀取保留在 Azure 儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="8013d-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

