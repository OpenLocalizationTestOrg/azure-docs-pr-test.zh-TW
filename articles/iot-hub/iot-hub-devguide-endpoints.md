---
title: "aaaUnderstand Azure IoT 中樞端點 |Microsoft 文件"
description: "開發人員指南 - IoT 中樞裝置對向端點和服務對向端點的相關參考資訊。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a><span data-ttu-id="cafa2-103">參考 - IoT 中樞端點</span><span class="sxs-lookup"><span data-stu-id="cafa2-103">Reference - IoT Hub endpoints</span></span>

## <a name="iot-hub-names"></a><span data-ttu-id="cafa2-104">IoT 中樞名稱</span><span class="sxs-lookup"><span data-stu-id="cafa2-104">IoT Hub names</span></span>

<span data-ttu-id="cafa2-105">您可以找到 hello hello IoT 中樞裝載 hello hello 入口網站中的端點名稱**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cafa2-105">You can find hello name of hello IoT hub that hosts your endpoints in hello portal on hello **Overview** blade.</span></span> <span data-ttu-id="cafa2-106">根據預設，hello DNS 名稱的 IoT 中樞看起來像： `{your iot hub name}.azure-devices.net`。</span><span class="sxs-lookup"><span data-stu-id="cafa2-106">By default, hello DNS name of an IoT hub looks like: `{your iot hub name}.azure-devices.net`.</span></span>

