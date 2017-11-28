---
title: "透過 Azure IoT 中樞進行裝置管理 | Microsoft Docs"
description: "Azure IoT 中樞的裝置管理概觀︰企業裝置生命週期及裝置管理模式，例如重新啟動、恢復出廠預設值、韌體更新、設定、裝置對應項、查詢、作業。"
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 6d667d42bfef2ec61b055009210d5621f51c17df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a><span data-ttu-id="d5731-103">IoT 中樞的裝置管理概觀</span><span class="sxs-lookup"><span data-stu-id="d5731-103">Overview of device management with IoT Hub</span></span>
## <a name="introduction"></a><span data-ttu-id="d5731-104">簡介</span><span class="sxs-lookup"><span data-stu-id="d5731-104">Introduction</span></span>
<span data-ttu-id="d5731-105">Azure IoT 中樞提供的功能和擴充性模型，可讓裝置與後端開發人員建置穩健的裝置管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="d5731-105">Azure IoT Hub provides the features and an extensibility model that enable device and back-end developers to build robust device management solutions.</span></span> <span data-ttu-id="d5731-106">裝置包羅萬象，從受限的感應器和單一用途的微控制器，到可路由傳送裝置群組通訊的強大閘道都是其中一份子。</span><span class="sxs-lookup"><span data-stu-id="d5731-106">Devices range from constrained sensors and single purpose microcontrollers, to powerful gateways that route communications for groups of devices.</span></span>  <span data-ttu-id="d5731-107">此外，各產業 IoT 操作員的使用案例和需求大不相同。</span><span class="sxs-lookup"><span data-stu-id="d5731-107">In addition, the use cases and requirements for IoT operators vary significantly across industries.</span></span>  <span data-ttu-id="d5731-108">儘管有此差異，IoT 中樞的裝置管理會提供一些功能、模式和程式碼程式庫，來滿足各種裝置和使用者的需求。</span><span class="sxs-lookup"><span data-stu-id="d5731-108">Despite this variation, device management with IoT Hub provides the capabilities, patterns, and code libraries to cater to a diverse set of devices and end users.</span></span>

<span data-ttu-id="d5731-109">建立成功企業 IoT 解決方案的關鍵在於，針對操作員該如何持續管理其裝置集合提供策略。</span><span class="sxs-lookup"><span data-stu-id="d5731-109">A crucial part of creating a successful enterprise IoT solution is to provide a strategy for how operators handle the ongoing management of their collection of devices.</span></span> <span data-ttu-id="d5731-110">IoT 操作員需要簡單可靠的工具和應用程式，讓他們能夠專注於作業中更為重要的層面上。</span><span class="sxs-lookup"><span data-stu-id="d5731-110">IoT operators require simple and reliable tools and applications that enable them to focus on the more strategic aspects of their jobs.</span></span> <span data-ttu-id="d5731-111">本文提供：</span><span class="sxs-lookup"><span data-stu-id="d5731-111">This article provides:</span></span>

* <span data-ttu-id="d5731-112">Azure IoT 中樞裝置管理方法的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="d5731-112">A brief overview of Azure IoT Hub approach to device management.</span></span>
* <span data-ttu-id="d5731-113">常見裝置管理原則的說明。</span><span class="sxs-lookup"><span data-stu-id="d5731-113">A description of common device management principles.</span></span>
* <span data-ttu-id="d5731-114">裝置生命週期的說明。</span><span class="sxs-lookup"><span data-stu-id="d5731-114">A description of the device lifecycle.</span></span>
* <span data-ttu-id="d5731-115">常見裝置管理模式的概觀。</span><span class="sxs-lookup"><span data-stu-id="d5731-115">An overview of common device management patterns.</span></span>

## <a name="device-management-principles"></a><span data-ttu-id="d5731-116">裝置管理原則</span><span class="sxs-lookup"><span data-stu-id="d5731-116">Device management principles</span></span>
<span data-ttu-id="d5731-117">IoT 本身伴隨著一組獨特的管理挑戰，因此每個企業級解決方案都必須符合下列原則︰</span><span class="sxs-lookup"><span data-stu-id="d5731-117">IoT brings with it a unique set of device management challenges and every enterprise-class solution must address the following principles:</span></span>

![裝置管理原則圖形][img-dm_principles]

