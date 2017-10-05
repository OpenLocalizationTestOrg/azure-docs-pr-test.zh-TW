---
title: "使用 Power BI 分析 Data Lake Store 中的資料 | Microsoft Docs"
description: "使用 Power BI 分析 Azure Data Lake Store 中所儲存的資料"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0cf7e385ef2edd650479e120f52469bc6632f2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a><span data-ttu-id="d63b7-103">使用 Power BI 分析 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="d63b7-103">Analyze data in Data Lake Store by using Power BI</span></span>
<span data-ttu-id="d63b7-104">在本文中，您將了解如何使用 Power BI Desktop 分析 Azure Data Lake Store 中所儲存的資料並加以視覺化。</span><span class="sxs-lookup"><span data-stu-id="d63b7-104">In this article you will learn how to use Power BI Desktop to analyze and visualize data stored in Azure Data Lake Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d63b7-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="d63b7-105">Prerequisites</span></span>
<span data-ttu-id="d63b7-106">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="d63b7-106">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="d63b7-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="d63b7-107">**An Azure subscription**.</span></span> <span data-ttu-id="d63b7-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d63b7-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d63b7-109">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="d63b7-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="d63b7-110">遵循 [使用 Azure 入口網站開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="d63b7-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="d63b7-111">本文假設您已經建立稱為 **mybidatalakestore** 的 Data Lake Store 帳戶，並將範例資料檔案 (**Drivers.txt**) 上傳到其中。</span><span class="sxs-lookup"><span data-stu-id="d63b7-111">This article assumes that you have already created a Data Lake Store account, called **mybidatalakestore**, and uploaded a sample data file (**Drivers.txt**) to it.</span></span> <span data-ttu-id="d63b7-112">此範例檔案可從 [Azure Data Lake Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)進行下載。</span><span class="sxs-lookup"><span data-stu-id="d63b7-112">This sample file is available for download from [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span>
* <span data-ttu-id="d63b7-113">**Power BI Desktop**。</span><span class="sxs-lookup"><span data-stu-id="d63b7-113">**Power BI Desktop**.</span></span> <span data-ttu-id="d63b7-114">您可以從 [Microsoft 下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=45331)下載此項目。</span><span class="sxs-lookup"><span data-stu-id="d63b7-114">You can download this from [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span></span> 

## <a name="create-a-report-in-power-bi-desktop"></a><span data-ttu-id="d63b7-115">在 Power BI Desktop 中建立報表</span><span class="sxs-lookup"><span data-stu-id="d63b7-115">Create a report in Power BI Desktop</span></span>
1. <span data-ttu-id="d63b7-116">在您的電腦上啟動 Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="d63b7-116">Launch Power BI Desktop on your computer.</span></span>
2. <span data-ttu-id="d63b7-117">從 [首頁] 功能區中，按一下 [取得資料]，然後按一下 [其他]。</span><span class="sxs-lookup"><span data-stu-id="d63b7-117">From the **Home** ribbon, click **Get Data**, and then click More.</span></span> <span data-ttu-id="d63b7-118">在 [取得資料] 對話方塊中，依序按一下 [Azure]、[Azure Data Lake Store] 和 [連線]。</span><span class="sxs-lookup"><span data-stu-id="d63b7-118">In the **Get Data** dialog box, click **Azure**, click **Azure Data Lake Store**, and then click **Connect**.</span></span>
   
    <span data-ttu-id="d63b7-119">![連線至 Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "連線至 Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d63b7-119">![Connect to Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect to Data Lake Store")</span></span>
3. <span data-ttu-id="d63b7-120">如果您看到連接器處於開發階段的對話方塊，請選擇繼續。</span><span class="sxs-lookup"><span data-stu-id="d63b7-120">If you see a dialog box about the connector being in a development phase, opt to continue.</span></span>
4. <span data-ttu-id="d63b7-121">在 [Microsoft Azure Data Lake Store] 對話方塊中，提供 Data Lake Store 帳戶的 URL，然後按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d63b7-121">In the **Microsoft Azure Data Lake Store** dialog box, provide the URL to your Data Lake Store account, and then click **OK**.</span></span>
   
    <span data-ttu-id="d63b7-122">![Data Lake Store 的 URL](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "Data Lake Store 的 URL")</span><span class="sxs-lookup"><span data-stu-id="d63b7-122">![URL for Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL for Data Lake Store")</span></span>
5. <span data-ttu-id="d63b7-123">在下一個對話方塊中，按一下 [登入]  登入 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d63b7-123">In the next dialog box, click **Sign in** to sign into Data Lake Store account.</span></span> <span data-ttu-id="d63b7-124">您將會被重新導向至組織的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="d63b7-124">You will be redirected to your organization's sign in page.</span></span> <span data-ttu-id="d63b7-125">遵循提示登入此帳戶。</span><span class="sxs-lookup"><span data-stu-id="d63b7-125">Follow the prompts to sign into the account.</span></span>
   
    <span data-ttu-id="d63b7-126">![登入 Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "登入 Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d63b7-126">![Sign into Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Sign into Data Lake Store")</span></span>
6. <span data-ttu-id="d63b7-127">順利登入之後，請按一下 [連線] 。</span><span class="sxs-lookup"><span data-stu-id="d63b7-127">After you have successfully signed in, click **Connect**.</span></span>
   
    <span data-ttu-id="d63b7-128">![連線至 Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "連線至 Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="d63b7-128">![Connect to Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect to Data Lake Store")</span></span>
7. <span data-ttu-id="d63b7-129">下一個對話方塊會顯示您已上傳至 Data Lake Store 帳戶的檔案。</span><span class="sxs-lookup"><span data-stu-id="d63b7-129">The next dialog box shows the file that you uploaded to your Data Lake Store account.</span></span> <span data-ttu-id="d63b7-130">驗證資訊，然後按一下 [載入] 。</span><span class="sxs-lookup"><span data-stu-id="d63b7-130">Verify the info and then click **Load**.</span></span>
   
    <span data-ttu-id="d63b7-131">![從 Data Lake Store 載入資料](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "從 Data Lake Store 載入資料")</span><span class="sxs-lookup"><span data-stu-id="d63b7-131">![Load data from Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Load data from Data Lake Store")</span></span>
8. <span data-ttu-id="d63b7-132">順利將資料載入至 Power BI 之後，即會在 [欄位]  索引標籤中看到下列欄位。</span><span class="sxs-lookup"><span data-stu-id="d63b7-132">After the data has been successfully loaded into Power BI, you will see the following fields in the **Fields** tab.</span></span>
   
    <span data-ttu-id="d63b7-133">![匯入的欄位](./media/data-lake-store-power-bi/imported-fields.png "匯入的欄位")</span><span class="sxs-lookup"><span data-stu-id="d63b7-133">![Imported fields](./media/data-lake-store-power-bi/imported-fields.png "Imported fields")</span></span>
   
    <span data-ttu-id="d63b7-134">不過，若要分析資料及加以視覺化，請使用下列欄位中的資料：</span><span class="sxs-lookup"><span data-stu-id="d63b7-134">However, to visualize and analyze the data, we prefer the data to be available per the following fields</span></span>
   
    <span data-ttu-id="d63b7-135">![所需的欄位](./media/data-lake-store-power-bi/desired-fields.png "所需的欄位")</span><span class="sxs-lookup"><span data-stu-id="d63b7-135">![Desired fields](./media/data-lake-store-power-bi/desired-fields.png "Desired fields")</span></span>
   
    <span data-ttu-id="d63b7-136">在後續步驟中，我們將更新查詢，以轉換所需格式的已匯入資料。</span><span class="sxs-lookup"><span data-stu-id="d63b7-136">In the next steps, we will update the query to convert the imported data in the desired format.</span></span>
9. <span data-ttu-id="d63b7-137">從 [首頁] 功能區中，按一下 [編輯查詢]。</span><span class="sxs-lookup"><span data-stu-id="d63b7-137">From the **Home** ribbon, click **Edit Queries**.</span></span>
   
    <span data-ttu-id="d63b7-138">![編輯查詢](./media/data-lake-store-power-bi/edit-queries.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="d63b7-138">![Edit queries](./media/data-lake-store-power-bi/edit-queries.png "Edit queries")</span></span>
10. <span data-ttu-id="d63b7-139">在 [查詢編輯器] 的 [內容] 資料行下，按一下 [二進位]。</span><span class="sxs-lookup"><span data-stu-id="d63b7-139">In the Query Editor, under the **Content** column, click **Binary**.</span></span>
    
    <span data-ttu-id="d63b7-140">![編輯查詢](./media/data-lake-store-power-bi/convert-query1.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="d63b7-140">![Edit queries](./media/data-lake-store-power-bi/convert-query1.png "Edit queries")</span></span>
11. <span data-ttu-id="d63b7-141">您將會看到檔案圖示，其代表您已上傳的 **Drivers.txt** 檔案。</span><span class="sxs-lookup"><span data-stu-id="d63b7-141">You will see a file icon, that represents the **Drivers.txt** file that you uploaded.</span></span> <span data-ttu-id="d63b7-142">在檔案上按一下滑鼠右鍵，然後按一下 [CSV] 。</span><span class="sxs-lookup"><span data-stu-id="d63b7-142">Right-click the file, and click **CSV**.</span></span>    
    
    <span data-ttu-id="d63b7-143">![編輯查詢](./media/data-lake-store-power-bi/convert-query2.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="d63b7-143">![Edit queries](./media/data-lake-store-power-bi/convert-query2.png "Edit queries")</span></span>
12. <span data-ttu-id="d63b7-144">您應該會看到如下的輸出。</span><span class="sxs-lookup"><span data-stu-id="d63b7-144">You should see an output as shown below.</span></span> <span data-ttu-id="d63b7-145">您的資料現在為可用來建立視覺效果的格式。</span><span class="sxs-lookup"><span data-stu-id="d63b7-145">Your data is now available in a format that you can use to create visualizations.</span></span>
    
    <span data-ttu-id="d63b7-146">![編輯查詢](./media/data-lake-store-power-bi/convert-query3.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="d63b7-146">![Edit queries](./media/data-lake-store-power-bi/convert-query3.png "Edit queries")</span></span>
13. <span data-ttu-id="d63b7-147">從 [首頁] 功能區中，按一下 [關閉並套用]，然後按一下 [關閉並套用]。</span><span class="sxs-lookup"><span data-stu-id="d63b7-147">From the **Home** ribbon, click **Close and Apply**, and then click **Close and Apply**.</span></span>
    
    <span data-ttu-id="d63b7-148">![編輯查詢](./media/data-lake-store-power-bi/load-edited-query.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="d63b7-148">![Edit queries](./media/data-lake-store-power-bi/load-edited-query.png "Edit queries")</span></span>
14. <span data-ttu-id="d63b7-149">更新查詢之後，[欄位]  索引標籤將會顯示可用於視覺效果的新欄位。</span><span class="sxs-lookup"><span data-stu-id="d63b7-149">Once the query is updated, the **Fields** tab will show the new fields available for visualization.</span></span>
    
    <span data-ttu-id="d63b7-150">![更新的欄位](./media/data-lake-store-power-bi/updated-query-fields.png "更新的欄位")</span><span class="sxs-lookup"><span data-stu-id="d63b7-150">![Updated fields](./media/data-lake-store-power-bi/updated-query-fields.png "Updated fields")</span></span>
15. <span data-ttu-id="d63b7-151">讓我們建立圓形圖，以代表指定國家/地區的每個城市中的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="d63b7-151">Let us create a pie chart to represent the drivers in each city for a given country.</span></span> <span data-ttu-id="d63b7-152">若要這麼做，請進行下列選擇。</span><span class="sxs-lookup"><span data-stu-id="d63b7-152">To do so, make the following selections.</span></span>
    
    1. <span data-ttu-id="d63b7-153">從 [視覺效果] 索引標籤中，按一下圓形圖的符號。</span><span class="sxs-lookup"><span data-stu-id="d63b7-153">From the Visualizations tab, click the symbol for a pie chart.</span></span>
       
        <span data-ttu-id="d63b7-154">![建立圓形圖](./media/data-lake-store-power-bi/create-pie-chart.png "建立圓形圖")</span><span class="sxs-lookup"><span data-stu-id="d63b7-154">![Create pie chart](./media/data-lake-store-power-bi/create-pie-chart.png "Create pie chart")</span></span>
    2. <span data-ttu-id="d63b7-155">我們將使用的資料行是 [資料行 4]\(城市名稱) 和 [資料行 7]\(國家/地區名稱)。</span><span class="sxs-lookup"><span data-stu-id="d63b7-155">The columns that we are going to use are **Column 4** (name of the city) and **Column 7** (name of the country).</span></span> <span data-ttu-id="d63b7-156">將這些資料行從 [欄位] 索引標籤拖曳到 [視覺效果] 索引標籤 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="d63b7-156">Drag these columns from **Fields** tab to **Visualizations** tab as shown below.</span></span>
       
        <span data-ttu-id="d63b7-157">![建立視覺效果](./media/data-lake-store-power-bi/create-visualizations.png "建立視覺效果")</span><span class="sxs-lookup"><span data-stu-id="d63b7-157">![Create visualizations](./media/data-lake-store-power-bi/create-visualizations.png "Create visualizations")</span></span>
    3. <span data-ttu-id="d63b7-158">圓形圖現在應該與下面類似。</span><span class="sxs-lookup"><span data-stu-id="d63b7-158">The pie chart should now resemble like the one shown below.</span></span>
       
        <span data-ttu-id="d63b7-159">![圓形圖](./media/data-lake-store-power-bi/pie-chart.png "建立視覺效果")</span><span class="sxs-lookup"><span data-stu-id="d63b7-159">![Pie chart](./media/data-lake-store-power-bi/pie-chart.png "Create visualizations")</span></span>
16. <span data-ttu-id="d63b7-160">透過從頁面層級篩選中選取特定國家/地區，您現在可以看到所選國家/地區的每個城市中的驅動程式數目。</span><span class="sxs-lookup"><span data-stu-id="d63b7-160">By selecting a specific country from the page level filters, you can now see the number of drivers in each city of the selected country.</span></span> <span data-ttu-id="d63b7-161">例如，在 [視覺效果] 索引標籤的 [頁面層級篩選] 下，選取 [巴西]。</span><span class="sxs-lookup"><span data-stu-id="d63b7-161">For example, under the **Visualizations** tab, under **Page level filters**, select **Brazil**.</span></span>
    
    <span data-ttu-id="d63b7-162">![選取國家/地區](./media/data-lake-store-power-bi/select-country.png "選取國家/地區")</span><span class="sxs-lookup"><span data-stu-id="d63b7-162">![Select a country](./media/data-lake-store-power-bi/select-country.png "Select a country")</span></span>
17. <span data-ttu-id="d63b7-163">圓形圖會自動更新以顯示巴西城市中的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="d63b7-163">The pie chart is automatically updated to display the drivers in the cities of Brazil.</span></span>
    
    <span data-ttu-id="d63b7-164">![國家/地區中的驅動程式](./media/data-lake-store-power-bi/driver-per-country.png "每個國家的驅動程式")</span><span class="sxs-lookup"><span data-stu-id="d63b7-164">![Drivers in a country](./media/data-lake-store-power-bi/driver-per-country.png "Drivers per country")</span></span>
18. <span data-ttu-id="d63b7-165">從 [檔案] 功能表中，按一下 [儲存] 將視覺效果儲存為 Power BI Desktop 檔案。</span><span class="sxs-lookup"><span data-stu-id="d63b7-165">From the **File** menu, click **Save** to save the visualization as a Power BI Desktop file.</span></span>

## <a name="publish-report-to-power-bi-service"></a><span data-ttu-id="d63b7-166">將報表發佈到 Power BI 服務</span><span class="sxs-lookup"><span data-stu-id="d63b7-166">Publish report to Power BI service</span></span>
<span data-ttu-id="d63b7-167">在 Power BI Desktop 中建立視覺效果之後，即可將它發佈到 Power BI 服務，與其他人共用。</span><span class="sxs-lookup"><span data-stu-id="d63b7-167">Once you have created the visualizations in Power BI Desktop, you can share it with others by publishing it to the Power BI service.</span></span> <span data-ttu-id="d63b7-168">如需如何執行的指示，請參閱[從 Power BI Desktop 發佈](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/)。</span><span class="sxs-lookup"><span data-stu-id="d63b7-168">For instructions on how to do that, see [Publish from Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span></span>

## <a name="see-also"></a><span data-ttu-id="d63b7-169">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d63b7-169">See also</span></span>
* [<span data-ttu-id="d63b7-170">使用 Data Lake Analytics 分析 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="d63b7-170">Analyze data in Data Lake Store using Data Lake Analytics</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

