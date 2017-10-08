---
title: "aaaUnderstand hello Azure IoT Sdk |Microsoft 文件"
description: "開發人員指南 》 的相關資訊和連結 toohello 各種 Azure IoT 裝置和服務的 Sdk，您可以使用 toobuild 裝置應用程式和後端應用程式。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a>了解和使用 Azure IoT SDK

有三種類別的 SDK 可與 IoT 中樞搭配使用：

* **裝置 Sdk** toobuild IoT 裝置執行的應用程式可讓您。 這些應用程式傳送遙測 tooyour IoT 中樞，並選擇性地從 IoT 中心接收訊息。

* **服務 Sdk**啟用您 toomanage IoT 中樞，並選擇性地將訊息傳送 tooyour IoT 裝置。

* **Azure IoT 邊緣**可讓您不使用其中一個支援的 hello 通訊協定，或當您需要在 hello 邊緣 tooprocess 訊息 toobuild 閘道 tooenable 裝置。

Sdk 會提供 toosupport 多種程式設計語言。

## <a name="azure-iot-device-sdks"></a>Azure IoT 裝置 SDK

hello Microsoft Azure IoT 裝置 Sdk 包含可協助建立裝置的程式碼，而且連接 tooand 的應用程式由 Azure IoT 中樞 services 管理。

hello 下列 Azure IoT 裝置 Sdk 會使用從 GitHub toodownload:

* 為了可攜性和廣泛平台相容性，以 ANSI C (C99) 撰寫之 [Azure IoT 裝置 SDK for C][lnk-c-device-sdk]。 有兩個裝置用戶端程式庫，c，hello 低階**iothub_client**和 hello**序列化程式**。
* [Azure IoT 裝置 SDK for .NET][lnk-dotnet-device-sdk]
* [Azure IoT 裝置 SDK for Java][lnk-java-device-sdk]
* [Azure IoT 裝置 SDK for Node.js][lnk-node-device-sdk]
* [適用於 Python 的 Azure IoT 裝置 SDK][lnk-python-device-sdk]

> [!NOTE]
> 請參閱 hello 讀我檔案 hello GitHub 儲存機制中的開發電腦上使用語言與平台專屬封裝管理員 tooinstall 二進位檔和相依性的相關資訊。
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>作業系統平台和硬體相容性

如需特定硬體裝置與 SDK 相容性的詳細資訊，請參閱 hello [IoT 裝置類別目錄的 Azure 認證][lnk-certified]。

## <a name="azure-iot-service-sdks"></a>Azure IoT 服務 SDK

hello Azure IoT 服務 Sdk 包含建置直接互動 IoT 中樞 toomanage 裝置和安全性的應用程式的程式碼 toofacilitate。

hello 下列 Azure IoT 服務 Sdk 是可從 GitHub toodownload:

* [Azure IoT 服務 SDK for .NET][lnk-dotnet-service-sdk]
* [Azure IoT 服務 SDK for Node.js][lnk-node-service-sdk]
* [Azure IoT 服務 SDK for Java][lnk-java-service-sdk]
* [適用於 Python 的 Azure IoT 服務 SDK][lnk-python-service-sdk]
* [適用於 C 的 Azure IoT 服務 SDK][lnk-c-service-sdk]

> [!NOTE]
> 請參閱 hello 讀我檔案 hello GitHub 儲存機制中的開發電腦上使用語言與平台專屬封裝管理員 tooinstall 二進位檔和相依性的相關資訊。

## <a name="azure-iot-edge"></a>Azure IoT Edge

Azure IoT 邊緣包含 hello 基礎結構和模組 toocreate IoT 閘道的解決方案。 您可以擴充 IoT 邊緣 toocreate 閘道量身訂做的 tooany 端對端案例。

您可以從 GitHub 下載 [Azure IoT Edge][lnk-iot-edge]。

## <a name="online-api-reference-documentation"></a>線上 API 參考文件

hello 下列清單包含連結 tooonline API 參考文件的 Azure IoT 裝置、 服務和閘道文件庫：

* [物聯網 (IoT) .NET (英文)][lnk-dotnet-ref]
* [IoT 中樞 REST (英文)][lnk-rest-ref]
* [Azure IoT 裝置 SDK for C][lnk-c-ref]
* [Azure IoT 裝置 SDK for Java][lnk-java-ref]
* [Azure IoT 服務 SDK for Java][lnk-java-service-ref]
* [Azure IoT 裝置 SDK for Node.js][lnk-node-ref]
* [Azure IoT 服務 SDK for Node.js][lnk-node-service-ref]
* [Azure IoT Edge][lnk-gateway-ref]

## <a name="next-steps"></a>後續步驟

此 IoT 中樞開發人員指南中的其他參考主題包括︰

* [IoT 中樞端點][lnk-devguide-endpoints]
* [裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query]
* [配額和節流][lnk-devguide-quotas]
* [IoT 中樞的 MQTT 支援][lnk-devguide-mqtt]

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
