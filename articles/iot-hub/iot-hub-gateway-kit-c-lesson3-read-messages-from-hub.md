---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 3 課：讀取訊息 | Microsoft Docs"
description: "在主機電腦上執行範例程式碼，以讀取來自 IoT 中樞的傳入訊息。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "在雲端的資料, 雲端資料收集, iot 雲端服務, iot 資料"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 45f3595c4848d5c283cdf95604adf8d2c8d6a809
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="55ab9-104">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="55ab9-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="55ab9-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="55ab9-105">What you will do</span></span>

- <span data-ttu-id="55ab9-106">在主機電腦上執行範例程式碼，以讀取來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="55ab9-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="55ab9-107">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="55ab9-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="55ab9-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="55ab9-108">What you will learn</span></span>

<span data-ttu-id="55ab9-109">如何使用 gulp 工具讀取來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="55ab9-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="55ab9-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="55ab9-110">What you need</span></span>

- <span data-ttu-id="55ab9-111">您在第 3 課執行成功的 BLE 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="55ab9-111">The BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="55ab9-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="55ab9-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="55ab9-113">您的裝置 (TI SensorTag 或模擬裝置) 會使用此裝置連接字串連接到您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="55ab9-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span></span> <span data-ttu-id="55ab9-114">IoT 中樞連接字串是用來連接到 IoT 中樞中的身分識別登錄，以便管理可連接到 IoT 中樞的裝置。</span><span class="sxs-lookup"><span data-stu-id="55ab9-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="55ab9-115">執行下列命令，列出您的資源群組中的所有 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="55ab9-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="55ab9-116">如果您未變更值，請使用 `iot-gateway` 作為 `{resource group name}` 的值。</span><span class="sxs-lookup"><span data-stu-id="55ab9-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span></span>
- <span data-ttu-id="55ab9-117">執行下列命令來取得 IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="55ab9-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="55ab9-118">`{my hub name}` 是您在第 2 課中指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="55ab9-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="55ab9-119">設定範例應用程式的裝置連線</span><span class="sxs-lookup"><span data-stu-id="55ab9-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="55ab9-120">更新裝置的組態檔 `config-azure.json`，使您能夠在主機電腦上讀取來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="55ab9-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="55ab9-121">若要這樣做，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="55ab9-121">To do this, follow these steps:</span></span>

1. <span data-ttu-id="55ab9-122">在主控台視窗中執行下列命令，在 Visual Studio Code 中開啟 `config-azure.json`︰</span><span class="sxs-lookup"><span data-stu-id="55ab9-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="55ab9-123">在 `config-azure.json` 檔案中進行下列取代：</span><span class="sxs-lookup"><span data-stu-id="55ab9-123">Make the following replacements in the `config-azure.json` file:</span></span>

   ![設定 azure 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="55ab9-125">將 `[IoT hub connection string]` 取代為您取得的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="55ab9-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="55ab9-126">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="55ab9-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="55ab9-127">如果您有 TI SensorTag，請確定您已開啟 SensorTag。</span><span class="sxs-lookup"><span data-stu-id="55ab9-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="55ab9-128">執行閘道器範例應用程式，並使用下列命令讀取 IoT 中樞訊息︰</span><span class="sxs-lookup"><span data-stu-id="55ab9-128">Run the gateway sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="55ab9-129">此命令會執行 BLE 範例應用程式，此程式會讀取及封裝來自 SensorTag 或模擬裝置的溫度資料，且每 2 秒會將訊息傳送至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="55ab9-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="55ab9-130">它也會繁衍子程序來接收訊息。</span><span class="sxs-lookup"><span data-stu-id="55ab9-130">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="55ab9-131">傳送和接收的所有訊息皆會立即顯示在主機電腦的同一主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="55ab9-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="55ab9-132">範例應用程式執行個體會在 40 秒後自動終止。</span><span class="sxs-lookup"><span data-stu-id="55ab9-132">The sample application instance will terminate automatically in 40 seconds.</span></span>

![BLE 範例應用程式及傳送和接收的訊息](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="55ab9-134">摘要</span><span class="sxs-lookup"><span data-stu-id="55ab9-134">Summary</span></span>

<span data-ttu-id="55ab9-135">您已執行範例程式碼來讀取來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="55ab9-135">You've run a sample code to read messages from your IoT hub.</span></span> <span data-ttu-id="55ab9-136">您可以開始讀取儲存在 Azure 表格儲存體中的訊息。</span><span class="sxs-lookup"><span data-stu-id="55ab9-136">You're ready to read the messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55ab9-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55ab9-137">Next steps</span></span>
[<span data-ttu-id="55ab9-138">建立 Azure 函數應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="55ab9-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


