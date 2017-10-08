---
title: "Azure IoT 中樞安全性 aaaUnderstand |Microsoft 文件"
description: "開發人員指南-toocontrol 存取 tooIoT 中樞裝置應用程式和後端應用程式的方式。 包含安全性權杖和 X.509 憑證支援的相關資訊。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a><span data-ttu-id="f2135-104">控制存取 tooIoT 中樞</span><span class="sxs-lookup"><span data-stu-id="f2135-104">Control access tooIoT Hub</span></span>

<span data-ttu-id="f2135-105">本文說明 hello 選項來保護您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f2135-105">This article describes hello options for securing your IoT hub.</span></span> <span data-ttu-id="f2135-106">IoT 中樞用*權限*toogrant 存取 tooeach IoT 中心端點。</span><span class="sxs-lookup"><span data-stu-id="f2135-106">IoT Hub uses *permissions* toogrant access tooeach IoT hub endpoint.</span></span> <span data-ttu-id="f2135-107">權限限制根據功能 hello 存取 tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f2135-107">Permissions limit hello access tooan IoT hub based on functionality.</span></span>

<span data-ttu-id="f2135-108">本文章說明：</span><span class="sxs-lookup"><span data-stu-id="f2135-108">This article describes:</span></span>

* <span data-ttu-id="f2135-109">您可以授與 tooa 裝置或後端應用程式 tooaccess IoT 中樞 hello 不同權限。</span><span class="sxs-lookup"><span data-stu-id="f2135-109">hello different permissions that you can grant tooa device or back-end app tooaccess your IoT hub.</span></span>
* <span data-ttu-id="f2135-110">hello 驗證程序和 hello token，它會使用 tooverify 權限。</span><span class="sxs-lookup"><span data-stu-id="f2135-110">hello authentication process and hello tokens it uses tooverify permissions.</span></span>
* <span data-ttu-id="f2135-111">如何 tooscope 認證 toolimit 存取 toospecific 資源。</span><span class="sxs-lookup"><span data-stu-id="f2135-111">How tooscope credentials toolimit access toospecific resources.</span></span>
* <span data-ttu-id="f2135-112">IoT 中樞支援 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="f2135-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="f2135-113">使用現有的裝置身分識別登錄或驗證結構描述的自訂裝置驗證機制。</span><span class="sxs-lookup"><span data-stu-id="f2135-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="f2135-114">當 toouse</span><span class="sxs-lookup"><span data-stu-id="f2135-114">When toouse</span></span>

<span data-ttu-id="f2135-115">您必須具備適當的權限 tooaccess hello IoT 中樞端點。</span><span class="sxs-lookup"><span data-stu-id="f2135-115">You must have appropriate permissions tooaccess any of hello IoT Hub endpoints.</span></span> <span data-ttu-id="f2135-116">例如，裝置必須包括包含安全性認證，以及傳送 tooIoT 中樞的每個訊息的權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-116">For example, a device must include a token containing security credentials along with every message it sends tooIoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="f2135-117">存取控制及權限</span><span class="sxs-lookup"><span data-stu-id="f2135-117">Access control and permissions</span></span>

