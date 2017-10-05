---
title: "使用 Azure 入口網站疑難排解 Azure Data Lake Analytics作業 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站疑難排解資料湖分析作業。 "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="8620b-103">使用 Azure 入口網站疑難排解 Azure 資料湖分析作業</span><span class="sxs-lookup"><span data-stu-id="8620b-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="8620b-104">了解如何使用 Azure 入口網站疑難排解資料湖分析作業。</span><span class="sxs-lookup"><span data-stu-id="8620b-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="8620b-105">在本教學課程中，將會建立一個來源檔案遺失的問題，並使用 Azure 入口網站疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="8620b-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="8620b-106">提交資料湖分析作業</span><span class="sxs-lookup"><span data-stu-id="8620b-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="8620b-107">提交下列 U-SQL 作業：</span><span class="sxs-lookup"><span data-stu-id="8620b-107">Submit the following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="8620b-108">指令碼中定義的來源檔案是 **/Samples/Data/SearchLog.tsv1**，此處應為 **/Samples/Data/SearchLog.tsv**。</span><span class="sxs-lookup"><span data-stu-id="8620b-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="8620b-109">疑難排解作業</span><span class="sxs-lookup"><span data-stu-id="8620b-109">Troubleshoot the job</span></span>

<span data-ttu-id="8620b-110">**查看所有工作**</span><span class="sxs-lookup"><span data-stu-id="8620b-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="8620b-111">在 Azure 入口網站中，按一下左上角的 [ **Microsoft Azure** ]。</span><span class="sxs-lookup"><span data-stu-id="8620b-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="8620b-112">按一下具有您資料湖分析帳戶名稱的磚。</span><span class="sxs-lookup"><span data-stu-id="8620b-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="8620b-113">工作摘要隨即顯示在 [ **工作管理** ] 磚上。</span><span class="sxs-lookup"><span data-stu-id="8620b-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Azure 資料湖分析作業管理](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="8620b-115">[工作管理可] 讓您對工作的狀態一目瞭然。</span><span class="sxs-lookup"><span data-stu-id="8620b-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="8620b-116">請注意失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="8620b-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="8620b-117">按一下 [ **工作管理** ] 磚以檢視工作。</span><span class="sxs-lookup"><span data-stu-id="8620b-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="8620b-118">工作分類成 [執行中]、[已排入序列] 和 [結束]。</span><span class="sxs-lookup"><span data-stu-id="8620b-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="8620b-119">您應該會在 [ **結束** ] 區段中看到失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="8620b-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="8620b-120">該工作應該列在清單中的首位。</span><span class="sxs-lookup"><span data-stu-id="8620b-120">It shall be first one in the list.</span></span> <span data-ttu-id="8620b-121">如果有很多工作，您可以按一下 [ **篩選** ] 來協助您找出工作。</span><span class="sxs-lookup"><span data-stu-id="8620b-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Azure 資料湖分析篩選作業](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="8620b-123">按一下清單中的失敗工作，會以新的刀鋒視窗開啟工作詳細資料：</span><span class="sxs-lookup"><span data-stu-id="8620b-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Azure 資料湖分析失敗作業](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="8620b-125">請注意 [ **重新提交** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8620b-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="8620b-126">修正問題之後，您可以重新提交工作。</span><span class="sxs-lookup"><span data-stu-id="8620b-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="8620b-127">按一下前一個螢幕擷取畫面中反白顯示的部分，開啟錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8620b-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="8620b-128">您會看到類似下面的畫面：</span><span class="sxs-lookup"><span data-stu-id="8620b-128">You shall see something like:</span></span>

    ![Azure 資料湖分析失敗作業詳細資料](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="8620b-130">它會告訴您找不到來源資料夾。</span><span class="sxs-lookup"><span data-stu-id="8620b-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="8620b-131">按一下 [ **重複的指令碼**]。</span><span class="sxs-lookup"><span data-stu-id="8620b-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="8620b-132">將 **FROM** 路徑更新成下方路徑：</span><span class="sxs-lookup"><span data-stu-id="8620b-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="8620b-133">"/Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="8620b-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="8620b-134">按一下 [ **提交作業**]。</span><span class="sxs-lookup"><span data-stu-id="8620b-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="8620b-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8620b-135">See also</span></span>
* [<span data-ttu-id="8620b-136">Azure 資料湖分析概觀</span><span class="sxs-lookup"><span data-stu-id="8620b-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="8620b-137">使用 Azure PowerShell 開始使用 Azure 資料湖分析</span><span class="sxs-lookup"><span data-stu-id="8620b-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="8620b-138">透過 Visual Studio 開始使用 Azure 資料湖分析與 U-SQL</span><span class="sxs-lookup"><span data-stu-id="8620b-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="8620b-139">使用 Azure 入口網站管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8620b-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
