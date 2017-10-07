---
title: "使用資料流分析的 IoT 解決方案 aaaBuild |Microsoft 文件"
description: "快速入門教學課程中的 hello 的收費站案例的資料流分析 IoT 解決方案"
keywords: "iot 解決方案, 視窗函數"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a><span data-ttu-id="77485-104">利用串流分析來建置 IoT 解決方案</span><span class="sxs-lookup"><span data-stu-id="77485-104">Build an IoT solution by using Stream Analytics</span></span>
## <a name="introduction"></a><span data-ttu-id="77485-105">簡介</span><span class="sxs-lookup"><span data-stu-id="77485-105">Introduction</span></span>
<span data-ttu-id="77485-106">在此教學課程中，您將學習如何 toouse Azure Stream Analytics tooget 即時深入資訊從您的資料。</span><span class="sxs-lookup"><span data-stu-id="77485-106">In this tutorial, you will learn how toouse Azure Stream Analytics tooget real-time insights from your data.</span></span> <span data-ttu-id="77485-107">開發人員可以輕鬆地結合資料的流，例如按一下資料流、 記錄檔，以及裝置產生的事件，歷程記錄或參考資料 tooderive 商業見解。</span><span class="sxs-lookup"><span data-stu-id="77485-107">Developers can easily combine streams of data, such as click-streams, logs, and device-generated events, with historical records or reference data tooderive business insights.</span></span> <span data-ttu-id="77485-108">以完全受管理、 即時資料流計算服務裝載於 Microsoft Azure，Azure Stream Analytics 提供內建的恢復功能、 低延遲度及延展性 tooget 啟動及執行以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="77485-108">As a fully managed, real-time stream computation service that's hosted in Microsoft Azure, Azure Stream Analytics provides built-in resiliency, low latency, and scalability tooget you up and running in minutes.</span></span>

<span data-ttu-id="77485-109">完成本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="77485-109">After completing this tutorial, you will be able to:</span></span>

* <span data-ttu-id="77485-110">熟悉 hello Azure Stream Analytics 入口網站。</span><span class="sxs-lookup"><span data-stu-id="77485-110">Familiarize yourself with hello Azure Stream Analytics portal.</span></span>
* <span data-ttu-id="77485-111">設定及部署串流工作。</span><span class="sxs-lookup"><span data-stu-id="77485-111">Configure and deploy a streaming job.</span></span>
* <span data-ttu-id="77485-112">表達真實問題和解決使用 hello Stream Analytics 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="77485-112">Articulate real-world problems and solve them by using hello Stream Analytics query language.</span></span>
* <span data-ttu-id="77485-113">有自信地使用串流分析來為客戶開發串流解決方案。</span><span class="sxs-lookup"><span data-stu-id="77485-113">Develop streaming solutions for your customers by using Stream Analytics with confidence.</span></span>
* <span data-ttu-id="77485-114">使用 hello 監視和記錄經驗 tootroubleshoot 問題。</span><span class="sxs-lookup"><span data-stu-id="77485-114">Use hello monitoring and logging experience tootroubleshoot issues.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77485-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="77485-115">Prerequisites</span></span>
<span data-ttu-id="77485-116">您將需要 hello 必要條件 toocomplete 遵循本教學課程：</span><span class="sxs-lookup"><span data-stu-id="77485-116">You will need hello following prerequisites toocomplete this tutorial:</span></span>

