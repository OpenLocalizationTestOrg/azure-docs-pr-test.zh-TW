---
title: "模擬裝置與 Azure IoT 閘道 - 第 4 課：表格儲存體 | Microsoft Docs"
description: "將訊息從 Intel NUC 儲存到您的 IoT 中樞，然後將訊息寫入 Azure 表格儲存體，並讀取雲端中的訊息。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "從雲端擷取資料, iot 雲端服務"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: de5fae794c195132e2a487c0095845c756aa28e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="b29a1-104">讀取保存在 Azure 表格儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="b29a1-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="b29a1-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="b29a1-105">What you will do</span></span>

- <span data-ttu-id="b29a1-106">在您的閘道器上執行閘道器範例應用程式，將訊息傳送至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b29a1-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="b29a1-107">在您的主機電腦上執行範例程式碼，以讀取 Azure表格儲存體中的訊息。</span><span class="sxs-lookup"><span data-stu-id="b29a1-107">Run sample code on your host computer to read messages in your Azure Table storage.</span></span>

<span data-ttu-id="b29a1-108">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="b29a1-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b29a1-109">學習目標</span><span class="sxs-lookup"><span data-stu-id="b29a1-109">What you will learn</span></span>

<span data-ttu-id="b29a1-110">如何使用 gulp 工具執行範例應用程式，以讀取在您的 Azure 表格儲存體中的訊息。</span><span class="sxs-lookup"><span data-stu-id="b29a1-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b29a1-111">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="b29a1-111">What you need</span></span>

<span data-ttu-id="b29a1-112">您已成功完成下列工作︰</span><span class="sxs-lookup"><span data-stu-id="b29a1-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="b29a1-113">[建立 Azure 函數應用程式與 Azure 儲存體帳戶](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="b29a1-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="b29a1-114">[執行閘道器範例應用程式](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)。</span><span class="sxs-lookup"><span data-stu-id="b29a1-114">[Run the gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="b29a1-115">[讀取來自 IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="b29a1-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="b29a1-116">取得您的 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="b29a1-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="b29a1-117">稍早在本課程中，您已成功建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b29a1-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="b29a1-118">若要取得 Azure 儲存體帳戶的連接字串，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b29a1-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="b29a1-119">列出您的所有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b29a1-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="b29a1-120">取得 Azure 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="b29a1-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="b29a1-121">如果您在第 2 課中沒有變更值，請使用 `iot-gateway` 作為 `{resource group name}` 的值。</span><span class="sxs-lookup"><span data-stu-id="b29a1-121">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="b29a1-122">設定裝置連線</span><span class="sxs-lookup"><span data-stu-id="b29a1-122">Configure the device connection</span></span>

<span data-ttu-id="b29a1-123">更新 `config-azure.json` 檔案，使在主機電腦上執行的範例程式碼可以讀取 Azure 表格儲存體中的訊息。</span><span class="sxs-lookup"><span data-stu-id="b29a1-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="b29a1-124">若要設定裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b29a1-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="b29a1-125">執行下列命令來產生裝置組態檔 `config-azure.json`：</span><span class="sxs-lookup"><span data-stu-id="b29a1-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![組態](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="b29a1-127">將 `[Azure storage connection string]` 取代為您取得的 Azure 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="b29a1-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="b29a1-128">`[IoT hub connection string]` 應該已經在第 3 課的[讀取來自 Azure IoT 中樞的傳入訊息](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)中被取代。</span><span class="sxs-lookup"><span data-stu-id="b29a1-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="b29a1-129">讀取 Azure 表格儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="b29a1-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="b29a1-130">執行閘道器範例應用程式，並使用下列命令讀取 Azure 表格儲存體訊息︰</span><span class="sxs-lookup"><span data-stu-id="b29a1-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="b29a1-131">您的 IoT 中樞會觸發您的 Azure 函數應用程式，當有新訊息進來時，後者會將訊息儲存到您的 Azure 表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="b29a1-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="b29a1-132">`gulp run` 命令會執行閘道器範例應用程式將訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b29a1-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="b29a1-133">使用 `table-storage` 參數，它也會繁衍子程序來接收儲存在 Azure表格儲存體中的訊息。</span><span class="sxs-lookup"><span data-stu-id="b29a1-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="b29a1-134">傳送和接收的所有訊息皆會立即顯示在主機電腦的同一主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="b29a1-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="b29a1-135">範例應用程式執行個體會在 40 秒後自動終止。</span><span class="sxs-lookup"><span data-stu-id="b29a1-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![gulp 讀取](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="b29a1-137">摘要</span><span class="sxs-lookup"><span data-stu-id="b29a1-137">Summary</span></span>

<span data-ttu-id="b29a1-138">您已執行範例程式碼來讀取由您的 Azure 函數應用程式儲存在您的 Azure 表格儲存體中的訊息。</span><span class="sxs-lookup"><span data-stu-id="b29a1-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>
