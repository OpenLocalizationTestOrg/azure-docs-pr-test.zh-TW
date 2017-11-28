---
title: "Azure IoT 套件 aaaCustomize 連接工廠 |Microsoft 文件"
description: "Hello toocustomize hello 行為連接處理站的方式描述預先設定的解決方案。"
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
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="6ecf1-103">自訂 hello 從 OPC UA 伺服器所連接的原廠方案顯示資料</span><span class="sxs-lookup"><span data-stu-id="6ecf1-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="6ecf1-104">簡介</span><span class="sxs-lookup"><span data-stu-id="6ecf1-104">Introduction</span></span>

<span data-ttu-id="6ecf1-105">hello 連接的工廠方案彙總，並顯示 hello OPC UA 伺服器已連線的 toohello 方案的資料。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="6ecf1-106">您可以瀏覽並傳送命令 toohello OPC UA 方案中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="6ecf1-107">如需有關 OPC UA 的詳細資訊，請參閱 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="6ecf1-108">Hello 方案中的彙總資料的範例包括 hello 整體設備效率 (OEE) 和關鍵效能指標 (Kpi)，您可以在 hello factory、 線條與站台層級的 hello 儀表板中檢視。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="6ecf1-109">hello 下列螢幕擷取畫面顯示 hello OEE 和 KPI 值 hello**組件**站，在**生產線 1**，在 hello**慕尼黑**factory:</span><span class="sxs-lookup"><span data-stu-id="6ecf1-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Hello 方案中的 OEE 和 KPI 值的範例][img-oee-kpi]

<span data-ttu-id="6ecf1-111">hello 方案可讓您 tooview 的詳細資訊，從特定資料的項目從 hello OPC UA 伺服器，稱為*電台*。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="6ecf1-112">hello 下列螢幕擷取畫面顯示繪圖 hello 的製造的項目，從特定站台的數字：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![製造項目數的繪圖][img-manufactured-items]

<span data-ttu-id="6ecf1-114">如果您按一下某個 hello 圖形，您可以瀏覽 hello 資料進一步使用時間序列 Insights (TSI):</span><span class="sxs-lookup"><span data-stu-id="6ecf1-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![使用 Time Series Insights 探索資料][img-tsi]

<span data-ttu-id="6ecf1-116">本文章說明：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-116">This article describes:</span></span>

- <span data-ttu-id="6ecf1-117">Hello 資料的方式進行可用 toohello 各種檢視 hello 方案中。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="6ecf1-118">您可以自訂 hello 方式 hello 方案的方式顯示 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="6ecf1-119">資料來源</span><span class="sxs-lookup"><span data-stu-id="6ecf1-119">Data sources</span></span>

<span data-ttu-id="6ecf1-120">hello 連接的工廠方案顯示 hello OPC UA 伺服器已連線的 toohello 方案的資料。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="6ecf1-121">hello 預設安裝包含數個執行的處理站模擬的 OPC UA 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="6ecf1-122">您可以新增您自己的 OPC UA 伺服器，[透過閘道連線][ lnk-connect-cf] tooyour 方案。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="6ecf1-123">您可以瀏覽的已連接的 OPC UA 伺服器可以傳送 tooyour 方案 hello 儀表板中的 hello 資料項目：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="6ecf1-124">瀏覽 toohello**選取 OPC UA 伺服器**檢視：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![瀏覽 toohello 選取 OPC UA 伺服器檢視][img-select-server]

1. <span data-ttu-id="6ecf1-126">選取伺服器，然後按一下 [Connect (連線)]。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="6ecf1-127">按一下**繼續**hello 安全性警告出現時。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6ecf1-128">這個警告只出現一次，每個伺服器，而且會建立 hello 方案儀表板與 hello 伺服器之間的信任關係。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="6ecf1-129">您現在即可以瀏覽 hello 資料項目 hello 伺服器可以傳送 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="6ecf1-130">傳送 toohello 方案的項目具有綠色的核取記號：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![發行的項目][img-published]

1. <span data-ttu-id="6ecf1-132">如果您是*管理員*hello 在解決方案中，您可以選擇 toopublish 資料的項目 toomake hello 提供連接出廠解決方案。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="6ecf1-133">身為管理員，您也可以變更 hello 值項目，並呼叫 hello OPC UA 伺服器中的方法。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="6ecf1-134">Hello 資料對應</span><span class="sxs-lookup"><span data-stu-id="6ecf1-134">Map hello data</span></span>

