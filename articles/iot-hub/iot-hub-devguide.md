---
title: "Azure IoT 中樞 aaaDeveloper 指南 |Microsoft 文件"
description: "hello Azure IoT 中樞開發人員指南包含端點、 安全性、 hello 身分識別登錄、 裝置管理、 直接的方法、 裝置雙、 檔案上傳、 作業、 hello IoT 中樞的查詢語言和傳訊的討論。"
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
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a><span data-ttu-id="af929-103">Azure IoT 中樞開發人員指南</span><span class="sxs-lookup"><span data-stu-id="af929-103">Azure IoT Hub developer guide</span></span>

<span data-ttu-id="af929-104">Azure IoT 中樞是一項完全受管理的服務，有助於讓數百萬個裝置和一個解決方案後端進行可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="af929-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="af929-105">Azure IoT 中樞可提供您︰</span><span class="sxs-lookup"><span data-stu-id="af929-105">Azure IoT Hub provides you with:</span></span>

* <span data-ttu-id="af929-106">使用每一裝置的安全性認證和存取控制來保護通訊的安全。</span><span class="sxs-lookup"><span data-stu-id="af929-106">Secure communications by using per-device security credentials and access control.</span></span>
* <span data-ttu-id="af929-107">多個裝置到雲端和雲端到裝置的超大規模通訊選項。</span><span class="sxs-lookup"><span data-stu-id="af929-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span></span>
* <span data-ttu-id="af929-108">每一裝置狀態資訊和中繼資料的可查詢儲存體。</span><span class="sxs-lookup"><span data-stu-id="af929-108">Queryable storage of per-device state information and meta-data.</span></span>
* <span data-ttu-id="af929-109">簡單的裝置與裝置 hello 最受歡迎的語言與平台的程式庫的連線。</span><span class="sxs-lookup"><span data-stu-id="af929-109">Easy device connectivity with device libraries for hello most popular languages and platforms.</span></span>

<span data-ttu-id="af929-110">此 IoT 中樞開發人員指南包含下列發行項的 hello:</span><span class="sxs-lookup"><span data-stu-id="af929-110">This IoT Hub developer guide includes hello following articles:</span></span>

* <span data-ttu-id="af929-111">[裝置對雲端通訊指引][lnk-d2c-guidance]可協助您在裝置對雲端訊息、裝置對應項報告屬性和檔案上傳之間做出選擇。</span><span class="sxs-lookup"><span data-stu-id="af929-111">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span></span>
* <span data-ttu-id="af929-112">[雲端對裝置通訊指引][lnk-c2d-guidance]可協助您在直接方法、裝置對應項所需屬性和雲端對裝置訊息之間做出選擇。</span><span class="sxs-lookup"><span data-stu-id="af929-112">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span></span>
* <span data-ttu-id="af929-113">[裝置的雲端和雲端的裝置與 IoT 中樞傳訊][ devguide-messaging]描述 hello 訊息功能 （裝置到雲端和雲端到裝置） 公開 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="af929-113">[Device-to-cloud and cloud-to-device messaging with IoT Hub][devguide-messaging] describes hello messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span></span>
  * <span data-ttu-id="af929-114">[傳送裝置到雲端訊息 tooIoT 中樞][devguide-messages-d2c]。</span><span class="sxs-lookup"><span data-stu-id="af929-114">[Send device-to-cloud messages tooIoT Hub][devguide-messages-d2c].</span></span>
  * <span data-ttu-id="af929-115">[讀取 hello 內建端點的裝置到雲端訊息][devguide-builtin]。</span><span class="sxs-lookup"><span data-stu-id="af929-115">[Read device-to-cloud messages from hello built-in endpoint][devguide-builtin].</span></span>
  * <span data-ttu-id="af929-116">[使用適用於裝置對雲端訊息的自訂端點和路由規則][devguide-custom]。</span><span class="sxs-lookup"><span data-stu-id="af929-116">[Use custom endpoints and routing rules for device-to-cloud messages][devguide-custom].</span></span>
  * <span data-ttu-id="af929-117">[從 IoT 中樞傳送雲端到裝置訊息][devguide-messages-c2d]。</span><span class="sxs-lookup"><span data-stu-id="af929-117">[Send cloud-to-device messages from IoT Hub][devguide-messages-c2d].</span></span>
  * <span data-ttu-id="af929-118">[建立及讀取 IoT 中樞訊息][devguide-format]。</span><span class="sxs-lookup"><span data-stu-id="af929-118">[Create and read IoT Hub messages][devguide-format].</span></span>
