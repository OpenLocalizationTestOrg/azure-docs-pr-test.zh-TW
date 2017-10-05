---
title: "為 Azure 備份的檔案和資料夾備份速度緩慢問題進行疑難排解 | Microsoft Docs"
description: "提供疑難排解指導方針，以協助您診斷 Azure 備份效能問題的原因"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 1688846957df3fbf0df747a6cd2a94b481d851b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a><span data-ttu-id="ea5f8-103">疑難排解 Azure 備份的檔案和資料夾備份速度緩慢問題</span><span class="sxs-lookup"><span data-stu-id="ea5f8-103">Troubleshoot slow backup of files and folders in Azure Backup</span></span>
<span data-ttu-id="ea5f8-104">這篇文章提供疑難排解指引，可協助您診斷當您使用 Azure 備份時，檔案與資料夾備份效能緩慢的原因。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-104">This article provides troubleshooting guidance to help you diagnose the cause of slow backup performance for files and folders when you're using Azure Backup.</span></span> <span data-ttu-id="ea5f8-105">當您使用 Azure 備份代理程式來備份檔案時，備份處理程序進行的時間可能比預期的還要久。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-105">When you use the Azure Backup agent to back up files, the backup process might take longer than expected.</span></span> <span data-ttu-id="ea5f8-106">此延遲可能是因為下列一或多個原因所造成：</span><span class="sxs-lookup"><span data-stu-id="ea5f8-106">This delay might be caused by one or more of the following:</span></span>

