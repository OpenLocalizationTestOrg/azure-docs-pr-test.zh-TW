---
title: "Azure IoT 中樞做法 | Microsoft Docs"
description: "身為開發人員，如何使用各種 IoT 中樞功能？"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 786121ae249d69376b4be4c74000868cbb208989
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-iot-hub"></a><span data-ttu-id="e681f-103">如何使用 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="e681f-103">How to use Azure IoT Hub</span></span>

<span data-ttu-id="e681f-104">您有各種選項可了解如何開發 IoT 中樞服務：</span><span class="sxs-lookup"><span data-stu-id="e681f-104">You have various options to learn how to develop for the IoT Hub service:</span></span>

* <span data-ttu-id="e681f-105">閱讀詳細描述 IoT 中樞功能的概念性文章。</span><span class="sxs-lookup"><span data-stu-id="e681f-105">Read the conceptual articles that describe the features of IoT Hub in detail.</span></span>
* <span data-ttu-id="e681f-106">遵循涵蓋 IoT 中樞各種功能的其中一個教學課程。</span><span class="sxs-lookup"><span data-stu-id="e681f-106">Follow one of the tutorials that cover the various features of IoT Hub.</span></span>

## <a name="developer-guide"></a><span data-ttu-id="e681f-107">開發人員指南</span><span class="sxs-lookup"><span data-stu-id="e681f-107">Developer guide</span></span>

<span data-ttu-id="e681f-108">身為開發人員，您可以閱讀[開發人員指南][lnk-devguide]中有關 IoT 中樞的詳細概念性指導方針。</span><span class="sxs-lookup"><span data-stu-id="e681f-108">As a developer, you can read detailed conceptual guidance about IoT Hub in the [Developer Guide][lnk-devguide].</span></span> <span data-ttu-id="e681f-109">本指南包含：</span><span class="sxs-lookup"><span data-stu-id="e681f-109">This guide includes:</span></span>

* <span data-ttu-id="e681f-110">可協助您了解如何使用之所有 IoT 中樞功能的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="e681f-110">Detailed descriptions of all IoT Hub features that help you to learn how to use them.</span></span>
* <span data-ttu-id="e681f-111">有多個選項可用時如何選擇的指南。</span><span class="sxs-lookup"><span data-stu-id="e681f-111">Guidance on how to choose when multiple options are available.</span></span>

## <a name="tutorials"></a><span data-ttu-id="e681f-112">教學課程</span><span class="sxs-lookup"><span data-stu-id="e681f-112">Tutorials</span></span>

<span data-ttu-id="e681f-113">如果您想要透過實際操作練習來了解特定的 IoT 中樞功能，有數個教學課程可供選擇。</span><span class="sxs-lookup"><span data-stu-id="e681f-113">If you prefer to learn about specific IoT Hub features by working through hands-on exercises, there are several tutorials to choose from.</span></span> <span data-ttu-id="e681f-114">其中許多教學課程都是以多種程式設計語言提供。</span><span class="sxs-lookup"><span data-stu-id="e681f-114">Many of these tutorials are available in multiple programming languages.</span></span> <span data-ttu-id="e681f-115">這些教學課程包括︰</span><span class="sxs-lookup"><span data-stu-id="e681f-115">These tutorials include:</span></span>

