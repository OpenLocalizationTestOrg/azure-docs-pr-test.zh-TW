---
title: "aaaPredict vehicle 健全狀況和驅動習慣-Azure |Microsoft 文件"
description: "一種載具，健全狀況使用 Cortana 智慧 toogain 即時和預測 insights hello 功能和驅動習慣。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="470cc-103">車輛遙測分析解決方案腳本</span><span class="sxs-lookup"><span data-stu-id="470cc-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="470cc-104">這**功能表**連結 toohello 章節，在這個腳本中的。</span><span class="sxs-lookup"><span data-stu-id="470cc-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="470cc-105">概觀</span><span class="sxs-lookup"><span data-stu-id="470cc-105">Overview</span></span>
<span data-ttu-id="470cc-106">超級電腦都移出 hello 實驗室，而且現在會保存在我們機庫 ！</span><span class="sxs-lookup"><span data-stu-id="470cc-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="470cc-107">這些尖端汽車包含各種感應器，提供它們 hello 能力 tootrack 和監視每秒數以百萬計的事件。</span><span class="sxs-lookup"><span data-stu-id="470cc-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="470cc-108">我們預期的由 2020，大部分的這些車輛將已經連接的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="470cc-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="470cc-109">想像一下接通這些豐富的資料 tooprovide 更安全、 可靠性及驅動更好的體驗 ！</span><span class="sxs-lookup"><span data-stu-id="470cc-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="470cc-110">Microsoft 透過 Cortana Intelligence 讓此一美好想像成真。</span><span class="sxs-lookup"><span data-stu-id="470cc-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="470cc-111">Microsoft 的 Cortana 智慧是完全受管理的巨量資料，並為智慧型動作 advanced analytics suite，可讓您 tootransform 您的資料。</span><span class="sxs-lookup"><span data-stu-id="470cc-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="470cc-112">我們希望 toointroduce toohello Cortana 智慧 Vehicle 遙測分析方案範本。</span><span class="sxs-lookup"><span data-stu-id="470cc-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="470cc-113">這個解決方案示範了如何汽車經銷商、 汽車的製造商和保險的公司可以使用 Cortana 智慧 toogain 即時 hello 功能及預測的洞察能力 vehicle 健全狀況和驅動習慣。</span><span class="sxs-lookup"><span data-stu-id="470cc-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="470cc-114">hello 方案會實作為[lambda 架構模式](https://en.wikipedia.org/wiki/Lambda_architecture)顯示 hello 潛力 hello Cortana 智慧平台的即時和批次處理。</span><span class="sxs-lookup"><span data-stu-id="470cc-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="470cc-115">hello 解決方案：</span><span class="sxs-lookup"><span data-stu-id="470cc-115">hello solution:</span></span> 

* <span data-ttu-id="470cc-116">提供車輛遠程資訊服務模擬器</span><span class="sxs-lookup"><span data-stu-id="470cc-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="470cc-117">運用事件中樞，以將數百萬計的模擬車輛遙測事件擷取至 Azure</span><span class="sxs-lookup"><span data-stu-id="470cc-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="470cc-118">使用資料流分析 toogain 即時 insights vehicle 健全狀況</span><span class="sxs-lookup"><span data-stu-id="470cc-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="470cc-119">hello 資料保存到更豐富的批次分析的長期的儲存體。</span><span class="sxs-lookup"><span data-stu-id="470cc-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="470cc-120">利用機器學習中的異常偵測的即時和批次處理處理 toogain 預測深入資訊。</span><span class="sxs-lookup"><span data-stu-id="470cc-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="470cc-121">會利用在標尺和 Data Factory toohandle 協調流程、 排程、 資源管理及監視 hello 批次處理管線的 HDInsight tootransform 資料</span><span class="sxs-lookup"><span data-stu-id="470cc-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="470cc-122">使用 Power BI 為此解決方案提供一個豐富的儀表板，來提供即時資料和預測性分析視覺效果</span><span class="sxs-lookup"><span data-stu-id="470cc-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="470cc-123">架構</span><span class="sxs-lookup"><span data-stu-id="470cc-123">Architecture</span></span>
<span data-ttu-id="470cc-124">![解決方案架構圖表](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*圖 1 – 車輛遙測分析解決方案架構*</span><span class="sxs-lookup"><span data-stu-id="470cc-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="470cc-125">此解決方案包括 hello 下列**Cortana 智慧元件**並展示其結束 tooend 整合：</span><span class="sxs-lookup"><span data-stu-id="470cc-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="470cc-126">**事件中樞** 可將數百萬計的車輛遙測事件擷取至 Azure。</span><span class="sxs-lookup"><span data-stu-id="470cc-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="470cc-127">**串流分析** 」可取得關於車輛健全狀態的即時情資，同時以長期儲存的方式保存這些資料，供日後進行更豐富廣泛的批次分析之用。</span><span class="sxs-lookup"><span data-stu-id="470cc-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="470cc-128">**機器學習**以便進行異常偵測即時和批次處理 toogain 預測的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="470cc-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="470cc-129">**HDInsight**運用 tootransform 大規模的資料</span><span class="sxs-lookup"><span data-stu-id="470cc-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="470cc-130">**Data Factory**處理協調流程排程、 資源管理和監視 hello 批次處理管線。</span><span class="sxs-lookup"><span data-stu-id="470cc-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="470cc-131">**Power BI** 為此解決方案提供具備即時資料與預測性分析視覺效果等豐富功能的儀表板。</span><span class="sxs-lookup"><span data-stu-id="470cc-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="470cc-132">此解決方案可存取兩種不同的 **資料來源**：</span><span class="sxs-lookup"><span data-stu-id="470cc-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="470cc-133">**模擬 vehicle 訊號和診斷**: vehicle 車用通訊模擬器會發出診斷資訊，並對應 toohello 狀態 hello vehicle 和 hello 推動特定時點的模式，時間的訊號。</span><span class="sxs-lookup"><span data-stu-id="470cc-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="470cc-134">**一種載具，目錄**： 包含 VIN toomodel 對應的參考資料集。</span><span class="sxs-lookup"><span data-stu-id="470cc-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

