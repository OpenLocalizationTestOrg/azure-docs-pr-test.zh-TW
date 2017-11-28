---
title: "使用 Azure 入口網站的 aaaTroubleshoot Azure Data Lake Analytics 作業 |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站 tootroubleshoot Data Lake Analytics 工作。 "
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
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="b4234-103">使用 Azure 入口網站疑難排解 Azure 資料湖分析作業</span><span class="sxs-lookup"><span data-stu-id="b4234-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="b4234-104">了解如何 toouse hello Azure 入口網站 tootroubleshoot Data Lake Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="b4234-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="b4234-105">在本教學課程中，您會安裝遺失的來源檔案問題，並使用 hello Azure 入口網站 tootroubleshoot hello 問題。</span><span class="sxs-lookup"><span data-stu-id="b4234-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="b4234-106">提交資料湖分析作業</span><span class="sxs-lookup"><span data-stu-id="b4234-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="b4234-107">送出 hello 遵循 U-SQL 作業：</span><span class="sxs-lookup"><span data-stu-id="b4234-107">Submit hello following U-SQL job:</span></span>

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
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="b4234-108">hello hello 指令碼中定義的原始程式檔是**/Samples/Data/SearchLog.tsv1**，應該是**/Samples/Data/SearchLog.tsv**。</span><span class="sxs-lookup"><span data-stu-id="b4234-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="b4234-109">疑難排解 hello 作業</span><span class="sxs-lookup"><span data-stu-id="b4234-109">Troubleshoot hello job</span></span>

<span data-ttu-id="b4234-110">**toosee 所有 hello 工作**</span><span class="sxs-lookup"><span data-stu-id="b4234-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="b4234-111">從 hello Azure 入口網站，按一下  **Microsoft Azure** hello 左上角。</span><span class="sxs-lookup"><span data-stu-id="b4234-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="b4234-112">按一下 hello 磚使用 Data Lake Analytics 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b4234-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="b4234-113">hello 工作摘要會顯示在 hello**作業管理**磚。</span><span class="sxs-lookup"><span data-stu-id="b4234-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Azure 資料湖分析作業管理](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="b4234-115">hello 作業管理可讓您一目瞭然 hello 作業狀態。</span><span class="sxs-lookup"><span data-stu-id="b4234-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="b4234-116">請注意失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="b4234-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="b4234-117">按一下 hello**作業管理**磚 toosee hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b4234-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="b4234-118">hello 作業分為**執行**，**排入佇列**，和**結束**。</span><span class="sxs-lookup"><span data-stu-id="b4234-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="b4234-119">您應該會看到您失敗的作業在 hello**結束**> 一節。</span><span class="sxs-lookup"><span data-stu-id="b4234-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="b4234-120">應該就能 hello 清單中的第一個。</span><span class="sxs-lookup"><span data-stu-id="b4234-120">It shall be first one in hello list.</span></span> <span data-ttu-id="b4234-121">當您有大量的工作時，您可以按一下**篩選**toohelp 您 toolocate 作業。</span><span class="sxs-lookup"><span data-stu-id="b4234-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Azure 資料湖分析篩選作業](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="b4234-123">按一下 hello hello 清單 tooopen hello 工作詳細資料中的新刀鋒視窗從失敗的作業：</span><span class="sxs-lookup"><span data-stu-id="b4234-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Azure 資料湖分析失敗作業](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="b4234-125">請注意 hello**重新提交** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b4234-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="b4234-126">修正 hello 問題之後，您可以重新提交 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b4234-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="b4234-127">按一下反白顯示的部分從 hello 上一個螢幕擷取畫面 tooopen hello 錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b4234-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="b4234-128">您會看到類似下面的畫面：</span><span class="sxs-lookup"><span data-stu-id="b4234-128">You shall see something like:</span></span>

    ![Azure 資料湖分析失敗作業詳細資料](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="b4234-130">它會告訴您找不到 hello 來源資料夾。</span><span class="sxs-lookup"><span data-stu-id="b4234-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="b4234-131">按一下 [ **重複的指令碼**]。</span><span class="sxs-lookup"><span data-stu-id="b4234-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="b4234-132">更新 hello **FROM**路徑 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="b4234-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="b4234-133">"/Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="b4234-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="b4234-134">按一下 [ **提交作業**]。</span><span class="sxs-lookup"><span data-stu-id="b4234-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="b4234-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b4234-135">See also</span></span>
* [<span data-ttu-id="b4234-136">Azure 資料湖分析概觀</span><span class="sxs-lookup"><span data-stu-id="b4234-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="b4234-137">使用 Azure PowerShell 開始使用 Azure 資料湖分析</span><span class="sxs-lookup"><span data-stu-id="b4234-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="b4234-138">透過 Visual Studio 開始使用 Azure 資料湖分析與 U-SQL</span><span class="sxs-lookup"><span data-stu-id="b4234-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="b4234-139">使用 Azure 入口網站管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b4234-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
