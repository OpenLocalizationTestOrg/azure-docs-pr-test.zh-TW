---
title: "Azure IoT 中樞開發人員指南 | Microsoft Docs"
description: "Azure IoT 中樞開發人員指南中討論到端點、安全性、身分識別登錄、裝置管理、直接方法、裝置對應項、檔案上傳、作業、IoT 中心查詢語言及傳訊。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: adb9a12899e9040cd83d522c734448989636fe29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-developer-guide"></a><span data-ttu-id="c2b59-103">Azure IoT 中樞開發人員指南</span><span class="sxs-lookup"><span data-stu-id="c2b59-103">Azure IoT Hub developer guide</span></span>

<span data-ttu-id="c2b59-104">Azure IoT 中樞是一項完全受管理的服務，有助於讓數百萬個裝置和一個解決方案後端進行可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="c2b59-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="c2b59-105">Azure IoT 中樞可提供您︰</span><span class="sxs-lookup"><span data-stu-id="c2b59-105">Azure IoT Hub provides you with:</span></span>

* <span data-ttu-id="c2b59-106">使用每一裝置的安全性認證和存取控制來保護通訊的安全。</span><span class="sxs-lookup"><span data-stu-id="c2b59-106">Secure communications by using per-device security credentials and access control.</span></span>
* <span data-ttu-id="c2b59-107">多個裝置到雲端和雲端到裝置的超大規模通訊選項。</span><span class="sxs-lookup"><span data-stu-id="c2b59-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span></span>
* <span data-ttu-id="c2b59-108">每一裝置狀態資訊和中繼資料的可查詢儲存體。</span><span class="sxs-lookup"><span data-stu-id="c2b59-108">Queryable storage of per-device state information and meta-data.</span></span>
* <span data-ttu-id="c2b59-109">透過最受歡迎的語言和平台的裝置程式庫，進行簡單的裝置連線。</span><span class="sxs-lookup"><span data-stu-id="c2b59-109">Easy device connectivity with device libraries for the most popular languages and platforms.</span></span>

<span data-ttu-id="c2b59-110">此 IoT 中樞開發人員指南包含下列文章︰</span><span class="sxs-lookup"><span data-stu-id="c2b59-110">This IoT Hub developer guide includes the following articles:</span></span>

* <span data-ttu-id="c2b59-111">[裝置對雲端通訊指引][lnk-d2c-guidance]可協助您在裝置對雲端訊息、裝置對應項報告屬性和檔案上傳之間做出選擇。</span><span class="sxs-lookup"><span data-stu-id="c2b59-111">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span></span>
* <span data-ttu-id="c2b59-112">[雲端對裝置通訊指引][lnk-c2d-guidance]可協助您在直接方法、裝置對應項所需屬性和雲端對裝置訊息之間做出選擇。</span><span class="sxs-lookup"><span data-stu-id="c2b59-112">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span></span>
* <span data-ttu-id="c2b59-113">[IoT 中樞的裝置到雲端及雲端到裝置傳訊][devguide-messaging]說明 IoT 中樞所公開的傳訊功能 (裝置到雲端和雲端到裝置)。</span><span class="sxs-lookup"><span data-stu-id="c2b59-113">[Device-to-cloud and cloud-to-device messaging with IoT Hub][devguide-messaging] describes the messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span></span>
  * <span data-ttu-id="c2b59-114">[將裝置到雲端訊息傳送至 IoT 中樞][devguide-messages-d2c]。</span><span class="sxs-lookup"><span data-stu-id="c2b59-114">[Send device-to-cloud messages to IoT Hub][devguide-messages-d2c].</span></span>
  * <span data-ttu-id="c2b59-115">[從內建端點讀取裝置對雲端訊息][devguide-builtin]。</span><span class="sxs-lookup"><span data-stu-id="c2b59-115">[Read device-to-cloud messages from the built-in endpoint][devguide-builtin].</span></span>
  * <span data-ttu-id="c2b59-116">[使用適用於裝置對雲端訊息的自訂端點和路由規則][devguide-custom]。</span><span class="sxs-lookup"><span data-stu-id="c2b59-116">[Use custom endpoints and routing rules for device-to-cloud messages][devguide-custom].</span></span>
  * <span data-ttu-id="c2b59-117">[從 IoT 中樞傳送雲端到裝置訊息][devguide-messages-c2d]。</span><span class="sxs-lookup"><span data-stu-id="c2b59-117">[Send cloud-to-device messages from IoT Hub][devguide-messages-c2d].</span></span>
  * <span data-ttu-id="c2b59-118">[建立及讀取 IoT 中樞訊息][devguide-format]。</span><span class="sxs-lookup"><span data-stu-id="c2b59-118">[Create and read IoT Hub messages][devguide-format].</span></span>
