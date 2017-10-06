---
title: "SensorTag 裝置與 Azure IoT 閘道 - 開始使用 | Microsoft Docs"
description: "開始使用 IoT 閘道入門套件，建立您的 Azure IoT 中樞，並連接 SensorTag 和閘道 toohello IoT 中樞"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot 中樞，iot 閘道使用，以開始使用 hello 物聯網 iot 工具組"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a>開始使用 IoT 閘道器入門套件與 SensorTag

> [!div class="op_single_selector"]
> * [SensorTag](iot-hub-gateway-kit-c-get-started.md)
> * [模擬裝置](iot-hub-gateway-kit-c-sim-get-started.md)

本教學課程中，在您開始學習使用的 hello 基本[IoT 閘道入門套件](https://aka.ms/gateway-kit)。 您即將使用 Intel NUC Wind 河 Linux 和 hello 執行[TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main)。 您將學習如何 tooseamleesly 連接您的裝置 toohello 雲端使用 Azure IoT 中樞。

***
**沒有套件嗎？**按一下[這裡](https://aka.ms/gateway-kit)。 **沒有 SensorTag？** [從模擬裝置開始](iot-hub-gateway-kit-c-sim-get-started.md)或[購買 SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)
***

## <a name="lesson-1-configure-your-nuc"></a>第 1 課：設定 NUC
![第 1 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

在這一課，您可以設定 hello 套件作為 Azure IoT 閘道 （下一個單位的運算） 的 Intel NUC、 NUC，在安裝 hello Azure IoT 邊緣套件並執行範例應用程式 tooverify hello 閘道功能。

*估計時間 toocomplete: 15 分鐘*

跳過[Intel NUC 為 IoT 閘道設定](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)

## <a name="lesson-2-create-your-iot-hub"></a>第 2 課：建立 IoT 中樞
![第 2 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

在這一課，您在主機電腦上安裝 hello 工具和軟體。 然後您建立免費的 Azure 帳戶、 佈建您的 Azure IoT 中樞和 hello IoT 中樞中建立您的第一個裝置。

開始本課程前，請先完成第 1 課。

### <a name="get-hello-tools"></a>取得 hello 工具
主機電腦上安裝 hello 工具和軟體。

*估計時間 toocomplete: 20 分鐘*

跳過[取得 hello 工具](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)

### <a name="create-an-iot-hub-and-register-your-device"></a>建立 IoT 中樞並登錄您的裝置
建立資源群組中，佈建第一個的 Azure IoT 中樞，並加入使用 hello Azure CLI 您第一次裝置 toohello IoT 中樞。

*估計時間 toocomplete: 10 分鐘*

跳過[建立 IoT 中樞，並註冊您的裝置](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a>第 3 課︰接收來自 SensorTag 的訊息，並從您的 IoT 中心讀取訊息
在這一課，您將使用指令碼 tooautomate hello 組態和執行 b 範例應用程式在您的閘道。 這類應用程式使用的模組 tooaggregate 和轉換資料收集、 處理命令，或執行任意數目的相關工作。 模組之間透過訊息代理程式相互通訊。 hello 範例應用程式具有 b 模組與 IoT 中樞模組。 hello b 模組 B SensorTag 接收資料。 hello 收到 hello 資料，並將它的 Azure IoT Edge 傳送 tooyour IoT 中樞透過 hello 閘道架構提供 IoT 中樞模組封裝。

![第 3 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a>設定及執行 hello b 範例應用程式
設定 hello SensorTag 和閘道之間的連線。 然後完成 hello 設定並執行 hello b 範例應用程式。

*估計時間 toocomplete: 15 分鐘*

跳過[設定和執行的 hello b 範例應用程式](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

### <a name="read-messages-from-your-iot-hub"></a>讀取來自 IoT 中樞的傳入訊息
執行範例程式碼在您的主機電腦 tooread 訊息從 IoT 中樞。

*估計時間 toocomplete: 15 分鐘*

跳過[從 IoT 中樞讀取訊息](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="lesson-4-save-messages-tooazure-table-storage"></a>第 4 課： 將訊息儲存 tooAzure 資料表儲存體
建立從 IoT 中樞取得內送訊息，並將其寫入 tooAzure 資料表儲存體的 Azure 函式應用程式。

![第 4 課端對端圖表](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a>建立 Azure 函數應用程式與 Azure 儲存體帳戶
Azure 的函式應用程式與 Azure 儲存體帳戶，請使用 Azure Resource Manager 範本 toocreate。

*估計時間 toocomplete: 10 分鐘*

跳過[建立 Azure 的函式應用程式與 Azure 儲存體帳戶](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)

### <a name="read-messages-persisted-in-azure-table-storage"></a>讀取保存在 Azure 表格儲存體中的訊息
當寫入 tooAzure 資料表儲存體監視 hello 閘道到雲端訊息。

*估計時間 toocomplete: 5 分鐘*

跳過[讀取訊息保存在 Azure 資料表儲存體](iot-hub-gateway-kit-c-lesson4-read-table-storage.md)。

## <a name="troubleshooting"></a>疑難排解
如果您在 hello 課程期間有任何問題，尋找在 hello 解決方案[疑難排解](iot-hub-gateway-kit-c-troubleshooting.md)發行項。

## <a name="explore-more"></a>探索更多
請瀏覽 hello [Intel IoT 閘道套件開發人員區域](http://software.intel.com/iot/microsoft-azure)toolearn 更多。
