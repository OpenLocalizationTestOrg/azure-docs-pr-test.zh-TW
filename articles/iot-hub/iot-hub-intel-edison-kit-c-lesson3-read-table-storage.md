---
title: "Connect Intel Edison (C) tooAzure IoT-第 3 課： 監視訊息 |Microsoft 文件"
description: "當寫入 tooyour Azure 資料表儲存體監視 hello 裝置到雲端訊息。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 雲端、 雲端資料收集、 iot 雲端服務、 iot 資料中的資料"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2679b22f2987f77ecd1eea03044ed8ea03bf73f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>讀取保存在 Azure 儲存體中的訊息
## <a name="what-you-will-do"></a>將執行的作業
監視從 Intel Edison tooyour IoT 中樞傳送 hello 訊息為 hello 裝置到雲端訊息會寫入 tooyour Azure 資料表儲存體。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將學習如何 toouse hello gulp 讀取訊息工作 tooread 訊息保存在您的 Azure 資料表儲存體。

## <a name="what-you-need"></a>您需要什麼
才能開始此程序，您必須先成功完成[執行 hello Azure 閃爍範例應用程式上 Intel Edison][run-the-azure-blink-sample-application-on-intel-edison]。

## <a name="read-new-messages-from-your-storage-account"></a>從您的儲存體帳戶讀取新訊息
在 hello 前一篇文章中，您可以執行範例應用程式 Edison 上。 hello 範例應用程式傳送訊息 tooyour Azure IoT 中樞。 傳送 tooyour IoT 中樞的 hello 訊息會儲存到您的 Azure 資料表儲存體，透過 hello Azure 函式應用程式。 您必須從您的 Azure 資料表儲存體的 hello Azure 儲存體連接字串 tooread 訊息。

tooread 訊息儲存在您的 Azure 資料表儲存體，請遵循下列步驟：

1. 藉由執行下列命令的 hello 收到 hello 連接字串：

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   hello 第一個命令會擷取 hello `storage name` hello 第二個命令 tooget hello 連接字串中使用。 使用`iot-sample`做為 hello 值`{resource group name}`如果您沒有變更 hello 值。
2. 開啟 hello 設定檔`config-edison.json`在 Visual Studio 程式碼執行下列命令的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. 取代`[Azure storage connection string]`hello 您在步驟 1 中取得的連接字串。
4. 儲存 hello`config-edison.json`檔案。
5. 重新傳送訊息，並從您的 Azure 資料表儲存體讀取透過執行下列命令的 hello:

   ```bash
   gulp run --read-storage
   ```

   hello 邏輯來讀取 Azure 資料表儲存體是在 hello`azure-table.js`檔案。

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a>摘要
您已成功連接 Edison tooyour IoT 中樞 hello 雲端中的，並使用 hello 閃爍範例應用程式 toosend 裝置到雲端訊息。 您也會使用 hello Azure 函式應用程式 toostore 傳入 IoT 中樞訊息 tooyour Azure 資料表儲存體。 您現在可以從您的 IoT 中樞 tooEdison 傳送雲端到裝置訊息。

## <a name="next-steps"></a>後續步驟
[執行範例應用程式 tooreceive 雲端到裝置訊息][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md