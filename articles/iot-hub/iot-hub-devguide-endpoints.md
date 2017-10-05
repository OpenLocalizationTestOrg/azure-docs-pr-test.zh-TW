---
title: "了解 Azure IoT 中樞端點 | Microsoft Docs"
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
ms.openlocfilehash: 93ada731fe70cf7d294537241f8104c0b89940ed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="reference---iot-hub-endpoints"></a><span data-ttu-id="03e44-103">參考 - IoT 中樞端點</span><span class="sxs-lookup"><span data-stu-id="03e44-103">Reference - IoT Hub endpoints</span></span>

## <a name="iot-hub-names"></a><span data-ttu-id="03e44-104">IoT 中樞名稱</span><span class="sxs-lookup"><span data-stu-id="03e44-104">IoT Hub names</span></span>

<span data-ttu-id="03e44-105">您可以在入口網站的 [概觀] 刀鋒視窗上，找到端點裝載所在的 IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="03e44-105">You can find the name of the IoT hub that hosts your endpoints in the portal on the **Overview** blade.</span></span> <span data-ttu-id="03e44-106">根據預設，IoT 中樞的 DNS 名稱看起來像：`{your iot hub name}.azure-devices.net`。</span><span class="sxs-lookup"><span data-stu-id="03e44-106">By default, the DNS name of an IoT hub looks like: `{your iot hub name}.azure-devices.net`.</span></span>

