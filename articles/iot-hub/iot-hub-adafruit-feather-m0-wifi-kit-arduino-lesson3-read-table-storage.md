---
title: "Connect Arduino (C) tooAzure IoT-第 3 課： 資料表儲存體 |Microsoft 文件"
description: "當寫入 tooyour Azure 資料表儲存體監視 hello 裝置到雲端訊息。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 雲端、 雲端資料收集、 iot 雲端服務、 iot 資料中的資料"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="a9a23-104">讀取保存在 Azure 儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="a9a23-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a9a23-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="a9a23-105">What you will do</span></span>
<span data-ttu-id="a9a23-106">監視從 Adafruit 羽毛 M0 WiFi Arduino 面板 tooyour IoT 中樞傳送 hello 訊息為 hello 裝置到雲端訊息會寫入 tooyour Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="a9a23-106">Monitor hello device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span>

<span data-ttu-id="a9a23-107">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="a9a23-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a9a23-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="a9a23-108">What you will learn</span></span>
<span data-ttu-id="a9a23-109">在本文中，您將學習如何 toouse hello gulp 讀取訊息工作 tooread 訊息保存在您的 Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="a9a23-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a9a23-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="a9a23-110">What you need</span></span>
<span data-ttu-id="a9a23-111">才能開始此程序，您必須先成功完成[Arduino 面板上執行 hello Azure 閃爍範例應用程式][run-blink-application]。</span><span class="sxs-lookup"><span data-stu-id="a9a23-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="a9a23-112">從您的儲存體帳戶讀取新訊息</span><span class="sxs-lookup"><span data-stu-id="a9a23-112">Read new messages from your storage account</span></span>
<span data-ttu-id="a9a23-113">在 hello 前一篇文章中，您可以執行範例應用程式 Arduino 面板上。</span><span class="sxs-lookup"><span data-stu-id="a9a23-113">In hello previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="a9a23-114">hello 範例應用程式傳送訊息 tooyour Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a9a23-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="a9a23-115">傳送 tooyour IoT 中樞的 hello 訊息會儲存到您的 Azure 資料表儲存體，透過 hello Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9a23-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="a9a23-116">您必須從您的 Azure 資料表儲存體的 hello Azure 儲存體連接字串 tooread 訊息。</span><span class="sxs-lookup"><span data-stu-id="a9a23-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="a9a23-117">tooread 訊息儲存在您的 Azure 資料表儲存體，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a9a23-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="a9a23-118">藉由執行下列命令的 hello 收到 hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="a9a23-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="a9a23-119">hello 第一個命令會擷取 hello `storage name` hello 第二個命令 tooget hello 連接字串中使用。</span><span class="sxs-lookup"><span data-stu-id="a9a23-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="a9a23-120">使用`iot-sample`做為 hello 值`{resource group name}`如果您沒有變更 hello 值。</span><span class="sxs-lookup"><span data-stu-id="a9a23-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="a9a23-121">開啟 hello 設定檔`config-arduino.json`在 Visual Studio 程式碼執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a9a23-121">Open hello configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="a9a23-122">取代`[Azure storage connection string]`hello 您在步驟 1 中取得的連接字串。</span><span class="sxs-lookup"><span data-stu-id="a9a23-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="a9a23-123">儲存 hello`config-arduino.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="a9a23-123">Save hello `config-arduino.json` file.</span></span>
5. <span data-ttu-id="a9a23-124">重新傳送訊息，並從您的 Azure 資料表儲存體讀取透過執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a9a23-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="a9a23-125">hello 邏輯來讀取 Azure 資料表儲存體是在 hello`azure-table.js`檔案。</span><span class="sxs-lookup"><span data-stu-id="a9a23-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp-run]

## <a name="summary"></a><span data-ttu-id="a9a23-127">摘要</span><span class="sxs-lookup"><span data-stu-id="a9a23-127">Summary</span></span>
<span data-ttu-id="a9a23-128">您已成功連接 hello 雲端中的您 Arduino 面板 tooyour IoT 中樞，並使用 hello 閃爍範例應用程式 toosend 裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="a9a23-128">You've successfully connected your Arduino board tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="a9a23-129">您也會使用 hello Azure 函式應用程式 toostore 傳入 IoT 中樞訊息 tooyour Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="a9a23-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="a9a23-130">您現在可以從您的 IoT 中樞 tooyour Arduino 面板傳送雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="a9a23-130">You can now send cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9a23-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9a23-131">Next steps</span></span>
<span data-ttu-id="a9a23-132">[傳送雲端到裝置的訊息][send-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="a9a23-132">[Send cloud-to-device messages][send-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md