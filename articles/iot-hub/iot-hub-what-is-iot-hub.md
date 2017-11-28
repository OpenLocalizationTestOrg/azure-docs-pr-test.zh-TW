---
title: "aaaAzure IoT 中樞概觀 |Microsoft 文件"
description: "Hello Azure IoT 中心服務的概觀： 什麼是 IoT 中樞、 裝置連線能力、 網際網路的事情通訊模式、 閘道和 hello 服務輔助通訊模式"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a><span data-ttu-id="66260-103">Hello Azure IoT 中心服務的概觀</span><span class="sxs-lookup"><span data-stu-id="66260-103">Overview of hello Azure IoT Hub service</span></span>

<span data-ttu-id="66260-104">歡迎使用 tooAzure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="66260-104">Welcome tooAzure IoT Hub.</span></span> <span data-ttu-id="66260-105">這篇文章會提供 Azure IoT 中樞的概觀，並說明為什麼您應該使用此服務 tooimplement 物聯網 (IoT) 解決方案。</span><span class="sxs-lookup"><span data-stu-id="66260-105">This article provides an overview of Azure IoT Hub and describes why you should use this service tooimplement an Internet of Things (IoT) solution.</span></span> <span data-ttu-id="66260-106">Azure IoT 中樞是一項完全受管理的服務，可在數百萬個 IoT 裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="66260-106">Azure IoT Hub is a fully managed service that enables reliable and secure bidirectional communications between millions of IoT devices and a solution back end.</span></span> <span data-ttu-id="66260-107">Azure IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="66260-107">Azure IoT Hub:</span></span>

* <span data-ttu-id="66260-108">提供多個裝置到雲端和雲端到裝置通訊選項，包括單向傳訊、檔案傳輸，以及要求-回覆方法。</span><span class="sxs-lookup"><span data-stu-id="66260-108">Provides multiple device-to-cloud and cloud-to-device communication options, including one-way messaging, file transfer, and request-reply methods.</span></span>
* <span data-ttu-id="66260-109">提供內建的宣告式訊息路由 tooother Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="66260-109">Provides built-in declarative message routing tooother Azure services.</span></span>
* <span data-ttu-id="66260-110">針對裝置中繼資料與同步化狀態資訊提供可查詢存放區。</span><span class="sxs-lookup"><span data-stu-id="66260-110">Provides a queryable store for device metadata and synchronized state information.</span></span>
* <span data-ttu-id="66260-111">使用每一裝置的安全性金鑰或 X.509 憑證啟用安全通訊與存取控制。</span><span class="sxs-lookup"><span data-stu-id="66260-111">Enables secure communications and access control using per-device security keys or X.509 certificates.</span></span>
* <span data-ttu-id="66260-112">可廣泛監視裝置的連線情況和裝置的身分識別管理事件。</span><span class="sxs-lookup"><span data-stu-id="66260-112">Provides extensive monitoring for device connectivity and device identity management events.</span></span>
* <span data-ttu-id="66260-113">包含裝置 hello 最受歡迎的語言與平台的程式庫。</span><span class="sxs-lookup"><span data-stu-id="66260-113">Includes device libraries for hello most popular languages and platforms.</span></span>

<span data-ttu-id="66260-114">hello 文章[比較的 IoT 中樞與事件中心][ lnk-compare]描述 hello 這兩個服務之間的主要差異，並反白顯示您的 IoT 解決方案中使用 IoT 中樞的 hello 優點。</span><span class="sxs-lookup"><span data-stu-id="66260-114">hello article [Comparison of IoT Hub and Event Hubs][lnk-compare] describes hello key differences between these two services and highlights hello advantages of using IoT Hub in your IoT solutions.</span></span>

<span data-ttu-id="66260-115">如需有關如何 Azure 與 IoT 中樞協助保護您的 IoT 解決方案的詳細資訊，請參閱[從 hello 地面物聯網安全性][lnk-security-ground-up]。</span><span class="sxs-lookup"><span data-stu-id="66260-115">For more information on how Azure and IoT Hub help secure your IoT solution, see [Internet of Things security from hello ground up][lnk-security-ground-up].</span></span>

![Azure IoT 中樞做為物聯網解決方案中的雲端閘道][img-architecture]