* <span data-ttu-id="77485-117">hello 最新版本的[Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="77485-117">hello latest version of [Azure PowerShell](/powershell/azure/overview)</span></span>
* <span data-ttu-id="77485-118">Visual Studio 2017，2015 中，或使用可用的 hello [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="77485-118">Visual Studio 2017, 2015, or hello free [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)</span></span>
* <span data-ttu-id="77485-119">[Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="77485-119">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="77485-120">Hello 電腦上的系統管理權限</span><span class="sxs-lookup"><span data-stu-id="77485-120">Administrative privileges on hello computer</span></span>
* <span data-ttu-id="77485-121">下載[TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip)從 Microsoft 下載中心 hello</span><span class="sxs-lookup"><span data-stu-id="77485-121">Download of [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) from hello Microsoft Download Center</span></span>
* <span data-ttu-id="77485-122">選擇性： Hello TollApp 事件產生器中的原始程式碼[GitHub](https://aka.ms/azure-stream-analytics-toll-source)</span><span class="sxs-lookup"><span data-stu-id="77485-122">Optional: Source code for hello TollApp event generator in [GitHub](https://aka.ms/azure-stream-analytics-toll-source)</span></span>

## <a name="scenario-introduction-hello-toll"></a><span data-ttu-id="77485-123">案例簡介：收費站，你好！</span><span class="sxs-lookup"><span data-stu-id="77485-123">Scenario introduction: “Hello, Toll!”</span></span>
<span data-ttu-id="77485-124">收費站是常見的設施。</span><span class="sxs-lookup"><span data-stu-id="77485-124">A toll station is a common phenomenon.</span></span> <span data-ttu-id="77485-125">您會遇到這些許多 expressways、 橋接器和通道 hello 世界各地。</span><span class="sxs-lookup"><span data-stu-id="77485-125">You encounter them on many expressways, bridges, and tunnels across hello world.</span></span> <span data-ttu-id="77485-126">每個收費站都有多個收費亭。</span><span class="sxs-lookup"><span data-stu-id="77485-126">Each toll station has multiple toll booths.</span></span> <span data-ttu-id="77485-127">在手動攤位，您可以停止 toopay hello 付費 tooan 服務員。</span><span class="sxs-lookup"><span data-stu-id="77485-127">At manual booths, you stop toopay hello toll tooan attendant.</span></span> <span data-ttu-id="77485-128">在自動化攤位，每個亭上方的感應器會掃描您傳送嗨收費亭為貼附 toohello 擋風玻璃上的汽車的 RFID 卡。</span><span class="sxs-lookup"><span data-stu-id="77485-128">At automated booths, a sensor on top of each booth scans an RFID card that's affixed toohello windshield of your vehicle as you pass hello toll booth.</span></span> <span data-ttu-id="77485-129">它是簡單 toovisualize hello 經過通過這些收費站的車輛的可執行有趣作業的事件資料流。</span><span class="sxs-lookup"><span data-stu-id="77485-129">It is easy toovisualize hello passage of vehicles through these toll stations as an event stream over which interesting operations can be performed.</span></span>

![收費亭中車輛的圖片](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a><span data-ttu-id="77485-131">傳入的資料</span><span class="sxs-lookup"><span data-stu-id="77485-131">Incoming data</span></span>
<span data-ttu-id="77485-132">本教學課程搭配兩個資料串流來教學。</span><span class="sxs-lookup"><span data-stu-id="77485-132">This tutorial works with two streams of data.</span></span> <span data-ttu-id="77485-133">感應器安裝在 hello 進入與離開 hello 付費電台產生 hello 第一個資料流。</span><span class="sxs-lookup"><span data-stu-id="77485-133">Sensors installed in hello entrance and exit of hello toll stations produce hello first stream.</span></span> <span data-ttu-id="77485-134">hello 第二個資料流是擁有車輛註冊資料的靜態查閱資料集。</span><span class="sxs-lookup"><span data-stu-id="77485-134">hello second stream is a static lookup dataset that has vehicle registration data.</span></span>

### <a name="entry-data-stream"></a><span data-ttu-id="77485-135">入口資料流</span><span class="sxs-lookup"><span data-stu-id="77485-135">Entry data stream</span></span>
<span data-ttu-id="77485-136">hello 項目資料流在進入收費站包含汽車的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="77485-136">hello entry data stream contains information about cars as they enter toll stations.</span></span>

| <span data-ttu-id="77485-137">TollID</span><span class="sxs-lookup"><span data-stu-id="77485-137">TollID</span></span> | <span data-ttu-id="77485-138">EntryTime</span><span class="sxs-lookup"><span data-stu-id="77485-138">EntryTime</span></span> | <span data-ttu-id="77485-139">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="77485-139">LicensePlate</span></span> | <span data-ttu-id="77485-140">State</span><span class="sxs-lookup"><span data-stu-id="77485-140">State</span></span> | <span data-ttu-id="77485-141">Make</span><span class="sxs-lookup"><span data-stu-id="77485-141">Make</span></span> | <span data-ttu-id="77485-142">模型</span><span class="sxs-lookup"><span data-stu-id="77485-142">Model</span></span> | <span data-ttu-id="77485-143">VehicleType</span><span class="sxs-lookup"><span data-stu-id="77485-143">VehicleType</span></span> | <span data-ttu-id="77485-144">VehicleWeight</span><span class="sxs-lookup"><span data-stu-id="77485-144">VehicleWeight</span></span> | <span data-ttu-id="77485-145">Toll</span><span class="sxs-lookup"><span data-stu-id="77485-145">Toll</span></span> | <span data-ttu-id="77485-146">Tag</span><span class="sxs-lookup"><span data-stu-id="77485-146">Tag</span></span> |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="77485-147">1</span><span class="sxs-lookup"><span data-stu-id="77485-147">1</span></span> |<span data-ttu-id="77485-148">2014-09-10 12:01:00.000</span><span class="sxs-lookup"><span data-stu-id="77485-148">2014-09-10 12:01:00.000</span></span> |<span data-ttu-id="77485-149">JNB 7001</span><span class="sxs-lookup"><span data-stu-id="77485-149">JNB 7001</span></span> |<span data-ttu-id="77485-150">NY</span><span class="sxs-lookup"><span data-stu-id="77485-150">NY</span></span> |<span data-ttu-id="77485-151">Honda</span><span class="sxs-lookup"><span data-stu-id="77485-151">Honda</span></span> |<span data-ttu-id="77485-152">CRV</span><span class="sxs-lookup"><span data-stu-id="77485-152">CRV</span></span> |<span data-ttu-id="77485-153">1</span><span class="sxs-lookup"><span data-stu-id="77485-153">1</span></span> |<span data-ttu-id="77485-154">0</span><span class="sxs-lookup"><span data-stu-id="77485-154">0</span></span> |<span data-ttu-id="77485-155">7</span><span class="sxs-lookup"><span data-stu-id="77485-155">7</span></span> | |
| <span data-ttu-id="77485-156">1</span><span class="sxs-lookup"><span data-stu-id="77485-156">1</span></span> |<span data-ttu-id="77485-157">2014-09-10 12:02:00.000</span><span class="sxs-lookup"><span data-stu-id="77485-157">2014-09-10 12:02:00.000</span></span> |<span data-ttu-id="77485-158">YXZ 1001</span><span class="sxs-lookup"><span data-stu-id="77485-158">YXZ 1001</span></span> |<span data-ttu-id="77485-159">NY</span><span class="sxs-lookup"><span data-stu-id="77485-159">NY</span></span> |<span data-ttu-id="77485-160">Toyota</span><span class="sxs-lookup"><span data-stu-id="77485-160">Toyota</span></span> |<span data-ttu-id="77485-161">Camry</span><span class="sxs-lookup"><span data-stu-id="77485-161">Camry</span></span> |<span data-ttu-id="77485-162">1</span><span class="sxs-lookup"><span data-stu-id="77485-162">1</span></span> |<span data-ttu-id="77485-163">0</span><span class="sxs-lookup"><span data-stu-id="77485-163">0</span></span> |<span data-ttu-id="77485-164">4</span><span class="sxs-lookup"><span data-stu-id="77485-164">4</span></span> |<span data-ttu-id="77485-165">123456789</span><span class="sxs-lookup"><span data-stu-id="77485-165">123456789</span></span> |
| <span data-ttu-id="77485-166">3</span><span class="sxs-lookup"><span data-stu-id="77485-166">3</span></span> |<span data-ttu-id="77485-167">2014-09-10 12:02:00.000</span><span class="sxs-lookup"><span data-stu-id="77485-167">2014-09-10 12:02:00.000</span></span> |<span data-ttu-id="77485-168">ABC 1004</span><span class="sxs-lookup"><span data-stu-id="77485-168">ABC 1004</span></span> |<span data-ttu-id="77485-169">CT</span><span class="sxs-lookup"><span data-stu-id="77485-169">CT</span></span> |<span data-ttu-id="77485-170">Ford</span><span class="sxs-lookup"><span data-stu-id="77485-170">Ford</span></span> |<span data-ttu-id="77485-171">Taurus</span><span class="sxs-lookup"><span data-stu-id="77485-171">Taurus</span></span> |<span data-ttu-id="77485-172">1</span><span class="sxs-lookup"><span data-stu-id="77485-172">1</span></span> |<span data-ttu-id="77485-173">0</span><span class="sxs-lookup"><span data-stu-id="77485-173">0</span></span> |<span data-ttu-id="77485-174">5</span><span class="sxs-lookup"><span data-stu-id="77485-174">5</span></span> |<span data-ttu-id="77485-175">456789123</span><span class="sxs-lookup"><span data-stu-id="77485-175">456789123</span></span> |
| <span data-ttu-id="77485-176">2</span><span class="sxs-lookup"><span data-stu-id="77485-176">2</span></span> |<span data-ttu-id="77485-177">2014-09-10 12:03:00.000</span><span class="sxs-lookup"><span data-stu-id="77485-177">2014-09-10 12:03:00.000</span></span> |<span data-ttu-id="77485-178">XYZ 1003</span><span class="sxs-lookup"><span data-stu-id="77485-178">XYZ 1003</span></span> |<span data-ttu-id="77485-179">CT</span><span class="sxs-lookup"><span data-stu-id="77485-179">CT</span></span> |<span data-ttu-id="77485-180">Toyota</span><span class="sxs-lookup"><span data-stu-id="77485-180">Toyota</span></span> |<span data-ttu-id="77485-181">Corolla</span><span class="sxs-lookup"><span data-stu-id="77485-181">Corolla</span></span> |<span data-ttu-id="77485-182">1</span><span class="sxs-lookup"><span data-stu-id="77485-182">1</span></span> |<span data-ttu-id="77485-183">0</span><span class="sxs-lookup"><span data-stu-id="77485-183">0</span></span> |<span data-ttu-id="77485-184">4</span><span class="sxs-lookup"><span data-stu-id="77485-184">4</span></span> | |
| <span data-ttu-id="77485-185">1</span><span class="sxs-lookup"><span data-stu-id="77485-185">1</span></span> |<span data-ttu-id="77485-186">2014-09-10 12:03:00.000</span><span class="sxs-lookup"><span data-stu-id="77485-186">2014-09-10 12:03:00.000</span></span> |<span data-ttu-id="77485-187">BNJ 1007</span><span class="sxs-lookup"><span data-stu-id="77485-187">BNJ 1007</span></span> |<span data-ttu-id="77485-188">NY</span><span class="sxs-lookup"><span data-stu-id="77485-188">NY</span></span> |<span data-ttu-id="77485-189">Honda</span><span class="sxs-lookup"><span data-stu-id="77485-189">Honda</span></span> |<span data-ttu-id="77485-190">CRV</span><span class="sxs-lookup"><span data-stu-id="77485-190">CRV</span></span> |<span data-ttu-id="77485-191">1</span><span class="sxs-lookup"><span data-stu-id="77485-191">1</span></span> |<span data-ttu-id="77485-192">0</span><span class="sxs-lookup"><span data-stu-id="77485-192">0</span></span> |<span data-ttu-id="77485-193">5</span><span class="sxs-lookup"><span data-stu-id="77485-193">5</span></span> |<span data-ttu-id="77485-194">789123456</span><span class="sxs-lookup"><span data-stu-id="77485-194">789123456</span></span> |
| <span data-ttu-id="77485-195">2</span><span class="sxs-lookup"><span data-stu-id="77485-195">2</span></span> |<span data-ttu-id="77485-196">2014-09-10 12:05:00.000</span><span class="sxs-lookup"><span data-stu-id="77485-196">2014-09-10 12:05:00.000</span></span> |<span data-ttu-id="77485-197">CDE 1007</span><span class="sxs-lookup"><span data-stu-id="77485-197">CDE 1007</span></span> |<span data-ttu-id="77485-198">NJ</span><span class="sxs-lookup"><span data-stu-id="77485-198">NJ</span></span> |<span data-ttu-id="77485-199">Toyota</span><span class="sxs-lookup"><span data-stu-id="77485-199">Toyota</span></span> |<span data-ttu-id="77485-200">4x4</span><span class="sxs-lookup"><span data-stu-id="77485-200">4x4</span></span> |<span data-ttu-id="77485-201">1</span><span class="sxs-lookup"><span data-stu-id="77485-201">1</span></span> |<span data-ttu-id="77485-202">0</span><span class="sxs-lookup"><span data-stu-id="77485-202">0</span></span> |<span data-ttu-id="77485-203">6</span><span class="sxs-lookup"><span data-stu-id="77485-203">6</span></span> |<span data-ttu-id="77485-204">321987654</span><span class="sxs-lookup"><span data-stu-id="77485-204">321987654</span></span> |

<span data-ttu-id="77485-205">以下是簡短 hello 資料行的描述：</span><span class="sxs-lookup"><span data-stu-id="77485-205">Here is a short description of hello columns:</span></span>

| <span data-ttu-id="77485-206">資料欄</span><span class="sxs-lookup"><span data-stu-id="77485-206">Column</span></span> | <span data-ttu-id="77485-207">說明</span><span class="sxs-lookup"><span data-stu-id="77485-207">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77485-208">TollID</span><span class="sxs-lookup"><span data-stu-id="77485-208">TollID</span></span> |<span data-ttu-id="77485-209">可唯一識別收費亭 hello 收費亭識別碼</span><span class="sxs-lookup"><span data-stu-id="77485-209">hello toll booth ID that uniquely identifies a toll booth</span></span> |
| <span data-ttu-id="77485-210">EntryTime</span><span class="sxs-lookup"><span data-stu-id="77485-210">EntryTime</span></span> |<span data-ttu-id="77485-211">hello 日期和時間-utc 時區 hello vehicle toohello 收費亭的項目</span><span class="sxs-lookup"><span data-stu-id="77485-211">hello date and time of entry of hello vehicle toohello toll booth in UTC</span></span> |
| <span data-ttu-id="77485-212">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="77485-212">LicensePlate</span></span> |<span data-ttu-id="77485-213">hello 與車牌號碼的一種載具，hello</span><span class="sxs-lookup"><span data-stu-id="77485-213">hello license plate number of hello vehicle</span></span> |
| <span data-ttu-id="77485-214">State</span><span class="sxs-lookup"><span data-stu-id="77485-214">State</span></span> |<span data-ttu-id="77485-215">美國的某個洲</span><span class="sxs-lookup"><span data-stu-id="77485-215">A state in United States</span></span> |
| <span data-ttu-id="77485-216">Make</span><span class="sxs-lookup"><span data-stu-id="77485-216">Make</span></span> |<span data-ttu-id="77485-217">hello 汽車的 hello 製造商</span><span class="sxs-lookup"><span data-stu-id="77485-217">hello manufacturer of hello automobile</span></span> |
| <span data-ttu-id="77485-218">模型</span><span class="sxs-lookup"><span data-stu-id="77485-218">Model</span></span> |<span data-ttu-id="77485-219">hello 汽車 hello 型號號碼</span><span class="sxs-lookup"><span data-stu-id="77485-219">hello model number of hello automobile</span></span> |
| <span data-ttu-id="77485-220">VehicleType</span><span class="sxs-lookup"><span data-stu-id="77485-220">VehicleType</span></span> |<span data-ttu-id="77485-221">1 代表載客車或 2 代表商用車</span><span class="sxs-lookup"><span data-stu-id="77485-221">Either 1 for passenger vehicles or 2 for commercial vehicles</span></span> |
| <span data-ttu-id="77485-222">WeightType</span><span class="sxs-lookup"><span data-stu-id="77485-222">WeightType</span></span> |<span data-ttu-id="77485-223">車輛的重量，單位為噸；0 代表客車</span><span class="sxs-lookup"><span data-stu-id="77485-223">Vehicle weight in tons; 0 for passenger vehicles</span></span> |
| <span data-ttu-id="77485-224">Toll</span><span class="sxs-lookup"><span data-stu-id="77485-224">Toll</span></span> |<span data-ttu-id="77485-225">以 usd 計算 hello 付費值</span><span class="sxs-lookup"><span data-stu-id="77485-225">hello toll value in USD</span></span> |
| <span data-ttu-id="77485-226">Tag</span><span class="sxs-lookup"><span data-stu-id="77485-226">Tag</span></span> |<span data-ttu-id="77485-227">hello E-tag 上自動執行付款; hello 汽車空白 hello 付款已手動完成</span><span class="sxs-lookup"><span data-stu-id="77485-227">hello e-Tag on hello automobile that automates payment; blank where hello payment was done manually</span></span> |

### <a name="exit-data-stream"></a><span data-ttu-id="77485-228">出口資料流</span><span class="sxs-lookup"><span data-stu-id="77485-228">Exit data stream</span></span>
<span data-ttu-id="77485-229">hello 結束資料流包含離開 hello 收費站的汽車相關資訊。</span><span class="sxs-lookup"><span data-stu-id="77485-229">hello exit data stream contains information about cars leaving hello toll station.</span></span>

| <span data-ttu-id="77485-230">**TollId**</span><span class="sxs-lookup"><span data-stu-id="77485-230">**TollId**</span></span> | <span data-ttu-id="77485-231">**ExitTime**</span><span class="sxs-lookup"><span data-stu-id="77485-231">**ExitTime**</span></span> | <span data-ttu-id="77485-232">**LicensePlate**</span><span class="sxs-lookup"><span data-stu-id="77485-232">**LicensePlate**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77485-233">1</span><span class="sxs-lookup"><span data-stu-id="77485-233">1</span></span> |<span data-ttu-id="77485-234">2014-09-10T12:03:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="77485-234">2014-09-10T12:03:00.0000000Z</span></span> |<span data-ttu-id="77485-235">JNB 7001</span><span class="sxs-lookup"><span data-stu-id="77485-235">JNB 7001</span></span> |
| <span data-ttu-id="77485-236">1</span><span class="sxs-lookup"><span data-stu-id="77485-236">1</span></span> |<span data-ttu-id="77485-237">2014-09-10T12:03:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="77485-237">2014-09-10T12:03:00.0000000Z</span></span> |<span data-ttu-id="77485-238">YXZ 1001</span><span class="sxs-lookup"><span data-stu-id="77485-238">YXZ 1001</span></span> |
| <span data-ttu-id="77485-239">3</span><span class="sxs-lookup"><span data-stu-id="77485-239">3</span></span> |<span data-ttu-id="77485-240">2014-09-10T12:04:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="77485-240">2014-09-10T12:04:00.0000000Z</span></span> |<span data-ttu-id="77485-241">ABC 1004</span><span class="sxs-lookup"><span data-stu-id="77485-241">ABC 1004</span></span> |
| <span data-ttu-id="77485-242">2</span><span class="sxs-lookup"><span data-stu-id="77485-242">2</span></span> |<span data-ttu-id="77485-243">2014-09-10T12:07:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="77485-243">2014-09-10T12:07:00.0000000Z</span></span> |<span data-ttu-id="77485-244">XYZ 1003</span><span class="sxs-lookup"><span data-stu-id="77485-244">XYZ 1003</span></span> |
| <span data-ttu-id="77485-245">1</span><span class="sxs-lookup"><span data-stu-id="77485-245">1</span></span> |<span data-ttu-id="77485-246">2014-09-10T12:08:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="77485-246">2014-09-10T12:08:00.0000000Z</span></span> |<span data-ttu-id="77485-247">BNJ 1007</span><span class="sxs-lookup"><span data-stu-id="77485-247">BNJ 1007</span></span> |
| <span data-ttu-id="77485-248">2</span><span class="sxs-lookup"><span data-stu-id="77485-248">2</span></span> |<span data-ttu-id="77485-249">2014-09-10T12:07:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="77485-249">2014-09-10T12:07:00.0000000Z</span></span> |<span data-ttu-id="77485-250">CDE 1007</span><span class="sxs-lookup"><span data-stu-id="77485-250">CDE 1007</span></span> |

<span data-ttu-id="77485-251">以下是簡短 hello 資料行的描述：</span><span class="sxs-lookup"><span data-stu-id="77485-251">Here is a short description of hello columns:</span></span>

| <span data-ttu-id="77485-252">資料欄</span><span class="sxs-lookup"><span data-stu-id="77485-252">Column</span></span> | <span data-ttu-id="77485-253">說明</span><span class="sxs-lookup"><span data-stu-id="77485-253">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77485-254">TollID</span><span class="sxs-lookup"><span data-stu-id="77485-254">TollID</span></span> |<span data-ttu-id="77485-255">可唯一識別收費亭 hello 收費亭識別碼</span><span class="sxs-lookup"><span data-stu-id="77485-255">hello toll booth ID that uniquely identifies a toll booth</span></span> |
| <span data-ttu-id="77485-256">ExitTime</span><span class="sxs-lookup"><span data-stu-id="77485-256">ExitTime</span></span> |<span data-ttu-id="77485-257">hello 日期和時間-utc 時區的收費亭的 hello 汽車結束</span><span class="sxs-lookup"><span data-stu-id="77485-257">hello date and time of exit of hello vehicle from toll booth in UTC</span></span> |
| <span data-ttu-id="77485-258">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="77485-258">LicensePlate</span></span> |<span data-ttu-id="77485-259">hello 與車牌號碼的一種載具，hello</span><span class="sxs-lookup"><span data-stu-id="77485-259">hello license plate number of hello vehicle</span></span> |

### <a name="commercial-vehicle-registration-data"></a><span data-ttu-id="77485-260">商用車的登記資料</span><span class="sxs-lookup"><span data-stu-id="77485-260">Commercial vehicle registration data</span></span>
<span data-ttu-id="77485-261">hello 教學課程使用靜態的商用車輛註冊資料庫快照集。</span><span class="sxs-lookup"><span data-stu-id="77485-261">hello tutorial uses a static snapshot of a commercial vehicle registration database.</span></span>

| <span data-ttu-id="77485-262">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="77485-262">LicensePlate</span></span> | <span data-ttu-id="77485-263">RegistrationId</span><span class="sxs-lookup"><span data-stu-id="77485-263">RegistrationId</span></span> | <span data-ttu-id="77485-264">已過期</span><span class="sxs-lookup"><span data-stu-id="77485-264">Expired</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77485-265">SVT 6023</span><span class="sxs-lookup"><span data-stu-id="77485-265">SVT 6023</span></span> |<span data-ttu-id="77485-266">285429838</span><span class="sxs-lookup"><span data-stu-id="77485-266">285429838</span></span> |<span data-ttu-id="77485-267">1</span><span class="sxs-lookup"><span data-stu-id="77485-267">1</span></span> |
| <span data-ttu-id="77485-268">XLZ 3463</span><span class="sxs-lookup"><span data-stu-id="77485-268">XLZ 3463</span></span> |<span data-ttu-id="77485-269">362715656</span><span class="sxs-lookup"><span data-stu-id="77485-269">362715656</span></span> |<span data-ttu-id="77485-270">0</span><span class="sxs-lookup"><span data-stu-id="77485-270">0</span></span> |
| <span data-ttu-id="77485-271">BAC 1005</span><span class="sxs-lookup"><span data-stu-id="77485-271">BAC 1005</span></span> |<span data-ttu-id="77485-272">876133137</span><span class="sxs-lookup"><span data-stu-id="77485-272">876133137</span></span> |<span data-ttu-id="77485-273">1</span><span class="sxs-lookup"><span data-stu-id="77485-273">1</span></span> |
| <span data-ttu-id="77485-274">RIV 8632</span><span class="sxs-lookup"><span data-stu-id="77485-274">RIV 8632</span></span> |<span data-ttu-id="77485-275">992711956</span><span class="sxs-lookup"><span data-stu-id="77485-275">992711956</span></span> |<span data-ttu-id="77485-276">0</span><span class="sxs-lookup"><span data-stu-id="77485-276">0</span></span> |
| <span data-ttu-id="77485-277">SNY 7188</span><span class="sxs-lookup"><span data-stu-id="77485-277">SNY 7188</span></span> |<span data-ttu-id="77485-278">592133890</span><span class="sxs-lookup"><span data-stu-id="77485-278">592133890</span></span> |<span data-ttu-id="77485-279">0</span><span class="sxs-lookup"><span data-stu-id="77485-279">0</span></span> |
| <span data-ttu-id="77485-280">ELH 9896</span><span class="sxs-lookup"><span data-stu-id="77485-280">ELH 9896</span></span> |<span data-ttu-id="77485-281">678427724</span><span class="sxs-lookup"><span data-stu-id="77485-281">678427724</span></span> |<span data-ttu-id="77485-282">1</span><span class="sxs-lookup"><span data-stu-id="77485-282">1</span></span> |

<span data-ttu-id="77485-283">以下是簡短 hello 資料行的描述：</span><span class="sxs-lookup"><span data-stu-id="77485-283">Here is a short description of hello columns:</span></span>

| <span data-ttu-id="77485-284">資料欄</span><span class="sxs-lookup"><span data-stu-id="77485-284">Column</span></span> | <span data-ttu-id="77485-285">說明</span><span class="sxs-lookup"><span data-stu-id="77485-285">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77485-286">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="77485-286">LicensePlate</span></span> |<span data-ttu-id="77485-287">hello 與車牌號碼的一種載具，hello</span><span class="sxs-lookup"><span data-stu-id="77485-287">hello license plate number of hello vehicle</span></span> |
| <span data-ttu-id="77485-288">RegistrationId</span><span class="sxs-lookup"><span data-stu-id="77485-288">RegistrationId</span></span> |<span data-ttu-id="77485-289">hello 車輛註冊識別碼</span><span class="sxs-lookup"><span data-stu-id="77485-289">hello vehicle's registration ID</span></span> |
| <span data-ttu-id="77485-290">已過期</span><span class="sxs-lookup"><span data-stu-id="77485-290">Expired</span></span> |<span data-ttu-id="77485-291">hello hello vehicle 登錄狀態： 0，如果車輛註冊為作用中，1，表示註冊已過期</span><span class="sxs-lookup"><span data-stu-id="77485-291">hello registration status of hello vehicle: 0 if vehicle registration is active, 1 if registration is expired</span></span> |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a><span data-ttu-id="77485-292">設定 Azure Stream Analytics hello 環境</span><span class="sxs-lookup"><span data-stu-id="77485-292">Set up hello environment for Azure Stream Analytics</span></span>
<span data-ttu-id="77485-293">toocomplete 本教學課程中，您需要 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="77485-293">toocomplete this tutorial, you need a Microsoft Azure subscription.</span></span> <span data-ttu-id="77485-294">Microsoft 能讓您免費試用 Microsoft Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="77485-294">Microsoft offers free trial for Microsoft Azure services.</span></span>

<span data-ttu-id="77485-295">如果您沒有 Azure 帳戶，您可以 [要求獲得免費試用版](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="77485-295">If you do not have an Azure account, you can [request a free trial version](http://azure.microsoft.com/pricing/free-trial/).</span></span>

> [!NOTE]
> <span data-ttu-id="77485-296">toosign 註冊免費試用版，您需要的行動裝置，可以接收文字訊息和有效的信用卡。</span><span class="sxs-lookup"><span data-stu-id="77485-296">toosign up for a free trial, you need a mobile device that can receive text messages and a valid credit card.</span></span>
> 
> 

<span data-ttu-id="77485-297">請務必 toofollow hello 步驟 hello 「 清除您的 Azure 帳戶 」 一節中的這篇文章的 hello 結尾，如此您就可以進行 hello 充分利用 Azure 信用額度。</span><span class="sxs-lookup"><span data-stu-id="77485-297">Be sure toofollow hello steps in hello “Clean up your Azure account” section at hello end of this article so that you can make hello best use of your Azure credit.</span></span>

## <a name="provision-azure-resources-required-for-hello-tutorial"></a><span data-ttu-id="77485-298">佈建 Azure hello 教學課程所需的資源</span><span class="sxs-lookup"><span data-stu-id="77485-298">Provision Azure resources required for hello tutorial</span></span>
<span data-ttu-id="77485-299">本教學課程需要兩個事件中樞 tooreceive*項目*和*結束*資料流。</span><span class="sxs-lookup"><span data-stu-id="77485-299">This tutorial requires two event hubs tooreceive *entry* and *exit* data streams.</span></span> <span data-ttu-id="77485-300">Azure SQL Database 輸出 hello hello 資料流分析工作的結果。</span><span class="sxs-lookup"><span data-stu-id="77485-300">Azure SQL Database outputs hello results of hello Stream Analytics jobs.</span></span> <span data-ttu-id="77485-301">Azure 儲存體會儲存車輛登記的相關參考資料。</span><span class="sxs-lookup"><span data-stu-id="77485-301">Azure Storage stores reference data about vehicle registrations.</span></span>

<span data-ttu-id="77485-302">您可以使用 hello Setup.ps1 指令碼在 hello TollApp 資料夾 GitHub toocreate 上所有必要的資源。</span><span class="sxs-lookup"><span data-stu-id="77485-302">You can use hello Setup.ps1 script in hello TollApp folder on GitHub toocreate all required resources.</span></span> <span data-ttu-id="77485-303">在 hello 感興趣的時間，我們建議您執行。</span><span class="sxs-lookup"><span data-stu-id="77485-303">In hello interest of time, we recommend that you run it.</span></span> <span data-ttu-id="77485-304">如果您想要深入了解如何 tooconfigure hello Azure 入口網站中的這些資源，請參閱 toolearn toohello < 在 Azure 入口網站中設定資源教學課程 > 的附錄。</span><span class="sxs-lookup"><span data-stu-id="77485-304">If you would like toolearn more about how tooconfigure these resources in hello Azure portal, refer toohello “Configuring tutorial resources in Azure portal” appendix.</span></span>

<span data-ttu-id="77485-305">下載並儲存 hello 支援[TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip)資料夾和檔案。</span><span class="sxs-lookup"><span data-stu-id="77485-305">Download and save hello supporting [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) folder and files.</span></span>

<span data-ttu-id="77485-306">請*以系統管理員的身分*開啟 [Microsoft Azure PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="77485-306">Open a **Microsoft Azure PowerShell** window *as an administrator*.</span></span> <span data-ttu-id="77485-307">如果您還沒有 Azure PowerShell，請依照下列中的 hello 指示[安裝和設定 Azure PowerShell](/powershell/azure/overview) tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="77485-307">If you do not yet have Azure PowerShell, follow hello instructions in [Install and configure Azure PowerShell](/powershell/azure/overview) tooinstall it.</span></span>

<span data-ttu-id="77485-308">因為 Windows 會自動封鎖.ps1、.dll 和.exe 檔案，然後再執行 hello 指令碼需要 tooset hello 執行原則。</span><span class="sxs-lookup"><span data-stu-id="77485-308">Because Windows automatically blocks .ps1, .dll, and .exe files, you need tooset hello execution policy before you run hello script.</span></span> <span data-ttu-id="77485-309">請確定 hello Azure PowerShell 視窗執行*身為系統管理員*。</span><span class="sxs-lookup"><span data-stu-id="77485-309">Make sure hello Azure PowerShell window is running *as an administrator*.</span></span> <span data-ttu-id="77485-310">請執行 **Set-ExecutionPolicy unrestricted**。</span><span class="sxs-lookup"><span data-stu-id="77485-310">Run **Set-ExecutionPolicy unrestricted**.</span></span> <span data-ttu-id="77485-311">在出現提示時按下 Y 鍵 。</span><span class="sxs-lookup"><span data-stu-id="77485-311">When prompted, type **Y**.</span></span>

!["Set-ExecutionPolicy unrestricted" 正在 Azure PowerShell 視窗中執行的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

<span data-ttu-id="77485-313">執行**Get-executionpolicy** toomake 確定 hello 命令處理。</span><span class="sxs-lookup"><span data-stu-id="77485-313">Run **Get-ExecutionPolicy** toomake sure that hello command worked.</span></span>

!["Get-ExecutionPolicy" 正在 Azure PowerShell 視窗中執行的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

<span data-ttu-id="77485-315">移 toohello 目錄具有 hello 指令碼和產生器應用程式。</span><span class="sxs-lookup"><span data-stu-id="77485-315">Go toohello directory that has hello scripts and generator application.</span></span>

![「 Cd.\TollApp\TollApp"hello Azure PowerShell 視窗中執行的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

<span data-ttu-id="77485-317">型別**。\\Setup.ps1** tooset 註冊 Azure 帳戶、 建立和設定所有必要的資源，並開始 toogenerate 事件。</span><span class="sxs-lookup"><span data-stu-id="77485-317">Type **.\\Setup.ps1** tooset up your Azure account, create and configure all required resources, and start toogenerate events.</span></span> <span data-ttu-id="77485-318">hello 指令碼隨機挑選區域 toocreate 您的資源。</span><span class="sxs-lookup"><span data-stu-id="77485-318">hello script randomly picks up a region toocreate your resources.</span></span> <span data-ttu-id="77485-319">tooexplicitly 指定地區，您可以傳遞 hello **-位置**參數如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="77485-319">tooexplicitly specify a region, you can pass hello **-location** parameter as in hello following example:</span></span>

<span data-ttu-id="77485-320">**.\\Setup.ps1 -location “Central US”**</span><span class="sxs-lookup"><span data-stu-id="77485-320">**.\\Setup.ps1 -location “Central US”**</span></span>

![Hello Azure 登入頁面的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

<span data-ttu-id="77485-322">hello 指令碼會開啟 hello**登入**Microsoft azure 的頁面。</span><span class="sxs-lookup"><span data-stu-id="77485-322">hello script opens hello **Sign In** page for Microsoft Azure.</span></span> <span data-ttu-id="77485-323">請輸入您的帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="77485-323">Enter your account credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="77485-324">如果您的帳戶有存取 toomultiple 訂閱，您會想 toouse hello 教學課程的問的 tooenter hello 訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="77485-324">If your account has access toomultiple subscriptions, you will be asked tooenter hello subscription name that you want toouse for hello tutorial.</span></span>
> 
> 

<span data-ttu-id="77485-325">hello 指令碼可能需要幾分鐘的時間 toorun。</span><span class="sxs-lookup"><span data-stu-id="77485-325">hello script can take several minutes toorun.</span></span> <span data-ttu-id="77485-326">完成之後，hello 輸出看起來應該像下列螢幕擷取畫面的 hello。</span><span class="sxs-lookup"><span data-stu-id="77485-326">After it finishes, hello output should look like hello following screenshot.</span></span>

![在 hello Azure PowerShell 視窗中的 hello 指令碼的輸出的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

<span data-ttu-id="77485-328">您也會看到類似下列螢幕擷取畫面的 toohello 另一個視窗。</span><span class="sxs-lookup"><span data-stu-id="77485-328">You will also see another window that's similar toohello following screenshot.</span></span> <span data-ttu-id="77485-329">此應用程式傳送事件 tooAzure 事件中心，也就必要的 toorun hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="77485-329">This application is sending events tooAzure Event Hubs, which is required toorun hello tutorial.</span></span> <span data-ttu-id="77485-330">因此，請勿停止 hello 應用程式或關閉此視窗，直到您完成 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="77485-330">So, do not stop hello application or close this window until you finish hello tutorial.</span></span>

![「正在傳送事件中樞資料」的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

<span data-ttu-id="77485-332">您應該能夠 toosee 資源在 Azure 入口網站現在。</span><span class="sxs-lookup"><span data-stu-id="77485-332">You should be able toosee your resources in Azure portal now.</span></span> <span data-ttu-id="77485-333">跳過<https://portal.azure.com>，並以您的帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="77485-333">Go too<https://portal.azure.com>, and sign in with your account credentials.</span></span> <span data-ttu-id="77485-334">請注意，目前有些功能會利用 hello 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="77485-334">Note that currently some functionality utilizes hello classic portal.</span></span> <span data-ttu-id="77485-335">將會清楚指出這些步驟。</span><span class="sxs-lookup"><span data-stu-id="77485-335">These steps will be clearly indicated.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="77485-336">Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="77485-336">Azure Event Hubs</span></span>
<span data-ttu-id="77485-337">在 hello Azure 入口網站，按一下 **更多服務**上 hello hello 左的管理 窗格的底部。</span><span class="sxs-lookup"><span data-stu-id="77485-337">In hello Azure portal, click **More services** on hello bottom of hello left management pane.</span></span> <span data-ttu-id="77485-338">型別**事件中心**在 hello 提供欄位，然後按一下**事件中心**。</span><span class="sxs-lookup"><span data-stu-id="77485-338">Type **Event hubs** in hello field provided and click **Event hubs**.</span></span> <span data-ttu-id="77485-339">這會啟動新的瀏覽器視窗 toodisplay hello **SERVICE BUS**  區域中 hello**傳統入口網站**。</span><span class="sxs-lookup"><span data-stu-id="77485-339">This launches a new browser window toodisplay hello **SERVICE BUS** area in hello **classic portal**.</span></span> <span data-ttu-id="77485-340">您可以在這裡看到 hello hello Setup.ps1 指令碼所建立的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="77485-340">Here you can see hello Event Hub created by hello Setup.ps1 script.</span></span>

![服務匯流排](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

<span data-ttu-id="77485-342">按一下它的開頭 hello *tolldata*。</span><span class="sxs-lookup"><span data-stu-id="77485-342">Click hello one that starts with *tolldata*.</span></span> <span data-ttu-id="77485-343">按一下 hello**事件中心** 索引標籤。您會在這個命名空間中看到 2 個已建立的事件中樞，分別名為 *entry* 和 *exit*。</span><span class="sxs-lookup"><span data-stu-id="77485-343">Click hello **EVENT HUBS** tab. You will see two event hubs named *entry* and *exit* created in this namespace.</span></span>

![Hello 傳統入口網站中的 [事件中樞] 索引標籤](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a><span data-ttu-id="77485-345">Azure 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="77485-345">Azure Storage container</span></span>
1. <span data-ttu-id="77485-346">返回您的瀏覽器開啟 tooAzure 入口網站中的 toohello 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="77485-346">Go back toohello tab in your browser open tooAzure portal.</span></span> <span data-ttu-id="77485-347">按一下**儲存體**上 hello hello Azure 入口網站 toosee hello Azure 儲存體容器 hello 教學課程中所使用的左方。</span><span class="sxs-lookup"><span data-stu-id="77485-347">Click **STORAGE** on hello left side of hello Azure portal toosee hello Azure Storage container that's used in hello tutorial.</span></span>
   
    ![儲存體功能表項目](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. <span data-ttu-id="77485-349">按一下 hello 開頭的其中一個*tolldata*。</span><span class="sxs-lookup"><span data-stu-id="77485-349">Click hello one that start with *tolldata*.</span></span> <span data-ttu-id="77485-350">按一下 hello**容器** 索引標籤 toosee hello 建立容器。</span><span class="sxs-lookup"><span data-stu-id="77485-350">Click hello **CONTAINERS** tab toosee hello created container.</span></span>
   
    ![在 hello Azure 入口網站中 容器 索引標籤](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. <span data-ttu-id="77485-352">按一下 hello **tolldata**容器 toosee hello 上傳內含車輛註冊資料的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="77485-352">Click hello **tolldata** container toosee hello uploaded JSON file that has vehicle registration data.</span></span>
   
    ![Hello 容器中的 hello registration.json 檔案的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a><span data-ttu-id="77485-354">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="77485-354">Azure SQL Database</span></span>
1. <span data-ttu-id="77485-355">請返回 toohello Azure 入口網站開啟 hello 瀏覽器中的 hello 第一個索引標籤。</span><span class="sxs-lookup"><span data-stu-id="77485-355">Go back toohello Azure portal on hello first tab that was opened in hello browser.</span></span> <span data-ttu-id="77485-356">按一下**SQL 資料庫**上的 hello Azure 入口網站 toosee hello SQL database，將用於 hello 教學課程中，按一下左方的 hello **tolldatadb**。</span><span class="sxs-lookup"><span data-stu-id="77485-356">Click **SQL DATABASES** on hello left side of hello Azure portal toosee hello SQL database that will be used in hello tutorial and click **tolldatadb**.</span></span>
   
    ![Hello 建立 SQL database 的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. <span data-ttu-id="77485-358">複製 hello 伺服器名稱沒有 hello 連接埠號碼 (*servername*。.database.windows.net，例如)。</span><span class="sxs-lookup"><span data-stu-id="77485-358">Copy hello server name without hello port number (*servername*.database.windows.net, for example).</span></span>
    <span data-ttu-id="77485-359">![Hello 建立 SQL 資料庫 db 的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)</span><span class="sxs-lookup"><span data-stu-id="77485-359">![Screenshot of hello created SQL database db](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)</span></span>

## <a name="connect-toohello-database-from-visual-studio"></a><span data-ttu-id="77485-360">從 Visual Studio 中連接 toohello 資料庫</span><span class="sxs-lookup"><span data-stu-id="77485-360">Connect toohello database from Visual Studio</span></span>
<span data-ttu-id="77485-361">您可以使用 Visual Studio tooaccess 查詢結果 hello 輸出資料庫中。</span><span class="sxs-lookup"><span data-stu-id="77485-361">Use Visual Studio tooaccess query results in hello output database.</span></span>

<span data-ttu-id="77485-362">從 Visual Studio 中連接 toohello SQL database （hello 目的地）：</span><span class="sxs-lookup"><span data-stu-id="77485-362">Connect toohello SQL database (hello destination) from Visual Studio:</span></span>

1. <span data-ttu-id="77485-363">開啟 Visual Studio 中，然後再按一下**工具** > **連接 tooDatabase**。</span><span class="sxs-lookup"><span data-stu-id="77485-363">Open Visual Studio, and then click **Tools** > **Connect tooDatabase**.</span></span>
2. <span data-ttu-id="77485-364">如果畫面出現提示，請按一下 [Microsoft SQL Server]  來做為資料來源。</span><span class="sxs-lookup"><span data-stu-id="77485-364">If asked, click **Microsoft SQL Server** as a data source.</span></span>
   
    ![[變更資料來源] 對話方塊](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. <span data-ttu-id="77485-366">在 hello**伺服器名稱**欄位中，貼上從 hello Azure 入口網站複製 hello 前一節中的 hello 名稱 (也就是*servername*。.database.windows.net)。</span><span class="sxs-lookup"><span data-stu-id="77485-366">In hello **Server name** field, paste hello name that you copied in hello previous section from hello Azure portal (that is, *servername*.database.windows.net).</span></span>
4. <span data-ttu-id="77485-367">按一下 [使用 SQL Server 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="77485-367">Click **Use SQL Server Authentication**.</span></span>
5. <span data-ttu-id="77485-368">輸入**tolladmin**在 hello**使用者名**欄位和**123toll ！**</span><span class="sxs-lookup"><span data-stu-id="77485-368">Enter **tolladmin** in hello **User name** field and **123toll!**</span></span> <span data-ttu-id="77485-369">在 hello**密碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="77485-369">in hello **Password** field.</span></span>
6. <span data-ttu-id="77485-370">按一下**選取或輸入資料庫名稱**，然後選取**TollDataDB** hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="77485-370">Click **Select or enter a database name**, and select **TollDataDB** as hello database.</span></span>
   
    ![[新增連線] 對話方塊](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. <span data-ttu-id="77485-372">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="77485-372">Click **OK**.</span></span>
8. <span data-ttu-id="77485-373">開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="77485-373">Open Server Explorer.</span></span>
   
    ![Server Explorer](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. <span data-ttu-id="77485-375">請參閱 hello TollDataDB 資料庫中的四個資料表。</span><span class="sxs-lookup"><span data-stu-id="77485-375">See four tables in hello TollDataDB database.</span></span>
   
    ![Hello TollDataDB 資料庫中的資料表](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a><span data-ttu-id="77485-377">事件產生器：TollApp 範例專案</span><span class="sxs-lookup"><span data-stu-id="77485-377">Event generator: TollApp sample project</span></span>
<span data-ttu-id="77485-378">自動 hello PowerShell 指令碼會使用 hello TollApp 範例應用程式以開始 toosend 事件。</span><span class="sxs-lookup"><span data-stu-id="77485-378">hello PowerShell script automatically starts toosend events by using hello TollApp sample application program.</span></span> <span data-ttu-id="77485-379">您不需要任何額外的步驟 tooperform。</span><span class="sxs-lookup"><span data-stu-id="77485-379">You don’t need tooperform any additional steps.</span></span>

<span data-ttu-id="77485-380">不過，如果您有興趣實作詳細資料，您可以找到 hello hello TollApp 應用程式原始碼 GitHub 中[範例/TollApp](https://aka.ms/azure-stream-analytics-toll-source)。</span><span class="sxs-lookup"><span data-stu-id="77485-380">However, if you are interested in implementation details, you can find hello source code of hello TollApp application in GitHub [samples/TollApp](https://aka.ms/azure-stream-analytics-toll-source).</span></span>

![Visual Studio 中所顯示範例程式碼的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="77485-382">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="77485-382">Create a Stream Analytics job</span></span>
1. <span data-ttu-id="77485-383">在 hello Azure 入口網站，按一下 hello hello 頁面 toocreate hello 左上角中的綠色加號新的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="77485-383">In hello Azure portal, click hello green plus sign in hello top-left corner of hello page toocreate a new Stream Analytics job.</span></span> <span data-ttu-id="77485-384">選取 智慧 + 分析，然後按一下串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="77485-384">Select **Intelligence + Analytics** and then click **Stream Analytics job**.</span></span>
   
    ![New button](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. <span data-ttu-id="77485-386">提供作業名稱、 驗證 hello 訂用帳戶均正確無誤，然後建立新的資源群組在 hello 與 hello 事件中樞的儲存體相同區域 （預設值為美國中南部 hello 指令碼）。</span><span class="sxs-lookup"><span data-stu-id="77485-386">Provide a job name, validate hello subscription is correct and then create a new Resource group in hello same region as hello Event hub storage (default is South Central US for hello script).</span></span>
3. <span data-ttu-id="77485-387">按一下**Pin toodashboard**然後**建立**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="77485-387">Click **Pin toodashboard** and then **CREATE** at hello bottom of hello page.</span></span>
   
    ![[建立串流分析工作] 選項](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a><span data-ttu-id="77485-389">定義輸入來源</span><span class="sxs-lookup"><span data-stu-id="77485-389">Define input sources</span></span>
1. <span data-ttu-id="77485-390">hello 作業會建立和開啟 hello 作業頁面。</span><span class="sxs-lookup"><span data-stu-id="77485-390">hello job will create and open hello job page.</span></span> <span data-ttu-id="77485-391">或者，您可以按一下 hello hello 入口網站儀表板上建立分析工作。</span><span class="sxs-lookup"><span data-stu-id="77485-391">Or you can click hello created analytics job on hello portal dashboard.</span></span>

2. <span data-ttu-id="77485-392">按一下 hello**輸入**toodefine hello 來源資料 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="77485-392">Click hello **INPUTS** tab toodefine hello source data.</span></span>
   
    ![hello 輸入 索引標籤](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. <span data-ttu-id="77485-394">按一下 [加入輸入] 。</span><span class="sxs-lookup"><span data-stu-id="77485-394">Click **ADD AN INPUT**.</span></span>
   
    ![hello 新增輸入選項](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. <span data-ttu-id="77485-396">輸入 **EntryStream** 做為 [輸入別名]。</span><span class="sxs-lookup"><span data-stu-id="77485-396">Enter **EntryStream** as **INPUT ALIAS**.</span></span>
5. <span data-ttu-id="77485-397">[來源類型] 是 [資料流]</span><span class="sxs-lookup"><span data-stu-id="77485-397">Source Type is **Data Stream**</span></span>
6. <span data-ttu-id="77485-398">[來源] 是 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="77485-398">Source is **Event hub**.</span></span>
7. <span data-ttu-id="77485-399">**服務匯流排命名空間**應該的 hello hello TollData 其中一個下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="77485-399">**Service bus namespace** should be hello TollData one in hello drop down.</span></span>
8. <span data-ttu-id="77485-400">**事件中樞名稱**應該設定太**項目**。</span><span class="sxs-lookup"><span data-stu-id="77485-400">**Event hub name** should be set too**entry**.</span></span>
9. <span data-ttu-id="77485-401">**事件中樞原則名稱*是**RootManageSharedAccessKey** (hello 預設值)。</span><span class="sxs-lookup"><span data-stu-id="77485-401">**Event hub policy name*is **RootManageSharedAccessKey**  (hello default value).</span></span>
10. <span data-ttu-id="77485-402">選取 [JSON] 做為 [事件序列化格式]，並選取 [UTF8] 做為 [編碼] 格式。</span><span class="sxs-lookup"><span data-stu-id="77485-402">Select **JSON** for **EVENT SERIALIZATION FORMAT** and **UTF8** for **ENCODING**.</span></span>
   
    <span data-ttu-id="77485-403">您的設定將看起來會像是：</span><span class="sxs-lookup"><span data-stu-id="77485-403">Your settings will look like:</span></span>
   
    ![[事件中樞] 設定](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. <span data-ttu-id="77485-405">按一下**建立**底部 hello hello 頁 toofinish hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="77485-405">Click **Create** at hello bottom of hello page toofinish hello wizard.</span></span>
    
    <span data-ttu-id="77485-406">既然您已建立 hello 項目資料流，您將遵循 hello 相同步驟 toocreate hello 結束資料流。</span><span class="sxs-lookup"><span data-stu-id="77485-406">Now that you've created hello entry stream, you will follow hello same steps toocreate hello exit stream.</span></span> <span data-ttu-id="77485-407">在下列螢幕擷取畫面的 hello 上是確定 tooenter 值。</span><span class="sxs-lookup"><span data-stu-id="77485-407">Be sure tooenter values as on hello following screenshot.</span></span>
    
    ![Hello 結束資料流設定](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    <span data-ttu-id="77485-409">您已經定義了兩個輸入串流：</span><span class="sxs-lookup"><span data-stu-id="77485-409">You have defined two input streams:</span></span>
    
    ![在 hello Azure 入口網站中定義輸入資料流](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    <span data-ttu-id="77485-411">接下來，您將加入包含汽車註冊資料的 hello blob 檔案的參考資料輸入。</span><span class="sxs-lookup"><span data-stu-id="77485-411">Next, you will add reference data input for hello blob file that contains car registration data.</span></span>
11. <span data-ttu-id="77485-412">按一下**新增**，然後遵循相同程序的 hello 資料流輸入，但選取的 hello**參考資料**而不是**資料流**和 hello**輸入別名**是**註冊**。</span><span class="sxs-lookup"><span data-stu-id="77485-412">Click **ADD**, and then follow hello same process for hello stream inputs but select **REFERENCE DATA** instead of **Data Stream** and hello **Input Alias** is **Registration**.</span></span>

12. <span data-ttu-id="77485-413">按一下開頭為 **tolldata** 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="77485-413">storage account that starts with **tolldata**.</span></span> <span data-ttu-id="77485-414">hello 容器名稱應該是**tolldata**，和 hello**路徑模式**應該**registration.json**。</span><span class="sxs-lookup"><span data-stu-id="77485-414">hello container name should be **tolldata**, and hello **PATH PATTERN** should be **registration.json**.</span></span> <span data-ttu-id="77485-415">這個檔案名稱會區分大小寫，且應該是**小寫**。</span><span class="sxs-lookup"><span data-stu-id="77485-415">This file name is case sensitive and should be **lowercase**.</span></span>
    
    ![[部落格儲存體] 設定](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. <span data-ttu-id="77485-417">按一下**建立**toofinish hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="77485-417">Click **Create** toofinish hello wizard.</span></span>

<span data-ttu-id="77485-418">現在，所有輸入都已經定義了。</span><span class="sxs-lookup"><span data-stu-id="77485-418">Now all inputs are defined.</span></span>

## <a name="define-output"></a><span data-ttu-id="77485-419">定義輸出</span><span class="sxs-lookup"><span data-stu-id="77485-419">Define output</span></span>
1. <span data-ttu-id="77485-420">在 hello 資料流分析作業概觀窗格中，選取 **輸出**。</span><span class="sxs-lookup"><span data-stu-id="77485-420">On hello Stream Analytics job overview pane, select **OUTPUTS**.</span></span>
   
    ![hello 輸出 索引標籤和 加入輸出 選項](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. <span data-ttu-id="77485-422">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="77485-422">Click **Add**.</span></span>
3. <span data-ttu-id="77485-423">設定 hello**輸出別名**too'output' 然後**Sink**太**SQL database**。</span><span class="sxs-lookup"><span data-stu-id="77485-423">Set hello **Output alias** too'output' and then **Sink** too**SQL database**.</span></span>
3. <span data-ttu-id="77485-424">選取在 hello hello 文章的 「 從 Visual Studio 連接 tooDatabase 」 一節中的 hello 所使用的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="77485-424">Select hello server name that was used in hello “Connect tooDatabase from Visual Studio” section of hello article.</span></span> <span data-ttu-id="77485-425">hello 資料庫名稱是**TollDataDB**。</span><span class="sxs-lookup"><span data-stu-id="77485-425">hello database name is **TollDataDB**.</span></span>
4. <span data-ttu-id="77485-426">輸入**tolladmin**在 hello **USERNAME**  欄位中， **123toll ！**</span><span class="sxs-lookup"><span data-stu-id="77485-426">Enter **tolladmin** in hello **USERNAME** field, **123toll!**</span></span> <span data-ttu-id="77485-427">在 [hello**密碼**] 欄位中，和**TollDataRefJoin**在 hello**資料表**欄位。</span><span class="sxs-lookup"><span data-stu-id="77485-427">in hello **PASSWORD** field, and **TollDataRefJoin** in hello **TABLE** field.</span></span>
   
    ![SQL Database 設定](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. <span data-ttu-id="77485-429">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="77485-429">Click **Create**.</span></span>

## <a name="azure-stream-analytics-query"></a><span data-ttu-id="77485-430">Azure 串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="77485-430">Azure Stream analytics query</span></span>
<span data-ttu-id="77485-431">hello**查詢** 索引標籤包含轉換 hello 內送資料的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="77485-431">hello **QUERY** tab contains a SQL query that transforms hello incoming data.</span></span>

![查詢加入 toohello 查詢索引標籤](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

<span data-ttu-id="77485-433">本教學課程中嘗試的 tooanswer tootoll 資料以及建構資料流分析查詢，其相關的數個商務問題可在 Azure Stream Analytics tooprovide 相關的回應。</span><span class="sxs-lookup"><span data-stu-id="77485-433">This tutorial attempts tooanswer several business questions that are related tootoll data and constructs Stream Analytics queries that can be used in Azure Stream Analytics tooprovide a relevant answer.</span></span>

<span data-ttu-id="77485-434">在您開始第一個資料流分析工作之前，請讓我們來探索少數的案例和 hello 的查詢語法。</span><span class="sxs-lookup"><span data-stu-id="77485-434">Before you start your first Stream Analytics job, let’s explore a few scenarios and hello query syntax.</span></span>

## <a name="introduction-tooazure-stream-analytics-query-language"></a><span data-ttu-id="77485-435">簡介 tooAzure 串流分析查詢語言</span><span class="sxs-lookup"><span data-stu-id="77485-435">Introduction tooAzure Stream Analytics query language</span></span>
- - -
<span data-ttu-id="77485-436">例如，假設您需要輸入收費亭的車輛 toocount hello 數目。</span><span class="sxs-lookup"><span data-stu-id="77485-436">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="77485-437">因為這是連續的資料流的事件，您有 toodefine 」 期間的時間。 」</span><span class="sxs-lookup"><span data-stu-id="77485-437">Because this is a continuous stream of events, you have toodefine a “period of time.”</span></span> <span data-ttu-id="77485-438">讓我們來修改 hello 問題 toobe 「 多少車輛輸入收費亭每隔三分鐘？ 」。</span><span class="sxs-lookup"><span data-stu-id="77485-438">Let's modify hello question toobe “How many vehicles enter a toll booth every three minutes?”.</span></span> <span data-ttu-id="77485-439">這是通常參照的 tooas hello 輪轉計數。</span><span class="sxs-lookup"><span data-stu-id="77485-439">This is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="77485-440">讓我們看看 hello Azure 串流分析查詢，此問題的答案：</span><span class="sxs-lookup"><span data-stu-id="77485-440">Let’s look at hello Azure Stream Analytics query that answers this question:</span></span>

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

<span data-ttu-id="77485-441">如您所見，Azure 串流分析會使用類似 SQL 的查詢語言加入幾個擴充功能 toospecify 時間相關的層面 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="77485-441">As you can see, Azure Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="77485-442">如需詳細資訊，閱讀[時間管理](https://msdn.microsoft.com/library/azure/mt582045.aspx)和[Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx)從 MSDN 的 hello 查詢中使用的建構。</span><span class="sxs-lookup"><span data-stu-id="77485-442">For more details, read about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

## <a name="testing-azure-stream-analytics-queries"></a><span data-ttu-id="77485-443">測試 Azure 串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="77485-443">Testing Azure Stream Analytics queries</span></span>
<span data-ttu-id="77485-444">既然您已經撰寫第一個 Azure 資料流分析查詢，它是時間 tootest 它藉由使用範例資料檔案位於下列路徑的 hello 中您 TollApp 資料夾中：</span><span class="sxs-lookup"><span data-stu-id="77485-444">Now that you have written your first Azure Stream Analytics query, it is time tootest it by using sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="77485-445">**..\\TollApp\\TollApp\\Data**</span><span class="sxs-lookup"><span data-stu-id="77485-445">**..\\TollApp\\TollApp\\Data**</span></span>

<span data-ttu-id="77485-446">此資料夾包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="77485-446">This folder contains hello following files:</span></span>

* <span data-ttu-id="77485-447">Entry.json</span><span class="sxs-lookup"><span data-stu-id="77485-447">Entry.json</span></span>
* <span data-ttu-id="77485-448">Exit.json</span><span class="sxs-lookup"><span data-stu-id="77485-448">Exit.json</span></span>
* <span data-ttu-id="77485-449">registration.json</span><span class="sxs-lookup"><span data-stu-id="77485-449">Registration.json</span></span>

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="77485-450">問題 1：進入某個收費亭的車輛數目</span><span class="sxs-lookup"><span data-stu-id="77485-450">Question 1: Number of vehicles entering a toll booth</span></span>
1. <span data-ttu-id="77485-451">開啟 hello Azure 入口網站，並移 tooyour 建立 Azure 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="77485-451">Open hello Azure portal and go tooyour created Azure Stream Analytics job.</span></span> <span data-ttu-id="77485-452">按一下 hello**查詢**索引標籤，然後貼上查詢 hello 前一節。</span><span class="sxs-lookup"><span data-stu-id="77485-452">Click hello **QUERY** tab and paste query from hello previous section.</span></span>

2. <span data-ttu-id="77485-453">toovalidate 這項查詢針對取樣資料，hello EntryStream 輸入，按一下 上傳 hello 資料...hello 符號，然後選取**從檔案的範例資料上傳**。</span><span class="sxs-lookup"><span data-stu-id="77485-453">toovalidate this query against sample data, upload hello data into hello EntryStream input by clicking hello ... symbol and selecting **Upload sample data from file**.</span></span>

    ![Hello Entry.json 檔案的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. <span data-ttu-id="77485-455">在您本機電腦，並按一下上顯示選取的 hello 檔案 (Entry.json) hello 窗格中**確定**。</span><span class="sxs-lookup"><span data-stu-id="77485-455">In hello pane that appears select hello file (Entry.json) on your local machine and click **OK**.</span></span> <span data-ttu-id="77485-456">hello**測試**圖示現在會在照亮，並能按。</span><span class="sxs-lookup"><span data-stu-id="77485-456">hello **Test** icon will now illuminate and be clickable.</span></span>
   
    ![Hello Entry.json 檔案的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. <span data-ttu-id="77485-458">驗證 hello 查詢的 hello 輸出如預期般：</span><span class="sxs-lookup"><span data-stu-id="77485-458">Validate that hello output of hello query is as expected:</span></span>
   
    ![Hello 測試的結果](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a><span data-ttu-id="77485-460">問題 2： 報告之每個透過 hello 收費亭的車輛 toopass 時間總計</span><span class="sxs-lookup"><span data-stu-id="77485-460">Question 2: Report total time for each car toopass through hello toll booth</span></span>
<span data-ttu-id="77485-461">hello 透過 hello 收費站的汽車 toopass 所需的平均時間有助於 hello 程序和 hello 客戶經驗 tooassess hello 效率。</span><span class="sxs-lookup"><span data-stu-id="77485-461">hello average time that's required for a car toopass through hello toll helps tooassess hello efficiency of hello process and hello customer experience.</span></span>

<span data-ttu-id="77485-462">toofind hello 總時間，您需要 toojoin hello EntryTime 資料流與 hello ExitTime 資料流。</span><span class="sxs-lookup"><span data-stu-id="77485-462">toofind hello total time, you need toojoin hello EntryTime stream with hello ExitTime stream.</span></span> <span data-ttu-id="77485-463">您會加入 hello TollId 且 LicencePlate 資料行上的資料流。</span><span class="sxs-lookup"><span data-stu-id="77485-463">You will join hello streams on TollId and LicencePlate columns.</span></span> <span data-ttu-id="77485-464">hello**聯結**運算子則需要一個 toospecify 時態彈性以描述 hello 差異 hello 加入事件可接受的時間。</span><span class="sxs-lookup"><span data-stu-id="77485-464">hello **JOIN** operator requires you toospecify temporal leeway that describes hello acceptable time difference between hello joined events.</span></span> <span data-ttu-id="77485-465">您將使用**DATEDIFF**函式 toospecify 事件應該彼此不超過 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="77485-465">You will use **DATEDIFF** function toospecify that events should be no more than 15 minutes from each other.</span></span> <span data-ttu-id="77485-466">您也會套用 hello **DATEDIFF**函式 tooexit 和 toocompute hello 實際的時間花在 hello 的汽車時間的項目付費站台。</span><span class="sxs-lookup"><span data-stu-id="77485-466">You will also apply hello **DATEDIFF** function tooexit and entry times toocompute hello actual time that a car spends in hello toll station.</span></span> <span data-ttu-id="77485-467">請注意 hello 用途的 hello 差異**DATEDIFF**使用中時**選取**陳述式而非**聯結**條件。</span><span class="sxs-lookup"><span data-stu-id="77485-467">Note hello difference of hello use of **DATEDIFF** when it's used in a **SELECT** statement rather than a **JOIN** condition.</span></span>

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. <span data-ttu-id="77485-468">tootest 此查詢中，更新 hello 查詢上 hello**查詢**hello 作業。</span><span class="sxs-lookup"><span data-stu-id="77485-468">tootest this query, update hello query on hello **QUERY** for hello job.</span></span> <span data-ttu-id="77485-469">加入 hello 測試檔案，如**ExitStream**一樣**EntryStream**輸入上方。</span><span class="sxs-lookup"><span data-stu-id="77485-469">Add hello test file for **ExitStream** just like **EntryStream** was entered above.</span></span>
   
2. <span data-ttu-id="77485-470">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="77485-470">Click **Test**.</span></span>

3. <span data-ttu-id="77485-471">選取 [hello] 核取方塊 tootest hello 查詢和檢視表 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="77485-471">Select hello check box tootest hello query and view hello output:</span></span>
   
    ![Hello 測試的輸出](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a><span data-ttu-id="77485-473">問題 3：回報所有車輛登記已過期的商用車</span><span class="sxs-lookup"><span data-stu-id="77485-473">Question 3: Report all commercial vehicles with expired registration</span></span>
<span data-ttu-id="77485-474">Azure Stream Analytics 可以暫時資料資料流使用資料 toojoin 靜態快照的集。</span><span class="sxs-lookup"><span data-stu-id="77485-474">Azure Stream Analytics can use static snapshots of data toojoin with temporal data streams.</span></span> <span data-ttu-id="77485-475">toodemonstrate 這項功能，使用 hello 遵循範例問題。</span><span class="sxs-lookup"><span data-stu-id="77485-475">toodemonstrate this capability, use hello following sample question.</span></span>

<span data-ttu-id="77485-476">如果與 hello 通行費管理公司註冊商用車輛，它可以通過 hello 收費亭不需停車檢查。</span><span class="sxs-lookup"><span data-stu-id="77485-476">If a commercial vehicle is registered with hello toll company, it can pass through hello toll booth without being stopped for inspection.</span></span> <span data-ttu-id="77485-477">您將使用商用車輛註冊查閱資料表 tooidentify 所有註冊過期的商用車輛。</span><span class="sxs-lookup"><span data-stu-id="77485-477">You will use Commercial Vehicle Registration lookup table tooidentify all commercial vehicles that have expired registrations.</span></span>

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

<span data-ttu-id="77485-478">tootest 使用參考資料的查詢，您會需要 toodefine 輸入來源 hello 參考資料，您已經完成。</span><span class="sxs-lookup"><span data-stu-id="77485-478">tootest a query by using reference data, you need toodefine an input source for hello reference data, which you have done already.</span></span>

<span data-ttu-id="77485-479">tootest 此查詢中，貼上 hello 查詢貼入 hello**查詢**索引標籤上，按一下 **測試**，並指定 hello 兩個輸入的來源並 hello 註冊範例資料，然後按一下**測試**。</span><span class="sxs-lookup"><span data-stu-id="77485-479">tootest this query, paste hello query into hello **QUERY** tab, click **Test**, and specify hello two input sources and hello registration sample data and click **Test**.</span></span>  
   
![Hello 測試的輸出](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="77485-481">啟動 hello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="77485-481">Start hello Stream Analytics job</span></span>
<span data-ttu-id="77485-482">現在它是時間 toofinish hello 設定和開始 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="77485-482">Now it's time toofinish hello configuration and start hello job.</span></span> <span data-ttu-id="77485-483">問題 3，會產生相符項目 hello hello 的結構描述的輸出儲存 hello 查詢**TollDataRefJoin**輸出資料表。</span><span class="sxs-lookup"><span data-stu-id="77485-483">Save hello query from Question 3, which will produce output that matches hello schema of hello **TollDataRefJoin** output table.</span></span>

<span data-ttu-id="77485-484">移 toohello 作業**儀表板**，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="77485-484">Go toohello job **DASHBOARD**, and click **START**.</span></span>

![Hello 作業儀表板中的 hello 開始 按鈕的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

<span data-ttu-id="77485-486">在 hello 開啟對話方塊，變更 hello**開始輸出**時間太**自訂時間**。</span><span class="sxs-lookup"><span data-stu-id="77485-486">In hello dialog box that opens, change hello **START OUTPUT** time too**CUSTOM TIME**.</span></span> <span data-ttu-id="77485-487">變更 hello 小時 tooone 小時 hello 目前時間之前。</span><span class="sxs-lookup"><span data-stu-id="77485-487">Change hello hour tooone hour before hello current time.</span></span> <span data-ttu-id="77485-488">這項變更可確保您在 hello 教學課程的 hello 開頭開始 toogenerate hello 事件之後處理的 hello 事件中心的所有事件。</span><span class="sxs-lookup"><span data-stu-id="77485-488">This change ensures that all events from hello event hub are processed since you started toogenerate hello events at hello beginning of hello tutorial.</span></span> <span data-ttu-id="77485-489">現在按一下 hello**啟動**按鈕 toostart hello 作業。</span><span class="sxs-lookup"><span data-stu-id="77485-489">Now click hello **Start** button toostart hello job.</span></span>

![自訂時間的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

<span data-ttu-id="77485-491">開始 hello 工作可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="77485-491">Starting hello job can take a few minutes.</span></span> <span data-ttu-id="77485-492">您可以在資料流分析的 hello 最上層頁面上查看 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="77485-492">You can see hello status on hello top-level page for Stream Analytics.</span></span>

![Hello hello 工作狀態的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a><span data-ttu-id="77485-494">在 Visual Studio 中查看結果</span><span class="sxs-lookup"><span data-stu-id="77485-494">Check results in Visual Studio</span></span>
1. <span data-ttu-id="77485-495">開啟 Visual Studio 伺服器總管 中，並以滑鼠右鍵按一下 hello **TollDataRefJoin**資料表。</span><span class="sxs-lookup"><span data-stu-id="77485-495">Open Visual Studio Server Explorer, and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="77485-496">按一下**顯示資料表資料**toosee hello 輸出的工作。</span><span class="sxs-lookup"><span data-stu-id="77485-496">Click **Show Table Data** toosee hello output of your job.</span></span>
   
    ![伺服器總管中 [顯示資料表資料] 的選取項目](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a><span data-ttu-id="77485-498">相應放大 Azure 串流分析工作</span><span class="sxs-lookup"><span data-stu-id="77485-498">Scale out Azure Stream Analytics jobs</span></span>
<span data-ttu-id="77485-499">Azure Stream Analytics 設計 tooelastically 調整，好讓它可以處理大量資料。</span><span class="sxs-lookup"><span data-stu-id="77485-499">Azure Stream Analytics is designed tooelastically scale so that it can handle a lot of data.</span></span> <span data-ttu-id="77485-500">hello Azure Stream Analytics 查詢就可以使用**PARTITION BY**子句 tootell hello 系統，此步驟會向外延展。**PartitionId**在於 hello 系統的特殊資料行加入 toomatch hello 資料分割識別碼 hello 輸入 （事件中心）。</span><span class="sxs-lookup"><span data-stu-id="77485-500">hello Azure Stream Analytics query can use a **PARTITION BY** clause tootell hello system that this step will scale out. **PartitionId** is a special column that hello system adds toomatch hello partition ID of hello input (event hub).</span></span>

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. <span data-ttu-id="77485-501">停止 hello 目前的工作，在 hello 更新 hello 查詢**查詢**索引標籤，然後開啟 hello**設定**齒輪 hello 作業儀表板中。</span><span class="sxs-lookup"><span data-stu-id="77485-501">Stop hello current job, update hello query in hello **QUERY** tab, and open hello **Settings** gear in hello job dashboard.</span></span> <span data-ttu-id="77485-502">按一下 [調整] 。</span><span class="sxs-lookup"><span data-stu-id="77485-502">Click **Scale**.</span></span>
   
    <span data-ttu-id="77485-503">**串流單位**定義可以收到 hello 數量 hello 工作的運算能力。</span><span class="sxs-lookup"><span data-stu-id="77485-503">**STREAMING UNITS** define hello amount of compute power that hello job can receive.</span></span>
2. <span data-ttu-id="77485-504">變更 hello 下拉式清單從 6 1。</span><span class="sxs-lookup"><span data-stu-id="77485-504">Change hello drop down from 1 from 6.</span></span>
   
    ![選取 6 個串流處理單位的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. <span data-ttu-id="77485-506">移 toohello**輸出**索引標籤，然後變更 hello hello SQL 資料表名稱太**TollDataTumblingCountPartitioned**。</span><span class="sxs-lookup"><span data-stu-id="77485-506">Go toohello **OUTPUTS** tab and change hello name of hello SQL table too**TollDataTumblingCountPartitioned**.</span></span>

<span data-ttu-id="77485-507">如果您啟動 hello 作業現在，Azure Stream Analytics 中可以將工作分散到運算資源就愈，達到更佳的輸送量。</span><span class="sxs-lookup"><span data-stu-id="77485-507">If you start hello job now, Azure Stream Analytics can distribute work across more compute resources and achieve better throughput.</span></span> <span data-ttu-id="77485-508">請注意該 hello TollApp 應用程式也會傳送事件的 TollId 來分割。</span><span class="sxs-lookup"><span data-stu-id="77485-508">Please note that hello TollApp application is also sending events partitioned by TollId.</span></span>

## <a name="monitor"></a><span data-ttu-id="77485-509">監視</span><span class="sxs-lookup"><span data-stu-id="77485-509">Monitor</span></span>
<span data-ttu-id="77485-510">hello**監視器**區域包含正在執行工作的 hello 相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="77485-510">hello **MONITOR** area contains statistics about hello running job.</span></span> <span data-ttu-id="77485-511">第一次設定時所需的 hello toouse hello 儲存體帳戶相同的區域 （例如 hello 這份文件其餘部分的名稱付費電話）。</span><span class="sxs-lookup"><span data-stu-id="77485-511">First time configuration is needed toouse hello storage account in hello same region (name toll like hello rest of this document).</span></span>   

![監視螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

<span data-ttu-id="77485-513">您可以存取**活動記錄**從 hello 作業儀表板**設定**以及區域。</span><span class="sxs-lookup"><span data-stu-id="77485-513">You can access **Activity Logs** from hello job dashboard **Settings** area as well.</span></span>


## <a name="conclusion"></a><span data-ttu-id="77485-514">結論</span><span class="sxs-lookup"><span data-stu-id="77485-514">Conclusion</span></span>
<span data-ttu-id="77485-515">本教學課程會引進 toohello Azure Stream Analytics 服務。</span><span class="sxs-lookup"><span data-stu-id="77485-515">This tutorial introduced you toohello Azure Stream Analytics service.</span></span> <span data-ttu-id="77485-516">它所示範的 tooconfigure 輸入和輸出 hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="77485-516">It demonstrated how tooconfigure inputs and outputs for hello Stream Analytics job.</span></span> <span data-ttu-id="77485-517">Hello 教學課程使用 hello 付費資料案例，說明常見的 hello 空間中的資料移動，以及如何解決使用簡單的類似 SQL 的查詢，在 Azure Stream Analytics 中發生的問題。</span><span class="sxs-lookup"><span data-stu-id="77485-517">Using hello Toll Data scenario, hello tutorial explained common types of problems that arise in hello space of data in motion and how they can be solved with simple SQL-like queries in Azure Stream Analytics.</span></span> <span data-ttu-id="77485-518">hello 教學課程所述使用暫存資料的 SQL 延伸模組建構。</span><span class="sxs-lookup"><span data-stu-id="77485-518">hello tutorial described SQL extension constructs for working with temporal data.</span></span> <span data-ttu-id="77485-519">它示範了如何 toojoin 資料流，tooenrich hello 資料流與靜態參考資料，以及如何 tooscale 出查詢 tooachieve 更高的輸送量。</span><span class="sxs-lookup"><span data-stu-id="77485-519">It showed how toojoin data streams, how tooenrich hello data stream with static reference data, and how tooscale out a query tooachieve higher throughput.</span></span>

<span data-ttu-id="77485-520">雖然本教學課程提供了詳盡的簡介，但也絕對不算是完整的說明。</span><span class="sxs-lookup"><span data-stu-id="77485-520">Although this tutorial provides a good introduction, it is not complete by any means.</span></span> <span data-ttu-id="77485-521">您可以找到多個查詢模式使用在 hello SAQL 語言[查詢常見的資料流分析使用模式的範例](stream-analytics-stream-analytics-query-patterns.md)。</span><span class="sxs-lookup"><span data-stu-id="77485-521">You can find more query patterns using hello SAQL language at [Query examples for common Stream Analytics usage patterns](stream-analytics-stream-analytics-query-patterns.md).</span></span>
<span data-ttu-id="77485-522">請參閱 toohello[線上文件](https://azure.microsoft.com/documentation/services/stream-analytics/)toolearn 深入了解 Azure Stream Analytics。</span><span class="sxs-lookup"><span data-stu-id="77485-522">Refer toohello [online documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn more about Azure Stream Analytics.</span></span>

## <a name="clean-up-your-azure-account"></a><span data-ttu-id="77485-523">清理您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="77485-523">Clean up your Azure account</span></span>
1. <span data-ttu-id="77485-524">停止 hello hello Azure 入口網站中的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="77485-524">Stop hello Stream Analytics job in hello Azure portal.</span></span>
   
    <span data-ttu-id="77485-525">hello Setup.ps1 指令碼會建立兩個事件中心 」 和 「 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="77485-525">hello Setup.ps1 script creates two event hubs and a SQL database.</span></span> <span data-ttu-id="77485-526">下列指示說明清除資源在 hello hello 教學課程結尾處的 hello。</span><span class="sxs-lookup"><span data-stu-id="77485-526">hello following instructions help you clean up resources at hello end of hello tutorial.</span></span>
2. <span data-ttu-id="77485-527">在 PowerShell 視窗中，輸入**。\\Cleanup.ps1** toostart hello 指令碼，以刪除 hello 教學課程中使用的資源。</span><span class="sxs-lookup"><span data-stu-id="77485-527">In a PowerShell window, type **.\\Cleanup.ps1** toostart hello script that deletes resources used in hello tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="77485-528">Hello 名稱所識別的資源。</span><span class="sxs-lookup"><span data-stu-id="77485-528">Resources are identified by hello name.</span></span> <span data-ttu-id="77485-529">請確認您在確認刪除之前，已仔細檢閱每個項目。</span><span class="sxs-lookup"><span data-stu-id="77485-529">Make sure you carefully review each item before confirming removal.</span></span>
   > 
   > 


