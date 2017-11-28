---
title: "開始使用 Azure 入口網站的 Azure Data Lake Analytics 使用 aaaGet |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站 toocreate Data Lake Analytics 帳戶中建立使用 U SQL Data Lake Analytics 工作並送出 hello 作業。 "
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
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="4214c-103">使用 Azure 入口網站開始使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4214c-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="4214c-104">了解如何 toouse hello Azure 入口網站 toocreate Azure Data Lake Analytics 帳戶，定義中的工作[U-SQL](data-lake-analytics-u-sql-get-started.md)，並提交作業 toohello 資料湖分析服務。</span><span class="sxs-lookup"><span data-stu-id="4214c-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="4214c-105">如需有關 Data Lake Analytics 的詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4214c-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4214c-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="4214c-106">Prerequisites</span></span>

<span data-ttu-id="4214c-107">開始進行本教學課程之前，您必須擁有 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="4214c-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="4214c-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="4214c-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="4214c-109">建立 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="4214c-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="4214c-110">現在，您會建立 Data Lake Analytics 並 Data Lake Store 帳戶 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="4214c-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="4214c-111">這個步驟很簡單，而且只需要 60 秒 toofinish。</span><span class="sxs-lookup"><span data-stu-id="4214c-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="4214c-112">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4214c-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4214c-113">按一下 [新增] >  [資料 + 分析] > [Data Lake Analytics]。</span><span class="sxs-lookup"><span data-stu-id="4214c-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="4214c-114">選取下列項目 hello 的值：</span><span class="sxs-lookup"><span data-stu-id="4214c-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="4214c-115">**名稱**：替 Data Lake Analytics 帳戶命名 (只允許小寫字母和數字)。</span><span class="sxs-lookup"><span data-stu-id="4214c-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="4214c-116">**訂用帳戶**： 選擇 hello 用於 hello Analytics 帳戶的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4214c-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="4214c-117">**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="4214c-117">**Resource Group**.</span></span> <span data-ttu-id="4214c-118">選取現有的 Azure 資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="4214c-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="4214c-119">**位置**。</span><span class="sxs-lookup"><span data-stu-id="4214c-119">**Location**.</span></span> <span data-ttu-id="4214c-120">選取 Azure 資料中心 hello Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4214c-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="4214c-121">**Data Lake Store**： 遵循 hello 指令 toocreate 新的 Data Lake Store 帳戶，或選取現有的我的最愛。</span><span class="sxs-lookup"><span data-stu-id="4214c-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="4214c-122">(選擇性) 選取 Data Lake Analytics 帳戶的定價層。</span><span class="sxs-lookup"><span data-stu-id="4214c-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="4214c-123">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4214c-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="4214c-124">您的第一個 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="4214c-124">Your first U-SQL script</span></span>

<span data-ttu-id="4214c-125">下列文字的 hello 是非常簡單的 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4214c-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="4214c-126">它會定義 hello 指令碼內的小型資料集，並接著寫為名的檔案中的 toohello 預設 Data Lake Store 出該資料集`/data.csv`。</span><span class="sxs-lookup"><span data-stu-id="4214c-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="4214c-127">提交 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="4214c-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="4214c-128">從 hello Data Lake Analytics 帳戶中，按一下 **新工作**。</span><span class="sxs-lookup"><span data-stu-id="4214c-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="4214c-129">如上所示的 U-SQL 指令碼貼上 hello hello 文字中。</span><span class="sxs-lookup"><span data-stu-id="4214c-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="4214c-130">按一下 [ **提交作業**]。</span><span class="sxs-lookup"><span data-stu-id="4214c-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="4214c-131">等候直到在 hello 作業狀態變更太**Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="4214c-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="4214c-132">如果 hello 作業失敗，請參閱[監視和疑難排解資料湖分析作業](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="4214c-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="4214c-133">按一下 hello**輸出**索引標籤，然後再按一下`data.csv`。</span><span class="sxs-lookup"><span data-stu-id="4214c-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="4214c-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4214c-134">See also</span></span>

* <span data-ttu-id="4214c-135">tooget 開始開發 U-SQL 應用程式，請參閱[使用 Data Lake Tools for Visual Studio 的開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="4214c-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="4214c-136">toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="4214c-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="4214c-137">針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="4214c-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
