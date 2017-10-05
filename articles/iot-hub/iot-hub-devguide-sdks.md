---
title: "了解 Azure IoT SDK | Microsoft Docs"
description: "開發人員指南 - 可用來建置裝置應用程式和後端應用程式的各種 Azure IoT 裝置和服務 SDK 的相關資訊和連結。"
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
ms.openlocfilehash: bcbf4b9633f58293edb19aeb33dec6602ac4ec8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="9c88c-103">了解和使用 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="9c88c-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="9c88c-104">有三種類別的 SDK 可與 IoT 中樞搭配使用：</span><span class="sxs-lookup"><span data-stu-id="9c88c-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="9c88c-105">**裝置 SDK** 可讓您建立在 IoT 裝置上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c88c-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span></span> <span data-ttu-id="9c88c-106">這些應用程式會將遙測傳送至您的IoT 中樞，並選擇性地接收來自 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="9c88c-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="9c88c-107">**服務 SDK** 可讓您管理 IoT 中樞，並選擇性地將訊息傳送到 IoT 裝置。</span><span class="sxs-lookup"><span data-stu-id="9c88c-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span></span>

* <span data-ttu-id="9c88c-108">**Azure IoT Edge** 可讓您建置閘道，以啟用不使用其中一個支援通訊協定的裝置，或者當您需要處理邊緣上的訊息時加以建置。</span><span class="sxs-lookup"><span data-stu-id="9c88c-108">**Azure IoT Edge** enables you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span></span>

<span data-ttu-id="9c88c-109">提供 SDK 的目的是支援多種程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="9c88c-109">SDKs are provided to support multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="9c88c-110">Azure IoT 裝置 SDK</span><span class="sxs-lookup"><span data-stu-id="9c88c-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="9c88c-111">Microsoft Azure IoT 裝置 SDK 包含有助於建置裝置和應用程式的程式碼，並使裝置和應用程式連接到 Azure IoT 中心服務，且由其進行管理。</span><span class="sxs-lookup"><span data-stu-id="9c88c-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="9c88c-112">您可從 GitHub 下載下列 Azure IoT 裝置 SDK：</span><span class="sxs-lookup"><span data-stu-id="9c88c-112">The following Azure IoT device SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="9c88c-113">為了可攜性和廣泛平台相容性，以 ANSI C (C99) 撰寫之 [Azure IoT 裝置 SDK for C][lnk-c-device-sdk]。</span><span class="sxs-lookup"><span data-stu-id="9c88c-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="9c88c-114">有兩個適用於 C 的裝置用戶端程式庫，即低階 **iothub_client** 和 **serializer**。</span><span class="sxs-lookup"><span data-stu-id="9c88c-114">There are two device client libraries for C, the low-level **iothub_client** and the **serializer**.</span></span>
* <span data-ttu-id="9c88c-115">[Azure IoT 裝置 SDK for .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c88c-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="9c88c-116">[Azure IoT 裝置 SDK for Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c88c-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="9c88c-117">[Azure IoT 裝置 SDK for Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c88c-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="9c88c-118">[適用於 Python 的 Azure IoT 裝置 SDK][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c88c-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="9c88c-119">請參閱 GitHub 儲存機制中的讀我檔案，以取得使用語言和平台特定套件管理員在開發電腦上安裝二進位檔和相依項目的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9c88c-119">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="9c88c-120">作業系統平台和硬體相容性</span><span class="sxs-lookup"><span data-stu-id="9c88c-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="9c88c-121">如需 SDK 與特定硬體裝置之相容性的詳細資訊，請參閱 [Azure IoT 認證裝置目錄][lnk-certified]。</span><span class="sxs-lookup"><span data-stu-id="9c88c-121">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="9c88c-122">Azure IoT 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="9c88c-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="9c88c-123">Microsoft Azure IoT 服務 SDK 包含可協助建置應用程式的程式碼，這些應用程式可直接與「IoT 中樞」互動來管理裝置和安全性。</span><span class="sxs-lookup"><span data-stu-id="9c88c-123">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span></span>

<span data-ttu-id="9c88c-124">您可從 GitHub 下載下列 Azure IoT 服務 SDK：</span><span class="sxs-lookup"><span data-stu-id="9c88c-124">The following Azure IoT service SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="9c88c-125">[Azure IoT 服務 SDK for .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c88c-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="9c88c-126">[Azure IoT 服務 SDK for Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c88c-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="9c88c-127">[Azure IoT 服務 SDK for Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c88c-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="9c88c-128">[適用於 Python 的 Azure IoT 服務 SDK][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c88c-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="9c88c-129">[適用於 C 的 Azure IoT 服務 SDK][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="9c88c-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="9c88c-130">請參閱 GitHub 儲存機制中的讀我檔案，以取得使用語言和平台特定套件管理員在開發電腦上安裝二進位檔和相依項目的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9c88c-130">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="9c88c-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="9c88c-131">Azure IoT Edge</span></span>

<span data-ttu-id="9c88c-132">Azure IoT Edge 包含用來建立 IoT 閘道解決方案的基礎結構和模組。</span><span class="sxs-lookup"><span data-stu-id="9c88c-132">Azure IoT Edge contains the infrastructure and modules to create IoT gateway solutions.</span></span> <span data-ttu-id="9c88c-133">您可以擴充 IoT Edge 來建立適合任何端對端案例的閘道。</span><span class="sxs-lookup"><span data-stu-id="9c88c-133">You can extend IoT Edge to create gateways tailored to any end-to-end scenario.</span></span>

<span data-ttu-id="9c88c-134">您可以從 GitHub 下載 [Azure IoT Edge][lnk-iot-edge]。</span><span class="sxs-lookup"><span data-stu-id="9c88c-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="9c88c-135">線上 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="9c88c-135">Online API reference documentation</span></span>

<span data-ttu-id="9c88c-136">以下清單包含 Azure IoT 裝置、服務及閘道器程式庫的線上 API 參考文件連結：</span><span class="sxs-lookup"><span data-stu-id="9c88c-136">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="9c88c-137">[物聯網 (IoT) .NET (英文)][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="9c88c-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="9c88c-138">[IoT 中樞 REST (英文)][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="9c88c-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="9c88c-139">[Azure IoT 裝置 SDK for C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="9c88c-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="9c88c-140">[Azure IoT 裝置 SDK for Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="9c88c-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="9c88c-141">[Azure IoT 服務 SDK for Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="9c88c-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="9c88c-142">[Azure IoT 裝置 SDK for Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="9c88c-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="9c88c-143">[Azure IoT 服務 SDK for Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="9c88c-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="9c88c-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="9c88c-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c88c-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c88c-145">Next steps</span></span>

<span data-ttu-id="9c88c-146">此 IoT 中樞開發人員指南中的其他參考主題包括︰</span><span class="sxs-lookup"><span data-stu-id="9c88c-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="9c88c-147">[IoT 中樞端點][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="9c88c-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="9c88c-148">[裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="9c88c-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="9c88c-149">[配額和節流][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="9c88c-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="9c88c-150">[IoT 中樞的 MQTT 支援][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="9c88c-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
