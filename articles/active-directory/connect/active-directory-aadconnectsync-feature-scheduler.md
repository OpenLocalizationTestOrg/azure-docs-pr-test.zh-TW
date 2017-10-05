---
title: "Azure AD Connect 同步：排程器 | Microsoft Docs"
description: "本主題說明 Azure AD Connect 同步處理中內建的排程器功能。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 63f69756b3933fecdec75cc677e1098447e5b94e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a><span data-ttu-id="e43ce-103">Azure AD Connect 同步處理：排程器</span><span class="sxs-lookup"><span data-stu-id="e43ce-103">Azure AD Connect sync: Scheduler</span></span>
<span data-ttu-id="e43ce-104">本主題說明 Azure AD Connect 同步處理 (又稱為</span><span class="sxs-lookup"><span data-stu-id="e43ce-104">This topic describes the built-in scheduler in Azure AD Connect sync (a.k.a.</span></span> <span data-ttu-id="e43ce-105">同步處理引擎) 中內建的排程器。</span><span class="sxs-lookup"><span data-stu-id="e43ce-105">sync engine).</span></span>

<span data-ttu-id="e43ce-106">此功能是隨組建 1.1.105.0 (於 2016 年 2 月發行) 一起導入。</span><span class="sxs-lookup"><span data-stu-id="e43ce-106">This feature was introduced with build 1.1.105.0 (released February 2016).</span></span>

## <a name="overview"></a><span data-ttu-id="e43ce-107">概觀</span><span class="sxs-lookup"><span data-stu-id="e43ce-107">Overview</span></span>
<span data-ttu-id="e43ce-108">Azure AD Connect 同步處理會使用排程器來同步處理您內部部署目錄中發生的變更。</span><span class="sxs-lookup"><span data-stu-id="e43ce-108">Azure AD Connect sync synchronize changes occurring in your on-premises directory using a scheduler.</span></span> <span data-ttu-id="e43ce-109">有兩個排程器程序，一個用於密碼同步處理，另一個用於物件/屬性同步處理以及維護工作。</span><span class="sxs-lookup"><span data-stu-id="e43ce-109">There are two scheduler processes, one for password sync and another for object/attribute sync and maintenance tasks.</span></span> <span data-ttu-id="e43ce-110">本主題包含後者。</span><span class="sxs-lookup"><span data-stu-id="e43ce-110">This topic covers the latter.</span></span>

<span data-ttu-id="e43ce-111">在舊版中，物件和屬性的排程器是在同步處理引擎的外部。</span><span class="sxs-lookup"><span data-stu-id="e43ce-111">In earlier releases, the scheduler for objects and attributes was external to the sync engine.</span></span> <span data-ttu-id="e43ce-112">它使用 Windows 工作排程器或個別的 Windows 服務來觸發同步處理程序。</span><span class="sxs-lookup"><span data-stu-id="e43ce-112">It used Windows task scheduler or a separate Windows service to trigger the synchronization process.</span></span> <span data-ttu-id="e43ce-113">排程器已隨 1.1 版內建於同步處理引擎中，並且允許進行一些自訂。</span><span class="sxs-lookup"><span data-stu-id="e43ce-113">The scheduler is with the 1.1 releases built-in to the sync engine and do allow some customization.</span></span> <span data-ttu-id="e43ce-114">新的預設同步處理頻率為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="e43ce-114">The new default synchronization frequency is 30 minutes.</span></span>

<span data-ttu-id="e43ce-115">排程器負責兩項工作：</span><span class="sxs-lookup"><span data-stu-id="e43ce-115">The scheduler is responsible for two tasks:</span></span>

* <span data-ttu-id="e43ce-116">**同步處理循環**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-116">**Synchronization cycle**.</span></span> <span data-ttu-id="e43ce-117">將變更匯入、同步處理及匯出的程序。</span><span class="sxs-lookup"><span data-stu-id="e43ce-117">The process to import, sync, and export changes.</span></span>
* <span data-ttu-id="e43ce-118">**維護工作**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-118">**Maintenance tasks**.</span></span> <span data-ttu-id="e43ce-119">為密碼重設和「裝置註冊服務」(DRS) 更新金鑰和憑證。</span><span class="sxs-lookup"><span data-stu-id="e43ce-119">Renew keys and certificates for Password reset and Device Registration Service (DRS).</span></span> <span data-ttu-id="e43ce-120">清除作業記錄檔中的舊項目。</span><span class="sxs-lookup"><span data-stu-id="e43ce-120">Purge old entries in the operations log.</span></span>

