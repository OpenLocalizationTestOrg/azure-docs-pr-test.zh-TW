---
featureFlags: usabilla
title: "連接覆盆子 Pi （節點） tooAzure IoT-第 1 課： 將應用程式部署 |Microsoft 文件"
description: "複製 hello 範例 Node.js 應用程式從 GitHub，而且這個應用程式 tooyour 覆盆子 Pi 3 版的 gulp toodeploy。 此範例應用程式會閃爍 hello LED 連接 toohello 面板每隔兩秒鐘。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "raspberry pi led 閃爍, raspberry pi 上的閃爍 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9732df3009b8342d4872fe2318a975a6251e772b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>建立及部署 hello 閃爍應用程式
## <a name="what-you-will-do"></a>將執行的作業
複製從 GitHub hello 範例 Node.js 應用程式，並使用 hello gulp 工具 toodeploy hello 範例應用程式 tooyour 覆盆子 Pi 3。 hello 範例應用程式會閃爍 hello LED 連接 toohello 面板每隔兩秒鐘。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：

* 如何 toouse hello`device-discover-cli`工具 tooretrieve 網路 Pi 的相關資訊。
* 如何 toodeploy 和執行的 hello 範例 pi 的應用程式。
* 如何從遠端執行 pi toodeploy 和偵錯應用程式。

## <a name="what-you-need"></a>您需要什麼
您必須先成功完成下列作業的 hello:

* [設定裝置](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [取得 hello 工具](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a>取得 hello IP 位址和主機名稱的 Pi
開啟命令提示字元在視窗中或在 macOS 或 Ubuntu，終端機，然後執行下列命令的 hello:

```bash
devdisco list --eth
```

您應該會看到類似 toohello 下列輸出：

![裝置探索](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

記下 hello`IP address`和`hostname`Pi。 本文稍後需要此資訊。

> [!NOTE]
> 請確定 Pi 為您的電腦相同網路的連線的 toohello。 例如，如果您的電腦是連線的 tooa 無線網路，Pi 是連接的 tooa 有線網路時，您可能不會看到 hello IP 位址 hello devdisco 輸出中的。

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式
tooopen hello 範例程式碼，請遵循下列步驟：

1. 藉由執行下列命令的 hello 複製從 GitHub hello 範例儲存機制：
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. 開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![儲存機制結構](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

hello`app.js`檔案在 hello`app`子資料夾是包含 hello 程式碼 toocontrol hello LED 的 hello 金鑰來源檔案。

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
   
   hello 設定檔`config-raspberrypi.json`包含 toolog 用於 tooPi hello 使用者認證。 tooavoid hello 流失 hello 設定檔產生 hello 子資料夾中的使用者認證`.iot-hub-getting-started`hello 您電腦上的主資料夾。

2. 開啟 Visual Studio 程式碼中的 hello 裝置組態檔，藉由執行下列命令的 hello:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. 取代 hello 預留位置`[device hostname or IP address]`hello IP 位址或您先前有"取得 hello IP 位址和主機名稱的 Pi。"中的 hello 主機名稱
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> 連接 tooRaspberry Pi 時，您可以使用 SSH 金鑰而不是使用者名稱和密碼。 在順序 toodo 此您將需要 toogenerate hello 索引鍵使用**透過像是**和**@ ssh-複製-識別碼 pi\<裝置位址\>**。
>
> 在 Windows 上，可在 **Git Bash** 中使用這些命令。
>
> 您需要 toorun MacOS **brew 安裝 ssh-複製-識別碼**。
>
> 已成功上傳之後 hello 金鑰 toohello 覆盆子 Pi，取代**device_password**與**device_key_path**屬性**config raspberrypi.json**。
>
> 更新的程式碼行應該如下所示︰
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

恭喜！ 您已成功建立 hello 第一個範例應用程式 Pi。

## <a name="deploy-and-run-hello-sample-application"></a>部署和執行 hello 範例應用程式
### <a name="install-nodejs-and-npm-on-pi"></a>在 Pi 上安裝 Node.js 和 NPM
執行下列命令的 hello pi 安裝 Node.js 及 NPM:

```bash
gulp install-tools
```

這項工作可能需要 10 分鐘 toocomplete hello 執行它的第一次。

### <a name="deploy-and-run-hello-sample-app"></a>部署和執行 hello 範例應用程式
部署和執行 hello 範例應用程式藉由執行下列命令的 hello:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>確認 hello 應用程式可運作
您現在應該看到 hello LED Pi 閃爍每隔兩秒鐘。  如果您沒有看到 hello LED 閃爍不停，請參閱 hello[疑難排解指南](iot-hub-raspberry-pi-kit-node-troubleshooting.md)解決方案 toocommon 問題。
![LED 閃爍](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>摘要
安裝所需的 hello 工具 toowork 使用 Pi 和部署範例應用程式 tooPi tooblink hello LED。 您現在可以建立、 部署和執行另一個連接 Pi tooAzure IoT 中樞 toosend 範例應用程式和接收訊息。

## <a name="next-steps"></a>後續步驟
[取得 hello Azure tools](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

