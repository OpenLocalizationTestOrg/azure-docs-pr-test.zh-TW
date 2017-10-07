---
title: "aaaDeep 深入了解預測一種載具，健全狀況和驅動習慣-Azure |Microsoft 文件"
description: "一種載具，健全狀況使用 Cortana 智慧 toogain 即時和預測 insights hello 功能和驅動習慣。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="3d5cc-103">一種載具遙測分析方案腳本： hello 方案深入探討</span><span class="sxs-lookup"><span data-stu-id="3d5cc-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="3d5cc-104">這**功能表**連結此腳本 toohello 區段：</span><span class="sxs-lookup"><span data-stu-id="3d5cc-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="3d5cc-105">此區段向下切入到每個所述的指示和指標以自訂的解決方案架構 hello hello 階段。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="3d5cc-106">資料來源</span><span class="sxs-lookup"><span data-stu-id="3d5cc-106">Data Sources</span></span>
<span data-ttu-id="3d5cc-107">hello 解決方案會使用兩個不同的資料來源：</span><span class="sxs-lookup"><span data-stu-id="3d5cc-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="3d5cc-108">**模擬車輛訊號和診斷資料集** 和</span><span class="sxs-lookup"><span data-stu-id="3d5cc-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="3d5cc-109">**車輛類別目錄**</span><span class="sxs-lookup"><span data-stu-id="3d5cc-109">**vehicle catalog**</span></span>