<span data-ttu-id="e43ce-121">排程器本身永遠處於執行狀態，但是您可以將它設定為只執行這些工作其中之一或完全不執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="e43ce-121">The scheduler itself is always running, but it can be configured to only run one or none of these tasks.</span></span> <span data-ttu-id="e43ce-122">例如，如果您需要使用自己的同步處理循環程序，您可以將此工作在排程器中停用，但仍執行維護工作。</span><span class="sxs-lookup"><span data-stu-id="e43ce-122">For example, if you need to have your own synchronization cycle process, you can disable this task in the scheduler but still run the maintenance task.</span></span>

## <a name="scheduler-configuration"></a><span data-ttu-id="e43ce-123">排程器組態</span><span class="sxs-lookup"><span data-stu-id="e43ce-123">Scheduler configuration</span></span>
<span data-ttu-id="e43ce-124">若要查看目前的組態設定，請移至 PowerShell 並執行 `Get-ADSyncScheduler`。</span><span class="sxs-lookup"><span data-stu-id="e43ce-124">To see your current configuration settings, go to PowerShell and run `Get-ADSyncScheduler`.</span></span> <span data-ttu-id="e43ce-125">它會向您顯示類似以下圖片︰</span><span class="sxs-lookup"><span data-stu-id="e43ce-125">It shows you something like this picture:</span></span>

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

<span data-ttu-id="e43ce-127">如果您在執行這個 Cmdlet 時看到 **無法使用同步命令或 Cmdlet** ，則表示 PowerShell 模組並未載入。</span><span class="sxs-lookup"><span data-stu-id="e43ce-127">If you see **The sync command or cmdlet is not available** when you run this cmdlet, then the PowerShell module is not loaded.</span></span> <span data-ttu-id="e43ce-128">如果您在網域控制站或 PowerShell 限制層級高於預設設定的伺服器上執行 Azure AD Connect，即會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="e43ce-128">This problem could happen if you run Azure AD Connect on a domain controller or on a server with higher PowerShell restriction levels than the default settings.</span></span> <span data-ttu-id="e43ce-129">如果您看到此錯誤，則請執行 `Import-Module ADSync` ，以使 Cmdlet 可供使用。</span><span class="sxs-lookup"><span data-stu-id="e43ce-129">If you see this error, then run `Import-Module ADSync` to make the cmdlet available.</span></span>