* <span data-ttu-id="d5731-119">**規模和自動化**：IoT 解決方案需要簡單的工具，以便能夠自動執行例行工作，並且只需要少數作業人員就可以管理數百萬個裝置。</span><span class="sxs-lookup"><span data-stu-id="d5731-119">**Scale and automation**: IoT solutions require simple tools that can automate routine tasks and enable a relatively small operations staff to manage millions of devices.</span></span> <span data-ttu-id="d5731-120">每一天，操作員無不期望能夠從遠端大量處理裝置作業，並且只在發生需要他們直接關注的問題時才接獲通知。</span><span class="sxs-lookup"><span data-stu-id="d5731-120">Day-to-day, operators expect to handle device operations remotely, in bulk, and to only be alerted when issues arise that require their direct attention.</span></span>
* <span data-ttu-id="d5731-121">**開放性和相容性**：裝置生態系統富含多樣性。</span><span class="sxs-lookup"><span data-stu-id="d5731-121">**Openness and compatibility**: The device ecosystem is extraordinarily diverse.</span></span> <span data-ttu-id="d5731-122">管理工具必須經過量身打造，才能配合數量眾多的裝置類別、平台和通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d5731-122">Management tools must be tailored to accommodate a multitude of device classes, platforms, and protocols.</span></span> <span data-ttu-id="d5731-123">操作員必須能夠支援許多類型的裝置，不論是最受限的內嵌單一處理晶片，乃至功能完整而強大的電腦。</span><span class="sxs-lookup"><span data-stu-id="d5731-123">Operators must be able to support many types of devices, from the most constrained embedded single-process chips, to powerful and fully functional computers.</span></span>
* <span data-ttu-id="d5731-124">**內容感知**：IoT 環境是動態且不斷變化的，</span><span class="sxs-lookup"><span data-stu-id="d5731-124">**Context awareness**: IoT environments are dynamic and ever-changing.</span></span> <span data-ttu-id="d5731-125">因此服務可靠性非常重要。</span><span class="sxs-lookup"><span data-stu-id="d5731-125">Service reliability is paramount.</span></span> <span data-ttu-id="d5731-126">裝置管理作業必須考量下列因素，以確保維護停機時間不會影響重要的商業運作或造成危險情況︰</span><span class="sxs-lookup"><span data-stu-id="d5731-126">Device management operations must take into account the following factors to ensure that maintenance downtime doesn't affect critical business operations or create dangerous conditions:</span></span>
    * <span data-ttu-id="d5731-127">SLA 維護期間</span><span class="sxs-lookup"><span data-stu-id="d5731-127">SLA maintenance windows</span></span>
    * <span data-ttu-id="d5731-128">網路和電源狀態</span><span class="sxs-lookup"><span data-stu-id="d5731-128">Network and power states</span></span>
    * <span data-ttu-id="d5731-129">使用中狀況</span><span class="sxs-lookup"><span data-stu-id="d5731-129">In-use conditions</span></span>
    * <span data-ttu-id="d5731-130">裝置地理位置</span><span class="sxs-lookup"><span data-stu-id="d5731-130">Device geolocation</span></span>
* <span data-ttu-id="d5731-131">**服務眾多角色**︰是否能夠支援 IoT 作業角色的獨特工作流程和處理程序非常重要。</span><span class="sxs-lookup"><span data-stu-id="d5731-131">**Service many roles**: Support for the unique workflows and processes of IoT operations roles is crucial.</span></span> <span data-ttu-id="d5731-132">操作人員必須和諧地配合內部 IT 部門指定的限制。</span><span class="sxs-lookup"><span data-stu-id="d5731-132">The operations staff must work harmoniously with the given constraints of internal IT departments.</span></span>  <span data-ttu-id="d5731-133">他們也必須找出向主管和其他商務管理角色呈現即時裝置作業資訊的永續方式。</span><span class="sxs-lookup"><span data-stu-id="d5731-133">They must also find sustainable ways to surface realtime device operations information to supervisors and other business managerial roles.</span></span>

