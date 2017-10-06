---
title: "Connect Raspberry Pi (C) tooAzure IoT-第 2 課： 註冊裝置 |Microsoft 文件"
description: "建立資源群組、 建立 Azure IoT 中樞，並註冊 Pi hello Azure IoT 中樞中使用 Azure CLI hello。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspberry pi 雲端, pi 雲端連線"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 473658c5a8e1e0d4cfced0efafbad2640a1e0696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a>建立 IoT 中樞並登錄 Raspberry Pi 3
## <a name="what-you-will-do"></a>將執行的作業
* 建立資源群組。
* 建立您的 Azure IoT 中樞 hello 資源群組中。
* 使用 hello Azure 命令列介面 (Azure CLI)，以新增覆盆子 Pi 3 toohello Azure IoT 中樞。

當您使用 hello Azure CLI tooadd Pi tooyour IoT 中樞時，hello 服務就會產生與 hello 服務 Pi tooauthenticate 的索引鍵。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：
* 如何 toouse hello Azure CLI toocreate IoT 中樞。
* 如何 toocreate pi IoT 中樞中的裝置身分識別。

## <a name="what-you-need"></a>您需要什麼
* 一個 Azure 帳戶
* 在 Mac 或 hello Azure CLI 安裝的 Windows 電腦

## <a name="create-your-iot-hub"></a>建立 IoT 中樞
Azure IoT 中樞可以協助您連接、監視並管理數以百萬計的 IoT 資產。 toocreate IoT 中樞，請遵循下列步驟：

1. 登入 tooyour Azure 帳戶執行下列命令的 hello:

   ```bash
   az login
   ```

   成功登入之後，系統將會列出所有可用的訂用帳戶。

2. 設定您藉由執行下列命令的 hello 想 toouse hello 預設訂用帳戶：

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`可以找到 hello 輸出中的 hello`az login`或 hello`az account list`命令。

3. 執行下列命令的 hello 註冊 hello 提供者。 資源提供者是為應用程式提供資源的服務。 您必須先註冊 hello 提供者，才能部署 hello hello 提供者提供的 Azure 資源。

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. 藉由執行下列命令的 hello 的 hello 美國西部地區中建立資源群組名稱 iot 範例：

   ```bash
   az group create --name iot-sample --location westus
   ```

   `westus`是您在建立資源群組的 hello 位置。 如果您想 toouse 另一個位置，您可以執行`az account list-locations -o table`toosee 所有 hello Azure 支援的位置。
 
5. 建立 IoT 中樞 hello iot 範例資源群組中，執行下列命令的 hello:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   根據預設，hello 工具會在 hello 可用的定價層中，建立 IoT 中樞。 如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。

> [!NOTE]
> IoT 中樞 hello 名稱必須是全域唯一的。 您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。

## <a name="register-pi-in-your-iot-hub"></a>在 IoT 中樞中登錄 Pi
傳送訊息 tooyour IoT 中樞和接收訊息，或從 IoT 中樞的每個裝置必須註冊並提供唯一的識別碼。

執行下列命令在中樞登錄 Pi：

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a>摘要
您已建立 IoT 中樞，並在 IoT 中樞中搭配裝置識別登錄 Pi。 您已準備好 toolearn toosend 從 Pi tooyour IoT 中樞的訊息。

## <a name="next-steps"></a>後續步驟
[建立 Azure 的函式應用程式與 Azure 儲存體帳戶 tooprocess 和市集 IoT 中樞訊息](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md)。