* [<span data-ttu-id="ea5f8-107">正在備份的電腦有效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-107">There are performance bottlenecks on the computer that’s being backed up.</span></span>](#cause1)
* [<span data-ttu-id="ea5f8-108">有其他處理程序或防毒軟體在干擾 Azure 備份處理程序。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-108">Another process or antivirus software is interfering with the Azure Backup process.</span></span>](#cause2)
* [<span data-ttu-id="ea5f8-109">備份代理程式是在 Azure 虛擬機器 (VM) 上執行。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-109">The Backup agent is running on an Azure virtual machine (VM).</span></span>](#cause3)  
* [<span data-ttu-id="ea5f8-110">您正在備份大量 (數百萬計) 的檔案。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-110">You're backing up a large number (millions) of files.</span></span>](#cause4)

<span data-ttu-id="ea5f8-111">在開始對問題進行疑難排解之前，建議您下載並安裝 [最新版的 Azure 備份代理程式](http://aka.ms/azurebackup_agent)。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-111">Before you start troubleshooting issues, we recommend that you download and install the [latest Azure Backup agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="ea5f8-112">我們會經常更新備份代理程式，以修正各種問題、新增功能和改善效能。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-112">We make frequent updates to the Backup agent to fix various issues, add features, and improve performance.</span></span>

<span data-ttu-id="ea5f8-113">我們也強烈建議您檢閱 [Azure 備份服務常見問題集](backup-azure-backup-faq.md) ，以確定所遇到的問題並非任何常見的組態問題。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-113">We also strongly recommend that you review the [Azure Backup service FAQ](backup-azure-backup-faq.md) to make sure you're not experiencing any of the common configuration issues.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-the-computer"></a><span data-ttu-id="ea5f8-114">原因：電腦的效能瓶頸</span><span class="sxs-lookup"><span data-stu-id="ea5f8-114">Cause: Performance bottlenecks on the computer</span></span>
<span data-ttu-id="ea5f8-115">所備份電腦上的瓶頸可能會造成延遲。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-115">Bottlenecks on the computer that's being backed up can cause delays.</span></span> <span data-ttu-id="ea5f8-116">例如，電腦讀取或寫入磁碟的能力，或者透過網路傳送資料的可用頻寬，都可能造成瓶頸。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-116">For example, the computer's ability to read or write to disk, or available bandwidth to send data over the network, can cause bottlenecks.</span></span>

<span data-ttu-id="ea5f8-117">Windows 提供了稱為 [效能監視器](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) (Perfmon) 的內建工具，以偵測這些瓶頸。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-117">Windows provides a built-in tool that's called [Performance Monitor](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) (Perfmon) to detect these bottlenecks.</span></span>

<span data-ttu-id="ea5f8-118">以下是能幫助您診斷最佳化備份瓶頸的一些效能計數器和範圍。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-118">Here are some performance counters and ranges that can be helpful in diagnosing bottlenecks for optimal backups.</span></span>

| <span data-ttu-id="ea5f8-119">計數器</span><span class="sxs-lookup"><span data-stu-id="ea5f8-119">Counter</span></span> | <span data-ttu-id="ea5f8-120">狀態</span><span class="sxs-lookup"><span data-stu-id="ea5f8-120">Status</span></span> |
| --- | --- |
| <span data-ttu-id="ea5f8-121">邏輯磁碟 (實體磁碟)--% 閒置</span><span class="sxs-lookup"><span data-stu-id="ea5f8-121">Logical Disk(Physical Disk)--%idle</span></span> |<span data-ttu-id="ea5f8-122">• 100% 閒置至 50% 閒置 = 狀況良好</span><span class="sxs-lookup"><span data-stu-id="ea5f8-122">• 100% idle to 50% idle = Healthy</span></span></br><span data-ttu-id="ea5f8-123">• 49% 閒置至 20% 閒置 = 警告或監視</span><span class="sxs-lookup"><span data-stu-id="ea5f8-123">• 49% idle to 20% idle = Warning or Monitor</span></span></br><span data-ttu-id="ea5f8-124">• 19% 閒置至 0% 閒置 = 重大或超出規範</span><span class="sxs-lookup"><span data-stu-id="ea5f8-124">• 19% idle to 0% idle = Critical or Out of Spec</span></span> |
| <span data-ttu-id="ea5f8-125">邏輯磁碟 (實體磁碟)--% 平均</span><span class="sxs-lookup"><span data-stu-id="ea5f8-125">Logical Disk(Physical Disk)--%Avg.</span></span> <span data-ttu-id="ea5f8-126">磁碟的讀取或寫入秒數</span><span class="sxs-lookup"><span data-stu-id="ea5f8-126">Disk Sec Read or Write</span></span> |<span data-ttu-id="ea5f8-127">• 0.001 毫秒到 0.015 毫秒 = 狀況良好</span><span class="sxs-lookup"><span data-stu-id="ea5f8-127">• 0.001 ms to 0.015 ms  = Healthy</span></span></br><span data-ttu-id="ea5f8-128">• 0.015 毫秒到 0.025 毫秒 = 警告或監視</span><span class="sxs-lookup"><span data-stu-id="ea5f8-128">• 0.015 ms to 0.025 ms = Warning or Monitor</span></span></br><span data-ttu-id="ea5f8-129">• 0.026 毫秒或更長 = 嚴重或超出規範</span><span class="sxs-lookup"><span data-stu-id="ea5f8-129">• 0.026 ms or longer = Critical or Out of Spec</span></span> |
| <span data-ttu-id="ea5f8-130">邏輯磁碟 (實體磁碟)--(所有執行個體) 目前的磁碟佇列長度</span><span class="sxs-lookup"><span data-stu-id="ea5f8-130">Logical Disk(Physical Disk)--Current Disk Queue Length (for all instances)</span></span> |<span data-ttu-id="ea5f8-131">80 個要求超過 6 分鐘</span><span class="sxs-lookup"><span data-stu-id="ea5f8-131">80 requests for more than 6 minutes</span></span> |
| <span data-ttu-id="ea5f8-132">記憶體--集區未分頁位元組</span><span class="sxs-lookup"><span data-stu-id="ea5f8-132">Memory--Pool Non Paged Bytes</span></span> |<span data-ttu-id="ea5f8-133">• 耗用不到 60% 集區 = 狀況良好</span><span class="sxs-lookup"><span data-stu-id="ea5f8-133">• Less than 60% of pool consumed = Healthy</span></span><br><span data-ttu-id="ea5f8-134">• 耗用 61% 到 80% 集區 = 警告或監視</span><span class="sxs-lookup"><span data-stu-id="ea5f8-134">• 61% to 80% of pool consumed = Warning or Monitor</span></span></br><span data-ttu-id="ea5f8-135">• 耗用超過 80% 集區 = 重大或超出規範</span><span class="sxs-lookup"><span data-stu-id="ea5f8-135">• Greater than 80% pool consumed = Critical or Out of Spec</span></span> |
| <span data-ttu-id="ea5f8-136">記憶體--集區分頁位元組</span><span class="sxs-lookup"><span data-stu-id="ea5f8-136">Memory--Pool Paged Bytes</span></span> |<span data-ttu-id="ea5f8-137">• 耗用不到 60% 集區 = 狀況良好</span><span class="sxs-lookup"><span data-stu-id="ea5f8-137">• Less than 60% of pool consumed = Healthy</span></span></br><span data-ttu-id="ea5f8-138">• 耗用 61% 到 80% 集區 = 警告或監視</span><span class="sxs-lookup"><span data-stu-id="ea5f8-138">• 61% to 80% of pool consumed = Warning or Monitor</span></span></br><span data-ttu-id="ea5f8-139">• 耗用超過 80% 集區 = 重大或超出規範</span><span class="sxs-lookup"><span data-stu-id="ea5f8-139">• Greater than 80% pool consumed = Critical or Out of Spec</span></span> |
| <span data-ttu-id="ea5f8-140">記憶體--可用 MB 數</span><span class="sxs-lookup"><span data-stu-id="ea5f8-140">Memory--Available Megabytes</span></span> |<span data-ttu-id="ea5f8-141">• 50% 以上的可用記憶體可供使用 = 狀況良好</span><span class="sxs-lookup"><span data-stu-id="ea5f8-141">• 50% of free memory available or more = Healthy</span></span></br><span data-ttu-id="ea5f8-142">• 25% 的可用記憶體可供使用 = 監視</span><span class="sxs-lookup"><span data-stu-id="ea5f8-142">• 25% of free memory available = Monitor</span></span></br><span data-ttu-id="ea5f8-143">• 10% 的可用記憶體可供使用 = 警告</span><span class="sxs-lookup"><span data-stu-id="ea5f8-143">• 10% of free memory available = Warning</span></span></br><span data-ttu-id="ea5f8-144">• 不到 100 MB 或 5% 的可用記憶體可供使用 = 重大或超出規範</span><span class="sxs-lookup"><span data-stu-id="ea5f8-144">• Less than 100 MB or 5% of free memory available = Critical or Out of Spec</span></span> |
| <span data-ttu-id="ea5f8-145">處理器--\% 處理器時間 (所有執行個體)</span><span class="sxs-lookup"><span data-stu-id="ea5f8-145">Processor--\%Processor Time (all instances)</span></span> |<span data-ttu-id="ea5f8-146">• 已消耗低於 60% = 狀況良好</span><span class="sxs-lookup"><span data-stu-id="ea5f8-146">• Less than 60% consumed = Healthy</span></span></br><span data-ttu-id="ea5f8-147">• 已消耗 61% 到 90% = 監視或警告</span><span class="sxs-lookup"><span data-stu-id="ea5f8-147">• 61% to 90% consumed = Monitor or Caution</span></span></br><span data-ttu-id="ea5f8-148">• 已消耗 91% 到 100% = 嚴重</span><span class="sxs-lookup"><span data-stu-id="ea5f8-148">• 91% to 100% consumed = Critical</span></span> |

> [!NOTE]
> <span data-ttu-id="ea5f8-149">如果您判斷是基礎結構問題，我們建議您定期執行磁碟重組以提升效能。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-149">If you determine that the infrastructure is the culprit, we recommend that you defragment the disks regularly for better performance.</span></span>
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a><span data-ttu-id="ea5f8-150">原因：有其他處理程序或防毒軟體在干擾 Azure 備份</span><span class="sxs-lookup"><span data-stu-id="ea5f8-150">Cause: Another process or antivirus software interfering with Azure Backup</span></span>
<span data-ttu-id="ea5f8-151">我們曾看過許多例子，Windows 系統中的其他處理程序會對 Azure 備份代理程式處理程序的效能造成不良影響。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-151">We've seen several instances where other processes in the Windows system have negatively affected performance of the Azure Backup agent process.</span></span> <span data-ttu-id="ea5f8-152">例如，如果您同時使用 Azure 備份代理程式和其他程式來備份資料，或是如果防毒軟體正在執行因而鎖定了要備份的檔案，檔案有多個鎖定可能會造成爭用情形。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-152">For example, if you use both the Azure Backup agent and another program to back up data, or if antivirus software is running and has a lock on files to be backed up, the multiple locks on files might cause contention.</span></span> <span data-ttu-id="ea5f8-153">在此情況下，備份可能會失敗，或作業執行時間可能會比預期的還要久。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-153">In this situation, the backup might fail, or the job might take longer than expected.</span></span>

<span data-ttu-id="ea5f8-154">此案例的最佳建議是關閉其他備份程式，以查看 Azure 備份代理程式的備份時間是否有變化。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-154">The best recommendation in this scenario is to turn off the other backup program to see whether the backup time for the Azure Backup agent changes.</span></span> <span data-ttu-id="ea5f8-155">通常只要確定多個備份作業不會在同一時間執行，就足以防止作業彼此干擾。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-155">Usually, making sure that multiple backup jobs are not running at the same time is sufficient to prevent them from affecting each other.</span></span>

<span data-ttu-id="ea5f8-156">至於防毒程式，我們建議您排除下列檔案和位置︰</span><span class="sxs-lookup"><span data-stu-id="ea5f8-156">For antivirus programs, we recommend that you exclude the following files and locations:</span></span>

* <span data-ttu-id="ea5f8-157">將 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\cbengine.exe 做為處理程序</span><span class="sxs-lookup"><span data-stu-id="ea5f8-157">C:\Program Files\Microsoft Azure Recovery Services Agent\bin\cbengine.exe as a process</span></span>
* <span data-ttu-id="ea5f8-158">C:\Program Files\Microsoft Azure Recovery Services Agent\ 資料夾</span><span class="sxs-lookup"><span data-stu-id="ea5f8-158">C:\Program Files\Microsoft Azure Recovery Services Agent\ folders</span></span>
* <span data-ttu-id="ea5f8-159">暫存位置 (如果您不是使用標準位置)</span><span class="sxs-lookup"><span data-stu-id="ea5f8-159">Scratch location (if you're not using the standard location)</span></span>

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a><span data-ttu-id="ea5f8-160">原因：Azure 虛擬機器上執行的備份代理程式</span><span class="sxs-lookup"><span data-stu-id="ea5f8-160">Cause: Backup agent running on an Azure virtual machine</span></span>
<span data-ttu-id="ea5f8-161">如果您在 VM 上執行備份代理程式，其效能會比在實體機器上執行來得慢。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-161">If you're running the Backup agent on a VM, performance will be slower than when you run it on a physical machine.</span></span> <span data-ttu-id="ea5f8-162">這是預期行為，因為有 IOPS 限制。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-162">This is expected due to IOPS limitations.</span></span>  <span data-ttu-id="ea5f8-163">不過，您可以藉由將正在備份的資料磁碟機切換到 Azure 進階儲存體來獲得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-163">However, you can optimize the performance by switching the data drives that are being backed up to Azure Premium Storage.</span></span> <span data-ttu-id="ea5f8-164">我們正在努力修正此問題，未來的版本將會有這方面的修正。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-164">We're working on fixing this issue, and the fix will be available in a future release.</span></span>

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a><span data-ttu-id="ea5f8-165">原因：備份大量的 (數百萬計) 檔案</span><span class="sxs-lookup"><span data-stu-id="ea5f8-165">Cause: Backing up a large number (millions) of files</span></span>
<span data-ttu-id="ea5f8-166">移動大量資料所花費的時間會比移動較少量資料更久。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-166">Moving a large volume of data will take longer than moving a smaller volume of data.</span></span> <span data-ttu-id="ea5f8-167">在某些情況下，備份時間不僅與資料大小有關，也與檔案或資料夾的數目有關。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-167">In some cases, backup time is related to not only the size of the data, but also the number of files or folders.</span></span> <span data-ttu-id="ea5f8-168">尤其是在備份數百萬計的小檔案 (幾位元組到幾千位元組) 時，更是如此。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-168">This is especially true when millions of small files (a few bytes to a few kilobytes) are being backed up.</span></span>

<span data-ttu-id="ea5f8-169">發生這個行為的原因是因為當您備份資料並將資料移動至 Azure 的時候，Azure 會同時分類您的檔案。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-169">This behavior occurs because while you're backing up the data and moving it to Azure, Azure is simultaneously cataloging your files.</span></span> <span data-ttu-id="ea5f8-170">在某些罕見的案例中，目錄作業花費的時間可能比預期時間更長。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-170">In some rare scenarios, the catalog operation might take longer than expected.</span></span>

<span data-ttu-id="ea5f8-171">下列指標可協助您了解瓶頸並據以處理下一個步驟︰</span><span class="sxs-lookup"><span data-stu-id="ea5f8-171">The following indicators can help you understand the bottleneck and accordingly work on the next steps:</span></span>

* <span data-ttu-id="ea5f8-172">**UI 正在顯示資料傳輸的進度**。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-172">**UI is showing progress for the data transfer**.</span></span> <span data-ttu-id="ea5f8-173">資料仍在傳輸中。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-173">The data is still being transferred.</span></span> <span data-ttu-id="ea5f8-174">網路頻寬或資料大小可能會造成延遲。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-174">The network bandwidth or the size of data might be causing delays.</span></span>
* <span data-ttu-id="ea5f8-175">**UI 未顯示資料傳輸的進度**。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-175">**UI is not showing progress for the data transfer**.</span></span> <span data-ttu-id="ea5f8-176">開啟位於 C:\Microsoft Azure Recovery Services Agent\Temp 的記錄檔，並查看記錄檔中的 FileProvider::EndData 項目。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-176">Open the logs located at C:\Microsoft Azure Recovery Services Agent\Temp, and then check for the FileProvider::EndData entry in the logs.</span></span> <span data-ttu-id="ea5f8-177">此項目表示資料傳輸完成，且目錄作業正在進行中。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-177">This entry signifies that the data transfer finished and the catalog operation is happening.</span></span> <span data-ttu-id="ea5f8-178">請勿取消備份工作。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-178">Don't cancel the backup jobs.</span></span> <span data-ttu-id="ea5f8-179">請稍微多等待一些時間讓目錄作業完成。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-179">Instead, wait a little longer for the catalog operation to finish.</span></span> <span data-ttu-id="ea5f8-180">若問題持續發生，請連絡 [Azure 支援](https://portal.azure.com/#create/Microsoft.Support)。</span><span class="sxs-lookup"><span data-stu-id="ea5f8-180">If the problem persists, contact [Azure support](https://portal.azure.com/#create/Microsoft.Support).</span></span>
