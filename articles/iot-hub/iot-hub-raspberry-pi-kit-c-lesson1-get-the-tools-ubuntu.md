---
title: "Connect Raspberry Pi (C) tooAzure IoT-第 1 課： 取得工具 (Ubuntu) |Microsoft 文件"
description: "下載並安裝 hello 必要工具及軟體 hello 第一個範例應用程式 Pi Ubuntu 上。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 開發, iot 軟體, 物聯網軟體, 在 ubuntu 上安裝 git, gulp 執行, 安裝 node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 794928b5da63521cb0a72cb54256f2ad9724ec84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>取得 hello 工具 (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 或更新版本](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>將執行的作業
下載 hello 開發工具及 hello 第一個範例應用程式程式覆盆子 Pi 3 hello 軟體。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)。

> [!NOTE]
> 雖然 hello 程式設計語言的 hello 主要邏輯是 C 的 Node.js 工具會用於 hello 課程 toodiscover 裝置，並建置和部署範例應用程式。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：

* 如何 tooinstall Git 和 Node.js
  * [Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。 這個發行項的 hello 範例應用程式會儲存在 Git。
  * [Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。
* 如何 toouse NPM tooinstall 其他 Node.js 開發工具。
  * hello 的最低必要的版本 Node.js 是 4.5 LTS。
  * [NPM](https://www.npmjs.com)是其中一個 hello for Node.js 的封裝管理員。

## <a name="what-you-need"></a>您需要什麼
toocomplete 這項作業，您將需要：

* 網際網路連線 toodownload hello 開發工具和 hello 軟體。
* 一部執行 Ubuntu 16.04 或以上版本的電腦。

## <a name="install-git-nodejs-and-npm"></a>安裝 Git、Node.js 及 NPM
使用 hello 鍵盤快速鍵`Ctrl + Alt + T`tooopen 終端機及執行 hello，下列命令：

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>安裝額外的 Node.js 開發工具
使用[cwd](http://gulpjs.com) hello 範例應用程式 tooPi tooautomate hello 部署。 使用 hello[裝置-探索-cli](https://github.com/Azure/device-discovery-cli) tooretrieve IoT 裝置相關的網路資訊。

安裝`gulp`和`device-discovery-cli`藉由執行下列命令在 hello 終端機中的 hello:

```bash
sudo npm install -g device-discovery-cli gulp
```

如果您遇到安裝 Node.js 和這些額外的開發工具在 Ubuntu 上的問題，請參閱 hello[疑難排解指南](iot-hub-raspberry-pi-kit-c-troubleshooting.md)解決方案 toocommon 問題。

## <a name="install-visual-studio-code"></a>安裝 Visual Studio Code
[下載](https://code.visualstudio.com/docs/setup/linux)並安裝 Visual Studio Code。 Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。 您可以使用此編輯器 hello 教學課程 tooedit hello 範例程式碼中的更新版本。

## <a name="summary"></a>摘要
您已安裝所需的 hello 開發工具及軟體 hello 第一個範例應用程式。 hello 下一個工作是 toocreate、 部署和執行 pi 的 hello 範例應用程式。

## <a name="next-steps"></a>後續步驟
[建立及部署 hello 閃爍應用程式](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