* <span data-ttu-id="c2b59-119">[從裝置上傳檔案][devguide-upload]說明如何從裝置上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="c2b59-119">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span></span> <span data-ttu-id="c2b59-120">本文也包含上傳程序可傳送之通知等主題的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c2b59-120">The article also includes information about topics such as the notifications the upload process can send.</span></span>
* <span data-ttu-id="c2b59-121">[在 IoT 中樞管理裝置身分識別][devguide-identities]說明各 IoT 中樞的身分識別登錄所儲存的資訊，以及您可以存取和修改資訊的方式。</span><span class="sxs-lookup"><span data-stu-id="c2b59-121">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span></span>
* <span data-ttu-id="c2b59-122">[控制 IoT 中樞的存取權][devguide-security]說明用來將存取權授與裝置和雲端元件之 IoT 中樞功能的安全性模型。</span><span class="sxs-lookup"><span data-stu-id="c2b59-122">[Control access to IoT Hub][devguide-security] describes the security model used to grant access to IoT Hub functionality for both devices and cloud components.</span></span> <span data-ttu-id="c2b59-123">本文包含使用權杖和 X.509 憑證的相關資訊，以及您可授與之權限的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c2b59-123">The article includes information about using tokens and X.509 certificates, and details of the permissions you can grant.</span></span>
* <span data-ttu-id="c2b59-124">[使用裝置對應項同步處理狀態和組態][devguide-device-twins]說明*裝置對應項*概念和其所公開的功能，例如同步處理裝置與其裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="c2b59-124">[Use device twins to synchronize state and configurations][devguide-device-twins] describes the *device twin* concept and the functionality it exposes such as synchronizing a device with its device twin.</span></span> <span data-ttu-id="c2b59-125">本文包含裝置對應項中儲存之資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c2b59-125">The article includes information about the data stored in a device twin.</span></span>
* <span data-ttu-id="c2b59-126">[叫用裝置上的直接方法][devguide-directmethods]說明直接方法的生命週期，以及如何從後端應用程式叫用裝置上方法及處理裝置上直接方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c2b59-126">[Invoke a direct method on a device][devguide-directmethods] describes the lifecycle of a direct method, information about how to invoke methods on a device from your back-end app and handle the direct method on your device.</span></span>
* <span data-ttu-id="c2b59-127">[排程多個裝置上的作業][devguide-jobs]說明如何排程多個裝置上的作業。</span><span class="sxs-lookup"><span data-stu-id="c2b59-127">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span></span> <span data-ttu-id="c2b59-128">本文說明如何將執行工作的作業提交為執行直接方法，使用裝置對應項更新裝置。</span><span class="sxs-lookup"><span data-stu-id="c2b59-128">The article describes how to submit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span></span> <span data-ttu-id="c2b59-129">它也說明如何查詢作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="c2b59-129">It also describes how to query the status of a job.</span></span>
* <span data-ttu-id="c2b59-130">[參考 - 選擇通訊協定][devguide-protocol]說明 IoT 中樞進行裝置通訊所支援的通訊協定，並列出應開啟的連接埠。</span><span class="sxs-lookup"><span data-stu-id="c2b59-130">[Reference - choose a communication protocol][devguide-protocol] describes the communication protocols that IoT Hub supports for device communication and lists the ports that should be open.</span></span>
* <span data-ttu-id="c2b59-131">[參考 - IoT 中樞端點][devguide-endpoints]說明每個 IoT 中樞針對執行階段和管理作業所公開的各種端點。</span><span class="sxs-lookup"><span data-stu-id="c2b59-131">[Reference - IoT Hub endpoints][devguide-endpoints] describes the various endpoints that each IoT hub exposes for runtime and management operations.</span></span> <span data-ttu-id="c2b59-132">本文也說明如何在 IoT 中樞中建立額外端點，以及如何使用現場閘道器啟用裝置在非標準案例中對 IoT 中樞端點的連線能力。</span><span class="sxs-lookup"><span data-stu-id="c2b59-132">The article also describes how you can create additional endpoints in your IoT hub, and how to use a field gateway to enable devices connectivity to your IoT Hub endpoints in non-standard scenarios.</span></span>
* <span data-ttu-id="c2b59-133">[參考 - 裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][devguide-query]說明的 IoT 中樞查詢語言可讓您從中樞擷取有關裝置對應項和作業的資訊。</span><span class="sxs-lookup"><span data-stu-id="c2b59-133">[Reference - IoT Hub query language for device twins, jobs, and message routing][devguide-query] describes that IoT Hub query language that enables you to retrieve information from your hub about your device twins and jobs.</span></span>
* <span data-ttu-id="c2b59-134">[參考 - 配額和節流][devguide-quotas]摘要說明 IoT 中樞服務中設定的配額，以及超過配額時的預期節流行為。</span><span class="sxs-lookup"><span data-stu-id="c2b59-134">[Reference - quotas and throttling][devguide-quotas] summarizes the quotas set in the IoT Hub service and the throttling behavior you can expect to see when you exceed a quota.</span></span>
* <span data-ttu-id="c2b59-135">[參考 - 定價][devguide-pricing]會提供關於 IoT 中樞之不同 SKU 和定價的一般資訊，以及 IoT 中樞如何以訊息的形式來針對各種 IoT 中樞功能進行計量的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c2b59-135">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how the various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>
* <span data-ttu-id="c2b59-136">[參考 - 裝置和服務 SDK][devguide-sdks] 列出的 Azure IoT SDK 可用來開發與 IoT 中樞互動的裝置和服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2b59-136">[Reference - Device and service SDKs][devguide-sdks] lists the Azure IoT SDKs you can use to develop both device and service apps that interact with your IoT hub.</span></span> <span data-ttu-id="c2b59-137">本文包含線上 API 文件的連結。</span><span class="sxs-lookup"><span data-stu-id="c2b59-137">The article includes links to online API documentation.</span></span>
* <span data-ttu-id="c2b59-138">[參考 - IoT 中樞 MQTT 支援][devguide-mqtt]提供 IoT 中樞如何支援 MQTT 通訊協定的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c2b59-138">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports the MQTT protocol.</span></span> <span data-ttu-id="c2b59-139">本文說明 Azure IoT SDK 內建之 MQTT 通訊協定的支援，並提供直接使用 MQTT 通訊協定的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c2b59-139">The article describes the support for the MQTT protocol built-in to the Azure IoT SDKs and provides information about using the MQTT protocol directly.</span></span>
* <span data-ttu-id="c2b59-140">[詞彙][devguide-glossary]是常見 IoT 中樞相關術語的清單。</span><span class="sxs-lookup"><span data-stu-id="c2b59-140">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span></span>

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
