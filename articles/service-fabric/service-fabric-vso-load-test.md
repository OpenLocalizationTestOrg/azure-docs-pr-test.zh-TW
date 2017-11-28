---
title: "使用 Visual Studio Team Services 對應用程式執行負載測試 | Microsoft Docs"
description: "了解如何使用 Visual Studio Team Services 對您的 Azure Service Fabric 應用程式執行壓力測試。"
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: e8e270ce865d4da3ee219958b308db2c1c89b11b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a><span data-ttu-id="d98ab-103">使用 Visual Studio Team Services 對您的應用程式執行負載測試</span><span class="sxs-lookup"><span data-stu-id="d98ab-103">Load test your application by using Visual Studio Team Services</span></span>
<span data-ttu-id="d98ab-104">本文章說明如何使用 Microsoft Visual Studio 負載測試功能對應用程式進行壓力測試。</span><span class="sxs-lookup"><span data-stu-id="d98ab-104">This article shows how to use Microsoft Visual Studio load test features to stress test an application.</span></span> <span data-ttu-id="d98ab-105">它會使用 Azure Service Fabric 具狀態服務後端和無狀態服務 Web 前端。</span><span class="sxs-lookup"><span data-stu-id="d98ab-105">It uses an Azure Service Fabric stateful service back end and a stateless service web front end.</span></span> <span data-ttu-id="d98ab-106">以下使用的範例應用程式是飛機位置模擬器。</span><span class="sxs-lookup"><span data-stu-id="d98ab-106">The example application used here is an airplane location simulator.</span></span> <span data-ttu-id="d98ab-107">您提供飛機識別碼、起飛時間和目的地。</span><span class="sxs-lookup"><span data-stu-id="d98ab-107">You provide an airplane ID, departure time, and destination.</span></span> <span data-ttu-id="d98ab-108">應用程式的後端會處理要求，而前端會顯示地圖上與準則相符的飛機。</span><span class="sxs-lookup"><span data-stu-id="d98ab-108">The application’s back end processes the requests, and the front end displays on a map the airplane that matches the criteria.</span></span>

<span data-ttu-id="d98ab-109">下圖說明您即將測試的 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d98ab-109">The following diagram illustrates the Service Fabric application that you'll be testing.</span></span>

![範例飛機位置應用程式的圖表][0]

## <a name="prerequisites"></a><span data-ttu-id="d98ab-111">先決條件</span><span class="sxs-lookup"><span data-stu-id="d98ab-111">Prerequisites</span></span>
<span data-ttu-id="d98ab-112">開始之前，您需要執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d98ab-112">Before getting started, you need to do the following:</span></span>

* <span data-ttu-id="d98ab-113">取得 Visual Studio Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d98ab-113">Get a Visual Studio Team Services account.</span></span> <span data-ttu-id="d98ab-114">您可以在 [Visual Studio Team Services](https://www.visualstudio.com)取得一個免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="d98ab-114">You can get one for free at [Visual Studio Team Services](https://www.visualstudio.com).</span></span>
* <span data-ttu-id="d98ab-115">取得並安裝 Visual Studio 2013 或 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="d98ab-115">Get and install Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="d98ab-116">本文使用 Visual Studio 2015 Enterprise 版本，但是 Visual Studio 2013 和其他版本應該也同樣可以運作。</span><span class="sxs-lookup"><span data-stu-id="d98ab-116">This article uses Visual Studio 2015 Enterprise edition, but Visual Studio 2013 and other editions should work similarly.</span></span>
* <span data-ttu-id="d98ab-117">將您的應用程式部署至預備環境。</span><span class="sxs-lookup"><span data-stu-id="d98ab-117">Deploy your application to a staging environment.</span></span> <span data-ttu-id="d98ab-118">如需相關詳細資訊，請參閱 [如何使用 Visual Studio 將應用程式部署至遠端叢集](service-fabric-publish-app-remote-cluster.md) 。</span><span class="sxs-lookup"><span data-stu-id="d98ab-118">See [How to deploy applications to a remote cluster using Visual Studio](service-fabric-publish-app-remote-cluster.md) for information about this.</span></span>
* <span data-ttu-id="d98ab-119">了解您的應用程式的使用模式。</span><span class="sxs-lookup"><span data-stu-id="d98ab-119">Understand your application’s usage pattern.</span></span> <span data-ttu-id="d98ab-120">這項資訊是用來模擬負載模式。</span><span class="sxs-lookup"><span data-stu-id="d98ab-120">This information is used to simulate the load pattern.</span></span>
* <span data-ttu-id="d98ab-121">了解您的負載測試的目標。</span><span class="sxs-lookup"><span data-stu-id="d98ab-121">Understand the goal for your load testing.</span></span> <span data-ttu-id="d98ab-122">這可協助您解譯和分析負載測試結果。</span><span class="sxs-lookup"><span data-stu-id="d98ab-122">This helps you interpret and analyze the load test results.</span></span>