* <span data-ttu-id="e43ce-130">**AllowedSyncCycleInterval**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-130">**AllowedSyncCycleInterval**.</span></span> <span data-ttu-id="e43ce-131">Azure AD 所允許的同步處理週期最短時間間隔。</span><span class="sxs-lookup"><span data-stu-id="e43ce-131">The shortest time interval between synchronization cycles allowed by Azure AD.</span></span> <span data-ttu-id="e43ce-132">同步處理頻率一旦超過此設定，即不受支援。</span><span class="sxs-lookup"><span data-stu-id="e43ce-132">You cannot synchronize more frequently than this setting and still be supported.</span></span>
* <span data-ttu-id="e43ce-133">**CurrentlyEffectiveSyncCycleInterval**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-133">**CurrentlyEffectiveSyncCycleInterval**.</span></span> <span data-ttu-id="e43ce-134">目前作用中的排程。</span><span class="sxs-lookup"><span data-stu-id="e43ce-134">The schedule currently in effect.</span></span> <span data-ttu-id="e43ce-135">如果頻率未高於 AllowedSyncInterval，其值就會與 CustomizedSyncInterval (如果已設定) 相同。</span><span class="sxs-lookup"><span data-stu-id="e43ce-135">It has the same value as CustomizedSyncInterval (if set) if it is not more frequent than AllowedSyncInterval.</span></span> <span data-ttu-id="e43ce-136">如果您使用 1.1.281 之前的組件且變更 CustomizedSyncCycleInterval，將會在下一個同步處理循環後才生效。</span><span class="sxs-lookup"><span data-stu-id="e43ce-136">If you use a build before 1.1.281 and you change CustomizedSyncCycleInterval, this change takes effect after next synchronization cycle.</span></span> <span data-ttu-id="e43ce-137">從組建 1.1.281 起，變更立即生效。</span><span class="sxs-lookup"><span data-stu-id="e43ce-137">From build 1.1.281 the change takes effect immediately.</span></span>
* <span data-ttu-id="e43ce-138">**CustomizedSyncCycleInterval**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-138">**CustomizedSyncCycleInterval**.</span></span> <span data-ttu-id="e43ce-139">如果您想要讓排程器以預設值 30 分鐘以外的任何其他頻率執行，那麼您要設定此設定。</span><span class="sxs-lookup"><span data-stu-id="e43ce-139">If you want the scheduler to run at any other frequency than the default 30 minutes, then you configure this setting.</span></span> <span data-ttu-id="e43ce-140">在上圖中，已將排程器改為設定成每小時執行一次。</span><span class="sxs-lookup"><span data-stu-id="e43ce-140">In the picture above, the scheduler has been set to run every hour instead.</span></span> <span data-ttu-id="e43ce-141">如果您將此設定設定成低於 AllowedSyncInterval 的值，則會使用後者。</span><span class="sxs-lookup"><span data-stu-id="e43ce-141">If you set this setting to a value lower than AllowedSyncInterval, then the latter is used.</span></span>
* <span data-ttu-id="e43ce-142">**NextSyncCyclePolicyType**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-142">**NextSyncCyclePolicyType**.</span></span> <span data-ttu-id="e43ce-143">Delta (差異) 或 Initial (初始)。</span><span class="sxs-lookup"><span data-stu-id="e43ce-143">Either Delta or Initial.</span></span> <span data-ttu-id="e43ce-144">定義下一次執行應該只處理差異變更，還是應該進行完整匯入並同步處理。</span><span class="sxs-lookup"><span data-stu-id="e43ce-144">Defines if the next run should only process delta changes, or if the next run should do a full import and sync.</span></span> <span data-ttu-id="e43ce-145">後者會一併重新處理任何新的或已變更的規則。</span><span class="sxs-lookup"><span data-stu-id="e43ce-145">The latter would also reprocess any new or changed rules.</span></span>
* <span data-ttu-id="e43ce-146">**NextSyncCycleStartTimeInUTC**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-146">**NextSyncCycleStartTimeInUTC**.</span></span> <span data-ttu-id="e43ce-147">排程器下一次啟動下一個同步處理循環的時間。</span><span class="sxs-lookup"><span data-stu-id="e43ce-147">Next time the scheduler starts the next sync cycle.</span></span>
* <span data-ttu-id="e43ce-148">**PurgeRunHistoryInterval**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-148">**PurgeRunHistoryInterval**.</span></span> <span data-ttu-id="e43ce-149">應該保留作業記錄的時間。</span><span class="sxs-lookup"><span data-stu-id="e43ce-149">The time operation logs should be kept.</span></span> <span data-ttu-id="e43ce-150">您可以在同步處理服務管理員中檢閱這些記錄。</span><span class="sxs-lookup"><span data-stu-id="e43ce-150">These logs can be reviewed in the synchronization service manager.</span></span> <span data-ttu-id="e43ce-151">這些記錄預設會保留 7 天。</span><span class="sxs-lookup"><span data-stu-id="e43ce-151">The default is to keep these logs for 7 days.</span></span>
* <span data-ttu-id="e43ce-152">**SyncCycleEnabled**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-152">**SyncCycleEnabled**.</span></span> <span data-ttu-id="e43ce-153">指出排程器是否要在其作業中一併執行匯入、同步處理及匯出程序。</span><span class="sxs-lookup"><span data-stu-id="e43ce-153">Indicates if the scheduler is running the import, sync, and export processes as part of its operation.</span></span>
* <span data-ttu-id="e43ce-154">**MaintenanceEnabled**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-154">**MaintenanceEnabled**.</span></span> <span data-ttu-id="e43ce-155">顯示是否已啟用維護程序。</span><span class="sxs-lookup"><span data-stu-id="e43ce-155">Shows if the maintenance process is enabled.</span></span> <span data-ttu-id="e43ce-156">它會更新憑證/金鑰，並清除作業記錄。</span><span class="sxs-lookup"><span data-stu-id="e43ce-156">It updates the certificates/keys and purges the operations log.</span></span>
* <span data-ttu-id="e43ce-157">**StagingModeEnabled**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-157">**StagingModeEnabled**.</span></span> <span data-ttu-id="e43ce-158">顯示是否已啟用 [預備模式](active-directory-aadconnectsync-operations.md#staging-mode) 。</span><span class="sxs-lookup"><span data-stu-id="e43ce-158">Shows if [staging mode](active-directory-aadconnectsync-operations.md#staging-mode) is enabled.</span></span> <span data-ttu-id="e43ce-159">如果已啟用此設定，則它會停用執行匯出，但仍執行匯入和同步處理。</span><span class="sxs-lookup"><span data-stu-id="e43ce-159">If this setting is enabled, then it suppresses the exports from running but still run import and synchronization.</span></span>
* <span data-ttu-id="e43ce-160">**SchedulerSuspended**。</span><span class="sxs-lookup"><span data-stu-id="e43ce-160">**SchedulerSuspended**.</span></span> <span data-ttu-id="e43ce-161">由 Connect 在升級時設定，用來防止排程器執行。</span><span class="sxs-lookup"><span data-stu-id="e43ce-161">Set by Connect during an upgrade to temporarily block the scheduler from running.</span></span>