<span data-ttu-id="6ecf1-135">hello 連接工廠方案對應，而彙總 hello 已發佈資料項目 hello OPC UA 伺服器 toohello 從各種檢視 hello 方案中。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="6ecf1-136">hello 連接的工廠方案 tooyour Azure 帳戶時部署您佈建 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="6ecf1-137">Hello 處理站的連線的 Visual Studio 方案中的 JSON 檔案會儲存此對應資訊。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="6ecf1-138">您可以檢視和修改這個 hello 連線 factory Visual Studio 方案中的 JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="6ecf1-139">您進行變更之後，您可以重新部署 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="6ecf1-140">您可以使用 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="6ecf1-141">編輯 hello 現有模擬處理站、 生產線條，以及站台。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="6ecf1-142">從實際的 OPC UA 伺服器 toohello 方案連接的資料對應。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="6ecf1-143">tooclone 副本 hello 連線 factory Visual Studio 方案，使用 hello 下列 git 命令：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="6ecf1-144">hello 檔案**ContosoTopologyDescription.json**定義 hello hello OPC UA 伺服器資料從對應 hello 連接的工廠方案儀表板中的項目 toohello 檢視。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="6ecf1-145">您可以找到這個組態檔中 hello **Contoso\Topology**資料夾中 hello **WebApp** hello Visual Studio 方案中的專案。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="6ecf1-146">hello hello JSON 檔案的內容會組織成原廠生產線上及站台節點的階層。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="6ecf1-147">此階層定義 hello 連接的工廠儀表板中的 hello 導覽階層。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="6ecf1-148">Hello 階層之每個節點的值會決定顯示 hello 儀表板中的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="6ecf1-149">例如，hello JSON 檔案包含 hello hello 慕尼黑 factory 的值：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

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

<span data-ttu-id="6ecf1-150">hello 名稱、 描述和位置會出現在這個檢視表 hello 儀表板中：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![慕尼黑 hello 儀表板中的資料][img-munich]

<span data-ttu-id="6ecf1-152">每個工廠、生產線和工作站都有一個映像屬性。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="6ecf1-153">您可以在 hello 找到這些 JPEG 檔案**Content\img**資料夾中 hello **WebApp**專案。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="6ecf1-154">這些映像檔會顯示 hello 連接的工廠儀表板中。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="6ecf1-155">每個站台包含數個定義 hello 從 hello OPC UA 對應資料項目的詳細的屬性。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="6ecf1-156">Hello 下列各節將描述這些屬性：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="6ecf1-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="6ecf1-157">OpcUri</span></span>

<span data-ttu-id="6ecf1-158">hello **OpcUri**值為 hello OPC UA 應用程式 URI 可唯一識別 hello OPC UA 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="6ecf1-159">例如，hello **OpcUri** hello 慕尼黑生產行 1 上的組件站看起來像 hello 下列值： **urn: scada2194:ua:munich:productionline0:assemblystation**。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="6ecf1-160">您可以在 hello 方案儀表板中檢視 hello hello 連接 OPC UA 伺服器的 Uri:</span><span class="sxs-lookup"><span data-stu-id="6ecf1-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![檢視 OPC UA 伺服器 URI][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="6ecf1-162">模擬</span><span class="sxs-lookup"><span data-stu-id="6ecf1-162">Simulation</span></span>

<span data-ttu-id="6ecf1-163">hello 資訊在 hello**模擬**節點是特定 toohello OPC UA 模擬執行 hello 的預設佈建的 OPC UA 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="6ecf1-164">它不會使用在實際的 OPC UA 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="6ecf1-165">Kpi1 和 Kpi2</span><span class="sxs-lookup"><span data-stu-id="6ecf1-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="6ecf1-166">這些節點會描述如何從 hello 站的資料造成 toohello 兩個 KPI 值 hello 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="6ecf1-167">在預設部署中，這些 KPI 值是每小時的單位及每小時的 kWh。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="6ecf1-168">hello 方案計算 KPI 值層級 hello 的站台，並加以彙總在 hello 生產線和 factory 層級。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="6ecf1-169">每個 KPI 都有最小值、最大值和目標值。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="6ecf1-170">每個 KPI 值也可以定義警示 hello 連接工廠方案 tooperform 動作。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="6ecf1-171">hello 下列程式碼片段顯示 hello 組件站台的 hello KPI 定義生產線上慕尼黑中為 1:</span><span class="sxs-lookup"><span data-stu-id="6ecf1-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

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

