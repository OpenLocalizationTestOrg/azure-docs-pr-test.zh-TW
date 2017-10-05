---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 4 課：建立函數應用程式 | Microsoft Docs"
description: "將訊息從 Intel NUC 儲存到您的 IoT 中樞，然後將訊息寫入 Azure 表格儲存體，並讀取雲端中的訊息。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "將資料儲存在雲端, 儲存在雲端的資料, iot 雲端服務"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 717c91e8332660f19d596c05a8a23afd8df1d51c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="b1176-104">建立 Azure 函式應用程式與儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b1176-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="b1176-105">Azure Functions 是可在雲端輕鬆執行「函式」(一小段程式碼) 的解決方案。</span><span class="sxs-lookup"><span data-stu-id="b1176-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="b1176-106">Azure 函數應用程式可在 Azure 中主控函數的執行。</span><span class="sxs-lookup"><span data-stu-id="b1176-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="b1176-107">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="b1176-107">What you will do</span></span>

- <span data-ttu-id="b1176-108">使用 Azure Resource Manager 範本來建立 Azure 函式應用程式及 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1176-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="b1176-109">Azure 函式應用程式會接聽 Azure IoT 中樞事件、處理傳入訊息，並將它們寫入 Azure 表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="b1176-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="b1176-110">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="b1176-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="b1176-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="b1176-111">What you will learn</span></span>

<span data-ttu-id="b1176-112">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="b1176-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="b1176-113">如何使用 Azure Resource Manager 部署 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b1176-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="b1176-114">如何使用 Azure 函數應用程式處理 IoT 中樞訊息，並將它們寫入 Azure 表格儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="b1176-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b1176-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="b1176-115">What you need</span></span>

<span data-ttu-id="b1176-116">您必須已順利完成先前的課程︰</span><span class="sxs-lookup"><span data-stu-id="b1176-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="b1176-117">第 1 課：將 Intel NUC 設定為 IoT 閘道器</span><span class="sxs-lookup"><span data-stu-id="b1176-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="b1176-118">第 2 課：準備好您的主機電腦和 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="b1176-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="b1176-119">第 3 課︰接收來自 SensorTag 的訊息，並讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="b1176-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="b1176-120">開啟範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b1176-120">Open a sample app</span></span>

<span data-ttu-id="b1176-121">前往您的 `iot-hub-c-intel-nuc-gateway-getting-started` 存放庫資料夾，初始化組態檔，然後執行下列命令在 Visual Studio Code 中開啟範例專案︰</span><span class="sxs-lookup"><span data-stu-id="b1176-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![存放庫結構](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="b1176-123">`arm-template.json` 檔案為包含 Azure 函式應用程式及 Azure 儲存體帳戶的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="b1176-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="b1176-124">`arm-template-param.json` 檔案是 Azure Resource Manager 範本使用的組態檔。</span><span class="sxs-lookup"><span data-stu-id="b1176-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="b1176-125">`ReceiveDeviceMessages` 子資料夾包含 Azure 函數的 Node.js 程式碼。</span><span class="sxs-lookup"><span data-stu-id="b1176-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="b1176-126">在 Azure 中設定 Azure Resource Manager 範本並建立資源</span><span class="sxs-lookup"><span data-stu-id="b1176-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="b1176-127">更新 Visual Studio Code 中的 `arm-template-param.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="b1176-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![arm 範本 json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="b1176-129">將 `[your IoT Hub name]` 取代為您在第 2 課指定的 `{my hub name}`。</span><span class="sxs-lookup"><span data-stu-id="b1176-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="b1176-130">在您更新 `arm-template-param.json` 檔案後，請執行下列命令來將資源部署到 Azure：</span><span class="sxs-lookup"><span data-stu-id="b1176-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="b1176-131">如果您在第 2 課中沒有變更值，請使用 `iot-gateway` 作為 `{resource group name}` 的值。</span><span class="sxs-lookup"><span data-stu-id="b1176-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="b1176-132">摘要</span><span class="sxs-lookup"><span data-stu-id="b1176-132">Summary</span></span>

<span data-ttu-id="b1176-133">您已建立 Azure 函式應用程式以處理 IoT 中樞訊息，並建立 Azure 儲存體帳戶以儲存這些訊息。</span><span class="sxs-lookup"><span data-stu-id="b1176-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="b1176-134">您現在可以讀取由您的閘道器傳送至 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="b1176-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1176-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1176-135">Next steps</span></span>
<span data-ttu-id="b1176-136">[讀取保存在 Azure 儲存體中的訊息](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="b1176-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
