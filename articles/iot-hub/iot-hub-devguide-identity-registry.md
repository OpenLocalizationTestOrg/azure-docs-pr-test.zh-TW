---
title: "了解 Azure IoT 中樞身分識別登錄 | Microsoft Docs"
description: "開發人員指南 - 說明 IoT 中樞身分識別登錄和如何用來管理裝置。 包含大量匯入和匯出裝置識別身分的相關資訊。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6e9c7b71fa6fc78f97c0144c735fc44778181d8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="understand-the-identity-registry-in-your-iot-hub"></a><span data-ttu-id="f4464-104">了解 IoT 中樞的身分識別登錄</span><span class="sxs-lookup"><span data-stu-id="f4464-104">Understand the identity registry in your IoT hub</span></span>

<span data-ttu-id="f4464-105">每個 IoT 中樞都有身分識別登錄，可儲存允許連線至 IoT 中樞之裝置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f4464-105">Every IoT hub has an identity registry that stores information about the devices permitted to connect to the IoT hub.</span></span> <span data-ttu-id="f4464-106">若要讓裝置可以連線到 IoT 中樞，IoT 中樞的身分識別登錄中必須先有該裝置的項目。</span><span class="sxs-lookup"><span data-stu-id="f4464-106">Before a device can connect to an IoT hub, there must be an entry for that device in the IoT hub's identity registry.</span></span> <span data-ttu-id="f4464-107">裝置也必須根據身分識別登錄中儲存的認證，向 IoT 中樞進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f4464-107">A device must also authenticate with the IoT hub based on credentials stored in the identity registry.</span></span>

<span data-ttu-id="f4464-108">儲存在身分識別登錄的裝置識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="f4464-108">The device ID stored in the identity registry is case-sensitive.</span></span>

<span data-ttu-id="f4464-109">總括來說，身分識別登錄是支援 REST 的裝置身分識別資源集合。</span><span class="sxs-lookup"><span data-stu-id="f4464-109">At a high level, the identity registry is a REST-capable collection of device identity resources.</span></span> <span data-ttu-id="f4464-110">當您在身分識別登錄中新增項目時，IoT 中樞會建立一組每一裝置資源，例如，包含傳遞中雲端到裝置訊息的佇列。</span><span class="sxs-lookup"><span data-stu-id="f4464-110">When you add an entry in the identity registry, IoT Hub creates a set of per-device resources such as the queue that contains in-flight cloud-to-device messages.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="f4464-111">使用時機</span><span class="sxs-lookup"><span data-stu-id="f4464-111">When to use</span></span>

<span data-ttu-id="f4464-112">當您需要執行下列作業時，請使用身分識別登錄：</span><span class="sxs-lookup"><span data-stu-id="f4464-112">Use the identity registry when you need to:</span></span>

* <span data-ttu-id="f4464-113">佈建裝置來連線到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f4464-113">Provision devices that connect to your IoT hub.</span></span>
* <span data-ttu-id="f4464-114">控制每一裝置對中樞之面對裝置端點的存取。</span><span class="sxs-lookup"><span data-stu-id="f4464-114">Control per-device access to your hub's device-facing endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="f4464-115">身分識別登錄不包含任何應用程式特有中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f4464-115">The identity registry does not contain any application-specific metadata.</span></span>

## <a name="identity-registry-operations"></a><span data-ttu-id="f4464-116">身分識別登錄作業</span><span class="sxs-lookup"><span data-stu-id="f4464-116">Identity registry operations</span></span>

<span data-ttu-id="f4464-117">IoT 中樞身分識別登錄會公開下列作業︰</span><span class="sxs-lookup"><span data-stu-id="f4464-117">The IoT Hub identity registry exposes the following operations:</span></span>

* <span data-ttu-id="f4464-118">建立裝置身分識別</span><span class="sxs-lookup"><span data-stu-id="f4464-118">Create device identity</span></span>
* <span data-ttu-id="f4464-119">更新裝置身分識別</span><span class="sxs-lookup"><span data-stu-id="f4464-119">Update device identity</span></span>
* <span data-ttu-id="f4464-120">依照 ID 擷取裝置身分識別別</span><span class="sxs-lookup"><span data-stu-id="f4464-120">Retrieve device identity by ID</span></span>
* <span data-ttu-id="f4464-121">刪除裝置身分識別</span><span class="sxs-lookup"><span data-stu-id="f4464-121">Delete device identity</span></span>
* <span data-ttu-id="f4464-122">列出多達 1000 個識別</span><span class="sxs-lookup"><span data-stu-id="f4464-122">List up to 1000 identities</span></span>
* <span data-ttu-id="f4464-123">將所有身分識別匯出至 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="f4464-123">Export all identities to Azure blob storage</span></span>
* <span data-ttu-id="f4464-124">從 Azure Blob 儲存體匯入身分識別</span><span class="sxs-lookup"><span data-stu-id="f4464-124">Import identities from Azure blob storage</span></span>

