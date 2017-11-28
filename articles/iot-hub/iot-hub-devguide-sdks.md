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
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="d648c-103">了解和使用 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="d648c-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="d648c-104">有三種類別的 SDK 可與 IoT 中樞搭配使用：</span><span class="sxs-lookup"><span data-stu-id="d648c-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="d648c-105">**裝置 Sdk** toobuild IoT 裝置執行的應用程式可讓您。</span><span class="sxs-lookup"><span data-stu-id="d648c-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="d648c-106">這些應用程式傳送遙測 tooyour IoT 中樞，並選擇性地從 IoT 中心接收訊息。</span><span class="sxs-lookup"><span data-stu-id="d648c-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="d648c-107">**服務 Sdk**啟用您 toomanage IoT 中樞，並選擇性地將訊息傳送 tooyour IoT 裝置。</span><span class="sxs-lookup"><span data-stu-id="d648c-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="d648c-108">**Azure IoT 邊緣**可讓您不使用其中一個支援的 hello 通訊協定，或當您需要在 hello 邊緣 tooprocess 訊息 toobuild 閘道 tooenable 裝置。</span><span class="sxs-lookup"><span data-stu-id="d648c-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="d648c-109">Sdk 會提供 toosupport 多種程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="d648c-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="d648c-110">Azure IoT 裝置 SDK</span><span class="sxs-lookup"><span data-stu-id="d648c-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="d648c-111">hello Microsoft Azure IoT 裝置 Sdk 包含可協助建立裝置的程式碼，而且連接 tooand 的應用程式由 Azure IoT 中樞 services 管理。</span><span class="sxs-lookup"><span data-stu-id="d648c-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="d648c-112">hello 下列 Azure IoT 裝置 Sdk 會使用從 GitHub toodownload:</span><span class="sxs-lookup"><span data-stu-id="d648c-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="d648c-113">為了可攜性和廣泛平台相容性，以 ANSI C (C99) 撰寫之 [Azure IoT 裝置 SDK for C][lnk-c-device-sdk]。</span><span class="sxs-lookup"><span data-stu-id="d648c-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="d648c-114">有兩個裝置用戶端程式庫，c，hello 低階**iothub_client**和 hello**序列化程式**。</span><span class="sxs-lookup"><span data-stu-id="d648c-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="d648c-115">[Azure IoT 裝置 SDK for .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="d648c-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="d648c-116">[Azure IoT 裝置 SDK for Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="d648c-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="d648c-117">[Azure IoT 裝置 SDK for Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="d648c-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="d648c-118">[適用於 Python 的 Azure IoT 裝置 SDK][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="d648c-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="d648c-119">請參閱 hello 讀我檔案 hello GitHub 儲存機制中的開發電腦上使用語言與平台專屬封裝管理員 tooinstall 二進位檔和相依性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d648c-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="d648c-120">作業系統平台和硬體相容性</span><span class="sxs-lookup"><span data-stu-id="d648c-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="d648c-121">如需特定硬體裝置與 SDK 相容性的詳細資訊，請參閱 hello [IoT 裝置類別目錄的 Azure 認證][lnk-certified]。</span><span class="sxs-lookup"><span data-stu-id="d648c-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="d648c-122">Azure IoT 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="d648c-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="d648c-123">hello Azure IoT 服務 Sdk 包含建置直接互動 IoT 中樞 toomanage 裝置和安全性的應用程式的程式碼 toofacilitate。</span><span class="sxs-lookup"><span data-stu-id="d648c-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="d648c-124">hello 下列 Azure IoT 服務 Sdk 是可從 GitHub toodownload:</span><span class="sxs-lookup"><span data-stu-id="d648c-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="d648c-125">[Azure IoT 服務 SDK for .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d648c-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="d648c-126">[Azure IoT 服務 SDK for Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d648c-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="d648c-127">[Azure IoT 服務 SDK for Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d648c-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="d648c-128">[適用於 Python 的 Azure IoT 服務 SDK][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d648c-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="d648c-129">[適用於 C 的 Azure IoT 服務 SDK][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="d648c-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="d648c-130">請參閱 hello 讀我檔案 hello GitHub 儲存機制中的開發電腦上使用語言與平台專屬封裝管理員 tooinstall 二進位檔和相依性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d648c-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="d648c-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="d648c-131">Azure IoT Edge</span></span>

<span data-ttu-id="d648c-132">Azure IoT 邊緣包含 hello 基礎結構和模組 toocreate IoT 閘道的解決方案。</span><span class="sxs-lookup"><span data-stu-id="d648c-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="d648c-133">您可以擴充 IoT 邊緣 toocreate 閘道量身訂做的 tooany 端對端案例。</span><span class="sxs-lookup"><span data-stu-id="d648c-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="d648c-134">您可以從 GitHub 下載 [Azure IoT Edge][lnk-iot-edge]。</span><span class="sxs-lookup"><span data-stu-id="d648c-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="d648c-135">線上 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="d648c-135">Online API reference documentation</span></span>

<span data-ttu-id="d648c-136">hello 下列清單包含連結 tooonline API 參考文件的 Azure IoT 裝置、 服務和閘道文件庫：</span><span class="sxs-lookup"><span data-stu-id="d648c-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="d648c-137">[物聯網 (IoT) .NET (英文)][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="d648c-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="d648c-138">[IoT 中樞 REST (英文)][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="d648c-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="d648c-139">[Azure IoT 裝置 SDK for C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="d648c-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="d648c-140">[Azure IoT 裝置 SDK for Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="d648c-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="d648c-141">[Azure IoT 服務 SDK for Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="d648c-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="d648c-142">[Azure IoT 裝置 SDK for Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="d648c-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="d648c-143">[Azure IoT 服務 SDK for Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="d648c-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="d648c-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="d648c-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="d648c-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d648c-145">Next steps</span></span>

<span data-ttu-id="d648c-146">此 IoT 中樞開發人員指南中的其他參考主題包括︰</span><span class="sxs-lookup"><span data-stu-id="d648c-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="d648c-147">[IoT 中樞端點][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="d648c-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="d648c-148">[裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="d648c-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="d648c-149">[配額和節流][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="d648c-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="d648c-150">[IoT 中樞的 MQTT 支援][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="d648c-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
