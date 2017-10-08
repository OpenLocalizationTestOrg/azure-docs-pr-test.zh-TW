---
title: "資料湖分析配額限制 aaaAzure |Microsoft 文件"
description: "了解如何 tooadjust 並增加配額會限制在 Azure 資料湖分析 (ADLA) 帳戶。"
services: data-lake-analytics
keywords: Azure Data Lake Analytics
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="29585-104">Azure Data Lake Analytics 配額限制</span><span class="sxs-lookup"><span data-stu-id="29585-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="29585-105">了解如何 tooadjust 並增加配額會限制在 Azure 資料湖分析 (ADLA) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="29585-105">Learn how tooadjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="29585-106">了解這些限制可幫助您了解 U-SQL 作業的行為。</span><span class="sxs-lookup"><span data-stu-id="29585-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="29585-107">所有配額限制都是軟性的因此您可以增加觸角 toous hello 最大限制。</span><span class="sxs-lookup"><span data-stu-id="29585-107">All quota limits are soft, so you can increase hello maximum limits by reaching out toous.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="29585-108">Azure 訂用帳戶限制</span><span class="sxs-lookup"><span data-stu-id="29585-108">Azure subscriptions limits</span></span>

<span data-ttu-id="29585-109">**每個訂用帳戶的 ADLA 帳戶最大數目︰**5</span><span class="sxs-lookup"><span data-stu-id="29585-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="29585-110">這是 hello ADLA 帳戶，您可以建立每個訂閱的數目上限。</span><span class="sxs-lookup"><span data-stu-id="29585-110">This is hello maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="29585-111">如果 toocreate 第六個 ADLA 帳戶再試一次，您會收到錯誤 「 您已在訂用帳戶名稱的區域中達到 hello Data Lake Analytics 帳戶允許 (5) 的數目上限 」。</span><span class="sxs-lookup"><span data-stu-id="29585-111">If you try toocreate a sixth ADLA account, you will get an error "You have reached hello maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="29585-112">在此情況下，刪除任何未使用的 ADLA 帳戶，或是聯繫 toous 由[開啟支援票證](#increase-maximum-quota-limits)。</span><span class="sxs-lookup"><span data-stu-id="29585-112">In this case, either delete any unused ADLA accounts, or reach out toous by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="29585-113">ADLA 帳戶限制</span><span class="sxs-lookup"><span data-stu-id="29585-113">ADLA account limits</span></span>

<span data-ttu-id="29585-114">**每個帳戶分析單位 (AU) 的最大數目︰**250</span><span class="sxs-lookup"><span data-stu-id="29585-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="29585-115">這是 hello 可以同時在您的帳戶中執行的澳洲的數目上限。</span><span class="sxs-lookup"><span data-stu-id="29585-115">This is hello maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="29585-116">如果您的所有作業加起來的執行中 AU 總數超過此限制，系統會自動將較新的工作排入佇列。</span><span class="sxs-lookup"><span data-stu-id="29585-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="29585-117">例如：</span><span class="sxs-lookup"><span data-stu-id="29585-117">For example:</span></span>

* <span data-ttu-id="29585-118">如果您有只有一個工作執行與 250 澳洲，當您送出第二個工作它 hello 第一個工作完成之前會等候 hello 工作佇列中。</span><span class="sxs-lookup"><span data-stu-id="29585-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in hello job queue until hello first job completes.</span></span>
* <span data-ttu-id="29585-119">如果您已經有五個執行的作業，而且每個都使用 50 澳洲，當您送出第六個工作需要 20 澳洲它會等候 hello 工作佇列中有 20 澳洲可用。</span><span class="sxs-lookup"><span data-stu-id="29585-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in hello job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="29585-120">**每個帳戶的並行 U-SQL 作業最大數目︰**20</span><span class="sxs-lookup"><span data-stu-id="29585-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="29585-121">這是 hello 可以同時在您的帳戶中執行的作業數目上限。</span><span class="sxs-lookup"><span data-stu-id="29585-121">This is hello maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="29585-122">超過此值，新的工作會自動排入佇列。</span><span class="sxs-lookup"><span data-stu-id="29585-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="29585-123">調整每個帳戶的 ADLA 配額限制</span><span class="sxs-lookup"><span data-stu-id="29585-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="29585-124">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="29585-124">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="29585-125">選擇現有的 ADLA 帳戶。</span><span class="sxs-lookup"><span data-stu-id="29585-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="29585-126">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="29585-126">Click **Properties**.</span></span>
4. <span data-ttu-id="29585-127">調整**平行處理原則**和**並行作業**toosuit 您的需求。</span><span class="sxs-lookup"><span data-stu-id="29585-127">Adjust **Parallelism** and **Concurrent Jobs** toosuit your needs.</span></span>

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="29585-129">增加配額限制上限</span><span class="sxs-lookup"><span data-stu-id="29585-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="29585-130">在 Azure 入口網站中開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="29585-130">Open a support request in Azure Portal.</span></span>

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="29585-133">選取問題類型排序 hello**配額**。</span><span class="sxs-lookup"><span data-stu-id="29585-133">Select hello issue type **Quota**.</span></span>
3. <span data-ttu-id="29585-134">選取您的 [訂用帳戶] \(請確定它不是「試用」的訂用帳戶\)。</span><span class="sxs-lookup"><span data-stu-id="29585-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="29585-135">選取 [Data Lake Analytics] 配額類型。</span><span class="sxs-lookup"><span data-stu-id="29585-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="29585-137">在 hello 問題 刀鋒視窗中，說明您要求的增加數目限制，而且具有**詳細資料**的為何需要這個額外的容量。</span><span class="sxs-lookup"><span data-stu-id="29585-137">In hello problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="29585-139">請確認您的連絡資訊，然後建立 hello 支援要求。</span><span class="sxs-lookup"><span data-stu-id="29585-139">Verify your contact information and create hello support request.</span></span>

<span data-ttu-id="29585-140">Microsoft 會檢閱您的要求，並嘗試您的業務需求儘速 tooaccommodate。</span><span class="sxs-lookup"><span data-stu-id="29585-140">Microsoft reviews your request and tries tooaccommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29585-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="29585-141">Next steps</span></span>

* [<span data-ttu-id="29585-142">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="29585-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="29585-143">使用 Azure PowerShell 管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="29585-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="29585-144">使用 Azure 入口網站監視和疑難排解 Azure Data Lake Analytics 作業</span><span class="sxs-lookup"><span data-stu-id="29585-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
