---
title: "將 Raspberry Pi (節點) 連接到 Azure IoT - 第 1 課：取得工具 (Windows) | Microsoft Docs"
description: "在 Windows 7 和更新版本上，針對 Pi 的第一個範例應用程式下載並安裝必要的工具和軟體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 開發, iot 軟體, 物聯網軟體, 在 windows 上安裝 git, gulp , 在 windows 上安裝 node js, 在 windows 上安裝 npm, 在 windows 上安裝 python"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 24c58e006bbef9bbc1fcd626a0f8f6bcac063f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a>取得工具 (Windows 7 或更新版本)

> [!div class="op_single_selector"]
> * [Windows 7 或更新版本](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a>將執行的作業
下載您 Raspberry Pi 3 第一個範例應用程式的開發工具和軟體。 如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)尋求解決方案。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：

* 如何安裝 Git 和 Node.js。
  * [Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。 本文的範例應用程式將會儲存在 Git 上。
  * [Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。
* 如何使用 NPM 安裝額外的 Node.js 開發工具。
  * Node.js 的最低版本需求為 4.5 LTS。
  * [NPM](https://www.npmjs.com) 是 Node.js 的其中一個套件管理員。

## <a name="what-you-need"></a>您需要什麼
若要完成此作業，您需要：

* 網際網路連線以下載開發工具和軟體。
* 一部執行 Windows 的電腦。

## <a name="install-git-and-nodejs"></a>安裝 Git 和 Node.js
按一下下列連結以下載並安裝 Git for Windows 和適用於 Windows 的 Node.js LTS。

* [取得 Git for Windows](https://git-scm.com/download/win/)
* [取得適用於 Windows 的 Node.js LTS](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>安裝額外的 Node.js 開發工具
使用 [gulp.js](http://gulpjs.com) 對 Pi 自動部署範例應用程式。 您也會使用 [device-discovery-cli](https://github.com/Azure/device-discovery-cli)來擷取關於您 IoT 裝置的網路資訊。

以系統管理員身分開啟命令提示字元。 執行下列命令以安裝 `gulp` 和 `device-discovery-cli`：

```bash
npm install -g device-discovery-cli gulp
```

如果您於電腦上安裝 Node.js 和這些額外的 Node.js 開發工具時遇到問題，請參閱[疑難排解指南](iot-hub-raspberry-pi-kit-node-troubleshooting.md)以取得常見問題的解決方案。

## <a name="install-visual-studio-code"></a>安裝 Visual Studio Code
[下載](https://code.visualstudio.com/docs/setup/windows)並安裝 Visual Studio Code。 Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。 您可以稍後於教學課程中使用此編輯器來編輯範例程式碼。

## <a name="summary"></a>摘要
您已安裝第一個範例應用程式所需的開發工具和軟體。 下一個工作是在 Pi 上建立、部署和執行範例應用程式。

## <a name="next-steps"></a>後續步驟
[建立並部署閃爍範例應用程式](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