> [!NOTE]
> <span data-ttu-id="66260-117">IoT 架構的深入討論，請參閱 hello [Microsoft Azure IoT 參考架構][lnk-refarch]。</span><span class="sxs-lookup"><span data-stu-id="66260-117">For an in-depth discussion of IoT architecture, see hello [Microsoft Azure IoT Reference Architecture][lnk-refarch].</span></span>

## <a name="iot-device-connectivity-challenges"></a><span data-ttu-id="66260-118">IoT 裝置連線能力面臨的挑戰</span><span class="sxs-lookup"><span data-stu-id="66260-118">IoT device-connectivity challenges</span></span>

<span data-ttu-id="66260-119">IoT 中樞與 hello 裝置庫幫助您如何 toomeet hello 挑戰 tooreliably 安全地連線裝置 toohello 方案後端。</span><span class="sxs-lookup"><span data-stu-id="66260-119">IoT Hub and hello device libraries help you toomeet hello challenges of how tooreliably and securely connect devices toohello solution back end.</span></span> <span data-ttu-id="66260-120">IoT 裝置：</span><span class="sxs-lookup"><span data-stu-id="66260-120">IoT devices:</span></span>

* <span data-ttu-id="66260-121">通常是無人操作的嵌入式系統。</span><span class="sxs-lookup"><span data-stu-id="66260-121">Are often embedded systems with no human operator.</span></span>
* <span data-ttu-id="66260-122">可以位於實體存取很昂貴的遠端位置。</span><span class="sxs-lookup"><span data-stu-id="66260-122">Can be in remote locations, where physical access is expensive.</span></span>
* <span data-ttu-id="66260-123">只能透過 hello 方案後端連線。</span><span class="sxs-lookup"><span data-stu-id="66260-123">May only be reachable through hello solution back end.</span></span>
* <span data-ttu-id="66260-124">能力和/或處理資源可能都有限。</span><span class="sxs-lookup"><span data-stu-id="66260-124">May have limited power and processing resources.</span></span>
* <span data-ttu-id="66260-125">網路連線能力可能不穩定、緩慢或昂貴。</span><span class="sxs-lookup"><span data-stu-id="66260-125">May have intermittent, slow, or expensive network connectivity.</span></span>
* <span data-ttu-id="66260-126">可能需要 toouse 專用、 自訂或業界特定的應用程式通訊協定。</span><span class="sxs-lookup"><span data-stu-id="66260-126">May need toouse proprietary, custom, or industry-specific application protocols.</span></span>
* <span data-ttu-id="66260-127">可以使用一組大型常見的硬體和軟體平台來建立。</span><span class="sxs-lookup"><span data-stu-id="66260-127">Can be created using a large set of popular hardware and software platforms.</span></span>

<span data-ttu-id="66260-128">除了上述 toohello 需求，任何 IoT 解決方案必須也提供小數位數、 安全性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="66260-128">In addition toohello requirements above, any IoT solution must also deliver scale, security, and reliability.</span></span> <span data-ttu-id="66260-129">hello 產生的連線需求是困難且耗時 tooimplement 當您使用傳統的技術，例如 web 容器及訊息代理人。</span><span class="sxs-lookup"><span data-stu-id="66260-129">hello resulting set of connectivity requirements is hard and time-consuming tooimplement when you use traditional technologies, such as web containers and messaging brokers.</span></span>

## <a name="why-use-azure-iot-hub"></a><span data-ttu-id="66260-130">為何使用 Azure IoT 中心？</span><span class="sxs-lookup"><span data-stu-id="66260-130">Why use Azure IoT Hub?</span></span>

<span data-ttu-id="66260-131">此外 tooa 豐富的[裝置到雲端][ lnk-d2c-guidance]和[雲端到裝置][ lnk-c2d-guidance]通訊選項，包括訊息、 檔案轉送和要求-回覆方法 Azure IoT 中樞位址 hello hello 下列方式中的裝置連線挑戰：</span><span class="sxs-lookup"><span data-stu-id="66260-131">In addition tooa rich set of [device-to-cloud][lnk-d2c-guidance] and [cloud-to-device][lnk-c2d-guidance] communication options, including messaging, file transfers, and request-reply methods, Azure IoT Hub addresses hello device-connectivity challenges in hello following ways:</span></span>

