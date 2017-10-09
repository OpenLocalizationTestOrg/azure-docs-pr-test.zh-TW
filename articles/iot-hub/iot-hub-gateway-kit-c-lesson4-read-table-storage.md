---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 4 課：表格儲存體 | Microsoft Docs"
description: "從 Intel NUC tooyour IoT 中樞儲存訊息、 將它們寫入 tooAzure 資料表儲存體，然後讀取它們從 hello 雲端。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "從雲端擷取資料, iot 雲端服務"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="ad9ce-104">讀取保存在 Azure 表格儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="ad9ce-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ad9ce-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="ad9ce-105">What you will do</span></span>

- <span data-ttu-id="ad9ce-106">傳送訊息 tooyour IoT 中樞在閘道上執行 hello 閘道範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="ad9ce-107">在您的 Azure 資料表儲存體中的主機電腦 tooread hello 訊息，然後執行範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-107">Then run a sample code on your host computer tooread hello messages in your Azure Table storage.</span></span> 

<span data-ttu-id="ad9ce-108">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ad9ce-109">學習目標</span><span class="sxs-lookup"><span data-stu-id="ad9ce-109">What you will learn</span></span>

<span data-ttu-id="ad9ce-110">如何 toouse hello 的 gulp 工具 toorun hello 範例程式碼 tooread 訊息在您的 Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ad9ce-111">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="ad9ce-111">What you need</span></span>

<span data-ttu-id="ad9ce-112">您有已成功地完成下列工作 hello:</span><span class="sxs-lookup"><span data-stu-id="ad9ce-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="ad9ce-113">[建立 hello Azure 函式應用程式和 hello Azure 儲存體帳戶](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="ad9ce-114">[執行應用程式-閘道範例 hello](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="ad9ce-115">[讀取來自 IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="ad9ce-116">取得您的 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="ad9ce-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="ad9ce-117">稍早在本課程中，您已成功建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="ad9ce-118">hello Azure 儲存體帳戶，執行下列命令的 hello tooget hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="ad9ce-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="ad9ce-119">列出您的所有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="ad9ce-120">取得 Azure 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="ad9ce-121">當做 hello 值使用 iot 閘道`{resource group name}`如果您沒有變更 hello 課程 2 中的值。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-121">Use iot-gateway as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="ad9ce-122">設定 hello 裝置連線</span><span class="sxs-lookup"><span data-stu-id="ad9ce-122">Configure hello device connection</span></span>

<span data-ttu-id="ad9ce-123">更新 hello`config-azure.json`檔案，以便在 hello 主機電腦執行的 hello 範例程式碼可以讀取您的 Azure 資料表儲存體中的訊息。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="ad9ce-124">tooconfigure hello 裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ad9ce-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="ad9ce-125">開啟 hello 裝置組態檔`config-azure.json`藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ad9ce-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![組態](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="ad9ce-127">取代`[Azure storage connection string]`以 hello 您取得的 Azure 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="ad9ce-128">`[IoT hub connection string]` 應該已經在第 3 課的[讀取來自 Azure IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)中被取代。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="ad9ce-129">讀取 Azure 表格儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="ad9ce-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="ad9ce-130">執行 hello 閘道範例應用程式，並讀取 Azure 資料表儲存體訊息 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="ad9ce-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="ad9ce-131">IoT 中樞觸發您 Azure 函式的應用程式 toosave 訊息到您的 Azure 資料表儲存體，新訊息到達時。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="ad9ce-132">hello`gulp run`命令執行閘道範例應用程式所傳送訊息 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="ad9ce-133">與`table-storage`參數，它也會產生您的 Azure 資料表儲存體中儲存訊息的子處理序 tooreceive hello。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="ad9ce-134">hello 訊息傳送，而且收到相同主控台視窗中的所有顯示立即在 hello hello 主機電腦。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="ad9ce-135">hello 範例應用程式執行個體將會自動在 40 秒終止。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![gulp 讀取](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="ad9ce-137">摘要</span><span class="sxs-lookup"><span data-stu-id="ad9ce-137">Summary</span></span>

<span data-ttu-id="ad9ce-138">您已在您 Azure 函式應用程式所儲存的 Azure 資料表儲存體執行 hello 範例程式碼 tooread hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="ad9ce-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>