<span data-ttu-id="f4464-125">上述所有作業均可使用 [RFC7232][lnk-rfc7232] 中指定的開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="f4464-125">All these operations can use optimistic concurrency, as specified in [RFC7232][lnk-rfc7232].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4464-126">如果要擷取 IoT 中樞的身分識別登錄中的所有身分識別，唯一方法是使用[匯出][lnk-export]功能。</span><span class="sxs-lookup"><span data-stu-id="f4464-126">The only way to retrieve all identities in an IoT hub's identity registry is to use the [Export][lnk-export] functionality.</span></span>

<span data-ttu-id="f4464-127">IoT 中樞身分識別登錄：</span><span class="sxs-lookup"><span data-stu-id="f4464-127">An IoT Hub identity registry:</span></span>

* <span data-ttu-id="f4464-128">不包含任何應用程式中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f4464-128">Does not contain any application metadata.</span></span>
* <span data-ttu-id="f4464-129">可以將 **deviceId** 做為索引鍵來存取，就像字典一樣。</span><span class="sxs-lookup"><span data-stu-id="f4464-129">Can be accessed like a dictionary, by using the **deviceId** as the key.</span></span>
* <span data-ttu-id="f4464-130">不支援表達式查詢。</span><span class="sxs-lookup"><span data-stu-id="f4464-130">Does not support expressive queries.</span></span>

<span data-ttu-id="f4464-131">IoT 方案通常具有不同的方案專屬存放區，其中包含應用程式特定的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f4464-131">An IoT solution typically has a separate solution-specific store that contains application-specific metadata.</span></span> <span data-ttu-id="f4464-132">例如，智慧建置方案中的解決方案專用存放區會記錄部署溫度感應器的空間。</span><span class="sxs-lookup"><span data-stu-id="f4464-132">For example, the solution-specific store in a smart building solution would record the room in which a temperature sensor is deployed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4464-133">只能將身分識別登錄用於裝置管理和佈建作業。</span><span class="sxs-lookup"><span data-stu-id="f4464-133">Only use the identity registry for device management and provisioning operations.</span></span> <span data-ttu-id="f4464-134">執行階段的高輸送量作業不應該仰賴在身分識別登錄中執行作業。</span><span class="sxs-lookup"><span data-stu-id="f4464-134">High throughput operations at run time should not depend on performing operations in the identity registry.</span></span> <span data-ttu-id="f4464-135">例如，在傳送命令前先檢查裝置的連線狀態就不是支援的模式。</span><span class="sxs-lookup"><span data-stu-id="f4464-135">For example, checking the connection state of a device before sending a command is not a supported pattern.</span></span> <span data-ttu-id="f4464-136">請務必檢查身分識別登錄的[節流速率][lnk-quotas]以及[裝置活動訊號][lnk-guidance-heartbeat]模式。</span><span class="sxs-lookup"><span data-stu-id="f4464-136">Make sure to check the [throttling rates][lnk-quotas] for the identity registry, and the [device heartbeat][lnk-guidance-heartbeat] pattern.</span></span>

## <a name="disable-devices"></a><span data-ttu-id="f4464-137">停用裝置</span><span class="sxs-lookup"><span data-stu-id="f4464-137">Disable devices</span></span>

<span data-ttu-id="f4464-138">您可以在身分識別登錄中更新身分識別的 [狀態] 屬性來停用裝置。</span><span class="sxs-lookup"><span data-stu-id="f4464-138">You can disable devices by updating the **status** property of an identity in the identity registry.</span></span> <span data-ttu-id="f4464-139">您通常會在兩種情況下使用此屬性：</span><span class="sxs-lookup"><span data-stu-id="f4464-139">Typically, you use this property in two scenarios:</span></span>

