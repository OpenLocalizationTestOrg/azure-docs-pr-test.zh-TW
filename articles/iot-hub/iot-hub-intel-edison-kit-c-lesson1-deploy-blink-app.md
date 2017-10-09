---
title: "Connect Intel Edison (C) tooAzure IoT-第 1 課： 將應用程式部署 |Microsoft 文件"
description: "複製 hello 範例 C 應用程式從 GitHub，並執行 gulp toodeploy 此應用程式 tooyour Intel Edison 面板。 此範例應用程式會閃爍 hello LED 連接 toohello 面板每隔兩秒鐘。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino led 專案, arduino led 閃爍, arduino led 閃爍程式碼, arduino 閃爍程式, arduino 閃爍範例"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>建立及部署 hello 閃爍應用程式
## <a name="what-you-will-do"></a>將執行的作業
複製 hello 範例 C 應用程式從 GitHub，並使用 hello gulp 工具 toodeploy hello 範例應用程式 tooIntel Edison。 hello 範例應用程式會閃爍 hello LED 連接 toohello 面板每隔兩秒鐘。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

## <a name="what-you-will-learn"></a>學習目標
* 如何 toodeploy 和執行的 hello 範例 Edison 上的應用程式。

## <a name="what-you-need"></a>您需要什麼
您必須先成功完成下列作業的 hello:

* [設定裝置][configure-your-device]
* [取得 hello 工具][get-the-tools]

## <a name="open-hello-sample-application"></a>開啟 hello 範例應用程式
tooopen hello 範例應用程式，請遵循下列步驟：

1. 藉由執行下列命令的 hello 複製從 GitHub hello 範例儲存機制：

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. 開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![儲存機制結構][repo-structure]

hello 檔案在 hello`app`子資料夾是包含 hello 程式碼 toocontrol hello LED 的 hello 金鑰來源檔案。

### <a name="install-application-dependencies"></a>安裝應用程式相依性
安裝 hello 程式庫和其他您需要執行下列命令的 hello hello 範例應用程式的模組：

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>設定 hello 裝置連線
tooconfigure hello 裝置連線，請遵循下列步驟：

1. 執行下列命令的 hello 產生 hello 裝置組態檔：

   ```bash
   gulp init
   ```

   hello 設定檔`config-edison.json`包含 toolog 用於 tooEdison hello 使用者認證。 tooavoid hello 流失 hello 設定檔產生 hello 子資料夾中的使用者認證`.iot-hub-getting-started`hello 您電腦上的主資料夾。

2. 開啟 Visual Studio 程式碼中的 hello 裝置組態檔，藉由執行下列命令的 hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. 取代 hello 預留位置`[device hostname or IP address]`和`[device password]`hello IP 位址與密碼在上一課中標記為。

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

恭喜！ 您已成功建立 hello 第一個範例應用程式 Edison。

## <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a>Edison 上安裝 hello Azure IoT 中樞 SDK
執行下列命令的 hello Edison 上安裝 hello Azure IoT 中樞 SDK:

```bash
gulp install-tools
```

這項工作可能需要很長的時間 toocomplete，取決於您的網路連線。 它需要 toobe 只執行一次針對一個 Edison。

### <a name="deploy-and-run-hello-sample-app"></a>部署和執行 hello 範例應用程式
部署和執行 hello 範例應用程式藉由執行下列命令的 hello:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>確認 hello 應用程式可運作
hello 範例應用程式會自動終止之後 hello LED 閃爍的 20 倍。 如果您沒有看到 hello LED 閃爍不停，請參閱 hello[疑難排解指南][ troubleshooting]解決方案 toocommon 問題。

![LED 閃爍][led-blinking]

## <a name="summary"></a>摘要
您所需的 hello 工具 toowork 隨 Edison 並部署範例應用程式 tooEdison tooblink hello LED。 您現在可以建立、 部署和執行另一個連接 Edison tooAzure IoT 中樞 toosend 範例應用程式和接收訊息。

## <a name="next-steps"></a>後續步驟
[取得 hello Azure tools][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
