---
title: "Azure Cosmos DB 連接器的 Power BI 教學課程 | Microsoft Docs"
description: "使用本 Power BI 教學課程以匯入 JSON、建立具深入資訊的報告以及使用 Azure Cosmos DB 和 Power BI 連接器將資料視覺化。"
keywords: "power bi 教學課程，視覺化資料，power bi 連接器"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: 7f56f6d89a9990ab7e7f50a86993e9e22b73d646
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-the-power-bi-connector"></a><span data-ttu-id="2d541-104">Azure Cosmos DB 的 Power BI 教學課程：使用 Power BI 連接器將資料視覺化</span><span class="sxs-lookup"><span data-stu-id="2d541-104">Power BI tutorial for Azure Cosmos DB: Visualize data using the Power BI connector</span></span>
<span data-ttu-id="2d541-105">[PowerBI.com](https://powerbi.microsoft.com/) 是一項線上服務，您可以在其中建立及共用具有您和組織之重要資料的儀表板和報告。</span><span class="sxs-lookup"><span data-stu-id="2d541-105">[PowerBI.com](https://powerbi.microsoft.com/) is an online service where you can create and share dashboards and reports with data that's important to you and your organization.</span></span>  <span data-ttu-id="2d541-106">Power BI Desktop 是一項專用的報告撰寫工具，可讓您從各種資料來源擷取資料、合併和轉換資料、建立功能強大的報告和視覺效果，以及將報告發佈至 Power BI。</span><span class="sxs-lookup"><span data-stu-id="2d541-106">Power BI Desktop is a dedicated report authoring tool that enables you to retrieve data from various data sources, merge and transform the data, create powerful reports and visualizations, and publish the reports to Power BI.</span></span>  <span data-ttu-id="2d541-107">有了最新版的 Power BI Desktop，您現在可以透過 Power BI 的 Cosmos DB 連接器連接到 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d541-107">With the latest version of Power BI Desktop, you can now connect to your Cosmos DB account via the Cosmos DB connector for Power BI.</span></span>   

<span data-ttu-id="2d541-108">在本 Power BI 教學課程中，我們將逐步解說在 Power BI Desktop 中連接到 Cosmos DB 帳戶、瀏覽到我們要使用瀏覽器擷取資料的集合、使用 Power BI Desktop 查詢編輯器將 JSON 資料轉換成表格式格式，和建置報告並將其發佈至 PowerBI.com 等作業的步驟。</span><span class="sxs-lookup"><span data-stu-id="2d541-108">In this Power BI tutorial, we walk through the steps to connect to a Cosmos DB account in Power BI Desktop, navigate to a collection where we want to extract the data using the Navigator, transform JSON data into tabular format using Power BI Desktop Query Editor, and build and publish a report to PowerBI.com.</span></span>

<span data-ttu-id="2d541-109">完成本教學課程後，您將能夠回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="2d541-109">After completing this Power BI tutorial, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="2d541-110">如何使用 Power BI Desktop 以 Cosmos DB 中的資料建置報告？</span><span class="sxs-lookup"><span data-stu-id="2d541-110">How can I build reports with data from Cosmos DB using Power BI Desktop?</span></span>
* <span data-ttu-id="2d541-111">如何在 Power BI Desktop 中連接到 Cosmos DB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="2d541-111">How can I connect to a Cosmos DB account in Power BI Desktop?</span></span>
* <span data-ttu-id="2d541-112">如何在 Power BI Desktop 中從集合擷取資料？</span><span class="sxs-lookup"><span data-stu-id="2d541-112">How can I retrieve data from a collection in Power BI Desktop?</span></span>
* <span data-ttu-id="2d541-113">如何在 Power BI Desktop 中轉換巢狀 JSON 資料？</span><span class="sxs-lookup"><span data-stu-id="2d541-113">How can I transform nested JSON data in Power BI Desktop?</span></span>
* <span data-ttu-id="2d541-114">如何在 PowerBI.com 中發佈及共用我的報告？</span><span class="sxs-lookup"><span data-stu-id="2d541-114">How can I publish and share my reports in PowerBI.com?</span></span>

> [!NOTE]
> <span data-ttu-id="2d541-115">適用於 Azure Cosmos DB 的 Power BI 連接器會連線到 Power BI Desktop 以擷取和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="2d541-115">The Power BI connector for Azure Cosmos DB connects to Power BI Desktop for extraction and transformation of data.</span></span> <span data-ttu-id="2d541-116">在 Power BI Desktop 中建立的報告接著可以發行至 PowerBI.com。您無法在 PowerBI.com 中直接擷取和轉換 Azure Cosmos DB 資料。</span><span class="sxs-lookup"><span data-stu-id="2d541-116">Reports created in Power BI Desktop can then be published to PowerBI.com. Direct extraction and transformation of Azure Cosmos DB data cannot be performed in PowerBI.com.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2d541-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="2d541-117">Prerequisites</span></span>
<span data-ttu-id="2d541-118">在依照本 Power BI 教學課程中的指示進行之前，請先確定您可以存取下列資源：</span><span class="sxs-lookup"><span data-stu-id="2d541-118">Before following the instructions in this Power BI tutorial, ensure that you have access to the following resources:</span></span>

* <span data-ttu-id="2d541-119">[最新版的 Power BI Desktop](https://powerbi.microsoft.com/desktop)</span><span class="sxs-lookup"><span data-stu-id="2d541-119">[The latest version of Power BI Desktop](https://powerbi.microsoft.com/desktop).</span></span>
* <span data-ttu-id="2d541-120">我們的示範帳戶或您的 Azure Cosmos DB 帳戶中資料的存取權。</span><span class="sxs-lookup"><span data-stu-id="2d541-120">Access to our demo account or data in your Cosmos DB account.</span></span>
  * <span data-ttu-id="2d541-121">示範帳戶會填入此教學課程中所顯示的火山資料。</span><span class="sxs-lookup"><span data-stu-id="2d541-121">The demo account is populated with the volcano data shown in this tutorial.</span></span> <span data-ttu-id="2d541-122">此示範帳戶未受限於任何 SLA，而是僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="2d541-122">This demo account is not bound by any SLAs and is meant for demonstration purposes only.</span></span>  <span data-ttu-id="2d541-123">我們保留對此示範帳戶隨時進行修改的權利，包括 (但不限於) 終止帳戶、變更金鑰、限制存取權、變更和刪除資料，不事先通知或告知原因。</span><span class="sxs-lookup"><span data-stu-id="2d541-123">We reserve the right to make modifications to this demo account including but not limited to, terminating the account, changing the key, restricting access, changing, and delete the data, at any time without advance notice or reason.</span></span>
    * <span data-ttu-id="2d541-124">URL：https://analytics.documents.azure.com</span><span class="sxs-lookup"><span data-stu-id="2d541-124">URL: https://analytics.documents.azure.com</span></span>
    * <span data-ttu-id="2d541-125">唯讀金鑰：MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==</span><span class="sxs-lookup"><span data-stu-id="2d541-125">Read-only key: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==</span></span>
  * <span data-ttu-id="2d541-126">或者，若要建立您自己的帳戶，請參閱[使用 Azure 入口網站建立 Azure Cosmos DB 資料庫帳戶](https://azure.microsoft.com/documentation/articles/create-account/)。</span><span class="sxs-lookup"><span data-stu-id="2d541-126">Or, to create your own account, see [Create an Azure Cosmos DB database account using the Azure portal](https://azure.microsoft.com/documentation/articles/create-account/).</span></span> <span data-ttu-id="2d541-127">然後，若要取得類似於本教學課程所使用的範例火山資料 (但不包含 GeoJSON 區塊)，請參閱 [NOAA 網站](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5)，然後使用 [Azure Cosmos DB 資料移轉工具](import-data.md)匯入資料。</span><span class="sxs-lookup"><span data-stu-id="2d541-127">Then, to get sample volcano data that's similar to what's used in this tutorial (but does not contain the GeoJSON blocks), see the [NOAA site](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) and then import the data using the [Azure Cosmos DB data migration tool](import-data.md).</span></span>

<span data-ttu-id="2d541-128">若要在 PowerBI.com 上共用您的報告，您必須有 PowerBI.com 中的帳戶。若要深入了解 Power BI for Free 和 Power BI Pro，請造訪 [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing)。</span><span class="sxs-lookup"><span data-stu-id="2d541-128">To share your reports in PowerBI.com, you must have an account in PowerBI.com.  To learn more about Power BI for Free and Power BI Pro, visit [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).</span></span>

## <a name="lets-get-started"></a><span data-ttu-id="2d541-129">現在就開始吧</span><span class="sxs-lookup"><span data-stu-id="2d541-129">Let's get started</span></span>
<span data-ttu-id="2d541-130">在本教學課程中，我們假設您是研究世界各地火山的地質學家。</span><span class="sxs-lookup"><span data-stu-id="2d541-130">In this tutorial, let's imagine that you are a geologist studying volcanoes around the world.</span></span>  <span data-ttu-id="2d541-131">火山資料儲存在 Cosmos DB 帳戶中，JSON 文件看起來有如下列範例文件。</span><span class="sxs-lookup"><span data-stu-id="2d541-131">The volcano data is stored in a Cosmos DB account and the JSON documents look like the following sample document.</span></span>

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

<span data-ttu-id="2d541-132">您想要從 Cosmos DB 帳戶擷取火山資料，並在互動式 Power BI 報告中將資料視覺化，如下列報告所示。</span><span class="sxs-lookup"><span data-stu-id="2d541-132">You want to retrieve the volcano data from the Cosmos DB account and visualize data in an interactive Power BI report like the following report.</span></span>

![藉由使用 Power BI 連接器完成這個 Power BI 教學課程，您將可以使用 Power BI Desktop 火山報告將資料視覺化](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

<span data-ttu-id="2d541-134">準備好要試試看了嗎？</span><span class="sxs-lookup"><span data-stu-id="2d541-134">Ready to give it a try?</span></span> <span data-ttu-id="2d541-135">現在就開始吧。</span><span class="sxs-lookup"><span data-stu-id="2d541-135">Let's get started.</span></span>

1. <span data-ttu-id="2d541-136">在您的工作站上執行 Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="2d541-136">Run Power BI Desktop on your workstation.</span></span>
2. <span data-ttu-id="2d541-137">Power BI Desktop 啟動時，會顯示 [歡迎使用]  畫面。</span><span class="sxs-lookup"><span data-stu-id="2d541-137">Once Power BI Desktop is launched, a *Welcome* screen is displayed.</span></span>
   
    ![Power BI Desktop 歡迎使用畫面 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. <span data-ttu-id="2d541-139">您可以 [取得資料]、檢視 [最近的來源]，或直接從 [歡迎使用] 畫面 [開啟其他報告]。</span><span class="sxs-lookup"><span data-stu-id="2d541-139">You can **Get Data**, see **Recent Sources**, or **Open Other Reports** directly from the *Welcome* screen.</span></span>  <span data-ttu-id="2d541-140">按一下右上角的 X，以關閉畫面。</span><span class="sxs-lookup"><span data-stu-id="2d541-140">Click the X at the top right corner to close the screen.</span></span> <span data-ttu-id="2d541-141">Power BI Desktop 的 [報告]  檢視隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="2d541-141">The **Report** view of Power BI Desktop is displayed.</span></span>
   
    ![Power BI Desktop 報告檢視 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. <span data-ttu-id="2d541-143">選取 [首頁] 功能區，然後按一下 [取得資料]。</span><span class="sxs-lookup"><span data-stu-id="2d541-143">Select the **Home** ribbon, then click on **Get Data**.</span></span>  <span data-ttu-id="2d541-144">此時應會出現 [取得資料]  視窗。</span><span class="sxs-lookup"><span data-stu-id="2d541-144">The **Get Data** window should appear.</span></span>
5. <span data-ttu-id="2d541-145">按一下 [Azure]、選取 [Microsoft Azure DocumentDB (Beta)]，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="2d541-145">Click on **Azure**, select **Microsoft Azure DocumentDB (Beta)**, and then click **Connect**.</span></span> 

    ![Power BI Desktop 取得資料 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. <span data-ttu-id="2d541-147">在 [預覽版連接器] 頁面上，按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="2d541-147">On the **Preview Connector** page, click **Continue**.</span></span> <span data-ttu-id="2d541-148">此時會出現 [Microsoft Azure DocumentDB 連接] 視窗。</span><span class="sxs-lookup"><span data-stu-id="2d541-148">The **Microsoft Azure DocumentDB Connect** window appears.</span></span>
7. <span data-ttu-id="2d541-149">依照下列方式指定您要從中擷取資料的 Cosmos DB 帳戶端點 URL，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2d541-149">Specify the Cosmos DB account endpoint URL you would like to retrieve the data from as shown below, and then click **OK**.</span></span> <span data-ttu-id="2d541-150">若要使用您的帳戶，可以從 Azure 入口網站 [[金鑰](manage-account.md#keys)] 刀鋒視窗的 [URI] 方塊中擷取 URL。</span><span class="sxs-lookup"><span data-stu-id="2d541-150">To use your own account, you can retrieve the URL from the URI box in the **[Keys](manage-account.md#keys)** blade of the Azure portal.</span></span> <span data-ttu-id="2d541-151">若要使用示範帳戶，請輸入 `https://analytics.documents.azure.com` 作為 URL。</span><span class="sxs-lookup"><span data-stu-id="2d541-151">To use the demo account, enter `https://analytics.documents.azure.com` for the URL.</span></span> 
   
    <span data-ttu-id="2d541-152">資料庫名稱、集合名稱、SQL 陳述式皆保留空白，這些欄位是選用的。</span><span class="sxs-lookup"><span data-stu-id="2d541-152">Leave the database name, collection name, and SQL statement blank as these fields are optional.</span></span>  <span data-ttu-id="2d541-153">我們將使用「瀏覽器」來選取資料庫和集合，以識別資料來自何處。</span><span class="sxs-lookup"><span data-stu-id="2d541-153">Instead, we will use the Navigator to select the Database and Collection to identify where the data comes from.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 桌面連接視窗](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. <span data-ttu-id="2d541-155">如果是第一次連接到此端點，系統會提示您提供帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="2d541-155">If you are connecting to this endpoint for the first time, you are prompted for the account key.</span></span> <span data-ttu-id="2d541-156">如果是您自己的帳戶，請從 Azure 入口網站 [[唯讀金鑰](manage-account.md#keys)] 刀鋒視窗的 [主要金鑰] 方塊中擷取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2d541-156">For your own account, retrieve the key from the **Primary Key** box in the **[Read-only Keys](manage-account.md#keys)** blade of the Azure portal.</span></span> <span data-ttu-id="2d541-157">如果是示範帳戶，金鑰是 `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`。</span><span class="sxs-lookup"><span data-stu-id="2d541-157">For the demo account, the key is `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`.</span></span> <span data-ttu-id="2d541-158">輸入適當的金鑰，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="2d541-158">Enter the appropriate key and then click **Connect**.</span></span>
   
    <span data-ttu-id="2d541-159">建議您在建置報告時使用唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="2d541-159">We recommend that you use the read-only key when building reports.</span></span>  <span data-ttu-id="2d541-160">這樣可避免非必要地將主要金鑰暴露於潛在的安全性風險下。</span><span class="sxs-lookup"><span data-stu-id="2d541-160">This will prevent unnecessary exposure of the master key to potential security risks.</span></span> <span data-ttu-id="2d541-161">唯讀金鑰可從 Azure 入口網站的 [[金鑰](manage-account.md#keys)] 刀鋒視窗取得，或使用上面提供的示範帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="2d541-161">The read-only key is available from the [Keys](manage-account.md#keys) blade of the Azure portal or you can use the demo account information provided above.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 帳戶金鑰](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > <span data-ttu-id="2d541-163">如果您收到指出「找不到指定的資料庫」的錯誤，</span><span class="sxs-lookup"><span data-stu-id="2d541-163">If you get an error that says "The specified database was not found."</span></span> <span data-ttu-id="2d541-164">請參閱此 [Power BI 問題](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200) \(英文\) 中的因應措施步驟。</span><span class="sxs-lookup"><span data-stu-id="2d541-164">see the workaround steps in this [Power BI issue](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).</span></span>
    
9. <span data-ttu-id="2d541-165">順利連接帳戶後，會出現 [瀏覽器]  。</span><span class="sxs-lookup"><span data-stu-id="2d541-165">When the account is successfully connected, the **Navigator** will appear.</span></span>  <span data-ttu-id="2d541-166">[瀏覽器]  會顯示帳戶下的資料庫清單。</span><span class="sxs-lookup"><span data-stu-id="2d541-166">The **Navigator** will show a list of databases under the account.</span></span>
10. <span data-ttu-id="2d541-167">按一下並展開作為報告資料來源的資料庫，如果您使用示範帳戶，請選取 [volcanodb] 。</span><span class="sxs-lookup"><span data-stu-id="2d541-167">Click and expand on the database where the data for the report will come from, if you're using the demo account, select **volcanodb**.</span></span>   
11. <span data-ttu-id="2d541-168">現在，選取您要從中擷取資料的集合。</span><span class="sxs-lookup"><span data-stu-id="2d541-168">Now, select a collection that you will retrieve the data from.</span></span> <span data-ttu-id="2d541-169">如果您使用示範帳戶，請選取 **volcano1**。</span><span class="sxs-lookup"><span data-stu-id="2d541-169">If you're using the demo account, select **volcano1**.</span></span>
    
    <span data-ttu-id="2d541-170">[預覽] 窗格會顯示 [記錄]  項目的清單。</span><span class="sxs-lookup"><span data-stu-id="2d541-170">The Preview pane shows a list of **Record** items.</span></span>  <span data-ttu-id="2d541-171">一份文件會顯示為 Power BI 中的 [記錄]  類型。</span><span class="sxs-lookup"><span data-stu-id="2d541-171">A Document is represented as a **Record** type in Power BI.</span></span> <span data-ttu-id="2d541-172">同樣地，文件內的巢狀 JSON 區塊也是 [記錄] 。</span><span class="sxs-lookup"><span data-stu-id="2d541-172">Similarly, a nested JSON block inside a document is also a **Record**.</span></span>
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 瀏覽器視窗](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. <span data-ttu-id="2d541-174">按一下 [編輯] 以在新視窗中啟動 [查詢編輯器] 來轉換資料。</span><span class="sxs-lookup"><span data-stu-id="2d541-174">Click **Edit** to launch the Query Editor in a new window to transform the data.</span></span>

## <a name="flattening-and-transforming-json-documents"></a><span data-ttu-id="2d541-175">簡維化和轉換 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="2d541-175">Flattening and transforming JSON documents</span></span>
1. <span data-ttu-id="2d541-176">切換至 [Power BI 查詢編輯器] 視窗，中央窗格內會顯示 [文件] 資料行。</span><span class="sxs-lookup"><span data-stu-id="2d541-176">Switch to the Power BI Query Editor window, where the **Document** column in the center pane.</span></span>
   <span data-ttu-id="2d541-177">![Power BI Desktop 查詢編輯器](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)</span><span class="sxs-lookup"><span data-stu-id="2d541-177">![Power BI Desktop Query Editor](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)</span></span>
2. <span data-ttu-id="2d541-178">按一下位於 [文件]  資料行標頭右側的展開器。</span><span class="sxs-lookup"><span data-stu-id="2d541-178">Click on the expander at the right side of the **Document** column header.</span></span>  <span data-ttu-id="2d541-179">此時會出現含有欄位清單的內容功能表。</span><span class="sxs-lookup"><span data-stu-id="2d541-179">The context menu with a list of fields will appear.</span></span>  <span data-ttu-id="2d541-180">選取您的報告所需的欄位，例如火山名稱、國家、區域、位置、高度、類型、狀態和已知的上次爆發時間，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2d541-180">Select the fields you need for your report, for instance,  Volcano Name, Country, Region, Location, Elevation, Type, Status and Last Know Eruption, and then click **OK**.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 展開文件](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. <span data-ttu-id="2d541-182">中央窗格會顯示所選欄位的結果預覽。</span><span class="sxs-lookup"><span data-stu-id="2d541-182">The center pane will display a preview of the result with the fields selected.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 壓平合併結果](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. <span data-ttu-id="2d541-184">在我們的範例中，[位置] 屬性是文件中的 GeoJSON 區塊。</span><span class="sxs-lookup"><span data-stu-id="2d541-184">In our example, the Location property is a GeoJSON block in a document.</span></span>  <span data-ttu-id="2d541-185">如您所見，[位置] 顯示為 Power BI Desktop 中的 [記錄]  類型。</span><span class="sxs-lookup"><span data-stu-id="2d541-185">As you can see, Location is represented as a **Record** type in Power BI Desktop.</span></span>  
5. <span data-ttu-id="2d541-186">按一下位於 [位置] 資料行標頭右側的展開器。</span><span class="sxs-lookup"><span data-stu-id="2d541-186">Click on the expander at the right side of the Location column header.</span></span>  <span data-ttu-id="2d541-187">此時會出現含有類型和座標欄位的內容功能表。</span><span class="sxs-lookup"><span data-stu-id="2d541-187">The context menu with type and coordinates fields will appear.</span></span>  <span data-ttu-id="2d541-188">我們選取座標欄位，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2d541-188">Let's select the coordinates field and click **OK**.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 位置記錄](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. <span data-ttu-id="2d541-190">中央窗格現在會顯示 [清單]  類型的座標資料行。</span><span class="sxs-lookup"><span data-stu-id="2d541-190">The center pane now shows a coordinates column of **List** type.</span></span>  <span data-ttu-id="2d541-191">如本教學課程一開始所說明，本教學課程中的 GeoJSON 資料屬於 Point 類型，具有座標陣列中所記錄的緯度和經度值。</span><span class="sxs-lookup"><span data-stu-id="2d541-191">As shown at the beginning of the tutorial, the GeoJSON data in this tutorial is of Point type with Latitude and Longitude values recorded in the coordinates array.</span></span>
   
    <span data-ttu-id="2d541-192">coordinates[0] 項目代表經度，coordinates[1] 則代表緯度。</span><span class="sxs-lookup"><span data-stu-id="2d541-192">The coordinates[0] element represents Longitude while coordinates[1] represents Latitude.</span></span>
    <span data-ttu-id="2d541-193">![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 座標清單](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)</span><span class="sxs-lookup"><span data-stu-id="2d541-193">![Power BI tutorial for Azure Cosmos DB Power BI connector - Coordinates list](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)</span></span>
7. <span data-ttu-id="2d541-194">為了將座標陣列簡維化，我們將建立名為 LatLong 的 [自訂資料行]  。</span><span class="sxs-lookup"><span data-stu-id="2d541-194">To flatten the coordinates array, we will create a **Custom Column** called LatLong.</span></span>  <span data-ttu-id="2d541-195">選取 [新增資料行] 功能區，然後按一下 [新增自訂資料行]。</span><span class="sxs-lookup"><span data-stu-id="2d541-195">Select the **Add Column** ribbon and click on **Add Custom Column**.</span></span>  <span data-ttu-id="2d541-196">此時應會出現 [新增自訂資料行]  視窗。</span><span class="sxs-lookup"><span data-stu-id="2d541-196">The **Add Custom Column** window should appear.</span></span>
8. <span data-ttu-id="2d541-197">提供新資料行的名稱，例如 LatLong。</span><span class="sxs-lookup"><span data-stu-id="2d541-197">Provide a name for the new column, e.g. LatLong.</span></span>
9. <span data-ttu-id="2d541-198">接下來，指定新資料行的自訂公式。</span><span class="sxs-lookup"><span data-stu-id="2d541-198">Next, specify the custom formula for the new column.</span></span>  <span data-ttu-id="2d541-199">在我們的範例中，我們將依照下列方式使用以下公式，串連以逗號分隔的緯度和經度值： `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`。</span><span class="sxs-lookup"><span data-stu-id="2d541-199">For our example, we will concatenate the Latitude and Longitude values separated by a comma as shown below using the following formula: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`.</span></span> <span data-ttu-id="2d541-200">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2d541-200">Click **OK**.</span></span>
   
    <span data-ttu-id="2d541-201">如需資料分析運算式 (DAX) (包括 DAX 函數) 的詳細資訊，請瀏覽 [Power BI Desktop 中的 DAX 基礎](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop)。</span><span class="sxs-lookup"><span data-stu-id="2d541-201">For more information on Data Analysis Expressions (DAX) including DAX functions, please visit [DAX Basic in Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 新增自訂資料行](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. <span data-ttu-id="2d541-203">現在，中央窗格會顯示新的 LatLong 資料行，並且已填入以逗號分隔的緯度和經度值。</span><span class="sxs-lookup"><span data-stu-id="2d541-203">Now, the center pane will show the new LatLong column populated with the Latitude and Longitude values separated by a comma.</span></span>
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 自訂 LatLong 資料行](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    <span data-ttu-id="2d541-205">如果您在新的資料行中收到錯誤，請確定在 [查詢設定] 下套用的步驟與下圖相同︰</span><span class="sxs-lookup"><span data-stu-id="2d541-205">If you receive an Error in the new column, make sure that the applied steps under Query Settings match the following figure:</span></span>
    
    ![套用的步驟應該是來源、瀏覽、展開的文件、展開的 Document.Location、新增的自訂](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    <span data-ttu-id="2d541-207">如果步驟不同，請刪除額外的步驟，然後再試一次新增自訂資料行。</span><span class="sxs-lookup"><span data-stu-id="2d541-207">If your steps are different, delete the extra steps and try adding the custom column again.</span></span> 
11. <span data-ttu-id="2d541-208">現在我們已將資料簡維化成表格式格式。</span><span class="sxs-lookup"><span data-stu-id="2d541-208">We have now completed flattening the data into tabular format.</span></span>  <span data-ttu-id="2d541-209">您可以利用查詢編輯器中所有可用的功能，將 Cosmos DB 中的資料圖形化及進行轉換。</span><span class="sxs-lookup"><span data-stu-id="2d541-209">You can leverage all of the features available in the Query Editor to shape and transform data in Cosmos DB.</span></span>  <span data-ttu-id="2d541-210">如果您使用範例，請在 [首頁] 功能區上變更 [資料類型]，以將 [高度] 的資料類型變更為 [整數]。</span><span class="sxs-lookup"><span data-stu-id="2d541-210">If you're using the sample, change the data type for Elevation to **Whole number** by changing the **Data Type** on the **Home** ribbon.</span></span>
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 變更資料行類型](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. <span data-ttu-id="2d541-212">按一下 [關閉並套用]  以儲存資料模型。</span><span class="sxs-lookup"><span data-stu-id="2d541-212">Click **Close and Apply** to save the data model.</span></span>
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 關閉並套用](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-the-reports"></a><span data-ttu-id="2d541-214">建置報告</span><span class="sxs-lookup"><span data-stu-id="2d541-214">Build the reports</span></span>
<span data-ttu-id="2d541-215">[Power BI Desktop 報告] 檢視可做為您開始建立報告以視覺化資料的起始點。</span><span class="sxs-lookup"><span data-stu-id="2d541-215">Power BI Desktop Report view is where you can start creating reports to visualize data.</span></span>  <span data-ttu-id="2d541-216">您可以將欄位拖放到 [報告]  畫布上，以建立報告。</span><span class="sxs-lookup"><span data-stu-id="2d541-216">You can create reports by dragging and dropping fields into the **Report** canvas.</span></span>

![Power BI Desktop 報告檢視 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

<span data-ttu-id="2d541-218">在 [報告] 檢視中，您應該會看到：</span><span class="sxs-lookup"><span data-stu-id="2d541-218">In the Report view, you should find:</span></span>

1. <span data-ttu-id="2d541-219">[欄位]  窗格，您會在這裡看到資料模型清單，以及您可以用於報告的欄位。</span><span class="sxs-lookup"><span data-stu-id="2d541-219">The **Fields** pane, this is where you will see a list of data models with fields you can use for your reports.</span></span>
2. <span data-ttu-id="2d541-220">[視覺效果]  窗格。</span><span class="sxs-lookup"><span data-stu-id="2d541-220">The **Visualizations** pane.</span></span> <span data-ttu-id="2d541-221">一份報告可以包含一或多個視覺效果。</span><span class="sxs-lookup"><span data-stu-id="2d541-221">A report can contain a single or multiple visualizations.</span></span>  <span data-ttu-id="2d541-222">請從 [視覺效果]  窗格中選擇適合本身需求的視覺化類型。</span><span class="sxs-lookup"><span data-stu-id="2d541-222">Pick the visual types fitting your needs from the **Visualizations** pane.</span></span>
3. <span data-ttu-id="2d541-223">[報告]  畫布，您可以在此處建置報告的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="2d541-223">The **Report** canvas, this is where you will build the visuals for your report.</span></span>
4. <span data-ttu-id="2d541-224">[報告]  頁面。</span><span class="sxs-lookup"><span data-stu-id="2d541-224">The **Report** page.</span></span> <span data-ttu-id="2d541-225">您可以在 Power BI Desktop 中心增多個報告頁面。</span><span class="sxs-lookup"><span data-stu-id="2d541-225">You can add multiple report pages in Power BI Desktop.</span></span>

<span data-ttu-id="2d541-226">以下說明建立簡單的互動式地圖檢視報告的基本步驟。</span><span class="sxs-lookup"><span data-stu-id="2d541-226">The following shows the basic steps of creating a simple interactive Map view report.</span></span>

1. <span data-ttu-id="2d541-227">在此處的範例中，我們將建立會顯示每個火山所在位置的地圖檢視。</span><span class="sxs-lookup"><span data-stu-id="2d541-227">For our example, we will create a map view showing the location of each volcano.</span></span>  <span data-ttu-id="2d541-228">在 [視覺效果]  窗格中，按一下地圖視覺類型，如上方的螢幕擷取畫面所強調顯示。</span><span class="sxs-lookup"><span data-stu-id="2d541-228">In the **Visualizations** pane, click on the Map visual type as highlighted in the screenshot above.</span></span>  <span data-ttu-id="2d541-229">您應該會看到地圖視覺化類型繪製於 [報告]  畫布上。</span><span class="sxs-lookup"><span data-stu-id="2d541-229">You should see the Map visual type painted on the **Report** canvas.</span></span>  <span data-ttu-id="2d541-230">[視覺效果]  窗格也應該會顯示一組與地圖視覺化類型相關的屬性。</span><span class="sxs-lookup"><span data-stu-id="2d541-230">The **Visualization** pane should also display a set of properties related to the Map visual type.</span></span>
2. <span data-ttu-id="2d541-231">現在，將 LatLong 欄位從 [欄位] 窗格拖放到 [視覺效果] 窗格中的 [位置] 屬性上。</span><span class="sxs-lookup"><span data-stu-id="2d541-231">Now, drag and drop the LatLong field from the **Fields** pane to the **Location** property in **Visualizations** pane.</span></span>
3. <span data-ttu-id="2d541-232">接下來，將 [火山名稱] 欄位拖放到 [圖例]  屬性上。</span><span class="sxs-lookup"><span data-stu-id="2d541-232">Next, drag and drop the Volcano Name field to the **Legend** property.</span></span>  
4. <span data-ttu-id="2d541-233">然後，將 [高度] 欄位拖放到 [大小]  屬性上。</span><span class="sxs-lookup"><span data-stu-id="2d541-233">Then, drag and drop the Elevation field to the **Size** property.</span></span>  
5. <span data-ttu-id="2d541-234">您現在應該會看到地圖視覺化顯示一組表示每個火山所在位置的泡泡，且泡泡的大小會與火山的高度相關聯。</span><span class="sxs-lookup"><span data-stu-id="2d541-234">You should now see the Map visual showing a set of bubbles indicating the location of each volcano with the size of the bubble correlating to the elevation of the volcano.</span></span>
6. <span data-ttu-id="2d541-235">現在您已建立基本報告。</span><span class="sxs-lookup"><span data-stu-id="2d541-235">You now have created a basic report.</span></span>  <span data-ttu-id="2d541-236">您可以新增更多視覺效果，以進一步自訂報告。</span><span class="sxs-lookup"><span data-stu-id="2d541-236">You can further customize the report by adding more visualizations.</span></span>  <span data-ttu-id="2d541-237">在本例中，我們新增 [火山類型] 交叉分析篩選器，讓報告更具互動性。</span><span class="sxs-lookup"><span data-stu-id="2d541-237">In our case, we added a Volcano Type slicer to make the report interactive.</span></span>  
   
    ![完成 Azure Cosmos DB 的 Power BI 教學課程後之最終 Power BI Desktop 報告的螢幕擷取畫面](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a><span data-ttu-id="2d541-239">發佈和共用您的報告</span><span class="sxs-lookup"><span data-stu-id="2d541-239">Publish and share your report</span></span>
<span data-ttu-id="2d541-240">若要共用您的報告，您必須有 PowerBI.com 中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d541-240">To share your report, you must have an account in PowerBI.com.</span></span>

1. <span data-ttu-id="2d541-241">在 Power BI Desktop 中，按一下 [首頁]  功能區。</span><span class="sxs-lookup"><span data-stu-id="2d541-241">In the Power BI Desktop, click on the **Home** ribbon.</span></span>
2. <span data-ttu-id="2d541-242">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="2d541-242">Click **Publish**.</span></span>  <span data-ttu-id="2d541-243">系統會提示您輸入 PowerBI.com 帳戶的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2d541-243">You will be prompted to enter the user name and password for your PowerBI.com account.</span></span>
3. <span data-ttu-id="2d541-244">認證經過驗證後，報告即會發佈至您選取的目的地。</span><span class="sxs-lookup"><span data-stu-id="2d541-244">Once the credential has been authenticated, the report is published to your destination you selected.</span></span>
4. <span data-ttu-id="2d541-245">按一下 [開啟 Power BI 中的 'PowerBITutorial.pbix']  在 PowerBI.com 上查看與共用您的報表。</span><span class="sxs-lookup"><span data-stu-id="2d541-245">Click **Open 'PowerBITutorial.pbix' in Power BI** to see and share your report on PowerBI.com.</span></span>
   
    ![成功發佈到 Power BI！](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a><span data-ttu-id="2d541-248">在 PowerBI.com 中建立儀表板</span><span class="sxs-lookup"><span data-stu-id="2d541-248">Create a dashboard in PowerBI.com</span></span>
<span data-ttu-id="2d541-249">現在，您有一份報表可在 PowerBI.com 上共用。</span><span class="sxs-lookup"><span data-stu-id="2d541-249">Now that you have a report, lets share it on PowerBI.com</span></span>

<span data-ttu-id="2d541-250">當您從 Power BI Desktop發佈報告至 PowerBI.com 時，在您的 PowerBI.com 租用戶中會產生 [報表] 和 [資料集]。</span><span class="sxs-lookup"><span data-stu-id="2d541-250">When you publish your report from Power BI Desktop to PowerBI.com, it generates a **Report** and a **Dataset** in your PowerBI.com tenant.</span></span> <span data-ttu-id="2d541-251">例如，您將名為 **PowerBITutorial** 的報表發佈到 PowerBI.com，會在 PowerBI.com 的 [報表] 和 [資料集] 區段看到 PowerBITutorial。</span><span class="sxs-lookup"><span data-stu-id="2d541-251">For example, after you published a report called **PowerBITutorial** to PowerBI.com, you will see PowerBITutorial in both the **Reports** and **Datasets** sections on PowerBI.com.</span></span>

   ![PowerBI.com 中新報表和資料集的螢幕擷取畫面](./media/powerbi-visualize/powerbi-reports-datasets.png)

<span data-ttu-id="2d541-253">若要建立可共用的儀表板，按一下 PowerBI.com 報表上的 [釘選即時頁面]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="2d541-253">To create a sharable dashboard, click the **Pin Live Page** button on your PowerBI.com report.</span></span>

   ![PowerBI.com 中新報表和資料集的螢幕擷取畫面](./media/powerbi-visualize/power-bi-pin-live-tile.png)

<span data-ttu-id="2d541-255">依照 [從報表釘選圖格](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) 的指示建立新的儀表板。</span><span class="sxs-lookup"><span data-stu-id="2d541-255">Then follow the instructions in [Pin a tile from a report](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) to create a new dashboard.</span></span> 

<span data-ttu-id="2d541-256">您也可以對之前建立的儀表板進行臨機操作修改。</span><span class="sxs-lookup"><span data-stu-id="2d541-256">You can also do ad hoc modifications to report before creating a dashboard.</span></span> <span data-ttu-id="2d541-257">不過，建議您使用 Power BI Desktop 進行修改，再將報表重新發佈至 PowerBI.com。</span><span class="sxs-lookup"><span data-stu-id="2d541-257">However, it's recommended that you use Power BI Desktop to perform the modifications and republish the report to PowerBI.com.</span></span>

## <a name="refresh-data-in-powerbicom"></a><span data-ttu-id="2d541-258">重新整理 PowerBI.com 中的資料</span><span class="sxs-lookup"><span data-stu-id="2d541-258">Refresh data in PowerBI.com</span></span>
<span data-ttu-id="2d541-259">有兩種方式可以重新整理資料：臨機操作和排程。</span><span class="sxs-lookup"><span data-stu-id="2d541-259">There are two ways to refresh data, ad hoc and scheduled.</span></span>

<span data-ttu-id="2d541-260">若以臨機操作方式重新整理，只要按一下**資料集** (例如 PowerBITutorial) 旁的刪節符號 (...)。</span><span class="sxs-lookup"><span data-stu-id="2d541-260">For an ad hoc refresh, simply click on the eclipses (…) by the **Dataset**, e.g. PowerBITutorial.</span></span> <span data-ttu-id="2d541-261">您應該會看到包括 [立即重新整理] 在內的動作清單。</span><span class="sxs-lookup"><span data-stu-id="2d541-261">You should see a list of actions including **Refresh Now**.</span></span> <span data-ttu-id="2d541-262">按一下 [立即重新整理] 以重新整理資料。</span><span class="sxs-lookup"><span data-stu-id="2d541-262">Click **Refresh Now** to refresh the data.</span></span>

![PowerBI.com 中立即重新整理的螢幕擷取畫面](./media/powerbi-visualize/power-bi-refresh-now.png)

<span data-ttu-id="2d541-264">若以排程方式重新整理，執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="2d541-264">For a scheduled refresh, do the following.</span></span>

1. <span data-ttu-id="2d541-265">按一下動作清單中的 [排程重新整理]  。</span><span class="sxs-lookup"><span data-stu-id="2d541-265">Click **Schedule Refresh** in the action list.</span></span> 

    ![PowerBI.com 中排程重新整理的螢幕擷取畫面](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. <span data-ttu-id="2d541-267">在 [設定] 頁面上，展開 [資料來源認證]。</span><span class="sxs-lookup"><span data-stu-id="2d541-267">In the **Settings** page, expand **Data source credentials**.</span></span> 
3. <span data-ttu-id="2d541-268">按一下 [編輯認證] 。</span><span class="sxs-lookup"><span data-stu-id="2d541-268">Click on **Edit credentials**.</span></span> 
   
    <span data-ttu-id="2d541-269">[設定] 快顯視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="2d541-269">The Configure popup appears.</span></span> 
4. <span data-ttu-id="2d541-270">輸入金鑰以將該資料集連接到 Cosmos DB 帳戶，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="2d541-270">Enter the key to connect to the Cosmos DB account for that data set, then click **Sign in**.</span></span> 
5. <span data-ttu-id="2d541-271">展開 [排程重新整理]  ，並設定您想要重新整理資料集的排程。</span><span class="sxs-lookup"><span data-stu-id="2d541-271">Expand **Schedule Refresh** and set up the schedule you want to refresh the dataset.</span></span> 
6. <span data-ttu-id="2d541-272">按一下 [套用]  即完成排程重新整理的設定。</span><span class="sxs-lookup"><span data-stu-id="2d541-272">Click **Apply** and you are done setting up the scheduled refresh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d541-273">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d541-273">Next steps</span></span>
* <span data-ttu-id="2d541-274">若要深入了解 Power BI，請參閱 [開始使用 Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="2d541-274">To learn more about Power BI, see [Get started with Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).</span></span>
* <span data-ttu-id="2d541-275">若要深入了解 Cosmos DB，請參閱 [Azure Cosmos DB 文件登錄頁面 (英文)](https://azure.microsoft.com/documentation/services/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="2d541-275">To learn more about Cosmos DB, see the [Azure Cosmos DB documentation landing page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

