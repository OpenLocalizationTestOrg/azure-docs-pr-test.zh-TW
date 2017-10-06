---
title: "一種載具，健全狀況和驅動 aaaPower BI 儀表板習慣-Azure |Microsoft 文件"
description: "一種載具，健全狀況使用 Cortana 智慧 toogain 即時和預測 insights hello 功能和驅動習慣。"
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
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="708fe-103">車輛遙測分析方案範本 Power BI 儀表板安裝指示</span><span class="sxs-lookup"><span data-stu-id="708fe-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="708fe-104">這**功能表**連結 toohello 章節，在這個腳本中的。</span><span class="sxs-lookup"><span data-stu-id="708fe-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="708fe-105">hello Vehicle 遙測分析解決方案示範汽車經銷商、 汽車的製造商和保險的公司可以利用 Cortana 智慧 toogain 即時和預測一種載具，健全狀況和洞察開車 hello 功能習慣 toodrive 改進 hello 區域中的客戶體驗，R&d 與行銷活動。</span><span class="sxs-lookup"><span data-stu-id="708fe-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="708fe-106">本文件包含逐步指示如何設定 hello Power BI 報表和儀表板一旦 hello 方案會部署您的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="708fe-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="708fe-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="708fe-107">Prerequisites</span></span>
1. <span data-ttu-id="708fe-108">部署 hello[遙測分析](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90)方案</span><span class="sxs-lookup"><span data-stu-id="708fe-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="708fe-109">安裝 Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="708fe-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="708fe-110">[Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="708fe-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="708fe-111">如果您沒有 Azure 訂用帳戶，請立即取得免費的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="708fe-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="708fe-112">Microsoft Power BI 帳戶</span><span class="sxs-lookup"><span data-stu-id="708fe-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="708fe-113">Cortana Intelligence Suite 元件</span><span class="sxs-lookup"><span data-stu-id="708fe-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="708fe-114">Hello Vehicle 遙測分析解決方案範本的一部分，hello 遵循 Cortana 智慧服務會部署在您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="708fe-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="708fe-115">事件中樞可將數百萬計的車輛遙測事件擷取至 Azure。</span><span class="sxs-lookup"><span data-stu-id="708fe-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="708fe-116">**串流分析** 」可取得關於車輛健全狀態的即時情資，同時以長期儲存的方式保存這些資料，供日後進行更豐富廣泛的批次分析之用。</span><span class="sxs-lookup"><span data-stu-id="708fe-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="708fe-117">**機器學習**以便進行異常偵測即時和批次處理 toogain 預測的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="708fe-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="708fe-118">**HDInsight**運用 tootransform 大規模的資料</span><span class="sxs-lookup"><span data-stu-id="708fe-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="708fe-119">**Data Factory**處理協調流程排程、 資源管理和監視 hello 批次處理管線。</span><span class="sxs-lookup"><span data-stu-id="708fe-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="708fe-120">**Power BI** 為此解決方案提供具備即時資料與預測性分析視覺效果等豐富功能的儀表板。</span><span class="sxs-lookup"><span data-stu-id="708fe-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="708fe-121">hello 解決方案會使用兩個不同的資料來源：**模擬 vehicle 訊號和診斷的資料集**和**vehicle 目錄**。</span><span class="sxs-lookup"><span data-stu-id="708fe-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="708fe-122">此方案包含車輛遠程資訊服務模擬器。</span><span class="sxs-lookup"><span data-stu-id="708fe-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="708fe-123">它會發出診斷資訊，並告知對應 toohello 狀態 hello vehicle 和推動模式特定時點的時間。</span><span class="sxs-lookup"><span data-stu-id="708fe-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="708fe-124">hello Vehicle 目錄是參考資料集包含 VIN toomodel 對應</span><span class="sxs-lookup"><span data-stu-id="708fe-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="708fe-125">Power BI 儀表板準備</span><span class="sxs-lookup"><span data-stu-id="708fe-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="708fe-126">設定 Power BI 即時儀表板</span><span class="sxs-lookup"><span data-stu-id="708fe-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="708fe-127">**啟動 hello 即時儀表板應用程式**hello 部署完成後，您應該遵循 hello 手動操作說明</span><span class="sxs-lookup"><span data-stu-id="708fe-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="708fe-128">下載即時儀表板應用程式 RealtimeDashboardApp.zip，並將它解壓縮。</span><span class="sxs-lookup"><span data-stu-id="708fe-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="708fe-129">在 hello 解壓縮資料夾中，開啟 應用程式組態檔 'RealtimeDashboardApp.exe.config'，取代 appSettings Eventhub、 Blob 儲存體和 ML 服務使用的連線 hello 值在 hello 手動操作的指示，和儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="708fe-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="708fe-130">執行應用程式 RealtimeDashboardApp.exe。</span><span class="sxs-lookup"><span data-stu-id="708fe-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="708fe-131">登入視窗會快顯，提供有效的 power Bi 認證，然後按一下 hello**接受** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="708fe-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="708fe-132">然後 toorun 會啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="708fe-132">Then hello app will start toorun.</span></span>

   ![登入 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI 儀表板權限](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="708fe-135">登入 tooPowerBI 網站，並建立即時儀表板。</span><span class="sxs-lookup"><span data-stu-id="708fe-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="708fe-136">現在，您準備好 tooconfigure hello Power BI 儀表板具有豐富視覺效果 toogain 即時而且預測的洞察能力 vehicle 健全狀況和驅動習慣。</span><span class="sxs-lookup"><span data-stu-id="708fe-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="708fe-137">它會採用約 45 分鐘內 tooan 小時 toocreate 所有 hello 報告，並設定 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="708fe-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="708fe-138">設定 Power BI 報告</span><span class="sxs-lookup"><span data-stu-id="708fe-138">Configure Power BI reports</span></span>
<span data-ttu-id="708fe-139">hello 即時報表和 hello 儀表板花費 30-45 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="708fe-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="708fe-140">瀏覽過[http://powerbi.com](http://powerbi.com)與登入。</span><span class="sxs-lookup"><span data-stu-id="708fe-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![登入 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="708fe-142">Power BI 中會產生新的資料集。</span><span class="sxs-lookup"><span data-stu-id="708fe-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="708fe-143">按一下 hello **ConnectedCarsRealtime**資料集。</span><span class="sxs-lookup"><span data-stu-id="708fe-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![選取連接的汽車即時資料集](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="708fe-145">儲存 hello 空白報表使用**Ctrl + s**。</span><span class="sxs-lookup"><span data-stu-id="708fe-145">Save hello blank report using **Ctrl + s**.</span></span>

![儲存空白報告](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="708fe-147">提供報告名稱「車輛遙測分析即時 - 報告」 。</span><span class="sxs-lookup"><span data-stu-id="708fe-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![提供報告名稱](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="708fe-149">即時報告</span><span class="sxs-lookup"><span data-stu-id="708fe-149">Real-time reports</span></span>
<span data-ttu-id="708fe-150">此解決方案有三份即時報告：</span><span class="sxs-lookup"><span data-stu-id="708fe-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="708fe-151">行駛中的車輛</span><span class="sxs-lookup"><span data-stu-id="708fe-151">Vehicles in operation</span></span>
2. <span data-ttu-id="708fe-152">需要維修的車輛</span><span class="sxs-lookup"><span data-stu-id="708fe-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="708fe-153">車輛健全狀況統計資料</span><span class="sxs-lookup"><span data-stu-id="708fe-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="708fe-154">您可以選擇 tooconfigure 所有三個即時報表 hello 或在任何階段後停止，然後繼續進行的設定 hello 批次報表 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="708fe-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="708fe-155">我們建議您所有的 toocreate hello 三報告 toovisualize hello 完整 insights 的 hello 方案 hello 即時路徑。</span><span class="sxs-lookup"><span data-stu-id="708fe-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="708fe-156">1.行駛中的車輛</span><span class="sxs-lookup"><span data-stu-id="708fe-156">1. Vehicles in operation</span></span>
<span data-ttu-id="708fe-157">按兩下**第 1 頁**並將它重新命名過"車輛作業中的"</span><span class="sxs-lookup"><span data-stu-id="708fe-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="708fe-158">![Connected Cars - 行駛中的車輛](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="708fe-159">從 [欄位] 中選取 **vin** 欄位，然後選擇「卡片」做為視覺效果類型。</span><span class="sxs-lookup"><span data-stu-id="708fe-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="708fe-160">建立的卡片視覺效果如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="708fe-160">Card visualization is created as shown in figure.</span></span>  
    ![Connected Cars - 選取 vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="708fe-162">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="708fe-163">從欄位中選取 **City** 和 **vin**。</span><span class="sxs-lookup"><span data-stu-id="708fe-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="708fe-164">變更視覺效果太**「 對應 」**。</span><span class="sxs-lookup"><span data-stu-id="708fe-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="708fe-165">將 **vin** 拖曳到值區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-165">Drag **vin** in values area.</span></span> <span data-ttu-id="708fe-166">拖曳**縣 （市)**欄位太**圖例**區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="708fe-167">![Connected Cars - 卡片視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="708fe-168">選取**格式**> 一節**視覺效果**，按一下 **標題**並變更 hello**文字**太**"車輛中依城市的作業 」**。</span><span class="sxs-lookup"><span data-stu-id="708fe-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="708fe-169">![Connected Cars - 行駛中的車輛 (依城市)](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="708fe-170">最終的視覺效果如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="708fe-170">Final visualization looks as shown in figure.</span></span>    
    ![Connected Cars - 最終視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="708fe-172">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="708fe-173">選取**縣 （市)**和**vin**，視覺效果類型變更太**群組直條圖**。</span><span class="sxs-lookup"><span data-stu-id="708fe-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="708fe-174">確定 **City** 欄位在 [軸] 區域，而 **vin** 在 [值] 區域</span><span class="sxs-lookup"><span data-stu-id="708fe-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="708fe-175">依 [vin 的計數] </span><span class="sxs-lookup"><span data-stu-id="708fe-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="708fe-176">![Connected Cars - vin 的計數](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="708fe-177">變更圖表**標題**太**」 作業依城市中的車輛"**</span><span class="sxs-lookup"><span data-stu-id="708fe-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="708fe-178">按一下 hello**格式**區段，然後選取 **資料色彩**，按一下 hello **「 On 」**太**全部顯示**</span><span class="sxs-lookup"><span data-stu-id="708fe-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="708fe-179">![Connected Cars - 顯示所有資料色彩](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="708fe-180">變更個別的城市 hello 色彩，色彩圖示即可。</span><span class="sxs-lookup"><span data-stu-id="708fe-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![Connected Cars - 變更色彩](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="708fe-182">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="708fe-183">從 [視覺效果] 中選取「群組直條圖」視覺效果，將 **city** 欄位拖曳到 [軸] 區域、將 **Model** 拖曳到 [圖例] 區域、將 **vin** 拖曳到 [值] 區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="708fe-184">![Connected Cars - 群組直條圖](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="708fe-185">![Connected Cars - 轉譯](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="708fe-186">重新排列此頁面上的所有視覺效果，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="708fe-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Connected Cars -視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="708fe-188">您已成功設定 hello"車輛作業中的"即時報表。</span><span class="sxs-lookup"><span data-stu-id="708fe-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="708fe-189">您可以繼續 toocreate hello 下一步，即時報表或在此停止，以及設定 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="708fe-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="708fe-190">2.需要維修的車輛</span><span class="sxs-lookup"><span data-stu-id="708fe-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="708fe-191">按一下![新增](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png)tooadd 新的報表，將它重新命名過**「 車輛需要維護 」**</span><span class="sxs-lookup"><span data-stu-id="708fe-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![Connected Cars - 需要維修的車輛](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="708fe-193">選取**vin**欄位和視覺效果類型變更太**卡**。</span><span class="sxs-lookup"><span data-stu-id="708fe-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="708fe-194">![Connected Cars - Vin 卡片視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="708fe-195">我們有 hello 資料集中名為"MaintenanceLabel"的欄位。</span><span class="sxs-lookup"><span data-stu-id="708fe-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="708fe-196">此欄位的值可以是 “0” 或 “1”。</span><span class="sxs-lookup"><span data-stu-id="708fe-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="708fe-197">它會設定由佈建為方案的一部分，而且與 hello 即時路徑整合 hello Azure 機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="708fe-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="708fe-198">hello 值"1"表示一種載具，需要維護。</span><span class="sxs-lookup"><span data-stu-id="708fe-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="708fe-199">tooadd**頁面層級**顯示需要維護的車輛資料篩選條件：</span><span class="sxs-lookup"><span data-stu-id="708fe-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="708fe-200">拖曳 hello **"MaintenanceLabel"**欄位到**頁面層級篩選**。</span><span class="sxs-lookup"><span data-stu-id="708fe-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="708fe-201">![Connected Cars - 頁面層級篩選](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="708fe-202">按一下 MaintenanceLabel 頁面層級篩選底部出現的 [基本篩選]  功能表。</span><span class="sxs-lookup"><span data-stu-id="708fe-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="708fe-203">![Connected Cars - 基本篩選](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="708fe-204">設定其篩選值太**"1"**  </span><span class="sxs-lookup"><span data-stu-id="708fe-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="708fe-205">![Connected Cars - 篩選值](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="708fe-206">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="708fe-207">從 [視覺效果] 中選取「群組直條圖」</span><span class="sxs-lookup"><span data-stu-id="708fe-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="708fe-208">![Connected Cars - Vind 卡片視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="708fe-209">![Connected Cars - 群組直條圖](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="708fe-210">拖曳欄位**模型**到**軸**區域中， **Vin**太**值**區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="708fe-211">然後，依 [vin 的計數] 排序視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="708fe-212">變更圖表**標題**太**"車輛模型需要維護 」**</span><span class="sxs-lookup"><span data-stu-id="708fe-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="708fe-213">將 **vin** 欄位拖曳到 [視覺效果] 索引標籤的 [欄位] ![欄位](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) 區段上出現的 [色彩飽和度]</span><span class="sxs-lookup"><span data-stu-id="708fe-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="708fe-214">![Connected Cars - 色彩飽和度](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="708fe-215">從 [格式] 區段變更視覺效果中的 [資料色彩]</span><span class="sxs-lookup"><span data-stu-id="708fe-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="708fe-216">將最小值色彩變更為：**F2C812**</span><span class="sxs-lookup"><span data-stu-id="708fe-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="708fe-217">將最大值色彩變更為：**FF6300**</span><span class="sxs-lookup"><span data-stu-id="708fe-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="708fe-218">![Connected Cars - 色彩變更](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="708fe-219">![Connected Cars - 新的視覺效果色彩](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="708fe-220">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="708fe-221">從 [視覺效果] 中選取「群組直條圖」，將 **vin** 欄位拖曳到 [值] 區域，將 **City** 欄位拖曳到 [軸] 區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="708fe-222">依 [vin 的計數] 排序圖表。</span><span class="sxs-lookup"><span data-stu-id="708fe-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="708fe-223">變更圖表**標題**太**"車輛需要維護縣 （市） 」** </span><span class="sxs-lookup"><span data-stu-id="708fe-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="708fe-224">![Connected Cars - 需要維修的車輛 (依城市)](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="708fe-225">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="708fe-226">選取**多列卡片**視覺效果，從視覺效果拖曳**模型**和**vin**到 hello**欄位**區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="708fe-227">![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="708fe-228">重新整理所有 hello 視覺效果，hello 最終報表看都起來如下：</span><span class="sxs-lookup"><span data-stu-id="708fe-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="708fe-230">您已成功設定 hello"車輛需要 Maintenance"即時報表。</span><span class="sxs-lookup"><span data-stu-id="708fe-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="708fe-231">您可以繼續 toocreate hello 下一步，即時報表或在此停止，以及設定 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="708fe-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="708fe-232">3.車輛健全狀況統計資料</span><span class="sxs-lookup"><span data-stu-id="708fe-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="708fe-233">按一下![新增](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png)tooadd 新報表、 將它重新命名過**"車輛健全狀況統計資料 」**</span><span class="sxs-lookup"><span data-stu-id="708fe-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="708fe-234">選取**量測計**視覺效果從視覺效果，然後將拖曳 hello**速度**欄位到**值、 最小值，最大值**區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="708fe-235">![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="708fe-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="708fe-236">變更 hello 預設彙總的**速度**中**值區域**太**平均**</span><span class="sxs-lookup"><span data-stu-id="708fe-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="708fe-237">變更 hello 預設彙總的**速度**中**最小值 區域**太**最小值**</span><span class="sxs-lookup"><span data-stu-id="708fe-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="708fe-238">變更 hello 預設彙總的**速度**中**最大值區**太**上限**</span><span class="sxs-lookup"><span data-stu-id="708fe-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![Connected Cars - 多列卡片](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="708fe-240">重新命名 hello**量測計標題**太**「 平均速度 」**</span><span class="sxs-lookup"><span data-stu-id="708fe-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![Connected Cars - 量測計](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="708fe-242">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="708fe-243">同樣地加入「平均機油」、「平均油量」和「平均引擎溫度」的**量測計**。</span><span class="sxs-lookup"><span data-stu-id="708fe-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="708fe-244">變更 hello 預設彙總的每個量測計中依照上述步驟中的欄位**「 平均速度 」**量測計。</span><span class="sxs-lookup"><span data-stu-id="708fe-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Connected Cars - 量測計](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="708fe-246">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="708fe-247">選取**折線與群組直條圖**從視覺效果，然後將拖曳**縣 （市)**欄位到**共用軸**，拖曳**速度**， **tirepressure 和 engineoil 欄位**到**資料行值**區域中，變更其彙總類型太**平均**。</span><span class="sxs-lookup"><span data-stu-id="708fe-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="708fe-248">拖曳 hello **engineTemperature**欄位到**行值**區域中，也變更 hello 彙總類型**平均**。</span><span class="sxs-lookup"><span data-stu-id="708fe-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![Connected Cars -視覺效果欄位](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="708fe-250">變更 hello 圖表**標題**太**「 平均速度、 tire 不足的壓力，引擎石油和引擎溫度 」**。</span><span class="sxs-lookup"><span data-stu-id="708fe-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Connected Cars -視覺效果欄位](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="708fe-252">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="708fe-253">選取**矩形式樹狀結構圖**視覺效果，從視覺效果拖曳 hello**模型**欄位到 hello**群組**區域中，然後拖曳 hello 欄位**MaintenanceProbability**到 hello**值**區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="708fe-254">變更 hello 圖表**標題**太**"Vehicle 模型需要維護 >**。</span><span class="sxs-lookup"><span data-stu-id="708fe-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![Connected Cars - 變更圖表標題](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="708fe-256">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="708fe-257">選取**100%堆疊橫條圖**從 視覺效果中，拖曳 hello**縣 （市)**欄位到 hello**軸**區域中，然後拖曳 hello **MaintenanceProbability**， **RecallProbability** hello 將欄位**值**區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![Connected Cars - 加入新的視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="708fe-259">按一下**格式**，選取**資料色彩**，並設定 hello **MaintenanceProbability**色彩 toohello 值**"F2C80F"**。</span><span class="sxs-lookup"><span data-stu-id="708fe-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="708fe-260">變更 hello**標題**hello 的圖表太**"機率的一種載具，維護及回收由 City"**。</span><span class="sxs-lookup"><span data-stu-id="708fe-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Connected Cars - 加入新的視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="708fe-262">按一下 hello 的空白區域 tooadd 新的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="708fe-263">選取**區域圖**從視覺效果的視覺效果，從拖曳 hello**模型**欄位到 hello**軸**區域中，然後拖曳 hello **engineOil，tirepressure，速度和 MaintenanceProbability** hello 將欄位**值**區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="708fe-264">變更其彙總類型太**「 平均數 」**。</span><span class="sxs-lookup"><span data-stu-id="708fe-264">Change their aggregation type too**“Average”**.</span></span> 

![Connected Cars - 變更彙總類型](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="708fe-266">變更 hello 圖表 hello 標題太**「 平均引擎石油，tire 不足的壓力、 速度以及維護機率模型 」**。</span><span class="sxs-lookup"><span data-stu-id="708fe-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Connected Cars - 變更圖表標題](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="708fe-268">按一下 hello 的空白區域 tooadd 新的視覺效果：</span><span class="sxs-lookup"><span data-stu-id="708fe-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="708fe-269">從 [視覺效果] 中選取「散佈圖」  視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="708fe-270">拖曳 hello**模型**欄位到 hello**詳細資料**和**圖例**區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="708fe-271">拖曳 hello**燃料**欄位到 hello **x 軸**區域中，也變更 hello 彙總**平均**。</span><span class="sxs-lookup"><span data-stu-id="708fe-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="708fe-272">拖曳**engineTemparature**到**y 軸區域**，也變更 hello 彙總**平均**</span><span class="sxs-lookup"><span data-stu-id="708fe-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="708fe-273">拖曳 hello **vin**欄位到 hello**大小**區域。</span><span class="sxs-lookup"><span data-stu-id="708fe-273">Drag hello **vin** field into hello **Size** area.</span></span>

![Connected Cars - 加入新的視覺效果](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="708fe-275">變更 hello 圖表**標題**太**"燃料的平均值，模型的引擎溫度"**。</span><span class="sxs-lookup"><span data-stu-id="708fe-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Connected Cars - 變更圖表標題](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="708fe-277">hello 最終報表看起來類似，如下所示。</span><span class="sxs-lookup"><span data-stu-id="708fe-277">hello final report will look like as shown below.</span></span>

![Connected Cars - 最終報告](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="708fe-279">從 hello 報表 toohello 即時儀表板釘選視覺效果</span><span class="sxs-lookup"><span data-stu-id="708fe-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="708fe-280">建立空白的儀表板上 hello 加號圖示的 下一步 tooDashboards 即可。</span><span class="sxs-lookup"><span data-stu-id="708fe-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="708fe-281">您可以將它命名為「車輛遙測分析儀表板」</span><span class="sxs-lookup"><span data-stu-id="708fe-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Connected Cars - 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="708fe-283">從報表 toohello 儀表板上方的 hello hello 釘選視覺效果。</span><span class="sxs-lookup"><span data-stu-id="708fe-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![Connected Cars - 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="708fe-285">hello 儀表板應該看起來像這樣當所有三個報表都是建立的 hello 和 hello 對應的視覺效果釘選的 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="708fe-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="708fe-286">如果您沒有建立 hello 的所有報表，您的儀表板看起來可能不同。</span><span class="sxs-lookup"><span data-stu-id="708fe-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![Connected Cars - 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="708fe-288">恭喜！</span><span class="sxs-lookup"><span data-stu-id="708fe-288">Congratulations!</span></span> <span data-ttu-id="708fe-289">您已成功建立 hello 即時儀表板。</span><span class="sxs-lookup"><span data-stu-id="708fe-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="708fe-290">當您繼續 tooexecute CarEventGenerator.exe 和 RealtimeDashboardApp.exe，您應該看到 hello 儀表板上的即時更新。</span><span class="sxs-lookup"><span data-stu-id="708fe-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="708fe-291">它應該採取下列步驟大約 10 個 too15 分鐘 toocomplete hello。</span><span class="sxs-lookup"><span data-stu-id="708fe-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="708fe-292">設定 Power BI 批次處理儀表板</span><span class="sxs-lookup"><span data-stu-id="708fe-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="708fe-293">它需要約兩小時的時間 （從 hello 部署的 hello 成功完成） hello 結束 tooend 批次處理管線 toofinish 執行並處理過去年度產生的資料。</span><span class="sxs-lookup"><span data-stu-id="708fe-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="708fe-294">因此等候 hello 處理 toofinish hello 接下來的步驟繼續執行。</span><span class="sxs-lookup"><span data-stu-id="708fe-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="708fe-295">**下載 hello Power BI 設計工具檔案**</span><span class="sxs-lookup"><span data-stu-id="708fe-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="708fe-296">建立預先設定的 Power BI 設計工具的檔案是包含在 hello 部署手動操作說明</span><span class="sxs-lookup"><span data-stu-id="708fe-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="708fe-297">尋找 2.</span><span class="sxs-lookup"><span data-stu-id="708fe-297">Look for 2.</span></span> <span data-ttu-id="708fe-298">安裝程式 PowerBI 批次處理儀表板，您可以下載此呼叫的批次處理儀表板的 hello PowerBI 範本**ConnectedCarsPbiReport.pbix**。</span><span class="sxs-lookup"><span data-stu-id="708fe-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="708fe-299">儲存在本機</span><span class="sxs-lookup"><span data-stu-id="708fe-299">Save locally</span></span>

<span data-ttu-id="708fe-300">**設定 Power BI 報告**</span><span class="sxs-lookup"><span data-stu-id="708fe-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="708fe-301">開啟 hello 設計工具檔案 '**ConnectedCarsPbiReport.pbix**' 使用 Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="708fe-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="708fe-302">如果您沒有已有，安裝 hello 從 Power BI Desktop [Power BI Desktop 安裝](http://www.microsoft.com/download/details.aspx?id=45331)。</span><span class="sxs-lookup"><span data-stu-id="708fe-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="708fe-303">按一下 hello**編輯查詢**。</span><span class="sxs-lookup"><span data-stu-id="708fe-303">Click hello **Edit Queries**.</span></span>

![編輯 Power BI 查詢](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="708fe-305">按兩下 hello**來源**。</span><span class="sxs-lookup"><span data-stu-id="708fe-305">Double-click hello **Source**.</span></span>

![設定 Power BI 來源](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="708fe-307">收到 hello 部署的一部分佈建的 hello Azure SQL server 更新伺服器的連接字串。</span><span class="sxs-lookup"><span data-stu-id="708fe-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="708fe-308">查詢 底下的 hello 手動操作說明</span><span class="sxs-lookup"><span data-stu-id="708fe-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="708fe-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="708fe-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="708fe-310">伺服器︰somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="708fe-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="708fe-311">資料庫︰connectedcar</span><span class="sxs-lookup"><span data-stu-id="708fe-311">Database: connectedcar</span></span>
    * <span data-ttu-id="708fe-312">使用者名稱︰使用者名稱</span><span class="sxs-lookup"><span data-stu-id="708fe-312">Username: username</span></span>
    * <span data-ttu-id="708fe-313">密碼︰ 您可以從 Azure 入口網站管理您的 SQL 伺服器密碼</span><span class="sxs-lookup"><span data-stu-id="708fe-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="708fe-314">將 [資料庫]  保留為 *connectedcar*。</span><span class="sxs-lookup"><span data-stu-id="708fe-314">Leave **Database** as *connectedcar*.</span></span>

![設定 Power BI 資料庫](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="708fe-316">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="708fe-316">Click **OK**.</span></span>
* <span data-ttu-id="708fe-317">您會看到**Windows 認證**預設選取索引標籤，變更太**資料庫認證**上的 **資料庫**右邊索引標籤。</span><span class="sxs-lookup"><span data-stu-id="708fe-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="708fe-318">提供 hello **Username**和**密碼**其部署安裝期間指定您 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="708fe-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![提供資料庫認證](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="708fe-320">按一下 [連接] </span><span class="sxs-lookup"><span data-stu-id="708fe-320">Click **Connect**</span></span>
* <span data-ttu-id="708fe-321">針對每個 hello 三個剩餘查詢出現在右窗格中，重複上述步驟 hello，然後更新 hello 資料來源連接的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="708fe-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="708fe-322">按一下 [關閉並載入] 。</span><span class="sxs-lookup"><span data-stu-id="708fe-322">Click **Close and Load**.</span></span> <span data-ttu-id="708fe-323">Power BI Desktop 檔案的資料集是已連線的 tooSQL Azure 資料庫的資料表。</span><span class="sxs-lookup"><span data-stu-id="708fe-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="708fe-324">**關閉** Power BI Desktop 檔案。</span><span class="sxs-lookup"><span data-stu-id="708fe-324">**Close** Power BI Desktop file.</span></span>

![關閉 Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="708fe-326">按一下**儲存**按鈕 toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="708fe-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="708fe-327">您現在已設定對應 toohello 批次處理路徑 hello 方案中的所有 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="708fe-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="708fe-328">上傳太*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="708fe-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="708fe-329">瀏覽 toohello http://powerbi.com 以及登入 Power BI web 入口網站。</span><span class="sxs-lookup"><span data-stu-id="708fe-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="708fe-330">按一下 [取得資料] </span><span class="sxs-lookup"><span data-stu-id="708fe-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="708fe-331">上傳 hello Power BI Desktop 檔案。</span><span class="sxs-lookup"><span data-stu-id="708fe-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="708fe-332">tooupload，按一下 **取得資料-> 檔案-> 本機檔案**</span><span class="sxs-lookup"><span data-stu-id="708fe-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="708fe-333">瀏覽 toohello **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="708fe-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="708fe-334">一旦上傳 hello 檔案時，會巡覽後 tooyour Power BI 工作空間。</span><span class="sxs-lookup"><span data-stu-id="708fe-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="708fe-335">將會為您建立資料集、報告和空白儀表板。</span><span class="sxs-lookup"><span data-stu-id="708fe-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="708fe-336">釘選圖呼叫 tooa 新儀表板**Vehicle 遙測分析儀表板**中**Power BI**。</span><span class="sxs-lookup"><span data-stu-id="708fe-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="708fe-337">按一下上面建立 hello 空白儀表板，然後瀏覽 toohello**報表**區段中，按一下 hello 新上傳報表。</span><span class="sxs-lookup"><span data-stu-id="708fe-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![車輛遙測 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="708fe-339">**請注意 hello 報表有六個頁面：**</span><span class="sxs-lookup"><span data-stu-id="708fe-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="708fe-340">第 1 頁︰車輛密度</span><span class="sxs-lookup"><span data-stu-id="708fe-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="708fe-341">第 2 頁︰即時車輛健全狀況</span><span class="sxs-lookup"><span data-stu-id="708fe-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="708fe-342">第 3 頁︰危險駕駛的車輛</span><span class="sxs-lookup"><span data-stu-id="708fe-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="708fe-343">第 4 頁︰召回的車輛</span><span class="sxs-lookup"><span data-stu-id="708fe-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="708fe-344">第 5 頁︰省油的車輛</span><span class="sxs-lookup"><span data-stu-id="708fe-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="708fe-345">第 6 頁︰Contoso 標誌</span><span class="sxs-lookup"><span data-stu-id="708fe-345">Page 6: Contoso Logo</span></span>  

![連接的車輛 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="708fe-347">**從第 3 頁**，釘選 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="708fe-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="708fe-348">VIN 的計數</span><span class="sxs-lookup"><span data-stu-id="708fe-348">Count of VIN</span></span>  
   ![連接的車輛 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="708fe-350">危險駕駛的車輛 (依車型) – 瀑布圖 </span><span class="sxs-lookup"><span data-stu-id="708fe-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![車輛遙測 - 釘選圖表 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="708fe-352">**從第 5 頁**，釘選 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="708fe-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="708fe-353">vin 的計數</span><span class="sxs-lookup"><span data-stu-id="708fe-353">Count of vin</span></span>    
   ![車輛遙測 - 釘選圖表 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="708fe-355">省油的車輛 (依車型)：群組直條圖 </span><span class="sxs-lookup"><span data-stu-id="708fe-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![車輛遙測 - 釘選圖表 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="708fe-357">**從第 4 頁**，釘選 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="708fe-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="708fe-358">vin 的計數</span><span class="sxs-lookup"><span data-stu-id="708fe-358">Count of vin</span></span>  
   ![車輛遙測 - 釘選圖表 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="708fe-360">召回的車輛 (依城市、車型)：樹狀圖 </span><span class="sxs-lookup"><span data-stu-id="708fe-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![車輛遙測 - 釘選圖表 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="708fe-362">**從第 6 頁**，釘選 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="708fe-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="708fe-363">Contoso Motors 標誌 </span><span class="sxs-lookup"><span data-stu-id="708fe-363">Contoso Motors logo</span></span>  
   ![車輛遙測 - 釘選圖表 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="708fe-365">**組織 hello 儀表板**</span><span class="sxs-lookup"><span data-stu-id="708fe-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="708fe-366">瀏覽 toohello 儀表板</span><span class="sxs-lookup"><span data-stu-id="708fe-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="708fe-367">將滑鼠停留在每個圖表，並將它會根據 hello 命名重新命名圖的 hello 完整儀表板中提供。</span><span class="sxs-lookup"><span data-stu-id="708fe-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="708fe-368">也會移動 hello 圖表周圍 toolook 像 hello 儀表板下方。</span><span class="sxs-lookup"><span data-stu-id="708fe-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![車輛遙測 - 組織儀表板 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![車輛遙測 Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="708fe-371">如果您已建立所有 hello 報告這份文件中所述，hello 最後完成的儀表板看起來應該像 hello 遵循圖。</span><span class="sxs-lookup"><span data-stu-id="708fe-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![車輛遙測 - 組織儀表板 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="708fe-373">恭喜！</span><span class="sxs-lookup"><span data-stu-id="708fe-373">Congratulations!</span></span> <span data-ttu-id="708fe-374">您已成功建立 hello 報告和 hello 儀表板 toogain 即時、 預測及批次的洞察能力 vehicle 健全狀況和驅動習慣。</span><span class="sxs-lookup"><span data-stu-id="708fe-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
