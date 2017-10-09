---
title: "aaaConnected factory Azure IoT 套件方案逐步解說 |Microsoft 文件"
description: "Hello 預先設定的 Azure IoT 解決方案描述連接處理站和其架構。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="a1ee0-103">連線處理站預先設定的解決方案逐步解說</span><span class="sxs-lookup"><span data-stu-id="a1ee0-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="a1ee0-104">hello IoT 套件連線 factory[預先設定的解決方案][ lnk-preconfigured-solutions]是端對端工業解決方案的實作的：</span><span class="sxs-lookup"><span data-stu-id="a1ee0-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="a1ee0-105">連接 tooboth 模擬工業 OPC UA 伺服器以執行模擬原廠生產線條，以及實際 OPC UA 伺服器裝置的裝置。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="a1ee0-106">如需有關 OPC UA 的詳細資訊，請參閱 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="a1ee0-107">顯示作業 KPI 和這些裝置與生產線的 OEE。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="a1ee0-108">示範如何以雲端為基礎的應用程式可能是使用的 toointeract 與 OPC UA 伺服器系統。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="a1ee0-109">可讓您 tooconnect 自己 OPC UA 伺服器裝置。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="a1ee0-110">可讓您 toobrowse 和修改 hello OPC UA 伺服器資料。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="a1ee0-111">整合與 hello Azure 時間數列 Insights (TSI) 服務 tooprovide OPC UA 伺服器 hello 資料的自訂的檢視。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="a1ee0-112">您可以做為起點使用 hello 解決方案，為您自己的實作和[自訂][ lnk-customize]它 toomeet 特定的業務需求。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="a1ee0-113">這篇文章會引導您完成 hello 索引鍵的某些項目連接的 hello factory 方案 tooenable 您 toounderstand 它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="a1ee0-114">這項知識能協助您︰</span><span class="sxs-lookup"><span data-stu-id="a1ee0-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="a1ee0-115">疑難排解 hello 方案中的問題。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="a1ee0-116">規劃如何 toocustomize toohello 方案 toomeet 您自己的特定需求。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="a1ee0-117">設計使用 Azure 服務的 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="a1ee0-118">如需詳細資訊，請參閱 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="a1ee0-119">邏輯架構</span><span class="sxs-lookup"><span data-stu-id="a1ee0-119">Logical architecture</span></span>

