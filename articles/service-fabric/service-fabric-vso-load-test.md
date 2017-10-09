---
title: "aaaLoad 測試您的應用程式使用 Visual Studio Team Services |Microsoft 文件"
description: "了解 toostress 如何使用 Visual Studio Team Services 測試 Azure Service Fabric 應用程式。"
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
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a><span data-ttu-id="f0522-103">使用 Visual Studio Team Services 對您的應用程式執行負載測試</span><span class="sxs-lookup"><span data-stu-id="f0522-103">Load test your application by using Visual Studio Team Services</span></span>
<span data-ttu-id="f0522-104">本文將說明如何 toouse Microsoft Visual Studio 負載測試功能 toostress 測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0522-104">This article shows how toouse Microsoft Visual Studio load test features toostress test an application.</span></span> <span data-ttu-id="f0522-105">它會使用 Azure Service Fabric 具狀態服務後端和無狀態服務 Web 前端。</span><span class="sxs-lookup"><span data-stu-id="f0522-105">It uses an Azure Service Fabric stateful service back end and a stateless service web front end.</span></span> <span data-ttu-id="f0522-106">hello 這裡使用的範例應用程式是飛機位置模擬器。</span><span class="sxs-lookup"><span data-stu-id="f0522-106">hello example application used here is an airplane location simulator.</span></span> <span data-ttu-id="f0522-107">您提供飛機識別碼、起飛時間和目的地。</span><span class="sxs-lookup"><span data-stu-id="f0522-107">You provide an airplane ID, departure time, and destination.</span></span> <span data-ttu-id="f0522-108">hello 應用程式的後端處理 hello 要求，並對應 hello 正在飛機符合 hello 準則顯示 hello 前端。</span><span class="sxs-lookup"><span data-stu-id="f0522-108">hello application’s back end processes hello requests, and hello front end displays on a map hello airplane that matches hello criteria.</span></span>

<span data-ttu-id="f0522-109">hello 下列圖表說明您在測試的 hello Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0522-109">hello following diagram illustrates hello Service Fabric application that you'll be testing.</span></span>

![Hello 範例飛機位置應用程式的圖表][0]

## <a name="prerequisites"></a><span data-ttu-id="f0522-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="f0522-111">Prerequisites</span></span>
<span data-ttu-id="f0522-112">之前開始，您必須 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f0522-112">Before getting started, you need toodo hello following:</span></span>

