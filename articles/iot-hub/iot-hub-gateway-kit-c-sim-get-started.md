---
title: "模擬裝置與 Azure IoT 閘道 - 開始使用 | Microsoft Docs"
description: "開始使用 IoT 閘道入門套件，建立您的 Azure IoT 中樞，並連接閘道 toohello IoT 中樞"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot 中樞，iot 閘道使用，以開始使用 hello 物聯網 iot 工具組"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a>開始使用 IoT 閘道器入門套件與模擬裝置

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [模擬裝置](iot-hub-gateway-kit-c-sim-get-started.md)

本教學課程中，在您開始學習使用的 hello 基本[IoT 閘道入門套件](https://aka.ms/gateway-kit)。 您將使用執行 Wind River Linux 的 Intel NUC。 您將學習如何 tooseamleesly 連接您的裝置 toohello 雲端使用 Azure IoT 中樞。

***
**沒有套件嗎？**按一下[這裡](https://aka.ms/gateway-kit)。
***

## <a name="lesson-1-configure-your-nuc"></a>第 1 課：設定 NUC
![第 1 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

在這一課，您可以設定 hello 套件作為 Azure IoT 閘道 （下一個單位的運算） 的 Intel NUC、 NUC，在安裝 hello Azure IoT 邊緣套件並執行範例應用程式 tooverify hello 閘道功能。

*估計時間 toocomplete: 15 分鐘*

跳過[Intel NUC 為 IoT 閘道設定](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>第 2 課：建立 IoT 中樞
![第 2 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

在這一課，您在主機電腦上安裝 hello 工具和軟體。 然後您建立免費的 Azure 帳戶、 佈建您的 Azure IoT 中樞和 hello IoT 中樞中建立您的第一個裝置。

開始本課程前，請先完成第 1 課。

### <a name="get-hello-tools"></a>取得 hello 工具
主機電腦上安裝 hello 工具和軟體。

*估計時間 toocomplete: 20 分鐘*

跳過[取得 hello 工具](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>建立 IoT 中樞並登錄您的裝置
建立資源群組中，佈建第一個的 Azure IoT 中樞，並加入使用 hello Azure CLI 您第一次裝置 toohello IoT 中樞。

*估計時間 toocomplete: 10 分鐘*

跳過[建立 IoT 中樞，並註冊您的裝置](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a>第 3 課： 從 hello 模擬裝置接收訊息，並從 IoT 中樞讀取訊息
在這一課，您將使用指令碼 tooautomate hello 組態和模擬的裝置應用程式的執行在您的閘道。 hello 模擬的裝置應用程式會產生範例溫度資料，並將它傳送 tooan IoT 中樞模組。 hello 收到 hello 資料，並將它的 Azure IoT Edge 傳送 tooyour IoT 中樞透過 hello 閘道架構提供 IoT 中樞模組封裝。

![第 3 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a>設定並執行模擬裝置
準備 hello 範例程式碼。 然後設定及執行 hello 模擬裝置的範例應用程式。

*估計時間 toocomplete: 15 分鐘*

跳過[設定及執行模擬的裝置](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

### <a name="read-messages-from-your-iot-hub"></a>讀取來自 IoT 中樞的傳入訊息
在主機電腦 tooread hello 訊息上執行範例程式碼，從 IoT 中樞。

*估計時間 toocomplete: 15 分鐘*

跳過[從 IoT 中樞讀取訊息](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>第 4 課： 將訊息儲存 tooAzure 資料表儲存體
建立從 IoT 中樞取得內送訊息，並將其寫入 tooAzure 資料表儲存體的 Azure 函式應用程式。

![第 4 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>建立 Azure 函數應用程式與 Azure 儲存體帳戶
Azure 的函式應用程式與 Azure 儲存體帳戶，請使用 Azure Resource Manager 範本 toocreate。

*估計時間 toocomplete: 10 分鐘*

跳過[建立 Azure 的函式應用程式與 Azure 儲存體帳戶](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>讀取保存在 Azure 表格儲存體中的訊息
當寫入 tooAzure 資料表儲存體監視 hello 閘道到雲端訊息。

*估計時間 toocomplete: 5 分鐘*

跳過[讀取訊息保存在 Azure 資料表儲存體](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md)。

## <a name="troubleshooting"></a>疑難排解
如果您在 hello 課程期間有任何問題，尋找在 hello 解決方案[疑難排解](iot-hub-gateway-kit-c-sim-troubleshooting.md)發行項。

## <a name="explore-more"></a>探索更多
請瀏覽 hello [Intel IoT 閘道套件開發人員區域](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit)toolearn 更多。
