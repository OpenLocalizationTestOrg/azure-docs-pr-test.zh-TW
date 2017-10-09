---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 2 課：登錄裝置 | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot 中樞, 物聯網雲端, azure iot 中樞建立裝置, ti sensortag, ti ble"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a>建立 IoT 中樞並登錄您的裝置

## <a name="what-you-will-do"></a>將執行的作業

- 建立資源群組
- 建立您的第一個 IoT 中樞
- 在您的 IoT 中樞註冊您的裝置，使用 Azure CLI hello。 

當您在 IoT 中樞註冊您的裝置時，hello Azure IoT 中心服務會產生與 hello 服務您裝置 toouse tooauthenticate 的索引鍵。 

如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標

在這一課，您將了解：

- 如何 toouse hello Azure CLI toocreate IoT 中樞。
- 如何 tooregister IoT 中樞中的裝置。

## <a name="what-you-need"></a>您需要什麼

- 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。
- 您應該有的 hello Azure CLI 安裝。

## <a name="create-an-iot-hub"></a>建立 IoT 中樞

toocreate IoT 中樞，請遵循下列步驟：

1. 登入 tooyour Azure 帳戶執行下列命令的 hello:

   ```bash
   az login
   ```

   成功登入之後，系統會列出所有可用的訂用帳戶。

2. 設定 hello 預設您藉由執行下列命令的 hello 想 toouse 的 Azure 訂用帳戶：

   ```bash
   az account set --subscription {subscription id or name}
   ```

   `subscription ID or name`可以找到 hello 輸出中的 hello`az login`或 hello`az account list`命令。

3. 執行下列命令的 hello 註冊 hello 提供者。 資源提供者是為應用程式提供資源的服務。 您必須先註冊 hello 提供者，才能部署 hello hello 提供者提供的 Azure 資源。

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. 建立資源群組名稱為`iot-gateway`藉由執行下列命令的 hello hello 美國西部區域中：

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   `westus`是您在建立資源群組的 hello 位置。 如果您想 toouse 另一個位置，您可以執行`az account list-locations -o table`toosee 所有 hello Azure 支援的位置。

5. 在 hello 建立 IoT 中樞`iot-gateway`資源群組，藉由執行下列命令的 hello:

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

根據預設，hello 工具會在 hello 可用的定價層中，建立 IoT 中樞。 如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。

> [!NOTE]
> IoT 中樞 hello 名稱必須是全域唯一的。 您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。

## <a name="register-your-device-in-your-iot-hub"></a>在 IoT 中樞登錄您的裝置

傳送訊息 tooyour IoT 中樞和接收訊息，或從 IoT 中樞的每個裝置必須註冊並提供唯一的識別碼。
執行下列命令在 Azure IoT 中樞中登錄您的裝置：

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a>摘要

您已建立 IoT 中樞，並在 IoT 中樞中登錄您的邏輯裝置及裝置身分識別。 您已準備好 toolearn tooconfigure 並從您的實體裝置 tooyour IoT 中樞 hello 中執行的閘道範例應用程式 toosend 資料的雲端。

## <a name="next-steps"></a>後續步驟
[設定和執行 BLE 範例應用程式](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)