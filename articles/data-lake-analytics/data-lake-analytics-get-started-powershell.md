---
title: "透過 Azure PowerShell 開始使用 Azure Data Lake Analytics | Microsoft Docs"
description: "使用 Azure PowerShell 建立 Data Lake Analytics 帳戶、使用 U-SQL 建立 Data Lake Analytics 作業，以及提交作業。 "
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
ms.openlocfilehash: 4f73e27c733edae658d1ea3bdabe48076328279b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="94180-103">使用 Azure PowerShell 開始使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="94180-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="94180-104">了解如何使用 Azure PowerShell 建立 Azure Data Lake Analytics 帳戶，然後提交和執行 U-SQL 作業。</span><span class="sxs-lookup"><span data-stu-id="94180-104">Learn how to use Azure PowerShell to create Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="94180-105">如需有關 Data Lake Analytics 的詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="94180-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94180-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="94180-106">Prerequisites</span></span>

<span data-ttu-id="94180-107">開始進行本教學課程之前，您必須具備下列資訊：</span><span class="sxs-lookup"><span data-stu-id="94180-107">Before you begin this tutorial, you must have the following information:</span></span>

* <span data-ttu-id="94180-108">**Azure Data Lake Analytics 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="94180-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="94180-109">請參閱[開始使用 Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal)。</span><span class="sxs-lookup"><span data-stu-id="94180-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="94180-110">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="94180-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="94180-111">請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="94180-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="94180-112">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="94180-112">Log in to Azure</span></span>

<span data-ttu-id="94180-113">本教學課程假設您已熟悉如何使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="94180-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="94180-114">特別是，您需要了解如何登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="94180-114">In particular, you need to know how to log in to Azure.</span></span> <span data-ttu-id="94180-115">如果您需要協助，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="94180-115">See the [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="94180-116">若要使用訂用帳戶名稱登入：</span><span class="sxs-lookup"><span data-stu-id="94180-116">To log in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="94180-117">除了訂用帳戶名稱之外，您也可以使用訂用帳戶識別碼來登入：</span><span class="sxs-lookup"><span data-stu-id="94180-117">Instead of the subscription name, you can also use a subscription id to log in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="94180-118">如果成功，這個命令的輸出看起來會類似下列文字：</span><span class="sxs-lookup"><span data-stu-id="94180-118">If  successful, the output of this command looks like the following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-the-tutorial"></a><span data-ttu-id="94180-119">準備教學課程</span><span class="sxs-lookup"><span data-stu-id="94180-119">Preparing for the tutorial</span></span>

<span data-ttu-id="94180-120">本教學課程中的 PowerShell 程式碼片段會使用這些變數來儲存此資訊：</span><span class="sxs-lookup"><span data-stu-id="94180-120">The PowerShell snippets in this tutorial use these variables to store this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="94180-121">取得 Data Lake Analytics 帳戶的相關資訊</span><span class="sxs-lookup"><span data-stu-id="94180-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="94180-122">提交 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="94180-122">Submit a U-SQL job</span></span>

<span data-ttu-id="94180-123">建立 PowerShell 變數，可保留 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="94180-123">Create a PowerShell variable to hold the U-SQL script.</span></span>

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
    TO "/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="94180-124">提交指令碼。</span><span class="sxs-lookup"><span data-stu-id="94180-124">Submit the script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="94180-125">或者，您可以將指令碼儲存為檔案，並使用下列命令提交：</span><span class="sxs-lookup"><span data-stu-id="94180-125">Alternatively, you could save the script as a file and submit with the following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="94180-126">取得特定作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="94180-126">Get the status of a specific job.</span></span> <span data-ttu-id="94180-127">繼續使用這個 Cmdlet，直到您看到作業完成為止。</span><span class="sxs-lookup"><span data-stu-id="94180-127">Keep using this cmdlet until you see the job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="94180-128">您可以使用 Wait-AdlJob Cmdlet，而不需在作業完成前反覆呼叫 Get-AdlAnalyticsJob。</span><span class="sxs-lookup"><span data-stu-id="94180-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use the Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="94180-129">下載輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="94180-129">Download the output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="94180-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="94180-130">See also</span></span>
* <span data-ttu-id="94180-131">若要使用其他工具檢視同一個教學課程，請按一下頁面最上方的索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="94180-131">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="94180-132">若要了解 U-SQL，請參閱 [開始使用 Azure Data Lake Analytics U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="94180-132">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="94180-133">針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="94180-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
