---
title: "連接 Arduino tooAzure IoT-第 2 課： Azure tools (Windows) |Microsoft 文件"
description: "在 Windows 7 和更新版本安裝 Python 和 hello Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 雲端服務, arduino 雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 70dfff14-4be1-468d-9919-e40f4bead308
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9b891224ff3974d9ce5382eb983470d5d41bcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>取得 Azure 工具 (Windows 7 和更新版本)

> [!div class="op_single_selector"]
> * [Windows 7 或更新版本][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>將執行的作業

安裝 Python 和 hello Azure 命令列介面 (Azure CLI)。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)Adafruit 羽毛 M0 WiFi Arduino 版。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 如何 tooinstall Python。
* 如何 tooinstall hello Azure CLI。

## <a name="what-you-need"></a>您需要什麼
* 一部具有網際網路連線的 Windows 電腦。
* 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。

## <a name="install-python"></a>安裝 Python
在 Windows 電腦上[安裝 Python](https://www.python.org/downloads/)。 您可以安裝 Python 2.7、3.4 或 3.5。 本教學課程是以 Python 2.7 為依據。 如果您已經安裝 Python，移 toohello 下一節，並安裝 hello Azure CLI。

您也需要 hello 資料夾其中 python.exe 和 pip.exe 是 已安裝的 toohello 系統 tooadd hello 路徑`PATH`環境變數。 根據預設，python.exe 是安裝在 `C:\Python27`，而 pip.exe 是安裝在 `C:\Python27\Scripts`。

## <a name="install-hello-azure-cli"></a>安裝 hello Azure CLI
hello Azure CLI 提供 Azure 的多平台命令列體驗。 您可以直接從命令列 tooprovision 工作和管理資源。

tooinstall hello Azure CLI，請遵循下列步驟：

1. 以系統管理員身分開啟 [命令提示字元] 視窗。
2. 執行下列命令的 hello:

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. 執行下列命令的 hello 驗證 hello 安裝：

   ```bash
   az iot -h
   ```

您會看到下列 hello 輸出 hello 安裝是否成功。

![表示成功的輸出][output]

## <a name="summary"></a>摘要
您已安裝 hello Azure CLI。 您的下一步 工作使用 hello Azure CLI toocreate 您的 Azure IoT 中樞和裝置身分識別。

## <a name="next-steps"></a>後續步驟
[建立 IoT 中樞並註冊您的 Arduino 面板][create-your-iot-hub-and-register-your-arduino-board]


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_win.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md