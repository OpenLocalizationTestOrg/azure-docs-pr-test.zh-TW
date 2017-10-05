---
title: "Microsoft Azure IoT 套件概觀 | Microsoft Docs"
description: "大致說明 Azure IoT 套件如何提供物聯網預先設定的解決方案，以收集、分析和儲存資料、提供視覺效果，以及與其他系統整合。"
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
ms.openlocfilehash: bfa8dbbd0b1d943a9eb7a042df0bac25189d9ac9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="ccf7f-103">Azure IoT 套件的概觀</span><span class="sxs-lookup"><span data-stu-id="ccf7f-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="ccf7f-104">Azure 物聯網 (IoT) 服務提供廣泛的功能。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-104">The Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="ccf7f-105">這些企業等級的服務可讓您：</span><span class="sxs-lookup"><span data-stu-id="ccf7f-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="ccf7f-106">從裝置收集資料</span><span class="sxs-lookup"><span data-stu-id="ccf7f-106">Collect data from devices</span></span>
* <span data-ttu-id="ccf7f-107">分析移動中的資料串流</span><span class="sxs-lookup"><span data-stu-id="ccf7f-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="ccf7f-108">儲存和查詢大型資料集</span><span class="sxs-lookup"><span data-stu-id="ccf7f-108">Store and query large data sets</span></span>
* <span data-ttu-id="ccf7f-109">視覺化即時和歷程記錄資料</span><span class="sxs-lookup"><span data-stu-id="ccf7f-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="ccf7f-110">與後端辦公室系統整合</span><span class="sxs-lookup"><span data-stu-id="ccf7f-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="ccf7f-111">管理您的裝置</span><span class="sxs-lookup"><span data-stu-id="ccf7f-111">Manage your devices</span></span>

<span data-ttu-id="ccf7f-112">為了提供這些功能，Azure IoT 套件將多個 Azure 服務與自訂擴充功能封裝在一起作為「預先設定的解決方案」。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="ccf7f-113">這些預先設定的解決方案是常見 IoT 解決方案模式的基礎實作，可幫助您減少實行 IoT 解決方案所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="ccf7f-114">透過使用 [IoT 軟體開發套件][lnk-sdks]，您將可自訂和擴充這些解決方案來滿足您自己的需求。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-114">Using the [IoT software development kits][lnk-sdks], you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="ccf7f-115">您也可以使用這些解決方案作為開發新 IoT 解決方案時的範例或範本。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="ccf7f-116">下列影片提供 Azure IoT 套件的簡介：</span><span class="sxs-lookup"><span data-stu-id="ccf7f-116">The following video provides an introduction to Azure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="ccf7f-117">Azure IoT 套件中的 Azure IoT 服務</span><span class="sxs-lookup"><span data-stu-id="ccf7f-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="ccf7f-118">預先設定的解決方案通常使用下列服務：</span><span class="sxs-lookup"><span data-stu-id="ccf7f-118">The preconfigured solutions typically use the following services:</span></span>

