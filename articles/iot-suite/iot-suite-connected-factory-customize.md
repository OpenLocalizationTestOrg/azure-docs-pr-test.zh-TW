---
title: "自訂 Azure IoT 套件連線工廠 | Microsoft Docs"
description: "說明如何自訂連線工廠預先設定之解決方案的行為。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 90a6172dbd887ecda5a9f5d9082a4e136092bc10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="37df8-103">自訂連線工廠解決方案顯示 OPC UA 伺服器資料的方式</span><span class="sxs-lookup"><span data-stu-id="37df8-103">Customize how the connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="37df8-104">簡介</span><span class="sxs-lookup"><span data-stu-id="37df8-104">Introduction</span></span>

<span data-ttu-id="37df8-105">連線工廠解決方案會彙總並顯示連接到解決方案之 OPC UA 伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="37df8-105">The connected factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="37df8-106">您可以瀏覽並傳送命令至解決方案的 OPC UA 伺服器。</span><span class="sxs-lookup"><span data-stu-id="37df8-106">You can browse and send commands to the OPC UA servers in your solution.</span></span> <span data-ttu-id="37df8-107">如需 OPC UA 的詳細資訊，請參閱[連線的處理站常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="37df8-107">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="37df8-108">解決方案中的彙總資料範例包括「整體設備效率 (OEE)」和「關鍵效能指標 (KPI)」，您可以在儀表板的工廠、生產線與工作站層級分別檢視這些資料。</span><span class="sxs-lookup"><span data-stu-id="37df8-108">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span></span> <span data-ttu-id="37df8-109">下列螢幕擷取畫面顯示 [Munich (慕尼黑)] 工廠的 [Production line 1 (生產線 1)] 的 [Assembly (組件)] 工作站的 OEE 和 KPI 值：</span><span class="sxs-lookup"><span data-stu-id="37df8-109">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span></span>

![解決方案中的 OEE 和 KPI 值範例][img-oee-kpi]

<span data-ttu-id="37df8-111">解決方案可讓您檢視 OPC UA 伺服器 (稱為「工作站」) 中特定資料項目的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="37df8-111">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span></span> <span data-ttu-id="37df8-112">下列螢幕擷取畫面顯示特定工作站製造的項目數的繪圖︰</span><span class="sxs-lookup"><span data-stu-id="37df8-112">The following screenshot shows plots of the number of manufactured items from a specific station:</span></span>

![製造項目數的繪圖][img-manufactured-items]

<span data-ttu-id="37df8-114">如果您按一下其中一個圖形，可使用 Time Series Insights (TSI) 進一步探索資料︰</span><span class="sxs-lookup"><span data-stu-id="37df8-114">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span></span>

![使用 Time Series Insights 探索資料][img-tsi]

<span data-ttu-id="37df8-116">本文章說明：</span><span class="sxs-lookup"><span data-stu-id="37df8-116">This article describes:</span></span>

- <span data-ttu-id="37df8-117">解決方案中各種檢視的資料是如何取得的。</span><span class="sxs-lookup"><span data-stu-id="37df8-117">How the data is made available to the various views in the solution.</span></span>
- <span data-ttu-id="37df8-118">如何自訂解決方案顯示資料的方式。</span><span class="sxs-lookup"><span data-stu-id="37df8-118">How you can customize the way the solution displays the data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="37df8-119">資料來源</span><span class="sxs-lookup"><span data-stu-id="37df8-119">Data sources</span></span>

<span data-ttu-id="37df8-120">連線工廠解決方案會顯示連接到解決方案之 OPC UA 伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="37df8-120">The connected factory solution displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="37df8-121">預設安裝包含數台執行工廠模擬的 OPC UA 伺服器。</span><span class="sxs-lookup"><span data-stu-id="37df8-121">The default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="37df8-122">您可以將[透過閘道連線][lnk-connect-cf]的自有 OPC UA 伺服器新增到解決方案。</span><span class="sxs-lookup"><span data-stu-id="37df8-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span></span>

<span data-ttu-id="37df8-123">您可以在儀表板中瀏覽連線的 OPC UA 伺服器可傳送至您的解決方案的資料項目︰</span><span class="sxs-lookup"><span data-stu-id="37df8-123">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span></span>

1. <span data-ttu-id="37df8-124">瀏覽至 [Select an OPC UA server (選取 OPC UA 伺服器)] 檢視︰</span><span class="sxs-lookup"><span data-stu-id="37df8-124">Navigate to the **Select an OPC UA server** view:</span></span>

    ![瀏覽至 [Select an OPC UA server (選取 OPC UA 伺服器)] 檢視][img-select-server]

1. <span data-ttu-id="37df8-126">選取伺服器，然後按一下 [Connect (連線)]。</span><span class="sxs-lookup"><span data-stu-id="37df8-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="37df8-127">出現安全性警告時，按一下 [Proceed (繼續)]。</span><span class="sxs-lookup"><span data-stu-id="37df8-127">Click **Proceed** when the security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="37df8-128">這個警告每台伺服器只會出現一次，是建立解決方案儀表板和伺服器之間的信任關係。</span><span class="sxs-lookup"><span data-stu-id="37df8-128">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span></span>

1. <span data-ttu-id="37df8-129">您現在可以瀏覽伺服器可傳送至解決方案的資料項目。</span><span class="sxs-lookup"><span data-stu-id="37df8-129">You can now browse the data items that the server can send to the solution.</span></span> <span data-ttu-id="37df8-130">正在傳送至解決方案的項目會有綠色的核取記號︰</span><span class="sxs-lookup"><span data-stu-id="37df8-130">Items that are being sent to the solution have a green check mark:</span></span>

    ![發行的項目][img-published]

1. <span data-ttu-id="37df8-132">如果您是解決方案的*管理員*，您可以選擇發行資料項目，以在連線工廠解決方案中提供。</span><span class="sxs-lookup"><span data-stu-id="37df8-132">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the connected factory solution.</span></span> <span data-ttu-id="37df8-133">身為管理員，您也可以變更 OPC UA 伺服器中的資料項目值及呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="37df8-133">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span></span>

## <a name="map-the-data"></a><span data-ttu-id="37df8-134">對應資料</span><span class="sxs-lookup"><span data-stu-id="37df8-134">Map the data</span></span>

<span data-ttu-id="37df8-135">連線工廠解決方案會將 OPC UA 伺服器中的已發行資料項目對應並彙總至解決方案中的各種檢視。</span><span class="sxs-lookup"><span data-stu-id="37df8-135">The connected factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span></span> <span data-ttu-id="37df8-136">當您佈建連線工廠解決方案時，解決方案會部署到您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="37df8-136">The connected factory solution deploys to your Azure account when you provision the solution.</span></span> <span data-ttu-id="37df8-137">Visual Studio 連線工廠方案中的 JSON 檔案會儲存此對應資訊。</span><span class="sxs-lookup"><span data-stu-id="37df8-137">A JSON file in the Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="37df8-138">您可以檢視及修改連線工廠 Visual Studio 解決方案中的這個 JSON 設定檔。</span><span class="sxs-lookup"><span data-stu-id="37df8-138">You can view and modify this JSON configuration file in the connected factory Visual Studio solution.</span></span> <span data-ttu-id="37df8-139">您進行變更之後，可以重新部署解決方案。</span><span class="sxs-lookup"><span data-stu-id="37df8-139">You can redeploy the solution after you make a change.</span></span>

<span data-ttu-id="37df8-140">您可以使用此組態檔來︰</span><span class="sxs-lookup"><span data-stu-id="37df8-140">You can use the configuration file to:</span></span>

- <span data-ttu-id="37df8-141">編輯現有的模擬工廠、生產線和工作站。</span><span class="sxs-lookup"><span data-stu-id="37df8-141">Edit the existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="37df8-142">從連接到解決方案的實際 OPC UA 伺服器對應資料。</span><span class="sxs-lookup"><span data-stu-id="37df8-142">Map data from real OPC UA servers that you connect to the solution.</span></span>

<span data-ttu-id="37df8-143">若要複製一份連線工廠 Visual Studio 方案，請使用下列 git 命令︰</span><span class="sxs-lookup"><span data-stu-id="37df8-143">To clone a copy of the connected factory Visual Studio solution, use the following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="37df8-144">**ContosoTopologyDescription.json** 檔案定義 OPC UA 伺服器資料項目與連線工廠解決方案儀表板檢視之間的對應。</span><span class="sxs-lookup"><span data-stu-id="37df8-144">The file **ContosoTopologyDescription.json** defines the mapping from the OPC UA server data items to the views in the connected factory solution dashboard.</span></span> <span data-ttu-id="37df8-145">您可以在 Visual Studio 方案的 **WebApp** 專案的 **Contoso\Topology** 資料夾中找到此組態檔。</span><span class="sxs-lookup"><span data-stu-id="37df8-145">You can find this configuration file in the **Contoso\Topology** folder in the **WebApp** project in the Visual Studio solution.</span></span>

<span data-ttu-id="37df8-146">JSON 檔案的內容是以工廠、生產線和工作站節點的階層來組織。</span><span class="sxs-lookup"><span data-stu-id="37df8-146">The content of the JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="37df8-147">此階層定義了連線工廠儀表板中的瀏覽階層。</span><span class="sxs-lookup"><span data-stu-id="37df8-147">This hierarchy defines the navigation hierarchy in the connected factory dashboard.</span></span> <span data-ttu-id="37df8-148">階層中每個節點的值決定儀表板中顯示的資訊。</span><span class="sxs-lookup"><span data-stu-id="37df8-148">Values at each node of the hierarchy determine the information displayed in the dashboard.</span></span> <span data-ttu-id="37df8-149">例如，慕尼黑工廠的 JSON 檔案包含下列值︰</span><span class="sxs-lookup"><span data-stu-id="37df8-149">For example, the JSON file contains the following values for the Munich factory:</span></span>

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

<span data-ttu-id="37df8-150">名稱、描述和位置會出現在儀表板的這個檢視中︰</span><span class="sxs-lookup"><span data-stu-id="37df8-150">The name, description, and location appear on this view in the dashboard:</span></span>

![儀表板中的幕尼黑資料][img-munich]

<span data-ttu-id="37df8-152">每個工廠、生產線和工作站都有一個映像屬性。</span><span class="sxs-lookup"><span data-stu-id="37df8-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="37df8-153">您可以在 **WebApp** 專案的 **Content\img** 資料夾中找到這些 JPEG 檔案。</span><span class="sxs-lookup"><span data-stu-id="37df8-153">You can find these JPEG files in the **Content\img** folder in the **WebApp** project.</span></span> <span data-ttu-id="37df8-154">這些影像檔會顯示在連線工廠儀表板中。</span><span class="sxs-lookup"><span data-stu-id="37df8-154">These image files display in the connected factory dashboard.</span></span>

<span data-ttu-id="37df8-155">每個工作站均包含數個詳細屬性，定義與 OPC UA 資料項目的對應。</span><span class="sxs-lookup"><span data-stu-id="37df8-155">Each station includes several detailed properties that define the mapping from the OPC UA data items.</span></span> <span data-ttu-id="37df8-156">這些屬性將於下列各節中說明：</span><span class="sxs-lookup"><span data-stu-id="37df8-156">These properties are described in the following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="37df8-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="37df8-157">OpcUri</span></span>

<span data-ttu-id="37df8-158">**OpcUri** 值是可唯一識別 OPC UA 伺服器的 OPC UA 應用程式 URI。</span><span class="sxs-lookup"><span data-stu-id="37df8-158">The **OpcUri** value is the OPC UA Application URI that uniquely identifies the OPC UA server.</span></span> <span data-ttu-id="37df8-159">例如，慕尼黑生產線 1 的組件工作站的 **OpcUri** 值看起來就像這樣︰**urn:scada2194:ua:munich:productionline0:assemblystation**。</span><span class="sxs-lookup"><span data-stu-id="37df8-159">For example, the **OpcUri** value for the assembly station on production line 1 in Munich looks like the following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="37df8-160">您可以在解決方案儀表板中檢視連接的 OPC UA 伺服器的 URI：</span><span class="sxs-lookup"><span data-stu-id="37df8-160">You can view the URIs of the connected OPC UA servers in the solution dashboard:</span></span>

![檢視 OPC UA 伺服器 URI][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="37df8-162">模擬</span><span class="sxs-lookup"><span data-stu-id="37df8-162">Simulation</span></span>

<span data-ttu-id="37df8-163">**Simulation** 節點是 OPC UA 模擬特有的，會在預設佈建的 OPC UA 伺服器中執行。</span><span class="sxs-lookup"><span data-stu-id="37df8-163">The information in the **Simulation** node is specific to the OPC UA simulation that runs in the OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="37df8-164">它不會使用在實際的 OPC UA 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="37df8-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="37df8-165">Kpi1 和 Kpi2</span><span class="sxs-lookup"><span data-stu-id="37df8-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="37df8-166">這些節點描述工作站中的資料如何影響儀表板中的這兩個 KPI 值。</span><span class="sxs-lookup"><span data-stu-id="37df8-166">These nodes describe how data from the station contributes to the two KPI values in the dashboard.</span></span> <span data-ttu-id="37df8-167">在預設部署中，這些 KPI 值是每小時的單位及每小時的 kWh。</span><span class="sxs-lookup"><span data-stu-id="37df8-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="37df8-168">解決方案會在工作站層級計算 KPI 值，並於生產線和工廠層級彙總這些 KPI 值。</span><span class="sxs-lookup"><span data-stu-id="37df8-168">The solution calculates KPI vales at the level of a station and aggregates them at the production line and factory levels.</span></span>

<span data-ttu-id="37df8-169">每個 KPI 都有最小值、最大值和目標值。</span><span class="sxs-lookup"><span data-stu-id="37df8-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="37df8-170">每個 KPI 值也可定義連線工廠解決方案要執行的警示動作。</span><span class="sxs-lookup"><span data-stu-id="37df8-170">Each KPI value can also define alert actions for the connected factory solution to perform.</span></span> <span data-ttu-id="37df8-171">下列程式碼片段顯示慕尼黑生產線 1 的組件工作站的 KPI 定義︰</span><span class="sxs-lookup"><span data-stu-id="37df8-171">The following snippet shows the KPI definitions for the assembly station on production line 1 in Munich:</span></span>

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

<span data-ttu-id="37df8-172">下列螢幕擷取畫面顯示儀表板中的 KPI 資料。</span><span class="sxs-lookup"><span data-stu-id="37df8-172">The following screenshot shows the KPI data in the dashboard.</span></span>

![儀表板中的 KPI 資訊][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="37df8-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="37df8-174">OpcNodes</span></span>

<span data-ttu-id="37df8-175">**OpcNodes** 節點識別 OPC UA 伺服器中發行的資料項目，並指定如何處理該資料。</span><span class="sxs-lookup"><span data-stu-id="37df8-175">The **OpcNodes** nodes identify the published data items from the OPC UA server and specify how to process that data.</span></span>

<span data-ttu-id="37df8-176">**NodeId** 值識別 OPC UA 伺服器中特定的 OPC UA NodeID。</span><span class="sxs-lookup"><span data-stu-id="37df8-176">The **NodeId** value identifies the specific OPC UA NodeID from the OPC UA server.</span></span> <span data-ttu-id="37df8-177">慕尼黑生產線 1 的組件工作站中的第一個節點的值為 **ns=2;i=385**。</span><span class="sxs-lookup"><span data-stu-id="37df8-177">The first node in the assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="37df8-178">**NodeId** 值指定要從 OPC UA 伺服器讀取的資料項目，**SymbolicName** 則為該資料提供使用於儀表板中的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="37df8-178">A **NodeId** value specifies the data item to read from the OPC UA server, and the **SymbolicName** provides a user-friendly name to use in the dashboard for that data.</span></span>

<span data-ttu-id="37df8-179">下表摘要說明每個節點相關聯的其他值︰</span><span class="sxs-lookup"><span data-stu-id="37df8-179">Other values associated with each node are summarized in the following table:</span></span>

| <span data-ttu-id="37df8-180">值</span><span class="sxs-lookup"><span data-stu-id="37df8-180">Value</span></span> | <span data-ttu-id="37df8-181">說明</span><span class="sxs-lookup"><span data-stu-id="37df8-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="37df8-182">相關性</span><span class="sxs-lookup"><span data-stu-id="37df8-182">Relevance</span></span>  | <span data-ttu-id="37df8-183">此資料影響的 KPI 和 OEE 值。</span><span class="sxs-lookup"><span data-stu-id="37df8-183">The KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="37df8-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="37df8-184">OpCode</span></span>     | <span data-ttu-id="37df8-185">資料彙總的方式。</span><span class="sxs-lookup"><span data-stu-id="37df8-185">How the data is aggregated.</span></span> |
| <span data-ttu-id="37df8-186">Units</span><span class="sxs-lookup"><span data-stu-id="37df8-186">Units</span></span>      | <span data-ttu-id="37df8-187">儀表板中使用的單位。</span><span class="sxs-lookup"><span data-stu-id="37df8-187">The units to use in the dashboard.</span></span>  |
| <span data-ttu-id="37df8-188">可見</span><span class="sxs-lookup"><span data-stu-id="37df8-188">Visible</span></span>    | <span data-ttu-id="37df8-189">是否在儀表板中顯示此值。</span><span class="sxs-lookup"><span data-stu-id="37df8-189">Whether to display this value in the dashboard.</span></span> <span data-ttu-id="37df8-190">部分值使用於計算中而不會顯示。</span><span class="sxs-lookup"><span data-stu-id="37df8-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="37df8-191">最大值</span><span class="sxs-lookup"><span data-stu-id="37df8-191">Maximum</span></span>    | <span data-ttu-id="37df8-192">觸發儀表板警示的最大值。</span><span class="sxs-lookup"><span data-stu-id="37df8-192">The maximum value that triggers an alert in the dashboard.</span></span> |
| <span data-ttu-id="37df8-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="37df8-193">MaximumAlertActions</span></span> | <span data-ttu-id="37df8-194">回應警示所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="37df8-194">An action to take in response to an alert.</span></span> <span data-ttu-id="37df8-195">例如，傳送命令到工作站。</span><span class="sxs-lookup"><span data-stu-id="37df8-195">For example, send a command to a station.</span></span> |
| <span data-ttu-id="37df8-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="37df8-196">ConstValue</span></span> | <span data-ttu-id="37df8-197">使用於計算的常數值。</span><span class="sxs-lookup"><span data-stu-id="37df8-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-the-changes"></a><span data-ttu-id="37df8-198">部署變更</span><span class="sxs-lookup"><span data-stu-id="37df8-198">Deploy the changes</span></span>

<span data-ttu-id="37df8-199">完成 **ContosoTopologyDescription.json** 檔案的變更後，您必須將連線工廠解決方案重新部署到您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="37df8-199">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the connected factory solution to your Azure account.</span></span>

<span data-ttu-id="37df8-200">**azure-iot-connected-factory** 存放庫包含一個 **build.ps1** PowerShell 指令碼，可用於重新建置並部署解決方案。</span><span class="sxs-lookup"><span data-stu-id="37df8-200">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37df8-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37df8-201">Next Steps</span></span>

<span data-ttu-id="37df8-202">閱讀下列文章，深入了解連線工廠預先設定的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="37df8-202">Learn more about the connected factory preconfigured solution by reading the following articles:</span></span>

* <span data-ttu-id="37df8-203">[連線處理站預先設定的解決方案逐步解說][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="37df8-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="37df8-204">[為連線處理站部署閘道][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="37df8-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="37df8-205">[azureiotsuite.com 網站的權限][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="37df8-205">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="37df8-206">連線的處理站常見問題</span><span class="sxs-lookup"><span data-stu-id="37df8-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="37df8-207">[常見問題集][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="37df8-207">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md