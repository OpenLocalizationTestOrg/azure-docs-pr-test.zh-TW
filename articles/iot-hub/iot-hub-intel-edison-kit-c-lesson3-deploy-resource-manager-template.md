---
title: "將 Intel Edison (C) 連接到 Azure IoT - 第 3 課：建立函數應用程式 | Microsoft Docs"
description: "Azure 函式應用程式會接聽 Azure IoT 中樞事件、處理傳入訊息，並將它們寫入 Azure 表格儲存體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "將資料儲存在雲端, 儲存在雲端的資料, iot 雲端服務"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 739b82e9-5d4e-4485-8971-f57cbb682faf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30018cc2d03fc19c13625ef066989a89f21800e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="585c3-104">建立 Azure 函式應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="585c3-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="585c3-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) 是可在雲端輕鬆執行「函式」(一小段程式碼) 的解決方案。</span><span class="sxs-lookup"><span data-stu-id="585c3-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="585c3-106">Azure 函數應用程式可在 Azure 中主控函數的執行。</span><span class="sxs-lookup"><span data-stu-id="585c3-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="585c3-107">您將會怎麼做</span><span class="sxs-lookup"><span data-stu-id="585c3-107">What will you do</span></span>
<span data-ttu-id="585c3-108">使用 Azure Resource Manager 範本來建立 Azure 函式應用程式及 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="585c3-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="585c3-109">Azure 函式應用程式會接聽 Azure IoT 中樞事件、處理傳入訊息，並將它們寫入 Azure 表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="585c3-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="585c3-110">儲存體帳戶可用於從 Azure 資料表讀取訊息的持續性複本。</span><span class="sxs-lookup"><span data-stu-id="585c3-110">The storage account is used for reading the persisted copies of messages from Azure table.</span></span> <span data-ttu-id="585c3-111">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="585c3-111">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="585c3-112">您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="585c3-112">What will you learn</span></span>
<span data-ttu-id="585c3-113">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="585c3-113">In this article, you will learn:</span></span>
* <span data-ttu-id="585c3-114">如何使用 [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) 部署 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="585c3-114">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="585c3-115">如何使用 Azure 函式應用程式處理 IoT 中樞訊息，並將它們寫入 Azure 表格儲存體中的表格。</span><span class="sxs-lookup"><span data-stu-id="585c3-115">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="585c3-116">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="585c3-116">What do you need</span></span>
<span data-ttu-id="585c3-117">您必須已成功完成：</span><span class="sxs-lookup"><span data-stu-id="585c3-117">You must have successfully completed:</span></span>
- <span data-ttu-id="585c3-118">[開始使用 Intel Edison][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="585c3-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="585c3-119">[建立您的 Azure IoT 中樞][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="585c3-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="585c3-120">開啟範例應用程式</span><span class="sxs-lookup"><span data-stu-id="585c3-120">Open the sample app</span></span>
<span data-ttu-id="585c3-121">執行下列命令來在 Visual Studio Code 中開啟範例專案︰</span><span class="sxs-lookup"><span data-stu-id="585c3-121">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![儲存機制結構][repo-structure]

* <span data-ttu-id="585c3-123">`app` 子資料夾中的檔案是關鍵的來源檔案。</span><span class="sxs-lookup"><span data-stu-id="585c3-123">The file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="585c3-124">這個來源檔案包含要將訊息傳送到 IoT 中樞 20 次，並於每次傳送訊息時使 LED 閃爍的程式碼。</span><span class="sxs-lookup"><span data-stu-id="585c3-124">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="585c3-125">`arm-template.json` 檔案為包含 Azure 函式應用程式及 Azure 儲存體帳戶的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="585c3-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="585c3-126">`arm-template-param.json` 檔案是 Azure Resource Manager 範本使用的組態檔。</span><span class="sxs-lookup"><span data-stu-id="585c3-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="585c3-127">`ReceiveDeviceMessages` 子資料夾包含 Azure 函數的 Node.js 程式碼。</span><span class="sxs-lookup"><span data-stu-id="585c3-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="585c3-128">在 Azure 中設定 Azure Resource Manager 範本並建立資源</span><span class="sxs-lookup"><span data-stu-id="585c3-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="585c3-129">更新 Visual Studio Code 中的 `arm-template-param.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="585c3-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager 範本參數][arm-template-parameters]

* <span data-ttu-id="585c3-131">將 **[your IoT Hub name]** 替換為您在[建立 IoT 中樞並登錄 Intel Edison][created-your-iot-hub-and-registered-intel-edison] 時所指定的 **{my hub name}**。</span><span class="sxs-lookup"><span data-stu-id="585c3-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="585c3-132">將 **[prefix string for new resources]** 以您想要的任何前置詞取代。</span><span class="sxs-lookup"><span data-stu-id="585c3-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="585c3-133">前置詞能確保資源名稱為全域唯一以避免衝突。</span><span class="sxs-lookup"><span data-stu-id="585c3-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="585c3-134">請不要在前置詞中使用破折號或字首數字。</span><span class="sxs-lookup"><span data-stu-id="585c3-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="585c3-135">在您更新 `arm-template-param.json` 檔案後，請執行下列命令來將資源部署到 Azure：</span><span class="sxs-lookup"><span data-stu-id="585c3-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="585c3-136">建立這些資源大概需要五分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="585c3-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="585c3-137">當資源建立正在進行時，您可以移至下一篇文章。</span><span class="sxs-lookup"><span data-stu-id="585c3-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="585c3-138">摘要</span><span class="sxs-lookup"><span data-stu-id="585c3-138">Summary</span></span>
<span data-ttu-id="585c3-139">您已建立 Azure 函式應用程式以處理 IoT 中樞訊息，並建立 Azure 儲存體帳戶以儲存這些訊息。</span><span class="sxs-lookup"><span data-stu-id="585c3-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="585c3-140">您現在可以部署並執行範例，以在 Edison 上傳送「裝置到雲端」訊息。</span><span class="sxs-lookup"><span data-stu-id="585c3-140">You can now deploy and run the sample to send device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="585c3-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="585c3-141">Next steps</span></span>
<span data-ttu-id="585c3-142">[執行範例應用程式以在 Intel Edison 上傳送「裝置到雲端」訊息][send-device-to-cloud-messages]。</span><span class="sxs-lookup"><span data-stu-id="585c3-142">[Run a sample application to send device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md