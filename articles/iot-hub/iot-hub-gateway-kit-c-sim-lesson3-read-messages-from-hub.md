---
title: "模擬裝置與 Azure IoT 閘道 - 第 3 課：讀取訊息 | Microsoft Docs"
description: "在主機電腦 tooread hello 訊息上執行範例程式碼，從 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 雲端、 雲端資料收集、 iot 雲端服務、 iot 資料中的資料"
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
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="6cfe4-104">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="6cfe4-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6cfe4-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="6cfe4-105">What you will do</span></span>

- <span data-ttu-id="6cfe4-106">執行範例程式碼在您的主機電腦 tooread 訊息從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="6cfe4-107">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6cfe4-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="6cfe4-108">What you will learn</span></span>

<span data-ttu-id="6cfe4-109">如何 toouse hello 的 gulp 工具 tooread 訊息從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6cfe4-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="6cfe4-110">What you need</span></span>

- <span data-ttu-id="6cfe4-111">中的 hello 模擬的裝置範例[設定及執行模擬的裝置雲端範例應用程式上傳](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="6cfe4-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="6cfe4-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="6cfe4-113">hello 裝置連接字串會使用模擬的裝置 tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="6cfe4-114">hello IoT 中樞連接字串是使用的 tooconnect toohello 身分識別登錄在 IoT 中樞 toomanage hello 裝置允許 tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="6cfe4-115">列出資源群組中的所有您 IoT 中樞執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cfe4-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="6cfe4-116">使用`iot-gateway`做為 hello 值`{resource group name}`如果您沒有變更它。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="6cfe4-117">藉由執行下列命令的 hello 收到 hello IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="6cfe4-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="6cfe4-118">`{my hub name}`這是您在第 2 課中指定的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="6cfe4-119">設定 hello hello 範例程式碼的裝置連線</span><span class="sxs-lookup"><span data-stu-id="6cfe4-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="6cfe4-120">更新中的 IoT 中樞與裝置連線組態`config-azure.json`藉由執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cfe4-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="6cfe4-121">開啟`config-azure.json`在 Visual Studio 程式碼執行下列命令，在主控台視窗中的 hello:</span><span class="sxs-lookup"><span data-stu-id="6cfe4-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="6cfe4-122">請遵循取代 hello hello`config-azure.json`檔案：</span><span class="sxs-lookup"><span data-stu-id="6cfe4-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![設定 azure 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="6cfe4-124">取代`[IoT hub connection string]`以 hello IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="6cfe4-125">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="6cfe4-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="6cfe4-126">執行 hello 模擬裝置的範例應用程式，並讀取 IoT 中樞訊息 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cfe4-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="6cfe4-127">hello 命令會執行每 2 秒會傳送訊息 tooyour IoT 中樞的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="6cfe4-128">它也會繁衍子處理序 tooreceive hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="6cfe4-129">hello 訊息傳送，而且收到相同主控台視窗中的所有顯示立即在 hello hello 主機電腦。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="6cfe4-130">hello 應用程式將會結束 40 秒中。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-130">hello application will exit in 40 seconds.</span></span>

![模擬的範例應用程式及傳送和接收的訊息](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="6cfe4-132">摘要</span><span class="sxs-lookup"><span data-stu-id="6cfe4-132">Summary</span></span>

<span data-ttu-id="6cfe4-133">您已成功地執行 hello 範例應用程式 toosend 資料 tooyour IoT 中樞，與模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="6cfe4-134">您也閱讀 tooyour IoT 中心已傳送 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="6cfe4-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cfe4-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cfe4-135">Next steps</span></span>
[<span data-ttu-id="6cfe4-136">建立 Azure 函數應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6cfe4-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