## <a name="device-lifecycle"></a><span data-ttu-id="d5731-134">裝置的生命週期</span><span class="sxs-lookup"><span data-stu-id="d5731-134">Device lifecycle</span></span>
<span data-ttu-id="d5731-135">有一組通用於所有企業 IoT 專案的一般裝置管理階段。</span><span class="sxs-lookup"><span data-stu-id="d5731-135">There is a set of general device management stages that are common to all enterprise IoT projects.</span></span> <span data-ttu-id="d5731-136">在 Azure IoT 中，裝置生命週期內有五個階段︰</span><span class="sxs-lookup"><span data-stu-id="d5731-136">In Azure IoT, there are five stages within the device lifecycle:</span></span>

![Azure IoT 裝置生命週期的五個階段︰計劃、佈建、設定、監視、淘汰][img-device_lifecycle]

<span data-ttu-id="d5731-138">在上述每個階段內，應滿足數個裝置操作員需求才能提供完整的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="d5731-138">Within each of these five stages, there are several device operator requirements that should be fulfilled to provide a complete solution:</span></span>

* <span data-ttu-id="d5731-139">**計劃**︰讓操作員得以建立裝置中繼資料配置，以便他們可以輕鬆且精確地查詢和鎖定要進行大量管理作業的裝置群組。</span><span class="sxs-lookup"><span data-stu-id="d5731-139">**Plan**: Enable operators to create a device metadata scheme that enables them to easily and accurately query for, and target a group of devices for bulk management operations.</span></span> <span data-ttu-id="d5731-140">您可以使用裝置對應項，以標記和屬性的形式來儲存此裝置中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d5731-140">You can use the device twin to store this device metadata in the form of tags and properties.</span></span>
  
    <span data-ttu-id="d5731-141">*進階閱讀*：[開始使用裝置對應項][lnk-twins-getstarted]、[了解裝置對應項][lnk-twins-devguide]、[如何使用裝置對應項屬性][lnk-twin-properties]。</span><span class="sxs-lookup"><span data-stu-id="d5731-141">*Further reading*: [Get started with device twins][lnk-twins-getstarted], [Understand device twins][lnk-twins-devguide], [How to use device twin properties][lnk-twin-properties].</span></span>
* <span data-ttu-id="d5731-142">**佈建**︰安全地向 IoT 中樞佈建新裝置，並且讓操作員能夠立即探索裝置功能。</span><span class="sxs-lookup"><span data-stu-id="d5731-142">**Provision**: Securely provision new devices to IoT Hub and enable operators to immediately discover device capabilities.</span></span>  <span data-ttu-id="d5731-143">使用 IoT 中樞身分識別登錄來建立富有彈性的裝置身分識別與認證，並利用作業 (Job) 大量執行此作業 (Operation)。</span><span class="sxs-lookup"><span data-stu-id="d5731-143">Use the IoT Hub identity registry to create flexible device identities and credentials, and perform this operation in bulk by using a job.</span></span> <span data-ttu-id="d5731-144">建置一些裝置，經由裝置對應項中的裝置屬性來報告其功能和狀況。</span><span class="sxs-lookup"><span data-stu-id="d5731-144">Build devices to report their capabilities and conditions through device properties in the device twin.</span></span>
  
    <span data-ttu-id="d5731-145">*進階閱讀*：[管理裝置身分識別][lnk-identity-registry]、[大量管理裝置身分識別][lnk-bulk-identity]、[如何使用裝置對應項屬性][lnk-twin-properties]。</span><span class="sxs-lookup"><span data-stu-id="d5731-145">*Further reading*: [Manage device identities][lnk-identity-registry], [Bulk management of device identities][lnk-bulk-identity], [How to use device twin properties][lnk-twin-properties].</span></span>
* <span data-ttu-id="d5731-146">**設定**︰協助裝置進行大量組態變更和韌體更新，同時維持健康狀態與安全性。</span><span class="sxs-lookup"><span data-stu-id="d5731-146">**Configure**: Facilitate bulk configuration changes and firmware updates to devices while maintaining both health and security.</span></span> <span data-ttu-id="d5731-147">使用所需的屬性或透過直接方法和廣播作業，大量執行這些裝置管理作業。</span><span class="sxs-lookup"><span data-stu-id="d5731-147">Perform these device management operations in bulk by using desired properties or with direct methods and broadcast jobs.</span></span>
  
    <span data-ttu-id="d5731-148">*進階閱讀*：[使用直接方法][lnk-c2d-methods]、[在裝置上叫用直接方法][lnk-methods-devguide]、[如何使用裝置對應項屬性][lnk-twin-properties]、[排程及廣播工作][lnk-jobs]、[在多個裝置上排程工作][lnk-jobs-devguide]。</span><span class="sxs-lookup"><span data-stu-id="d5731-148">*Further reading*:  [Use direct methods][lnk-c2d-methods], [Invoke a direct method on a device][lnk-methods-devguide], [How to use device twin properties][lnk-twin-properties], [Schedule and broadcast jobs][lnk-jobs], [Schedule jobs on multiple devices][lnk-jobs-devguide].</span></span>
