---
title: "aaaMicrosoft Azure IoT 套件概觀 |Microsoft 文件"
description: "Azure IoT 套件如何傳遞的項目預先設定的解決方案 toocollect，網際網路概觀分析，和儲存資料、 提供視覺效果，並與其他系統整合。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="43d8e-103">Azure IoT 套件的概觀</span><span class="sxs-lookup"><span data-stu-id="43d8e-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="43d8e-104">hello 的項目 (IoT) 服務的 Azure 網際網路提供廣泛的功能。</span><span class="sxs-lookup"><span data-stu-id="43d8e-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="43d8e-105">這些企業等級的服務可讓您：</span><span class="sxs-lookup"><span data-stu-id="43d8e-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="43d8e-106">從裝置收集資料</span><span class="sxs-lookup"><span data-stu-id="43d8e-106">Collect data from devices</span></span>
* <span data-ttu-id="43d8e-107">分析移動中的資料串流</span><span class="sxs-lookup"><span data-stu-id="43d8e-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="43d8e-108">儲存和查詢大型資料集</span><span class="sxs-lookup"><span data-stu-id="43d8e-108">Store and query large data sets</span></span>
* <span data-ttu-id="43d8e-109">視覺化即時和歷程記錄資料</span><span class="sxs-lookup"><span data-stu-id="43d8e-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="43d8e-110">與後端辦公室系統整合</span><span class="sxs-lookup"><span data-stu-id="43d8e-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="43d8e-111">管理您的裝置</span><span class="sxs-lookup"><span data-stu-id="43d8e-111">Manage your devices</span></span>

<span data-ttu-id="43d8e-112">toodeliver 這些功能，Azure IoT 套件一起封裝以做為自訂延伸模組的多個 Azure 服務*預先設定的解決方案*。</span><span class="sxs-lookup"><span data-stu-id="43d8e-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="43d8e-113">這些預先設定的解決方案是常見的 IoT 解決方案模式可協助您採取 toodeliver IoT 解決方案 tooreduce hello 時間的基底實作。</span><span class="sxs-lookup"><span data-stu-id="43d8e-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="43d8e-114">使用 hello [IoT 軟體開發套件][lnk-sdks]，您可以自訂及擴充這些解決方案 toomeet 您自己的需求。</span><span class="sxs-lookup"><span data-stu-id="43d8e-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="43d8e-115">您也可以使用這些解決方案作為開發新 IoT 解決方案時的範例或範本。</span><span class="sxs-lookup"><span data-stu-id="43d8e-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="43d8e-116">hello 下列影片提供簡介 tooAzure IoT 套件：</span><span class="sxs-lookup"><span data-stu-id="43d8e-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="43d8e-117">Azure IoT 套件中的 Azure IoT 服務</span><span class="sxs-lookup"><span data-stu-id="43d8e-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="43d8e-118">預先設定的 hello 解決方案通常是使用下列服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="43d8e-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="43d8e-119">核心 tooAzure IoT 套件為 hello [Azure IoT 中樞][ lnk-iot-hub]服務。</span><span class="sxs-lookup"><span data-stu-id="43d8e-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="43d8e-120">此服務會提供 hello 裝置的雲端和雲端到裝置訊息功能是做為 hello 閘道 toohello 雲端和 hello 其他索引鍵的 IoT Suite 服務。</span><span class="sxs-lookup"><span data-stu-id="43d8e-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="43d8e-121">hello 服務可讓您從您的裝置在標尺，tooreceive 訊息，並將命令傳送 tooyour 裝置。</span><span class="sxs-lookup"><span data-stu-id="43d8e-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="43d8e-122">hello 服務也可讓您太[管理您的裝置][lnk-device-management]。</span><span class="sxs-lookup"><span data-stu-id="43d8e-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="43d8e-123">例如，您可以設定、 重新開機，或為原廠重設一或多個裝置連線的 toohello 集線器上。</span><span class="sxs-lookup"><span data-stu-id="43d8e-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="43d8e-124">[Azure 串流分析][lnk-asa]提供移動中的資料分析。</span><span class="sxs-lookup"><span data-stu-id="43d8e-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="43d8e-125">IoT 套件會使用此服務 tooprocess 傳入遙測、 執行彙總，以及偵測到事件。</span><span class="sxs-lookup"><span data-stu-id="43d8e-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="43d8e-126">預先設定的 hello 解決方案也使用資料流分析 tooprocess 參考用訊息包含資料，例如從裝置的中繼資料或命令的回應。</span><span class="sxs-lookup"><span data-stu-id="43d8e-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="43d8e-127">hello 解決方案會使用資料流分析 tooprocess hello 訊息，從您的裝置，並將這些訊息傳遞 tooother 服務。</span><span class="sxs-lookup"><span data-stu-id="43d8e-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="43d8e-128">[Azure 儲存體][ lnk-azure-storage]和[Azure Cosmos DB] [ lnk-document-db]提供 hello 資料儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="43d8e-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="43d8e-129">hello 預先設定的解決方案使用 blob 儲存體 toostore 遙測和 toomake 它可用於分析。</span><span class="sxs-lookup"><span data-stu-id="43d8e-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="43d8e-130">hello 解決方案使用 Cosmos DB toostore 裝置中繼資料，並啟用 hello 解決方案 hello 裝置管理功能。</span><span class="sxs-lookup"><span data-stu-id="43d8e-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="43d8e-131">[Azure Web Apps] [ lnk-web-apps]和[Microsoft Power BI] [ lnk-power-bi]提供 hello 資料視覺效果功能。</span><span class="sxs-lookup"><span data-stu-id="43d8e-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="43d8e-132">hello 彈性的 Power BI 可讓您 tooquickly 建置您自己使用 IoT 套件資料的互動式儀表板。</span><span class="sxs-lookup"><span data-stu-id="43d8e-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="43d8e-133">典型的 IoT 解決方案的 hello 架構的概觀，請參閱[Microsoft Azure 與 hello 物聯網 (IoT)][iot-suite-what-is-azure-iot]。</span><span class="sxs-lookup"><span data-stu-id="43d8e-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="43d8e-134">預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="43d8e-134">Preconfigured solutions</span></span>

<span data-ttu-id="43d8e-135">IoT 套件包含預先設定的解決方案，啟用您 tooquickly 開始使用和 tooexplore hello 常見 IoT 案例中，例如：</span><span class="sxs-lookup"><span data-stu-id="43d8e-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="43d8e-136">遠端監視</span><span class="sxs-lookup"><span data-stu-id="43d8e-136">Remote monitoring</span></span>
* <span data-ttu-id="43d8e-137">預測性維護</span><span class="sxs-lookup"><span data-stu-id="43d8e-137">Predictive maintenance</span></span>
* <span data-ttu-id="43d8e-138">連線的處理站</span><span class="sxs-lookup"><span data-stu-id="43d8e-138">Connected factory</span></span>

<span data-ttu-id="43d8e-139">您可以部署這些方案 tooyour Azure 訂用帳戶，然後再執行完整的端對端的 IoT 案例。</span><span class="sxs-lookup"><span data-stu-id="43d8e-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43d8e-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43d8e-140">Next steps</span></span>

<span data-ttu-id="43d8e-141">您已經有 IoT 套件可以做什麼，以及其主要元件的概觀，您可以深入了解 IoT 套件中的 hello 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="43d8e-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="43d8e-142">如需詳細資訊，請參閱[為何 hello Azure IoT 預先設定的解決方案嗎？][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="43d8e-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