## <a name="create-and-run-the-web-performance-and-load-test-project"></a><span data-ttu-id="d98ab-123">建立及執行 Web 效能和負載測試專案</span><span class="sxs-lookup"><span data-stu-id="d98ab-123">Create and run the Web Performance and Load Test project</span></span>
### <a name="create-a-web-performance-and-load-test-project"></a><span data-ttu-id="d98ab-124">建立 Web 效能和負載測試專案</span><span class="sxs-lookup"><span data-stu-id="d98ab-124">Create a Web Performance and Load Test project</span></span>
1. <span data-ttu-id="d98ab-125">開啟 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="d98ab-125">Open Visual Studio 2015.</span></span> <span data-ttu-id="d98ab-126">在功能表列上選擇 [檔案]  >  [新增]  >  [專案] 以開啟 [新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d98ab-126">Choose **File** > **New** > **Project** on the menu bar to open the **New Project** dialog box.</span></span>
2. <span data-ttu-id="d98ab-127">展開 [Visual C#] 節點，然後選擇 [測試]  >  [Web 效能和負載測試專案]。</span><span class="sxs-lookup"><span data-stu-id="d98ab-127">Expand the **Visual C#** node and choose **Test** > **Web Performance and Load Test project**.</span></span> <span data-ttu-id="d98ab-128">給予專案名稱，然後選擇 [確定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d98ab-128">Give the project a name and then choose the **OK** button.</span></span>

    ![[新增專案] 對話方塊的螢幕擷取畫面][1]

    <span data-ttu-id="d98ab-130">您應該會在 [方案總管] 中看到新的 Web 效能和負載測試專案。</span><span class="sxs-lookup"><span data-stu-id="d98ab-130">You should see a new Web Performance and Load Test project in Solution Explorer.</span></span>

    ![顯示新專案的 [方案總管] 螢幕擷取畫面][2]

### <a name="record-a-web-performance-test"></a><span data-ttu-id="d98ab-132">記錄 Web 效能測試</span><span class="sxs-lookup"><span data-stu-id="d98ab-132">Record a web performance test</span></span>
1. <span data-ttu-id="d98ab-133">開啟 .webtest 專案。</span><span class="sxs-lookup"><span data-stu-id="d98ab-133">Open the .webtest project.</span></span>
2. <span data-ttu-id="d98ab-134">選擇 [加入錄製]  圖示以在瀏覽器中啟動錄製工作階段。</span><span class="sxs-lookup"><span data-stu-id="d98ab-134">Choose the **Add Recording** icon to start a recording session in your browser.</span></span>

    ![瀏覽器中 [加入錄製] 圖示的螢幕擷取畫面][3]

    ![瀏覽器中 [錄製] 按鈕的螢幕擷取畫面][4]
3. <span data-ttu-id="d98ab-137">瀏覽至 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d98ab-137">Browse to the Service Fabric application.</span></span> <span data-ttu-id="d98ab-138">[錄製] 面板應該會顯示 Web 要求。</span><span class="sxs-lookup"><span data-stu-id="d98ab-138">The recording panel should show the web requests.</span></span>

    ![錄製面板中 Web 要求的螢幕擷取畫面][5]
4. <span data-ttu-id="d98ab-140">執行您預期使用者執行的一系列動作。</span><span class="sxs-lookup"><span data-stu-id="d98ab-140">Perform a sequence of actions that you expect the users to perform.</span></span> <span data-ttu-id="d98ab-141">這些動作會當做產生負載的模式。</span><span class="sxs-lookup"><span data-stu-id="d98ab-141">These actions are used as a pattern to generate the load.</span></span>
5. <span data-ttu-id="d98ab-142">完成時，選擇 [停止]  按鈕以停止錄製。</span><span class="sxs-lookup"><span data-stu-id="d98ab-142">When you're done, choose the **Stop** button to stop recording.</span></span>

    ![[停止] 按鈕的螢幕擷取畫面][6]

    <span data-ttu-id="d98ab-144">Visual Studio 中的 .webtest 專案應該已擷取一系列的要求。</span><span class="sxs-lookup"><span data-stu-id="d98ab-144">The .webtest project in Visual Studio should have captured a series of requests.</span></span> <span data-ttu-id="d98ab-145">會自動取代動態參數。</span><span class="sxs-lookup"><span data-stu-id="d98ab-145">Dynamic parameters are replaced automatically.</span></span> <span data-ttu-id="d98ab-146">此時，您可以刪除不屬於您的測試案例的任何額外、重複相依性要求。</span><span class="sxs-lookup"><span data-stu-id="d98ab-146">At this point, you can delete any extra, repeated dependency requests that are not part of your test scenario.</span></span>
6. <span data-ttu-id="d98ab-147">儲存專案，然後選擇 [執行測試]  命令以在本機執行 Web 效能測試，並且確認一切運作正常。</span><span class="sxs-lookup"><span data-stu-id="d98ab-147">Save the project and then choose the **Run Test** command to run the web performance test locally and make sure everything works correctly.</span></span>

    ![[執行測試] 命令的螢幕擷取畫面][7]

### <a name="parameterize-the-web-performance-test"></a><span data-ttu-id="d98ab-149">參數化 Web 效能測試</span><span class="sxs-lookup"><span data-stu-id="d98ab-149">Parameterize the web performance test</span></span>
<span data-ttu-id="d98ab-150">您可以將 Web 效能測試轉換成 Web 效能測試程式碼，然後編輯程式碼，以參數化 Web 效能測試。</span><span class="sxs-lookup"><span data-stu-id="d98ab-150">You can parameterize the web performance test by converting it to a coded web performance test and then editing the code.</span></span> <span data-ttu-id="d98ab-151">或者，您可以將 Web 效能測試繫結至資料清單，以便測試逐一查看資料。</span><span class="sxs-lookup"><span data-stu-id="d98ab-151">As an alternative, you can bind the web performance test to a data list so that the test iterates through the data.</span></span> <span data-ttu-id="d98ab-152">請參閱 [產生和執行 Web 效能測試程式碼](https://msdn.microsoft.com/library/ms182552.aspx) 以取得如何將 Web 效能測試轉換成程式碼測試的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d98ab-152">See [Generate and run a coded web performance test](https://msdn.microsoft.com/library/ms182552.aspx) for details about how to convert the web performance test to a coded test.</span></span> <span data-ttu-id="d98ab-153">請參閱 [將資料來源新增至 Web 效能測試](https://msdn.microsoft.com/library/ms243142.aspx) 以取得如何將資料繫結至 Web 效能測試的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d98ab-153">See [Add a data source to a web performance test](https://msdn.microsoft.com/library/ms243142.aspx) for information about how to bind data to a web performance test.</span></span>

<span data-ttu-id="d98ab-154">對於此範例，我們會將 Web 效能測試轉換成程式碼測試，您就可以使用產生的 GUID 取代飛機識別碼，並且加入更多要求以將航班傳送至不同位置。</span><span class="sxs-lookup"><span data-stu-id="d98ab-154">For this example, we'll convert the web performance test to a coded test so you can replace the airplane ID with a generated GUID and add more requests to send flights to different locations.</span></span>

### <a name="create-a-load-test-project"></a><span data-ttu-id="d98ab-155">建立負載測試專案</span><span class="sxs-lookup"><span data-stu-id="d98ab-155">Create a load test project</span></span>
<span data-ttu-id="d98ab-156">負載測試專案是由 Web 效能測試和單位測試所描述的一或多個案例，以及其他指定的負載測試設定組成。</span><span class="sxs-lookup"><span data-stu-id="d98ab-156">A load test project is composed of one or more scenarios described by the web performance test and unit test, along with additional specified load test settings.</span></span> <span data-ttu-id="d98ab-157">下列步驟說明如何建立負載測試專案：</span><span class="sxs-lookup"><span data-stu-id="d98ab-157">The following steps show how to create a load test project:</span></span>

1. <span data-ttu-id="d98ab-158">在您的 Web 效能和負載測試專案的捷徑功能表上選擇 [新增]  > 取得一個免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="d98ab-158">On the shortcut menu of your Web Performance and Load Test project, choose **Add** > **Load Test**.</span></span> <span data-ttu-id="d98ab-159">在 [負載測試] 精靈中，選擇 [下一步] 按鈕以設定測試設定。</span><span class="sxs-lookup"><span data-stu-id="d98ab-159">In the **Load Test** wizard, choose the **Next** button to configure the test settings.</span></span>
2. <span data-ttu-id="d98ab-160">在 [負載模式]  區段中，選擇要常數使用者負載或逐步執行負載，開頭為少數使用者並且隨著時間經過增加使用者。</span><span class="sxs-lookup"><span data-stu-id="d98ab-160">In the **Load Pattern** section, choose whether you want a constant user load or a step load, which starts with a few users and increases the users over time.</span></span>

    <span data-ttu-id="d98ab-161">如果您對於使用者負載量有良好的評估並且想要查看目前系統的執行方式，請選擇 [常數負載] 。</span><span class="sxs-lookup"><span data-stu-id="d98ab-161">If you have a good estimate of the amount of user load and want to see how the current system performs, choose **Constant Load**.</span></span> <span data-ttu-id="d98ab-162">如果您的目標是了解系統在不同負載之下的執行是否一致，請選擇 [逐步執行負載] 。</span><span class="sxs-lookup"><span data-stu-id="d98ab-162">If your goal is to learn whether the system performs consistently under various loads, choose **Step Load**.</span></span>
3. <span data-ttu-id="d98ab-163">在 [測試混合] 區段中，選擇 [新增] 按鈕，然後選取您要包含在負載測試的測試。</span><span class="sxs-lookup"><span data-stu-id="d98ab-163">In the **Test Mix** section, choose the **Add** button and then select the test that you want to include in the load test.</span></span> <span data-ttu-id="d98ab-164">您可以使用 [散發]  資料行指定每一項測試的測試執行總計百分比。</span><span class="sxs-lookup"><span data-stu-id="d98ab-164">You can use the **Distribution** column to specify the percentage of total tests run for each test.</span></span>
4. <span data-ttu-id="d98ab-165">在 [回合設定]  區段中，指定負載測試持續期間。</span><span class="sxs-lookup"><span data-stu-id="d98ab-165">In the **Run Settings** section, specify the load test duration.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d98ab-166">[測試反覆項目] 選項只有當您使用 Visual Studio 在本機執行負載測試時才可以使用。</span><span class="sxs-lookup"><span data-stu-id="d98ab-166">The **Test Iterations** option is available only when you run a load test locally using Visual Studio.</span></span>
   >
   >
5. <span data-ttu-id="d98ab-167">在 [回合設定] 的 [位置] 區段中，指定產生負載測試要求的位置。</span><span class="sxs-lookup"><span data-stu-id="d98ab-167">In the **Location** section of **Run Settings**, specify the location where load test requests are generated.</span></span> <span data-ttu-id="d98ab-168">此精靈可能會提示您登入您的 Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d98ab-168">The wizard may prompt you to log in to your Team Services account.</span></span> <span data-ttu-id="d98ab-169">登入，然後選擇一個地理位置。</span><span class="sxs-lookup"><span data-stu-id="d98ab-169">Log in and then choose a geographic location.</span></span> <span data-ttu-id="d98ab-170">完成時，選擇 [完成]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d98ab-170">When you're done, choose the **Finish** button.</span></span>
6. <span data-ttu-id="d98ab-171">建立負載測試之後，開啟 取得一個免費帳戶。loadtest 專案並選擇目前回合設定，例如 [回合設定]  > **1 [Active]**取得一個免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="d98ab-171">After the load test is created, open the .loadtest project and choose the current run setting, such as **Run Settings** > **Run Settings1 [Active]**.</span></span> <span data-ttu-id="d98ab-172">這會在 [屬性]  視窗中開啟回合設定。</span><span class="sxs-lookup"><span data-stu-id="d98ab-172">This opens the run settings in the **Properties** window.</span></span>
7. <span data-ttu-id="d98ab-173">在 [回合設定] 屬性視窗中的 [結果] 區段中，[計時詳細資料儲存區] 設定的預設值應該為 [無]。</span><span class="sxs-lookup"><span data-stu-id="d98ab-173">In the **Results** section of the **Run Settings** properties window, the **Timing Details Storage** setting should have **None** as its default value.</span></span> <span data-ttu-id="d98ab-174">將此值變更為 [所有個別細節]  以取得更多有關負載測試結果的資訊。</span><span class="sxs-lookup"><span data-stu-id="d98ab-174">Change this value to **All Individual Details** to get more information on the load test results.</span></span> <span data-ttu-id="d98ab-175">如需如何連接至 Visual Studio Team Services 及執行負載測試的詳細資訊，請參閱 [負載測試](https://www.visualstudio.com/load-testing.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="d98ab-175">See [Load Testing](https://www.visualstudio.com/load-testing.aspx) for more information on how to connect to Visual Studio Team Services and run a load test.</span></span>

### <a name="run-the-load-test-by-using-visual-studio-team-services"></a><span data-ttu-id="d98ab-176">使用 Visual Studio Team Services 執行負載測試</span><span class="sxs-lookup"><span data-stu-id="d98ab-176">Run the load test by using Visual Studio Team Services</span></span>
<span data-ttu-id="d98ab-177">選擇 [執行負載測試]  命令來啟動測試回合。</span><span class="sxs-lookup"><span data-stu-id="d98ab-177">Choose the **Run Load Test** command to start the test run.</span></span>

![[執行負載測試] 命令的螢幕擷取畫面][8]

## <a name="view-and-analyze-the-load-test-results"></a><span data-ttu-id="d98ab-179">檢視及分析負載測試結果</span><span class="sxs-lookup"><span data-stu-id="d98ab-179">View and analyze the load test results</span></span>
<span data-ttu-id="d98ab-180">隨著負載測試進行，效能資訊會圖表化。</span><span class="sxs-lookup"><span data-stu-id="d98ab-180">As the load test progresses, the performance information is graphed.</span></span> <span data-ttu-id="d98ab-181">您應該會看到類似下面的圖形。</span><span class="sxs-lookup"><span data-stu-id="d98ab-181">You should see something similar to the following graph.</span></span>

![負載測試結果的效能圖表的螢幕擷取畫面][9]

1. <span data-ttu-id="d98ab-183">選擇頁面頂端附近的 [下載報告]  連結。</span><span class="sxs-lookup"><span data-stu-id="d98ab-183">Choose the **Download report** link near the top of the page.</span></span> <span data-ttu-id="d98ab-184">下載報告之後，選擇 [檢視報告]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d98ab-184">After the report is downloaded, choose the **View report** button.</span></span>

    <span data-ttu-id="d98ab-185">在 [圖形]  索引標籤上，您可以看到各種效能計數器的圖形。</span><span class="sxs-lookup"><span data-stu-id="d98ab-185">On the **Graph** tab you can see graphs for various performance counters.</span></span> <span data-ttu-id="d98ab-186">在 [摘要]  索引標籤上，會顯示整體測試結果。</span><span class="sxs-lookup"><span data-stu-id="d98ab-186">On the **Summary** tab, the overall test results appear.</span></span> <span data-ttu-id="d98ab-187">[資料表]  索引標籤會顯示成功和失敗負載測試的總數。</span><span class="sxs-lookup"><span data-stu-id="d98ab-187">The **Tables** tab shows the total number of passed and failed load tests.</span></span>
2. <span data-ttu-id="d98ab-188">在 [測試]  >  [失敗] 和 [錯誤]  >  [計數] 資料行上選擇數字連結，以查看錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d98ab-188">Choose the number links on the **Test** > **Failed** and the **Errors** > **Count** columns to see error details.</span></span>

    <span data-ttu-id="d98ab-189">[詳細資料]  索引標籤會顯示失敗要求的虛擬使用者和測試案例資訊。</span><span class="sxs-lookup"><span data-stu-id="d98ab-189">The **Detail** tab shows virtual user and test scenario information for failed requests.</span></span> <span data-ttu-id="d98ab-190">如果負載測試包含多個案例，此資料相當有用。</span><span class="sxs-lookup"><span data-stu-id="d98ab-190">This data can be useful if the load test includes multiple scenarios.</span></span>

<span data-ttu-id="d98ab-191">請參閱 [在負載測試分析器的圖形檢視中分析負載測試結果](https://www.visualstudio.com/load-testing.aspx) 以取得有關檢視負載測試結果的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d98ab-191">See [Analyzing Load Test Results in the Graphs View of the Load Test Analyzer](https://www.visualstudio.com/load-testing.aspx) for more information on viewing load test results.</span></span>

## <a name="automate-your-load-test"></a><span data-ttu-id="d98ab-192">自動化您的負載測試</span><span class="sxs-lookup"><span data-stu-id="d98ab-192">Automate your load test</span></span>
<span data-ttu-id="d98ab-193">Visual Studio Team Services 負載測試會提供 API 協助您管理負載測試，並分析 Team Services 帳戶中的結果。</span><span class="sxs-lookup"><span data-stu-id="d98ab-193">Visual Studio Team Services Load Test provides APIs to help you manage load tests and analyze results in a Team Services account.</span></span> <span data-ttu-id="d98ab-194">如需詳細資訊，請參閱 [雲端負載測試 Rest API](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="d98ab-194">See [Cloud Load Testing Rest APIs](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d98ab-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d98ab-195">Next steps</span></span>
* [<span data-ttu-id="d98ab-196">監視和診斷本機開發設定中的服務</span><span class="sxs-lookup"><span data-stu-id="d98ab-196">Monitoring and diagnosing services in a local machine development setup</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
