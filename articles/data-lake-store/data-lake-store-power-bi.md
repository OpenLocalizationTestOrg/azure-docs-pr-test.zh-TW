---
title: "資料湖存放區中使用 Power BI 的 aaaAnalyze 資料 |Microsoft 文件"
description: "使用 Power BI tooanalyze 資料儲存在 Azure 資料湖存放區"
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
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a><span data-ttu-id="61962-103">使用 Power BI 分析 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="61962-103">Analyze data in Data Lake Store by using Power BI</span></span>
<span data-ttu-id="61962-104">在本文中，您將學習如何 toouse Power BI Desktop tooanalyze 及視覺化儲存在 Azure 資料湖存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="61962-104">In this article you will learn how toouse Power BI Desktop tooanalyze and visualize data stored in Azure Data Lake Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61962-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="61962-105">Prerequisites</span></span>
<span data-ttu-id="61962-106">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="61962-106">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="61962-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="61962-107">**An Azure subscription**.</span></span> <span data-ttu-id="61962-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="61962-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="61962-109">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="61962-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="61962-110">請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="61962-110">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="61962-111">本文假設您已經建立名為的 Data Lake Store 帳戶**mybidatalakestore**，並上傳範例資料檔 (**Drivers.txt**) tooit。</span><span class="sxs-lookup"><span data-stu-id="61962-111">This article assumes that you have already created a Data Lake Store account, called **mybidatalakestore**, and uploaded a sample data file (**Drivers.txt**) tooit.</span></span> <span data-ttu-id="61962-112">此範例檔案可從 [Azure Data Lake Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)進行下載。</span><span class="sxs-lookup"><span data-stu-id="61962-112">This sample file is available for download from [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span>
* <span data-ttu-id="61962-113">**Power BI Desktop**。</span><span class="sxs-lookup"><span data-stu-id="61962-113">**Power BI Desktop**.</span></span> <span data-ttu-id="61962-114">您可以從 [Microsoft 下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=45331)下載此項目。</span><span class="sxs-lookup"><span data-stu-id="61962-114">You can download this from [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span></span> 

## <a name="create-a-report-in-power-bi-desktop"></a><span data-ttu-id="61962-115">在 Power BI Desktop 中建立報表</span><span class="sxs-lookup"><span data-stu-id="61962-115">Create a report in Power BI Desktop</span></span>
1. <span data-ttu-id="61962-116">在您的電腦上啟動 Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="61962-116">Launch Power BI Desktop on your computer.</span></span>
2. <span data-ttu-id="61962-117">從 hello**首頁**功能區中，按一下 **取得資料**，然後按一下更多。</span><span class="sxs-lookup"><span data-stu-id="61962-117">From hello **Home** ribbon, click **Get Data**, and then click More.</span></span> <span data-ttu-id="61962-118">在 hello**取得資料**對話方塊中，按一下  **Azure**，按一下**Azure Data Lake Store**，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="61962-118">In hello **Get Data** dialog box, click **Azure**, click **Azure Data Lake Store**, and then click **Connect**.</span></span>
   
    <span data-ttu-id="61962-119">![連接 tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "連接 tooData 湖存放區")</span><span class="sxs-lookup"><span data-stu-id="61962-119">![Connect tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect tooData Lake Store")</span></span>
3. <span data-ttu-id="61962-120">如果您看到有關 hello 連接器處於開發階段的對話方塊，選擇 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="61962-120">If you see a dialog box about hello connector being in a development phase, opt toocontinue.</span></span>
4. <span data-ttu-id="61962-121">在 hello **Microsoft Azure Data Lake Store**對話方塊中，提供 hello URL tooyour Data Lake Store 帳戶，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="61962-121">In hello **Microsoft Azure Data Lake Store** dialog box, provide hello URL tooyour Data Lake Store account, and then click **OK**.</span></span>
   
    <span data-ttu-id="61962-122">![Data Lake Store 的 URL](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "Data Lake Store 的 URL")</span><span class="sxs-lookup"><span data-stu-id="61962-122">![URL for Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL for Data Lake Store")</span></span>
5. <span data-ttu-id="61962-123">在 hello 下一步 對話方塊中，按一下 **登入**toosign 到 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="61962-123">In hello next dialog box, click **Sign in** toosign into Data Lake Store account.</span></span> <span data-ttu-id="61962-124">您將會重新導向 tooyour 組織的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="61962-124">You will be redirected tooyour organization's sign in page.</span></span> <span data-ttu-id="61962-125">遵循 hello 提示 toosign hello 考量。</span><span class="sxs-lookup"><span data-stu-id="61962-125">Follow hello prompts toosign into hello account.</span></span>
   
    <span data-ttu-id="61962-126">![登入 Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "登入 Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="61962-126">![Sign into Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Sign into Data Lake Store")</span></span>
6. <span data-ttu-id="61962-127">順利登入之後，請按一下 [連線] 。</span><span class="sxs-lookup"><span data-stu-id="61962-127">After you have successfully signed in, click **Connect**.</span></span>
   
    <span data-ttu-id="61962-128">![連接 tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "連接 tooData 湖存放區")</span><span class="sxs-lookup"><span data-stu-id="61962-128">![Connect tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect tooData Lake Store")</span></span>
7. <span data-ttu-id="61962-129">hello 下一步 對話方塊會顯示 hello 檔案上傳 tooyour Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="61962-129">hello next dialog box shows hello file that you uploaded tooyour Data Lake Store account.</span></span> <span data-ttu-id="61962-130">確認 hello 資訊，然後按一下**負載**。</span><span class="sxs-lookup"><span data-stu-id="61962-130">Verify hello info and then click **Load**.</span></span>
   
    <span data-ttu-id="61962-131">![從 Data Lake Store 載入資料](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "從 Data Lake Store 載入資料")</span><span class="sxs-lookup"><span data-stu-id="61962-131">![Load data from Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Load data from Data Lake Store")</span></span>
8. <span data-ttu-id="61962-132">Hello 資料已成功載入 Power BI 之後，您會看到下列 hello 中的欄位的 hello**欄位** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="61962-132">After hello data has been successfully loaded into Power BI, you will see hello following fields in hello **Fields** tab.</span></span>
   
    <span data-ttu-id="61962-133">![匯入的欄位](./media/data-lake-store-power-bi/imported-fields.png "匯入的欄位")</span><span class="sxs-lookup"><span data-stu-id="61962-133">![Imported fields](./media/data-lake-store-power-bi/imported-fields.png "Imported fields")</span></span>
   
    <span data-ttu-id="61962-134">不過，toovisualize 和分析 hello 資料，我們喜歡 hello 資料 toobe hello 下列欄位可用</span><span class="sxs-lookup"><span data-stu-id="61962-134">However, toovisualize and analyze hello data, we prefer hello data toobe available per hello following fields</span></span>
   
    <span data-ttu-id="61962-135">![所需的欄位](./media/data-lake-store-power-bi/desired-fields.png "所需的欄位")</span><span class="sxs-lookup"><span data-stu-id="61962-135">![Desired fields](./media/data-lake-store-power-bi/desired-fields.png "Desired fields")</span></span>
   
    <span data-ttu-id="61962-136">在 hello 下一個步驟中，我們將會更新 hello 查詢 tooconvert hello 所要的格式中的 hello 匯入資料。</span><span class="sxs-lookup"><span data-stu-id="61962-136">In hello next steps, we will update hello query tooconvert hello imported data in hello desired format.</span></span>
9. <span data-ttu-id="61962-137">從 hello**首頁**功能區中，按一下 **編輯查詢**。</span><span class="sxs-lookup"><span data-stu-id="61962-137">From hello **Home** ribbon, click **Edit Queries**.</span></span>
   
    <span data-ttu-id="61962-138">![編輯查詢](./media/data-lake-store-power-bi/edit-queries.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="61962-138">![Edit queries](./media/data-lake-store-power-bi/edit-queries.png "Edit queries")</span></span>
10. <span data-ttu-id="61962-139">在 hello 查詢編輯器中，在 hello**內容**資料行中，按一下 **二進位**。</span><span class="sxs-lookup"><span data-stu-id="61962-139">In hello Query Editor, under hello **Content** column, click **Binary**.</span></span>
    
    <span data-ttu-id="61962-140">![編輯查詢](./media/data-lake-store-power-bi/convert-query1.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="61962-140">![Edit queries](./media/data-lake-store-power-bi/convert-query1.png "Edit queries")</span></span>
11. <span data-ttu-id="61962-141">您會看到檔案圖示，表示 hello **Drivers.txt**您上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="61962-141">You will see a file icon, that represents hello **Drivers.txt** file that you uploaded.</span></span> <span data-ttu-id="61962-142">Hello 檔案上按一下滑鼠右鍵，然後按一下**CSV**。</span><span class="sxs-lookup"><span data-stu-id="61962-142">Right-click hello file, and click **CSV**.</span></span>    
    
    <span data-ttu-id="61962-143">![編輯查詢](./media/data-lake-store-power-bi/convert-query2.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="61962-143">![Edit queries](./media/data-lake-store-power-bi/convert-query2.png "Edit queries")</span></span>
12. <span data-ttu-id="61962-144">您應該會看到如下的輸出。</span><span class="sxs-lookup"><span data-stu-id="61962-144">You should see an output as shown below.</span></span> <span data-ttu-id="61962-145">現在您可以使用 toocreate 視覺效果格式提供您的資料。</span><span class="sxs-lookup"><span data-stu-id="61962-145">Your data is now available in a format that you can use toocreate visualizations.</span></span>
    
    <span data-ttu-id="61962-146">![編輯查詢](./media/data-lake-store-power-bi/convert-query3.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="61962-146">![Edit queries](./media/data-lake-store-power-bi/convert-query3.png "Edit queries")</span></span>
13. <span data-ttu-id="61962-147">從 hello**首頁**功能區中，按一下 **關閉並套用**，然後按一下**關閉並套用**。</span><span class="sxs-lookup"><span data-stu-id="61962-147">From hello **Home** ribbon, click **Close and Apply**, and then click **Close and Apply**.</span></span>
    
    <span data-ttu-id="61962-148">![編輯查詢](./media/data-lake-store-power-bi/load-edited-query.png "編輯查詢")</span><span class="sxs-lookup"><span data-stu-id="61962-148">![Edit queries](./media/data-lake-store-power-bi/load-edited-query.png "Edit queries")</span></span>
14. <span data-ttu-id="61962-149">一旦更新 hello 查詢時，hello**欄位**索引標籤會顯示 hello 可用視覺效果的新欄位。</span><span class="sxs-lookup"><span data-stu-id="61962-149">Once hello query is updated, hello **Fields** tab will show hello new fields available for visualization.</span></span>
    
    <span data-ttu-id="61962-150">![更新的欄位](./media/data-lake-store-power-bi/updated-query-fields.png "更新的欄位")</span><span class="sxs-lookup"><span data-stu-id="61962-150">![Updated fields](./media/data-lake-store-power-bi/updated-query-fields.png "Updated fields")</span></span>
15. <span data-ttu-id="61962-151">讓我們建立圓形圖 toorepresent hello 驅動程式在給定的國家/地區的每個城市。</span><span class="sxs-lookup"><span data-stu-id="61962-151">Let us create a pie chart toorepresent hello drivers in each city for a given country.</span></span> <span data-ttu-id="61962-152">toodo，進行下列選取項目 hello。</span><span class="sxs-lookup"><span data-stu-id="61962-152">toodo so, make hello following selections.</span></span>
    
    1. <span data-ttu-id="61962-153">Hello 視覺效果 索引標籤中，按一下圓形圖的 hello 符號。</span><span class="sxs-lookup"><span data-stu-id="61962-153">From hello Visualizations tab, click hello symbol for a pie chart.</span></span>
       
        <span data-ttu-id="61962-154">![建立圓形圖](./media/data-lake-store-power-bi/create-pie-chart.png "建立圓形圖")</span><span class="sxs-lookup"><span data-stu-id="61962-154">![Create pie chart](./media/data-lake-store-power-bi/create-pie-chart.png "Create pie chart")</span></span>
    2. <span data-ttu-id="61962-155">hello 資料行，我們會 toouse**資料行 4** （hello 縣 （市） 的名稱） 和**資料行 7** （hello 國家/地區的名稱）。</span><span class="sxs-lookup"><span data-stu-id="61962-155">hello columns that we are going toouse are **Column 4** (name of hello city) and **Column 7** (name of hello country).</span></span> <span data-ttu-id="61962-156">拖曳資料行，從**欄位**索引標籤太**視覺效果**索引標籤上，如下所示。</span><span class="sxs-lookup"><span data-stu-id="61962-156">Drag these columns from **Fields** tab too**Visualizations** tab as shown below.</span></span>
       
        <span data-ttu-id="61962-157">![建立視覺效果](./media/data-lake-store-power-bi/create-visualizations.png "建立視覺效果")</span><span class="sxs-lookup"><span data-stu-id="61962-157">![Create visualizations](./media/data-lake-store-power-bi/create-visualizations.png "Create visualizations")</span></span>
    3. <span data-ttu-id="61962-158">hello 圓形圖現在應該類似如下所示的其中一個 hello 類似。</span><span class="sxs-lookup"><span data-stu-id="61962-158">hello pie chart should now resemble like hello one shown below.</span></span>
       
        <span data-ttu-id="61962-159">![圓形圖](./media/data-lake-store-power-bi/pie-chart.png "建立視覺效果")</span><span class="sxs-lookup"><span data-stu-id="61962-159">![Pie chart](./media/data-lake-store-power-bi/pie-chart.png "Create visualizations")</span></span>
16. <span data-ttu-id="61962-160">藉由從 hello 頁面層級篩選中選取特定國家/地區，您現在可以看到 hello hello 選取國家/地區的每個城市中的驅動程式數目。</span><span class="sxs-lookup"><span data-stu-id="61962-160">By selecting a specific country from hello page level filters, you can now see hello number of drivers in each city of hello selected country.</span></span> <span data-ttu-id="61962-161">例如，在 hello**視覺效果**索引標籤，下方**頁面層級篩選**，選取**巴西**。</span><span class="sxs-lookup"><span data-stu-id="61962-161">For example, under hello **Visualizations** tab, under **Page level filters**, select **Brazil**.</span></span>
    
    <span data-ttu-id="61962-162">![選取國家/地區](./media/data-lake-store-power-bi/select-country.png "選取國家/地區")</span><span class="sxs-lookup"><span data-stu-id="61962-162">![Select a country](./media/data-lake-store-power-bi/select-country.png "Select a country")</span></span>
17. <span data-ttu-id="61962-163">hello 圓形圖是巴西的 hello 城市中的自動更新的 toodisplay hello 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="61962-163">hello pie chart is automatically updated toodisplay hello drivers in hello cities of Brazil.</span></span>
    
    <span data-ttu-id="61962-164">![國家/地區中的驅動程式](./media/data-lake-store-power-bi/driver-per-country.png "每個國家的驅動程式")</span><span class="sxs-lookup"><span data-stu-id="61962-164">![Drivers in a country](./media/data-lake-store-power-bi/driver-per-country.png "Drivers per country")</span></span>
18. <span data-ttu-id="61962-165">從 hello**檔案**功能表上，按一下 **儲存**toosave hello 視覺效果，與 Power BI Desktop 檔案。</span><span class="sxs-lookup"><span data-stu-id="61962-165">From hello **File** menu, click **Save** toosave hello visualization as a Power BI Desktop file.</span></span>

## <a name="publish-report-toopower-bi-service"></a><span data-ttu-id="61962-166">發行報表 tooPower BI 服務</span><span class="sxs-lookup"><span data-stu-id="61962-166">Publish report tooPower BI service</span></span>
<span data-ttu-id="61962-167">Power BI Desktop 中建立 hello 視覺效果之後，您可以與其他人共用發佈 toohello Power BI 服務。</span><span class="sxs-lookup"><span data-stu-id="61962-167">Once you have created hello visualizations in Power BI Desktop, you can share it with others by publishing it toohello Power BI service.</span></span> <span data-ttu-id="61962-168">如需指示，請參閱 toodo[從 Power BI Desktop 發佈](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/)。</span><span class="sxs-lookup"><span data-stu-id="61962-168">For instructions on how toodo that, see [Publish from Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span></span>

## <a name="see-also"></a><span data-ttu-id="61962-169">另請參閱</span><span class="sxs-lookup"><span data-stu-id="61962-169">See also</span></span>
* [<span data-ttu-id="61962-170">使用 Data Lake Analytics 分析 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="61962-170">Analyze data in Data Lake Store using Data Lake Analytics</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

