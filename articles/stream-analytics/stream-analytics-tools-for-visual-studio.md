---
title: "使用適用於 Visual Studio 的 Azure 串流分析工具 | Microsoft Docs"
description: "開始使用適用於 Visual Studio 的 Azure 串流分析工具"
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
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="58534-104">使用適用於 Visual Studio 的 Azure 串流分析工具</span><span class="sxs-lookup"><span data-stu-id="58534-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="58534-105">簡介</span><span class="sxs-lookup"><span data-stu-id="58534-105">Introduction</span></span>
<span data-ttu-id="58534-106">在本教學課程中，您將學習如何使用適用於 Visual Studio 的 Azure 串流分析工具來建立、撰寫、在本機測試、管理及偵錯 Azure 串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="58534-106">In this tutorial, you learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="58534-107">完成本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="58534-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="58534-108">熟悉適用於 Visual Studio 的串流分析工具。</span><span class="sxs-lookup"><span data-stu-id="58534-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="58534-109">設定及部署串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="58534-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="58534-110">使用本機範例資料於本機測試作業。</span><span class="sxs-lookup"><span data-stu-id="58534-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="58534-111">使用監視功能進行問題疑難排解。</span><span class="sxs-lookup"><span data-stu-id="58534-111">Use monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="58534-112">將現有作業匯出到專案。</span><span class="sxs-lookup"><span data-stu-id="58534-112">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58534-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="58534-113">Prerequisites</span></span>
<span data-ttu-id="58534-114">若要完成本教學課程，您需要下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="58534-114">To complete this tutorial, you need the following prerequisites:</span></span>
* <span data-ttu-id="58534-115">完成[利用串流分析來建置 IoT 解決方案教學課程](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics)中的「建立串流分析作業」之前的步驟。</span><span class="sxs-lookup"><span data-stu-id="58534-115">Finish the steps that precede "Create a Stream Analytics job" in the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="58534-116">使用 Visual Studio 2015、Visual Studio 2013 Update 4 或 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="58534-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="58534-117">支援 Enterprise (Ultimate/Premium)、Professional 和 Community 版本。</span><span class="sxs-lookup"><span data-stu-id="58534-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="58534-118">不支援 Express 版本。</span><span class="sxs-lookup"><span data-stu-id="58534-118">Express edition is not supported.</span></span> <span data-ttu-id="58534-119">不支援 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="58534-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="58534-120">使用 Azure SDK for .NET 2.7.1 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="58534-120">Use the Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="58534-121">使用 [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx) 來進行安裝。</span><span class="sxs-lookup"><span data-stu-id="58534-121">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="58534-122">安裝[適用於 Visual Studio 的串流分析工具](http://aka.ms/asatoolsvs)。</span><span class="sxs-lookup"><span data-stu-id="58534-122">Install the [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="58534-123">建立串流分析專案</span><span class="sxs-lookup"><span data-stu-id="58534-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="58534-124">在 Visual Studio 中，按一下 [檔案] 功能表，然後選取 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="58534-124">In Visual Studio, click the **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="58534-125">在左側的範本清單中，選取 [串流分析]，然後按一下 [Azure 串流分析應用程式]。</span><span class="sxs-lookup"><span data-stu-id="58534-125">In the templates list on the left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="58534-126">就像建立其他專案一樣，輸入專案 [名稱]、[位置] 和 [方案名稱]。</span><span class="sxs-lookup"><span data-stu-id="58534-126">Enter the project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![[新增專案] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="58534-128">[方案總管] 中會產生 **Toll** 專案。</span><span class="sxs-lookup"><span data-stu-id="58534-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![[方案總管] 中產生的 Toll 專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="58534-130">選擇正確的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="58534-130">Choose the correct subscription</span></span>
1. <span data-ttu-id="58534-131">在 Visual Studio 中，按一下 [檢視] 功能表，然後開啟 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="58534-131">In Visual Studio, click the **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="58534-132">使用 Azure 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="58534-132">Sign in with your Azure Account.</span></span> 

## <a name="define-the-input-sources"></a><span data-ttu-id="58534-133">定義輸入來源</span><span class="sxs-lookup"><span data-stu-id="58534-133">Define the input sources</span></span>
1.  <span data-ttu-id="58534-134">在 [方案總管] 中，展開 [輸入] 節點，並將 **Input.json** 重新命名為 **EntryStream.json**。</span><span class="sxs-lookup"><span data-stu-id="58534-134">In **Solution Explorer**, expand the **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="58534-135">按兩下 **EntryStream.json**。</span><span class="sxs-lookup"><span data-stu-id="58534-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="58534-136">[輸入別名] 現在是 **EntryStream**。</span><span class="sxs-lookup"><span data-stu-id="58534-136">The **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="58534-137">查詢指令碼中會使用此輸入別名。</span><span class="sxs-lookup"><span data-stu-id="58534-137">The input alias is used in the query script.</span></span> 
3.  <span data-ttu-id="58534-138">在 [來源類型] 中，選取 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="58534-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="58534-139">在 [來源] 中，選取 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="58534-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="58534-140">在 [服務匯流排命名空間] 中，選取 [TollData] 選項。</span><span class="sxs-lookup"><span data-stu-id="58534-140">In **Service Bus Namespace**, select the **TollData** option.</span></span>
6.  <span data-ttu-id="58534-141">在 [事件中樞名稱] 中，選取 [entry]。</span><span class="sxs-lookup"><span data-stu-id="58534-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="58534-142">在 [事件中樞原則名稱] 中，選取 [RootManageSharedAccessKey] \(預設值)。</span><span class="sxs-lookup"><span data-stu-id="58534-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="58534-143">在 [事件序列化格式] 中，選取 [Json]。</span><span class="sxs-lookup"><span data-stu-id="58534-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="58534-144">在 [編碼] 中，選取 [UTF8]。</span><span class="sxs-lookup"><span data-stu-id="58534-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="58534-145">您的設定應該如以下的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="58534-145">Your settings should look like the following screenshot:</span></span>

    ![[輸入] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="58534-147">若要完成精靈，請按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="58534-147">To finish the wizard, click **Save**.</span></span> <span data-ttu-id="58534-148">您現在可以新增另一個輸入來源以建立輸出資料流。</span><span class="sxs-lookup"><span data-stu-id="58534-148">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="58534-149">以滑鼠右鍵按一下 [輸入] 節點，然後選取 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="58534-149">Right-click the **Inputs** node, and select **New Item**.</span></span>

    ![新增項目](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="58534-151">在視窗中，選取 [Azure 串流分析輸入]，然後將 [名稱] 變更為 **ExitStream.json**。</span><span class="sxs-lookup"><span data-stu-id="58534-151">In the window, select **Azure Stream Analytics Input**, and change the **Name** to **ExitStream.json**.</span></span> <span data-ttu-id="58534-152">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="58534-152">Click **Add**.</span></span>

    ![[加入新項目] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="58534-154">在專案中按兩下 [ExitStream.json]，然後依照您在進入資料流中所做的相同步驟操作。</span><span class="sxs-lookup"><span data-stu-id="58534-154">Double-click **ExitStream.json** in the project, and follow the same steps as you did for the entry stream.</span></span> <span data-ttu-id="58534-155">請務必輸入 **exit** 作為 [事件中樞名稱]，如下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="58534-155">Be sure to enter **exit** for the **Event Hub Name** as shown in the following screenshot:</span></span>

    ![ExitStream 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="58534-157">您現在已定義兩個輸入資料流：</span><span class="sxs-lookup"><span data-stu-id="58534-157">Now you have defined two input streams:</span></span>

    ![進入和離開的輸入資料流](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="58534-159">接下來，為包含車輛登記資料的 Blob 檔案新增參考資料輸入。</span><span class="sxs-lookup"><span data-stu-id="58534-159">Next, add reference data input for the blob file that contains car registration data.</span></span>

13. <span data-ttu-id="58534-160">以滑鼠右鍵按一下專案中的 [輸入] 節點，然後依照您在資料流輸入中所做的相同步驟操作。</span><span class="sxs-lookup"><span data-stu-id="58534-160">Right-click the **Inputs** node in the project, and then follow the same steps as you did for the stream inputs.</span></span> <span data-ttu-id="58534-161">在 [輸入別名] 中，輸入 **Registration**，然後在 [來源類型] 中，選取 [參考資料]。</span><span class="sxs-lookup"><span data-stu-id="58534-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![[註冊] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="58534-163">在 [儲存體帳戶] 中，選取 [tolldata] 選項。</span><span class="sxs-lookup"><span data-stu-id="58534-163">In **Storage Account**, select the **tolldata** option.</span></span> <span data-ttu-id="58534-164">在 [容器] 中，選取 [tolldata]，然後在 [路徑模式] 中，輸入 **registration.json**。</span><span class="sxs-lookup"><span data-stu-id="58534-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="58534-165">這個檔案名稱會區分大小寫，且應該是小寫。</span><span class="sxs-lookup"><span data-stu-id="58534-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="58534-166">若要完成精靈，請按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="58534-166">To finish the wizard, click **Save**.</span></span>

<span data-ttu-id="58534-167">現在，所有輸入都已定義。</span><span class="sxs-lookup"><span data-stu-id="58534-167">Now all the inputs are defined.</span></span>

## <a name="define-the-output"></a><span data-ttu-id="58534-168">定義輸出</span><span class="sxs-lookup"><span data-stu-id="58534-168">Define the output</span></span>
1.  <span data-ttu-id="58534-169">在 [方案總管] 中，展開 [輸入] 節點，然後按兩下 [Output.json]。</span><span class="sxs-lookup"><span data-stu-id="58534-169">In **Solution Explorer**, expand the **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="58534-170">在 [輸出別名] 中，輸入 **output**。</span><span class="sxs-lookup"><span data-stu-id="58534-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="58534-171">在 [接收] 中，選取 [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="58534-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="58534-172">在 [資料庫] 中，選取 [TollDataDB]。</span><span class="sxs-lookup"><span data-stu-id="58534-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="58534-173">在 [使用者名稱] 中，輸入 **tolladmin**。</span><span class="sxs-lookup"><span data-stu-id="58534-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="58534-174">在 [密碼] 中，輸入 **123toll!**。</span><span class="sxs-lookup"><span data-stu-id="58534-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="58534-175">在 [資料表] 中，輸入 **TollDataRefJoin**。</span><span class="sxs-lookup"><span data-stu-id="58534-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="58534-176">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="58534-176">Click **Save**.</span></span>

    ![[輸出] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="58534-178">建立串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="58534-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="58534-179">本教學課程會嘗試回答幾個與付費資料相關的商務問題。</span><span class="sxs-lookup"><span data-stu-id="58534-179">This tutorial attempts to answer several business questions that are related to toll data.</span></span> <span data-ttu-id="58534-180">也會建構串流分析查詢，可以在串流分析中用來提供相關的答案。</span><span class="sxs-lookup"><span data-stu-id="58534-180">It also constructs Stream Analytics queries that can be used in Stream Analytics to provide relevant answers.</span></span>
<span data-ttu-id="58534-181">在開始第一個串流分析作業之前，讓我們先來探索一個簡單的情節和查詢語法。</span><span class="sxs-lookup"><span data-stu-id="58534-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and the query syntax.</span></span>

### <a name="introduction-to-the-stream-analytics-query-language"></a><span data-ttu-id="58534-182">串流分析查詢語言簡介</span><span class="sxs-lookup"><span data-stu-id="58534-182">Introduction to the Stream Analytics query language</span></span>
<span data-ttu-id="58534-183">假設您需要計算進入某個收費亭的車輛數目。</span><span class="sxs-lookup"><span data-stu-id="58534-183">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="58534-184">因為此範例是連續的事件資料流，您必須定義一段時間。</span><span class="sxs-lookup"><span data-stu-id="58534-184">Because this example is a continuous stream of events, you have to define a period of time.</span></span> <span data-ttu-id="58534-185">將問題修改為「每三分鐘有多少車輛進入收費亭？」</span><span class="sxs-lookup"><span data-stu-id="58534-185">Modify the question to be “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="58534-186">這樣的資料計數方式通常稱為輪轉計數。</span><span class="sxs-lookup"><span data-stu-id="58534-186">This way to count data is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="58534-187">查看可回答這個問題的串流分析查詢：</span><span class="sxs-lookup"><span data-stu-id="58534-187">Look at the Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="58534-188">串流分析會使用類似 SQL 的查詢語言，並新增幾個擴充來指定和時間有關的查詢層面。</span><span class="sxs-lookup"><span data-stu-id="58534-188">Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="58534-189">如需詳細資訊，請參閱 MSDN 中的[時間管理](https://msdn.microsoft.com/library/azure/mt582045.aspx)，以及查詢中所用的[時間範圍](https://msdn.microsoft.com/library/azure/dn835019.aspx)建構。</span><span class="sxs-lookup"><span data-stu-id="58534-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="58534-190">既然您已經撰寫第一個串流分析查詢，現在就開始測試。</span><span class="sxs-lookup"><span data-stu-id="58534-190">Now that you have written your first Stream Analytics query, it's time to test it.</span></span> <span data-ttu-id="58534-191">使用下列路徑中位於 TollApp 資料夾的範例資料檔案：</span><span class="sxs-lookup"><span data-stu-id="58534-191">Use the sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="58534-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="58534-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="58534-193">這個資料夾包含下列檔案：</span><span class="sxs-lookup"><span data-stu-id="58534-193">This folder contains the following files:</span></span>
*   <span data-ttu-id="58534-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="58534-194">Entry.json</span></span>
*   <span data-ttu-id="58534-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="58534-195">Exit.json</span></span>
*   <span data-ttu-id="58534-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="58534-196">Registration.json</span></span>

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="58534-197">計算進入收費亭的車輛數目</span><span class="sxs-lookup"><span data-stu-id="58534-197">Count the number of vehicles entering a toll booth</span></span>
<span data-ttu-id="58534-198">在專案中，按兩下 [Script.asaql]，就會在 [查詢編輯器] 中開啟指令碼。</span><span class="sxs-lookup"><span data-stu-id="58534-198">In the project, double-click **Script.asaql** to open the script in the **Query Editor**.</span></span> <span data-ttu-id="58534-199">將上一節中的指令碼，複製並貼到編輯器中。</span><span class="sxs-lookup"><span data-stu-id="58534-199">Copy and paste the script in the previous section into the editor.</span></span> <span data-ttu-id="58534-200">查詢編輯器支援 IntelliSense、語法著色和錯誤標記。</span><span class="sxs-lookup"><span data-stu-id="58534-200">The Query Editor supports IntelliSense, syntax coloring, and the error marker.</span></span>

![查詢編輯器](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="58534-202">在本機測試串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="58534-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="58534-203">若要編譯查詢來檢查語法是否錯誤，請以滑鼠右鍵按一下專案，然後選取 [建置]。</span><span class="sxs-lookup"><span data-stu-id="58534-203">To compile the query to see if there is a syntax error, right-click the project and select **Build**.</span></span> 

2. <span data-ttu-id="58534-204">若要利用範例資料來驗證這個查詢，您可以使用本機範例資料。</span><span class="sxs-lookup"><span data-stu-id="58534-204">To validate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="58534-205">以滑鼠右鍵按一下輸入，然後選取 [新增本機輸入]。</span><span class="sxs-lookup"><span data-stu-id="58534-205">Right-click the input, and select **Add local input**.</span></span>

    ![新增本機輸入](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="58534-207">在快顯視窗中，從本機路徑選取範例資料。</span><span class="sxs-lookup"><span data-stu-id="58534-207">In the pop-up window, select the sample data from your local path.</span></span> <span data-ttu-id="58534-208">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="58534-208">Click **Save**.</span></span>

    ![[新增本機輸入] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="58534-210">名為 **local_EntryStream.json** 的檔案會自動新增至您的輸入資料夾。</span><span class="sxs-lookup"><span data-stu-id="58534-210">A file named **local_EntryStream.json** is automatically added to your inputs folder.</span></span>

    ![新增至輸入資料夾的檔案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="58534-212">在 [查詢編輯器] 中，按一下 [在本機執行]。</span><span class="sxs-lookup"><span data-stu-id="58534-212">In the **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="58534-213">或者，您可以按 F5 鍵。</span><span class="sxs-lookup"><span data-stu-id="58534-213">Or you can press the F5 key.</span></span>

    ![在本機執行](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![本機執行輸出](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="58534-216">按下任何鍵，可在 Visual Studio 中的 [ASA 本機執行結果] 視窗中檢視輸出。</span><span class="sxs-lookup"><span data-stu-id="58534-216">Press any key to view the output in the **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![[ASA 本機執行結果] 視窗](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="58534-218">按一下 [開啟結果資料夾]，可同時以 CSV 和 JSON 格式來檢查輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="58534-218">Click **Open Result Folder** to check the output files both in CSV and JSON format.</span></span>

    ![開啟結果資料夾輸出](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a><span data-ttu-id="58534-220">取樣輸入資料</span><span class="sxs-lookup"><span data-stu-id="58534-220">Sample the input data</span></span>
<span data-ttu-id="58534-221">您也可以將輸入來源的輸入資料取樣到本機檔案。</span><span class="sxs-lookup"><span data-stu-id="58534-221">You can also sample input data from input sources to a local file.</span></span> 
1. <span data-ttu-id="58534-222">以滑鼠右鍵按一下輸入設定檔，然後選取 [範例資料]。</span><span class="sxs-lookup"><span data-stu-id="58534-222">Right-click the input config file, and select **Sample Data**.</span></span> 

   ![範例資料](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="58534-224">目前只能取樣事件中樞或 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="58534-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="58534-225">不支援其他輸入來源。</span><span class="sxs-lookup"><span data-stu-id="58534-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="58534-226">在快顯視窗中，輸入用來儲存範例資料的本機路徑。</span><span class="sxs-lookup"><span data-stu-id="58534-226">In the pop-up window, enter the local path used to save the sample data.</span></span> <span data-ttu-id="58534-227">按一下 [取樣]。</span><span class="sxs-lookup"><span data-stu-id="58534-227">Click **Sample**.</span></span>

    ![[範例資料] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="58534-229">您可以在 [輸出] 視窗中查看進度。</span><span class="sxs-lookup"><span data-stu-id="58534-229">You can see the progress in the **Output** window.</span></span> 

    ![[輸出] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a><span data-ttu-id="58534-231">將串流分析查詢提交至 Azure</span><span class="sxs-lookup"><span data-stu-id="58534-231">Submit a Stream Analytics query to Azure</span></span>
1. <span data-ttu-id="58534-232">在 [查詢編輯器] 中，按一下指令碼編輯器中的 [提交至 Azure]。</span><span class="sxs-lookup"><span data-stu-id="58534-232">In the **Query Editor**, click **Submit To Azure** in the script editor.</span></span>

    ![提交至 Azure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="58534-234">選取 [建立新的 Azure 串流分析作業]。</span><span class="sxs-lookup"><span data-stu-id="58534-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="58534-235">輸入 [作業名稱]，然後選取正確的 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="58534-235">Enter the **Job Name**, and select the correct **Subscription**.</span></span> <span data-ttu-id="58534-236">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="58534-236">Click **Submit**.</span></span>

    ![[提交作業] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="58534-238">啟動作業</span><span class="sxs-lookup"><span data-stu-id="58534-238">Start a job</span></span>
<span data-ttu-id="58534-239">現在已建立作業，作業檢視會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="58534-239">Now that your job is created, the job view is automatically opened.</span></span> 
1. <span data-ttu-id="58534-240">若要啟動作業，請按一下**綠色箭頭**按鈕。</span><span class="sxs-lookup"><span data-stu-id="58534-240">To start the job, click the **green arrow** button.</span></span>

    ![啟動作業](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="58534-242">選取預設設定，然後按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="58534-242">Select the default setting, and click **Start**.</span></span>
 
    ![[啟動作業] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="58534-244">作業 [狀態] 會變為 [執行中]，也出現 [輸入事件] 和 [輸出事件]。</span><span class="sxs-lookup"><span data-stu-id="58534-244">The job **Status** changes to **Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![作業摘要中的 [執行中] 狀態](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a><span data-ttu-id="58534-246">在 Visual Studio 中查看結果</span><span class="sxs-lookup"><span data-stu-id="58534-246">Check the results in Visual Studio</span></span>
1. <span data-ttu-id="58534-247">在 Visual Studio 中，開啟 [伺服器總管]，然後以滑鼠右鍵按一下 [TollDataRefJoin] 資料表。</span><span class="sxs-lookup"><span data-stu-id="58534-247">In Visual Studio, open **Server Explorer** and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="58534-248">選取 [顯示資料表資料] 可查看作業的輸出。</span><span class="sxs-lookup"><span data-stu-id="58534-248">Select **Show Table Data** to see the output of your job.</span></span>
   
    ![在伺服器總管中選取 [顯示資料表資料]](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a><span data-ttu-id="58534-250">檢視作業計量</span><span class="sxs-lookup"><span data-stu-id="58534-250">View the job metrics</span></span>
<span data-ttu-id="58534-251">您可以在 [作業計量] 找到一些基本的作業統計資料。</span><span class="sxs-lookup"><span data-stu-id="58534-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![[作業計量] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a><span data-ttu-id="58534-253">在伺服器總管中列出作業</span><span class="sxs-lookup"><span data-stu-id="58534-253">List the job in Server Explorer</span></span>
<span data-ttu-id="58534-254">在 [伺服器總管] 中，按一下 [串流分析作業]，然後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="58534-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="58534-255">作業會出現在 [串流分析作業] 下。</span><span class="sxs-lookup"><span data-stu-id="58534-255">The job appears under **Stream Analytics jobs**.</span></span>

![伺服器總管中列出的串流分析作業](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a><span data-ttu-id="58534-257">開啟作業檢視</span><span class="sxs-lookup"><span data-stu-id="58534-257">Open the job view</span></span>
<span data-ttu-id="58534-258">若要開啟作業檢視，請展開作業節點，然後按兩下 [作業檢視] 節點。</span><span class="sxs-lookup"><span data-stu-id="58534-258">To open the job view, expand your job node and double-click the **Job View** node.</span></span>

![[作業檢視] 節點](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="58534-260">將現有作業匯出到專案</span><span class="sxs-lookup"><span data-stu-id="58534-260">Export an existing job to a project</span></span>
<span data-ttu-id="58534-261">有兩種方式可以將現有的作業匯出到專案。</span><span class="sxs-lookup"><span data-stu-id="58534-261">There are two ways you can export an existing job to a project.</span></span>

<span data-ttu-id="58534-262">在 [伺服器總管] 中，以滑鼠右鍵按一下 [串流分析作業] 節點中的作業節點，然後選取 [匯出至新的串流分析專案]。</span><span class="sxs-lookup"><span data-stu-id="58534-262">In **Server Explorer**, right-click the job node in the **Stream Analytics Jobs** node and select **Export to New Stream Analytics Project**.</span></span>

![匯出至新的串流分析專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="58534-264">[方案總管] 中會產生專案。</span><span class="sxs-lookup"><span data-stu-id="58534-264">The project is generated in **Solution Explorer**.</span></span>

![[方案總管] 中產生的專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="58534-266">您也可以使用作業檢視並按一下 [產生專案]。</span><span class="sxs-lookup"><span data-stu-id="58534-266">You also can use the job view, and click **Generate Project**.</span></span>

![產生專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="58534-268">已知問題與限制</span><span class="sxs-lookup"><span data-stu-id="58534-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="58534-269">不支援 Power BI 輸出和 Azure Data Lake Store 輸出。</span><span class="sxs-lookup"><span data-stu-id="58534-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="58534-270">編輯器不支援新增或變更 JavaScript 使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="58534-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58534-271">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58534-271">Next steps</span></span>
* [<span data-ttu-id="58534-272">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="58534-272">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="58534-273">開始使用 Azure 串流分析</span><span class="sxs-lookup"><span data-stu-id="58534-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="58534-274">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="58534-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="58534-275">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="58534-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="58534-276">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="58534-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
