---
title: "連接覆盆子 Pi （節點） tooAzure IoT-第 2 課： 取得工具 (Ubuntu) |Microsoft 文件"
description: "安裝 Python 和 macOS 上 hello Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 雲端服務, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 1814b703-2d81-45db-aff0-eb338c97f120
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3f35fae53a360a758bc8f61ed2063f7e2f2dc067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>取得 Azure 工具 (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 和更新版本](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>將執行的作業
安裝 hello Azure 命令列介面 (Azure CLI)。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 如何 tooinstall Azure CLI。
* 如何 tooadd 的 hello Azure CLI IoT 子群組。

## <a name="what-you-need"></a>您需要什麼
* 有網際網路連線的 Mac。
* 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。

## <a name="install-python"></a>安裝 Python
雖然 macOS 隨附 Python 2.7 hello 立即可用，但我們建議您安裝 Homebrew 透過 Python。 請參閱 [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/) (在 macOS 上安裝 Python)。

安裝 Python 和 pip 執行 hello 下列命令：

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>安裝 hello Azure CLI
hello Azure CLI 提供 Azure 的多平台命令列體驗。 您可以直接從您的命令列 tooprovision 工作和管理資源。 

tooinstall hello 最新的 Azure CLI，請遵循下列步驟：

1. 執行下列命令在 terminal 視窗中的 hello。 可能需要五分鐘 tooinstall hello Azure CLI。

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. 執行下列命令的 hello 驗證 hello 安裝：

   ```bash
   az iot -h
   ```

您應該會看到下列 hello 輸出 hello 安裝是否成功。

![表示成功的輸出](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>摘要
您已安裝 hello Azure CLI。 您的下一個工作是 toocreate 使用您 Azure IoT 中樞和裝置身分識別 hello Azure CLI。

## <a name="next-steps"></a>後續步驟
[建立 IoT 中樞並登錄 Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