<span data-ttu-id="a1ee0-120">下列圖表中的 hello 概述 hello 邏輯解決方案元件的預先設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1ee0-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![連線處理站的邏輯架構][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="a1ee0-122">通訊模式</span><span class="sxs-lookup"><span data-stu-id="a1ee0-122">Communication patterns</span></span>

<span data-ttu-id="a1ee0-123">hello 解決方案使用 hello [OPC UA Pub/Sub 規格](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/)toosend OPC UA 遙測資料 tooIoT 中樞 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="a1ee0-124">hello 解決方案使用 hello [OPC 發行者](https://github.com/Azure/iot-edge-opc-publisher)IoT 邊緣適用於此用途的模組。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="a1ee0-125">hello 方案還有整合到 web 應用程式，可以建立具有內部 OPC UA 伺服器連接的 OPC UA 用戶端。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="a1ee0-126">hello 用戶端會使用[反向 proxy](https://wikipedia.org/wiki/Reverse_proxy) ，並接收來自 IoT 中樞 toomake hello 連線的說明，而不需要 hello 內部防火牆中的開啟通訊埠。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="a1ee0-127">此通訊模式稱為[服務輔助通訊](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/)。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="a1ee0-128">hello 解決方案使用 hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT 邊緣適用於此用途的模組。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="a1ee0-129">模擬</span><span class="sxs-lookup"><span data-stu-id="a1ee0-129">Simulation</span></span>

<span data-ttu-id="a1ee0-130">hello 模擬工作站與 hello 模擬製造執行 systems (MES) 組成原廠生產線上。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="a1ee0-131">hello 模擬的裝置和 hello OPC 發行者模組取決於 hello [OPC UA.NET 標準][ lnk-OPC-UA-NET-Standard] hello OPC Foundation 所發行。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="a1ee0-132">hello OPC Proxy 和 OPC 發行者會實作為基礎的模組[Azure IoT 邊緣][lnk-Azure-IoT-Gateway]。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="a1ee0-133">每個模擬產品線都已連結指定的閘道。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="a1ee0-134">所有模擬元件都是在裝載於 Azure Linux VM 的 Docker 容器中執行。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="a1ee0-135">hello 模擬是設定的 toorun 八個模擬的生產行的預設值。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="a1ee0-136">模擬生產線</span><span class="sxs-lookup"><span data-stu-id="a1ee0-136">Simulated production line</span></span>

<span data-ttu-id="a1ee0-137">生產線可製造零件。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-137">A production line manufactures parts.</span></span> <span data-ttu-id="a1ee0-138">它是由不同的工作站所組成︰組裝工作站、測試工作站和包裝工作站。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="a1ee0-139">hello 模擬執行，並更新透過 hello OPC UA 節點公開的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="a1ee0-140">所有的模擬的生產線站台是由 hello 透過 OPC UA MES 協調。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="a1ee0-141">模擬製造執行系統</span><span class="sxs-lookup"><span data-stu-id="a1ee0-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="a1ee0-142">hello MES 監視透過 OPC UA toodetect 站台的狀態變更的 hello 生產列中的每個站台。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="a1ee0-143">它呼叫 OPC UA 方法 toocontrol hello 站台，並傳遞產品從一個站台 toohello 下一步完成為止。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="a1ee0-144">閘道 OPC 發行者模組</span><span class="sxs-lookup"><span data-stu-id="a1ee0-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="a1ee0-145">OPC 發行者模組會連接 toohello 站 OPC UA 伺服器，並訂閱 toohello OPC 節點 toobe 發行。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="a1ee0-146">hello 模組將 hello 節點資料轉換成 JSON 格式，會加密，並將它以 OPC UA Pub/Sub 訊息傳送 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="a1ee0-147">hello OPC 發行者模組只需要輸出的 https 連接埠 (443)，並且可以使用與現有的企業基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="a1ee0-148">閘道 OPC Proxy 模組</span><span class="sxs-lookup"><span data-stu-id="a1ee0-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="a1ee0-149">hello 閘道 OPC UA Proxy 模組二進位 OPC UA 命令和控制訊息以通道連接，而且只要求的輸出 https 連接埠 (443)。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="a1ee0-150">它可以使用現有的企業基礎結構，包括 Web Proxy。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="a1ee0-151">它使用 hello 應用程式層級的 IoT 中樞裝置方法 tootransfer packetized TCP/IP 資料，並因此可確保端點信任、 資料加密，以及使用 SSL/TLS 的完整性。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="a1ee0-152">UA 驗證和加密，則會使用 hello OPC UA 二進位通訊協定透過本身的 hello proxy 轉送。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="a1ee0-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="a1ee0-153">Azure Time Series Insights</span></span>

<span data-ttu-id="a1ee0-154">hello 閘道 OPC 發行者模組訂閱 tooOPC UA 伺服器節點 toodetect hello 資料值變更。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="a1ee0-155">其中一個 hello 節點中，偵測到的資料變更時，此模組會接著傳送訊息 tooAzure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="a1ee0-156">IoT 中樞提供事件來源 tooAzure TSI。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="a1ee0-157">TSI 30 天的時間戳記為基礎的存放區資料會附加 toohello 訊息。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="a1ee0-158">這項資料包括︰</span><span class="sxs-lookup"><span data-stu-id="a1ee0-158">This data includes:</span></span>

* <span data-ttu-id="a1ee0-159">OPC UA ApplicationUri</span><span class="sxs-lookup"><span data-stu-id="a1ee0-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="a1ee0-160">OPC UA NodeId</span><span class="sxs-lookup"><span data-stu-id="a1ee0-160">OPC UA NodeId</span></span>
* <span data-ttu-id="a1ee0-161">Hello 節點的值</span><span class="sxs-lookup"><span data-stu-id="a1ee0-161">Value of hello node</span></span>
* <span data-ttu-id="a1ee0-162">來源時間戳記</span><span class="sxs-lookup"><span data-stu-id="a1ee0-162">Source timestamp</span></span>
* <span data-ttu-id="a1ee0-163">OPC UA DisplayName</span><span class="sxs-lookup"><span data-stu-id="a1ee0-163">OPC UA DisplayName</span></span>

<span data-ttu-id="a1ee0-164">目前，TSI 不允許客戶 toocustomize 多久他們希望 tookeep hello 資料。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="a1ee0-165">TSI 會使用 SearchSpan (Time.From、Time.To) 針對節點資料進行查詢，並依 OPC UA ApplicationUri 或 OPC UA NodeId 或 OPC UA DisplayName 進行彙總。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="a1ee0-166">依計數事件、 Sum、 Avg、 Min 和 Max 彙總 tooretrieve hello hello OEE 和 KPI 量測計和 hello 時間序列圖表資料的資料。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="a1ee0-167">使用不同的處理序建立 hello 時間序列。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-167">hello time series are built using a different process.</span></span> <span data-ttu-id="a1ee0-168">OEE 和 Kpi 從站台的基底資料計算出來，hello 應用程式中的反昇註冊 hello 拓撲 （生產線、 處理站、 enterprise）。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="a1ee0-169">此外，OEE 和 KPI 拓撲的時間序列是在計算 hello 應用程式，準備好顯示的時間範圍時。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="a1ee0-170">例如，每個完整小時會更新 hello 天檢視。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="a1ee0-171">節點資料 hello 時間序列檢視直接來自 TSI 使用彙總的 timespan。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="a1ee0-172">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="a1ee0-172">IoT Hub</span></span>
<span data-ttu-id="a1ee0-173">hello [IoT 中樞][ lnk-IoT Hub]接收到 hello 雲端 hello OPC 發行者模組從傳送的資料並使其可用 toohello Azure TSI 服務。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="a1ee0-174">hello 方案中的 hello IoT 中樞也：</span><span class="sxs-lookup"><span data-stu-id="a1ee0-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="a1ee0-175">會維護所有 OPC 發行者模組和所有 OPC Proxy 模組儲存 hello 識別碼的身分識別登錄。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="a1ee0-176">作為傳輸通道的 hello OPC 的 Proxy 模組的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="a1ee0-177">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="a1ee0-177">Azure Storage</span></span>
<span data-ttu-id="a1ee0-178">hello 解決方案會使用磁碟儲存體與 Azure blob 儲存體，hello 的 VM 和 toostore 部署的資料。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="a1ee0-179">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a1ee0-179">Web app</span></span>
<span data-ttu-id="a1ee0-180">hello web 應用程式部署為預先設定的 hello 方案的一部分包含整合式的 OPC UA 用戶端、 處理警示和遙測視覺效果。</span><span class="sxs-lookup"><span data-stu-id="a1ee0-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1ee0-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1ee0-181">Next steps</span></span>

<span data-ttu-id="a1ee0-182">您可以繼續閱讀下列文章 hello 入門 IoT 套件：</span><span class="sxs-lookup"><span data-stu-id="a1ee0-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="a1ee0-183">[Hello azureiotsuite.com 網站的權限][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="a1ee0-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="a1ee0-184">部署 Windows 或 Linux 上閘道連線的 hello factory 預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="a1ee0-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
