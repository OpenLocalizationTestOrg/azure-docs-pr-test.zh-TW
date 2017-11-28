---
title: "aaaUse Azure Backup tooreplace 磁帶基礎結構 |Microsoft 文件"
description: "了解如何 Azure Backup 會提供可讓您的磁帶類似的語意 toobackup 和還原在 Azure 中的資料"
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
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="e27ca-103">移動您的長期存放裝置從磁帶 toohello Azure 雲端</span><span class="sxs-lookup"><span data-stu-id="e27ca-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="e27ca-104">使用 Azure 備份和 System Center Data Protection Manager 的客戶可以進行下列操作：</span><span class="sxs-lookup"><span data-stu-id="e27ca-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="e27ca-105">備份在其最符合組織需求的 hello 排程中的資料。</span><span class="sxs-lookup"><span data-stu-id="e27ca-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="e27ca-106">較長時間保留 hello 備份資料</span><span class="sxs-lookup"><span data-stu-id="e27ca-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="e27ca-107">讓 Azure (而非磁帶) 成為長期保留需求的一部分。</span><span class="sxs-lookup"><span data-stu-id="e27ca-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="e27ca-108">此文章說明客戶如何啟用備份和保留原則。</span><span class="sxs-lookup"><span data-stu-id="e27ca-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="e27ca-109">使用磁帶 tooaddress 客戶現在有功能強大且可行的替代方式，與 hello 可用性，這項功能需要其長期-長期保留。</span><span class="sxs-lookup"><span data-stu-id="e27ca-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="e27ca-110">hello 功能在 hello 最新版本中的 hello Azure Backup (所提供[這裡](http://aka.ms/azurebackup_agent))。</span><span class="sxs-lookup"><span data-stu-id="e27ca-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="e27ca-111">System Center DPM 客戶必須更新，才能使用 DPM 和 DPM 2012 R2 UR5 至少 hello Azure 備份服務。</span><span class="sxs-lookup"><span data-stu-id="e27ca-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="e27ca-112">Hello 備份排程是什麼？</span><span class="sxs-lookup"><span data-stu-id="e27ca-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="e27ca-113">hello 備份排程指出 hello hello 備份作業頻率。</span><span class="sxs-lookup"><span data-stu-id="e27ca-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="e27ca-114">例如，hello 遵循螢幕中的 hello 設定會指出備份會執行每日下午 6 點，並在午夜。</span><span class="sxs-lookup"><span data-stu-id="e27ca-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![每日排程](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="e27ca-116">客戶也可以排程每週備份。</span><span class="sxs-lookup"><span data-stu-id="e27ca-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="e27ca-117">比方說，hello 設定在 hello 遵循螢幕指示，備份每個替代星期日 & 星期三上午 9:30 和 1:00 AM。</span><span class="sxs-lookup"><span data-stu-id="e27ca-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![每週排程](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="e27ca-119">Hello 保留原則是什麼？</span><span class="sxs-lookup"><span data-stu-id="e27ca-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="e27ca-120">hello 保留原則會指定必須儲存 hello 備份 hello 持續時間。</span><span class="sxs-lookup"><span data-stu-id="e27ca-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="e27ca-121">而不是只指定 「 一般原則 」 的所有備份點時，客戶可以指定不同的保留原則以 hello 備份時。</span><span class="sxs-lookup"><span data-stu-id="e27ca-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="e27ca-122">例如，hello 備份點採取，每天會做為操作的復原點，會保留 90 天。</span><span class="sxs-lookup"><span data-stu-id="e27ca-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="e27ca-123">在 hello 基於稽核目的每季結束時採取的 hello 備份點保留較長時間。</span><span class="sxs-lookup"><span data-stu-id="e27ca-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![保留原則](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="e27ca-125">hello 的此原則中指定 「 保留點 」 總數是 90 （每日點） 加上 40 (分別指派 10 年的季) = 130。</span><span class="sxs-lookup"><span data-stu-id="e27ca-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="e27ca-126">範例 – 將兩者綜合比較</span><span class="sxs-lookup"><span data-stu-id="e27ca-126">Example – Putting both together</span></span>
![範例畫面](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="e27ca-128">**每日的保留原則**：每日所進行的備份會儲存 7 天。</span><span class="sxs-lookup"><span data-stu-id="e27ca-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="e27ca-129">**每週的保留原則**：每天午夜和星期六下午 6 點所進行的備份會保留 4 週</span><span class="sxs-lookup"><span data-stu-id="e27ca-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="e27ca-130">**每月保留原則**： 在午夜到下午 6 hello 上每個月的最後一個星期六的備份會保留 12 個月</span><span class="sxs-lookup"><span data-stu-id="e27ca-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="e27ca-131">**每年保留原則**: hello 午夜建立的每年 3 月的最後一個星期六的備份會保留為 10 年</span><span class="sxs-lookup"><span data-stu-id="e27ca-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="e27ca-132">hello 「 保留點 」 的總數 （客戶可以還原資料點） hello 在上圖的計算方式如下：</span><span class="sxs-lookup"><span data-stu-id="e27ca-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="e27ca-133">7 天中每天 2 個保留點 = 14 個復原點</span><span class="sxs-lookup"><span data-stu-id="e27ca-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="e27ca-134">4 週中每週 2 個保留點 = 8 個復原點</span><span class="sxs-lookup"><span data-stu-id="e27ca-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="e27ca-135">12 個月中每月 2 個保留點 = 24 個復原點</span><span class="sxs-lookup"><span data-stu-id="e27ca-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="e27ca-136">10 年中每年 1 個保留點 = 10 個復原點</span><span class="sxs-lookup"><span data-stu-id="e27ca-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="e27ca-137">hello 總數的復原點是 56。</span><span class="sxs-lookup"><span data-stu-id="e27ca-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="e27ca-138">Azure 備份對於復原點數目沒有限制。</span><span class="sxs-lookup"><span data-stu-id="e27ca-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="e27ca-139">進階組態</span><span class="sxs-lookup"><span data-stu-id="e27ca-139">Advanced configuration</span></span>
<span data-ttu-id="e27ca-140">依序按一下**修改**hello 前面螢幕，在客戶會有進一步彈性，指定保留排程。</span><span class="sxs-lookup"><span data-stu-id="e27ca-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![修改](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="e27ca-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e27ca-142">Next Steps</span></span>
<span data-ttu-id="e27ca-143">如需有關 Azure Backup 的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e27ca-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="e27ca-144">簡介 tooAzure 備份</span><span class="sxs-lookup"><span data-stu-id="e27ca-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="e27ca-145">試用 Azure 備份</span><span class="sxs-lookup"><span data-stu-id="e27ca-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
