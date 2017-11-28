---
title: "aaaUnderstand hello Azure IoT 中樞身分識別登錄 |Microsoft 文件"
description: "開發人員指南-hello IoT 中樞身分識別登錄的描述以及 toouse 它 toomanage 您的裝置。 包含大量的 hello 匯入和匯出裝置身分識別的相關資訊。"
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
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a><span data-ttu-id="7b034-104">了解 hello 身分識別登錄在 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="7b034-104">Understand hello identity registry in your IoT hub</span></span>

<span data-ttu-id="7b034-105">每個 IoT 中樞的身分識別登錄儲存 hello 裝置允許 tooconnect toohello IoT 中樞的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7b034-105">Every IoT hub has an identity registry that stores information about hello devices permitted tooconnect toohello IoT hub.</span></span> <span data-ttu-id="7b034-106">裝置可以連線 tooan IoT 中樞之前，必須是該裝置 hello IoT 中樞的身分識別登錄中的項目。</span><span class="sxs-lookup"><span data-stu-id="7b034-106">Before a device can connect tooan IoT hub, there must be an entry for that device in hello IoT hub's identity registry.</span></span> <span data-ttu-id="7b034-107">裝置也必須與 hello IoT 中樞根據 hello 身分識別登錄中儲存的認證驗證。</span><span class="sxs-lookup"><span data-stu-id="7b034-107">A device must also authenticate with hello IoT hub based on credentials stored in hello identity registry.</span></span>

<span data-ttu-id="7b034-108">儲存在 hello 身分識別登錄中的 hello 裝置識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7b034-108">hello device ID stored in hello identity registry is case-sensitive.</span></span>

<span data-ttu-id="7b034-109">在高層級，hello 身分識別登錄是 REST 支援的裝置識別資源的集合。</span><span class="sxs-lookup"><span data-stu-id="7b034-109">At a high level, hello identity registry is a REST-capable collection of device identity resources.</span></span> <span data-ttu-id="7b034-110">當您在 hello 身分識別登錄中新增項目時，IoT 中樞將建立每一裝置的資源，例如 hello 佇列，其中包含執行中雲端到裝置訊息的集。</span><span class="sxs-lookup"><span data-stu-id="7b034-110">When you add an entry in hello identity registry, IoT Hub creates a set of per-device resources such as hello queue that contains in-flight cloud-to-device messages.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="7b034-111">當 toouse</span><span class="sxs-lookup"><span data-stu-id="7b034-111">When toouse</span></span>

<span data-ttu-id="7b034-112">當您需要時，請使用 hello 身分識別登錄：</span><span class="sxs-lookup"><span data-stu-id="7b034-112">Use hello identity registry when you need to:</span></span>

* <span data-ttu-id="7b034-113">連接 tooyour IoT 中樞的佈建裝置。</span><span class="sxs-lookup"><span data-stu-id="7b034-113">Provision devices that connect tooyour IoT hub.</span></span>
* <span data-ttu-id="7b034-114">控制每一裝置存取 tooyour 中樞的面對裝置的端點。</span><span class="sxs-lookup"><span data-stu-id="7b034-114">Control per-device access tooyour hub's device-facing endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="7b034-115">hello 身分識別登錄未包含任何應用程式專屬的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7b034-115">hello identity registry does not contain any application-specific metadata.</span></span>

## <a name="identity-registry-operations"></a><span data-ttu-id="7b034-116">身分識別登錄作業</span><span class="sxs-lookup"><span data-stu-id="7b034-116">Identity registry operations</span></span>

<span data-ttu-id="7b034-117">hello IoT 中樞身分識別登錄公開 hello 下列作業：</span><span class="sxs-lookup"><span data-stu-id="7b034-117">hello IoT Hub identity registry exposes hello following operations:</span></span>

* <span data-ttu-id="7b034-118">建立裝置身分識別</span><span class="sxs-lookup"><span data-stu-id="7b034-118">Create device identity</span></span>
* <span data-ttu-id="7b034-119">更新裝置身分識別</span><span class="sxs-lookup"><span data-stu-id="7b034-119">Update device identity</span></span>
* <span data-ttu-id="7b034-120">依照 ID 擷取裝置身分識別別</span><span class="sxs-lookup"><span data-stu-id="7b034-120">Retrieve device identity by ID</span></span>
* <span data-ttu-id="7b034-121">刪除裝置身分識別</span><span class="sxs-lookup"><span data-stu-id="7b034-121">Delete device identity</span></span>
* <span data-ttu-id="7b034-122">列出向上 too1000 身分識別</span><span class="sxs-lookup"><span data-stu-id="7b034-122">List up too1000 identities</span></span>
* <span data-ttu-id="7b034-123">匯出所有識別 tooAzure blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="7b034-123">Export all identities tooAzure blob storage</span></span>
* <span data-ttu-id="7b034-124">從 Azure Blob 儲存體匯入身分識別</span><span class="sxs-lookup"><span data-stu-id="7b034-124">Import identities from Azure blob storage</span></span>