<span data-ttu-id="6ecf1-172">hello 下列螢幕擷取畫面顯示 hello KPI 資料 hello 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![Hello 儀表板中的 KPI 資訊][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="6ecf1-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="6ecf1-174">OpcNodes</span></span>

<span data-ttu-id="6ecf1-175">hello **OpcNodes**節點識別 hello hello OPC UA 伺服器從已發佈的資料項目，並指定如何 tooprocess 該資料。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="6ecf1-176">hello **NodeId**值識別 hello hello OPC UA 伺服器從特定的 OPC UA NodeID。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="6ecf1-177">hello 生產線慕尼黑中為 1 的 hello 組件站中的第一個節點的值**ns = 2; 我 = 385**。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="6ecf1-178">A **NodeId**值會指定從 hello OPC UA 伺服器與 hello hello 資料項目 tooread **SymbolicName** hello 儀表板中的使用者易記名稱 toouse 提供該資料。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="6ecf1-179">Hello 下表中摘要說明每個節點相關聯的其他值：</span><span class="sxs-lookup"><span data-stu-id="6ecf1-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="6ecf1-180">值</span><span class="sxs-lookup"><span data-stu-id="6ecf1-180">Value</span></span> | <span data-ttu-id="6ecf1-181">說明</span><span class="sxs-lookup"><span data-stu-id="6ecf1-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="6ecf1-182">相關性</span><span class="sxs-lookup"><span data-stu-id="6ecf1-182">Relevance</span></span>  | <span data-ttu-id="6ecf1-183">此資料提供給 hello KPI 和 OEE 值。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="6ecf1-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="6ecf1-184">OpCode</span></span>     | <span data-ttu-id="6ecf1-185">Hello 資料彙總方式。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="6ecf1-186">Units</span><span class="sxs-lookup"><span data-stu-id="6ecf1-186">Units</span></span>      | <span data-ttu-id="6ecf1-187">hello 單位 toouse hello 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="6ecf1-188">可見</span><span class="sxs-lookup"><span data-stu-id="6ecf1-188">Visible</span></span>    | <span data-ttu-id="6ecf1-189">Toodisplay 這中是否有值 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="6ecf1-190">部分值使用於計算中而不會顯示。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="6ecf1-191">最大值</span><span class="sxs-lookup"><span data-stu-id="6ecf1-191">Maximum</span></span>    | <span data-ttu-id="6ecf1-192">hello 最大值，會觸發警示 hello 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="6ecf1-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="6ecf1-193">MaximumAlertActions</span></span> | <span data-ttu-id="6ecf1-194">在回應 tooan 警示動作 tootake。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="6ecf1-195">例如，傳送命令 tooa 站台。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="6ecf1-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="6ecf1-196">ConstValue</span></span> | <span data-ttu-id="6ecf1-197">使用於計算的常數值。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="6ecf1-198">部署 hello 變更</span><span class="sxs-lookup"><span data-stu-id="6ecf1-198">Deploy hello changes</span></span>

<span data-ttu-id="6ecf1-199">當您完成之後變更 toohello **ContosoTopologyDescription.json**檔案中，您就必須重新部署 hello 連接工廠方案 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="6ecf1-200">hello **azure-iot-連線-原廠**儲存機制包括**build.ps1** PowerShell 指令碼，您可以使用 toorebuild 並部署 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="6ecf1-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ecf1-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ecf1-201">Next Steps</span></span>

<span data-ttu-id="6ecf1-202">深入了解 hello 連接工廠預先設定方案的下列文章閱讀 hello:</span><span class="sxs-lookup"><span data-stu-id="6ecf1-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="6ecf1-203">[連線處理站預先設定的解決方案逐步解說][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="6ecf1-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="6ecf1-204">[為連線處理站部署閘道][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="6ecf1-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="6ecf1-205">[Hello azureiotsuite.com 網站的權限][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="6ecf1-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="6ecf1-206">連線的處理站常見問題</span><span class="sxs-lookup"><span data-stu-id="6ecf1-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="6ecf1-207">[常見問題集][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="6ecf1-207">[FAQ][lnk-faq]</span></span>


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