* <span data-ttu-id="d5731-149">**監視**︰監視整體裝置集合健康狀態、進行中作業的狀態，以及就可能需要關注的問題對操作員發出警示。</span><span class="sxs-lookup"><span data-stu-id="d5731-149">**Monitor**: Monitor overall device collection health, the status of ongoing operations, and alert operators to issues that might require their attention.</span></span>  <span data-ttu-id="d5731-150">套用裝置對應項，可讓裝置報告更新作業的即時作業狀況和狀態。</span><span class="sxs-lookup"><span data-stu-id="d5731-150">Apply the device twin to allow devices to report realtime operating conditions and status of update operations.</span></span> <span data-ttu-id="d5731-151">建置強大的儀表板報告，以使用裝置對應項查詢來呈現最即時的問題。</span><span class="sxs-lookup"><span data-stu-id="d5731-151">Build powerful dashboard reports that surface the most immediate issues by using device twin queries.</span></span>
  
    <span data-ttu-id="d5731-152">*進階閱讀*：[如何使用裝置對應項屬性][lnk-twin-properties]、[裝置對應項、作業與訊息路由的 IoT 中樞查詢語言][lnk-query-language]。</span><span class="sxs-lookup"><span data-stu-id="d5731-152">*Further reading*: [How to use device twin properties][lnk-twin-properties], [IoT Hub query language for device twins, jobs, and message routing][lnk-query-language].</span></span>
* <span data-ttu-id="d5731-153">**淘汰**︰在故障、升級循環或服務存留期結束後，更換裝置或予以解除委任。</span><span class="sxs-lookup"><span data-stu-id="d5731-153">**Retire**:  Replace or decommission devices after a failure, upgrade cycle, or at the end of the service lifetime.</span></span>  <span data-ttu-id="d5731-154">如果實體裝置正被取代，則使用裝置對應項來維護裝置資訊，若正在淘汰中則加以封存。</span><span class="sxs-lookup"><span data-stu-id="d5731-154">Use the device twin to maintain device info if the physical device is being replaced, or archived if being retired.</span></span> <span data-ttu-id="d5731-155">使用 IoT 中樞身分識別登錄，安全地撤銷裝置身分識別與認證。</span><span class="sxs-lookup"><span data-stu-id="d5731-155">Use the IoT Hub identity registry for securely revoking device identities and credentials.</span></span>
  
    <span data-ttu-id="d5731-156">*進階閱讀*：[如何使用裝置對應項屬性][lnk-twin-properties]、[管理裝置身分識別][lnk-identity-registry]。</span><span class="sxs-lookup"><span data-stu-id="d5731-156">*Further reading*: [How to use device twin properties][lnk-twin-properties], [Manage device identities][lnk-identity-registry].</span></span>

## <a name="device-management-patterns"></a><span data-ttu-id="d5731-157">裝置管理模式</span><span class="sxs-lookup"><span data-stu-id="d5731-157">Device management patterns</span></span>
<span data-ttu-id="d5731-158">IoT 中樞可實現下列這套裝置管理模式。</span><span class="sxs-lookup"><span data-stu-id="d5731-158">IoT Hub enables the following set of device management patterns.</span></span>  <span data-ttu-id="d5731-159">[裝置管理教學課程][lnk-get-started]更詳細地說明如何擴充這些模式來符合確切的案例，以及如何根據這些核心範本來設計新模式。</span><span class="sxs-lookup"><span data-stu-id="d5731-159">The [device management tutorials][lnk-get-started] show you in more detail how to extend these patterns to fit your exact scenario and how to design new patterns based on these core templates.</span></span>

