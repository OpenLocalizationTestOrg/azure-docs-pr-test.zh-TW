---
title: "Connect Intel Edison (C) tooAzure IoT-第 3 課： 建立函數應用程式 |Microsoft 文件"
description: "hello Azure 函式應用程式會接聽 tooAzure IoT 中樞事件、 處理內送訊息，並將其寫入 tooAzure 資料表儲存體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "將資料儲存在 hello 雲端中，儲存在雲端中，資料 iot 雲端服務"
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
ms.openlocfilehash: ef045ec2f44fe379a5e6c777d1bfb97de8b965a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a>建立 Azure 函式應用程式與 Azure 儲存體帳戶
[Azure 函數](../../articles/azure-functions/functions-overview.md)是方案，輕鬆地執行*函式*（一些程式碼片段） hello 雲端中。 Azure 的函式應用程式裝載函式在 Azure 中的 hello 執行。

## <a name="what-will-you-do"></a>您將會怎麼做
Azure 的函式應用程式與 Azure 儲存體帳戶，請使用 Azure Resource Manager 範本 toocreate。 hello Azure 函式應用程式會接聽 tooAzure IoT 中樞事件、 處理內送訊息，並將其寫入 tooAzure 資料表儲存體。 hello 儲存體帳戶用來讀取 hello 保存訊息從 Azure 資料表的複本。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

## <a name="what-will-you-learn"></a>您將學到什麼
在本文中，您將了解：
* 如何 toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure 資源。
* 如何 toouse Azure 函式應用程式 tooprocess IoT 中樞訊息，並在 Azure 資料表儲存體中撰寫 tooa 資料表。

## <a name="what-do-you-need"></a>您需要什麼
您必須已成功完成：
- [開始使用 Intel Edison][get-started-with-your-intel-edison]
- [建立您的 Azure IoT 中樞][create-your-azure-iot-hub]

## <a name="open-hello-sample-app"></a>開啟 hello 範例應用程式
開啟 Visual Studio 程式碼中的 hello 範例專案，藉由執行下列命令的 hello:

```bash
cd Lesson3
code .
```

![儲存機制結構][repo-structure]

* hello 檔案在 hello`app`子資料夾位於 hello 金鑰來源檔案。 這個原始程式檔包含 hello 程式碼 toosend 它所傳送的訊息 20 倍 tooyour IoT 中樞與閃爍 hello LED 為每個訊息。
* hello`arm-template.json`檔案是包含 Azure 的函式應用程式與 Azure 儲存體帳戶的 hello Azure Resource Manager 範本。
* hello`arm-template-param.json`檔案為 hello hello Azure Resource Manager 範本所使用的組態檔。
* hello`ReceiveDeviceMessages`子資料夾包含 hello Node.js hello Azure 函式程式碼。

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a>在 Azure 中設定 Azure Resource Manager 範本並建立資源
更新 hello `arm-template-param.json` Visual Studio 程式碼中的檔案。

![Azure Resource Manager 範本參數][arm-template-parameters]

* 將 **[your IoT Hub name]** 替換為您在[建立 IoT 中樞並登錄 Intel Edison][created-your-iot-hub-and-registered-intel-edison] 時所指定的 **{my hub name}**。
* 將 **[prefix string for new resources]** 以您想要的任何前置詞取代。 hello 前置詞可確保該 hello 資源名稱是全域唯一 tooavoid 衝突。 請勿使用破折號或初始 hello 前置詞中的數字。

更新 hello 之後`arm-template-param.json`檔案中，執行下列命令的 hello 部署 hello 資源 tooAzure:

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

花費大約五分鐘 toocreate 這些資源。 在進行 hello 資源建立時，您可以移動 toohello 下一個發行項。

## <a name="summary"></a>摘要
您已建立您的 Azure 函式應用程式 tooprocess IoT 中樞訊息，與 Azure 儲存體帳戶的 toostore 這些訊息。 您現在可以部署和執行 Edison hello 範例 toosend 裝置到雲端訊息。

## <a name="next-steps"></a>後續步驟
[在 Intel Edison 上執行範例應用程式 toosend 裝置到雲端訊息][send-device-to-cloud-messages]。
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md