---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 4 課：建立函數應用程式 | Microsoft Docs"
description: "從 Intel NUC tooyour IoT 中樞儲存訊息、 將它們寫入 tooAzure 資料表儲存體，然後讀取它們從 hello 雲端。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "將資料儲存在 hello 雲端中，儲存在雲端中，資料 iot 雲端服務"
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
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="f6468-104">建立 Azure 函式應用程式與儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f6468-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="f6468-105">Azure 的函式是方案，輕鬆地執行_函式_（一些程式碼片段） hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="f6468-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="f6468-106">Azure 的函式應用程式裝載函式在 Azure 中的 hello 執行。</span><span class="sxs-lookup"><span data-stu-id="f6468-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="f6468-107">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="f6468-107">What you will do</span></span>

- <span data-ttu-id="f6468-108">Azure 的函式應用程式與 Azure 儲存體帳戶，請使用 Azure Resource Manager 範本 toocreate。</span><span class="sxs-lookup"><span data-stu-id="f6468-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="f6468-109">hello Azure 函式應用程式會接聽 tooAzure IoT 中樞事件、 處理內送訊息，並將其寫入 tooAzure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="f6468-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="f6468-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="f6468-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="f6468-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="f6468-111">What you will learn</span></span>

<span data-ttu-id="f6468-112">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="f6468-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f6468-113">如何 toouse Azure 資源管理員 toodeploy Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f6468-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="f6468-114">如何 toouse Azure 函式應用程式 tooprocess IoT 中樞的訊息，並在 Azure 資料表儲存體中撰寫 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="f6468-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f6468-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="f6468-115">What you need</span></span>

<span data-ttu-id="f6468-116">您必須已順利完成 hello 先前的課程：</span><span class="sxs-lookup"><span data-stu-id="f6468-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="f6468-117">第 1 課：將 Intel NUC 設定為 IoT 閘道器</span><span class="sxs-lookup"><span data-stu-id="f6468-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="f6468-118">第 2 課：準備好您的主機電腦和 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="f6468-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="f6468-119">第 3 課︰接收來自 SensorTag 的訊息，並讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="f6468-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="f6468-120">開啟範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f6468-120">Open a sample app</span></span>

<span data-ttu-id="f6468-121">移 tooyour`iot-hub-c-intel-nuc-gateway-getting-started`儲存機制資料夾，初始化 hello 設定檔，然後開啟 hello 範例專案在 Visual Studio 程式碼中藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f6468-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![存放庫結構](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="f6468-123">hello`arm-template.json`檔案是包含 Azure 的函式應用程式與 Azure 儲存體帳戶的 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="f6468-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="f6468-124">hello`arm-template-param.json`檔案為 hello hello Azure Resource Manager 範本所使用的組態檔。</span><span class="sxs-lookup"><span data-stu-id="f6468-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="f6468-125">hello`ReceiveDeviceMessages`子資料夾包含 hello Node.js hello Azure 函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="f6468-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="f6468-126">在 Azure 中設定 Azure Resource Manager 範本並建立資源</span><span class="sxs-lookup"><span data-stu-id="f6468-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="f6468-127">更新 hello `arm-template-param.json` Visual Studio 程式碼中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f6468-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![arm 範本 json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="f6468-129">將 `[your IoT Hub name]` 取代為您在第 2 課指定的 `{my hub name}`。</span><span class="sxs-lookup"><span data-stu-id="f6468-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="f6468-130">更新 hello 之後`arm-template-param.json`檔案中，執行下列命令的 hello 部署 hello 資源 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="f6468-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="f6468-131">使用`iot-gateway`做為 hello 值`{resource group name}`如果您沒有變更 hello 課程 2 中的值。</span><span class="sxs-lookup"><span data-stu-id="f6468-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="f6468-132">摘要</span><span class="sxs-lookup"><span data-stu-id="f6468-132">Summary</span></span>

<span data-ttu-id="f6468-133">您已建立您的 Azure 函式應用程式 tooprocess IoT 中樞訊息，與 Azure 儲存體帳戶的 toostore 這些訊息。</span><span class="sxs-lookup"><span data-stu-id="f6468-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="f6468-134">您現在可以讀取由您的閘道 tooyour IoT 中樞傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="f6468-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6468-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6468-135">Next steps</span></span>
<span data-ttu-id="f6468-136">[讀取保存在 Azure 儲存體中的訊息](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="f6468-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