* <span data-ttu-id="d5731-160">**重新啟動** - 後端應用程式會透過直接方法讓裝置知道已起始重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d5731-160">**Reboot** - The back-end app informs the device through a direct method that it has initiated a reboot.</span></span>  <span data-ttu-id="d5731-161">裝置會使用報告的屬性來更新裝置的重新開機狀態。</span><span class="sxs-lookup"><span data-stu-id="d5731-161">The device uses the reported properties to update the reboot status of the device.</span></span>
  
    ![裝置管理重新啟動模式圖形][img-reboot_pattern]
* <span data-ttu-id="d5731-163">**恢復出廠預設值** - 後端應用程式會透過直接方法讓裝置知道已起始恢復出廠預設值。</span><span class="sxs-lookup"><span data-stu-id="d5731-163">**Factory Reset** - The back-end app informs the device through a direct method that it has initiated a factory reset.</span></span>  <span data-ttu-id="d5731-164">裝置會使用報告的屬性來更新裝置的恢復出廠預設值狀態。</span><span class="sxs-lookup"><span data-stu-id="d5731-164">The device uses the reported properties to update the factory reset status of the device.</span></span>
  
    ![裝置管理恢復出廠預設值模式圖形][img-facreset_pattern]
* <span data-ttu-id="d5731-166">**設定** - 後端應用程式使用所需的屬性來設定裝置上執行的軟體。</span><span class="sxs-lookup"><span data-stu-id="d5731-166">**Configuration** - The back-end app uses the desired properties to configure software running on the device.</span></span>  <span data-ttu-id="d5731-167">裝置會使用報告的屬性來更新裝置的組態狀態。</span><span class="sxs-lookup"><span data-stu-id="d5731-167">The device uses the reported properties to update configuration status of the device.</span></span>
  
    ![裝置管理設定模式圖形][img-config_pattern]
* <span data-ttu-id="d5731-169">**韌體更新** - 後端應用程式會透過直接方法讓裝置知道已起始韌體更新。</span><span class="sxs-lookup"><span data-stu-id="d5731-169">**Firmware Update** - The back-end app informs the device through a direct method that it has initiated a firmware update.</span></span>  <span data-ttu-id="d5731-170">裝置會起始多步驟程序，以下載韌體映像、套用韌體映像，並於最後重新連線到 IoT 中樞服務。</span><span class="sxs-lookup"><span data-stu-id="d5731-170">The device initiates a multistep process to download the firmware image, apply the firmware image, and finally reconnect to the IoT Hub service.</span></span>  <span data-ttu-id="d5731-171">透過多步驟程序，裝置會使用報告的屬性來更新裝置的進度與狀態。</span><span class="sxs-lookup"><span data-stu-id="d5731-171">Throughout the multistep process, the device uses the reported properties to update the progress and status of the device.</span></span>
  
    ![裝置管理韌體更新模式圖形][img-fwupdate_pattern]
* <span data-ttu-id="d5731-173">**報告進度和狀態** - 解決方案後端會橫跨一組裝置來執行裝置對應項查詢，以報告裝置上所執行動作的狀態和進度。</span><span class="sxs-lookup"><span data-stu-id="d5731-173">**Reporting progress and status** - The solution back end runs device twin queries, across a set of devices, to report on the status and progress of actions running on the devices.</span></span>
  
    ![裝置管理報告進度和狀態模式圖形][img-report_progress_pattern]

## <a name="next-steps"></a><span data-ttu-id="d5731-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5731-175">Next Steps</span></span>
<span data-ttu-id="d5731-176">IoT 中樞針對裝置管理所提供的功能、模式和程式碼程式庫，可讓您建立 IoT 應用程式，以滿足企業 IoT 操作員在裝置生命週期內各階段的需求。</span><span class="sxs-lookup"><span data-stu-id="d5731-176">The capabilities, patterns, and code libraries that IoT Hub provides for device management, enable you to create IoT applications that fulfill enterprise IoT operator requirements within each device lifecycle stage.</span></span>

<span data-ttu-id="d5731-177">若要繼續了解 IoT 中樞內的裝置管理功能，請參閱[開始使用裝置管理][lnk-get-started]教學課程。</span><span class="sxs-lookup"><span data-stu-id="d5731-177">To continue learning about the device management features in IoT Hub, see the [Get started with device management][lnk-get-started] tutorial.</span></span>

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md