- <span data-ttu-id="e681f-116">[使用路由處理 Azure IoT 中樞的裝置到雲端訊息][lnk-routes-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="e681f-116">[Process IoT Hub device-to-cloud messages using routes][lnk-routes-tutorial].</span></span> <span data-ttu-id="e681f-117">本教學課程說明如何使用 IoT 中樞路由規則，以簡單的設定方式來分派裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="e681f-117">This tutorial shows you how to use IoT Hub routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>

- <span data-ttu-id="e681f-118">[使用 IoT 中樞傳送雲端到裝置訊息][lnk-c2d-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="e681f-118">[Send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial].</span></span> <span data-ttu-id="e681f-119">本教學課程說明如何透過 IoT 中樞傳送雲端到裝置訊息，以及在裝置上接收雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="e681f-119">This tutorial shows you how to send cloud-to-device messages through IoT Hub and receive cloud-to-device messages on a device.</span></span>

- <span data-ttu-id="e681f-120">[使用 IoT 中樞從裝置將檔案上傳至雲端][lnk-upload-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="e681f-120">[Upload files from devices to the cloud with IoT Hub][lnk-upload-tutorial].</span></span> <span data-ttu-id="e681f-121">本教學課程說明如何使用 IoT 中樞的檔案上傳功能。</span><span class="sxs-lookup"><span data-stu-id="e681f-121">This tutorial shows you how to use the file upload capabilities of IoT Hub.</span></span>

- <span data-ttu-id="e681f-122">[開始使用裝置對應項][lnk-twin-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="e681f-122">[Get started with device twins][lnk-twin-tutorial].</span></span> <span data-ttu-id="e681f-123">本教學課程簡介裝置對應項、報告屬性、所需屬性和標記。</span><span class="sxs-lookup"><span data-stu-id="e681f-123">This tutorial introduces you to device twins, reported properties, desired properties, and tags.</span></span> <span data-ttu-id="e681f-124">您可使用裝置對應項來同步處理值與裝置。</span><span class="sxs-lookup"><span data-stu-id="e681f-124">You use device twins to synchronize values with your devices.</span></span>

- <span data-ttu-id="e681f-125">[使用直接方法][lnk-methods-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="e681f-125">[Use direct methods][lnk-methods-tutorial].</span></span> <span data-ttu-id="e681f-126">本教學課程說明如何使用直接方法。</span><span class="sxs-lookup"><span data-stu-id="e681f-126">This tutorial shows you how to use direct methods.</span></span> <span data-ttu-id="e681f-127">您可在模擬裝置中新增直接方法的處理常式，並從 IoT 中樞叫用直接方法。</span><span class="sxs-lookup"><span data-stu-id="e681f-127">You add a handler for a direct method in your simulated device and invoke the direct method from IoT Hub.</span></span>

- <span data-ttu-id="e681f-128">[開始使用裝置管理][lnk-dm-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="e681f-128">[Get started with device management][lnk-dm-tutorial].</span></span> <span data-ttu-id="e681f-129">本教學課程說明如何使用主要裝置管理功能，例如裝置對應項和直接方法。</span><span class="sxs-lookup"><span data-stu-id="e681f-129">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="e681f-130">您可以使用這些功能從遠端重新啟動您的模擬裝置。</span><span class="sxs-lookup"><span data-stu-id="e681f-130">You use these features to remotely reboot your simulated device.</span></span>

- <span data-ttu-id="e681f-131">[使用所需屬性來設定裝置][lnk-properties-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="e681f-131">[Use desired properties to configure devices][lnk-properties-tutorial].</span></span> <span data-ttu-id="e681f-132">本教學課程說明如何使用裝置對應項的所需屬性以及報告屬性，從遠端設定您的裝置。</span><span class="sxs-lookup"><span data-stu-id="e681f-132">This tutorial shows you how to use the device twin's desired and reported properties, to remotely configure your device.</span></span>

- <span data-ttu-id="e681f-133">[使用裝置作業來起始裝置韌體更新][lnk-jobs-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="e681f-133">[Use device jobs to initiate a device firmware update][lnk-jobs-tutorial].</span></span> <span data-ttu-id="e681f-134">本教學課程說明如何使用主要裝置管理功能，例如裝置對應項和直接方法。</span><span class="sxs-lookup"><span data-stu-id="e681f-134">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="e681f-135">了解如何使用這些功能以從遠端更新裝置的韌體。</span><span class="sxs-lookup"><span data-stu-id="e681f-135">You learn how to use these features to remotely update your device's firmware.</span></span>

- <span data-ttu-id="e681f-136">[排程及廣播作業][lnk-schedule-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="e681f-136">[Schedule and broadcast jobs][lnk-schedule-tutorial].</span></span> <span data-ttu-id="e681f-137">本教學課程說明如何使用所需屬性和直接方法，在排定的時間與多個裝置互動。</span><span class="sxs-lookup"><span data-stu-id="e681f-137">This tutorial shows you how to use desired properties and direct methods to interact with multiple devices at a scheduled time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e681f-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e681f-138">Next steps</span></span>

<span data-ttu-id="e681f-139">若要深入了解 IoT 中樞服務，請參閱[開發人員指南][lnk-devguide]。</span><span class="sxs-lookup"><span data-stu-id="e681f-139">To learn more about the IoT Hub service, see the [Developer Guide][lnk-devguide].</span></span>

[lnk-devguide]: ./iot-hub-devguide.md
[lnk-routes-tutorial]: ./iot-hub-csharp-csharp-process-d2c.md
[lnk-c2d-tutorial]: ./iot-hub-csharp-csharp-c2d.md
[lnk-upload-tutorial]: ./iot-hub-csharp-csharp-file-upload.md
[lnk-twin-tutorial]: ./iot-hub-node-node-twin-getstarted.md
[lnk-methods-tutorial]: ./iot-hub-node-node-direct-methods.md
[lnk-dm-tutorial]: ./iot-hub-node-node-device-management-get-started.md
[lnk-properties-tutorial]: ./iot-hub-node-node-twin-how-to-configure.md
[lnk-jobs-tutorial]: ./iot-hub-node-node-firmware-update.md
[lnk-schedule-tutorial]: ./iot-hub-node-node-schedule-jobs.md