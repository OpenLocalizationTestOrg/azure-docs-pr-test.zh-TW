---
title: "連接 （節點） 的 Intel Edison tooAzure IoT-第 2 課： Azure tools (Windows) |Microsoft 文件"
description: "在 Windows 7 和更新版本安裝 Python 和 hello Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 雲端服務, arduino 雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 60631b54-6d2e-4e8a-88bf-7c2f8e7e1f29
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0a2e941119f9106add708591d52f32eb9ed08451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>取得 Azure 工具 (Windows 7 和更新版本)
> [!div class="op_single_selector"]
> * [Windows 7 和更新版本][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>將執行的作業
安裝 Python 和 hello Azure 命令列介面 (Azure CLI)。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

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

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. 執行下列命令的 hello 驗證 hello 安裝：

   ```cmd
   az iot -h
   ```

您會看到下列 hello 輸出 hello 安裝是否成功。

![表示成功的輸出](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>摘要
您已安裝 hello Azure CLI。 您的下一步 工作使用 hello Azure CLI toocreate 您的 Azure IoT 中樞和裝置身分識別。

## <a name="next-steps"></a>後續步驟
[建立 IoT 中樞並登錄 Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