<span data-ttu-id="03e44-107">您可以使用 Azure DNS 來建立 IoT 中樞的自訂 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="03e44-107">You can use Azure DNS to create a custom DNS name for your IoT hub.</span></span> <span data-ttu-id="03e44-108">如需詳細資訊，請參閱[使用 Azure DNS 為 Azure 服務提供自訂網域設定](../dns/dns-custom-domain.md#azure-iot)。</span><span class="sxs-lookup"><span data-stu-id="03e44-108">For more information, see [Use Azure DNS to provide custom domain settings for an Azure service](../dns/dns-custom-domain.md#azure-iot).</span></span>

## <a name="list-of-built-in-iot-hub-endpoints"></a><span data-ttu-id="03e44-109">內建 IoT 中樞端點清單</span><span class="sxs-lookup"><span data-stu-id="03e44-109">List of built-in IoT Hub endpoints</span></span>

<span data-ttu-id="03e44-110">Azure IoT 中樞是一項多租用戶服務，可將其功能公開給各種動作項目。</span><span class="sxs-lookup"><span data-stu-id="03e44-110">Azure IoT Hub is a multi-tenant service that exposes its functionality to various actors.</span></span> <span data-ttu-id="03e44-111">下圖顯示 IoT 中樞公開的各種端點。</span><span class="sxs-lookup"><span data-stu-id="03e44-111">The following diagram shows the various endpoints that IoT Hub exposes.</span></span>

![IoT 中樞端點][img-endpoints]

<span data-ttu-id="03e44-113">下列清單說明這些端點：</span><span class="sxs-lookup"><span data-stu-id="03e44-113">The following list describes the endpoints:</span></span>

* <span data-ttu-id="03e44-114">**資源提供者**。</span><span class="sxs-lookup"><span data-stu-id="03e44-114">**Resource provider**.</span></span> <span data-ttu-id="03e44-115">IoT 中樞資源提供者會公開 [Azure Resource Manager][lnk-arm] 介面。</span><span class="sxs-lookup"><span data-stu-id="03e44-115">The IoT Hub resource provider exposes an [Azure Resource Manager][lnk-arm] interface.</span></span> <span data-ttu-id="03e44-116">此介面可讓 Azure 訂用帳戶擁有者建立和刪除 IoT 中樞，以及更新 IoT 中樞屬性。</span><span class="sxs-lookup"><span data-stu-id="03e44-116">This interface enables Azure subscription owners to create and delete IoT hubs, and to update IoT hub properties.</span></span> <span data-ttu-id="03e44-117">IoT 中樞屬性用來管理[中樞層級的安全性原則][lnk-accesscontrol] (相對於裝置層級的存取控制) 和雲端到裝置與裝置到雲端傳訊的功能選項。</span><span class="sxs-lookup"><span data-stu-id="03e44-117">IoT Hub properties govern [hub-level security policies][lnk-accesscontrol], as opposed to device-level access control, and functional options for cloud-to-device and device-to-cloud messaging.</span></span> <span data-ttu-id="03e44-118">IoT 中樞資源提供者也可讓您[匯出裝置身分識別][lnk-importexport]。</span><span class="sxs-lookup"><span data-stu-id="03e44-118">The IoT Hub resource provider also enables you to [export device identities][lnk-importexport].</span></span>
* <span data-ttu-id="03e44-119">**裝置身分識別管理**。</span><span class="sxs-lookup"><span data-stu-id="03e44-119">**Device identity management**.</span></span> <span data-ttu-id="03e44-120">每個 IoT 中樞都會公開一組用來管理裝置身分識別的 HTTP REST 端點 (建立、擷取、更新和刪除)。</span><span class="sxs-lookup"><span data-stu-id="03e44-120">Each IoT hub exposes a set of HTTP REST endpoints to manage device identities (create, retrieve, update, and delete).</span></span> <span data-ttu-id="03e44-121">[裝置身分識別][lnk-device-identities]用於裝置驗證和存取控制。</span><span class="sxs-lookup"><span data-stu-id="03e44-121">[Device identities][lnk-device-identities] are used for device authentication and access control.</span></span>
* <span data-ttu-id="03e44-122">**裝置對應項管理**。</span><span class="sxs-lookup"><span data-stu-id="03e44-122">**Device twin management**.</span></span> <span data-ttu-id="03e44-123">每個 IoT 中樞會公開一組服務面向的 HTTP REST 端點，以查詢和更新[裝置對應項][lnk-twins] (更新標籤和屬性)。</span><span class="sxs-lookup"><span data-stu-id="03e44-123">Each IoT hub exposes a set of service-facing HTTP REST endpoint to query and update [device twins][lnk-twins] (update tags and properties).</span></span>
* <span data-ttu-id="03e44-124">**作業管理**。</span><span class="sxs-lookup"><span data-stu-id="03e44-124">**Jobs management**.</span></span> <span data-ttu-id="03e44-125">每個 IoT 中樞會公開一組服務面向的 HTTP REST 端點，以查詢和管理[作業][lnk-jobs]。</span><span class="sxs-lookup"><span data-stu-id="03e44-125">Each IoT hub exposes a set of service-facing HTTP REST endpoint to query and manage [jobs][lnk-jobs].</span></span>
* <span data-ttu-id="03e44-126">**裝置端點**。</span><span class="sxs-lookup"><span data-stu-id="03e44-126">**Device endpoints**.</span></span> <span data-ttu-id="03e44-127">針對身分識別登錄中的每個裝置，IoT 中樞會公開一組端點：</span><span class="sxs-lookup"><span data-stu-id="03e44-127">For each device in the identity registry, IoT Hub exposes a set of endpoints:</span></span>

  * <span data-ttu-id="03e44-128">傳送裝置到雲端的訊息。</span><span class="sxs-lookup"><span data-stu-id="03e44-128">*Send device-to-cloud messages*.</span></span> <span data-ttu-id="03e44-129">裝置會使用這個端點來[傳送裝置到雲端的訊息][lnk-d2c]。</span><span class="sxs-lookup"><span data-stu-id="03e44-129">A device uses this endpoint to [send device-to-cloud messages][lnk-d2c].</span></span>
  * <span data-ttu-id="03e44-130">接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="03e44-130">*Receive cloud-to-device messages*.</span></span> <span data-ttu-id="03e44-131">使用此端點來接收目標[雲端到裝置訊息][lnk-c2d]的裝置。</span><span class="sxs-lookup"><span data-stu-id="03e44-131">A device uses this endpoint to receive targeted [cloud-to-device messages][lnk-c2d].</span></span>
  * <span data-ttu-id="03e44-132">*起始檔案上傳*。</span><span class="sxs-lookup"><span data-stu-id="03e44-132">*Initiate file uploads*.</span></span> <span data-ttu-id="03e44-133">裝置會使用這個端點從 IoT 中樞接收 Azure 儲存體 SAS URI，以[上傳檔案][lnk-upload]。</span><span class="sxs-lookup"><span data-stu-id="03e44-133">A device uses this endpoint to receive an Azure Storage SAS URI from IoT Hub to [upload a file][lnk-upload].</span></span>
  * <span data-ttu-id="03e44-134">*擷取和更新裝置對應項的屬性*。</span><span class="sxs-lookup"><span data-stu-id="03e44-134">*Retrieve and update device twin properties*.</span></span> <span data-ttu-id="03e44-135">裝置使用此端點來存取其[裝置對應項][lnk-twins]的屬性。</span><span class="sxs-lookup"><span data-stu-id="03e44-135">A device uses this endpoint to access its [device twin][lnk-twins]'s properties.</span></span>
  * <span data-ttu-id="03e44-136">*接收直接方法要求*。</span><span class="sxs-lookup"><span data-stu-id="03e44-136">*Receive direct method requests*.</span></span> <span data-ttu-id="03e44-137">裝置使用此端點來接聽[直接方法][lnk-methods]的要求。</span><span class="sxs-lookup"><span data-stu-id="03e44-137">A device uses this endpoint to listen for [direct method][lnk-methods]'s requests.</span></span>

    <span data-ttu-id="03e44-138">公開這些端點時，是使用 [MQTT v3.1.1][lnk-mqtt]、HTTP 1.1 及 [AMQP 1.0][lnk-amqp] 通訊協定來公開。</span><span class="sxs-lookup"><span data-stu-id="03e44-138">These endpoints are exposed using [MQTT v3.1.1][lnk-mqtt], HTTP 1.1, and [AMQP 1.0][lnk-amqp] protocols.</span></span> <span data-ttu-id="03e44-139">您也可以透過連接埠 443 上的 [WebSockets][lnk-websockets] 取得 AMQP。</span><span class="sxs-lookup"><span data-stu-id="03e44-139">AMQP is also available over [WebSockets][lnk-websockets] on port 443.</span></span>

    <span data-ttu-id="03e44-140">裝置對應項端點和方法端點只能在使用 [MQTT v3.1.1][lnk-mqtt] 通訊協定時取得。</span><span class="sxs-lookup"><span data-stu-id="03e44-140">The device twins and methods endpoints are available only when you use the [MQTT v3.1.1][lnk-mqtt] protocol.</span></span>

* <span data-ttu-id="03e44-141">**服務端點**。</span><span class="sxs-lookup"><span data-stu-id="03e44-141">**Service endpoints**.</span></span> <span data-ttu-id="03e44-142">每個 IoT 中樞都會公開一組端點，供您的解決方案後端用來與您的裝置通訊。</span><span class="sxs-lookup"><span data-stu-id="03e44-142">Each IoT hub exposes a set of endpoints  for your solution back end to communicate with your devices.</span></span> <span data-ttu-id="03e44-143">但有一個例外狀況，這些端點只會在使用 [AMQP][lnk-amqp] 通訊協定時公開。</span><span class="sxs-lookup"><span data-stu-id="03e44-143">With one exception, these endpoints are only exposed using the [AMQP][lnk-amqp] protocol.</span></span> <span data-ttu-id="03e44-144">方法引動過程端點會透過 HTTP 通訊協定來公開。</span><span class="sxs-lookup"><span data-stu-id="03e44-144">The method invocation endpoint is exposed over the HTTP protocol.</span></span>
  
  * <span data-ttu-id="03e44-145">*接收裝置到雲端的訊息*。</span><span class="sxs-lookup"><span data-stu-id="03e44-145">*Receive device-to-cloud messages*.</span></span> <span data-ttu-id="03e44-146">此端點與 [Azure 事件中樞][lnk-event-hubs]相容。</span><span class="sxs-lookup"><span data-stu-id="03e44-146">This endpoint is compatible with [Azure Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="03e44-147">後端服務可用它來讀取由您的裝置所傳送的[裝置到雲端訊息][lnk-d2c]。</span><span class="sxs-lookup"><span data-stu-id="03e44-147">A back-end service can use it to read the [device-to-cloud messages][lnk-d2c] sent by your devices.</span></span> <span data-ttu-id="03e44-148">除了這個內建端點外，您可以在 IoT 中樞上建立自訂端點。</span><span class="sxs-lookup"><span data-stu-id="03e44-148">You can create custom endpoints on your IoT hub in addition to this built-in endpoint.</span></span>
  * <span data-ttu-id="03e44-149">*傳送雲端到裝置的訊息及接收傳遞通知*。</span><span class="sxs-lookup"><span data-stu-id="03e44-149">*Send cloud-to-device messages and receive delivery acknowledgments*.</span></span> <span data-ttu-id="03e44-150">這些端點可讓您的解決方案後端傳送可靠的[雲端到裝置訊息][lnk-c2d]，以及接收相對應的傳遞或到期通知。</span><span class="sxs-lookup"><span data-stu-id="03e44-150">These endpoints enable your solution back end to send reliable [cloud-to-device messages][lnk-c2d], and to receive the corresponding delivery or expiration acknowledgments.</span></span>
  * <span data-ttu-id="03e44-151">*接收檔案通知*。</span><span class="sxs-lookup"><span data-stu-id="03e44-151">*Receive file notifications*.</span></span> <span data-ttu-id="03e44-152">此訊息的端點可讓您接收您的裝置已成功上傳檔案的通知。</span><span class="sxs-lookup"><span data-stu-id="03e44-152">This messaging endpoint allows you to receive notifications of when your devices successfully upload a file.</span></span> 
  * <span data-ttu-id="03e44-153">*直接方法叫用*。</span><span class="sxs-lookup"><span data-stu-id="03e44-153">*Direct method invocation*.</span></span> <span data-ttu-id="03e44-154">此端點可讓後端服務在裝置上叫用[直接方法][lnk-methods]。</span><span class="sxs-lookup"><span data-stu-id="03e44-154">This endpoint allows a back-end service to invoke a [direct method][lnk-methods] on a device.</span></span>
  * <span data-ttu-id="03e44-155">*接收作業監視事件*。</span><span class="sxs-lookup"><span data-stu-id="03e44-155">*Receive operations monitoring events*.</span></span> <span data-ttu-id="03e44-156">如果已設定 IoT 中樞要發出接收作業監視事件，此端點可讓您這些事件。</span><span class="sxs-lookup"><span data-stu-id="03e44-156">This endpoint allows you to receive operations monitoring events if your IoT hub has been configured to emit them.</span></span> <span data-ttu-id="03e44-157">如需詳細資訊，請參閱 [IoT 中樞作業監視][lnk-operations-mon]。</span><span class="sxs-lookup"><span data-stu-id="03e44-157">For more information, see [IoT Hub operations monitoring][lnk-operations-mon].</span></span>

<span data-ttu-id="03e44-158">[Azure IoT SDK][lnk-sdks] 一文說明您可用來存取這些端點的各種方式。</span><span class="sxs-lookup"><span data-stu-id="03e44-158">The [Azure IoT SDKs][lnk-sdks] article describes the various ways to access these endpoints.</span></span>

<span data-ttu-id="03e44-159">所有的 IoT 中樞端點都使用 [TLS][lnk-tls] 通訊協定，且絕不會在未加密/不安全的通道上公開任何端點。</span><span class="sxs-lookup"><span data-stu-id="03e44-159">All IoT Hub endpoints use the [TLS][lnk-tls] protocol, and no endpoint is ever exposed on unencrypted/unsecured channels.</span></span>

## <a name="custom-endpoints"></a><span data-ttu-id="03e44-160">自訂端點</span><span class="sxs-lookup"><span data-stu-id="03e44-160">Custom endpoints</span></span>

<span data-ttu-id="03e44-161">您可以將訂用帳戶中的現有 Azure 服務連結至 IoT 中樞，以便做為訊息路由傳送的端點。</span><span class="sxs-lookup"><span data-stu-id="03e44-161">You can link existing Azure services in your subscription to your IoT hub to act as endpoints for message routing.</span></span> <span data-ttu-id="03e44-162">這些端點可做為服務端點，並當作訊息路由的接收器。</span><span class="sxs-lookup"><span data-stu-id="03e44-162">These endpoints act as service endpoints and are used as sinks for message routes.</span></span> <span data-ttu-id="03e44-163">裝置無法直接寫入至其他端點。</span><span class="sxs-lookup"><span data-stu-id="03e44-163">Devices cannot write directly to the additional endpoints.</span></span> <span data-ttu-id="03e44-164">若要深入了解訊息路由，請參閱[透過 IoT 中樞傳送和接收訊息][lnk-devguide-messaging]上的開發人員指南項目。</span><span class="sxs-lookup"><span data-stu-id="03e44-164">To learn more about message routes, see the developer guide entry on [sending and receiving messages with IoT hub][lnk-devguide-messaging].</span></span>

<span data-ttu-id="03e44-165">IoT 中樞目前支援下列 Azure 服務做為額外的端點︰</span><span class="sxs-lookup"><span data-stu-id="03e44-165">IoT Hub currently supports the following Azure services as additional endpoints:</span></span>

* <span data-ttu-id="03e44-166">事件中樞</span><span class="sxs-lookup"><span data-stu-id="03e44-166">Event Hubs</span></span>
* <span data-ttu-id="03e44-167">服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="03e44-167">Service Bus Queues</span></span>
* <span data-ttu-id="03e44-168">服務匯流排主題</span><span class="sxs-lookup"><span data-stu-id="03e44-168">Service Bus Topics</span></span>

<span data-ttu-id="03e44-169">IoT 中樞需要這些服務端點的寫入權限，才能將訊息路由傳送至工作。</span><span class="sxs-lookup"><span data-stu-id="03e44-169">IoT Hub needs write access to these service endpoints for message routing to work.</span></span> <span data-ttu-id="03e44-170">如果您透過 Azure 入口網站設定您的端點，則會為您新增必要的權限。</span><span class="sxs-lookup"><span data-stu-id="03e44-170">If you configure your endpoints through the Azure portal, the necessary permissions are added for you.</span></span> <span data-ttu-id="03e44-171">請務必設定您的服務，以支援預期的輸送量。</span><span class="sxs-lookup"><span data-stu-id="03e44-171">Make sure you configure your services to support the expected throughput.</span></span> <span data-ttu-id="03e44-172">當您第一次設定您的 IoT 解決方案時，您可能需要監視其他端點，然後對實際負載進行必要的調整。</span><span class="sxs-lookup"><span data-stu-id="03e44-172">When you first configure your IoT solution, you may need to monitor your additional endpoints and make any necessary adjustments for the actual load.</span></span>

<span data-ttu-id="03e44-173">如果訊息符合多個指向相同端點的路由，則 IoT 中樞只會將訊息傳遞至該端點一次。</span><span class="sxs-lookup"><span data-stu-id="03e44-173">If a message matches multiple routes that all point to the same endpoint, IoT Hub delivers message to that endpoint only once.</span></span> <span data-ttu-id="03e44-174">因此，您不需要在您的服務匯流排佇列或主題上設定重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="03e44-174">Therefore, you do not need to configure deduplication on your Service Bus queue or topic.</span></span> <span data-ttu-id="03e44-175">在分割佇列中，分割區同質性可保證訊息排序。</span><span class="sxs-lookup"><span data-stu-id="03e44-175">In partitioned queues, partition affinity guarantees message ordering.</span></span>

> [!NOTE]
> <span data-ttu-id="03e44-176">做為 IoT 中樞端點的服務匯流排佇列和主題不能啟用 [工作階段] 或 [重複偵測]。</span><span class="sxs-lookup"><span data-stu-id="03e44-176">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="03e44-177">如果已啟用其中一個選項，端點會在 Azure 入口網站中顯示為 [無法連線]。</span><span class="sxs-lookup"><span data-stu-id="03e44-177">If either of those options are enabled, the endpoint appears as **Unreachable** in the Azure portal.</span></span>

<span data-ttu-id="03e44-178">如需您可以新增的端點數目限制，請參閱[配額和節流][lnk-devguide-quotas]。</span><span class="sxs-lookup"><span data-stu-id="03e44-178">For the limits on the number of endpoints you can add, see [Quotas and throttling][lnk-devguide-quotas].</span></span>

## <a name="field-gateways"></a><span data-ttu-id="03e44-179">現場閘道器</span><span class="sxs-lookup"><span data-stu-id="03e44-179">Field gateways</span></span>

<span data-ttu-id="03e44-180">在 IoT 解決方案中， *現場閘道*位於裝置和 IoT 中樞端點之間。</span><span class="sxs-lookup"><span data-stu-id="03e44-180">In an IoT solution, a *field gateway* sits between your devices and your IoT Hub endpoints.</span></span> <span data-ttu-id="03e44-181">它通常位於接近您的裝置的位置。</span><span class="sxs-lookup"><span data-stu-id="03e44-181">It is typically located close to your devices.</span></span> <span data-ttu-id="03e44-182">您的裝置會使用裝置所支援的通訊協定，直接與現場閘道器通訊。</span><span class="sxs-lookup"><span data-stu-id="03e44-182">Your devices communicate directly with the field gateway by using a protocol supported by the devices.</span></span> <span data-ttu-id="03e44-183">現場閘道會使用 IoT 中樞所支援的通訊協定來連線到 IoT 中樞端點。</span><span class="sxs-lookup"><span data-stu-id="03e44-183">The field gateway connects to an IoT Hub endpoint using a protocol that is supported by IoT Hub.</span></span> <span data-ttu-id="03e44-184">現場閘道可能是專用的硬體裝置或是執行自訂閘道軟體的低功率電腦。</span><span class="sxs-lookup"><span data-stu-id="03e44-184">A field gateway might be a dedicated hardware device or a low-power computer running custom gateway software.</span></span>

<span data-ttu-id="03e44-185">您可以使用 [Azure IoT Edge][lnk-iot-edge] 來實作現場閘道。</span><span class="sxs-lookup"><span data-stu-id="03e44-185">You can use [Azure IoT Edge][lnk-iot-edge] to implement a field gateway.</span></span> <span data-ttu-id="03e44-186">IoT Edge 提供某些功能，例如對從多個裝置到相同 IoT 中樞連線的通訊進行多工處理。</span><span class="sxs-lookup"><span data-stu-id="03e44-186">IoT Edge offers functionality such as multiplexing communications from multiple devices onto the same IoT Hub connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03e44-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03e44-187">Next steps</span></span>

<span data-ttu-id="03e44-188">此 IoT 中樞開發人員指南中的其他參考主題包括︰</span><span class="sxs-lookup"><span data-stu-id="03e44-188">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="03e44-189">[裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="03e44-189">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="03e44-190">[配額和節流][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="03e44-190">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="03e44-191">[IoT 中樞的 MQTT 支援][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="03e44-191">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
