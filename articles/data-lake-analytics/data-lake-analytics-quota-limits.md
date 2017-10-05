---
title: "Azure Data Lake Analytics 配額限制 | Microsoft Docs"
description: "了解如何調整並提高 Azure Data Lake Analytics (ADLA) 帳戶中的配額限制。"
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
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="d284e-104">Azure Data Lake Analytics 配額限制</span><span class="sxs-lookup"><span data-stu-id="d284e-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="d284e-105">了解如何調整並提高 Azure Data Lake Analytics (ADLA) 帳戶中的配額限制。</span><span class="sxs-lookup"><span data-stu-id="d284e-105">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="d284e-106">了解這些限制可幫助您了解 U-SQL 作業的行為。</span><span class="sxs-lookup"><span data-stu-id="d284e-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="d284e-107">所有配額限制並非強制，因此您可以與我們連絡來增加上限。</span><span class="sxs-lookup"><span data-stu-id="d284e-107">All quota limits are soft, so you can increase the maximum limits by reaching out to us.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="d284e-108">Azure 訂用帳戶限制</span><span class="sxs-lookup"><span data-stu-id="d284e-108">Azure subscriptions limits</span></span>

<span data-ttu-id="d284e-109">**每個訂用帳戶的 ADLA 帳戶最大數目︰**5</span><span class="sxs-lookup"><span data-stu-id="d284e-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="d284e-110">這是每個訂用帳戶您可以建立的 ADLA 帳戶的數目上限。</span><span class="sxs-lookup"><span data-stu-id="d284e-110">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="d284e-111">如果您嘗試建立第六個 ADLA 帳戶，會收到「您已達到訂用帳戶名稱下區域中允許的 Data Lake Analytics 帳戶的數目上限 (5)」錯誤。</span><span class="sxs-lookup"><span data-stu-id="d284e-111">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="d284e-112">在此情況下，您可刪除任何未使用的 ADLA 帳戶，或[建立支援票證](#increase-maximum-quota-limits)與我們聯絡。</span><span class="sxs-lookup"><span data-stu-id="d284e-112">In this case, either delete any unused ADLA accounts, or reach out to us by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="d284e-113">ADLA 帳戶限制</span><span class="sxs-lookup"><span data-stu-id="d284e-113">ADLA account limits</span></span>

<span data-ttu-id="d284e-114">**每個帳戶分析單位 (AU) 的最大數目︰**250</span><span class="sxs-lookup"><span data-stu-id="d284e-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="d284e-115">這是可以同時在您的帳戶中執行的 AU 的最大數目。</span><span class="sxs-lookup"><span data-stu-id="d284e-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="d284e-116">如果您的所有作業加起來的執行中 AU 總數超過此限制，系統會自動將較新的工作排入佇列。</span><span class="sxs-lookup"><span data-stu-id="d284e-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="d284e-117">例如：</span><span class="sxs-lookup"><span data-stu-id="d284e-117">For example:</span></span>

* <span data-ttu-id="d284e-118">如果您只有一個作業使用 250 個 AU 在執行，當您提交第二個作業時，在第一個作業完成之前，第二個作業會在作業佇列中等待。</span><span class="sxs-lookup"><span data-stu-id="d284e-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="d284e-119">如果您已經有五個執行的作業，而且每個都使用 50 AU，當您送出第六個需要 20 AU 的作業時它會在佇列中等到有 20 AU 可使用。</span><span class="sxs-lookup"><span data-stu-id="d284e-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in the job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="d284e-120">**每個帳戶的並行 U-SQL 作業最大數目︰**20</span><span class="sxs-lookup"><span data-stu-id="d284e-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="d284e-121">這是可以同時在您的帳戶中執行之工作的最大數目。</span><span class="sxs-lookup"><span data-stu-id="d284e-121">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="d284e-122">超過此值，新的工作會自動排入佇列。</span><span class="sxs-lookup"><span data-stu-id="d284e-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="d284e-123">調整每個帳戶的 ADLA 配額限制</span><span class="sxs-lookup"><span data-stu-id="d284e-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="d284e-124">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d284e-124">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d284e-125">選擇現有的 ADLA 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d284e-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="d284e-126">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="d284e-126">Click **Properties**.</span></span>
4. <span data-ttu-id="d284e-127">調整 [平行處理原則] 和 [並行工作] 以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="d284e-127">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="d284e-129">增加配額限制上限</span><span class="sxs-lookup"><span data-stu-id="d284e-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="d284e-130">在 Azure 入口網站中開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="d284e-130">Open a support request in Azure Portal.</span></span>

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="d284e-133">選取 [配額] 問題類型。</span><span class="sxs-lookup"><span data-stu-id="d284e-133">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="d284e-134">選取您的 [訂用帳戶] \(請確定它不是「試用」的訂用帳戶\)。</span><span class="sxs-lookup"><span data-stu-id="d284e-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="d284e-135">選取 [Data Lake Analytics] 配額類型。</span><span class="sxs-lookup"><span data-stu-id="d284e-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="d284e-137">在問題刀鋒視窗中，說明您所要增加的限制，以及您為何需要這個額外的容量的**詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="d284e-137">In the problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Azure Data Lake Analytics 入口網站刀鋒視窗](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="d284e-139">確認您的連絡資訊，建立支援要求。</span><span class="sxs-lookup"><span data-stu-id="d284e-139">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="d284e-140">Microsoft 會檢閱您的要求，並嘗試盡速符合您的業務需求。</span><span class="sxs-lookup"><span data-stu-id="d284e-140">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d284e-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d284e-141">Next steps</span></span>

* [<span data-ttu-id="d284e-142">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="d284e-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="d284e-143">使用 Azure PowerShell 管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d284e-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="d284e-144">使用 Azure 入口網站監視和疑難排解 Azure Data Lake Analytics 作業</span><span class="sxs-lookup"><span data-stu-id="d284e-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
