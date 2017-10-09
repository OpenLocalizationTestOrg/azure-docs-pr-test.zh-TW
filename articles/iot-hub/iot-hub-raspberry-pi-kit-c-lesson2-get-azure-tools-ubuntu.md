---
title: "Connect Raspberry Pi (C) tooAzure IoT-第 2 課： Azure tools (Ubuntu) |Microsoft 文件"
description: "在 Ubuntu 上安裝 Python 與 Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 雲端服務, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a03512f2-fabe-40c5-8505-b93eef8e5bec
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1af4848f9fe0508e362c15b36eec8a35aea9ac5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>取得 Azure 工具 (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 和更新版本](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>將執行的作業
安裝 hello Azure 命令列介面 (Azure CLI)。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 如何 tooinstall hello Azure CLI。
* 如何 tooadd 的 hello Azure CLI IoT 子群組。

## <a name="what-you-need"></a>您需要什麼
* 一部具有網際網路連線的 Ubuntu 電腦。
* 有效的 Azure 訂用帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。

## <a name="install-hello-azure-cli"></a>安裝 hello Azure CLI
提供以多平台命令列體驗 azure，讓您直接從命令列 tooprovision toowork hello Azure CLI，並管理資源。

tooinstall hello 最新的 Azure CLI，請遵循下列步驟：

1. 執行下列命令在 terminal 視窗中的 hello。 可能需要五分鐘 tooinstall hello Azure CLI。

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. 執行下列命令的 hello 驗證 hello 安裝：

   ```bash
   az iot -h
   ```

您應該會看到下列 hello 輸出 hello 安裝是否成功。

![表示成功的輸出](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>摘要
您已安裝 hello Azure CLI。 您的下一個工作是 toocreate 您的 Azure IoT 中樞與裝置身分識別使用 hello Azure CLI。

## <a name="next-steps"></a>後續步驟
[建立 IoT 中樞並登錄 Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

