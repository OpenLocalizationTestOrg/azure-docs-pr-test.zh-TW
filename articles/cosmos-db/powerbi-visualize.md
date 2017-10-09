---
title: "Azure Cosmos DB 連接器 aaaPower BI 教學課程 |Microsoft 文件"
description: "使用此 Power BI 教學課程 tooimport JSON、 建立具洞察力的報表和視覺化資料使用 hello Azure Cosmos DB 和 Power BI 連接器。"
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
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a><span data-ttu-id="dc949-104">Power BI Azure Cosmos DB 教學課程： 使用 hello Power BI 連接器的資料視覺化</span><span class="sxs-lookup"><span data-stu-id="dc949-104">Power BI tutorial for Azure Cosmos DB: Visualize data using hello Power BI connector</span></span>
<span data-ttu-id="dc949-105">[PowerBI.com](https://powerbi.microsoft.com/)是您可以在其中建立並與重要 tooyou 和貴組織的資料共用儀表板和報表的線上服務。</span><span class="sxs-lookup"><span data-stu-id="dc949-105">[PowerBI.com](https://powerbi.microsoft.com/) is an online service where you can create and share dashboards and reports with data that's important tooyou and your organization.</span></span>  <span data-ttu-id="dc949-106">Power BI Desktop 是專用報表撰寫工具，可讓您從各種資料來源的 tooretrieve 資料、 合併和轉換 hello 資料、 建立功能強大的報表和視覺效果，然後發行 hello 報表 tooPower BI。</span><span class="sxs-lookup"><span data-stu-id="dc949-106">Power BI Desktop is a dedicated report authoring tool that enables you tooretrieve data from various data sources, merge and transform hello data, create powerful reports and visualizations, and publish hello reports tooPower BI.</span></span>  <span data-ttu-id="dc949-107">Hello 最新版本的 Power BI Desktop，您現在可以透過 hello Cosmos DB 連接器 tooyour Cosmos DB 帳戶連接 Power bi。</span><span class="sxs-lookup"><span data-stu-id="dc949-107">With hello latest version of Power BI Desktop, you can now connect tooyour Cosmos DB account via hello Cosmos DB connector for Power BI.</span></span>   

<span data-ttu-id="dc949-108">在此 Power BI 教學課程中，我們逐步解說 hello 步驟 tooconnect tooa Cosmos DB 帳戶在 Power BI Desktop 中，瀏覽我們想要使用 hello 導覽器中，將 JSON 資料轉換成表格式格式使用 Power BI Desktop 查詢 tooextract hello 資料 tooa 集合編輯器中，建立和發行報表 tooPowerBI.com 和。</span><span class="sxs-lookup"><span data-stu-id="dc949-108">In this Power BI tutorial, we walk through hello steps tooconnect tooa Cosmos DB account in Power BI Desktop, navigate tooa collection where we want tooextract hello data using hello Navigator, transform JSON data into tabular format using Power BI Desktop Query Editor, and build and publish a report tooPowerBI.com.</span></span>

<span data-ttu-id="dc949-109">完成本教學課程中 Power BI 之後，您會無法 tooanswer hello 下列問題：</span><span class="sxs-lookup"><span data-stu-id="dc949-109">After completing this Power BI tutorial, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="dc949-110">如何使用 Power BI Desktop 以 Cosmos DB 中的資料建置報告？</span><span class="sxs-lookup"><span data-stu-id="dc949-110">How can I build reports with data from Cosmos DB using Power BI Desktop?</span></span>
* <span data-ttu-id="dc949-111">如何在 Power BI Desktop tooa Cosmos DB 帳戶連接？</span><span class="sxs-lookup"><span data-stu-id="dc949-111">How can I connect tooa Cosmos DB account in Power BI Desktop?</span></span>
* <span data-ttu-id="dc949-112">如何在 Power BI Desktop 中從集合擷取資料？</span><span class="sxs-lookup"><span data-stu-id="dc949-112">How can I retrieve data from a collection in Power BI Desktop?</span></span>
* <span data-ttu-id="dc949-113">如何在 Power BI Desktop 中轉換巢狀 JSON 資料？</span><span class="sxs-lookup"><span data-stu-id="dc949-113">How can I transform nested JSON data in Power BI Desktop?</span></span>
* <span data-ttu-id="dc949-114">如何在 PowerBI.com 中發佈及共用我的報告？</span><span class="sxs-lookup"><span data-stu-id="dc949-114">How can I publish and share my reports in PowerBI.com?</span></span>

> [!NOTE]
> <span data-ttu-id="dc949-115">Azure Cosmos DB 的 hello Power BI 連接器連接 tooPower BI Desktop 擷取和轉換的資料。</span><span class="sxs-lookup"><span data-stu-id="dc949-115">hello Power BI connector for Azure Cosmos DB connects tooPower BI Desktop for extraction and transformation of data.</span></span> <span data-ttu-id="dc949-116">Power BI Desktop 中建立的報表然後可以是已發行的 tooPowerBI.com。您無法在 PowerBI.com 中直接擷取和轉換 Azure Cosmos DB 資料。</span><span class="sxs-lookup"><span data-stu-id="dc949-116">Reports created in Power BI Desktop can then be published tooPowerBI.com. Direct extraction and transformation of Azure Cosmos DB data cannot be performed in PowerBI.com.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dc949-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="dc949-117">Prerequisites</span></span>
<span data-ttu-id="dc949-118">之前遵循此教學課程中 Power BI 中的 hello 指示，請確定您有存取 toohello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="dc949-118">Before following hello instructions in this Power BI tutorial, ensure that you have access toohello following resources:</span></span>

* <span data-ttu-id="dc949-119">[hello 最新版本的 Power BI Desktop](https://powerbi.microsoft.com/desktop)。</span><span class="sxs-lookup"><span data-stu-id="dc949-119">[hello latest version of Power BI Desktop](https://powerbi.microsoft.com/desktop).</span></span>
* <span data-ttu-id="dc949-120">存取 tooour 示範帳戶或 Cosmos DB 帳戶中的資料。</span><span class="sxs-lookup"><span data-stu-id="dc949-120">Access tooour demo account or data in your Cosmos DB account.</span></span>
  * <span data-ttu-id="dc949-121">本教學課程中所顯示的 hello 火山資料擴展 hello 示範帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc949-121">hello demo account is populated with hello volcano data shown in this tutorial.</span></span> <span data-ttu-id="dc949-122">此示範帳戶未受限於任何 SLA，而是僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="dc949-122">This demo account is not bound by any SLAs and is meant for demonstration purposes only.</span></span>  <span data-ttu-id="dc949-123">保留： hello 右 toomake 修改 toothis 示範帳戶包括但不是限於、 終止 hello 變更 hello 索引鍵，限制存取，變更帳戶，並刪除 hello 資料，在任何時間，而不需要事先通知或原因。</span><span class="sxs-lookup"><span data-stu-id="dc949-123">We reserve hello right toomake modifications toothis demo account including but not limited to, terminating hello account, changing hello key, restricting access, changing, and delete hello data, at any time without advance notice or reason.</span></span>
    * <span data-ttu-id="dc949-124">URL：https://analytics.documents.azure.com</span><span class="sxs-lookup"><span data-stu-id="dc949-124">URL: https://analytics.documents.azure.com</span></span>
    * <span data-ttu-id="dc949-125">唯讀金鑰：MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==</span><span class="sxs-lookup"><span data-stu-id="dc949-125">Read-only key: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==</span></span>
  * <span data-ttu-id="dc949-126">或者，toocreate 您自己的帳戶，請參閱[建立使用 hello Azure 入口網站的 Azure Cosmos DB 資料庫帳戶](https://azure.microsoft.com/documentation/articles/create-account/)。</span><span class="sxs-lookup"><span data-stu-id="dc949-126">Or, toocreate your own account, see [Create an Azure Cosmos DB database account using hello Azure portal](https://azure.microsoft.com/documentation/articles/create-account/).</span></span> <span data-ttu-id="dc949-127">然後，會類似 toowhat tooget 範例火山資料在本教學課程中使用 （但不包含 hello GeoJSON 區塊），請參閱 hello [NOAA 網站](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5)然後匯入使用 hello hello 資料[Azure Cosmos DB 的資料移轉工具](import-data.md)。</span><span class="sxs-lookup"><span data-stu-id="dc949-127">Then, tooget sample volcano data that's similar toowhat's used in this tutorial (but does not contain hello GeoJSON blocks), see hello [NOAA site](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) and then import hello data using hello [Azure Cosmos DB data migration tool](import-data.md).</span></span>

<span data-ttu-id="dc949-128">tooshare 您的報表在 PowerBI.com 中您必須在 PowerBI.com 中擁有帳戶。 深入了解 Power BI 免費和 Power BI Pro，toolearn 造訪[https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing)。</span><span class="sxs-lookup"><span data-stu-id="dc949-128">tooshare your reports in PowerBI.com, you must have an account in PowerBI.com.  toolearn more about Power BI for Free and Power BI Pro, visit [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).</span></span>

## <a name="lets-get-started"></a><span data-ttu-id="dc949-129">現在就開始吧</span><span class="sxs-lookup"><span data-stu-id="dc949-129">Let's get started</span></span>
<span data-ttu-id="dc949-130">在本教學課程中，我們假設您是 geologist，研究火山 hello 世界各地。</span><span class="sxs-lookup"><span data-stu-id="dc949-130">In this tutorial, let's imagine that you are a geologist studying volcanoes around hello world.</span></span>  <span data-ttu-id="dc949-131">hello 火山資料會儲存在 Cosmos DB 帳戶且 hello JSON 文件看起來 hello 遵循範例文件。</span><span class="sxs-lookup"><span data-stu-id="dc949-131">hello volcano data is stored in a Cosmos DB account and hello JSON documents look like hello following sample document.</span></span>

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

<span data-ttu-id="dc949-132">希望從 Cosmos DB hello tooretrieve hello 火山資料帳戶，並將類似下列報表 hello 互動式 Power BI 報表中的資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="dc949-132">You want tooretrieve hello volcano data from hello Cosmos DB account and visualize data in an interactive Power BI report like hello following report.</span></span>

![完成本 hello Power BI 連接器使用的 Power BI 教學課程，您將會以 hello Power BI Desktop 火山報表無法 toovisualize 資料](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

<span data-ttu-id="dc949-134">準備好 toogive 為再試一次嗎？</span><span class="sxs-lookup"><span data-stu-id="dc949-134">Ready toogive it a try?</span></span> <span data-ttu-id="dc949-135">現在就開始吧。</span><span class="sxs-lookup"><span data-stu-id="dc949-135">Let's get started.</span></span>

1. <span data-ttu-id="dc949-136">在您的工作站上執行 Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="dc949-136">Run Power BI Desktop on your workstation.</span></span>
2. <span data-ttu-id="dc949-137">Power BI Desktop 啟動時，會顯示 [歡迎使用]  畫面。</span><span class="sxs-lookup"><span data-stu-id="dc949-137">Once Power BI Desktop is launched, a *Welcome* screen is displayed.</span></span>
   
    ![Power BI Desktop 歡迎使用畫面 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. <span data-ttu-id="dc949-139">您可以**取得資料**，請參閱**最近使用的來源**，或**開啟其他報表**直接從 hello * 褖畫惎*螢幕。</span><span class="sxs-lookup"><span data-stu-id="dc949-139">You can **Get Data**, see **Recent Sources**, or **Open Other Reports** directly from hello *Welcome* screen.</span></span>  <span data-ttu-id="dc949-140">按一下 hello X 在 hello 右上角 tooclose 囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="dc949-140">Click hello X at hello top right corner tooclose hello screen.</span></span> <span data-ttu-id="dc949-141">hello**報表**Power BI Desktop 的檢視會顯示。</span><span class="sxs-lookup"><span data-stu-id="dc949-141">hello **Report** view of Power BI Desktop is displayed.</span></span>
   
    ![Power BI Desktop 報告檢視 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. <span data-ttu-id="dc949-143">選取 hello**首頁**功能區，然後按一下 **取得資料**。</span><span class="sxs-lookup"><span data-stu-id="dc949-143">Select hello **Home** ribbon, then click on **Get Data**.</span></span>  <span data-ttu-id="dc949-144">hello**取得資料**視窗應該會出現。</span><span class="sxs-lookup"><span data-stu-id="dc949-144">hello **Get Data** window should appear.</span></span>
5. <span data-ttu-id="dc949-145">按一下 Azure、選取 Microsoft Azure DocumentDB (Beta)，然後按一下連接。</span><span class="sxs-lookup"><span data-stu-id="dc949-145">Click on **Azure**, select **Microsoft Azure DocumentDB (Beta)**, and then click **Connect**.</span></span> 

    ![Power BI Desktop 取得資料 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. <span data-ttu-id="dc949-147">在 hello**預覽連接器**頁面上，按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="dc949-147">On hello **Preview Connector** page, click **Continue**.</span></span> <span data-ttu-id="dc949-148">hello **Microsoft Azure DocumentDB Connect**  視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="dc949-148">hello **Microsoft Azure DocumentDB Connect** window appears.</span></span>
7. <span data-ttu-id="dc949-149">指定 hello Cosmos DB 帳戶端點的 URL，從 tooretrieve hello 資料如下所示，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="dc949-149">Specify hello Cosmos DB account endpoint URL you would like tooretrieve hello data from as shown below, and then click **OK**.</span></span> <span data-ttu-id="dc949-150">toouse 您自己的帳戶，您可以擷取來自 hello URI URL 方塊中 hello hello **[金鑰](manage-account.md#keys)** hello Azure 入口網站的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dc949-150">toouse your own account, you can retrieve hello URL from hello URI box in hello **[Keys](manage-account.md#keys)** blade of hello Azure portal.</span></span> <span data-ttu-id="dc949-151">toouse hello 示範帳戶中，輸入`https://analytics.documents.azure.com`hello url。</span><span class="sxs-lookup"><span data-stu-id="dc949-151">toouse hello demo account, enter `https://analytics.documents.azure.com` for hello URL.</span></span> 
   
    <span data-ttu-id="dc949-152">項目留 hello 資料庫名稱、 集合名稱和 SQL 陳述式時這些欄位為選擇性。</span><span class="sxs-lookup"><span data-stu-id="dc949-152">Leave hello database name, collection name, and SQL statement blank as these fields are optional.</span></span>  <span data-ttu-id="dc949-153">相反地，我們將使用 hello 導覽 tooselect hello 資料庫與集合 tooidentify hello 資料來自何處。</span><span class="sxs-lookup"><span data-stu-id="dc949-153">Instead, we will use hello Navigator tooselect hello Database and Collection tooidentify where hello data comes from.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 桌面連接視窗](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. <span data-ttu-id="dc949-155">如果您第一次連接 hello toothis 端點，系統會提示您 hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="dc949-155">If you are connecting toothis endpoint for hello first time, you are prompted for hello account key.</span></span> <span data-ttu-id="dc949-156">為您自己的帳戶擷取 hello 金鑰 hello**主索引鍵**方塊中 hello **[唯讀金鑰](manage-account.md#keys)** hello Azure 入口網站的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="dc949-156">For your own account, retrieve hello key from hello **Primary Key** box in hello **[Read-only Keys](manage-account.md#keys)** blade of hello Azure portal.</span></span> <span data-ttu-id="dc949-157">Hello 示範帳戶，hello 金鑰是`MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`。</span><span class="sxs-lookup"><span data-stu-id="dc949-157">For hello demo account, hello key is `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`.</span></span> <span data-ttu-id="dc949-158">輸入 hello 適當的索引鍵，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="dc949-158">Enter hello appropriate key and then click **Connect**.</span></span>
   
    <span data-ttu-id="dc949-159">我們建議您在建立報表時使用 hello 唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="dc949-159">We recommend that you use hello read-only key when building reports.</span></span>  <span data-ttu-id="dc949-160">如此可防止不必要的曝光的 hello 主要金鑰 toopotential 安全性風險。</span><span class="sxs-lookup"><span data-stu-id="dc949-160">This will prevent unnecessary exposure of hello master key toopotential security risks.</span></span> <span data-ttu-id="dc949-161">hello 唯讀索引鍵是可從 hello[金鑰](manage-account.md#keys)刀鋒視窗中的 hello Azure 入口網站，或者您可以使用以上所提供的 hello 示範帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="dc949-161">hello read-only key is available from hello [Keys](manage-account.md#keys) blade of hello Azure portal or you can use hello demo account information provided above.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 帳戶金鑰](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > <span data-ttu-id="dc949-163">如果您收到錯誤指出 「 hello 指定的資料庫已找不到。 」</span><span class="sxs-lookup"><span data-stu-id="dc949-163">If you get an error that says "hello specified database was not found."</span></span> <span data-ttu-id="dc949-164">在這個步驟 hello 因應措施請參閱[Power BI 問題](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200)。</span><span class="sxs-lookup"><span data-stu-id="dc949-164">see hello workaround steps in this [Power BI issue](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).</span></span>
    
9. <span data-ttu-id="dc949-165">當 hello 帳戶順利連線時，hello**導覽**會出現。</span><span class="sxs-lookup"><span data-stu-id="dc949-165">When hello account is successfully connected, hello **Navigator** will appear.</span></span>  <span data-ttu-id="dc949-166">hello**導覽**會顯示 hello 帳戶下的資料庫清單。</span><span class="sxs-lookup"><span data-stu-id="dc949-166">hello **Navigator** will show a list of databases under hello account.</span></span>
10. <span data-ttu-id="dc949-167">按一下以展開其中 hello 資料 hello 報表，將來自，如果您使用 hello 示範帳戶，請選取 hello 資料庫上**volcanodb**。</span><span class="sxs-lookup"><span data-stu-id="dc949-167">Click and expand on hello database where hello data for hello report will come from, if you're using hello demo account, select **volcanodb**.</span></span>   
11. <span data-ttu-id="dc949-168">現在，選取您將 hello 從中擷取資料的集合。</span><span class="sxs-lookup"><span data-stu-id="dc949-168">Now, select a collection that you will retrieve hello data from.</span></span> <span data-ttu-id="dc949-169">如果您使用 hello 示範帳戶，請選取**volcano1**。</span><span class="sxs-lookup"><span data-stu-id="dc949-169">If you're using hello demo account, select **volcano1**.</span></span>
    
    <span data-ttu-id="dc949-170">hello 預覽 窗格會顯示一份**記錄**項目。</span><span class="sxs-lookup"><span data-stu-id="dc949-170">hello Preview pane shows a list of **Record** items.</span></span>  <span data-ttu-id="dc949-171">一份文件會顯示為 Power BI 中的 [記錄]  類型。</span><span class="sxs-lookup"><span data-stu-id="dc949-171">A Document is represented as a **Record** type in Power BI.</span></span> <span data-ttu-id="dc949-172">同樣地，文件內的巢狀 JSON 區塊也是 [記錄] 。</span><span class="sxs-lookup"><span data-stu-id="dc949-172">Similarly, a nested JSON block inside a document is also a **Record**.</span></span>
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 瀏覽器視窗](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. <span data-ttu-id="dc949-174">按一下**編輯**toolaunch hello 查詢編輯器中新的視窗 tootransform hello 資料。</span><span class="sxs-lookup"><span data-stu-id="dc949-174">Click **Edit** toolaunch hello Query Editor in a new window tootransform hello data.</span></span>

## <a name="flattening-and-transforming-json-documents"></a><span data-ttu-id="dc949-175">簡維化和轉換 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="dc949-175">Flattening and transforming JSON documents</span></span>
1. <span data-ttu-id="dc949-176">切換 toohello Power BI 查詢編輯器 視窗，其中 hello**文件**hello 中間窗格內的資料行。</span><span class="sxs-lookup"><span data-stu-id="dc949-176">Switch toohello Power BI Query Editor window, where hello **Document** column in hello center pane.</span></span>
   <span data-ttu-id="dc949-177">![Power BI Desktop 查詢編輯器](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)</span><span class="sxs-lookup"><span data-stu-id="dc949-177">![Power BI Desktop Query Editor](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)</span></span>
2. <span data-ttu-id="dc949-178">按一下 在 hello hello 右邊 hello expander**文件**資料行標頭。</span><span class="sxs-lookup"><span data-stu-id="dc949-178">Click on hello expander at hello right side of hello **Document** column header.</span></span>  <span data-ttu-id="dc949-179">hello 與欄位清單的內容功能表隨即出現。</span><span class="sxs-lookup"><span data-stu-id="dc949-179">hello context menu with a list of fields will appear.</span></span>  <span data-ttu-id="dc949-180">選取您報表所需的例如 hello 欄位、 火山名稱、 國家/地區、 區域、 位置、 提高權限、 類型、 狀態和上次知道 Eruption，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="dc949-180">Select hello fields you need for your report, for instance,  Volcano Name, Country, Region, Location, Elevation, Type, Status and Last Know Eruption, and then click **OK**.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 展開文件](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. <span data-ttu-id="dc949-182">hello 中央窗格會顯示 hello 結果的預覽與選取的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="dc949-182">hello center pane will display a preview of hello result with hello fields selected.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 壓平合併結果](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. <span data-ttu-id="dc949-184">在本例中，hello Location 屬性是 GeoJSON 區塊文件中。</span><span class="sxs-lookup"><span data-stu-id="dc949-184">In our example, hello Location property is a GeoJSON block in a document.</span></span>  <span data-ttu-id="dc949-185">如您所見，[位置] 顯示為 Power BI Desktop 中的 [記錄]  類型。</span><span class="sxs-lookup"><span data-stu-id="dc949-185">As you can see, Location is represented as a **Record** type in Power BI Desktop.</span></span>  
5. <span data-ttu-id="dc949-186">按一下 hello expander 在 hello 位置資料行標頭 hello 右邊。</span><span class="sxs-lookup"><span data-stu-id="dc949-186">Click on hello expander at hello right side of hello Location column header.</span></span>  <span data-ttu-id="dc949-187">hello 的型別與座標欄位的內容功能表隨即出現。</span><span class="sxs-lookup"><span data-stu-id="dc949-187">hello context menu with type and coordinates fields will appear.</span></span>  <span data-ttu-id="dc949-188">讓我們選取 hello 座標欄位並按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="dc949-188">Let's select hello coordinates field and click **OK**.</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 位置記錄](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. <span data-ttu-id="dc949-190">hello 中央窗格現在會顯示的資料行座標**清單**型別。</span><span class="sxs-lookup"><span data-stu-id="dc949-190">hello center pane now shows a coordinates column of **List** type.</span></span>  <span data-ttu-id="dc949-191">在 hello 開頭 hello 教學課程中所示，hello GeoJSON 資料在本教學課程是點型別的記錄 hello 座標陣列中的緯度與經度值。</span><span class="sxs-lookup"><span data-stu-id="dc949-191">As shown at hello beginning of hello tutorial, hello GeoJSON data in this tutorial is of Point type with Latitude and Longitude values recorded in hello coordinates array.</span></span>
   
    <span data-ttu-id="dc949-192">hello 座標 [0] 項目代表經度，而座標 [1] 表示緯度。</span><span class="sxs-lookup"><span data-stu-id="dc949-192">hello coordinates[0] element represents Longitude while coordinates[1] represents Latitude.</span></span>
    <span data-ttu-id="dc949-193">![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 座標清單](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)</span><span class="sxs-lookup"><span data-stu-id="dc949-193">![Power BI tutorial for Azure Cosmos DB Power BI connector - Coordinates list](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)</span></span>
7. <span data-ttu-id="dc949-194">tooflatten hello 座標的陣列，我們將建立**自訂資料行**呼叫 LatLong。</span><span class="sxs-lookup"><span data-stu-id="dc949-194">tooflatten hello coordinates array, we will create a **Custom Column** called LatLong.</span></span>  <span data-ttu-id="dc949-195">選取 hello**加入資料行**功能區，然後按一下 **新增自訂資料行**。</span><span class="sxs-lookup"><span data-stu-id="dc949-195">Select hello **Add Column** ribbon and click on **Add Custom Column**.</span></span>  <span data-ttu-id="dc949-196">hello**新增自訂資料行**視窗應該會出現。</span><span class="sxs-lookup"><span data-stu-id="dc949-196">hello **Add Custom Column** window should appear.</span></span>
8. <span data-ttu-id="dc949-197">提供 hello 新資料行，例如 LatLong 的名稱。</span><span class="sxs-lookup"><span data-stu-id="dc949-197">Provide a name for hello new column, e.g. LatLong.</span></span>
9. <span data-ttu-id="dc949-198">接下來，指定 hello hello 新資料行的自訂公式。</span><span class="sxs-lookup"><span data-stu-id="dc949-198">Next, specify hello custom formula for hello new column.</span></span>  <span data-ttu-id="dc949-199">範例中，我們將串連 hello 緯度與經度值以逗號分隔，如下所示使用下列公式的 hello: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`。</span><span class="sxs-lookup"><span data-stu-id="dc949-199">For our example, we will concatenate hello Latitude and Longitude values separated by a comma as shown below using hello following formula: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`.</span></span> <span data-ttu-id="dc949-200">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="dc949-200">Click **OK**.</span></span>
   
    <span data-ttu-id="dc949-201">如需資料分析運算式 (DAX) (包括 DAX 函數) 的詳細資訊，請瀏覽 [Power BI Desktop 中的 DAX 基礎](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop)。</span><span class="sxs-lookup"><span data-stu-id="dc949-201">For more information on Data Analysis Expressions (DAX) including DAX functions, please visit [DAX Basic in Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).</span></span>
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 新增自訂資料行](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. <span data-ttu-id="dc949-203">現在，hello 中央窗格會顯示 hello 新 LatLong 的資料行填入 hello 緯度和經度值以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="dc949-203">Now, hello center pane will show hello new LatLong column populated with hello Latitude and Longitude values separated by a comma.</span></span>
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 自訂 LatLong 資料行](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    <span data-ttu-id="dc949-205">如果您收到錯誤 hello 新資料行中，確定 [查詢設定] 下的 hello 套用步驟符合下列圖的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc949-205">If you receive an Error in hello new column, make sure that hello applied steps under Query Settings match hello following figure:</span></span>
    
    ![套用的步驟應該是來源、瀏覽、展開的文件、展開的 Document.Location、新增的自訂](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    <span data-ttu-id="dc949-207">如果您的步驟不同，刪除 hello 額外的步驟，然後再試一次加入 hello 自訂資料行。</span><span class="sxs-lookup"><span data-stu-id="dc949-207">If your steps are different, delete hello extra steps and try adding hello custom column again.</span></span> 
11. <span data-ttu-id="dc949-208">我們現在已經完成將簡維的 hello 資料成表格式格式。</span><span class="sxs-lookup"><span data-stu-id="dc949-208">We have now completed flattening hello data into tabular format.</span></span>  <span data-ttu-id="dc949-209">您可以利用所有可用 hello tooshape 查詢編輯器中的 hello 功能，並轉換 Cosmos DB 中的資料。</span><span class="sxs-lookup"><span data-stu-id="dc949-209">You can leverage all of hello features available in hello Query Editor tooshape and transform data in Cosmos DB.</span></span>  <span data-ttu-id="dc949-210">如果您使用 hello 範例，hello 資料類型變更的提升權限太**整數**藉由變更 hello**資料型別**上 hello**首頁**功能區。</span><span class="sxs-lookup"><span data-stu-id="dc949-210">If you're using hello sample, change hello data type for Elevation too**Whole number** by changing hello **Data Type** on hello **Home** ribbon.</span></span>
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 變更資料行類型](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. <span data-ttu-id="dc949-212">按一下**關閉並套用**toosave hello 資料模型。</span><span class="sxs-lookup"><span data-stu-id="dc949-212">Click **Close and Apply** toosave hello data model.</span></span>
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 關閉並套用](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a><span data-ttu-id="dc949-214">建立 hello 報表</span><span class="sxs-lookup"><span data-stu-id="dc949-214">Build hello reports</span></span>
<span data-ttu-id="dc949-215">Power BI Desktop 報表檢視是您可以啟動 toovisualize 資料建立報表的位置。</span><span class="sxs-lookup"><span data-stu-id="dc949-215">Power BI Desktop Report view is where you can start creating reports toovisualize data.</span></span>  <span data-ttu-id="dc949-216">您可以建立報表的欄位拖放到 hello**報表**畫布。</span><span class="sxs-lookup"><span data-stu-id="dc949-216">You can create reports by dragging and dropping fields into hello **Report** canvas.</span></span>

![Power BI Desktop 報告檢視 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

<span data-ttu-id="dc949-218">在 hello 報表檢視中，您應該看到：</span><span class="sxs-lookup"><span data-stu-id="dc949-218">In hello Report view, you should find:</span></span>

1. <span data-ttu-id="dc949-219">hello**欄位** 窗格中，這是您會看到的資料模型，您可以使用報表的欄位清單的位置。</span><span class="sxs-lookup"><span data-stu-id="dc949-219">hello **Fields** pane, this is where you will see a list of data models with fields you can use for your reports.</span></span>
2. <span data-ttu-id="dc949-220">hello**視覺效果**窗格。</span><span class="sxs-lookup"><span data-stu-id="dc949-220">hello **Visualizations** pane.</span></span> <span data-ttu-id="dc949-221">一份報告可以包含一或多個視覺效果。</span><span class="sxs-lookup"><span data-stu-id="dc949-221">A report can contain a single or multiple visualizations.</span></span>  <span data-ttu-id="dc949-222">挑選適合您的需求，從 hello hello visual 類型**視覺效果**窗格。</span><span class="sxs-lookup"><span data-stu-id="dc949-222">Pick hello visual types fitting your needs from hello **Visualizations** pane.</span></span>
3. <span data-ttu-id="dc949-223">hello**報表**畫布，這是您將在其中建立報表 hello 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="dc949-223">hello **Report** canvas, this is where you will build hello visuals for your report.</span></span>
4. <span data-ttu-id="dc949-224">hello**報表**頁面。</span><span class="sxs-lookup"><span data-stu-id="dc949-224">hello **Report** page.</span></span> <span data-ttu-id="dc949-225">您可以在 Power BI Desktop 中心增多個報告頁面。</span><span class="sxs-lookup"><span data-stu-id="dc949-225">You can add multiple report pages in Power BI Desktop.</span></span>

<span data-ttu-id="dc949-226">hello 下列範例示範建立簡單的互動式地圖檢視報表的 hello 基本步驟。</span><span class="sxs-lookup"><span data-stu-id="dc949-226">hello following shows hello basic steps of creating a simple interactive Map view report.</span></span>

1. <span data-ttu-id="dc949-227">範例中，我們將建立地圖檢視顯示每個火山 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="dc949-227">For our example, we will create a map view showing hello location of each volcano.</span></span>  <span data-ttu-id="dc949-228">在 hello**視覺效果** 窗格中，按一下 hello 上方螢幕擷取畫面中反白顯示 hello 地圖視覺效果類型。</span><span class="sxs-lookup"><span data-stu-id="dc949-228">In hello **Visualizations** pane, click on hello Map visual type as highlighted in hello screenshot above.</span></span>  <span data-ttu-id="dc949-229">您應該會看見 hello 地圖視覺效果類型繪製在 hello**報表**畫布。</span><span class="sxs-lookup"><span data-stu-id="dc949-229">You should see hello Map visual type painted on hello **Report** canvas.</span></span>  <span data-ttu-id="dc949-230">hello**視覺效果**窗格也應該會顯示一組屬性相關 toohello 地圖視覺效果類型。</span><span class="sxs-lookup"><span data-stu-id="dc949-230">hello **Visualization** pane should also display a set of properties related toohello Map visual type.</span></span>
2. <span data-ttu-id="dc949-231">現在，從拖放 hello LatLong 欄位 hello**欄位**窗格 toohello**位置**屬性**視覺效果**窗格。</span><span class="sxs-lookup"><span data-stu-id="dc949-231">Now, drag and drop hello LatLong field from hello **Fields** pane toohello **Location** property in **Visualizations** pane.</span></span>
3. <span data-ttu-id="dc949-232">下一步，拖曳和卸除 hello 火山名稱欄位 toohello**圖例**屬性。</span><span class="sxs-lookup"><span data-stu-id="dc949-232">Next, drag and drop hello Volcano Name field toohello **Legend** property.</span></span>  
4. <span data-ttu-id="dc949-233">然後，拖曳和卸除 hello 提高權限欄位 toohello**大小**屬性。</span><span class="sxs-lookup"><span data-stu-id="dc949-233">Then, drag and drop hello Elevation field toohello **Size** property.</span></span>  
5. <span data-ttu-id="dc949-234">您現在應該會看到 hello 視覺顯示一組指出 hello 位置的每個火山 hello 相互關聯的 hello 火山 toohello 提高權限的 hello 泡泡大小的泡泡地圖。</span><span class="sxs-lookup"><span data-stu-id="dc949-234">You should now see hello Map visual showing a set of bubbles indicating hello location of each volcano with hello size of hello bubble correlating toohello elevation of hello volcano.</span></span>
6. <span data-ttu-id="dc949-235">現在您已建立基本報告。</span><span class="sxs-lookup"><span data-stu-id="dc949-235">You now have created a basic report.</span></span>  <span data-ttu-id="dc949-236">您可以加入更多視覺效果，進一步自訂 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="dc949-236">You can further customize hello report by adding more visualizations.</span></span>  <span data-ttu-id="dc949-237">在我們的案例中，我們加入了火山類型交叉分析篩選器 toomake hello 報表互動。</span><span class="sxs-lookup"><span data-stu-id="dc949-237">In our case, we added a Volcano Type slicer toomake hello report interactive.</span></span>  
   
    ![Hello 最終 Power BI Desktop 報表 for Azure Cosmos DB hello Power BI 教學課程完成時的螢幕擷取畫面](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a><span data-ttu-id="dc949-239">發佈和共用您的報告</span><span class="sxs-lookup"><span data-stu-id="dc949-239">Publish and share your report</span></span>
<span data-ttu-id="dc949-240">tooshare 報表時，您必須在 PowerBI.com 中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc949-240">tooshare your report, you must have an account in PowerBI.com.</span></span>

1. <span data-ttu-id="dc949-241">在 hello Power BI Desktop 中，按一下 hello**首頁**功能區。</span><span class="sxs-lookup"><span data-stu-id="dc949-241">In hello Power BI Desktop, click on hello **Home** ribbon.</span></span>
2. <span data-ttu-id="dc949-242">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="dc949-242">Click **Publish**.</span></span>  <span data-ttu-id="dc949-243">PowerBI.com 帳戶，您將會是提示的 tooenter hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="dc949-243">You will be prompted tooenter hello user name and password for your PowerBI.com account.</span></span>
3. <span data-ttu-id="dc949-244">Hello 認證經過驗證之後，一旦 hello 報表就會是您所選取的已發行的 tooyour 目的地。</span><span class="sxs-lookup"><span data-stu-id="dc949-244">Once hello credential has been authenticated, hello report is published tooyour destination you selected.</span></span>
4. <span data-ttu-id="dc949-245">按一下**開啟 'PowerBITutorial.pbix' Power BI 中的**toosee 和共用您在 powerbi.com 內的報表。</span><span class="sxs-lookup"><span data-stu-id="dc949-245">Click **Open 'PowerBITutorial.pbix' in Power BI** toosee and share your report on PowerBI.com.</span></span>
   
    ![發行 tooPower BI 成功 ！](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a><span data-ttu-id="dc949-248">在 PowerBI.com 中建立儀表板</span><span class="sxs-lookup"><span data-stu-id="dc949-248">Create a dashboard in PowerBI.com</span></span>
<span data-ttu-id="dc949-249">現在，您有一份報表可在 PowerBI.com 上共用。</span><span class="sxs-lookup"><span data-stu-id="dc949-249">Now that you have a report, lets share it on PowerBI.com</span></span>

<span data-ttu-id="dc949-250">當您發行報表從 Power BI Desktop tooPowerBI.com 時，它會產生**報表**和**資料集**PowerBI.com 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="dc949-250">When you publish your report from Power BI Desktop tooPowerBI.com, it generates a **Report** and a **Dataset** in your PowerBI.com tenant.</span></span> <span data-ttu-id="dc949-251">比方說，之後您將報表發行呼叫**PowerBITutorial** tooPowerBI.com，您會看到 PowerBITutorial 中這兩個 hello**報表**和**資料集**上一節PowerBI.com。</span><span class="sxs-lookup"><span data-stu-id="dc949-251">For example, after you published a report called **PowerBITutorial** tooPowerBI.com, you will see PowerBITutorial in both hello **Reports** and **Datasets** sections on PowerBI.com.</span></span>

   ![新的報表和 PowerBI.com 中的資料集，hello 的螢幕擷取畫面](./media/powerbi-visualize/powerbi-reports-datasets.png)

<span data-ttu-id="dc949-253">toocreate 可共用的儀表板，按一下 hello**釘選即時頁面**PowerBI.com 報表上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc949-253">toocreate a sharable dashboard, click hello **Pin Live Page** button on your PowerBI.com report.</span></span>

   ![新的報表和 PowerBI.com 中的資料集，hello 的螢幕擷取畫面](./media/powerbi-visualize/power-bi-pin-live-tile.png)

<span data-ttu-id="dc949-255">然後依照中的 hello 指示[從報表將磚釘選](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report)toocreate 新儀表板。</span><span class="sxs-lookup"><span data-stu-id="dc949-255">Then follow hello instructions in [Pin a tile from a report](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate a new dashboard.</span></span> 

<span data-ttu-id="dc949-256">您也可以建立儀表板之前進行臨機操作修改 tooreport。</span><span class="sxs-lookup"><span data-stu-id="dc949-256">You can also do ad hoc modifications tooreport before creating a dashboard.</span></span> <span data-ttu-id="dc949-257">不過，建議您使用 Power BI Desktop tooperform hello 修改並重新發行 hello 報表 tooPowerBI.com。</span><span class="sxs-lookup"><span data-stu-id="dc949-257">However, it's recommended that you use Power BI Desktop tooperform hello modifications and republish hello report tooPowerBI.com.</span></span>

## <a name="refresh-data-in-powerbicom"></a><span data-ttu-id="dc949-258">重新整理 PowerBI.com 中的資料</span><span class="sxs-lookup"><span data-stu-id="dc949-258">Refresh data in PowerBI.com</span></span>
<span data-ttu-id="dc949-259">有兩種方式 toorefresh 資料，隨選和排程。</span><span class="sxs-lookup"><span data-stu-id="dc949-259">There are two ways toorefresh data, ad hoc and scheduled.</span></span>

<span data-ttu-id="dc949-260">針對臨機操作的重新整理，只要按一下 hello eclipses （...） 的 hello**資料集**，例如 PowerBITutorial。</span><span class="sxs-lookup"><span data-stu-id="dc949-260">For an ad hoc refresh, simply click on hello eclipses (…) by hello **Dataset**, e.g. PowerBITutorial.</span></span> <span data-ttu-id="dc949-261">您應該會看到包括 [立即重新整理] 在內的動作清單。</span><span class="sxs-lookup"><span data-stu-id="dc949-261">You should see a list of actions including **Refresh Now**.</span></span> <span data-ttu-id="dc949-262">按一下**立即重新整理**toorefresh hello 資料。</span><span class="sxs-lookup"><span data-stu-id="dc949-262">Click **Refresh Now** toorefresh hello data.</span></span>

![PowerBI.com 中立即重新整理的螢幕擷取畫面](./media/powerbi-visualize/power-bi-refresh-now.png)

<span data-ttu-id="dc949-264">排定的重新整理，請勿 hello 遵循。</span><span class="sxs-lookup"><span data-stu-id="dc949-264">For a scheduled refresh, do hello following.</span></span>

1. <span data-ttu-id="dc949-265">按一下**排程重新整理**hello 動作清單中。</span><span class="sxs-lookup"><span data-stu-id="dc949-265">Click **Schedule Refresh** in hello action list.</span></span> 

    ![排程重新整理在 PowerBI.com 中的 hello 的螢幕擷取畫面](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. <span data-ttu-id="dc949-267">在 hello**設定**頁面上，展開**資料來源認證**。</span><span class="sxs-lookup"><span data-stu-id="dc949-267">In hello **Settings** page, expand **Data source credentials**.</span></span> 
3. <span data-ttu-id="dc949-268">按一下 [編輯認證] 。</span><span class="sxs-lookup"><span data-stu-id="dc949-268">Click on **Edit credentials**.</span></span> 
   
    <span data-ttu-id="dc949-269">hello 設定快顯視窗出現。</span><span class="sxs-lookup"><span data-stu-id="dc949-269">hello Configure popup appears.</span></span> 
4. <span data-ttu-id="dc949-270">輸入 hello 金鑰 tooconnect toohello Cosmos DB 帳戶，該資料集，然後按一下 **登入**。</span><span class="sxs-lookup"><span data-stu-id="dc949-270">Enter hello key tooconnect toohello Cosmos DB account for that data set, then click **Sign in**.</span></span> 
5. <span data-ttu-id="dc949-271">展開**排程重新整理**和您設定 hello 排程要 toorefresh hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="dc949-271">Expand **Schedule Refresh** and set up hello schedule you want toorefresh hello dataset.</span></span> 
6. <span data-ttu-id="dc949-272">按一下**套用**和您在設定 hello 排定的重新整理。</span><span class="sxs-lookup"><span data-stu-id="dc949-272">Click **Apply** and you are done setting up hello scheduled refresh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc949-273">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc949-273">Next steps</span></span>
* <span data-ttu-id="dc949-274">toolearn 深入了解 Power BI 中，請參閱[開始使用 Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="dc949-274">toolearn more about Power BI, see [Get started with Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).</span></span>
* <span data-ttu-id="dc949-275">深入了解 Cosmos DB toolearn 看到 hello [Azure Cosmos DB 文件登陸頁面](https://azure.microsoft.com/documentation/services/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="dc949-275">toolearn more about Cosmos DB, see hello [Azure Cosmos DB documentation landing page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