* <span data-ttu-id="66260-132">**裝置對應項**。</span><span class="sxs-lookup"><span data-stu-id="66260-132">**Device twins**.</span></span> <span data-ttu-id="66260-133">使用[裝置對應項][lnk-twins]，您可以儲存、同步處理，以及查詢裝置中繼資料與狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="66260-133">Using [Device twins][lnk-twins], you can store, synchronize, and query device metadata and state information.</span></span> <span data-ttu-id="66260-134">「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="66260-134">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="66260-135">IoT 中樞保存您連接 tooIoT 中樞的每個裝置的裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="66260-135">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span>

* <span data-ttu-id="66260-136">**每一裝置的驗證和安全連線能力**。</span><span class="sxs-lookup"><span data-stu-id="66260-136">**Per-device authentication and secure connectivity**.</span></span> <span data-ttu-id="66260-137">您可以將每個裝置使用它自己佈建[安全性金鑰][ lnk-devguide-security] tooenable 它 tooconnect tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="66260-137">You can provision each device with its own [security key][lnk-devguide-security] tooenable it tooconnect tooIoT Hub.</span></span> <span data-ttu-id="66260-138">hello [IoT 中樞身分識別登錄][ lnk-devguide-identityregistry]將裝置身分識別和索引鍵儲存在方案中。</span><span class="sxs-lookup"><span data-stu-id="66260-138">hello [IoT Hub identity registry][lnk-devguide-identityregistry] stores device identities and keys in a solution.</span></span> <span data-ttu-id="66260-139">方案的後端加入個別裝置 tooallow 或拒絕清單 tooenable 擁有完整控制權存取裝置。</span><span class="sxs-lookup"><span data-stu-id="66260-139">A solution back end can add individual devices tooallow or deny lists tooenable complete control over device access.</span></span>

* <span data-ttu-id="66260-140">**路由裝置到雲端訊息的宣告式規則為基礎的 tooAzure 服務**。</span><span class="sxs-lookup"><span data-stu-id="66260-140">**Route device-to-cloud messages tooAzure services based on declarative rules**.</span></span> <span data-ttu-id="66260-141">IoT 中樞可讓您 toodefine 訊息讓您的中樞傳送裝置到雲端訊息的路由規則 toocontrol 為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="66260-141">IoT Hub enables you toodefine message routes based on routing rules toocontrol where your hub sends device-to-cloud messages.</span></span> <span data-ttu-id="66260-142">路由規則不需要您 toowrite 任何程式碼中，而且可以進行 hello 的自訂後擷取訊息發送器。</span><span class="sxs-lookup"><span data-stu-id="66260-142">Routing rules do not require you toowrite any code, and can take hello place of custom post-ingestion message dispatchers.</span></span>

* <span data-ttu-id="66260-143">**裝置連線作業的監視**。</span><span class="sxs-lookup"><span data-stu-id="66260-143">**Monitoring of device connectivity operations**.</span></span> <span data-ttu-id="66260-144">您可以收到有關裝置身分識別管理作業與裝置連線事件的詳細作業記錄檔。</span><span class="sxs-lookup"><span data-stu-id="66260-144">You can receive detailed operation logs about device identity management operations and device connectivity events.</span></span> <span data-ttu-id="66260-145">這項監視功能可以讓您 IoT 解決方案 tooidentify 連線問題，例如頻率太高，傳送訊息，或拒絕所有雲端到裝置訊息 tooconnect 不正確的認證，再試一次的裝置。</span><span class="sxs-lookup"><span data-stu-id="66260-145">This monitoring capability enables your IoT solution tooidentify connectivity issues, such as devices that try tooconnect with wrong credentials, send messages too frequently, or reject all cloud-to-device messages.</span></span>

