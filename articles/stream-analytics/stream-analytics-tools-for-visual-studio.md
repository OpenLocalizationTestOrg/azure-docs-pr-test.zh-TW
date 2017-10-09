---
title: "Azure 資料流分析 Tools for Visual Studio aaaUse |Microsoft 文件"
description: "Hello Azure 資料流分析 Tools for Visual Studio 使用者入門教學課程"
keywords: visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="0c9ee-104">使用適用於 Visual Studio 的 Azure 串流分析工具</span><span class="sxs-lookup"><span data-stu-id="0c9ee-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="0c9ee-105">簡介</span><span class="sxs-lookup"><span data-stu-id="0c9ee-105">Introduction</span></span>
<span data-ttu-id="0c9ee-106">在本教學課程中，您將學習如何 toouse Azure 資料流分析 Tools for Visual Studio toocreate 撰寫、 在本機測試，和偵錯資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="0c9ee-107">完成本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="0c9ee-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="0c9ee-108">熟悉適用於 Visual Studio 的串流分析工具。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="0c9ee-109">設定及部署串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="0c9ee-110">使用本機範例資料於本機測試作業。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="0c9ee-111">使用監視 tootroubleshoot 問題。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="0c9ee-112">將現有的工作 tooprojects 的匯出。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c9ee-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="0c9ee-113">Prerequisites</span></span>
<span data-ttu-id="0c9ee-114">toocomplete 本教學課程中，您需要下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="0c9ee-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="0c9ee-115">在 hello 完成前面的 「 建立資料流分析工作 」 的 hello 步驟[使用 Stream Analytics 教學課程建置的 IoT 解決方案](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics)。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="0c9ee-116">使用 Visual Studio 2015、Visual Studio 2013 Update 4 或 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="0c9ee-117">支援 Enterprise (Ultimate/Premium)、Professional 和 Community 版本。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="0c9ee-118">不支援 Express 版本。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-118">Express edition is not supported.</span></span> <span data-ttu-id="0c9ee-119">不支援 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="0c9ee-120">使用 hello Azure SDK for.NET 版本 2.7.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="0c9ee-121">安裝使用 hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="0c9ee-122">安裝 hello[資料流分析 Tools for Visual Studio](http://aka.ms/asatoolsvs)。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="0c9ee-123">建立串流分析專案</span><span class="sxs-lookup"><span data-stu-id="0c9ee-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="0c9ee-124">在 Visual Studio 中，按一下 hello**檔案**功能表，然後選取**新專案**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="0c9ee-125">在左側 hello hello 範本清單中選取**Stream Analytics** ，然後按一下 **Azure 資料流分析應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="0c9ee-126">輸入 hello 專案**名稱**，**位置**，和**方案名稱**的其他專案一樣。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![[新增專案] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="0c9ee-128">[方案總管] 中會產生 **Toll** 專案。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![[方案總管] 中產生的 Toll 專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="0c9ee-130">選擇 hello 正確的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0c9ee-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="0c9ee-131">在 Visual Studio 中，按一下 hello**檢視**功能表，並開啟**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="0c9ee-132">使用 Azure 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="0c9ee-133">定義 hello 輸入的來源</span><span class="sxs-lookup"><span data-stu-id="0c9ee-133">Define hello input sources</span></span>
1.  <span data-ttu-id="0c9ee-134">在**方案總管] 中**，依序展開 [hello**輸入**節點，然後重新命名**Input.json**太**EntryStream.json**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="0c9ee-135">按兩下 **EntryStream.json**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="0c9ee-136">hello**輸入別名**現在**EntryStream**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="0c9ee-137">hello 輸入別名是 hello 查詢指令碼中使用。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="0c9ee-138">在 [來源類型] 中，選取 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="0c9ee-139">在 [來源] 中，選取 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="0c9ee-140">在**服務匯流排命名空間**，選取 hello **TollData**選項。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="0c9ee-141">在 [事件中樞名稱] 中，選取 [entry]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="0c9ee-142">在**事件中樞原則名稱**，選取**RootManageSharedAccessKey** (hello 預設值)。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="0c9ee-143">在 [事件序列化格式] 中，選取 [Json]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="0c9ee-144">在 [編碼] 中，選取 [UTF8]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="0c9ee-145">您的設定應該看起來像下列螢幕擷取畫面的 hello:</span><span class="sxs-lookup"><span data-stu-id="0c9ee-145">Your settings should look like hello following screenshot:</span></span>

    ![[輸入] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="0c9ee-147">toofinish hello 精靈] 中，按一下 [**儲存**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="0c9ee-148">現在您可以加入另一個輸入的來源 toocreate hello 結束資料流。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="0c9ee-149">以滑鼠右鍵按一下 hello**輸入**節點，然後選取**新項目**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![新增項目](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="0c9ee-151">在 hello 視窗中，選取  **Azure 資料流分析輸入**，並變更 hello**名稱**太**ExitStream.json**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="0c9ee-152">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-152">Click **Add**.</span></span>

    ![[加入新項目] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="0c9ee-154">按兩下**ExitStream.json** hello 專案和後續 hello 相同步驟的 hello 項目資料流中。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="0c9ee-155">要確定 tooenter**結束**hello**事件中樞名稱**hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="0c9ee-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![ExitStream 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="0c9ee-157">您現在已定義兩個輸入資料流：</span><span class="sxs-lookup"><span data-stu-id="0c9ee-157">Now you have defined two input streams:</span></span>

    ![進入和離開的輸入資料流](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="0c9ee-159">接下來，加入包含汽車註冊資料的 hello blob 檔案的參考資料輸入。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="0c9ee-160">以滑鼠右鍵按一下 hello**輸入**hello 專案，然後再遵循 hello 相同步驟 hello 資料流輸入的節點。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="0c9ee-161">在 [輸入別名] 中，輸入 **Registration**，然後在 [來源類型] 中，選取 [參考資料]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![[註冊] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="0c9ee-163">在**儲存體帳戶**，選取 hello **tolldata**選項。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="0c9ee-164">在 [容器] 中，選取 [tolldata]，然後在 [路徑模式] 中，輸入 **registration.json**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="0c9ee-165">這個檔案名稱會區分大小寫，且應該是小寫。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="0c9ee-166">toofinish hello 精靈] 中，按一下 [**儲存**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="0c9ee-167">現在會定義所有 hello 輸入值。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="0c9ee-168">定義 hello 輸出</span><span class="sxs-lookup"><span data-stu-id="0c9ee-168">Define hello output</span></span>
1.  <span data-ttu-id="0c9ee-169">在**方案總管] 中**，依序展開 [hello**輸入**節點，然後按兩下**Output.json**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="0c9ee-170">在 [輸出別名] 中，輸入 **output**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="0c9ee-171">在 [接收] 中，選取 [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="0c9ee-172">在 [資料庫] 中，選取 [TollDataDB]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="0c9ee-173">在 [使用者名稱] 中，輸入 **tolladmin**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="0c9ee-174">在 [密碼] 中，輸入 **123toll!**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="0c9ee-175">在 [資料表] 中，輸入 **TollDataRefJoin**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="0c9ee-176">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-176">Click **Save**.</span></span>

    ![[輸出] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="0c9ee-178">建立串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="0c9ee-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="0c9ee-179">本教學課程中嘗試 tooanswer tootoll 相關資料的數個商務問題。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="0c9ee-180">它也會建構資料流分析查詢，可用於資料流分析 tooprovide 相關解答。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="0c9ee-181">在您開始第一個資料流分析工作之前，讓我們來探索簡單的案例和 hello 查詢語法。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="0c9ee-182">簡介 toohello 串流分析查詢語言</span><span class="sxs-lookup"><span data-stu-id="0c9ee-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="0c9ee-183">例如，假設您需要輸入收費亭的車輛 toocount hello 數目。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="0c9ee-184">這個範例是連續的資料流的事件，因為您尚未 toodefine 一段時間。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="0c9ee-185">修改 hello 問題 toobe 「 多少車輛輸入收費亭每隔三分鐘？ 」</span><span class="sxs-lookup"><span data-stu-id="0c9ee-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="0c9ee-186">這通常是資料的方式 toocount 稱為 tooas hello 輪轉計數。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="0c9ee-187">查看 hello 資料流分析查詢，此問題的答案：</span><span class="sxs-lookup"><span data-stu-id="0c9ee-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="0c9ee-188">資料流分析會使用類似 SQL 的查詢語言加入幾個擴充功能 toospecify 時間相關的層面 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="0c9ee-189">如需詳細資訊，請參閱[時間管理](https://msdn.microsoft.com/library/azure/mt582045.aspx)和[Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx)從 MSDN 的 hello 查詢中使用的建構。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="0c9ee-190">現在您已經撰寫第一個資料流分析查詢，它是時間 tootest 它。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="0c9ee-191">使用位於下列路徑的 hello 中您 TollApp 資料夾中的 hello 範例資料檔：</span><span class="sxs-lookup"><span data-stu-id="0c9ee-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="0c9ee-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="0c9ee-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="0c9ee-193">此資料夾包含下列檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="0c9ee-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="0c9ee-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="0c9ee-194">Entry.json</span></span>
*   <span data-ttu-id="0c9ee-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="0c9ee-195">Exit.json</span></span>
*   <span data-ttu-id="0c9ee-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="0c9ee-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="0c9ee-197">計算 hello 進入收費亭的車輛數目。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="0c9ee-198">在 hello 專案中，按兩下**Script.asaql** tooopen hello 指令碼在 hello**查詢編輯器**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="0c9ee-199">複製並貼入 hello 指令碼 hello 前一節中 hello 編輯器。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="0c9ee-200">hello 查詢編輯器支援 IntelliSense、 語法著色和 hello 錯誤標記。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![查詢編輯器](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="0c9ee-202">在本機測試串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="0c9ee-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="0c9ee-203">如果沒有語法錯誤，toocompile hello 查詢 toosee hello 專案上按一下滑鼠右鍵，然後選取**建置**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="0c9ee-204">toovalidate 這項查詢針對取樣資料，您可以使用本機的範例資料。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="0c9ee-205">以滑鼠右鍵按一下 hello 輸入，然後選取**新增本機輸入**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-205">Right-click hello input, and select **Add local input**.</span></span>

    ![新增本機輸入](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="0c9ee-207">在 hello 快顯視窗中，請從您的本機路徑選取 hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="0c9ee-208">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-208">Click **Save**.</span></span>

    ![[新增本機輸入] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="0c9ee-210">名為**local_EntryStream.json**會自動加入 tooyour 輸入資料夾。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![檔案已加入的 tooinputs 資料夾](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="0c9ee-212">在 hello**查詢編輯器**，按一下 **在本機執行**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="0c9ee-213">或者，您可以按 F5 鍵，hello。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-213">Or you can press hello F5 key.</span></span>

    ![在本機執行](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![本機執行輸出](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="0c9ee-216">在 hello 中按下任何鍵 tooview hello 輸出**ASA 本機執行結果**Visual Studio 中的視窗。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![[ASA 本機執行結果] 視窗](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="0c9ee-218">按一下**開啟結果資料夾**toocheck hello 輸出檔案，兩者都採用 CSV 和 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![開啟結果資料夾輸出](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="0c9ee-220">範例 hello 輸入的資料</span><span class="sxs-lookup"><span data-stu-id="0c9ee-220">Sample hello input data</span></span>
<span data-ttu-id="0c9ee-221">您也可以從輸入的來源 tooa 本機檔案的範例輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="0c9ee-222">Hello 輸入的組態檔中，以滑鼠右鍵按一下並選取**範例資料**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![範例資料](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="0c9ee-224">目前只能取樣事件中樞或 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="0c9ee-225">不支援其他輸入來源。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="0c9ee-226">在 [hello] 快顯視窗中，輸入 hello 用的本機路徑 toosave hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="0c9ee-227">按一下 [取樣]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-227">Click **Sample**.</span></span>

    ![[範例資料] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="0c9ee-229">您可以看到在 hello hello 進度**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-229">You can see hello progress in hello **Output** window.</span></span> 

    ![[輸出] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="0c9ee-231">提交資料流分析查詢 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0c9ee-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="0c9ee-232">在 hello**查詢編輯器**，按一下 **提交 tooAzure** hello 指令碼編輯器中。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![提交 tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="0c9ee-234">選取 [建立新的 Azure 串流分析作業]。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="0c9ee-235">輸入 hello**工作名稱**，並選取正確的 hello**訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="0c9ee-236">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-236">Click **Submit**.</span></span>

    ![[提交作業] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="0c9ee-238">啟動作業</span><span class="sxs-lookup"><span data-stu-id="0c9ee-238">Start a job</span></span>
<span data-ttu-id="0c9ee-239">現在，建立您的工作時，會自動開啟 hello 工作檢視。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="0c9ee-240">toostart hello 作業中，按一下 hello**綠色箭號** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![啟動作業](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="0c9ee-242">選取 hello 預設設定，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-242">Select hello default setting, and click **Start**.</span></span>
 
    ![[啟動作業] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="0c9ee-244">hello 作業**狀態**變更太**執行**，和**輸入事件**和**輸出事件**出現。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![作業摘要中的 [執行中] 狀態](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="0c9ee-246">檢查 Visual Studio 中的 hello 結果</span><span class="sxs-lookup"><span data-stu-id="0c9ee-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="0c9ee-247">在 Visual Studio 中開啟**伺服器總管**並以滑鼠右鍵按一下 hello **TollDataRefJoin**資料表。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="0c9ee-248">選取**顯示資料表資料**toosee hello 輸出的工作。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![在伺服器總管中選取 [顯示資料表資料]](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="0c9ee-250">檢視 hello 工作指標</span><span class="sxs-lookup"><span data-stu-id="0c9ee-250">View hello job metrics</span></span>
<span data-ttu-id="0c9ee-251">您可以在 [作業計量] 找到一些基本的作業統計資料。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![[作業計量] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="0c9ee-253">在伺服器總管 中的清單 hello 工作</span><span class="sxs-lookup"><span data-stu-id="0c9ee-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="0c9ee-254">在 伺服器總管 中，按一下 串流分析作業，然後按一下重新整理。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="0c9ee-255">hello 作業之下**串流分析工作**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-255">hello job appears under **Stream Analytics jobs**.</span></span>

![伺服器總管中列出的串流分析作業](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="0c9ee-257">開啟 hello 工作檢視</span><span class="sxs-lookup"><span data-stu-id="0c9ee-257">Open hello job view</span></span>
<span data-ttu-id="0c9ee-258">tooopen hello 工作檢視中，展開作業節點，然後按兩下 hello**工作檢視**節點。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![[作業檢視] 節點](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="0c9ee-260">匯出工作 tooa 現有專案</span><span class="sxs-lookup"><span data-stu-id="0c9ee-260">Export an existing job tooa project</span></span>
<span data-ttu-id="0c9ee-261">有兩種方式，您可以將現有的工作 tooa 專案匯出。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="0c9ee-262">中**伺服器總管**，以滑鼠右鍵按一下 hello 作業節點在 hello**資料流分析工作**節點，然後選取**匯出 tooNew 資料流分析專案**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![匯出 tooNew 資料流分析的專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="0c9ee-264">hello 專案中產生**方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-264">hello project is generated in **Solution Explorer**.</span></span>

![[方案總管] 中產生的專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="0c9ee-266">您也可以使用 hello 工作檢視，然後按一下**產生專案**。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-266">You also can use hello job view, and click **Generate Project**.</span></span>

![產生專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="0c9ee-268">已知問題與限制</span><span class="sxs-lookup"><span data-stu-id="0c9ee-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="0c9ee-269">不支援 Power BI 輸出和 Azure Data Lake Store 輸出。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="0c9ee-270">編輯器不支援新增或變更 JavaScript 使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="0c9ee-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c9ee-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c9ee-271">Next steps</span></span>
* [<span data-ttu-id="0c9ee-272">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="0c9ee-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0c9ee-273">開始使用 Azure 串流分析</span><span class="sxs-lookup"><span data-stu-id="0c9ee-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0c9ee-274">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="0c9ee-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0c9ee-275">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="0c9ee-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0c9ee-276">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="0c9ee-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
