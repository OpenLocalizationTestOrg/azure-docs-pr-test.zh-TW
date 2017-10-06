---
title: "Connect Raspberry Pi (C) tooAzure IoT-第 3 課： 部署範本 |Microsoft 文件"
description: "hello Azure 函式應用程式會接聽 tooAzure IoT 中樞事件、 處理內送訊息，並將其寫入 tooAzure 資料表儲存體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "將資料儲存在 hello 雲端中，儲存在雲端中，資料 iot 雲端服務"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 11aaad4935681d8b3d338779eec1b19d77cb11e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="127d5-104">建立 Azure 函式應用程式與 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="127d5-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="127d5-105">[Azure 函數](../../articles/azure-functions/functions-overview.md)是方案，輕鬆地執行*函式*（一些程式碼片段） hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="127d5-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="127d5-106">Azure 的函式應用程式裝載函式在 Azure 中的 hello 執行。</span><span class="sxs-lookup"><span data-stu-id="127d5-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="127d5-107">您將會怎麼做</span><span class="sxs-lookup"><span data-stu-id="127d5-107">What will you do</span></span>
<span data-ttu-id="127d5-108">Azure 的函式應用程式與 Azure 儲存體帳戶，請使用 Azure Resource Manager 範本 toocreate。</span><span class="sxs-lookup"><span data-stu-id="127d5-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="127d5-109">hello Azure 函式應用程式會接聽 tooAzure IoT 中樞事件、 處理內送訊息，並將其寫入 tooAzure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="127d5-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="127d5-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="127d5-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="127d5-111">您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="127d5-111">What will you learn</span></span>
<span data-ttu-id="127d5-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="127d5-112">In this article, you will learn:</span></span>
* <span data-ttu-id="127d5-113">如何 toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="127d5-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="127d5-114">如何 toouse Azure 函式應用程式 tooprocess IoT 中樞訊息，並在 Azure 資料表儲存體中撰寫 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="127d5-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="127d5-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="127d5-115">What do you need</span></span>
* <span data-ttu-id="127d5-116">您必須已成功完成：</span><span class="sxs-lookup"><span data-stu-id="127d5-116">You must have successfully completed:</span></span>
- [<span data-ttu-id="127d5-117">開始使用 Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="127d5-117">Get started with your Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)
- [<span data-ttu-id="127d5-118">建立您的 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="127d5-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)

## <a name="open-hello-sample-app"></a><span data-ttu-id="127d5-119">開啟 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="127d5-119">Open hello sample app</span></span>
<span data-ttu-id="127d5-120">開啟 Visual Studio 程式碼中的 hello 範例專案，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="127d5-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![儲存機制結構](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure_c.png)

* <span data-ttu-id="127d5-122">hello`main.c`檔案在 hello`app`子資料夾位於 hello 金鑰來源檔案。</span><span class="sxs-lookup"><span data-stu-id="127d5-122">hello `main.c` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="127d5-123">這個原始程式檔包含 hello 程式碼 toosend 它所傳送的訊息 20 倍 tooyour IoT 中樞與閃爍 hello LED 為每個訊息。</span><span class="sxs-lookup"><span data-stu-id="127d5-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="127d5-124">hello`arm-template.json`檔案是包含 Azure 的函式應用程式與 Azure 儲存體帳戶的 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="127d5-124">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="127d5-125">hello`arm-template-param.json`檔案為 hello hello Azure Resource Manager 範本所使用的組態檔。</span><span class="sxs-lookup"><span data-stu-id="127d5-125">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="127d5-126">hello`ReceiveDeviceMessages`子資料夾包含 hello Node.js hello Azure 函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="127d5-126">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="127d5-127">在 Azure 中設定 Azure Resource Manager 範本並建立資源</span><span class="sxs-lookup"><span data-stu-id="127d5-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="127d5-128">更新 hello `arm-template-param.json` Visual Studio 程式碼中的檔案。</span><span class="sxs-lookup"><span data-stu-id="127d5-128">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager 範本參數](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para_c.png)

* <span data-ttu-id="127d5-130">將 **[your IoT Hub name]** 替換為您在[建立 IoT 中樞並登錄 Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md) 時所指定的 **{my hub name}**。</span><span class="sxs-lookup"><span data-stu-id="127d5-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="127d5-131">將 **[prefix string for new resources]** 以您想要的任何前置詞取代。</span><span class="sxs-lookup"><span data-stu-id="127d5-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="127d5-132">hello 前置詞可確保該 hello 資源名稱是全域唯一 tooavoid 衝突。</span><span class="sxs-lookup"><span data-stu-id="127d5-132">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="127d5-133">請勿使用破折號或初始 hello 前置詞中的數字。</span><span class="sxs-lookup"><span data-stu-id="127d5-133">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="127d5-134">更新 hello 之後`arm-template-param.json`檔案中，執行下列命令的 hello 部署 hello 資源 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="127d5-134">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="127d5-135">花費大約五分鐘 toocreate 這些資源。</span><span class="sxs-lookup"><span data-stu-id="127d5-135">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="127d5-136">在進行 hello 資源建立時，您可以移動 toohello 下一個發行項。</span><span class="sxs-lookup"><span data-stu-id="127d5-136">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="127d5-137">摘要</span><span class="sxs-lookup"><span data-stu-id="127d5-137">Summary</span></span>
<span data-ttu-id="127d5-138">您已建立您的 Azure 函式應用程式 tooprocess IoT 中樞訊息，與 Azure 儲存體帳戶的 toostore 這些訊息。</span><span class="sxs-lookup"><span data-stu-id="127d5-138">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="127d5-139">您可以現在上部署及執行 hello 範例 toosend 裝置到雲端訊息 Pi。</span><span class="sxs-lookup"><span data-stu-id="127d5-139">You can now deploy and run hello sample toosend device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="127d5-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="127d5-140">Next steps</span></span>
[<span data-ttu-id="127d5-141">執行範例應用程式 toosend 裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="127d5-141">Run a sample application toosend device-to-cloud messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md)