* <span data-ttu-id="f0522-113">取得 Visual Studio Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0522-113">Get a Visual Studio Team Services account.</span></span> <span data-ttu-id="f0522-114">您可以在 [Visual Studio Team Services](https://www.visualstudio.com)取得一個免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0522-114">You can get one for free at [Visual Studio Team Services](https://www.visualstudio.com).</span></span>
* <span data-ttu-id="f0522-115">取得並安裝 Visual Studio 2013 或 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="f0522-115">Get and install Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="f0522-116">本文使用 Visual Studio 2015 Enterprise 版本，但是 Visual Studio 2013 和其他版本應該也同樣可以運作。</span><span class="sxs-lookup"><span data-stu-id="f0522-116">This article uses Visual Studio 2015 Enterprise edition, but Visual Studio 2013 and other editions should work similarly.</span></span>
* <span data-ttu-id="f0522-117">部署您的應用程式 tooa 預備環境。</span><span class="sxs-lookup"><span data-stu-id="f0522-117">Deploy your application tooa staging environment.</span></span> <span data-ttu-id="f0522-118">請參閱[toodeploy 應用程式 tooa 遠端叢集使用 Visual Studio](service-fabric-publish-app-remote-cluster.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f0522-118">See [How toodeploy applications tooa remote cluster using Visual Studio](service-fabric-publish-app-remote-cluster.md) for information about this.</span></span>
* <span data-ttu-id="f0522-119">了解您的應用程式的使用模式。</span><span class="sxs-lookup"><span data-stu-id="f0522-119">Understand your application’s usage pattern.</span></span> <span data-ttu-id="f0522-120">這項資訊是使用的 toosimulate hello 負載模式。</span><span class="sxs-lookup"><span data-stu-id="f0522-120">This information is used toosimulate hello load pattern.</span></span>
* <span data-ttu-id="f0522-121">了解 hello 進行負載測試的目標。</span><span class="sxs-lookup"><span data-stu-id="f0522-121">Understand hello goal for your load testing.</span></span> <span data-ttu-id="f0522-122">這可協助您解譯及分析 hello 負載測試結果。</span><span class="sxs-lookup"><span data-stu-id="f0522-122">This helps you interpret and analyze hello load test results.</span></span>

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a><span data-ttu-id="f0522-123">建立及執行 hello Web 效能和負載測試專案</span><span class="sxs-lookup"><span data-stu-id="f0522-123">Create and run hello Web Performance and Load Test project</span></span>
### <a name="create-a-web-performance-and-load-test-project"></a><span data-ttu-id="f0522-124">建立 Web 效能和負載測試專案</span><span class="sxs-lookup"><span data-stu-id="f0522-124">Create a Web Performance and Load Test project</span></span>
1. <span data-ttu-id="f0522-125">開啟 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="f0522-125">Open Visual Studio 2015.</span></span> <span data-ttu-id="f0522-126">選擇**檔案** > **新增** > **專案**功能表列 tooopen hello hello**新專案** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f0522-126">Choose **File** > **New** > **Project** on hello menu bar tooopen hello **New Project** dialog box.</span></span>
2. <span data-ttu-id="f0522-127">展開 hello **Visual C#**節點，然後選擇 **測試** > **Web 效能和負載測試專案**。</span><span class="sxs-lookup"><span data-stu-id="f0522-127">Expand hello **Visual C#** node and choose **Test** > **Web Performance and Load Test project**.</span></span> <span data-ttu-id="f0522-128">指定 hello 專案的名稱，然後選擇 [hello**確定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0522-128">Give hello project a name and then choose hello **OK** button.</span></span>

    ![Hello 新增專案 對話方塊的螢幕擷取畫面][1]

    <span data-ttu-id="f0522-130">您應該會在 [方案總管] 中看到新的 Web 效能和負載測試專案。</span><span class="sxs-lookup"><span data-stu-id="f0522-130">You should see a new Web Performance and Load Test project in Solution Explorer.</span></span>

    ![顯示 hello 新專案的方案總管的螢幕擷取畫面][2]

### <a name="record-a-web-performance-test"></a><span data-ttu-id="f0522-132">記錄 Web 效能測試</span><span class="sxs-lookup"><span data-stu-id="f0522-132">Record a web performance test</span></span>
1. <span data-ttu-id="f0522-133">開啟 hello.webtest 專案。</span><span class="sxs-lookup"><span data-stu-id="f0522-133">Open hello .webtest project.</span></span>
2. <span data-ttu-id="f0522-134">選擇 hello**加入錄製**圖示 toostart 瀏覽器中的錄製工作階段。</span><span class="sxs-lookup"><span data-stu-id="f0522-134">Choose hello **Add Recording** icon toostart a recording session in your browser.</span></span>

    ![在瀏覽器中的 hello 加入錄製圖示的螢幕擷取畫面][3]

    ![在瀏覽器中的 hello Record 按鈕的螢幕擷取畫面][4]
3. <span data-ttu-id="f0522-137">瀏覽 toohello Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0522-137">Browse toohello Service Fabric application.</span></span> <span data-ttu-id="f0522-138">hello 錄製面板應該會顯示 hello web 要求。</span><span class="sxs-lookup"><span data-stu-id="f0522-138">hello recording panel should show hello web requests.</span></span>

    ![Hello 錄製面板中的 web 要求的螢幕擷取畫面][5]
4. <span data-ttu-id="f0522-140">執行一系列您預期 hello 使用者 tooperform 的動作。</span><span class="sxs-lookup"><span data-stu-id="f0522-140">Perform a sequence of actions that you expect hello users tooperform.</span></span> <span data-ttu-id="f0522-141">這些動作會使用模式 toogenerate hello 負載。</span><span class="sxs-lookup"><span data-stu-id="f0522-141">These actions are used as a pattern toogenerate hello load.</span></span>
5. <span data-ttu-id="f0522-142">當您完成時，選擇 hello**停止**按鈕 toostop 錄製。</span><span class="sxs-lookup"><span data-stu-id="f0522-142">When you're done, choose hello **Stop** button toostop recording.</span></span>

    ![Hello [停止] 按鈕的螢幕擷取畫面][6]

    <span data-ttu-id="f0522-144">Visual Studio 中的 hello.webtest 專案應該有擷取的一系列的要求。</span><span class="sxs-lookup"><span data-stu-id="f0522-144">hello .webtest project in Visual Studio should have captured a series of requests.</span></span> <span data-ttu-id="f0522-145">會自動取代動態參數。</span><span class="sxs-lookup"><span data-stu-id="f0522-145">Dynamic parameters are replaced automatically.</span></span> <span data-ttu-id="f0522-146">此時，您可以刪除不屬於您的測試案例的任何額外、重複相依性要求。</span><span class="sxs-lookup"><span data-stu-id="f0522-146">At this point, you can delete any extra, repeated dependency requests that are not part of your test scenario.</span></span>
6. <span data-ttu-id="f0522-147">儲存 hello 專案，然後選擇 hello**執行測試**命令 toorun hello web 效能測試在本機，並確定一切運作正常。</span><span class="sxs-lookup"><span data-stu-id="f0522-147">Save hello project and then choose hello **Run Test** command toorun hello web performance test locally and make sure everything works correctly.</span></span>

    ![Hello 執行測試命令的螢幕擷取畫面][7]

### <a name="parameterize-hello-web-performance-test"></a><span data-ttu-id="f0522-149">參數化 hello web 效能測試</span><span class="sxs-lookup"><span data-stu-id="f0522-149">Parameterize hello web performance test</span></span>
<span data-ttu-id="f0522-150">您可以將它轉換 tooa 自動程式化 web 效能測試，然後編輯 hello 程式碼來參數化 hello web 效能測試。</span><span class="sxs-lookup"><span data-stu-id="f0522-150">You can parameterize hello web performance test by converting it tooa coded web performance test and then editing hello code.</span></span> <span data-ttu-id="f0522-151">或者，您可以繫結 hello web 效能測試 tooa 資料清單以便 hello 測試逐一 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f0522-151">As an alternative, you can bind hello web performance test tooa data list so that hello test iterates through hello data.</span></span> <span data-ttu-id="f0522-152">請參閱[產生和執行自動程式化的 web 效能測試](https://msdn.microsoft.com/library/ms182552.aspx)如需如何 tooconvert hello web 效能測試 tooa 自動程式化測試詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f0522-152">See [Generate and run a coded web performance test](https://msdn.microsoft.com/library/ms182552.aspx) for details about how tooconvert hello web performance test tooa coded test.</span></span> <span data-ttu-id="f0522-153">請參閱[加入資料來源 tooa web 效能測試](https://msdn.microsoft.com/library/ms243142.aspx)如需如何 toobind 資料 tooa web 效能測試。</span><span class="sxs-lookup"><span data-stu-id="f0522-153">See [Add a data source tooa web performance test](https://msdn.microsoft.com/library/ms243142.aspx) for information about how toobind data tooa web performance test.</span></span>

<span data-ttu-id="f0522-154">針對此範例中，我們將轉換 hello web 效能測試 tooa 自動程式化測試，讓您可以將 hello 飛機識別碼取代產生的 GUID，並加入更多要求 toosend 班機 toodifferent 位置。</span><span class="sxs-lookup"><span data-stu-id="f0522-154">For this example, we'll convert hello web performance test tooa coded test so you can replace hello airplane ID with a generated GUID and add more requests toosend flights toodifferent locations.</span></span>

### <a name="create-a-load-test-project"></a><span data-ttu-id="f0522-155">建立負載測試專案</span><span class="sxs-lookup"><span data-stu-id="f0522-155">Create a load test project</span></span>
<span data-ttu-id="f0522-156">負載測試專案所組成 hello web 效能測試和單元測試，以及其他指定的負載測試設定所描述的一或多個案例。</span><span class="sxs-lookup"><span data-stu-id="f0522-156">A load test project is composed of one or more scenarios described by hello web performance test and unit test, along with additional specified load test settings.</span></span> <span data-ttu-id="f0522-157">hello 下列步驟顯示如何 toocreate 負載測試專案：</span><span class="sxs-lookup"><span data-stu-id="f0522-157">hello following steps show how toocreate a load test project:</span></span>

1. <span data-ttu-id="f0522-158">Hello Web 效能和負載測試專案的捷徑功能表，選擇 **新增** > **負載測試**。</span><span class="sxs-lookup"><span data-stu-id="f0522-158">On hello shortcut menu of your Web Performance and Load Test project, choose **Add** > **Load Test**.</span></span> <span data-ttu-id="f0522-159">在 [hello**負載測試**精靈] 中，選擇 hello**下一步**按鈕 tooconfigure hello 測試設定。</span><span class="sxs-lookup"><span data-stu-id="f0522-159">In hello **Load Test** wizard, choose hello **Next** button tooconfigure hello test settings.</span></span>
2. <span data-ttu-id="f0522-160">在 hello**負載模式**區段中，選擇是否要讓常數的使用者負載或逐步執行負載，就會開始與少數使用者以及增加 hello 使用者一段時間。</span><span class="sxs-lookup"><span data-stu-id="f0522-160">In hello **Load Pattern** section, choose whether you want a constant user load or a step load, which starts with a few users and increases hello users over time.</span></span>

    <span data-ttu-id="f0522-161">如果您有良好的估計量 hello 使用者負載，並想的 toosee hello 目前系統的執行方式，選擇**常數載入**。</span><span class="sxs-lookup"><span data-stu-id="f0522-161">If you have a good estimate of hello amount of user load and want toosee how hello current system performs, choose **Constant Load**.</span></span> <span data-ttu-id="f0522-162">如果您的目標 toolearn 是否 hello 系統就會在各種負載一致的方式執行，請選擇**逐步執行負載**。</span><span class="sxs-lookup"><span data-stu-id="f0522-162">If your goal is toolearn whether hello system performs consistently under various loads, choose **Step Load**.</span></span>
3. <span data-ttu-id="f0522-163">在 hello**測試混合**區段中，選擇 hello**新增**按鈕，然後選取 hello 測試您想 tooinclude hello 負載測試中的。</span><span class="sxs-lookup"><span data-stu-id="f0522-163">In hello **Test Mix** section, choose hello **Add** button and then select hello test that you want tooinclude in hello load test.</span></span> <span data-ttu-id="f0522-164">您可以使用 hello**發佈**資料行 toospecify hello 執行每一項測試的測試總數百分比。</span><span class="sxs-lookup"><span data-stu-id="f0522-164">You can use hello **Distribution** column toospecify hello percentage of total tests run for each test.</span></span>
4. <span data-ttu-id="f0522-165">在 hello**回合設定**區段中，指定 hello 負載測試持續期間。</span><span class="sxs-lookup"><span data-stu-id="f0522-165">In hello **Run Settings** section, specify hello load test duration.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f0522-166">hello**測試反覆項目**選項才可以使用只有當您執行負載測試使用 Visual Studio 在本機。</span><span class="sxs-lookup"><span data-stu-id="f0522-166">hello **Test Iterations** option is available only when you run a load test locally using Visual Studio.</span></span>
   >
   >
5. <span data-ttu-id="f0522-167">在 hello**位置**區段**回合設定**，指定產生負載測試要求 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="f0522-167">In hello **Location** section of **Run Settings**, specify hello location where load test requests are generated.</span></span> <span data-ttu-id="f0522-168">hello 精靈可能會提示您 toolog tooyour Team Services 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="f0522-168">hello wizard may prompt you toolog in tooyour Team Services account.</span></span> <span data-ttu-id="f0522-169">登入，然後選擇一個地理位置。</span><span class="sxs-lookup"><span data-stu-id="f0522-169">Log in and then choose a geographic location.</span></span> <span data-ttu-id="f0522-170">當您完成時，選擇 hello**完成** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0522-170">When you're done, choose hello **Finish** button.</span></span>
6. <span data-ttu-id="f0522-171">建立 hello 負載測試之後，開啟 hello.loadtest 專案，然後選擇 執行設定，例如 hello 目前**回合設定** > **回合設定 1 [Active]**。</span><span class="sxs-lookup"><span data-stu-id="f0522-171">After hello load test is created, open hello .loadtest project and choose hello current run setting, such as **Run Settings** > **Run Settings1 [Active]**.</span></span> <span data-ttu-id="f0522-172">這會開啟 hello hello 執行設定**屬性**視窗。</span><span class="sxs-lookup"><span data-stu-id="f0522-172">This opens hello run settings in hello **Properties** window.</span></span>
7. <span data-ttu-id="f0522-173">在 [hello**結果**hello 區段**回合設定**屬性] 視窗、 hello**計時詳細資料儲存區**設定應該有**無**做為預設值。</span><span class="sxs-lookup"><span data-stu-id="f0522-173">In hello **Results** section of hello **Run Settings** properties window, hello **Timing Details Storage** setting should have **None** as its default value.</span></span> <span data-ttu-id="f0522-174">變更此值太**所有個別細節**tooget hello 負載測試結果的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f0522-174">Change this value too**All Individual Details** tooget more information on hello load test results.</span></span> <span data-ttu-id="f0522-175">請參閱[載入測試](https://www.visualstudio.com/load-testing.aspx)如需有關如何 tooconnect tooVisual Studio Team Services 和執行負載測試。</span><span class="sxs-lookup"><span data-stu-id="f0522-175">See [Load Testing](https://www.visualstudio.com/load-testing.aspx) for more information on how tooconnect tooVisual Studio Team Services and run a load test.</span></span>

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a><span data-ttu-id="f0522-176">使用 Visual Studio Team Services 執行 hello 負載測試</span><span class="sxs-lookup"><span data-stu-id="f0522-176">Run hello load test by using Visual Studio Team Services</span></span>
<span data-ttu-id="f0522-177">選擇 hello**執行負載測試**命令 toostart hello 測試回合。</span><span class="sxs-lookup"><span data-stu-id="f0522-177">Choose hello **Run Load Test** command toostart hello test run.</span></span>

![Hello 執行負載測試命令的螢幕擷取畫面][8]

## <a name="view-and-analyze-hello-load-test-results"></a><span data-ttu-id="f0522-179">檢視及分析 hello 負載測試結果</span><span class="sxs-lookup"><span data-stu-id="f0522-179">View and analyze hello load test results</span></span>
<span data-ttu-id="f0522-180">Hello 為負載測試進行時，圖表化 hello 效能資訊。</span><span class="sxs-lookup"><span data-stu-id="f0522-180">As hello load test progresses, hello performance information is graphed.</span></span> <span data-ttu-id="f0522-181">您應該會看到類似 toohello 下列圖形。</span><span class="sxs-lookup"><span data-stu-id="f0522-181">You should see something similar toohello following graph.</span></span>

![負載測試結果的效能圖表的螢幕擷取畫面][9]

1. <span data-ttu-id="f0522-183">選擇 hello**下載報表**hello hello 頁面頂端附近的連結。</span><span class="sxs-lookup"><span data-stu-id="f0522-183">Choose hello **Download report** link near hello top of hello page.</span></span> <span data-ttu-id="f0522-184">下載 hello 報表之後，選擇 hello**檢視報表** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0522-184">After hello report is downloaded, choose hello **View report** button.</span></span>

    <span data-ttu-id="f0522-185">在 [hello**圖形**] 索引標籤，您可以查看各種效能計數器的圖形。</span><span class="sxs-lookup"><span data-stu-id="f0522-185">On hello **Graph** tab you can see graphs for various performance counters.</span></span> <span data-ttu-id="f0522-186">在 hello**摘要**索引標籤上，hello 整體測試結果會出現。</span><span class="sxs-lookup"><span data-stu-id="f0522-186">On hello **Summary** tab, hello overall test results appear.</span></span> <span data-ttu-id="f0522-187">hello**資料表**索引標籤會顯示成功和失敗的負載測試的 hello 總數。</span><span class="sxs-lookup"><span data-stu-id="f0522-187">hello **Tables** tab shows hello total number of passed and failed load tests.</span></span>
2. <span data-ttu-id="f0522-188">選擇在 hello hello 連結**測試** > **失敗**和 hello**錯誤** > **計數**資料行toosee 錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f0522-188">Choose hello number links on hello **Test** > **Failed** and hello **Errors** > **Count** columns toosee error details.</span></span>

    <span data-ttu-id="f0522-189">hello**詳細**索引標籤會顯示失敗的要求的虛擬使用者和測試案例資訊。</span><span class="sxs-lookup"><span data-stu-id="f0522-189">hello **Detail** tab shows virtual user and test scenario information for failed requests.</span></span> <span data-ttu-id="f0522-190">此資料非常適合如果 hello 負載測試包含多個案例。</span><span class="sxs-lookup"><span data-stu-id="f0522-190">This data can be useful if hello load test includes multiple scenarios.</span></span>

<span data-ttu-id="f0522-191">請參閱[分析負載測試結果 hello hello 負載測試分析器的圖形檢視中](https://www.visualstudio.com/load-testing.aspx)如需有關檢視負載測試結果。</span><span class="sxs-lookup"><span data-stu-id="f0522-191">See [Analyzing Load Test Results in hello Graphs View of hello Load Test Analyzer](https://www.visualstudio.com/load-testing.aspx) for more information on viewing load test results.</span></span>

## <a name="automate-your-load-test"></a><span data-ttu-id="f0522-192">自動化您的負載測試</span><span class="sxs-lookup"><span data-stu-id="f0522-192">Automate your load test</span></span>
<span data-ttu-id="f0522-193">Visual Studio Team Services 負載測試提供 Api toohelp 您管理負載測試和分析 Team Services 帳戶中的結果。</span><span class="sxs-lookup"><span data-stu-id="f0522-193">Visual Studio Team Services Load Test provides APIs toohelp you manage load tests and analyze results in a Team Services account.</span></span> <span data-ttu-id="f0522-194">如需詳細資訊，請參閱 [雲端負載測試 Rest API](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="f0522-194">See [Cloud Load Testing Rest APIs](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0522-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0522-195">Next steps</span></span>
* [<span data-ttu-id="f0522-196">監視和診斷本機開發設定中的服務</span><span class="sxs-lookup"><span data-stu-id="f0522-196">Monitoring and diagnosing services in a local machine development setup</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

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