<span data-ttu-id="7b034-125">上述所有作業均可使用 [RFC7232][lnk-rfc7232] 中指定的開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="7b034-125">All these operations can use optimistic concurrency, as specified in [RFC7232][lnk-rfc7232].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b034-126">hello 只方式 tooretrieve IoT 中樞的身分識別登錄中的所有識別身分為 toouse hello[匯出][ lnk-export]功能。</span><span class="sxs-lookup"><span data-stu-id="7b034-126">hello only way tooretrieve all identities in an IoT hub's identity registry is toouse hello [Export][lnk-export] functionality.</span></span>

<span data-ttu-id="7b034-127">IoT 中樞身分識別登錄：</span><span class="sxs-lookup"><span data-stu-id="7b034-127">An IoT Hub identity registry:</span></span>

* <span data-ttu-id="7b034-128">不包含任何應用程式中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7b034-128">Does not contain any application metadata.</span></span>
* <span data-ttu-id="7b034-129">就如同字典，可以存取使用 hello **deviceId** hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7b034-129">Can be accessed like a dictionary, by using hello **deviceId** as hello key.</span></span>
* <span data-ttu-id="7b034-130">不支援表達式查詢。</span><span class="sxs-lookup"><span data-stu-id="7b034-130">Does not support expressive queries.</span></span>

<span data-ttu-id="7b034-131">IoT 方案通常具有不同的方案專屬存放區，其中包含應用程式特定的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7b034-131">An IoT solution typically has a separate solution-specific store that contains application-specific metadata.</span></span> <span data-ttu-id="7b034-132">比方說，hello 智慧建置方案中的特定解決方案的存放區會記錄其中溫度感應器部署的 hello 聊天室。</span><span class="sxs-lookup"><span data-stu-id="7b034-132">For example, hello solution-specific store in a smart building solution would record hello room in which a temperature sensor is deployed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b034-133">只使用 hello 身分識別登錄裝置管理和佈建作業。</span><span class="sxs-lookup"><span data-stu-id="7b034-133">Only use hello identity registry for device management and provisioning operations.</span></span> <span data-ttu-id="7b034-134">在執行階段的高輸送量作業不應依賴在 hello 身分識別登錄中執行作業。</span><span class="sxs-lookup"><span data-stu-id="7b034-134">High throughput operations at run time should not depend on performing operations in hello identity registry.</span></span> <span data-ttu-id="7b034-135">例如，傳送命令之前，先檢查裝置 hello 連線狀態不支援的模式。</span><span class="sxs-lookup"><span data-stu-id="7b034-135">For example, checking hello connection state of a device before sending a command is not a supported pattern.</span></span> <span data-ttu-id="7b034-136">請確定 toocheck hello[節流速率][ lnk-quotas] hello 身分識別登錄及 hello[裝置活動訊號][ lnk-guidance-heartbeat]模式。</span><span class="sxs-lookup"><span data-stu-id="7b034-136">Make sure toocheck hello [throttling rates][lnk-quotas] for hello identity registry, and hello [device heartbeat][lnk-guidance-heartbeat] pattern.</span></span>

## <a name="disable-devices"></a><span data-ttu-id="7b034-137">停用裝置</span><span class="sxs-lookup"><span data-stu-id="7b034-137">Disable devices</span></span>

<span data-ttu-id="7b034-138">您可以藉由更新 hello 停用裝置**狀態**hello 身分識別登錄中的身分識別的屬性。</span><span class="sxs-lookup"><span data-stu-id="7b034-138">You can disable devices by updating hello **status** property of an identity in hello identity registry.</span></span> <span data-ttu-id="7b034-139">您通常會在兩種情況下使用此屬性：</span><span class="sxs-lookup"><span data-stu-id="7b034-139">Typically, you use this property in two scenarios:</span></span>

