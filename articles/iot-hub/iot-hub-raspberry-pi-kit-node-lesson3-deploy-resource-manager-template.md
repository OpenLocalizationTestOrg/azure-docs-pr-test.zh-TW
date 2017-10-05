---
title: "將 Raspberry Pi (節點) 連接到 Azure IoT - 第 3 課：範本部署 | Microsoft Docs"
description: "Azure 函式應用程式會接聽 Azure IoT 中樞事件、處理傳入訊息，並將它們寫入 Azure 表格儲存體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "將資料儲存在雲端, 儲存在雲端的資料, iot 雲端服務"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="6ce73-104">建立 Azure 函式應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6ce73-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="6ce73-105">[Azure Functions](../azure-functions/functions-overview.md) 是可在雲端輕鬆執行「函式」(一小段程式碼) 的解決方案。</span><span class="sxs-lookup"><span data-stu-id="6ce73-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="6ce73-106">Azure 函數應用程式可在 Azure 中主控函數的執行。</span><span class="sxs-lookup"><span data-stu-id="6ce73-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6ce73-107">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="6ce73-107">What you will do</span></span>
<span data-ttu-id="6ce73-108">使用 Azure Resource Manager 範本來建立 Azure 函式應用程式及 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6ce73-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="6ce73-109">Azure 函式應用程式會接聽 Azure IoT 中樞事件、處理傳入訊息，並將它們寫入 Azure 表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="6ce73-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="6ce73-110">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="6ce73-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6ce73-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="6ce73-111">What you will learn</span></span>
<span data-ttu-id="6ce73-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="6ce73-112">In this article, you will learn:</span></span>

* <span data-ttu-id="6ce73-113">如何使用 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 部署 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="6ce73-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="6ce73-114">如何使用 Azure 函式應用程式處理 IoT 中樞訊息，並將它們寫入 Azure 表格儲存體中的表格。</span><span class="sxs-lookup"><span data-stu-id="6ce73-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6ce73-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="6ce73-115">What you need</span></span>
<span data-ttu-id="6ce73-116">您必須已成功完成：</span><span class="sxs-lookup"><span data-stu-id="6ce73-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="6ce73-117">開始使用 Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="6ce73-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="6ce73-118">建立您的 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="6ce73-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-the-sample-app"></a><span data-ttu-id="6ce73-119">開啟範例應用程式</span><span class="sxs-lookup"><span data-stu-id="6ce73-119">Open the sample app</span></span>
<span data-ttu-id="6ce73-120">執行下列命令來在 Visual Studio Code 中開啟範例專案︰</span><span class="sxs-lookup"><span data-stu-id="6ce73-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![儲存機制結構](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="6ce73-122">`app` 子資料夾中的 `app.js` 檔案是關鍵的來源檔案。</span><span class="sxs-lookup"><span data-stu-id="6ce73-122">The `app.js` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="6ce73-123">這個來源檔案包含要將訊息傳送到 IoT 中樞 20 次，並於每次傳送訊息時使 LED 閃爍的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6ce73-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="6ce73-124">`arm-template.json` 檔案為包含 Azure 函式應用程式及 Azure 儲存體帳戶的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6ce73-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="6ce73-125">`arm-template-param.json` 檔案是 Azure Resource Manager 範本使用的組態檔。</span><span class="sxs-lookup"><span data-stu-id="6ce73-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="6ce73-126">`ReceiveDeviceMessages` 子資料夾包含 Azure 函數的 Node.js 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6ce73-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="6ce73-127">在 Azure 中設定 Azure Resource Manager 範本並建立資源</span><span class="sxs-lookup"><span data-stu-id="6ce73-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="6ce73-128">更新 Visual Studio Code 中的 `arm-template-param.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="6ce73-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager 範本參數](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="6ce73-130">將 **[your IoT Hub name]** 替換為您在[建立 IoT 中樞並登錄 Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md) 時所指定的 **{my hub name}**。</span><span class="sxs-lookup"><span data-stu-id="6ce73-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="6ce73-131">將 **[prefix string for new resources]** 以您想要的任何前置詞取代。</span><span class="sxs-lookup"><span data-stu-id="6ce73-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="6ce73-132">前置詞能確保資源名稱為全域唯一以避免衝突。</span><span class="sxs-lookup"><span data-stu-id="6ce73-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="6ce73-133">請不要在前置詞中使用破折號或字首數字。</span><span class="sxs-lookup"><span data-stu-id="6ce73-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="6ce73-134">在您更新 `arm-template-param.json` 檔案後，請執行下列命令來將資源部署到 Azure：</span><span class="sxs-lookup"><span data-stu-id="6ce73-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="6ce73-135">建立這些資源大概需要五分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="6ce73-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="6ce73-136">當資源建立正在進行時，您可以移至下一篇文章。</span><span class="sxs-lookup"><span data-stu-id="6ce73-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="6ce73-137">摘要</span><span class="sxs-lookup"><span data-stu-id="6ce73-137">Summary</span></span>
<span data-ttu-id="6ce73-138">您已建立 Azure 函式應用程式以處理 IoT 中樞訊息，並建立 Azure 儲存體帳戶以儲存這些訊息。</span><span class="sxs-lookup"><span data-stu-id="6ce73-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="6ce73-139">您現在可以部署並執行範例，以在 Pi 上傳送「裝置到雲端」訊息。</span><span class="sxs-lookup"><span data-stu-id="6ce73-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ce73-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ce73-140">Next steps</span></span>
[<span data-ttu-id="6ce73-141">執行範例應用程式以在 Raspberry Pi 3 上傳送「裝置到雲端」訊息</span><span class="sxs-lookup"><span data-stu-id="6ce73-141">Run a sample application to send device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