* <span data-ttu-id="66260-146">**一組廣泛的裝置程式庫**。</span><span class="sxs-lookup"><span data-stu-id="66260-146">**An extensive set of device libraries**.</span></span> <span data-ttu-id="66260-147">[Azure IoT 裝置 SDK][lnk-device-sdks] 可供各種語言和平台使用並受其支援，例如許多 Linux 發行版本都支援的 C、Windows 和即時作業系統。</span><span class="sxs-lookup"><span data-stu-id="66260-147">[Azure IoT device SDKs][lnk-device-sdks] are available and supported for various languages and platforms--C for many Linux distributions, Windows, and real-time operating systems.</span></span> <span data-ttu-id="66260-148">Azure IoT 裝置 SDK 也支援 C#、Java 和 JavaScript 等 Managed 語言。</span><span class="sxs-lookup"><span data-stu-id="66260-148">Azure IoT device SDKs also support managed languages, such as C#, Java, and JavaScript.</span></span>

* <span data-ttu-id="66260-149">**IoT 通訊協定和擴充性**。</span><span class="sxs-lookup"><span data-stu-id="66260-149">**IoT protocols and extensibility**.</span></span> <span data-ttu-id="66260-150">如果您的方案無法使用 hello 裝置程式庫，IoT 中樞會公開公用的通訊協定，可讓裝置 toonatively 使用 hello MQTT v3.1.1、 HTTP 1.1 或 AMQP 1.0 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="66260-150">If your solution cannot use hello device libraries, IoT Hub exposes a public protocol that enables devices toonatively use hello MQTT v3.1.1, HTTP 1.1, or AMQP 1.0 protocols.</span></span> <span data-ttu-id="66260-151">您也可以擴充的自訂通訊協定的 IoT 中樞 toosupport:</span><span class="sxs-lookup"><span data-stu-id="66260-151">You can also extend IoT Hub toosupport for custom protocols by:</span></span>

  * <span data-ttu-id="66260-152">建立具有欄位閘道[Azure IoT 邊緣][ lnk-iot-edge]將您的自訂通訊協定 tooone hello 三種通訊協定瞭解 IoT 中樞的轉換。</span><span class="sxs-lookup"><span data-stu-id="66260-152">Creating a field gateway with [Azure IoT Edge][lnk-iot-edge] that converts your custom protocol tooone of hello three protocols understood by IoT Hub.</span></span>
  * <span data-ttu-id="66260-153">自訂 hello [Azure IoT 通訊協定閘道][protocol-gateway]，hello 雲端中執行的開放原始碼元件。</span><span class="sxs-lookup"><span data-stu-id="66260-153">Customizing hello [Azure IoT protocol gateway][protocol-gateway], an open source component that runs in hello cloud.</span></span>

* <span data-ttu-id="66260-154">**規模**。</span><span class="sxs-lookup"><span data-stu-id="66260-154">**Scale**.</span></span> <span data-ttu-id="66260-155">Azure IoT 中樞縮放 toomillions 的同時連線的裝置和數百萬個每秒的事件。</span><span class="sxs-lookup"><span data-stu-id="66260-155">Azure IoT Hub scales toomillions of simultaneously connected devices and millions of events per second.</span></span>

## <a name="gateways"></a><span data-ttu-id="66260-156">閘道</span><span class="sxs-lookup"><span data-stu-id="66260-156">Gateways</span></span>

<span data-ttu-id="66260-157">閘道的 IoT 解決方案通常是 [通訊協定閘道][ lnk-iotedge] hello 雲端中為針對部署或[欄位閘道][ lnk-field-gateway]也就是部署在本機裝置。</span><span class="sxs-lookup"><span data-stu-id="66260-157">A gateway in an IoT solution is typically either a [protocol gateway][lnk-iotedge] that is deployed in hello cloud or a [field gateway][lnk-field-gateway] that is deployed locally with your devices.</span></span> <span data-ttu-id="66260-158">通訊協定閘道執行通訊協定轉譯，例如 MQTT tooAMQP。</span><span class="sxs-lookup"><span data-stu-id="66260-158">A protocol gateway performs protocol translation, for example MQTT tooAMQP.</span></span> <span data-ttu-id="66260-159">欄位閘道可以 hello 邊緣上執行分析，做出時間緊迫 tooreduce 延遲、 提供裝置管理服務，強制執行安全性和隱私權條件約束，且也執行通訊協定轉譯。</span><span class="sxs-lookup"><span data-stu-id="66260-159">A field gateway can run analytics on hello edge, make time-sensitive decisions tooreduce latency, provide device management services, enforce security and privacy constraints, and also perform protocol translation.</span></span> <span data-ttu-id="66260-160">這兩種閘道器可做為您的裝置與 IoT 中樞之間的媒介。</span><span class="sxs-lookup"><span data-stu-id="66260-160">Both gateway types act as intermediaries between your devices and your IoT hub.</span></span>