* <span data-ttu-id="7b034-140">在佈建協調程序期間。</span><span class="sxs-lookup"><span data-stu-id="7b034-140">During a provisioning orchestration process.</span></span> <span data-ttu-id="7b034-141">如需詳細資訊，請參閱[裝置佈建][lnk-guidance-provisioning]。</span><span class="sxs-lookup"><span data-stu-id="7b034-141">For more information, see [Device Provisioning][lnk-guidance-provisioning].</span></span>
* <span data-ttu-id="7b034-142">如果因為任何原因，您認為裝置遭到入侵，或變成未經授權。</span><span class="sxs-lookup"><span data-stu-id="7b034-142">If, for any reason, you consider a device is compromised or has become unauthorized.</span></span>

## <a name="import-and-export-device-identities"></a><span data-ttu-id="7b034-143">匯入和匯出裝置身分識別</span><span class="sxs-lookup"><span data-stu-id="7b034-143">Import and export device identities</span></span>

<span data-ttu-id="7b034-144">您也可以使用非同步作業上 hello 從 IoT 中樞的身分識別登錄，匯出大量裝置身分識別[IoT 中樞資源提供者端點][lnk-endpoints]。</span><span class="sxs-lookup"><span data-stu-id="7b034-144">You can export device identities in bulk from an IoT hub's identity registry, by using asynchronous operations on hello [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="7b034-145">匯出是長時間執行從 hello 身分識別登錄讀取使用客戶所提供的 blob 容器 toosave 裝置身分識別資料的工作。</span><span class="sxs-lookup"><span data-stu-id="7b034-145">Exports are long-running jobs that use a customer-supplied blob container toosave device identity data read from hello identity registry.</span></span>

<span data-ttu-id="7b034-146">您可以使用非同步作業上 hello 匯入裝置身分識別在大量 tooan IoT 中樞的身分識別登錄中， [IoT 中樞資源提供者端點][lnk-endpoints]。</span><span class="sxs-lookup"><span data-stu-id="7b034-146">You can import device identities in bulk tooan IoT hub's identity registry, by using asynchronous operations on hello [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="7b034-147">匯入而使用客戶所提供的 blob 容器 toowrite 裝置身分識別資料中的資料，到 hello 身分識別登錄的長時間執行作業。</span><span class="sxs-lookup"><span data-stu-id="7b034-147">Imports are long-running jobs that use data in a customer-supplied blob container toowrite device identity data into hello identity registry.</span></span>