* <span data-ttu-id="f4464-140">在佈建協調程序期間。</span><span class="sxs-lookup"><span data-stu-id="f4464-140">During a provisioning orchestration process.</span></span> <span data-ttu-id="f4464-141">如需詳細資訊，請參閱[裝置佈建][lnk-guidance-provisioning]。</span><span class="sxs-lookup"><span data-stu-id="f4464-141">For more information, see [Device Provisioning][lnk-guidance-provisioning].</span></span>
* <span data-ttu-id="f4464-142">如果因為任何原因，您認為裝置遭到入侵，或變成未經授權。</span><span class="sxs-lookup"><span data-stu-id="f4464-142">If, for any reason, you consider a device is compromised or has become unauthorized.</span></span>

## <a name="import-and-export-device-identities"></a><span data-ttu-id="f4464-143">匯入和匯出裝置身分識別</span><span class="sxs-lookup"><span data-stu-id="f4464-143">Import and export device identities</span></span>

<span data-ttu-id="f4464-144">您可以使用 [IoT 中樞資源提供者端點][lnk-endpoints]上的非同步作業，從 IoT 中樞的身分識別登錄大量匯出裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="f4464-144">You can export device identities in bulk from an IoT hub's identity registry, by using asynchronous operations on the [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="f4464-145">匯出是長時間執行的作業，其使用客戶提供的 Blob 容器來儲存讀取自身分識別登錄的裝置身分識別資料。</span><span class="sxs-lookup"><span data-stu-id="f4464-145">Exports are long-running jobs that use a customer-supplied blob container to save device identity data read from the identity registry.</span></span>

<span data-ttu-id="f4464-146">您可以使用 [IoT 中樞資源提供者端點][lnk-endpoints]上的非同步作業，將裝置身分識別大量匯入 IoT 中樞的身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="f4464-146">You can import device identities in bulk to an IoT hub's identity registry, by using asynchronous operations on the [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="f4464-147">匯入是長時間執行的作業，其使用客戶提供的 Blob 容器中的資料，將裝置身分識別資料寫入至身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="f4464-147">Imports are long-running jobs that use data in a customer-supplied blob container to write device identity data into the identity registry.</span></span>

