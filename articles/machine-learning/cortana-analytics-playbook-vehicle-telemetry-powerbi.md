---
title: "適用於車輛健全狀態與駕駛習慣的 Power BI 儀表板 - Azure | Microsoft Docs"
description: "使用 Cortana Intelligence 具備的強大功能，取得關於車輛健全狀態與駕駛習慣的即時預測情資。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: f880aceb1657ffdfe909b73f175b9673d9ab02cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="eaa1d-103">車輛遙測分析方案範本 Power BI 儀表板安裝指示</span><span class="sxs-lookup"><span data-stu-id="eaa1d-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="eaa1d-104">此 **功能表** 連結至此腳本的章節。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="eaa1d-105">「車輛遙測分析」方案示範汽車經銷商、汽車製造商和保險公司如何運用 Cortana Intelligence 功能，取得車輛健全狀態與駕駛習慣的即時預測情資，以改善客戶體驗、R&D 和行銷活動等方面。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="eaa1d-106">本文件包含在您的訂用帳戶中部署方案之後，如何設定 Power BI 報告和儀表板的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eaa1d-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="eaa1d-107">Prerequisites</span></span>
1. <span data-ttu-id="eaa1d-108">部署[遙測分析](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90)解決方案</span><span class="sxs-lookup"><span data-stu-id="eaa1d-108">Deploy the [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="eaa1d-109">安裝 Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="eaa1d-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="eaa1d-110">[Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="eaa1d-111">如果您沒有 Azure 訂用帳戶，請立即取得免費的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="eaa1d-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="eaa1d-112">Microsoft Power BI 帳戶</span><span class="sxs-lookup"><span data-stu-id="eaa1d-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="eaa1d-113">Cortana Intelligence Suite 元件</span><span class="sxs-lookup"><span data-stu-id="eaa1d-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="eaa1d-114">「車輛遙測分析」方案範本會在您的訂用帳戶中部署下列 Cortana Intelligence 服務。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="eaa1d-115">事件中樞可將數百萬計的車輛遙測事件擷取至 Azure。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="eaa1d-116">**串流分析** 」可取得關於車輛健全狀態的即時情資，同時以長期儲存的方式保存這些資料，供日後進行更豐富廣泛的批次分析之用。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="eaa1d-117">**機器學習服務** 」可即時進行異常偵測與批次處理以取得預測情資。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="eaa1d-118">**HDInsight** 用於大規模的資料轉換</span><span class="sxs-lookup"><span data-stu-id="eaa1d-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="eaa1d-119">**Data Factory** 可執行批次處理管線的協調、排程、資源管理和監控工作。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="eaa1d-120">**Power BI** 為此解決方案提供具備即時資料與預測性分析視覺效果等豐富功能的儀表板。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="eaa1d-121">此解決方案使用兩種不同的資料來源：**模擬車輛訊號和診斷資料集**與**車輛類別目錄**。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="eaa1d-122">此方案包含車輛遠程資訊服務模擬器。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="eaa1d-123">它會在指定時間點發出對應於車輛狀態與駕駛模式的診斷資訊和訊號。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="eaa1d-124">「車輛類別目錄」是包含 VIN 至車型對應的參考資料集</span><span class="sxs-lookup"><span data-stu-id="eaa1d-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="eaa1d-125">Power BI 儀表板準備</span><span class="sxs-lookup"><span data-stu-id="eaa1d-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="eaa1d-126">設定 Power BI 即時儀表板</span><span class="sxs-lookup"><span data-stu-id="eaa1d-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="eaa1d-127">啟動即時儀表板應用程式部署完成後，應遵循手動操作說明</span><span class="sxs-lookup"><span data-stu-id="eaa1d-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="eaa1d-128">下載即時儀表板應用程式 RealtimeDashboardApp.zip，並將它解壓縮。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="eaa1d-129">在解壓縮的資料夾中，開啟應用程式組態檔「RealtimeDashboardApp.exe.config」，並將事件中樞、Blob 儲存體及 ML 服務連線的 appsettings，更換為手動操作說明中的值，並儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="eaa1d-130">執行應用程式 RealtimeDashboardApp.exe。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="eaa1d-131">將顯示登入視窗，請提供您有效的 PowerBI 認證，然後按一下 [接受] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="eaa1d-132">應用程式將開始執行。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-132">Then the app will start to run.</span></span>

   ![登入 Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI 儀表板權限](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="eaa1d-135">登入 PowerBI 網站，並建立即時儀表板。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="eaa1d-136">現在，您可以使用豐富的視覺效果來設定 Power BI 儀表板，以取得車輛健全狀況和駕駛習慣的即時預測性情資。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="eaa1d-137">建立所有報告和設定儀表板大約需要 45 分鐘至一小時。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="eaa1d-138">設定 Power BI 報告</span><span class="sxs-lookup"><span data-stu-id="eaa1d-138">Configure Power BI reports</span></span>
<span data-ttu-id="eaa1d-139">即時報告和儀表板需要大約 30-45 分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="eaa1d-140">瀏覽至 [http://powerbi.com](http://powerbi.com) 並登入。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![登入 Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="eaa1d-142">Power BI 中會產生新的資料集。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="eaa1d-143">按一下 **ConnectedCarsRealtime** 資料集。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![選取連接的汽車即時資料集](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="eaa1d-145">使用 **Ctrl + s**儲存空白報告。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-145">Save the blank report using **Ctrl + s**.</span></span>

![儲存空白報告](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="eaa1d-147">提供報告名稱「車輛遙測分析即時 - 報告」 。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![提供報告名稱](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="eaa1d-149">即時報告</span><span class="sxs-lookup"><span data-stu-id="eaa1d-149">Real-time reports</span></span>
<span data-ttu-id="eaa1d-150">此解決方案有三份即時報告：</span><span class="sxs-lookup"><span data-stu-id="eaa1d-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="eaa1d-151">行駛中的車輛</span><span class="sxs-lookup"><span data-stu-id="eaa1d-151">Vehicles in operation</span></span>
2. <span data-ttu-id="eaa1d-152">需要維修的車輛</span><span class="sxs-lookup"><span data-stu-id="eaa1d-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="eaa1d-153">車輛健全狀況統計資料</span><span class="sxs-lookup"><span data-stu-id="eaa1d-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="eaa1d-154">您可以選擇設定上述三份即時報告，或在任何階段後停止並繼續進行設定批次報告的下一節。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="eaa1d-155">我們建議您建立上述三份報表，以將解決方案即時路徑的完整深入分析視覺化。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="eaa1d-156">1.行駛中的車輛</span><span class="sxs-lookup"><span data-stu-id="eaa1d-156">1. Vehicles in operation</span></span>
<span data-ttu-id="eaa1d-157">按兩下 [第 1 頁]，重新命名為「行駛中的車輛」</span><span class="sxs-lookup"><span data-stu-id="eaa1d-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="eaa1d-158">![Connected Cars - 行駛中的車輛](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="eaa1d-159">從 [欄位] 中選取 **vin** 欄位，然後選擇「卡片」做為視覺效果類型。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="eaa1d-160">建立的卡片視覺效果如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-160">Card visualization is created as shown in figure.</span></span>  
    ![Connected Cars - 選取 vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="eaa1d-162">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="eaa1d-163">從欄位中選取 **City** 和 **vin**。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="eaa1d-164">將視覺效果變更為「地圖」。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="eaa1d-165">將 **vin** 拖曳到值區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-165">Drag **vin** in values area.</span></span> <span data-ttu-id="eaa1d-166">從欄位中將 **city** 拖曳到 [圖例] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="eaa1d-167">![Connected Cars - 卡片視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="eaa1d-168">從 [視覺效果] 中選取 [格式] 區段，按一下 [標題]，將 [文字] 變更為**行駛中的車輛 (依城市)**。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="eaa1d-169">![Connected Cars - 行駛中的車輛 (依城市)](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="eaa1d-170">最終的視覺效果如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-170">Final visualization looks as shown in figure.</span></span>    
    ![Connected Cars - 最終視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="eaa1d-172">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="eaa1d-173">選取 **City** 和 **vin**，將視覺效果類型變更為「群組直條圖」。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="eaa1d-174">確定 **City** 欄位在 [軸] 區域，而 **vin** 在 [值] 區域</span><span class="sxs-lookup"><span data-stu-id="eaa1d-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="eaa1d-175">依 [vin 的計數] </span><span class="sxs-lookup"><span data-stu-id="eaa1d-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="eaa1d-176">![Connected Cars - vin 的計數](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="eaa1d-177">將圖表**標題**變更為「行駛中的車輛 (依城市)」</span><span class="sxs-lookup"><span data-stu-id="eaa1d-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="eaa1d-178">按一下 [格式] 區段，然後選取 [資料色彩]，按一下 [全部顯示] 的 [開啟]</span><span class="sxs-lookup"><span data-stu-id="eaa1d-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="eaa1d-179">![Connected Cars - 顯示所有資料色彩](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="eaa1d-180">按一下色彩圖示變更個別城市的色彩。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![Connected Cars - 變更色彩](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="eaa1d-182">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="eaa1d-183">從 [視覺效果] 中選取「群組直條圖」視覺效果，將 **city** 欄位拖曳到 [軸] 區域、將 **Model** 拖曳到 [圖例] 區域、將 **vin** 拖曳到 [值] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="eaa1d-184">![Connected Cars - 群組直條圖](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="eaa1d-185">![Connected Cars - 轉譯](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="eaa1d-186">重新排列此頁面上的所有視覺效果，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Connected Cars -視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="eaa1d-188">您已經成功設定「行駛中的車輛」即時報告。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="eaa1d-189">您可以繼續建立下一份即時報告，或在此停止並設定儀表板。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="eaa1d-190">2.需要維修的車輛</span><span class="sxs-lookup"><span data-stu-id="eaa1d-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="eaa1d-191">按一下 ![新增](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) 以加入新的報告，並重新命名為「需要維修的車輛」</span><span class="sxs-lookup"><span data-stu-id="eaa1d-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![Connected Cars - 需要維修的車輛](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="eaa1d-193">選取 **vin** 欄位，將視覺效果類型變更為「卡片」。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="eaa1d-194">![Connected Cars - Vin 卡片視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="eaa1d-195">我們在資料集中有一個名為 "MaintenanceLabel" 的欄位。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="eaa1d-196">此欄位的值可以是 “0” 或 “1”。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="eaa1d-197">它是由佈建為解決方案一部分並與即時路徑整合的 Azure Machine Learning 模型設定。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="eaa1d-198">值為 "1" 表示車輛需要維修。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="eaa1d-199">若要加入 [頁面層級]  篩選以顯示需要維修的車輛資料：</span><span class="sxs-lookup"><span data-stu-id="eaa1d-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="eaa1d-200">將 **"MaintenanceLabel"** 欄位拖曳到 [頁面層級篩選]。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="eaa1d-201">![Connected Cars - 頁面層級篩選](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="eaa1d-202">按一下 MaintenanceLabel 頁面層級篩選底部出現的 [基本篩選]  功能表。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="eaa1d-203">![Connected Cars - 基本篩選](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="eaa1d-204">將篩選值設為 **“1”**  </span><span class="sxs-lookup"><span data-stu-id="eaa1d-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="eaa1d-205">![Connected Cars - 篩選值](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="eaa1d-206">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="eaa1d-207">從 [視覺效果] 中選取「群組直條圖」</span><span class="sxs-lookup"><span data-stu-id="eaa1d-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="eaa1d-208">![Connected Cars - Vind 卡片視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="eaa1d-209">![Connected Cars - 群組直條圖](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="eaa1d-210">將 **Model** 欄位拖曳到 [軸] 區域，將 **Vin** 拖曳到 [值] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="eaa1d-211">然後，依 [vin 的計數] 排序視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="eaa1d-212">將圖表**標題**變更為「需要維修的車輛 (依車型)」</span><span class="sxs-lookup"><span data-stu-id="eaa1d-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="eaa1d-213">將 **vin** 欄位拖曳到 [視覺效果] 索引標籤的 [欄位] ![欄位](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) 區段上出現的 [色彩飽和度]</span><span class="sxs-lookup"><span data-stu-id="eaa1d-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="eaa1d-214">![Connected Cars - 色彩飽和度](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="eaa1d-215">從 [格式] 區段變更視覺效果中的 [資料色彩]</span><span class="sxs-lookup"><span data-stu-id="eaa1d-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="eaa1d-216">將最小值色彩變更為：**F2C812**</span><span class="sxs-lookup"><span data-stu-id="eaa1d-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="eaa1d-217">將最大值色彩變更為：**FF6300**</span><span class="sxs-lookup"><span data-stu-id="eaa1d-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="eaa1d-218">![Connected Cars - 色彩變更](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="eaa1d-219">![Connected Cars - 新的視覺效果色彩](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="eaa1d-220">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="eaa1d-221">從 [視覺效果] 中選取「群組直條圖」，將 **vin** 欄位拖曳到 [值] 區域，將 **City** 欄位拖曳到 [軸] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="eaa1d-222">依 [vin 的計數] 排序圖表。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="eaa1d-223">將圖表**標題**變更為「需要維修的車輛 (依城市)」 </span><span class="sxs-lookup"><span data-stu-id="eaa1d-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="eaa1d-224">![Connected Cars - 需要維修的車輛 (依城市)](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="eaa1d-225">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="eaa1d-226">從 [視覺效果] 中選取「多列卡片」視覺效果，將 **Model** 和 **vin** 拖曳到 [欄位] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="eaa1d-227">![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="eaa1d-228">重新排列所有視覺效果，最終報告看起來如下︰</span><span class="sxs-lookup"><span data-stu-id="eaa1d-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="eaa1d-230">您已經成功設定「需要維修的車輛」即時報告。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="eaa1d-231">您可以繼續建立下一份即時報告，或在此停止並設定儀表板。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="eaa1d-232">3.車輛健全狀況統計資料</span><span class="sxs-lookup"><span data-stu-id="eaa1d-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="eaa1d-233">按一下 ![新增](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) 以加入新的報告，並重新命名為「車輛健全狀況統計資料」</span><span class="sxs-lookup"><span data-stu-id="eaa1d-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="eaa1d-234">從 [視覺效果] 中選取「量測計」視覺效果，然後將 **Speed** 欄位拖曳到 [值]、[最小值]。[最大值] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="eaa1d-235">![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="eaa1d-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="eaa1d-236">將 [值] 區域中的 **speed** 預設彙總變更為 [平均值]</span><span class="sxs-lookup"><span data-stu-id="eaa1d-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="eaa1d-237">將 [最小值] 區域中的 **speed** 預設彙總變更為 [最小值]</span><span class="sxs-lookup"><span data-stu-id="eaa1d-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="eaa1d-238">將 [最大值] 區域中的 **speed** 預設彙總變更為 [最大值]</span><span class="sxs-lookup"><span data-stu-id="eaa1d-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="eaa1d-240">將 [量測計標題] 重新命名為「平均速度」</span><span class="sxs-lookup"><span data-stu-id="eaa1d-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![Connected Cars - 量測計](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="eaa1d-242">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="eaa1d-243">同樣地加入「平均機油」、「平均油量」和「平均引擎溫度」的**量測計**。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="eaa1d-244">依照上述「平均速度」  量測計中的步驟，變更每個量測計中各欄位的預設彙總。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Connected Cars - 量測計](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="eaa1d-246">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="eaa1d-247">從 [視覺效果] 中選取「折線與群組直條圖」，然後將 **City** 欄位拖曳到 [共用軸]，將 **speed**、將 **tirepressure 和 engineoil 欄位**拖曳到 [資料行值] 區域，將其彙總類型變更為 [平均值]。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="eaa1d-248">將 **engineTemperature** 欄位拖曳到 [折線圖值] 區域，將彙總類型變更為 [平均值]。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![Connected Cars -視覺效果欄位](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="eaa1d-250">將圖表**標題**變更為「平均速度、胎壓、機油和引擎溫度」。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Connected Cars -視覺效果欄位](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="eaa1d-252">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="eaa1d-253">從 [視覺效果] 中選取「樹狀圖」視覺效果，將 **Model** 欄位拖曳到 [群組] 區域，將 **MaintenanceProbability** 欄位拖曳到 [值] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="eaa1d-254">將圖表**標題**變更為「需要維修的車型」。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![Connected Cars - 變更圖表標題](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="eaa1d-256">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="eaa1d-257">從 [視覺效果] 中選取「100% 堆疊橫條圖」視覺效果，將 **city** 欄位拖曳到 [軸] 區域，將 **MaintenanceProbability**、**RecallProbability** 欄位拖曳到 [值] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![Connected Cars - 加入新的視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="eaa1d-259">按一下 [格式]，選取 [資料色彩]，並將 **MaintenanceProbability** 色彩設定為值 **"F2C80F"**。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="eaa1d-260">將圖表**標題**變更為「車輛維修和召回的機率 (依城市)」。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Connected Cars - 加入新的視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="eaa1d-262">按一下空白區域以加入新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="eaa1d-263">從 [視覺效果] 中選取「區域圖」視覺效果，將 **Model** 欄位拖曳到 [軸] 區域，將 **engineOil、tirepressure、speed 和 MaintenanceProbability** 欄位拖曳到 [值] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="eaa1d-264">將其彙總類型變更為 [平均值] 。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-264">Change their aggregation type to **“Average”**.</span></span> 

![Connected Cars - 變更彙總類型](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="eaa1d-266">將圖表的標題變更為「平均機油、胎壓、速度和維修機率 (依車型)」 。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Connected Cars - 變更圖表標題](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="eaa1d-268">按一下空白區域以加入新的視覺效果：</span><span class="sxs-lookup"><span data-stu-id="eaa1d-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="eaa1d-269">從 [視覺效果] 中選取「散佈圖」  視覺效果。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="eaa1d-270">將 **Model** 欄位拖曳到 [詳細資料] 和 [圖例] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="eaa1d-271">將 **fuel** 欄位拖曳到 [X 軸] 區域，將彙總變更為 [平均值]。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="eaa1d-272">將 **engineTemparature** 欄位拖曳到 [Y 軸] 區域，將彙總變更為 [平均值]</span><span class="sxs-lookup"><span data-stu-id="eaa1d-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="eaa1d-273">將 **vin** 欄位拖曳到 [大小] 區域。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-273">Drag the **vin** field into the **Size** area.</span></span>

![Connected Cars - 加入新的視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="eaa1d-275">將圖表**標題**變更為「燃料、引擎溫度的平均值 (依車型)」。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Connected Cars - 變更圖表標題](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="eaa1d-277">最終的報告顯示如下。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-277">The final report will look like as shown below.</span></span>

![Connected Cars - 最終報告](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="eaa1d-279">將報告中的視覺效果釘選到即時儀表板</span><span class="sxs-lookup"><span data-stu-id="eaa1d-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="eaa1d-280">按一下 [儀表板] 旁邊的加號圖示，以建立空白儀表板。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="eaa1d-281">您可以將它命名為「車輛遙測分析儀表板」</span><span class="sxs-lookup"><span data-stu-id="eaa1d-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Connected Cars - 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="eaa1d-283">將上述報告中的視覺效果釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![Connected Cars - 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="eaa1d-285">已建立上述三份報告並將對應的視覺效果釘選到儀表板時，儀表板應如下所示。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="eaa1d-286">如果您尚未建立所有報告，儀表板看起來可能有所不同。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![Connected Cars - 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="eaa1d-288">恭喜！</span><span class="sxs-lookup"><span data-stu-id="eaa1d-288">Congratulations!</span></span> <span data-ttu-id="eaa1d-289">您已成功建立即時儀表板。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="eaa1d-290">隨著您繼續執行 CarEventGenerator.exe 和 RealtimeDashboardApp.exe，您應該會在儀表板上看見即時更新。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="eaa1d-291">應該需要約 10 至 15 分鐘的時間才能完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="eaa1d-292">設定 Power BI 批次處理儀表板</span><span class="sxs-lookup"><span data-stu-id="eaa1d-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="eaa1d-293">端對端批次處理管線大約需要兩小時 (從成功完成部署開始算起) 的時間才能完成執行並處理一年份的已產生資料。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="eaa1d-294">因此請等處理完成後再繼續進行後續步驟。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="eaa1d-295">**下載 Power BI 設計工具檔案**</span><span class="sxs-lookup"><span data-stu-id="eaa1d-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="eaa1d-296">預先設定的 Power BI 設計工具檔案會包含於部署中 手動操作說明</span><span class="sxs-lookup"><span data-stu-id="eaa1d-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="eaa1d-297">尋找 2.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-297">Look for 2.</span></span> <span data-ttu-id="eaa1d-298">安裝 PowerBI 批次處理儀表板，您可以下載批次處理儀表板的 PowerBI 範本，在此稱為 ConnectedCarsPbiReport.pbix。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="eaa1d-299">儲存在本機</span><span class="sxs-lookup"><span data-stu-id="eaa1d-299">Save locally</span></span>

<span data-ttu-id="eaa1d-300">**設定 Power BI 報告**</span><span class="sxs-lookup"><span data-stu-id="eaa1d-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="eaa1d-301">使用 Power BI Desktop，開啟設計工具檔案「ConnectedCarsPbiReport.pbix」。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="eaa1d-302">如果您還沒有安裝 Power BI Desktop，請從 [Power BI Desktop 安裝](http://www.microsoft.com/download/details.aspx?id=45331)進行安裝。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="eaa1d-303">按一下 [編輯查詢] 。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-303">Click the **Edit Queries**.</span></span>

![編輯 Power BI 查詢](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="eaa1d-305">按兩下 [來源] 。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-305">Double-click the **Source**.</span></span>

![設定 Power BI 來源](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="eaa1d-307">以佈建為部署一部分的 Azure SQL Server 更新伺服器連接字串。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="eaa1d-308">在下列位置查看手動操作說明</span><span class="sxs-lookup"><span data-stu-id="eaa1d-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="eaa1d-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="eaa1d-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="eaa1d-310">伺服器︰somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="eaa1d-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="eaa1d-311">資料庫︰connectedcar</span><span class="sxs-lookup"><span data-stu-id="eaa1d-311">Database: connectedcar</span></span>
    * <span data-ttu-id="eaa1d-312">使用者名稱︰使用者名稱</span><span class="sxs-lookup"><span data-stu-id="eaa1d-312">Username: username</span></span>
    * <span data-ttu-id="eaa1d-313">密碼︰ 您可以從 Azure 入口網站管理您的 SQL 伺服器密碼</span><span class="sxs-lookup"><span data-stu-id="eaa1d-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="eaa1d-314">將 [資料庫]  保留為 *connectedcar*。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-314">Leave **Database** as *connectedcar*.</span></span>

![設定 Power BI 資料庫](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="eaa1d-316">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-316">Click **OK**.</span></span>
* <span data-ttu-id="eaa1d-317">依預設會選取 [Windows 認證] 索引標籤，請按一下右邊的 [資料庫] 索引標籤，將它變更為 [資料庫認證]。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="eaa1d-318">提供在 Azure SQL Database 部署安裝過程中提供的 [使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![提供資料庫認證](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="eaa1d-320">按一下 [連接] </span><span class="sxs-lookup"><span data-stu-id="eaa1d-320">Click **Connect**</span></span>
* <span data-ttu-id="eaa1d-321">針對右窗格中出現的其餘三個查詢各重複上述步驟，然後更新資料來源連接詳細資料。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="eaa1d-322">按一下 [關閉並載入] 。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-322">Click **Close and Load**.</span></span> <span data-ttu-id="eaa1d-323">Power BI Desktop 檔案資料集會連接到 SQL Azure 資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="eaa1d-324">**關閉** Power BI Desktop 檔案。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-324">**Close** Power BI Desktop file.</span></span>

![關閉 Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="eaa1d-326">按一下 [儲存]  按鈕以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="eaa1d-327">您現在已設定對應至解決方案中的批次處理路徑的所有報告。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="eaa1d-328">上傳至 *powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="eaa1d-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="eaa1d-329">瀏覽至 Power BI Web 入口網站 (http://powerbi.com) 並且登入。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="eaa1d-330">按一下 [取得資料] </span><span class="sxs-lookup"><span data-stu-id="eaa1d-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="eaa1d-331">上傳 Power BI Desktop 檔案。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="eaa1d-332">若要上傳，請按一下 [取得資料] -> [檔案取得]-> [本機檔案]</span><span class="sxs-lookup"><span data-stu-id="eaa1d-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="eaa1d-333">瀏覽至**「**ConnectedCarsPbiReport.pbix**」**</span><span class="sxs-lookup"><span data-stu-id="eaa1d-333">Navigate to the **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="eaa1d-334">一旦上傳檔案，將會瀏覽回到您的 Power BI 工作區。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="eaa1d-335">將會為您建立資料集、報告和空白儀表板。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="eaa1d-336">將圖表釘選至 Power BI 中的新儀表板，名稱為車輛遙測分析儀表板。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="eaa1d-337">按一下上面建立的空白儀表板，然後瀏覽至剛才上傳的報告上的 [報告]  區段。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![車輛遙測 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="eaa1d-339">**注意報告有六頁：**</span><span class="sxs-lookup"><span data-stu-id="eaa1d-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="eaa1d-340">第 1 頁︰車輛密度</span><span class="sxs-lookup"><span data-stu-id="eaa1d-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="eaa1d-341">第 2 頁︰即時車輛健全狀況</span><span class="sxs-lookup"><span data-stu-id="eaa1d-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="eaa1d-342">第 3 頁︰危險駕駛的車輛</span><span class="sxs-lookup"><span data-stu-id="eaa1d-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="eaa1d-343">第 4 頁︰召回的車輛</span><span class="sxs-lookup"><span data-stu-id="eaa1d-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="eaa1d-344">第 5 頁︰省油的車輛</span><span class="sxs-lookup"><span data-stu-id="eaa1d-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="eaa1d-345">第 6 頁︰Contoso 標誌</span><span class="sxs-lookup"><span data-stu-id="eaa1d-345">Page 6: Contoso Logo</span></span>  

![連接的車輛 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="eaa1d-347">**從第 3 頁**，釘選下列項目：</span><span class="sxs-lookup"><span data-stu-id="eaa1d-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="eaa1d-348">VIN 的計數</span><span class="sxs-lookup"><span data-stu-id="eaa1d-348">Count of VIN</span></span>  
   ![連接的車輛 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="eaa1d-350">危險駕駛的車輛 (依車型) – 瀑布圖 </span><span class="sxs-lookup"><span data-stu-id="eaa1d-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![車輛遙測 - 釘選圖表 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="eaa1d-352">**從第 5 頁**，釘選下列項目：</span><span class="sxs-lookup"><span data-stu-id="eaa1d-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="eaa1d-353">vin 的計數</span><span class="sxs-lookup"><span data-stu-id="eaa1d-353">Count of vin</span></span>    
   ![車輛遙測 - 釘選圖表 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="eaa1d-355">省油的車輛 (依車型)：群組直條圖 </span><span class="sxs-lookup"><span data-stu-id="eaa1d-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![車輛遙測 - 釘選圖表 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="eaa1d-357">**從第 4 頁**，釘選下列項目：</span><span class="sxs-lookup"><span data-stu-id="eaa1d-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="eaa1d-358">vin 的計數</span><span class="sxs-lookup"><span data-stu-id="eaa1d-358">Count of vin</span></span>  
   ![車輛遙測 - 釘選圖表 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="eaa1d-360">召回的車輛 (依城市、車型)：樹狀圖 </span><span class="sxs-lookup"><span data-stu-id="eaa1d-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![車輛遙測 - 釘選圖表 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="eaa1d-362">**從第 6 頁**，釘選下列項目：</span><span class="sxs-lookup"><span data-stu-id="eaa1d-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="eaa1d-363">Contoso Motors 標誌 </span><span class="sxs-lookup"><span data-stu-id="eaa1d-363">Contoso Motors logo</span></span>  
   ![車輛遙測 - 釘選圖表 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="eaa1d-365">**組織儀表板**</span><span class="sxs-lookup"><span data-stu-id="eaa1d-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="eaa1d-366">瀏覽至儀表板</span><span class="sxs-lookup"><span data-stu-id="eaa1d-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="eaa1d-367">將滑鼠暫留在每個圖表，根據下列完整儀表板影像中提供的名稱來重新命名。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="eaa1d-368">另外也將圖表排列成如下列儀表板所示。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![車輛遙測 - 組織儀表板 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![車輛遙測 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="eaa1d-371">如果您已建立本文件中提到的所有報報，則最終完成的儀表板應該看起來如下圖。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![車輛遙測 - 組織儀表板 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="eaa1d-373">恭喜！</span><span class="sxs-lookup"><span data-stu-id="eaa1d-373">Congratulations!</span></span> <span data-ttu-id="eaa1d-374">您已成功建立報報和儀表板，可取得車輛健全狀況和駕駛習慣的即時、預測和批次深入分析。</span><span class="sxs-lookup"><span data-stu-id="eaa1d-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