* <span data-ttu-id="7b034-148">如需 hello 匯入和匯出應用程式開發介面的詳細資訊，請參閱[IoT 中樞資源提供者 REST Api][lnk-resource-provider-apis]。</span><span class="sxs-lookup"><span data-stu-id="7b034-148">For detailed information about hello import and export APIs, see [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span>
* <span data-ttu-id="7b034-149">執行有關的詳細資訊匯入和匯出工作，請參閱的 toolearn[大量的 IoT 中樞裝置身分識別管理][lnk-bulk-identity]。</span><span class="sxs-lookup"><span data-stu-id="7b034-149">toolearn more about running import and export jobs, see [Bulk management of IoT Hub device identities][lnk-bulk-identity].</span></span>

## <a name="device-provisioning"></a><span data-ttu-id="7b034-150">裝置佈建</span><span class="sxs-lookup"><span data-stu-id="7b034-150">Device provisioning</span></span>

<span data-ttu-id="7b034-151">給定的 IoT 解決方案儲存 hello 裝置資料 hello 的該方案的特定需求而定。</span><span class="sxs-lookup"><span data-stu-id="7b034-151">hello device data that a given IoT solution stores depends on hello specific requirements of that solution.</span></span> <span data-ttu-id="7b034-152">但是解決方案至少必須儲存裝置身分識別和驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="7b034-152">But, as a minimum, a solution must store device identities and authentication keys.</span></span> <span data-ttu-id="7b034-153">Azure IoT 中樞包含身分識別登錄，其可以儲存每個裝置的值，例如識別碼、驗證金鑰和狀態碼。</span><span class="sxs-lookup"><span data-stu-id="7b034-153">Azure IoT Hub includes an identity registry that can store values for each device such as IDs, authentication keys, and status codes.</span></span> <span data-ttu-id="7b034-154">解決方案可以使用其他 Azure 服務，例如資料表儲存體、 blob 儲存體或 Cosmos DB toostore 任何其他裝置的資料。</span><span class="sxs-lookup"><span data-stu-id="7b034-154">A solution can use other Azure services such as table storage, blob storage, or Cosmos DB toostore any additional device data.</span></span>

<span data-ttu-id="7b034-155">*裝置佈建*是 hello 程序在您的方案中加入 hello 初始裝置資料 toohello 存放區。</span><span class="sxs-lookup"><span data-stu-id="7b034-155">*Device provisioning* is hello process of adding hello initial device data toohello stores in your solution.</span></span> <span data-ttu-id="7b034-156">tooenable 新裝置 tooconnect tooyour 中樞，您必須新增裝置識別碼和金鑰 toohello IoT 中樞身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="7b034-156">tooenable a new device tooconnect tooyour hub, you must add a device ID and keys toohello IoT Hub identity registry.</span></span> <span data-ttu-id="7b034-157">Hello 佈建程序的一部分，您可能需要其他的方案存放區中的 tooinitialize 裝置的特定資料。</span><span class="sxs-lookup"><span data-stu-id="7b034-157">As part of hello provisioning process, you might need tooinitialize device-specific data in other solution stores.</span></span>

## <a name="device-heartbeat"></a><span data-ttu-id="7b034-158">裝置活動訊號</span><span class="sxs-lookup"><span data-stu-id="7b034-158">Device heartbeat</span></span>

<span data-ttu-id="7b034-159">hello IoT 中樞身分識別登錄包含名為的欄位**connectionState**。</span><span class="sxs-lookup"><span data-stu-id="7b034-159">hello IoT Hub identity registry contains a field called **connectionState**.</span></span> <span data-ttu-id="7b034-160">只使用 hello **connectionState**欄位在開發和偵錯。</span><span class="sxs-lookup"><span data-stu-id="7b034-160">Only use hello **connectionState** field during development and debugging.</span></span> <span data-ttu-id="7b034-161">IoT 解決方案不應該在執行階段查詢 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="7b034-161">IoT solutions should not query hello field at run time.</span></span> <span data-ttu-id="7b034-162">例如，不會查詢 hello **connectionState**欄位 toocheck 如果裝置傳送 SMS 或雲端到裝置訊息之前，先連線。</span><span class="sxs-lookup"><span data-stu-id="7b034-162">For example, do not query hello **connectionState** field toocheck if a device is connected before you send a cloud-to-device message or an SMS.</span></span>

<span data-ttu-id="7b034-163">如果您的 IoT 解決方案需要 tooknow，如果裝置連線，您應該實作 hello*活動訊號模式*。</span><span class="sxs-lookup"><span data-stu-id="7b034-163">If your IoT solution needs tooknow if a device is connected, you should implement hello *heartbeat pattern*.</span></span>

<span data-ttu-id="7b034-164">在 hello 活動訊號模式中，hello 裝置傳送裝置到雲端訊息至少一次每個固定的 （例如，至少一次每小時） 的時間量。</span><span class="sxs-lookup"><span data-stu-id="7b034-164">In hello heartbeat pattern, hello device sends device-to-cloud messages at least once every fixed amount of time (for example, at least once every hour).</span></span> <span data-ttu-id="7b034-165">因此，即使裝置沒有任何資料 toosend，它仍會傳送空的裝置到雲端訊息 （通常會有這種屬性識別為活動訊號）。</span><span class="sxs-lookup"><span data-stu-id="7b034-165">Therefore, even if a device does not have any data toosend, it still sends an empty device-to-cloud message (usually with a property that identifies it as a heartbeat).</span></span> <span data-ttu-id="7b034-166">Hello 服務端，hello 方案會針對每個裝置收到 hello 上次活動訊號與維護對應。</span><span class="sxs-lookup"><span data-stu-id="7b034-166">On hello service side, hello solution maintains a map with hello last heartbeat received for each device.</span></span> <span data-ttu-id="7b034-167">如果 hello 方案從 hello 裝置 hello 預期時間內未收到活動訊號訊息，則會假設沒有發生 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="7b034-167">If hello solution does not receive a heartbeat message within hello expected time from hello device, it assumes that there is a problem with hello device.</span></span>

<span data-ttu-id="7b034-168">更複雜的實作可能包含來自 hello 資訊[作業監視][ lnk-devguide-opmon]嘗試 tooconnect 或通訊的 tooidentify 裝置但失敗。</span><span class="sxs-lookup"><span data-stu-id="7b034-168">A more complex implementation could include hello information from [operations monitoring][lnk-devguide-opmon] tooidentify devices that are trying tooconnect or communicate but failing.</span></span> <span data-ttu-id="7b034-169">當您實作 hello 活動訊號模式時，請確定 toocheck [IoT 中樞配額與節流閥][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="7b034-169">When you implement hello heartbeat pattern, make sure toocheck [IoT Hub Quotas and Throttles][lnk-quotas].</span></span>

> [!NOTE]
> <span data-ttu-id="7b034-170">如果 IoT 解決方案會使用 hello 連接狀態而單獨 toodetermine 是否 toosend 雲端到裝置訊息，而且訊息已經不廣播 toolarge 設定的裝置，請考慮使用簡單的 hello*簡短到期時間*模式。</span><span class="sxs-lookup"><span data-stu-id="7b034-170">If an IoT solution uses hello connection state solely toodetermine whether toosend cloud-to-device messages, and messages are not broadcast toolarge sets of devices, consider using hello simpler *short expiry time* pattern.</span></span> <span data-ttu-id="7b034-171">此模式不會達到相同結果與維護裝置連線狀態登錄使用 hello 活動訊號模式，同時會更有效率的 hello。</span><span class="sxs-lookup"><span data-stu-id="7b034-171">This pattern achieves hello same result as maintaining a device connection state registry using hello heartbeat pattern, while being more efficient.</span></span> <span data-ttu-id="7b034-172">如果您要求訊息收條，IoT 中樞會通知您相關的裝置是無法 tooreceive 訊息，並不是。</span><span class="sxs-lookup"><span data-stu-id="7b034-172">If you request message acknowledgements, IoT Hub can notify you about which devices are able tooreceive messages and which are not.</span></span>

## <a name="device-lifecycle-notifications"></a><span data-ttu-id="7b034-173">裝置的生命週期通知</span><span class="sxs-lookup"><span data-stu-id="7b034-173">Device lifecycle notifications</span></span>

<span data-ttu-id="7b034-174">IoT 中樞在裝置身分識別建立或刪除時，可透過傳送裝置的生命週期通知，以通知 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b034-174">IoT Hub can notify your IoT solution when a device identity is created or deleted by sending device lifecycle notifications.</span></span> <span data-ttu-id="7b034-175">toodo 因此，您的 IoT 解決方案需要 toocreate 路由和 tooset hello 資料來源等太*DeviceLifecycleEvents*。</span><span class="sxs-lookup"><span data-stu-id="7b034-175">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*DeviceLifecycleEvents*.</span></span> <span data-ttu-id="7b034-176">根據預設，不會傳送任何生命週期通知，亦即沒有預先存在的這類路由。</span><span class="sxs-lookup"><span data-stu-id="7b034-176">By default, no lifecycle notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="7b034-177">hello 通知訊息包含屬性和內文。</span><span class="sxs-lookup"><span data-stu-id="7b034-177">hello notification message includes properties, and body.</span></span>

<span data-ttu-id="7b034-178">屬性： 訊息系統屬性前面會加上 hello`'$'`符號。</span><span class="sxs-lookup"><span data-stu-id="7b034-178">Properties: Message system properties are prefixed with hello `'$'` symbol.</span></span>

| <span data-ttu-id="7b034-179">名稱</span><span class="sxs-lookup"><span data-stu-id="7b034-179">Name</span></span> | <span data-ttu-id="7b034-180">值</span><span class="sxs-lookup"><span data-stu-id="7b034-180">Value</span></span> |
| --- | --- |
<span data-ttu-id="7b034-181">$content-type</span><span class="sxs-lookup"><span data-stu-id="7b034-181">$content-type</span></span> | <span data-ttu-id="7b034-182">application/json</span><span class="sxs-lookup"><span data-stu-id="7b034-182">application/json</span></span> |
<span data-ttu-id="7b034-183">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="7b034-183">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="7b034-184">傳送嗨通知時間</span><span class="sxs-lookup"><span data-stu-id="7b034-184">Time when hello notification was sent</span></span> |
<span data-ttu-id="7b034-185">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="7b034-185">$iothub-message-source</span></span> | <span data-ttu-id="7b034-186">deviceLifecycleEvents</span><span class="sxs-lookup"><span data-stu-id="7b034-186">deviceLifecycleEvents</span></span> |
<span data-ttu-id="7b034-187">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="7b034-187">$content-encoding</span></span> | <span data-ttu-id="7b034-188">utf-8</span><span class="sxs-lookup"><span data-stu-id="7b034-188">utf-8</span></span> |
<span data-ttu-id="7b034-189">opType</span><span class="sxs-lookup"><span data-stu-id="7b034-189">opType</span></span> | <span data-ttu-id="7b034-190">**createDeviceIdentity** 或 **deleteDeviceIdentity**</span><span class="sxs-lookup"><span data-stu-id="7b034-190">**createDeviceIdentity** or **deleteDeviceIdentity**</span></span> |
<span data-ttu-id="7b034-191">hubName</span><span class="sxs-lookup"><span data-stu-id="7b034-191">hubName</span></span> | <span data-ttu-id="7b034-192">IoT 中樞名稱</span><span class="sxs-lookup"><span data-stu-id="7b034-192">Name of IoT Hub</span></span> |
<span data-ttu-id="7b034-193">deviceId</span><span class="sxs-lookup"><span data-stu-id="7b034-193">deviceId</span></span> | <span data-ttu-id="7b034-194">Hello 裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="7b034-194">ID of hello device</span></span> |
<span data-ttu-id="7b034-195">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="7b034-195">operationTimestamp</span></span> | <span data-ttu-id="7b034-196">作業的 ISO8601 時間戳記</span><span class="sxs-lookup"><span data-stu-id="7b034-196">ISO8601 timestamp of operation</span></span> |
<span data-ttu-id="7b034-197">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="7b034-197">iothub-message-schema</span></span> | <span data-ttu-id="7b034-198">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="7b034-198">deviceLifecycleNotification</span></span> |

<span data-ttu-id="7b034-199">本文： 本章節的 JSON 格式，並代表 hello 兩個的 hello 建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="7b034-199">Body: This section is in JSON format and represents hello twin of hello created device identity.</span></span> <span data-ttu-id="7b034-200">例如，</span><span class="sxs-lookup"><span data-stu-id="7b034-200">For example,</span></span>

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

## <a name="reference-topics"></a><span data-ttu-id="7b034-201">參考主題：</span><span class="sxs-lookup"><span data-stu-id="7b034-201">Reference topics:</span></span>

<span data-ttu-id="7b034-202">hello 下列參考主題提供您有關 hello 身分識別登錄的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7b034-202">hello following reference topics provide you with more information about hello identity registry.</span></span>

## <a name="device-identity-properties"></a><span data-ttu-id="7b034-203">裝置身分識別屬性</span><span class="sxs-lookup"><span data-stu-id="7b034-203">Device identity properties</span></span>

<span data-ttu-id="7b034-204">裝置身分識別被以 JSON 文件以 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="7b034-204">Device identities are represented as JSON documents with hello following properties:</span></span>

| <span data-ttu-id="7b034-205">屬性</span><span class="sxs-lookup"><span data-stu-id="7b034-205">Property</span></span> | <span data-ttu-id="7b034-206">選項</span><span class="sxs-lookup"><span data-stu-id="7b034-206">Options</span></span> | <span data-ttu-id="7b034-207">說明</span><span class="sxs-lookup"><span data-stu-id="7b034-207">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b034-208">deviceId</span><span class="sxs-lookup"><span data-stu-id="7b034-208">deviceId</span></span> |<span data-ttu-id="7b034-209">必要，只能讀取更新</span><span class="sxs-lookup"><span data-stu-id="7b034-209">required, read-only on updates</span></span> |<span data-ttu-id="7b034-210">ASCII 7 位元的英數字元的區分大小寫字串 （向上 too128 字元） + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`。</span><span class="sxs-lookup"><span data-stu-id="7b034-210">A case-sensitive string (up too128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="7b034-211">generationId</span><span class="sxs-lookup"><span data-stu-id="7b034-211">generationId</span></span> |<span data-ttu-id="7b034-212">必要，唯讀</span><span class="sxs-lookup"><span data-stu-id="7b034-212">required, read-only</span></span> |<span data-ttu-id="7b034-213">IoT 中樞產生、 區分大小寫的字串 too128 字元組成。</span><span class="sxs-lookup"><span data-stu-id="7b034-213">An IoT hub-generated, case-sensitive string up too128 characters long.</span></span> <span data-ttu-id="7b034-214">這個值是使用的 toodistinguish 裝置 hello 相同**deviceId**，當它們已經刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="7b034-214">This value is used toodistinguish devices with hello same **deviceId**, when they have been deleted and re-created.</span></span> |
| <span data-ttu-id="7b034-215">etag</span><span class="sxs-lookup"><span data-stu-id="7b034-215">etag</span></span> |<span data-ttu-id="7b034-216">必要，唯讀</span><span class="sxs-lookup"><span data-stu-id="7b034-216">required, read-only</span></span> |<span data-ttu-id="7b034-217">表示弱式 ETag hello 裝置身分識別，做為每個字串[RFC7232][lnk-rfc7232]。</span><span class="sxs-lookup"><span data-stu-id="7b034-217">A string representing a weak ETag for hello device identity, as per [RFC7232][lnk-rfc7232].</span></span> |
| <span data-ttu-id="7b034-218">auth</span><span class="sxs-lookup"><span data-stu-id="7b034-218">auth</span></span> |<span data-ttu-id="7b034-219">選用</span><span class="sxs-lookup"><span data-stu-id="7b034-219">optional</span></span> |<span data-ttu-id="7b034-220">包含驗證資訊和安全性資料的複合物件。</span><span class="sxs-lookup"><span data-stu-id="7b034-220">A composite object containing authentication information and security materials.</span></span> |
| <span data-ttu-id="7b034-221">auth.symkey</span><span class="sxs-lookup"><span data-stu-id="7b034-221">auth.symkey</span></span> |<span data-ttu-id="7b034-222">選用</span><span class="sxs-lookup"><span data-stu-id="7b034-222">optional</span></span> |<span data-ttu-id="7b034-223">包含主要和次要金鑰 (以 base64 格式儲存) 的複合物件。</span><span class="sxs-lookup"><span data-stu-id="7b034-223">A composite object containing a primary and a secondary key, stored in base64 format.</span></span> |
| <span data-ttu-id="7b034-224">status</span><span class="sxs-lookup"><span data-stu-id="7b034-224">status</span></span> |<span data-ttu-id="7b034-225">必要</span><span class="sxs-lookup"><span data-stu-id="7b034-225">required</span></span> |<span data-ttu-id="7b034-226">存取指示器。</span><span class="sxs-lookup"><span data-stu-id="7b034-226">An access indicator.</span></span> <span data-ttu-id="7b034-227">可以是 [已啟用] 或 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="7b034-227">Can be **Enabled** or **Disabled**.</span></span> <span data-ttu-id="7b034-228">如果**啟用**，且允許 tooconnect hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="7b034-228">If **Enabled**, hello device is allowed tooconnect.</span></span> <span data-ttu-id="7b034-229">如果為 [已停用] ，此裝置無法存取任何裝置面向的端點。</span><span class="sxs-lookup"><span data-stu-id="7b034-229">If **Disabled**, this device cannot access any device-facing endpoint.</span></span> |
| <span data-ttu-id="7b034-230">statusReason</span><span class="sxs-lookup"><span data-stu-id="7b034-230">statusReason</span></span> |<span data-ttu-id="7b034-231">選用</span><span class="sxs-lookup"><span data-stu-id="7b034-231">optional</span></span> |<span data-ttu-id="7b034-232">128 字元長時間的字串存放區 hello 因此 hello 裝置身分識別的狀態。</span><span class="sxs-lookup"><span data-stu-id="7b034-232">A 128 character-long string that stores hello reason for hello device identity status.</span></span> <span data-ttu-id="7b034-233">允許所有 UTF-8 字元。</span><span class="sxs-lookup"><span data-stu-id="7b034-233">All UTF-8 characters are allowed.</span></span> |
| <span data-ttu-id="7b034-234">statusUpdateTime</span><span class="sxs-lookup"><span data-stu-id="7b034-234">statusUpdateTime</span></span> |<span data-ttu-id="7b034-235">唯讀</span><span class="sxs-lookup"><span data-stu-id="7b034-235">read-only</span></span> |<span data-ttu-id="7b034-236">顯示 hello 日期和時間的最後一個狀態更新 hello 時態指標。</span><span class="sxs-lookup"><span data-stu-id="7b034-236">A temporal indicator, showing hello date and time of hello last status update.</span></span> |
| <span data-ttu-id="7b034-237">connectionState</span><span class="sxs-lookup"><span data-stu-id="7b034-237">connectionState</span></span> |<span data-ttu-id="7b034-238">唯讀</span><span class="sxs-lookup"><span data-stu-id="7b034-238">read-only</span></span> |<span data-ttu-id="7b034-239">指出連線狀態的欄位︰**已連線**或**已中斷連線**。</span><span class="sxs-lookup"><span data-stu-id="7b034-239">A field indicating connection status: either **Connected** or **Disconnected**.</span></span> <span data-ttu-id="7b034-240">此欄位會顯示 hello IoT 中樞角度 hello 裝置連接狀態。</span><span class="sxs-lookup"><span data-stu-id="7b034-240">This field represents hello IoT Hub view of hello device connection status.</span></span> <span data-ttu-id="7b034-241">**重要事項**：此欄位只應用於開發/偵錯用途。</span><span class="sxs-lookup"><span data-stu-id="7b034-241">**Important**: This field should be used only for development/debugging purposes.</span></span> <span data-ttu-id="7b034-242">hello 連線狀態會更新僅適用於使用 MQTT 或 AMQP 的裝置。</span><span class="sxs-lookup"><span data-stu-id="7b034-242">hello connection state is updated only for devices using MQTT or AMQP.</span></span> <span data-ttu-id="7b034-243">此外，它是以通訊協定層級的偵測 (MQTT 偵測或 AMQP 偵測) 為基礎，而且最多只能有 5 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="7b034-243">Also, it is based on protocol-level pings (MQTT pings, or AMQP pings), and it can have a maximum delay of only 5 minutes.</span></span> <span data-ttu-id="7b034-244">基於這些理由，其中可能會有誤判的情形，例如將裝置回報為已連線，但卻已中斷連線。</span><span class="sxs-lookup"><span data-stu-id="7b034-244">For these reasons, there can be false positives, such as devices reported as connected but that are disconnected.</span></span> |
| <span data-ttu-id="7b034-245">connectionStateUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="7b034-245">connectionStateUpdatedTime</span></span> |<span data-ttu-id="7b034-246">唯讀</span><span class="sxs-lookup"><span data-stu-id="7b034-246">read-only</span></span> |<span data-ttu-id="7b034-247">已更新時態的指標，並顯示 hello 日期和最後一個階段 hello 連線狀態。</span><span class="sxs-lookup"><span data-stu-id="7b034-247">A temporal indicator, showing hello date and last time hello connection state was updated.</span></span> |
| <span data-ttu-id="7b034-248">lastActivityTime</span><span class="sxs-lookup"><span data-stu-id="7b034-248">lastActivityTime</span></span> |<span data-ttu-id="7b034-249">唯讀</span><span class="sxs-lookup"><span data-stu-id="7b034-249">read-only</span></span> |<span data-ttu-id="7b034-250">暫時的指標，並顯示 hello 日期和最後一個時間 hello 裝置連線、 收到，或已傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="7b034-250">A temporal indicator, showing hello date and last time hello device connected, received, or sent a message.</span></span> |

> [!NOTE]
> <span data-ttu-id="7b034-251">連接狀態只能表示 hello IoT 中樞角度 hello hello 連線狀態。</span><span class="sxs-lookup"><span data-stu-id="7b034-251">Connection state can only represent hello IoT Hub view of hello status of hello connection.</span></span> <span data-ttu-id="7b034-252">更新 toothis 狀態可能會延遲，視網路狀況和組態而定。</span><span class="sxs-lookup"><span data-stu-id="7b034-252">Updates toothis state may be delayed, depending on network conditions and configurations.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="7b034-253">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="7b034-253">Additional reference material</span></span>

<span data-ttu-id="7b034-254">Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：</span><span class="sxs-lookup"><span data-stu-id="7b034-254">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="7b034-255">[IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。</span><span class="sxs-lookup"><span data-stu-id="7b034-255">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="7b034-256">[節流和配額][ lnk-quotas]描述 hello 配額和節流套用 toohello IoT 中心服務的行為。</span><span class="sxs-lookup"><span data-stu-id="7b034-256">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="7b034-257">[Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用的 Sdk。</span><span class="sxs-lookup"><span data-stu-id="7b034-257">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="7b034-258">[IoT 中樞的查詢語言][ lnk-query]描述 hello 查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7b034-258">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="7b034-259">[IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7b034-259">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b034-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b034-260">Next steps</span></span>

<span data-ttu-id="7b034-261">現在您已經學會如何 toouse hello IoT 中樞身分識別登錄，您可能會想要遵循 IoT 中樞開發人員指南主題 hello:</span><span class="sxs-lookup"><span data-stu-id="7b034-261">Now you have learned how toouse hello IoT Hub identity registry, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="7b034-262">[控制存取 tooIoT 中樞][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="7b034-262">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="7b034-263">[使用裝置雙 toosynchronize 狀態和組態][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="7b034-263">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="7b034-264">[在裝置上叫用直接方法][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="7b034-264">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="7b034-265">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="7b034-265">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="7b034-266">如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b034-266">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="7b034-267">[開始使用 Azure IoT 中樞][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="7b034-267">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>

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