<span data-ttu-id="e43ce-162">您可以使用 `Set-ADSyncScheduler`變更這些設定的其中一部分。</span><span class="sxs-lookup"><span data-stu-id="e43ce-162">You can change some of these settings with `Set-ADSyncScheduler`.</span></span> <span data-ttu-id="e43ce-163">您可以修改下列參數：</span><span class="sxs-lookup"><span data-stu-id="e43ce-163">The following parameters can be modified:</span></span>

* <span data-ttu-id="e43ce-164">CustomizedSyncCycleInterval</span><span class="sxs-lookup"><span data-stu-id="e43ce-164">CustomizedSyncCycleInterval</span></span>
* <span data-ttu-id="e43ce-165">NextSyncCyclePolicyType</span><span class="sxs-lookup"><span data-stu-id="e43ce-165">NextSyncCyclePolicyType</span></span>
* <span data-ttu-id="e43ce-166">PurgeRunHistoryInterval</span><span class="sxs-lookup"><span data-stu-id="e43ce-166">PurgeRunHistoryInterval</span></span>
* <span data-ttu-id="e43ce-167">SyncCycleEnabled</span><span class="sxs-lookup"><span data-stu-id="e43ce-167">SyncCycleEnabled</span></span>
* <span data-ttu-id="e43ce-168">MaintenanceEnabled</span><span class="sxs-lookup"><span data-stu-id="e43ce-168">MaintenanceEnabled</span></span>

<span data-ttu-id="e43ce-169">在先前的 Azure AD Connect 組建中，**isStagingModeEnabled** 已在 Set-ADSyncScheduler 中公開。</span><span class="sxs-lookup"><span data-stu-id="e43ce-169">In earlier builds of Azure AD Connect, **isStagingModeEnabled** was exposed in Set-ADSyncScheduler.</span></span> <span data-ttu-id="e43ce-170">**不支援**設定此屬性。</span><span class="sxs-lookup"><span data-stu-id="e43ce-170">It is **unsupported** to set this property.</span></span> <span data-ttu-id="e43ce-171">**SchedulerSuspended** 屬性應該僅供 Connect 修改。</span><span class="sxs-lookup"><span data-stu-id="e43ce-171">The property **SchedulerSuspended** should only be modified by Connect.</span></span> <span data-ttu-id="e43ce-172">**不支援**直接使用 PowerShell 來修改此屬性。</span><span class="sxs-lookup"><span data-stu-id="e43ce-172">It is **unsupported** to set this with PowerShell directly.</span></span>

<span data-ttu-id="e43ce-173">排程器組態儲存在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="e43ce-173">The scheduler configuration is stored in Azure AD.</span></span> <span data-ttu-id="e43ce-174">如果您有預備伺服器，主要伺服器上的任何變更也會影響預備伺服器 (IsStagingModeEnabled 除外)。</span><span class="sxs-lookup"><span data-stu-id="e43ce-174">If you have a staging server, any change on the primary server also affects the staging server (except IsStagingModeEnabled).</span></span>

### <a name="customizedsynccycleinterval"></a><span data-ttu-id="e43ce-175">CustomizedSyncCycleInterval</span><span class="sxs-lookup"><span data-stu-id="e43ce-175">CustomizedSyncCycleInterval</span></span>
<span data-ttu-id="e43ce-176">語法： `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`</span><span class="sxs-lookup"><span data-stu-id="e43ce-176">Syntax: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`</span></span>  
<span data-ttu-id="e43ce-177">d - 天、HH - 小時、mm - 分鐘、ss - 秒</span><span class="sxs-lookup"><span data-stu-id="e43ce-177">d - days, HH - hours, mm - minutes, ss - seconds</span></span>

<span data-ttu-id="e43ce-178">範例： `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`</span><span class="sxs-lookup"><span data-stu-id="e43ce-178">Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`</span></span>  
<span data-ttu-id="e43ce-179">將排程器變更為每隔 3 小時執行一次。</span><span class="sxs-lookup"><span data-stu-id="e43ce-179">Changes the scheduler to run every 3 hours.</span></span>

