---
title: "使用 Azure 備份來取代您的磁帶基礎結構 | Microsoft Docs"
description: "了解 Azure 備份如何提供可讓您在 Azure 中備份和還原資料的磁帶式語意"
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0f3152daf5f91f7c9e540797bf09b21969d2d33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="9960f-103">將您的長期儲存空間從磁帶移至 Azure 雲端</span><span class="sxs-lookup"><span data-stu-id="9960f-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="9960f-104">使用 Azure 備份和 System Center Data Protection Manager 的客戶可以進行下列操作：</span><span class="sxs-lookup"><span data-stu-id="9960f-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="9960f-105">依照最適合組織需求的排程備份資料。</span><span class="sxs-lookup"><span data-stu-id="9960f-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="9960f-106">長期保留備份資料</span><span class="sxs-lookup"><span data-stu-id="9960f-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="9960f-107">讓 Azure (而非磁帶) 成為長期保留需求的一部分。</span><span class="sxs-lookup"><span data-stu-id="9960f-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="9960f-108">此文章說明客戶如何啟用備份和保留原則。</span><span class="sxs-lookup"><span data-stu-id="9960f-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="9960f-109">使用磁帶處理長期保留需求的客戶，透過此功能的可用性現在擁有功能強大且可行的替代方案。</span><span class="sxs-lookup"><span data-stu-id="9960f-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="9960f-110">最新版的 Azure 備份已啟用此功能 (可從 [這裡](http://aka.ms/azurebackup_agent)取得)。</span><span class="sxs-lookup"><span data-stu-id="9960f-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="9960f-111">System Center DPM 客戶至少必須更新為 DPM 2012 R2 UR5，才能搭配使用 DPM 與 Azure 備份服務。</span><span class="sxs-lookup"><span data-stu-id="9960f-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="9960f-112">什麼是備份排程？</span><span class="sxs-lookup"><span data-stu-id="9960f-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="9960f-113">備份排程會指出備份作業的頻率。</span><span class="sxs-lookup"><span data-stu-id="9960f-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="9960f-114">例如，下列畫面中的設定指出備份將於每日下午 6 點和午夜執行。</span><span class="sxs-lookup"><span data-stu-id="9960f-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![每日排程](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="9960f-116">客戶也可以排程每週備份。</span><span class="sxs-lookup"><span data-stu-id="9960f-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="9960f-117">例如，下列畫面中的設定指出備份將於每隔兩週的星期日和星期三上午 9:30 和 1:00 執行。</span><span class="sxs-lookup"><span data-stu-id="9960f-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![每週排程](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="9960f-119">保留原則為何？</span><span class="sxs-lookup"><span data-stu-id="9960f-119">What is the Retention Policy?</span></span>
<span data-ttu-id="9960f-120">保留原則會指定備份必須儲存的期間。</span><span class="sxs-lookup"><span data-stu-id="9960f-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="9960f-121">除了僅針對所有備份點指定「一般原則」之外，客戶可以指定在進行備份時根據不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="9960f-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="9960f-122">例如，每日取得的備份點 (可充當作業復原點) 可保留 90 天。</span><span class="sxs-lookup"><span data-stu-id="9960f-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="9960f-123">在每一季結尾所取得的備份點 (供稽核之用) 可能需要保留較長的時間。</span><span class="sxs-lookup"><span data-stu-id="9960f-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![保留原則](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="9960f-125">此原則中指定的「保留點」總數是 90 (每日保留點) + 40 (每季一點，連續 10 年) = 130。</span><span class="sxs-lookup"><span data-stu-id="9960f-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="9960f-126">範例 – 將兩者綜合比較</span><span class="sxs-lookup"><span data-stu-id="9960f-126">Example – Putting both together</span></span>
![範例畫面](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="9960f-128">**每日的保留原則**：每日所進行的備份會儲存 7 天。</span><span class="sxs-lookup"><span data-stu-id="9960f-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="9960f-129">**每週的保留原則**：每天午夜和星期六下午 6 點所進行的備份會保留 4 週</span><span class="sxs-lookup"><span data-stu-id="9960f-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="9960f-130">**每月的保留原則**：每月最後一個星期六午夜和下午 6 點所進行的備份會保留 12 個月</span><span class="sxs-lookup"><span data-stu-id="9960f-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="9960f-131">**每年的保留原則**：每年三月最後一個星期六午夜所進行的備份會保留 10 年</span><span class="sxs-lookup"><span data-stu-id="9960f-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="9960f-132">上圖中計算「保留點」總數 (客戶可從該保留點還原資料) 的方式如下：</span><span class="sxs-lookup"><span data-stu-id="9960f-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="9960f-133">7 天中每天 2 個保留點 = 14 個復原點</span><span class="sxs-lookup"><span data-stu-id="9960f-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="9960f-134">4 週中每週 2 個保留點 = 8 個復原點</span><span class="sxs-lookup"><span data-stu-id="9960f-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="9960f-135">12 個月中每月 2 個保留點 = 24 個復原點</span><span class="sxs-lookup"><span data-stu-id="9960f-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="9960f-136">10 年中每年 1 個保留點 = 10 個復原點</span><span class="sxs-lookup"><span data-stu-id="9960f-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="9960f-137">因此復原點的總數是 56。</span><span class="sxs-lookup"><span data-stu-id="9960f-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="9960f-138">Azure 備份對於復原點數目沒有限制。</span><span class="sxs-lookup"><span data-stu-id="9960f-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="9960f-139">進階組態</span><span class="sxs-lookup"><span data-stu-id="9960f-139">Advanced configuration</span></span>
<span data-ttu-id="9960f-140">按一下上方畫面中的 [修改]  ，客戶在指定保留排程時擁有更進一步的彈性。</span><span class="sxs-lookup"><span data-stu-id="9960f-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![修改](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="9960f-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9960f-142">Next Steps</span></span>
<span data-ttu-id="9960f-143">如需有關 Azure Backup 的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9960f-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="9960f-144">Azure 備份的簡介</span><span class="sxs-lookup"><span data-stu-id="9960f-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="9960f-145">試用 Azure 備份</span><span class="sxs-lookup"><span data-stu-id="9960f-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
