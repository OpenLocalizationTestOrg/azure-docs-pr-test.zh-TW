---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 2 課︰取得工具 (macOS) | Microsoft Docs"
description: "您的 Mac 電腦上安裝工具、 建立 IoT 中樞和在 hello IoT 中樞註冊您的裝置。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 開發, iot 軟體, iot 雲端服務, 物聯網軟體, azure cli, 安裝 python mac, 在 mac 上安裝 git, gulp 執行, 安裝 node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a>取得 hello 工具 (MacOS)
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

- 如何 tooinstall [Git](https://git-scm.com/)和[Node.js](https://nodejs.org/en/)。
  - Git 是一個開放原始碼分散式版本控制系統。 本課程中的 hello 範例應用程式會儲存在 Git。
  - Node.js 是一個具有豐富套件生態系統的 JavaScript 執行階段。
- 如何 toouse [NPM](https://www.npmjs.com/) tooinstall Node.js 開發工具。
  - hello 的最低必要的版本 Node.js 是 4.5 LTS。
  - NPM 是一個 Node.js 的 hello 封裝管理員。
- 如何 tooinstall Visual Studio 程式碼。
  - Visual Studio Code 是一個跨平台、輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。 它對偵錯、內嵌的 Git 控制項、語法反白顯示、智慧型程式碼完成、程式碼片段、程式碼重構也有絕佳的支援。
- 如何 tooinstall Python。
  - Python 是普遍使用的高階、一般用途、解譯、動態的程式設計語言。
- 如何 tooinstall hello Azure CLI。
  - hello Azure CLI 提供 Azure 的多平台命令列體驗。 您可以直接從命令列 tooprovision 工作和管理資源。
- 如何 toouse hello Azure CLI toocreate IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

- 網際網路連線 toodownload hello 工具和軟體。
- 執行 OS X Yosemite (10.10) 或更新版本的 Mac 電腦。

## <a name="install-git-and-nodejs"></a>安裝 Git 和 Node.js

tooinstall Git 和 Node.js，請依照下列步驟使用 hello Homebrew 套件管理公用程式：

1. [下載](http://brew.sh/)並安裝 Homebrew。 如果您已經安裝 Homebrew，請移 toostep 2。
   1. 按`Cmd + Space`輸入`Terminal`tooopen 終端機。
   2. 執行下列命令的 hello:

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. 安裝 Git 和 Node.js 藉由執行下列命令的 hello:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>安裝 Node.js 開發工具

您使用[cwd](http://gulpjs.com/) tooautomate 部署和執行指令碼。

tooinstall gulp，執行下列命令在 hello 終端機中的 hello:

```bash
npm install -g gulp
```

如果您遇到 hello 安裝問題，請參閱 hello[疑難排解指南](iot-hub-gateway-kit-c-troubleshooting.md)解決方案 toocommon 問題。

> [!Note]
> 節點、 NPM 及 Gulp 是在 Node.js 中開發的必要的 toorun 自動化指令碼。

## <a name="install-python"></a>安裝 Python

雖然 Mac OS X 有 Python 2.7，但建議您透過 Homebrew 安裝 Python。 請參閱[在 Mac OS X 上安裝 Python](http://docs.python-guide.org/en/latest/starting/install/osx/)。

安裝 Python 和 pip 執行 hello 下列命令：

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>安裝 hello Azure CLI

tooinstall hello Azure CLI，請遵循下列步驟：

1. 執行下列命令在 hello 終端機的 hello:
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   hello 安裝可能需要 5 分鐘。

2. 執行下列命令的 hello 驗證 hello 安裝：
   ```bash
   az iot -h
   ```
   您應該會看到下列 hello 輸出 hello 安裝是否成功。

   ![確認 Azure CLI 安裝](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>安裝 Visual Studio Code

您稍後在 hello 教學課程 tooedit 組態檔中使用 Visual Studio 程式碼。

[下載](https://code.visualstudio.com/docs/setup/osx)並安裝 Visual Studio Code。

## <a name="summary"></a>摘要

您已在您的 Mac 電腦上安裝所有必要的 hello 工具和軟體。 下一個工作是 toouse hello Azure CLI toocreate IoT 中樞，並在您的 IoT 中樞註冊您的裝置。

## <a name="next-steps"></a>後續步驟
[建立 IoT 中樞並登錄裝置](iot-hub-gateway-kit-c-lesson2-register-device.md)
