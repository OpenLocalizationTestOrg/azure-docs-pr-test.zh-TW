---
title: "將 Raspberry Pi (C) 連接到 Azure IoT - 第 2 課：Azure 工具 (macOS) | Microsoft Docs"
description: "在 macOS 上安裝 Python 與 Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 雲端服務, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3810990f4a27270fa45709f4d9dbb36a8f4369a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a>取得 Azure 工具 (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 和更新版本](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>將執行的作業
安裝 Azure 命令列介面 (Azure CLI)。 如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)尋求解決方案。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 如何安裝 Azure CLI。
* 如何新增 Azure CLI 的 IoT 子群組。

## <a name="what-you-need"></a>您需要什麼
* 有網際網路連線的 Mac。
* 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。

## <a name="install-python"></a>安裝 Python
雖然 macOS 有現成的 Python 2.7，但建議您透過 Homebrew 安裝 Python。 請參閱 [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/) (在 macOS 上安裝 Python)。

執行下列命令安裝 Python 與 pip：

```bash
brew install python
```

## <a name="install-the-azure-cli"></a>安裝 Azure CLI
Azure CLI 提供適用於 Azure 的多平台命令列體驗。 您可直接從命令列工作以佈建和管理資源。 

若要安裝最新的 Azure CLI，請遵循下列步驟：

1. 在終端機視窗中執行下列命令。 安裝 Azure CLI 可能需要五分鐘的時間。

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. 執行下列命令以驗證安裝：

   ```bash
   az iot -h
   ```

如果已成功安裝，您應該會看見下列輸出。

![表示成功的輸出](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>摘要
您已安裝 Azure CLI。 下一個工作是使用 Azure CLI 建立 Azure IoT 中樞和裝置身分識別。

## <a name="next-steps"></a>後續步驟
[建立 IoT 中樞並登錄 Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

