---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 3 課：讀取訊息 | Microsoft Docs"
description: "在主機電腦 tooread hello 訊息上執行範例程式碼，從 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 雲端、 雲端資料收集、 iot 雲端服務、 iot 資料中的資料"
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
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="d1a26-104">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="d1a26-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d1a26-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="d1a26-105">What you will do</span></span>

- <span data-ttu-id="d1a26-106">執行範例程式碼在您的主機電腦 tooread 訊息從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d1a26-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="d1a26-107">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="d1a26-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d1a26-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="d1a26-108">What you will learn</span></span>

<span data-ttu-id="d1a26-109">如何 toouse hello 的 gulp 工具 tooread 訊息從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d1a26-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d1a26-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="d1a26-110">What you need</span></span>

- <span data-ttu-id="d1a26-111">hello 第 3 課順利執行 b 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1a26-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="d1a26-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="d1a26-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="d1a26-113">hello 裝置連接字串會使用您的裝置 （TI SensorTag 或模擬的裝置） tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d1a26-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="d1a26-114">hello IoT 中樞連接字串是使用的 tooconnect toohello 身分識別登錄在 IoT 中樞 toomanage hello 裝置允許 tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d1a26-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="d1a26-115">列出資源群組中的所有您 IoT 中樞執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1a26-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="d1a26-116">使用`iot-gateway`做為 hello 值`{resource group name}`如果您沒有變更 hello 值。</span><span class="sxs-lookup"><span data-stu-id="d1a26-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="d1a26-117">藉由執行下列命令的 hello 收到 hello IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="d1a26-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="d1a26-118">`{my hub name}`這是您在第 2 課中指定的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d1a26-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="d1a26-119">設定 hello hello 範例程式碼的裝置連線</span><span class="sxs-lookup"><span data-stu-id="d1a26-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="d1a26-120">更新 hello 裝置的組態檔`config-azure.json`，使您能夠從 IoT 中樞讀取訊息，主機電腦上。</span><span class="sxs-lookup"><span data-stu-id="d1a26-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="d1a26-121">toodo，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1a26-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="d1a26-122">開啟`config-azure.json`在 Visual Studio 程式碼執行下列命令，在主控台視窗中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d1a26-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="d1a26-123">請遵循取代 hello hello`config-azure.json`檔案：</span><span class="sxs-lookup"><span data-stu-id="d1a26-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![設定 azure 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="d1a26-125">取代`[IoT hub connection string]`以 hello 您取得的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="d1a26-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="d1a26-126">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="d1a26-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="d1a26-127">如果您有 TI SensorTag，請確定您已開啟 SensorTag。</span><span class="sxs-lookup"><span data-stu-id="d1a26-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="d1a26-128">執行 hello 閘道範例應用程式，並讀取 IoT 中樞訊息 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1a26-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="d1a26-129">hello 命令執行 hello b 範例應用程式讀取並從 SensorTag 或模擬的裝置溫度資料封裝，然後每 2 秒會傳送 hello 訊息 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d1a26-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="d1a26-130">它也會繁衍子處理序 tooreceive hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="d1a26-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="d1a26-131">hello 訊息傳送，而且收到相同主控台視窗中的所有顯示立即在 hello hello 主機電腦。</span><span class="sxs-lookup"><span data-stu-id="d1a26-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="d1a26-132">hello 範例應用程式執行個體將會自動在 40 秒終止。</span><span class="sxs-lookup"><span data-stu-id="d1a26-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![BLE 範例應用程式及傳送和接收的訊息](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="d1a26-134">摘要</span><span class="sxs-lookup"><span data-stu-id="d1a26-134">Summary</span></span>

<span data-ttu-id="d1a26-135">您已從 IoT 中樞執行範例程式碼 tooread 訊息。</span><span class="sxs-lookup"><span data-stu-id="d1a26-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="d1a26-136">您已準備好 tooread hello 訊息儲存在您的 Azure 資料表儲存體中。</span><span class="sxs-lookup"><span data-stu-id="d1a26-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1a26-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1a26-137">Next steps</span></span>
[<span data-ttu-id="d1a26-138">建立 Azure 函數應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d1a26-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


