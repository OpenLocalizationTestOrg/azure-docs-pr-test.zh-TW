---
title: "將 Intel Edison (節點) 連接到 Azure IoT - 第 3 課：傳送訊息 | Microsoft Docs"
description: "將範例應用程式部署至 Intel Edison 裝置，並執行該應用程式以傳送訊息至 IoT 中樞並讓 LED 閃爍。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 雲端服務, arduino 傳送資料到雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d4b520b9a1852a285b1e10b5b35447a54313af9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="167a7-104">執行範例應用程式以傳送裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="167a7-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="167a7-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="167a7-105">What you will do</span></span>
<span data-ttu-id="167a7-106">本文將說明如何將範例應用程式部署至 Intel Edison，並執行該應用程式以傳送訊息至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="167a7-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="167a7-107">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="167a7-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="167a7-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="167a7-108">What you will learn</span></span>
<span data-ttu-id="167a7-109">您將了解如何使用 gulp 工具將範例 C 應用程式部署在 Edison 上並執行。</span><span class="sxs-lookup"><span data-stu-id="167a7-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="167a7-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="167a7-110">What you need</span></span>
* <span data-ttu-id="167a7-111">開始這項工作之前，您必須先成功完成[建立 Azure 函式應用程式與儲存體帳戶以處理與儲存 IoT 中樞訊息][process-and-store-iot-hub-messages]。</span><span class="sxs-lookup"><span data-stu-id="167a7-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="167a7-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="167a7-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="167a7-113">裝置連接字串用於將 Edison 連線至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="167a7-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="167a7-114">IoT 中樞連接字串用於將 IoT 中樞連線至在 IoT 中樞內代表 Edison 的裝置識別。</span><span class="sxs-lookup"><span data-stu-id="167a7-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="167a7-115">執行下列 Azure CLI 命令，列出您的資源群組中的所有 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="167a7-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="167a7-116">如果您未變更值，請使用 `iot-sample` 作為 `{resource group name}` 的值。</span><span class="sxs-lookup"><span data-stu-id="167a7-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="167a7-117">執行下列 Azure CLI 命令取得 IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="167a7-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="167a7-118">`{my hub name}` 是您建立 IoT 中樞並登錄 Edison 時所指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="167a7-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="167a7-119">執行下列命令來取得裝置連接字串：</span><span class="sxs-lookup"><span data-stu-id="167a7-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="167a7-120">如果您未變更值，請使用 `myinteledison` 作為 `{device id}` 的值。</span><span class="sxs-lookup"><span data-stu-id="167a7-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="167a7-121">設定裝置連線</span><span class="sxs-lookup"><span data-stu-id="167a7-121">Configure the device connection</span></span>
1. <span data-ttu-id="167a7-122">執行下列命令初始化組態檔：</span><span class="sxs-lookup"><span data-stu-id="167a7-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="167a7-123">執行下列命令在 Visual Studio Code 中開啟裝置組態檔 `config-edison.json`：</span><span class="sxs-lookup"><span data-stu-id="167a7-123">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="167a7-125">在 `config-edison.json` 檔案中進行下列取代：</span><span class="sxs-lookup"><span data-stu-id="167a7-125">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="167a7-126">以您設定裝置時所記下的裝置 IP 位址來取代 **[device hostname or IP address]**。</span><span class="sxs-lookup"><span data-stu-id="167a7-126">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="167a7-127">以您取得的 `device connection string` 來取代 **[IoT device connection string]**。</span><span class="sxs-lookup"><span data-stu-id="167a7-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="167a7-128">以您取得的 `iot hub connection string` 來取代 **[IoT hub connection string]**。</span><span class="sxs-lookup"><span data-stu-id="167a7-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="167a7-129">您在本文中不需要 `azure_storage_connection_string`。</span><span class="sxs-lookup"><span data-stu-id="167a7-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="167a7-130">請讓它保持原狀。</span><span class="sxs-lookup"><span data-stu-id="167a7-130">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="167a7-131">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="167a7-131">Deploy and run the sample application</span></span>
<span data-ttu-id="167a7-132">執行下列命令，在 Edison 上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="167a7-132">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="167a7-133">確認範例應用程式可運作</span><span class="sxs-lookup"><span data-stu-id="167a7-133">Verify that the sample application works</span></span>
<span data-ttu-id="167a7-134">您應該會看到與 Edison 連接的 LED 每兩秒閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="167a7-134">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="167a7-135">每次 LED 閃爍時，範例應用程式就會將訊息傳送至 IoT 中樞，並驗證該訊息已成功傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="167a7-135">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="167a7-136">此外，IoT 中樞所收到的每則訊息都會列印在主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="167a7-136">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="167a7-137">在傳送 20 則訊息後，範例應用程式會自動終止。</span><span class="sxs-lookup"><span data-stu-id="167a7-137">The sample application terminates automatically after sending 20 messages.</span></span>

![具有所傳送和接收之訊息的範例應用程式][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="167a7-139">摘要</span><span class="sxs-lookup"><span data-stu-id="167a7-139">Summary</span></span>
<span data-ttu-id="167a7-140">您已在 Edison 上部署新的閃爍範例應用程式，並執行該應用程式以將裝置到雲端訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="167a7-140">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="167a7-141">現在，您可以在訊息寫入儲存體帳戶時加以監視。</span><span class="sxs-lookup"><span data-stu-id="167a7-141">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="167a7-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="167a7-142">Next steps</span></span>
<span data-ttu-id="167a7-143">[讀取保存在 Azure 儲存體中的訊息][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="167a7-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md