<span data-ttu-id="f2135-118">您可以授與[權限](#iot-hub-permissions)hello 遵循方法中：</span><span class="sxs-lookup"><span data-stu-id="f2135-118">You can grant [permissions](#iot-hub-permissions) in hello following ways:</span></span>

* <span data-ttu-id="f2135-119">**IoT 中樞層級的共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="f2135-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="f2135-120">共用存取原則可以授與上面所列[權限](#iot-hub-permissions)的任意組合。</span><span class="sxs-lookup"><span data-stu-id="f2135-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="f2135-121">您可以定義原則中 hello [Azure 入口網站][lnk-management-portal]，或以程式設計方式利用 hello [IoT 中樞資源提供者 REST Api][lnk-resource-provider-apis]。</span><span class="sxs-lookup"><span data-stu-id="f2135-121">You can define policies in hello [Azure portal][lnk-management-portal], or programmatically by using hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="f2135-122">新建立的 IoT 中樞有下列預設原則的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2135-122">A newly created IoT hub has hello following default policies:</span></span>

  * <span data-ttu-id="f2135-123">**iothubowner**︰具備所有權限的原則。</span><span class="sxs-lookup"><span data-stu-id="f2135-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="f2135-124">**service**︰具備 **ServiceConnect** 權限的原則。</span><span class="sxs-lookup"><span data-stu-id="f2135-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="f2135-125">**device**︰具備 **DeviceConnect** 權限的原則。</span><span class="sxs-lookup"><span data-stu-id="f2135-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="f2135-126">**registryRead**︰具備 **RegistryRead** 權限的原則。</span><span class="sxs-lookup"><span data-stu-id="f2135-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="f2135-127">**registryReadWrite**︰具備 **RegistryRead** 和 RegistryWrite 權限的原則。</span><span class="sxs-lookup"><span data-stu-id="f2135-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="f2135-128">**各裝置的安全性認證**。</span><span class="sxs-lookup"><span data-stu-id="f2135-128">**Per-device security credentials**.</span></span> <span data-ttu-id="f2135-129">每個 IoT 中樞都包含[身分識別登錄][lnk-identity-registry]。</span><span class="sxs-lookup"><span data-stu-id="f2135-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="f2135-130">對於這個身分識別登錄中的每個裝置，您可以設定授與的安全性認證**DeviceConnect**權限範圍 toohello 對應裝置的端點。</span><span class="sxs-lookup"><span data-stu-id="f2135-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped toohello corresponding device endpoints.</span></span>

<span data-ttu-id="f2135-131">例如，在典型的 IoT 解決方案中︰</span><span class="sxs-lookup"><span data-stu-id="f2135-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="f2135-132">hello 裝置管理元件會使用 hello *registryReadWrite*原則。</span><span class="sxs-lookup"><span data-stu-id="f2135-132">hello device management component uses hello *registryReadWrite* policy.</span></span>
* <span data-ttu-id="f2135-133">hello 事件處理器元件會使用 hello*服務*原則。</span><span class="sxs-lookup"><span data-stu-id="f2135-133">hello event processor component uses hello *service* policy.</span></span>
* <span data-ttu-id="f2135-134">hello 裝置執行階段商務邏輯元件會使用 hello*服務*原則。</span><span class="sxs-lookup"><span data-stu-id="f2135-134">hello run-time device business logic component uses hello *service* policy.</span></span>
* <span data-ttu-id="f2135-135">個別裝置使用 hello IoT 中樞的身分識別登錄中儲存的認證進行連接。</span><span class="sxs-lookup"><span data-stu-id="f2135-135">Individual devices connect using credentials stored in hello IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="f2135-136">如需詳細資訊，請參閱[權限](#iot-hub-permissions)。</span><span class="sxs-lookup"><span data-stu-id="f2135-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="f2135-137">驗證</span><span class="sxs-lookup"><span data-stu-id="f2135-137">Authentication</span></span>

<span data-ttu-id="f2135-138">Azure IoT 中樞中，會授與存取 tooendpoints 針對 hello 共用存取原則和身分識別登錄安全性認證的權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f2135-138">Azure IoT Hub grants access tooendpoints by verifying a token against hello shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="f2135-139">安全性認證，例如對稱金鑰，就不會傳送 hello 線上。</span><span class="sxs-lookup"><span data-stu-id="f2135-139">Security credentials, such as symmetric keys, are never sent over hello wire.</span></span>

> [!NOTE]
> <span data-ttu-id="f2135-140">hello Azure IoT 中樞資源提供者透過保護您 Azure 訂用帳戶，因為所有的提供者在 hello [Azure Resource Manager][lnk-azure-resource-manager]。</span><span class="sxs-lookup"><span data-stu-id="f2135-140">hello Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in hello [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="f2135-141">如需有關如何 tooconstruct 和使用的安全性權杖，請參閱[IoT 中樞安全性語彙基元][lnk-sas-tokens]。</span><span class="sxs-lookup"><span data-stu-id="f2135-141">For more information about how tooconstruct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="f2135-142">通訊協定詳細規格</span><span class="sxs-lookup"><span data-stu-id="f2135-142">Protocol specifics</span></span>

<span data-ttu-id="f2135-143">每個支援的通訊協定 (例如 MQTT、AMQP 及 HTTP) 會以不同的方式傳輸權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="f2135-144">Hello 連線封包時使用 MQTT，有 hello deviceId 如下 hello ClientId、 {iothubhostname} / {deviceId} hello 使用者名稱欄位和 SAS 權杖在 hello 密碼 欄位中。</span><span class="sxs-lookup"><span data-stu-id="f2135-144">When using MQTT, hello CONNECT packet has hello deviceId as hello ClientId, {iothubhostname}/{deviceId} in hello Username field, and a SAS token in hello Password field.</span></span> <span data-ttu-id="f2135-145">{iothubhostname} 應該 hello hello IoT 中樞 (例如，devices.net contoso.azure) 的完整 CName。</span><span class="sxs-lookup"><span data-stu-id="f2135-145">{iothubhostname} should be hello full CName of hello IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="f2135-146">使用 [AMQP][lnk-amqp] 時，IoT 中樞支援 [SASL PLAIN][lnk-sasl-plain] 和 [AMQP 宣告式安全性][lnk-cbs]。</span><span class="sxs-lookup"><span data-stu-id="f2135-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="f2135-147">如果您使用 AMQP 宣告為基礎的安全性、 hello 標準指定如何 tootransmit 這些語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f2135-147">If you use AMQP claims-based-security, hello standard specifies how tootransmit these tokens.</span></span>

<span data-ttu-id="f2135-148">如 SASL 純 hello **username**可以是：</span><span class="sxs-lookup"><span data-stu-id="f2135-148">For SASL PLAIN, hello **username** can be:</span></span>

* <span data-ttu-id="f2135-149">`{policyName}@sas.root.{iothubName}`，如果使用 IoT 中樞層級權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="f2135-150">`{deviceId}@sas.{iothubname}`，如果使用裝置範圍權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="f2135-151">在這兩種情況下，hello 密碼欄位包含 hello 語彙基元，如下所示[IoT 中樞安全性語彙基元][lnk-sas-tokens]。</span><span class="sxs-lookup"><span data-stu-id="f2135-151">In both cases, hello password field contains hello token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="f2135-152">HTTP 實作驗證有效的語彙基元併入 hello**授權**要求標頭。</span><span class="sxs-lookup"><span data-stu-id="f2135-152">HTTP implements authentication by including a valid token in hello **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="f2135-153">範例</span><span class="sxs-lookup"><span data-stu-id="f2135-153">Example</span></span>

<span data-ttu-id="f2135-154">使用者名稱 (DeviceId 區分大小寫)︰ `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="f2135-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="f2135-155">密碼 (產生 SAS 權杖，以 hello[裝置總管][ lnk-device-explorer]工具):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="f2135-155">Password (Generate SAS token with hello [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="f2135-156">hello [Azure IoT Sdk] [ lnk-sdks]連接 toohello 服務時，自動產生語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f2135-156">hello [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting toohello service.</span></span> <span data-ttu-id="f2135-157">在某些情況下，hello Azure IoT Sdk 不支援所有的 hello 通訊協定或 hello 的所有驗證方法。</span><span class="sxs-lookup"><span data-stu-id="f2135-157">In some cases, hello Azure IoT SDKs do not support all hello protocols or all hello authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="f2135-158">SASL PLAIN 的特殊考量</span><span class="sxs-lookup"><span data-stu-id="f2135-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="f2135-159">當使用 AMQP SASL 純，連線 tooan IoT 中樞的用戶端可以使用單一語彙基元為每個 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="f2135-159">When using SASL PLAIN with AMQP, a client connecting tooan IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="f2135-160">Hello 權杖過期時，hello TCP 連線從 hello 服務中斷連線再觸發重新連線。</span><span class="sxs-lookup"><span data-stu-id="f2135-160">When hello token expires, hello TCP connection disconnects from hello service and triggers a reconnect.</span></span> <span data-ttu-id="f2135-161">此行為，雖然後端應用程式中，不會有問題會造成損害裝置應用程式中的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="f2135-161">This behavior, while not problematic for a back-end app, is damaging for a device app for hello following reasons:</span></span>

* <span data-ttu-id="f2135-162">閘道器通常會代表許多裝置連線。</span><span class="sxs-lookup"><span data-stu-id="f2135-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="f2135-163">當使用 SASL 純，它們有 toocreate 不同的 TCP 連接的每個裝置連接 tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f2135-163">When using SASL PLAIN, they have toocreate a distinct TCP connection for each device connecting tooan IoT hub.</span></span> <span data-ttu-id="f2135-164">這種情況下大幅增加 hello 電源和網路功能的資源耗用量，而且增加每個裝置連接的 hello 延遲。</span><span class="sxs-lookup"><span data-stu-id="f2135-164">This scenario considerably increases hello consumption of power and networking resources, and increases hello latency of each device connection.</span></span>
* <span data-ttu-id="f2135-165">有限資源的裝置會受到負面影響資源 tooreconnect hello 增加使用每個權杖到期之後。</span><span class="sxs-lookup"><span data-stu-id="f2135-165">Resource-constrained devices are adversely affected by hello increased use of resources tooreconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="f2135-166">設定 IoT 中樞層級認證的範圍</span><span class="sxs-lookup"><span data-stu-id="f2135-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="f2135-167">使用受限制的資源 URI 建立權杖，可以設定 IoT 中樞層級安全性原則的範圍。</span><span class="sxs-lookup"><span data-stu-id="f2135-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="f2135-168">例如，從裝置 hello 端點 toosend 裝置到雲端訊息是**/devices/ {deviceId} / 訊息/事件**。</span><span class="sxs-lookup"><span data-stu-id="f2135-168">For example, hello endpoint toosend device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="f2135-169">您也可以使用具有的 IoT 中樞層級的共用的存取原則**DeviceConnect**權限 toosign 語彙基元是其 resourceURI **/devices/ {deviceId}**。</span><span class="sxs-lookup"><span data-stu-id="f2135-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions toosign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="f2135-170">這種方法建立的權杖，才可使用 toosend 訊息代表裝置**deviceId**。</span><span class="sxs-lookup"><span data-stu-id="f2135-170">This approach creates a token that is only usable toosend messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="f2135-171">這項機制是類似 toohello[事件中心發行者原則][lnk-event-hubs-publisher-policy]，並可讓您 tooimplement 自訂驗證方法。</span><span class="sxs-lookup"><span data-stu-id="f2135-171">This mechanism is similar toohello [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you tooimplement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="f2135-172">安全性權杖</span><span class="sxs-lookup"><span data-stu-id="f2135-172">Security tokens</span></span>

<span data-ttu-id="f2135-173">IoT 中樞使用的安全性語彙基元 tooauthenticate 裝置，而且服務 tooavoid 傳送 hello 網路上的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f2135-173">IoT Hub uses security tokens tooauthenticate devices and services tooavoid sending keys on hello wire.</span></span> <span data-ttu-id="f2135-174">此外，安全性權杖有時效性和範圍的限制。</span><span class="sxs-lookup"><span data-stu-id="f2135-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="f2135-175">[Azure IoT SDK][lnk-sdks] 能在不需要任何特殊組態的情況下自動產生權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="f2135-176">某些情況下需要您 toogenerate 作業，並直接使用安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-176">Some scenarios do require you toogenerate and use security tokens directly.</span></span> <span data-ttu-id="f2135-177">這類案例包括：</span><span class="sxs-lookup"><span data-stu-id="f2135-177">Such scenarios include:</span></span>

* <span data-ttu-id="f2135-178">hello MQTT、 AMQP 或 HTTP 介面的 hello 直接使用。</span><span class="sxs-lookup"><span data-stu-id="f2135-178">hello direct use of hello MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="f2135-179">hello hello 語彙基元服務模式，實作中所述[自訂裝置驗證][lnk-custom-auth]。</span><span class="sxs-lookup"><span data-stu-id="f2135-179">hello implementation of hello token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="f2135-180">IoT 中樞也可讓裝置 tooauthenticate 與 IoT 中樞使用[X.509 憑證][lnk-x509]。</span><span class="sxs-lookup"><span data-stu-id="f2135-180">IoT Hub also allows devices tooauthenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="f2135-181">安全性權杖結構</span><span class="sxs-lookup"><span data-stu-id="f2135-181">Security token structure</span></span>

<span data-ttu-id="f2135-182">您使用的安全性語彙基元 toogrant 時間界限存取 toodevices 和服務 toospecific 功能 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f2135-182">You use security tokens toogrant time-bounded access toodevices and services toospecific functionality in IoT Hub.</span></span> <span data-ttu-id="f2135-183">tooget 授權 tooconnect tooIoT 集線器、 裝置和服務必須傳送以共用的存取或對稱金鑰簽章的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-183">tooget authorization tooconnect tooIoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="f2135-184">這些金鑰存放在與 hello 身分識別登錄中的裝置識別身分。</span><span class="sxs-lookup"><span data-stu-id="f2135-184">These keys are stored with a device identity in hello identity registry.</span></span>

<span data-ttu-id="f2135-185">共用的存取金鑰授與存取 tooall hello 功能 hello 共用存取原則權限相關聯簽署權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-185">A token signed with a shared access key grants access tooall hello functionality associated with hello shared access policy permissions.</span></span> <span data-ttu-id="f2135-186">裝置識別身分的對稱金鑰只會授與 hello 簽署權杖**DeviceConnect** hello 的權限相關聯的裝置識別身分。</span><span class="sxs-lookup"><span data-stu-id="f2135-186">A token signed with a device identity's symmetric key only grants hello **DeviceConnect** permission for hello associated device identity.</span></span>

<span data-ttu-id="f2135-187">hello 安全性權杖具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2135-187">hello security token has hello following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="f2135-188">以下是 hello 預期值：</span><span class="sxs-lookup"><span data-stu-id="f2135-188">Here are hello expected values:</span></span>

| <span data-ttu-id="f2135-189">值</span><span class="sxs-lookup"><span data-stu-id="f2135-189">Value</span></span> | <span data-ttu-id="f2135-190">說明</span><span class="sxs-lookup"><span data-stu-id="f2135-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f2135-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="f2135-191">{signature}</span></span> |<span data-ttu-id="f2135-192">Hello 表單的 hmac-sha256 簽章字串： `{URL-encoded-resourceURI} + "\n" + expiry`。</span><span class="sxs-lookup"><span data-stu-id="f2135-192">An HMAC-SHA256 signature string of hello form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="f2135-193">**重要**: hello 金鑰從 base64 解碼，並做為索引鍵 tooperform hello hmac-sha256 計算。</span><span class="sxs-lookup"><span data-stu-id="f2135-193">**Important**: hello key is decoded from base64 and used as key tooperform hello HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="f2135-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="f2135-194">{resourceURI}</span></span> |<span data-ttu-id="f2135-195">URI 的前置詞 （依區段） 可以使用這個語彙基元開頭的 hello IoT 中樞 （沒有任何通訊協定） 的主機名稱來存取的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="f2135-195">URI prefix (by segment) of hello endpoints that can be accessed with this token, starting with host name of hello IoT hub (no protocol).</span></span> <span data-ttu-id="f2135-196">例如， `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="f2135-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="f2135-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="f2135-197">{expiry}</span></span> |<span data-ttu-id="f2135-198">UTF8 字串 hello epoch 00:00:00 UTC 在 1 年 1 月 1970年起的秒數。</span><span class="sxs-lookup"><span data-stu-id="f2135-198">UTF8 strings for number of seconds since hello epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="f2135-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="f2135-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="f2135-200">較低的大小寫 URL 編碼的 hello 小寫資源 URI</span><span class="sxs-lookup"><span data-stu-id="f2135-200">Lower case URL-encoding of hello lower case resource URI</span></span> |
| <span data-ttu-id="f2135-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="f2135-201">{policyName}</span></span> |<span data-ttu-id="f2135-202">這個語彙基元所參考的 hello 共用存取原則 toowhich hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="f2135-202">hello name of hello shared access policy toowhich this token refers.</span></span> <span data-ttu-id="f2135-203">若 hello 語彙基元是指 toodevice 登錄的認證。</span><span class="sxs-lookup"><span data-stu-id="f2135-203">Absent if hello token refers toodevice-registry credentials.</span></span> |

<span data-ttu-id="f2135-204">**請注意，前置詞**: hello URI 前置詞計算的區段，而不是由字元。</span><span class="sxs-lookup"><span data-stu-id="f2135-204">**Note on prefix**: hello URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="f2135-205">例如，`/a/b` 是 `/a/b/c` 的前置詞，而不是 `/a/bc` 的前置詞。</span><span class="sxs-lookup"><span data-stu-id="f2135-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="f2135-206">hello 下列 Node.js 的程式碼片段示範函式呼叫**generateSasToken**計算 hello hello 輸入中的語彙基元`resourceUri, signingKey, policyName, expiresInMins`。</span><span class="sxs-lookup"><span data-stu-id="f2135-206">hello following Node.js snippet shows a function called **generateSasToken** that computes hello token from hello inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="f2135-207">hello 下一節中詳細說明如何 tooinitialize hello 不同的輸入 hello 不同語彙基元的使用案例。</span><span class="sxs-lookup"><span data-stu-id="f2135-207">hello next sections detail how tooinitialize hello different inputs for hello different token use cases.</span></span>

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

<span data-ttu-id="f2135-208">比較結果為 hello 安全性語彙基元是相等的 Python 程式碼 toogenerate:</span><span class="sxs-lookup"><span data-stu-id="f2135-208">As a comparison, hello equivalent Python code toogenerate a security token is:</span></span>

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> <span data-ttu-id="f2135-209">IoT 中樞機器上驗證 hello hello 權杖的有效時間，因為 hello 漂移 hello 產生 hello 語彙基元的 hello 電腦時鐘必須是最小。</span><span class="sxs-lookup"><span data-stu-id="f2135-209">Since hello time validity of hello token is validated on IoT Hub machines, hello drift on hello clock of hello machine that generates hello token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="f2135-210">在裝置應用程式中使用 SAS 權杖</span><span class="sxs-lookup"><span data-stu-id="f2135-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="f2135-211">有兩種方式 tooobtain **DeviceConnect**與 IoT 中樞與安全性權杖的權限： 使用[hello 身分識別登錄中的對稱式裝置金鑰](#use-a-symmetric-key-in-the-identity-registry)，或使用[的共用的存取金鑰](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="f2135-211">There are two ways tooobtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from hello identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="f2135-212">請記住，所有可從裝置存取的功能，在設計上會於前置詞為 `/devices/{deviceId}`的端點公開。</span><span class="sxs-lookup"><span data-stu-id="f2135-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2135-213">hello IoT 中樞會驗證特定裝置的唯一方法使用 hello 裝置身分識別對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="f2135-213">hello only way that IoT Hub authenticates a specific device is using hello device identity symmetric key.</span></span> <span data-ttu-id="f2135-214">萬一共用的存取原則是使用的 tooaccess 裝置功能，當 hello 方案必須考慮 hello 元件發出 hello 做為受信任的子元件的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-214">In cases when a shared access policy is used tooaccess device functionality, hello solution must consider hello component issuing hello security token as a trusted subcomponent.</span></span>

<span data-ttu-id="f2135-215">hello 面對裝置的端點是 （不管 hello 通訊協定）：</span><span class="sxs-lookup"><span data-stu-id="f2135-215">hello device-facing endpoints are (irrespective of hello protocol):</span></span>

| <span data-ttu-id="f2135-216">端點</span><span class="sxs-lookup"><span data-stu-id="f2135-216">Endpoint</span></span> | <span data-ttu-id="f2135-217">功能</span><span class="sxs-lookup"><span data-stu-id="f2135-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="f2135-218">傳送裝置到雲端的訊息。</span><span class="sxs-lookup"><span data-stu-id="f2135-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="f2135-219">接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="f2135-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a><span data-ttu-id="f2135-220">在 hello 身分識別登錄中使用對稱金鑰</span><span class="sxs-lookup"><span data-stu-id="f2135-220">Use a symmetric key in hello identity registry</span></span>

<span data-ttu-id="f2135-221">當使用裝置身分識別對稱金鑰 toogenerate 語彙基元，hello policyName (`skn`) 省略 hello 語彙基元的元素。</span><span class="sxs-lookup"><span data-stu-id="f2135-221">When using a device identity's symmetric key toogenerate a token, hello policyName (`skn`) element of hello token is omitted.</span></span>

<span data-ttu-id="f2135-222">例如，語彙基元建立的 tooaccess 裝置的所有功能應擁有都 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="f2135-222">For example, a token created tooaccess all device functionality should have hello following parameters:</span></span>

* <span data-ttu-id="f2135-223">資源 URI： `{IoT hub name}.azure-devices.net/devices/{device id}`、</span><span class="sxs-lookup"><span data-stu-id="f2135-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="f2135-224">簽署金鑰： hello 任何對稱金鑰`{device id}`身分識別，</span><span class="sxs-lookup"><span data-stu-id="f2135-224">signing key: any symmetric key for hello `{device id}` identity,</span></span>
* <span data-ttu-id="f2135-225">無原則名稱、</span><span class="sxs-lookup"><span data-stu-id="f2135-225">no policy name,</span></span>
* <span data-ttu-id="f2135-226">任何到期時間。</span><span class="sxs-lookup"><span data-stu-id="f2135-226">any expiration time.</span></span>

<span data-ttu-id="f2135-227">會使用 hello 前面 Node.js 函式的範例：</span><span class="sxs-lookup"><span data-stu-id="f2135-227">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="f2135-228">hello 結果，這會授與存取 tooall device1 的功能，會是：</span><span class="sxs-lookup"><span data-stu-id="f2135-228">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="f2135-229">它是可能 toogenerate SAS 權杖使用 hello.NET[裝置總管][ lnk-device-explorer]工具或 hello 跨平台，節點基礎[iot 中樞總管][ lnk-iothub-explorer]命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="f2135-229">It is possible toogenerate a SAS token using hello .NET [device explorer][lnk-device-explorer] tool or hello cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="f2135-230">使用共用存取原則</span><span class="sxs-lookup"><span data-stu-id="f2135-230">Use a shared access policy</span></span>

<span data-ttu-id="f2135-231">當您建立語彙基元從共用的存取原則時，設定 hello`skn`欄位 toohello hello 原則名稱。</span><span class="sxs-lookup"><span data-stu-id="f2135-231">When you create a token from a shared access policy, set hello `skn` field toohello name of hello policy.</span></span> <span data-ttu-id="f2135-232">此原則必須授與 hello **DeviceConnect**權限。</span><span class="sxs-lookup"><span data-stu-id="f2135-232">This policy must grant hello **DeviceConnect** permission.</span></span>

<span data-ttu-id="f2135-233">hello 兩個主要案例使用共用的存取原則 tooaccess 裝置功能包括：</span><span class="sxs-lookup"><span data-stu-id="f2135-233">hello two main scenarios for using shared access policies tooaccess device functionality are:</span></span>

* <span data-ttu-id="f2135-234">[雲端通訊協定閘道][lnk-endpoints]、</span><span class="sxs-lookup"><span data-stu-id="f2135-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="f2135-235">[權杖服務][ lnk-custom-auth]用 tooimplement 自訂驗證配置。</span><span class="sxs-lookup"><span data-stu-id="f2135-235">[token services][lnk-custom-auth] used tooimplement custom authentication schemes.</span></span>

<span data-ttu-id="f2135-236">因為 hello 共用的存取原則可以可能授與存取 tooconnect 為任何裝置，建立安全性權杖時，它會是重要的 toouse hello 正確的資源 URI。</span><span class="sxs-lookup"><span data-stu-id="f2135-236">Since hello shared access policy can potentially grant access tooconnect as any device, it is important toouse hello correct resource URI when creating security tokens.</span></span> <span data-ttu-id="f2135-237">這項設定，請務必特別有 tooscope hello 語彙基元 tooa 特定裝置使用 hello 資源 URI 中的權杖服務。</span><span class="sxs-lookup"><span data-stu-id="f2135-237">This setting is especially important for token services, which have tooscope hello token tooa specific device using hello resource URI.</span></span> <span data-ttu-id="f2135-238">這點與通訊協定閘道的關聯性比較薄弱，因為它們已經在為所有裝置調節流量。</span><span class="sxs-lookup"><span data-stu-id="f2135-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="f2135-239">例如，權杖的服務使用 hello 預先建立共用存取原則**裝置**就會建立包含下列參數的 hello 的語彙基元：</span><span class="sxs-lookup"><span data-stu-id="f2135-239">As an example, a token service using hello pre-created shared access policy called **device** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="f2135-240">資源 URI： `{IoT hub name}.azure-devices.net/devices/{device id}`、</span><span class="sxs-lookup"><span data-stu-id="f2135-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="f2135-241">簽署金鑰： hello 的 hello 金鑰的其中之一`device`原則，</span><span class="sxs-lookup"><span data-stu-id="f2135-241">signing key: one of hello keys of hello `device` policy,</span></span>
* <span data-ttu-id="f2135-242">原則名稱： `device`、</span><span class="sxs-lookup"><span data-stu-id="f2135-242">policy name: `device`,</span></span>
* <span data-ttu-id="f2135-243">任何到期時間。</span><span class="sxs-lookup"><span data-stu-id="f2135-243">any expiration time.</span></span>

<span data-ttu-id="f2135-244">會使用 hello 前面 Node.js 函式的範例：</span><span class="sxs-lookup"><span data-stu-id="f2135-244">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="f2135-245">hello 結果，這會授與存取 tooall device1 的功能，會是：</span><span class="sxs-lookup"><span data-stu-id="f2135-245">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="f2135-246">通訊協定閘道無法使用相同語彙基元的只要設定的所有裝置都 hello 資源 URI 太都 hello`myhub.azure-devices.net/devices`。</span><span class="sxs-lookup"><span data-stu-id="f2135-246">A protocol gateway could use hello same token for all devices simply setting hello resource URI too`myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="f2135-247">使用來自服務元件的安全性權杖</span><span class="sxs-lookup"><span data-stu-id="f2135-247">Use security tokens from service components</span></span>

<span data-ttu-id="f2135-248">服務元件只會產生使用共用的存取原則授與 hello 適當的權限，如先前所述的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-248">Service components can only generate security tokens using shared access policies granting hello appropriate permissions as explained previously.</span></span>

<span data-ttu-id="f2135-249">以下是 hello hello 端點上公開的服務功能：</span><span class="sxs-lookup"><span data-stu-id="f2135-249">Here is hello service functions exposed on hello endpoints:</span></span>

| <span data-ttu-id="f2135-250">端點</span><span class="sxs-lookup"><span data-stu-id="f2135-250">Endpoint</span></span> | <span data-ttu-id="f2135-251">功能</span><span class="sxs-lookup"><span data-stu-id="f2135-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="f2135-252">建立、更新、擷取及刪除裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="f2135-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="f2135-253">接收裝置到雲端的訊息。</span><span class="sxs-lookup"><span data-stu-id="f2135-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="f2135-254">接收雲端到裝置之訊息的意見反應。</span><span class="sxs-lookup"><span data-stu-id="f2135-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="f2135-255">傳送雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="f2135-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="f2135-256">例如，產生使用 hello 預先建立的服務共用存取原則**registryRead**就會建立包含下列參數的 hello 的語彙基元：</span><span class="sxs-lookup"><span data-stu-id="f2135-256">As an example, a service generating using hello pre-created shared access policy called **registryRead** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="f2135-257">資源 URI： `{IoT hub name}.azure-devices.net/devices`、</span><span class="sxs-lookup"><span data-stu-id="f2135-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="f2135-258">簽署金鑰： hello 的 hello 金鑰的其中之一`registryRead`原則，</span><span class="sxs-lookup"><span data-stu-id="f2135-258">signing key: one of hello keys of hello `registryRead` policy,</span></span>
* <span data-ttu-id="f2135-259">原則名稱： `registryRead`、</span><span class="sxs-lookup"><span data-stu-id="f2135-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="f2135-260">任何到期時間。</span><span class="sxs-lookup"><span data-stu-id="f2135-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="f2135-261">hello 結果，會授與存取 tooread 所有的裝置識別身分，也會是：</span><span class="sxs-lookup"><span data-stu-id="f2135-261">hello result, which would grant access tooread all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="f2135-262">支援的 X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="f2135-262">Supported X.509 certificates</span></span>

<span data-ttu-id="f2135-263">您可以使用任何 X.509 憑證 tooauthenticate 裝置與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f2135-263">You can use any X.509 certificate tooauthenticate a device with IoT Hub.</span></span> <span data-ttu-id="f2135-264">憑證包含：</span><span class="sxs-lookup"><span data-stu-id="f2135-264">Certificates include:</span></span>

* <span data-ttu-id="f2135-265">**現有的 X.509 憑證**。</span><span class="sxs-lookup"><span data-stu-id="f2135-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="f2135-266">裝置可能已經有與其關聯的 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="f2135-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="f2135-267">hello 裝置可以使用此憑證 tooauthenticate 與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f2135-267">hello device can use this certificate tooauthenticate with IoT Hub.</span></span>
* <span data-ttu-id="f2135-268">**自我產生及自我簽署的 X-509 憑證**。</span><span class="sxs-lookup"><span data-stu-id="f2135-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="f2135-269">裝置製造商或內部部署器都可以產生這些憑證，並存放在 hello 裝置 hello 相對應的私密金鑰 （和憑證）。</span><span class="sxs-lookup"><span data-stu-id="f2135-269">A device manufacturer or in-house deployer can generate these certificates and store hello corresponding private key (and certificate) on hello device.</span></span> <span data-ttu-id="f2135-270">您可以使用 [OpenSSL][lnk-openssl] 和 [Windows SelfSignedCertificate][lnk-selfsigned] 公用程式之類的工具來達到此目的。</span><span class="sxs-lookup"><span data-stu-id="f2135-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="f2135-271">**CA 簽署的 X.509 憑證**。</span><span class="sxs-lookup"><span data-stu-id="f2135-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="f2135-272">tooidentify 裝置並驗證與 IoT 中樞，您可以使用產生和簽署的憑證授權單位 (CA) 的 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="f2135-272">tooidentify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="f2135-273">IoT 中樞只會驗證呈現該 hello 指紋符合 hello 設定憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="f2135-273">IoT Hub only verifies that hello thumbprint presented matches hello configured thumbprint.</span></span> <span data-ttu-id="f2135-274">Iot 中樞不會驗證 hello 憑證鏈結。</span><span class="sxs-lookup"><span data-stu-id="f2135-274">IotHub does not validate hello certificate chain.</span></span>

<span data-ttu-id="f2135-275">裝置可以使用 X.509 憑證或安全性權杖來進行驗證，但不可同時使用兩者。</span><span class="sxs-lookup"><span data-stu-id="f2135-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="f2135-276">註冊裝置的 X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="f2135-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="f2135-277">hello [Azure IoT 服務 SDK，C#] [ lnk-service-sdk] (版本 1.0.8+) 支援註冊的裝置，會使用 X.509 憑證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f2135-277">hello [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="f2135-278">其他 API (例如匯入/匯出裝置) 也支援 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="f2135-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="f2135-279">C\# 支援</span><span class="sxs-lookup"><span data-stu-id="f2135-279">C\# Support</span></span>

<span data-ttu-id="f2135-280">hello **RegistryManager**類別會提供程式設計的方式 tooregister 裝置。</span><span class="sxs-lookup"><span data-stu-id="f2135-280">hello **RegistryManager** class provides a programmatic way tooregister a device.</span></span> <span data-ttu-id="f2135-281">特別是，hello **AddDeviceAsync**和**UpdateDeviceAsync** tooregister 可讓您方法，並更新 hello IoT 中樞身分識別登錄中的裝置。</span><span class="sxs-lookup"><span data-stu-id="f2135-281">In particular, hello **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you tooregister and update a device in hello IoT Hub identity registry.</span></span> <span data-ttu-id="f2135-282">這兩種方法都會採用 **Device** 執行個體做為輸入。</span><span class="sxs-lookup"><span data-stu-id="f2135-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="f2135-283">hello**裝置**類別包含**驗證**屬性，可讓您 toospecify 主要和次要 X.509 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="f2135-283">hello **Device** class includes an **Authentication** property that allows you toospecify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="f2135-284">hello 指紋表示 （使用二進位 DER 編碼方式儲存） 的 hello X.509 憑證的 sha-1 雜湊。</span><span class="sxs-lookup"><span data-stu-id="f2135-284">hello thumbprint represents a SHA-1 hash of hello X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="f2135-285">您必須指定主憑證指紋或次要的憑證指紋或兩者的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="f2135-285">You have hello option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="f2135-286">主要和次要指紋是支援的 toohandle 憑證變換的情況。</span><span class="sxs-lookup"><span data-stu-id="f2135-286">Primary and secondary thumbprints are supported toohandle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="f2135-287">IoT 中樞不需要或儲存 hello 的整個 X.509 憑證，而只 hello 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="f2135-287">IoT Hub does not require or store hello entire X.509 certificate, only hello thumbprint.</span></span>

<span data-ttu-id="f2135-288">以下是範例 C\#程式碼片段 tooregister 使用 X.509 憑證的裝置：</span><span class="sxs-lookup"><span data-stu-id="f2135-288">Here is a sample C\# code snippet tooregister a device using an X.509 certificate:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="f2135-289">在執行階段作業期間使用 X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="f2135-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="f2135-290">hello[適用於.NET 的 Azure IoT 裝置 SDK] [ lnk-client-sdk] (版本 1.0.11+) 支援 hello 使用 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="f2135-290">hello [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports hello use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="f2135-291">C\# 支援</span><span class="sxs-lookup"><span data-stu-id="f2135-291">C\# Support</span></span>

<span data-ttu-id="f2135-292">hello 類別**DeviceAuthenticationWithX509Certificate**支援 hello 建立**DeviceClient**執行個體使用 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="f2135-292">hello class **DeviceAuthenticationWithX509Certificate** supports hello creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="f2135-293">hello X.509 憑證必須包含 hello 私密金鑰的 hello （也稱為 PKCS #12） 的 PFX 格式。</span><span class="sxs-lookup"><span data-stu-id="f2135-293">hello X.509 certificate must be in hello PFX (also called PKCS #12) format that includes hello private key.</span></span>

<span data-ttu-id="f2135-294">以下是範例程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="f2135-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="f2135-295">自訂裝置驗證</span><span class="sxs-lookup"><span data-stu-id="f2135-295">Custom device authentication</span></span>

<span data-ttu-id="f2135-296">您可以使用 hello IoT 中樞[身分識別登錄][ lnk-identity-registry] tooconfigure 每一裝置的安全性認證和存取控制使用[語彙基元][ lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="f2135-296">You can use hello IoT Hub [identity registry][lnk-identity-registry] tooconfigure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="f2135-297">如果您的 IoT 解決方案已有自訂身分識別登錄及/或驗證配置，請考慮建立*token service 的*toointegrate 這項基礎結構與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f2135-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* toointegrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="f2135-298">如此一來，您可以在解決方案中使用其他 IoT 功能。</span><span class="sxs-lookup"><span data-stu-id="f2135-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="f2135-299">權杖服務是自訂雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f2135-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="f2135-300">它會使用 IoT 中樞*共用存取原則*與**DeviceConnect**權限 toocreate*裝置範圍*語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f2135-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions toocreate *device-scoped* tokens.</span></span> <span data-ttu-id="f2135-301">這些語彙基元可讓裝置 tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f2135-301">These tokens enable a device tooconnect tooyour IoT hub.</span></span>

![Hello 語彙基元服務模式中的步驟][img-tokenservice]

<span data-ttu-id="f2135-303">Hello hello 語彙基元服務模式的主要步驟如下：</span><span class="sxs-lookup"><span data-stu-id="f2135-303">Here are hello main steps of hello token service pattern:</span></span>

1. <span data-ttu-id="f2135-304">為您的 IoT 中樞建立具備 **DeviceConnect** 權限的 IoT 中樞共用存取原則。</span><span class="sxs-lookup"><span data-stu-id="f2135-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="f2135-305">您可以建立此原則在 hello [Azure 入口網站][ lnk-management-portal]或以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="f2135-305">You can create this policy in hello [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="f2135-306">hello 語彙基元服務會使用它會建立此原則 toosign hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f2135-306">hello token service uses this policy toosign hello tokens it creates.</span></span>
1. <span data-ttu-id="f2135-307">當裝置需要 tooaccess IoT 中樞時，它會從您的權杖服務要求已簽署的權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-307">When a device needs tooaccess your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="f2135-308">hello 裝置可以驗證您自訂身分識別登錄/驗證配置 toodetermine hello 裝置身分識別的 hello 語彙基元服務會使用 toocreate hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f2135-308">hello device can authenticate with your custom identity registry/authentication scheme toodetermine hello device identity that hello token service uses toocreate hello token.</span></span>
1. <span data-ttu-id="f2135-309">hello 權杖服務傳回的權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-309">hello token service returns a token.</span></span> <span data-ttu-id="f2135-310">hello 語彙基元由使用`/devices/{deviceId}`為`resourceURI`，與`deviceId`為 hello 裝置驗證。</span><span class="sxs-lookup"><span data-stu-id="f2135-310">hello token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as hello device being authenticated.</span></span> <span data-ttu-id="f2135-311">hello 語彙基元服務會使用 hello 共用的存取原則 tooconstruct hello token。</span><span class="sxs-lookup"><span data-stu-id="f2135-311">hello token service uses hello shared access policy tooconstruct hello token.</span></span>
1. <span data-ttu-id="f2135-312">hello 裝置會使用直接與 hello IoT 中樞 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f2135-312">hello device uses hello token directly with hello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="f2135-313">您可以使用 hello.NET 類別[SharedAccessSignatureBuilder] [ lnk-dotnet-sas]或 hello Java 類別[IotHubServiceSasToken] [ lnk-java-sas] toocreate 語彙基元在權杖的服務中。</span><span class="sxs-lookup"><span data-stu-id="f2135-313">You can use hello .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or hello Java class [IotHubServiceSasToken][lnk-java-sas] toocreate a token in your token service.</span></span>

<span data-ttu-id="f2135-314">hello 語彙基元服務可以視需要設定 hello 權杖到期。</span><span class="sxs-lookup"><span data-stu-id="f2135-314">hello token service can set hello token expiration as desired.</span></span> <span data-ttu-id="f2135-315">Hello 權杖過期時，hello IoT 中樞伺服器 hello 裝置連線。</span><span class="sxs-lookup"><span data-stu-id="f2135-315">When hello token expires, hello IoT hub severs hello device connection.</span></span> <span data-ttu-id="f2135-316">然後，hello 裝置必須從 hello 語彙基元服務要求新權杖。</span><span class="sxs-lookup"><span data-stu-id="f2135-316">Then, hello device must request a new token from hello token service.</span></span> <span data-ttu-id="f2135-317">較短的到期時間會增加 hello 負載 hello 裝置和 hello 語彙基元服務。</span><span class="sxs-lookup"><span data-stu-id="f2135-317">A short expiry time increases hello load on both hello device and hello token service.</span></span>

<span data-ttu-id="f2135-318">裝置 tooconnect tooyour 中樞，還是必須將它 toohello IoT 中樞身分識別登錄 — 即使 hello 裝置使用的語彙基元和沒有裝置金鑰 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="f2135-318">For a device tooconnect tooyour hub, you must still add it toohello IoT Hub identity registry — even though hello device is using a token and not a device key tooconnect.</span></span> <span data-ttu-id="f2135-319">因此，您可以繼續 toouse 每一裝置的存取控制，啟用或停用裝置身分識別中 hello[身分識別登錄][lnk-identity-registry]。</span><span class="sxs-lookup"><span data-stu-id="f2135-319">Therefore, you can continue toouse per-device access control by enabling or disabling device identities in hello [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="f2135-320">這種方式可降低 hello 風險使用 token 搭配長時間的到期時間。</span><span class="sxs-lookup"><span data-stu-id="f2135-320">This approach mitigates hello risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="f2135-321">和自訂閘道器的比較</span><span class="sxs-lookup"><span data-stu-id="f2135-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="f2135-322">hello 語彙基元服務模式是 hello 建議的方式 tooimplement IoT 中樞的自訂身分識別登錄/驗證配置。</span><span class="sxs-lookup"><span data-stu-id="f2135-322">hello token service pattern is hello recommended way tooimplement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="f2135-323">因為 IoT 中心會繼續 toohandle 建議使用此模式，大部分的 hello 方案流量。</span><span class="sxs-lookup"><span data-stu-id="f2135-323">This pattern is recommended because IoT Hub continues toohandle most of hello solution traffic.</span></span> <span data-ttu-id="f2135-324">不過，如果使用 hello 通訊協定因此密不可分 hello 自訂驗證配置，您可能需要*自訂閘道*tooprocess 所有 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="f2135-324">However, if hello custom authentication scheme is so intertwined with hello protocol, you may require a *custom gateway* tooprocess all hello traffic.</span></span> <span data-ttu-id="f2135-325">使用[傳輸層安全性 (TLS) 和預先共用金鑰 (PSK)][lnk-tls-psk] 是這類案例的範例之一。</span><span class="sxs-lookup"><span data-stu-id="f2135-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="f2135-326">如需詳細資訊，請參閱 hello[通訊協定閘道][ lnk-protocols]主題。</span><span class="sxs-lookup"><span data-stu-id="f2135-326">For more information, see hello [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="f2135-327">參考主題：</span><span class="sxs-lookup"><span data-stu-id="f2135-327">Reference topics:</span></span>

<span data-ttu-id="f2135-328">hello 下列參考主題提供您有關控制存取 tooyour IoT 中樞的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f2135-328">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="f2135-329">IoT 中樞權限</span><span class="sxs-lookup"><span data-stu-id="f2135-329">IoT Hub permissions</span></span>

<span data-ttu-id="f2135-330">hello 下表列出您可以使用 toocontrol 存取 tooyour IoT 中樞的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="f2135-330">hello following table lists hello permissions you can use toocontrol access tooyour IoT hub.</span></span>

| <span data-ttu-id="f2135-331">權限</span><span class="sxs-lookup"><span data-stu-id="f2135-331">Permission</span></span> | <span data-ttu-id="f2135-332">注意事項</span><span class="sxs-lookup"><span data-stu-id="f2135-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="f2135-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="f2135-333">**RegistryRead**</span></span> |<span data-ttu-id="f2135-334">授與讀取存取 toohello 身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="f2135-334">Grants read access toohello identity registry.</span></span> <span data-ttu-id="f2135-335">如需詳細資訊，請參閱[身分識別登錄][lnk-identity-registry]。</span><span class="sxs-lookup"><span data-stu-id="f2135-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="f2135-336">後端雲端服務會使用此權限。</span><span class="sxs-lookup"><span data-stu-id="f2135-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="f2135-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="f2135-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="f2135-338">授與讀取和寫入存取 toohello 身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="f2135-338">Grants read and write access toohello identity registry.</span></span> <span data-ttu-id="f2135-339">如需詳細資訊，請參閱[身分識別登錄][lnk-identity-registry]。</span><span class="sxs-lookup"><span data-stu-id="f2135-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="f2135-340">後端雲端服務會使用此權限。</span><span class="sxs-lookup"><span data-stu-id="f2135-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="f2135-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="f2135-341">**ServiceConnect**</span></span> |<span data-ttu-id="f2135-342">授與存取 toocloud 面對服務的通訊和監視端點。</span><span class="sxs-lookup"><span data-stu-id="f2135-342">Grants access toocloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="f2135-343">授與權限 tooreceive 裝置到雲端訊息傳送雲端到裝置訊息，以及擷取 hello 對應傳遞通知。</span><span class="sxs-lookup"><span data-stu-id="f2135-343">Grants permission tooreceive device-to-cloud messages, send cloud-to-device messages, and retrieve hello corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="f2135-344">授與權限 tooretrieve 傳遞通知檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="f2135-344">Grants permission tooretrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="f2135-345">授與權限 tooaccess 裝置雙 tooupdate 標記和所需的屬性，擷取報告的屬性，並執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f2135-345">Grants permission tooaccess device twins tooupdate tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="f2135-346">後端雲端服務會使用此權限。</span><span class="sxs-lookup"><span data-stu-id="f2135-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="f2135-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="f2135-347">**DeviceConnect**</span></span> |<span data-ttu-id="f2135-348">授與存取 toodevice 向端點。</span><span class="sxs-lookup"><span data-stu-id="f2135-348">Grants access toodevice-facing endpoints.</span></span> <br/><span data-ttu-id="f2135-349">授與權限 toosend 裝置到雲端訊息和接收雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="f2135-349">Grants permission toosend device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="f2135-350">授與權限 tooperform 檔案上傳的裝置。</span><span class="sxs-lookup"><span data-stu-id="f2135-350">Grants permission tooperform file upload from a device.</span></span> <br/><span data-ttu-id="f2135-351">授與權限 tooreceive 裝置所需的兩個屬性通知和更新裝置 twin 報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="f2135-351">Grants permission tooreceive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="f2135-352">授與權限 tooperform 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="f2135-352">Grants permission tooperform file uploads.</span></span> <br/><span data-ttu-id="f2135-353">裝置會使用此權限。</span><span class="sxs-lookup"><span data-stu-id="f2135-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="f2135-354">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="f2135-354">Additional reference material</span></span>

<span data-ttu-id="f2135-355">Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：</span><span class="sxs-lookup"><span data-stu-id="f2135-355">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="f2135-356">[IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。</span><span class="sxs-lookup"><span data-stu-id="f2135-356">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="f2135-357">[節流和配額][ lnk-quotas]描述 hello 配額和節流套用 toohello IoT 中心服務的行為。</span><span class="sxs-lookup"><span data-stu-id="f2135-357">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="f2135-358">[Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用的 Sdk。</span><span class="sxs-lookup"><span data-stu-id="f2135-358">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="f2135-359">[IoT 中樞的查詢語言][ lnk-query]描述 hello 查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f2135-359">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="f2135-360">[IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f2135-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2135-361">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2135-361">Next steps</span></span>

<span data-ttu-id="f2135-362">現在您已經學會如何 toocontrol 存取 IoT 中樞時，您可能想要遵循 IoT 中樞開發人員指南主題 hello:</span><span class="sxs-lookup"><span data-stu-id="f2135-362">Now you have learned how toocontrol access IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="f2135-363">[使用裝置雙 toosynchronize 狀態和組態][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="f2135-363">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="f2135-364">[在裝置上叫用直接方法][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="f2135-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="f2135-365">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="f2135-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="f2135-366">如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2135-366">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="f2135-367">[開始使用 Azure IoT 中樞][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f2135-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="f2135-368">[Toosend 雲端到裝置與 IoT 中樞的訊息][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f2135-368">[How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="f2135-369">[如何 tooprocess IoT 中樞裝置到雲端訊息][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f2135-369">[How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