<span data-ttu-id="3d5cc-110">此方案包含車輛遠程資訊服務模擬器。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="3d5cc-111">它會發出診斷資訊，並發出對應 toohello 狀態 hello vehicle 和 toohello 時間推動特定時點的模式。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="3d5cc-112">按一下[Vehicle 車用通訊模擬器](http://go.microsoft.com/fwlink/?LinkId=717075)toodownload hello **Vehicle 車用通訊模擬器 Visual Studio 方案**適用於您的需求為基礎的自訂。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="3d5cc-113">hello vehicle 類別目錄含有 VIN toomodel 對應的參考資料集。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![車輛遠程資訊服務模擬器](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="3d5cc-115">圖 1 – 車輛遠程資訊服務模擬器</span><span class="sxs-lookup"><span data-stu-id="3d5cc-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="3d5cc-116">這是 JSON 格式的資料集，其中包含下列結構描述的 hello。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="3d5cc-117">資料欄</span><span class="sxs-lookup"><span data-stu-id="3d5cc-117">Column</span></span> | <span data-ttu-id="3d5cc-118">說明</span><span class="sxs-lookup"><span data-stu-id="3d5cc-118">Description</span></span> | <span data-ttu-id="3d5cc-119">值</span><span class="sxs-lookup"><span data-stu-id="3d5cc-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3d5cc-120">VIN</span><span class="sxs-lookup"><span data-stu-id="3d5cc-120">VIN</span></span> |<span data-ttu-id="3d5cc-121">隨機產生的車輛識別號碼</span><span class="sxs-lookup"><span data-stu-id="3d5cc-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="3d5cc-122">這取自於一份含有 10,000 個隨機產生車輛識別號碼的主要清單。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="3d5cc-123">Outside temperature</span><span class="sxs-lookup"><span data-stu-id="3d5cc-123">Outside temperature</span></span> |<span data-ttu-id="3d5cc-124">hello 外溫度 hello vehicle 驅動的位置</span><span class="sxs-lookup"><span data-stu-id="3d5cc-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="3d5cc-125">從 0-100 隨機產生的數字</span><span class="sxs-lookup"><span data-stu-id="3d5cc-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="3d5cc-126">Engine temperature</span><span class="sxs-lookup"><span data-stu-id="3d5cc-126">Engine temperature</span></span> |<span data-ttu-id="3d5cc-127">hello 汽車的 hello 引擎溫度</span><span class="sxs-lookup"><span data-stu-id="3d5cc-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="3d5cc-128">從 0-500 隨機產生的數字</span><span class="sxs-lookup"><span data-stu-id="3d5cc-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="3d5cc-129">速度</span><span class="sxs-lookup"><span data-stu-id="3d5cc-129">Speed</span></span> |<span data-ttu-id="3d5cc-130">一種載具，隨著控制在哪些 hello hello 引擎速度</span><span class="sxs-lookup"><span data-stu-id="3d5cc-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="3d5cc-131">從 0-100 隨機產生的數字</span><span class="sxs-lookup"><span data-stu-id="3d5cc-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="3d5cc-132">Fuel</span><span class="sxs-lookup"><span data-stu-id="3d5cc-132">Fuel</span></span> |<span data-ttu-id="3d5cc-133">hello vehicle hello 燃料層級</span><span class="sxs-lookup"><span data-stu-id="3d5cc-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="3d5cc-134">從 0-100 隨機產生的數字 (表示燃油量百分比)</span><span class="sxs-lookup"><span data-stu-id="3d5cc-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="3d5cc-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="3d5cc-135">EngineOil</span></span> |<span data-ttu-id="3d5cc-136">hello 的 hello 汽車引擎石油層級</span><span class="sxs-lookup"><span data-stu-id="3d5cc-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="3d5cc-137">從 0-100 隨機產生的數字 (表示機油量百分比)</span><span class="sxs-lookup"><span data-stu-id="3d5cc-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="3d5cc-138">胎壓</span><span class="sxs-lookup"><span data-stu-id="3d5cc-138">Tire pressure</span></span> |<span data-ttu-id="3d5cc-139">hello 汽車的 hello tire 壓力</span><span class="sxs-lookup"><span data-stu-id="3d5cc-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="3d5cc-140">從 0-50 隨機產生的數字 (表示胎壓位準百分比)</span><span class="sxs-lookup"><span data-stu-id="3d5cc-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="3d5cc-141">Odometer</span><span class="sxs-lookup"><span data-stu-id="3d5cc-141">Odometer</span></span> |<span data-ttu-id="3d5cc-142">hello 里程計讀取的一種載具，hello</span><span class="sxs-lookup"><span data-stu-id="3d5cc-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="3d5cc-143">從 0-200000 隨機產生的數字</span><span class="sxs-lookup"><span data-stu-id="3d5cc-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="3d5cc-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="3d5cc-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="3d5cc-145">hello accelerator 踏板位置的一種載具，hello</span><span class="sxs-lookup"><span data-stu-id="3d5cc-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="3d5cc-146">從 0-100 隨機產生的數字 (表示油門位準百分比)</span><span class="sxs-lookup"><span data-stu-id="3d5cc-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="3d5cc-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="3d5cc-147">Parking_brake_status</span></span> |<span data-ttu-id="3d5cc-148">指出是否駐留 hello vehicle</span><span class="sxs-lookup"><span data-stu-id="3d5cc-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="3d5cc-149">True 或 False</span><span class="sxs-lookup"><span data-stu-id="3d5cc-149">True or False</span></span> |
| <span data-ttu-id="3d5cc-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="3d5cc-150">Headlamp_status</span></span> |<span data-ttu-id="3d5cc-151">指出其中 hello headlamp 上為</span><span class="sxs-lookup"><span data-stu-id="3d5cc-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="3d5cc-152">True 或 False</span><span class="sxs-lookup"><span data-stu-id="3d5cc-152">True or False</span></span> |
| <span data-ttu-id="3d5cc-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="3d5cc-153">Brake_pedal_status</span></span> |<span data-ttu-id="3d5cc-154">指出是否 hello 剎車組踏板或不已按下</span><span class="sxs-lookup"><span data-stu-id="3d5cc-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="3d5cc-155">True 或 False</span><span class="sxs-lookup"><span data-stu-id="3d5cc-155">True or False</span></span> |
| <span data-ttu-id="3d5cc-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="3d5cc-156">Transmission_gear_position</span></span> |<span data-ttu-id="3d5cc-157">hello 車輛的 hello 傳輸齒輪位置</span><span class="sxs-lookup"><span data-stu-id="3d5cc-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="3d5cc-158">狀態：first、second、third、fourth、fifth、sixth、seventh、eighth</span><span class="sxs-lookup"><span data-stu-id="3d5cc-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="3d5cc-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="3d5cc-159">Ignition_status</span></span> |<span data-ttu-id="3d5cc-160">表示一種載具，hello 執行或完全停止</span><span class="sxs-lookup"><span data-stu-id="3d5cc-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="3d5cc-161">True 或 False</span><span class="sxs-lookup"><span data-stu-id="3d5cc-161">True or False</span></span> |
| <span data-ttu-id="3d5cc-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="3d5cc-162">Windshield_wiper_status</span></span> |<span data-ttu-id="3d5cc-163">指出是否 hello 擋風玻璃挪移或未開啟</span><span class="sxs-lookup"><span data-stu-id="3d5cc-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="3d5cc-164">True 或 False</span><span class="sxs-lookup"><span data-stu-id="3d5cc-164">True or False</span></span> |
| <span data-ttu-id="3d5cc-165">ABS</span><span class="sxs-lookup"><span data-stu-id="3d5cc-165">ABS</span></span> |<span data-ttu-id="3d5cc-166">指出 ABS 是否發揮作用</span><span class="sxs-lookup"><span data-stu-id="3d5cc-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="3d5cc-167">True 或 False</span><span class="sxs-lookup"><span data-stu-id="3d5cc-167">True or False</span></span> |
| <span data-ttu-id="3d5cc-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="3d5cc-168">Timestamp</span></span> |<span data-ttu-id="3d5cc-169">hello 建立 hello 資料點時的時間戳記</span><span class="sxs-lookup"><span data-stu-id="3d5cc-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="3d5cc-170">Date</span><span class="sxs-lookup"><span data-stu-id="3d5cc-170">Date</span></span> |
| <span data-ttu-id="3d5cc-171">City</span><span class="sxs-lookup"><span data-stu-id="3d5cc-171">City</span></span> |<span data-ttu-id="3d5cc-172">一種載具，hello 的 hello 位置</span><span class="sxs-lookup"><span data-stu-id="3d5cc-172">hello location of hello vehicle</span></span> |<span data-ttu-id="3d5cc-173">此方案中有 4 個城市：Bellevue、Redmond、Sammamish、Seattle</span><span class="sxs-lookup"><span data-stu-id="3d5cc-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="3d5cc-174">hello vehicle 模型參考資料集包含 VIN toohello 模型對應。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="3d5cc-175">VIN</span><span class="sxs-lookup"><span data-stu-id="3d5cc-175">VIN</span></span> | <span data-ttu-id="3d5cc-176">模型</span><span class="sxs-lookup"><span data-stu-id="3d5cc-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="3d5cc-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="3d5cc-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="3d5cc-178">轎車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-178">Sedan</span></span> |
| <span data-ttu-id="3d5cc-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="3d5cc-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="3d5cc-180">混合式</span><span class="sxs-lookup"><span data-stu-id="3d5cc-180">Hybrid</span></span> |
| <span data-ttu-id="3d5cc-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="3d5cc-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="3d5cc-182">家庭房車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-182">Family Saloon</span></span> |
| <span data-ttu-id="3d5cc-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="3d5cc-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="3d5cc-184">轎車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-184">Sedan</span></span> |
| <span data-ttu-id="3d5cc-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="3d5cc-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="3d5cc-186">混合式</span><span class="sxs-lookup"><span data-stu-id="3d5cc-186">Hybrid</span></span> |
| <span data-ttu-id="3d5cc-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="3d5cc-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="3d5cc-188">家庭房車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-188">Family Saloon</span></span> |
| <span data-ttu-id="3d5cc-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="3d5cc-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="3d5cc-190">轎車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-190">Sedan</span></span> |
| <span data-ttu-id="3d5cc-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="3d5cc-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="3d5cc-192">混合式</span><span class="sxs-lookup"><span data-stu-id="3d5cc-192">Hybrid</span></span> |
| <span data-ttu-id="3d5cc-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="3d5cc-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="3d5cc-194">家庭房車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-194">Family Saloon</span></span> |
| <span data-ttu-id="3d5cc-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="3d5cc-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="3d5cc-196">敞篷車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-196">Convertible</span></span> |
| <span data-ttu-id="3d5cc-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="3d5cc-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="3d5cc-198">旅行車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-198">Station Wagon</span></span> |
| <span data-ttu-id="3d5cc-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="3d5cc-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="3d5cc-200">小型車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-200">Compact Car</span></span> |
| <span data-ttu-id="3d5cc-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="3d5cc-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="3d5cc-202">小型 SUV</span><span class="sxs-lookup"><span data-stu-id="3d5cc-202">Small SUV</span></span> |
| <span data-ttu-id="3d5cc-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="3d5cc-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="3d5cc-204">跑車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-204">Sports Car</span></span> |
| <span data-ttu-id="3d5cc-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="3d5cc-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="3d5cc-206">中型 SUV</span><span class="sxs-lookup"><span data-stu-id="3d5cc-206">Medium SUV</span></span> |
| <span data-ttu-id="3d5cc-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="3d5cc-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="3d5cc-208">旅行車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-208">Station Wagon</span></span> |
| <span data-ttu-id="3d5cc-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="3d5cc-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="3d5cc-210">大型 SUV</span><span class="sxs-lookup"><span data-stu-id="3d5cc-210">Large SUV</span></span> |
| <span data-ttu-id="3d5cc-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="3d5cc-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="3d5cc-212">大型 SUV</span><span class="sxs-lookup"><span data-stu-id="3d5cc-212">Large SUV</span></span> |
| <span data-ttu-id="3d5cc-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="3d5cc-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="3d5cc-214">兩人座轎車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-214">Coupe</span></span> |
| <span data-ttu-id="3d5cc-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="3d5cc-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="3d5cc-216">轎車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-216">Sedan</span></span> |
| <span data-ttu-id="3d5cc-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="3d5cc-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="3d5cc-218">混合式</span><span class="sxs-lookup"><span data-stu-id="3d5cc-218">Hybrid</span></span> |
| <span data-ttu-id="3d5cc-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="3d5cc-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="3d5cc-220">家庭房車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-220">Family Saloon</span></span> |
| <span data-ttu-id="3d5cc-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="3d5cc-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="3d5cc-222">轎車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-222">Sedan</span></span> |
| <span data-ttu-id="3d5cc-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="3d5cc-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="3d5cc-224">混合式</span><span class="sxs-lookup"><span data-stu-id="3d5cc-224">Hybrid</span></span> |
| <span data-ttu-id="3d5cc-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="3d5cc-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="3d5cc-226">家庭房車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-226">Family Saloon</span></span> |
| <span data-ttu-id="3d5cc-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="3d5cc-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="3d5cc-228">轎車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-228">Sedan</span></span> |
| <span data-ttu-id="3d5cc-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="3d5cc-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="3d5cc-230">混合式</span><span class="sxs-lookup"><span data-stu-id="3d5cc-230">Hybrid</span></span> |
| <span data-ttu-id="3d5cc-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="3d5cc-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="3d5cc-232">家庭房車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-232">Family Saloon</span></span> |
| <span data-ttu-id="3d5cc-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="3d5cc-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="3d5cc-234">敞篷車</span><span class="sxs-lookup"><span data-stu-id="3d5cc-234">Convertible</span></span> |
| <span data-ttu-id="3d5cc-235">…….</span><span class="sxs-lookup"><span data-stu-id="3d5cc-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="3d5cc-236">參考</span><span class="sxs-lookup"><span data-stu-id="3d5cc-236">References</span></span>
[<span data-ttu-id="3d5cc-237">Vehicle Telematics Simulator Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="3d5cc-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="3d5cc-238">Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="3d5cc-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="3d5cc-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3d5cc-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="3d5cc-240">擷取</span><span class="sxs-lookup"><span data-stu-id="3d5cc-240">Ingestion</span></span>
<span data-ttu-id="3d5cc-241">Azure 事件中樞、 Stream Analytics 中，與 Data Factory 的組合會運用 tooingest hello vehicle 訊號，hello 診斷事件，與即時和批次分析。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="3d5cc-242">所有這些元件建立和設定為 hello 方案部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="3d5cc-243">即時分析</span><span class="sxs-lookup"><span data-stu-id="3d5cc-243">Real-time analysis</span></span>
<span data-ttu-id="3d5cc-244">hello hello Vehicle 車用通訊模擬器所產生的事件發行 toohello 事件中心使用 hello 事件中樞 SDK。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="3d5cc-245">hello 資料流分析工作內嵌 hello 事件中心中的這些事件和處理序 hello 即時 tooanalyze hello vehicle 健全狀況中的資料。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![事件中樞儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="3d5cc-247">圖 4 - 事件中樞儀表板</span><span class="sxs-lookup"><span data-stu-id="3d5cc-247">*Figure 4 - Event Hub dashboard*</span></span>

![處理資料的串流分析作業](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="3d5cc-249">圖 5 - 處理資料的串流分析作業</span><span class="sxs-lookup"><span data-stu-id="3d5cc-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="3d5cc-250">hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="3d5cc-251">內嵌 hello 事件中心的資料</span><span class="sxs-lookup"><span data-stu-id="3d5cc-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="3d5cc-252">執行與 hello 的參考資料 toomap hello vehicle VIN toohello 對應模型的聯結</span><span class="sxs-lookup"><span data-stu-id="3d5cc-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="3d5cc-253">將資料保存到 Azure Blob 儲存體以進行充分的批次分析。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="3d5cc-254">下列資料流分析查詢的 hello 是使用的 toopersist hello 資料到 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![用於擷取資料的串流分析作業查詢](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="3d5cc-256">圖 6 - 用於擷取資料的串流分析作業查詢</span><span class="sxs-lookup"><span data-stu-id="3d5cc-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="3d5cc-257">批次分析</span><span class="sxs-lookup"><span data-stu-id="3d5cc-257">Batch analysis</span></span>
<span data-ttu-id="3d5cc-258">我們也會產生另一批模擬車輛訊號和診斷資料集，以進行更多樣的批次分析。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="3d5cc-259">這是必要的 tooensure 批次處理的良好的代表性資料磁碟區。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="3d5cc-260">基於此目的，我們會使用管線 hello Azure Data Factory 的工作流程 toogenerate 中名為"PrepareSampleDataPipeline"模擬的 vehicle 訊號和診斷的資料集的一年的價值。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="3d5cc-261">按一下[Data Factory 的自訂活動](http://go.microsoft.com/fwlink/?LinkId=717077)toodownload hello Data Factory 自訂 DotNet 活動 Visual Studio 方案的自訂項目會根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![準備批次處理工作流程的範例資料](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="3d5cc-263">圖 7 - 準備批次處理工作流程的範例資料</span><span class="sxs-lookup"><span data-stu-id="3d5cc-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="3d5cc-264">hello 管線包含自訂的 ADF.Net 這裡顯示的活動：</span><span class="sxs-lookup"><span data-stu-id="3d5cc-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![PrepareSampleDataPipeline 活動](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="3d5cc-266">圖 8 - PrepareSampleDataPipeline</span><span class="sxs-lookup"><span data-stu-id="3d5cc-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="3d5cc-267">一旦 hello 管線執行成功，並且 「 RawCarEventsTable 」 資料集標示為 「 準備 」，一年值得的一種載具，模擬的訊號和診斷資料所產生。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="3d5cc-268">您看到 hello 下列資料夾和 hello"connectedcar 」 容器下的儲存體帳戶中建立的檔案：</span><span class="sxs-lookup"><span data-stu-id="3d5cc-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![PrepareSampleDataPipeline 輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="3d5cc-270">圖 9 - PrepareSampleDataPipeline 輸出</span><span class="sxs-lookup"><span data-stu-id="3d5cc-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="3d5cc-271">參考</span><span class="sxs-lookup"><span data-stu-id="3d5cc-271">References</span></span>
[<span data-ttu-id="3d5cc-272">適用於串流擷取的 Azure 事件中樞 SDK</span><span class="sxs-lookup"><span data-stu-id="3d5cc-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="3d5cc-273">[Azure Data Factory 資料移動功能](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet 活動](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="3d5cc-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="3d5cc-274">適用於準備範例資料的 Azure Data Factory DotNet 活動 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="3d5cc-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="3d5cc-275">資料分割 hello 資料集</span><span class="sxs-lookup"><span data-stu-id="3d5cc-275">Partition hello dataset</span></span>
<span data-ttu-id="3d5cc-276">hello 原始半結構化的車輛訊號和診斷的資料集被分割成年/月格式 hello 資料準備步驟中。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="3d5cc-277">接下來，做為 hello 第一個帳戶啟用容錯移轉從某個 blob 帳戶 toohello 可擴充長期的儲存體已滿和這樣的分割升級更有效率的查詢。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="3d5cc-278">Hello 方案中的這個步驟是適用的唯一 toobatch 處理。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="3d5cc-279">輸入和輸出資料的資料管理︰</span><span class="sxs-lookup"><span data-stu-id="3d5cc-279">Input and output data data management:</span></span>

* <span data-ttu-id="3d5cc-280">hello**輸出資料**(標示為*PartitionedCarEventsTable*) toobe 保留很長一段時間的形式 hello 基本 /"rawest"hello 客戶 」 資料湖"中的資料。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="3d5cc-281">hello**輸入資料**toothis 管線會通常會被捨去 hello 輸出資料具有完整不失真 toohello 輸入-只儲存 （分割） 更好供後續使用。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![分割汽車事件工作流程](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="3d5cc-283">圖 10 – 分割汽車事件工作流程</span><span class="sxs-lookup"><span data-stu-id="3d5cc-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="3d5cc-284">hello 未經處理資料分割"PartitionCarEventsPipeline 」 中使用 Hive HDInsight 活動。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="3d5cc-285">依年/月會分割為一年產生在步驟 1 中的 hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="3d5cc-286">hello 分割區是使用的 toogenerate vehicle 訊號和診斷資料，每個月 （總計 12 個資料分割） 的一年。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![PartitionCarEventsPipeline 活動](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="3d5cc-288">圖 11 - PartitionCarEventsPipeline</span><span class="sxs-lookup"><span data-stu-id="3d5cc-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="3d5cc-289">PartitionConnectedCarEvents Hive 指令碼</span><span class="sxs-lookup"><span data-stu-id="3d5cc-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="3d5cc-290">hello 下列 Hive 指令碼名為"partitioncarevents.hql 」，用於資料分割和位於 hello 下載 zip hello"\demo\src\connectedcar\scripts"資料夾中。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="3d5cc-291">一旦 hello 管線已成功執行之後，您會看到下列資料分割產生 hello"connectedcar 」 容器下的儲存體帳戶中的 hello。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![分割的輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="3d5cc-293">圖 12 - 分割的輸出</span><span class="sxs-lookup"><span data-stu-id="3d5cc-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="3d5cc-294">hello 資料現在已最佳化，更容易管理而且準備好進行進一步的處理 toogain 豐富的批次的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="3d5cc-295">資料分析</span><span class="sxs-lookup"><span data-stu-id="3d5cc-295">Data Analysis</span></span>
<span data-ttu-id="3d5cc-296">在本節中，您會看到 toocombine Azure Stream Analytics、 Azure 機器學習服務、 Azure Data Factory 和豐富的 Azure HDInsight 的進階分析一種載具，健全狀況和推動習慣。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="3d5cc-297">以下共有三個小節︰</span><span class="sxs-lookup"><span data-stu-id="3d5cc-297">There are three subsections here:</span></span>

1. <span data-ttu-id="3d5cc-298">**機器學習**： 本小節包含我們已使用需要的服務維護和車輛需要恢復 toosafety 問題因為此方案 toopredict 車輛的 hello 異常偵測實驗的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="3d5cc-299">**即時分析**： 本小節包含有關 hello 即時分析使用 hello Stream Analytics 查詢語言，並運用 hello 機器學習實驗中使用自訂的應用程式的即時資訊。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="3d5cc-300">**批次分析**： 本小節包含 hello 轉換和使用 Azure HDInsight 和 Azure Machine Learning 實際運作的 Azure Data Factory 的 hello 批次資料處理的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="3d5cc-301">機器學習服務</span><span class="sxs-lookup"><span data-stu-id="3d5cc-301">Machine Learning</span></span>
<span data-ttu-id="3d5cc-302">我們的目標是 toopredict hello 車輛，需要維護或重新叫用特定的健全狀況統計資料為基礎。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="3d5cc-303">我們進行下列假設 hello</span><span class="sxs-lookup"><span data-stu-id="3d5cc-303">We make hello following assumptions</span></span>

* <span data-ttu-id="3d5cc-304">如果其中一個 hello 下列三個條件都成立，hello 車輛需要**服務維護**:</span><span class="sxs-lookup"><span data-stu-id="3d5cc-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="3d5cc-305">胎壓偏低</span><span class="sxs-lookup"><span data-stu-id="3d5cc-305">Tire pressure is low</span></span>
  * <span data-ttu-id="3d5cc-306">機油量偏低</span><span class="sxs-lookup"><span data-stu-id="3d5cc-306">Engine oil level is low</span></span>
  * <span data-ttu-id="3d5cc-307">引擎溫度偏高</span><span class="sxs-lookup"><span data-stu-id="3d5cc-307">Engine temperature is high</span></span>
* <span data-ttu-id="3d5cc-308">如果其中一個 hello 下列條件都成立，可能會有 hello 車輛**安全性問題**，而且需要**回收**:</span><span class="sxs-lookup"><span data-stu-id="3d5cc-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="3d5cc-309">引擎溫度偏高，但外部溫度偏低</span><span class="sxs-lookup"><span data-stu-id="3d5cc-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="3d5cc-310">引擎溫度偏低，但外部溫度偏高</span><span class="sxs-lookup"><span data-stu-id="3d5cc-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="3d5cc-311">根據 hello 先前的需求，我們已經建立兩個不同的模型 toodetect 異常 vehicle 維護偵測，一個汽車重新叫用偵測。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="3d5cc-312">在這兩個這些模型 hello 內建的主體元件分析 (PCA) 演算法用於異常偵測。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="3d5cc-313">**維修偵測模型**</span><span class="sxs-lookup"><span data-stu-id="3d5cc-313">**Maintenance detection model**</span></span>

<span data-ttu-id="3d5cc-314">如果其中一個三個指標-tire 不足的壓力，引擎石油或引擎溫度-滿足其各自的條件，hello 維護偵測模型報告異常狀況。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="3d5cc-315">如此一來，我們只需要 tooconsider 這些建立 hello 模型中的三個變數。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="3d5cc-316">在 Azure Machine Learning 中我們實驗中，我們會先使用**資料集中選取的資料行**模組 tooextract 這些三個變數。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="3d5cc-317">接下來，我們會使用 hello PCA 為基礎的異常偵測模組 toobuild hello 異常偵測模型。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="3d5cc-318">主體元件分析 (PCA) 是可以套用的 toofeature 選取範圍、 分類以及異常偵測的機器學習中建立的技術。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="3d5cc-319">PCA 會將一組包含可能相關變數的案例，轉換成一組稱為主成分的值。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="3d5cc-320">hello 以 PCA 為基礎的模型化的索引鍵的概念是 tooproject 至較低維空間的資料，因此功能和異常情況更方便識別。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="3d5cc-321">針對每個新的輸入太 hello 偵測模型，hello 異常偵測器會先計算上 hello 特徵向量，其投影，然後計算 hello 正規化重建錯誤。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="3d5cc-322">這個正規化的錯誤是 hello 異常分數。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="3d5cc-323">hello hello 錯誤的機率越高，hello 更多異常 hello 執行個體是。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="3d5cc-324">Hello 維護偵測問題，請在 3d 空間中的點由 tire 不足的壓力，引擎石油和引擎溫度座標可視為每一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="3d5cc-325">toocapture 這些異常情況中，我們可以投射 hello hello 3d 空間中的原始資料使用 PCA 2 維度空間。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="3d5cc-326">因此，我們會在 PCA toobe 2 中設定 hello 參數元件 toouse 數目。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="3d5cc-327">在套用以 PCA 為基礎的異常偵測時，這個參數扮演重要的角色。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="3d5cc-328">使用 PCA 投射資料之後，我們可以更輕鬆識別這些異常。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="3d5cc-329">**回收異常偵測模型**hello 回收異常偵測模型，我們使用 hello 選取資料行中的資料集和 PCA 為基礎的異常偵測模組類似的方式。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="3d5cc-330">具體來說，我們先擷取三個變數-引擎溫度、 外部溫度、 和速度-使用 hello**資料集中選取的資料行**模組。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="3d5cc-331">我們也包含 hello 速度變數 hello 引擎溫度通常是因為相互關聯 toohello 速度。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="3d5cc-332">接下來我們使用 PCA 為基礎的異常偵測模組 tooproject hello 資料從 hello 3d 空間至 2 維度空間。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="3d5cc-333">hello 回收準則符合，而且引擎溫度外部溫度高負面相互關聯時 hello 一種載具，因此需要重新叫用。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="3d5cc-334">使用以 PCA 為基礎的異常偵測演算法，我們可以執行 PCA 之後擷取 hello 異常狀況。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="3d5cc-335">訓練兩種模式中，我們需要 toouse 一般資料，不需要維護或重新叫用為 hello 輸入的資料 tootrain hello PCA 為基礎的異常偵測模型。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="3d5cc-336">在 hello 計分實驗，我們會使用 hello 定型異常偵測模型 toodetect hello vehicle 需要維護或重新叫用。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="3d5cc-337">即時分析</span><span class="sxs-lookup"><span data-stu-id="3d5cc-337">Real-time analysis</span></span>
<span data-ttu-id="3d5cc-338">hello 遵循串流分析 SQL 查詢會使用所有 tooget 都 hello 平均都 hello 重要的一種載具參數如 vehicle 速度、 燃料層級、 引擎溫度、 里程計讀取、 tire 不足的壓力，引擎石油層級，與其他人。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="3d5cc-339">hello 平均值是使用的 toodetect 異常發出警示，並判斷 hello 的特定區域中運作的車輛通行狀況的整體健全狀況，然後關聯 toodemographics。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![用於即時處理的串流分析查詢](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="3d5cc-341">圖 13 – 用於即時處理的串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="3d5cc-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="3d5cc-342">所有的 hello 平均會計算透過 3 秒 TumblingWindow。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="3d5cc-343">因為我們需要非重疊和連續的時間間隔，所以在此案例中使用 TubmlingWindow。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="3d5cc-344">toolearn 進一步了解所有 hello 「 視窗 」 功能，在 Azure Stream Analytics 中，按一下[視窗化 (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="3d5cc-345">**即時預測**</span><span class="sxs-lookup"><span data-stu-id="3d5cc-345">**Real-time prediction**</span></span>

<span data-ttu-id="3d5cc-346">實際的時間，應用程式是 hello 方案 toooperationalize hello 機器學習模型的一部分。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="3d5cc-347">此應用程式呼叫 「 RealTimeDashboardApp"建立並設定為 hello 方案部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="3d5cc-348">hello 應用程式會執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="3d5cc-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="3d5cc-349">會接聽 tooan 事件中樞執行個體，其中資料流分析會發佈 hello 事件模式中持續。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="3d5cc-350">![發行 hello 資料的資料流分析查詢](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png)*圖 14-發行 hello 資料 tooan 資料流分析查詢的輸出事件中樞執行個體*</span><span class="sxs-lookup"><span data-stu-id="3d5cc-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="3d5cc-351">對於此應用程式收到的每個事件：</span><span class="sxs-lookup"><span data-stu-id="3d5cc-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="3d5cc-352">處理序 hello 資料使用機器學習要求回應計分 (RR) 端點。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="3d5cc-353">hello RR 端點就會自動發行 hello 部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="3d5cc-354">hello RR 輸出為已發行的 tooa Power BI 資料集使用 hello 推入應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="3d5cc-355">此模式也是您想 toointegrate 企業營運 (LoB) 應用程式與 hello 即時分析流量，例如警示、 通知和傳訊案例的適用 tooscenarios。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="3d5cc-356">按一下[RealtimeDashboardApp 下載](http://go.microsoft.com/fwlink/?LinkId=717078)toodownload hello RealtimeDashboardApp Visual Studio 方案的自訂項目。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="3d5cc-357">**tooexecute hello 即時儀表板應用程式**</span><span class="sxs-lookup"><span data-stu-id="3d5cc-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="3d5cc-358">在本機擷取並儲存 ![RealtimeDashboardApp 資料夾](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png)圖 16 – RealtimeDashboardApp 資料夾</span><span class="sxs-lookup"><span data-stu-id="3d5cc-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="3d5cc-359">執行 hello 應用程式 RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="3d5cc-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="3d5cc-360">提供有效的 Power BI 認證、登入，然後按一下 [接受]</span><span class="sxs-lookup"><span data-stu-id="3d5cc-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![即時儀表板應用程式登入 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![即時儀表板應用程式完成登入 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="3d5cc-363">*圖 17-RealtimeDashboardApp： 登入 tooPower BI*</span><span class="sxs-lookup"><span data-stu-id="3d5cc-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="3d5cc-364">如果您想 tooflush hello Power BI 資料集時，執行 hello RealtimeDashboardApp hello"flushdata 」 參數：</span><span class="sxs-lookup"><span data-stu-id="3d5cc-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="3d5cc-365">批次分析</span><span class="sxs-lookup"><span data-stu-id="3d5cc-365">Batch analysis</span></span>
<span data-ttu-id="3d5cc-366">hello 現在的目標是的 tooshow Contoso 馬達如何利用 hello Azure 計算功能 tooharness 巨量資料 toogain 豐富的洞察能力模式、 使用方式的行為，以及一種載具，健全狀況。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="3d5cc-367">這可達成下列目標：</span><span class="sxs-lookup"><span data-stu-id="3d5cc-367">This makes it possible to:</span></span>

* <span data-ttu-id="3d5cc-368">改善 hello 客戶經驗並使其成本較低習慣以及燃料有效率驅動行為提供深入資訊</span><span class="sxs-lookup"><span data-stu-id="3d5cc-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="3d5cc-369">主動了解客戶和推動詳述 toogovern 業務決策，並在類別產品 & 服務最適合提供 hello</span><span class="sxs-lookup"><span data-stu-id="3d5cc-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="3d5cc-370">在此解決方案中，我們的目標 hello 下列度量：</span><span class="sxs-lookup"><span data-stu-id="3d5cc-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="3d5cc-371">**主動驅使行為**： 識別 hello 趨勢的 hello 模型、 位置、 推動條件與 hello 年 toogain 的洞察能力積極驅動模式的時間。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="3d5cc-372">Contoso Motors 可使用這些了解來進行行銷活動、推出新的人性化功能，以及基於使用方式的保險。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="3d5cc-373">**促進了有效率的推動行為**： 識別 hello 趨勢的 hello 模型、 位置、 推動條件與 hello 年 toogain 的洞察能力燃料有效率驅動模式的時間。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="3d5cc-374">Contoso 馬達可以使用這些 insights 行銷活動時，驅動的新功能和主動式報告 toohello 驅動程式成本效益與環境易記驅動習慣。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="3d5cc-375">**前文提過模型**： 識別模型需要由運用 hello 異常偵測機器學習實驗的恢復</span><span class="sxs-lookup"><span data-stu-id="3d5cc-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="3d5cc-376">讓我們來看到 hello 詳細資料的每個這些度量，</span><span class="sxs-lookup"><span data-stu-id="3d5cc-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="3d5cc-377">**危險駕駛模式**</span><span class="sxs-lookup"><span data-stu-id="3d5cc-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="3d5cc-378">hello 分割 vehicle 訊號和診斷資料會處理在 hello 管線中名為"AggresiveDrivingPatternPipeline 」 使用 Hive toodetermine hello 模型、 位置、 一種載具，推動 and 表現其他參數積極驅動的模式。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="3d5cc-379">![危險駕駛模式工作流程](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*圖 18 – 危險駕駛模式工作流程*</span><span class="sxs-lookup"><span data-stu-id="3d5cc-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="3d5cc-380">危險駕駛模式 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="3d5cc-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="3d5cc-381">hello 名為"aggresivedriving.hql 」 可用來分析積極驅動條件模式的 Hive 指令碼位於 「 \demo\src\connectedcar\scripts"hello 下載 zip 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="3d5cc-382">它會使用 hello 組合車輛的傳輸齒輪位置、 剎車組踏板狀態和速度 toodetect 魯莽/積極驅使行為根據煞車最高速度的模式。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="3d5cc-383">一旦 hello 管線已成功執行之後，您會看到下列資料分割產生 hello"connectedcar 」 容器下的儲存體帳戶中的 hello。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![AggressiveDrivingPatternPipeline 輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="3d5cc-385">圖 19 – AggressiveDrivingPatternPipeline 輸出</span><span class="sxs-lookup"><span data-stu-id="3d5cc-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="3d5cc-386">**省油駕駛模式**</span><span class="sxs-lookup"><span data-stu-id="3d5cc-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="3d5cc-387">hello 分割 vehicle 訊號，然後在名為"FuelEfficientDrivingPatternPipeline"hello 管線中處理診斷資料。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="3d5cc-388">Hive 是使用的 toodetermine hello 模型、 位置、 vehicle、 推動條件和其他屬性，才會看到燃料有效率驅動模式。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![省油駕駛模式](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="3d5cc-390">圖 20 – 省油駕駛模式工作流程</span><span class="sxs-lookup"><span data-stu-id="3d5cc-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="3d5cc-391">省油駕駛模式 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="3d5cc-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="3d5cc-392">hello 名為"fuelefficientdriving.hql 」 可用來分析積極驅動條件模式的 Hive 指令碼位於 「 \demo\src\connectedcar\scripts"hello 下載 zip 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="3d5cc-393">它會使用 hello 組合車輛的傳輸齒輪位置、 剎車組踏板狀態、 速度以及 accelerator 踏板位置 toodetect 燃料有效率驅動行為根據加速，煞車，並加速模式。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="3d5cc-394">一旦 hello 管線已成功執行之後，您會看到下列資料分割產生 hello"connectedcar 」 容器下的儲存體帳戶中的 hello。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![FuelEfficientDrivingPatternPipeline 輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="3d5cc-396">圖 21 – FuelEfficientDrivingPatternPipeline 輸出</span><span class="sxs-lookup"><span data-stu-id="3d5cc-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="3d5cc-397">**召回預測**</span><span class="sxs-lookup"><span data-stu-id="3d5cc-397">**Recall Predictions**</span></span>

<span data-ttu-id="3d5cc-398">hello 機器學習實驗佈建並發佈為 web 服務為 hello 方案部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="3d5cc-399">此工作流程，註冊為資料連結的 factory 服務，並使用資料處理站批次計分活動實際運作可用 hello 批次計分結束點。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![機器學習服務端點](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="3d5cc-401">圖 22 – 在 Data Factory 中註冊為連結服務的機器學習服務端點</span><span class="sxs-lookup"><span data-stu-id="3d5cc-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="3d5cc-402">hello 註冊連結的服務用於使用 hello 異常偵測模型 hello DetectAnomalyPipeline tooscore hello 資料。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Data Factory 中的 Azure Machine Learning 批次評分活動](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="3d5cc-404">圖 23 – Data Factory 中的 Azure Machine Learning 批次評分活動</span><span class="sxs-lookup"><span data-stu-id="3d5cc-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="3d5cc-405">有幾個步驟，讓它可以 operationalized hello 批次計分 web 服務，在資料準備為此管線中執行。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![用於預測需要召回車輛的 DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="3d5cc-407">圖 24 – 用於預測需要召回車輛的 DetectAnomalyPipeline</span><span class="sxs-lookup"><span data-stu-id="3d5cc-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="3d5cc-408">異常偵測 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="3d5cc-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="3d5cc-409">一旦完成 hello 計分，HDInsight 活動是使用的 tooprocess 和彙總的 hello 資料分類為異常 0.60 或更高的機率分數與 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="3d5cc-410">一旦 hello 管線已成功執行之後，您會看到下列資料分割產生 hello"connectedcar 」 容器下的儲存體帳戶中的 hello。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![DetectAnomalyPipeline 輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="3d5cc-412">圖 25 – DetectAnomalyPipeline 輸出</span><span class="sxs-lookup"><span data-stu-id="3d5cc-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="3d5cc-413">發佈</span><span class="sxs-lookup"><span data-stu-id="3d5cc-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="3d5cc-414">即時分析</span><span class="sxs-lookup"><span data-stu-id="3d5cc-414">Real-time analysis</span></span>
<span data-ttu-id="3d5cc-415">其中一個 hello 資料流分析作業中的 hello 查詢發行 hello 事件 tooan 輸出事件中樞執行個體。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![串流分析工作發行 tooan 輸出事件中樞執行個體](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="3d5cc-417">*圖 26 – 資料流分析工作發行 tooan 輸出事件中樞執行個體*</span><span class="sxs-lookup"><span data-stu-id="3d5cc-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![資料流分析查詢 toopublish toohello 輸出事件中樞執行個體](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="3d5cc-419">*圖 27-Stream Analytics 查詢 toopublish toohello 輸出事件中樞執行個體*</span><span class="sxs-lookup"><span data-stu-id="3d5cc-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="3d5cc-420">這個資料流的事件是由包含在 hello 解決方案中 RealTimeDashboardApp hello 取用。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="3d5cc-421">此應用程式會利用進行即時計分 hello 機器學習要求-回應 web 服務，並將發佈 hello 產生的資料 tooa Power BI 資料集供取用。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="3d5cc-422">批次分析</span><span class="sxs-lookup"><span data-stu-id="3d5cc-422">Batch analysis</span></span>
<span data-ttu-id="3d5cc-423">hello 的 hello 批次和即時處理的結果會耗用的已發行的 toohello Azure SQL Database 資料表。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="3d5cc-424">hello Azure SQL Server、 資料庫和 hello 資料表會自動建立 hello 安裝指令碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![批次處理結果複製 toodata 超市流程](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="3d5cc-426">*圖 28-批次處理的結果複製 toodata 超市工作流程*</span><span class="sxs-lookup"><span data-stu-id="3d5cc-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![串流分析工作發行 toodata 超市](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="3d5cc-428">*圖 29 – 資料流分析工作發行 toodata 超市*</span><span class="sxs-lookup"><span data-stu-id="3d5cc-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![串流分析作業中的資料超市設定](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="3d5cc-430">圖 30 – 串流分析作業中的資料超市設定</span><span class="sxs-lookup"><span data-stu-id="3d5cc-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="3d5cc-431">取用</span><span class="sxs-lookup"><span data-stu-id="3d5cc-431">Consume</span></span>
<span data-ttu-id="3d5cc-432">Power BI 給此方案一個豐富的儀表板來提供即時資料和預測性分析視覺效果。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="3d5cc-433">如需有關設定 hello Power BI 報表和 hello 儀表板的詳細指示，請按一下這裡。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="3d5cc-434">hello 最終儀表板看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="3d5cc-434">hello final dashboard looks like this:</span></span>

![Power BI 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="3d5cc-436">圖 31 - Power BI 儀表板</span><span class="sxs-lookup"><span data-stu-id="3d5cc-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="3d5cc-437">摘要</span><span class="sxs-lookup"><span data-stu-id="3d5cc-437">Summary</span></span>
<span data-ttu-id="3d5cc-438">本文件包含詳細的向下鑽研的 hello Vehicle 遙測分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="3d5cc-439">這以預測和動作示範即時和批次分析的 Lambda 架構模式。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="3d5cc-440">此模式適用於 tooa 各種不同的使用案例需要最忙碌路徑 （即時） 和 （批次） 的冷路徑分析。</span><span class="sxs-lookup"><span data-stu-id="3d5cc-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