<span data-ttu-id="66260-161">現場閘道器與簡單的流量路由裝置 (例如網路位址轉譯裝置或防火牆) 不同，因為它通常會在解決方案內管理存取和資訊流程中扮演主動的角色。</span><span class="sxs-lookup"><span data-stu-id="66260-161">A field gateway differs from a simple traffic routing device (such as a network address translation device or firewall) because it typically performs an active role in managing access and information flow in your solution.</span></span>

<span data-ttu-id="66260-162">解決方案可以同時包含通訊協定閘道和領域閘道。</span><span class="sxs-lookup"><span data-stu-id="66260-162">A solution may include both protocol and field gateways.</span></span>

## <a name="how-does-iot-hub-work"></a><span data-ttu-id="66260-163">IoT 中樞如何運作？</span><span class="sxs-lookup"><span data-stu-id="66260-163">How does IoT Hub work?</span></span>

<span data-ttu-id="66260-164">Azure IoT 中樞實作 hello[服務輔助通訊][ lnk-service-assisted-pattern]您的裝置與您的方案之間的模式 toomediate hello 互動後端。</span><span class="sxs-lookup"><span data-stu-id="66260-164">Azure IoT Hub implements hello [service-assisted communication][lnk-service-assisted-pattern] pattern toomediate hello interactions between your devices and your solution back end.</span></span> <span data-ttu-id="66260-165">hello 目標服務輔助通訊是 tooestablish trustworthy，雙向通訊路徑之間控制系統，例如 IoT 中樞和特殊用途的裝置部署在不受信任的實體空間。</span><span class="sxs-lookup"><span data-stu-id="66260-165">hello goal of service-assisted communication is tooestablish trustworthy, bidirectional communication paths between a control system, such as IoT Hub, and special-purpose devices that are deployed in untrusted physical space.</span></span> <span data-ttu-id="66260-166">hello 模式建立 hello 下列原則：</span><span class="sxs-lookup"><span data-stu-id="66260-166">hello pattern establishes hello following principles:</span></span>

* <span data-ttu-id="66260-167">安全性的優先順序高於所有其他功能。</span><span class="sxs-lookup"><span data-stu-id="66260-167">Security takes precedence over all other capabilities.</span></span>

* <span data-ttu-id="66260-168">裝置不會接受未經要求的網路資訊。</span><span class="sxs-lookup"><span data-stu-id="66260-168">Devices do not accept unsolicited network information.</span></span> <span data-ttu-id="66260-169">裝置會以僅限輸出方式建立所有連接和路由。</span><span class="sxs-lookup"><span data-stu-id="66260-169">A device establishes all connections and routes in an outbound-only fashion.</span></span> <span data-ttu-id="66260-170">裝置 tooreceive hello 方案後端的命令，如 hello 裝置必須定期啟動任何暫止命令 tooprocess 連接的 toocheck。</span><span class="sxs-lookup"><span data-stu-id="66260-170">For a device tooreceive a command from hello solution back end, hello device must regularly initiate a connection toocheck for any pending commands tooprocess.</span></span>

* <span data-ttu-id="66260-171">裝置應該只在連接 tooor 建立它們是否例如 IoT Hub 對等與路由 toowell 已知服務。</span><span class="sxs-lookup"><span data-stu-id="66260-171">Devices should only connect tooor establish routes toowell-known services they are peered with, such as IoT Hub.</span></span>

* <span data-ttu-id="66260-172">hello 應用程式通訊協定層級受到保護裝置與服務之間或裝置和閘道之間的 hello 通訊路徑。</span><span class="sxs-lookup"><span data-stu-id="66260-172">hello communication path between device and service or between device and gateway is secured at hello application protocol layer.</span></span>