* <span data-ttu-id="af929-119">[從裝置上傳檔案][devguide-upload]說明如何從裝置上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="af929-119">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span></span> <span data-ttu-id="af929-120">hello 文章也包含通知 hello 上傳程序可以傳送 hello 等主題的資訊。</span><span class="sxs-lookup"><span data-stu-id="af929-120">hello article also includes information about topics such as hello notifications hello upload process can send.</span></span>
* <span data-ttu-id="af929-121">[在 IoT 中樞管理裝置身分識別][devguide-identities]說明各 IoT 中樞的身分識別登錄所儲存的資訊，以及您可以存取和修改資訊的方式。</span><span class="sxs-lookup"><span data-stu-id="af929-121">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span></span>
* <span data-ttu-id="af929-122">[控制存取 tooIoT 中樞][ devguide-security]描述 hello 安全性模型使用 toogrant 存取 tooIoT 中樞功能的裝置和雲端元件。</span><span class="sxs-lookup"><span data-stu-id="af929-122">[Control access tooIoT Hub][devguide-security] describes hello security model used toogrant access tooIoT Hub functionality for both devices and cloud components.</span></span> <span data-ttu-id="af929-123">hello 發行項包含使用權杖和 X.509 憑證和 hello 可以授與的權限的詳細資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="af929-123">hello article includes information about using tokens and X.509 certificates, and details of hello permissions you can grant.</span></span>
* <span data-ttu-id="af929-124">[使用裝置雙 toosynchronize 狀態和設定][ devguide-device-twins]描述 hello*裝置兩個*概念和 hello 與裝置同步處理裝置，例如，它會公開的功能兩個。</span><span class="sxs-lookup"><span data-stu-id="af929-124">[Use device twins toosynchronize state and configurations][devguide-device-twins] describes hello *device twin* concept and hello functionality it exposes such as synchronizing a device with its device twin.</span></span> <span data-ttu-id="af929-125">hello 發行項包含 hello 資料儲存在裝置的兩個相關資訊。</span><span class="sxs-lookup"><span data-stu-id="af929-125">hello article includes information about hello data stored in a device twin.</span></span>
* <span data-ttu-id="af929-126">[叫用的裝置上直接方法][ devguide-directmethods]描述 hello 生命週期的直接的方法時，如何 tooinvoke 方法從後端應用程式和控制代碼 hello 裝置上的直接在裝置上的方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="af929-126">[Invoke a direct method on a device][devguide-directmethods] describes hello lifecycle of a direct method, information about how tooinvoke methods on a device from your back-end app and handle hello direct method on your device.</span></span>
* <span data-ttu-id="af929-127">[排程多個裝置上的作業][devguide-jobs]說明如何排程多個裝置上的作業。</span><span class="sxs-lookup"><span data-stu-id="af929-127">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span></span> <span data-ttu-id="af929-128">hello 文章說明如何 toosubmit 工作在執行直接的方法，更新使用裝置的兩個裝置時執行工作。</span><span class="sxs-lookup"><span data-stu-id="af929-128">hello article describes how toosubmit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span></span> <span data-ttu-id="af929-129">此外也說明如何 tooquery hello 工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="af929-129">It also describes how tooquery hello status of a job.</span></span>
* <span data-ttu-id="af929-130">[參考-選擇通訊協定][ devguide-protocol]描述 hello 通訊協定支援的裝置通訊的 IoT 中樞，並列出 hello 應開啟的連接埠。</span><span class="sxs-lookup"><span data-stu-id="af929-130">[Reference - choose a communication protocol][devguide-protocol] describes hello communication protocols that IoT Hub supports for device communication and lists hello ports that should be open.</span></span>
* <span data-ttu-id="af929-131">[參考-IoT 中樞端點][ devguide-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。</span><span class="sxs-lookup"><span data-stu-id="af929-131">[Reference - IoT Hub endpoints][devguide-endpoints] describes hello various endpoints that each IoT hub exposes for runtime and management operations.</span></span> <span data-ttu-id="af929-132">hello 本文也描述您可以建立其他端點，在您的 IoT 中樞，以及如何 toouse 欄位閘道 tooenable 裝置連線 tooyour IoT 中樞端點在非標準的案例。</span><span class="sxs-lookup"><span data-stu-id="af929-132">hello article also describes how you can create additional endpoints in your IoT hub, and how toouse a field gateway tooenable devices connectivity tooyour IoT Hub endpoints in non-standard scenarios.</span></span>
* <span data-ttu-id="af929-133">[參考-裝置雙、 作業和訊息路由的 IoT 中樞查詢語言][ devguide-query]描述該裝置雙和作業的相關的 tooretrieve 資訊從您的中樞可讓您的 IoT 中樞查詢語言。</span><span class="sxs-lookup"><span data-stu-id="af929-133">[Reference - IoT Hub query language for device twins, jobs, and message routing][devguide-query] describes that IoT Hub query language that enables you tooretrieve information from your hub about your device twins and jobs.</span></span>
* <span data-ttu-id="af929-134">[參考-配額和節流][ devguide-quotas] hello 配額 hello IoT 中心服務和節流行為，當超過配額時，您可以預期 toosee hello 設定彙總。</span><span class="sxs-lookup"><span data-stu-id="af929-134">[Reference - quotas and throttling][devguide-quotas] summarizes hello quotas set in hello IoT Hub service and hello throttling behavior you can expect toosee when you exceed a quota.</span></span>
* <span data-ttu-id="af929-135">[參考-定價][ devguide-pricing]提供不同的 Sku 和定價的 IoT 中樞與 hello 做為計量 IoT 中樞的各種不同功能的 IoT 中樞的訊息的詳細資訊的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="af929-135">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how hello various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>
* <span data-ttu-id="af929-136">[參考-裝置和服務 Sdk] [ devguide-sdks]清單 hello Azure IoT Sdk，您可以使用 toodevelop 與 IoT 中樞互動的裝置和服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="af929-136">[Reference - Device and service SDKs][devguide-sdks] lists hello Azure IoT SDKs you can use toodevelop both device and service apps that interact with your IoT hub.</span></span> <span data-ttu-id="af929-137">hello 文件包含連結 tooonline API 文件。</span><span class="sxs-lookup"><span data-stu-id="af929-137">hello article includes links tooonline API documentation.</span></span>
* <span data-ttu-id="af929-138">[參考-IoT 中樞 MQTT 支援][ devguide-mqtt]提供 IoT 中樞的 hello MQTT 通訊協定的支援方式的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="af929-138">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports hello MQTT protocol.</span></span> <span data-ttu-id="af929-139">hello 文件描述 hello hello MQTT 通訊協定內建 toohello Azure IoT Sdk 支援，並且提供直接使用 hello MQTT 通訊協定的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="af929-139">hello article describes hello support for hello MQTT protocol built-in toohello Azure IoT SDKs and provides information about using hello MQTT protocol directly.</span></span>
* <span data-ttu-id="af929-140">[詞彙][devguide-glossary]是常見 IoT 中樞相關術語的清單。</span><span class="sxs-lookup"><span data-stu-id="af929-140">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span></span>

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
