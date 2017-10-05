---
featureFlags: usabilla
title: "將 Raspberry Pi (節點) 連接到 Azure IoT - 第 3 課：表格儲存體 | Microsoft Docs"
description: "當裝置到雲端訊息寫入您的 Azure 表格儲存體時對其進行監視。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "從雲端擷取資料, iot 雲端服務"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 60084906c05ff9e5396f8e2378d73f7ac939d8df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="7fdca-104">讀取保存在 Azure 儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="7fdca-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="7fdca-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="7fdca-105">What you will do</span></span>
<span data-ttu-id="7fdca-106">當從 Raspberry Pi 3 傳送至 IoT 中樞的裝置到雲端訊息寫入您的 Azure 表格儲存體時，對其進行監視。</span><span class="sxs-lookup"><span data-stu-id="7fdca-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="7fdca-107">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="7fdca-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7fdca-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="7fdca-108">What you will learn</span></span>
<span data-ttu-id="7fdca-109">在本文中，您將了解如何使用 gulp 讀取訊息工作來讀取保留在您的 Azure 表格儲存體中的訊息。</span><span class="sxs-lookup"><span data-stu-id="7fdca-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7fdca-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="7fdca-110">What you need</span></span>
<span data-ttu-id="7fdca-111">開始此程序之前，您必須已成功完成[在 Raspberry Pi 3 中執行 Azure 閃爍範例應用程式](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)。</span><span class="sxs-lookup"><span data-stu-id="7fdca-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="7fdca-112">從您的儲存體帳戶讀取新訊息</span><span class="sxs-lookup"><span data-stu-id="7fdca-112">Read new messages from your storage account</span></span>
<span data-ttu-id="7fdca-113">在上一篇文章中，您在 Pi 上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fdca-113">In the previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="7fdca-114">範例應用程式會將訊息傳送至 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7fdca-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="7fdca-115">傳送至 IoT 中樞的訊息會透過 Azure 函式應用程式儲存至您的 Azure 表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="7fdca-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="7fdca-116">您需要 Azure 儲存體連接字串，來讀取您的 Azure 表格儲存體中的訊息。</span><span class="sxs-lookup"><span data-stu-id="7fdca-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="7fdca-117">若要讀取 Azure 表格儲存體中儲存的訊息，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="7fdca-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="7fdca-118">執行下列命令來取得連接字串：</span><span class="sxs-lookup"><span data-stu-id="7fdca-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="7fdca-119">第一個命令會擷取 `storage name`，在第二個命令中用來取得連接字串。</span><span class="sxs-lookup"><span data-stu-id="7fdca-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="7fdca-120">如果您未變更值，請使用 `iot-sample` 作為 `{resource group name}` 的值。</span><span class="sxs-lookup"><span data-stu-id="7fdca-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="7fdca-121">在 Visual Studio Code 中開啟組態檔 `config-raspberrypi.json`，方法是執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="7fdca-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="7fdca-122">將 `[Azure storage connection string]` 取代為您在步驟 1 中取得的連接字串。</span><span class="sxs-lookup"><span data-stu-id="7fdca-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="7fdca-123">儲存 `config-raspberrypi.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="7fdca-123">Save the `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="7fdca-124">重新傳送訊息並且從您的 Azure 表格儲存體中讀取它們，方法是執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="7fdca-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="7fdca-125">從 Azure 表格儲存體讀取的邏輯是在 `azure-table.js` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7fdca-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>
   
    ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a><span data-ttu-id="7fdca-127">摘要</span><span class="sxs-lookup"><span data-stu-id="7fdca-127">Summary</span></span>
<span data-ttu-id="7fdca-128">您已成功將 Pi 連接至雲端中的 IoT 中樞，並且使用閃爍範例應用程式以傳送裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="7fdca-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="7fdca-129">您也會使用 Azure 函式應用程式，將內送 IoT 中樞訊息儲存至 Azure 表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="7fdca-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="7fdca-130">現在，您可以從 IoT 中樞將雲端到裝置訊息傳送至 Pi。</span><span class="sxs-lookup"><span data-stu-id="7fdca-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fdca-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7fdca-131">Next steps</span></span>
[<span data-ttu-id="7fdca-132">執行範例應用程式以接收雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="7fdca-132">Run the sample application to receive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

