---
title: "模擬裝置與 Azure IoT 閘道 - 第 3 課：讀取訊息 | Microsoft Docs"
description: "在主機電腦上執行範例程式碼，以讀取來自 IoT 中樞的傳入訊息。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "在雲端的資料, 雲端資料收集, iot 雲端服務, iot 資料"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="493e1-104">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="493e1-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="493e1-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="493e1-105">What you will do</span></span>

- <span data-ttu-id="493e1-106">在主機電腦上執行範例程式碼，以讀取來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="493e1-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="493e1-107">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="493e1-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="493e1-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="493e1-108">What you will learn</span></span>

<span data-ttu-id="493e1-109">如何使用 gulp 工具讀取來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="493e1-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="493e1-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="493e1-110">What you need</span></span>

- <span data-ttu-id="493e1-111">[設定及執行模擬裝置雲端上傳範例應用程式](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)中的模擬裝置。</span><span class="sxs-lookup"><span data-stu-id="493e1-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="493e1-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="493e1-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="493e1-113">您的模擬裝置會使用此裝置連接字串連接到您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="493e1-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="493e1-114">IoT 中樞連接字串是用來連接到 IoT 中樞中的身分識別登錄，以便管理可連接到 IoT 中樞的裝置。</span><span class="sxs-lookup"><span data-stu-id="493e1-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="493e1-115">執行下列命令，列出您的資源群組中的所有 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="493e1-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="493e1-116">如果您未變更值，請使用 `iot-gateway` 作為 `{resource group name}` 的值。</span><span class="sxs-lookup"><span data-stu-id="493e1-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="493e1-117">執行下列命令來取得 IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="493e1-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="493e1-118">`{my hub name}` 是您在第 2 課中指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="493e1-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="493e1-119">設定範例應用程式的裝置連線</span><span class="sxs-lookup"><span data-stu-id="493e1-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="493e1-120">執行下列步驟，更新 `config-azure.json` 中 IoT 中樞與裝置連線的組態︰</span><span class="sxs-lookup"><span data-stu-id="493e1-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="493e1-121">在主控台視窗中執行下列命令，在 Visual Studio Code 中開啟 `config-azure.json`︰</span><span class="sxs-lookup"><span data-stu-id="493e1-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="493e1-122">在 `config-azure.json` 檔案中進行下列取代：</span><span class="sxs-lookup"><span data-stu-id="493e1-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![設定 azure 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="493e1-124">將 `[IoT hub connection string]` 取代為 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="493e1-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="493e1-125">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="493e1-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="493e1-126">執行模擬裝置範例應用程式，並使用下列命令讀取 IoT 中樞訊息︰</span><span class="sxs-lookup"><span data-stu-id="493e1-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="493e1-127">此命令會執行此應用程式，應用程式每 2 秒會將訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="493e1-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="493e1-128">它也會繁衍子程序來接收訊息。</span><span class="sxs-lookup"><span data-stu-id="493e1-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="493e1-129">傳送和接收的所有訊息皆會立即顯示在主機電腦的同一主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="493e1-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="493e1-130">應用程式會在 40 秒後結束。</span><span class="sxs-lookup"><span data-stu-id="493e1-130">The application will exit in 40 seconds.</span></span>

![模擬的範例應用程式及傳送和接收的訊息](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="493e1-132">摘要</span><span class="sxs-lookup"><span data-stu-id="493e1-132">Summary</span></span>

<span data-ttu-id="493e1-133">您已成功執行範例應用程式，以模擬裝置將資料傳送至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="493e1-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="493e1-134">您也已經讀取傳送至 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="493e1-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="493e1-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="493e1-135">Next steps</span></span>
[<span data-ttu-id="493e1-136">建立 Azure 函數應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="493e1-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


