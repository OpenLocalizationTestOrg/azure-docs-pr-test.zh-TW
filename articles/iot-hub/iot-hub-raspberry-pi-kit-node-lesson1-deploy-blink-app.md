---
featureFlags: usabilla
title: "將 Raspberry Pi (節點) 連接到 Azure IoT - 第 1 課：部署應用程式 | Microsoft Docs"
description: "從 GitHub 複製範例 Node.js 應用程式，並複製 gulp 以將此應用程式部署至您的 Raspberry Pi 3 面板。 此範例應用程式會讓與面板連接的 LED 每兩秒閃爍一次。"
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
ms.openlocfilehash: 8b73000c166950172c07b8e188025dc9da5bc011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>建立並部署閃爍應用程式
## <a name="what-you-will-do"></a>將執行的作業
從 GitHub 複製範例 Node.js 應用程式，並使用 gulp 工具將範例應用程式部署至您的 Raspberry Pi 3。 範例應用程式會讓與面板連接的 LED 每兩秒閃爍一次。 如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)尋求解決方案。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：

* 如何使用 `device-discover-cli` 工具擷取關於 Pi 的網路資訊。
* 如何在 Pi 上部署和執行範例應用程式。
* 如何在 Pi 上部署和偵錯遠端執行的應用程式。

## <a name="what-you-need"></a>您需要什麼
您必須已順利完成下列作業︰

* [設定裝置](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [取得工具](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a>取得 Pi 的 IP 位址和主機名稱
在 Windows 開啟命令提示字元或在 macOS 或 Ubuntu 開啟終端機，然後執行下列命令︰

```bash
devdisco list --eth
```

您應該會看到如下所示的輸出：

![裝置探索](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

記下 Pi 的 `IP address` 和 `hostname`。 本文稍後需要此資訊。

> [!NOTE]
> 請確定 Pi 是連接到與您電腦相同的網路。 例如，如果您的電腦連線到無線網路，而 Pi 連線到有線網路，您可能不會在 devdisco 輸出中看到 IP 位址。

## <a name="clone-the-sample-application"></a>複製範例應用程式
若要開啟範例程式碼，請遵循下列步驟：

1. 執行下列命令，從 GitHub 複製範例儲存機制︰
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. 執行下列命令來在 Visual Studio Code 中開啟範例應用程式︰
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![儲存機制結構](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

`app` 子資料夾中的 `app.js` 檔案是包含 LED 控制程式碼的關鍵來源檔案。

### <a name="install-application-dependencies"></a>安裝應用程式相依性
執行下列命令，安裝範例應用程式需要的程式庫和其他模組︰

```bash
npm install
```

## <a name="configure-the-device-connection"></a>設定裝置連線
若要設定裝置連線，請遵循下列步驟：

1. 執行下列命令來產生裝置組態檔：
   
   ```bash
   gulp init
   ```
   
   組態檔 `config-raspberrypi.json` 包含您用來登入 Pi 的使用者認證。 為了避免使用者認證外流，組態檔會產生於電腦主資料夾的 `.iot-hub-getting-started` 子資料夾中。

2. 執行下列命令在 Visual Studio Code 中開啟裝置組態檔：
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. 使用先前在＜取得 Pi 的 IP 位址和主機名稱＞中取得的 IP 位址和主機名稱取代預留位置 `[device hostname or IP address]`。
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> 在連接到 Raspberry Pi 時，您可以使用 SSH 金鑰而非使用者名稱和密碼。 若要這樣做您必須產生索引鍵使用**透過像是**和**@ ssh-複製-識別碼 pi\<裝置位址\>**。
>
> 在 Windows 上，可在 **Git Bash** 中使用這些命令。
>
> 在 MacOS 上，則必須執行 **brew install ssh-copy-id**。
>
> 成功將金鑰上傳至 Raspberry Pi 後，請將 **device_password** 替換為 **config-raspberrypi.json** 中的 **device_key_path** 屬性。
>
> 更新的程式碼行應該如下所示︰
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

恭喜！ 您已成功建立 Pi 的第一個範例應用程式。

## <a name="deploy-and-run-the-sample-application"></a>部署和執行範例應用程式
### <a name="install-nodejs-and-npm-on-pi"></a>在 Pi 上安裝 Node.js 和 NPM
執行下列命令，在 Pi 上安裝 Node.js 和 NPM︰

```bash
gulp install-tools
```

第一次執行此工作時，可能需要 10 分鐘才會完成。

### <a name="deploy-and-run-the-sample-app"></a>部署和執行範例應用程式
執行下列命令，部署和執行範例應用程式：

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a>確認應用程式可以運作
您現在應該會看到 Pi 上的 LED 每兩秒閃爍一次。  如果 LED 沒有閃爍，請參閱[疑難排解指南](iot-hub-raspberry-pi-kit-node-troubleshooting.md)，裡面有常見問題的解決方案。
![LED 閃爍](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>摘要
您已安裝必要工具來使用 Pi，並已在 Pi 上部署範例應用程式來讓 LED 閃爍。 現在，您可以建立、部署和執行另一個範例應用程式，將 Pi 連線至 Azure IoT 中樞來傳送和接收訊息。

## <a name="next-steps"></a>後續步驟
[取得 Azure 工具](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