<span data-ttu-id="e43ce-180">範例： `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`</span><span class="sxs-lookup"><span data-stu-id="e43ce-180">Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`</span></span>  
<span data-ttu-id="e43ce-181">將排程器變更為每天執行。</span><span class="sxs-lookup"><span data-stu-id="e43ce-181">Changes change the scheduler to run daily.</span></span>

### <a name="disable-the-scheduler"></a><span data-ttu-id="e43ce-182">停用排程器</span><span class="sxs-lookup"><span data-stu-id="e43ce-182">Disable the scheduler</span></span>  
<span data-ttu-id="e43ce-183">如果您需要變更組態，那麼您需要停用排程器。</span><span class="sxs-lookup"><span data-stu-id="e43ce-183">If you need to make configuration changes, then you want to disable the scheduler.</span></span> <span data-ttu-id="e43ce-184">例如，當您[設定篩選](active-directory-aadconnectsync-configure-filtering.md)或[變更同步處理規則](active-directory-aadconnectsync-change-the-configuration.md)時。</span><span class="sxs-lookup"><span data-stu-id="e43ce-184">For example, when you [configure filtering](active-directory-aadconnectsync-configure-filtering.md) or [make changes to synchronization rules](active-directory-aadconnectsync-change-the-configuration.md).</span></span>

<span data-ttu-id="e43ce-185">若要停用排程器，請執行 `Set-ADSyncScheduler -SyncCycleEnabled $false`。</span><span class="sxs-lookup"><span data-stu-id="e43ce-185">To disable the scheduler, run `Set-ADSyncScheduler -SyncCycleEnabled $false`.</span></span>

![停用排程器](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

<span data-ttu-id="e43ce-187">當您完成變更之後，不要忘記使用 `Set-ADSyncScheduler -SyncCycleEnabled $true` 再次啟用排程器。</span><span class="sxs-lookup"><span data-stu-id="e43ce-187">When you've made your changes, do not forget to enable the scheduler again with `Set-ADSyncScheduler -SyncCycleEnabled $true`.</span></span>

## <a name="start-the-scheduler"></a><span data-ttu-id="e43ce-188">啟動排程器</span><span class="sxs-lookup"><span data-stu-id="e43ce-188">Start the scheduler</span></span>
<span data-ttu-id="e43ce-189">排程器預設為每隔 30 分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="e43ce-189">The scheduler is by default run every 30 minutes.</span></span> <span data-ttu-id="e43ce-190">在某些情況下，您可能會想要在排定的循環之間執行同步處理循環，或是需要執行不同類型的同步處理循環。</span><span class="sxs-lookup"><span data-stu-id="e43ce-190">In some cases, you might want to run a sync cycle in between the scheduled cycles or you need to run a different type.</span></span>

<span data-ttu-id="e43ce-191">**差異同步處理循環**</span><span class="sxs-lookup"><span data-stu-id="e43ce-191">**Delta sync cycle**</span></span>  
<span data-ttu-id="e43ce-192">：差異同步處理循環包含下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e43ce-192">A delta sync cycle includes the following steps:</span></span>

* <span data-ttu-id="e43ce-193">在所有的連接器上執行差異匯入</span><span class="sxs-lookup"><span data-stu-id="e43ce-193">Delta import on all Connectors</span></span>
* <span data-ttu-id="e43ce-194">在所有的連接器上執行差異同步處理</span><span class="sxs-lookup"><span data-stu-id="e43ce-194">Delta sync on all Connectors</span></span>
* <span data-ttu-id="e43ce-195">在所有的連接器上執行匯出</span><span class="sxs-lookup"><span data-stu-id="e43ce-195">Export on all Connectors</span></span>

<span data-ttu-id="e43ce-196">您可能因為有一個必須立即同步處理的緊急變更，而需要手動執行循環。</span><span class="sxs-lookup"><span data-stu-id="e43ce-196">It could be that you have an urgent change that must be synchronized immediately, which is why you need to manually run a cycle.</span></span> <span data-ttu-id="e43ce-197">如果您需要手動執行循環，則請從 PowerShell 執行 `Start-ADSyncSyncCycle -PolicyType Delta`。</span><span class="sxs-lookup"><span data-stu-id="e43ce-197">If you need to manually run a cycle, then from PowerShell run `Start-ADSyncSyncCycle -PolicyType Delta`.</span></span>

<span data-ttu-id="e43ce-198">**完整同步處理循環**</span><span class="sxs-lookup"><span data-stu-id="e43ce-198">**Full sync cycle**</span></span>  
<span data-ttu-id="e43ce-199">如果您已進行下列其中一項組態變更，就需要執行完整同步處理循環 (也稱為</span><span class="sxs-lookup"><span data-stu-id="e43ce-199">If you have made one of the following configuration changes, you need to run a full sync cycle (a.k.a.</span></span> <span data-ttu-id="e43ce-200">Initial (初始))：</span><span class="sxs-lookup"><span data-stu-id="e43ce-200">Initial):</span></span>

* <span data-ttu-id="e43ce-201">新增更多要從來源目錄匯入的物件或屬性</span><span class="sxs-lookup"><span data-stu-id="e43ce-201">Added more objects or attributes to be imported from a source directory</span></span>
* <span data-ttu-id="e43ce-202">對同步處理規則進行變更</span><span class="sxs-lookup"><span data-stu-id="e43ce-202">Made changes to the Synchronization rules</span></span>
* <span data-ttu-id="e43ce-203">變更 [篩選](active-directory-aadconnectsync-configure-filtering.md) 以納入不同數目的物件</span><span class="sxs-lookup"><span data-stu-id="e43ce-203">Changed [filtering](active-directory-aadconnectsync-configure-filtering.md) so a different number of objects should be included</span></span>

<span data-ttu-id="e43ce-204">如果您已進行上述其中一項變更，您就需要執行完整同步處理循環，以便讓同步處理引擎有機會重新合併連接器空間。</span><span class="sxs-lookup"><span data-stu-id="e43ce-204">If you have made one of these changes, then you need to run a full sync cycle so the sync engine has the opportunity to reconsolidate the connector spaces.</span></span> <span data-ttu-id="e43ce-205">完整同步處理循環包含下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e43ce-205">A full sync cycle includes the following steps:</span></span>

* <span data-ttu-id="e43ce-206">在所有的連接器上執行完整匯入</span><span class="sxs-lookup"><span data-stu-id="e43ce-206">Full Import on all Connectors</span></span>
* <span data-ttu-id="e43ce-207">在所有的連接器上執行完整同步處理</span><span class="sxs-lookup"><span data-stu-id="e43ce-207">Full Sync on all Connectors</span></span>
* <span data-ttu-id="e43ce-208">在所有的連接器上執行匯出</span><span class="sxs-lookup"><span data-stu-id="e43ce-208">Export on all Connectors</span></span>

<span data-ttu-id="e43ce-209">若要起始完整同步處理循環，請從 PowerShell 提示字元執行 `Start-ADSyncSyncCycle -PolicyType Initial` 。</span><span class="sxs-lookup"><span data-stu-id="e43ce-209">To initiate a full sync cycle, run `Start-ADSyncSyncCycle -PolicyType Initial` from a PowerShell prompt.</span></span> <span data-ttu-id="e43ce-210">此命令會啟動完整同步處理循環。</span><span class="sxs-lookup"><span data-stu-id="e43ce-210">This command starts a full sync cycle.</span></span>

## <a name="stop-the-scheduler"></a><span data-ttu-id="e43ce-211">停止排程器</span><span class="sxs-lookup"><span data-stu-id="e43ce-211">Stop the scheduler</span></span>
<span data-ttu-id="e43ce-212">如果排程器目前正在執行同步處理循環，您可能必須將它停止。</span><span class="sxs-lookup"><span data-stu-id="e43ce-212">If the scheduler is currently running a synchronization cycle, you might need to stop it.</span></span> <span data-ttu-id="e43ce-213">例如，如果您啟動安裝精靈並收到以下錯誤：</span><span class="sxs-lookup"><span data-stu-id="e43ce-213">For example if you start the installation wizard and you get this error:</span></span>

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

<span data-ttu-id="e43ce-215">當同步處理循環正在執行時，您會無法進行組態變更。</span><span class="sxs-lookup"><span data-stu-id="e43ce-215">When a sync cycle is running, you cannot make configuration changes.</span></span> <span data-ttu-id="e43ce-216">您可以等到排程器完成程序，也可以停止它，以便立即進行變更。</span><span class="sxs-lookup"><span data-stu-id="e43ce-216">You could wait until the scheduler has finished the process, but you can also stop it so you can make your changes immediately.</span></span> <span data-ttu-id="e43ce-217">停止目前的循環並無任何損害，而且擱置的變更會在下一次執行時處理。</span><span class="sxs-lookup"><span data-stu-id="e43ce-217">Stopping the current cycle is not harmful and pending changes are processed with next run.</span></span>

1. <span data-ttu-id="e43ce-218">首先，使用 PowerShell Cmdlet `Stop-ADSyncSyncCycle`來通知排程器停止其目前的循環。</span><span class="sxs-lookup"><span data-stu-id="e43ce-218">Start by telling the scheduler to stop its current cycle with the PowerShell cmdlet `Stop-ADSyncSyncCycle`.</span></span>
2. <span data-ttu-id="e43ce-219">如果您使用 1.1.281 之前的組件，停止排程器並不會阻止目前的連接器進行其目前的工作。</span><span class="sxs-lookup"><span data-stu-id="e43ce-219">If you use a build before 1.1.281, then stopping the scheduler does not stop the current Connector from its current task.</span></span> <span data-ttu-id="e43ce-220">若要強制停止連接器，請採取下列動作：![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)</span><span class="sxs-lookup"><span data-stu-id="e43ce-220">To force the Connector to stop, take the following actions: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)</span></span>
   * <span data-ttu-id="e43ce-221">從 [開始] 功能表啟動 [同步處理服務]  。</span><span class="sxs-lookup"><span data-stu-id="e43ce-221">Start **Synchronization Service** from the start menu.</span></span> <span data-ttu-id="e43ce-222">移至 [連接器]，反白選取狀態為 [正在執行] 的連接器，然後從 [動作] 中選取 [停止]。</span><span class="sxs-lookup"><span data-stu-id="e43ce-222">Go to **Connectors**, highlight the Connector with the state **Running**, and select **Stop** from the Actions.</span></span>

<span data-ttu-id="e43ce-223">排程器仍在作用中，並且會在下次有機會時重新啟動。</span><span class="sxs-lookup"><span data-stu-id="e43ce-223">The scheduler is still active and starts again on next opportunity.</span></span>

## <a name="custom-scheduler"></a><span data-ttu-id="e43ce-224">自訂排程器</span><span class="sxs-lookup"><span data-stu-id="e43ce-224">Custom scheduler</span></span>
<span data-ttu-id="e43ce-225">本節記載的 Cmdlet 只有在組建 [1.1.130.0](active-directory-aadconnect-version-history.md#111300) 和更新版本中才有提供。</span><span class="sxs-lookup"><span data-stu-id="e43ce-225">The cmdlets documented in this section are only available in build [1.1.130.0](active-directory-aadconnect-version-history.md#111300) and later.</span></span>

<span data-ttu-id="e43ce-226">如果內建的排程器無法滿足您的需求，您可以使用 PowerShell 來排程連接器。</span><span class="sxs-lookup"><span data-stu-id="e43ce-226">If the built-in scheduler does not satisfy your requirements, then you can schedule the Connectors using PowerShell.</span></span>

### <a name="invoke-adsyncrunprofile"></a><span data-ttu-id="e43ce-227">Invoke-ADSyncRunProfile</span><span class="sxs-lookup"><span data-stu-id="e43ce-227">Invoke-ADSyncRunProfile</span></span>
<span data-ttu-id="e43ce-228">您可使用下列方式，啟動連接器的設定檔：</span><span class="sxs-lookup"><span data-stu-id="e43ce-228">You can start a profile for a Connector in this way:</span></span>

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

<span data-ttu-id="e43ce-229">您可以在 [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md) 中找到可用來做為[連接器名稱](active-directory-aadconnectsync-service-manager-ui-connectors.md)和[執行設定檔名稱](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles)的名稱。</span><span class="sxs-lookup"><span data-stu-id="e43ce-229">The names to use for [Connector names](active-directory-aadconnectsync-service-manager-ui-connectors.md) and [Run Profile Names](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) can be found in the [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

![叫用執行設定檔](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

<span data-ttu-id="e43ce-231">`Invoke-ADSyncRunProfile` Cmdlet 是同步的，亦即只有當連接器完成作業 (不論成功或發生錯誤) 時，它才會交回控制權。</span><span class="sxs-lookup"><span data-stu-id="e43ce-231">The `Invoke-ADSyncRunProfile` cmdlet is synchronous, that is, it does not return control until the Connector has completed the operation, either successfully or with an error.</span></span>

<span data-ttu-id="e43ce-232">排程連接器時，建議您遵循下列順序進行排程︰</span><span class="sxs-lookup"><span data-stu-id="e43ce-232">When you schedule your Connectors, the recommendation is to schedule them in the following order:</span></span>

1. <span data-ttu-id="e43ce-233">(完整/差異) 從內部部署目錄匯入，例如 Active Directory</span><span class="sxs-lookup"><span data-stu-id="e43ce-233">(Full/Delta) Import from on-premises directories, such as Active Directory</span></span>
2. <span data-ttu-id="e43ce-234">(完整/差異) 從 Azure AD 匯入</span><span class="sxs-lookup"><span data-stu-id="e43ce-234">(Full/Delta) Import from Azure AD</span></span>
3. <span data-ttu-id="e43ce-235">(完整/差異) 從內部部署目錄同步處理，例如 Active Directory</span><span class="sxs-lookup"><span data-stu-id="e43ce-235">(Full/Delta) Synchronization from on-premises directories, such as Active Directory</span></span>
4. <span data-ttu-id="e43ce-236">(完整/差異) 從 Azure AD 同步處理</span><span class="sxs-lookup"><span data-stu-id="e43ce-236">(Full/Delta) Synchronization from Azure AD</span></span>
5. <span data-ttu-id="e43ce-237">匯出至 Azure AD</span><span class="sxs-lookup"><span data-stu-id="e43ce-237">Export to Azure AD</span></span>
6. <span data-ttu-id="e43ce-238">匯出至內部部署目錄，例如 Active Directory</span><span class="sxs-lookup"><span data-stu-id="e43ce-238">Export to on-premises directories, such as Active Directory</span></span>

<span data-ttu-id="e43ce-239">此順序是內建的排程器執行連接器的方式。</span><span class="sxs-lookup"><span data-stu-id="e43ce-239">This order is how the built-in scheduler runs the Connectors.</span></span>

### <a name="get-adsyncconnectorrunstatus"></a><span data-ttu-id="e43ce-240">Get-ADSyncConnectorRunStatus</span><span class="sxs-lookup"><span data-stu-id="e43ce-240">Get-ADSyncConnectorRunStatus</span></span>
<span data-ttu-id="e43ce-241">您也可以監視同步處理引擎，以查看其為忙碌或閒置。</span><span class="sxs-lookup"><span data-stu-id="e43ce-241">You can also monitor the sync engine to see if it is busy or idle.</span></span> <span data-ttu-id="e43ce-242">如果同步處理引擎處於閒置狀態且沒有執行連接器，這個 Cmdlet 會傳回空的結果。</span><span class="sxs-lookup"><span data-stu-id="e43ce-242">This cmdlet returns an empty result if the sync engine is idle and is not running a Connector.</span></span> <span data-ttu-id="e43ce-243">如果連接器正在執行，它會傳回連接器的名稱。</span><span class="sxs-lookup"><span data-stu-id="e43ce-243">If a Connector is running, it returns the name of the Connector.</span></span>

```
Get-ADSyncConnectorRunStatus
```

![連接器執行狀態](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
<span data-ttu-id="e43ce-245">在上圖中，第一行是來自同步處理引擎處於閒置狀態時。</span><span class="sxs-lookup"><span data-stu-id="e43ce-245">In the picture above, the first line is from a state where the sync engine is idle.</span></span> <span data-ttu-id="e43ce-246">第二行則是從 Azure AD 連接器執行時。</span><span class="sxs-lookup"><span data-stu-id="e43ce-246">The second line from when the Azure AD Connector is running.</span></span>

## <a name="scheduler-and-installation-wizard"></a><span data-ttu-id="e43ce-247">排程器和安裝精靈</span><span class="sxs-lookup"><span data-stu-id="e43ce-247">Scheduler and installation wizard</span></span>
<span data-ttu-id="e43ce-248">如果您啟動安裝精靈，則排程器將會暫時停用。</span><span class="sxs-lookup"><span data-stu-id="e43ce-248">If you start the installation wizard, then the scheduler is temporarily suspended.</span></span> <span data-ttu-id="e43ce-249">此行為是因為系統會假設您進行組態變更，而如果同步處理引擎正在執行中，將會無法套用這些設定。</span><span class="sxs-lookup"><span data-stu-id="e43ce-249">This behavior is because it is assumed you make configuration changes and these settings cannot be applied if the sync engine is actively running.</span></span> <span data-ttu-id="e43ce-250">基於這個理由，請勿讓安裝精靈保持開啟，因為這會阻止同步處理引擎執行任何同步處理動作。</span><span class="sxs-lookup"><span data-stu-id="e43ce-250">For this reason, do not leave the installation wizard open since it stops the sync engine from performing any synchronization actions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e43ce-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e43ce-251">Next steps</span></span>
<span data-ttu-id="e43ce-252">深入了解 [Azure AD Connect 同步](active-directory-aadconnectsync-whatis.md) 組態。</span><span class="sxs-lookup"><span data-stu-id="e43ce-252">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="e43ce-253">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="e43ce-253">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
