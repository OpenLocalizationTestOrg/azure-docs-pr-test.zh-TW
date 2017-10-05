---
title: "將 Arduino 連線至 Azure IoT - 第 2 課：取得工具 (Ubuntu) | Microsoft Docs"
description: "在 Ubuntu 上安裝 Python 與 Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 雲端服務, arduino 雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a2f83e59a37abc3f44e770b22ac089b88481a6a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>取得 Azure 工具 (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 或更新版本][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>將執行的作業

安裝 Azure 命令列介面 (Azure CLI)。 如果您有任何問題，請在 Adafruit Feather M0 WiFi Arduino 面版的[疑難排解頁面](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)尋求解決方案。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 如何安裝 Azure CLI。
* 如何新增 Azure CLI 的 IoT 子群組。

## <a name="what-you-need"></a>您需要什麼
* 一部具有網際網路連線的 Ubuntu 電腦。
* 有效的 Azure 訂用帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。

## <a name="install-the-azure-cli"></a>安裝 Azure CLI
Azure CLI 能為 Azure 提供多平台的命令列體驗，使您可以直接從命令列進行資源的佈建及管理。

若要安裝最新的 Azure CLI，請遵循下列步驟：

1. 在終端機視窗中執行下列命令。 安裝 Azure CLI 可能需要五分鐘的時間。

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. 執行下列命令以驗證安裝：

   ```bash
   az iot -h
   ```

如果已成功安裝，您應該會看見下列輸出。

![表示成功的輸出][output]

## <a name="summary"></a>摘要
您已安裝 Azure CLI。 下一個工作是使用 Azure CLI 建立 Azure IoT 中樞和裝置身分識別。

## <a name="next-steps"></a>後續步驟
[建立 IoT 中樞並註冊您的 Arduino 面板][create-your-iot-hub-and-register-your-arduino-board]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md