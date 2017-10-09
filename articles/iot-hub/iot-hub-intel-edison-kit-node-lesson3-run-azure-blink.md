---
title: "連接 （節點） 的 Intel Edison tooAzure IoT-第 3 課： 將訊息傳送 |Microsoft 文件"
description: "部署和執行範例應用程式 tooIntel Edison 傳送訊息 tooyour IoT 中樞和閃爍 hello LED。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 雲端服務，arduino 傳送資料 toocloud"
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
ms.openlocfilehash: ebd4c7558544d64086fb4cd615cee546aeed2fc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="2c4af-104">執行範例應用程式 toosend 裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="2c4af-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="2c4af-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="2c4af-105">What you will do</span></span>
<span data-ttu-id="2c4af-106">本文將告訴您 toodeploy 及執行範例應用程式上傳送的 Intel Edison 訊息 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2c4af-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="2c4af-107">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="2c4af-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2c4af-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="2c4af-108">What you will learn</span></span>
<span data-ttu-id="2c4af-109">您將學習如何 toouse hello 的 gulp 工具 toodeploy 並 Edison 上執行 hello 範例 C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c4af-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2c4af-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="2c4af-110">What you need</span></span>
* <span data-ttu-id="2c4af-111">在開始這項工作之前，您必須已順利完成[建立 Azure 的函式應用程式與儲存體帳戶 tooprocess 和市集 IoT 中樞訊息][process-and-store-iot-hub-messages]。</span><span class="sxs-lookup"><span data-stu-id="2c4af-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="2c4af-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="2c4af-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="2c4af-113">hello 裝置連接字串是使用的 tooconnect Edison tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2c4af-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="2c4af-114">hello IoT 中樞連接字串是使用的 tooconnect 您 IoT 中樞 toohello 裝置身分識別代表 Edison hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2c4af-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="2c4af-115">列出資源群組中的所有您 IoT 中樞執行下列 Azure CLI 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c4af-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="2c4af-116">使用`iot-sample`做為 hello 值`{resource group name}`如果您沒有變更 hello 值。</span><span class="sxs-lookup"><span data-stu-id="2c4af-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="2c4af-117">藉由執行下列 Azure CLI 命令的 hello 收到 hello IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="2c4af-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="2c4af-118">`{my hub name}`這是您指定當您建立 IoT 中樞，並註冊 Edison hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2c4af-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="2c4af-119">藉由執行下列命令的 hello 收到 hello 裝置連接字串：</span><span class="sxs-lookup"><span data-stu-id="2c4af-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="2c4af-120">使用`myinteledison`做為 hello 值`{device id}`如果您沒有變更 hello 值。</span><span class="sxs-lookup"><span data-stu-id="2c4af-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="2c4af-121">設定 hello 裝置連線</span><span class="sxs-lookup"><span data-stu-id="2c4af-121">Configure hello device connection</span></span>
1. <span data-ttu-id="2c4af-122">藉由執行下列命令的 hello 初始化 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="2c4af-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="2c4af-123">開啟 hello 裝置組態檔`config-edison.json`在 Visual Studio 程式碼執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c4af-123">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="2c4af-125">請遵循取代 hello hello`config-edison.json`檔案：</span><span class="sxs-lookup"><span data-stu-id="2c4af-125">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="2c4af-126">取代**[裝置的主機名稱或 IP 位址]** hello 裝置的 IP 位址設定您的裝置時關閉標記。</span><span class="sxs-lookup"><span data-stu-id="2c4af-126">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="2c4af-127">取代**[IoT 裝置連接字串]**以 hello`device connection string`您取得的。</span><span class="sxs-lookup"><span data-stu-id="2c4af-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="2c4af-128">取代**[IoT 中樞連接字串]**以 hello`iot hub connection string`您取得的。</span><span class="sxs-lookup"><span data-stu-id="2c4af-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2c4af-129">您在本文中不需要 `azure_storage_connection_string`。</span><span class="sxs-lookup"><span data-stu-id="2c4af-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="2c4af-130">請讓它保持原狀。</span><span class="sxs-lookup"><span data-stu-id="2c4af-130">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="2c4af-131">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="2c4af-131">Deploy and run hello sample application</span></span>
<span data-ttu-id="2c4af-132">部署和執行下列命令的 hello Edison 執行 hello 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="2c4af-132">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="2c4af-133">確認 hello 範例應用程式可正常運作</span><span class="sxs-lookup"><span data-stu-id="2c4af-133">Verify that hello sample application works</span></span>
<span data-ttu-id="2c4af-134">您應該會看到 hello LED 所連接的 tooEdison 閃爍每隔兩秒鐘。</span><span class="sxs-lookup"><span data-stu-id="2c4af-134">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="2c4af-135">每次 hello LED 閃爍，hello 範例應用程式傳送訊息 tooyour IoT 中樞，並確認該 hello 訊息已成功傳送 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2c4af-135">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="2c4af-136">此外，收到 hello IoT 中樞的每個訊息會列印 hello 主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="2c4af-136">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="2c4af-137">hello 範例應用程式會自動終止後傳送 20 則訊息。</span><span class="sxs-lookup"><span data-stu-id="2c4af-137">hello sample application terminates automatically after sending 20 messages.</span></span>

![具有所傳送和接收之訊息的範例應用程式][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="2c4af-139">摘要</span><span class="sxs-lookup"><span data-stu-id="2c4af-139">Summary</span></span>
<span data-ttu-id="2c4af-140">您已部署，而且執行 Edison toosend 裝置到雲端訊息 tooyour IoT 中樞 hello 新閃爍範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c4af-140">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="2c4af-141">您現在監視您的郵件將它們寫入 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c4af-141">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c4af-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c4af-142">Next steps</span></span>
<span data-ttu-id="2c4af-143">[讀取保存在 Azure 儲存體中的訊息][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="2c4af-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md