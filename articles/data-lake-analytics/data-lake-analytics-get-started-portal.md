---
title: "使用 Azure 入口網站開始使用 Azure Data Lake Analytics | Microsoft Docs"
description: "了解如何使用 Azure 入口網站建立 Data Lake Analytics 帳戶、使用 U-SQL 建立 Data Lake Analytics 作業，以及提交作業。 "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 2722a2d72ed90ea0005362563ecaee30750c040a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="706d2-103">使用 Azure 入口網站開始使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="706d2-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="706d2-104">了解如何使用 Azure 入口網站建立 Azure Data Lake Analytics 帳戶、在 [U-SQL](data-lake-analytics-u-sql-get-started.md)中定義作業，以及將作業提交至 Data Lake Analytics 服務。</span><span class="sxs-lookup"><span data-stu-id="706d2-104">Learn how to use the Azure portal to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="706d2-105">如需有關 Data Lake Analytics 的詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="706d2-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="706d2-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="706d2-106">Prerequisites</span></span>

<span data-ttu-id="706d2-107">開始進行本教學課程之前，您必須擁有 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="706d2-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="706d2-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="706d2-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="706d2-109">建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="706d2-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="706d2-110">現在，您會同時建立 Data Lake Analytics 和 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="706d2-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at the same time.</span></span>  <span data-ttu-id="706d2-111">這個步驟很簡單，只需要大約 60 秒即可完成。</span><span class="sxs-lookup"><span data-stu-id="706d2-111">This step is simple and only takes about 60 seconds to finish.</span></span>

1. <span data-ttu-id="706d2-112">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="706d2-112">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="706d2-113">按一下 [新增] >  [資料 + 分析] > [Data Lake Analytics]。</span><span class="sxs-lookup"><span data-stu-id="706d2-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="706d2-114">選取下列項目的值︰</span><span class="sxs-lookup"><span data-stu-id="706d2-114">Select values for the following items:</span></span>
   * <span data-ttu-id="706d2-115">**名稱**：替 Data Lake Analytics 帳戶命名 (只允許小寫字母和數字)。</span><span class="sxs-lookup"><span data-stu-id="706d2-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="706d2-116">**訂用帳戶**：選擇用於分析帳戶的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="706d2-116">**Subscription**: Choose the Azure subscription used for the Analytics account.</span></span>
   * <span data-ttu-id="706d2-117">**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="706d2-117">**Resource Group**.</span></span> <span data-ttu-id="706d2-118">選取現有的 Azure 資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="706d2-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="706d2-119">**位置**。</span><span class="sxs-lookup"><span data-stu-id="706d2-119">**Location**.</span></span> <span data-ttu-id="706d2-120">為 Data Lake Analytics 帳戶選取 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="706d2-120">Select an Azure data center for the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="706d2-121">**Data Lake Store**：請依照指示來建立新的 Data Lake Store 帳戶，或選取現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="706d2-121">**Data Lake Store**: Follow the instruction to create a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="706d2-122">(選擇性) 選取 Data Lake Analytics 帳戶的定價層。</span><span class="sxs-lookup"><span data-stu-id="706d2-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="706d2-123">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="706d2-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="706d2-124">您的第一個 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="706d2-124">Your first U-SQL script</span></span>

<span data-ttu-id="706d2-125">下列文字是很簡單的 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="706d2-125">The following text is a very simple U-SQL script.</span></span> <span data-ttu-id="706d2-126">它會定義指令碼內的小型資料集，然後將該資料集寫入預設的 Data Lake Store，作為名為 `/data.csv` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="706d2-126">All it does is define a small dataset within the script and then write that dataset out to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="706d2-127">提交 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="706d2-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="706d2-128">從 Data Lake Analytics 帳戶中，按一下 [新增作業]。</span><span class="sxs-lookup"><span data-stu-id="706d2-128">From the Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="706d2-129">貼上以上所示的 U-SQL 指令碼文字。</span><span class="sxs-lookup"><span data-stu-id="706d2-129">Paste in the text of the U-SQL script shown above.</span></span> 
3. <span data-ttu-id="706d2-130">按一下 [ **提交作業**]。</span><span class="sxs-lookup"><span data-stu-id="706d2-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="706d2-131">請等候作業狀態變更為 [成功]。</span><span class="sxs-lookup"><span data-stu-id="706d2-131">Wait until the job status changes to **Succeeded**.</span></span>
5. <span data-ttu-id="706d2-132">如果作業失敗，請參閱[監視和移難排解 Data Lake Analytics 作業](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="706d2-132">If the job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="706d2-133">按一下 [輸出] 索引標籤，然後按一下 `data.csv`。</span><span class="sxs-lookup"><span data-stu-id="706d2-133">Click the **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="706d2-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="706d2-134">See also</span></span>

* <span data-ttu-id="706d2-135">若要開始開發 U-SQL 應用程式，請參閱 [使用適用於 Visual Studio 的 Data Lake 工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="706d2-135">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="706d2-136">若要了解 U-SQL，請參閱 [開始使用 Azure Data Lake Analytics U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="706d2-136">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="706d2-137">針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="706d2-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
