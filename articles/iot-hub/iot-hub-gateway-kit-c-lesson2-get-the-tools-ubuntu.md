---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 2 課︰取得工具 (Ubuntu) | Microsoft Docs"
description: "執行 Ubuntu 的主機電腦上安裝 hello 工具和 hello 軟體建立 IoT 中心時，在 hello IoT 中樞註冊您的裝置。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 開發, iot 軟體, iot 雲端服務, 物聯網軟體, azure cli, 在 ubuntu 上安裝 git, gulp 執行, 安裝 node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>取得 hello 工具 (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 或更新版本](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>將執行的作業

- 安裝 Git、Node.js、Gulp、Python。
- 安裝 hello Azure 命令列介面 (Azure CLI)。 

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。
## <a name="what-you-will-learn"></a>學習目標

在這一課，您將了解：

- 如何 tooinstall Git 和 Node.js。
  - Git 是一個開放原始碼分散式版本控制系統。 本課程中的 hello 範例應用程式會儲存在 Git。
  - Node.js 是一個具有豐富套件生態系統的 JavaScript 執行階段。
- 如何 toouse NPM tooinstall Node.js 開發工具。
  - hello 的最低必要的版本 Node.js 是 4.5 LTS。
  - NPM 是一個 Node.js 的 hello 封裝管理員。
- 如何 tooinstall Visual Studio 程式碼。
  - Visual Studio Code 是一個跨平台、輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。 它對偵錯、內嵌的 Git 控制項、語法反白顯示、智慧型程式碼完成、程式碼片段、程式碼重構也有絕佳的支援。
- 如何 tooinstall hello Azure CLI
  - hello Azure CLI 提供 Azure 的多平台命令列體驗。 您可以直接從命令列 tooprovision 工作和管理資源。
- 如何 toouse hello Azure CLI toocreate IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

- 網際網路連線 toodownload hello 工具和軟體。
- 一部執行 Ubuntu 16.04 或以上版本的電腦。

## <a name="install-git-and-nodejs"></a>安裝 Git 和 Node.js

tooinstall Git 和 Node.js，請遵循下列步驟：

1. 按`Ctrl + Alt + T`tooopen 終端機。
2. 執行下列命令的 hello:

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>安裝 Node.js 開發工具

您使用[cwd](http://gulpjs.com/) tooautomate 部署和執行指令碼。

tooinstall gulp，執行下列命令在 hello 終端機中的 hello:

```bash
sudo npm install -g gulp
```

如果您遇到 hello 安裝問題，請參閱 hello[疑難排解指南](iot-hub-gateway-kit-c-troubleshooting.md)解決方案 toocommon 問題。

> [!Note]
> 節點、 NPM 及 Gulp 是在 Node.js 中開發的必要的 toorun 自動化指令碼。

## <a name="install-hello-azure-cli"></a>安裝 hello Azure CLI

tooinstall hello Azure CLI，請遵循下列步驟：

1. 執行下列命令在 hello 終端機的 hello:

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   hello 安裝可能需要 5 分鐘。

2. 執行下列命令的 hello 驗證 hello 安裝：

   ```bash
   az iot -h
   ```
您應該會看到下列 hello 輸出 hello 安裝是否成功。
![確認 Azure CLI 安裝](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>安裝 Visual Studio Code

您稍後在 hello 教學課程 tooedit 組態檔中使用 Visual Studio 程式碼。

[下載](https://code.visualstudio.com/docs/setup/linux)並安裝 Visual Studio Code。

## <a name="summary"></a>摘要

您已在主機電腦上安裝所有必要的 hello 工具和軟體。 下一個工作是 toouse hello Azure CLI toocreate IoT 中樞，並在您的 IoT 中樞註冊您的裝置。

## <a name="next-steps"></a>後續步驟
[建立 IoT 中樞並登錄您的裝置](iot-hub-gateway-kit-c-lesson2-register-device.md)