* <span data-ttu-id="66260-173">系統層級的授權和驗證是以每個裝置的身分識別為基礎。</span><span class="sxs-lookup"><span data-stu-id="66260-173">System-level authorization and authentication are based on per-device identities.</span></span> <span data-ttu-id="66260-174">可讓存取認證和權限能近乎即時撤銷。</span><span class="sxs-lookup"><span data-stu-id="66260-174">They make access credentials and permissions nearly instantly revocable.</span></span>

* <span data-ttu-id="66260-175">連線偶發性到期 toopower 或連線問題的裝置的雙向通訊透過來保存命令和裝置通知，直到裝置連線 tooreceive 實現它們。</span><span class="sxs-lookup"><span data-stu-id="66260-175">Bidirectional communication for devices that connect sporadically due toopower or connectivity concerns is facilitated by holding commands and device notifications until a device connects tooreceive them.</span></span> <span data-ttu-id="66260-176">IoT 中樞維護裝置的特定佇列傳送 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="66260-176">IoT Hub maintains device-specific queues for hello commands it sends.</span></span>

* <span data-ttu-id="66260-177">應用程式裝載資料是透過閘道 tooa 特定服務的受保護傳輸資料的報表分開保護。</span><span class="sxs-lookup"><span data-stu-id="66260-177">Application payload data is secured separately for protected transit through gateways tooa particular service.</span></span>

<span data-ttu-id="66260-178">hello 行動業界已用 hello 服務輔助通訊模式在龐大的小數位數 tooimplement 推播通知服務如[Windows 推播通知服務][lnk-wns]， [Google 雲端訊息][lnk-google-messaging]，和[Apple 推播通知服務][lnk-apple-push]。</span><span class="sxs-lookup"><span data-stu-id="66260-178">hello mobile industry has used hello service-assisted communication pattern at enormous scale tooimplement push notification services such as [Windows Push Notification Services][lnk-wns], [Google Cloud Messaging][lnk-google-messaging], and [Apple Push Notification Service][lnk-apple-push].</span></span>

<span data-ttu-id="66260-179">ExpressRoute 的公用對等互連路徑支援 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="66260-179">IoT Hub is supported over ExpressRoute's public peering path.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66260-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66260-180">Next steps</span></span>

<span data-ttu-id="66260-181">toolearn toosend 訊息從裝置的方式，並接收 IoT 中樞，以及如何 tooconfigure 訊息會路由傳送，請參閱[傳送和接收訊息與 IoT 中樞][lnk-send-messages]。</span><span class="sxs-lookup"><span data-stu-id="66260-181">toolearn how toosend messages from a device and receive them from IoT Hub, as well as how tooconfigure message routes, see [Send and receive messages with IoT Hub][lnk-send-messages].</span></span>

<span data-ttu-id="66260-182">toolearn 如何 IoT 中樞可讓標準為基礎的裝置管理，針對您 tooremotely 管理、 設定及更新您的裝置，請參閱[裝置管理概觀與 IoT 中樞][lnk-device-management]。</span><span class="sxs-lookup"><span data-stu-id="66260-182">toolearn how IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="66260-183">tooimplement 各種裝置的硬體平台和作業系統上的用戶端應用程式，您可以使用 hello Azure IoT 裝置 Sdk。</span><span class="sxs-lookup"><span data-stu-id="66260-183">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="66260-184">hello 裝置 Sdk 包含程式庫，以便傳送遙測 tooan IoT 中樞與接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="66260-184">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="66260-185">當您使用 hello 裝置 Sdk 時，您可以選擇從各種網路通訊協定 toocommunicate 與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="66260-185">When you use hello device SDKs, you can choose from various network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="66260-186">toolearn 詳細資訊，請參閱 hello[裝置 Sdk 的相關資訊][lnk-device-sdks]。</span><span class="sxs-lookup"><span data-stu-id="66260-186">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="66260-187">tooget 啟動撰寫一些程式碼，並執行一些範例，請參閱 hello[開始使用 IoT 中樞][ lnk-get-started]教學課程。</span><span class="sxs-lookup"><span data-stu-id="66260-187">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-get-started] tutorial.</span></span>

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "服務輔助通訊 (由 Clemens Vasters 撰寫的部落格文章)"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md
