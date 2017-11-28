---
title: "開始使用 Azure PowerShell 的 Azure Data Lake Analytics aaaGet |Microsoft 文件"
description: "使用 Azure PowerShell toocreate Data Lake Analytics 帳戶、 建立使用 U SQL Data Lake Analytics 工作和送出 hello 作業。 "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="f3d62-103">使用 Azure PowerShell 開始使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f3d62-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="f3d62-104">了解如何 toouse Azure PowerShell toocreate Azure Data Lake Analytics 帳戶，然後送出並執行 U SQL 作業。</span><span class="sxs-lookup"><span data-stu-id="f3d62-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="f3d62-105">如需有關 Data Lake Analytics 的詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d62-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3d62-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="f3d62-106">Prerequisites</span></span>

<span data-ttu-id="f3d62-107">開始本教學課程之前，您必須擁有下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3d62-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="f3d62-108">**Azure Data Lake Analytics 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f3d62-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="f3d62-109">請參閱[開始使用 Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal)。</span><span class="sxs-lookup"><span data-stu-id="f3d62-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="f3d62-110">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="f3d62-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="f3d62-111">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f3d62-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="f3d62-112">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="f3d62-112">Log in tooAzure</span></span>

<span data-ttu-id="f3d62-113">本教學課程假設您已熟悉如何使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f3d62-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="f3d62-114">特別是，您需要 tooknow 如何 toolog tooAzure 中的。</span><span class="sxs-lookup"><span data-stu-id="f3d62-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="f3d62-115">請參閱 hello[開始使用 Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps)如果您需要協助。</span><span class="sxs-lookup"><span data-stu-id="f3d62-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="f3d62-116">toolog 入訂用帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="f3d62-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="f3d62-117">而不是 hello 訂用帳戶名稱，您也可以使用訂用帳戶 id toolog 中：</span><span class="sxs-lookup"><span data-stu-id="f3d62-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="f3d62-118">如果成功，這個命令的 hello 輸出看起來 hello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="f3d62-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="f3d62-119">準備 hello 教學課程</span><span class="sxs-lookup"><span data-stu-id="f3d62-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="f3d62-120">在此教學課程中的 hello PowerShell 程式碼片段會使用這些變數 toostore 這項資訊：</span><span class="sxs-lookup"><span data-stu-id="f3d62-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="f3d62-121">取得 Data Lake Analytics 帳戶的相關資訊</span><span class="sxs-lookup"><span data-stu-id="f3d62-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="f3d62-122">提交 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="f3d62-122">Submit a U-SQL job</span></span>

<span data-ttu-id="f3d62-123">建立 PowerShell 變數 toohold hello U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3d62-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

```
$script = @"
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

"@
```

<span data-ttu-id="f3d62-124">送出 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f3d62-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="f3d62-125">或者，您無法將 hello 指令碼儲存到檔案，並送出 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="f3d62-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="f3d62-126">取得 hello 特定作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="f3d62-126">Get hello status of a specific job.</span></span> <span data-ttu-id="f3d62-127">繼續使用這個指令程式，直到您看到 hello 工作完成為止。</span><span class="sxs-lookup"><span data-stu-id="f3d62-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="f3d62-128">而不是反覆呼叫 Get AdlAnalyticsJob，直到工作完成，您可以使用 hello 等候 AdlJob cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f3d62-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="f3d62-129">下載 hello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="f3d62-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="f3d62-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f3d62-130">See also</span></span>
* <span data-ttu-id="f3d62-131">toosee hello 相同教學課程中使用其他工具中，按一下在 hello hello 頁面最上方的 hello 索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="f3d62-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="f3d62-132">toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d62-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="f3d62-133">針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="f3d62-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