* <span data-ttu-id="f4464-148">如須匯入和匯出 API 的詳細資訊，請參閱 [IoT 中樞資源提供者 REST API][lnk-resource-provider-apis]。</span><span class="sxs-lookup"><span data-stu-id="f4464-148">For detailed information about the import and export APIs, see [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span>
* <span data-ttu-id="f4464-149">若要深入了解如何執行匯入和匯出作業，請參閱[大量管理 IoT 中樞的裝置身分識別][lnk-bulk-identity]。</span><span class="sxs-lookup"><span data-stu-id="f4464-149">To learn more about running import and export jobs, see [Bulk management of IoT Hub device identities][lnk-bulk-identity].</span></span>

## <a name="device-provisioning"></a><span data-ttu-id="f4464-150">裝置佈建</span><span class="sxs-lookup"><span data-stu-id="f4464-150">Device provisioning</span></span>

<span data-ttu-id="f4464-151">給定的 IoT 解決方案儲存的裝置資料取決於該解決方案的特定需求。</span><span class="sxs-lookup"><span data-stu-id="f4464-151">The device data that a given IoT solution stores depends on the specific requirements of that solution.</span></span> <span data-ttu-id="f4464-152">但是解決方案至少必須儲存裝置身分識別和驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="f4464-152">But, as a minimum, a solution must store device identities and authentication keys.</span></span> <span data-ttu-id="f4464-153">Azure IoT 中樞包含身分識別登錄，其可以儲存每個裝置的值，例如識別碼、驗證金鑰和狀態碼。</span><span class="sxs-lookup"><span data-stu-id="f4464-153">Azure IoT Hub includes an identity registry that can store values for each device such as IDs, authentication keys, and status codes.</span></span> <span data-ttu-id="f4464-154">解決方案可以使用其他 Azure 服務 (例如表格儲存體、Blob 儲存體或 Cosmos DB) 來儲存任何其他裝置資料。</span><span class="sxs-lookup"><span data-stu-id="f4464-154">A solution can use other Azure services such as table storage, blob storage, or Cosmos DB to store any additional device data.</span></span>

<span data-ttu-id="f4464-155">*裝置佈建* 是將初始裝置資料加入至解決方案中存放區的程序。</span><span class="sxs-lookup"><span data-stu-id="f4464-155">*Device provisioning* is the process of adding the initial device data to the stores in your solution.</span></span> <span data-ttu-id="f4464-156">若要讓新裝置能夠連接到您的中樞，必須將裝置識別碼和金鑰新增至「IoT 中樞」身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="f4464-156">To enable a new device to connect to your hub, you must add a device ID and keys to the IoT Hub identity registry.</span></span> <span data-ttu-id="f4464-157">做為佈建程序的一部分，您可能需要初始化其他解決方案存放區中的裝置特定資料。</span><span class="sxs-lookup"><span data-stu-id="f4464-157">As part of the provisioning process, you might need to initialize device-specific data in other solution stores.</span></span>

## <a name="device-heartbeat"></a><span data-ttu-id="f4464-158">裝置活動訊號</span><span class="sxs-lookup"><span data-stu-id="f4464-158">Device heartbeat</span></span>

<span data-ttu-id="f4464-159">IoT 中樞身分識別登錄包含稱為 **connectionState** 的欄位。</span><span class="sxs-lookup"><span data-stu-id="f4464-159">The IoT Hub identity registry contains a field called **connectionState**.</span></span> <span data-ttu-id="f4464-160">請只在進行開發和偵錯時才使用 **connectionState**。</span><span class="sxs-lookup"><span data-stu-id="f4464-160">Only use the **connectionState** field during development and debugging.</span></span> <span data-ttu-id="f4464-161">IoT 解決方案不應該在執行階段查詢欄位。</span><span class="sxs-lookup"><span data-stu-id="f4464-161">IoT solutions should not query the field at run time.</span></span> <span data-ttu-id="f4464-162">例如，請勿查詢 **connectionState** 欄位從而在傳送雲端到裝置訊息或 SMS 之前先確認裝置是否已連線。</span><span class="sxs-lookup"><span data-stu-id="f4464-162">For example, do not query the **connectionState** field to check if a device is connected before you send a cloud-to-device message or an SMS.</span></span>

<span data-ttu-id="f4464-163">如果 IoT 解決方案需要知道裝置是否已連線，請實作*活動訊號模式*。</span><span class="sxs-lookup"><span data-stu-id="f4464-163">If your IoT solution needs to know if a device is connected, you should implement the *heartbeat pattern*.</span></span>

<span data-ttu-id="f4464-164">在活動訊號模式中，裝置每隔固定時間就會至少傳送一次裝置到雲端的訊息 (例如，每小時至少一次)。</span><span class="sxs-lookup"><span data-stu-id="f4464-164">In the heartbeat pattern, the device sends device-to-cloud messages at least once every fixed amount of time (for example, at least once every hour).</span></span> <span data-ttu-id="f4464-165">因此，即使裝置沒有任何要傳送的資料，它仍會傳送空的裝置到雲端的訊息 (通常具有可識別它是活動訊號的屬性)。</span><span class="sxs-lookup"><span data-stu-id="f4464-165">Therefore, even if a device does not have any data to send, it still sends an empty device-to-cloud message (usually with a property that identifies it as a heartbeat).</span></span> <span data-ttu-id="f4464-166">此解決方案會在服務端保有一份對應，其中有針對每個裝置收到的最後一次活動訊號。</span><span class="sxs-lookup"><span data-stu-id="f4464-166">On the service side, the solution maintains a map with the last heartbeat received for each device.</span></span> <span data-ttu-id="f4464-167">此解決方案若未在預期時間內收到裝置傳來的活動訊號訊息，就會假設該裝置發生問題。</span><span class="sxs-lookup"><span data-stu-id="f4464-167">If the solution does not receive a heartbeat message within the expected time from the device, it assumes that there is a problem with the device.</span></span>

<span data-ttu-id="f4464-168">更複雜的實作可以包含來自[作業監視][lnk-devguide-opmon]的資訊，以便識別嘗試連接或通訊但失敗的裝置。</span><span class="sxs-lookup"><span data-stu-id="f4464-168">A more complex implementation could include the information from [operations monitoring][lnk-devguide-opmon] to identify devices that are trying to connect or communicate but failing.</span></span> <span data-ttu-id="f4464-169">當您實作活動訊號模式時，請務必檢查 [IoT 中樞配額與節流][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="f4464-169">When you implement the heartbeat pattern, make sure to check [IoT Hub Quotas and Throttles][lnk-quotas].</span></span>

> [!NOTE]
> <span data-ttu-id="f4464-170">如果 IoT 解決方案僅使用連線狀態來判斷是否要傳送雲端到裝置訊息，而且訊息未廣播到大量的裝置組合，請考慮使用較簡單的「短暫的到期時間」模式。</span><span class="sxs-lookup"><span data-stu-id="f4464-170">If an IoT solution uses the connection state solely to determine whether to send cloud-to-device messages, and messages are not broadcast to large sets of devices, consider using the simpler *short expiry time* pattern.</span></span> <span data-ttu-id="f4464-171">此模式所達到的效果與使用活動訊號模式來維護裝置連線狀態登錄相同，但更有效率。</span><span class="sxs-lookup"><span data-stu-id="f4464-171">This pattern achieves the same result as maintaining a device connection state registry using the heartbeat pattern, while being more efficient.</span></span> <span data-ttu-id="f4464-172">如果您要求訊息收條，IoT 中樞會通知您哪些裝置能夠收到訊息，哪些裝置不能收到。</span><span class="sxs-lookup"><span data-stu-id="f4464-172">If you request message acknowledgements, IoT Hub can notify you about which devices are able to receive messages and which are not.</span></span>

## <a name="device-lifecycle-notifications"></a><span data-ttu-id="f4464-173">裝置的生命週期通知</span><span class="sxs-lookup"><span data-stu-id="f4464-173">Device lifecycle notifications</span></span>

<span data-ttu-id="f4464-174">IoT 中樞在裝置身分識別建立或刪除時，可透過傳送裝置的生命週期通知，以通知 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="f4464-174">IoT Hub can notify your IoT solution when a device identity is created or deleted by sending device lifecycle notifications.</span></span> <span data-ttu-id="f4464-175">若要這樣做，您的 IoT 解決方案必須建立路由，並將資料來源設為等於 *DeviceLifecycleEvents*。</span><span class="sxs-lookup"><span data-stu-id="f4464-175">To do so, your IoT solution needs to create a route and to set the Data Source equal to *DeviceLifecycleEvents*.</span></span> <span data-ttu-id="f4464-176">根據預設，不會傳送任何生命週期通知，亦即沒有預先存在的這類路由。</span><span class="sxs-lookup"><span data-stu-id="f4464-176">By default, no lifecycle notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="f4464-177">通知訊息包含屬性和內文。</span><span class="sxs-lookup"><span data-stu-id="f4464-177">The notification message includes properties, and body.</span></span>

<span data-ttu-id="f4464-178">屬性：訊息系統屬性前面會加上 `'$'` 符號。</span><span class="sxs-lookup"><span data-stu-id="f4464-178">Properties: Message system properties are prefixed with the `'$'` symbol.</span></span>

| <span data-ttu-id="f4464-179">名稱</span><span class="sxs-lookup"><span data-stu-id="f4464-179">Name</span></span> | <span data-ttu-id="f4464-180">值</span><span class="sxs-lookup"><span data-stu-id="f4464-180">Value</span></span> |
| --- | --- |
<span data-ttu-id="f4464-181">$content-type</span><span class="sxs-lookup"><span data-stu-id="f4464-181">$content-type</span></span> | <span data-ttu-id="f4464-182">application/json</span><span class="sxs-lookup"><span data-stu-id="f4464-182">application/json</span></span> |
<span data-ttu-id="f4464-183">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="f4464-183">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="f4464-184">傳送通知的時間</span><span class="sxs-lookup"><span data-stu-id="f4464-184">Time when the notification was sent</span></span> |
<span data-ttu-id="f4464-185">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="f4464-185">$iothub-message-source</span></span> | <span data-ttu-id="f4464-186">deviceLifecycleEvents</span><span class="sxs-lookup"><span data-stu-id="f4464-186">deviceLifecycleEvents</span></span> |
<span data-ttu-id="f4464-187">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="f4464-187">$content-encoding</span></span> | <span data-ttu-id="f4464-188">utf-8</span><span class="sxs-lookup"><span data-stu-id="f4464-188">utf-8</span></span> |
<span data-ttu-id="f4464-189">opType</span><span class="sxs-lookup"><span data-stu-id="f4464-189">opType</span></span> | <span data-ttu-id="f4464-190">**createDeviceIdentity** 或 **deleteDeviceIdentity**</span><span class="sxs-lookup"><span data-stu-id="f4464-190">**createDeviceIdentity** or **deleteDeviceIdentity**</span></span> |
<span data-ttu-id="f4464-191">hubName</span><span class="sxs-lookup"><span data-stu-id="f4464-191">hubName</span></span> | <span data-ttu-id="f4464-192">IoT 中樞名稱</span><span class="sxs-lookup"><span data-stu-id="f4464-192">Name of IoT Hub</span></span> |
<span data-ttu-id="f4464-193">deviceId</span><span class="sxs-lookup"><span data-stu-id="f4464-193">deviceId</span></span> | <span data-ttu-id="f4464-194">裝置的識別碼</span><span class="sxs-lookup"><span data-stu-id="f4464-194">ID of the device</span></span> |
<span data-ttu-id="f4464-195">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="f4464-195">operationTimestamp</span></span> | <span data-ttu-id="f4464-196">作業的 ISO8601 時間戳記</span><span class="sxs-lookup"><span data-stu-id="f4464-196">ISO8601 timestamp of operation</span></span> |
<span data-ttu-id="f4464-197">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="f4464-197">iothub-message-schema</span></span> | <span data-ttu-id="f4464-198">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="f4464-198">deviceLifecycleNotification</span></span> |

<span data-ttu-id="f4464-199">主體：本節為 JSON 格式，它表示所建立裝置身分識別的對應項。</span><span class="sxs-lookup"><span data-stu-id="f4464-199">Body: This section is in JSON format and represents the twin of the created device identity.</span></span> <span data-ttu-id="f4464-200">例如，</span><span class="sxs-lookup"><span data-stu-id="f4464-200">For example,</span></span>

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a><span data-ttu-id="f4464-201">參考主題：</span><span class="sxs-lookup"><span data-stu-id="f4464-201">Reference topics:</span></span>

<span data-ttu-id="f4464-202">下列參考主題會提供您關於身分識別登錄的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f4464-202">The following reference topics provide you with more information about the identity registry.</span></span>

## <a name="device-identity-properties"></a><span data-ttu-id="f4464-203">裝置身分識別屬性</span><span class="sxs-lookup"><span data-stu-id="f4464-203">Device identity properties</span></span>

<span data-ttu-id="f4464-204">裝置身分識別會以具有下列屬性的 JSON 文件表示：</span><span class="sxs-lookup"><span data-stu-id="f4464-204">Device identities are represented as JSON documents with the following properties:</span></span>

| <span data-ttu-id="f4464-205">屬性</span><span class="sxs-lookup"><span data-stu-id="f4464-205">Property</span></span> | <span data-ttu-id="f4464-206">選項</span><span class="sxs-lookup"><span data-stu-id="f4464-206">Options</span></span> | <span data-ttu-id="f4464-207">說明</span><span class="sxs-lookup"><span data-stu-id="f4464-207">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f4464-208">deviceId</span><span class="sxs-lookup"><span data-stu-id="f4464-208">deviceId</span></span> |<span data-ttu-id="f4464-209">必要，只能讀取更新</span><span class="sxs-lookup"><span data-stu-id="f4464-209">required, read-only on updates</span></span> |<span data-ttu-id="f4464-210">區分大小寫的字串，最長為 128 個字元，可使用 ASCII 7 位元英數字元和 `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`。</span><span class="sxs-lookup"><span data-stu-id="f4464-210">A case-sensitive string (up to 128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="f4464-211">generationId</span><span class="sxs-lookup"><span data-stu-id="f4464-211">generationId</span></span> |<span data-ttu-id="f4464-212">必要，唯讀</span><span class="sxs-lookup"><span data-stu-id="f4464-212">required, read-only</span></span> |<span data-ttu-id="f4464-213">IoT 中樞產生的區分大小寫字串，最長為 128 個字元。</span><span class="sxs-lookup"><span data-stu-id="f4464-213">An IoT hub-generated, case-sensitive string up to 128 characters long.</span></span> <span data-ttu-id="f4464-214">此值可用來在刪除並重建裝置時，區分具有相同 **deviceId** 的裝置。</span><span class="sxs-lookup"><span data-stu-id="f4464-214">This value is used to distinguish devices with the same **deviceId**, when they have been deleted and re-created.</span></span> |
| <span data-ttu-id="f4464-215">etag</span><span class="sxs-lookup"><span data-stu-id="f4464-215">etag</span></span> |<span data-ttu-id="f4464-216">必要，唯讀</span><span class="sxs-lookup"><span data-stu-id="f4464-216">required, read-only</span></span> |<span data-ttu-id="f4464-217">依據 [RFC7232][lnk-rfc7232]，此字串代表裝置身分識別的弱式 ETag。</span><span class="sxs-lookup"><span data-stu-id="f4464-217">A string representing a weak ETag for the device identity, as per [RFC7232][lnk-rfc7232].</span></span> |
| <span data-ttu-id="f4464-218">auth</span><span class="sxs-lookup"><span data-stu-id="f4464-218">auth</span></span> |<span data-ttu-id="f4464-219">選用</span><span class="sxs-lookup"><span data-stu-id="f4464-219">optional</span></span> |<span data-ttu-id="f4464-220">包含驗證資訊和安全性資料的複合物件。</span><span class="sxs-lookup"><span data-stu-id="f4464-220">A composite object containing authentication information and security materials.</span></span> |
| <span data-ttu-id="f4464-221">auth.symkey</span><span class="sxs-lookup"><span data-stu-id="f4464-221">auth.symkey</span></span> |<span data-ttu-id="f4464-222">選用</span><span class="sxs-lookup"><span data-stu-id="f4464-222">optional</span></span> |<span data-ttu-id="f4464-223">包含主要和次要金鑰 (以 base64 格式儲存) 的複合物件。</span><span class="sxs-lookup"><span data-stu-id="f4464-223">A composite object containing a primary and a secondary key, stored in base64 format.</span></span> |
| <span data-ttu-id="f4464-224">status</span><span class="sxs-lookup"><span data-stu-id="f4464-224">status</span></span> |<span data-ttu-id="f4464-225">必要</span><span class="sxs-lookup"><span data-stu-id="f4464-225">required</span></span> |<span data-ttu-id="f4464-226">存取指示器。</span><span class="sxs-lookup"><span data-stu-id="f4464-226">An access indicator.</span></span> <span data-ttu-id="f4464-227">可以是 [已啟用] 或 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="f4464-227">Can be **Enabled** or **Disabled**.</span></span> <span data-ttu-id="f4464-228">如果為 [已啟用] ，則允許連接裝置。</span><span class="sxs-lookup"><span data-stu-id="f4464-228">If **Enabled**, the device is allowed to connect.</span></span> <span data-ttu-id="f4464-229">如果為 [已停用] ，此裝置無法存取任何裝置面向的端點。</span><span class="sxs-lookup"><span data-stu-id="f4464-229">If **Disabled**, this device cannot access any device-facing endpoint.</span></span> |
| <span data-ttu-id="f4464-230">statusReason</span><span class="sxs-lookup"><span data-stu-id="f4464-230">statusReason</span></span> |<span data-ttu-id="f4464-231">選用</span><span class="sxs-lookup"><span data-stu-id="f4464-231">optional</span></span> |<span data-ttu-id="f4464-232">長度為 128 個字元的字串，用來儲存裝置身分識別狀態的原因。</span><span class="sxs-lookup"><span data-stu-id="f4464-232">A 128 character-long string that stores the reason for the device identity status.</span></span> <span data-ttu-id="f4464-233">允許所有 UTF-8 字元。</span><span class="sxs-lookup"><span data-stu-id="f4464-233">All UTF-8 characters are allowed.</span></span> |
| <span data-ttu-id="f4464-234">statusUpdateTime</span><span class="sxs-lookup"><span data-stu-id="f4464-234">statusUpdateTime</span></span> |<span data-ttu-id="f4464-235">唯讀</span><span class="sxs-lookup"><span data-stu-id="f4464-235">read-only</span></span> |<span data-ttu-id="f4464-236">暫時指示器，顯示上次狀態更新的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="f4464-236">A temporal indicator, showing the date and time of the last status update.</span></span> |
| <span data-ttu-id="f4464-237">connectionState</span><span class="sxs-lookup"><span data-stu-id="f4464-237">connectionState</span></span> |<span data-ttu-id="f4464-238">唯讀</span><span class="sxs-lookup"><span data-stu-id="f4464-238">read-only</span></span> |<span data-ttu-id="f4464-239">指出連線狀態的欄位︰**已連線**或**已中斷連線**。</span><span class="sxs-lookup"><span data-stu-id="f4464-239">A field indicating connection status: either **Connected** or **Disconnected**.</span></span> <span data-ttu-id="f4464-240">這個欄位代表裝置連線狀態的 IoT 中樞檢視。</span><span class="sxs-lookup"><span data-stu-id="f4464-240">This field represents the IoT Hub view of the device connection status.</span></span> <span data-ttu-id="f4464-241">**重要事項**：此欄位只應用於開發/偵錯用途。</span><span class="sxs-lookup"><span data-stu-id="f4464-241">**Important**: This field should be used only for development/debugging purposes.</span></span> <span data-ttu-id="f4464-242">只有針對使用 MQTT 或 AMQP 的裝置才會更新連線狀態。</span><span class="sxs-lookup"><span data-stu-id="f4464-242">The connection state is updated only for devices using MQTT or AMQP.</span></span> <span data-ttu-id="f4464-243">此外，它是以通訊協定層級的偵測 (MQTT 偵測或 AMQP 偵測) 為基礎，而且最多只能有 5 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="f4464-243">Also, it is based on protocol-level pings (MQTT pings, or AMQP pings), and it can have a maximum delay of only 5 minutes.</span></span> <span data-ttu-id="f4464-244">基於這些理由，其中可能會有誤判的情形，例如將裝置回報為已連線，但卻已中斷連線。</span><span class="sxs-lookup"><span data-stu-id="f4464-244">For these reasons, there can be false positives, such as devices reported as connected but that are disconnected.</span></span> |
| <span data-ttu-id="f4464-245">connectionStateUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="f4464-245">connectionStateUpdatedTime</span></span> |<span data-ttu-id="f4464-246">唯讀</span><span class="sxs-lookup"><span data-stu-id="f4464-246">read-only</span></span> |<span data-ttu-id="f4464-247">暫時指示器，顯示上次更新連線狀態的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="f4464-247">A temporal indicator, showing the date and last time the connection state was updated.</span></span> |
| <span data-ttu-id="f4464-248">lastActivityTime</span><span class="sxs-lookup"><span data-stu-id="f4464-248">lastActivityTime</span></span> |<span data-ttu-id="f4464-249">唯讀</span><span class="sxs-lookup"><span data-stu-id="f4464-249">read-only</span></span> |<span data-ttu-id="f4464-250">暫時指示器，顯示裝置上次連接、接收或傳送訊息的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="f4464-250">A temporal indicator, showing the date and last time the device connected, received, or sent a message.</span></span> |

> [!NOTE]
> <span data-ttu-id="f4464-251">連線狀態只能代表連線狀態的 IoT 中樞檢視。</span><span class="sxs-lookup"><span data-stu-id="f4464-251">Connection state can only represent the IoT Hub view of the status of the connection.</span></span> <span data-ttu-id="f4464-252">根據網路狀況和組態而定，可能會延遲此狀態的更新。</span><span class="sxs-lookup"><span data-stu-id="f4464-252">Updates to this state may be delayed, depending on network conditions and configurations.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="f4464-253">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="f4464-253">Additional reference material</span></span>

<span data-ttu-id="f4464-254">IoT 中樞開發人員指南中的其他參考主題包括︰</span><span class="sxs-lookup"><span data-stu-id="f4464-254">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="f4464-255">[IoT 中樞端點][lnk-endpoints]說明每個 IoT 中樞公開給執行階段和管理作業的各種端點。</span><span class="sxs-lookup"><span data-stu-id="f4464-255">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="f4464-256">[節流和配額][lnk-quotas]描述適用於 IoT 中樞服務的配額和節流行為。</span><span class="sxs-lookup"><span data-stu-id="f4464-256">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="f4464-257">[Azure IoT 裝置和服務 SDK][lnk-sdks] 列出各種語言 SDK，可供您在開發與「IoT 中樞」互動的裝置和服務應用程式時使用。</span><span class="sxs-lookup"><span data-stu-id="f4464-257">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="f4464-258">[IoT 中樞查詢語言][lnk-query]描述可用來從 IoT 中樞擷取有關裝置對應項和作業之資訊的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="f4464-258">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="f4464-259">[IoT 中樞 MQTT 支援][lnk-devguide-mqtt]針對 MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f4464-259">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4464-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4464-260">Next steps</span></span>

<span data-ttu-id="f4464-261">現在您已了解如何使用 IoT 中樞身分識別登錄，接下來您可能對下列 IoT 中樞開發人員指南主題感興趣︰</span><span class="sxs-lookup"><span data-stu-id="f4464-261">Now you have learned how to use the IoT Hub identity registry, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="f4464-262">[控制 IoT 中樞的存取權][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="f4464-262">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="f4464-263">[使用裝置對應項同步處理狀態和組態][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="f4464-263">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="f4464-264">[在裝置上叫用直接方法][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="f4464-264">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="f4464-265">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="f4464-265">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="f4464-266">如果您想要嘗試本文章所述的概念，您可能會對下列 IoT 中樞教學課程感興趣：</span><span class="sxs-lookup"><span data-stu-id="f4464-266">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="f4464-267">[開始使用 Azure IoT 中樞][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f4464-267">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