* <span data-ttu-id="ccf7f-119">「Azure IoT 套件」的核心是 [Azure IoT 中樞][lnk-iot-hub]服務。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-119">Core to Azure IoT Suite is the [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="ccf7f-120">這項服務提供裝置到雲端和雲端到裝置的傳訊功能，並作為雲端到其他重要的 IoT 套件服務的閘道器。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-120">This service provides the device-to-cloud and cloud-to-device messaging capabilities and acts as the gateway to the cloud and the other key IoT Suite services.</span></span> <span data-ttu-id="ccf7f-121">此服務可讓您從您的裝置大量接收訊息，並將命令傳送給您的裝置。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-121">The service enables you to receive messages from your devices at scale, and send commands to your devices.</span></span> <span data-ttu-id="ccf7f-122">此服務還可讓您[管理您的裝置][lnk-device-management]。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-122">The service also enables you to [manage your devices][lnk-device-management].</span></span> <span data-ttu-id="ccf7f-123">例如，您可以在一或多個連接到中樞的裝置上，進行設定、重新啟動，或執行恢復出場預設值的作業。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected to the hub.</span></span>
* <span data-ttu-id="ccf7f-124">[Azure 串流分析][lnk-asa]提供移動中的資料分析。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="ccf7f-125">「IoT 套件」會使用這項服務來處理內送的遙測資料、執行彙總，以及偵測事件。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-125">IoT Suite uses this service to process incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="ccf7f-126">預先設定的解決方案也會使用串流分析來處理資訊訊息，它包含像是中繼資料或是從裝置回應的命令的資料。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-126">The preconfigured solutions also use stream analytics to process informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="ccf7f-127">這些解決方案使用「串流分析」來處理來自您裝置的訊息，並將這些訊息傳送給其他服務。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-127">The solutions use Stream Analytics to process the messages from your devices and deliver those messages to other services.</span></span>
* <span data-ttu-id="ccf7f-128">[Azure 儲存體][lnk-azure-storage]和 [Azure Cosmos DB][lnk-document-db] 提供資料儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide the data storage capabilities.</span></span> <span data-ttu-id="ccf7f-129">預先設定的解決方案使用 Blob 儲存體來儲存遙測，並且讓它可用於分析。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-129">The preconfigured solutions use blob storage to store telemetry and to make it available for analysis.</span></span> <span data-ttu-id="ccf7f-130">這些解決方案使用 Cosmos DB 來儲存裝置中繼資料，以及將解決方案的裝置管理功能啟用。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-130">The solutions use Cosmos DB to store device metadata and enable the device management capabilities of the solutions.</span></span>
* <span data-ttu-id="ccf7f-131">[Azure Web Apps][lnk-web-apps] 和 [Microsoft Power BI][lnk-power-bi] 提供資料視覺化功能。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide the data visualization capabilities.</span></span> <span data-ttu-id="ccf7f-132">Power BI 的彈性可讓您快速建置自己的互動式儀表板 (使用 IoT 套件資料)。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-132">The flexibility of Power BI enables you to quickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="ccf7f-133">如需典型 IoT 解決方案架構的概觀，請參閱 [Microsoft Azure 和物聯網 (IoT)][iot-suite-what-is-azure-iot]。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-133">For an overview of the architecture of a typical IoT solution, see [Microsoft Azure and the Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="ccf7f-134">預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="ccf7f-134">Preconfigured solutions</span></span>

<span data-ttu-id="ccf7f-135">「IoT 套件」包括預先設定的解決方案，可讓您快速開始使用及探索常見的 IoT 案例，例如：</span><span class="sxs-lookup"><span data-stu-id="ccf7f-135">IoT Suite includes preconfigured solutions that enable you to quickly get started with and to explore the common IoT scenarios, such as:</span></span>

* <span data-ttu-id="ccf7f-136">遠端監視</span><span class="sxs-lookup"><span data-stu-id="ccf7f-136">Remote monitoring</span></span>
* <span data-ttu-id="ccf7f-137">預測性維護</span><span class="sxs-lookup"><span data-stu-id="ccf7f-137">Predictive maintenance</span></span>
* <span data-ttu-id="ccf7f-138">連線的處理站</span><span class="sxs-lookup"><span data-stu-id="ccf7f-138">Connected factory</span></span>

<span data-ttu-id="ccf7f-139">您可以將這些解決方案部署到您的 Azure 訂用帳戶，然後執行完整的端對端 IoT 案例。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-139">You can deploy these solutions to your Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccf7f-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ccf7f-140">Next steps</span></span>

<span data-ttu-id="ccf7f-141">既然您已概略了解「IoT 套件」的功能及其主要元件，您現在可以深入了解「IoT 套件」中預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="ccf7f-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about the preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="ccf7f-142">如需詳細資訊，請參閱[什麼是 Azure IoT 套件預先設定的解決方案？][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="ccf7f-142">For more information, see [What are the Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

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