<span data-ttu-id="cafa2-107">您可以使用 Azure DNS toocreate IoT 中樞的自訂 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="cafa2-107">You can use Azure DNS toocreate a custom DNS name for your IoT hub.</span></span> <span data-ttu-id="cafa2-108">如需詳細資訊，請參閱[一項 Azure 服務使用 Azure DNS tooprovide 自訂網域設定](../dns/dns-custom-domain.md#azure-iot)。</span><span class="sxs-lookup"><span data-stu-id="cafa2-108">For more information, see [Use Azure DNS tooprovide custom domain settings for an Azure service](../dns/dns-custom-domain.md#azure-iot).</span></span>

## <a name="list-of-built-in-iot-hub-endpoints"></a><span data-ttu-id="cafa2-109">內建 IoT 中樞端點清單</span><span class="sxs-lookup"><span data-stu-id="cafa2-109">List of built-in IoT Hub endpoints</span></span>

<span data-ttu-id="cafa2-110">Azure IoT 中樞是公開其功能 toovarious 執行者的多租用戶服務。</span><span class="sxs-lookup"><span data-stu-id="cafa2-110">Azure IoT Hub is a multi-tenant service that exposes its functionality toovarious actors.</span></span> <span data-ttu-id="cafa2-111">hello 下列圖表顯示 hello 各種 IoT 中樞會公開的端點。</span><span class="sxs-lookup"><span data-stu-id="cafa2-111">hello following diagram shows hello various endpoints that IoT Hub exposes.</span></span>

![IoT 中樞端點][img-endpoints]

<span data-ttu-id="cafa2-113">hello 下列清單描述 hello 端點：</span><span class="sxs-lookup"><span data-stu-id="cafa2-113">hello following list describes hello endpoints:</span></span>

* <span data-ttu-id="cafa2-114">**資源提供者**。</span><span class="sxs-lookup"><span data-stu-id="cafa2-114">**Resource provider**.</span></span> <span data-ttu-id="cafa2-115">hello IoT 中樞資源提供者會公開[Azure Resource Manager] [ lnk-arm]介面。</span><span class="sxs-lookup"><span data-stu-id="cafa2-115">hello IoT Hub resource provider exposes an [Azure Resource Manager][lnk-arm] interface.</span></span> <span data-ttu-id="cafa2-116">此介面可讓 Azure 訂用帳戶擁有者 toocreate，而且刪除 IoT 中樞與 tooupdate IoT 中樞內容。</span><span class="sxs-lookup"><span data-stu-id="cafa2-116">This interface enables Azure subscription owners toocreate and delete IoT hubs, and tooupdate IoT hub properties.</span></span> <span data-ttu-id="cafa2-117">IoT 中樞屬性用來管理[中樞層級安全性原則][lnk-accesscontrol]，與 toodevice 層級存取控制和雲端到裝置和裝置到雲端訊息的功能選項。</span><span class="sxs-lookup"><span data-stu-id="cafa2-117">IoT Hub properties govern [hub-level security policies][lnk-accesscontrol], as opposed toodevice-level access control, and functional options for cloud-to-device and device-to-cloud messaging.</span></span> <span data-ttu-id="cafa2-118">hello IoT 中樞資源提供者也可讓您太[匯出裝置身分識別][lnk-importexport]。</span><span class="sxs-lookup"><span data-stu-id="cafa2-118">hello IoT Hub resource provider also enables you too[export device identities][lnk-importexport].</span></span>
* <span data-ttu-id="cafa2-119">**裝置身分識別管理**。</span><span class="sxs-lookup"><span data-stu-id="cafa2-119">**Device identity management**.</span></span> <span data-ttu-id="cafa2-120">每個 IoT 中樞會公開一組 HTTP 的 REST 端點 toomanage 裝置身分識別 （建立、 擷取、 更新和刪除）。</span><span class="sxs-lookup"><span data-stu-id="cafa2-120">Each IoT hub exposes a set of HTTP REST endpoints toomanage device identities (create, retrieve, update, and delete).</span></span> <span data-ttu-id="cafa2-121">[裝置身分識別][lnk-device-identities]用於裝置驗證和存取控制。</span><span class="sxs-lookup"><span data-stu-id="cafa2-121">[Device identities][lnk-device-identities] are used for device authentication and access control.</span></span>
* <span data-ttu-id="cafa2-122">**裝置對應項管理**。</span><span class="sxs-lookup"><span data-stu-id="cafa2-122">**Device twin management**.</span></span> <span data-ttu-id="cafa2-123">每個 IoT 中樞會公開一組服務向 HTTP 的 REST 端點 tooquery 和更新[裝置雙][ lnk-twins] （更新標記和屬性）。</span><span class="sxs-lookup"><span data-stu-id="cafa2-123">Each IoT hub exposes a set of service-facing HTTP REST endpoint tooquery and update [device twins][lnk-twins] (update tags and properties).</span></span>
* <span data-ttu-id="cafa2-124">**作業管理**。</span><span class="sxs-lookup"><span data-stu-id="cafa2-124">**Jobs management**.</span></span> <span data-ttu-id="cafa2-125">每個 IoT 中樞會公開一組服務向 HTTP 的 REST 端點 tooquery 和管理[作業][lnk-jobs]。</span><span class="sxs-lookup"><span data-stu-id="cafa2-125">Each IoT hub exposes a set of service-facing HTTP REST endpoint tooquery and manage [jobs][lnk-jobs].</span></span>
* <span data-ttu-id="cafa2-126">**裝置端點**。</span><span class="sxs-lookup"><span data-stu-id="cafa2-126">**Device endpoints**.</span></span> <span data-ttu-id="cafa2-127">Hello 身分識別登錄中的每個裝置 IoT 中樞會公開一組端點：</span><span class="sxs-lookup"><span data-stu-id="cafa2-127">For each device in hello identity registry, IoT Hub exposes a set of endpoints:</span></span>

  * <span data-ttu-id="cafa2-128">傳送裝置到雲端的訊息。</span><span class="sxs-lookup"><span data-stu-id="cafa2-128">*Send device-to-cloud messages*.</span></span> <span data-ttu-id="cafa2-129">裝置使用此端點太[傳送裝置到雲端訊息][lnk-d2c]。</span><span class="sxs-lookup"><span data-stu-id="cafa2-129">A device uses this endpoint too[send device-to-cloud messages][lnk-d2c].</span></span>
  * <span data-ttu-id="cafa2-130">接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="cafa2-130">*Receive cloud-to-device messages*.</span></span> <span data-ttu-id="cafa2-131">裝置使用此目標的端點 tooreceive[雲端到裝置訊息][lnk-c2d]。</span><span class="sxs-lookup"><span data-stu-id="cafa2-131">A device uses this endpoint tooreceive targeted [cloud-to-device messages][lnk-c2d].</span></span>
  * <span data-ttu-id="cafa2-132">*起始檔案上傳*。</span><span class="sxs-lookup"><span data-stu-id="cafa2-132">*Initiate file uploads*.</span></span> <span data-ttu-id="cafa2-133">裝置使用此端點 tooreceive 從 IoT 中樞是 Azure 儲存體 SAS URI 太[將檔案上傳][lnk-upload]。</span><span class="sxs-lookup"><span data-stu-id="cafa2-133">A device uses this endpoint tooreceive an Azure Storage SAS URI from IoT Hub too[upload a file][lnk-upload].</span></span>
  * <span data-ttu-id="cafa2-134">*擷取和更新裝置對應項的屬性*。</span><span class="sxs-lookup"><span data-stu-id="cafa2-134">*Retrieve and update device twin properties*.</span></span> <span data-ttu-id="cafa2-135">裝置使用此端點 tooaccess 其[裝置兩個][lnk-twins]的屬性。</span><span class="sxs-lookup"><span data-stu-id="cafa2-135">A device uses this endpoint tooaccess its [device twin][lnk-twins]'s properties.</span></span>
  * <span data-ttu-id="cafa2-136">*接收直接方法要求*。</span><span class="sxs-lookup"><span data-stu-id="cafa2-136">*Receive direct method requests*.</span></span> <span data-ttu-id="cafa2-137">裝置使用的這個端點 toolisten[直接方法][lnk-methods]的要求。</span><span class="sxs-lookup"><span data-stu-id="cafa2-137">A device uses this endpoint toolisten for [direct method][lnk-methods]'s requests.</span></span>

    <span data-ttu-id="cafa2-138">公開這些端點時，是使用 [MQTT v3.1.1][lnk-mqtt]、HTTP 1.1 及 [AMQP 1.0][lnk-amqp] 通訊協定來公開。</span><span class="sxs-lookup"><span data-stu-id="cafa2-138">These endpoints are exposed using [MQTT v3.1.1][lnk-mqtt], HTTP 1.1, and [AMQP 1.0][lnk-amqp] protocols.</span></span> <span data-ttu-id="cafa2-139">您也可以透過連接埠 443 上的 [WebSockets][lnk-websockets] 取得 AMQP。</span><span class="sxs-lookup"><span data-stu-id="cafa2-139">AMQP is also available over [WebSockets][lnk-websockets] on port 443.</span></span>

    <span data-ttu-id="cafa2-140">hello 裝置雙和方法可用的端點只有當您使用 hello 時[MQTT v3.1.1] [ lnk-mqtt]通訊協定。</span><span class="sxs-lookup"><span data-stu-id="cafa2-140">hello device twins and methods endpoints are available only when you use hello [MQTT v3.1.1][lnk-mqtt] protocol.</span></span>

* <span data-ttu-id="cafa2-141">**服務端點**。</span><span class="sxs-lookup"><span data-stu-id="cafa2-141">**Service endpoints**.</span></span> <span data-ttu-id="cafa2-142">每個 IoT 中樞以一組您方案的後端 toocommunicate 的端點來公開您的裝置。</span><span class="sxs-lookup"><span data-stu-id="cafa2-142">Each IoT hub exposes a set of endpoints  for your solution back end toocommunicate with your devices.</span></span> <span data-ttu-id="cafa2-143">有一個例外狀況，這些端點，才會顯示使用 hello [AMQP] [ lnk-amqp]通訊協定。</span><span class="sxs-lookup"><span data-stu-id="cafa2-143">With one exception, these endpoints are only exposed using hello [AMQP][lnk-amqp] protocol.</span></span> <span data-ttu-id="cafa2-144">hello 方法引動過程端點會公開透過 hello HTTP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="cafa2-144">hello method invocation endpoint is exposed over hello HTTP protocol.</span></span>
  
  * <span data-ttu-id="cafa2-145">*接收裝置到雲端的訊息*。</span><span class="sxs-lookup"><span data-stu-id="cafa2-145">*Receive device-to-cloud messages*.</span></span> <span data-ttu-id="cafa2-146">此端點與 [Azure 事件中樞][lnk-event-hubs]相容。</span><span class="sxs-lookup"><span data-stu-id="cafa2-146">This endpoint is compatible with [Azure Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="cafa2-147">後端服務可以使用它 tooread hello[裝置到雲端訊息][ lnk-d2c]您的裝置所傳送。</span><span class="sxs-lookup"><span data-stu-id="cafa2-147">A back-end service can use it tooread hello [device-to-cloud messages][lnk-d2c] sent by your devices.</span></span> <span data-ttu-id="cafa2-148">您可以建立 IoT 中樞上的自訂端點，加法 toothis 內建端點中。</span><span class="sxs-lookup"><span data-stu-id="cafa2-148">You can create custom endpoints on your IoT hub in addition toothis built-in endpoint.</span></span>
  * <span data-ttu-id="cafa2-149">*傳送雲端到裝置的訊息及接收傳遞通知*。</span><span class="sxs-lookup"><span data-stu-id="cafa2-149">*Send cloud-to-device messages and receive delivery acknowledgments*.</span></span> <span data-ttu-id="cafa2-150">這些端點啟用可靠您方案後端 toosend[雲端到裝置訊息][lnk-c2d]，和 tooreceive hello 對應傳遞或逾期的通知。</span><span class="sxs-lookup"><span data-stu-id="cafa2-150">These endpoints enable your solution back end toosend reliable [cloud-to-device messages][lnk-c2d], and tooreceive hello corresponding delivery or expiration acknowledgments.</span></span>
  * <span data-ttu-id="cafa2-151">*接收檔案通知*。</span><span class="sxs-lookup"><span data-stu-id="cafa2-151">*Receive file notifications*.</span></span> <span data-ttu-id="cafa2-152">此訊息的端點可讓您的 tooreceive 通知時您的裝置已成功上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="cafa2-152">This messaging endpoint allows you tooreceive notifications of when your devices successfully upload a file.</span></span> 
  * <span data-ttu-id="cafa2-153">*直接方法叫用*。</span><span class="sxs-lookup"><span data-stu-id="cafa2-153">*Direct method invocation*.</span></span> <span data-ttu-id="cafa2-154">此端點可讓後端服務 tooinvoke[直接方法][ lnk-methods]在裝置上。</span><span class="sxs-lookup"><span data-stu-id="cafa2-154">This endpoint allows a back-end service tooinvoke a [direct method][lnk-methods] on a device.</span></span>
  * <span data-ttu-id="cafa2-155">*接收作業監視事件*。</span><span class="sxs-lookup"><span data-stu-id="cafa2-155">*Receive operations monitoring events*.</span></span> <span data-ttu-id="cafa2-156">此端點可讓您監視的事件，如果您的 IoT 中樞已設定 tooemit tooreceive 作業它們。</span><span class="sxs-lookup"><span data-stu-id="cafa2-156">This endpoint allows you tooreceive operations monitoring events if your IoT hub has been configured tooemit them.</span></span> <span data-ttu-id="cafa2-157">如需詳細資訊，請參閱 [IoT 中樞作業監視][lnk-operations-mon]。</span><span class="sxs-lookup"><span data-stu-id="cafa2-157">For more information, see [IoT Hub operations monitoring][lnk-operations-mon].</span></span>

<span data-ttu-id="cafa2-158">hello [Azure IoT Sdk] [ lnk-sdks]文章說明 hello 各種方式 tooaccess 這些端點。</span><span class="sxs-lookup"><span data-stu-id="cafa2-158">hello [Azure IoT SDKs][lnk-sdks] article describes hello various ways tooaccess these endpoints.</span></span>

<span data-ttu-id="cafa2-159">所有的 IoT 中樞端點使用 hello [TLS] [ lnk-tls]未加密/不安全的通道上的通訊協定，以及任何端點曾公開。</span><span class="sxs-lookup"><span data-stu-id="cafa2-159">All IoT Hub endpoints use hello [TLS][lnk-tls] protocol, and no endpoint is ever exposed on unencrypted/unsecured channels.</span></span>

## <a name="custom-endpoints"></a><span data-ttu-id="cafa2-160">自訂端點</span><span class="sxs-lookup"><span data-stu-id="cafa2-160">Custom endpoints</span></span>

<span data-ttu-id="cafa2-161">為訊息路由的端點，您可以在訂用帳戶 tooyour IoT 中樞 tooact 連結現有的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="cafa2-161">You can link existing Azure services in your subscription tooyour IoT hub tooact as endpoints for message routing.</span></span> <span data-ttu-id="cafa2-162">這些端點可做為服務端點，並當作訊息路由的接收器。</span><span class="sxs-lookup"><span data-stu-id="cafa2-162">These endpoints act as service endpoints and are used as sinks for message routes.</span></span> <span data-ttu-id="cafa2-163">裝置無法直接寫入 toohello 其他端點。</span><span class="sxs-lookup"><span data-stu-id="cafa2-163">Devices cannot write directly toohello additional endpoints.</span></span> <span data-ttu-id="cafa2-164">toolearn 進一步了解訊息路由，請參閱 hello 開發人員指南項目上[傳送和接收訊息與 IoT 中樞][lnk-devguide-messaging]。</span><span class="sxs-lookup"><span data-stu-id="cafa2-164">toolearn more about message routes, see hello developer guide entry on [sending and receiving messages with IoT hub][lnk-devguide-messaging].</span></span>

<span data-ttu-id="cafa2-165">IoT 中樞目前支援下列其他端點的 Azure 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="cafa2-165">IoT Hub currently supports hello following Azure services as additional endpoints:</span></span>

* <span data-ttu-id="cafa2-166">事件中樞</span><span class="sxs-lookup"><span data-stu-id="cafa2-166">Event Hubs</span></span>
* <span data-ttu-id="cafa2-167">服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="cafa2-167">Service Bus Queues</span></span>
* <span data-ttu-id="cafa2-168">服務匯流排主題</span><span class="sxs-lookup"><span data-stu-id="cafa2-168">Service Bus Topics</span></span>

<span data-ttu-id="cafa2-169">IoT 中樞的訊息路由 toowork 需要寫入權限 toothese 服務端點。</span><span class="sxs-lookup"><span data-stu-id="cafa2-169">IoT Hub needs write access toothese service endpoints for message routing toowork.</span></span> <span data-ttu-id="cafa2-170">如果您設定透過 hello Azure 入口網站端點，則會為您加入 hello 必要的權限。</span><span class="sxs-lookup"><span data-stu-id="cafa2-170">If you configure your endpoints through hello Azure portal, hello necessary permissions are added for you.</span></span> <span data-ttu-id="cafa2-171">請確定您設定您的服務 toosupport hello 預期輸送量。</span><span class="sxs-lookup"><span data-stu-id="cafa2-171">Make sure you configure your services toosupport hello expected throughput.</span></span> <span data-ttu-id="cafa2-172">當您第一次設定您的 IoT 解決方案時，您可能需要 toomonitor 其他端點，並進行必要的調整 hello 實際負載。</span><span class="sxs-lookup"><span data-stu-id="cafa2-172">When you first configure your IoT solution, you may need toomonitor your additional endpoints and make any necessary adjustments for hello actual load.</span></span>

<span data-ttu-id="cafa2-173">如果訊息符合多個路由所有點 toohello 相同的端點，IoT 中樞將傳遞訊息 toothat 端點只有一次。</span><span class="sxs-lookup"><span data-stu-id="cafa2-173">If a message matches multiple routes that all point toohello same endpoint, IoT Hub delivers message toothat endpoint only once.</span></span> <span data-ttu-id="cafa2-174">因此，您不需要 tooconfigure 重複資料刪除服務匯流排佇列或主題上。</span><span class="sxs-lookup"><span data-stu-id="cafa2-174">Therefore, you do not need tooconfigure deduplication on your Service Bus queue or topic.</span></span> <span data-ttu-id="cafa2-175">在分割佇列中，分割區同質性可保證訊息排序。</span><span class="sxs-lookup"><span data-stu-id="cafa2-175">In partitioned queues, partition affinity guarantees message ordering.</span></span>

> [!NOTE]
> <span data-ttu-id="cafa2-176">做為 IoT 中樞端點的服務匯流排佇列和主題不能啟用 [工作階段] 或 [重複偵測]。</span><span class="sxs-lookup"><span data-stu-id="cafa2-176">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="cafa2-177">如果這些選項的其中一個已啟用，以顯示 hello 端點**連線**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="cafa2-177">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

<span data-ttu-id="cafa2-178">Hello hello 可以新增的端點數目的限制，請參閱[配額和節流][lnk-devguide-quotas]。</span><span class="sxs-lookup"><span data-stu-id="cafa2-178">For hello limits on hello number of endpoints you can add, see [Quotas and throttling][lnk-devguide-quotas].</span></span>

## <a name="field-gateways"></a><span data-ttu-id="cafa2-179">現場閘道器</span><span class="sxs-lookup"><span data-stu-id="cafa2-179">Field gateways</span></span>

<span data-ttu-id="cafa2-180">在 IoT 解決方案中， *現場閘道*位於裝置和 IoT 中樞端點之間。</span><span class="sxs-lookup"><span data-stu-id="cafa2-180">In an IoT solution, a *field gateway* sits between your devices and your IoT Hub endpoints.</span></span> <span data-ttu-id="cafa2-181">它是通常位於關閉 tooyour 裝置。</span><span class="sxs-lookup"><span data-stu-id="cafa2-181">It is typically located close tooyour devices.</span></span> <span data-ttu-id="cafa2-182">您的裝置直接與 hello 欄位閘道使用通訊 hello 裝置所支援的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="cafa2-182">Your devices communicate directly with hello field gateway by using a protocol supported by hello devices.</span></span> <span data-ttu-id="cafa2-183">hello 欄位閘道正在連接 tooan IoT 中樞端點使用通訊協定所支援的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="cafa2-183">hello field gateway connects tooan IoT Hub endpoint using a protocol that is supported by IoT Hub.</span></span> <span data-ttu-id="cafa2-184">現場閘道可能是專用的硬體裝置或是執行自訂閘道軟體的低功率電腦。</span><span class="sxs-lookup"><span data-stu-id="cafa2-184">A field gateway might be a dedicated hardware device or a low-power computer running custom gateway software.</span></span>

<span data-ttu-id="cafa2-185">您可以使用[Azure IoT 邊緣][ lnk-iot-edge] tooimplement 欄位閘道。</span><span class="sxs-lookup"><span data-stu-id="cafa2-185">You can use [Azure IoT Edge][lnk-iot-edge] tooimplement a field gateway.</span></span> <span data-ttu-id="cafa2-186">IoT 邊緣提供功能，例如來自 hello 到多個裝置的通訊多工作業相同的 IoT 中樞連線。</span><span class="sxs-lookup"><span data-stu-id="cafa2-186">IoT Edge offers functionality such as multiplexing communications from multiple devices onto hello same IoT Hub connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cafa2-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cafa2-187">Next steps</span></span>

<span data-ttu-id="cafa2-188">此 IoT 中樞開發人員指南中的其他參考主題包括︰</span><span class="sxs-lookup"><span data-stu-id="cafa2-188">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="cafa2-189">[裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="cafa2-189">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="cafa2-190">[配額和節流][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="cafa2-190">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="cafa2-191">[IoT 中樞的 MQTT 支援][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="cafa2-191">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
